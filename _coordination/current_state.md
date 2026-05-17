狀態：REVIEW
版本：1.1-candidate
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
| Repo 初始化 | 已 git init，已建 commit |
| Branch | master，追蹤 origin/master |
| Commits | 5 total；recent: 094907c（F1 audit follow-up iter2）/ 3da3dce（32B + 維護債）/ 479dfac（Codex audit P1/P2/P3 follow-up）/ ba49579（F1 minimal phase launch + audit follow-up）；initial: 58d33a7（claude 重構 HARNESS） |
| Remote URL | https://github.com/mark75369/writing-tool-project-folder.git |
| Remote 實際設定 | ✓ origin |
| .git/index.lock 殘留 | 無（已確認） |
| 最近一次 push | 2026-05-17 user-side（GitHub Desktop），master → origin/master，最新 head: 094907c |

設定 remote / 處理 index.lock 為 strict gate 動作；Codex 不主動執行（依 Adapter §7a）。

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

歷史紀錄：
- 2026-05-17 OPEN（user 在 PowerShell `git push -u origin master`，commit 3da3dce）→ CLOSED
- 2026-05-17 OPEN（user 在 PowerShell push 479dfac audit follow-up）→ CLOSED
- 2026-05-17 OPEN（user 在 PowerShell push ba49579 F1 minimal phase launch）→ CLOSED
- 2026-05-17 OPEN（user 在 GitHub Desktop push 094907c F1 audit follow-up iter2）→ CLOSED

當前授權詞表是否被更新：無。

## 9. Pending Decisions / TBD

| 項目 | 狀態 |
| --- | --- |
| 設計室 / 實作室 / review room / validation room 具體名稱 | TBD |
| External advisory reviewer | not configured；本對話 Codex 一次性 review 為 advisory only |
| protected source 清單擴充（含本專案內子路徑） | TBD，未來會做 |
| Mode B 需求定義 | TBD；F2-A 到 F2-H 決策採 B-2.B extension: {} 方向，但 F2 schema 尚未啟動 |
| 第一個 commit | ✓ 完成（58d33a7） |
| .git/index.lock 清除 | N/A（無殘留） |
| git remote add origin 執行 | ✓ 完成（user-side） |
| 第一次 push | ✓ 完成（user-side，2026-05-17） |
| Adapter §7a Sandbox / Platform Git Boundary 新增 | ✓ 完成（commit 3da3dce 已含） |
| §12 異常紀錄補錯誤 #2 / #3 | ✓ 完成（commit 3da3dce 已含） |
| Adapter §12/§13/§7/§20 與 startup packet 對齊 §7a | ✓ 完成（commit 479dfac，依 Codex audit P1/P2/P3） |
| F1 minimal 設計 | ✓ 已啟動，REVIEW 1.0-candidate（commit ba49579） |
| F1 minimal Codex audit | ✓ 完成（iter2 已 push at 094907c） |
| F2 minimal pre-check dispatch | ✓ 完成（32D 發出，Codex 32E 回） |
| F2 minimal launch（Strict Gate） | 待 user 明文授權；F2-A 到 F2-H pre-launch design decisions finalized as REVIEW evidence |
| F2 schema 完整版設計檔（32F 或同期 workflow note） | 待 F2 strict gate 後啟動 |
| F2 minimal 設計 | 準備就緒；strict gate 授權後啟動 |
| Platform Capability Hook 設計 | 下一個 phase（F1+F2 後） |
| F3 / F4 設計 | 延後 |
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
| 2026-05-17 | user-side 在 PowerShell 完成 git init recovery（毀 config 事件處理） |
| 2026-05-17 | user-side 設定 origin remote、執行首次 git push -u origin master 成功 |
| 2026-05-17 | user 詢問 HARNESS 對 Claude 行為的影響 / token 消耗 / 4 feature 對齊度 / 維護負擔 |
| 2026-05-17 | Claude 提交 Phase 32B 提案 `20260517_32_b_claude_harness_optimization_proposal_for_codex_review.md`（30,258 bytes） |
| 2026-05-17 | Codex 完成 32B review，回覆 5 個 review findings（2 P1 + 3 P2）+ 順序建議 + 32A-LOCK 結論 |
| 2026-05-17 | Claude 對 Codex review 逐條表態並提出本輪維護債設計稿（a/b/c） |
| 2026-05-17 | 維護債 a/b/c 走 standard gate 落實到 current_state.md + Adapter |
| 2026-05-17 | user-side push commit 479dfac（Codex audit P1/P2/P3 follow-up） |
| 2026-05-17 | F1 minimal phase 啟動（user 回 F1-A 到 F1-H 8 項決策） |
| 2026-05-17 | Claude 落檔 F1 schema 設計 + sample action file + index 初始版 |
| 2026-05-17 | user-side push commit ba49579（F1 minimal phase launch + audit follow-up） |
| 2026-05-17 | Codex 完成 F1 audit，回覆 2 P1 / 2 P2 / 2 P3 findings |
| 2026-05-17 | Claude 本輪維護債 follow-up 套用 P1/P2/P3 修正 + dog-food gate_pass action file |
| 2026-05-17 | Codex F1 audit 第二輪（diff-only 模式）回覆，2 P2 + 2 P3 findings，無 P1 |
| 2026-05-17 | Claude 套用 5 個小修正 + dog-food 第三個 action file（F1-audit-followup iter2） |
| 2026-05-17 | user-side push commit 094907c（F1 audit follow-up iter2，via GitHub Desktop） |
| 2026-05-18 | F2 minimal pre-check dispatch packet（32D）產出，由 user 轉交 Codex peer review |
| 2026-05-18 | Codex peer review response（32E）收到 — 11 校核點全答 + 3 refinement + 3 design contribution |
| 2026-05-18 | Active controller §4.2「sync 自然消除」設計判斷修正（advisory correction，未進 §12） |
| 2026-05-18 | User 對 Codex 校核作 4 條 pushback；全採 active controller 子選項建議（#1 4-C / #2 T6a+T6b / #3 S-B / #4 X） |
| 2026-05-18 | Codex peer review 二輪校核 L1-L6 提案；P2 5 條 + P3 4 條修正套用後落檔 |
| 2026-05-18 | L1–L6 落檔提案執行（32D + 32E workflow notes + §11/§9 update + 2 action files + index 手動更新） |

## 12. 異常紀錄 / Anomaly Log

```
2026-05-17  Codex 誤將 git status 暫態 warning「unable to unlink .git/index.lock」
            判讀為永久殘留，寫入 Adapter §7、current_state §5 / §9 / §13；
            重驗 ls .git/ 後確認無殘留；依 Adapter §14 揭露、提案回復、等 user 決定。
            user 授權「全做」，依 standard gate 一次修正 5 處錯誤資訊；
            上輪訊息內「.git/index.lock 存在」相關判斷一併作廢。

2026-05-17  #2 Codex 從 sandbox 執行 git remote add origin <url>，
            atomic rename 跨 sandbox-Windows mount 失敗，
            導致 .git/config 被覆寫為 216 bytes null bytes、.git/config.lock 殘留 0 bytes，
            git 全面失效（fatal: bad config line 1 in file .git/config）。

            user 在 Windows PowerShell 執行：
              Remove-Item .git\config.lock -Force -ErrorAction SilentlyContinue
              Remove-Item .git\config -Force
              git init
            重建 default config 後恢復；commit / refs / objects / logs 全部完好。

            依 Adapter §15 行使 pushback：
              本平台（Claude Cowork sandbox）對 Windows-mounted .git/ 寫入不可靠，
              所有 git 寫入改為 user-side 在 Windows PowerShell 執行。

            根因（依 Codex 32B review 重寫）：
              平台 / 工具輸出沒有 provenance 與 reliability tiering，
              加上 atomic rename 跨 mount 邊界這個高風險動作缺乏 platform blacklist。

            衍生規則建議：Adapter §7a「Sandbox / Platform Git Boundary」（本輪 standard gate 落實）。

2026-05-17  #3 Codex 從 sandbox 執行 git status，把回傳的 stale "M modified" 狀態當真，
            推論 working tree ≠ HEAD、提出「stat cache 卡住」假說、建議
            git update-index --really-refresh 等修復路徑。

            user 在 Windows PowerShell 執行 git hash-object 比對：
              working tree SHA = HEAD SHA = ab48bce... / 4e7cb50...
            揭穿 stale 視圖；A-F 修正其實已於 commit 58d33a7 內。

            純訊息層作廢，無檔案修正動作。

            根因（依 Codex 32B review 重寫）：
              重要 Git claim 沒有跨工具獨立驗證路徑；
              sandbox-git 對 .git/ 的視圖被當 single source of truth。

            衍生規則建議：
              Adapter §7a 邊界擴大到「禁止從 sandbox 跑任何 git 指令（含 read-only）」；
              未來 F1 schema 內 tool_provenance 欄位應強制標記跨平台高風險操作的雙路徑驗證需求。
```

未來 Codex 犯錯 / user override / 規則衝突均寫入本段。

## 13. Next Recommended Step

```
1. user 審本輪 F1 audit follow-up（current_state §5/§8/§9/§11/§13 + F1 schema §6/§9/§14 + Adapter §0 + index）
2. 若 ok，user-side commit + push
3. 後續路徑（依 Codex 順序）：F1 minimal 觀察期 → F2 minimal → Platform Capability Hook → F3 → F4
4. F2 / 後續 phase 每一個都需獨立啟動 gate；F1 觀察期 = 累積幾個真實 action file 看 schema 是否實用
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
