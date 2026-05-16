狀態：REVIEW
版本：1.0-candidate
最後更新：2026-05-17
適用範圍：writing-tool project route contract（reference 形式）
優先級：高

# Writing-tool Route Contract（Reference）

## 1. Purpose

本檔是啟用說明書 §5 點名的 canonical `writing_tool_route_contract.md`。

採 reference 形式（依本專案 C5-b 決策）：

- 不重複 32A-LOCK 鎖定的條款內容
- 僅指向 authority source 並補上本專案使用慣例

權威來源：

```
harness/route_contracts/20260517_32_a_lock_writing_tool_route_contract_decision_note.md
```

該檔為 LOCKED；其鎖定條款即本路線邊界。

## 2. Boundary

本檔是 REVIEW reference 檔，不是 authority。

- 不修改 32A-LOCK 任何字
- 不另外鎖定 32A-LOCK 未鎖的條款
- 不擴張 32A-LOCK 邊界
- 32A-LOCK 與本檔內容衝突時，以 32A-LOCK 為準

## 3. Files Referenced

完整讀取以理解本路線：

- harness/route_contracts/20260517_32_a_lock_writing_tool_route_contract_decision_note.md（LOCKED authority）
- harness/core/workflow_harness_core_v1_0_freeze.md（REVIEW Core）
- harness/core/workflow_harness_new_project_usage_manual.md（REVIEW Manual）
- _coordination/project_adapter/writing_tool_project_adapter.md（REVIEW Adapter）

## 4. 引用要點摘要（advisory only）

以下摘要僅供日常引用，權威內容以 32A-LOCK 為準：

- A 路線：以 HARNESS 開發下一份 writing-tool（劇本工具）
- HARNESS 本體當穩定工具，不擴張（除非重大 blocker）
- 新 writing-tool 專案需有自己的 Project Adapter（本專案 Adapter 即為此）
- protected creative content 預設關閉，需 exact read gate
- 人類仍主導 canon / FINAL / LOCKED / Canon Delta / publication
- QA / validator / room reports 只是 evidence，不是 approval
- Runtime / SDK 與本路線分開
- 遠端發佈獨立 gate
- B 路線（用 HARNESS 自己迭代 HARNESS）為延後決定

完整條款請讀 32A-LOCK §6–§13。

## 5. 本專案使用慣例（依 Project Adapter）

- 本專案目前為 Mode A 純治理工具
- Mode B（AI 寫作工具）進入須獨立 strict gate
- 三級 gate（Light / Standard / Strict）依 Adapter §12 操作
- Push Gate 只認 Adapter §7 詞表
- protected source 清單暫定，未來會擴充

## 6. Source Limitations

- 本檔是 REVIEW reference，不是 authority
- 本檔不重複 32A-LOCK 條款內容（依 C5-b）
- 本檔不評估 32A-LOCK 之有效性
- 本檔不擴張路線邊界
- 本檔不能單獨作為產品實作授權

## 7. Stop Conditions

stop-and-ask 條件：

- 本檔內容與 32A-LOCK 衝突（以 32A-LOCK 為準並回報衝突）
- 有人引用本檔摘要當 authority
- 要修改 32A-LOCK 文字
- 要把本檔升級為 LOCKED（須 strict gate）
- 要擴張本檔到 32A-LOCK 未涵蓋的條款

## 8. Not Approved

本檔不批准：

- 32A-LOCK 修改、升級或降級
- 路線邊界擴張
- Mode B 切換
- product code 建立
- protected content read
- commit / push / remote 設定
- Runtime / SDK 啟動
- B 路線啟動

## 9. Classification

```
WRITING_TOOL_ROUTE_CONTRACT_REVIEW_REFERENCE_TO_32A_LOCK
```

Meaning:

- 本路線 contract 以 reference 形式建立
- authority 仍為 32A-LOCK 決定書
- 本檔未鎖定任何新條款
- 本檔未修改任何既有檔
- 本檔僅補上本專案使用慣例與引用要點摘要

## 10. Boundary Confirmation

本檔是 REVIEW reference only。

不是：

- LOCKED 文件
- authority source
- product implementation 授權
- 32A-LOCK 修改授權
- Mode B 切換授權
- 路線擴張授權
- B 路線啟動授權
