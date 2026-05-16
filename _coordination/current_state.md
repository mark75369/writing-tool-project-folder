狀態：REVIEW
版本：1.0-candidate
最後更新：2026-05-17
適用範圍：writing-tool project active state dashboard
優先級：高

# Current State — writing-tool project

## 0. 用途與性質

本檔是 active state operational dashboard。

不是 authority source。
不是 approval。
不是 LOCKED 文件。
更新本檔需 standard gate。

新對話啟動讀本檔 + Project Adapter + route contract，即可取得當前 routing。

## 1. Last Confirmed

| 項目 | 值 |
| --- | --- |
| Last Confirmed By | user（本對話） |
| Last Confirmed At | 2026-05-17 |
| Snapshot Purpose | writing-tool project HARNESS adoption Phase 32A-STARTUP |

## 2. Active Controller / Report-back

| 角色 | 名稱 | 狀態 |
| --- | --- | --- |
| Active Controller | Codex-WT 主控室 | active |
| Official Report-back Target | Codex-WT 主控室（本對話） | active |

generic 名稱不視為有效 routing target。

## 3. Active / Standby / Excluded Rooms

| Room | 狀態 |
| --- | --- |
| 設計室 | reserved，未啟用 |
| 實作室 | reserved，未啟用 |
| Review Room | reserved，未啟用 |
| Validation Room | reserved，未啟用 |
| External Advisory Reviewer | not configured |

啟用任一 room 需 strict gate。

## 4. Project Mode

| 項目 | 值 |
| --- | --- |
| Current Mode | Mode A — 純治理工具 |
| Mode B（AI 寫作工具）狀態 | 未啟用 |
| Mode 切換 gate | Strict |

切換到 Mode B 需獨立 gate 並更新本表。

## 5. Git State

| 項目 | 值 |
| --- | --- |
| Repo 初始化 | 已 git init，無 commit |
| Branch | master |
| Commits | 0 |
| Predefined Remote URL | https://github.com/mark75369/writing-tool-project-folder.git |
| Remote 實際設定 | 未設定 |
| .git/index.lock 殘留 | 無（已確認 .git/ 內無殘留 lock） |
| 最近一次 push | 從未 push |

設定 remote / 處理 index.lock 為 strict gate 動作；Codex 不主動執行。

## 6. HARNESS Files Status

| 檔案 | 狀態 |
| --- | --- |
| harness/core/workflow_harness_core_v1_0_freeze.md | REVIEW（原樣，本專案不改） |
| harness/core/workflow_harness_core_v1_0_export_profile.md | REVIEW（原樣，本專案不改） |
| harness/core/workflow_harness_new_project_usage_manual.md | REVIEW（原樣，本專案不改） |
| harness/core/workflow_harness_tool_package_index.md | REVIEW（原樣，本專案不改） |
| harness/core/啟用說明書.md | REVIEW（原樣，本專案不改） |
| harness/core/writing_tool_project_startup_packet.md | REVIEW（本次新建） |
| harness/route_contracts/20260517_32_a_lock_writing_tool_route_contract_decision_note.md | LOCKED（原樣，本專案不改） |
| harness/route_contracts/writing_tool_route_contract.md | REVIEW（本次新建，reference 32A-LOCK） |
| _coordination/project_adapter/writing_tool_project_adapter.md | REVIEW（本次新建） |
| _coordination/current_state.md | REVIEW（本檔） |

## 7. Protected Sources Summary

完整清單見 Adapter §6。

本檔摘要：

- 本專案外的劇本內容
- 舊專案 game-dialogue-bible 所有 protected content
- 商業客戶資料
- LOCKED 文件 body
- archive/ 內容
- D:\writing-tool project folder 之外的任何路徑

狀態：暫定，未來會擴充。

## 8. Push Gate State

```
Push Gate：CLOSED
```

打開條件：user 明文授權（詞表見 Adapter §7）。
當前授權詞表是否被更新：無。

## 9. Pending Decisions / TBD

| 項目 | 狀態 |
| --- | --- |
| 設計室 / 實作室 / review room / validation room 具體名稱 | TBD |
| External advisory reviewer | not configured |
| protected source 清單擴充（含本專案內子路徑） | TBD，未來會做 |
| Mode B 需求定義 | TBD |
| 第一個 commit | TBD |
| .git/index.lock 清除 | N/A（無殘留） |
| git remote add origin 執行 | 待 commit gate 後另外 gate |
| LOCKED 升級候選 | 暫無 |

## 10. Stop-and-ask Flags（目前生效）

- 任何讀 protected content 的請求
- 任何要 commit / push / remote 設定的請求
- 任何要進入 Mode B 的請求
- 任何要修改 Core / 32A-LOCK 的請求
- 任何要動 .git/ 的請求
- 任何 evidence-as-approval 推論
- 任何要啟用 reserved room 的請求
- 任何 protected source 清單擴張的請求

## 11. Recent Activity Log

| 時間 | 事件 |
| --- | --- |
| 2026-05-17 | HARNESS 5 個 startup 檔讀取完成，active state 回報 |
| 2026-05-17 | 優化計畫提出（B1–B7 預設 + C1/C2/C3/C4/C5/C6 決策請示） |
| 2026-05-17 | user 答覆：C1-b（Codex-WT 主控室）、C2-b（暫定+未來擴充）、C3（雙模式）、C4-a（remote URL 給定）、C5-b（route contract reference 形式）、C6-a（dashboard 預填+TBD） |
| 2026-05-17 | Project Adapter 1.0-candidate 落檔 |
| 2026-05-17 | current_state.md 1.0-candidate 落檔（本檔） |
| 2026-05-17 | writing_tool_route_contract.md 1.0-candidate 落檔 |
| 2026-05-17 | writing_tool_project_startup_packet.md 1.0-candidate 落檔 |

## 12. 異常紀錄 / Anomaly Log

```
2026-05-17  Codex 誤將 git status 暫態 warning「unable to unlink .git/index.lock」
            判讀為永久殘留，寫入 Adapter §7、current_state §5 / §9 / §13；
            重驗 ls .git/ 後確認無殘留；依 Adapter §14 揭露、提案回復、等 user 決定。
            user 授權「全做」，依 standard gate 一次修正 5 處錯誤資訊；
            上輪訊息內「.git/index.lock 存在」相關判斷一併作廢。
```

未來 Codex 犯錯 / user override / 規則衝突均寫入本段。

## 13. Next Recommended Step

```
1. user 審 Adapter / current_state.md / route_contract.md / startup_packet.md 4 個新檔
2. 若 ok，user 明文授權 commit gate（範圍 + message）
3. commit 後保持 Push Gate CLOSED；待 user 明文授權才 push
4. 後續：依需要進入 Mode B 規劃 gate 或補 protected source 清單
```

本段是 advisory，不是 approval。

## 14. Boundary Confirmation

本檔不是：

- authority source
- approval
- LOCKED 文件
- product implementation 授權
- commit / push 授權
- protected source read 授權
- Mode B 切換授權

更新本檔需 standard gate。
