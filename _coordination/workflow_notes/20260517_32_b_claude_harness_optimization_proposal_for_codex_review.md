狀態：REVIEW
版本：1.0-candidate
最後更新：2026-05-17
適用範圍：Phase 32B Claude 提交給 Codex review 的 HARNESS 優化評估與 F1+F2 啟動建議
優先級：中高
撰寫者：Claude（Anthropic, Cowork mode, 本對話內）
讀者：Codex（user 將轉交此檔，由 Codex 審查）

# Phase 32B：HARNESS 優化評估與 F1+F2 啟動建議書（Claude 提交，待 Codex review）

## 0. 提交摘要 / TL;DR

我是 Claude，在本對話中協助 user 完成 writing-tool project 的 HARNESS adoption（Phase 32A-STARTUP）。

第一輪工作已完成：建立 Project Adapter / current_state.md / route_contract / startup_packet 4 個 REVIEW 檔；user 完成首個 commit + remote + push 到 GitHub。

過程中發生 3 次 §14 mistake disclosure。對話歷時長且 token 消耗顯著。

User 已採納我提出的 4 個未來 feature（F1–F4），並決定優先設計 + 啟動 F1（動作文件化 + 選擇性讀取）與 F2（主控室快速繼承），F3 / F4 延後。

本文件目的：把我累積的判斷、現況評估、未完成事項、設計建議一次交給 Codex 審查，由 Codex 對我的判斷進行獨立校核。

本文件 **不** 批准：HARNESS Core 修改、32A-LOCK 修改、LOCKED 升級、F1 / F2 落地實作、Mode B 切換、protected content read、commit / push、Runtime / SDK 啟動。

## 1. 對話 Context（給 Codex 補資訊）

### 1.1 Active routing

| 角色 | 名稱 |
| --- | --- |
| Active Controller | Codex-WT 主控室 |
| Report-back Target | Codex-WT 主控室（本對話 = Claude） |
| Project Mode | Mode A 純治理工具 |
| Branch / Remote | master / `https://github.com/mark75369/writing-tool-project-folder.git` |
| 已 push | commit `58d33a7 claude 重構 HARNESS` |

### 1.2 Files Read（我作為 Claude 完整讀過）

- `harness/core/workflow_harness_core_v1_0_freeze.md`
- `harness/core/workflow_harness_core_v1_0_export_profile.md`
- `harness/core/workflow_harness_new_project_usage_manual.md`
- `harness/core/啟用說明書.md`
- `harness/route_contracts/20260517_32_a_lock_writing_tool_route_contract_decision_note.md`
- `_coordination/project_adapter/writing_tool_project_adapter.md`（我自己建立）
- `_coordination/current_state.md`（我自己建立）
- `harness/route_contracts/writing_tool_route_contract.md`（我自己建立）
- `harness/core/writing_tool_project_startup_packet.md`（我自己建立）

### 1.3 Files Not Read

- `harness/core/workflow_harness_tool_package_index.md`（user 未指定，本對話未讀其 body）
- 任何 protected creative content
- 舊專案 game-dialogue-bible 任何 body
- runtime / SDK / scripts 任何 body
- `_exports/` `tasks/` `templates/` 任何 body
- 外部 reviewer 來源
- internal Codex database

### 1.4 Source Limitations

- 我對 Codex CLI 最新版能力的掌握度有限（我的 knowledge cutoff = 2025-05）；本文件涉及「Codex 能否做 X」之處，**請 Codex 自己校核** capability，必要時修正本文件對應段落
- 我對 HARNESS Phase 1–31 的詳細演進過程僅讀過 Phase 32A 系列檔案，沒讀 Phase 1–31 的 workflow notes
- 我的判斷基礎是本對話內提供的檔案 + 我自己的 reasoning，**不**包含 user 私有 / 商業劇本內容
- 本文件是 advisory 提案，**不**是 authority

## 2. HARNESS 現況評估（Claude 觀點）

### 2.1 做得好的地方

| 項目 | 評估 |
| --- | --- |
| 安全不變式（Core §3） | 嚴謹、明文、不易繞過 |
| Gate 系統（Core §4 / Manual §15） | 清楚區分讀 / 寫 / commit / push / authority 等不同 gate |
| approval vs evidence 區隔（Core §11 §13 §14） | 防止 PASS / READY / VERIFIED 被誤判為 approval，非常有效 |
| Protected source 預設關閉（Core §17–18 / Manual §13） | 對商業創作是必要底線 |
| Core / Adapter 分層（Core §21 / Export Profile §4–5） | 真的可移植到新專案（本專案就是證據） |
| Stop-and-ask（Core §19） | 在邊界不明時觸發停下，這次對話多次觸發都正確 |

### 2.2 我認為的「重心偏移」（**重要，請 Codex 重點 review 此節**）

讀完 5 個檔的整體印象：HARNESS Phase 1–32A 的設計重心高度集中在「防線層」，相對忽略「營運層」。

| 層次 | HARNESS 投資比例（我的估計） | 解釋 |
| --- | --- | --- |
| 防線層 | ~80% | gate 系統、approval boundary、protected source、§14 mistake protocol、§15 pushback、stop-and-ask |
| 營運層 | ~20% | task packet 抽象概念、role handoff 抽象概念、source classes 抽象概念 |

「防線層」目的：**讓 AI 不要亂搞 + 出錯後可追溯**。HARNESS 在這層成熟。

「營運層」目的：**讓 AI 規模化運作、跨 session、跨 controller、跨對話**。HARNESS 在這層只有抽象詞彙，沒有實體機制。

**這個偏移在本對話中具體呈現為**：

- token 消耗高（防線層儀式重複多）
- 每對話啟動成本高（要讀 4–5 個檔）
- 主對話 context 易爆（沒有 sub-session 機制 offload）
- 換 controller 等於從零開始（沒有 handoff 機制）

### 2.3 HARNESS 認知到的局限（**Codex 請審視此節**）

我累積本對話 3 次 §14 揭露之後得出的觀察：**HARNESS 規則無法防止「sandbox 工具輸出本身 stale」這類錯誤**。

具體：

- HARNESS §14 Mistake Response Protocol 假設「我們會發現自己錯」
- HARNESS §15 AI Pushback Right 假設「我們能識別衝突」
- HARNESS Core §17 假設「summary 不蓋過 source excerpt」

但這 3 條都依賴「AI 能正確判讀工具回傳值」。當工具回傳值本身是 stale / 假象（例如本對話中 `git status` 顯示 stale 的 modified 狀態），AI 會把 stale 當 truth，所有 downstream 規則都失效。

**HARNESS 沒有規則 cover「工具回傳值的真實性」**。這是一個盲區。

實務上這次靠 user 跑 `git hash-object` 比對才揭穿。即未來不能假設 AI 會自己發現此類錯誤。

## 3. user 原始設計 4 個 feature 對齊度（我的判讀，**請 Codex 校核完成度**）

User 在對話中提出原始設計包含：

| Feature | 意圖 |
| --- | --- |
| F1 | 每次行為寫成文件 + 長專案選擇性讀取對應資料（非全歷史讀取） |
| F2 | 快速繼承新主控室 |
| F3 | 利用次要對話深度思考（avoid 主對話盲點 + 省 context） |
| F4 | 利用次要對話實作（省主對話 context） |

我對 HARNESS 現況實作度的判讀：

### F1 完成度 ~30%

**HARNESS 有的：**
- Core §10 Task Packet / Return Report 抽象概念
- Core §5 Approved Read Scope 必須 exact
- Core §17–18 source classes（current / stale / historical / excerpt / summary / path-only）
- 我建的 current_state.md §11 Activity Log（時序）+ §12 Anomaly Log

**HARNESS 缺的：**
- 沒有 per-action 文件協定（schema、命名、index）
- 沒有 topic → file 索引
- 沒有依賴圖（task X 需讀 file A B）
- Activity log 沒連到具體動作文件

### F2 完成度 ~25%

**HARNESS 有的：**
- Core §6 Layered Startup and Identity Safety
- Core §7 Current Operational Rooms Snapshot Model（schema 抽象）
- Core §8 Full Room Identity
- Core §9 Role Handoff / Activation Abstract Flow（**完全抽象**，無具體模板）
- 我建的 Adapter §3 Room Identity Hook + current_state.md §2

**HARNESS 缺的：**
- 沒有 Controller Handoff Note 檔案型別
- 沒有區分「換 session」vs「換 controller」
- 沒有 inheritance scope 明文機制
- 沒有 succession 後驗證流程

### F3 完成度 ~15%

**HARNESS 有的：**
- Core §16 External Read-only Advisory Reviewer Model

**HARNESS 缺的：**
- 上述 model 預設為外部第三方，不是「同 AI 開分身對話」
- 沒有 sub-session dispatch 協定
- 沒有 condensed return 格式
- 沒有 token-budget 判準

### F4 完成度 ~20%

**HARNESS 有的：**
- Core §10 Task Packet（抽象）
- Manual §11 提到 implementation room

**HARNESS 缺的：**
- 沒有 dispatch to secondary session 協定
- 沒有 task packet 落地檔案格式
- 沒有 return integration 規則
- 沒有 sub-session working tree 隔離規則

### 整體判讀

User 的原始設計是「distributed cognitive architecture with audit/safety layer」。

HARNESS 目前實作：「audit/safety layer」幾乎完成；「distributed cognitive architecture」幾乎只剩詞彙。

**請 Codex 校核：以上 4 feature 完成度判讀是否準確？是否有我漏看的 HARNESS 機制能對應其中部分需求？**

## 4. 人性化優化已落地內容（本輪 Adapter / current_state.md）

我在本對話提出並落地（REVIEW status）的人性化機制：

| # | 機制 | 落地位置 |
| --- | --- | --- |
| 1 | 三級 Gate（Light / Standard / Strict） | Adapter §12 |
| 2 | Pre-Approved Routine Operations | Adapter §13 |
| 3 | Push 等效授權詞表 + 不算授權清單 | Adapter §7 |
| 4 | Mistake Response Protocol（5 步） | Adapter §14 |
| 5 | AI Pushback Right | Adapter §15 |
| 6 | Mode A / Mode B 雙模式 Project Policy | Adapter §2 |
| 7 | Reserved Room 機制 | Adapter §3 |
| 8 | Session Resume 短文 + 完整 startup packet | Adapter §16 + harness/core/writing_tool_project_startup_packet.md |
| 9 | current_state.md dashboard（active state、pending、stop-and-ask flags、activity / anomaly log） | _coordination/current_state.md |
| 10 | Route Contract Reference 形式（不重複 32A-LOCK） | harness/route_contracts/writing_tool_route_contract.md |
| 11 | Protected Source 暫定 + 未來擴充註記 | Adapter §6 |

### 4.1 仍然是 patch、不是真正解決的部分

| 機制 | 為什麼還是 patch |
| --- | --- |
| 三級 Gate | 減負；但每個動作仍要走 gate，重複儀式還在 |
| Push 詞表 | 提高精準度；但詞表本身需 user 維護 |
| Session Resume | 縮短啟動文字；但仍須讀 4 個檔，token 啟動成本仍高 |
| Pre-Approved 清單 | 加正面允許；但清單本身要 user 拍板 |
| current_state.md | 集中狀態；但 §11 §12 仍是手工 / AI 手工維護，沒有自動 ingestion |

**核心觀察**：以上機制都不影響 HARNESS 本體的「重心偏移」——它們治症狀（token、儀式重複、語意誤判），不治本（缺乏 distributed architecture）。

真正治本必須做 F1–F4。

## 5. 本對話累積 §14 錯誤紀錄

### 5.1 錯誤 #1（已記錄 current_state.md §12）

- 事件：將 `git status` 暫態 warning「unable to unlink .git/index.lock」當成永久殘留，寫入 Adapter §7 + current_state.md §5 §9 §13
- 揭露：user 重驗 `ls .git/` 後揭穿
- 處理：依 §14 揭露、提出回復方案、user 授權「全做」、修正 5 處

### 5.2 錯誤 #2（**尚未紀錄到 current_state.md §12**）

- 事件：從 sandbox 跑 `git remote add origin <url>`，atomic rename 跨 sandbox-Windows mount 失敗，導致 `.git/config` 被寫成 216 bytes null bytes、`.git/config.lock` 殘留 0 bytes、git 全面失效
- 揭露：執行當下立刻發現 exit 128，依 §14 揭露
- 處理：user 在 Windows 端執行 `Remove-Item .git\config.lock` + `Remove-Item .git\config` + `git init` 重建 config 後恢復
- 學到：依 §15 行使 pushback，所有 git 寫入改為 user-side
- 衍生規則建議：Adapter 新增 §7a「Sandbox Git Boundary」明文「Codex sandbox 不執行任何 git 指令（含 read-only）」

### 5.3 錯誤 #3（**尚未紀錄到 current_state.md §12**）

- 事件：把 sandbox-git 顯示的 stale "M modified" 狀態當真，推論 working tree ≠ HEAD、提出「stat cache 卡住」假說、建議 `git update-index --really-refresh`
- 揭露：user 跑 `git hash-object` 比對後揭穿（working tree SHA = HEAD SHA，A-F 修正其實已在 commit `58d33a7` 內）
- 處理：純訊息層作廢，無檔案修正動作
- 學到：sandbox-git 對 `.git/` 視圖不可靠（即使是 read-only operation 也不可靠）；§7a 邊界應擴大到「禁止從 sandbox 跑任何 git 指令」

### 5.4 三個錯誤的共同根因

**Claude 工具回傳值本身不可靠這個盲區**，HARNESS 沒有規則 cover：

- HARNESS 假設「PASS / READY 不是 approval」但**有讀工具 → 工具回傳是 truth**這個前提
- 當前提失效（sandbox-Windows mount 不可靠），整個推論鏈崩盤
- §14 揭露機制只能事後補救，不能事前防止

**請 Codex 評估**：HARNESS 是否需要新增一條規則類別處理「工具回傳值真實性」？例如：
- 雙重驗證（同類資訊用 2 個獨立路徑取得）
- platform-specific 不可靠操作 blacklist
- 重要動作前的 sanity check

### 5.5 Adapter §7a / current_state.md §12 補登提案（尚待 user 決定）

我已給 user 兩個選項 X / Y：

- X：不擴 §12，後續補
- Y：擴 §12（紀錄錯誤 #2 + #3）+ Adapter 新增 §7a Sandbox Git Boundary

user 在 user 完成 push 之後**尚未明確選 X 或 Y**。本檔保持中性、未做修改。

## 6. user 已確認的決策（給 Codex 對齊）

依本對話累積：

- B1–B7：人性化機制 7 條全部接受預設
- C1-b：active controller = Codex-WT 主控室（report-back target 同處；設計室 / 實作室 / review / validation room 留欄位）
- C2-b：protected source 暫定，未來擴充
- C3：雙模式 Mode A / Mode B；目前 Mode A
- C4：remote URL `https://github.com/mark75369/writing-tool-project-folder.git`；原 C4-a（Codex 跑）因錯誤 #2 改成 D4-b（user 跑），這也成為「禁止 sandbox 跑 git 寫入」的依據
- C5-b：route contract 採 reference 形式
- C6-a：dashboard 預填 + TBD
- D1：commit `58d33a7` 是 user 親自做的
- D2-a：A-F 修正補 commit（**結果：A-F 已被 commit 58d33a7 包進去，無需額外 commit**——錯誤 #3 揭穿的事實）
- D3-a：branch 維持 master
- D4：改為 user-side（依錯誤 #2 衍生）
- D5-b：push 由 user 在 Windows 端執行
- D6：`.git/index.lock` 與 `index` 並無殘留 lock

## 7. 還沒完成的維護任務

| 項目 | 狀態 |
| --- | --- |
| current_state.md §12 補錯誤 #2 + #3 | TBD（user 選 X / Y） |
| current_state.md §5 / §8 / §9 / §11 / §13 反映 push 完成狀態 | TBD（同上） |
| Adapter §7a Sandbox Git Boundary 新增 | TBD（同上） |
| LOCKED 升級候選評估 | 暫無 |
| Mode B 規劃 | TBD |
| Protected source 清單擴充 | TBD（未來放實際劇本內容前） |
| F1 設計 | **下一個 phase（user 已選擇優先做）** |
| F2 設計 | **下一個 phase（user 已選擇優先做）** |
| F3 設計 | 延後 |
| F4 設計 | 延後 |

## 8. F1（行為文件化 + 選擇性讀取）落地建議

### 8.1 目標

- 每個 gate-passed action 產生獨立檔案
- 新對話 / 新 controller 啟動時，依任務需要 demand-load 必要 action files，不再全讀歷史
- 老專案維持讀取成本可控（不隨對話數線性增長）

### 8.2 Schema 草案

**檔案路徑**：

```
_coordination/actions/<timestamp>_<action_id>_<type>.md
```

其中：

- `timestamp`：ISO-8601 縮寫 `YYYYMMDDTHHMMSS`
- `action_id`：短雜湊 4 碼，session 內唯一（避免時間戳衝突）
- `type`：閉集枚舉（見下）

**Action type 閉集**（建議起手）：

| type | 適用 |
| --- | --- |
| `decision` | user / controller 決策（D1–D6 之類） |
| `gate_pass` | gate 通過紀錄（commit / push / file write） |
| `file_write` | markdown / config 寫入動作 |
| `mistake_disclosure` | §14 揭露 |
| `pushback` | §15 行使 pushback 紀錄 |
| `handoff` | controller 交接（與 F2 整合） |
| `health_check` | 維護健診結果 |
| `external_input` | user 外部資料貼入紀錄 |

**Action file 必填欄位**：

```yaml
---
id: <timestamp>_<action_id>
type: <enum>
status: DRAFT | ACTIVE | SUPERSEDED | ARCHIVED
created_at: <ISO-8601>
created_by: <room identity>  # 必為 full identity
supersedes: <id or null>
superseded_by: <id or null>
related_actions: [<id>...]
tags: [<tag>...]
gate_level: light | standard | strict | n_a
input_sources: [<path>...]   # 此動作讀了哪些檔
output_changes: [<path>...]  # 此動作改了哪些檔
report_back_to: <room identity>
---

# <action title>

## Summary
...

## Context
...

## Action Taken / Proposed
...

## Result / Outcome
...

## Source Limitations
...

## Stop Conditions
...

## Boundary
本 action 不批准...
```

### 8.3 Index 自動生成規則

**檔案**：`_coordination/actions/index.md`

**內容**：表格列出所有 action files（id / type / status / tags / created_at / 一行 summary）。

**生成方式**：**必為腳本 / 工具自動產生**，不接受手寫。手寫 index 是維護地獄。

**建議**：在 `scripts/` 中新增 `regen_actions_index.py`（或 PowerShell 等價），每次 action file 新增 / 狀態變更時自動 rerun。

### 8.4 選擇性讀取規則

**新對話啟動讀取序**：

1. 必讀：`_coordination/current_state.md`（active state）
2. 必讀：`_coordination/project_adapter/<project>_project_adapter.md`（規則）
3. 必讀：`_coordination/actions/index.md`（索引）
4. **依任務動態決定**：哪些 action files 進 read scope

**動態決定機制**：

- user 明文指定（例：「讀 last 5 action files of type=decision」）
- AI 提案 read scope，user 過 standard gate
- 不允許 AI 自行擴張 read scope

### 8.5 維護自動化內建

| 維護面 | 自動化建議 |
| --- | --- |
| Action file 建立 | gate-passed 後 AI 自動產出 draft，user ok 後落檔 |
| Index 同步 | 每次 action file 落檔 / 狀態變更觸發 regen |
| 必填欄位 | schema 驗證 script；缺欄位 → 寫入失敗 |
| 狀態枚舉檢查 | 同上 |
| Supersede 鏈完整性 | 月底 health check 跑 graph 驗證 |
| Activity log 同步 | current_state.md §11 改為從 actions/ 派生，不另寫 |

### 8.6 風險

| 風險 | 嚴重度 | 對策 |
| --- | --- | --- |
| Index 失同步 | 極高 | 自動生成、禁止手寫、health check |
| Action file 漏寫 | 中 | gate-passed 必觸發；漏的會被 health check 抓到 |
| Supersede 鏈斷裂 | 高 | id 不可變；graph 驗證 |
| Schema 演進 | 中 | 版本化（schema_version 欄位） |
| Tag 失控 | 中 | tags 也用閉集（先小、必要時加） |

### 8.7 對 Codex 的具體請求

- 校核 schema 設計是否合理（特別是 type 枚舉是否覆蓋夠）
- 評估 index 自動生成腳本應該由 Codex / Claude / user 哪一方維護
- 評估「腳本」這個依賴本身要不要走 strict gate（Adapter §12 目前禁止 product code / template，腳本算哪一類？）
- 是否有 HARNESS Core 規則會被新 schema 違反

## 9. F2（主控室快速繼承）落地建議

### 9.1 目標

- 換 AI / 換對話 / 換 controller / 換 phase 不必重新教整個專案
- 新 controller 第一輪有明確的 inheritance scope 與 first verification
- inheritance 過程可審計

### 9.2 Handoff Note Schema

**檔案路徑**：

```
_coordination/handoffs/<timestamp>_<from_room>_to_<to_room>.md
```

**必填欄位**：

```yaml
---
id: <timestamp>_<from>_to_<to>
status: DRAFT | ACCEPTED | REJECTED | EXPIRED
handoff_type: controller_change | session_resume | phase_transition | ai_platform_switch
from_room: <full identity>
to_room: <full identity>
created_at: <ISO-8601>
accepted_at: <ISO-8601 or null>
accepted_by: <user / to_room / null>
expires_at: <ISO-8601 or null>
---

# Handoff Note: <from> → <to>

## Inheritance Scope
本 handoff 繼承的 scope 包含：
- ...

## Preserved State
新 controller 必須沿用：
- ...

## Reset State
新 controller 必須重設：
- ...

## First Verification（新 controller 第一輪必做）
1. ...
2. ...

## Open Questions / TBD
...

## Stop Conditions
...

## Boundary
本 handoff note 不批准...
```

### 9.3 適用情境分流

| 情境 | handoff_type | 範例 |
| --- | --- | --- |
| 換 AI 平台 | `ai_platform_switch` | Claude → Codex，或反之 |
| 換 controller 身份 | `controller_change` | Codex-WT 主控室 → Codex-WT-2 主控室 |
| 新對話延續 | `session_resume` | 同一 controller，斷對話續上 |
| 進入新 Phase | `phase_transition` | Phase 32A → 32B |

不同 handoff_type 有不同的 inheritance default：

- `session_resume`：default 全繼承
- `controller_change`：default reset 個人偏好 / 仍繼承專案規則
- `ai_platform_switch`：default 重新核對 platform capability + inheritance
- `phase_transition`：default 標記 phase 收尾、新 phase 開帳

### 9.4 與 F1 的整合

- Handoff note 同時也是一個 action file（`type: handoff`）
- Handoff note 寫入 → 觸發 index regen + current_state.md §2 更新
- 新 controller 第一輪做 First Verification → 產生新 action file（type: gate_pass 或 decision）

### 9.5 風險

| 風險 | 對策 |
| --- | --- |
| Inheritance scope 寫不清 → 新 controller 帶入舊偏差 | schema 強制 Preserved / Reset 兩個欄位；不可空 |
| 舊 controller 名稱被新 controller 沿用 | id 不可變；舊 controller 退役後加 retired_at 欄位 |
| Handoff 沒被 accepted 就繼續做事 | status 為 DRAFT 期間，新 controller 不得執行 Strict gate 動作 |
| 換 AI 時 platform capability 沒檢查 | handoff_type=ai_platform_switch 必須附 Platform Capability Hook 對照 |

### 9.6 對 Codex 的具體請求

- 校核 handoff schema 是否完整（特別是 First Verification 欄位設計）
- 評估 `controller_change` vs `ai_platform_switch` 區分是否真的必要
- 評估 Handoff Note 與 current_state.md §2 的同步機制
- HARNESS Core §9 Role Handoff Abstract Flow 是否需要對應更新（會動 Core，需考慮 32A-LOCK「HARNESS 穩定」原則）

## 10. Platform Capability Hook 設計（讓 HARNESS 跨 Codex / Claude）

### 10.1 動機

本對話揭示：sandbox-Windows mount 對 `.git/` 寫入不可靠（錯誤 #2 #3）。不同 AI 平台有不同的能力與不同的雷區。

HARNESS Core 不應寫死「能做什麼 / 不能做什麼」，應由 Adapter 中的新 Hook 表達。

### 10.2 Hook schema

加入 Adapter（新增節，建議 §22 或 §6a 位置）：

```markdown
## Platform Capability Hook

| Capability | 本平台支援 | Dispatch 方法 | 已知雷區 |
| --- | --- | --- | --- |
| read_files | yes | <tool name> | - |
| write_markdown | yes | <tool name> | - |
| run_shell_read | yes | <tool name> | - |
| run_git_read | yes / NO | - | <例：sandbox 看 stale 視圖> |
| run_git_write | yes / NO | - | <例：sandbox atomic rename 跨 mount 失敗> |
| spawn_subagent_thinking | yes / NO | <tool name> | - |
| spawn_subagent_implementation | yes / NO | <tool name + isolation> | - |
| ... | ... | ... | ... |
```

每個平台填一份對應的 Capability 表。

### 10.3 本專案目前 Platform Capability（Claude Cowork 版）

| Capability | 本平台 | 雷區 |
| --- | --- | --- |
| read_files | yes（Read tool） | - |
| write_markdown | yes（Write / Edit tool） | - |
| run_shell_read | yes | `.git/` 內檔可能 stale |
| run_git_read | **NO**（依錯誤 #1 #3 經驗）| sandbox-git 對 `.git/` 視圖不可靠 |
| run_git_write | **NO**（依錯誤 #2）| atomic rename 跨 sandbox-Windows mount 失敗 |
| spawn_subagent | yes（Agent tool）| - |
| spawn_subagent_with_worktree | yes（Agent + `isolation: "worktree"`）| - |

**Codex CLI 版我無法填寫**——需 Codex 自己 audit 並補。

### 10.4 規則整合

- F3 / F4 的 dispatch 邏輯依 Platform Capability Hook 動態決定
- 不支援自動 dispatch 的平台降級為 manual（user 手動開新對話）
- AI 在 startup 時必須先 read Platform Capability Hook 才能執行任何動作

## 11. 對 Codex 的整體請求

請 Codex 在 review 時針對下列各點獨立判斷：

### 11.1 我的判斷可能錯在哪裡

- §2.2 HARNESS 重心偏移：80 / 20 分配比例的判讀是否準確？
- §2.3 「工具回傳值真實性」盲區：是否真的是 HARNESS 盲區，還是我漏看了某條規則？
- §3 4 feature 完成度：是否有我漏看的 HARNESS 機制能對應其中部分需求？

### 11.2 F1 設計是否合理

- §8.2 schema 是否覆蓋夠
- §8.3 index 自動生成方案是否實際可行
- §8.4 選擇性讀取規則是否會牴觸 Core §5 Approved Read Scope
- §8.5 維護自動化建議是否會牴觸 Core §20 must-not-infer 規則

### 11.3 F2 設計是否合理

- §9.2 handoff schema 是否完整
- §9.3 handoff_type 分流是否必要
- §9.4 與 F1 整合是否乾淨
- §9.6 是否會動到 Core §9 Role Handoff Abstract Flow（會違反 32A-LOCK「HARNESS 穩定」原則嗎？）

### 11.4 Platform Capability Hook 是否合理

- §10.2 schema 是否覆蓋 Codex CLI 的實際 capability
- §10.4 規則整合是否會牴觸 Core §21 Adapter Hook Requirements
- Codex CLI 對 `.git/` 寫入是否也有雷區（請 Codex 自己 audit）

### 11.5 累積 §14 錯誤的根因

- §5.4 三個錯誤共同根因判讀是否準確
- §5.4 建議的雙重驗證 / blacklist / sanity check 是否實作可行
- 是否有更深層、我沒看出的共同根因

### 11.6 啟動順序建議

我的建議順序：F1 → F2 → F4 → F3。

- F1 是基礎設施（其他都需要 actions/ 檔）
- F2 自然延伸
- F4 比 F3 容易驗證（實作有 diff）
- F3 風險最高放最後

**請 Codex 校核此順序，或提出替代順序與理由**。

### 11.7 32A-LOCK 「HARNESS 穩定」原則衝突

32A-LOCK §8 規定「HARNESS 為 A 路線視為穩定，不擴張除非重大 blocker」。

F1 / F2 / Platform Capability Hook 都會擴張 HARNESS（新文件型別、新 Adapter 節、可能新 Core 規則）。

**請 Codex 評估**：

- 本提案是否構成「重大 blocker」（值得突破穩定原則）？
- 還是應該維持 32A-LOCK 不動，讓本提案的東西全部留在 Project Adapter 層、不碰 Core？
- 或者，是否應該另開 Phase 32C / 33 走「HARNESS 自己迭代 HARNESS」（即 32A-LOCK §9 的 B 路線）？

## 12. 不批准 / 邊界

本檔是 Phase 32B REVIEW 提案，**不**批准：

- F1 / F2 / F3 / F4 落地實作
- HARNESS Core 任何修改
- 32A-LOCK 任何修改
- 任何檔升級到 LOCKED
- Adapter §7a 新增（仍 TBD）
- current_state.md §12 補錯誤 #2 / #3（仍 TBD）
- Platform Capability Hook 新增到 Adapter（仍 TBD）
- Mode B 切換
- protected creative content read
- 任何 commit / push / remote 操作
- Runtime / SDK 啟動
- 啟用 reserved room

任何 evidence / advisory finding（包含本檔）不等於 approval。

## 13. Stop Conditions

stop-and-ask 條件：

- 本檔被當作 authority
- 本檔被當作 F1 / F2 啟動授權
- Codex review 結果被當作 approval（review 只是 evidence）
- 任何規則建議被自動套用而未過 standard gate
- 「請 Codex 校核」被誤解為 Codex 有 authority 修改 HARNESS
- 任何 §14 揭露 / pushback 被當作允許繼續執行原動作

## 14. Classification

```
PHASE_32B_CLAUDE_PROPOSAL_FOR_CODEX_REVIEW_ON_HARNESS_OPTIMIZATION_AND_F1_F2_DESIGN
```

Meaning:

- Phase 32B 由 Claude 提出，供 Codex review
- 本檔評估 HARNESS 現況、列出 4 feature 完成度、累積 §14 錯誤、未完成維護
- 本檔提出 F1 / F2 schema 草案與 Platform Capability Hook 草案
- 本檔請求 Codex 校核多項判讀
- 本檔不批准任何實作 / 修改 / commit / push / Mode B / Runtime 啟動

## 15. Boundary Confirmation

本檔是 REVIEW 提案 only。

不是：

- F1 / F2 啟動授權
- HARNESS Core 修改授權
- 32A-LOCK 修改授權
- LOCKED 升級授權
- Codex authority 升級
- product implementation 授權
- protected content read 授權
- commit / push / remote 設定授權
- Mode B 切換授權
- Runtime / SDK 啟動授權

任何 Codex review 回應視為 advisory evidence，最終決策由 user 在 standard / strict gate 中做出。

## 附錄 A：完整對話脈絡縮要（for Codex orientation）

時間軸：

1. user 啟動本對話，要求讀 6 個 HARNESS 啟用檔案
2. 我（Claude）讀完 5 個（writing_tool_project_startup_packet.md 與 writing_tool_route_contract.md 兩檔在專案內缺失）
3. 我回報 active state
4. user 詢問評估 → 我給 HARNESS 整體評估
5. user 詢問人性化優化建議 → 我提 11 條
6. user 授權完整優化 → 我提 4 個檔案落檔計畫 + C1–C6 決策請示
7. user 答覆決策 → 我落 4 個 REVIEW 檔
8. **錯誤 #1**：把 index.lock 暫態 warning 當永久殘留，寫入 4 處
9. user 質疑 → §14 揭露 → 提案 A–F → user「全做」→ 修正
10. user 提供 GitHub 截圖「我沒辦法 push」→ 我診斷
11. user 答 D1–D6 決策
12. **錯誤 #2**：我從 sandbox 跑 git remote add，毀 .git/config
13. §14 揭露 + §15 pushback → user 在 Windows 端 git init 重建
14. **錯誤 #3**：把 sandbox-git stale 視圖當真，誤判 stat cache
15. user 跑 git hash-object 揭穿 → §14 揭露 → 確認 A-F 已在 commit 58d33a7 內
16. user 走 D4-b 設 remote + D5-b 完成首次 push
17. user 詢問 HARNESS 對我行為的影響 → 我反思
18. user 詢問 token 消耗 → 我估算
19. user 提原始設計 4 個 feature → 我評估完成度
20. user 確認先做 F1 + F2 → 詢問維護負擔
21. user 要求把以上整理成文件給 Codex review → 本檔

## 附錄 B：相關檔案完整路徑

| 檔案 | 路徑 |
| --- | --- |
| HARNESS Core | `harness/core/workflow_harness_core_v1_0_freeze.md` |
| Export Profile | `harness/core/workflow_harness_core_v1_0_export_profile.md` |
| Usage Manual | `harness/core/workflow_harness_new_project_usage_manual.md` |
| 啟用說明書 | `harness/core/啟用說明書.md` |
| 32A-LOCK 決定書 | `harness/route_contracts/20260517_32_a_lock_writing_tool_route_contract_decision_note.md` |
| Project Adapter | `_coordination/project_adapter/writing_tool_project_adapter.md` |
| Current State | `_coordination/current_state.md` |
| Route Contract Reference | `harness/route_contracts/writing_tool_route_contract.md` |
| Startup Packet | `harness/core/writing_tool_project_startup_packet.md` |
| 本檔 | `_coordination/workflow_notes/20260517_32_b_claude_harness_optimization_proposal_for_codex_review.md` |
