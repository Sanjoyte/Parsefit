# Saved part plans

Implementation plan home: `docs/agent/plans/`. No part implementation plan is approved or created by COORD-DOCS; this index preserves the directory without fabricating one.

Current approved plan: [AUDIT-DOCS revision 1](part-audit-docs-final-pre-implementation-audit.md), approved and saved on 13 October 2026 for documentation review only. Application-part plans remain unapproved. [HANDOFF](../HANDOFF.md) records execution status; the saved approved wording is not rewritten as live status changes.

Use `part-<lowercase-id>-<short-slug>.md`, for example `part-0a-repository-toolchain.md` (example filename only; not an existing plan). A built-in temporary plan must still be copied here as the exact owner-approved Markdown before implementation. Link the actual saved plan from [HANDOFF](../HANDOFF.md).

Each plan must record:

1. Part ID/title, status (`Proposed` or `Approved`), author/date, and approval provenance/date. Never infer approval.
2. Bounded scope, exclusions and deliverables; parent task acceptance and PDF/architecture/R/D/T/O references.
3. Completed prerequisites with evidence, unresolved gates and required owner/environment inputs.
4. Exact proposed file changes; interfaces, data models, migrations, compatibility and security/privacy implications.
5. Ordered implementation sequence and explicit stopping point.
6. Edge cases; unit/integration/static/build checks; browser/Android/manual steps with prerequisites and expected outcomes.
7. Rollback/recovery: preserve existing work and unsent data; schema/protocol limits; no destructive Git rollback. Owner-reviewed production changes separately.
8. Decisions, rejected alternatives when relevant, dependencies requiring approval, and remaining questions.
9. Checkable acceptance criteria, completion evidence and documentation updates, including `docs/test-command.md`.
10. Separate PLAN and IMPLEMENT model/effort recommendations; VS Code picker availability controls actual selection.

An optional proposed plan may live here with `Proposed` status. The **SAVE** step records the exact approved revision and HANDOFF link without implementing. Later amendments require review and a revision/approval note; do not silently edit an approved plan's scope. Do not create empty files for every roadmap row. Follow [AGENTS.md](../../../AGENTS.md) and [task.md](../../../task.md).
