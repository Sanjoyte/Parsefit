# Parsefit

Parsefit is a planned adult wellness app for food, workouts, sleep, and practical next steps. Its product goal is to make logging and planning useful through imperfect weeks: people can correct estimates, move sessions, record incomplete days honestly, and choose manageable actions without punitive streaks. The [product blueprint](docs/Adaptive_Health_App_Product_Blueprint.pdf) describes the intended experience.

> **Current status (11 October 2026): documentation and planning only.** There is no application scaffold, installable app, API, database, test suite, or deployment in this repository yet. The capabilities below describe approved direction and planned work, not shipped features.

## Intended first release

- **Food:** manual and saved meal logging, editable estimates with visible sources and uncertainty, nutrient detail, and explicit day completeness.
- **Workout:** manual routines and reviewed proposals, equipment-aware plans, actual set completion, partial sessions, and deliberate move or skip actions.
- **Sleep:** duration-first logging, optional timing and restfulness, backdating, and honest treatment of overlapping or missing evidence.
- **Overall:** day, month, and year history; coverage-aware trends; and one explainable next action. Missing data remains unknown rather than counting as failure.
- **Control and reliability:** guest logging, optional accounts and synchronization, offline local saves, edit/delete/undo, export, privacy controls, and accessibility checks.

The website is the first publication target. Android uses the same application source and must pass installed-build checks during the foundation work; Android distribution is a later decision. The intended pilot is for adults, with an English interface and Bangladesh-first food validation. Optional AI may assist with proposals or evidence-based wording, but confirmed records and numerical calculations remain under user and deterministic application control.

## Planned architecture

| Area | Approved direction |
| --- | --- |
| Universal client | One Expo / React Native / React Native Web / Expo Router app in `apps/universal` |
| API | One modular Fastify service in `apps/api` |
| Shared code | `packages/domain`, `packages/contracts`, `packages/api-client`, and `packages/test-utils` |
| Data | PostgreSQL with Drizzle on the server; Dexie/IndexedDB on web and Expo SQLite on Android behind shared local contracts |
| Workspace | Strict TypeScript and pnpm; exact compatible versions are still to be verified |

These paths are planned and do not exist yet. The [architecture](docs/ARCHITECTURE.md) defines behavior and open gates; the [structure plan](docs/STRUCTURE.md) owns paths and source boundaries.

## Project documents

| Document | Purpose |
| --- | --- |
| [Product blueprint](docs/Adaptive_Health_App_Product_Blueprint.pdf) | Product intent and proposed user experience |
| [Analysis](docs/ANALYSIS.md) | Requirements, decision history, acceptance scenarios, and open questions |
| [Architecture](docs/ARCHITECTURE.md) | Approved technical behavior, invariants, and remaining gates |
| [Structure](docs/STRUCTURE.md) | Planned repository layout and source ownership |
| [Execution roadmap](task.md) | Dependencies, part status, acceptance, and required workflow |
| [Agent instructions](AGENTS.md) | Rules for changes, approvals, privacy, verification, and Git actions |
| [Live handoff](docs/agent/HANDOFF.md) | Current work state, evidence, and next action |

## Getting started

There are no runnable setup or test commands yet. The owner first completes the manual setup prerequisite **S0** described in [task.md](task.md#manual-setup-prerequisite-s0). After that, work proceeds one approved part at a time, starting with a plan for **0A — Repository and compatible toolchain**. That part will choose and verify the toolchain, create the workspace, and add actual commands. Do not infer installation steps or working scripts from the planned layout.

Development uses synthetic data until the applicable privacy, health-policy, external-processing, and release gates are approved and verified. Do not place credentials or private health data in the repository.
