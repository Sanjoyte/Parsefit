# Final pre-implementation architecture and documentation audit

**Part:** AUDIT-DOCS. **Date:** 13 October 2026 (Asia/Dhaka). **Status:** Done, documentation scope only. **Authority:** [approved revision 1](plans/part-audit-docs-final-pre-implementation-audit.md), followed by the owner's `Execute AUDIT-DOCS.` instruction. `/root` was the sole repository writer. Read-only reviewers supplied partial observations before a tool usage limit stopped them; the primary editor completed the review and verification. No reviewer failure is represented as a completed independent sign-off.

Reviewed the complete 24-page [blueprint](../Adaptive_Health_App_Product_Blueprint.pdf), [ANALYSIS](../ANALYSIS.md), [ARCHITECTURE](../ARCHITECTURE.md), [STRUCTURE](../STRUCTURE.md), [SETUP](../SETUP.md), [ENV_GUIDE](../ENV_GUIDE.md), [test runbook](../test-command.md), [82-part roadmap](../../task.md), [AGENTS](../../AGENTS.md), [CLAUDE](../../CLAUDE.md), [HANDOFF](HANDOFF.md), [MEMORY](MEMORY.md), root README and saved-plan conventions. Physical PDF pages 7, 19 and 22 were also rendered and visually checked for calendar meaning, MVP order and acceptance scenarios. No generated agent configuration exists. The external task attachment is outside the repository.

This report assesses specified behavior and readiness to begin setup. Every application, storage, browser, native, operational and pilot test below is a **required future test, Not run**. Passing documentation checks cannot close O1 or O4–O9. ANALYSIS's historical pending stack/O2/O3 wording is preserved; architecture's approval record governs those decisions.

## 1. Critical blockers

**No remaining BLOCKER to manual S0 environment setup was found.** Clear documentation defects were corrected under the approved audit scope. No consequential architecture change was needed or made.

The following remain blockers **at their affected gates**, not blockers to reading the guide or installing owner toolchains:

| Finding | Severity / affected phase | Evidence and consequence | Resolution / approval / verification |
| --- | --- | --- | --- |
| G01 | HIGH; blocks core if 0N fails | Architecture §§12–13; 0G/0J/0K/0N. Universal UI, protected stores, Hermes and auth have no installed-build evidence. | Execute separately approved foundation parts; record real browser/Android proof. Structural failure requires owner architecture amendment. Not run. |
| G02 | HIGH; blocks real health data | Architecture §10.2/O4: key lifecycle, recovery, metadata and local-copy promises remain unresolved. | Owner-approved policy plus verified 0I/0J/22/39 behavior. Synthetic prototypes only until then. Open. |
| G03 | HIGH; blocks production sync/privacy/recovery commitments | Architecture §§5.4/10.3/O6: replay, receipts, undo, deletion, export and backups have coupled retention obligations. | Owner approves coherent durations and recovery objectives before affected 26/29–31/39 production finalization. No guessed values. Open. |
| G04 | HIGH; blocks advice, external processing or real pilot/release as applicable | Architecture §14.3/O5/O7/O8/O9. Reviewer, license, provider, budget and pilot approvals are absent. | Follow the individual gates in §4 below; engineering tests cannot substitute for owner/expert approval. Open. |

## 2. Important risks

| Finding | Severity | Evidence / consequence | Mitigation, first proof and disposition |
| --- | --- | --- | --- |
| RISK01 | HIGH | Custom sync couples transactions, immutable retries, revisions, conflicts, cursors and deletion; a superficially green UI could lose pending work. Architecture §§5/11. | 0H contracts, real-store 0I/0J, real PG 23, entity 23A–23C, two-client 24–27, recovery 30–31, integrated 39–41. Keep manual pending intent visible. Open implementation risk; no managed-sync substitution approved. |
| RISK02 | HIGH | SDK candidate compatibility is not proven. Better Auth's current Expo guide targets SDK 55 while SETUP's current Expo candidate is 57. | 0A candidate investigation and 0K installed authentication proof; this documentation mismatch is a reason to test, not proof of incompatibility or permission to downgrade. Official sources in Appendix E. |
| RISK03 | HIGH | Web crypto awaits can outlive IndexedDB transactions; unscoped native transactions can admit unrelated async writes. | Architecture §5.1 already prescribes encryption before short CAS transactions and scoped native transactions. 0I/0J must prove crash/quota/concurrency behavior on real stores. |
| RISK04 | HIGH | Wrong missingness, target binding, set identity or sleep totals would create misleading health facts. | Retain the existing state distinctions; Appendix C walks concrete failures. T01–T19/T30 require deterministic and real-store evidence. No policy or calculation threshold added. |
| RISK05 | MEDIUM | Model/effort recommendations may be unavailable to the owner's account. Research parts could also be mistaken for permission to ship experiments. | Picker availability is authoritative; retain quality recommendations and disclose unavailable choices. T34 promotion and a fresh approved plan precede later functionality. No permanent model configuration. |
| RISK06 | MEDIUM | Large coupled parts 23C, 25, 26, 30, 31, 39 and 41 could exceed a comfortable implementation turn. | Their concrete plans must bound fixtures, migrations, command families, environments and acceptance evidence. Split by an approved plan amendment if needed; no arbitrary new roadmap dependency or automatic scope cut made here. |
| RISK07 | MEDIUM | Actual Safari, physical Android, CI access and qualified reviewers are not established by the historical Ubuntu inventory. | Owner arranges access before the relevant 0G/0N/38/43 checks. Record unavailable required checks as blocked, never replace actual Safari with WebKit. |

## 3. Documentation inconsistencies found and fixed

All corrections below implement already stated intent. Approval basis is AUDIT-DOCS revision 1; none changes O2/O3, adds a dependency family, changes a graph edge or authorizes installs. Verification is source comparison plus the documented checks; it is not execution of the future commands.

| Finding | Severity / affected phase | Before / consequence | Correction and evidence |
| --- | --- | --- | --- |
| F01 | HIGH / 0E | Browser installation deferred to 0F although 0E requires Playwright browser acceptance. | [SETUP Phase B](../SETUP.md#phase-b--after-foundation-scaffolding-is-implemented), troubleshooting, 0E and runbook now put pinned runner/browser prerequisites at 0E; 0F consolidates CI. |
| F02 | MEDIUM / 31, 42 | Provider/domain/budget selection appeared after staging/pilot parts needing it. | SETUP Phase D places O7 before external provisioning, including 31 if hosted resources are required, and before 42. |
| F03 | MEDIUM / 0G, 0J | Blanket native prebuild restriction conflicted with approved CNG and SQLCipher feasibility. | SETUP Phase E permits approved generation; source remains app config/plugins. Hand-editing or committing generated native ownership still needs amendment. |
| F04 | MEDIUM / 0D, 0E | All CLI checks were described as root commands; copying API env could be mistaken for Compose interpolation setup. | SETUP/ENV_GUIDE name application versus root directories and make Compose lines conditional on explicit 0D wiring. No secret values or speculative ports supplied. |
| F05 | MEDIUM / 0E; LOW / 0G | Client env example was missing from 0E expected paths; Android identity appeared needed only at 47. | 0E names `apps/universal/.env.example`; SETUP/ENV_GUIDE select development identity at 0G, review distribution identity at 47. |
| F06 | HIGH / 1, 5, 8 | Part 1's manual scenario implicitly needed unbuilt Sleep logging; part 5 required Food despite no dependency on 3. | Part 1 verifies sleep-only onboarding plus its implemented Note/date flow. Part 5 verifies Sleep independently; existing part 8 dependencies on 3/5 own the combined manual-module baseline. Full T22 remains required. |
| F07 | HIGH / 25, 26, 28, 41 | Conflict/bootstrap acceptance implied usable export before part 28 created it. | 25/26 preserve exportable pending evidence; 28 verifies export integration, 41 explicitly tests expired replay → export before old-store cleanup. No pending-loss escape or release waiver. |
| F08 | MEDIUM / 1, 13, 8, 9 | R08 old-goal review was implicit; warm-up/working history was less explicit in architecture than the task cards. | Architecture §§2.1/8.1 and T22 state both existing requirements; parts 1/13 explicitly validate restored preferences and old-goal review under next-day activation. |
| F09 | MEDIUM / 0L | Local hosting proof could assume a CLI introduced only at deployment. | 0L/SETUP require the concrete plan to select and approve local preview tooling at first use; pinned Wrangler if chosen, no login/deployment authority. |
| F10 | MEDIUM / 42, 44 | A blanket prohibition on staging tests conflicted with planned staging rehearsal and limited production smoke. | Runbook distinguishes isolated routine/fault tests from explicitly approved synthetic staging operations and limited synthetic production smoke. |
| F11 | LOW / coordination | Existing test guide and approved documentation plan were still described as absent/future; live SAVE status was stale after execution. | AGENTS, architecture, task, plan index, README, MEMORY, STRUCTURE and HANDOFF align current versus historical status. Approved plan's historical wording remains unchanged. |
| F12 | LOW / path ownership | STRUCTURE placed manual overlap at M3, file export at M1 and staging workflow at M4 despite owning cards. | Manual overlap marked M1/6, files M4/28–29, staging workflow M6/42. No source paths added beyond approved documentation artifacts. |

## 4. Remaining unresolved decisions

| Gate | Owner / earliest affected work | Required decision or evidence; current disposition |
| --- | --- | --- |
| O1 | Owner + implementer; 0A through 0N | Mutually compatible lockfile, OS/browser/device matrix, Paper accessibility, native plugins, date/auth/protected-store proofs. Stack direction approved; empirical exit remains open. |
| O2 | Owner | Page-19 MVP and pp.20–21 deferrals already approved. No reapproval requested. |
| O3 | Owner | First and later target activations begin next journal day; only deliberate finish/skip consumes an occurrence. Already approved. |
| O4 | Owner; 0I/0J feasibility, 22/39 before real data | Unlock/setup friction; key wrapping/rotation/recovery/lock; backup exclusion; metadata/index exposure; logout/local-copy/unsynced-loss behavior. Synthetic proof may proceed under approved plans. |
| O5 | Owner + qualified reviewers/curator; 14/32/37 | Eligible population, methods, constraints and uncertainty language. No PDF equation, example or numerical range becomes approved clinical/product policy by this audit. |
| O6 | Owner + operator; 26/29–31/39 | Joint undo/receipt/replay/tombstone/device-proof/export/backup retention and measured recovery objectives. Restore suppression must survive independently of an old backup. |
| O7 | Owner/operator; before external provisioning, 31 if needed, 42 | Exact vendor, domain/origins, region, budget, email, operator and credentials. Local synthetic development needs none of these production accounts. |
| O8 | Owner/curator; 32–36 and promoted integrations | Licensed catalog/media/food data; Bangladesh benchmark and approved thresholds; AI terms, consent, region, retention, caps and kill switch. No real external processing assumed. |
| O9 | Owner/researcher; 43/44 and later 47 | Adult recruitment, consent, privacy/distribution review, device coverage and pilot criteria. No participant count, success threshold or release approval invented. |

0D's exact Compose wiring, 0E runner ownership, 0G package identity and 0L local preview tool remain ordinary concrete-plan decisions within these boundaries. Environment variable names in ENV_GUIDE are a proposed registry until adopted by code. Exact native/plugin versions, key policy, retention durations and provider budgets are intentionally unresolved, not filled with fake values.

## 5. Android portability assessment

The approved architecture minimizes avoidable UI/domain duplication: one universal app, thin shared routes, platform-selected adapters, portable contracts and shared behavioral fixtures. It does **not** establish a reuse percentage or demonstrated compatibility. Native build evidence starts at **0G**, protected native storage at **0J**, auth at **0K**, isolated Health Connect feasibility at **0M**, and integrated exit at **0N**, before core feature part 1. Website publication remains 44; Android hardening/signing/distribution preparation remains 46/47. Appendix B gives each risk its earliest proof and failure consequence.

No browser-only dependency belongs in domain/contracts or an unconditional universal import. Dexie/IndexedDB, service workers and browser download handling are web adapters; SQLite, SecureStore, native permissions and future device services are native adapters. Drizzle/PostgreSQL and provider SDKs stay in the API. TanStack Query remains a remote cache. Camera/notification/health adapters are extension boundaries, not installed features. New plugins still require their own approved plan.

## 6. Missing requirements or tests

After the corrections, **no unassigned approved MVP capability was identified**. Appendix A maps all R01–R74, including independently testable sub-capabilities and explicit Later gaps. All T01–T34 remain represented. Missing implementation and runtime evidence is universal because implementation has not started; a mapping is not a passing test.

The previously weak explicit assertions were re-enable/old-goal review, warm-up/comparable actual history, staged manual-module integration, and preserved conflict/rebootstrap data reaching export. Their owning parts and tests are now explicit. The seven physical p.22 scenarios remain T01–T07, with completion/retry/coverage/history/fallback/module behavior expanded by T08–T34 rather than treated as exhaustive coverage.

Later requirements without a concrete implementation part are visibly retained: richer timers/supersets/effort/demo tools, custom day-boundary UI, HealthKit and non-sleep/device imports, cooperative groups, automatic tracking-burden detection, and billing/monetization. Some research cards evaluate only one selected idea (58/59); they are not approval for every item in their requirement group. A fresh bounded PLAN with T34 evidence and relevant O gates is required before promotion. These are not MVP blockers.

## 7. Manual setup readiness

**Documentation is ready for manual environment setup. Application implementation has not started.**

S0 starts with owner Git/Node/pnpm/Docker/Compose/editor checks. Existing machine versions are dated observations from 12 October, not new compatibility evidence. Services wait for 0D; browser runner/binaries for 0E; Android build prerequisites for 0G; actual Safari and the complete portability matrix for 0N. No app env file or secret is required now. Commands and classifications are in Appendix D.

Documentation verification is recorded in [the audit runbook](../test-command.md#audit-docs-documentation-verification): local links/anchors, 82 table/card pairs and their 18 fields, dependency agreement/acyclicity, complete R/T coverage, protected-source hashes, documentation-only scope and whitespace. PDF/ANALYSIS/approved plan are unchanged. No install, app generation, type/lint/build/runtime test, account setup, service startup, secret creation, deployment, staging, commit or push occurred.

## 8. Recommended next action

The owner completes and records **S0** using [SETUP](../SETUP.md), noting later device/browser access gaps, then requests **PLAN 0A**. A concrete 0A plan must be approved and saved before an explicit implementation instruction. No application part begins automatically. The owner may review the documentation diff and commit manually. Live editing ownership and current evidence are in [HANDOFF](HANDOFF.md).

## Appendix A. Capability traceability

Physical page references link to the blueprint; section topics follow ANALYSIS §3. **P** = PDF, **U** = owner addition, **E** = engineering interpretation. MVP includes necessary foundation/reliability work. **D** = pure domain/property, **C** = component, **S** = real storage, **A** = real API/PostgreSQL, **W** = browser, **N** = installed Android, **Q** = qualified/rights review, **PIL** = observed pilot, **OP** = operational rehearsal. Architecture numbers refer to [ARCHITECTURE](../ARCHITECTURE.md); part numbers to [task cards](../../task.md#part-cards). First validation is the earliest meaningful proof for that row; later listed parts complete integration. All tests are Not run. Scope/gate column says where approval or a future part is still needed.

| ID / PDF page, topic / source | Independently verifiable capability | Release | Architecture | Implementation part(s) | First validation | Required assertion / T ID / layer | Gate or gap |
| --- | --- | --- | --- | --- | --- | --- | --- |
| R01a / 1–2,24 audience / P | Use each module independently | MVP | 2.1,6.3 | 1,16,21 | 1 | Sleep-only onboarding; disabled module absent from evaluation; T07/T22, C/W/N | O1; full pilot 43 |
| R01b / 1–2,24 audience / P | Adult, non-wearable wellness scope | MVP | 7.3,14.3 | 14,37,43 | 14 | No unsupported prescription or wearable prerequisite; T27/T33, Q/PIL | O5/O9 |
| R02 / 1–3,15 principles / P | Understand feedback and choose a manageable next action | MVP | 2.1,7.3 | 21,37,43 | 37 | No punitive streak/restriction; explain/dismiss; T27/T33, C/Q/PIL | O5/O9 |
| R03a / 2–4,12 control / P | Disable module without deleting history | MVP | 2.1,6.2–6.3 | 1,16,21,37 | 1 | Stop prompts, retain history and dated eligibility; T07/T22, D/C/W/N | — |
| R03b / 2–4,12 control / P | Choose visible metrics and recommendation tone | MVP | 2.1–2.2,7.3 | 1,15,37 | 1 | Preference survives restart; hiding/tone does not change facts; T22/T26, C/S | — |
| R04a / 3,20–22 simulation / P | Preview busy-day plans without changing actual work | Later | 8,14.2 | 49,61 | 49 | Preview has no record/plan mutation until acceptance; T34, D/W/N | O5/T34 promotion |
| R04b / 15,20–22 engagement / P | Optional mosaic/comeback experience | Later/Research | 2.2,14.2 | 58, selected prototype | 58 | Celebration opt-out/reduced motion; no fabricated completed work; T25/T34, C/PIL | Fresh plan for unselected variants |
| R05a / 4,19 onboarding / P | Select goals/modules and preview assumptions | MVP | 2.1,6.2 | 1,13,14 | 1 | Relevant questions only; target acceptance next day; T22/T05, C/D | Estimate O5 at 14 |
| R05b / 4,19 onboarding / P | Save first useful entry | MVP | 2.1,5.1 | 1,3,5,8 | 1 | Note save preserves selected date; full three-module baseline at 8; T01/T22, S/W/N | Staged acceptance F06 |
| R06a / 4–5 profile / P | Reuse shared profile without forcing unrelated inputs | MVP | 2.1,4.2 | 1,13 | 1 | Sleep-only asks no calories/weight; later module reuses answers; T22, C/W/N | — |
| R06b / 4–5 profile / P | Decline formula inputs and use manual target | MVP | 6.2,7.3 | 13,14 | 13 | Blank differs from zero; declined input retains usable manual path; T14/T27, D/C/Q | O5 for estimates |
| R07a / 4,19 guest / P+U | Guest save without account/network | MVP | 1.2,5.1,5.5 | 0I,0J,1,3,5,8 | 0I/0J | Unlocked local save/relaunch while API absent; T19/T22, S/W/N | O4 before real data |
| R07b / 4,19 accounts / U+E | Optional signup and explicit guest import | MVP | 5.5,10.1 | 22,27 | 22 | Existing account choice; interrupted import retries same identities; T20/T21, A/W/N | O4 |
| R08a / 4,12–13 controls / P | Stable tabs, simple/detailed mode and history access | MVP | 2.1–2.2 | 1,15,38 | 1 | Hidden module reachable via history/settings; errors remain visible; T22/T25, C/W/N | — |
| R08b / 4,12–13 controls / P | Restore preferences and review old goal on re-enable | MVP | 2.1,6.2 | 1,13,16 | 1; target proof 13 | Old goal review never silently rebinds history; new activation next day; T22/T05, D/C/S | F08 fixed |
| R09a / 4 Add / P | Add Food/Workout/Sleep using selected date | MVP | 2.1,6.1 | 1,3,5,8,9 | 1; module saves 3/5/8 | Display selected date; edits/undo affect intended day; T01/T22, C/S/W/N | No fake placeholder saves |
| R09b / 4 Add / P+E | Minimal Weight and Note entry with undo | MVP | 2.1,4.2,5.1 | 1,23B | 1 | Store dated measurement/note once; undo restores prior projection; T01/T19/T22, D/S | — |
| R10 / 4,19 accessibility / P | Accessible forms, errors and non-color controls | MVP | 2.2,12 | 0E,1,38 | 0E | Keyboard/labels/targets/reduced motion; detail mode preserves errors; T25, C/W/N | Actual AT evidence at milestones |
| R11a / 5,19 targets / P | Provisional maintenance estimate with editable assumptions | MVP | 6.2,7.3 | 14 | 14 | Resting/maintenance/target distinct; no double-added exercise energy; T14/T27, D/Q | O5 |
| R11b / 5,19 targets / P | Manual target and method/input/policy snapshot | MVP | 4.2,6.2 | 13,14,23A | 13 | Historical input/policy evidence survives later edits; T05/T14, D/S/A | O3 preserved |
| R12a / 5 goals / P | Negotiate deadline/goal with alternatives | MVP | 6.2,7.3 | 14 | 14 | More time/revised goal/consistency option, no exact recomposition promise; T27, C/Q | O5 |
| R12b / 5 goals / P | Adaptive trajectory prediction | Later/Research | 14.2 | 52,61 | 52 | Held-out baseline/calibration; decline inadequate evidence; T34, D/Q | O5/T34 |
| R13a / 5–6 bars / P | Pin/remove/reorder and goal-based defaults | MVP | 2.1,6.2 | 15 | 15 | Initially at most two bars; correct goal defaults, saved order; T22/T25, C/S | — |
| R13b / 5–6 bars / P | Hide numeric values and use habit-only intent | MVP | 2.1,6.3 | 13,15,16 | 13 | Hiding never deletes nutrients or creates attainment; T07/T22/T25, D/C | — |
| R14 / 5–7 targets / P | Target zones and nutrient detail without excess reward | MVP | 6.3,7.1,9.2 | 15,16,19 | 15 | Complete intake distinct from meeting target; overage no bonus; T04/T14/T27, D/C/Q | O5 policy |
| R15a / 7,13,18,22 history / P+E | First and subsequent targets activate next journal day | MVP | 6.2 | 13,23A | 13 | Today unassessed on first activation; old snapshots unchanged; T05, D/S/A | O3 approved |
| R15b / 7,13,18,22 history / E | Competing offline target proposals remain explicit | MVP | 5.4,6.2 | 23A,24,25 | 23A | Delayed acceptance never overwrites accepted past binding; T18, A/two-client | O6 replay policy |
| R16 / 5,13–14,22,24 safety / P | Unsupported population/condition gets logging/manual path | MVP | 7.3,14.3 | 14,32,37 | 14 | Reviewed eligibility blocks unsuitable prescriptions; T27, D/Q | O5 |
| R17a / 3,6,19 Food / P | Manual text/quantity/source entry and search | MVP | 7.1–7.2 | 2,3,33 | 3 | Quantity/cooking/brand assumptions editable before confirmed save; T15/T28, D/C/A | O8 for catalog |
| R17b / 3,6,19 Food / P | Optional AI source-match proposal | MVP | 7.3 | 35 | 35 | Confirmed source/quantity drive deterministic values; no AI save authority; T06/T26, A/W/N | O8 |
| R18a / 3,6,16 uncertainty / P | Inspect source, portion and editable nutrient evidence | MVP | 4.2,7.1 | 2,3,33 | 2 | Snapshot original source and corrections; absent nutrient unknown; T15, D/S | O8 providers |
| R18b / 3,6,16 uncertainty / P | Cake/frosting clarification or preserved assumption | MVP | 7.1–7.3 | 33,35 | 33 | Eaten/original weight ambiguity cannot invent exact subtraction; T15/T26, D/provider eval | O8 |
| R19a / 6–7 nutrients / P | Nutrient-specific arithmetic and detail | MVP | 4.4,7.1 | 2,3,15 | 2 | Preserve provider energy, unit/source precision; missing protein not zero; T14/T15, D | — |
| R19b / 6–7 nutrients / P | Bars/aggregates retain unknown and approximate labels | MVP | 6.3,7.1 | 15,17 | 15 | Known subtotal stays incomplete when one required nutrient absent; T04/T15, D/C | — |
| R20a / 6,16,19 reuse / P | Repeat/copy recent meal to chosen date | MVP | 4.2,7.1 | 4 | 4 | New record identity and date; no offline duplication; T16, D/S/W/N | — |
| R20b / 6,16,19 reuse / P | Save/edit a reusable meal version explicitly | MVP | 4.2,7.1 | 4 | 4 | Today's correction never changes old entries or saved template implicitly; T16, D/S | — |
| R21a / 6–7,13,18 correction / P | Edit/delete/undo/backdate Food | MVP | 5.1,6.1,6.3 | 3,17,23B,25 | 3 | Both dates and dependent summaries invalidate; T01/T05/T23, D/S/A | O6 accepted undo |
| R21b / 6–7,13,18 coverage / P | Explicit partial/complete/unknown intake | MVP | 6.3 | 3,16,17 | 3 | Empty complete day unknown absent valid zero assertion; deleting last entry not zero; T04, D/S | — |
| R22a / 6,13,18–19 offline / P | Manual/saved Food survives crash and disconnection | MVP | 5.1 | 0I,0J,3,4 | 0I/0J; Food 3 | Save record/outbox atomically or show failure; T19, S/W/N | O4 real data |
| R22b / 6,13,18–19 outage / P | Search/AI failure preserves manual fallback | MVP | 7.2–7.3 | 33,35 | 33 | Timeout never saves late unconfirmed estimate; T06/T28, A/W/N | O8 |
| R23a / 6,16,20,22 regional / P+U | Bounded Bangladesh food/language benchmark | MVP | 7.2 | 34,35 | 34 | Rice raw/cooked, dal/oil/portions, Bengali and mixed input fixtures; T15/T28, Q/provider eval | O8 thresholds/rights |
| R23b / 6,16,20,22 regional / P | Broad regional/budget-aware proposals | Later | 14.2 | 65 | 65 | Price/source/date uncertainty and affordable alternative reviewed; T34, Q/eval | O8 promotion |
| R24a / 6,13,20 recipes / P | Batch recipe/yield versions | Later | 4.2,14.2 | 48 | 48 | Yield/serving conversion preserves historical snapshots; T16/T34, D/S | T34 |
| R24b / 6,13,20 portions / P | Personal containers and visual portion guidance | Later | 7.1,14.2 | 48 | 48 | Unknown bowl mass not exact grams; editable assumptions; T15/T34, D/C/Q | O8 content |
| R24c / 6,13,20 affordability / P | Affordable suggestions | Later | 14.2 | 65 | 65 | Regional price provenance and approved bounds; T34, Q/eval | O5/O8 |
| R25a / 6,16,20–21 input / P | Barcode food lookup | Later | 2.3,14.2 | 53 | 53 | Denied camera/unknown barcode/manual fallback; T34, A/W/N | O8/plugin approval |
| R25b / 6,16,20–21 input / P | Photo food proposal | Later/Research | 2.3,7.3,14.2 | 54 | 54 | No exact grams from image; correction and media expiry; T26/T34, eval/N | O8 consent/retention |
| R25c / 6,16,20–21 input / P | Voice food input | Later/Research | 2.3,7.3,14.2 | 55 | 55 | Language/error benchmark, denied mic and manual fallback; T34, eval/N | O8 |
| R25d / 6,16,20–21 input / P | Nutrition-label OCR | Later/Research | 7.1,14.2 | 56 | 56 | Unit/serving correction before confirmation; T15/T34, D/eval | O8 |
| R25e / 16 corrections / P | Explicit remembered correction | MVP saved reuse | 7.1 | 4 | 4 | Remember changes saved version only on explicit choice; T16, D/S | Rich learned parser at 60 |
| R25f / 16,20–21 memory / P | Private on-device food model | Research | 14.2 | 60 | 60 | Beat simple retrieval on approved regional/device metrics; T34, eval/N | O8 promotion |
| R26 / 8,19 Workout / P | Relevant training inputs and equipment profiles | MVP | 2.1,8.1 | 1,7,8,32 | 7 | Home/gym/travel context, exclusions and declined Workout respected; T22/T27, D/C/Q | O5 generation |
| R27a / 8,19 routines / P | Manual routine builder | MVP | 8.1–8.2 | 8 | 8 | Editable draft never becomes performed work; T02/T10, D/S/W/N | — |
| R27b / 8,19 routines / P | Vetted template or constrained proposal | MVP | 7.3,8.1 | 32 | 32 | Reviewed catalog/equipment/exclusions; acceptance required; T27, D/Q | O5/O8 |
| R28a / 8–9 set types / P | Warm-up/working and typed load/work modes | MVP | 4.4,8.1 | 8,9,23C | 8 | Timed/distance/bodyweight/assistance/unilateral not forced into kg/reps; T14, D/S | — |
| R28b / 8–9 history / P | Last comparable completed actuals | MVP | 8.1 | 8,9,23C | 9 | Match exercise/equipment/set kind/load convention; undone/no-match yields no invented value; T09/T14, D/S/A | F08 clarified |
| R29a / 9,22 complete / P | Checking a set immediately persists actual values | MVP | 5.1,8.2 | 9 | 9 | Displayed/edited actuals plus stable ID and completion time survive crash; T02/T19, S/N | — |
| R29b / 9,22 complete / P | Edit/recheck preserves performed identity | MVP | 8.2–8.3 | 9,23C,25 | 9 | One logical performed ID through edit/undo/recompletion; T09, D/S/A | — |
| R30a / 9 quick-complete / P | Zero-performed Complete all N sets | MVP | 8.2 | 10 | 10 | Explicit counted confirmation, exact N actuals and Undo; T08, D/C/W/N | — |
| R30b / 9 finish / P | Partial Finish versus Complete remaining | MVP | 8.2 | 10 | 10 | Finish after 2/3 keeps two actuals; separate action completes remainder; T02/T08, D/S/W/N | — |
| R31a / 9,19,22 session / P | Explicit partial/full Finish with recap | MVP | 8.2–8.3 | 10 | 10 | Remaining work skipped; checked-all still needs Finish; T02/T11, D/S | O3 approved |
| R31b / 9,19,22 interruption / P | Resume interrupted session | MVP | 5.1,8.3 | 9,10 | 9 | Crash/close retains checked sets and does not finish session; T19, S/W/N | — |
| R32a / 9 undo / P | Undo completion/Finish locally | MVP | 8.3 | 9,10,11 | 9 | Totals recompute; undo Finish preserves checked sets; T09/T11, D/S | — |
| R32b / 9 undo / E | Conditional accepted compensation | MVP | 5.4,8.3 | 23C,25 | 23C | Guard session and schedule revisions; later foreign edit not overwritten; T09/T11, A/two-client | O6 undo horizon |
| R33 / 8–9 versions / P | Today-only versus future routine edit | MVP | 4.2,8.2–8.3 | 12,23C | 12 | Old original-plan snapshot unchanged; future version explicit; T10, D/S/A | — |
| R34a / 8–9,14,20 stability / P | Stable basic movements and comparable history | MVP | 8.1 | 7,8,9,32 | 7 | Catalog identities stable; no numeric transfer between unlike exercises; T14/T27, D/Q | O5/O8 templates |
| R34b / 8–9,14,20 progression / P | Reviewed progression/variation proposal | Later | 14.2 | 51 | 51 | Comparable actual evidence and explicit acceptance; T34, D/Q/eval | O5 |
| R34c / 8–9,14,20 tools / P | Demos, timers, supersets, effort ratings | Later | 14.2 | Unassigned future bounded part | Future promoted part | Separate timer/state, effort meaning and licensed demo assertions; T34, C/N/Q | Explicit gap; not MVP |
| R35 / 10,19 scheduling / P | Calendar slot independent of session sequence | MVP | 8.3 | 11,23C | 11 | Missed day creates no automatic doubled work/debt; T11, D/S/A | — |
| R36a / 10,19 scheduling / P+E | Move occurrence without consuming it | MVP | 8.3 | 11 | 11 | Same occurrence ID, preview consequences; T11, D/S | O3 approved |
| R36b / 10,19 scheduling / P+E | Deliberate skip/finish consumes once | MVP | 8.3 | 11,23C,25 | 11 | Retry exactly once; lateness/crash never advances sequence; T11/T30, D/A | O3 approved |
| R37 / 4,10,13 extra work / P | Rest day/custom session preserves next planned work | MVP | 8.3 | 8,10,11 | 11 | Extra actuals counted but no implicit occurrence replacement; T11/T27, D/S | O5 advice |
| R38a / 10,13,22 pause / P | Pause travel/week/module without penalty | MVP | 6.2–6.3,8.3 | 1,11,16 | 1 | Paused/rest/disabled differ from missing; resume retains history; T07/T11/T17, D/C | — |
| R38b / 10,13,22 reminders / P | Reshape scheduled reminders | Later | 2.3,14.2 | 57 | 57 | Pause/opt-out cancels delivery; no nag escalation; T34, N | Permission/promotion |
| R39a / 3,10,20 capacity / P | Full/compact/minimal session preview | Later | 14.2 | 49 | 49 | Removed work visible; do not cut rest blindly; T34, D/Q | O5 |
| R39b / 3,10,20 substitutions / P | Equipment substitution/reordering | Later | 14.2 | 50 | 50 | Reviewed equivalence or explicit no suitable substitute; T34, D/Q | O5/O8 |
| R40a / 10,13–14,20 return / P | Pause and manually reduce/revise intent | MVP | 6.2,8.3 | 1,11,12 | 11 | No debt or exact detraining claim; changes require action; T11/T27, D/C | — |
| R40b / 10,13–14,20 return / P | Adaptive re-entry proposal | Later | 14.2 | 51 | 51 | Pain/illness suppress automatic progression; T34, D/Q | O5 |
| R41a / 4,11,19 Sleep / P | Duration with optional timing/restfulness | MVP | 9.1 | 5 | 5 | No fabricated start/end/stages; typed optional values; T12, D/S/W/N | — |
| R41b / 4,11,19 Sleep / P | Configurable sleep target | MVP | 6.2,9.1 | 5,13,15 | 13 | Dated range, no recovery certification; T05/T27, D/C | O5 automated guidance |
| R42 / 7,11,19 attribution / P | Overnight/split sleep, naps and chosen journal date | MVP | 6.1,9.1 | 5 | 5 | Wake-date default, user choice, period shown only when known; T12/T13, D/W/N | — |
| R43a / 11,13,17 overlap / P | Reconcile manual sleep overlaps | MVP | 9.1 | 6 | 6 | Union confirmed continuous intervals; container/duration ambiguity unresolved; T12, D/S | — |
| R43b / 11,13,17 sources / P | Reconcile imported and manual sleep | Later | 9.1,14.2 | 45 | 45 | Stable source IDs/revisions; manual corrections not overwritten; T12/T34, A/N | O8/consent |
| R44 / 11–12 Sleep insight / P | Duration/coverage and only available regularity | MVP | 6.3,9.1,7.3 | 17,21,37 | 17 | No timing means no regularity; duration alone not readiness; T12/T17/T27, D/Q | O5 suggestions |
| R45a / 11,20 safety / P | General support without diagnosis | MVP | 7.3 | 37 | 37 | Reviewed persistent-difficulty wording; no exact debt repayment; T27, Q | O5 |
| R45b / 11,20 context / P | Optional caffeine/travel/disturbance context | Later | 14.2 | 59, one selected input | 59 | Decline/delete sensitive context without breaking sleep log; T34, C/S | Fresh plan for remaining inputs |
| R45c / 11,20 reminders/import / P | Optional reminder and wearable context | Later | 2.3,14.2 | 57,45 | 45/57 | Denied/revoked still leaves manual Sleep functional; T32/T34, N | Permission/consent |
| R46a / 7,19 calendars / P | Day entry and drilldown | MVP | 9.2 | 18 | 18 | Selected date consistent across module/Add/history; T01/T25, C/W/N | — |
| R46b / 7,19 calendars / P | Monthly selectable days and twelve yearly tiles | MVP | 9.2 | 19,20 | 19; year 20 | Accessible text meaning and correct drilldown; T17/T25, C/W/N | — |
| R47 / 7 rings / P | Attainment/partial/unknown/rest/paused/disabled distinctions | MVP | 6.3,9.2 | 16,17,19 | 16 | Performed work and sufficient nutrition evidence only; no unlimited-sleep reward; T04/T07/T17, D/C | O5 ranges |
| R48a / 7,11,22 dates / P | Midnight view rollover and backdated late event | MVP | 6.1 | 0C,1,3,5 | 0C; UI 1/3 | Journal date independent of instant/zone/save time; T01/T13, D/W/N | O1 Hermes parity |
| R48b / 7,11,22 dates / E | Custom day-boundary settings UI | Later | 6.1,14.2 | Unassigned future part | Future promoted part | New default boundary never rewrites old attribution; T13/T34, D/W/N | Explicit gap; not MVP |
| R49a / 7,12,22 coverage / P | Nutrient-specific known-day denominators | MVP | 6.3 | 16,17 | 17 | Missing intake/sleep not zero; different nutrient coverage disclosed; T04/T17, D | — |
| R49b / 7,12,22 trends / P | Compare like periods and historical eligibility | MVP | 6.2–6.3,9.2 | 17,20 | 17 | Partial month/year labeled; old enabled/paused periods retained; T17, D/W/N | — |
| R50 / 7,13,18,22 correction / P | Rebuild old/new dates, periods and stale narratives | MVP | 6.3,7.3 | 17,24,36 | 17 | Goal binding retained and delayed narrative rejected after correction; T05/T18/T26, D/A/W | — |
| R51 / 12,19 Overall / P | Enabled-module cards and one primary action | MVP | 2.1,7.3 | 21,37 | 21; action 37 | No fourth journal or global verdict; Why/easier/dismiss work; T22/T27, C/Q | O5 action rules |
| R52 / 12–14,18 priorities / P | Conservative evidence-aware prioritization | MVP | 6.3,7.3 | 37 | 37 | Partial Food not low intake; conflicting evidence explained; T04/T27, D/Q | O5 |
| R53a / 12,18–19 explanation / P | Retain rule/evidence provenance | MVP | 4.2,7.3 | 36,37 | 36 | Explanation cites supplied revisions; no unsupported cause; T26/T27, D/A | O5/O8 |
| R53b / 12,18–19 tone / P | Tone/dismissal/module controls respected | MVP | 2.1,7.3 | 1,37 | 37 | Style cannot change numeric facts or revive disabled advice; T22/T26, C/A | — |
| R54a / 7,12,18–19 summaries / P | Factual day/month/year summary | MVP | 6.3,7.3 | 17,36 | 36 | Computed stats/coverage agree; sparse evidence labeled; T05/T26, D/W/N | — |
| R54b / 7,12,18–19 summaries / P | Bounded optional narrative and fallback | MVP | 7.3 | 36 | 36 | Reject extra numbers/injection/stale facts; template works without AI; T06/T26, A/W/N | O8 |
| R55a / 12,14,17,20 reflection / P+E | Basic descriptive weekly reflection | MVP | 7.3 | 36,37 | 37 | One manageable reflection from actual evidence, no precise body-composition inference; T27, D/Q | O5 |
| R55b / 12,14,17,20 adaptation / P | Plateau/adaptive target review | Later | 14.2 | 51,52 | 51/52 | Comparable evidence and reviewed bounds before accepted change; T34, Q/eval | O5 |
| R55c / 12,14,17,20 experiments / P | Future planning and personal experiment | Research | 14.2 | 61,62 | 61/62 | Baseline/non-actioning evaluation and one accepted factor; T34, Q/eval | O5/O9 |
| R56a / 6,9,13,18–19 persistence / P+U+E | Atomic local manual save | MVP | 5.1 | 0H,0I,0J,1–10 | 0I/0J | Projection/outbox/undo/invalidation all or none; T19, S/W/N | O4 |
| R56b / 6,9,13,18–19 resume / P | Resume drafts distinct from actual work | MVP | 5.1,8 | 3,5,8,9,10 | 3; workout 9 | Crash retains committed state; unsaved draft not performed; T02/T19, S/W/N | — |
| R57a / 18,22 identity / P+E | Stable records and immutable operation retry | MVP | 4.1,5.2–5.3 | 0B,0H,23,24 | 0B; server 23 | Lost ack retries identical seal; receipt checked before revision; T03/T30, D/A | O6 replay |
| R57b / 18,22 ordering / E | Account-ordered feed and atomic cursor apply | MVP | 5.3,11.2 | 23,24 | 23 | Concurrent commits cannot skip a late change; page/cursor all or none; T30, A/S | — |
| R58a / 18–19 ownership / P+U | Authenticated account synchronization/isolation | MVP | 5.5,10.1 | 0K,22,23A–23C,24 | 0K | Authorize every parent/reference/cursor; stale account response rejected; T21, A/W/N | O4 |
| R58b / 18–19 conflict / P+E | Visible competing edits and preserved intent | MVP | 5.4 | 25,26 | 25 | No timestamp winner/automatic destructive rebase; T09/T18/T30, A/two-client | O6 |
| R59a / 13,18–19 status / P | Save/estimate/sync/error statuses remain separate | MVP | 2.3,5.2 | 3,9,22,24,25 | 3 | Local saved does not mean synced or estimate confirmed; T19/T21, C/S | — |
| R59b / 13,18–19 recovery / E | Foreground/reconnect/manual sync; expiry retains work | MVP | 5.2,5.5 | 22,24 | 22 | Background execution unnecessary for correctness; expired session never erases outbox; T19/T21, A/N | — |
| R60a / 18–19 privacy / P+E | Delete raw and derived data with tombstones | MVP | 5.4,10.3 | 30 | 30 | Stale updates cannot resurrect; recommendation/cache/job artifacts covered; T23, A/OP | O6 |
| R60b / 18–19 restore / E | Independently current suppression before service reopens | MVP | 10.3,13.2 | 31 | 31 | Restore backup predating deletion, account still suppressed; T31, OP | O6/O7 |
| R61a / 18–19 migration / E | Three storage migration tracks preserve pending work | MVP | 4.4,5.1 | 0D,0I,0J,26,40 | 0D; local 0I/0J | Failed upgrade enters recovery, never silently recreates store; T19/T30, A/S/N | Every persisted-shape plan |
| R61b / 18–19 shell / E | Compatible offline shell upgrade across tabs | MVP | 11.3,13.2 | 0L,40 | 0L | No forced update over dirty editor; no private API precache; T24, W | Actual Safari 0N |
| R61c / 18–19 expired replay / E | Rebootstrap preserves pending evidence through export | MVP | 5.4,11.3 | 26,28,41 | 26; end-to-end 41 | Old store retained until pending intent reconciled/exported; T23/T29/T30, S/A/W/N | F07; O6 horizon |
| R62a / 4,13,18–19 autonomy / P | Numeric/module controls preserve records | MVP | 2.1,6.2 | 1,15,22,38 | 1 | Hide/disable differs from delete; T07/T22/T25, C/S | — |
| R62b / 4,13,18–19 permissions / P | Consent and health-platform permission controls distinct | MVP explanation; Later integration | 2.3,10.3 | 22,0M,45 | 0M capability; 45 product | Denied/revoked integration leaves journal/manual entry intact; T32/T34, N | O8 and promoted scopes |
| R63a / 18 security / P | Protect web/native journals and credentials | MVP gate | 5.1,10.1–10.2 | 0I,0J,0K,22,39 | 0I/0J | Protected at rest, lock/recovery/error behavior, no journal in SecureStore; T19/T21/T32, S/N | O4 |
| R63b / 18 security / P | TLS, server/backup protection, access limits | MVP gate | 10,13.2 | 31,39,42 | 31/39 | Restore/least privilege/redacted logs; bundles have no secrets; T21/T31, A/OP | O6/O7 |
| R64a / 18,20 processing / P | Disclosed bounded processing; no sensitive telemetry/training default | MVP policy | 7.3,10 | 35,36,39 | 35 | Consent/caps/fallback and no health bodies in logs; T26/T28, A/Q | O8 terms |
| R64b / 18,20 raw media / P | Purpose-limited photo/audio retention | Later | 10.3,14.2 | 54,55,63 | Promoted media part | Expiry/deletion of raw and derived artifacts; T23/T34, A/N/Q | O6/O8 |
| R65a / 13,18–20 export / P+E | Free local JSON/CSV with complete labels | MVP | 10.3 | 28 | 28 | Dates/units/history/disabled modules/pending status; CSV injection neutralized; T29, file/W/N | Export not import/restore |
| R65b / 13,18–20 export / P+E | Owned account export jobs and expiry | MVP | 10.3 | 29 | 29 | Correct snapshot scope, no foreign/expired download, no secrets; T29, A/OP | O6 |
| R65c / 13,18–20 deletion / P | Free account deletion with honest device limits | MVP | 10.3 | 30,31 | 30 | Bound proof, 401/403/timeout never purges local data; T23/T31, A/N/OP | O6 |
| R66 / 4,7,15,19 accessibility / P+E | Accessible progress/calendar and assistive-tech flows | MVP | 2.2,9.2,12 | 0E,38,41 | 0E | Text alternatives, zoom/reflow, keyboard, TalkBack/Safari evidence; T25, C/W/N | No automated-only conformance claim |
| R67a / 16,20–21 memory / P | Approved saved-food reuse | MVP | 7.1 | 4 | 4 | Explicit update, new copied IDs, old snapshots retained; T16, D/S | — |
| R67b / 16,20–21 model / P | Personal parser/retrieval research | Research | 14.2 | 60 | 60 | Compare simple retrieval; regional error/latency/memory/battery; T34, eval/N | O8 promotion |
| R68 / 17,21 simulation / P | Feasible future planner | Research | 14.2 | 61 | 61 | Constraint feasibility, uncertainty, held-out baseline; no live mutation; T34, D/eval | O5/O8 |
| R69a / 11,13,17,20 integration / P+U | Health Connect feasibility then optional sleep ingestion | Foundation proof; Later product | 2.3,9.1,13.3 | 0M,45 | 0M | Supported/empty/denied/unsupported read without product ingestion; source revisions at 45; T32/T34, N | Plugin approval/consent |
| R69b / 11,13,17,20 integration / P | Weight/steps/workout imports, other platforms/HealthKit | Later | 14.2 | Unassigned future parts | Future promoted parts | Ownership/source revision/overlap/permissions by type; T34, A/N | Explicit gap; no iOS decision |
| R70a / 15,20–21 engagement / P | Preparation prompts and private atlas/comeback prototype | Later/Research | 14.2 | 57,58 | 57/58 | Opt-out, no pressure, private defaults; T34, N/PIL | Selected scope only |
| R70b / 15,20–21 cooperation / P | Opt-in groups share selected intentions | Later | 14.2 | Unassigned future part | Future promoted part | Weight/calories/notes private by default; consent/revocation; T34, A/Q | Explicit gap; separate ownership design |
| R71a / 20–21 context / P | One optional hydration/body/cycle context input | Later | 14.2 | 59 | 59 | Explicit sensitive-data opt-in, delete/decline works; T34, S/Q | Unselected inputs need own plan |
| R71b / 20–21 experiments / P | Conservative personal experiment protocol | Research | 14.2 | 62 | 62 | No unsafe restriction experiment, reviewed outcome limits; T34, Q/eval | O5/O9 |
| R71c / 20–21 camera / P | Camera-assisted training notes | Research | 14.2 | 63 | 63 | No technique-safety certification; consent/retention/fallback; T34, Q/N | O8 |
| R71d / 20–21 household / P | Household recipe-sharing feasibility | Later/Research | 14.2 | 64 | 64 | Separate ownership/personal portions/private journals; T34, A/Q | O8/O9 |
| R72a / 20,22,24 validation / P | Adult imperfect-week pilot | MVP research | 12.2,13.3 | 43 | 43 | Observe first save, correction, return, trust and pressure across specified users; T33, PIL | O4–O9 |
| R72b / 20,22,24 market / P | Willingness to pay and monetization choice | Later decision | 14.2 | 43 may research; billing unassigned | Approved research/future part | No invented market/clinical success; privacy/export never paywalled; T33/T34, PIL | No billing implementation approved |
| R73a / 14 burden / P+E | User invokes saved meals/fewer bars/habit-only | MVP | 2.1,6.3,7.3 | 1,4,15,37 | 4 | Less data reduces confidence, not user standing; T22/T27, C/Q | — |
| R73b / 14 burden / E | Automatic sporadic-logging detector | Later | 14.2 | Unassigned future part | Future promoted part | User can reject simplification; no pressure/reminder escalation; T34, Q/PIL | Explicit gap; no guessed trigger |
| R74 / 15 discoveries / P | Evidence-supported private discovery cards | Later | 14.2 | 58, if selected | 58 | Association not causation; dismiss/no-evidence behavior; T34, D/PIL | Fresh plan for broader feature |

## Appendix B. Platform risks and earliest proof

Every row is a documentation assessment, with runtime verification Not run. Required environments must be named in each concrete plan.

| Risk / severity | Mitigation and source | Earliest validating part / environment | Failure consequence |
| --- | --- | --- | --- |
| Universal navigation/responsive forms / HIGH | Thin Router routes, shared use cases, measured width, native back/keyboard/safe area; architecture §2 | 0E browser then 0G installed APK; integrated 0N | Block M0 if fundamental interaction cannot meet both platforms. |
| Paper styling/focus/accessibility / HIGH | Wrappers/tokens; platform escape hatches confined to UI, text alternatives and reduced motion; §2.2 | 0E keyboard/browser; 0G TalkBack/large text; actual Safari 0N | Replace/fix bounded widget under approved plan; do not assume RN support proves web accessibility. |
| English/Bangla font and input / MEDIUM | Licensed glyph-complete assets and realistic mixed-language fixtures; §§2/7.2 | 0E shell, 0G Android; regional input 34 | Record missing glyph/input issue; no silent language degradation. |
| DOM/Node/private imports leaking / HIGH | Strict target libs, four packages, `.web`/`.native` adapters and composition roots; §3.2 | 0A negative import checks, 0B DTOs, both bundles 0E/0G | Stop affected build; never solve by global DOM/Node ambient pollution. |
| pnpm/autolinking/duplicate React / HIGH | One compatible pinned workspace; exact version record; §13.1 | 0A resolve, 0E web, 0G native build/CI | O1 remains open; no independent latest-version upgrades. |
| DTO/runtime-object leakage / HIGH | Portable dates/decimal strings/UUIDs, strict schemas; §§4/11 | 0B roundtrip, 0G Hermes/API | Reject ORM/Luxon/platform objects at public boundaries. |
| Hermes Intl/date/unit differences / HIGH | Injected clock/date adapter, DST gap rejection/ambiguity choice; §§4.4/6.1 | 0C Node then 0G/0N real Hermes/browsers | Wrong date/amount blocks core; no timestamp-based journal inference. |
| Browser protected storage / HIGH | Encrypt before short generation-checked transaction; no network/crypto wait inside; §5.1 | 0I real IndexedDB multiple tabs/quota/abort; Safari 0N | No false save; protected recovery required. O4 still gates real data. |
| Native protected storage / HIGH | Scoped SQLite transactions, SQLCipher candidate, small key material in SecureStore; §§5.1/10.2 | 0J installed build, file/side-file inspection, kill/relaunch | Expo Go/mock success insufficient; key loss/backup policy unresolved under O4. |
| Native auth differs from browser cookies / HIGH | Browser HttpOnly same-site/CSRF versus native session header adapter; §10.1 | 0K HTTPS browser/local email and installed APK deep-link roundtrip | Pending local work survives expiry; no custom token storage workaround without review. |
| Device localhost/network lifecycle / MEDIUM | Per-target public origin, explicit offline state, foreground/reconnect/manual sync; §§1.2/5.2 | 0G API reachability, 24 reconnect/two-client | Show network failure; cannot make local save depend on network/background scheduling. |
| Download/export platform API / MEDIUM | Files port; web download and native file/share adapters; §2.3/10.3 | 28 browser and installed Android files | Exported contents and cleanup checked; UI success alone insufficient. |
| Service worker leaking into native / HIGH | Web-only registration/public shell precache; §11.3/13.2 | 0L exported web and native build regression | No private API caching or force update over active editor. |
| Camera/barcode/voice / MEDIUM | Optional capability ports and denied/cancel/unsupported states; §2.3 | 53/54/55/56/63 after promotion | No current plugin installed; denial preserves manual workflows. |
| Notifications / MEDIUM | Optional scheduling adapter, permission/time-zone/pause handling; §2.3 | 57 device scheduling/revocation | No MVP delivery guarantee; no presumed background execution. |
| Health Connect / HIGH | Isolated capability/read/denied spike first; source IDs/corrections for later ingestion; §9.1 | 0M installed device/emulator; product 45 | Unsupported returns explicit result; feasibility cannot silently ingest records. |
| Build/CI/native ownership / HIGH | Generated Android ignored, config/plugins source truth, installed smoke CI and equivalent local checks; §§12/13.3 | 0G APK/CI then affected changes | Do not defer native proof to release or hand-maintain generated output silently. |
| Signing/OS floor/distribution / HIGH | Website first; release-like upgrades, identity review, protected signing; §13.3 | 46 physical release matrix, 47 signed artifact | No store publication/account purchase authorized now; current SDK floor is not product support promise. |

## Appendix C. Data and task feasibility review

### Data under failure and correction

| Walkthrough | Required documented outcome / authority | First proof → integrated proof |
| --- | --- | --- |
| Local save → transaction failure/crash | UUID and pending intent allocated locally; projection/outbox/undo/invalidations commit together or none. Crypto prepared before short IDB CAS; unrelated native async query excluded. Architecture §§4.1/5.1. | 0H–0J T19 → feature saves/40/41 |
| Server commits → acknowledgement lost → retry | Same sealed operation ID/body; receipt lookup before revision comparison; receipt/revisions/account change group one transaction. No false duplicate/conflict from replay. §§5.2–5.3. | 23 T03/T30 → 24/41 |
| Competing commits → paged pull → crash | Account-ordered commit sequence; authorize cursor and references; pull changes/cursor committed atomically; no skip of late commit. §§5.3/11.2. | 23/24 T30 → 41 |
| Account A request returns after switching to B | Namespace/session generation rejects stale result, locks/clears appropriate caches; verified server identity determines ownership. §§5.5/10.1. | 0K/22 T21 → 39/41 |
| Offline goal activated then delivered after another device | Requested effective date retained; no replacement of accepted historical binding; conflict retains candidate intent; all first/subsequent activations next journal day. §6.2. | 13/23A T05/T18 → 25/41 |
| Last meal deleted or date moved | Empty complete is not zero without distinct valid assertion; old/new dates, periods and narratives rebuild; nutrient-specific denominator. §6.3. | 3/16/17 T01/T04/T05 → 23B/41 |
| Planned three sets → two checked → Finish → undo/recheck | Two performed IDs, third skipped; undo Finish preserves checked sets; recheck reuses identity; original plan and set kind retained. §§8.1–8.3. | 9/10 T02/T08/T09 → 23C/25/41 |
| Moved/late/custom session → finish/skip/compensation | Move preserves occurrence; crash/lateness/custom session do not consume; deliberate finish/skip once; compensation guards both session and schedule revisions. §8.3. | 11 T11 → 23C/25/41 |
| Duration-only plus overlap | No inferred endpoints/stages; union only confirmed continuous intervals; reconcile time-in-bed container overlap or uncertain duplicates. §9.1. | 5/6 T12/T13 → 23B/41; imports 45 |
| Schema/shell upgrade → expired replay | Three independent migration tracks preserve pending data; failed upgrade recovery; no forced reload; review/export before removing old evidence. §§4.4/5.4/11.3. | 0I/0J/0L/26 T19/T24/T30 → 28/40/41 |
| 401/403/timeout → deletion claim → old backup restored | Authentication error never purges. Definitive account/device-bound proof required. Independently retained current suppressions applied before service opens after restore. §§5.4/10.3. | 30/31 T23/T31 → 39/42 |
| AI response arrives after correction or contains injected policy/numbers | Check draft/evidence versions, permitted IDs and supplied numeric facts; no write tools; factual/manual fallback. §7.3. | 35/36 T06/T26/T28 → 39/41 |

These walkthroughs found no unresolved contradiction in the approved state model. Concrete storage schemas, SQL locking strategy and migration implementation still require each part's approved design and real tests. In particular, “atomically” in prose does not establish crash safety, and “encrypted” does not establish key recovery or metadata privacy.

### Reverse task coverage and ordering

All 82 cards have the specified 18 fields, meaningful scoped acceptance, explicit testing layers and separate PLAN/IMPLEMENT recommendations. Direct dependencies match the summary table, reference existing parts (S0 is the external manual prerequisite), and form an acyclic graph. Semantic review went beyond graph syntax and produced F01/F06/F07/F09. No direct edge was changed. All 82 remain Not Started with empty completion boxes.

| Parts reviewed | Product or engineering justification / decision | Earliest dependency and acceptance conclusion |
| --- | --- | --- |
| 0A–0D | R48/R56–R63; D2/D4/D8/D12: tooling, portable DTOs, date/units, isolated API/PG | S0 first; built-in Node checks 0A, Vitest 0B, real PG 0D. No phantom runner requirement. |
| 0E–0G | R10/R66, D1/D3/D11/D12: UI/browser/component tests and early Android | 0E owns its runner/binaries; 0F CI consolidation; installed native 0G. |
| 0H–0N | R56–R63/R69; D5–D7: contracts, protected stores, auth, offline shell, bounded health spike | Synthetic stores before core; 0K includes security at first auth use. 0N closes all foundation evidence, not merely builds. |
| 1–6 | R05–R10/R17–R22/R41–R43; D3/D5/D8/D9 | Independent onboarding/manual Food/Sleep, preserved-source arithmetic and overlap. Combined baseline tested by 8. |
| 7–12 | R26–R40; D8/D10 | Catalog/manual drafts before actual sets and explicit finish; schedule before future routine versions. |
| 13–17 | R11–R16/R47–R50; D8/D10 | Manual snapshots precede reviewed estimates, bars and aggregation; coverage before conclusions. |
| 18–21 | R46/R49–R54; D3/D8/D11 | Reliable dated records/aggregates before calendars and factual Overall; no AI prerequisite. |
| 22–23, 23A–23C | R07/R15/R56–R63; D6/D7 | Product identity before acceptance/feed and entity server commands; server-private schemas and ownership at first use. |
| 24–27 | R57–R61; D6 | Kernel/entity commands precede coordinator/conflict/bootstrap/import. Pending preservation now; export integration 28/41. |
| 28–31 | R60/R63/R65; D7/D12 | Local export, server jobs, tombstones/proof, independent suppression restore all present before release. O6/O7 remain explicit. |
| 32–37 | R11/R17–R19/R23/R27/R51–R55; D9/D10 | Trusted manual records and policies precede vetted routines, regional search, AI proposals and summaries; O5/O8 block unreviewed content. |
| 38–41 | R56–R66 and T01–T32; D11/D12 | Accessibility/security/upgrade/performance plus cross-platform acceptance. This consolidation does not defer early security/native obligations. |
| 42–44 | R63/R72; D12 | Approved staging/operations → observed adult pilot → separately authorized website promotion, with restore and rollback. |
| 45–47 | R69 and owner web-first Android direction; D1/D12 | Optional sleep integration after website; native hardening does not require 45; separate signing/release preparation. |
| 48–52 | R24/R34/R39/R40/R55; D8/D10 | Post-MVP recipes, capacity/substitution, progression/target evaluation with T34 gates. |
| 53–57 | R25/R38/R45; D1/D9/D10 | Optional barcode/photo/voice/OCR/reminders retain denial and manual fallback; no premature plugins. |
| 58–65 | R04/R23/R67–R74; D7/D9/D10 | Individually bounded engagement/context/food model/simulator/experiment/camera/household/budget evaluations. No blanket research promotion. |

D1–D12 each have an owning foundation/feature group above; D11 accessibility is supported early and audited in 38, and D12 includes operational recovery rather than deployment alone. These engineering parts support PDF pp.18–19 plus owner portability/privacy constraints; the PDF does not prescribe those libraries or CI filenames.

Migration obligations are global to persisted-shape changes, now explicit in task's mandatory checks: identify affected PostgreSQL, IndexedDB and native SQLite migrations, test pending work and failure recovery, and never use a planned directory as proof. The 0A plan should reconcile ancillary planned tooling paths such as `.editorconfig`/`.prettierignore` in its exact file list; the roadmap list is not authority to create unrelated tooling. `scripts/check-docs.mjs` is a future convenience with no current acceptance dependency, not an audit implementation artifact.

No whole part is appropriately downgraded to a mechanical model merely due to usage limits. High-risk planning and security/sync/native implementation retain their current strong recommendations. A model recommendation is not a plan approval, account entitlement or mandatory configuration.

## Appendix D. Setup command inventory and classification

**PRE:** can be invoked before scaffolding if the owner has the tool; **POST:** executable only after the named approved part creates its prerequisites; **OPTIONAL:** diagnostic or conditional route; **OWNER:** installation/authentication/configuration or availability requires owner action. These labels may coexist. Except the documentation commands explicitly observed in the audit runbook, **execution was Not run in this audit**. Historical machine observations retain their 12 October date. Rows group commands with identical purpose/prerequisites; every literal setup/runbook command family is included. No credentials were inspected to classify them.

| Source / literal command or command family | Class / working directory | Prerequisite / earliest part | Side effect and expected result; verification limit |
| --- | --- | --- | --- |
| SETUP A / `cat /etc/os-release`, `git --version`, `node --version`, `code --version` | PRE; any | Host tools | Read-only version/OS output; no compatibility proof. |
| SETUP A / `sudo apt update`, `sudo apt install git curl ca-certificates` | PRE/OWNER; any | Owner Ubuntu administration | Updates package metadata/installs packages; only if missing. Not run. |
| SETUP A / Node, VS Code, pnpm and Docker vendor installation procedures | PRE/OWNER; vendor-specified directory | Owner selects OS route and compatible candidates | System changes; follow current official instructions, not an invented all-in-one script. Not run. |
| SETUP A / `git remote -v`, `ssh -T git@github.com` | OPTIONAL/OWNER; repo for remote, any for SSH | Owner remote/key/account | Remote check read-only; SSH authenticates and can update known-host trust. Greeting with exit 1 is expected for GitHub; private values must not be shared. Not run here. |
| SETUP A / `pnpm --version`, `docker --version`, `docker compose version` | PRE; any | Tools installed | Version only; no daemon/build proof. Historical observations only. |
| SETUP A / `docker info`, `systemctl status docker` | PRE; any | Installed local daemon | Read-only daemon/access check; output may contain host metadata, not evidence of PG readiness. Not run. |
| SETUP A / `sudo docker ...` | OWNER; example prefix, not a runnable command | Owner permission route | Ellipsis is prose, not literal shell input. No blanket sudo authorization. |
| SETUP A / `psql --version`; optional `postgresql-client` install | OPTIONAL/OWNER; any | Optional host client | No host server needed; client version does not connect to a database. Not run. |
| SETUP A / `java -version`, `echo "$JAVA_HOME"`, `echo "$ANDROID_HOME"` | PRE/OWNER; any | Selected JDK/SDK paths before 0G | Only nonsecret machine paths and version; not Gradle compatibility. No secret environment dump. |
| SETUP A / `adb version`, `adb devices` | PRE/OWNER; any | Platform Tools, authorized device/emulator by 0G | Lists tool/device state; no installed app test. Device RSA prompt is owner action. |
| SETUP A / browser About or installed browser `--version` | PRE/OWNER; any | Browser installation/access | Records version; actual Safari requires macOS/iOS. Not run. |
| SETUP B / `test -f package.json`, `test -f pnpm-lock.yaml` | POST 0A; root | Approved scaffold/lockfile | Exit 0 confirms file presence only. Files intentionally absent today. |
| SETUP B / `pnpm install --frozen-lockfile` | POST 0A/OWNER; root | Approved installation scope and pinned lockfile | Installs exactly locked dependencies; no test/build result implied. Not run. |
| SETUP B / `cp --no-clobber apps/api/.env.example apps/api/.env` | POST 0D/OWNER; root | Example and .gitignore exist; actual configuration chosen | Creates ignored local file if absent; fill privately before startup. No value created here. |
| SETUP B / `docker compose -f infra/local/compose.yaml config --quiet` | POST 0D/OWNER; root | Real Compose file plus explicit interpolation/env wiring | Validates topology without printing expanded config. Add required 0D env arguments; current conditional illustration not a tested invocation. |
| SETUP B / `docker compose -f infra/local/compose.yaml up -d` | POST 0D/OWNER; root | Same wiring, isolated synthetic DB/email | Starts chosen containers; readiness still needs checks. Not run. |
| SETUP B / `docker compose -f infra/local/compose.yaml ps` | POST 0D; root | Same actual wiring/topology | Lists selected services; no guessed service names. Not run. |
| SETUP B / `docker compose -f infra/local/compose.yaml down` | POST 0D/OWNER; root | Same stack/wiring and approved shutdown | Stops isolated stack, no `-v`; preserve diagnostic data. Not run. |
| SETUP B / `pnpm exec tsc --version`, `pnpm exec eslint --version`, `pnpm exec prettier --version` | POST 0A; root | Installed root dependencies | Version checks only; missing bin requires owner manifest review. Not run. |
| SETUP B / `pnpm exec vitest --version` | POST 0B; root | Approved root runner | Version only; actual suite script from 0B. Not run. |
| SETUP B / `pnpm exec expo --version`, `pnpm exec jest --version` | POST 0E; `apps/universal` | App dependencies; use actual root if Jest deliberately owned there | Correct package binary resolves; no native proof. Not run. |
| SETUP B / `pnpm exec playwright --version`, `pnpm exec playwright install --with-deps` | POST 0E/OWNER; root | Approved pinned root runner | Version read; install downloads browsers/system dependencies. Required before 0E checks, CI consolidation 0F. Not run. |
| SETUP B / `maestro --help` and official CLI install | POST 0G/OWNER; any | Java 17+, ADB/device and approved tool version | Help only; installing CLI does not run an APK flow. Not run. |
| SETUP D / `pnpm exec wrangler --version` | POST 0L if chosen, otherwise 42; dependency-owning directory | Concrete plan approves/pins local preview dependency | Version only; no login/deploy. Not run. |
| SETUP E / `expo prebuild` | POST 0G/0J; app via actual approved runner command | Approved native build/plugin plan | Generates ignored native output; not a hand-maintained source-ownership change. No command inferred/executed now. |
| SETUP troubleshooting / `which node`, `node --version` | PRE; any | Shell/version manager | Read-only resolution check. Not run in audit. |
| ENV / `git check-ignore -v apps/api/.env apps/universal/.env` | POST 0A/OWNER; root, only after local files exist | Ignore rules and owner-created files | Shows matching rule/path, never contents. Not run; no env files created. |
| Runbook / `command -v NAME` (replace NAME with the tool being checked) | PRE; any | Shell and named tool | Presence/path only; not compatibility or an install. Not repeated for the owner in this audit. |
| Runbook / `git status --short` | PRE; root | Checkout | Read-only intended changes; observed for audit. |
| Runbook / `Ctrl-C` | POST; corresponding service terminal | Foreground service running | Stops only that service; not a shell script. No services ran here. |
| SETUP/runbook / `pnpm test`, `pnpm dev`, `drizzle-kit migrate`, `expo run:android`, `npm install`, `pnpm install` | NOT authorized current invocations | Explicitly examples of commands not to infer/run now | Owning parts must supply literal scripts and prerequisites; npm lockfile is not the approved workspace route. |
| Audit runbook / `python3` heredoc, `git diff --check`, `git diff --stat`, `rg --files`, `sha256sum`, `pdftotext`, `pdftoppm` | PRE/documentation; root | Existing Python/Git/ripgrep/Poppler | Actual read-only audit checks and temporary PDF renders; observed separately below. No application test claim. |

ENV_GUIDE separates public client build values, private API/migration/provider values, local/CI/staging/production environments and signing credentials. It supplies names and ownership, not fabricated credentials or runnable remote URLs. A phone's loopback cannot be assumed to reach the host. Production cookie/origin behavior must be proven at 0K and reviewed at 42; development allowances must not migrate into release configuration.

## Appendix E. Official-source verification and evidence limits

Official documentation was checked on **13 October 2026**. These are dated observations used to assess setup instructions; implementation must recheck the chosen versions. Each entry is limited to the claim it supports; no external install or account was tested.

| Primary source | Verified implication for this audit |
| --- | --- |
| [Expo SDK matrix](https://docs.expo.dev/versions/latest/) | Current candidate set in SETUP is SDK 57 / RN 0.86 / React 19.2.3 / RN Web 0.21.0 with Node floor 22.13.x. This is not a Parsefit lockfile or support-floor commitment. |
| [Node release table](https://nodejs.org/en/about/previous-releases), [pnpm installation matrix](https://pnpm.io/installation/) | Node 24 is an LTS candidate supported by pnpm's matrix; exact pin and project compatibility belong to 0A. |
| [pnpm exec](https://pnpm.io/cli/exec) | Local project binaries resolve in package context; app-owned Expo commands cannot be assumed available at root. |
| [Expo monorepos](https://docs.expo.dev/guides/monorepos/) | Workspace support does not remove the need to test dependency resolution/autolinking with the selected SDK. |
| [Better Auth Expo integration](https://better-auth.com/docs/integrations/expo) | Guide targets SDK 55, describes native SecureStore/session transport and scheme/trusted-origin configuration. Therefore SDK 57 compatibility still needs 0K proof. Its optional Expo API route example does not replace the approved Fastify API. |
| [Expo SQLite](https://docs.expo.dev/versions/latest/sdk/sqlite/) | SQLCipher requires configured native generation/build and is unavailable in Expo Go. Scoped exclusive transaction API addresses unrelated async-query participation; native store tests remain required. |
| [Expo SecureStore](https://docs.expo.dev/versions/latest/sdk/securestore/) | Secure credential storage has lifecycle/backup limitations; it is not the journal database or a complete key-recovery policy. |
| [Dexie transaction guidance](https://dexie.org/docs/Dexie/Dexie.transaction%28%29) | IndexedDB auto-commit constrains unrelated async waits inside transactions, supporting architecture's encryption-before-transaction rule. |
| [Docker Compose interpolation](https://docs.docker.com/compose/how-tos/environment-variables/variable-interpolation/) | API subdirectory `.env` is not automatically root Compose interpolation; explicit env-file/wiring is required. |
| [Android JDK guidance](https://developer.android.com/build/jdks) | JDK must match the selected Gradle/AGP combination. Merely observing JDK 21 or stating 17+ does not establish a passing build. |
| [Playwright requirements](https://playwright.dev/docs/intro), [Maestro installation](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli) | Browser binaries/system prerequisites and native CLI/JDK/device prerequisites must be installed before their first checks. No actual Safari or device test is implied. |
| [PostgreSQL support policy](https://www.postgresql.org/support/versioning/) | PostgreSQL 18 is a supported candidate; pin a maintained minor and prove real migration/transaction behavior in 0D onward. |
| [OpenAI model selection](https://developers.openai.com/api/docs/guides/model-selection), [Codex IDE guide](https://learn.chatgpt.com/docs/codex/ide) | Model tradeoffs support strong planning/implementation recommendations; guide availability is not proof that this owner's picker exposes a model/effort. No account inspection or permanent model settings. |

### Verification record

The reproducible documentation check and observed results are in [test-command](../test-command.md#audit-docs-documentation-verification). Source hash baselines were captured before corrections. Blueprint, ANALYSIS and exact approved plan hashes must match; links, cards, graph and source-scope checks run against the final files. Manual review assessed semantic mappings, page-19 scope, page-22 scenarios, command sequencing and the diff. Automated ID presence alone cannot prove those judgments.

No application tests, type checks, lints, builds, native flows, migrations, recovery rehearsals, accessibility sessions, pilot observations or deployment smoke were run. Their precise prerequisites are the approved owning part, created scripts/fixtures, installed toolchain, real isolated stores/services and applicable browser/device/reviewer/owner gates described above.
