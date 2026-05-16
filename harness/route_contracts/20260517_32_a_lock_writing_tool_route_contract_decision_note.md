狀態：LOCKED
版本：1.0
最後更新：2026-05-17
適用範圍：Phase 32A-LOCK Writing-tool Route Contract Decision
優先級：高

# Phase 32A-LOCK Writing-tool Route Contract Decision Note

## 1. Purpose

Phase 32A-LOCK records the Writing-tool route contract boundary decision.

Plain-language purpose:

```text
32A-LOCK 只鎖「劇本工具路線邊界」。

它確認：
- A 路線可以使用 HARNESS 開發下一份劇本工具；
- HARNESS 本體先視為穩定工具；
- 沒有重大阻塞時，不修改 HARNESS；
- 32A-LOCK 後允許開新的 writing-tool project folder；
- 新資料夾由使用者手動建立；
- Codex 後續負責寫新專案啟動文件 / startup packet；
- protected creative content 仍然不得預設讀；
- product implementation 要等新專案 gate。

32A-LOCK 不建立新資料夾。
32A-LOCK 不建立 adapter。
32A-LOCK 不讀 protected creative content。
32A-LOCK 不開始產品實作。
32A-LOCK 不啟動 Runtime / SDK。
32A-LOCK 不 git push。
```

## 2. Boundary

32A-LOCK is a route-boundary decision note.

It locks the Writing-tool route contract boundary by reference to the validated 32A-5 route contract draft.

It does not edit the 32A-5 source file in this step.

It does not lock Core, Project Adapter, future folder layout, future adapter file content, product implementation, protected creative content, Runtime / SDK behavior, schema, registry, database, automation, git push, or remote publication.

## 3. Files Read

Files read in full for 32A-LOCK:

- `AGENTS.md`
- `_coordination/workflow_notes/20260517_32_a_3_future_writing_tool_project_folder_spec_note.md`
- `_coordination/workflow_notes/20260517_32_a_4_future_writing_tool_project_adapter_spec_note.md`
- `_coordination/workflow_notes/20260517_32_a_5_writing_tool_route_contract_draft_note.md`
- `_coordination/workflow_notes/20260517_32_a_6_writing_tool_route_contract_validation_note.md`
- `_coordination/workflow_harness_core/workflow_harness_core_v1_0_freeze.md`
- `_coordination/workflow_harness_core/workflow_harness_new_project_usage_manual.md`
- `_coordination/workflow_harness_core/game_dialogue_bible_project_adapter.md`
- `_coordination/workflow_harness_core/writing_tool_product_route_boundary.md`

Commands / checks used before writing:

- `git status --short -uall`
- `git status -sb`
- `git log -1 --oneline`
- `Test-Path _coordination\workflow_notes\20260517_32_a_lock_writing_tool_route_contract_decision_note.md`
- `Get-Content -Raw -Encoding UTF8`

Observed repo state before write:

```text
latest commit: 9441e0b docs: add phase 32 writing tool route contract validation
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
- external writing-tool project folder
- external SDK / runtime project folder
- future writing-tool Project Adapter file
- internal Codex database
- live external room inventory
- live remote repository state beyond local `master...origin/master` branch view

## 5. Source Limitations

- 32A-LOCK is a route-boundary decision note, not product implementation.
- 32A-LOCK relies on 32A-6 validation evidence.
- 32A-LOCK locks the 32A-5 route contract boundary by reference, without editing the 32A-5 file in this step.
- 32A-LOCK does not inspect protected creative content.
- 32A-LOCK does not inspect or create an external product folder.
- 32A-LOCK does not create or validate a future adapter file.
- 32A-LOCK does not test product code.
- 32A-LOCK does not test future project adoption.
- 32A-LOCK does not read runtime payload bodies.
- 32A-LOCK does not read helper or validator script implementations.
- Existing Core remains REVIEW, not LOCKED.
- Existing Project Adapter remains REVIEW, not LOCKED.
- Existing Writing-tool Product Route boundary remains REVIEW, not LOCKED.
- Validation output remains evidence only.

## 6. LOCK Target

32A-LOCK target:

```text
_coordination/workflow_notes/20260517_32_a_5_writing_tool_route_contract_draft_note.md
```

LOCK scope:

```text
Only the route contract boundary clauses validated by 32A-6 are locked as the Phase 32A Writing-tool route boundary.
```

This locks the following boundary decisions:

- Writing-tool route is product behavior, not Core;
- future writing-tool project needs its own Project Adapter;
- future writing-tool product work happens in a separate product folder after 32A-LOCK;
- the new product folder is created manually by the user;
- protected creative content requires exact read gate;
- human decisions remain required for canon, `FINAL`, `LOCKED`, Canon Delta, and publication;
- QA / validator / room reports are evidence only;
- Runtime / SDK remains separate until 32B or later;
- remote publication remains separately gated.

This does not lock:

- actual product implementation;
- future folder layout as final architecture;
- future adapter file content;
- UI / editor;
- task templates;
- export pipeline;
- sample content;
- protected creative content;
- SDK framework;
- automation;
- database;
- registry;
- future folder creation command.

## 7. A Route Decision

32A-LOCK records the A route decision:

```text
A route uses the HARNESS to develop the next writing-tool project.
```

Meaning:

- the HARNESS is used as the development governance layer for the next tool;
- the next writing-tool project starts after the user manually creates the new folder;
- Codex should prepare a new-project startup file / startup packet for that folder;
- product work should happen in the new project context, not inside the current HARNESS source repo by default;
- protected creative content remains closed by default.

## 8. HARNESS Stability Rule

32A-LOCK records this HARNESS stability rule:

```text
The HARNESS is treated as stable for A route work unless a major blocker appears.
```

Meaning:

- A route should use the current HARNESS instead of continuing to expand it;
- ordinary product needs should be handled in the future writing-tool project;
- HARNESS changes should be reserved for major blockers, portability failures, or route-boundary contradictions;
- minor product preferences should not reopen HARNESS Core or Phase 32A boundaries.

This does not prevent later B route work.

It only prevents A route from turning every product issue into HARNESS modification.

## 9. B Route Deferred Decision

32A-LOCK records the B route as deferred:

```text
B route remains future HARNESS optimization / iteration discussion.
```

The deferred B route question is:

```text
Should HARNESS be iterated by using the HARNESS itself, or should it be directly refactored / optimized?
```

This note does not decide that question.

B route remains outside 32A-LOCK.

## 10. Manual Folder Creation Rule

32A-LOCK records this folder rule:

```text
After 32A-LOCK, opening a new writing-tool project folder is allowed, but the user creates that folder manually.
```

Codex must not:

- create the folder automatically;
- choose the final folder path without user confirmation;
- copy protected creative content into it;
- copy this whole repo into it;
- install `game_dialogue_bible_project_adapter.md` as-is;
- create product code before the new project gate.

Codex may later:

- write a startup file / startup packet for the new project;
- provide copy-ready bootstrap instructions;
- help validate the new project's Project Adapter after exact scope confirmation.

## 11. New-project Startup File Rule

32A-LOCK records this next deliverable:

```text
Codex should write a new-project startup file for the next writing-tool project.
```

The startup file should include:

- active controller identity placeholder;
- report-back target placeholder;
- HARNESS package status;
- A route purpose;
- manual folder creation assumption;
- exact first read scope;
- future Project Adapter scope;
- protected-source rule;
- Files Not Read;
- source limitations;
- stop conditions;
- validation commands;
- Push Gate rule;
- fixed footer.

The startup file should not:

- create the folder;
- create the adapter;
- read protected creative content;
- start product implementation;
- activate Runtime / SDK;
- create automation;
- grant git push.

## 12. Not Approved

32A-LOCK does not approve:

- Core LOCKED promotion;
- Project Adapter LOCKED promotion;
- future Project Adapter LOCKED promotion;
- product implementation LOCKED promotion;
- Core modification;
- current 32A-5 source-file edit;
- adapter file creation;
- adapter installation into another project;
- automatic external adoption;
- protected creative-content read;
- protected creative-content modification;
- writing-tool product implementation;
- task/template creation;
- frontend / GUI / editor creation;
- export pipeline creation;
- `_exports/` creation;
- `tasks/` creation;
- `templates/` creation;
- project workspace creation by Codex;
- writing-tool project folder creation by Codex;
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
- commit proof for this 32A-LOCK note;
- git push;
- remote publication.

## 13. Stop Conditions

Stop before proceeding if a later step attempts:

- treating this note as permission for Codex to create the new folder;
- creating the future adapter file before exact startup-file / adapter gate;
- copying `game_dialogue_bible_project_adapter.md` as-is;
- copying protected creative content;
- reading protected creative content without exact approval;
- treating 32A-LOCK as product implementation approval;
- treating 32A-LOCK as Core LOCKED approval;
- treating 32A-LOCK as Runtime / SDK approval;
- creating product code;
- creating task templates;
- creating frontend / GUI / editor files;
- creating export pipeline files;
- creating sample data from protected content;
- modifying Core;
- executing helpers beyond validation commands;
- reading or editing script implementations;
- creating schema / registry / database / connector / automation;
- accepting reports automatically;
- dispatching;
- updating snapshot or authority state;
- claiming commit proof without actual commit;
- running git push or remote publication without explicit remote-publication approval.

## 14. Validation Commands

Recommended validation commands after writing this file:

```powershell
python scripts\partial_read_validator_v1.py --file _coordination\workflow_notes\20260517_32_a_lock_writing_tool_route_contract_decision_note.md
python scripts\partial_read_validator_v1.py --self-check
python scripts\test_partial_read_validator_v1.py
git diff --check
git status --short -uall
```

Expected interpretation:

- validator result is evidence only;
- self-check result is evidence only;
- regression result is evidence only;
- git diff check result is evidence only;
- clean status is evidence only;
- none of these results creates Core LOCKED, Project Adapter LOCKED, product implementation approval, folder creation by Codex, protected-source read approval, Runtime / SDK activation, report acceptance, dispatch, HOLD release, snapshot update, authority update, automation approval, commit proof, push authorization, or remote publication proof.

## 15. Commit Gate Candidate

If only this Phase 32A-LOCK note is created, recommended commit message:

```text
docs: add phase 32 writing tool route lock decision
```

Recommended commit scope:

```text
_coordination/workflow_notes/20260517_32_a_lock_writing_tool_route_contract_decision_note.md
```

Commit still does not grant remote publication permission.

## 16. Classification

```text
PHASE_32A_LOCK_WRITING_TOOL_ROUTE_BOUNDARY_LOCKED_FOR_A_ROUTE_STARTUP_FILE
```

Meaning:

- Phase 32A Writing-tool route boundary is locked by this decision note;
- A route may use the HARNESS to develop the next writing-tool project;
- the HARNESS should not be modified during A route unless a major blocker appears;
- B route remains a deferred HARNESS optimization discussion;
- the user may manually create a new writing-tool project folder after 32A-LOCK;
- Codex should next write a new-project startup file / startup packet;
- protected creative content remains unread and closed by default;
- product implementation has not started;
- Codex has not created the product folder;
- no Core LOCKED promotion, product folder creation by Codex, adapter installation, Runtime / SDK activation, authority update, commit proof, git push, or remote publication is approved.

## 17. Boundary Confirmation

This note is a LOCKED route-boundary decision note for Phase 32A only.

It is not:

- Core LOCKED promotion;
- Project Adapter LOCKED promotion;
- future adapter file creation approval;
- future adapter installation approval;
- product implementation approval;
- new product folder creation by Codex;
- protected-source read approval;
- task/template creation approval;
- frontend / editor / export approval;
- Canon Delta write-back approval;
- Runtime / SDK activation approval;
- SDK package approval;
- external adoption approval;
- report acceptance;
- dispatch permission;
- HOLD release;
- snapshot update;
- authority update;
- commit proof;
- git push approval;
- remote publication proof.

## 18. Recommended Next Step

Recommended next step after this note is reviewed and committed:

```text
Proceed to Phase 32A-STARTUP-FILE: write the next writing-tool project startup file / startup packet.
```

That startup file should prepare the next project for A route use.

It should not create the new folder, install the adapter, read protected creative content, create product artifacts, or activate Runtime / SDK.
