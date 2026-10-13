# Adaptive Health App: incremental execution plan

**Part creating this coordination system:** COORD-DOCS. **Created:** 11 October 2026. **Final review:** 12 October 2026 (Asia/Dhaka).
**Reality:** Documentation only. No application scaffold, dependency installation, runtime tests, deployment, commit or push has occurred in this task. All build parts below are proposals and start **Not Started**. This roadmap does not approve an implementation plan.

**AUDIT-DOCS:** Done, 13 October 2026; approved revision 1 executed on the owner's explicit instruction. [Report and traceability](docs/agent/pre-implementation-audit.md), [runnable documentation checks](docs/test-command.md#audit-docs-documentation-verification) and [live handoff](docs/agent/HANDOFF.md) record evidence and remaining gates. This separate documentation part does not complete S0 or any of the 82 application parts.

## Sources, scope and current paths

Read [AGENTS.md](AGENTS.md), [HANDOFF](docs/agent/HANDOFF.md) and relevant [MEMORY](docs/agent/MEMORY.md), then [ARCHITECTURE.md](docs/ARCHITECTURE.md), [STRUCTURE.md](docs/STRUCTURE.md), [ANALYSIS.md](docs/ANALYSIS.md) and the relevant physical pages of the [24-page blueprint](docs/Adaptive_Health_App_Product_Blueprint.pdf). PDF page numbers below mean physical pages 1-24, not section labels. Technical foundation details are engineering requirements supporting pp.18-19, not claims the PDF chooses specific frameworks.

ARCHITECTURE is the approved technical authority. ANALYSIS preserves R01-R74 requirements, D1-D12 decisions and T01-T34 validation IDs. Its historical pending stack/O2/O3 wording is resolved by ARCHITECTURE's authority record. Preserve the approved Expo stack, page-19 MVP/deferrals, next-journal-day target activation (including first activation), and explicit finish/skip sequence policy. Do not replace the architecture or silently amend ANALYSIS.

COORD-DOCS created this file and root AGENTS/CLAUDE plus `docs/agent/HANDOFF.md`, `MEMORY.md`, and `plans/README.md`. Root `README.md` exists from README-DOC. SETUP-DOC created `docs/SETUP.md`, `docs/ENV_GUIDE.md` and `docs/test-command.md` on 12 October 2026. All application/tooling/test/infra paths listed in task cards are **PLANNED future change locations**, not existing/runnable files. Brace notation denotes specific sibling destinations, not literal filenames. The three setup guides exist, but app scripts remain future placeholders. `.codex/` is intentionally omitted: canonical root instructions and saved-plan conventions suffice; no permanent model/effort settings are needed.

## Manual setup prerequisite S0

S0 is an owner setup gate, not an application implementation part and not completed. Follow [SETUP.md](docs/SETUP.md), [ENV_GUIDE.md](docs/ENV_GUIDE.md) and [test-command.md](docs/test-command.md) for supported Node/pnpm, local PostgreSQL/email tooling, Android SDK/JDK/emulator/device/build prerequisites and test browsers. Owner installs toolchains, creates external accounts and supplies configuration; agents must not print secret values. Paid production services/provider keys/signing/store setup are deferred until their relevant approved gates. Confirm setup using read-only/version/presence checks, not an invented compatible-version claim. Record unavailable Safari/devices/CI access explicitly.

For S0 entry to PLAN 0A, verify local Git, supported Node, pnpm, Docker/Compose and the editor workflow. PostgreSQL/email service configuration starts only after 0D creates it; pinned browser binaries belong to 0E; Android SDK/JDK/emulator/physical-device prerequisites must be ready for 0G, with actual Safari/browser evidence by 0N. Record future environment gaps now without claiming those later checks passed. This staging does not waive any required platform acceptance.

**First implementation after S0:** 0A, Repository and compatible toolchain. First ask the agent to **PLAN 0A**; that request does not authorize implementation. Current next action is owner manual S0 using the three guides, then request PLAN 0A.

## Mandatory single-part workflow

Only one repository editor at a time; HANDOFF names that owner. Review-only parallel agents may inspect sources/changes without repository writes, dependency installations or mutating application workflows. Ownership transfer requires a completed handoff and fresh worktree inspection.

1. **PLAN:** Read current docs/dependency evidence and plan only the specified part. No implementation. Draft may be saved in `docs/agent/plans/` as **Proposed**; no approval implied.
2. **APPROVAL:** Owner reviews the concrete part plan and approves or requests changes. Record exact approved revision/decisions; do not infer approval from the roadmap.
3. **SAVE:** Store the exact approved Markdown at `docs/agent/plans/part-<lowercase-id>-<slug>.md` and link it from HANDOFF. No implementation in this saving step; return control for an implementation instruction.
4. **IMPLEMENT:** On that instruction, implement only the approved part. Changes to scope, policy, dependency or architecture require an approved amendment before dependent work.
5. **VERIFY:** Run relevant real automated/static/build/browser/device/manual checks. Record actual commands, environment, results and blocked/not-run evidence separately from expectations.
6. **DOCUMENT:** Update this table/card evidence, HANDOFF, relevant durable MEMORY, STRUCTURE creation statuses and applicable docs. Finished implementation parts append commands/results to `docs/test-command.md` once created in setup. COORD-DOCS records its documentation checks in HANDOFF; it does not create the deferred command guide.
7. **STOP:** Report changes, results, blockers and exact next action; wait. Never auto-start another part. Owner may make a normal small commit after the approved plan and after verified implementation; agents do not stage/commit/push.

See [saved-plan convention](docs/agent/plans/README.md) for required scope, dependencies, exact files, sequence, tests, rollback/recovery, decisions, acceptance, approval provenance and model choices. Built-in plan-mode temporary files do not replace the approved saved Markdown. No application-part plan is approved yet. The separate [AUDIT-DOCS plan](docs/agent/plans/part-audit-docs-final-pre-implementation-audit.md) approves documentation review only; its [report](docs/agent/pre-implementation-audit.md) records the audit evidence and remaining gates.

## Status and evidence rules

| Status | Meaning / transition evidence |
| --- | --- |
| Not Started | Roadmap proposal only; no concrete part planning started. |
| Planned | Concrete proposed/approved part plan exists and is linked; approval state is stated separately. |
| In Progress | Approved part is being implemented or validated; not all required acceptance evidence exists. |
| Blocked | Active part cannot proceed/finish due to a named failed prerequisite, unresolved decision or missing required environment/evidence; record unblock action. |
| Done | Approved scope, required tests/builds/manual/platform acceptance and documentation all verified with dated evidence. Code alone is insufficient. |

Check the completion box only at Done. Every status change records owner, plan/approval state and evidence location in HANDOFF. A known future gate does not mark an inactive proposal Blocked. Required failed/unavailable checks keep an active part unfinished; optional checks must be explicitly identified in its approved plan, never silently waived.

## Models and effort

Recommendations favor quality and separate **PLAN** from **IMPLEMENT** for every part. GPT-6 Astra xhigh/max suits architecture, health correctness, security/sync and difficult portability planning. GPT-6.1 Sol high/xhigh/max suits bounded through complex implementation; Astra max is retained for the security audit. GPT-6 Luna is reserved for truly mechanical follow-up edits only after interfaces/tests are settled; none of the whole parts below is downgraded to Luna. Sol medium is acceptable only for an explicitly isolated mechanical substep, not the critical part.

Names/efforts are recommendations, not account entitlement claims. **The VS Code model/effort picker is authoritative for actual ChatGPT Plus/account/extension availability.** If a listed option is absent, disclose it and obtain a quality-preserving selection; do not silently downgrade. Select model/effort in the VS Code UI; do not set permanent `model` or `model_reasoning_effort` in `.codex/config.toml`. Official [OpenAI model-selection guidance](https://developers.openai.com/api/docs/guides/model-selection) and [Codex IDE documentation](https://learn.chatgpt.com/docs/codex/ide) were checked on 11 October 2026; the per-part choices below are project engineering recommendations.

## Approval and evidence gates

| Gate | Owner/reviewer action and dependency |
| --- | --- |
| O1 evidence | Stack direction already approved. 0G establishes early installed Android; 0N closes tested versions, browser/mobile/physical-device UI/auth/protected-store/date/API feasibility. Structural failure blocks core and requires reviewed direction amendment. |
| O2/O3 | Already approved: p.19 MVP/deferrals, next-day targets, explicit skip/finish consumption. No repeated reapproval absent a proposed change. |
| O4 | Owner reviews unlock/setup friction, key/wrapping/rotation/recovery/lock, backup exclusion, metadata/index exposure and logout/local-copy/unsynced-loss policy. Synthetic protected prototypes may advance; no real health data until approved and verified (0I/0J, 22, 39). |
| O5 | Qualified nutrition/training reviewers and curator plus owner approve supported population, estimator/activity/protein/goal/training bounds and uncertainty language. Blocks advice release (14, 32, 37) and later adaptation. PDF numbers do not approve policy. |
| O6 | Owner approves coupled undo/receipt/tombstone/offline replay/proof/deletion/export/backup retention and measured recovery objectives. Blocks production sync/privacy finalization (26, 29-31, 39). No invented durations. |
| O7 | Owner approves exact hosting/domain/email/region/operator/budget and provisions accounts/secrets. Blocks purchases/provisioning/staging/production, not local synthetic development. |
| O8 | Owner/curator verifies food/price/media licenses, Bangladesh benchmark/thresholds and AI provider terms/region/retention/consent/hard caps/kill switch. Blocks content release/real external processing (32-36 and later integrations). |
| O9 | Owner obtains applicable privacy/distribution review and approves adult recruitment/consent/device/research measures. Blocks real/public pilot/publication (43-44) and later distribution. |

Manual-only pilot without reviewed estimator/intelligence is reduced scope and must not claim full page-19 MVP. Website pilot/release does not approve Android publication, Health Connect ingestion or other Later work.

## Dependency order and critical chains

Foundation part 0G installs Android **before** core features, then 0J/0K/0N repeat real encrypted-store/auth/date/offline checks; Android is a continuous gate. M0 is not complete from web success or Expo Go.

| Chain | Critical order and purpose |
| --- | --- |
| Foundation | S0 → 0A → 0B → 0C/0D → 0E → 0F → 0G early Android. 0H → 0I/0J, then 0K/0L/0M → 0N integrated M0. Only explicitly independent prerequisites may be planned/reviewed in parallel. |
| Trustworthy manual loop | 0N → 1 → 2/3/4 Food and 5/6 Sleep plus 7/8 manual Workout drafts → 9/10 performed states → 11 schedule → 12 future routine versions. All three manual modules precede advanced workout states. |
| History and feedback | 12 → 13 manual goals (+14 reviewed estimator independently gated) → 15 bars; 16 coverage → 17 aggregates → 18 day → 19 month → 20 year → 21 factual Overall. |
| Account correctness | 21 → 22 → 23 receipt/feed kernel → 23A/23B/23C handlers → 24 coordinator → 25 conflicts → 26 bootstrap → 27 guest import. 28/29 exports → 30 deletion/proof → 31 independent suppression restore. |
| Narrow intelligence | 14/17/31 → 32 vetted proposals; 33 database search → 34 regional evidence → 35 optional AI; 36 supplied-fact summaries → 37 reviewed Overall next action. No costly AI is needed for manual logging. |
| Website release | 37 → 38 accessibility / 39 security → 40 offline/performance → 41 E2E → 42 synthetic staging → 43 explicitly approved restricted pilot/observation → 44 approved website publication. |
| Android release | Website 44 → 46 native hardening → 47 signed release preparation. Optional 45 product Health Connect is separately promoted and does not block manual Android release. |
| Evidence-only later work | 48-65 remain Later/Research; each needs explicit promotion, evidence and a fresh approved plan. Evaluation-only completion means go/no-go evidence, not implementation of an unapproved expensive subsystem. |

The table below lists direct prerequisites; their transitive prerequisites also apply. `S0` is the manual setup gate and O IDs are owner/reviewer gates, not part IDs. Numeric order is the default sequence, but genuinely independent branches can be selected by the owner after dependencies pass. One active editor remains mandatory.

## Mandatory test-command guide convention

SETUP-DOC created `docs/test-command.md` with S0 checks and future placeholders; COORD-DOCS did not create it. Every finished implementation part appends a clearly named section containing:

- Part ID, plan/build/version/date and required environment/tool/device versions; isolated synthetic/test service prerequisites and configuration **names only**.
- Working directory for **each runnable command**, actual literal script names, and terminal arrangement: explicitly say whether a second terminal is required and what runs in each terminal. Use existing scripts only.
- Unit/integration/static/build/browser/Android commands plus any intentionally inapplicable checks with reasons.
- Expected outcomes, separately from observed command result/exit code/date. `Expected: passes` is never evidence that it passed. Mark `Not run`/`Blocked` with exact missing prerequisite.
- Browser URLs/routes, viewport/keyboard/offline/multi-tab steps; installed APK/build/device/permission/restart/manual steps and expected visible behavior.
- Actual evidence location, failures, recovery/cleanup instructions and any remaining blocker. Never print secrets or personal health data; no production DB tests.

All cards require relevant feature tests and appropriate real-store/database/native checks; expand/repeat verification only for changed risk or unresolved evidence. Save/build success is not an assertion of manual accessibility, clinical validation or deployment. Every concrete part plan that changes persisted shapes must name its affected IndexedDB, native SQLite and/or PostgreSQL migration track, preserve pending work and record upgrade/recovery tests under ARCHITECTURE §4.4. A planned migration directory is not evidence that migrations have run.

## Part status table

| Complete | Part | Milestone / scope | Direct prerequisites | Status | PLAN model / effort | IMPLEMENT model / effort | Plan / acceptance evidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [ ] | [0A - Repository and compatible toolchain](#part-0a) | Foundation M0 | S0 owner manual setup | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [0B - Portable domain and wire foundation](#part-0b) | Foundation M0 | 0A | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [0C - Deterministic dates and units](#part-0c) | Foundation M0 | 0B | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [0D - Local API and PostgreSQL foundation](#part-0d) | Foundation M0 | 0A, 0B | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [0E - Universal responsive application shell](#part-0e) | Foundation M0 | 0A, 0B, 0C, 0D | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [0F - Test runners and initial CI](#part-0f) | Foundation M0 | 0A, 0B, 0D, 0E | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [0G - Early installed Android smoke build](#part-0g) | Foundation M0 | 0C, 0E, 0F | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [0H - Local transaction and sync contracts](#part-0h) | Foundation M0 | 0B, 0C | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [0I - Protected web storage feasibility](#part-0i) | Foundation M0 | 0E, 0F, 0H | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [0J - Protected native storage feasibility](#part-0j) | Foundation M0 | 0G, 0H, 0I | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [0K - Browser and native auth feasibility](#part-0k) | Foundation M0 | 0D, 0G, 0I, 0J | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [0L - Static routing and safe offline shell](#part-0l) | Foundation M0 | 0E, 0I | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [0M - Isolated Health Connect feasibility](#part-0m) | Foundation M0 | 0G, 0J | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [0N - Integrated M0 portability exit](#part-0n) | Foundation M0 | 0A, 0B, 0C, 0D, 0E, 0F, 0G, 0H, 0I, 0J, 0K, 0L, 0M | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [1 - Shared onboarding and journal entry points](#part-1) | Core M1 | 0N | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [2 - Manual nutrition calculations and records](#part-2) | Core M1 | 1 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [3 - Reliable manual Food logging and corrections](#part-3) | Core M1 | 1, 2 | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [4 - Recent foods and saved meal versions](#part-4) | Core M1 | 3 | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [5 - Manual duration-first Sleep logging](#part-5) | Core M1 | 1 | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [6 - Sleep overlap reconciliation](#part-6) | Core M1 | 5 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [7 - Equipment and minimal exercise catalog](#part-7) | Core M1/M2 | 1 | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [8 - Manual routines and session drafts](#part-8) | Core M1/M2 | 3, 5, 7 | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [9 - Performed-set completion identity](#part-9) | Core M2 | 8 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [10 - Explicit exercise and session finish](#part-10) | Core M2 | 9 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [11 - Flexible schedule and routine sequence](#part-11) | Core M2 | 1, 10 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [12 - Today-only and future routine versions](#part-12) | Core M2 | 8, 11 | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [13 - Manual goals and dated target snapshots](#part-13) | Core M3 | 3, 5, 11, 12 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [14 - Reviewed maintenance and goal discussion](#part-14) | Core M3 policy-gated | 13; O5 reviewed policy approval | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [15 - Configurable progress bars and nutrient detail](#part-15) | Core M3 | 4, 13 | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [16 - Coverage and eligible-day state](#part-16) | Core M3 | 3, 6, 11, 13 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [17 - Coverage-aware aggregates and invalidation](#part-17) | Core M3 | 12, 13, 16 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [18 - Day journal and accessible history](#part-18) | Core M3 | 15, 17 | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [19 - Month calendar and coverage statistics](#part-19) | Core M3 | 18 | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [20 - Year calendar and comparable trends](#part-20) | Core M3 | 19 | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [21 - Overall factual dashboard](#part-21) | Core M3 | 20 | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [22 - Product account lifecycle and isolation](#part-22) | Core M4 | 0K, 21; O4 approved local-copy/key policy before real data | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [23 - Server acceptance and ordered feed kernel](#part-23) | Core M4 | 22, 0H | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [23A - Profile and target server commands](#part-23a) | Core M4 | 23, 13, 16 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [23B - Food, Sleep and journal server commands](#part-23b) | Core M4 | 23, 4, 6, 16 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [23C - Workout and schedule server commands](#part-23c) | Core M4 | 23, 12 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [24 - Client sync coordination and atomic pages](#part-24) | Core M4 | 23A, 23B, 23C | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [25 - Explicit conflict review and compensation](#part-25) | Core M4 | 24 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [26 - Consistent bootstrap and expired replay](#part-26) | Core M4 | 25; O6 coupled replay/retention policy for finalization | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [27 - Explicit retryable guest import](#part-27) | Core M4 | 26 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [28 - Versioned local JSON and CSV export](#part-28) | Core M4 | 21, 25 | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [29 - Account export jobs and expiry](#part-29) | Core M4 | 26, 28; O6 export/job policy | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [30 - Deletion jobs, tombstones and device proof](#part-30) | Core M4 | 27, 29; O4/O6 approved deletion/proof policy | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [31 - Independent backup and suppression restore](#part-31) | Core M4 | 30; O6 recovery/retention; O7 before external provisioning | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [32 - Constrained vetted workout proposals](#part-32) | Intelligence M5 | 14, 17, 31; O5 review and O8 content rights | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [33 - Database-backed Food search and matching](#part-33) | Intelligence M5 | 2, 24, 31; O8 provider/data terms | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [34 - Bangladesh food validation and curated records](#part-34) | Intelligence M5 | 33; O8 regional licenses/benchmark approval | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [35 - Optional AI Food proposals with fallback](#part-35) | Intelligence M5 | 25, 34; O8 provider/consent/caps/kill-switch approval | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [36 - Bounded summaries grounded in computed facts](#part-36) | Intelligence M5 | 20, 21, 25, 35 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [37 - Evidence-aware next action and reflection](#part-37) | Intelligence M5 | 14, 32, 36 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [38 - Accessibility audit and bounded fixes](#part-38) | Polish M6 | 37 | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [39 - Security, privacy and policy hardening](#part-39) | Polish M6 | 31, 37, 38; O4-O8 applicable approvals | Not Started | GPT-6 Astra / max | GPT-6 Astra / max | None; no part plan or acceptance run |
| [ ] | [40 - Offline upgrades and measured performance](#part-40) | Polish M6 | 26, 31, 39 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [41 - Cross-platform MVP acceptance suite](#part-41) | Polish M6 | 38, 39, 40 | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [42 - Owner-provisioned staging and operations](#part-42) | Polish M6 | 31, 41; O7 exact domain/vendors/region/operator/budget approval | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [43 - Approved adult imperfect-week pilot](#part-43) | Polish M6 pilot-gated | 14, 34, 37, 42; O4-O9 release/pilot approvals | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [44 - Website publication and release handoff](#part-44) | Polish M6 release-gated | 43; explicit owner production promotion approval | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [45 - Optional Health Connect product integration](#part-45) | Later Android optional | 44, 0M; explicit scope promotion and content/permission/privacy review | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [46 - Native Android product hardening](#part-46) | Later Android release preparation | 44; updated SDK/device/plugin release matrix | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [47 - Android signed release preparation](#part-47) | Later Android release preparation | 46; owner signing/distribution/privacy approval | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [48 - Recipe yields and personal portions](#part-48) | Later enhancement | 34, 44; explicit promotion/content approval | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [49 - Busy-day capacity proposal](#part-49) | Later enhancement | 32, 44; explicit promotion/review | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [50 - Equipment substitution proposals](#part-50) | Later enhancement | 32, 44; explicit catalog/reviewer promotion | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [51 - Reviewed progression proposal evaluation](#part-51) | Later enhancement/research | 37, 43; sufficient comparable history and O5 promotion | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [52 - Adaptive target and plateau evaluation](#part-52) | Later enhancement/research | 14, 37, 43; sufficient complete comparable history and O5 promotion | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [53 - Barcode food lookup](#part-53) | Later enhancement | 33, 34, 44; explicit provider/license/permission promotion | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [54 - Photo food proposal evaluation](#part-54) | Later enhancement/research | 35, 44; explicit media/privacy/quality promotion | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [55 - Voice food input evaluation](#part-55) | Later enhancement/research | 34, 35, 44; explicit audio/language/privacy promotion | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [56 - Nutrition-label OCR evaluation](#part-56) | Later enhancement/research | 33, 44; explicit label/media/license promotion | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [57 - Optional scheduled reminders](#part-57) | Later enhancement | 43; explicit O2 promotion/permission/tone policy | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [58 - Private engagement prototype evaluation](#part-58) | Later research | 43; explicit behavioral/pressure evaluation promotion | Not Started | GPT-6 Astra / xhigh | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [59 - One opt-in broader context input](#part-59) | Later enhancement | 43; explicit purpose/privacy/benefit promotion | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [60 - On-device personal food memory evaluation](#part-60) | Later research | 34, 43; explicit device/privacy/ML promotion | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [61 - Feasible-future simulator evaluation](#part-61) | Later research | 49, 51, 52; explicit forecast/non-actioning review | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [62 - Personal experiment protocol evaluation](#part-62) | Later research | 43, 59; explicit reviewer/research promotion | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / high | None; no part plan or acceptance run |
| [ ] | [63 - Camera-assisted training-note evaluation](#part-63) | Later research | 51, 46; explicit exercise-specific/privacy promotion | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / max | None; no part plan or acceptance run |
| [ ] | [64 - Household recipe-sharing feasibility](#part-64) | Later research | 48, 43; explicit demand/sharing/privacy promotion | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |
| [ ] | [65 - Regional budget-aware food proposal evaluation](#part-65) | Later enhancement/research | 34, 43; explicit price/source/reviewer promotion | Not Started | GPT-6 Astra / max | GPT-6.1 Sol / xhigh | None; no part plan or acceptance run |

**Total: 82 proposed parts:** 14 foundation, 34 core (including 23A-23C), 6 intelligence, 7 website polish/pilot/release, 3 later Android, 18 later enhancement/research. COORD-DOCS and owner gate S0 are not included.

## Part cards

Application/tooling/test/infra locations below are PLANNED until a part creates them; existing documentation locations are update targets. Root README already exists and 0A updates it as needed. Every card's completion definition includes the workflow and verification requirements above. Test names are required behaviors/tools, not claims scripts already exist.

<a id="part-0a"></a>

### 0A - Repository and compatible toolchain

1. **Part / status:** 0A - Repository and compatible toolchain; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Initialize the bounded workspace/tooling only; select a mutually compatible stable version set, enforce import boundaries and provide a minimal built-in Node check/test entry point for this part. Update the existing project README without replacing owner content. App screens and infrastructure provisioning are excluded.
3. **Prerequisites:** S0 owner manual setup. Require their acceptance evidence, not only code.
4. **PDF pages:** 18-19 (physical pages).
5. **ARCHITECTURE sections:** 3.2, 12.1, 13.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** package.json; pnpm-workspace.yaml; pnpm-lock.yaml; .node-version; .npmrc; tsconfig.base.json; tsconfig.json; eslint.config.mjs; prettier.config.mjs; .gitignore; README.md; scripts/check-boundaries.mjs (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Four approved package boundaries; supported engines and one dependency lock.
8. **Edge cases:** Duplicate React/RN; pnpm autolinking; DOM/Node ambient leakage; unsupported owner toolchain.
9. **Unit and integration tests:** Unit: Import-rule and strict-typing negative fixtures. Integration: Clean owner-authorized dependency resolution and workspace checks.
10. **Browser testing:** Not applicable: no runnable app yet; web resolution proven in 0E.
11. **Android compatibility:** No installed app yet; record SDK/plugin candidates for 0G/0N.
12. **Security/privacy:** Ignore secrets/generated artifacts; no registry tokens in config. Installation only within approved plan.
13. **Acceptance criteria:** [ ] Workspace checks run; one lockfile and tested version record; no extra app/package framework.
14. **Manual verification:** Owner verifies documented Node/pnpm versions and reproduces clean workspace checks.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; SETUP/ENV_GUIDE compatibility and installation record.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-0b"></a>

### 0B - Portable domain and wire foundation

1. **Part / status:** 0B - Portable domain and wire foundation; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Create four package manifests/strict configs, minimal portable vocabulary, schema/error envelopes, typed client transport and synthetic builders needed by foundation. Bootstrap the approved Vitest runner/scripts now so 0B-0D can verify their acceptance before 0F consolidates CI. Feature command schemas arrive with their parts.
3. **Prerequisites:** 0A. Require their acceptance evidence, not only code.
4. **PDF pages:** 18-19 (physical pages).
5. **ARCHITECTURE sections:** 3.2, 4.1, 11.1-11.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/{domain,contracts,api-client,test-utils}/{package.json,tsconfig.json}; packages/domain/src/primitives/; packages/contracts/src/{common.ts,errors.ts,versions.ts,commands.ts,sync.ts,openapi.ts}; packages/api-client/src/; packages/test-utils/src/; tests/contracts/; vitest.config.ts; package.json (runner scripts). Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan.
7. **Interfaces/data-model dependencies:** UUIDv4; JournalDate/Instant/DecimalText vocabulary; safe errors; injected transport; protocol versions.
8. **Edge cases:** Invalid UUID/date/decimal; extra mutation fields; additive responses; bigint string roundtrip.
9. **Unit and integration tests:** Unit: Schema/serialization and deterministic ID/clock fixture tests. Integration: Client/schema roundtrip and forbidden-import checks.
10. **Browser testing:** No screen yet; browser serialization checks in 0E.
11. **Android compatibility:** Portable types only; bundling/serialization evidence in 0G/0N.
12. **Security/privacy:** No ORM/auth/provider objects or secrets in public DTOs.
13. **Acceptance criteria:** [ ] Public shapes roundtrip; private/runtime imports rejected; one wire authority.
14. **Manual verification:** Review a synthetic malformed request and safe error; inspect dependency graph.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record protocol ownership and schema compatibility decisions.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-0c"></a>

### 0C - Deterministic dates and units

1. **Part / status:** 0C - Deterministic dates and units; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement pure Luxon-backed date resolution and decimal.js unit/precision rules; no target policy or custom-boundary settings UI.
3. **Prerequisites:** 0B. Require their acceptance evidence, not only code.
4. **PDF pages:** 4-7, 9, 11, 18, 22 (physical pages).
5. **ARCHITECTURE sections:** 4.4, 6.1, 7.1, 9.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/{dates,units}/; tests/fixtures/dates-and-zones.json (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Injected Clock; separate journal date/event/zone; decimal strings; measurement variants.
8. **Edge cases:** Asia/Dhaka midnight; DST gap/ambiguity; travel/leap dates; blank versus zero; kg/lb; assistance/per-dumbbell.
9. **Unit and integration tests:** Unit: Table/property tests for date validity, elapsed duration, precision and conversion stability. Integration: Node serialization/fixture execution required here; browser/Hermes parity is an explicit 0N gate.
10. **Browser testing:** Runtime date/locale parity owned by 0E/0N once shell exists.
11. **Android compatibility:** Hermes parity owned by 0G/0N; no mock portability claim.
12. **Security/privacy:** No personal data; reject nonfinite/extreme malformed input without inventing health bounds.
13. **Acceptance criteria:** [ ] Pure deterministic functions pass supplied-clock fixtures and preserve original units/date attribution.
14. **Manual verification:** Review 00:30 yesterday attribution and DST examples against fixtures.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Document precision/rounding and unresolved runtime checks.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-0d"></a>

### 0D - Local API and PostgreSQL foundation

1. **Part / status:** 0D - Local API and PostgreSQL foundation; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Build injectable Fastify/local PG health/readiness, safe config, migration baseline and local email capture. No feature CRUD alternate path or paid infrastructure.
3. **Prerequisites:** 0A, 0B. Require their acceptance evidence, not only code.
4. **PDF pages:** 18-19 (physical pages).
5. **ARCHITECTURE sections:** 1.1-1.2, 4.3, 10.1, 11, 13.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/api/{package.json,tsconfig.json,.env.example,drizzle.config.ts}; apps/api/src/{app.ts,server.ts,config.ts}; apps/api/src/{plugins,database}/; infra/local/compose.yaml; tests/api/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Safe errors/OpenAPI; private Drizzle schema; auth-to-JournalAccount seam; account lock/revision vocabulary.
8. **Edge cases:** DB unavailable; failed migration/startup; readiness before schema; malformed config; concurrent shutdown.
9. **Unit and integration tests:** Unit: Config/error/route registration tests. Integration: Fastify injection plus real isolated PG migration/rollback and readiness tests.
10. **Browser testing:** Synthetic public health/API roundtrip from 0E; not a core journal endpoint.
11. **Android compatibility:** Reachable emulator/device API origin exercised by 0K/0N.
12. **Security/privacy:** Local-only credentials; redacted logs; bounded requests/SQL; never production DB.
13. **Acceptance criteria:** [ ] API starts locally, readiness distinguishes DB/schema, migrations run against isolated PG, secrets stay server-only.
14. **Manual verification:** Start local services in documented terminals, stop DB, verify readiness failure and safe logs.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Document local service ports, test DB and private env ownership.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-0e"></a>

### 0E - Universal responsive application shell

1. **Part / status:** 0E - Universal responsive application shell; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Build Expo shared shell/tokens/Paper/RHF wrappers with synthetic form, selectable calendar and SVG trend. Bootstrap compatible Jest/jest-expo/RNTL component and Playwright web harnesses in this part so its acceptance can run before 0F CI consolidation. Stable tab order, error boundary, focus/back behavior; no feature persistence.
3. **Prerequisites:** 0A, 0B, 0C, 0D. Require their acceptance evidence, not only code.
4. **PDF pages:** 4, 7, 19 (physical pages).
5. **ARCHITECTURE sections:** 2.1-2.3, 3.2, 12.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/{package.json,app.config.ts,.env.example,metro.config.js,babel.config.js,tsconfig.json,jest.config.js}; apps/universal/src/{app,ui,bootstrap,adapters/runtime}/; tests/web/playwright.config.ts; package.json (component/browser scripts and pinned runner). Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan.
7. **Interfaces/data-model dependencies:** Thin routes; measured-width layout; Clock/IdSource; public config; form schema.
8. **Edge cases:** 600/1024 widths; zoom/large text; keyboard; invalid numeric text; Bangla glyphs; static render browser APIs.
9. **Unit and integration tests:** Unit: Component tests for form errors, labels, layouts and date capture. Integration: Web export/routing and import-boundary checks; synthetic API health roundtrip.
10. **Browser testing:** Chromium/Firefox/WebKit form/calendar/trend; keyboard, reflow, refresh/deep links.
11. **Android compatibility:** Initial native install in 0G; shared widgets must use RN-safe primitives now.
12. **Security/privacy:** Public config only; synthetic data; safe text; no private static export.
13. **Acceptance criteria:** [ ] Shared shell exports; readable responsive layouts and non-color semantics; no platform import leakage.
14. **Manual verification:** Resize/zoom, enter invalid number, select date, inspect focus and Bangla name rendering.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record responsive defaults, asset/font rights and supported shell routes.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-0f"></a>

### 0F - Test runners and initial CI

1. **Part / status:** 0F - Test runners and initial CI; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Consolidate existing runnable foundation unit/component/API/web checks and builds into CI and consistent local entry points; retain the minimal runners bootstrapped in 0A/0B/0E. Add secret/import artifact inspection. Android workflow is added with the installed build in 0G.
3. **Prerequisites:** 0A, 0B, 0D, 0E. Require their acceptance evidence, not only code.
4. **PDF pages:** 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 12.1, 13.1-13.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** vitest.config.ts; apps/universal/jest.config.js; packages/test-utils/; tests/{contracts,api,web}/; .github/workflows/{ci.yml,integration.yml}; scripts/check-public-artifacts.mjs (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Separate Vitest/Jest discovery; local equivalents to CI; synthetic fixtures.
8. **Edge cases:** RN tests collected by Vitest; test-utils bundled; CI service race; missing browser binaries.
9. **Unit and integration tests:** Unit: Runner discovery and fixture determinism checks. Integration: Execute local CI equivalents against isolated PG and exported shell.
10. **Browser testing:** Playwright foundation smoke and accessibility runner works.
11. **Android compatibility:** Native runner/build prerequisites recorded for 0G; no Android pass claimed here.
12. **Security/privacy:** Synthetic-only tests; CI secrets scoped; output redacted; no invented coverage percentage.
13. **Acceptance criteria:** [ ] CI/local commands run existing suites and web/API checks with separate discovery.
14. **Manual verification:** Reproduce one local CI run; inspect actual failure output from a synthetic invalid fixture.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Add exact existing commands and terminal prerequisites to test-command.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-0g"></a>

### 0G - Early installed Android smoke build

1. **Part / status:** 0G - Early installed Android smoke build; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Build and install a development APK; exercise routing/form/calendar/trend, dates, API reachability, keyboard/back and kill/reopen shell. Establish CI smoke before core product investment.
3. **Prerequisites:** 0C, 0E, 0F. Require their acceptance evidence, not only code.
4. **PDF pages:** 4, 7, 9, 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 2.3, 12.1, 13.1, 13.3, 14.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/app.config.ts; apps/universal/src/{bootstrap/compose.native.ts,adapters/runtime/runtime.native.ts}; tests/android/{harness,maestro/foundation.yaml}; .github/workflows/android-smoke.yml (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Selected SDK/native plugins; Hermes; shared shell/date/form values.
8. **Edge cases:** Host/device localhost; native autolinking; duplicate RN; unsupported emulator; locale fonts; process kill.
9. **Unit and integration tests:** Unit: Shared domain/component suites remain green. Integration: Installed build + Maestro shell flow and API health roundtrip; CI build/smoke execution.
10. **Browser testing:** Recheck web export for native-import contamination.
11. **Android compatibility:** Real emulator install and representative physical-device check; record build/SDK/OS versions. Storage/auth are repeated in 0J/0K/0N.
12. **Security/privacy:** Synthetic data; no store publication/signing secrets committed.
13. **Acceptance criteria:** [ ] Installed Android smoke runs during foundation; failures resolved or explicitly block M0; Expo Go is insufficient.
14. **Manual verification:** Owner installs documented APK, navigates/back/types Bangla, kills/reopens and verifies API response.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record install/build/device evidence and native dependency matrix.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-0h"></a>

### 0H - Local transaction and sync contracts

1. **Part / status:** 0H - Local transaction and sync contracts; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Specify and implement portable transaction/outbox vocabulary and shared behavioral corpus; no network dispatcher or full feature repositories.
3. **Prerequisites:** 0B, 0C. Require their acceptance evidence, not only code.
4. **PDF pages:** 9, 13, 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 4, 5.1-5.4, 11. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/application/ports.ts; apps/universal/src/data/{storage-contract.ts,sync/outbox.ts}; packages/contracts/src/{commands.ts,sync.ts}; tests/repositories/contract-suite.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** LocalJournal/LocalUnitOfWork; CAS generations; canonical shadow; stable operation/predecessor/sealed envelope.
8. **Edge cases:** Crash before/after commit; multi-aggregate generation mismatch; unsent versus uncertain command; quota/migration failures.
9. **Unit and integration tests:** Unit: Outbox state/sealing/dependency tests. Integration: Portable contract harness required here; real implementations execute it in 0I/0J.
10. **Browser testing:** No storage UI yet; multi-tab contract cases assigned to 0I.
11. **Android compatibility:** Real SQLite contract execution assigned to 0J; mocks do not close it.
12. **Security/privacy:** Sensitive payloads must be protected; define opaque persistent metadata and failure semantics.
13. **Acceptance criteria:** [ ] Atomic batch and generation contracts are explicit; no second mutation queue; fixtures cover both adapters.
14. **Manual verification:** Trace a synthetic command through local commit, sealing, receipt and conflict states.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record contract refinements without changing approved sync rules.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-0i"></a>

### 0I - Protected web storage feasibility

1. **Part / status:** 0I - Protected web storage feasibility; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement synthetic-data protected IndexedDB prototype and unlock/lock/transaction/reload recovery. Supply O4 key/recovery/metadata/local-copy decision packet; production policy remains unapproved until owner review.
3. **Prerequisites:** 0E, 0F, 0H. Require their acceptance evidence, not only code.
4. **PDF pages:** 6, 13, 18-19 (physical pages).
5. **ARCHITECTURE sections:** 5.1, 10.2, 12.1, 14.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/adapters/storage/indexeddb/; apps/universal/src/adapters/vault/vault.web.ts; apps/universal/src/bootstrap/compose.web.ts; tests/repositories/indexeddb.spec.ts; tests/web/offline-upgrade.spec.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Protected codec/vault port; local batch/CAS/outbox; O4 policy candidate.
8. **Edge cases:** Crypto prepare failure; transaction auto-commit; two tabs; quota/denial; lost key; caches after lock.
9. **Unit and integration tests:** Unit: Codec/key lifecycle error and CAS tests. Integration: Real browser IndexedDB contract suite with commit faults, reopen, lock and competing tabs.
10. **Browser testing:** Inspect persistent data for plaintext dates/notes; unlock/reload, denial and recovery UX.
11. **Android compatibility:** Web-only adapter import isolation; native equivalent is 0J.
12. **Security/privacy:** Reviewed crypto APIs/libraries; no homemade crypto; synthetic keys only; no real data before O4.
13. **Acceptance criteria:** [ ] Synthetic protected store passes real transactions/relaunch; no false save or secret leakage; O4 open items recorded.
14. **Manual verification:** Save synthetic entry, lock, inspect storage, reopen, simulate failed write and lost unlock material.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record O4 proposal/approval truth and web transaction pitfalls.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-0j"></a>

### 0J - Protected native storage feasibility

1. **Part / status:** 0J - Protected native storage feasibility; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Run synthetic protected SQLite/unlock/key/store parity prototype in installed Android build. Final real-data key/logout/backup policy needs O4; do not substitute plaintext persistence.
3. **Prerequisites:** 0G, 0H, 0I. Require their acceptance evidence, not only code.
4. **PDF pages:** 9, 13, 18-19 (physical pages).
5. **ARCHITECTURE sections:** 5.1, 10.2, 12.1, 13.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/adapters/storage/sqlite/; apps/universal/src/adapters/vault/vault.native.ts; apps/universal/src/bootstrap/compose.native.ts; tests/repositories/sqlite.scenarios.ts; tests/android/harness/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Same batch/outbox contracts; encrypted SQLite candidate; protected small keys; separate native SQL migrations.
8. **Edge cases:** WAL/side files; exclusive transactions; kill between writes; key invalidation; upgrade failure.
9. **Unit and integration tests:** Unit: Native adapter/key error and shared contract fixtures. Integration: Real installed SQLite contract suite, encryption/transaction faults and kill/reopen.
10. **Browser testing:** Web export still excludes native storage/key imports.
11. **Android compatibility:** Rebuild native plugins; emulator and physical-device unlock/relaunch checks, not Expo Go.
12. **Security/privacy:** Protect side files/backup exclusion; SecureStore is not journal DB; synthetic only while O4 open.
13. **Acceptance criteria:** [ ] Real native protected transactions preserve data+outbox together; web/native semantic parity demonstrated.
14. **Manual verification:** Inspect test-store behavior after kill, lock/unlock and simulated key/migration failure.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record native plugin compatibility and O4 remaining decisions.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-0k"></a>

### 0K - Browser and native auth feasibility

1. **Part / status:** 0K - Browser and native auth feasibility; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Prove real web/native sign-in, verified local-email links, session API roundtrip, expiration/revocation and basic namespace isolation. Full account product UI remains part 22.
3. **Prerequisites:** 0D, 0G, 0I, 0J. Require their acceptance evidence, not only code.
4. **PDF pages:** 4, 18-19 (physical pages).
5. **ARCHITECTURE sections:** 5.5, 10.1-10.2, 11.1, 13.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/api/src/plugins/{auth.ts,security.ts}; apps/api/src/database/schema/identity.ts; apps/api/src/providers/email/; apps/universal/src/adapters/auth/; apps/universal/src/application/namespace-session.ts; tests/api/ownership.test.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Better Auth; opaque auth ID to JournalAccount UUID; SessionTransport; namespace generation.
8. **Edge cases:** HttpOnly cookie versus native headers; CSRF/CORS; reset deep link; stale response; 401 while pending.
9. **Unit and integration tests:** Unit: Transport/error and stale-generation tests. Integration: Real PG/auth + browser cookies/local email + installed native session integration.
10. **Browser testing:** Production-like local HTTPS same-site cookies; foreign origin rejected.
11. **Android compatibility:** Installed Better Auth Expo transport, SecureStore, verification/reset links and logout.
12. **Security/privacy:** No custom password system; trusted origins, CSRF, rate bounds, redacted local email; no journal in email.
13. **Acceptance criteria:** [ ] Both platforms authenticate one API without client cookie access or cross-account state; pending synthetic work survives expiry.
14. **Manual verification:** Use two synthetic accounts, inspect session behavior and reset link, expire session with a pending record.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record tested auth origin/device configuration and remaining production O7 needs.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-0l"></a>

### 0L - Static routing and safe offline shell

1. **Part / status:** 0L - Static routing and safe offline shell; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Prove local exported route refresh/deep links, warmed-shell offline startup and safe update prompt. Host config proof only; no deployment/provisioning. The concrete plan identifies and obtains approval for any required local host-preview dependency; do not assume tooling deferred to part 42 already exists.
3. **Prerequisites:** 0E, 0I. Require their acceptance evidence, not only code.
4. **PDF pages:** 7, 13, 18-19 (physical pages).
5. **ARCHITECTURE sections:** 2.1, 11.3, 13.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/{workbox-config.cjs,public/manifest.json}; apps/universal/src/web/service-worker-registration.web.ts; infra/cloudflare/wrangler.jsonc; tests/web/offline-upgrade.spec.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Fixed public shells; versioned cache/schema; safe update lifecycle.
8. **Edge cases:** First uncached visit offline; dirty editor; incompatible old tab; private API cache; static render storage access.
9. **Unit and integration tests:** Unit: Cache route/compatibility decision tests. Integration: Real exported shell/service worker offline and old/new-tab update tests.
10. **Browser testing:** Chromium/Firefox/WebKit cached reload and fallback; actual Safari milestone in 0N.
11. **Android compatibility:** Native export/build regression; no service worker dependency on Android.
12. **Security/privacy:** Cache public shell/assets only; private authenticated API responses excluded; no forced activation.
13. **Acceptance criteria:** [ ] Cached offline startup works after prior load; refresh resolves fixed shells; update preserves pending work.
14. **Manual verification:** Warm cache, disconnect, refresh, keep old tab/editor open while publishing local new shell.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Document offline first-visit limits and shell/schema compatibility.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-0m"></a>

### 0M - Isolated Health Connect feasibility

1. **Part / status:** 0M - Isolated Health Connect feasibility; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Perform minimal native capability, permission, empty/controlled read and denial/unsupported spike. Test-build only; no product import, wearable onboarding or retained personal records.
3. **Prerequisites:** 0G, 0J. Require their acceptance evidence, not only code.
4. **PDF pages:** 11, 17-19, 24 (physical pages).
5. **ARCHITECTURE sections:** 2.3, 9.1, 13.3, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** tests/android/harness/; apps/universal/src/adapters/health/{capability.web.ts,health-connect.native.ts}; apps/universal/app.config.ts (native spike only; product ingestion remains Later) (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** HealthIntegration capability/read/denied results; no journal ingestion.
8. **Edge cases:** Missing service; unsupported OS; denied/revoked permission; empty data; plugin web leak.
9. **Unit and integration tests:** Unit: Capability-result contract tests. Integration: Installed native isolated test harness checks permission/read outcomes.
10. **Browser testing:** Web returns explicit unsupported and remains functional.
11. **Android compatibility:** Actual device/emulator capability matrix; no Expo Go substitution.
12. **Security/privacy:** No real health logs retained/exported; minimum permissions; plugin requires approval in spike plan.
13. **Acceptance criteria:** [ ] Feasibility results and support limits recorded without promoting Later ingestion.
14. **Manual verification:** Run supported/unsupported and denied scenarios; inspect manifest and absence of journal import.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record plugin/device evidence and explicit future integration gate.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-0n"></a>

### 0N - Integrated M0 portability exit

1. **Part / status:** 0N - Integrated M0 portability exit; Foundation M0; Not Started; [ ] complete.
2. **Scope and deliverables:** Close synthetic feasibility evidence, record exact compatible versions/browser/device/OS floor, repeat integrated installed Android smoke and physical checks. Structural failures block core advancement; owner decides any architecture amendment.
3. **Prerequisites:** 0A, 0B, 0C, 0D, 0E, 0F, 0G, 0H, 0I, 0J, 0K, 0L, 0M. Require their acceptance evidence, not only code.
4. **PDF pages:** 4, 7, 17-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 12, 13.3, 14.1, 14.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** tests/{web,android,manual}/; .github/workflows/; docs/SETUP.md; docs/ENV_GUIDE.md (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Integrated shell/forms/calendar/trend + date parity + real auth + protected stores + API.
8. **Edge cases:** Hermes/Intl parity; inaccessible Paper widget; autolink/encryption/auth incompatibility; no Safari/device access.
9. **Unit and integration tests:** Unit: Full critical foundation domain/schema/component suites. Integration: Real IndexedDB/SQLite/PG + auth roundtrip + cache/update + Android CI smoke.
10. **Browser testing:** Current/previous major Chrome/Edge/Firefox/Safari and mobile matrix; record gaps, actual Safari manually.
11. **Android compatibility:** Integrated installed emulator/physical build: native auth, encrypted SQL/unlock, offline relaunch, keyboard/back and capability spike.
12. **Security/privacy:** Synthetic only unless O4 separately closed; inspect public bundles/logs.
13. **Acceptance criteria:** [ ] M0 evidence covers architecture §13.3; no missing mandatory platform check; O1 evidence decision recorded.
14. **Manual verification:** Follow one documented end-to-end synthetic scenario on browser and physical Android.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record M0 evidence and O1 disposition; keep O4-O9 open where unresolved.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-1"></a>

### 1 - Shared onboarding and journal entry points

1. **Part / status:** 1 - Shared onboarding and journal entry points; Core M1; Not Started; [ ] complete.
2. **Scope and deliverables:** Deliver progressive shared profile/module preferences, guest namespace, date-preserving universal Add, minimal Weight/Note, simple/detail/numeric controls. Goal/routine preview binds later parts; no invented estimator.
3. **Prerequisites:** 0N. Require their acceptance evidence, not only code.
4. **PDF pages:** 2, 4-5, 7, 19 (physical pages).
5. **ARCHITECTURE sections:** 2.1-2.2, 3.1, 4.2, 6.1-6.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/features/{profile,preferences,journal}/; apps/universal/src/application/selected-date.ts; apps/universal/src/data/repositories/{profile-goals.ts,sleep-journal.ts}; apps/universal/src/app/{onboarding.tsx,settings.tsx,add/weight.tsx,add/note.tsx}; packages/domain/src/{profile,journal}/; packages/contracts/src/records/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Profile/PreferencePeriod; module eligibility; EventContext; Measurement/Note; selected-date port.
8. **Edge cases:** Sleep-only asks no weight/calories; enabling another module reuses inputs; re-enabling restores preferences; midnight editor date; disabled history; blank weight. Existing-goal review is integrated when part 13 supplies goal versions.
9. **Unit and integration tests:** Unit: Profile requirement, effective-period, date-capture and unit tests. Integration: Both repositories commit profile/preferences/measurement/note plus outbox/drafts; migration recovery.
10. **Browser testing:** Keyboard/mobile onboarding, stable tabs, Add chosen yesterday and dirty-editor navigation.
11. **Android compatibility:** Installed date/keyboard/back, guest save, kill/reopen and module-toggle checks.
12. **Security/privacy:** O4 before real data; notes protected; no required account or server anonymous guest.
13. **Acceptance criteria:** [ ] Any single module can start locally; relevant questions only; Weight/Note/Add preserve visible date and units.
14. **Manual verification:** Start sleep-only guest onboarding without weight/calorie questions; use the implemented Note shortcut to save yesterday; enable Food and verify reused answers, restored preferences and retained history. Actual Sleep entry is verified in part 5, Food in part 3, and existing-goal review in part 13.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record preference defaults, consent separation and source/schema creation.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-2"></a>

### 2 - Manual nutrition calculations and records

1. **Part / status:** 2 - Manual nutrition calculations and records; Core M1; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement deterministic confirmed nutrition snapshots, source/basis normalization and manual total/per-basis override rules. No external search or AI.
3. **Prerequisites:** 1. Require their acceptance evidence, not only code.
4. **PDF pages:** 3, 6, 18-19 (physical pages).
5. **ARCHITECTURE sections:** 4.2, 4.4, 7.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/food/; packages/contracts/src/records/; packages/test-utils/src/; tests/fixtures/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** FoodEntry/ComponentSnapshot; nutrient registry; quantity/basis; nullable values; explicit override scopes.
8. **Edge cases:** Missing protein; source energy differs rounded macros; raw/cooked; bowl without grams; entry-total override quantity change.
9. **Unit and integration tests:** Unit: Decimal scaling/property and missingness/override fixtures including 150g arithmetic and cake ambiguity. Integration: Schema/domain serialization and historical source-snapshot immutability fixtures.
10. **Browser testing:** No food screen yet; calculation display exercised in part 3.
11. **Android compatibility:** Shared calculation parity smoke; UI/native persistence belongs to part 3.
12. **Security/privacy:** Synthetic licensed fixtures; no nutritional prescription or inferred exact mass.
13. **Acceptance criteria:** [ ] Known subtotals/unknown coverage explicit; preserved source energy and immutable confirmed snapshots.
14. **Manual verification:** Inspect synthetic source calculation, unknown nutrient, and overridden quantity confirmation cases.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record nutrient registry/override contract and provenance decisions.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-3"></a>

### 3 - Reliable manual Food logging and corrections

1. **Part / status:** 3 - Reliable manual Food logging and corrections; Core M1; Not Started; [ ] complete.
2. **Scope and deliverables:** Deliver manual Food add/detail/edit/delete/undo with optional description, explicit date, nutrient drilldown, immediate local commit and retryable errors. Day completeness UI arrives in 16.
3. **Prerequisites:** 1, 2. Require their acceptance evidence, not only code.
4. **PDF pages:** 3, 6-7, 13, 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 5.1, 6.1, 6.3, 7.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/features/food/; apps/universal/src/app/{add/food.tsx,entry.tsx}; apps/universal/src/data/repositories/food-journal.ts; packages/domain/src/food/; packages/contracts/src/commands.ts; tests/web/journal.spec.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Confirmed FoodEntry snapshots; local command/draft/outbox; undo reference; EventContext.
8. **Edge cases:** 00:30 dinner yesterday; failed save; stale draft; delete/undo identity; decimal text; source overrides.
9. **Unit and integration tests:** Unit: Command validation, correction, date-invalidation and undo fixtures. Integration: Both real stores commit entry/outbox/undo atomically, reopen and migrate pending records.
10. **Browser testing:** Offline manual add/edit/delete/undo and nutrient unknown display; no false saving success.
11. **Android compatibility:** Installed offline food/date/keyboard flow with kill/reopen.
12. **Security/privacy:** Protected payloads; no auth/AI requirement; safe note/description rendering.
13. **Acceptance criteria:** [ ] T01/T15 local slice passes; actual confirmed values/date survive; no duplicate correction or false save.
14. **Manual verification:** Log synthetic dinner after midnight to yesterday, edit mass, delete/undo, restart offline.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record Food schema/migration and T01/T15 evidence.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-4"></a>

### 4 - Recent foods and saved meal versions

1. **Part / status:** 4 - Recent foods and saved meal versions; Core M1; Not Started; [ ] complete.
2. **Scope and deliverables:** Add recent selection, explicitly saved meal definitions, repeat/copy to chosen date and known-basis portion edits. Remember updates create new definition version. Rich recipe yield is Later.
3. **Prerequisites:** 3. Require their acceptance evidence, not only code.
4. **PDF pages:** 6, 16, 19 (physical pages).
5. **ARCHITECTURE sections:** 4.2, 7.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/features/food/; apps/universal/src/data/repositories/food-journal.ts; packages/domain/src/food/; packages/contracts/src/records/; tests/fixtures/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** SavedMealVersion; copied confirmed components; stable definition/new entry IDs.
8. **Edge cases:** Identical meals legitimate; old log edit changes neither saved version nor past logs; total override cannot auto-scale.
9. **Unit and integration tests:** Unit: Version/identity/portion and explicit Remember tests. Integration: Both stores repeat/copy/reopen/migration and outbox relationship tests.
10. **Browser testing:** Repeat/copy date chips, old/new definition selection and offline fallback.
11. **Android compatibility:** Installed saved/repeat/portion flow, fonts/keyboard and offline restart.
12. **Security/privacy:** Local protected definitions; no implicit personal food memory consent.
13. **Acceptance criteria:** [ ] T16 passes locally: copied entries have new IDs/date; past and reusable snapshots stable.
14. **Manual verification:** Repeat breakfast tomorrow, edit original, explicitly Remember another version and compare history.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Document reusable-version and override semantics.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-5"></a>

### 5 - Manual duration-first Sleep logging

1. **Part / status:** 5 - Manual duration-first Sleep logging; Core M1; Not Started; [ ] complete.
2. **Scope and deliverables:** Deliver local duration-first main/nap add/edit/delete/undo, optional timing/restfulness, wake-date default where known and explicit backdating. No wearable ingestion.
3. **Prerequisites:** 1. Require their acceptance evidence, not only code.
4. **PDF pages:** 4, 11, 13, 19 (physical pages).
5. **ARCHITECTURE sections:** 4.2, 6.1, 9.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/features/sleep/; apps/universal/src/app/add/sleep.tsx; apps/universal/src/data/repositories/sleep-journal.ts; packages/domain/src/sleep/; packages/contracts/src/records/; tests/fixtures/sleep-overlaps.json (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** SleepSession/Observation; main/nap; duration minutes; optional endpoints/interval meaning.
8. **Edge cases:** Duration-only no endpoints; one endpoint; overnight/DST; time-in-bed shorter slept duration; negative/noninteger input.
9. **Unit and integration tests:** Unit: Timing/duration/precision/attribution and no-fabricated-endpoint tests. Integration: Both stores transactional sleep+outbox/reopen/corrections.
10. **Browser testing:** Duration-only save without weight/calories; optional timings/backdate and errors.
11. **Android compatibility:** Installed overnight/date picker/keyboard/kill-reopen tests.
12. **Security/privacy:** O4 real-data gate; no diagnosis or readiness inference from duration alone.
13. **Acceptance criteria:** [ ] Manual Sleep works independently/offline; timing semantics preserved. Part 8, which depends on both 3 and 5, verifies the combined manual Food/Sleep prerequisite before workout state work.
14. **Manual verification:** Save duration only, add a nap, backdate overnight sleep and inspect separate duration/interval meaning.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record manual sleep semantics and T12/T13 slice.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-6"></a>

### 6 - Sleep overlap reconciliation

1. **Part / status:** 6 - Sleep overlap reconciliation; Core M1; Not Started; [ ] complete.
2. **Scope and deliverables:** Add overlap/suspected duplicate review and deterministic confirmed totals; preserve originals and selected attribution. Future source imports remain excluded.
3. **Prerequisites:** 5. Require their acceptance evidence, not only code.
4. **PDF pages:** 11, 13, 18 (physical pages).
5. **ARCHITECTURE sections:** 4.2, 6.3, 9.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/sleep/; apps/universal/src/features/sleep/; apps/universal/src/data/repositories/sleep-journal.ts; tests/fixtures/sleep-overlaps.json (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** ReconciliationGroup; inclusion/exclusion; source identity seam; provisional totals.
8. **Edge cases:** Cross-date overlaps; continuous interval union; container duration ambiguity; duration-only duplicates; undone resolution.
9. **Unit and integration tests:** Unit: Union no-double-counting/property and reconciliation-state fixtures. Integration: Both stores atomic resolution and old/new-date invalidations.
10. **Browser testing:** Overlap review shows included/excluded/unresolved evidence; totals provisional before choice.
11. **Android compatibility:** Installed multi-session reconciliation and offline reopen.
12. **Security/privacy:** Minimum evidence; no silent source deletion or fabricated sleep stages.
13. **Acceptance criteria:** [ ] T12 passes: definite totals only for resolved evidence; no counting interval twice or inferring unknown timing.
14. **Manual verification:** Enter overlapping continuous and container examples, compare unresolved/resolved totals and undo.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record overlap rules and source provenance readiness.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-7"></a>

### 7 - Equipment and minimal exercise catalog

1. **Part / status:** 7 - Equipment and minimal exercise catalog; Core M1/M2; Not Started; [ ] complete.
2. **Scope and deliverables:** Add home/gym/travel profiles and a bounded reviewed catalog for manual routine/session selection. O5/content-rights gate applies to released exercise advice; synthetic catalog may develop first.
3. **Prerequisites:** 1. Require their acceptance evidence, not only code.
4. **PDF pages:** 8-9, 19, 22 (physical pages).
5. **ARCHITECTURE sections:** 3.1, 4.2, 8.1, 14.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/features/equipment/; apps/universal/src/app/equipment.tsx; packages/domain/src/catalog/; packages/contracts/src/records/; tests/fixtures/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** EquipmentProfile; versioned reviewed ExerciseDefinition; typed measurement/load convention.
8. **Edge cases:** Unavailable equipment; excluded movements; bodyweight/assisted/unilateral/timed/distance; per-dumbbell versus total barbell.
9. **Unit and integration tests:** Unit: Measurement/catalog/equipment validation fixtures. Integration: Local profile/catalog cache and schema version compatibility.
10. **Browser testing:** Keyboard searchable selector, unavailable/unknown catalog result and Bangla labels.
11. **Android compatibility:** Installed selector and measurement variants without unsupported native imports.
12. **Security/privacy:** Document license/curator review; no invented exercise/equipment or unreviewed treatment guidance.
13. **Acceptance criteria:** [ ] Manual users choose explicit measurement conventions; catalog provenance/review recorded; no automatic generation.
14. **Manual verification:** Create home/travel profiles; select different measurement modes and inspect excluded equipment behavior.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record catalog rights/version/curation and O5 open/closed state.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-8"></a>

### 8 - Manual routines and session drafts

1. **Part / status:** 8 - Manual routines and session drafts; Core M1/M2; Not Started; [ ] complete.
2. **Scope and deliverables:** Deliver manual ordered routines/templates and custom/plan session drafts with stable slots and recoverable input. No performed rows until part 9 completion actions.
3. **Prerequisites:** 3, 5, 7. Require their acceptance evidence, not only code.
4. **PDF pages:** 8-9, 19 (physical pages).
5. **ARCHITECTURE sections:** 4.2, 8.1-8.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/features/workout/; apps/universal/src/app/{routine.tsx,session.tsx,add/workout.tsx}; apps/universal/src/data/repositories/workout-schedule.ts; packages/domain/src/workout/; packages/contracts/src/records/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** RoutineVersion; WorkoutSession/ExerciseInstance; immutable original plan/stable slot; explicit warm-up versus working set kind; typed measurement/load convention; DraftActual.
8. **Edge cases:** Unchecked default/draft counts zero; warm-up and working kinds survive copy/edit; add/duplicate slot new ID; empty routine/custom baseline; interrupted editor.
9. **Unit and integration tests:** Unit: Snapshot/slot/draft, warm-up versus working classification and typed-value tests. Integration: Both stores save/reopen/migrate routine/session drafts and preserve set kind without performed actuals.
10. **Browser testing:** Manual three-module baseline: create/edit workout draft offline; original values preserved.
11. **Android compatibility:** Installed draft/keyboard/kill-reopen and load conventions.
12. **Security/privacy:** Protected drafts; reviewed catalog usage; no implied workout advice from synthetic defaults.
13. **Acceptance criteria:** [ ] Food/Sleep/manual Workout drafts all usable; unchecked plan has zero performed work/volume; warm-up and working set kinds explicit and preserved.
14. **Manual verification:** Create three-set working bench draft plus separate warm-up slot, edit unchecked load, kill/reopen and verify kinds and zero actual-set count.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record M1 baseline and immutable plan/draft separation.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-9"></a>

### 9 - Performed-set completion identity

1. **Part / status:** 9 - Performed-set completion identity; Core M2; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement complete-one-set, edit actuals, undo-one-set and recompletion with immediate durable persistence. Preserve warm-up/working kind and display read-only last comparable performed values/session context on the Workout destination and set editor; use exercise/equipment/measurement/load-convention comparability, never progression advice. Exercise/session finish remains part 10.
3. **Prerequisites:** 8. Require their acceptance evidence, not only code.
4. **PDF pages:** 4, 8-9, 18, 22 (physical pages).
5. **ARCHITECTURE sections:** 2.1, 4.3, 5.1, 8.1-8.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/workout/; apps/universal/src/features/workout/; apps/universal/src/app/(tabs)/workout.tsx; apps/universal/src/application/{command-services.ts,query-services.ts}; apps/universal/src/data/repositories/workout-schedule.ts; packages/contracts/src/commands.ts; tests/android/maestro/journal-offline.yaml. Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan.
7. **Interfaces/data-model dependencies:** Session aggregate revision; slot/PerformedSet identity and warm-up/working kind; actual variant/completedAt; stable command ID; read-only comparable actual-history query.
8. **Edge cases:** Repeated check; unchecked edits; warm-up versus working; zero/blank; two local writers; backdated performance versus action time; no prior comparable work; partial/undone sessions; different equipment/load convention.
9. **Unit and integration tests:** Unit: Set-ID conservation/replay/property, set-kind preservation and measurement-state tests; last-comparable filters with no-match, partial, undone and incompatible equipment/load fixtures. Integration: Both stores atomic projection/outbox/undo, actual-history query, synthetic server command contract fixtures and completed/undone history recalculation.
10. **Browser testing:** Check/edit/undo/recheck visible values; storage failure shows unsaved state.
11. **Android compatibility:** Installed real SQLite kill immediately after check and reopen; Hermes/date tests.
12. **Security/privacy:** No performed data fabricated from defaults absent explicit action; protected records.
13. **Acceptance criteria:** [ ] Same performed ID and set kind through edit/undo/recompletion; only completed actuals count; local save survives interruption; last comparable values disclose their session/context and no-match state without mixing incompatible work.
14. **Manual verification:** Check first two working bench slots and a warm-up, edit/undo/recheck, restart and count identities/kinds. Start next compatible session and compare actual-history context; change equipment/load convention and verify incompatible values are excluded.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record performed-set state evidence and T02/T09 local slice.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-10"></a>

### 10 - Explicit exercise and session finish

1. **Part / status:** 10 - Explicit exercise and session finish; Core M2; Not Started; [ ] complete.
2. **Scope and deliverables:** Add counted zero-completed Complete all N, separate Complete remaining, partial exercise Finish, explicit session recap/Finish/Skip and grouped undo. No schedule consumption yet for unlinked sessions.
3. **Prerequisites:** 9. Require their acceptance evidence, not only code.
4. **PDF pages:** 9, 13, 19, 22 (physical pages).
5. **ARCHITECTURE sections:** 8.2-8.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/workout/; apps/universal/src/features/workout/; apps/universal/src/application/command-services.ts; tests/fixtures/three-set-workout.json; tests/web/workout.spec.ts; tests/android/maestro/workout.yaml (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Active/closed lifecycle; completed/finished-early/skipped outcomes; grouped conditional undo.
8. **Edge cases:** Finish 2/3 skips third; N=0; all checked still active; closed-object reopen; custom no invented denominator; undo Finish preserves actuals.
9. **Unit and integration tests:** Unit: Transition table, group-undo and retry/reopen property tests. Integration: Both stores multi-object atomic finish/undo/failure and interruption tests.
10. **Browser testing:** Distinct counted quick action versus partial Finish; accessible recap/undo.
11. **Android compatibility:** Installed custom/partial/all-checked/zero-work session and crash-resume checks.
12. **Security/privacy:** No punitive or fabricated completion; revision guards prevent erasing newer edits.
13. **Acceptance criteria:** [ ] T02/T08 pass locally; Finish creates no extra actuals; all session closure explicit.
14. **Manual verification:** Perform bench 2/3 then Finish; Undo Finish keeps two sets; test zero-work Skip and custom finish.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record full workout lifecycle and original-scope coverage.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-11"></a>

### 11 - Flexible schedule and routine sequence

1. **Part / status:** 11 - Flexible schedule and routine sequence; Core M2; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement preferred/rest days, occurrence move/skip, pause, Continue with next preview and atomic linked finish/consumption/undo. Custom sessions link only via explicit eligible choice.
3. **Prerequisites:** 1, 10. Require their acceptance evidence, not only code.
4. **PDF pages:** 10, 13, 19, 22 (physical pages).
5. **ARCHITECTURE sections:** 3.2, 6.2, 8.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/features/scheduling/; apps/universal/src/app/schedule.tsx; packages/domain/src/scheduling/; apps/universal/src/application/command-services.ts; apps/universal/src/data/repositories/workout-schedule.ts; packages/contracts/src/commands.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** PlannedSession stable occurrence; preferred slots versus sequence; session/schedule preconditions.
8. **Edge cases:** Move/lateness/crash no consume; finish/skip once; competing starts; active-work skip; rest-day custom; downstream undo conflict.
9. **Unit and integration tests:** Unit: Exactly-once consumption and sequence/compensation property tests. Integration: Both stores multi-aggregate CAS and rollback, immutable occurrence snapshot fixtures.
10. **Browser testing:** Move/skip preview, pause/rest labels and history accessibility.
11. **Android compatibility:** Installed back/kill/late/move/custom linked/unlinked schedule scenarios.
12. **Security/privacy:** No nagging disabled/paused domains; no silent prior work loss.
13. **Acceptance criteria:** [ ] T07/T11 local slice passes; identity preserved and consumption atomically tied to explicit outcome.
14. **Manual verification:** Move Monday session, finish partly, undo before/after downstream schedule change and inspect conflict.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record O3 policy implementation and schedule revision boundaries.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-12"></a>

### 12 - Today-only and future routine versions

1. **Part / status:** 12 - Today-only and future routine versions; Core M2; Not Started; [ ] complete.
2. **Scope and deliverables:** Add today-only changes versus Also to routine future version, explicit replacement of unstarted occurrences and historical routine view.
3. **Prerequisites:** 8, 11. Require their acceptance evidence, not only code.
4. **PDF pages:** 8-9, 18 (physical pages).
5. **ARCHITECTURE sections:** 4.2-4.3, 8.2-8.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/{workout,scheduling}/; apps/universal/src/features/workout/; apps/universal/src/application/command-services.ts; apps/universal/src/data/repositories/workout-schedule.ts; packages/contracts/src/commands.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Routine pointer/version; original/current session scope; explicit unstarted replacement.
8. **Edge cases:** Concurrent pointer edit; started occurrence immutable original; omitted original sets; change after close requires reopen.
9. **Unit and integration tests:** Unit: Version/snapshot preservation and coordinated revision tests. Integration: Both stores session+future-version all-or-nothing and failure tests.
10. **Browser testing:** Separate actions and future-effect preview; history comparison.
11. **Android compatibility:** Installed today/future changes, offline reopen and snapshot parity.
12. **Security/privacy:** Preserve owned references; no silent wider scope application.
13. **Acceptance criteria:** [ ] T10 passes locally; current original plan/prior sessions preserved; future versions explicit.
14. **Manual verification:** Add exercise today, compare routine; repeat with Also to routine and inspect next eligible occurrence.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record routine/version update contract and immutable history evidence.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-13"></a>

### 13 - Manual goals and dated target snapshots

1. **Part / status:** 13 - Manual goals and dated target snapshots; Core M3; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement manual goals/targets with next-journal-day activation and immutable historical bindings, preview and manual target history. Automated estimate belongs to 14.
3. **Prerequisites:** 3, 5, 11, 12. Require their acceptance evidence, not only code.
4. **PDF pages:** 5, 7, 13, 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 4.2-4.3, 6.2, 11.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/goals/; apps/universal/src/features/goals/; apps/universal/src/app/goals.tsx; apps/universal/src/data/repositories/profile-goals.ts; packages/contracts/src/{records,commands.ts} (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** GoalTimeline/version; unique daily TargetSnapshot; input/policy provenance; effective date.
8. **Edge cases:** First activation today unassessed; offline captured tomorrow; accepted historical binding conflict; no target; goal change then old edit; re-enabled module restores preferences and asks whether the old goal still applies without changing historical bindings.
9. **Unit and integration tests:** Unit: Effective-date/snapshot immutability and candidate-conflict fixtures. Integration: Both stores timeline+binding CAS, migrated pending activations and invalidation tests.
10. **Browser testing:** Activation preview clearly names effective date; no retroactive option.
11. **Android compatibility:** Installed dates/travel/offline activation/reconnect contract scenarios.
12. **Security/privacy:** No guessed health thresholds/forecast; owner manual controls; O5 later automation.
13. **Acceptance criteria:** [ ] T05/T18 local semantics pass; first/subsequent next-day activation; old target/input version never rewritten.
14. **Manual verification:** Create first target today, inspect today/tomorrow; change later and edit yesterday record. Disable/re-enable the module, review its old goal, and verify any newly accepted activation begins next journal day without rewriting past targets (R08/T05/T22).
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record O3 activation details and future server conflict tests.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-14"></a>

### 14 - Reviewed maintenance and goal discussion

1. **Part / status:** 14 - Reviewed maintenance and goal discussion; Core M3 policy-gated; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement approved provisional resting/maintenance/chosen-target distinctions, uncertainty and realistic goal alternatives. Manual paths remain independent; no precise body-composition/deadline prediction.
3. **Prerequisites:** 13; O5 reviewed policy approval. Require their acceptance evidence, not only code.
4. **PDF pages:** 5, 19, 22, 24 (physical pages).
5. **ARCHITECTURE sections:** 6.2, 7.3, 14.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/{policy,goals}/; apps/universal/src/features/goals/; tests/fixtures/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Versioned reviewer-approved formula/activity/goal/protein/population rules; input snapshot.
8. **Edge cases:** Declined physiological input; unsupported population; activity double-add; blank values; review unavailable.
9. **Unit and integration tests:** Unit: Qualified-reviewer fixtures for supported inputs/bounds and manual fallback. Integration: Policy version/input snapshot survives activation, migration and historical edits.
10. **Browser testing:** How calculated, manual option, eligibility and alternative goal discussion.
11. **Android compatibility:** Installed formula/unit/date parity, screen reader wording and manual fallback.
12. **Security/privacy:** No advice before O5; PDF examples do not approve numerical policy; unsupported conditions stay logging/manual.
13. **Acceptance criteria:** [ ] Reviewed fixtures pass; estimate differs clearly from target; method/inputs/version visible; manual fallback always works.
14. **Manual verification:** Compare approved examples, decline formula input, inspect manual path and unsupported scope messaging.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record reviewer/owner approval provenance and versioned policy, no clinical claims.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-15"></a>

### 15 - Configurable progress bars and nutrient detail

1. **Part / status:** 15 - Configurable progress bars and nutrient detail; Core M3; Not Started; [ ] complete.
2. **Scope and deliverables:** Add goal-based at-most-two initial bars, pin/remove/reorder extras, target zones and meaningful nutrient drilldown. Manual targets support this without waiting for automatic policy.
3. **Prerequisites:** 4, 13. Require their acceptance evidence, not only code.
4. **PDF pages:** 5-7, 19 (physical pages).
5. **ARCHITECTURE sections:** 2.2, 6.3, 9.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/features/{food,goals,preferences}/; apps/universal/src/ui/{components,charts}/; packages/domain/src/goals/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Selected/pinned nutrient bars; effective targets; known subtotal/coverage; numeric hiding.
8. **Edge cases:** Over-target no extra reward; partial/unknown intake; no active target; numeric text in accessibility labels; detail toggle.
9. **Unit and integration tests:** Unit: Selection/order/zone/unknown and hidden-number component tests. Integration: Preferences+target snapshot+food read model integration.
10. **Browser testing:** Keyboard reorder/remove, zoom/touch and accessible text alternative.
11. **Android compatibility:** Installed layout/large text/TalkBack and shared state parity.
12. **Security/privacy:** Do not delete hidden nutrients; nonpunitive progress; no disclosure through hidden accessibility text.
13. **Acceptance criteria:** [ ] Bars reflect confirmed evidence/current dated target; user controls persist; unknown and unassessed labeled.
14. **Manual verification:** Pin protein, hide numbers, inspect screen-reader text, exceed synthetic target without extra celebration.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record progress-bar semantics and T25 numeric hiding evidence.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-16"></a>

### 16 - Coverage and eligible-day state

1. **Part / status:** 16 - Coverage and eligible-day state; Core M3; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement explicit partial/complete/unknown Food coverage and valid zero-intake assertion; separate eligibility, attainment, plan state, sleep resolution and sync axes.
3. **Prerequisites:** 3, 6, 11, 13. Require their acceptance evidence, not only code.
4. **PDF pages:** 6-7, 11-13, 18, 22 (physical pages).
5. **ARCHITECTURE sections:** 4.2, 6.2-6.3, 9.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/journal/; apps/universal/src/features/journal/; apps/universal/src/data/repositories/; packages/contracts/src/records/; tests/fixtures/imperfect-week.json (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** DayStatus; zero-intake assertion; preference periods; plan/rest/outcome; nutrient sufficiency.
8. **Edge cases:** Empty complete not zero; add/edit invalidates zero assertion; last meal moved/deleted; paused history; rest/custom work.
9. **Unit and integration tests:** Unit: Missingness/zero-assertion/eligibility timeline tests. Integration: Both stores DayStatus revision, assertion invalidation and snapshot joins.
10. **Browser testing:** Completeness/zero controls distinct; disabled/paused/rest/unknown labels.
11. **Android compatibility:** Installed coverage controls and historical preference behavior.
12. **Security/privacy:** No low-intake conclusion from partial/unknown; no auto-complete by meal count.
13. **Acceptance criteria:** [ ] T04/T07 semantics hold; unknown/partial never failed or zero; historical denominators stable.
14. **Manual verification:** Mark empty day complete, explicitly confirm zero, then add/move entry and inspect assertion invalidation.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record coverage axes and evidence policy.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-17"></a>

### 17 - Coverage-aware aggregates and invalidation

1. **Part / status:** 17 - Coverage-aware aggregates and invalidation; Core M3; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement daily/period nutrient/sleep/workout facts, comparable-period statistics and incremental invalidation/full rebuild equivalence. No UI calendar or AI prose yet.
3. **Prerequisites:** 12, 13, 16. Require their acceptance evidence, not only code.
4. **PDF pages:** 7, 11-12, 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 6.3, 9.2, 12.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/aggregates/; apps/universal/src/data/projections/; apps/universal/src/application/query-services.ts; tests/fixtures/imperfect-week.json (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Observed/complete/eligible/metric-known counts; evidence revision digest; target binding.
8. **Edge cases:** Unknown nutrient denominator; partial month/year; incompatible load conventions; date move invalidates both; unresolved sleep; stale target candidate.
9. **Unit and integration tests:** Unit: Property tests for missingness, historical target selection and incremental/full rebuild equality. Integration: Both stores corrections/delete/undo/reconciliation update all affected read models.
10. **Browser testing:** Consumer view checks in 18-21; pure output text reviewed here.
11. **Android compatibility:** Execute shared aggregate fixtures on Hermes through existing harness.
12. **Security/privacy:** No health score/cause/low-intake assertion from inadequate evidence.
13. **Acceptance criteria:** [ ] T04/T05/T17 calculations pass; old targets stay; cached fact identity includes evidence/calculator versions.
14. **Manual verification:** Run imperfect-week fixture, correct old meal date and compare rebuild/incremental period output.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record calculator version/cache invalidation and metric denominators.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-18"></a>

### 18 - Day journal and accessible history

1. **Part / status:** 18 - Day journal and accessible history; Core M3; Not Started; [ ] complete.
2. **Scope and deliverables:** Deliver day view for each module with entries, target/coverage labels, edit/backdate navigation and accessible agenda.
3. **Prerequisites:** 15, 17. Require their acceptance evidence, not only code.
4. **PDF pages:** 4, 7, 11-12, 19 (physical pages).
5. **ARCHITECTURE sections:** 2.1, 6.1, 9.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/app/journal/day.tsx; apps/universal/src/features/journal/; apps/universal/src/ui/calendar/; tests/web/journal.spec.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Selected-date/context; domain day entries/coverage/targets; history links.
8. **Edge cases:** Empty/disabled history; rest with custom session; dirty edit; midnight default versus captured date; conflict provisional.
9. **Unit and integration tests:** Unit: Date-navigation/label component tests. Integration: Entry correction through day view invalidates correct read models.
10. **Browser testing:** Keyboard date selection, back/refresh, mobile reflow and focused edit return.
11. **Android compatibility:** Installed back/date/keyboard/large-text behavior.
12. **Security/privacy:** Record route params do not authorize; safe sensitive text and numeric hiding.
13. **Acceptance criteria:** [ ] Day drilldown preserves chosen date and honest independent states across modules.
14. **Manual verification:** Navigate yesterday in each module, edit from day view and return with date preserved.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Document day route/read model and browser/device evidence.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-19"></a>

### 19 - Month calendar and coverage statistics

1. **Part / status:** 19 - Month calendar and coverage statistics; Core M3; Not Started; [ ] complete.
2. **Scope and deliverables:** Add selectable daily month rings plus observed/complete/eligible/known counts, partial-month label and date-preserving drilldown.
3. **Prerequisites:** 18. Require their acceptance evidence, not only code.
4. **PDF pages:** 7, 11-12, 19 (physical pages).
5. **ARCHITECTURE sections:** 2.1-2.2, 6.3, 9.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/app/journal/month.tsx; apps/universal/src/ui/calendar/; apps/universal/src/features/journal/; tests/web/journal.spec.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Month cells/rings; module-specific meanings; agenda alternative; elapsed comparable period.
8. **Edge cases:** Leap month; unknown/paused/rest; complete unknown nutrient; no target; more sleep not unlimited achievement.
9. **Unit and integration tests:** Unit: Ring classification, grid keyboard and coverage-label tests. Integration: Corrections and date moves update month immediately.
10. **Browser testing:** Keyboard/calendar agenda, screen-reader order, zoom and actual Safari milestone.
11. **Android compatibility:** Installed month touch/large-text/TalkBack and day return.
12. **Security/privacy:** No unexplained combined score or missing-as-failure coloring.
13. **Acceptance criteria:** [ ] Month states match facts and historical targets; accessible labels/agenda convey equivalent meaning.
14. **Manual verification:** Use imperfect-week month, select unknown/rest day, correct old entry and inspect rings/counts.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record ring semantics and month evidence.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-20"></a>

### 20 - Year calendar and comparable trends

1. **Part / status:** 20 - Year calendar and comparable trends; Core M3; Not Started; [ ] complete.
2. **Scope and deliverables:** Add twelve-month overview/trends and month/day drilldown, partial-year labeling and coverage disclosures.
3. **Prerequisites:** 19. Require their acceptance evidence, not only code.
4. **PDF pages:** 7, 11-12, 19 (physical pages).
5. **ARCHITECTURE sections:** 6.3, 9.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/app/journal/year.tsx; apps/universal/src/ui/{calendar,charts}/; apps/universal/src/features/journal/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Twelve month tiles; year aggregates; historical goal changes; like elapsed periods.
8. **Edge cases:** Leap year; sparse history; date across year; changing targets; unsupported load comparisons.
9. **Unit and integration tests:** Unit: Year period/label/navigation tests. Integration: Old edit/date reassignment rebuilds all affected years and months.
10. **Browser testing:** Responsive grid, keyboard/SR/text trend alternatives and date drilldown.
11. **Android compatibility:** Installed year layout/scroll/TalkBack and shared fixture parity.
12. **Security/privacy:** Trend text limited to facts; hidden numbers remain hidden in alternatives.
13. **Acceptance criteria:** [ ] T17 year slice passes; compare like elapsed windows and disclose missing/known counts.
14. **Manual verification:** Inspect sparse/current year, drill down, move record across year boundary and compare updated counts.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Document period comparison convention and year evidence.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-21"></a>

### 21 - Overall factual dashboard

1. **Part / status:** 21 - Overall factual dashboard; Core M3; Not Started; [ ] complete.
2. **Scope and deliverables:** Deliver compact enabled-module cards, separate domain rings, factual trends and descriptive reflection. Coaching/AI remain 36-37 after reviewed intelligence.
3. **Prerequisites:** 20. Require their acceptance evidence, not only code.
4. **PDF pages:** 12, 19, 22 (physical pages).
5. **ARCHITECTURE sections:** 2.1, 3.1, 6.3, 9.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/features/overall/; apps/universal/src/app/(tabs)/overall.tsx; packages/domain/src/aggregates/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Enabled-domain read models; coverage/conflict/staleness; descriptive weekly facts.
8. **Edge cases:** Single-module user; contradictory/sparse evidence; paused week; historical correction; provisional conflict.
9. **Unit and integration tests:** Unit: Visibility/fact/coverage/deterministic-copy tests. Integration: Dashboard subscriptions reflect corrections, targets and preference timelines.
10. **Browser testing:** Desktop/mobile cards, linked day view, text chart alternatives.
11. **Android compatibility:** Installed dashboard/rotation/large-text and stale state display.
12. **Security/privacy:** No global health score, causal verdict, fabricated inactivity or medical claims.
13. **Acceptance criteria:** [ ] T01/T04/T05/T07 dashboard slice passes; only factual evidence shown with coverage.
14. **Manual verification:** Disable Workout, enter incomplete Food, correct yesterday and inspect cards/trend staleness.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record factual Overall boundary and later coaching dependency.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-22"></a>

### 22 - Product account lifecycle and isolation

1. **Part / status:** 22 - Product account lifecycle and isolation; Core M4; Not Started; [ ] complete.
2. **Scope and deliverables:** Extend feasibility into complete register/sign-in/verify/reset/logout/local-copy/account-switch UX. Login offers import choice but does not upload guest data; import is part 27.
3. **Prerequisites:** 0K, 21; O4 approved local-copy/key policy before real data. Require their acceptance evidence, not only code.
4. **PDF pages:** 4, 18-19 (physical pages).
5. **ARCHITECTURE sections:** 5.5, 10.1-10.2, 11.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/features/account/; apps/universal/src/app/account/{sign-in,sign-up,verify,recovery}.tsx; apps/universal/src/application/namespace-session.ts; apps/universal/src/adapters/auth/; apps/api/src/plugins/auth.ts; apps/api/src/database/schema/identity.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Verified account/JournalAccount mapping; protected namespace; session generation; email/recovery.
8. **Edge cases:** Offline/expired session; reset is not vault recovery; unsynced logout warning; stale requests; enumeration/email outage.
9. **Unit and integration tests:** Unit: Account state/generation/copy-choice tests. Integration: Real PG/auth email, browser/native transports and two-account stale-response tests.
10. **Browser testing:** Cookie/CSRF, recovery links, sign-in switch with pending local work.
11. **Android compatibility:** Installed native deep links/logout/switch, protected session and back flow.
12. **Security/privacy:** Recent/session authorization; redacted email; O4 local retention policy; no anonymous-server guest requirement.
13. **Acceptance criteria:** [ ] T21 account slice passes; no cross-account cache/data; expiry preserves protected pending intent.
14. **Manual verification:** Switch A/B with in-flight request and unsynced entry, reset password, verify no false key-recovery promise.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record tested production-like auth setup and local-copy decisions.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-23"></a>

### 23 - Server acceptance and ordered feed kernel

1. **Part / status:** 23 - Server acceptance and ordered feed kernel; Core M4; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement bounded command acceptance kernel, device/replay binding, receipts, atomic feed and owned canonical-read infrastructure with synthetic command handler. Product handlers are separate 23A-23C.
3. **Prerequisites:** 22, 0H. Require their acceptance evidence, not only code.
4. **PDF pages:** 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 4.3, 5.3, 11.1-11.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/api/src/application/{command-coordinator.ts,ownership.ts}; apps/api/src/modules/sync/; apps/api/src/database/schema/sync.ts; apps/api/src/database/repositories/; tests/api/sync-concurrency.test.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Receipt fingerprint; account lock/change sequence; expected revisions; sealed command/results; replay lease.
8. **Edge cases:** Lost ack; receipt before revision; same ID/different request; late commit/rollback; foreign cursor; group too large.
9. **Unit and integration tests:** Unit: Envelope/fingerprint/error/protocol tests. Integration: Real concurrent PG locks/rollback/duplicate and feed ordering/property tests.
10. **Browser testing:** Browser synthetic kernel request/error display; product sync later 24.
11. **Android compatibility:** Native transport smoke against same kernel; no separate API.
12. **Security/privacy:** Server-derived ownership; CSRF/rate/byte limits; account/device-bound cursors; O6 production retention gate.
13. **Acceptance criteria:** [ ] T03/T30 kernel passes: one commit/result, no split/skipped change group, missing update never create.
14. **Manual verification:** Submit same synthetic sealed operation twice and changed payload once; inspect safe receipts/feed under concurrent delay.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record bounds, ownership, protocol and O6 unresolved retention settings.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-23a"></a>

### 23A - Profile and target server commands

1. **Part / status:** 23A - Profile and target server commands; Core M4; Not Started; [ ] complete.
2. **Scope and deliverables:** Add owned server handlers/migrations for profile, preferences, manual goal activation and dated target binding via common acceptance. No alternate CRUD writes.
3. **Prerequisites:** 23, 13, 16. Require their acceptance evidence, not only code.
4. **PDF pages:** 4-5, 7, 18, 22 (physical pages).
5. **ARCHITECTURE sections:** 4.2-4.3, 5.3, 6.2, 11. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/api/src/modules/{profile,goals}/; apps/api/src/database/schema/profile-goals.ts; apps/api/src/database/repositories/; tests/api/ownership.test.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Profile/preferences/GoalTimeline expected revisions; unique accepted TargetSnapshot; shared domain rules.
8. **Edge cases:** Two offline goals; first activation; delayed effective date versus accepted history; foreign target input/reference.
9. **Unit and integration tests:** Unit: Shared goal/profile command fixtures. Integration: Real PG unique bindings, timeline conflict, migration and receipt replay/rollback tests.
10. **Browser testing:** Two-client target conflict evidence used in 25; safe request integration here.
11. **Android compatibility:** Same schemas/native transport target command smoke.
12. **Security/privacy:** Authoritative ownership/policy checks; immutable accepted historical targets; O5 only for approved advice.
13. **Acceptance criteria:** [ ] T05/T18 server slices pass; accepted binding preserved; competing candidate explicitly conflicts.
14. **Manual verification:** Replay offline activation after accepted target history and verify rejection/provisional evidence without overwrite.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record profile/goal server migrations and reviewed conflict contract.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-23b"></a>

### 23B - Food, Sleep and journal server commands

1. **Part / status:** 23B - Food, Sleep and journal server commands; Core M4; Not Started; [ ] complete.
2. **Scope and deliverables:** Add owned server command/read handlers and migrations for established Food/Sleep/Weight/Note/coverage features using common receipts/feed.
3. **Prerequisites:** 23, 4, 6, 16. Require their acceptance evidence, not only code.
4. **PDF pages:** 4, 6-7, 11, 18, 22 (physical pages).
5. **ARCHITECTURE sections:** 4.2-4.3, 5.3, 6.3, 7.1, 9.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/api/src/modules/{food,sleep,journal}/; apps/api/src/database/schema/{food,sleep-journal}.ts; apps/api/src/database/repositories/; tests/api/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Food/SavedMealVersion; Sleep/Reconciliation; DayStatus; Measurement/Note; tombstones.
8. **Edge cases:** Foreign components/groups; partial nutrient values; duplicate source identity; delete/undo; date move; explicit zero invalidation.
9. **Unit and integration tests:** Unit: Shared feature command fixtures and server normalization tests. Integration: Real PG owned FKs/revision/rollback/receipt and old/new date invalidation tests.
10. **Browser testing:** Canonical read/command contract integration; real sync display follows 24.
11. **Android compatibility:** Native transport sends same feature shapes; no platform business divergence.
12. **Security/privacy:** Sensitive payload/log redaction; parent ownership; no content-based meal deduplication.
13. **Acceptance criteria:** [ ] Existing local semantics match accepted canonical records; T01/T12/T15/T16/T19 server slice evidenced.
14. **Manual verification:** Submit correction/date move/delete and compare local expected/canonical snapshot and safe feed.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record feature migrations/constraints and compatibility fixtures.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-23c"></a>

### 23C - Workout and schedule server commands

1. **Part / status:** 23C - Workout and schedule server commands; Core M4; Not Started; [ ] complete.
2. **Scope and deliverables:** Add server handlers/migrations for routine, actual-set and linked schedule actions, including atomic finish/consumption/conditional undo.
3. **Prerequisites:** 23, 12. Require their acceptance evidence, not only code.
4. **PDF pages:** 8-10, 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 4.3, 5.3, 8, 11. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/api/src/modules/{workout,scheduling,catalog}/; apps/api/src/database/schema/workout.ts; apps/api/src/application/command-coordinator.ts; tests/api/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Session revision aggregate; occurrence uniqueness; stable performed IDs and warm-up/working kind; comparable actual-history read DTO; routine/schedule additional preconditions.
8. **Edge cases:** Concurrent starts; edits to different sets conflict; retry finish; schedule downstream undo; foreign slot; missing update.
9. **Unit and integration tests:** Unit: Shared transition/compensation, warm-up/working preservation, comparability and typed-measurement fixtures. Integration: Real PG unique occurrence/set IDs, set-kind roundtrip, comparable-history reads, deterministic lock order, all-or-nothing revisions/feed and rollback.
10. **Browser testing:** Canonical command/recap contract integration; two-client UI in 25.
11. **Android compatibility:** Native shared command transport/serialization; same semantics.
12. **Security/privacy:** No silent health-history merge; owned parent/slot validation; no fabricated actuals.
13. **Acceptance criteria:** [ ] T02/T08-T11 server slices pass; each semantic command increments affected aggregate once and cannot duplicate work; set kind and comparable actual-history context match the local contract.
14. **Manual verification:** Two concurrent clients start one occurrence, complete/finish/undo and verify canonical IDs, warm-up/working kinds, last comparable values and explicit conflicts.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record workout/schedule constraints and transaction evidence.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-24"></a>

### 24 - Client sync coordination and atomic pages

1. **Part / status:** 24 - Client sync coordination and atomic pages; Core M4; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement one bounded foreground/reconnect/manual sync coordinator, dependent sealing, identical retries, atomic acknowledgement and pull application.
3. **Prerequisites:** 23A, 23B, 23C. Require their acceptance evidence, not only code.
4. **PDF pages:** 13, 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 5.2-5.3, 11.2-11.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/data/sync/{coordinator,acknowledgements,pull}.ts; packages/api-client/; apps/universal/src/features/account/; tests/web/accounts-sync.spec.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Outbox predecessors/sealed envelope; canonical shadow/pending projection; dispatch lease; page cursor.
8. **Edge cases:** Lost ack after commit; two tabs dispatch; 429/Retry-After; 401/403; later local edit before ack; page failure.
9. **Unit and integration tests:** Unit: Retry/seal/successor/cancellation tests. Integration: Real two clients + both stores + PG with faults before/after ack/page/commit.
10. **Browser testing:** Multi-tab offline/online retry and sync state distinct from local save.
11. **Android compatibility:** Installed offline→reconnect/kill/resume and native transport; background not required.
12. **Security/privacy:** Account-bound dispatch; session switch cancels and drops stale results; logs contain no journals.
13. **Acceptance criteria:** [ ] T03/T19/T21/T30 pass: one logical record, cursor/records atomic, protected pending work preserved.
14. **Manual verification:** Save offline, lose server ack, edit again, reconnect twice and inspect identities/status.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Document sync commands, failure taxonomy and lease assumptions.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-25"></a>

### 25 - Explicit conflict review and compensation

1. **Part / status:** 25 - Explicit conflict review and compensation; Core M4; Not Started; [ ] complete.
2. **Scope and deliverables:** Add conflict UI and keep-server/reviewed replacement/preserve-for-later choices across record, goal and schedule cases. Retain all exportable evidence; part 28 implements and verifies the local export action. No timestamp winner or automatic overwrite, and no working export control is claimed before part 28.
3. **Prerequisites:** 24. Require their acceptance evidence, not only code.
4. **PDF pages:** 9, 13, 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 5.4, 6.2, 8.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/data/sync/conflicts.ts; apps/universal/src/features/account/; packages/contracts/src/sync.ts; tests/web/accounts-sync.spec.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Local/base/canonical comparison; dependent block; new reviewed resolution operation; conditional undo.
8. **Edge cases:** Different sets same session; delete versus edit; conflicting target candidate; undo after remote edit; unresolved dependent work.
9. **Unit and integration tests:** Unit: Resolution/precondition/provisional-attainment tests. Integration: Real two-client conflicts and compensating operation against current revision.
10. **Browser testing:** Accessible comparisons and explicit consequences; editor preserved.
11. **Android compatibility:** Installed conflict resolution and lock/reopen/pending preservation.
12. **Security/privacy:** Do not disclose foreign account existence; preserve evidence and bounded undo policy.
13. **Acceptance criteria:** [ ] T09/T18 pass; resolution new operation validates current canonical state; conflict-dependent attainment stays provisional.
14. **Manual verification:** Edit same set from two devices, resolve, then attempt stale undo and inspect rejected compensation.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record supported conflict choices and unresolved work evidence.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-26"></a>

### 26 - Consistent bootstrap and expired replay

1. **Part / status:** 26 - Consistent bootstrap and expired replay; Core M4; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement bounded watermark-consistent bootstrap, lease/cursor expiry and explicit pending-work reconciliation under approved policy. No blind old replay under new identity/lease.
3. **Prerequisites:** 25; O6 coupled replay/retention policy for finalization. Require their acceptance evidence, not only code.
4. **PDF pages:** 18-19 (physical pages).
5. **ARCHITECTURE sections:** 5.4, 11.3, 13.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/data/sync/rebootstrap.ts; apps/api/src/modules/sync/; apps/api/src/jobs/runner.ts; packages/contracts/src/sync.ts; tests/api/sync-concurrency.test.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Snapshot watermark/job; cursor/feed epoch; replay lease; preserved pending manifest.
8. **Edge cases:** Paged live data changes; expired job; unknown prior accepted ID after pruning; interrupted reconciliation; incompatible old client.
9. **Unit and integration tests:** Unit: Expiry/reconciliation/compatibility tests. Integration: Real PG concurrent snapshot/feed, both-store preserved pending work and restart tests.
10. **Browser testing:** Expired cursor UI, multi-tab old-shell compatibility and review/preserve choice. Preserve pending evidence for part 28's export; the integrated expired-replay-to-export path is required in part 41 after both features exist.
11. **Android compatibility:** Installed long-offline simulated epoch expiry and interrupted bootstrap.
12. **Security/privacy:** O6 exact durations approved, not guessed; snapshot account-bound; sensitive job payload expires.
13. **Acceptance criteria:** [ ] T23/T24/T30 slices pass; no loss/resurrection, one consistent snapshot watermark, old uncertainty not converted to create.
14. **Manual verification:** Expire synthetic lease while pending work exists, bootstrap during another write and review uncertainty safely.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record approved horizon/protocol/schema support and reconciliation runbook.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-27"></a>

### 27 - Explicit retryable guest import

1. **Part / status:** 27 - Explicit retryable guest import; Core M4; Not Started; [ ] complete.
2. **Scope and deliverables:** Deliver import preview/consent/progress/resume into existing/new account while preserving guest source and graph identity.
3. **Prerequisites:** 26. Require their acceptance evidence, not only code.
4. **PDF pages:** 4, 18-19 (physical pages).
5. **ARCHITECTURE sections:** 5.5, 11.1-11.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/data/sync/guest-import.ts; apps/universal/src/app/account/import.tsx; apps/api/src/modules/privacy/; packages/contracts/src/privacy.ts; apps/api/src/database/schema/operations.ts; tests/api/import-delete.test.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Frozen manifest/batch; per-item stable ops; dependency graph; ID collision mapping; destination account.
8. **Edge cases:** Interrupted partial batch; identical meals distinct; actual ID collision; post-snapshot guest edits; overlapping goals/sleep; account switch.
9. **Unit and integration tests:** Unit: Manifest/graph ordering/progress and collision-choice tests. Integration: Real PG and stores retry/chunks/owned references and import failure/restart tests.
10. **Browser testing:** Destination/count/conflict preview; no upload merely by login; reconnect resume.
11. **Android compatibility:** Installed offline guest→sign-in→explicit import and interrupted/resumed batch.
12. **Security/privacy:** Purpose-limited consent; O4/O6 source-copy retention; no silent health upload or deletion.
13. **Acceptance criteria:** [ ] T20 passes; imports idempotent; relationships intact; completion only after acknowledged manifest items.
14. **Manual verification:** Interrupt existing-account import, retry twice, add guest edit during import and inspect remaining separate work.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record import choices/retention and actual progress evidence.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-28"></a>

### 28 - Versioned local JSON and CSV export

1. **Part / status:** 28 - Versioned local JSON and CSV export; Core M4; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement user-initiated local complete JSON and useful module CSV export including retained disabled history. This is not an import/restore product.
3. **Prerequisites:** 21, 25. Require their acceptance evidence, not only code.
4. **PDF pages:** 13, 18-20 (physical pages).
5. **ARCHITECTURE sections:** 10.3, 11.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/adapters/files/{export.web.ts,export.native.ts}; apps/universal/src/features/account/; packages/contracts/src/privacy.ts; packages/domain/src/journal/; tests/security/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Versioned export schema; unlocked local snapshot; pending/conflict/accepted labels.
8. **Edge cases:** CSV formula injection; quotes/newlines/Bangla; partial local conflict; unknown time/nutrient; large export; locked vault.
9. **Unit and integration tests:** Unit: Serialization/missingness/formula-neutralization tests. Integration: Both stores consistent export content + platform file generation/cancel/cleanup.
10. **Browser testing:** Download/safe filename and explicit sensitive-file explanation.
11. **Android compatibility:** Installed native share/file cancellation and cleanup, no unprotected temporary residue.
12. **Security/privacy:** No credentials/provider tokens; export only unlocked owned store; clear retention limits.
13. **Acceptance criteria:** [ ] T29 local slice passes; original/canonical units/date/provenance/history retained with honest sync labels.
14. **Manual verification:** Export synthetic disabled-module/pending/conflicted data, including work preserved by part 25's conflict UI, and compare fields/CSV text without exposing real data. The expired-replay-to-export combination with part 26 is exercised in part 41.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record export schema/version and platform file behavior.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-29"></a>

### 29 - Account export jobs and expiry

1. **Part / status:** 29 - Account export jobs and expiry; Core M4; Not Started; [ ] complete.
2. **Scope and deliverables:** Add authorized asynchronous canonical export jobs, retry/resume, download/status/expiry and payload cleanup using versioned format.
3. **Prerequisites:** 26, 28; O6 export/job policy. Require their acceptance evidence, not only code.
4. **PDF pages:** 13, 18-20 (physical pages).
5. **ARCHITECTURE sections:** 10.3, 11.1, 13.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/api/src/jobs/{runner.ts,export.ts}; apps/api/src/modules/privacy/; apps/api/src/database/schema/operations.ts; apps/universal/src/features/account/; tests/security/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Stable export request ID; accepted-data snapshot watermark; bounded DB job lease; protected expiring artifact.
8. **Edge cases:** Job restart; account switch/deletion; expired URL; duplicate request; changing data during export.
9. **Unit and integration tests:** Unit: Job status/idempotency/download error tests. Integration: Real PG snapshot/job lease/retry + download ownership/expiry cleanup tests.
10. **Browser testing:** Create/poll/cancel/download and no false completion; foreign export denied.
11. **Android compatibility:** Installed same account job flow and native file adapter regression.
12. **Security/privacy:** O6 approved retention; protected downloads/artifacts; no wellness data in operational logs.
13. **Acceptance criteria:** [ ] T29 server slice passes; consistent accepted snapshot, one job per request, expired/foreign downloads denied.
14. **Manual verification:** Restart runner mid-export and retry request; inspect consistent fields and expiry denial.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record job/expiry policy and operational test commands.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-30"></a>

### 30 - Deletion jobs, tombstones and device proof

1. **Part / status:** 30 - Deletion jobs, tombstones and device proof; Core M4; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement record/account deletion, tracked raw/derived/export cleanup and minimal post-revocation status proof; only definitive bound deleted proof initiates local purge. Backup integration follows 31.
3. **Prerequisites:** 27, 29; O4/O6 approved deletion/proof policy. Require their acceptance evidence, not only code.
4. **PDF pages:** 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 5.4, 10.3, 11.1-11.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/api/src/jobs/deletion.ts; apps/api/src/modules/privacy/; apps/api/src/database/schema/{identity,operations,sync}.ts; apps/universal/src/data/sync/; apps/universal/src/features/account/; packages/contracts/src/privacy.ts; tests/api/import-delete.test.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Recent auth + request ID; immediate write deny; tombstone/revision; device-bound limited capability; suppression generation.
8. **Edge cases:** Offline stale edit; lost deletion ack; 401/403/no network; expired/wrong-device proof; disconnected device; undo expiry.
9. **Unit and integration tests:** Unit: Deletion state/binding/no-false-purge and tombstone tests. Integration: Real PG idempotency/session revocation/deny/cleanup/proof + two-client stale resurrection tests.
10. **Browser testing:** Explicit recent-auth confirm/status; preserved locked store when proof unavailable.
11. **Android compatibility:** Installed disconnected/reconnect/proof/purge and protected pending-loss UX.
12. **Security/privacy:** O4 key/capability and O6 lifetimes/targets approved; minimal hash/proof storage; no remote-wipe guarantee.
13. **Acceptance criteria:** [ ] T23 passes; no writes after deletion begins; retries do not recreate jobs/accounts; failures are never deletion evidence.
14. **Manual verification:** Delete synthetic account with offline second device, fail/expire proof then obtain bound proof and observe correct retention/purge.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record deletion completion semantics, suppression contract and residual exported/disconnected limits.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-31"></a>

### 31 - Independent backup and suppression restore

1. **Part / status:** 31 - Independent backup and suppression restore; Core M4; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement/rehearse isolated synthetic backup/restore, apply current deletion suppressions before opening service and rebuild derived state. Local test first; owner-approved backup service later.
3. **Prerequisites:** 30; O6 recovery/retention; O7 before external provisioning. Require their acceptance evidence, not only code.
4. **PDF pages:** 18-19 (physical pages).
5. **ARCHITECTURE sections:** 10.3, 12.2, 13.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** infra/backups/{export.sh,restore.sh,suppression-manifest.md}; tests/operations/restore-deletion.md; apps/api/src/jobs/; tests/security/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Encrypted consistent backup; independently retained suppression manifest; recovery objectives; migration readiness.
8. **Edge cases:** Restore snapshot before deletion; missing manifest/key; failed migration; incomplete backup; expired artifacts; retry cleanup.
9. **Unit and integration tests:** Unit: Manifest/restore preflight and access-deny tests. Integration: Real isolated PG backup→later deletion→old restore→current suppression rehearsal with measured recovery.
10. **Browser testing:** Restored synthetic account denied; unaffected account history/readiness intact.
11. **Android compatibility:** Native returning-client sync/proof smoke against restored isolated service.
12. **Security/privacy:** Least-privilege keys/access; no backup data committed/printed; O6 objectives measured, not promises.
13. **Acceptance criteria:** [ ] T31 passes: deleted account cannot resurrect; measured recovery and approved policy recorded; manifest independent of snapshot.
14. **Manual verification:** Run documented restore in isolated destination, deliberately omit manifest once and verify fail-closed preflight.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record actual recovery measurements, operator runbook and approved retention.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-32"></a>

### 32 - Constrained vetted workout proposals

1. **Part / status:** 32 - Constrained vetted workout proposals; Intelligence M5; Not Started; [ ] complete.
2. **Scope and deliverables:** Add bounded deterministic selection/assembly of vetted routine proposals, explain constraints and preview/edit before acceptance. No LLM-authored exercises or advanced adaptive planner.
3. **Prerequisites:** 14, 17, 31; O5 review and O8 content rights. Require their acceptance evidence, not only code.
4. **PDF pages:** 8, 19, 22 (physical pages).
5. **ARCHITECTURE sections:** 3.1, 7.3, 8, 14.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/{catalog,policy}/; apps/universal/src/features/workout/; apps/api/src/modules/catalog/; packages/contracts/src/providers.ts; tests/fixtures/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Reviewed template/version; equipment/time/preferences/exclusions; transparent proposal; explicit routine acceptance.
8. **Edge cases:** One/two/three/four/5+ day preferences; no valid equipment fit; movement limit; no Workout; sparse history.
9. **Unit and integration tests:** Unit: Reviewed constraint/template and no-invented-exercise fixtures. Integration: Proposal acceptance creates future RoutineVersion through established command path.
10. **Browser testing:** Preview/Why/change/decline without journal mutation; invalid fit honest fallback.
11. **Android compatibility:** Installed proposal/edit/accept and snapshot preservation.
12. **Security/privacy:** O5 curator bounds and O8 licenses approved; no diagnosis or forced exercise.
13. **Acceptance criteria:** [ ] Valid vetted proposal respects all hard constraints; only explicit acceptance changes routine; manual builder available.
14. **Manual verification:** Request home/time-limited routine, exclude movement, decline then edit/accept and inspect future version.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record content/policy approvals and constraint benchmark evidence.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-33"></a>

### 33 - Database-backed Food search and matching

1. **Part / status:** 33 - Database-backed Food search and matching; Intelligence M5; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement FDC server adapter/cache/search/details and editable confirmed source-match flow. Nutrients calculated from confirmed basis; provider calls outside record transactions.
3. **Prerequisites:** 2, 24, 31; O8 provider/data terms. Require their acceptance evidence, not only code.
4. **PDF pages:** 6, 18-19, 24 (physical pages).
5. **ARCHITECTURE sections:** 7.1-7.2, 11.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/api/src/providers/food/food-data-central.ts; apps/api/src/modules/catalog/; packages/domain/src/food/; packages/contracts/src/providers.ts; apps/universal/src/features/food/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Normalized provider ID/revision/basis/registry; bounded catalog cache; source proposal.
8. **Edge cases:** 429/quota/timeouts; raw/cooked; duplicate names; serving no grams; unsupported unit/nutrient; stale source refresh.
9. **Unit and integration tests:** Unit: Provider normalization/provenance/missingness fixture tests. Integration: Mocked external fixtures + real API/cache/outage/confirmed snapshot integration; live smoke only owner-authorized.
10. **Browser testing:** Search/manual/cached fallback, source assumptions and confirmation.
11. **Android compatibility:** Installed catalog request/offline fallback and Bangla rendering.
12. **Security/privacy:** Server-only provider key; O8 permitted cache/license; bounded/rate-limited queries; minimum disclosed content.
13. **Acceptance criteria:** [ ] T15/T28 source slice passes; search outage never blocks manual/saved logging; old snapshots stable.
14. **Manual verification:** Confirm source match, change quantity, refresh provider and compare old entry; simulate quota/offline.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record provider rights/source attribution and tested normalization.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-34"></a>

### 34 - Bangladesh food validation and curated records

1. **Part / status:** 34 - Bangladesh food validation and curated records; Intelligence M5; Not Started; [ ] complete.
2. **Scope and deliverables:** Add bounded vetted regional records and benchmark realistic Bangladesh search/matching/manual correction. No full bilingual UI or mass import of downloadable tables.
3. **Prerequisites:** 33; O8 regional licenses/benchmark approval. Require their acceptance evidence, not only code.
4. **PDF pages:** 6, 16, 20, 22 (physical pages).
5. **ARCHITECTURE sections:** 7.2, 14.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** tests/fixtures/regional-food/; apps/api/src/providers/food/; apps/api/src/modules/catalog/; apps/universal/src/features/food/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Licensed source/version/preparation/portion; Bangla-English benchmark; correction/unknown coverage.
8. **Edge cases:** Rice raw/cooked; dal/curry/khichuri/roti/oil; serving ambiguity; Bengali script/transliteration/mixed English; packaged variant.
9. **Unit and integration tests:** Unit: Licensed normalization/ambiguity and Unicode fixtures. Integration: Reproducible benchmark reports match/correction/unknown/manual-fallback outcomes under approved thresholds.
10. **Browser testing:** English UI displays/edit searches Bangla names across mobile/desktop.
11. **Android compatibility:** Installed glyph/input/locale and identical source/nutrient snapshots.
12. **Security/privacy:** Content rights/curator evidence; synthetic sample phrases; no personal meal logs or fabricated benchmark success.
13. **Acceptance criteria:** [ ] O8 approved bounded benchmark meets reviewed threshold; failures/coverage gaps recorded honestly.
14. **Manual verification:** Run benchmark, review ambiguous bowl/raw-cooked cases, manually correct source and inspect provenance.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record dated license/curator/threshold and observed regional results.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-35"></a>

### 35 - Optional AI Food proposals with fallback

1. **Part / status:** 35 - Optional AI Food proposals with fallback; Intelligence M5; Not Started; [ ] complete.
2. **Scope and deliverables:** Implement opt-in structured food parsing that proposes licensed matches and one bounded clarification. Confirmed arithmetic remains deterministic; stale responses cannot overwrite corrected draft.
3. **Prerequisites:** 25, 34; O8 provider/consent/caps/kill-switch approval. Require their acceptance evidence, not only code.
4. **PDF pages:** 3, 6, 16, 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 6.3, 7.3, 10.1, 11.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/api/src/providers/ai/; apps/api/src/modules/ai/; packages/contracts/src/providers.ts; apps/universal/src/features/food/; tests/security/; tests/operations/provider-outages.md (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** FoodProposal permitted source IDs/quantity/basis/exclusions/assumptions; draft version; consent and budgets.
8. **Edge cases:** Cake consumed/original mass; prompt injection; unsupported source; late response; refusal/429/cap/outage; user opt-out.
9. **Unit and integration tests:** Unit: Strict proposal/adversarial/stale-version/budget tests. Integration: Provider failure/cap/disabled integration + manual/source/saved persistence unaffected.
10. **Browser testing:** Correct/skip clarification/save estimate; opt-out and timeout maintain draft/manual path.
11. **Android compatibility:** Installed flaky-network request/cancel/background-return and stale draft checks.
12. **Security/privacy:** O8 terms/retention/region approved; minimum purpose content, no prompt logs/media; server-only key; no write tools.
13. **Acceptance criteria:** [ ] T06/T26/T28 pass; AI cannot save facts/change policy/mark workout; kill switch and hard caps enforce fallback.
14. **Manual verification:** Submit cake ambiguity/injected phrase, correct draft before late response, disable provider and log manually.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record provider approval/consent/cap configuration and adversarial results.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-36"></a>

### 36 - Bounded summaries grounded in computed facts

1. **Part / status:** 36 - Bounded summaries grounded in computed facts; Intelligence M5; Not Started; [ ] complete.
2. **Scope and deliverables:** Add optional qualitative summaries of computed day/month/year/weekly facts. Numbers render deterministically; invalid/unsupported narrative rejected for factual template.
3. **Prerequisites:** 20, 21, 25, 35. Require their acceptance evidence, not only code.
4. **PDF pages:** 7, 12, 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 6.3, 7.3, 11.1. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/api/src/modules/{ai,insights}/; apps/api/src/providers/ai/; packages/contracts/src/providers.ts; packages/domain/src/aggregates/; apps/universal/src/features/{journal,overall}/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** SummaryProposal; supplied fact/evidence revision digest; coverage/policy/model version; staleness.
8. **Edge cases:** Extra numbers; unsupported cause/diagnosis; sparse evidence; old-entry edit; goal conflict; late response; provider cap.
9. **Unit and integration tests:** Unit: Fact-reference/unsupported-claim and stale-narrative tests. Integration: Revision invalidation, provider failure and deterministic fallback across client/server read models.
10. **Browser testing:** Numbers and current narrative consistent; stale prose hidden/flagged before refreshed facts.
11. **Android compatibility:** Installed correction/offline/fallback; same facts and staleness semantics.
12. **Security/privacy:** Minimum consented evidence; no whole journal by default or retained raw prompts.
13. **Acceptance criteria:** [ ] T05/T06/T26 pass; corrections invalidate narrative; unsupported claims never displayed; useful factual fallback.
14. **Manual verification:** Generate synthetic month, edit yesterday then deliver old response; inspect stale rejection and no-AI summary.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record supported narrative contract and model/provider version evidence.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-37"></a>

### 37 - Evidence-aware next action and reflection

1. **Part / status:** 37 - Evidence-aware next action and reflection; Intelligence M5; Not Started; [ ] complete.
2. **Scope and deliverables:** Add one conservative reviewed next step with Why this, Make it easier, Dismiss/tone and basic descriptive weekly reflection. Accepted actions call owning commands; no adaptive target/progression automation.
3. **Prerequisites:** 14, 32, 36. Require their acceptance evidence, not only code.
4. **PDF pages:** 2, 12-14, 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 3.1, 6.3, 7.3, 14.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/policy/; apps/universal/src/features/overall/; apps/api/src/modules/insights/; packages/contracts/src/records/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Recommendation/evidence revisions; approved rule priority; dismissal/acceptance; tone.
8. **Edge cases:** Partial Food no low-intake inference; duration-only no readiness; user-reported safety; disabled/paused; contradictory/sparse evidence.
9. **Unit and integration tests:** Unit: Reviewed priority/coverage/nonpunitive/dismissal fixtures. Integration: Stale evidence invalidation and accepted action through correct owned command.
10. **Browser testing:** One primary action, clear reason/easier/manual choice and persistent dismissal.
11. **Android compatibility:** Installed screen-reader action/explanation and offline factual behavior.
12. **Security/privacy:** O5 policy; no punitive restriction/repayment, diagnosis or automatic new health prescription.
13. **Acceptance criteria:** [ ] T04/T07/T27 pass; suggestion grounded in known evidence and user priority; sparse history yields clarification/control, not adaptation.
14. **Manual verification:** Run imperfect-week with gaps/disabled Workout/short sleep, inspect reasons, dismiss and correct evidence.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record reviewed rules, minimum evidence gates and historical recommendation staleness.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-38"></a>

### 38 - Accessibility audit and bounded fixes

1. **Part / status:** 38 - Accessibility audit and bounded fixes; Polish M6; Not Started; [ ] complete.
2. **Scope and deliverables:** Audit all MVP core/account/intelligence paths and fix concrete accessibility defects. Target WCAG 2.2 AA; no conformance claim from scans alone.
3. **Prerequisites:** 37. Require their acceptance evidence, not only code.
4. **PDF pages:** 4, 7, 13, 15, 19, 22 (physical pages).
5. **ARCHITECTURE sections:** 2.1-2.2, 9.2, 12.1-12.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/ui/; apps/universal/src/features/ (only defects named in approved audit plan); tests/web/accessibility.spec.ts; tests/manual/{accessibility.md,android-device.md} (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Labels/focus/agenda equivalents; hidden-number policy; touch/motion/reflow.
8. **Edge cases:** Keyboard traps/dialog restore; zoom/reflow; large text; screen-reader numbers hidden; color-only rings; reduced motion.
9. **Unit and integration tests:** Unit: Regression tests for each reproducible component defect. Integration: Automated accessibility scans plus navigation/labels/error association in exported app.
10. **Browser testing:** Actual keyboard/SR/Safari/mobile checks with versions and results.
11. **Android compatibility:** Physical TalkBack/large-text/back/touch checks; emulator automation complements.
12. **Security/privacy:** Numeric privacy and respectful optional celebration; no sensitive screenshot fixtures.
13. **Acceptance criteria:** [ ] T25 required automated/manual cases pass or remain blocking defects with evidence; equivalent chart meaning.
14. **Manual verification:** Complete Add/edit/finish/conflict/export flows by keyboard and screen reader with numeric hiding.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record actual assistive-tech/browser/device findings and fixes.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-39"></a>

### 39 - Security, privacy and policy hardening

1. **Part / status:** 39 - Security, privacy and policy hardening; Polish M6; Not Started; [ ] complete.
2. **Scope and deliverables:** Audit and fix MVP authorization, key/local-copy lifecycle, public artifact/log leaks, dependency/config/consent gaps and deletion/export safety. Finalize synthetic prototypes to approved policies.
3. **Prerequisites:** 31, 37, 38; O4-O8 applicable approvals. Require their acceptance evidence, not only code.
4. **PDF pages:** 13, 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 5, 7.3, 10, 11, 12. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/api/src/plugins/security.ts; apps/universal/src/adapters/{auth,vault}/; apps/universal/src/bootstrap/public-config.ts; apps/api/src/modules/privacy/; apps/api/src/jobs/{deletion,export}.ts; scripts/check-public-artifacts.mjs; tests/security/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Threat model; approved key/metadata/retention/provider policy; authorization/CSRF; telemetry schema.
8. **Edge cases:** Foreign parent/cursor/proof; XSS/injected text; key rotation/loss; logout pending; secret bundled; same-origin unlocked limitations.
9. **Unit and integration tests:** Unit: Negative authorization/schema/policy and per-defect regression tests. Integration: Real auth/PG/stores; vault failure; deletion proof/suppression and export isolation drills.
10. **Browser testing:** CSP/CSRF/origins, account switching and unlock/lock cache clearing.
11. **Android compatibility:** Physical native protected files/keys/backups/deep links, bundle inspection.
12. **Security/privacy:** O4/O6 policy approval, no invented certification/E2EE/remote-wipe; no logs with health bodies.
13. **Acceptance criteria:** [ ] T21/T23/T26/T29/T31 pass; unresolved privacy/security launch defects block release; policy provenance explicit.
14. **Manual verification:** Inspect redacted artifacts, lock/switch/revoke, foreign references and restored-deletion denial.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record threat findings/approved policy and actual audit evidence.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6 Astra / max; keep quality-critical choice, disclose unavailable options.

<a id="part-40"></a>

### 40 - Offline upgrades and measured performance

1. **Part / status:** 40 - Offline upgrades and measured performance; Polish M6; Not Started; [ ] complete.
2. **Scope and deliverables:** Harden crash/quota/migration/old-tab/offline recovery and optimize only measured bottlenecks. Record workload/device baseline and agreed budgets before judging performance.
3. **Prerequisites:** 26, 31, 39. Require their acceptance evidence, not only code.
4. **PDF pages:** 13, 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 5, 11.3, 12, 13.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/data/projections/; apps/universal/src/adapters/storage/; apps/universal/src/web/service-worker-registration.web.ts; tests/web/offline-upgrade.spec.ts; tests/android/harness/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Shell/store/protocol compatibility; bounded batches/queries; approved evidence-based budgets.
8. **Edge cases:** Long offline/expired replay; failed encrypted migration; eviction; dirty old/new tabs; large synthetic history; battery/lifecycle.
9. **Unit and integration tests:** Unit: Upgrade/recovery/invalidation regression properties. Integration: Real store/PG fault injection and reproducible load/latency/memory measurements.
10. **Browser testing:** Warmed-shell reload/update coordination, multi-tab upgrade and responsive synthetic large-history flow.
11. **Android compatibility:** Installed kill/relaunch/migration/slow-device profiling; no background dependency.
12. **Security/privacy:** No real health benchmarks or secret logs; preserve pending work; cache only public shell.
13. **Acceptance criteria:** [ ] T19/T24/T30 hold under faults; measured regressions fixed against recorded budget; no fabricated benchmark.
14. **Manual verification:** Run old/new-shell upgrade with queued data and editor, interrupt migration and recover/export safely.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record measured workload/budgets and repeatable performance/recovery commands.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-41"></a>

### 41 - Cross-platform MVP acceptance suite

1. **Part / status:** 41 - Cross-platform MVP acceptance suite; Polish M6; Not Started; [ ] complete.
2. **Scope and deliverables:** Integrate release-relevant automated/system/manual T01-T32 scenarios and synthetic imperfect-week walkthrough; prepare O9 observed T33 protocol. Fix bounded defects via approved amendment if scope grows.
3. **Prerequisites:** 38, 39, 40. Require their acceptance evidence, not only code.
4. **PDF pages:** 19, 22 (physical pages).
5. **ARCHITECTURE sections:** 12, 13.3, 14.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** tests/{fixtures,web,android,api,security,operations,manual}/; .github/workflows/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Release build/version; T01-T33 evidence matrix; deferred T34 promotion gate.
8. **Edge cases:** Lost ack; partial workout; old goal/edit; incomplete intake; AI disabled; disabled/paused; permission denial.
9. **Unit and integration tests:** Unit: All critical shared state/date/calculation tests. Integration: Real PG/both stores and two-client concurrency; ops restoration/outage suite.
10. **Browser testing:** Exported shell Chromium/Firefox/WebKit plus actual Safari/mobile manual evidence.
11. **Android compatibility:** Installed release-like emulator and physical device Maestro/manual evidence.
12. **Security/privacy:** Synthetic until real pilot approval; no fabricated T33 observation or premature Later T34 pass.
13. **Acceptance criteria:** [ ] T01-T32 relevant MVP evidence complete, failures blocking; T33 reserved for 43; T34 explicitly Later.
14. **Manual verification:** Execute seven PDF p.22 scenarios across website and installed Android with build/date/result records. Also preserve unresolved work after expired replay, export it through part 28, and verify pending/conflict labels and retained evidence before any old-store cleanup (T23/T29/T30).
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Publish actual acceptance matrix and remaining pilot prerequisites.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-42"></a>

### 42 - Owner-provisioned staging and operations

1. **Part / status:** 42 - Owner-provisioned staging and operations; Polish M6; Not Started; [ ] complete.
2. **Scope and deliverables:** Prepare and, only when part authorization covers it, deploy approved staging artifacts. Owner provisions accounts/secrets; test domain/email/restore/alerts/outage. No public pilot or production publication.
3. **Prerequisites:** 31, 41; O7 exact domain/vendors/region/operator/budget approval. Require their acceptance evidence, not only code.
4. **PDF pages:** 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 1.1, 10.1, 13.1-13.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** infra/{cloudflare,render}/; .github/workflows/deploy-staging.yml; apps/api/Dockerfile; apps/api/src/config.ts; apps/api/src/jobs/; tests/operations/; docs/SETUP.md; docs/ENV_GUIDE.md (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Same owned site/cookies; secret references; server-first migration/artifact compatibility; readiness/jobs/backups.
8. **Edge cases:** Migration rollout failure; stale client; email DNS/429; job process restart; unavailable secret; rollback compatibility.
9. **Unit and integration tests:** Unit: Deployment config/preflight and scrubbed alert tests. Integration: Staging synthetic migration/job/backup/restore/auth/email outage rehearsal.
10. **Browser testing:** HTTPS route fallback/cookies/CSP/static assets and uncached/cached behavior.
11. **Android compatibility:** Installed device reaches staging HTTPS/API and deep links.
12. **Security/privacy:** Distinct staging credentials/data; least privilege; current limits checked at provisioning; no cost/purchase assumption.
13. **Acceptance criteria:** [ ] Synthetic staging works under owned domain; rollback/migration/restore tested; operator responsibilities approved.
14. **Manual verification:** Owner follows setup and reproduces staging login/save/restore/readiness and redacted alerts.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record exact approved environment/services without secret values.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-43"></a>

### 43 - Approved adult imperfect-week pilot

1. **Part / status:** 43 - Approved adult imperfect-week pilot; Polish M6 pilot-gated; Not Started; [ ] complete.
2. **Scope and deliverables:** Use an explicitly approved restricted pilot deployment and observe several real weeks as owner protocol permits; collect minimal approved measures. No invented participant count/clinical outcome/benchmark.
3. **Prerequisites:** 14, 34, 37, 42; O4-O9 release/pilot approvals. Require their acceptance evidence, not only code.
4. **PDF pages:** 19, 22, 24 (physical pages).
5. **ARCHITECTURE sections:** 12.2, 13.3, 14.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** tests/manual/pilot.md; infra/{cloudflare,render}/ (restricted pilot access only); exact bounded defect files named in approved plan; docs/agent/HANDOFF.md (sanitized evidence links) (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Consent/recruitment/device protocol; observed activation/friction/trust/return/pressure; T33.
8. **Edge cases:** Food-only/sleep-only; beginner/two-day/shift worker/limited equipment; Bangla input; interruption/correction; perceived pressure.
9. **Unit and integration tests:** Unit: Existing regression suites plus targeted fixes supported by observed defects. Integration: Pilot operations/backup/deletion and outage evidence using authorized environments.
10. **Browser testing:** Observe first session and imperfect-week corrections without developer help.
11. **Android compatibility:** Physical Android compatibility observation where approved; website remains first release target.
12. **Security/privacy:** O9 consent/privacy/distribution review; protect research/health evidence outside Git; no telemetry bodies.
13. **Acceptance criteria:** [ ] T33 observed evidence meets owner-defined pilot criteria; full p.19 scope verified; reduced manual-only pilot labeled reduced scope.
14. **Manual verification:** Owner/researcher follows approved observation script and records anonymized outcome classes and blockers.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record dated pilot decisions/limitations and release recommendation without participant health logs.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-44"></a>

### 44 - Website publication and release handoff

1. **Part / status:** 44 - Website publication and release handoff; Polish M6 release-gated; Not Started; [ ] complete.
2. **Scope and deliverables:** Prepare concrete production promotion/rollback and publish website only under owner-approved release action; verify operation and hand off. No Android store release.
3. **Prerequisites:** 43; explicit owner production promotion approval. Require their acceptance evidence, not only code.
4. **PDF pages:** 18-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 13.2-13.3, 14.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** .github/workflows/deploy-production.yml; infra/{cloudflare,render}/; docs/SETUP.md (release/operator runbook); apps/universal/src/bootstrap/public-config.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Verified web/API artifacts; approved production schema/protocol; feature switches; recovery/rollback.
8. **Edge cases:** Old shell/native client; secret config; migration readiness; DNS/email; rollback after additive changes; provider switch.
9. **Unit and integration tests:** Unit: Existing required suite/artifact/preflight checks for exact release. Integration: Production smoke limited to approved synthetic account; backup/readiness/job/alerts evidence.
10. **Browser testing:** Published route/HTTPS/login/local save/sync/manual AI-off fallback and safe cache behavior.
11. **Android compatibility:** Installed compatibility regression against production API, no distribution.
12. **Security/privacy:** O4-O9 closed; no real-data deployment past gates; no destructive schema downgrade or unapproved purchase.
13. **Acceptance criteria:** [ ] Verified website live at recorded approved URL/build; actual smoke and operator handoff complete; release proof truthful.
14. **Manual verification:** Owner-approved smoke, monitoring and rollback checks; inspect release URL/version and privacy controls.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record deployment URL/build/date/results, operator runbook and next approved action.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-45"></a>

### 45 - Optional Health Connect product integration

1. **Part / status:** 45 - Optional Health Connect product integration; Later Android optional; Not Started; [ ] complete.
2. **Scope and deliverables:** Plan and implement a bounded read-only sleep integration after promotion, with revocation/source-update/delete handling. This is optional and never a prerequisite for Android manual release.
3. **Prerequisites:** 44, 0M; explicit scope promotion and content/permission/privacy review. Require their acceptance evidence, not only code.
4. **PDF pages:** 11, 13, 17, 20, 24 (physical pages).
5. **ARCHITECTURE sections:** 2.3, 9.1, 10.3, 13.3, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/adapters/health/; packages/domain/src/sleep/; apps/universal/src/features/sleep/; packages/contracts/src/records/; tests/android/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Provider/connection/source identity+revision; correction overlay; reconciliation; capability/consent/deletion.
8. **Edge cases:** Denied/revoked/unsupported; repeated/update/delete imports; manual correction; overlapping sources; permission scope.
9. **Unit and integration tests:** Unit: Source identity/revision/overlay and permission-state tests. Integration: Installed native service + local/PG idempotent import, reconciliation/deletion integration.
10. **Browser testing:** Web unsupported retains manual Sleep; no new wearable requirement.
11. **Android compatibility:** Supported physical devices; permissions/revocation and source edits tested.
12. **Security/privacy:** Minimum read permissions; explicit consent/retention/rights; no sensitive import logs.
13. **Acceptance criteria:** [ ] T34 promotion and imported T12/T23/T32 pass; no duplicate totals or overwritten manual correction.
14. **Manual verification:** Authorize/deny/revoke, reread updated/deleted source and resolve overlap with manual entry.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record approval/permission/device matrix and source correction lessons.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-46"></a>

### 46 - Native Android product hardening

1. **Part / status:** 46 - Native Android product hardening; Later Android release preparation; Not Started; [ ] complete.
2. **Scope and deliverables:** Harden installed release-like manual Android app for lifecycle, battery/network, navigation/accessibility, permissions and upgrade behavior. Optional 45 included only if separately approved.
3. **Prerequisites:** 44; updated SDK/device/plugin release matrix. Require their acceptance evidence, not only code.
4. **PDF pages:** 4, 13, 17-19, 22 (physical pages).
5. **ARCHITECTURE sections:** 2.3, 10, 12, 13.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/app.config.ts; apps/universal/src/adapters/; apps/universal/src/ui/ (named defects only); tests/android/; tests/manual/android-device.md (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Production native modules/schema/protocol; protected files/session; lifecycle/capabilities.
8. **Edge cases:** Low memory/background kill; secure key invalidation; upgraded DB; offline expiry; split screen; denied optional permissions.
9. **Unit and integration tests:** Unit: Native boundary/lifecycle/error regression tests. Integration: Release-like build + real protected SQLite/auth/sync/upgrade flows.
10. **Browser testing:** Web regression for shared changes and native import isolation.
11. **Android compatibility:** Representative supported physical devices/OS floor, TalkBack/back/keyboard/battery and release-like Maestro.
12. **Security/privacy:** No debug harness/provider secrets in binary; signing credentials externally held.
13. **Acceptance criteria:** [ ] T32 release evidence plus required MVP regressions complete; native module/schema compatibility recorded.
14. **Manual verification:** Install upgrade over prior test build with pending data, expire network/auth and exercise all manual modules.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record current native support and actual product-hardening evidence.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-47"></a>

### 47 - Android signed release preparation

1. **Part / status:** 47 - Android signed release preparation; Later Android release preparation; Not Started; [ ] complete.
2. **Scope and deliverables:** Produce approved signed release candidate and concrete distribution checklist/rollback/support handoff. Upload/publication requires its own explicit release authorization; no store account/key generated by agent.
3. **Prerequisites:** 46; owner signing/distribution/privacy approval. Require their acceptance evidence, not only code.
4. **PDF pages:** 18-22, 24 (physical pages).
5. **ARCHITECTURE sections:** 10.1, 13.3, 14.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/app.config.ts; .github/workflows/android-smoke.yml (signed-candidate job only); docs/SETUP.md (release runbook); tests/android/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** App ID/version/native runtime/schema; externally held signing key; distribution policy.
8. **Edge cases:** Signing mismatch; incompatible OTA/native module; downgrade schema; offline old device; missing privacy declaration.
9. **Unit and integration tests:** Unit: Release config/public-artifact and compatibility tests. Integration: Exact signed candidate install/upgrade/smoke, integrity/version and pending migration checks.
10. **Browser testing:** Website regression/build remains valid.
11. **Android compatibility:** Physical signed candidate, release permissions, unlock/offline auth/deep links and update tests.
12. **Security/privacy:** Owner secret/signing storage; accurate platform disclosures; no debug fixture/harness or false store publication.
13. **Acceptance criteria:** [ ] Reviewable signed candidate/checklist and actual install evidence; distribution approval clearly recorded separately.
14. **Manual verification:** Owner installs signed candidate, checks manifest/version/privacy controls and rehearses supported update path.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record candidate build/provenance/verification and exact optional publish next action.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-48"></a>

### 48 - Recipe yields and personal portions

1. **Part / status:** 48 - Recipe yields and personal portions; Later enhancement; Not Started; [ ] complete.
2. **Scope and deliverables:** Add bounded batch/yield/serving and measured personal-bowl workflow after food-entry friction evidence; preserve prior meal snapshots.
3. **Prerequisites:** 34, 44; explicit promotion/content approval. Require their acceptance evidence, not only code.
4. **PDF pages:** 6, 13, 20 (physical pages).
5. **ARCHITECTURE sections:** 4.2, 4.4, 7.1, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/food/; apps/universal/src/features/food/; packages/contracts/src/records/; apps/universal/src/data/repositories/food-journal.ts; apps/api/src/modules/food/; apps/api/src/database/schema/food.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** RecipeVersion; ingredients/finished yield; measured grams-per-container; snapshot references.
8. **Edge cases:** Cooking yield unknown; remaining portion; bowl mass unmeasured; recipe revision; total override.
9. **Unit and integration tests:** Unit: Yield/portion/missingness and old-snapshot fixtures. Integration: Both stores/server command version migration and repeat/copy parity.
10. **Browser testing:** Batch/edit/version/portion confirmation and offline manual fallback.
11. **Android compatibility:** Installed decimal/input/local recipe flows.
12. **Security/privacy:** Licensed inputs; never exact photo density or auto-update old meals.
13. **Acceptance criteria:** [ ] T34 gate plus yield arithmetic/snapshot evidence; unknown grams stays unknown.
14. **Manual verification:** Create synthetic batch, measure serving, revise recipe and compare old logged bowl.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record measured friction, promotion and recipe version compatibility.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-49"></a>

### 49 - Busy-day capacity proposal

1. **Part / status:** 49 - Busy-day capacity proposal; Later enhancement; Not Started; [ ] complete.
2. **Scope and deliverables:** Add one bounded shorter-session proposal with visible preserved/omitted scope; no actual work logged until accepted/completed.
3. **Prerequisites:** 32, 44; explicit promotion/review. Require their acceptance evidence, not only code.
4. **PDF pages:** 3, 10, 13, 20 (physical pages).
5. **ARCHITECTURE sections:** 8, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/policy/; apps/universal/src/features/workout/; packages/contracts/src/providers.ts; tests/fixtures/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Time/capacity constraint; reviewed template; original/current session snapshots.
8. **Edge cases:** No feasible safe fit; active/closed session; duration uncertainty; no equipment; declined proposal.
9. **Unit and integration tests:** Unit: Constraint/preserved-scope/reviewed-limit fixtures. Integration: Explicit proposal acceptance/current-session command with original denominator intact.
10. **Browser testing:** Preview simulation versus real acceptance clearly separated.
11. **Android compatibility:** Installed proposal acceptance/offline/manual path.
12. **Security/privacy:** Reviewer bounds; no pressure/intensity escalation or automatic completion.
13. **Acceptance criteria:** [ ] T34/T10 gate: proposal feasible under reviewed constraints; declining changes nothing.
14. **Manual verification:** Try 15-minute synthetic limit, decline then accept and compare original/current scope.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record observed schedule friction and validated proposal limits.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-50"></a>

### 50 - Equipment substitution proposals

1. **Part / status:** 50 - Equipment substitution proposals; Later enhancement; Not Started; [ ] complete.
2. **Scope and deliverables:** Add vetted alternatives for unavailable equipment with explicit accept/today/future choice and honest no-fit.
3. **Prerequisites:** 32, 44; explicit catalog/reviewer promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 8, 10, 13, 20 (physical pages).
5. **ARCHITECTURE sections:** 3.1, 8, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/{catalog,policy}/; apps/universal/src/features/{equipment,workout}/; tests/fixtures/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Reviewed movement/equipment/limit mapping; distinct comparable history conventions.
8. **Edge cases:** Busy machine; excluded movement; assisted/bodyweight convention change; no valid alternative.
9. **Unit and integration tests:** Unit: Reviewed mapping and hard-constraint tests. Integration: Accepted substitution version/snapshot and actual comparison-series integration.
10. **Browser testing:** Alternative reason/decline and original-plan disclosure.
11. **Android compatibility:** Installed selector/state restore and equipment profiles.
12. **Security/privacy:** No unreviewed exercise, pain treatment or false comparable-volume series.
13. **Acceptance criteria:** [ ] T34 gate; all proposed alternatives satisfy approved constraints; no silent history rewrite.
14. **Manual verification:** Mark equipment unavailable, exclude a movement, review no-fit and accepted replacement.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record mapping/content rights/review and comparison rules.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-51"></a>

### 51 - Reviewed progression proposal evaluation

1. **Part / status:** 51 - Reviewed progression proposal evaluation; Later enhancement/research; Not Started; [ ] complete.
2. **Scope and deliverables:** Evaluate one conservative progression rule against fixed-history/manual baseline; implement proposal-only UI only after evidence approval. No automatic load/routine changes.
3. **Prerequisites:** 37, 43; sufficient comparable history and O5 promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 8-9, 14, 20 (physical pages).
5. **ARCHITECTURE sections:** 8, 14.2-14.3. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/policy/; tests/fixtures/; apps/universal/src/features/workout/ (only after approved evaluation scope) (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Comparable performed actuals; optional effort observations; reviewed proposal bounds.
8. **Edge cases:** Sparse/incompatible load history; pain/illness; missed week; RPE missing; regression.
9. **Unit and integration tests:** Unit: Reviewer cases and no-action/uncertainty fixtures. Integration: Replay real-store synthetic histories and accepted-versus-declined proposal command tests.
10. **Browser testing:** Proposal explains evidence and manual choice if promoted.
11. **Android compatibility:** Installed measurement/history parity and proposal UI if promoted.
12. **Security/privacy:** No unsafe prescriptions; reviewed supported population and thresholds; evaluation uses synthetic/anonymized approved evidence.
13. **Acceptance criteria:** [ ] T34 baseline/evidence gate met or documented no-go; no adaptive automation without new approved plan.
14. **Manual verification:** Compare proposed action with manual baseline for sparse/pain/mixed-equipment cases.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record reviewer/baseline outcomes and explicit go/no-go.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-52"></a>

### 52 - Adaptive target and plateau evaluation

1. **Part / status:** 52 - Adaptive target and plateau evaluation; Later enhancement/research; Not Started; [ ] complete.
2. **Scope and deliverables:** Evaluate one bounded adaptive-target/plateau proposal against conservative baseline; retain non-actioning mode until reviewer/owner approval.
3. **Prerequisites:** 14, 37, 43; sufficient complete comparable history and O5 promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 5, 14, 20 (physical pages).
5. **ARCHITECTURE sections:** 6.2-6.3, 7.3, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/{policy,goals}/; tests/fixtures/; apps/universal/src/features/goals/ (only after promotion) (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Complete/known intake; comparable measurements; reviewed evidence window; future target version.
8. **Edge cases:** Incomplete intake; sparse weight; short window; travel; unsupported conditions; existing historical binding.
9. **Unit and integration tests:** Unit: History-quality/no-action/uncertainty and immutable-target fixtures. Integration: Synthetic recorded-history replay and explicitly accepted future activation tests.
10. **Browser testing:** Explain enough/insufficient evidence; manual target retained.
11. **Android compatibility:** Installed date/unit/history and no-auto-activation checks.
12. **Security/privacy:** No universal thresholds or precise forecast; O5 review; privacy-approved evidence only.
13. **Acceptance criteria:** [ ] T34 gate; adaptation abstains on poor evidence, never rewrites past/current-day targets.
14. **Manual verification:** Replay sparse versus sufficient reviewed histories; decline proposal and inspect unchanged timeline.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record evidence threshold/baseline/reviewer decision and future-only contract.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-53"></a>

### 53 - Barcode food lookup

1. **Part / status:** 53 - Barcode food lookup; Later enhancement; Not Started; [ ] complete.
2. **Scope and deliverables:** Add bounded barcode-to-licensed-source proposal with manual entry fallback; no new inferred nutrient facts.
3. **Prerequisites:** 33, 34, 44; explicit provider/license/permission promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 6, 20 (physical pages).
5. **ARCHITECTURE sections:** 7.2-7.3, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/adapters/runtime/ (scanner port selected in promoted plan); apps/universal/src/features/food/; apps/api/src/providers/food/; packages/contracts/src/providers.ts (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Barcode/source match; reviewed product DB; camera capability; confirmation.
8. **Edge cases:** Unknown product; wrong country/version; denied camera; unavailable web capability; ambiguous serving.
9. **Unit and integration tests:** Unit: Barcode/lookup/source normalization fixtures. Integration: Provider fixture/permission/cached-manual confirmation integration.
10. **Browser testing:** Browser supported/unsupported scanner and keyboard manual path.
11. **Android compatibility:** Actual scanner/native plugin builds and denied/revoked permission.
12. **Security/privacy:** O8 content rights; minimal permission/media retention; no captured-frame logs.
13. **Acceptance criteria:** [ ] T34 gate; scanned food still reviewed/confirmed; unknown/permission failure never blocks manual logging.
14. **Manual verification:** Scan approved synthetic test barcode, deny permission and confirm source/serving manually.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record supported devices/provider rights and product-match quality.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-54"></a>

### 54 - Photo food proposal evaluation

1. **Part / status:** 54 - Photo food proposal evaluation; Later enhancement/research; Not Started; [ ] complete.
2. **Scope and deliverables:** Benchmark a bounded photo proposal experiment; product integration only after measured quality/cost/privacy approval. No exact grams from photo.
3. **Prerequisites:** 35, 44; explicit media/privacy/quality promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 6, 16, 20 (physical pages).
5. **ARCHITECTURE sections:** 7.3, 10, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/api/src/providers/ai/; apps/universal/src/features/food/; apps/universal/src/adapters/runtime/ (approved media seam); tests/fixtures/regional-food/ (licensed synthetic image evaluation only) (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Consented photo proposal; uncertainty/source candidates; editable quantity; retention policy.
8. **Edge cases:** Occlusion/mixed dishes/oil; no scale; unknown source; denied camera; late corrected draft.
9. **Unit and integration tests:** Unit: Proposal/source/uncertainty and stale-version tests. Integration: Licensed-image benchmark/provider failure + manual confirmation pipeline.
10. **Browser testing:** Upload/cancel/delete and unsupported/manual path if promoted.
11. **Android compatibility:** Actual camera capability, permission and lifecycle tests if promoted.
12. **Security/privacy:** Explicit media consent/retention; no real-photo fixtures/raw logs; O8 provider terms.
13. **Acceptance criteria:** [ ] T34 benchmark gate or explicit no-go; source/portion uncertainty visible and manual fallback intact.
14. **Manual verification:** Review ambiguous dish image, correct portion, delete media and compare factual saved result.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record licensed benchmark/quality/cost/retention and go/no-go.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-55"></a>

### 55 - Voice food input evaluation

1. **Part / status:** 55 - Voice food input evaluation; Later enhancement/research; Not Started; [ ] complete.
2. **Scope and deliverables:** Evaluate bounded speech-to-editable-food-text input before product promotion; reuse confirmed parsing pipeline.
3. **Prerequisites:** 34, 35, 44; explicit audio/language/privacy promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 6, 16, 20 (physical pages).
5. **ARCHITECTURE sections:** 7.3, 10, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/adapters/runtime/ (approved audio port); apps/universal/src/features/food/; apps/api/src/providers/ai/; tests/fixtures/regional-food/ (licensed synthetic audio only) (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Transcript proposal; Bangla-English language/error benchmark; editable draft.
8. **Edge cases:** Bangla-English code switching; noise; quantity misheard; denied mic; interruption; transcript corrections.
9. **Unit and integration tests:** Unit: Transcript/quantity/no-autosave and stale-draft fixtures. Integration: Licensed synthetic audio benchmark plus provider timeout/cancel/manual fallback.
10. **Browser testing:** Mic supported/unsupported/manual typed path if promoted.
11. **Android compatibility:** Physical mic/permission/audio focus/lifecycle tests if promoted.
12. **Security/privacy:** Explicit audio retention/consent; no real audio logs or always-on recording.
13. **Acceptance criteria:** [ ] T34 quality/privacy gate or no-go; transcript confirmed before food proposal/save.
14. **Manual verification:** Read synthetic mixed-language example, correct quantity, deny microphone and type same entry.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record language/error/latency/cost and approval outcome.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-56"></a>

### 56 - Nutrition-label OCR evaluation

1. **Part / status:** 56 - Nutrition-label OCR evaluation; Later enhancement/research; Not Started; [ ] complete.
2. **Scope and deliverables:** Benchmark bounded label OCR into editable source/basis proposal; no unconfirmed label automatically becomes fact.
3. **Prerequisites:** 33, 44; explicit label/media/license promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 6, 20 (physical pages).
5. **ARCHITECTURE sections:** 7.1-7.3, 10, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/adapters/runtime/ (approved OCR/media port); apps/universal/src/features/food/; packages/domain/src/food/; tests/fixtures/regional-food/ (licensed label corpus) (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Label nutrient registry; serving/per-100g basis; OCR proposal uncertainty.
8. **Edge cases:** Decimal/unit errors; per-serving/per-package; energy units; missing protein; glare/language.
9. **Unit and integration tests:** Unit: Nutrient mapping/basis/unknown OCR fixtures. Integration: Licensed-label accuracy/error benchmark and deterministic quantity confirmation.
10. **Browser testing:** Upload/review/correct/manual path if promoted.
11. **Android compatibility:** Camera/file capability/permission and numeric input parity if promoted.
12. **Security/privacy:** Media consent/retention, source rights, no raw private label-photo logs.
13. **Acceptance criteria:** [ ] T34 gate or no-go; every saved nutrient tied to confirmed explicit source/basis.
14. **Manual verification:** Use synthetic glare/serving label, correct OCR unit and inspect deterministic total.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record OCR benchmark/rights and source confidence limits.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-57"></a>

### 57 - Optional scheduled reminders

1. **Part / status:** 57 - Optional scheduled reminders; Later enhancement; Not Started; [ ] complete.
2. **Scope and deliverables:** Add bounded user-selected reminder schedule and opt-out; no background work needed for saving/sync correctness.
3. **Prerequisites:** 43; explicit O2 promotion/permission/tone policy. Require their acceptance evidence, not only code.
4. **PDF pages:** 4, 13, 15, 20 (physical pages).
5. **ARCHITECTURE sections:** 2.3, 6.2, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/features/preferences/; apps/universal/src/adapters/runtime/ (approved notification port); tests/android/; packages/contracts/src/records/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Quiet-time/time-zone preferences; module effective periods; optional delivery capability.
8. **Edge cases:** Denied permission; disabled/paused; travel/DST; stale schedule; duplicates; missed delivery.
9. **Unit and integration tests:** Unit: Schedule/quiet-time/eligibility and no-nag tests. Integration: Permission/reinstall/update/cancel across actual supported runtime.
10. **Browser testing:** Supported web capability only; in-app/manual fallback and never promised delivery.
11. **Android compatibility:** Installed notification permission/lifecycle/delivery checks across approved devices.
12. **Security/privacy:** No sensitive lock-screen health content by default; consent and provider terms.
13. **Acceptance criteria:** [ ] T34 promotion; reminders obey preferences/pause and can be disabled; delivery limits honest.
14. **Manual verification:** Set reminder, pause module, change zone, deny permission and inspect canceled/no-nag state.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record supported delivery limits/permission and review decision.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-58"></a>

### 58 - Private engagement prototype evaluation

1. **Part / status:** 58 - Private engagement prototype evaluation; Later research; Not Started; [ ] complete.
2. **Scope and deliverables:** Evaluate one bounded engagement concept per approved plan against simple history. Select separate follow-up parts for additional concepts; no large gamification platform.
3. **Prerequisites:** 43; explicit behavioral/pressure evaluation promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 3, 15, 20-21 (physical pages).
5. **ARCHITECTURE sections:** 2.2, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** apps/universal/src/features/overall/ (isolated chosen prototype only); apps/universal/src/features/preferences/; tests/manual/pilot.md (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** One chosen mosaic/comeback/discovery/living-atlas concept; explicit consent/tone; no health score.
8. **Edge cases:** Missed week; rest; reduced motion; hidden metrics; perceived compulsion; unwanted celebration.
9. **Unit and integration tests:** Unit: No extreme-intake/intensity reward and motion/opt-out component tests. Integration: Prototype state cannot mutate real log/targets; history/correction integrity.
10. **Browser testing:** Accessible opt-out/reduced motion and nonpunitive gaps.
11. **Android compatibility:** Installed animation/large-text/TalkBack/low-device-cost check if prototype targeted.
12. **Security/privacy:** Measure pressure/control, not compulsive time; research consent and minimal evidence.
13. **Acceptance criteria:** [ ] T34 evaluation yields go/no-go; no penalties/extreme rewards; core log unaffected.
14. **Manual verification:** Compare interrupted-week simple history with chosen prototype and collect approved pressure feedback.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record chosen concept/evaluation protocol and honest go/no-go.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / xhigh; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-59"></a>

### 59 - One opt-in broader context input

1. **Part / status:** 59 - One opt-in broader context input; Later enhancement; Not Started; [ ] complete.
2. **Scope and deliverables:** Introduce only one evidence-backed optional input per plan; future fields require their own approval. No medical diagnosis or expanding required onboarding.
3. **Prerequisites:** 43; explicit purpose/privacy/benefit promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 11, 13, 20 (physical pages).
5. **ARCHITECTURE sections:** 3.1, 9.1, 10, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/sleep/ or packages/domain/src/journal/ (one chosen observation); apps/universal/src/features/preferences/; packages/contracts/src/records/; apps/api/src/database/schema/sleep-journal.ts; exact owning feature selected in promoted plan (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** One selected readiness/stress/energy/steps/hydration/cycle/body input; observation/source identity.
8. **Edge cases:** Declined/withdrawn; missing/partial; sensitive input; source duplicates; stale correlation.
9. **Unit and integration tests:** Unit: Observation/missingness/opt-out/no-required-field tests. Integration: Owned encrypted persistence/migration/export/delete and eligibility integration.
10. **Browser testing:** Optional control, explanation and omission without blocked logging.
11. **Android compatibility:** Installed input/accessibility/offline behavior.
12. **Security/privacy:** Purpose-specific consent/data minimization; no causal medical conclusion.
13. **Acceptance criteria:** [ ] T34 benefit/review gate; optional input works/export/delete and never compulsory.
14. **Manual verification:** Decline/enable/log/remove the chosen field and verify core save plus retained policy choice.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record chosen field/purpose/retention and evidence of benefit.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-60"></a>

### 60 - On-device personal food memory evaluation

1. **Part / status:** 60 - On-device personal food memory evaluation; Later research; Not Started; [ ] complete.
2. **Scope and deliverables:** Benchmark one private on-device retrieval/inference approach against saved/cached search. No model deployment or autonomous personal learning absent follow-up approval.
3. **Prerequisites:** 34, 43; explicit device/privacy/ML promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 16-17, 21, 24 (physical pages).
5. **ARCHITECTURE sections:** 7, 13.3, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** tests/android/harness/ (isolated on-device experiment); tests/fixtures/regional-food/; packages/domain/src/food/ (retrieval seam only) (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Explicit Remember versions; cached-search baseline; local model/device resource metrics.
8. **Edge cases:** Low-end device; Bangla variation; forgotten correction; opt-out/delete; stale food version; battery/memory.
9. **Unit and integration tests:** Unit: Version/consent/delete and bounded proposal tests. Integration: Reproducible accuracy/latency/resource benchmark plus cache fallback.
10. **Browser testing:** Web unsupported/cached baseline; no forced native ML dependency.
11. **Android compatibility:** Installed target devices and real resource measurement; plugin compatibility.
12. **Security/privacy:** No real personal training corpus or external upload; approved rights/consent and deletion.
13. **Acceptance criteria:** [ ] T34 baseline advantage gate or no-go; correction explicit, manual offline route unchanged.
14. **Manual verification:** Run synthetic saved-meal benchmark, remove remembered entry and inspect retrieval/resource report.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record baseline/measurements/device constraints and go/no-go.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-61"></a>

### 61 - Feasible-future simulator evaluation

1. **Part / status:** 61 - Feasible-future simulator evaluation; Later research; Not Started; [ ] complete.
2. **Scope and deliverables:** Evaluate one non-actioning schedule simulator against simple rule/manual baseline. Body-outcome forecasts need separate validated review; no automatic real-plan mutation.
3. **Prerequisites:** 49, 51, 52; explicit forecast/non-actioning review. Require their acceptance evidence, not only code.
4. **PDF pages:** 3, 17, 21 (physical pages).
5. **ARCHITECTURE sections:** 6, 8, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/domain/src/scheduling/ (isolated non-actioning prototype); apps/universal/src/features/scheduling/ (simulation only); tests/fixtures/ (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Time/equipment/hard constraint model; original schedule; uncertain forecast; baseline.
8. **Edge cases:** Infeasible constraints; skipped activity; sparse evidence; uncertain trajectory; simulated versus real save.
9. **Unit and integration tests:** Unit: Constraint/feasibility/no-mutation property tests. Integration: Synthetic scenario replay/baseline/uncertainty validation.
10. **Browser testing:** Simulation labeled; accept only via existing command after explicit review if promoted.
11. **Android compatibility:** Installed graph/input/resource and web/native parity if targeted.
12. **Security/privacy:** No guaranteed body outcome or unsafe optimization; approved research evidence only.
13. **Acceptance criteria:** [ ] T34 validated constraint/baseline gate or no-go; simulation cannot log activity or rewrite history.
14. **Manual verification:** Drag synthetic busy week, observe infeasibility and compare real schedule remains unchanged.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record solver/baseline/uncertainty and explicit investment decision.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-62"></a>

### 62 - Personal experiment protocol evaluation

1. **Part / status:** 62 - Personal experiment protocol evaluation; Later research; Not Started; [ ] complete.
2. **Scope and deliverables:** Evaluate one optional safe habit experiment workflow; no unsafe restriction experiment or automatic treatment/causal claims.
3. **Prerequisites:** 43, 59; explicit reviewer/research promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 14, 21 (physical pages).
5. **ARCHITECTURE sections:** 6.3, 7.3, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** tests/manual/pilot.md (approved experiment protocol); packages/domain/src/policy/ (synthetic evidence evaluation only); apps/universal/src/features/overall/ only after prototype approval (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Chosen modest habit/outcome/confounder; observation coverage; noncausal reflection.
8. **Edge cases:** Sparse/biased reporting; overlapping habit changes; opt-out; illness; incomplete outcome.
9. **Unit and integration tests:** Unit: Coverage/uncertainty/withdrawal/no-causal-template fixtures. Integration: Synthetic experiment replay plus approved minimal observation protocol.
10. **Browser testing:** Explicit consent/exit and known/unknown outcome reflection if prototyped.
11. **Android compatibility:** Installed opt-in/offline/accessibility flow if targeted.
12. **Security/privacy:** Qualified review/research consent; data minimization; no clinical-effectiveness claim.
13. **Acceptance criteria:** [ ] T34 safe protocol/evidence gate or no-go; uncertainty/withdrawal clear and no unsafe goal changes.
14. **Manual verification:** Review wind-down-type synthetic experiment with missing/confounded observations and exit.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record approved protocol/confounders and go/no-go.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / high; keep quality-critical choice, disclose unavailable options.

<a id="part-63"></a>

### 63 - Camera-assisted training-note evaluation

1. **Part / status:** 63 - Camera-assisted training-note evaluation; Later research; Not Started; [ ] complete.
2. **Scope and deliverables:** Benchmark one exercise/counting setup for optional notes against manual logging. No certification of safe technique, pain diagnosis or automatic completed sets.
3. **Prerequisites:** 51, 46; explicit exercise-specific/privacy promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 21 (physical pages).
5. **ARCHITECTURE sections:** 8, 10, 13.3, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** tests/android/harness/ (isolated camera-note evaluation); tests/fixtures/ (licensed synthetic clips); apps/universal/src/adapters/runtime/ (approved camera test seam) (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Supported exercise/camera position; optional count proposal; correction; no performed-set command.
8. **Edge cases:** Occlusion/position/body diversity; wrong exercise; denied camera; battery/resource; false reps.
9. **Unit and integration tests:** Unit: Proposal/no-completion/uncertainty fixtures. Integration: Licensed exercise-specific benchmark and manual correction/fallback.
10. **Browser testing:** Web manual unsupported path; no camera requirement.
11. **Android compatibility:** Actual target device/camera permission/resource measurements.
12. **Security/privacy:** No real video retained by default; consent/rights/deletion; no health claim.
13. **Acceptance criteria:** [ ] T34 exercise-specific validation or no-go; proposed notes cannot fabricate performed work.
14. **Manual verification:** Run synthetic supported/occluded clips, correct count and verify set remains unchecked.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record benchmark/device/privacy and go/no-go.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / max; keep quality-critical choice, disclose unavailable options.

<a id="part-64"></a>

### 64 - Household recipe-sharing feasibility

1. **Part / status:** 64 - Household recipe-sharing feasibility; Later research; Not Started; [ ] complete.
2. **Scope and deliverables:** Evaluate only recipe sharing/portion-accounting boundary and demand, preserving each account journal privacy; implement product only under a later approved plan.
3. **Prerequisites:** 48, 43; explicit demand/sharing/privacy promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 21 (physical pages).
5. **ARCHITECTURE sections:** 4, 10, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** packages/contracts/src/privacy.ts (proposed sharing boundary only); tests/security/; tests/api/ownership.test.ts; apps/api/src/modules/privacy/ only for approved isolated authorization prototype (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Shared recipe batch versus private journals; portions; explicit invite/revoke roles.
8. **Edge cases:** Revoked invite; guessed ID; different targets; double allocation; owner deletion; recipe revision.
9. **Unit and integration tests:** Unit: Role/portion/revocation/foreign-reference tests. Integration: Isolated real PG authorization prototype if approved; no production collaboration.
10. **Browser testing:** Invite/revoke/private-history separation prototype.
11. **Android compatibility:** Native shared recipe/private-log parity if targeted.
12. **Security/privacy:** No inferred household consent; no health-history sharing by default; reviewed access/deletion policy.
13. **Acceptance criteria:** [ ] T34 demand/authorization gate or no-go; private journal inaccessible to recipe collaborators.
14. **Manual verification:** Use two synthetic accounts, share recipe only, revoke and attempt foreign history read.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record sharing threat/demand evidence and scope go/no-go.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

<a id="part-65"></a>

### 65 - Regional budget-aware food proposal evaluation

1. **Part / status:** 65 - Regional budget-aware food proposal evaluation; Later enhancement/research; Not Started; [ ] complete.
2. **Scope and deliverables:** Evaluate one bounded affordable-meal proposal set using real permitted price provenance, with manual comparison. No invented prices or exact personalized nutrition claims.
3. **Prerequisites:** 34, 43; explicit price/source/reviewer promotion. Require their acceptance evidence, not only code.
4. **PDF pages:** 6, 16, 20 (physical pages).
5. **ARCHITECTURE sections:** 7.2-7.3, 14.2. Preserve relevant R/D/T mapping below and in the concrete plan.
6. **Expected file/directory changes:** tests/fixtures/regional-food/; apps/api/src/providers/food/; packages/domain/src/policy/; apps/universal/src/features/food/ (approved proposal prototype only) (Expected change locations; absent targets are PLANNED, existing documents/configs are updated within the approved plan).
7. **Interfaces/data-model dependencies:** Licensed local foods; user/sourced dated prices; dietary preferences; uncertainty.
8. **Edge cases:** Prices stale/unavailable; regional availability; unknown portion/oil; excluded food; inadequate nutrient coverage.
9. **Unit and integration tests:** Unit: Price provenance/staleness/constraint and unknown fixtures. Integration: Reproducible reviewed proposal benchmark/source fallback.
10. **Browser testing:** Show dated price/source/assumptions and decline/correct controls if promoted.
11. **Android compatibility:** Installed Bangla/input/price unit rendering and offline cache.
12. **Security/privacy:** O8 price/content rights; O5 nutrition review; minimal preferences; no private food logs in benchmark.
13. **Acceptance criteria:** [ ] T34 regional/pricing evidence gate or no-go; unsupported cost/nutrient precision never shown.
14. **Manual verification:** Compare source-dated synthetic permitted prices, expire them and verify honest no-price/manual fallback.
15. **Documentation updates:** task.md status/evidence, HANDOFF commands/results/next action, relevant MEMORY, STRUCTURE actual creation labels, and test-command runnable/expected/observed section; Record rights/date/region/price quality and explicit promotion outcome.
16. **Completion definition:** [ ] Approved scope delivered; all required acceptance, automated/static/build and specified manual/platform checks evidenced; docs updated; unresolved required checks keep part unfinished; report and stop before next part.
17. **Recommended PLAN model / effort:** GPT-6 Astra / max; VS Code picker availability is authoritative.
18. **Recommended IMPLEMENT model / effort:** GPT-6.1 Sol / xhigh; keep quality-critical choice, disclose unavailable options.

## Preserved requirement and acceptance traceability

These groups retain the full ANALYSIS inventory without promoting deferred features. Concrete plans name the applicable R/D/T IDs and exact scenarios. Architecture §12.2 remains the acceptance authority; this table supplies execution owners.

| Requirements / decisions | Parts and scope |
| --- | --- |
| R01-R04 / D1,D3,D10,D11 | 0E/0N, 1, 21, 37, 43; R04 engagement/simulation is Later 49/58/61. |
| R05-R10 / D3,D5-D8,D11 | 1, 13-15, 22/27, 38; universal Add/Weight/Note and module independence explicitly in 1. |
| R11-R16 / D8,D10 | 13-16, 14 O5-reviewed estimate/goal discussion; advanced prediction/adaptive targets Later 52/61. |
| R17-R25 / D5,D8-D10 | 2-4, 16, 33-35; recipes/portions Later 48; barcode/photo/voice/OCR Later 53-56; on-device food memory Later 60. |
| R26-R34 / D3,D8,D10 | 7-12, 23C, 32; richer training/progression only evaluation in 51 and separately scoped follow-up after its gate. |
| R35-R40 / D3,D8,D10 | 11-12, 23C, 32, 37; capacity/substitution/progression Later 49-51; simulator Later 61. |
| R41-R45 / D5,D8,D10 | 5-6, 16-20; Health Connect product ingestion Later 45; richer optional context Later 59. |
| R46-R50 / D8,D11 | 0C, 13, 16-21; future boundary-settings UI remains deferred and requires its own promoted plan under date invariants. |
| R51-R55 / D8,D10 | 17, 21, 36-37; adaptive/predictive rules Later 51-52/61; no causal verdict from incomplete evidence. |
| R56-R61 / D2,D4-D8,D12 | 0B-0D, 0H-0L, 22-31, 39-44, 46-47; durable identities, protected atomic save, sync/recovery/privacy are MVP obligations. |
| R62-R66 / D3,D7,D11,D12 | 1, 15, 22, 28-31, 38-44; notifications Later 57; numeric hiding/accessibility/export/corrections remain MVP. |
| R67-R71 / D1,D8-D10 | Saved reuse 4 now; ML 60, simulator 61, integrations 45/59, household 64 and camera notes 63 Later. |
| R72-R74 / D10-D12 | Adult observed pilot 43; low-burden controls 1/37; research/experiments/discovery/atlas Later 58/62, price-aware support 65. |

| Acceptance IDs | Required execution/evidence owners |
| --- | --- |
| T01 | 0C, 3, 17-21, 23B, 41: late dinner changes yesterday only and no auto-completeness. |
| T02, T08-T11 | 8-12, 23C-25, 41: exact performed IDs, partial Finish, scoped undo, today/future changes and exactly-once schedule consumption. |
| T03, T19, T30 | 0H-0J, 23-26, 40-41: real atomic stores/PG, commit/lost-ack retries, cursor groups and concurrency. |
| T04-T05, T14, T17-T18 | 2-3, 13-17, 20-21, 23A/23B, 25, 36-37, 41: missingness, units, dated targets/coverage/conflicts and stale prose. |
| T06, T15-T16, T26-T28 | 2-4, 7, 14, 32-37, 39, 41: source/meal truth, reviewed policy, provider/AI/manual/factual fallback and adversarial text. |
| T07, T22, T25 | 1, 11, 15-21, 37-38, 41: independence/pause, Add/minimal journals, accessibility/numeric controls. |
| T12-T13 | 0C/0G/0N, 5-6, 17-20, 23B, 41: attribution/DST/overlap/missing time and runtime parity. |
| T20-T21 | 0K, 22-27, 39, 41: explicit imports, ownership/auth/CSRF and account switch isolation. |
| T23-T24, T29-T31 | 0L, 26, 28-31, 39-42: stale replay/deletion proof, compatible offline shell, export, restore suppression and operations. |
| T32 | 0G-0N continuously, 41-43 and 46-47: installed native routing/auth/protected SQL/unlock/offline/permissions. |
| T33 | 43: actual approved adult imperfect-week observation, not synthetic E2E or clinical evidence. |
| T34 | 45, 48-65 and any other promoted feature: rights/consent/review/regional/device and baseline/non-actioning evidence; not claimed passed at MVP. |

## Deferred work and stopping point

Parts 45-65 are not first-website-release prerequisites. Other page-20/21 ideas (custom day-boundary UI, full bilingual UI, richer demonstrations/timers/supersets/effort tools, new device/scale/activity imports, billing, iOS, a worker fleet, clinical/social features) are retained as explicitly deferred scope, not secretly bundled into an MVP task. If promoted, split the selected capability into fresh bounded part IDs with the same 18 fields and acceptance mapping; do not use a later research result as blanket implementation approval. No speculative frameworks/directories/services are to be scaffolded now.

COORD-DOCS is a completed historical documentation stage. AUDIT-DOCS records its review and bounded corrections in the [audit report](docs/agent/pre-implementation-audit.md) and [HANDOFF](docs/agent/HANDOFF.md), without starting any of the 82 application parts. Follow HANDOFF's actual next action; owner S0 and a separately approved/saved 0A plan still precede application implementation.
