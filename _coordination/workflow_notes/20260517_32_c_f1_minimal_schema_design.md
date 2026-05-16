狀態：REVIEW
版本：1.0-candidate
最後更新：2026-05-17
適用範圍：F1 minimal action file schema 設計
優先級：高

# F1 Minimal Action File Schema Design

## 1. Purpose

定義 action file 格式，讓「每次 gate-passed 行為寫成獨立檔 + 新對話 / 新 controller 選擇性讀取必要檔」可以開始運作。

本檔是 F1 minimal phase 主要交付物。

## 2. Boundary

本檔屬 REVIEW，不是 LOCKED。

**包含**：folder 結構、檔名約定、frontmatter schema（21 欄位）、type 枚舉（8 種）、record_status / decision_effect 拆分、selective read 規則、index regen PowerShell 草案、維護紀律。

**不包含**：schema validator 實作、automation、把 current_state.md §11 遷到 actions/、過去事件回填、HARNESS Core 修改、LOCKED 升級。這些都在 F1 minimal scope 之外。

## 3. Folder Structure

```
_coordination/
  actions/
    index.md                            # 自動產生索引
    20260517T200000_a3f7_decision.md    # 動作檔
    ...
```

平面結構；不依 phase 分子目錄。phase 資訊在 frontmatter `phase_ref`。

## 4. Filename Convention

```
<timestamp>_<action_id>_<type>.md
```

| 欄位 | 格式 | 範例 |
| --- | --- | --- |
| timestamp | `YYYYMMDDTHHMMSS` local time | `20260517T200000` |
| action_id | 4 碼 hex；session 內唯一 | `a3f7` |
| type | 8 種閉集枚舉 | `decision` |

完整範例：`20260517T200000_a3f7_decision.md`

規則：

- id 一旦建立**不可變**
- rename = strict gate
- 重複 id = write 前必檢查並 stop-and-ask

## 5. Action Type 閉集（8 種）

| type | 適用 |
| --- | --- |
| `decision` | user / controller 決策 |
| `gate_pass` | gate 通過紀錄（commit / push / file write / phase 啟動） |
| `file_write` | markdown / config 寫入動作 |
| `mistake_disclosure` | §14 揭露 |
| `pushback` | §15 行使 pushback |
| `handoff` | controller 交接（與 F2 整合） |
| `health_check` | 維護健診 |
| `external_input` | user 外部資料貼入（截圖、PowerShell 輸出等） |

擴張 type 枚舉 = strict gate。

## 6. Record Status / Decision Effect 拆分（Codex P2.4）

兩個獨立維度，不合併。

### `record_status`（檔案本身狀態）

```
DRAFT       初稿，尚未被視為 recorded
RECORDED    正式記錄，audit trail 一部分
SUPERSEDED  被另一個 action file 取代（必設 superseded_by）
ARCHIVED    歷史保留，不在 active scope
```

### `decision_effect`（決策效力）

```
proposed         僅提案，尚無 user accept
accepted_by_user user 明文接受
superseded       被另一個 decision 取代
n_a              不適用（type ≠ decision）
```

組合範例：

- `RECORDED + accepted_by_user`：已落地的 user 決策
- `RECORDED + n_a`：已落地的非決策動作（如 mistake_disclosure）
- `DRAFT + proposed`：尚在 standard gate 內的提案
- `SUPERSEDED + superseded`：被新版取代的舊決策

## 7. Frontmatter 完整欄位（21 個）

YAML，包覆於 `---`。

### 7.1 強制必填（10 個）

```yaml
schema_version: 1.0
id: 20260517T200000_a3f7
type: decision
phase_ref: F1-launch
record_status: RECORDED
decision_effect: accepted_by_user
created_at: 2026-05-17T20:00:00+08:00
created_by: Codex-WT 主控室
gate_level: strict                       # light / standard / strict / n_a
non_authority_boundary: "本 action 紀錄 X；evidence-only；不批准 Y / Z"
```

### 7.2 條件必填（6 個）

```yaml
report_back_to: Codex-WT 主控室            # type=handoff 必填
manual_gate_status: approved             # gate_level ≠ n_a 必填
approved_read_scope_ref:                 # 含讀檔動作必填
  - _coordination/current_state.md
input_sources:                           # 同上：實際讀過的 sources
  - _coordination/current_state.md
output_changes:                          # 含寫檔動作必填
  - _coordination/actions/20260517T200000_a3f7_decision.md
tool_provenance:                         # 含工具動作必填
  platform: claude_cowork_sandbox
  tool: Write
  version: n_a
```

### 7.3 可選（5 個）

```yaml
source_freshness:
  _coordination/current_state.md: current
supersedes: null
superseded_by: null
related_actions: []
tags: [F1, phase_launch]
```

## 8. Body Sections（markdown）

frontmatter 之後 body 建議結構（不強制）：

```
# <title>
## Summary
## Context
## Action Taken / Proposed
## Result / Outcome
## Source Limitations
## Stop Conditions
## Boundary
```

## 9. Selective Read 規則

新對話啟動讀檔順序：

**必讀**（startup packet 三本）：

1. `_coordination/current_state.md`
2. `_coordination/project_adapter/writing_tool_project_adapter.md`
3. `_coordination/actions/index.md`

**動態決定**（依任務）：

- user / controller 明文指定 action ids
- 依 tag / type / phase_ref 篩選

**禁止**：

- 全讀 `actions/`（除非明文授權）
- 推測「相關 action」並擴張
- 把 index.md 之外的 action body 當 authority

## 10. Index Regen 設計（G-c PowerShell）

### 10.1 目的

`_coordination/actions/index.md` 自動產生 metadata 索引。

### 10.2 不做（依 Codex P2.5）

- 不驗 schema、不擋寫入、不自動 commit
- 只做：讀 frontmatter → 產 markdown table → 寫 index.md

### 10.3 PowerShell 草案（user-side 跑；Codex 不執行）

```powershell
# regen_actions_index.ps1
param(
    [string]$ActionsDir = "_coordination\actions",
    [string]$IndexFile = "_coordination\actions\index.md"
)

$actionFiles = Get-ChildItem -Path $ActionsDir -Filter "*.md" |
    Where-Object { $_.Name -ne "index.md" } |
    Sort-Object Name

$now = Get-Date -Format "yyyy-MM-ddTHH:mm:sszzz"
$header = @"
狀態：REVIEW（自動產生，不可手改）
最後更新：$now

# Actions Index

| id | type | record_status | decision_effect | phase_ref | created_at | title |
| --- | --- | --- | --- | --- | --- | --- |
"@

$rows = foreach ($file in $actionFiles) {
    $content = Get-Content $file.FullName -Raw -Encoding UTF8
    $fm = @{}
    if ($content -match '(?s)^---\s*\r?\n(.*?)\r?\n---') {
        $matches[1] -split "`r?`n" | ForEach-Object {
            if ($_ -match '^(\w+):\s*(.+)$') {
                $fm[$matches[1].Trim()] = $matches[2].Trim()
            }
        }
    }
    $title = ""
    if ($content -match '(?m)^# (.+)$') { $title = $matches[1].Trim() }
    "| $($fm['id']) | $($fm['type']) | $($fm['record_status']) | $($fm['decision_effect']) | $($fm['phase_ref']) | $($fm['created_at']) | $title |"
}

@($header) + $rows | Out-File -FilePath $IndexFile -Encoding UTF8
Write-Host "Index regenerated: $IndexFile ($($actionFiles.Count) entries)"
```

### 10.4 執行

```powershell
.\regen_actions_index.ps1
```

每次 action file 新增 / 變更後 user-side 手動跑；或 commit 前批次跑。

### 10.5 失效模式

| 失敗模式 | 影響 |
| --- | --- |
| YAML 解析失敗 | 該 row 欄位空；user 看到後手動修 |
| 重複 id | 兩個 row 同 id；user 決定 supersede |
| Missing required field | row 欄位空；validator phase 才擋 |

## 11. 維護紀律

- 每個 gate-passed action **應**產出 action file（漏寫 = 中度失維）
- index 由 script 重生，**不**手寫
- RECORDED action **不可改**內容；修正用 supersede 鏈
- 健診（list DRAFT > 7 天 / supersede 鏈斷裂等）延後到 F2

## 12. Validator / Automation 延後（依 Codex P2.5）

下列項目 F1 minimal **不做**：

- schema validator
- 自動 ingestion / file system hook
- 自動 supersede chain 驗證
- 自動把 current_state.md §11 遷移
- 自動 commit / push hook

F1 minimal 跑一段觀察期後另開 strict gate phase 啟動上述。

## 13. Not Approved

- schema validator 實作 / 部署
- automation 啟動
- §11 Activity Log 遷移
- 過去事件批量回填
- HARNESS Core 修改 / 32A-LOCK 修改
- F1 LOCKED 升級
- F2 / Platform Capability / F3 / F4 啟動
- commit / push

## 14. Stop Conditions

- schema 被當 LOCKED authority
- validator / automation 未經 strict gate 上線
- §11 被自動遷移
- index 手寫
- action file id 被改 / RECORDED 內容被改
- SUPERSEDED action 被當 current authority
- 任何 evidence-as-approval

## 15. Classification

```
F1_MINIMAL_SCHEMA_DESIGN_REVIEW_CANDIDATE
```

## 16. Boundary Confirmation

本檔是 REVIEW F1 minimal schema 設計 only。不是 LOCKED schema、不是 validator / automation 啟動授權、不是 F1 LOCKED 升級、不是 F2 / Platform / F3 / F4 啟動授權、不是 §11 遷移授權、不是 HARNESS Core 修改授權。
