# Adaptive Health App: System Architecture

**Part:** ARCH-DOCS

**Date:** 11 October 2026

**Status:** Approved architecture direction, documented here for implementation; no application or infrastructure exists yet. Conditional feasibility and policy gates remain open.

**Companion:** [Planned repository structure](STRUCTURE.md)

## Authority and decision record

This is the implementation team's source of truth for technical behavior. The [product blueprint](Adaptive_Health_App_Product_Blueprint.pdf) supplies product intent; [ANALYSIS.md](ANALYSIS.md) supplies stable R01-R74 requirements, D1-D12 decisions, T01-T34 acceptance scenarios, and O1-O9 approval gates. PDF references mean physical pages 1-24. The blueprint SHA-256 is `31c85d96fa511dbd3b9243612254b6fb7d8c15200e644ed3fd57dfe78a25b358`.

The owner approved the implementation plan in this conversation: the Expo-centered recommended stack with M0 feasibility gates; O2's page-19 MVP and deferrals; O3's next-journal-day target activation and explicit skip/finish sequence policy; and a gated protected-storage/privacy design. This resolves the analysis's pending architecture-direction status without modifying that source document. It does not approve unresolved O4/O6 policies, purchases, deployment, external processing, or health advice.

Labels used below: **P** = PDF requirement, **U** = approved owner decision, **E** = engineering specification supporting those requirements, **G** = unresolved gate. Unless identified as P/U/G, concrete interfaces, storage choices, field names, and algorithms below are E. Normative “must” defines intended implementation behavior, not evidence of implementation. Schemas and signatures are illustrative specifications, not installed/generated code. New decisions that change an approved behavior or product protection promise require owner approval; ordinary implementation refinements must preserve these contracts.

| Decision | Current disposition and remaining evidence |
| --- | --- |
| D1 | Expo, React Native, React Native Web, Expo Router approved as primary. M0 must prove web usability and installed Android compatibility. No separate Next.js application. |
| D2 | Strict TypeScript/pnpm workspace, shared domain/contracts, separate Fastify modular monolith. No microservices or extra orchestration layer initially. |
| D3 | Paper wrappers/tokens, React Hook Form/Zod, local React UI state, repository subscriptions, TanStack Query for remote cache. Browser accessibility remains an M0 gate. |
| D4 | PostgreSQL/Drizzle with reviewed SQL migrations; server schemas stay private to the API. |
| D5 | Dexie/IndexedDB web and Expo SQLite Android, shared behavioral contracts. Protected records, migration parity, and real-store tests remain required. |
| D6 | Bounded application sync, explicit conflicts, receipts and tombstones. O6 fixes production retention/replay limits. |
| D7 | Better Auth with web/native session adapters. Protected web vault/native store direction approved; O4 key lifecycle and O6 deletion/retention details remain open. |
| D8 | Pure deterministic domain, Luxon date adapter, decimal.js, immutable historical snapshots. O3 activation/sequence defaults approved. |
| D9 | FoodData Central server adapter, manual/saved foods, vetted regional expansion; O8 licensing/quality/processing gate. |
| D10 | Reviewed deterministic policies plus optional bounded AI; O5 reviewer/policy and O8 provider/consent/cap gates. |
| D11 | Small SVG charts and accessible calendar/agenda; cross-platform manual evidence required. |
| D12 | Layered CI, independent static web and managed API/database direction. O7 hosting and O9 pilot approvals remain open. |

## 1. System boundaries and deployment topology

### 1.1 Launch system

```text
                          SAME OWNED SITE, HTTPS
 app.<owned-domain>                              api.<owned-domain>
 Static Expo web shell                           Fastify /api/v1 + /api/auth
      |                                                    |
      v                                                    v
 Universal screens/use cases <--- typed contracts ---> Auth + domain commands
      |                   account-scoped sync               |       |
      +-- Web adapter: protected Dexie/IndexedDB            |       +-- Email provider
      +-- Android adapter: protected Expo SQLite            |       +-- Food catalog provider
          (installed compatibility builds in M0)            |       +-- Optional AI provider
                                                           v
                                                   PostgreSQL / Drizzle
                                                           |
                                                   Encrypted backups
                                                   + deletion suppression
```

Deploy the exported web application independently from the API. Launch recommendation: Cloudflare Workers Static Assets for the web shell; a paid Render API and paid PostgreSQL in the same approved region. Exact services, domain, plan, region and budget are O7 decisions. Static pages must contain no private journal data; logged-in data is loaded at runtime. There is no request-time SSR dependency for logging and no direct client database connection.

The API is one modular process with bounded database-backed operational jobs. Email, deletion, export, and cache refresh can run from that deployment with leases/retries; no Redis, message broker, separate worker fleet, vector database, or analytics warehouse is required. Transactional jobs must record their pending work before an API acknowledgement. Provider calls never occur inside health-record database transactions.

Android uses the same application source and API. M0 produces installed development builds; Android store release is later. EAS cloud builds are optional, not a correctness or paid-service prerequisite. Native health integrations are future adapters, not launch services.

### 1.2 Authority and network requirements

| Data/action | Authority and availability |
| --- | --- |
| Guest journal | Separate local namespace; no anonymous server account required. Manual food, saved meals, workouts, sleep, weight, notes, date edits and local summaries work offline after local initialization/unlock. |
| Account journal | Server-accepted history is canonical in PostgreSQL. Local committed pending intent remains visible and durable; it is not permission to overwrite server revisions. |
| Drafts and pending commands | Local repository owns them. Draft input is not confirmed food or performed exercise. A locally saved record can still be unsynchronized. |
| Targets/plans/nutrient snapshots | Accepted immutable snapshots preserve the evidence used at that time. Candidate snapshots may be provisional during conflicts. |
| Aggregates/narratives | Derived from evidence, revisions, coverage and policy. Rebuild or invalidate; never silently become record authority. |
| Authentication/sync/import to account | Network required. Expired authentication does not prevent local manual saves in the protected existing namespace. |
| New external food lookup/AI/email/server export/account deletion | Network required. Cached catalog/manual input and local export remain available where unlocked. Never report a remote action completed before acknowledgement. |

Offline web startup requires a previously loaded compatible shell and local store. A first visit with no connectivity cannot load an uncached website. Storage eviction or device loss can destroy guest/unsynchronized records. Synchronization is not a substitute for tested server backups, and local persistence is not a backup.

### 1.3 Future infrastructure and reconsideration triggers

Health Connect, notifications, camera/barcode, on-device inference, richer recipes, advanced planning, a separate job worker and materialized analytics are Later/Research. Add them only at their approved gates. Reconsider Next.js/Capacitor if M0 shows structural browser problems; separate clients only if platform divergence warrants duplicated UI. Reconsider managed replication if custom sync exceeds its bounded scope or cannot pass correctness tests. These are decisions to review, not automatic fallback implementations.

## 2. Universal UI architecture

### 2.1 Screens, navigation and responsive behavior

Expo Router route files are thin composition/navigation entries. Feature directories own screens and workflows; shared application services own commands; reusable UI owns presentation. No route file accesses SQL, Dexie, provider SDKs or authentication secrets.

Food, Workout, Sleep, Overall remain in that order on both platforms. Disabling a tracker preserves access to its history/settings, stops prompts and removes current combined evaluation. Optional compact navigation hides disabled trackers while retaining a settings/history entry point. Overall is a read-model consumer, not another journal obligation [P pp. 4, 12].

Re-enabling restores prior preferences and asks whether the old goal still applies [P p.4; R08]. That review does not silently reactivate or rewrite historical targets; any newly accepted activation follows section 6.2's next-journal-day rule.

| Viewport, logical pixels (E defaults) | Layout |
| --- | --- |
| Under 600 | Single-column screens, bottom navigation, full-screen editors where space requires; safe areas and keyboard avoidance on Android. |
| 600-1023 | Navigation rail, bounded readable forms, single-column details or contextual side panel when space permits. |
| 1024 and wider | Rail and content grid; list/detail or calendar/agenda panes; no stretched phone-sized controls spanning the page. |

Breakpoints control layout, never domain meaning. Use measured available width, not user-agent/device assumptions. Browser zoom, split-screen Android and large text may move layouts between modes. User preference and reduced motion override decorative animation.

| Destination | Shared capability on web and Android |
| --- | --- |
| Food | Selected journal date, up to two initially pinned bars, meal list, Add food, source/assumption review, full nutrient details, completeness control. |
| Workout | Planned occurrence/rest, last comparable work, Start/Resume, custom session, set controls, explicit finish recap, schedule move/skip. |
| Sleep | Last main sleep, duration-first entry, optional timing/restfulness, date choice, naps and overlap review. |
| Overall | Enabled-module status/coverage, a meaningful trend and one primary next step with Why this, Make it easier, Dismiss. |
| Shared | Progressive onboarding, module/goal/settings controls, day/month/year calendars, account/sync/conflict/privacy/export flows; universal Add supports Food, Workout, Sleep, Weight and Note. |

The selected journal date is explicit navigation/application state and is passed into editors. Universal Add displays it before Save. Browser routes use fixed shells with query parameters for private entry IDs/dates; do not attempt to prerender each user's dynamic records. Refresh and deep links resolve to a shell, then perform account/namespace checks. Native back navigation and browser back preserve sensible editor navigation; leaving dirty input offers save/discard/cancel. A foreground day rollover updates the default Today view but never changes an open editor's captured date silently.

### 2.2 Components, forms and state ownership

Own semantic tokens for color/status, typography, spacing, radii, focus, motion and chart scales, expressed through Paper wrappers and RN layout primitives. Keep error/unknown/rest/paused colors semantically distinct with text/icons. Theme state is presentation, not journal state. Provide non-color labels, generous targets, readable contrast, visible keyboard focus, focus restoration after dialogs, logical heading/order semantics on web and accessible labels on Android. Target WCAG 2.2 AA; automated checks do not establish conformance.

React state/context owns transient input and navigation; repository subscriptions own durable records; TanStack Query owns disposable remote catalog/request caching. Do not create a second journal write queue through Query mutations. React Hook Form/Zod wrappers retain editable numeric text until validation: blank is not zero; invalid input retains the user's text and shows a field-linked error. Unit conversion occurs through the domain, not the form library. Bangla names and mixed Bangla-English input must render even though interface copy is English.

Simple/detailed mode changes visibility, not stored values, validation correctness or required error messages. Numeric hiding must also cover accessible labels and chart summaries while retaining a nonnumeric description; it must not delete underlying evidence. Pending AI, pending sync, local saving and locally saved are separate statuses.

### 2.3 Platform interfaces and error states

| Interface | Web implementation | Android implementation |
| --- | --- | --- |
| JournalRepository / LocalUnitOfWork | Dexie/IndexedDB and protected record codec | Expo SQLite with protected database/key configuration |
| SessionTransport | Browser credentials/cookies | Better Auth Expo protected cookie/header transport |
| Vault / CredentialStore | Reviewed unlock/key lifecycle; no session secret in IndexedDB | SecureStore for small session/key material; encrypted SQLite for logs |
| Connectivity / AppLifecycle | Browser online/visibility plus actual request results | Native network/AppState notifications plus actual request results |
| Clock / IdSource | Runtime wrappers supplying instants and cryptographic UUIDs | Equivalent native-safe implementation |
| FileExport | Browser file/download adapter | Native file/share adapter; explicit user action |
| HealthIntegration (Later) | Unsupported capability result | Health Connect capability/permission adapter after approval |

Universal business logic consumes interfaces, never `window`, `document`, `localStorage`, native modules or ambient network state. Platform-aware date inputs and chart renderers may differ behind shared values/semantics. Native-only imports must not leak through a shared barrel into the web graph, and vice versa.

Loading/locked storage is distinct from no entries. Show recoverable local-save failures without a false success indicator. Pending sync does not block continued independent logging. Conflicts provide local/canonical comparison. Provider failure offers manual/factual fallback; global error boundaries preserve already committed records and offer recovery. Unsupported/denied optional integrations never disable core logging.

## 3. Domain-driven feature boundaries

### 3.1 Responsibilities and interactions

| Boundary | Owns | Consumes / may request |
| --- | --- | --- |
| Profile/onboarding | Shared inputs, units, adult-scope information, progressive missing-field prompts | Goal/module-specific requirements; no repeated shared questions. Sleep-only requires no calorie/weight data. |
| Preferences/settings | Enabled/paused periods, tone, visible bars, detail mode, date conventions, consent | Profile identity and journal dates; preserves historical eligibility. |
| Goals | Append-only GoalVersion timeline, policy/input snapshots, TargetSnapshot binding | Profile/measurements by explicit snapshot; never today's mutable values for old targets. |
| Food | Entries, component snapshots, ingredients, nutrient provenance, saved meals and recipe versions | Units/dates, provider proposals, applicable targets as read-only comparison. |
| Workout | Template/routine versions, session/exercise/slot snapshots, draft actuals and performed sets | Reviewed exercise catalog, equipment, occurrence linkage; no inferred completed work. |
| Scheduling | Preferred calendar slots, ordered routine sequence, planned occurrences, explicit consumption/move/skip | Session outcomes through a coordinating use case; not direct workout UI imports. |
| Equipment/catalog | Owner equipment profiles, reviewed exercises, permitted measurement modes, load conventions and licensed content | Constraint inputs; external/user text cannot invent vetted capabilities. |
| Sleep | Sessions, duration/timing, restfulness observations, reconciliation groups | Dates, source provenance; no diagnosis or duration-only readiness inference. |
| Journal | Date selection, per-domain day status, minimal weight measurements/notes, history read models | All feature read interfaces; does not own their calculation rules. |
| Aggregates/Overall | Daily/period statistics, coverage, eligible counts, evidence-bound recommendation/dismissal state | Read models only; accepted suggestions invoke owning feature commands. |
| Identity/privacy/sync | Account namespaces, sessions, authorization, outbox/feed/import/conflicts, export/deletion | Typed commands and owned records; no alternate platform business rules. |
| AI assistance | Validated food proposals and optional supplied-evidence narrative | Read-only purpose-limited input; cannot write logs, targets, routine state or exclusions. |

### 3.2 Dependency direction

```text
domain primitives (IDs, dates, units, evidence)
          -> feature rules (food / workout / sleep / goals / preferences)
          -> aggregate calculators and deterministic policy

contracts -> portable domain vocabulary (never database types)
api-client -> contracts + injected session transport

universal screens -> application use cases -> domain + repository/adapter ports
Fastify routes -> application command coordinator -> domain + private DB repositories
platform/provider adapters -> implement ports; composition roots wire implementations
```

Keep cross-feature coordination above feature rules. Finishing a scheduled workout validates and commits session changes plus occurrence consumption in one unit of work. Updating a routine from an in-session action coordinates separate versioned aggregates atomically. This is a modular monolith, not distributed transactions or an event-sourced platform. Audit/recovery records are bounded supporting data, not a mandate to retain every sensitive event forever.

## 4. Data contracts and persistence

### 4.1 Identity, ownership and metadata

Generate domain record, operation, batch and device IDs as cryptographically random UUIDv4 values through `IdSource`, including offline creation. Do not use timestamps, meal contents or array positions as identity. Auth-library user IDs may be opaque strings: a server-owned `JournalAccount` UUID maps uniquely to the Better Auth user; do not assume the auth schema shares domain ID types.

A local namespace is either `guest:<uuid>` or `account:<journalAccountId>`. The server never accepts a guest namespace as authority and derives `accountId` from the verified session. Local drafts/commands retain their original binding across account switches. Every synchronized child/reference must match that account, even if the submitted UUID exists elsewhere.

Illustrative portable record shapes (not implemented):

```ts
type UUID = string;          // validated UUIDv4 for generated domain identities
type Instant = string;       // canonical ISO-8601 UTC instant
type JournalDate = string;   // validated YYYY-MM-DD calendar date
type DecimalText = string;   // finite canonical decimal; no binary-float serialization

type EventContext = {
  journalDate: JournalDate;
  occurredAt: Instant | null;
  originalZone: string | null;       // validated IANA zone when known
  originalOffsetMinutes: number | null;
  precision: "instant" | "date-only" | "duration-only";
  attribution: "user" | "default" | "wake-date";
};

type RecordMeta = {
  id: UUID;
  accountId: UUID;                   // server output, not client authorization
  revision: number;                  // accepted revision >= 1
  createdAt: Instant;                // original record creation; may be client-origin
  updatedAt: Instant;                // server acceptance time of current revision
  serverReceivedAt: Instant;
  deletedAt: Instant | null;
};

type LocalState = {
  namespace: string;
  localGeneration: number;           // transaction/CAS guard; not server revision
  acceptedRevision: number | null;
  pendingOperationIds: UUID[];
  syncState: "local-only" | "pending" | "synced" | "conflict" | "blocked";
};

type NutrientValue = {
  nutrientId: string;
  unit: "kcal" | "g" | "mg" | "ug";
  value: DecimalText | null;         // null = unknown; "0" is known zero
  quality: "source" | "estimated" | "manual";
  sourceRef: string | null;
  assumptions: string[];
};
```

Keep device creation/edit timestamps for provenance, separate from server acceptance and actual event time. Client clocks never order conflicts, expire leases or decide winners. Public revisions are bounded positive integers; local-only aggregates have no accepted revision. Sync sequence numbers use decimal strings on the wire if represented by PostgreSQL bigint. Soft deletion is a versioned mutation, not an absent response or authorization failure.

### 4.2 Entity relationships and minimum semantics

```text
JournalAccount / local guest namespace
 +-- Profile, PreferencePeriod, GoalTimeline -> GoalVersion -> TargetSnapshot
 +-- FoodEntry -> FoodComponentSnapshot <- optional SavedMealVersion / RecipeVersion
 +-- EquipmentProfile; Routine -> RoutineVersion -> PlannedSession
 |                                                |
 |                                                v (optional, at most one session)
 +-- WorkoutSession -> ExerciseInstance -> PlannedSetSlot + DraftActual + PerformedSet
 +-- SleepSession -> SleepObservation; SleepReconciliationGroup
 +-- Measurement, Note, DayStatus
 +-- Recommendation -> EvidenceReference
 +-- SyncReceipt, ChangeFeed, Tombstone, GuestImport, ExportJob, DeletionJob
```

| Entity family | Required content / historical behavior |
| --- | --- |
| Profile / PreferencePeriod | Shared inputs and current preferences; effective date periods for enablement/pause and date conventions. Security consent events retain policy version. Current hidden/disabled state does not rewrite historical denominators. |
| GoalTimeline / GoalVersion | Per-account/domain timeline revision protects concurrent changes. Immutable version includes objective, effective-from date, input snapshot, method/policy version and explicit manual/estimated provenance. Next version determines the prior effective end. |
| TargetSnapshot | One canonical binding per account/domain/journal date. Stores concrete targets/ranges, goal version, inputs and calculation version, or explicit absence of an applicable target in the read model. Offline competing candidates remain distinct until reconciled. |
| FoodEntry / components | Event context, confirmed quantities and original portion conventions, source/version/basis, nullable nutrients, overrides and uncertainty. Components belong to an entry; provider changes never recalculate a confirmed old snapshot silently. |
| IngredientReference / NutrientSource | Public/provider catalog reference and licensed provenance, separate from account-owned copies/overrides. Retain source ID, revision/retrieval time, preparation, serving basis, attribution and snapshot used. |
| SavedMealVersion / RecipeVersion | Stable definition identity with immutable versions. Repeat/copy creates a new entry ID. Rich yield/serving UI is Later; references support it without rewriting logged meals. |
| Routine / RoutineVersion / template | Routine pointer plus append-only versions; template content revision/license and accepted constraints. Version contains ordered session definitions and stable exercise/set slots. |
| PlannedSession | Stable occurrence ID, routine version, sequence position, intended date, original plan snapshot and explicit moved/skipped/consumed status. A move preserves ID. Routine definition is not an occurrence. |
| WorkoutSession / ExerciseInstance | Optional occurrence link, original plan snapshot, current-session adjustments, lifecycle, finished time/reason, actual performed work. Custom sessions have no invented occurrence. |
| PlannedSetSlot / DraftActual / PerformedSet | Stable slot identity; immutable original defaults; recoverable editable draft; actual typed measurements only on completion. PerformedSet retains identity through edit/undo/recompletion. |
| SleepSession / SleepObservation | Main/nap, confirmed duration, optional interval, event context, optional restfulness. Separate optional observations avoid expanding required logging inputs. |
| SleepReconciliationGroup | References conflicting sessions and chosen inclusion/resolution. Retain original source records; do not delete source evidence just to avoid double counting. |
| Measurement / Note | Minimal weight measurement with original/canonical units; sensitive note text. Both support dates and ownership. Expanded body/context measures are Later. |
| DayStatus | Per-account/domain/date explicit coverage assertion, revision and attribution; does not combine target attainment, eligibility, rest, lifecycle or sync state into one enum. |
| Recommendation / EvidenceReference | Rule/policy/model versions, evidence IDs/revisions, coverage/window, generated time, dismissal/acceptance and stale status. Acceptance issues a separate owned command. |
| Sync/operational records | Account/device binding, operation hash/result, change sequence, tombstone, batch/job progress and retention policy version. Sensitive payload retention is bounded under O6. |

Illustrative aggregate payloads clarify the difference between source basis and confirmed totals (metadata/local state are the separate envelopes above):

```ts
type FoodComponentData = {
  id: UUID;
  quantity: {
    amount: DecimalText;
    unit: "g" | "serving";
    gramsPerServing: DecimalText | null;
  } | null;                         // null only for explicitly entered meal/component totals
  sourceSnapshot: {
    provider: string;
    sourceId: string;
    sourceRevision: string | null;
    retrievedAt: Instant;
    preparation: string | null;
    basisAmount: DecimalText;
    basisUnit: "g" | "serving";
    nutrients: NutrientValue[];     // source values at that basis, not eaten totals
  } | null;                         // manual input has explicit manual provenance
  confirmedTotals: NutrientValue[];
  overrides: {
    nutrientId: string;
    previousValue: DecimalText | null;
    value: DecimalText;
    scope: "component-total" | "per-basis";
    reason: string | null;
  }[];
};

type FoodEntryData = {
  event: EventContext;
  label: string;
  components: FoodComponentData[];
  savedMealVersionId: UUID | null;
  calculationVersion: string;
};

type SleepSessionData = {
  event: EventContext;
  kind: "main" | "nap";
  durationMinutes: number;           // confirmed integer; not necessarily time in bed
  timing: {
    startAt: Instant | null;
    endAt: Instant | null;
    intervalMeaning: "continuous-sleep" | "time-in-bed" | null;
  };
  sourceRecordId: string | null;
  sourceRevision: string | null;
  reconciliationGroupId: UUID | null;
};
```

Runtime refinements require positive source bases, nonnegative known quantities, valid dates/units, and consistent sleep timing. Both null endpoints mean duration-only; one known endpoint supplies context without a derived opposite endpoint. A complete continuous-sleep interval must agree with duration at the declared minute precision; time-in-bed may contain a shorter slept duration. Per-source identity also carries provider and connection metadata described above. An empty/missing nutrient list never implies known zero. UI drafts are separate types; these confirmed payloads cannot encode an unaccepted AI proposal as a saved fact.

### 4.3 Constraints, revisions and indexes

Use account-scoped composite references and queries. All private parent/child foreign keys include account ownership. PostgreSQL constraints must enforce what they can: valid references, nonnegative known quantities, valid interval ordering, unique slot mappings and canonical day bindings. Runtime domain validation supplies cross-row/state invariants. Shared Zod wire validation never replaces authorization.

| Constraint/index | Purpose |
| --- | --- |
| Primary/unique `(account_id, id)` and owned composite FKs | Reject foreign-parent attachment and account leaks. |
| `(account_id, journal_date, id)` on journal families | Stable day/range reads and keyset pagination. |
| Unique `(account_id, operation_id)` plus request fingerprint | Receipt-based idempotency; same key/different request is an error. |
| Unique `(account_id, sequence)` on change transactions | Ordered account feed, with an account sync-state row as lock/sequence authority. |
| Unique `(account_id, occurrence_id)` for non-null workout links | At most one logical performed session per planned occurrence; concurrent starts conflict. |
| Unique `(account_id, session_id, exercise_instance_id, slot_id)` | At most one retained PerformedSet identity per slot, including undone sets. |
| Unique `(account_id, routine_id, version_number)` and goal equivalent | Immutable version identity; protect mutable timeline/pointer with revisions. |
| Unique `(account_id, domain, journal_date)` target binding / DayStatus | One canonical evaluation basis and coverage assertion; conflicts cannot overwrite it silently. |
| `(account_id, start_at, end_at)` sleep and reconciliation membership | Overlap candidates; no blanket no-overlap constraint, because unresolved evidence must remain representable. |
| Unique `(account_id, provider, connection_id, source_record_id)` when external identity exists | Future idempotent import/update; source revision is data, not part of uniqueness. |

WorkoutSession is the revision boundary for its actuals, slots and exercise statuses; each command increments the session revision once. GoalTimeline guards goal activation; FoodEntry and SleepSession guard their child snapshots. Cross-aggregate commands carry all required expected revisions, acquire locks in a deterministic order under the account lock, and commit all-or-nothing. Two devices editing different sets in one session may conflict: MVP favors explicit reconciliation over clever automatic merging.

Child read DTOs identify their parent aggregate and carry its accepted revision for concurrency; they do not expose an independent writable revision stream. DayStatus, preference timelines, routine pointers and schedule/occurrence coordination have explicit aggregate revision guards as well. All local multi-aggregate writes compare the complete set of expected local generations, matching the server's additional preconditions.

### 4.4 Units, history and migrations

Use decimal.js with 28 significant digits and round-half-up for nutrition/conversions. Serialize decimal strings; use PostgreSQL numeric and canonical text in SQLite/IndexedDB. Round only at documented snapshot/output boundaries. Initial display is whole kcal and one decimal gram, never an accuracy claim. Preserve original input and source precision. Canonical mass is grams for food and kilograms for body/external exercise load; length centimeters/meters by field; exercise elapsed time seconds; sleep duration integer minutes; energy kcal; nutrients retain a registry-defined canonical unit. Counts are integers. Distinguish per-dumbbell from total-barbell load, unilateral work, bodyweight and assistance instead of encoding assistance as negative external weight.

Goal/routine/source definition versions and original session plans are immutable; accepted entry corrections create new record revisions without mutating the original definition. Bounded mutation metadata supports provenance and undo; no unlimited full-payload audit archive. Recovery/undo eligibility is an O6 policy, not an assumption of permanent reversibility.

Server SQL migrations, IndexedDB versions and native SQL migrations are separate, versioned tracks with one shared behavioral fixture corpus. Back up/rehearse recovery before destructive server changes; prefer expand/contract. Local migration must preserve unsent operations, identities, account binding and encrypted payloads. A failed migration enters recoverable/read-only state rather than deleting/recreating the store. New clients must not upgrade a store underneath an incompatible open tab: coordinate close/upgrade, show blocking state, and prevent old writers. Supported schema/protocol compatibility is recorded at each release; no automatic destructive downgrade.

## 5. Offline-first behavior

### 5.1 Repository contract and protected transactions

The local repository exposes aggregate-oriented reads/subscriptions, command commits, durable drafts, outbox access, canonical shadow updates and migration/recovery. It does not expose SQL or IndexedDB objects to use cases. Illustrative signatures:

```ts
interface LocalJournal {
  read(query: JournalQuery): Promise<JournalReadModel>;
  subscribe(query: JournalQuery, changed: () => void): () => void;
  commit(command: DomainCommand, expectedLocalGenerations: AggregateGeneration[]): Promise<LocalCommit>;
  saveDraft(draft: EntryDraft): Promise<void>;
  applyAcknowledgement(result: AcceptedOperation): Promise<void>;
  applyPullPage(page: ChangePage): Promise<void>;
}
```

These names describe ports; referenced types will be refined in the planned application/contracts modules. `AggregateGeneration` pairs an affected aggregate identity with its expected local generation. `commit` atomically writes the aggregate projection, affected derived invalidations, undo metadata and outbox intent. Local UI can show a saving preview, but success means the database transaction committed. On failure, keep editable input, show retry/export/recovery where available, and do not check a set as durably saved. Guest commands commit locally without contacting a server.

On web, store sensitive journal, draft, outbox, conflict and undo payloads encrypted under the approved vault design. Dates/nutrients/notes must not leak through convenient plaintext secondary indexes. O4 approves any retained metadata/index exposure; until then, the conservative design uses opaque identifiers/version metadata persistently and reconstructs sensitive query indexes in memory after unlock. Lock closes plaintext subscriptions and clears decrypted caches. Native SQLite protection must cover the database and operational side files under the selected configuration, not merely the session token.

Encryption work occurs before entering the short IndexedDB write transaction: read the needed versions, validate/prepare/encrypt, then compare all local generations and commit the encrypted batch inside the transaction. If versions changed, discard prepared output and repeat from current records. Atomic generation checks prevent two tabs overwriting each other. Do not await network or unrelated cryptographic promises inside a Dexie transaction; IndexedDB may auto-commit. Use an exclusive scoped transaction for native multi-record writes and route all writes through the repository. These differences are why identical adapter code is not a requirement. [Dexie transactions](https://dexie.org/docs/Dexie/Dexie.transaction()), [Expo SQLite transactions](https://docs.expo.dev/versions/latest/sdk/sqlite/)

### 5.2 Outbox lifecycle and retries

```text
validated local command
    -> atomic projection + outbox intent
    -> queued -> sealed for dispatch -> in flight
                    |                      |
                    |                      +-> accepted -> atomic local acknowledgement
                    |                      +-> uncertain delivery -> retry SAME envelope
                    |                      +-> conflict -> preserve + block dependants
                    |                      +-> invalid -> repair/replace explicitly
                    +-> auth/offline/capability blocked -> retain and resume
```

Keep the accepted canonical shadow separate from the local pending projection. A local generation increments on every local write; it is never used as an API expected revision. Sequential pending commands reference predecessor operation IDs. Seal a wire envelope only when its predecessor results are known, using the accepted revisions then available. The stable operation ID is allocated at local commit; once sealed or sent, its expected revisions and payload never change. A modified conflict resolution is a new operation with an explicit link to the superseded intent. No automatic timestamp-based rebase.

Use one foreground sync coordinator per namespace, with a durable lease/claim for multi-tab dispatch. Database compare-and-set plus server receipts provide correctness even if leadership notifications are lost. Serialize dependent aggregate commands; independent aggregates may proceed in a bounded queue. UI/Query/provider code cannot submit duplicate business writes independently.

Retry timeouts, lost acknowledgements and transient 5xx/network failures using the same sealed envelope; exponential backoff with jitter starts at roughly one second and caps at one minute while active. Honor Retry-After for 429. Connectivity signals trigger attempts, not assertions of success. 401 pauses for authentication, 403 blocks for investigation, validation errors need correction, and conflicts need resolution. None implies deletion. Manual retry resets waiting but not operation identity. Background execution may improve freshness and is never needed for correctness.

### 5.3 Server acceptance and committed change ordering

For each semantic command:

1. Verify session, active account, route authorization, bounded envelope and account binding. Lock that account's sync-state row; all journal writers, imports, deletions and relevant jobs use this same discipline.
2. Look up `(accountId, operationId)` before expected-revision checks. If accepted with the same canonical request fingerprint, return the original result. Different content under that ID is `IDEMPOTENCY_KEY_REUSED`.
3. For new work, verify protocol/replay lease, parent ownership, expected revisions, schema and domain invariants. A missing update target is never treated as create. A deleted record cannot be recreated by an ordinary create/update.
4. Apply the entire semantic action, increment affected aggregate revisions once each, allocate the next account change sequence under the lock, and persist the receipt and change group in that PostgreSQL transaction. Any failure rolls all of it back.
5. Commit before returning canonical changes/revisions or success. Release the account lock on commit. Another transaction cannot allocate/publish the next sequence before this one commits or rolls back.

One feed sequence represents one committed command/change group, possibly touching multiple records. A pull page never splits a change group; bounds reject excessively large commands before commit. Server-side maintenance that changes visible data emits the same kind of group. Catalog data may use a separate public cache/version path.

The client commits accepted canonical revisions, receipt state and queue progress together. If later local intents exist, reconstruct their pending projection on top of the accepted shadow only if their recorded assumptions still validate; otherwise expose a conflict. Never replace the user's current draft with an old acknowledgement.

Pull uses an opaque account/device-bound cursor identifying a committed sequence and protocol/feed epoch. Apply each page's records, tombstones, invalidations and next cursor atomically. Pending local work survives: incoming canonical data goes to its shadow and may produce an explicit conflict. Account deletion/authorization failures are not empty pull pages.

### 5.4 Conflict, deletion and stale-client handling

Conflict UI shows the local intended action, server version and relevant original base. Choices are keep server, create a reviewed replacement/merged command, or preserve/export local work for later. Keeping local is not an unconditional overwrite; it creates a validated command against the displayed current revisions. Conflicting goal/target candidates remain provisional, and dependent attainment/narratives disclose that status.

Deletes create revisioned tombstones and immediately remove the record's contribution from normal read models. Restore/undo is an explicit permitted command referencing the deletion revision and retained payload; it creates a new revision. Undo expiry and payload purge are O6 decisions. Accepted receipts are never erased to simulate undo.

The supported unattended-offline horizon, operation receipts, tombstones, undo payload retention and device replay leases are one policy. Devices receive account-bound server-issued replay leases/epochs. Expired leases/cursors require rebootstrap and explicit pending-work reconciliation; clients may not simply put an old operation under a new lease. Preserve the old store until reconciliation/export finishes. The absence of an old ID in a pruned snapshot does not prove its write never happened. Uncertain old operations are not replayed as creates; an explicitly reviewed replacement uses a new identity. O6 must approve the minimal suppression evidence and retention required to prevent resurrection. A production release must not invent those durations.

Rebootstrap downloads a bounded, consistent canonical snapshot at a feed watermark, then resumes later change groups. Preserve pending intent separately and reconcile before dispatch. Bootstrap pagination must represent a single watermark-consistent view, not unrelated live table scans. Server implementation may materialize a temporary account snapshot as a bounded job; expiry and cleanup are part of O6. Catalog caches and derived caches may be rebuilt freely; journals may not.

### 5.5 Guest import, logout and recovery

Guest-to-account import is explicit and retryable. Preview record counts, goal overlap, sleep conflicts and destination account; offer keeping the guest journal separate. Create a stable import batch with a frozen snapshot/manifest and stable per-item operation identities. Preserve domain IDs and child references. Persist server progress and use the normal acceptance rules. Dependent records import in graph order; the batch may be partially complete, but each aggregate/semantic group is atomic and progress is visible. Do not report completion early.

Identical-looking meals are legitimate separate records. An actual ID collision is a conflict: choose the existing record or explicitly copy the affected graph using a consistent new-ID mapping. Never silently remap a single child. Edits made to guest records after the captured snapshot remain guest-local and require a follow-up import. Do not delete the guest source merely because login succeeded; completion/retention behavior is governed by O4/O6 and explicit user choice.

On account switch, cancel old requests/sync, increment an in-memory account-session generation, close/lock its store, clear UI/query/decrypted state and ignore stale responses before opening the next namespace. Logout must distinguish session revocation from keeping/erasing the protected offline copy; O4 fixes the policy and unsynced-loss choices. Expired sessions retain protected pending work. Reinstallation can restore accepted account history after sign-in, but not promise recovery of unbacked-up guest records, lost vault keys or unsent changes. Machine-readable export does not imply an implemented import/restore feature.

## 6. Date, time, and history invariants

### 6.1 Four distinct time concepts

| Concept | Meaning |
| --- | --- |
| Actual event instant | When an event happened, if known; store UTC instant. Never substitute creation/sync time. |
| Original zone/offset | IANA zone and resolved offset used to interpret input. Unknown imported/old context may remain null; do not invent it. |
| Assigned journal date | Valid date chosen/confirmed for organization and evaluation, independent from event instant. No UTC-midnight representation for a date-only value. |
| Record/transport times | Creation, local edit, accepted update, server receipt, completion and deletion times each retain their own meanings. |

Luxon sits behind portable date functions; public contracts contain only date/instant/zone primitives. Supply current time through Clock, not calls to ambient time inside rules. User-entered local times must resolve against a zone: reject nonexistent DST times and ask which offset is intended for ambiguous times. Known sleep elapsed duration uses resolved instants, not wall-clock subtraction. Record-level attribution persists through travel or later preference changes.

Default journal day is the local calendar day with midnight boundary. The model retains effective date-boundary preferences; Later custom boundary settings apply only to future default assignment. Backdating and explicit sleep-date choice are MVP. Across overnight sleep, main sleep defaults to wake date; naps keep their own selected date. Interval aggregation uses the whole session under its confirmed journal attribution, not automatic splitting at midnight. Cross-date overlap is still checked before totals.

At 00:30, a dinner can have today's actual instant and yesterday's journal date. Yesterday's Food and Overall totals change; today is not charged. Saving the meal does not mark yesterday complete [P pp. 7, 22]. Editing a record's assigned date invalidates both old and new days and their month/year/Overall/evidence windows.

### 6.2 Effective targets and preferences

U/O3: newly activated goals/targets take effect next journal day; no same-day or retroactive target-policy correction in MVP. This rule also avoids an undocumented special case for first activation: onboarding may preview the proposed target, while a day with no effective target is shown as unassessed. If current-day first-activation behavior is later requested, record it as an explicit O3 amendment rather than silently backdating a version.

An offline activation captures the confirmed next journal date, date-context snapshot and base timeline revision when the user acts. Reconnection does not move its requested effective date to the server's tomorrow. Delayed acceptance must validate that base and all affected canonical target bindings; an incompatible already accepted historical binding produces a conflict, never a retroactive overwrite. Device timestamps are provenance, not permission to defeat those checks. This preserves a legitimate delayed proposal while keeping already accepted history stable.

Evaluate any historical day against the applicable immutable GoalVersion/input/policy snapshot. Lazily materializing a daily TargetSnapshot is allowed only from that historical version, never from today's profile or formula version. If none existed, show no historical target. The canonical target binding is unique; offline candidates cannot overwrite one another. Explicit reconciliation preserves an already accepted historical binding and resolves competing provisional candidates against the legitimate accepted timeline without erasing rejected evidence. A rejected goal proposal can be revised for a permitted future date, not used to rewrite accepted past targets. Conflicting attainment remains provisional until resolved.

Enablement and pause periods are effective-dated. Disabling now stops current prompts without rewriting prior eligible days. A record can exist on a paused/rest day; show the observation and intentional state separately. Changes to UI-only bar ordering or tone need no retroactive reinterpretation of records. For date-boundary/zone changes, use the context captured when a target activation or record assignment was confirmed; do not recalculate stored dates on another device.

### 6.3 Coverage, eligibility, attainment and rebuilds

Keep these independent axes:

| Axis | States / calculation |
| --- | --- |
| Logging coverage | unknown, partial, complete. Completeness is a user assertion where applicable, not inferred from a meal count. |
| Eligibility | enabled/disabled and active/paused from applicable periods. |
| Schedule intent | planned work, planned rest, unscheduled; not evidence of performed activity. |
| Execution | Workout lifecycle/coverage in section 8. |
| Attainment | unassessed or evaluated against the applicable target with sufficient evidence; never use missing as failed. |
| Data quality/sync | known/estimated/unknown nutrient coverage, provisional conflicts, pending/accepted records. |

First confirmed food on an unasserted day makes its logging coverage partial; only an explicit action makes it complete. Entry edits retain the user's completeness assertion but invalidate/recalculate nutrient sufficiency and attainment. An empty food day has unknown intake unless the user separately confirms zero intake for that empty day; completeness alone is not that confirmation. Removing/moving the last meal cannot manufacture an explicit zero. A zero-intake assertion is tied to the current day evidence and becomes invalid when entries are added or changed; DayStatus retains this distinction. Sleep totals disclose resolved observation coverage; unknown days remain absent, not zero. No activity is inferred from an empty workout calendar.

Daily/period read models carry observed, complete, eligible and metric-known day counts. Complete-day nutrition averages exclude partial/unknown days and use nutrient-specific known-day denominators; display observed subtotals separately. Planned adherence and actual volume are distinct. Partial current months/years are labeled and compared to like elapsed periods. Do not sum or average across incompatible load conventions/exercises as if comparable.

Recompute indexed affected days and all dependent periods/recommendations after every accepted or pending local correction, deletion, undo, reconciliation or attribution change. Cache identity includes evidence revision vector/digest, coverage, target binding and calculator/policy version. Mark narrative stale before showing recalculated numbers beside old prose; use deterministic fallback until a validated current narrative is available. For pilot scale, query canonical indexed rows and use small disposable caches; full rebuild must produce the same result as incremental updates.

## 7. Food calculation and AI boundary

### 7.1 Confirmed quantities and provenance

Manual nutrients, cached source search/details and saved meals remain usable without AI. A parsed phrase is a proposal, not a saved confirmed entry. Display proposed food/source, preparation, amount/basis, uncertainty and editable assumptions before confirmation. A late AI response must compare the draft/evidence version and be discarded or offered as a new suggestion after user corrections.

Normalize provider nutrient IDs and units into an explicit registry. Retain raw/cooked state, per-100-g/per-serving basis, source record/revision, retrieval time and licensed attribution. For a mass-based source, calculate `confirmed grams / basis grams * source nutrient value` with decimal arithmetic. For example, 150 g of a confirmed food whose source states 120 kcal and 4 g protein per 100 g contributes 180 kcal and 6 g protein. These are arithmetic fixtures, not a dietary recommendation or real food assertion.

If protein is unknown in one component, report the sum of known protein plus missing-component coverage, not an exact total. Provider energy remains the energy source; do not reconstruct it silently from rounded macros. A manual override is explicit, retains the original source/calculated value and its scope, and survives source refresh. When quantity changes after an entry-total override, require confirmation/replacement of that override; do not silently scale a value whose basis is unknown. Portion scaling works automatically only when an explicit per-unit basis exists.

Mass-to-volume conversion requires measured serving equivalence or a supported density. “One bowl” without a measured equivalent cannot yield exact grams. For the cake/frosting case, ask whether 50 g was consumed mass or original slice mass; if unknown, retain an explicit estimate/assumption, never an exact invented frosting subtraction [P pp. 3, 6, 16].

Saved meals are versioned reusable definitions. Repeat/copy has a new entry identity/date and a copied confirmed snapshot. Editing a log does not mutate the reusable definition or earlier logs; “Remember this” creates a new version explicitly. Rich recipe yield/cooking-loss/personal-container UI is Later. Ingredient and recipe version references exist now so that feature can be added without rewriting old entries.

### 7.2 Providers and regional expansion

FoodData Central is the first server-side catalog adapter/cache. API credentials stay server-only. Bound request sizes, rate-limit, cache permitted catalog responses and handle quota/outage with manual/cached fallback. Data availability does not establish regional coverage or licensing for other sources.

The Bangladesh-first benchmark includes raw/cooked rice, dal variants, fish/chicken curry, khichuri, roti, mixed dishes/oil, packaged items, serving ambiguity, Bengali script, transliterated Bangla and mixed English. Record source-match quality, assumptions, unknown nutrients, corrections and manual fallback. O8 approves licensed regional content and measured acceptance thresholds; no automatic import of a published table merely because it is downloadable. Barcode/Open Food Facts expansion requires its own license/quality review. See [ANALYSIS.md section 6.4](ANALYSIS.md#64-food-providers-and-regional-validation).

### 7.3 Narrow AI contracts

`FoodProposal` contains candidate permitted source IDs, quantity/basis proposals, exclusions, assumptions and clarification choices. `SummaryProposal` references precomputed facts/evidence, approved policy and allowed qualitative language. The server validates both against the central schemas. The adapter has no journal write tools and cannot update goals, exclusions, completion or remembered recipes.

Render numeric summary facts deterministically; permit AI connective language only within supplied evidence. Reject extra numerical claims, unrecognized sources, diagnoses, policy changes and unsupported causal explanations. On timeout/refusal/invalid result/provider outage/budget exhaustion, use manual food entry or a factual summary. Treat all free text as data, including malicious instructions embedded in meals/notes.

Send only purpose-necessary consented content, never the whole journal by default. Do not log prompts or retain raw media in MVP. Provider selection, retention/training terms, region, consent, user/project hard caps and kill switch are O8 gates. Reviewed eligibility, estimator/activity/protein/goal bounds and training policy are O5 gates. No numeric health threshold becomes approved merely by appearing in the PDF. If review is absent, a manual-only pilot is a reduced release, not full page-19 MVP completion.

## 8. Workout state machine

### 8.1 State vocabulary

Plans are intentions. A performed row exists only after a completion action; unchecked defaults and drafts do not count toward volume [P pp. 9, 22]. Every exercise instance has stable set slots, including explicitly added sets. Adding/duplicating a planned set creates a new slot with no performed values. Rechecking an undone set uses its retained performed ID.

Preserve each slot's warm-up versus working set classification in original-plan snapshots and performed history [P p.8; R28]. Comparable-history queries distinguish this classification alongside exercise, equipment, measurement mode and load convention; undone or incompatible work cannot become a suggested previous performance. Parts 8/9 and 23C verify these existing requirements.

| Object | Persisted state | Display/derived meaning |
| --- | --- | --- |
| Planned occurrence | scheduled, consumed-finished, consumed-skipped | Move changes its date only. Consumed state links the responsible outcome; each occurrence is consumed at most once. |
| Set slot | pending, performed, skipped; optional retained undone actual | Planned/pending counts no performed work. Skipped counts no work. Undo returns to pending and retains recoverable actuals marked undone. |
| PerformedSet | completed or undone, typed actuals, completedAt and optional undoneAt | Only completed contributes to current totals. Editing preserves identity and original completion instant unless explicitly correcting it. |
| Exercise/session lifecycle | planned, active, closed | `closed` requires explicit Finish/Skip, not a checked-last-set inference. |
| Closed outcome | completed, finished-early, skipped | Completed satisfies planned scope; finished-early retains some performed work with omitted scope; skipped has no performed work. |
| Coverage | none, partial, full, unplanned | Derived separately; active partial is in progress, closed partial is finished early. Custom work without a baseline reports actuals with unplanned coverage. |

“Undone” describes reversal of a completion, not an extra completed set. Display skipped and undone differently. An active session can have all planned sets checked but still awaits explicit finish. A custom session can be closed-completed without an invented plan percentage. Removing a planned set from today's execution does not erase the original denominator; omitted work remains explainable. Routine changes never alter that original session snapshot.

### 8.2 Commands and transitions

| Action / guard | Atomic result |
| --- | --- |
| Start planned occurrence | Create/return one linked active session with plan/exercise/slot snapshots; competing create conflicts under the unique occurrence link. Do not consume the occurrence. |
| Start custom session | Create active unlinked session; no queue consumption. |
| Edit unchecked displayed values | Save draft actuals against the slot. Preserve original planned defaults; no performed row or training volume. |
| Complete set, pending/undone slot | Validate measurement mode; create or reactivate the same performed identity using displayed confirmed actuals. Persist completion and local outbox immediately. Exercise/session become active if previously planned. |
| Complete already-completed set | No duplicate. Exact repeated command returns its prior result; changing actuals requires the edit command. |
| Edit completed actuals | Update the same PerformedSet under expected session revision, keep completion identity and recalculate totals. |
| Quick-complete exercise with zero currently completed sets | Explicit “Complete all N sets” for the visible eligible slots, with count and values. Validate and commit all as one command; close completed if original scope is satisfied, otherwise finished-early with omitted scope visible. Retain undo group. If N=0, no completion action. |
| Finish exercise with some completed sets | Keep completed actuals; mark remaining pending/undone slots skipped, close finished-early when scope omitted. No performed rows are created for skipped slots. |
| Finish exercise with all planned scope completed | Close completed. Still no automatic session finish. |
| Complete remaining sets | Separate explicitly counted action for outstanding visible slots. Previously skipped work requires explicit reopen/review; Finish never invokes it. |
| Skip exercise with no completed sets | Mark slots skipped and close skipped. With performed work, use Finish early, not a skip that erases actuals. |
| Finish session | Show performed/skipped recap. Preserve partial exercises; close unfinished exercises with performed work as finished-early, zero-work exercises as skipped, and fully performed exercises as completed. Close session with matching outcome. Consume linked occurrence once. |
| Finish zero-work session | Recap offers explicit Skip; do not report a completed/partial workout with fabricated work. |
| Move/skip occurrence | Move preserves ID/position. Explicit skip consumes once; if active work exists, require its reviewed finish outcome rather than silently discarding the session. |
| Add exercise today / also to routine | Today adds session-specific slots. Also to routine additionally creates a future RoutineVersion under expected routine revision. Multi-aggregate command is atomic; current original plan remains intact. |
| Kill/close/reopen | Restore last committed actuals/drafts and lifecycle. No finish, skipped inference, or queue advancement. |

Timed/distance/bodyweight/assisted/unilateral exercises validate their own measurement variants. A set does not require kg/reps if that exercise does not use them. Different equipment and load conventions remain separate comparison series. Quick completion confirms displayed actuals explicitly; it is not permission to invent absent required values.

New performed work in a planned object uses the documented start/completion transition. Before changing a closed object's completion or planned scope, explicitly reopen the affected exercise/session; it cannot acquire new performed work silently. Correcting values of an already completed set is allowed without reopening, since it does not assert additional completion. Reopening a closed session preserves prior actuals and uses the revision-checked schedule compensation rules below when consumption must change.

`completedAt` is the recorded completion action time, retained for audit/recovery. Actual performance time and assigned journal date use the session/event context; checking a backdated set today must not fabricate a known performance instant for yesterday. Recompletion after undo records the new action time while the undo history retains the previous action. Correcting actual event time is explicit. Deleting a historical session removes its aggregate contribution and emits a tombstone; it does not silently requeue an already consumed occurrence. Schedule correction is a separate explicit revision-checked action.

### 8.3 Undo, recovery and routine sequence

Every undoable semantic action records its affected pre-state, IDs and revisions within the approved retention window. Undo is a new command referencing that action. It restores only the action's changes: undoing Finish does not undo earlier checked sets, and undoing quick-complete reverses only sets completed by that group. Retained actuals become undone/non-counting with their edits recoverable. Recompletion reuses identity. Normal undo cannot erase a later edit on another device; revision mismatch requires reconciliation.

Undoing a closed exercise/session reopens its lifecycle if required. If session finish consumed an occurrence, compensating undo must check both the session and schedule revisions and restore that consumption atomically. If later schedule changes depend on it, surface the conflict rather than rewinding the sequence silently. Local undo after uncertain delivery also queues a dependent compensation; it must not discard an operation that may already have committed remotely.

Example: bench plan has `8 @ 40 kg`, `8 @ 40 kg`, `10 @ 35 kg`. Completing slots 1 and 2 creates exactly two completed PerformedSets. Finish exercise skips slot 3 and closes finished-early. Retrying Finish creates nothing. Undo Finish restores slot 3 pending and exercise active while preserving the same two completed sets. Undo set 2 marks that same row undone and reduces totals to one; checking it again restores the same ID, not a third performed identity.

U/O3: moving/lateness/app closure never consumes an occurrence. Explicit skip or deliberate partial/full session finish consumes it once. Continue with next previews the skip consequence. A custom session leaves the queue unchanged unless the user explicitly links it to an eligible unconsumed occurrence through a reviewed command. Routine edits create future versions; replacing an unstarted occurrence is explicit. Started/completed occurrences retain original snapshots. Actual volume, original-plan completion and routine-sequence position are separate facts.

## 9. Sleep and calendar invariants

### 9.1 Input and overlap model

SleepSession belongs to one namespace/account; observations and reconciliation references share ownership. Duration-only records require confirmed nonnegative duration minutes and journal date, with no invented bedtime, wake time or stages. With both endpoints, calculate elapsed minutes from instants. If the user supplies a different slept duration, retain elapsed interval and confirmed slept duration separately and flag their distinction; duration cannot exceed its containing interval without correction. One endpoint alone does not fabricate the other from sleep duration, because time in bed may differ from time asleep. Minute rounding is explicit at confirmation, not repeatedly accumulated.

Main sleep defaults to the known wake journal date; duration-only forms use the displayed chosen date and label it, rather than fabricating a wake instant. Naps and split sessions remain separate. Optional restfulness and future context are observations, never required for saving duration.

For known intervals, detect overlap across dates/sources. If each record represents continuous sleep, union included intervals before totaling. If intervals are time-in-bed containers with shorter reported slept durations, the overlap cannot locate actual sleep: require reconciliation instead of subtracting an invented overlap duration. Unresolved candidates remain visible and make the affected total provisional; do not display a definitive summed total. Duration-only suspected duplicates also require user resolution. Clearly show which entries are included, excluded as duplicates, or unresolved and preserve source evidence. A cross-date reconciliation explicitly assigns included sleep to journal date(s) without counting the same included interval twice.

Future imports use provider/connection/source-record identity and source revisions. Permission denial, revocation, unsupported capabilities and deleted/updated source records have explicit adapter results. Imported records do not silently overwrite manual corrections; store the correction overlay and show material source changes. This is data-model readiness, not implemented Health Connect ingestion.

### 9.2 Calendar semantics

Every module exposes day entries, selectable month days, twelve year-month tiles, and drilldown preserving date selection. Overall can display separate enabled-domain rings; no unexplained combined score. Provide agenda/text alternatives and keyboard/screen-reader date navigation [P pp. 7, 11-12].

Food classification requires explicit complete logging plus known data for the evaluated nutrient. Workout rings use actual completion of the original planned scope, with rest and finished-early labels. Sleep shows confirmed resolved duration against the chosen target with an upper-range treatment, not unlimited reward. Unknown, paused and disabled are independent labeled states. A rest day can contain a custom workout; report actuals without rewriting planned rest. A disabled domain's history remains reachable.

Regularity metrics require enough comparable known timestamps; duration-only sleep cannot supply bedtime consistency. Missing or unresolved days are excluded from definitive averages and disclosed in coverage. Edits, duplicate resolution and date changes rebuild day/month/year/Overall and invalidate related narratives. Unknown never means failed, inactive or zero.

## 10. Authentication, security, and privacy

### 10.1 Sessions, authorization and secrets

Use maintained Better Auth email/password authentication, verified email and recovery with server-side session verification/revocation. Do not build a password/session system. Web uses Secure, HttpOnly, host-only API cookies with an explicit SameSite policy, exact trusted origins and credentialed CORS. Host UI and API under one owned site; unrelated default hosting domains are not an acceptable assumed cookie configuration. Apply origin/CSRF protection to business mutation routes as well as library auth routes. Browser client code never reads the session cookie.

Android uses the Better Auth Expo integration with SecureStore-protected session material and the documented native cookie/header path for business requests. Browser `credentials: include` is not native session transport. Deep links, reset/verification flows, refresh, logout and account switching must pass installed-build tests. A cached session display is never server authorization. [Better Auth Expo integration](https://better-auth.com/docs/integrations/expo)

All API routes authorize the account and every referenced entity. Apply parameterized SQL, bounded request sizes, shared input validation and server-only policy checks. Reject unknown/foreign references without leaking other accounts' existence. Use least-privilege database/provider credentials, TLS, private database networking, encrypted server disks/backups, restricted operator access and rotation procedures. Rate-limit auth/reset/verification, import, export, catalog and AI separately; no account enumeration through recovery messages.

Only publishable configuration (API URL, release identifier and public feature availability) may enter Expo bundles. Database URLs, auth secrets, food-provider keys, email tokens, signing credentials and AI keys belong in server/CI secret stores. Validate required secrets on server startup; never print them. A variable's name or build system prefix does not make a secret safe to publish. Inspect web and Android bundle/config outputs for accidental credentials.

Use a restrictive CSP, safe text rendering for notes/AI, controlled dependency updates and minimal third-party scripts. No session replay or sensitive journal/request/prompt bodies in telemetry. Record error classes, request IDs, duration and aggregate operational counters with approved retention; identifiers are minimized/redacted. Do not use logs as an unbounded shadow health database.

Health records are not used for advertising or model training by default. External AI is opt-in/purpose-disclosed under O8 and can be disabled without losing manual functionality. Do not claim a medical, privacy-law or distribution-compliance certification from this design; applicable review remains an O9 release dependency.

### 10.2 Local protection and unresolved policy

G/O4: protected offline storage must receive a reviewed key lifecycle before real health data is stored. Preferred web direction is an unlock-protected vault using reviewed cryptographic APIs/libraries; native direction is encrypted SQLite (SQLCipher candidate) with protected keys. SQLCipher requires an actual native build rather than Expo Go. SecureStore handles small keys/session material, not the entire journal. IndexedDB alone, HTTPS, native OS storage or server encryption do not by themselves satisfy the app-level local confidentiality promise. [Expo SQLite encryption](https://docs.expo.dev/versions/latest/sdk/sqlite/)

O4 must approve unlock/setup friction, key generation/wrapping/rotation, memory clearing, forgotten-secret recovery, device lock behavior, backup exclusion, metadata exposure, and logout/offline-copy retention. Separate account credentials from the vault secret: online password reset must not be represented as recovery of unrelated local encrypted pending data. Synthetic-data development may proceed while this gate is open. Never silently substitute unprotected persistence in a real-data build. At-rest encryption does not protect plaintext from hostile same-origin code while unlocked; full cloud end-to-end encryption is not promised.

### 10.3 Export, deletion and restoration suppression

Provide versioned JSON including original/canonical units, journal dates/event precision/zones, history/snapshots, provenance, coverage and retained disabled-module data, plus useful per-module CSVs. Local export works from the unlocked local store and labels pending/conflicted versus accepted values. Server export is an account-scoped asynchronous job over accepted data with an expiring protected download. Neither contains credentials. Neutralize CSV formula injection in text cells. Export/import formats are not automatically a backup-restore product feature. Export expiry and retained job payloads are O6 policy.

Account deletion requires recent authentication and explicit confirmation. Persist the deletion job and immediately deny new health writes, revoke normal sessions and stop recommendation/provider jobs. Erase raw records, retained revisions/undo payloads, derived summaries, exports, caches and eligible provider artifacts under approved service targets. Keep only approved minimal suppression/proof metadata. Restore routines apply deletion suppressions from an independently retained protected backup manifest before reopening a restored database; storing that manifest only inside the old database snapshot is insufficient.

Returning disconnected devices need deletion evidence even after normal sessions are revoked. The gated design uses a distinct per-device, high-entropy deletion-status capability issued while authenticated, stored protected locally and hashed server-side. It authorizes only the minimal status for that account/device, never journal reads/writes. A dedicated TLS endpoint returns account/device-bound deletion generation and status; it is rate-limited and remains available after normal session revocation for the approved O6 lifetime. The client validates response binding and a definitive `deleted` result before automatic local purge. This proof/status path and independently retained suppression metadata must be validated together before production; exact lifetimes/key lifecycle remain O4/O6 gates.

An ordinary 401/403, missing account response, expired capability, timeout or network error is not deletion evidence. If status cannot be verified, retain the locked/protected store pending reconciliation or explicit local erase. Connected devices can erase promptly; disconnected devices and already exported files cannot be guaranteed remotely erased. Explain the distinction between denial of access, primary-store cleanup, backup expiry and final deletion completion.

O6 must specify record undo period, receipt/tombstone retention, maximum offline age, replay/proof capability lifetime, deletion service targets, export lifetime, backup retention and recovery objectives as one consistent policy. Analysis defaults of daily independent encrypted exports, 30-day backup retention and proposed 24-hour recovery/data-loss objectives remain proposals, not approved service guarantees.

## 11. API and shared contracts

### 11.1 One contract and endpoint surface

`packages/contracts` owns Zod wire schemas, command/result unions, error codes, protocol versions and OpenAPI definitions. `packages/api-client` owns typed request methods consuming them and injected session transport. Server routes validate the same wire shapes, then use shared domain rules and server authorization. Database/ORM/Luxon objects never appear in public DTOs. Server and client can release separately; additive compatible changes come first, incompatible changes require a new supported protocol/API version and migration plan.

The following is the preliminary authoritative route surface, not implemented endpoints:

| Route | Behavior |
| --- | --- |
| `/api/auth/*` | Better Auth's maintained authentication protocol, shared by both platforms through their adapters; not a second business API. |
| `GET /api/v1/capabilities` | Supported protocol/schema compatibility, permitted operations, published policy configuration and sync limits for the authenticated account. No secret configuration. |
| `POST /api/v1/sync/push` | Bounded batch of sealed commands. Per-command results; each semantic command atomic, batch not globally atomic. |
| `GET /api/v1/sync/pull?cursor=...` | Account-bound ordered change groups/tombstones with next cursor; cannot split a semantic group. |
| `POST /api/v1/sync/bootstrap` and `GET /api/v1/sync/bootstrap/:id` | Create/poll/download a consistent snapshot and feed watermark; preserve pending local intent. |
| `GET /api/v1/journal/:domain` | Authorized canonical record reads with bounded date filters and opaque keyset pagination. All journal mutations use command acceptance, not a parallel CRUD write path. |
| `POST /api/v1/imports` and `GET /api/v1/imports/:id` | Idempotent guest-import manifest/preview/progress. Confirmed import chunks use shared commands/receipts. |
| `GET /api/v1/catalog/foods` and `GET /api/v1/catalog/foods/:source/:id` | Bounded normalized food search/details; server provider/cache adapter, provenance and failure status. |
| `GET /api/v1/catalog/exercises` and `/api/v1/catalog/templates` | Versioned reviewed catalog/template content with license/policy metadata. |
| `POST /api/v1/ai/food-proposals` and `/api/v1/ai/summaries` | Consented bounded proposal jobs/requests; no health-record writes; budget limits and stale-evidence validation. |
| `POST /api/v1/exports`, `GET /api/v1/exports/:id` | Idempotent export job with protected expiring download. |
| `POST /api/v1/account-deletions`, `GET /api/v1/account-deletions/:id` | Recent-authenticated deletion initiation/status where credentials remain valid; durable job and immediate denial of health writes. |
| `POST /api/v1/devices`, `POST /api/v1/device-deletion-status` | Register authenticated device/replay binding; limited-capability post-revocation deletion evidence described in section 10. |

Static health/readiness endpoints expose no private state. Do not place provider SDKs, API routes or database access inside Expo Router server routes: the independently deployed Fastify service owns server behavior.

### 11.2 Mutations, errors and pagination

Illustrative wire envelope:

```json
{
  "protocolVersion": 1,
  "operationId": "a73d6e82-b904-4e65-9008-7caf764ea1be",
  "deviceId": "fd017f66-c15c-4df3-b0b1-bad87a0a2ad7",
  "replayLeaseId": "opaque-server-issued-binding",
  "aggregate": {"type": "workoutSession", "id": "c4f82e25-c0bd-4a97-a4ea-68fa9952c8bd"},
  "expectedRevision": 7,
  "additionalPreconditions": [],
  "command": "workout.completeSet",
  "payload": {
    "exerciseInstanceId": "27cdb293-cbfc-425c-8c43-171a38c0cf62",
    "slotId": "9845415d-d115-4197-a5b3-4eb9e0a09d17",
    "performedSetId": "2b92c602-1c74-43bd-8342-eb4d11f98be9",
    "actual": {"kind": "reps-load", "reps": 8, "loadKg": "40", "loadConvention": "total-barbell"},
    "completedAt": "2026-10-11T12:30:00Z"
  }
}
```

Create uses `expectedRevision: 0` meaning the owned identity has never been accepted; normal updates/restores require their actual positive expected revision. Server account identity is absent from payload authorization. Cross-aggregate commands specify additional type/ID/revision preconditions. The fingerprint includes semantic command data, IDs, protocol and sealed preconditions, excluding session credentials and transport retry headers. Reused accepted IDs return the stored original result, even if current revisions are higher.

Results are discriminated `accepted`, `conflict`, `invalid`, `blocked` or `retryable` with operation ID, canonical revision/change group where applicable, and a safe error. Results do not imply other commands in the batch succeeded. Dependent commands are never sent together until predecessor acceptance supplies their revisions. Unrelated commands can share a batch. State-changing operational requests outside the journal (import creation/export/deletion/device registration) also require stable idempotency keys scoped to account and operation kind; repeated attempts must not create duplicate jobs or reveal previously deleted payloads.

Error envelope: `code`, safe `message`, `requestId`, optional field paths, `retryable`, optional retry-after and conflict references. Use 400/422 for malformed/domain-invalid input, 401 unauthenticated, 403 unauthorized/blocked, 404 non-disclosing not-found, 409 conflict/idempotency mismatch, 410 expired sync/bootstrap resources, 429 rate limit, 503 transient service failure; unsupported protocol is an explicit `UPGRADE_REQUIRED` error. Batch results carry equivalent typed per-operation errors. Never leak SQL, raw tokens, sensitive logs or another account's existence. Current account deletion proof uses the dedicated capability endpoint, not interpretation of these statuses.

Canonical reads use `(journalDate, id)` keyset ordering and opaque account/query-bound page cursors. Limit defaults to 50 and maximum 200 records as an E starting bound; enforce bytes and command-size limits independently, with final measured limits recorded at M0/M4. Sync cursor is a commit watermark, not a page offset or client timestamp. Restart ordinary pagination when filters change. Snapshot-consistent exports/bootstrap use their own bounded job snapshot, not potentially changing list pagination.

### 11.3 Compatibility and schema ownership

Use strict known fields on mutations; clients tolerate additive documented response fields but validate required semantics. Version local storage schemas independently from wire protocol and calculator/policy versions. Declare minimum compatible client/shell/native versions before pruning/migrating; rejected clients preserve pending work for reconciliation/export. Server-first additive rollout allows an older web shell or offline Android client to return safely. A client update is not permission to replay old commands under new identities.

Generate OpenAPI from the selected schema integration rather than hand-maintaining a contradictory second schema. The chosen Fastify Zod provider/OpenAPI bridge, Zod major version, RHF resolver and TypeScript tooling must be tested together at M0. No compatibility claim follows from this package list alone.

## 12. Testing architecture

### 12.1 Layers and CI ownership

All tests below are planned, not executed. Use synthetic data only until O4 and applicable release gates close.

| Layer | Required tools/evidence | Run policy |
| --- | --- | --- |
| Domain/contracts | Vitest; table fixtures and fast-check property tests for dates, decimal conversions, unknown propagation, state transitions, rebuild equivalence and serialization | Every relevant change/PR; critical domain suite always in CI. |
| Components | Jest/jest-expo + React Native Testing Library; forms, labels, completion/undo, focus/error/status states | Every UI/shared contract change; production-like web build in CI. |
| Local repositories | Same behavioral corpus against real browser IndexedDB and installed Android SQLite, including protected-storage failures | Persistence, migration, encryption, sync and recovery changes; mocks only for fast isolated units. |
| API/database | Fastify injection/request tests against isolated real PostgreSQL; transactions, owned FKs, concurrency, revisions, rollback and commit ordering | API/auth/sync/migration changes; never a production database. |
| Browser E2E | Playwright Chromium/Firefox/WebKit on exported shell + API; multiple tabs/accounts, offline cached reload and service-worker changes | Core smoke on PR; affected integration suites on risky changes; full release suite at milestones. Actual Safari is a manual milestone check. |
| Android smoke/E2E | Installed development/release-like build + Maestro; Hermes dates, native SQL, auth, deep links, keyboard/back, kill/reopen | Build and minimal smoke start at M0; shared/native/auth/storage/date changes must pass Android gates before merge. Broader suite scheduled and at milestones. |
| Security/accessibility | Negative authorization/reference/CSRF, secret/log inspection, automated accessibility + keyboard/screen readers/zoom/motion | Relevant changes plus release audit; manual physical-device/assistive-technology evidence. |
| Operations/policy/pilot | Restore/deletion-suppression rehearsal, migrations, load/provider/email outage, reviewer fixtures and observed adult pilot | M0 measurements; M4 recovery; O5/O8 before advice/external processing; M6 release. |

Future root scripts and the existing `docs/test-command.md` runbook provide local equivalents to CI as each part implements them. Select a mutually compatible Expo/React/RN/jest-expo/RNTL renderer set; use Vitest for framework-independent code and Jest for RN components, with separate test discovery. No invented coverage percentage or success benchmark replaces scenario evidence. Package versions, native Android OS floor, performance budgets and exact browser versions are measured/recorded at foundation, not claimed here.

### 12.2 Acceptance matrix preserving T01-T34

T01-T07 are the seven blueprint p. 22 release scenarios. The remaining IDs preserve the analysis's expanded cases; all must retain their original meaning.

| ID | Required observation | Principal layers |
| --- | --- | --- |
| T01 | Dinner at 00:30 assigned yesterday changes yesterday's Food/Overall, preserves actual instant, does not charge today or auto-complete the day. | Domain, both stores, web/Android |
| T02 | Two bench sets then Finish yields exactly two completed performed identities and a skipped third slot; undo/retry adds none. | State machine, DB, E2E |
| T03 | Offline save, server commit, lost acknowledgement, reconnect/retry yields one confirmed logical entry with correct date; receipt check precedes revision rejection. | Stores, DB, two clients |
| T04 | Partial/absent food produces no low-intake conclusion; averages exclude unknown days and show nutrient-specific coverage. | Domain, components, E2E |
| T05 | New goal then old-entry edit preserves old target and refreshes day/month/year/Overall plus narrative staleness. | Domain, sync, E2E |
| T06 | AI outage/refusal/cap leaves manual/search/saved logging functional, preserves sessions, and uses factual fallback. | Provider contracts, E2E |
| T07 | Disabled workout/paused week has no nags/penalty; history and historical eligible denominators remain correct. | Domain, components, E2E |
| T08 | Zero-set counted quick-complete differs from partial Finish; Complete remaining is separate and explicit. | Domain, E2E |
| T09 | Edit/undo after sync changes the same performed ID; compensation cannot erase another device's later edit. | DB, stores, two clients |
| T10 | Today-only changes leave routine intact; also-to-routine creates a future version and preserves current original snapshot. | Domain, E2E |
| T11 | Move preserves occurrence; skip/finish advances once; lateness/crash/custom session does not consume it; undo checks schedule dependencies. | Domain, DB, E2E |
| T12 | Duration-only has no fabricated interval; overnight/naps preserve attribution; overlap/uncertain duplicates reconcile before definitive totals. | Domain, both platforms |
| T13 | Asia/Dhaka, travel, DST ambiguity/gaps, leap dates and custom-boundary model preserve assigned dates and elapsed duration. | Node, browser, Hermes |
| T14 | Resting/maintenance/target distinctions, manual input, blank/zero, unit conversion and load conventions match reviewer fixtures. | Domain, forms, policy review |
| T15 | Cake/raw-cooked/serving/nutrient mappings retain source energy and uncertainty; no invented frosting mass/density/unknown-as-zero. | Domain, provider fixtures, E2E |
| T16 | Repeat/copy gets new ID/date; saved-meal and prior-log versions survive edits; remembering is explicit. | Domain, stores, E2E |
| T17 | Partial month/year comparisons, observed/complete/eligible counts and historical preferences remain correct. | Property tests, E2E |
| T18 | Offline competing goal/target proposals remain visible; no silent snapshot overwrite; attainment stays provisional until resolved. | API, two clients |
| T19 | Crash/quota/denial/encryption/migration failure commits record+outbox together or neither; no false save; recovery preserves checked sets. | Real stores, devices |
| T20 | Interrupted guest import into existing account preserves identities/references, progress and choice; no content-based deduplication. | API, E2E |
| T21 | Foreign IDs/references/cursors/CSRF rejected; switch drops stale responses; session expiry/401/403 preserves pending work. | Security, browser/native |
| T22 | Sleep-only onboarding asks no calories; later modules reuse profile; re-enabling restores preferences and reviews the old goal without rewriting history; Add preserves date; notes/weight, stable tabs and detail/numeric controls work. | Components, E2E, pilot |
| T23 | Stale updates cannot resurrect deleted records/accounts; only bound deletion proof triggers remote-requested local purge; undo expiry/raw/derived cleanup honored. | API, two clients, operations |
| T24 | Warmed-shell offline reload works; no generic private API cache; old/new tabs and shell/schema upgrades preserve pending operations. | Browser E2E |
| T25 | Keyboard/focus/screen-reader/zoom/reflow/touch/reduced-motion pass; chart meaning has text; numeric hiding retains records and respects accessibility text. | Automated + manual platforms |
| T26 | Injected food text, unsupported sources/numbers and stale AI response cannot change policy or overwrite corrected evidence; telemetry excludes sensitive bodies. | Adversarial contracts, E2E |
| T27 | Reviewed population/bounds/catalog; no punitive prescription, invented equipment/exercise, diagnostic claim or duration-only readiness inference. | Reviewer fixtures, rules, pilot |
| T28 | Food/email/AI timeout/429/quota/cap handled honestly; manual/cache fallback works; email delivery is not falsely reported. | Integration, E2E |
| T29 | JSON/CSV includes retained history, provenance, dates, units, disabled modules and pending labels; no secrets; formula text neutralized and expired links denied. | Content checks, API |
| T30 | Real concurrent transactions cannot skip a late commit, double-apply an operation or partially commit receipts/pages; expired replay preserves work. | PostgreSQL/store concurrency |
| T31 | Restore a backup predating account deletion; independent current suppressions prevent resurrection before service opens; measure recovery targets and scrubbed alerts. | Operational rehearsal |
| T32 | Installed Android proves routing, native auth, encrypted SQL/unlock, offline relaunch, keyboard/locale and denied/unsupported integration behavior. | Emulator + physical device |
| T33 | Adult users complete/correct an imperfect week without developer help; observe friction, trust, return and pressure without invented target metrics. | Approved observed pilot |
| T34 | Promoted Later features require content rights, consent/review, measured regional/device evidence and forecast/baseline/non-actioning evaluation where relevant. | Future gates |

Property tests include command replay stability, nonnegative known subtotals, missingness propagation, immutable target selection, set-ID conservation under edit/undo, exactly-once occurrence consumption, interval-union no-double-counting, and incremental/full-rebuild equivalence. Fault injection covers failure before/after each local/server transaction boundary and account switch while requests are in flight.

### 12.3 Requirement-to-location traceability

The analysis retains the detailed inventory; these contiguous groups map all R01-R74 without changing release classification. Locations refer to planned directories in STRUCTURE.md; no code exists yet.

| Requirements | Primary architecture sections | Planned ownership / main acceptance IDs |
| --- | --- | --- |
| R01-R04 | 2, 3, 14 | universal features/preferences/overall, domain policy; T07, T22, T33-T34 |
| R05-R10 | 2, 3, 5, 10 | features/profile/preferences/journal/account; T20-T22, T25 |
| R11-R16 | 4, 6, 7, 14 | domain goals/policy, features/goals; T05, T14, T18, T27 |
| R17-R25 | 4, 5, 7 | domain food, features/food, API providers; T06, T15-T16, T26, T28, T34 |
| R26-R34 | 3, 4, 8 | domain workout/catalog, features/workout/equipment; T02, T08-T10, T27, T34 |
| R35-R40 | 3, 6, 8 | domain scheduling, features/scheduling, command coordinator; T07, T11, T27, T34 |
| R41-R45 | 4, 6, 9 | domain sleep, features/sleep, health adapter Later; T12-T13, T27, T34 |
| R46-R50 | 2, 6, 9 | domain journal/aggregates, features/journal/overall; T01, T04-T05, T13, T17 |
| R51-R55 | 3, 6, 7 | domain aggregates/policy, features/overall, API AI/insights; T04, T06, T26-T27, T33-T34 |
| R56-R61 | 4, 5, 10, 11, 13 | local data/sync/adapters, API sync/privacy/database; T03, T09, T18-T24, T29-T31 |
| R62-R66 | 2, 10, 13 | preferences/account, API privacy/auth, operations; T21, T23, T25-T26, T29, T31 |
| R67-R71 | 7, 9, 14 | saved meals now; deferred health/AI/planning extension points; T15-T16, T32, T34 |
| R72-R74 | 2, 12, 14 | pilot evidence, low-burden controls now; deferred discovery/adaptation; T22, T33-T34 |

## 13. Deployment and future Android release

### 13.1 Foundation, local development and environments

The owner handles toolchain installation, service accounts, credentials and external configuration under the analysis's manual-setup preference. This documentation part installs/scaffolds/deploys nothing. Future setup instructions belong to the exact paths in STRUCTURE.md.

M0 selects supported Node LTS, pnpm, Expo SDK/React/RN/Router, native plugins and compatible testing/schema tooling as one tested set, pins them in one lockfile and records browser/device versions. Expo monorepo support does not prove every package combination compatible. Confirm pnpm resolver/native autolinking behavior against the selected SDK; avoid multiple React/RN copies or blanket resolver hacks. [Expo monorepo guidance](https://docs.expo.dev/guides/monorepos/)

Local development runs the universal app, Fastify, isolated PostgreSQL and local email capture with synthetic fixtures. Emulator/device networking must use reachable configured API origins, not assume the device's localhost is the development machine. Test production-like HTTPS/cookie behavior separately; development shortcuts do not enter production configuration. Test databases, staging and production use distinct credentials, domains, data and provider caps; no production health data copied into fixtures.

### 13.2 Hosting, rollout and operations

Export a static Expo website with explicit host navigation fallback/fixed routes, versioned assets and a reviewed Workbox app-shell cache/update strategy. Do not cache authenticated journal API responses or bake health data into static exports. A service-worker update must coordinate with local schema and open tabs, preserve pending work and prompt for a safe reload; do not force immediate activation over active editors. Browser API initialization occurs only client-side, never during static render.

Deploy API and PostgreSQL independently of the web artifact. Use an owned shared parent domain and exact trusted origins. The API database is private; migration credentials are separate from runtime privileges. Health/readiness distinguish process availability, DB availability and migration readiness without exposing secrets. Scheduled jobs acquire database leases, retry idempotently and survive process restart. A separate worker is deferred until measured need.

Recommended managed hosting reduces infrastructure operations but does not approve location, vendor suitability or budget. Singapore is only a latency candidate pending O7 review. VPS/Caddy/API/PostgreSQL remains the explicit alternative if the owner accepts patching, firewall, database, backup and shared-failure-domain responsibilities. No free tier guarantees capacity, uptime, indefinite retention or permanent pricing. Recheck plan limits/pricing at provisioning; analysis estimates are dated planning examples, not purchase authority.

CI produces separate web/API/Android artifacts, runs required tests, and promotes through staging with approval of schema/production changes. Deploy backward-compatible server changes before clients. Use expand/contract migrations, verified backups and rehearsed recovery. Rollback a web/API artifact only while schema/protocol compatibility is supported; do not assume destructive schema downgrades are safe. Feature/provider switches default off until their gates pass.

Monitor redacted API error/latency/resource metrics, database saturation, queue age/conflict counts, failed imports, email failures, AI cap/fallback rates and backup/restore age. Alerts carry identifiers/error classes needed for diagnosis without food/weight/notes/prompts. O6 approves retention and recovery objectives. Before first real-data pilot, restore an isolated backup, apply later deletion suppressions, rebuild derived views and measure recovery. Retain encrypted independent backups with reviewed key access and minimum protected deletion manifest outside the restored snapshot.

### 13.3 Milestones and Android

| Milestone | Dependency and required outcome |
| --- | --- |
| M0 foundation | Approved direction; owner toolchains. Synthetic shared form/calendar/trend, static routing/caching, real web/native auth, local transaction/relaunch and one API roundtrip. Installed Android build/smoke in CI. Separate minimal Health Connect capability/read/denied feasibility test without product import. |
| M1 manual journals | M0; O4 before real local data. Profile/preferences, manual food/sleep/weight/notes, saved meals, repository migrations/outbox and continuously persisted sets. |
| M2 workout/schedule | M1 and reviewed minimal catalog. Full state machine, custom/partial sessions, routine snapshots, move/skip/sequence/undo. |
| M3 targets/calendar | Reliable local data/date rules; O5 before automated advice. Versioned targets, coverage, day/month/year and deterministic Overall; manual target work can proceed first. |
| M4 accounts/sync/privacy | O4/O6 policies; O7 before service provisioning. Auth/account separation/import, ordered sync/conflicts, export/delete and restore rehearsal. |
| M5 vetted intelligence | M3-M4 data reliability, O5/O8 review. Licensed food sources, regional benchmark, bounded optional AI, deterministic recommendation/fallback. |
| M6 website pilot | Required tests, O4-O9 release gates and owner approval. Imperfect-week observation, browser/physical Android checks, operational rehearsal, website first. |
| Later Android publication | Revisit device/SDK/plugin support; owner signing/distribution setup and release approval. Harden permissions, accessibility, battery/lifecycle and production builds. |

Use Expo configuration/plugins and generated native projects (CNG) initially; generated Android files are build artifacts unless an approved custom native requirement changes ownership. SQLCipher and future Health Connect checks require installed native builds, not Expo Go alone. Signing keys are held in approved local/CI secret storage, never the repository. Cloud building/OTA updates/store distribution are separate later choices; none permits releasing a native binary that mismatches its native modules or data/schema compatibility.

## 14. Architecture invariants and deferred work

### 14.1 Rules future coding agents must preserve

1. Keep the universal Expo app and one central business API; platform differences live behind explicit adapters.
2. Keep domain logic deterministic and free of browser/native/server infrastructure imports.
3. Save locally and atomically with durable outbox intent before reporting success; network and AI are not prerequisites.
4. Derive server ownership from authenticated identity and verify every parent/reference; isolate local namespaces and stale asynchronous work.
5. Preserve stable record/operation IDs; look up accepted receipts before revision checks; retry identical sealed requests.
6. Never resolve health-record/goal/workout conflicts through timestamps or silent last-write-wins.
7. Preserve original plan, nutrient, goal and date evidence; historical corrections rebuild derived output, not historical targets.
8. Actual event time, journal date, original zone and save time are different values; do not fabricate unknown time.
9. Unknown is not zero, inactivity, failure or a complete record. Coverage, eligibility, attainment, lifecycle and sync are separate axes.
10. Only explicit completion creates performed work. Finish never completes remaining sets. Edit/undo/retry never append duplicate performed identities.
11. Move/crash/lateness/custom work never silently consumes the planned sequence; explicit finish/skip consumes once.
12. Deterministic confirmed quantities produce nutrients; AI cannot invent exact values, modify records/policies or overwrite corrections.
13. Do not double-count overlapping sleep or device imports. Preserve source evidence and explicit reconciliation.
14. No privileged credentials in public bundles, telemetry, fixtures or client storage; protect local journals as well as sessions.
15. Never treat authentication/network failure as account deletion evidence; prevent stale-client and backup-restore resurrection.
16. No real-data deployment past unresolved privacy/retention gates, unreviewed advice policy or unapproved external processing.
17. Start real Android smoke tests at M0; mocked components, Expo Go or web success alone do not prove Android readiness.
18. Keep all planned file/status claims truthful and update architecture/structure together when approved behavior or boundaries change.

### 14.2 Deferred scope

U/O2 retains page 19 as MVP. Custom-boundary settings, scheduled notifications, rich recipe yields/personal portions, capacity dial, equipment substitution engine, advanced progression/plateau/adaptive targets, barcode/photo/voice/OCR, wearable ingestion, on-device ML, solver forecasts, rich gamification/discovery cards, cooperative/household features, billing and iOS release remain Later/Research. Backdating/date choice, in-app controls, manual/vetted routines, module independence, minimal notes/weight and bounded Bangladesh food validation remain MVP. Advanced endpoints/directories are extension points only; do not scaffold speculative subsystems.

Page 23 is a finished-product story, not an expansion of page-19 scope. Its “complete” late-dinner day requires a user completeness assertion. Privacy/export/manual fallback/corrections are not deferred because AI or infrastructure is unavailable. Full cloud end-to-end encryption and guaranteed immediate remote wipe are not promised. If health-policy review is unavailable, identify a manual-only pilot as reduced scope.

### 14.3 Remaining gates and contradictions resolved

| Gate | Approval/evidence still required | Blocks |
| --- | --- | --- |
| O1 evidence | Current/previous major Chrome/Edge/Firefox/Safari and mobile browser/device matrix recorded; accessible shared UI, real stores/auth/native plugin compatibility demonstrated | Advancement beyond structural M0 failures; stack direction itself is approved |
| O4 | Unlock/recovery/key lifecycle, metadata/index exposure, local-copy/logout policy and honest unsynced-loss UX | Real-data local persistence/pilot; synthetic development allowed |
| O5 | Qualified reviewers/curator, supported population, estimator/goal/training bounds, contraindications and uncertainty wording | Advice-producing M3/M5 release |
| O6 | Coupled retention/undo/replay/proof/deletion/backup/export policies and tested recovery objectives | Production sync/deletion/privacy finalization |
| O7 | Hosting/domain/email/region/workspace suitability, operating owner and budget | Provisioning/purchases/production deployment |
| O8 | Food licenses/benchmark, AI terms/consent/provider/caps/kill switch | Real external processing and data-content release |
| O9 | Pilot recruitment/consent/devices/research measures, applicable privacy/distribution review | Real-data/public pilot |

O2/O3 are approved; do not repeatedly ask for those choices. Protected storage versus guest convenience is an explicit O4 tradeoff, not a hidden exception. Finishing versus full completion is resolved by lifecycle plus coverage. Offline availability versus bounded deletion/replay is resolved by preserving pending work with gated reconciliation. Authoritative documentation with unresolved policies means those policies are normative release blockers, not permission for a future agent to guess.

Sources checked during architecture planning on 11 October 2026 include the official Expo SQLite/PWA/monorepo, Better Auth Expo and Dexie transaction documentation linked above. They inform engineering choices, not empirical compatibility or security certification. Further official dependency/version/security references must be rechecked during setup. This part creates only this document and STRUCTURE.md; no application feature, dependency installation, runtime test, deployment, commit or push has occurred.
