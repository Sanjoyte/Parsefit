# Durable engineering memory

Seeded 11 October 2026 (Asia/Dhaka), part COORD-DOCS. These are source-backed constraints, not runtime discoveries or passing tests. Live work belongs in [HANDOFF](HANDOFF.md).

## Decisions and authority

- [ARCHITECTURE authority record](../ARCHITECTURE.md#authority-and-decision-record) resolves ANALYSIS's original pending stack/O2/O3 wording. Expo direction, page-19 MVP/deferred scope, next-journal-day targets and explicit skip/finish sequence policy are already approved. O1 feasibility evidence and O4-O9 gates remain open. Read the actual gate scope in architecture §14.3; do not request the resolved choices again.
- [STRUCTURE](../STRUCTURE.md) owns exact paths and four shared packages. Use singular `docs/agent/`, root `task.md`, one universal app and one central API. Its ARCH-DOCS-only statements describe that historical stage.
- Universal business rules live in `packages/domain`; wire schemas in `packages/contracts`; use-case ports in `apps/universal/src/application/ports.ts`; atomic adapter capabilities in `data/storage-contract.ts`. Composition roots select adapters. Cross-feature coordination belongs above feature rules.

## Correctness constraints worth remembering

- Architecture §§4-6: local generation is not server revision; UUIDv4 IDs are stable. Source/nutrient, routine/original-plan, goal/input/policy and target snapshots preserve history. **First** target activation also begins next journal day; onboarding may preview it while today remains unassessed. Offline requested activation dates are not shifted at reconnect, but cannot replace accepted historical target bindings.
- Dates are calendar strings, not UTC-midnight instants. Event instant, journal attribution, original zone/offset and save time differ. Test Asia/Dhaka plus DST gaps/ambiguities, travel and leap dates across Node, browsers and Hermes.
- decimal.js: 28 significant digits, half-up; canonical decimal strings; preserve original units/precision and source energy. `null`/missing differs from known `"0"`. Per-dumbbell/total-barbell/bodyweight/assistance/timed/distance work need typed conventions.
- Architecture §6.3: food completeness is a coverage assertion, not target attainment. Empty complete intake stays unknown unless separately confirmed zero; deleting/moving the last entry does not create zero. Use nutrient-specific known-day denominators. Date changes invalidate both dates and related periods/narratives.
- ANALYSIS R28/R34 and architecture §§2.1/8: preserve warm-up versus working set kind. Last comparable history uses exercise/equipment/measurement/load-convention context and completed actuals; no-match or undone work cannot invent performance. Only a completion action creates performed work; Finish after 2/3 records two actual sets and skips the third. Undo Finish preserves checked sets. Recheck reuses the performed ID. All checked sets still require explicit session Finish. Move/crash/lateness/custom work never consumes a routine occurrence; finish/skip consumes once; compensation guards session and schedule revisions.
- Architecture §9: duration-only sleep has no fabricated endpoints. Continuous sleep can use interval union; overlapping time-in-bed containers with shorter slept durations require reconciliation. Unknown/unresolved sleep never becomes zero or a definitive total.

## Persistence, migrations and platform pitfalls

- Architecture §5.1: prepare encryption before IndexedDB write transactions, then CAS all generations. Crypto/network awaits inside short transactions risk auto-commit. Native writes need scoped exclusive transactions and protection of SQLite side files. Projection/outbox/undo/invalidations commit together.
- Architecture §§5/11: allocate operation ID at local commit, seal immutable envelope after predecessor acceptance, check server receipt **before** revisions, and retry identical sealed data after uncertain delivery. Account-locked commit sequence and atomic page/cursor application prevent skipped late commits. No timestamp winners or silent rebase. Expired replay preserves pending intent for reviewed reconciliation.
- PostgreSQL, IndexedDB and native SQLite use separate migration tracks sharing a behavioral corpus. Failed migration enters recovery rather than recreating the journal. Shell/schema upgrades coordinate with open tabs; never force reload over editors. Generated Android/CNG output is initially ignored; app configuration/plugins are source truth.
- Architecture §§10/13: browser cookies and native Better Auth transport differ. SecureStore is for small key/session material. SQLCipher and Health Connect require installed builds, not Expo Go. Device localhost is not necessarily the host API; use tested reachable origins. Actual Safari is separate from Playwright WebKit.
- O4 key/unlock/recovery/metadata/local-copy policy gates real data; synthetic feasibility is allowed. Neither IndexedDB nor HTTPS alone fulfills local-at-rest protection. Password reset cannot recover unrelated vault keys.
- Authentication failures are not account-deletion proof. Device-bound minimal deletion capability and independently retained suppression manifest must work together. Apply current suppression before opening a restored older backup; a manifest inside that backup alone is insufficient.

## Testing and intelligence conventions

- [SETUP](../SETUP.md), [ENV_GUIDE](../ENV_GUIDE.md) and [test-command](../test-command.md) were created by SETUP-DOC on 12 October 2026. Version matrix entries are candidates; 0A pins/tests compatibility. Environment names are a proposed registry for owning parts to adopt consistently. The test guide indexes 82 placeholders and only read-only S0 checks are currently runnable; no application result exists.
- [ARCHITECTURE §12](../ARCHITECTURE.md#12-testing-architecture) preserves T01-T34. Vitest/fast-check and RN Jest suites have separate discovery. Real stores/DB/native builds are required for their contracts; mocked tests are insufficient portability evidence. Installed Android smoke begins at M0.
- PDF p.19 order: shared data/date/local storage → manual logging in three modules → workout states → goals/bars → calendars/aggregates → constrained generation/summaries → Overall coaching. Expensive adaptation/ML/integrations are Later gates.
- AI has no journal/policy write authority. Deterministic calculations supply numbers; source/draft/evidence versions guard late responses. Bangladesh-first examples require licensed provenance, raw/cooked/portion ambiguity, Bengali script and mixed Bangla-English fixtures. O5/O8 gates are not engineering guesses.
- No runtime debugging, compatibility, migration or benchmark result exists yet. Add only verified reusable lessons with source/part/date when implementation supplies them; remove obsolete advice with a reason. Never include credentials or personal health data.
