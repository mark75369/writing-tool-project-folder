狀態：REVIEW
版本：1.0-candidate
最後更新：2026-05-12
適用範圍：Workflow Harness Core v1.0 export profile candidate
優先級：高

# Workflow Harness Core v1.0 Export Profile Candidate

## 1. Purpose / Boundary

This REVIEW-status export profile candidate describes safe project adoption / mapping of Workflow Harness Core v1.0.

It explains how a project may map the Core protocol through adapter hooks and project-local exclusions.

It is not an installable package.

It is not a project adapter.

It is not a template.

It is not schema.

It is not a validator.

It is not automation input.

It is not an authority source.

It does not authorize external adoption by itself.

It does not approve execution, git, helper scripts, external reviewer execution, automation, or authority updates.

## 2. Source Core Reference

Source protocol baseline:

```text
_coordination/workflow_harness_core/workflow_harness_core_v1_0_freeze.md
```

The source Core file is REVIEW-status.

It is not LOCKED.

It is not installable.

It is not machine-readable schema.

It is not a project adapter.

It is not export approval.

It requires separate controller / user approval before LOCKED promotion or external adoption.

## 3. Export Readiness Status

Export profile status: REVIEW

Core status: REVIEW

This export profile candidate is not ready for external adoption.

External adoption waits for:

- Core LOCKED status; or
- separate controller / user approval for a specific adoption scope.

Internal dry-run mapping may happen while this profile is REVIEW only if separately routed.

Internal dry-run mapping is read-only unless separately authorized.

## 4. Required Adapter Mapping

An adopting project must map these adapter hooks before using Core concepts operationally:

- Room Identity Hook;
- Language / UX Hook;
- Project Policy Hook;
- Source Authority Hook;
- Confidentiality Hook;
- Git / Push UX Hook;
- External Reviewer Hook;
- Local Path Hook;
- Current Operational Snapshot Hook;
- Authority File / Local Governance Hook, if applicable.

Project-specific values belong in adapter, not in Core.

Room Identity Hook:

- maps concrete controller / room / reviewer identities;
- must preserve full room identity requirements;
- must define how generic role names are rejected for official routing.

Language / UX Hook:

- maps user-facing wording, footer language, response tone, and local communication conventions;
- must preserve user-facing control surface and fixed closing structure concept without forcing one language globally.

Project Policy Hook:

- maps project policy, local operating rules, document status rules, protected source rules, and governance rules;
- must not weaken controller / user gates.

Source Authority Hook:

- maps authoritative, protected, stale, historical, archived, excluded, summary, excerpt, and path-only source classes;
- must preserve exact Approved Read Scope.

Confidentiality Hook:

- maps private, commercial, protected, sensitive, or non-transferable content rules;
- must preserve least-necessary data transfer.

Git / Push UX Hook:

- maps local git, push, release, publish, or handoff practices;
- must not make Core approval imply git permission.

External Reviewer Hook:

- maps any external read-only advisory reviewer role;
- must preserve non-controller, non-authority, non-execution, and non-automation boundaries.

Local Path Hook:

- maps project-local paths and file layout;
- must not make local paths universal Core requirements.

Current Operational Snapshot Hook:

- maps current identity source and report-back target source;
- must preserve stop-and-ask when identity is missing, stale, conflicting, or expired.

Authority File / Local Governance Hook:

- maps local decision logs, open questions, handoff files, master state, or similar governance files if the project has them;
- must not let Core update those files without explicit local approval.

## 5. Required Project-local Exclusions

Project-local exclusions:

- concrete room identities;
- actual repo paths;
- concrete project policy wording;
- protected / LOCKED file details;
- story / world / character / dialogue / chapter / scene content;
- current snapshot instance;
- pushed note history;
- local validation provenance;
- authority files;
- concrete external reviewer identity;
- exact footer wording;
- push / post-push history.

These may be referenced by a project adapter.

They must not become universal Core content.

They must not become adapter-agnostic export profile content.

They must not be used as proof that another project has adopted Core safely.

## 6. Required Safety Invariants

Required safety invariants:

- manual controller / user gate;
- exact Approved Read Scope;
- current identity source before startup behavior;
- full room identity;
- `Report back` safety;
- stale / archived / excluded source handling;
- non-acceptance rules;
- external advisory reviewer boundary;
- data transfer safety;
- stop-and-ask;
- must-not-infer.

Non-acceptance rules include:

- `PASS` is not approval;
- `READY` is not approval;
- `VALID` is not approval;
- Recommended Next Route is not approval and not auto dispatch;
- labels are not approval;
- reminders are not approval;
- advisory findings are not approval.

Safety invariants must not be weakened by project adapters.

## 7. Project Adoption Checklist

Before adopting Core, a project should:

- map adapter hooks;
- list project-local exclusions;
- identify protected / authority sources;
- define current operational rooms snapshot equivalent;
- define official `Report back` target handling;
- define external reviewer rules, if used;
- define data transfer scope and confidentiality rules;
- confirm non-automation boundary;
- run read-only portability dry-run;
- obtain controller / user adoption approval.

The adoption checklist is guidance only.

It is not a template.

It is not schema.

It does not approve adoption by itself.

## 8. Validation Evidence Requirements

An adopting project must provide its own validation evidence.

Required adoption evidence should include:

- adapter mapping review;
- project-local exclusion review;
- read-only portability dry-run;
- stale-source / identity / `Report back` safety test;
- protected-source / confidentiality check;
- non-automation boundary check.

Local provenance from this repo is origin context only.

It is not universal proof.

Do not copy this repo's 1.13 validation as adoption evidence.

Do not copy this repo's 1.14 validation as adoption evidence.

Do not copy this repo's post-creation validation as adoption evidence.

Other projects must produce their own evidence through their own project adapter / controller gate.

## 9. Non-goals / Deferred Items

Deferred items:

- template;
- schema;
- validator;
- report inbox;
- automated intake;
- auto dispatch;
- auto acceptance;
- registry / checkpoint / work item instances;
- external reviewer execution / connector;
- git automation;
- 2.x automation;
- 3.x automation;
- project adapter creation;
- Core LOCKED promotion.

These items are not created by this export profile candidate.

These items require separate controller / user approval if ever pursued.

## 10. Stop-and-ask Conditions

Stop and ask when:

- project adapter mapping is missing;
- project-local exclusions are unclear;
- protected sources are unclear;
- active room identity is unclear;
- official `Report back` target is unclear;
- external reviewer boundary is unclear;
- data transfer scope is too broad;
- export profile is mistaken as installable package;
- export profile is mistaken as template;
- export profile is mistaken as schema;
- export profile is mistaken as automation;
- Core REVIEW status is mistaken as LOCKED.

Stop-and-ask is safety behavior.

It is not adoption approval.

It is not permission to proceed.

## 11. Must-not-infer Rules

Do not infer from this export profile candidate:

- adoption approval;
- project adapter creation;
- template creation;
- schema creation;
- validator creation;
- automation;
- authority update;
- Core LOCKED promotion;
- external adoption authorization;
- execution permission;
- git permission;
- helper script permission;
- external reviewer execution permission;
- report inbox creation;
- automated intake;
- auto dispatch;
- auto acceptance;
- registry / checkpoint / work item instance creation.

This export profile does not replace project policy.

This export profile does not replace project adapter mapping.

This export profile does not replace controller / user gate.

## 12. Advisory Boundary

This is a REVIEW-status export profile candidate only.

It requires validation before acceptance.

External adoption requires separate approval.

Internal dry-run mapping requires separate routing.

It is not external adoption approval.

It is not Core LOCKED promotion.

It is not project adapter creation.

It is not template creation.

It is not schema creation.

It is not validator creation.

It is not automation creation.

It is not authority update.

It is not git permission.

It is not external reviewer execution permission.

It is not report inbox approval.

It is not automated intake approval.

It is not auto-dispatch approval.

It is not auto-acceptance approval.

It is not registry / checkpoint / work item instance approval.
