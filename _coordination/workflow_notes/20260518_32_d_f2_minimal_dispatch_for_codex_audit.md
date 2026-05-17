狀態：REVIEW
版本：1.0-candidate
事件日期：2026-05-17 (產出) / 2026-05-18 (落檔)
落檔日期：2026-05-18
最後更新：2026-05-18
適用範圍：F2 minimal phase 啟動前校核 dispatch packet（manual dispatch / advisory packet）
優先級：高

# Phase 32D — F2 Minimal 啟動前校核 Dispatch（for Codex）

## 0. Dispatch Metadata

- 來源:writing-tool project active controller「Codex-WT 主控室」（Claude Cowork session）
- 對象:Codex（任一獨立 session — fresh / peer / cli 皆可）
- 性質:Advisory dispatch；**不是** authority / approval / strict gate 啟動 / room activation
- 期望回應:校核 + 設計建議（diff-only / 校核-only mode OK）
- 不被授權:修改 HARNESS Core、32A-LOCK、任何 LOCKED 文件、直接落檔到 writing-tool project

## 1. Project Context Snapshot

### 1.1 Active State（~2026-05-17 末）

- Phase 32A-STARTUP:完成
- Phase 32B Claude proposal + Codex P1/P2/P3 audit:完成
- Phase 32C F1 minimal schema:完成；iter2 audit follow-up pushed at commit `094907c`；進入觀察期
- Phase 32D F2 minimal:**本 dispatch 的目標 phase**；啟動前討論中

### 1.2 Project Mode

Mode A 純治理工具。Mode B（AI 寫作工具）未啟用（Adapter §2）。

### 1.3 Active Controller / Routing

- Active controller:Codex-WT 主控室（本 dispatch 發送 session）
- Report-back target:同上
- 本 dispatch 屬 outgoing peer 校核，不是 controller succession

### 1.4 Files Codex 應已讀（路徑；本 dispatch 不重述其內容）

- `harness/core/workflow_harness_core_v1_0_freeze.md`（REVIEW Core；尤其 §9 Role Handoff Abstract Flow、§21 Adapter Hook Requirements）
- `harness/route_contracts/20260517_32_a_lock_writing_tool_route_contract_decision_note.md`（LOCKED；尤其 §8 HARNESS 穩定原則）
- `_coordination/project_adapter/writing_tool_project_adapter.md`（REVIEW Adapter；§2 mode、§3 rooms、§7a Sandbox Git Boundary、§12 三級 gate）
- `_coordination/workflow_notes/20260517_32_b_claude_harness_optimization_proposal_for_codex_review.md`（特別 §9 F2 落地建議、§9.6 校核點）
- `_coordination/workflow_notes/20260517_32_c_f1_minimal_schema_design.md`（F1 minimal schema；本 dispatch §4.2 涉及整合）

若收件 Codex 缺以上檔案存取，請 user 補上必要片段。

## 2. Peer Reviewer Baseline（老對話建議 A1–A5 + β-2）

另一 Claude / Codex session 對 5 個 F2 啟動問題給出初步建議:

| Q | 問題 | Baseline 答 |
| --- | --- | --- |
| Q1 | 下一項:F1 obs 繼續 vs F2 啟動討論 | **乙**（F2 啟動討論） |
| Q2 | F2 與 F1 obs 平行（Q）或先後（P） | **Q**（平行） |
| Q3 | F2 minimal scope:α（1 type）/ β（4 types）/ γ（full integration） | **β** |
| Q4 | F2 限定 Adapter + actions/ 層、不動 Core | **是** |
| Q5 | 先 dispatch §9.6 校核再啟動 strict gate | **是** |

老對話額外提 β-2 維度:

> F2 schema 應預留 Mode B / 跨專案 handoff 欄位，避免將來 retrofit。
> 具體建議:加 `cross_project_ref` / `creative_content_handoff` 等欄位。

## 3. §9.6 4 個校核點（32B 提案原文，未變動）

```
1. 校核 handoff schema 是否完整（特別是 First Verification 欄位設計）
2. 評估 controller_change vs ai_platform_switch 區分是否必要
3. 評估 Handoff Note 與 current_state.md §2 的同步機制
4. HARNESS Core §9 Role Handoff Abstract Flow 是否需要對應更新
   （會違反 32A-LOCK §8「HARNESS 穩定」原則嗎？）
```

## 4. Active Controller 的觀察與 Push Back 清單

以下是本 session（Codex-WT 主控室）對 baseline 的補充與質疑，請 Codex 一併校核。

### 4.1 handoff_type 互斥性問題（§9.6 #2 範圍）

老對話 A3 β 採 32B §9.3 4 種 handoff_type:

```
session_resume     | 同 controller / 新對話
controller_change  | 換 controller
ai_platform_switch | 跨 AI 平台
phase_transition   | phase 邊界
```

**問題**:`controller_change` 與 `ai_platform_switch` 不互斥。情境矩陣:

| 情境 | controller_change? | ai_platform_switch? |
| --- | --- | --- |
| Claude (Cowork) → Claude (新對話) 同身份 | NO（純 session_resume） | NO |
| Claude → Codex CLI 同身份 | 不明 | YES |
| Claude 主控室 → Claude-2 主控室 同平台 | YES | NO |
| Claude 主控室 → Codex 主控室 跨平台 | **YES + YES**（同時觸發） | 同左 |

最後一列同時觸發兩 type。4 種 enum 互斥假設破裂。

可能解 path:

- **path 1**:`handoff_type` 改 array，允許多選
- **path 2**:合併 `controller_change` + `ai_platform_switch` 為單一 `subject_change`，把 platform 細節拆到獨立欄位 `platform_from` / `platform_to`
- **path 3**:維持 4 種互斥，跨平台 + 跨身份走 priority 規則

**Active controller 傾向 path 2**:schema 簡潔；platform 細節本來就會在未來 Platform Capability Hook phase 出現，不該在 type enum 裡 hard-code。

**請 Codex**:path 1/2/3 哪一個？或第 4 條路？

### 4.2 F1 / F2 Schema 重疊風險

F1 schema（32C）§5 type enum **已包含** `handoff`:

```
| `handoff` | controller 交接（與 F2 整合） |
```

32B 提案 §9.2 同時提議 F2 開**獨立 folder** `_coordination/handoffs/`。

雙設計矛盾:

- 若一個 handoff event 同時寫進 `actions/` 與 `handoffs/` → 兩處同步債
- 若只寫一處 → 另一處設計浪費

可能整合方式:

- **整合-1**:handoff **只在 `actions/`**，F2 schema 描述 `type=handoff` 的特化 frontmatter 欄位（在 F1 21 欄位之上補 Preserved / Reset / First Verification 等）。**不**新建 `handoffs/` folder
- **整合-2**:handoff **只在 `handoffs/`**，F1 type 枚舉移除 `handoff`
- **整合-3**:兩處並存但角色分立 — `actions/` 記事件本身、`handoffs/` 記詳細 note（兩檔互引用）

**Active controller 傾向整合-1**:

- F1 schema 已預留 `type=handoff`
- 避免新建 folder
- 自然解決 §9.6 #3 同步問題（同源資料 = no sync needed）

**但這需要 explicitly 推翻 32B §9.2 folder 結構提議**。

**請 Codex**:整合-1/2/3 哪一個？

### 4.3 β-2 Mode B 預留方式

老對話建議（B-2.A）:F2 schema 加 `cross_project_ref` / `creative_content_handoff` 具體欄位。

**問題**:Mode B 規格目前**空白**（Adapter §2 只有名稱定義，任何子欄位都沒設計）。在 Mode B 規格未定義狀態下預留具體欄位 = 在猜未來的 schema。

可能方式:

| 方式 | 內容 | Trade-off |
| --- | --- | --- |
| **B-2.A**（老對話） | 加 `cross_project_ref` / `creative_content_handoff` 具體欄位 | 猜錯 → 將來這兩欄位浪費 / 改名 |
| **B-2.B**（本 session） | 加單一 `extension: {}` namespace（dict 值），Mode B 將來在 namespace 內填具體欄位 | 預留接口、不預設內容；`schema_version` 跨版相容；猜錯成本 ≈ 零 |
| **B-2.C** | 完全不預留，待 Mode B alignment 啟動時走 supersede 鏈 | 簡單；retrofit 成本承擔給未來 |

**Active controller 傾向 B-2.B**（extension namespace）:對 Mode B 不假設，保留擴展能力。

**邊界 confirm 請 Codex 同意 / 否決**:β-2 任何版本**不**觸發 Mode A → B 切換（Adapter §2 Mode B 觸發條件 = 「指定產品形態 / 建 product code / template / frontend / export」；schema 欄位保留**不在**觸發條件內）。此邊界若同意，應寫進 F2 schema 設計檔 boundary 段。

**請 Codex**:B-2.A / B / C 哪一個？邊界 confirm 對嗎？

### 4.4 A2 平行設計時的 Hard Rule 偵測機制

老對話 Q 路線 hard rule:

> F2 設計過程中發現 F1 schema 不夠用 → 必須先補 F1 再繼續 F2，不能挾持 F2 為由偷改 F1。

老對話沒給偵測機制。Active controller 建議:

| 觸發點 | 條件 |
| --- | --- |
| **T1** | F2 schema 設計需新增 F1 type 才能 cover |
| **T2** | F2 schema frontmatter 與 F1 重複度 > 80%（表示應合併不是分立） |
| **T3** | §9.6 dispatch Codex 回應涉及 F1 schema（Codex 答案連動 F1） |

觸發後流程:F2 設計**暫停** → F1 走 supersede 鏈修（F1 schema §11 已備）→ 恢復 F2。

**請 Codex**:T1/T2/T3 是否充分？漏什麼觸發點？

### 4.5 A4 不動 Core 的 Secondary Nuance

A4 是（Adapter only）Active controller 完全同意，強化理由:Core §21 Adapter Hook Requirements 規定「Adapter 落地 Core 抽象條款」是合法演進路徑。F2 把 Core §9 抽象具體化在 Adapter 層完全符合設計意圖。

但有一個 secondary observation:

> F2 minimal 落地後，若實證證明 Core §9 抽象條款**用詞需要對齊**才能 cross-project portable（例如 Core §9 用 "role handoff"、F2 用 "handoff_type"，兩邊用詞分歧），未來可能需要 minor wording 對齊。

這**不是現在的問題**，是 F2 LOCKED 升級時才浮現。

**請 Codex**:建議用詞對齊現在做（pre-emptive）？還是留給未來 LOCKED 升級評估時處理？

### 4.6 §9.6 Dispatch Target 設計

本 dispatch 即為 §9.6 dispatch 之具體實現。Dispatch target 選擇本身影響後續流程:

- **D-1**:dispatch 給老對話 peer reviewer（已知 32B 脈絡）
- **D-2**:active session 自己回答（self-review，獨立性弱）
- **D-3**:fresh Codex（最 independent，需 packet 自含 context — 即本 dispatch 設計目標）
- **D-4**:不 dispatch，active session 直接做 F2 設計，§9.6 邊做邊答

User 的選擇影響本 dispatch 處理流:

| Target | 後續 |
| --- | --- |
| D-1 / D-3 | Codex 回應 → active session 整合 → Strict Gate 啟動 F2 |
| D-2 | active session 自批判 → Standard Gate 啟動 F2（獨立性弱） |
| D-4 | 跳校核 → 直接 Strict Gate 啟動 F2 |

**請 Codex（若為 D-1 或 D-3 收件方）**:你的角色是 advisory peer reviewer，**不是 authority**。回應為 evidence，不是 approval。

### 4.7 Cadence / Token 預算

F2 minimal 完整 cadence 預估（參考 F1 minimal ~6 小時 / 4 個 commits 的實績）:

| 階段 | 預估 token |
| --- | --- |
| §9.6 dispatch + Codex 回應 | ~3–5K |
| F2 minimal schema 設計初版 | ~10–15K |
| Codex audit | ~5–10K |
| Iter1 follow-up | ~5–8K |
| 可能 iter2 | ~5–8K |
| **總估** | **~30–50K** |

**請 Codex**:此估計是否合理？是否需要分段 dispatch / 分散到多 session？

## 5. 校核 / 設計請求清單彙整

| # | 主題 | Active controller 傾向 | 請 Codex 確認 / 否決 / 提替代 |
| --- | --- | --- | --- |
| 1 | A1 乙（F2 啟動討論） | 同意 | 同意 / 否 |
| 2 | A2 Q（平行）+ Hard rule 偵測 T1/T2/T3 | 同意 + 加偵測 | 偵測機制充分？ |
| 3 | A3 + §9.6 #2 handoff_type 互斥 | path 2（合併 + platform 拆獨立） | path 1/2/3/4？ |
| 4 | A4 不動 Core + §9 用詞對齊 | 同意 + 用詞對齊留未來 | 同意？對齊時點？ |
| 5 | A5 §9.6 dispatch 必要 | 同意（本 dispatch 即實現） | 同意？ |
| 6 | β-2 Mode B 預留 | B-2.B（extension namespace） | A/B/C？Mode 切換邊界 confirm？ |
| 7 | F1/F2 schema 整合 | 整合-1（handoff 留 `actions/`） | 1/2/3？ |
| 8 | F2 cadence 預估 | 單 session 30–50K | 合理？分段 dispatch？ |
| 9 | §9.6 #1 First Verification 欄位設計 | （未提傾向；交 Codex） | 需要哪些必填子欄位？ |
| 10 | §9.6 #3 與 current_state.md §2 同步 | 整合-1 自然消除（同源） | 同意？或還是需要 sync rule？ |
| 11 | §9.6 #4 Core §9 是否需更新 | 同 #4 答；不需現在動 | confirm？ |

> 落檔註記:§5 表第 10 列 active controller 原傾向「自然消除」被 32E Codex 校核 R3 修正為「需要 manual sync declaration」，新增必填欄位 `current_state_sync`。屬 advisory correction，未進 §12 Anomaly Log。

## 6. Boundary

本 dispatch **不是**:

- F2 minimal strict gate 啟動授權
- HARNESS Core 修改授權
- 32A-LOCK 修改授權
- LOCKED 升級授權
- Mode B 切換授權
- product code / template / frontend / export 建立授權
- commit / push / remote 設定授權
- protected creative content read 授權
- Runtime / SDK 啟動授權
- Codex authority 升級
- room activation（本 dispatch 為 manual advisory packet，不啟動任何 reserved room）

本 dispatch **是**:

- Advisory dispatch 請求 Codex 校核設計考量
- 未來 F2 minimal strict gate 啟動的 evidence input
- 不取代 user 在 strict gate 內的明文授權

## 7. Stop Conditions（Codex 收件方應遵守）

- 本 dispatch 被當 authority → stop, 通知 user
- 本 dispatch 被當 F2 啟動授權 → stop, 通知 user
- Codex 回應被當 approval → stop, 通知 user
- 任何規則建議被自動套用而未過 standard gate → stop, 通知 user

## 8. 期望回應格式（請 Codex 採以下任一）

- **Diff-only mode**:對 §4 每個 subsection 與 §5 表每列給「同意 / 修正路徑 / 否決 + 理由」
- **校核-only mode**:對 §3 §9.6 4 校核點 + §4 觀察清單給 evidence-based 評估
- **設計協作 mode**:額外提建議方案（path 4 / 新 type / 新 trigger 等）

回應落地路徑:user 將 Codex 回應 paste 回 writing-tool project active session（Codex-WT 主控室），由 active controller 整合進 F2 minimal schema 設計。

## 9. Classification

```
PHASE_32D_F2_MINIMAL_LAUNCH_PRECHECK_DISPATCH_FOR_CODEX_AUDIT
```

意義:

- F2 minimal 啟動前的校核 dispatch
- 11 個校核 / 設計請求項目
- baseline 為老對話 peer reviewer 建議（A1–A5 + β-2）
- active controller push back 7 條
- 不批准任何實作 / strict gate 啟動 / Core 修改

## 10. Boundary Confirmation

本檔是 advisory dispatch only。不是:

- F2 minimal LOCKED schema
- F2 minimal strict gate 啟動授權
- HARNESS Core 修改授權
- 32A-LOCK 修改授權
- Mode B 切換授權
- product implementation 授權
- Codex authority 升級
- room activation（本 dispatch 為 manual advisory packet，不啟動任何 reserved room）

任何 Codex 回應均為 advisory evidence，最終 F2 啟動仍需 user 在 strict gate 中明文授權。
