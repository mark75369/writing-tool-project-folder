狀態：REVIEW
版本：1.0
最後更新：2026-05-12
適用範圍：Workflow Harness Core v1.0 manual protocol baseline
優先級：高

# Workflow Harness Core v1.0 Freeze

## 1. Purpose / Boundary

This is the Workflow Harness Core v1.0 freeze file in REVIEW status.

It is a project-agnostic manual protocol baseline.

It preserves safety invariants, manual gates, identity boundaries, scope boundaries, stale-source boundaries, report-back boundaries, and adapter hook requirements.

It is not an export profile.

It is not a template.

It is not schema.

It is not a validator.

It is not automation.

It is not an authority update.

It does not include project-local room identities.

It does not include repo paths.

It does not include story content.

It does not include project authority files.

It does not approve implementation, git, external reviewer execution, automation, export, or adapter installation.

## 2. Core Version / Freeze Status

Core Version Candidate: v1.0

Status: REVIEW

LOCKED status requires separate post-creation validation and controller / user freeze approval.

Export profile creation requires a separate task after validation.

This file must not be treated as LOCKED.

This file must not be treated as installable Core package.

This file must not be treated as export profile.

## 3. Core Safety Invariants

Core safety invariants:

- manual controller / user gate is required;
- exact Approved Read Scope is required;
- current identity source must be checked before startup behavior source;
- Current Operational Rooms Snapshot model is required for active room identity handling;
- full room identity is required for routing;
- official `Report back` target must come from current identity source or controller / user gate;
- generic role names are invalid for official routing;
- stale / archived / excluded sources never become current state;
- `PASS` is not approval;
- `READY` is not approval;
- `VALID` is not approval;
- Recommended Next Route is not approval and not auto dispatch;
- labels are not approval;
- reminders are not approval;
- advisory findings are not approval;
- external advisory reviewer is not controller;
- external advisory reviewer is not co-controller;
- external advisory reviewer is not implementation room;
- external advisory reviewer is not execution room;
- external advisory reviewer is not authority source;
- external advisory reviewer is not automation layer;
- file paths are not full-content review;
- summaries do not override source excerpts;
- unclear identity means stop and ask;
- unclear scope means stop and ask;
- unclear freshness means stop and ask;
- unclear permission means stop and ask;
- unclear authority means stop and ask.

These invariants must not be weakened by adapters, examples, project policy, convenience routing, or future automation design.

## 4. Manual Controller / User Gates

Workflow Harness Core assumes manual controller / user gates.

A controller / user gate is required before:

- routing a task;
- expanding Approved Read Scope;
- approving repo modification;
- approving file creation;
- approving git / push;
- accepting a report;
- accepting a review;
- changing authority state;
- changing active room identity;
- creating templates;
- creating schema;
- creating registry / checkpoint / work item instances;
- starting automation;
- enabling external execution.

No report, label, reminder, validation result, helper output, advisory finding, or recommended route replaces the controller / user gate.

## 5. Approved Read Scope

Approved Read Scope must be exact.

Allowed sources should be listed by exact path, exact pasted excerpt, or exact named source.

Broad source descriptions require explicit controller / user approval.

The following are invalid unless separately approved and risk-reviewed:

- whole repo;
- whole folder;
- all workflow notes;
- all project docs;
- inferred related files;
- unlisted archives;
- unlisted locked or protected content.

If a room needs more source material, it must report scope insufficiency rather than expanding scope independently.

Approved Read Scope does not authorize write access.

Approved Read Scope does not authorize git.

Approved Read Scope does not authorize execution.

## 6. Layered Startup and Identity Safety

Startup must check current identity source before startup behavior source.

Current identity source should identify:

- active controller;
- official report-back target;
- active workflow rooms;
- external advisory reviewers;
- standby rooms;
- historical rooms;
- validation-only rooms;
- stale / excluded room identities;
- expiration or recheck triggers.

Startup behavior source may define response shape, routing style, pacing, and task-specific protocol.

Startup behavior source must not override current identity source.

If current identity source is missing, stale, conflicting, expired, contradicted, or insufficient for routing, stop and ask.

## 7. Current Operational Rooms Snapshot Model

The Current Operational Rooms Snapshot model should include:

- Snapshot Purpose / Boundary;
- Last Confirmed By;
- Last Confirmed At;
- Current Active Controller;
- Official Report-back Target;
- Active Workflow Rooms;
- Standby Rooms;
- Historical Rooms;
- Validation-only Rooms;
- External Advisory Reviewer Rooms;
- Stale / Excluded Room Identities;
- Allowed Use;
- Must Not Infer;
- Expiration / Recheck Triggers;
- Stop-and-ask Conditions;
- Advisory / Non-authority Boundary.

The snapshot is operational routing reference.

The snapshot is not authority source.

The snapshot does not approve routing, execution, repo modification, file creation, git, automation, or external execution.

Project adapters may define concrete snapshot fields and values, but must preserve the non-authority boundary.

## 8. Full Room Identity and Report-back Safety

Full room identity is required for:

- routing target;
- source room;
- report-back target;
- next reviewer;
- integration owner;
- standby or historical room reference;
- external advisory reviewer reference.

Generic role names are invalid for official routing.

Official report-back target must come from:

- current operational identity source; or
- current controller / user gate.

Stale report-back targets must not be inherited.

Historical, standby, validation-only, stale, excluded, or external advisory rooms must not receive official reports unless explicitly designated by current controller / user gate.

If report-back target is unclear, stop and ask.

## 9. Role Handoff / Activation Abstract Flow

Role handoff and activation concepts preserve controlled context transfer.

A role handoff should distinguish:

- target role;
- purpose;
- current workflow state;
- role boundary;
- current sources;
- task-specific sources;
- archived / excluded sources;
- next allowed step;
- manual gates;
- non-acceptance rules;
- output / report requirements;
- blockers;
- advisory boundary.

An activation packet concept may add startup source policy, permissions, forbidden actions, pacing rules, and activation confirmation.

Handoff and activation do not switch controller by themselves.

Handoff and activation do not approve execution.

Handoff and activation do not update authority state.

## 10. Task Packet / Return Report Abstract Flow

Task packet concepts should describe a single scoped routed step.

Task packet concepts should include:

- source room;
- target room;
- task type;
- approved read scope;
- objective;
- required work;
- permissions;
- forbidden actions;
- expected output;
- report-back target;
- manual gates;
- advisory boundary.

Return report concepts should include:

- report source;
- report target;
- sources read;
- work performed;
- result status;
- findings / output;
- scope compliance;
- risks / warnings;
- recommended next route;
- needs controller decision;
- needs user decision;
- non-acceptance statement;
- blockers;
- advisory boundary.

Recommended Next Route is advisory only.

Return report status is not controller acceptance.

## 11. Controller Acceptance and Non-acceptance Rules

Controller acceptance is a separate controller decision.

A return report is not acceptance.

A review report is not acceptance.

QA `PASS` is not acceptance.

`PASS WITH NON-BLOCKING ISSUES` is not acceptance.

`READY` is not acceptance.

`VALID` is not acceptance.

Advisory findings are not acceptance.

Controller acceptance should review:

- content;
- scope compliance;
- source compliance;
- gate readiness;
- warnings / risks;
- dependencies;
- authority split;
- required user decision;
- required controller decision;
- report-back safety.

Accepted-for-next-step does not imply git, push, authority update, automation, or external execution.

## 12. Decision Reminder / User-facing Control Surface Concept

Decision reminders are user-facing control surface aids.

They should surface:

- current state;
- pending decision;
- decision owner;
- urgency;
- blocking level;
- options;
- recommendation;
- key risks;
- permission / authority impact;
- next step after decision;
- trace reference;
- non-approval boundary.

Decision reminders are not approval.

Decision reminders do not create registry instances.

Decision reminders do not create authority state.

Decision reminders do not approve routing, implementation, git, automation, or external execution.

## 13. Labels and Trace References

Labels and trace references are references only.

They may identify:

- work item;
- room;
- handoff;
- activation packet;
- task packet;
- return report;
- controller acceptance;
- decision reminder;
- gate;
- checkpoint.

Labels do not create artifacts.

Labels do not create registry / checkpoint / work item instances.

Labels do not prove active room identity.

Labels do not approve dispatch.

Labels do not approve implementation.

Trace chain arrows mean reference relationship only.

Trace chain arrows do not mean route authorization, approval sequence, or auto dispatch.

## 14. Warning Severity / Disposition

Warning severity and disposition are human review guidance.

Severity describes seriousness.

Disposition describes controller treatment.

Recommended severity categories may include:

- INFO;
- NON_BLOCKING;
- FOLLOW_UP_NEEDED;
- NEEDS_REVISION;
- BLOCKING.

Recommended disposition categories may include:

- record_only;
- accept_with_note;
- accept_with_follow_up;
- return_for_revision;
- hold_for_decision;
- block;
- out_of_scope.

Warning severity is not approval.

Warning disposition is not approval.

Warning disposition does not create files, gates, reminders, templates, registry instances, or automation.

If an issue affects scope, source, permission, authority, identity, report-back target, git, automation, external execution, or blocking gate, it must not be treated as ordinary minor warning.

## 15. Read-only Dry-run Validation Classification

Read-only dry-run validation may classify results as:

- PASS;
- PASS WITH NON-BLOCKING ISSUES;
- FAIL.

Use PASS WITH NON-BLOCKING ISSUES for successful validation with recorded non-blocking issues.

Do not use PASS WITH WARNING as the preferred classification.

Validation result is not controller acceptance by itself.

Validation result is not implementation approval.

Validation result is not authority update.

Validation result is not git permission.

## 16. External Read-only Advisory Reviewer Model

An external read-only advisory reviewer may receive exact allowed data and return advisory findings.

The reviewer:

- is not controller;
- is not co-controller;
- is not implementation room;
- is not execution room;
- is not authority source;
- is not automation layer;
- does not accept reports;
- does not approve implementation;
- does not approve git;
- does not update rules automatically.

External advisory findings are input evidence only.

Controller / user gate decides whether findings become accepted evidence, follow-up, revision, block, or out of scope.

## 17. Data Transfer Safety for Paths / Excerpts / Summaries

Data transfer must preserve source type.

File paths are provenance or scope signals.

File paths are not full-content review.

Pasted excerpts are directly reviewable material.

Pasted excerpts should identify source, section, and whether they are partial, complete, or redacted.

Summaries must be marked as summaries.

Summaries do not override source excerpts when source review is required.

Summaries do not override current operational identity source.

Summaries do not expand Approved Read Scope.

If source content is unavailable, partial, redacted, stale, or summary-only, reviewer confidence and controller handling must reflect that limitation.

## 18. Stale / Archived / Excluded Source Handling

Sources should be classified when relevant:

- current;
- historical;
- stale;
- archived;
- excluded;
- summary;
- excerpt;
- path-only.

Stale / archived / excluded sources never become current state by existing.

Historical sources may be used for archaeology only when explicitly in scope.

Stale sources must not provide current active identity.

Stale sources must not provide official report-back target.

Stale sources must not override current operational rooms snapshot.

If stale conflict remains unclear, stop and ask.

## 19. Stop-and-ask Conditions

Stop and ask when:

- current identity is missing;
- current identity is stale;
- current identity is conflicting;
- current identity is expired;
- routing target lacks full room identity;
- report-back target is unclear;
- Approved Read Scope is missing;
- Approved Read Scope is too broad without explicit approval;
- source freshness is unclear;
- stale source conflicts with current state;
- permission boundary is unclear;
- authority boundary is unclear;
- requested action implies repo modification without approval;
- requested action implies git without approval;
- requested action implies automation without approval;
- requested action implies external execution without approval;
- project adapter hook is missing for protected source, confidentiality, local paths, or authority files.

Stop-and-ask is safety behavior.

It is not failure by itself.

It is not permission to proceed.

## 20. Must-not-infer Rules

Do not infer from this file:

- authority update;
- controller switch;
- role activation;
- implementation approval;
- git permission;
- automation approval;
- external execution permission;
- external reviewer execution permission;
- export profile creation;
- template creation;
- schema creation;
- validator creation;
- report inbox creation;
- automated intake;
- auto dispatch;
- auto acceptance;
- registry / checkpoint / work item instance creation;
- project adapter creation;
- installable package creation.

REVIEW does not mean LOCKED.

Core baseline does not replace project adapter.

Core baseline does not override project policy.

Core baseline does not override controller / user gate.

## 21. Adapter Hook Requirements

Required adapter hook categories:

- Room Identity Hook;
- Language / UX Hook;
- Project Policy Hook;
- Source Authority Hook;
- Confidentiality Hook;
- Git / Push UX Hook;
- External Reviewer Hook;
- Local Path Hook;
- Current Operational Snapshot Hook;
- Authority File / Local Governance Hook, if the project has such files.

Adapter hooks must not weaken core safety invariants.

Adapter hooks must not turn project-local examples into universal requirements.

Adapter hooks must not bypass controller / user gates.

Adapter hooks must not treat external advisory reviewers as execution integrations.

Adapter hooks must preserve protected source and confidentiality rules for the target project.

## 22. Project-local Exclusions

Project-local exclusions:

- concrete room identities;
- actual current active rooms snapshot instance;
- actual repo paths;
- concrete AGENTS.md wording;
- concrete LOCKED / DEPRECATED file details;
- story content;
- world content;
- character content;
- dialogue content;
- chapter content;
- scene content;
- pushed note history;
- validation outcomes;
- stale controller cleanup history;
- DEC / OQ / H / master / handoff authority files;
- repo-specific response examples;
- exact footer wording;
- push / post-push history;
- concrete external reviewer identity.

Project-local exclusions may appear in project adapters or local documentation.

They must not be embedded in project-agnostic core as universal requirements.

## 23. Local Validation Provenance / Non-core Evidence

Validation evidence available before this REVIEW file:

- 1.13 portability dry-run accepted as PASS WITH NON-BLOCKING ISSUES;
- 1.14 freeze-candidate validation accepted as PASS WITH NON-BLOCKING ISSUES;
- artifact boundary design accepted with two-artifact plan.

This evidence records local validation provenance for this REVIEW artifact.

It must not be exported as project-agnostic core requirement.

It must not be copied into adapter-agnostic export profile content.

Other projects must provide their own validation evidence through their project adapter / controller gate.

This file still requires post-creation validation before promotion or export profile creation.

Post-creation validation should confirm:

- status is REVIEW, not LOCKED;
- no export profile was created;
- no project-local room identities are embedded as core requirements;
- no repo paths are embedded as core requirements;
- no story / dialogue / protected project content is embedded;
- adapter hook requirements are present;
- deferred items remain deferred;
- safety invariants are preserved.

## 24. Change / Extension Rules

Changes require controller / user gate.

Extensions must not weaken safety invariants.

Project adapter examples must not enter core body as universal requirements.

LOCKED status requires separate approval.

Export profile requires separate approved task.

Templates require separate approval.

Schema requires separate approval.

Automation requires separate approval.

External execution integration requires separate approval.

## 25. Deferred Items

Deferred items:

- export profile file;
- templates;
- schema;
- validator;
- report inbox;
- automated intake;
- auto dispatch;
- auto acceptance;
- registry / checkpoint / work item instances;
- external reviewer execution;
- external reviewer connector;
- git automation;
- 2.x automation;
- 3.x automation.

These deferred items are not created by this REVIEW file.

## 26. Advisory Boundary

This is a REVIEW-status core artifact.

It requires post-creation validation.

It must not be used as an installable package.

It must not be used as automation input.

It must not be used as schema.

It must not be used as project adapter without separate approval.

It is not an authority source.

It is not an authority update.

It is not execution permission.

It is not implementation approval.

It is not git permission.

It is not automation approval.

It is not external reviewer execution permission.

It is not export profile.

It is not template.

It is not schema.

It is not validator.

It is not report inbox.

It is not automated intake.

It is not auto dispatch.

It is not auto acceptance.

It is not controller switch.

It is not role activation.

REVIEW does not mean LOCKED.
