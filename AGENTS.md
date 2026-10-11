# Agent instructions

## Authority and reading order

Owner instructions and recorded approvals govern scope. Read this file, root [task.md](task.md), [HANDOFF](docs/agent/HANDOFF.md), relevant [MEMORY](docs/agent/MEMORY.md), [ARCHITECTURE](docs/ARCHITECTURE.md), and [STRUCTURE](docs/STRUCTURE.md) before work. Then read the specified part's saved plan, relevant [ANALYSIS](docs/ANALYSIS.md) R/D/T/O IDs, and cited physical pages of the [blueprint](docs/Adaptive_Health_App_Product_Blueprint.pdf). Missing required context is a blocker; never invent its contents.

The PDF governs product intent; ANALYSIS supplies requirements and decision history; ARCHITECTURE governs approved technical behavior and current gate dispositions; STRUCTURE governs source ownership/paths; task.md governs part dependencies and acceptance; an owner-approved saved plan governs one part. HANDOFF is live state; MEMORY is durable knowledge. Architecture's approved stack/O2/O3 supersede ANALYSIS's historical pending wording. Historical ARCH-DOCS-only output limits describe that completed stage. Stop and identify material contradictions; do not silently replace approved decisions.

## Execution and coordination

Only one agent may actively edit the repository at a time. HANDOFF records that owner. Parallel agents may read/review only; they must not install, generate repository artifacts, run mutating application workflows, or edit files. Before transfer, finish current writes, record actual state/results/next action, release ownership, and have the next agent reread continuity files and inspect the worktree. Do not overwrite owner edits or another agent's unfinished work.

Use exactly this workflow for each specified part:

1. **PLAN:** Read dependencies and current docs; plan only that part. No implementation. A proposal may be saved under `docs/agent/plans/` with explicit `Proposed` status.
2. **APPROVAL:** Owner reviews that concrete plan and approves or requests changes. A roadmap row, model recommendation, or another part's approval is not approval of this plan.
3. **SAVE:** Save the exact approved Markdown plan under `docs/agent/plans/part-<lowercase-id>-<slug>.md`, record approval/provenance, and link it in HANDOFF. No implementation in this saving step. Return control for the implementation instruction.
4. **IMPLEMENT:** On the owner's implementation instruction, change only the approved part. No silent scope expansion, dependency substitution, policy threshold, architecture change, or next part. If necessary, propose a plan amendment and obtain approval before dependent work.
5. **VERIFY:** Run relevant automated tests, type/lint checks, builds and manual browser/device checks. Use real stores/databases/native builds for their contracts. Record unavailable checks as blocked/not run, with the precise environment prerequisite.
6. **DOCUMENT:** Update task status/evidence, HANDOFF, relevant durable MEMORY, STRUCTURE creation statuses and relevant docs. Append the part's runnable checks to `docs/test-command.md` once that later setup file exists; a finished implementation part cannot omit it.
7. **STOP:** Present changes, actual results, remaining blockers and exact next action. Wait for the next instruction. Never start another part automatically.

`Done` requires all acceptance criteria and required verification evidence, not merely code or directory creation. Keep required failed/unavailable checks visible and the part In Progress or Blocked. Use the five task.md statuses exactly. Prefer a normal small commit by the owner after an approved plan and after its verified implementation.

## Approved boundaries and correctness

Use one `apps/universal` Expo/React Native/React Native Web/Expo Router app, one `apps/api` Fastify modular API, strict TypeScript/pnpm, and only the four approved packages: domain, contracts, api-client, test-utils. PostgreSQL/Drizzle is server-private; Dexie/IndexedDB and Expo SQLite implement shared local contracts. Domain stays pure; DTOs contain portable values, never ORM/Luxon/platform objects. UI calls use cases, not raw storage/providers; platform adapters are selected at composition roots. TanStack Query is remote cache, never a second journal/outbox.

Web first, Android ready: installed Android build/smoke begins during foundation, before core features. Expo Go, mocked SQLite and web success do not prove native compatibility. Repeat affected real Android checks for shared/date/auth/storage/sync/native changes. Preserve config/plugin/CNG ownership; generated Android projects are initially ignored build outputs. Health Connect foundation work is an isolated capability/read/denied feasibility check, not product ingestion. Publish the website before separately approved Android distribution.

Preserve ARCHITECTURE §§4-11 and §14 invariants:

- Stable UUIDv4 record/operation IDs; local generations differ from accepted revisions. Commit projection, outbox intent, undo and invalidations atomically before reporting a save. Encrypt before short IndexedDB transactions and compare all generations; use scoped native transactions. Network, AI and authentication refresh cannot be prerequisites for local manual saving.
- Derive server ownership from verified identity; authorize every parent/reference/cursor. Separate guest/account namespaces, lock/clear caches on switch, and reject stale asynchronous responses.
- Seal retries once; retry the same envelope. Check receipts before revisions. No timestamp winners or silent last-write-wins. Commit receipt, revisions and account-ordered change group together; apply pull changes/cursor atomically. Keep pending intent during conflicts, upgrades and rebootstrap.
- Separate journal date, actual instant, original zone/offset and transport times. Inject clocks; reject DST gaps and resolve ambiguity explicitly. Serialize decimal strings; use approved precision/units. Unknown is not zero, failed, inactive or complete.
- Preserve nutrient, original-plan, goal/input/policy and target snapshots. All new target activations, including the first, begin next journal day. Offline activation cannot overwrite accepted historical bindings. Corrections rebuild affected old/new dates, periods and stale narratives.
- Coverage, eligibility, attainment, plan intent, execution and sync remain separate. Food completeness is explicit; an empty complete day is unknown absent a distinct valid zero-intake assertion. Use nutrient-specific known-day denominators.
- Only explicit completion creates performed work. Edit/undo/retry/recompletion preserve identity; Finish skips remaining sets. Zero-performed quick completion explicitly counts all N sets; partial Finish never does. Move/crash/lateness/custom work never silently consumes an occurrence; deliberate finish/skip consumes once. Compensation checks session and schedule revisions.
- Duration-only sleep invents no endpoints. Union confirmed continuous intervals; reconcile container overlaps/uncertain duplicates before definitive totals. Preserve source evidence and manual corrections.
- AI proposes permitted matches or supplied-evidence language; deterministic code supplies numerical facts. No journal/policy write tools, invented exact nutrition, diagnoses, or unsupported causality. Check draft/evidence versions and preserve manual/factual fallback.
- 401/403/timeouts are not deletion evidence. Remote-requested local purge requires definitive account/device-bound proof. Backup restore must apply independently retained current deletion suppressions before service opens.

## Configuration, privacy and dependencies

Owner handles toolchain installation, external accounts, credentials and configuration. Repository dependency installation must be explicitly within an approved implementation part; none is authorized by the coordination-documents task. Use synthetic data until O4 and applicable release gates close. O5 review gates automated advice; O6 gates production retention/replay/deletion; O7 gates provisioning/budget; O8 gates licensed content/external processing; O9 gates pilot/release. Do not guess approval or durations.

Keep local development, test, staging and production credentials/domains/data separate. Local shortcuts cannot enter production. Only publishable client config enters Expo bundles. No credentials, signing keys, tokens, private health logs, notes, prompts, or raw media in Git, fixtures, terminal/chat output or telemetry. Do not read or print secret values to establish setup. Use secret names/presence and redacted failures. No production data copied into tests. Do not create real secrets during planning.

Use approved dependency families only after compatible-version checks. A new dependency, paid service, native plugin, architectural layer or scope promotion needs an explicit rationale and owner approval in the part plan. Do not independently upgrade every package to latest. Recheck official documentation during version/security/integration work; today's proposed package list is not tested compatibility.

Feature tests must cover meaningful behaviors and edge cases, not mirror implementation. Follow ARCHITECTURE §12: Vitest/fast-check pure logic, Jest/jest-expo/RNTL components, real PostgreSQL/IndexedDB/installed SQLite contracts, Playwright and Maestro, plus actual Safari/physical-device/accessibility milestone evidence. No private API service-worker cache or forced update over active editors. Never fake test results, command output, benchmarks, devices, approvals or deployments. Expected outcomes and observed results must be separate.

`docs/test-command.md` is intentionally created by a later setup prompt. Each finished part adds prerequisites, working directory, literal runnable commands, terminal count/second-terminal instructions, expected outcomes, browser/device steps, and separately dated observed results or Not run/Blocked. Do not invent scripts before they exist. Store all part plans in `docs/agent/plans/`, even when built-in plan mode uses another temporary location. MEMORY must remain concise technical knowledge with links, not a chat transcript or duplicate live status.

## Git and tool configuration

Read-only Git inspection is allowed. The owner commits and pushes manually. **Do not commit, push, force push, perform destructive resets, rewrite history, amend/rebase history, delete branches/worktrees, or discard work without explicit owner authorization for that action.** Task implementation approval does not authorize Git mutations. Do not stage changes on the owner's behalf.

Root AGENTS.md is canonical; CLAUDE.md is only a bridge. No `.codex/` config is required for these instructions. Never pin permanent model or reasoning-effort settings in `.codex/config.toml`; the owner selects both in the VS Code UI. Quality-critical parts retain strong recommendations even if usage is constrained; disclose picker availability rather than silently downgrade.
