# AUDIT-DOCS — Final pre-implementation architecture and documentation audit

**Part:** AUDIT-DOCS  
**Plan status:** Approved  
**Part status:** Planned; execution has not started  
**Revision:** 1  
**Author:** Codex `/root`  
**Proposed and approved:** 13 October 2026 (Asia/Dhaka)  
**Approval provenance:** The owner replied `approved` immediately after the complete approach reproduced below. This approval applies to that revision's documentation-only scope and boundaries.  
**Saved:** 13 October 2026 (Asia/Dhaka), separate SAVE step  
**Live status:** [HANDOFF](../HANDOFF.md)

The approved response is reproduced verbatim below, including its planning-time observations and closing approval request. Those statements describe the proposal at presentation time; the approval recorded above satisfies that request. This wrapper records provenance only and does not amend the approved scope. Preliminary observations are not a completed audit report or passing runtime evidence.

## Approved approach (verbatim)

I recommend treating this as a separate **documentation-only audit, provisionally named `AUDIT-DOCS`**. It should establish whether the documents are consistent and actionable, while keeping runtime compatibility and release approval as separate, unproven matters.

**No files have been created or modified.** The worktree remains clean. The observations below inform the proposed approach; they are not a completed audit verdict.

Several concrete issues already justify careful cross-document checking:

- **Browser-test sequencing:** [part 0E](/home/sanjoy-rozario/Parsefit/task.md:287) requires Playwright and three-browser checks, but [SETUP](/home/sanjoy-rozario/Parsefit/docs/SETUP.md:89) defers browser installation to 0F.
- **Deployment prerequisites:** [SETUP](/home/sanjoy-rozario/Parsefit/docs/SETUP.md:132) places provider/domain/budget selection after 42/43, although staging part 42 requires those approvals first.
- **Command ownership:** [SETUP](/home/sanjoy-rozario/Parsefit/docs/SETUP.md:113) instructs running every tool-version command from the repository root. Commands for application-owned dependencies need their working directories and package resolution checked.
- **Semantic dependencies:** the read-only structural check found 82 matching task cards and an acyclic explicit dependency graph. That does not establish that every acceptance step has its prerequisites available.

My proposed execution approach is:

1. **Establish the authoritative baseline.**  
   Read the entire requested documentation set, all 24 physical PDF pages, root README, plan conventions, and any repository-local agent configuration. Record source hashes and worktree state. Preserve the authority hierarchy: approved architecture and owner decisions supersede historical pending wording. Distinguish existing files, planned destinations, historical evidence, and currently runnable commands.

2. **Build requirement traceability in both directions.**  
   Use one row per independently testable capability—not merely one row per broad requirement group. Preserve existing R/D/T/O identifiers, splitting mixed MVP/Later requirements into clearly labeled audit subrows.

   The matrix will contain:

   `Physical PDF page/section → capability and provenance → MVP/Later/Research → architecture clause → implementation part → first validating part → concrete test assertion and T ID → test layer → gate/gap/disposition`

   Every MVP capability must have an implementation owner and meaningful verification. Conversely, every proposed task must have a product, owner-decision, or engineering justification. The seven page-22 scenarios anchor the review, but do not replace coverage of the remaining requirements.

3. **Audit portability through the earliest proof points.**  
   Examine shared screens/navigation, Paper styling and accessibility, platform import boundaries, portable DTOs, Hermes/date behavior, browser and native authentication, protected storage, networking, file export, permissions, and optional adapters.

   For each risk, identify its mitigation, first validating task, required environment, and failure consequence. Verify the existing chain: **0G installed Android → 0J protected native storage → 0K authentication → 0M isolated Health Connect feasibility → 0N integrated exit**. Later signing and publication remain separate. Documentation support will never be described as demonstrated compatibility.

4. **Walk through data correctness under failure and correction.**  
   Trace representative commands through local commit, crash, retry, acknowledgement, competing device changes, edit/undo, migration, rebootstrap, export, and deletion. Check identity, generations/revisions, snapshots, ownership, and invalidation at every transition.

   Priority cases include delayed offline target activation; unknown versus zero intake; nutrient-specific denominators; date moves affecting both dates; planned versus performed sets; finish/undo/recompletion identity; sleep overlap reconciliation; account switching; immutable retry envelopes; and deletion suppression during backup restoration. Ambiguous behavior affecting calculations or data protection becomes an explicit finding.

5. **Audit task feasibility beyond graph syntax.**  
   Validate all 82 cards, table/card agreement, dependency references, cycles, acceptance criteria, source ownership, and PLAN/IMPLEMENT recommendations. Then check when each capability is first needed: runners before tests, security before exposed operations, migrations before persisted schema changes, and reliable records before intelligence.

   Identify oversized parts by their coupled deliverables and verification burden. Proposed splits or dependency changes must preserve existing scope and evidence. Model recommendations remain recommendations; actual selection stays in the VS Code picker.

6. **Audit setup and environment instructions without executing installations.**  
   Inventory commands with their source, working directory, prerequisite files/tools, earliest owning part, side effects, expected result, and verification status. Classify each as pre-scaffold executable, post-part executable, optional, or unverified/owner-dependent.

   Recheck version-sensitive claims against current official documentation, including the Expo ecosystem, pnpm workspace behavior, authentication/storage integrations, Android tooling, and test runners. Check Compose environment loading, device API origins, public/private configuration, same-site authentication, and staging/production separation. Preserve historical machine observations as dated observations—not current compatibility proof.

7. **Reconcile documentation, verify corrections, and report.**  
   Check links and anchors, exact paths, terminology, creation statuses, environment names, scope labels, instruction precedence, plan locations, and generated configuration. Check for repository prompt artifacts without confusing canonical instructions or the external attachment with accidental prompt files.

   After approved documentation corrections, rerun link/path checks, graph/card checks, coverage checks, whitespace validation, protected-source integrity checks, and diff review. Record actual audit commands separately from future application tests.

The architectural decisions and alternatives will be handled as follows:

| Decision | Audit treatment and boundary |
|---|---|
| Universal Expo app and central Fastify API | Preserve the approved direction. Reconsider alternative clients only if concrete evidence exposes a structural failure. |
| Separate IndexedDB and SQLite adapters | Require shared behavioral contracts and real-store evidence; identical adapter code is unnecessary. |
| Custom synchronization | Test whether the documented protocol is bounded and complete. Managed replication is an escalation option requiring an approved architectural amendment. |
| Protected offline storage | Examine key lifecycle and usability tradeoffs under O4; never resolve uncertainty by silently weakening protection. |
| Targets, workout sequence, historical snapshots | Preserve approved semantics. Changes to activation dates, conflict handling, or completion rules require explicit approval. |
| Providers, retention, advice, release | Keep O4–O9 attached to their actual affected phases. Do not invent vendors, durations, thresholds, budgets, or approvals. |

Each finding will record **severity, evidence, consequence, affected phase, proposed resolution, approval requirement, and verification status**:

- **BLOCKER:** prevents the relevant next phase from proceeding coherently or safely.
- **HIGH:** substantial correctness, privacy, portability, or feasibility risk.
- **MEDIUM:** actionable ambiguity or inconsistency.
- **LOW:** editorial or navigation issue without behavioral impact.

This avoids treating every future release gate as a blocker to manual setup, while keeping those gates visible.

I propose these artifacts and edit boundaries:

- Save the approved plan as `docs/agent/plans/part-audit-docs-final-pre-implementation-audit.md`.
- Create `docs/agent/pre-implementation-audit.md` containing the eight requested report sections and appendices for requirements, portability, command classification, and findings.
- Update HANDOFF with actual status, evidence, unresolved decisions, and the precise next action.
- Update STRUCTURE and the test-command runbook for the audit’s actual artifacts and checks; update MEMORY only for durable conclusions.
- Correct existing documentation only where authoritative intent is clear. Preserve ANALYSIS’s decision history. Record consequential changes as proposals requiring approval.
- Leave the original PDF unchanged. Create no application code, tooling scaffold, credentials, deployments, or Git mutations.

Completion requires full source review, explicit disposition of every finding, meaningful requirement/task/test mapping, consistent setup sequencing, and verified documentation changes. Missing runtime evidence will remain clearly marked **Not run** with its prerequisite.

The requested readiness statement will appear only if the audit supports it:

> Documentation is ready for manual environment setup. Application implementation has not started.

**The next action is your approval or amendment of this approach.** Under the separate SAVE step required by [AGENTS.md](/home/sanjoy-rozario/Parsefit/AGENTS.md:17), approval leads to saving the exact plan and updating HANDOFF, then stopping. Audit execution and documentation corrections begin on your subsequent instruction.
