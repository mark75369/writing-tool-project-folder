狀態：REVIEW
版本：1.0-candidate
最後更新：2026-05-16
適用範圍：Workflow Harness new-project usage manual
優先級：高

# Workflow Harness New-project Usage Manual

## 0. Quick Start / 先看這段

如果你只是想在新專案使用這套 HARNESS，先照這 6 步做：

1. 把 Core 視為通用安全規則。
2. 不要直接沿用舊專案的 Adapter。
3. 在新專案建立自己的 Project Adapter。
4. 先列出哪些資料不能亂讀。
5. 選第一條路線：Writing-tool 或 Runtime / SDK。
6. 每次修改後驗證，commit 後停在 Push Gate。

最短理解：

```text
Core = 通用規則
Project Adapter = 新專案自己的接法
Writing-tool route = 劇本工具線
Runtime / SDK route = 執行層線
LOCKED = 驗證後才鎖住的穩定契約
```

新專案第一次不要做這些事：

- 不要讀 protected creative content；
- 不要建立 runtime；
- 不要建立 SDK package；
- 不要建立 automation；
- 不要直接做 frontend / editor / export；
- 不要把 REVIEW 當 LOCKED；
- 不要把 commit 當 push 權限；
- 不要把設計室或實作室回報當 authority。

## 0.1 Who This Manual Is For

這份手冊給三種人看：

| 讀者 | 你要看什麼 |
| --- | --- |
| 新專案主控室 | 先看 Sections 8-15 和 Section 21 startup packet |
| 想做劇本工具的人 | 先看 Section 16 Writing-tool Product Route Start |
| 想串 SDK / runtime 的人 | 先看 Section 17 Runtime / SDK Route Start |

如果你只想快速啟動新專案：

```text
看 Section 8：要用哪些檔案
看 Section 10：第一次啟動順序
看 Section 11：Project Adapter 要填什麼
看 Section 13：protected source 怎麼列
看 Section 21：直接複製 startup packet
```

## 0.2 One Concrete Example

假設你開了一個新 repo：

```text
C:\Projects\new-narrative-tool
```

你不應該把 `game-dialogue-bible` 的規則整包搬過去。

你應該做的是：

1. 複製或引用 HARNESS Core。
2. 複製或引用 export profile。
3. 複製或引用這份 usage manual。
4. 建立新檔：

```text
_coordination/workflow_harness_core/new_narrative_tool_project_adapter.md
```

5. 在 adapter 裡填新專案自己的規則：

```text
這個專案是什麼？
哪些資料不能讀？
主控室叫什麼？
回報要回到哪裡？
commit 後是否可以 push？
設計室 / 實作室的回報能不能當 authority？
```

答案通常是：

```text
設計室 / 實作室回報只能當 supporting evidence。
commit 後不能自動 push。
protected creative content 不能預設讀。
```

## 1. Purpose

This manual explains how to use the Workflow Harness package in a new project.

Plain-language purpose:

```text
你開一個新專案時，不需要重讀 Phase 27-31。

先拿 Core。
再建立新專案自己的 Project Adapter。
再依照產品路線決定是否使用 Writing-tool boundary 或 Runtime / SDK boundary。
最後用小步驗證，確認沒有把專案內容、runtime、SDK、automation、git push 混進 Core。
```

This manual is a usage guide.

It is not an installable package, not schema, not automation, not runtime, not SDK package, and not external adoption approval by itself.

## 2. Boundary

This file is a new-project usage manual for the REVIEW HARNESS package.

It explains adoption order, file roles, adapter creation, route setup, validation, and stop conditions.

It does not:

- promote Core to LOCKED;
- install the HARNESS into another project by itself;
- create a new project adapter by itself;
- create runtime / SDK files;
- create writing-tool product files;
- read protected creative content;
- approve automation;
- approve git push;
- update authority state.

## 3. Files Read

Files read in full for this manual:

- `AGENTS.md`
- `_docs/harness_usage_order_and_agent_mvp_plan.md`
- `_coordination/workflow_notes/20260516_31_c_final_harness_tool_seal_gate_note.md`
- `_coordination/workflow_harness_core/workflow_harness_core_v1_0_freeze.md`
- `_coordination/workflow_harness_core/workflow_harness_core_v1_0_export_profile.md`
- `_coordination/workflow_harness_core/workflow_harness_tool_package_index.md`
- `_coordination/workflow_harness_core/game_dialogue_bible_project_adapter.md`
- `_coordination/workflow_harness_core/historical_excluded_source_boundary.md`
- `_coordination/workflow_harness_core/runtime_sdk_adapter_boundary.md`
- `_coordination/workflow_harness_core/writing_tool_product_route_boundary.md`

Commands / checks used before writing:

- `git status --short -uall`
- `git status -sb`
- `git log -1 --oneline`
- `Test-Path _coordination\workflow_harness_core\workflow_harness_new_project_usage_manual.md`
- `Get-Content -Raw -Encoding UTF8`

Observed repo state before write:

```text
latest commit: d71d978 docs: add phase 31 final harness seal gate
working tree: clean
target file existed before write: no
branch view: master...origin/master
```

## 4. Files Not Read

- protected story / world / character / plot / scene / dialogue body text
- `00_protocol/` body text
- `01_world/` body text
- `03_characters/` body text
- `05_plot/` body text
- `08_dialogue_outputs/` body text
- `archive/` body text
- `_reports/` body text
- `_patches/` body text
- `_prototypes/` body text
- `_coordination/workflow_runtime/` payload bodies
- full `scripts/` implementations
- helper output payloads
- runner result payloads
- transport run payloads
- SDK package files
- schema / registry / database artifacts
- connector implementation files
- automation definitions
- frontend / GUI / editor files
- `_exports/`
- `tasks/`
- `templates/`
- `_projects/` project data
- internal Codex database
- live external room inventory
- live remote repository state beyond local `master...origin/master` branch view

## 5. Source Limitations

- This manual is based on the Phase 31 REVIEW HARNESS package.
- Existing Core remains REVIEW, not LOCKED.
- Existing package files remain REVIEW, not LOCKED.
- This manual does not inspect protected creative content.
- This manual does not read runtime payload bodies.
- This manual does not read helper or validator script implementations.
- This manual does not execute helpers before writing.
- This manual does not validate another project's actual adapter.
- This manual does not prove external adoption.
- A new project must create its own Project Adapter and adoption evidence.

## 6. What The HARNESS Is

The HARNESS is a manual, document-driven workflow control package.

It helps a project keep these boundaries clear:

- who is the active controller;
- what source material is allowed to be read;
- what is current evidence versus stale or excluded source;
- what output is only evidence;
- what needs user confirmation;
- what belongs in portable Core;
- what belongs in a Project Adapter;
- what belongs in product route work;
- what belongs in runtime / SDK work;
- what must never imply git push.

The HARNESS is especially useful when a project uses multiple rooms or roles, such as:

- controller;
- design room;
- implementation room;
- review room;
- validation room;
- external read-only reviewer.

## 7. What The HARNESS Is Not

The HARNESS is not:

- a story Bible;
- a database schema;
- an SDK;
- a runtime;
- an automation system;
- a task runner;
- an external reviewer connector;
- a frontend;
- a writing editor;
- an export pipeline;
- a replacement for human approval;
- a replacement for project-specific policy.

The HARNESS does not decide canon, product quality, final status, LOCKED status, or publication by itself.

## 8. Package Files And Roles

Use the package files in this order:

| order | file | use |
| --- | --- | --- |
| 1 | `workflow_harness_core_v1_0_freeze.md` | portable Core safety invariants |
| 2 | `workflow_harness_core_v1_0_export_profile.md` | adoption checklist and adapter mapping requirements |
| 3 | `workflow_harness_new_project_usage_manual.md` | this manual |
| 4 | `workflow_harness_tool_package_index.md` | package entry point and file order |
| 5 | project-specific adapter | local rules for the new project |
| 6 | `historical_excluded_source_boundary.md` | stale / archived / excluded source handling |
| 7 | `runtime_sdk_adapter_boundary.md` | future runtime / SDK boundary |
| 8 | `writing_tool_product_route_boundary.md` | future writing-tool product boundary |

Important:

```text
Do not copy `game_dialogue_bible_project_adapter.md` as-is into a new project.

Use it only as an example.
Every new project needs its own Project Adapter.
```

## 9. Minimum New-project File Set

Recommended minimum files for a new project:

```text
_coordination/workflow_harness_core/
  workflow_harness_core_v1_0_freeze.md
  workflow_harness_core_v1_0_export_profile.md
  workflow_harness_tool_package_index.md
  workflow_harness_new_project_usage_manual.md
  historical_excluded_source_boundary.md
  runtime_sdk_adapter_boundary.md
  writing_tool_product_route_boundary.md
  <new_project>_project_adapter.md
```

The new project may reference the original files instead of copying them during evaluation.

If the new project wants operational use, it should create a local copy or local package folder so later validation is stable.

## 10. First Startup Flow For A New Project

Use this order when starting a new project:

1. Confirm the project goal.
2. Confirm active controller identity.
3. Confirm report-back target.
4. Read Core.
5. Read export profile.
6. Create or review the new Project Adapter.
7. Identify protected sources.
8. Identify stale, archived, historical, excluded, summary-only, and path-only sources.
9. Decide whether the first route is planning-only, writing-tool route, or runtime / SDK route.
10. Run a read-only adoption check.
11. Only then allow repo writes.
12. Stop at Push Gate after commit.

Do not start with automation, schema, runtime, SDK package, or product implementation.

Practical first conversation shape:

```text
先確認身份。
再確認 git 狀態。
再讀 Core / export profile / usage manual。
再提出 Project Adapter scope。
先不要寫檔。
等使用者確認後才建立 adapter。
```

First output should answer:

- active controller 是誰；
- report-back target 是誰；
- git state；
- HARNESS package status；
- proposed Project Adapter path；
- Files Not Read；
- source limitations；
- stop conditions；
- validation commands；
- Push Gate rule。

## 11. Project Adapter Requirements

Every new project must create its own Project Adapter.

The adapter should include these hooks:

| hook | what to define |
| --- | --- |
| Project Policy Hook | project purpose and highest-priority local rules |
| Room Identity Hook | controller, design room, implementation room, reviewer naming and report-back rules |
| Language / UX Hook | response language, footer format, user-facing style |
| Source Authority Hook | current / stale / archived / excluded / summary-only / path-only handling |
| Confidentiality Hook | private, protected, commercial, or sensitive source rules |
| Git / Push UX Hook | local commit and remote publication rules |
| External Reviewer Hook | how advisory reviewers can be used and what they cannot approve |
| Local Path Hook | project path and path portability warning |
| Current Operational Snapshot Hook | how active identity and report-back target are checked |
| Authority File / Local Governance Hook | local decision logs, snapshots, or authority files if they exist |

Minimum adapter status:

```text
狀態：REVIEW
版本：1.0-candidate
最後更新：
適用範圍：
優先級：高
```

Minimum adapter content:

```text
# <project-name> Project Adapter

## Purpose
這個 adapter 把 HARNESS Core 接到本專案。

## Local Project Policy
本專案的目的、重要規則、不能破壞的品質要求。

## Protected Sources
哪些資料不能預設讀。

## Room Identity
主控室、設計室、實作室、review room 的完整身份規則。

## Report-back Rule
回報要回到哪個對話或哪個 controller。

## Git / Push Rule
commit 後是否停在 Push Gate，以及什麼文字才算 push 授權。

## Not Approved
列出 adapter 本身不能批准的事。
```

## 12. Project Adapter Must Not Do

A Project Adapter must not:

- weaken Core safety invariants;
- treat local examples as universal Core rules;
- grant protected-source read by default;
- grant git push;
- grant automation;
- grant runtime activation;
- grant report acceptance;
- grant LOCKED promotion;
- treat design-room or implementation-room output as authority;
- treat `PASS`, `READY`, or `VERIFIED` as approval.

## 13. Protected-source Setup

Every new project should list protected sources before work starts.

For a game writing project, protected sources may include:

- story Bible;
- worldbuilding;
- character cards;
- plot outlines;
- scene plans;
- dialogue drafts;
- final scripts;
- commercial source materials;
- private notes;
- archives;
- LOCKED documents;
- DEPRECATED documents unless explicitly scoped.

Rule:

```text
Protected source body text is not default input.
It requires an exact user-approved read gate.
```

Example protected-source rule:

```text
未經 exact read gate，不讀：
- 世界觀正文
- 角色卡正文
- 大綱 / 細綱正文
- 場景內容
- 台詞內容
- archive 內容
- LOCKED 文件
```

Good request:

```text
允許讀 03_characters/main/protagonist_voice_card.md，用於本次 voice QA。
```

Bad request:

```text
把角色資料都看一下。
```

Bad request is too broad. Stop and ask for exact scope.

## 14. Room And Report-back Setup

A new project should define full identities for active rooms.

Recommended fields:

- active controller;
- report-back target;
- active design rooms;
- active implementation rooms;
- review rooms;
- validation rooms;
- standby rooms;
- historical rooms;
- stale / excluded rooms;
- external advisory reviewers.

Generic labels are display labels only.

Do not use `主控室`, `設計室`, or `實作室` alone as official routing targets.

## 15. Standard Development Step

For normal development, use this sequence:

1. Live check git status and latest commit.
2. State files to read.
3. State files planned for modification.
4. Read only the approved scope.
5. Stop if LOCKED, protected, stale, or authority conflict appears.
6. Make the smallest useful edit.
7. Run validation.
8. Report modified files, summary, impact, checks, and source limitations.
9. Provide copyable commit info.
10. Stop at Push Gate.

For risky work, insert design-room analysis before writing.

For implementation-heavy work, use implementation-room support only as supporting evidence.

Normal small edit example:

```text
1. git status
2. read AGENTS.md and exact target file
3. say target file to modify
4. edit one file
5. run validator / diff check
6. report modified file and checks
7. give commit command
8. stop at Push Gate
```

Normal planning example:

```text
1. git status
2. read Core / adapter / route boundary
3. do not write files
4. explain route options
5. wait for user confirmation
```

## 16. Writing-tool Product Route Start

Use the Writing-tool route when the project wants to build or operate writing workflows.

Plain-language meaning:

```text
Writing-tool route 是「用這套 HARNESS 做劇本工具」。
它可以處理 Bible Builder、任務包、台詞生成流程、QA、人類裁決。
但它不是 Core。
它不能把產品流程塞回 Core。
```

Allowed first goals:

- project-specific Bible Builder planning;
- dialogue task package planning;
- QA workflow planning;
- human arbitration workflow planning;
- product route contract drafting.

Not allowed from the route boundary alone:

- protected creative-content read;
- task/template creation;
- editor or frontend creation;
- export pipeline creation;
- Canon Delta write-back;
- automatic `FINAL`;
- automatic `LOCKED`.

Recommended first gate:

```text
Writing-tool Route Start Gate:
Read Core, Project Adapter, historical boundary, and Writing-tool Product Route boundary.
Do not read protected creative content.
Do not implement product artifacts until exact write scope is approved.
```

## 17. Runtime / SDK Route Start

Use the Runtime / SDK route when the project wants an execution layer.

Plain-language meaning:

```text
Runtime / SDK route 是「把 HARNESS 接到執行層」。
它可以討論 task packet、return report、preflight、runner、SDK。
但它不是 authority。
它不能自動 dispatch、不能自動 accept report、不能自動 push。
```

Allowed first goals:

- read-only SDK planning;
- runtime boundary mapping;
- task packet shape discussion;
- return report shape discussion;
- preflight-only validation design;
- route contract drafting.

Not allowed from the route boundary alone:

- runtime activation;
- queue activation;
- inbox activation;
- `chain_state` authority state;
- schema creation;
- registry activation;
- database creation;
- connector integration;
- automation;
- helper execution;
- script implementation read;
- SDK package creation.

Recommended first gate:

```text
Runtime / SDK Route Start Gate:
Read Core, Project Adapter, historical boundary, and Runtime / SDK boundary.
Keep all runtime concepts candidate-only.
Do not execute helpers or activate transport.
```

## 18. LOCKED Handling

Do not LOCK everything at adoption time.

Plain-language meaning:

```text
LOCKED 是把穩定規則鎖住。
不是把所有寫完的文件都鎖住。
也不是讓 AI 自動升級狀態。
```

Recommended LOCKED posture:

- keep Core as REVIEW until the project has validated its adapter mapping;
- keep Project Adapter as REVIEW until the project has one successful route start;
- lock only small route contracts after route validation;
- do not lock product behavior before product work exists;
- do not lock runtime behavior before runtime evidence exists.

Good LOCKED candidates later:

- Core, after adoption validation;
- package index, after package validation;
- Writing-tool route contract, after Writing-tool route start validation;
- Runtime / SDK route contract, after Runtime / SDK route start validation.

Bad LOCKED candidates early:

- protected creative content;
- product implementation roadmap;
- SDK framework choice;
- unfinished adapter details;
- broad route plans.

## 19. Validation Commands

For this repo, validate this manual with:

```powershell
python scripts\partial_read_validator_v1.py --file _coordination\workflow_harness_core\workflow_harness_new_project_usage_manual.md
python scripts\partial_read_validator_v1.py --self-check
python scripts\test_partial_read_validator_v1.py
git diff --check
git status --short -uall
```

For a new project, adapt validation to local scripts.

Minimum manual validation checklist:

- required `.md` header exists;
- Core is not treated as LOCKED unless explicitly approved;
- Project Adapter exists or is explicitly pending;
- protected sources are listed;
- Files Not Read are listed;
- source limitations are listed;
- Push Gate rule is explicit;
- runtime / SDK remains inactive unless separately approved;
- writing-tool product work is not mixed into Core;
- stale / archived / excluded sources cannot become authority by existing.

## 20. Stop Conditions

Stop before proceeding if:

- active controller is unclear;
- report-back target is unclear;
- Project Adapter is missing;
- protected sources are unclear;
- requested read scope is broad or implied;
- source freshness is unclear;
- a historical, stale, archived, excluded, summary-only, or path-only source is being used as current authority;
- a protected source would need body-text read without exact approval;
- a LOCKED file would need modification without exact approval;
- runtime, SDK, schema, registry, database, connector, automation, or helper execution is implied;
- writing-tool product implementation is implied without exact write scope;
- commit is requested without exact target clarity;
- remote publication is requested without explicit push authorization.

## 21. Copyable New-project Startup Packet

Use this packet to start a new project controller.

```text
身份：Codex-Phase 1 主控室
狀態：new-project HARNESS adoption candidate
Report back to：Codex-Phase 1 主控室（本對話）

目的：
使用 Workflow Harness package 啟動新專案，但先只做 adoption alignment。

硬規則：
1. 只使用 Phase 命名。
2. `PUSH`、`已 PUSH`、`PUSH 繼續`、`長跑`、`commit` 都不等於授權 git push。
3. 除非使用者明確說「你可以 push / 授權你 git push」，不得執行 git push。
4. PASS / READY / VERIFIED 都只是 evidence，不是 approval。
5. 設計室 / 實作室回報只是 supporting evidence，不是 authority。
6. 不讀 protected creative content，除非有 exact read gate。
7. 不做 automation / dispatch / snapshot / authority update。
8. 不把 REVIEW 當 LOCKED。
9. 不把 Core 當 Project Adapter。
10. 每一步先確認 read scope / write scope / stop conditions / validation commands。

啟動後第一步：
1. live check `git status --short -uall`
2. live check `git status -sb`
3. live check `git log -1 --oneline`
4. 讀 HARNESS Core
5. 讀 export profile
6. 讀 new-project usage manual
7. 提出 Project Adapter exact scope proposal
8. 不直接寫檔，先回報 active state

Approved Read Scope：
- `_coordination/workflow_harness_core/workflow_harness_core_v1_0_freeze.md`
- `_coordination/workflow_harness_core/workflow_harness_core_v1_0_export_profile.md`
- `_coordination/workflow_harness_core/workflow_harness_new_project_usage_manual.md`

Output Required：
- active controller 是誰
- Report back target 是誰
- git state
- HARNESS package status
- proposed Project Adapter path
- Files Not Read
- source limitations
- stop conditions
- validation commands
- Push Gate rule confirmation
- 現在在幹嘛
- 下一步要做的事
- 後續建議
```

## 22. Adoption Checklist

Before treating the HARNESS as adopted in a new project, confirm:

- Core was read;
- export profile was read;
- usage manual was read;
- Project Adapter exists or has exact creation approval;
- protected sources are listed;
- local git / Push Gate rules are listed;
- local room identity rules are listed;
- local report-back rules are listed;
- historical / excluded source handling is listed;
- runtime / SDK route is inactive unless separately approved;
- writing-tool route is not product implementation unless separately approved;
- validation evidence exists;
- user accepted the adoption gate.

Simple adoption pass rule:

```text
如果新專案已經有：
- Core
- export profile
- usage manual
- 自己的 Project Adapter
- protected-source list
- Push Gate rule
- first route selection
- validation evidence

才可以說 HARNESS adoption gate ready for review。

不能說 automatically adopted。
不能說 LOCKED。
不能說 runtime active。
```

## 23. Not Approved

This manual does not approve:

- Core LOCKED promotion;
- Project Adapter LOCKED promotion;
- any file LOCKED promotion;
- Core modification;
- adapter installation without a project-specific gate;
- protected creative-content read;
- protected creative-content modification;
- writing-tool product implementation;
- task/template creation;
- frontend / GUI / editor creation;
- export pipeline creation;
- `_exports/` creation;
- `tasks/` creation;
- `templates/` creation;
- project workspace creation;
- project data write;
- Canon Delta write-back;
- `FINAL` promotion;
- runtime activation;
- SDK package creation;
- SDK framework selection;
- helper execution;
- helper or validator script implementation read;
- helper or validator script modification;
- runtime payload body read;
- runtime artifact modification;
- queue activation;
- inbox activation;
- `chain_state` activation;
- schema creation;
- registry creation or activation;
- database creation;
- connector integration;
- automation;
- report acceptance;
- dispatch;
- HOLD release;
- snapshot update;
- authority update;
- commit proof;
- git push;
- remote publication.

## 24. Classification

```text
PHASE_31E_NEW_PROJECT_USAGE_MANUAL_CREATED_AS_REVIEW_DELIVERABLE
```

Meaning:

- the HARNESS package now has a new-project usage manual;
- new projects have an adoption sequence;
- Project Adapter requirements are explicit;
- protected-source and Push Gate handling are explicit;
- Writing-tool and Runtime / SDK route starts are separated;
- Core and package files remain REVIEW;
- no LOCKED promotion, runtime activation, SDK package, writing-tool implementation, protected-content read, authority update, commit proof, git push, or remote publication is approved.

## 25. Boundary Confirmation

This file is REVIEW usage documentation only.

It is not:

- external adoption approval;
- Core LOCKED promotion;
- adapter installation approval;
- project creation approval;
- writing-tool implementation approval;
- runtime activation approval;
- SDK package approval;
- automation approval;
- protected-source read approval;
- report acceptance;
- dispatch permission;
- HOLD release;
- snapshot update;
- authority update;
- commit proof;
- git push approval;
- remote publication proof.

## 26. Recommended Next Step

Recommended next step:

```text
Run Phase 31F usage-manual validation.
```

31F should check whether this manual is complete enough for a new project to start without reading Phase 27-31 history.

If validation passes, Phase 31 can close.
