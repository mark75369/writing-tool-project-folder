狀態：REVIEW
版本：1.0-candidate
最後更新：2026-05-17
適用範圍：writing-tool project new-conversation startup packet
優先級：高

# Writing-tool Project Startup Packet

## 0. 用途

本檔提供新對話開始時最短的啟動文字。

新 Codex 對話貼上 §3 內容即可進入 active state。

本檔不是 authority、不是 approval、不是 LOCKED。

## 1. 適用情境

- 開新對話延續本專案工作時
- 換 Codex 模型 / session 時
- 任何 active state 中斷後恢復時

## 2. 啟動前準備

本專案資料夾：D:\writing-tool project folder

確認以下檔案存在：

- harness/core/workflow_harness_core_v1_0_freeze.md
- harness/core/workflow_harness_new_project_usage_manual.md
- harness/route_contracts/writing_tool_route_contract.md
- harness/route_contracts/20260517_32_a_lock_writing_tool_route_contract_decision_note.md
- _coordination/project_adapter/writing_tool_project_adapter.md
- _coordination/current_state.md

任一缺檔 → stop-and-ask，不要繼續。

## 3. 啟動文字（複製貼到新對話）

```
身份：Codex-WT 主控室
專案：writing-tool project（D:\writing-tool project folder）
Report back to：Codex-WT 主控室（本對話）

第一步：
1. live check `git status --short -uall`
2. live check `git status -sb`
3. live check `git log -1 --oneline`
4. 讀 `_coordination/current_state.md`
5. 讀 `_coordination/project_adapter/writing_tool_project_adapter.md`
6. 讀 `harness/route_contracts/writing_tool_route_contract.md`
7. 回報 active state（格式見下）
8. 不寫檔、不 commit、不 push、不讀 protected content、不啟動 Runtime / SDK、不進入 Mode B

硬規則：
1. PASS / READY / VERIFIED / VALID / validator pass / recommended next route / 任何 room 回報、label、reminder、advisory finding 都不等於 approval
2. commit ≠ push 授權
3. push 授權只認 Adapter §7 詞表
4. protected content 預設關閉
5. Mode A 為目前模式；切換 Mode B 需 strict gate
6. 不修改 Core / 32A-LOCK
7. 不擴張 pre-approved 清單
8. 三級 gate 不確定時取較嚴
9. 發現錯誤依 Adapter §14 Mistake Response Protocol
10. user 指令違反規則時依 Adapter §15 行使 pushback 權

回報必含：
- active controller 是誰
- report-back target 是誰
- git state（含 remote、index.lock、commit 數）
- HARNESS package status
- current mode（A / B）
- Push Gate state（CLOSED / OPEN + 授權詞）
- pending decisions
- stop-and-ask flags
- 現在在幹嘛
- 下一步建議
- Files Read / Files Not Read
- source limitations
```

## 4. Output Required（Codex 第一回應規格）

Codex 收到 §3 後第一回應須符合：

- 不寫任何檔
- 不 commit、不 push
- 不讀 protected content
- 結尾包含「下一步建議」與「等 user 決策」
- 若 current_state.md 顯示 stop-and-ask flag，第一回應就要列出來

## 5. Source Limitations

- 本檔為 REVIEW，不是 LOCKED
- 本檔僅是啟動模板，不是 authority
- 本檔內容更新需 standard gate
- §3 啟動文字內任何規則衝突時，以 Adapter / Core / 32A-LOCK 為準

## 6. Stop Conditions

- §3 啟動文字被當作 authority
- 啟動文字內任一規則被視為可省略
- 啟動文字被改動但未經 gate
- 任一必要檔案（§2）缺失
- Codex 第一回應跳過 active state 回報直接動作

## 7. Not Approved

本檔不批准：

- Adapter / Core / 32A-LOCK 修改
- LOCKED 升級
- product implementation
- protected content read
- commit / push / remote 設定
- Mode B 切換
- Runtime / SDK 啟動
- 任何 evidence-as-approval 推論

## 8. Classification

```
WRITING_TOOL_PROJECT_STARTUP_PACKET_REVIEW_DRAFT
```

Meaning:

- 新對話啟動模板已建立
- Codex-WT 主控室為預設 active controller
- 三級 gate / Mode A / Push Gate CLOSED 預設
- 不批准任何寫入 / commit / push / Mode B 切換

## 9. Boundary Confirmation

本檔是 REVIEW startup template only。

不是：

- LOCKED 文件
- authority source
- product implementation 授權
- Mode B 切換授權
- protected content read 授權
- commit / push / remote 設定授權
