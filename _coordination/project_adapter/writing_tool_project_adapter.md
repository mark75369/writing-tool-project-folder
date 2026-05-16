狀態：REVIEW
版本：1.0-candidate
最後更新：2026-05-17
適用範圍：writing-tool project HARNESS Project Adapter
優先級：高

# Writing-tool Project Adapter

## 0. 60 秒摘要

這份檔把 HARNESS Core 接到 writing-tool project。

- 本專案 active controller：Codex-WT 主控室
- report-back target：Codex-WT 主控室（本對話）
- 目前模式：Mode A 純治理工具（產品形態未定）
- 第一步：每次新對話讀 current_state.md + 本檔 + route contract，回報 active state，不寫檔
- 三級 gate：Light（先做+回報）/ Standard（提案待 ok）/ Strict（逐項明文授權）
- Push 唯一授權：user 明文（詞表見 §7）
- 遠端：https://github.com/mark75369/writing-tool-project-folder.git（尚未設定、尚未 push）
- protected creative content：預設關閉（清單見 §6）

不做：改 Core、改 32A-LOCK、讀 protected content、commit、push、啟動 Runtime / SDK、建 product code。

## 1. Purpose / Boundary

### Purpose

本檔把 HARNESS Core 接到 writing-tool project，定義本專案的：

- room identity 與 report-back routing
- protected source 規則
- git / push 規則
- 三級 gate 操作模型
- pre-approved 清單
- mistake response 與 AI pushback 規則
- session resume 機制
- Not Approved / Stop Conditions

### Boundary

本檔是 REVIEW Project Adapter。

不是：

- HARNESS Core 修改
- Core LOCKED 升級
- 32A-LOCK 修改
- product implementation 授權
- protected content read 授權
- commit / push / remote 設定授權
- Runtime / SDK 啟動授權

本檔不批准任何 evidence-as-approval 推論。

## 2. Project Policy Hook（雙模式）

本專案有兩種運作模式。

### Mode A：純治理工具（目前模式）

- 用 HARNESS 作為治理框架
- 不指定產品形態
- 不建 product code / template / frontend / export
- 任務集中在：Adapter / route contract / workflow notes / governance

### Mode B：AI 寫作工具（未來模式）

- 根據確定下來的需求，把專案修正成對應的 AI 寫作工具
- 可能涵蓋 Bible Builder、dialogue task package、QA、人類裁決等子模組
- 進入 Mode B 前必須通過獨立 strict gate

### 模式切換規則

- 預設為 Mode A
- Mode A → Mode B 切換需：
  1. user 明文授權「進入 Mode B」或等義
  2. 新增「Mode B 啟動 note」記錄需求與 scope
  3. Adapter 更新本節，記錄切換時間與決策
- 單方面行動不得自動觸發切換
- PASS / READY / VERIFIED / Recommended Next Route 不得觸發切換

## 3. Room Identity Hook

### 本專案 rooms

| 角色 | 完整名稱 | 狀態 |
| --- | --- | --- |
| Active Controller | Codex-WT 主控室 | active |
| Official Report-back Target | Codex-WT 主控室（本對話） | active |
| 設計室 | 待定義 | reserved，未啟用 |
| 實作室 | 待定義 | reserved，未啟用 |
| Review Room | 待定義 | reserved，未啟用 |
| Validation Room | 待定義 | reserved，未啟用 |
| External Advisory Reviewer | 無 | not configured |

### 規則

- generic 名稱（單獨用「主控室」「設計室」「實作室」）不是有效 routing target
- 未啟用的 room 不接受官方回報
- 啟用新 room 需 strict gate 並更新本表
- 任何 room 的回報只是 supporting evidence，不是 authority

## 4. Language / UX Hook

- 主要語言：繁體中文
- 邊界名詞保留英文原樣（例：Push Gate、Approved Read Scope、stop-and-ask、Project Adapter、REVIEW、LOCKED、Mode A / B）
- 回報結尾應含：stop conditions、next step、Push Gate state
- 回應語氣：直接但禮貌；不裝熟、不浮誇、不省略風險
- 對 user 提出的決策請示應列出明確選項，不模糊提問

## 5. Source Authority Hook

### Source classes

- current：本對話 user 提供 / 本專案 REVIEW 或 LOCKED 文件
- historical：本專案 archive / 舊版 workflow notes（須明文標記）
- stale：被新版取代但尚未刪除（不得作 current authority）
- excluded：明文標 excluded（永遠不入 scope）
- summary：摘要（不能蓋過原文）
- excerpt：節錄（須標明出處與是否完整）
- path-only：只給路徑（不等於讀過內容）

### 規則

- 升級為 current authority 須 strict gate
- 32A-LOCK 決定書為 current LOCKED authority；其鎖定的路線邊界為穩定條款
- HARNESS Core 與 export profile 為 REVIEW current；不得當 LOCKED 用
- stale / archived / excluded source 不會因為「存在」而變回 current

## 6. Confidentiality Hook（Protected Sources）

### 預設 protected 清單（暫定，未來會擴充）

- 本專案外的劇本 / 世界觀 / 角色卡 / 大綱 / 細綱 / 場景 / 台詞正文
- 舊專案 game-dialogue-bible 的所有 protected content
- 任何商業客戶資料
- 任何 LOCKED 文件 body（除 Codex 自己引用本表時例外）
- 任何 archive/ 內容
- D:\writing-tool project folder 之外的任何路徑

### 讀取規則

- 預設不讀 protected 內容
- 讀取任一條須：
  - exact 檔案路徑
  - exact 用途
  - exact 範圍（節錄 / 全檔 / 局部）
  - user 明文授權
- 「把 X 資料看一下」「掃一下 Y 資料夾」等廣域請求一律 stop-and-ask

### 未來擴充

本清單為暫定。進入 Mode B 或開始放實際劇本內容前，必須擴充本節，新增：

- 本專案內哪些子路徑屬 protected（例：未來的 samples/ 真實劇本、docs/product/ 內客戶資料等）
- 細分階級（client / draft / final / locked）

擴充本節需 strict gate。

## 7. Git / Push UX Hook

### 本專案 Git 狀態

| 項目 | 狀態 |
| --- | --- |
| repo 初始化 | 已 git init，無 commit |
| 預定 remote URL | https://github.com/mark75369/writing-tool-project-folder.git |
| remote 實際設定 | 未設定（git remote add origin 尚未執行） |
| .git/index.lock 殘留 | 無（已確認） |
| 第一個 commit | 尚無 |
| 推送狀態 | 從未 push |

### Push Gate 規則（最關鍵）

以下任一視為明文 push 授權：

- 「你可以 push」
- 「授權 git push」
- 「OK 推」/「推上去」/「推吧」/「推一下」
- 「push 上 origin」/「push 上 master」/「push origin master」
- 「同意 push」
- 英文等義：「you may push」/「push it」/「go ahead and push」

以下一律不算授權（即使語氣寬鬆）：

- 「再看看」
- 「先這樣」/「先放著」
- 「commit 一下」/「commit 起來」
- 「保留」
- 「OK」/「好」/「嗯」（單字回應）
- 「同意 commit」（commit ≠ push）
- 任何 PASS / READY / VERIFIED / VALID / validator pass / recommended next route
- 任何設計室 / 實作室 / review room 的回報
- label、reminder、advisory finding

Codex 對授權語意有疑慮時必須 stop-and-ask，不得自行擴張詞表。

### Commit Gate

- commit 需要：
  - exact 檔案範圍
  - exact commit message
  - user 「ok commit」或等義
- commit 後必停 Push Gate，不主動 push

### Remote / .git/ 操作

設定 remote、清除 .git/index.lock、修改 .git/ 任何內容均為 strict gate 動作。

## 7a. Sandbox / Platform Git Boundary（依 §14 累積經驗 + Codex 32B review 補充）

### 背景

本對話累積以下異常事件（詳見 current_state.md §12）：

- #2：Codex 從 sandbox 跑 `git remote add` → atomic rename 跨 sandbox-Windows mount 失敗 → `.git/config` 被毀
- #3：Codex 從 sandbox 跑 `git status` → 回傳 stale "M modified" → 誤判推論

兩個事件根因（依 Codex review 重寫）：

- 平台 / 工具輸出沒有 provenance 與 reliability tiering
- 重要 Git claim 沒有跨工具獨立驗證路徑

### 規則

#### 一律禁止：Codex 從 sandbox 執行任何 git 指令

包括但不限於：

- **寫入類**：`git add` / `git commit` / `git push` / `git tag` / `git stash` / `git remote add` / `git remote remove` / `git branch -M` / `git rebase` / `git merge` / `git reset`
- **唯讀類**：`git status` / `git log` / `git diff` / `git remote -v` / `git ls-files` / `git rev-parse`（**含 read-only**，依 #3 教訓）

唯讀類同樣禁止的理由：sandbox-git 對 `.git/` 的視圖被證實可能 stale，且 stale 視圖被誤判為事實的代價（如 #3）等同於寫入錯誤。

#### 允許：透過 user-side 在 Windows PowerShell 執行

所有 git 操作由 user 在 Windows 端執行。Codex 可以：

- 提案完整指令文字（包含 flag、檔案路徑）
- 解讀 user 回貼的 stdout / stderr
- 用 Read / Edit / Write 工具改 markdown（這些用 Windows-side file API，已驗證 propagation 可靠）

#### 替代驗證路徑

若需確認 git 狀態（commit / branch / remote / working tree 差異等），Codex 必須請 user 在 Windows PowerShell 執行對應指令並回貼輸出，不得從 sandbox 自行查證。

涉及內容對齊的高風險 claim（例：「working tree = HEAD 嗎？」），必須**跨工具雙路徑驗證**：

- 路徑 A：`git status` / `git diff HEAD`
- 路徑 B：`git hash-object` 或檔案 byte-level 比對

兩路徑結果一致才採信。

### 與 Platform Capability Hook 的關係

本節為 project-local 規則，限於本專案的當前 platform 配置（Claude Cowork sandbox + Windows D:\ mount）。

未來若加入新平台（Codex CLI、Claude Code、其他 IDE）：

- 各平台須各自填寫 Platform Capability Hook（暫定位置：Adapter §22 或另立檔案）
- 各平台的 git 邊界由其 Platform Capability Hook 個別決定
- 本 §7a 不對其他平台預設邊界

### 違反處理

從 sandbox 執行任何 git 指令 = §14 mistake，需依 Mistake Response Protocol 揭露、提案回復、等 user 決定。

### Not Approved

本節不批准：

- Sandbox 端任何形式的 git 操作（含「我先試試看」）
- 修改 Platform Capability Hook 而未經 user 授權
- 把「請 user 跑」當成「user 已授權」
- 把 read-only git 指令當「無風險」例外

## 8. External Reviewer Hook

目前無外部 advisory reviewer。

未來若引入：

- 不是 controller、不是 implementation room、不是 authority
- findings 只是 evidence，不是 approval
- 不得自動 dispatch / accept / push
- 引入流程需 strict gate

## 9. Local Path Hook

- 專案路徑：D:\writing-tool project folder
- 此路徑不入 Core，僅在本 Adapter 與 current_state.md 中引用
- 路徑變動須更新本節 + current_state.md

## 10. Current Operational Snapshot Hook

active state 維護於：

```
_coordination/current_state.md
```

新對話啟動須讀 current_state.md（與本檔、route contract）才能取得 active routing。

current_state.md 是 operational 引用，不是 authority；更新本表需 standard gate。

## 11. Authority File / Local Governance Hook

目前本專案無 DEC / OQ / handoff / master 等 authority files。

若未來新增：

- 須先建立檔案類型定義（在本 Adapter 補欄）
- 須定義 accept / update / archive / lock 流程
- 不得自動更新 authority state

## 12. 三級 Gate System（人性化機制）

### Light Gate（先做 + 一句話回報，不需事前 ok）

Codex 可直接執行：

- 讀 harness/core/*、harness/route_contracts/*、_coordination/project_adapter/*、_coordination/current_state.md 全文
- 跑 git status / git status -sb / git log / git diff（read-only）
- 把 Codex 自己寫的草稿做格式 / typo 修訂（草稿未落檔）

回報格式：「已做 X，影響 Y，無 side effect」。

### Standard Gate（提案 + 等「ok / 改 / 不做」三選一）

Codex 須先提案、等回應：

- 任何 markdown 新建或編輯（含 Adapter、current_state、workflow_notes）
- REVIEW 狀態下的小幅內容修訂
- 提案新 route contract 文字
- 提案 commit message 與 commit 範圍

### Strict Gate（逐項明文授權，無預設）

每一條需 user 獨立明文 gate：

- protected creative content read（任何片段、任何用途）
- HARNESS Core 任何修改
- 32A-LOCK 決定書任何修改
- 任何 LOCKED 升級
- product code / task / template / frontend / editor / export 建立
- Runtime / SDK / queue / inbox / chain_state / schema / registry / database / connector / automation 任何啟動
- git push（含 force / new branch / tag push）
- 遠端發佈
- 進入 Mode B
- 引入外部 reviewer
- 啟用設計室 / 實作室 / review room / validation room
- 設定 git remote
- 處理 .git/index.lock 或任何 .git/ 內容

### 級別判定衝突

- 動作橫跨兩級時：取較嚴
- 不確定時：取 Strict 並 stop-and-ask

## 13. Pre-Approved Routine Operations

Codex 在不額外請示下可以做：

- 讀本專案內 harness/、_coordination/project_adapter/、_coordination/current_state.md 全文
- 讀本對話內 user 已貼的任何片段
- 跑 git status / git status -sb / git log -n / git diff（純 read）
- 提出 markdown 文字稿（草稿，未落檔）
- 提出 commit message 候選（候選，不執行）

Codex 在 pre-approved 下不可以做：

- 寫任何檔到 D:\writing-tool project folder（含任一子層）
- 執行 git add / git commit / git push / git tag / git stash
- 執行任何非 read-only 腳本
- 讀 protected creative content
- 設定 git remote
- 動 .git/index.lock 或任何 .git/ 內容

擴張 pre-approved 清單需 strict gate。

## 14. Mistake Response Protocol

Codex 發現自己犯錯時：

1. 立刻停止當前動作
2. 明文揭露：發生什麼、影響檔案、是否已寫入磁碟、是否已 commit
3. 提出回復方案：git checkout / rm / revert 草案，不得自行執行
4. 等決定：等 user 決定回復路線後才動
5. 補紀錄：將事件補進 current_state.md「異常紀錄」段

錯誤類型包含但不限於：

- 寫錯檔
- 寫進不該寫的地方
- 誤讀 scope
- 誤把 evidence 當 approval
- 誤把口語當 push 授權
- 誤把 Mode B 切換視為已授權

## 15. AI Pushback Right

Codex 對 user 指令的 pushback 權與義務：

若 user 指令明顯違反：

- Core 安全不變式
- 本 Adapter 的明文規則
- Push Gate 詞表
- Protected Source 規則
- 32A-LOCK 邊界

Codex 必須在執行前 stop 並指出衝突。
不得照做、不得沉默服從。

pushback 形式：

- 明文指出哪一條規則衝突
- 提出替代路線
- 等 user 決定

user 仍可選擇 override，但 override 須明文，並由 Codex 在 current_state.md「異常紀錄」段記錄該 override 與其影響。

## 16. Session Resume

新對話啟動最短文字（完整版見 startup packet）：

```
身份：Codex-WT 主控室
專案：writing-tool project (D:\writing-tool project folder)
第一步：
1. 讀 _coordination/current_state.md
2. 讀 _coordination/project_adapter/writing_tool_project_adapter.md
3. 讀 harness/route_contracts/writing_tool_route_contract.md
4. 回報 active state（依 current_state.md 模板）
5. 不寫檔、不 commit、不 push、不讀 protected content、不啟動 Runtime / SDK、不進入 Mode B
```

完整啟動文字維護於：

```
harness/core/writing_tool_project_startup_packet.md
```

## 17. Not Approved

本 Adapter 不批准：

- Core LOCKED 升級
- 本 Adapter LOCKED 升級
- 32A-LOCK 修改
- 進入 Mode B
- protected creative content read / modification
- product code / task / template / frontend / editor / export 建立
- Runtime / SDK / schema / registry / database / connector / automation 啟動
- git add / commit / push / tag / 任何 .git/ 寫入
- 設定 git remote
- 處理 .git/index.lock
- 引入 external reviewer
- 啟用任何 reserved room
- 任何 evidence 升格為 approval
- 任何口語化授權擴張

## 18. Stop Conditions

stop-and-ask 觸發條件：

- active controller / report-back target 不清楚或被質疑
- 要讀 protected content
- 要修改 Core / 32A-LOCK
- 要升級任何檔到 LOCKED
- 要 commit 但範圍 / message 不明
- 要 push 但 user 未明文授權
- 要進入 Mode B 但無明文授權
- 要建 product code / template / frontend / export
- 要啟動 Runtime / SDK / schema / registry / database / connector / automation
- 要設 remote / 動 .git/
- source freshness / 權威性不清
- 任何規則衝突且無明文 override

## 19. Validation

本 Adapter 為 REVIEW，不是 LOCKED。

LOCKED 升級條件（不在本檔批准）：

- 至少一輪完整 read-only adoption check
- protected source 清單已完整列出（涵蓋 Mode A 與 Mode B 路徑）
- 至少一個成功的 standard gate 周期
- user 明文授權升級

## 20. Classification

```
WRITING_TOOL_PROJECT_ADAPTER_REVIEW_DRAFT_WITH_HUMANIZATION_LAYER
```

Meaning:

- 本專案 Project Adapter 已建立 REVIEW 草稿
- 包含三級 gate、pre-approved 清單、push 詞表、mistake protocol、AI pushback 權、session resume
- Mode A（純治理工具）為目前模式
- protected source 清單為暫定，未來會擴充
- Adapter 本身未 LOCKED
- HARNESS Core 未修改
- 32A-LOCK 未修改
- product implementation 未開始
- Runtime / SDK 未啟動
- 未 commit、未 push

## 21. Boundary Confirmation

本檔是 REVIEW Project Adapter only。

不是：

- Core LOCKED 升級
- Adapter LOCKED 升級
- product implementation 授權
- protected source read 授權
- Mode B 切換授權
- Runtime / SDK 啟動授權
- git commit / push / remote 設定授權
- external reviewer 引入授權
- LOCKED 文件升級授權
