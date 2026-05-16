狀態：REVIEW
版本：1.0-candidate
最後更新：2026-05-16
適用範圍：Workflow Harness tool boundary package
優先級：高

# Workflow Harness Tool Package Index

## 1. Purpose

This file is the entry point for the Phase 31 HARNESS split package.

The package goal is practical:

```text
Core stays portable.
Project-local rules move to adapter.
Historical / excluded sources stay contained.
Runtime / SDK remains a boundary, not runtime activation.
Writing-tool product route stays outside Core.
```

This package is a REVIEW deliverable candidate. It is not LOCKED.

## 2. Boundary

This file is a package index.

It lists the HARNESS split deliverable files and their use order.

It does not replace the package files.

It does not approve LOCKED promotion, runtime activation, SDK package creation, product implementation, authority update, commit, or remote publication.

## 3. Package Files

| package role | file |
| --- | --- |
| Portable Core baseline | `_coordination/workflow_harness_core/workflow_harness_core_v1_0_freeze.md` |
| Export / adoption profile candidate | `_coordination/workflow_harness_core/workflow_harness_core_v1_0_export_profile.md` |
| New-project usage manual | `_coordination/workflow_harness_core/workflow_harness_new_project_usage_manual.md` |
| Project Adapter for this repo | `_coordination/workflow_harness_core/game_dialogue_bible_project_adapter.md` |
| Historical / Excluded Source boundary | `_coordination/workflow_harness_core/historical_excluded_source_boundary.md` |
| Runtime / SDK Adapter boundary | `_coordination/workflow_harness_core/runtime_sdk_adapter_boundary.md` |
| Writing-tool Product Route boundary | `_coordination/workflow_harness_core/writing_tool_product_route_boundary.md` |

## 4. Files Read

This package was prepared from:

- `AGENTS.md`
- `_docs/harness_usage_order_and_agent_mvp_plan.md`
- `_coordination/workflow_notes/20260516_31_a_exact_seal_scope_gate_note.md`
- `_coordination/workflow_notes/20260516_30_f_freeze_gate_tool_seal_decision_note.md`
- `_coordination/workflow_notes/20260516_29_a_harness_core_finalization_candidate_note.md`
- `_coordination/workflow_notes/20260516_29_b_project_adapter_candidate_note.md`
- `_coordination/workflow_notes/20260516_29_c_historical_excluded_source_boundary_note.md`
- `_coordination/workflow_notes/20260516_29_d_runtime_sdk_adapter_boundary_note.md`
- `_coordination/workflow_notes/20260516_29_e_source_to_destination_map_note.md`
- `_coordination/workflow_harness_core/workflow_harness_core_v1_0_freeze.md`
- `_coordination/workflow_harness_core/workflow_harness_core_v1_0_export_profile.md`

## 5. Files Not Read

- protected story / world / character / plot / scene / dialogue body text
- `00_protocol/` body text
- `01_world/` body text
- `03_characters/` body text
- `05_plot/` body text
- `08_dialogue_outputs/` body text
- `_coordination/workflow_runtime/` payload bodies
- full `scripts/` implementations
- SDK package files
- schema / registry / database artifacts
- connector implementation files
- automation definitions
- frontend / GUI / editor files
- `_exports/`
- `tasks/`
- `templates/`
- `_projects/` project data
- `archive/` body text
- `_reports/` body text
- `_patches/` body text
- `_prototypes/` body text

## 6. Source Limitations

- This is a document-level split package, not a full repo audit.
- Existing Core files remain REVIEW.
- This package does not inspect protected creative content.
- This package does not read runtime payload bodies.
- This package does not read helper or validator script implementations.
- This package does not execute helpers.
- This package does not create SDK package, schema, registry, database, connector, automation, frontend, export pipeline, task templates, or project workspace.
- Path references are scope signals, not content review.
- Validation output remains evidence only.

## 7. Use Rule

Use this package in this order:

1. Start from `workflow_harness_core_v1_0_freeze.md` for portable Core invariants.
2. Use `workflow_harness_core_v1_0_export_profile.md` for adoption checks.
3. Use `workflow_harness_new_project_usage_manual.md` for new-project adoption steps.
4. Apply `game_dialogue_bible_project_adapter.md` only for this repo.
5. Apply `historical_excluded_source_boundary.md` before using old notes, archives, reports, prototypes, or path-only evidence.
6. Apply `runtime_sdk_adapter_boundary.md` before runtime / SDK planning.
7. Apply `writing_tool_product_route_boundary.md` before writing-tool planning.

## 8. Not Approved

This package does not approve:

- Core LOCKED promotion;
- adapter installation;
- runtime activation;
- SDK package creation;
- protected creative-content read;
- writing-tool implementation;
- file move / copy / delete / rename / deprecation;
- report acceptance;
- dispatch;
- HOLD release;
- snapshot update;
- authority update;
- automation;
- commit proof;
- remote publication.

## 9. Seal Posture

The HARNESS tool boundary is split into deliverable REVIEW package files.

Final LOCKED status, if wanted, requires a separate final gate with exact targets and impact statement.

## 10. Classification

```text
PHASE_31_SPLIT_PACKAGE_INDEX_CREATED_AS_REVIEW_DELIVERABLE
```

Meaning:

- the split package has a package index;
- Core, Project Adapter, Historical / Excluded Source, Runtime / SDK, and Writing-tool boundaries are separated;
- existing Core files remain REVIEW;
- no LOCKED promotion, runtime activation, SDK package, writing-tool implementation, protected-content read, authority update, commit proof, or remote publication is approved.

## 11. Boundary Confirmation

This file is REVIEW evidence only.

It is not final tool seal approval, LOCKED approval, adapter installation approval, runtime approval, SDK approval, product implementation approval, report acceptance, dispatch permission, HOLD release, snapshot update, authority update, commit proof, or remote publication proof.
