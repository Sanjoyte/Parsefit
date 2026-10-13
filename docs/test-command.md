# Manual and automated test runbook

**Created:** 12 October 2026 (Asia/Dhaka), setup-documentation stage. **Current result:** no application test has run. The repository has no `package.json`, app, API, migrations, test runner, Compose file, web export or Android build. Every application part in the [root roadmap](../task.md) is **Not Started**. This document is a manual instruction and evidence format, not a claim of passing tests.

## 1. How to use this guide

1. Read [SETUP.md](SETUP.md) and [ENV_GUIDE.md](ENV_GUIDE.md). Complete S0 manually. Pick only the approved part and follow its saved plan.
2. A part's section is runnable only after that part creates the stated scripts/files and replaces its placeholder below with literal commands. Run commands from the **working directory shown for that command**. A path in [STRUCTURE.md](STRUCTURE.md) marked PLANNED is not a command.
3. Open the specified number of terminals. Long-running services stay in separate terminals; a command that performs a one-shot check should exit. Stop foreground services with `Ctrl-C` in their own terminal. Stop only the isolated Compose stack according to the part's recorded command; never remove a volume/database just to reset a failed test without an approved recovery step.
4. Use synthetic fixtures and isolated local/test services for routine tests, migration/deletion and fault injection. Part 42 may rehearse specifically approved operations in separate synthetic staging; part 44 permits only the separately approved limited production smoke using a synthetic account. Those plans must name the target and cleanup boundary. Never point a routine test suite at staging/production or use real health records for fault tests. Record component/OS/browser/device versions and only secret **names/presence**, never values.
5. Record `Expected` before running and `Observed` after running with date, command, exit code, environment, browser/device/build and evidence location. A green message in a planned checklist is not observed proof. If a required check cannot run, write `Blocked` or `Not run` with the exact prerequisite; leave the active part In Progress or Blocked. `Done` follows the [task status rules](../task.md#status-and-evidence-rules).

**Shell notation:** code blocks use bash on Ubuntu unless labelled otherwise. Do not type a leading `$` if one appears in a linked vendor example. `<...>` in prose is a value to obtain, not a literal command. `pnpm exec` refers to a package already installed by an approved part. Never run a guessed `pnpm test`, `pnpm dev`, Compose service name or migration command. A browser URL appears only after a part fixes the actual local port/route. For shell setup checks, `command -v NAME` tests presence and prints a path; it does not establish compatibility.

### Current read-only S0 checks (no project script)

Working directory: repository root for `git status`; any directory for version commands. **One terminal; no service.** These do not install or authenticate:

```bash
git status --short
git --version
node --version
pnpm --version
docker --version
docker compose version
java -version
adb version
```

Expected: commands for tools actually installed print versions; a missing pnpm/adb currently produces `command not found` until the owner installs them. `git status --short` reports only intended documentation changes. **Observed on 12 October 2026:** Ubuntu 24.04.4, Git 2.43.0, Node 24.21.0, Docker 29.8.2, Compose 5.6.0, OpenJDK 21.0.12.1; pnpm and adb absent on `PATH`. These are machine observations, not application validation. Docker daemon, browser versions, SDK, actual device and CI access remain unverified.

## 2. Service and terminal convention once implemented

Part 0D must record the exact Compose file, environment-file wiring, service names, API start/migration/health commands and port. Part 0E must record the Expo web start/export command, browser URL, pinned Playwright/browser installation and browser-check commands needed for its own acceptance. Part 0F consolidates those existing runners in CI and records CI/local equivalents. Part 0G must record build/install/ADB/Maestro commands. Until those files exist, no literal startup command is safe to put here.

Typical arrangement **after those parts specify it**: terminal 1 runs the isolated database/email Compose stack, terminal 2 runs the Fastify API, terminal 3 runs the Expo web dev server or static preview. One-shot migrations/tests run in a separate terminal after service readiness. A browser/Android test may require an additional terminal. The implementing part must replace this illustrative arrangement with exact count, directories, ports, readiness check, shutdown and cleanup. Do not start the API before required migration/readiness instructions.

## 3. Required test layers and evidence

| Layer | Owning parts / requirement | What proves it; exact command added later |
| --- | --- | --- |
| Pure unit and property | 0B onward; dates/units/food/workout/coverage/sync | Vitest and fast-check with meaningful edge fixtures, deterministic clocks and serialization. No React/native imports in domain. |
| Type, lint, formatting, import boundaries | 0A onward | Strict TypeScript, ESLint, Prettier check and boundary script on actual workspace. Must reject forbidden sample imports; no global DOM/Node leakage. |
| Web components | 0E onward | Jest/jest-expo/React Native Testing Library, separately discovered from Vitest; validation errors, focus/labels, numeric hiding and layout. |
| API and database | 0D onward; 22-31 critical | Fastify injection/request tests against isolated **real PostgreSQL**, reviewed Drizzle SQL migrations, ownership/rollback/concurrency/receipt/feed/readiness. Mocked DB tests are supplementary. |
| Web local store | 0I onward | Real browser Dexie/IndexedDB, protected commit/CAS/multi-tab/migration/failure/relaunch. Stubs alone are not proof. |
| Native local store | 0G/0J onward | Installed APK, real protected Expo SQLite/SQLCipher candidate, scoped atomic writes/side files/relaunch; native harness and Maestro where applicable. Expo Go or mocked SQLite is not proof. |
| Browser E2E | 0E/0F onward; 41 release | Playwright Chromium/Firefox/WebKit on exported/static shell plus API; deep link, offline reload, multiple tabs, date/history/permissions. Actual Safari manual check is separate. |
| Android E2E/smoke | 0G foundation; repeat for shared/native/date/auth/storage/sync | Installed development build and Maestro, API reachability, back/keyboard/Bangla, kill/relaunch, denied integration. Record emulator and physical device separately. |
| Accessibility | 0E basics; 38/41 release | Automated labels/reflow plus human keyboard, visible focus, screen reader, zoom, touch target, reduced motion, text equivalents and actual Safari/physical Android. Target WCAG 2.2 AA; one automated pass is insufficient. |
| Authentication/privacy/security | 0K, 22-31, 39-41 | Web cookie/CSRF/Origin and native session tests; foreign IDs/references/cursors, account switch/stale responses, 401/403 preservation, export/deletion proof and restore suppressions, secret/artifact/log inspection. |
| CI, operations and deployment | 0F/0G, 31, 42-44, 47 | Local equivalents to CI; installed Android CI; isolated restore/replay/provider outage; staging before production; publication and signing only after owner gates. |

Follow [ARCHITECTURE §12](ARCHITECTURE.md#12-testing-architecture) for T01-T34 and [task.md](../task.md) for part prerequisites. Re-run affected real Android checks whenever shared date, auth, storage, sync or native behavior changes. Automated WebKit does not replace an actual Safari run. Failure to access a required physical device/Safari environment is recorded as a blocker at the milestone, not converted into an expected pass.

## 4. Browser and device manual convention

For each browser run record browser/OS version, viewport, route, selected journal date, local namespace, network state and build ID. Verify current and previous major Chrome/Edge/Firefox/Safari where available under O1; 0N records the concrete support matrix. Check 600 and 1024 logical-pixel transitions, zoom/large text, keyboard-only navigation, focus restoration, back/refresh/deep link, offline warmed-shell reload and multi-tab schema/update safety. Never force a service-worker update over an active editor or cache private API responses. Use synthetic accounts and data.

For each Android run record APK/build ID, Expo SDK/native plugin set, device model/OS/ABI, install method, API origin, locale, permissions and whether it was an emulator or physical device. Install the development build (not Expo Go), navigate, type a mixed Bangla-English sample, use Back, kill/reopen, disconnect/reconnect and inspect locally saved versus synchronized status. For health capability feasibility in 0M, check available/read/denied paths only with synthetic/test data; no product ingestion. Never print logs containing health entries or secrets.

## 5. Critical behavior scenarios to keep in future sections

These are **expected outcomes**, not observed results. Their earliest implementation owner is listed; part 41 runs the cross-platform MVP acceptance suite. Later corrections must preserve the same behavior.

| Scenario / authority | Earliest owning parts | Expected observation |
| --- | --- | --- |
| T01, PDF pp.22-23: 00:30 meal assigned to yesterday | 0C date model, 3 Food, 17/18 aggregates | Yesterday changes, event instant remains 00:30, today unchanged; day completeness is explicit, not inferred. |
| T02/T08: three planned sets, only two checked, then Finish | 9/10 Workout | Exactly two performed-set IDs persist and the third is skipped; undo/retry/recompletion cannot duplicate. Zero-performed quick completion explicitly differs. |
| T03/T19/T30: offline save, server commit, lost acknowledgement, retry | 0H-0J, 23-26 | One logical entry/receipt, same sealed operation envelope, durable pending state until acceptance and atomic cursor/feed application. |
| T04: missing or partial food logs | 16/17, 21 | No low-intake verdict or misleading average; nutrient-specific known-day denominator; empty complete day remains unknown absent separate valid zero assertion. |
| T05/T18: later goal, old-entry edit and offline conflict | 13, 17, 23A/25 | Old target binding stays historical; affected old/new dates, periods and narrative rebuild; conflict remains visible. First new target also begins next journal day. |
| T06/T26/T28: AI unavailable, invalid or over cap | 35/36 | Manual/saved/search logging and factual summary still work; no AI write authority or invented numeric fact. |
| T07/T11: Workout disabled/paused and missed schedule | 1/11, 16 | No reminders/penalty, history remains, eligibility correct; move/crash/lateness do not consume occurrence; explicit finish/skip does once. |
| T12/T13: sleep and dates | 0C, 5/6, 17 | Duration-only adds no invented endpoints; confirmed intervals union, uncertain overlap stays unresolved; Asia/Dhaka, DST gap/ambiguity, travel/leap dates preserve attribution. |
| T20/T21/T23/T31: account and deletion | 22-31 | Foreign data/cursor rejected; switch rejects stale response; 401/403/timeout never purges local work; independently current deletion suppression is applied before restored service opens. |

## 6. Standard future-part section template

Copy this under a heading `### Part <ID> — <roadmap title>` **when the part is implemented**, replacing every bracket with actual evidence. Add a link from its index row below. Do not state `pass` for a command not run. A part may omit an inapplicable layer only with an explicit reason in its approved plan.

```text
Part / plan and approval: <ID, saved plan link/revision, owner approval>
Build and date: <commit or working-tree identifier, YYYY-MM-DD Asia/Dhaka>
Prerequisites: <tool versions, synthetic services, config names only, browser/device>
Terminal arrangement: <N terminals; what runs in each; readiness and Ctrl-C/cleanup>

Command 1:
  Working directory: <absolute or repo-relative directory>
  Literal command: <existing command, copied exactly from manifest/config>
  Expected: <behavior and exit code>
  Observed: <date, actual exit code/result/evidence link, or Not run/Blocked + prerequisite>

<Repeat for type/lint/format/unit/component/API/real DB/real web store/build/E2E/Android as applicable.>

Manual browser: <URL/route, viewport, keyboard/offline/multi-tab steps, expected, dated observed>
Manual Android: <installed APK/device/OS, permission/restart steps, expected, dated observed>
Accessibility/security/privacy: <applicable steps, expected, dated observed>
Failures and recovery: <actual issue, rerun, safe cleanup; no secret/health-data output>
Remaining blocker / next action: <exact owner or environment prerequisite>
```

## 7. Part index: placeholders until implementation

Every row below is **Future placeholder — no executable command, no observed result**. Open its [task.md](../task.md) card for dependencies, acceptance and required platform checks. The implementing part replaces its row's state with a link to a full section using the template, and updates HANDOFF, MEMORY (durable findings only), STRUCTURE creation records and task status. This index covers all roadmap parts, including Later research that may never be promoted. `0A` is the first after owner S0.

| Part | Roadmap title | State |
| --- | --- | --- |
| [0A](../task.md#part-0a) | Repository and compatible toolchain | Future placeholder; commands and observations pending |
| [0B](../task.md#part-0b) | Portable domain and wire foundation | Future placeholder; commands and observations pending |
| [0C](../task.md#part-0c) | Deterministic dates and units | Future placeholder; commands and observations pending |
| [0D](../task.md#part-0d) | Local API and PostgreSQL foundation | Future placeholder; commands and observations pending |
| [0E](../task.md#part-0e) | Universal responsive application shell | Future placeholder; commands and observations pending |
| [0F](../task.md#part-0f) | Test runners and initial CI | Future placeholder; commands and observations pending |
| [0G](../task.md#part-0g) | Early installed Android smoke build | Future placeholder; commands and observations pending |
| [0H](../task.md#part-0h) | Local transaction and sync contracts | Future placeholder; commands and observations pending |
| [0I](../task.md#part-0i) | Protected web storage feasibility | Future placeholder; commands and observations pending |
| [0J](../task.md#part-0j) | Protected native storage feasibility | Future placeholder; commands and observations pending |
| [0K](../task.md#part-0k) | Browser and native auth feasibility | Future placeholder; commands and observations pending |
| [0L](../task.md#part-0l) | Static routing and safe offline shell | Future placeholder; commands and observations pending |
| [0M](../task.md#part-0m) | Isolated Health Connect feasibility | Future placeholder; commands and observations pending |
| [0N](../task.md#part-0n) | Integrated M0 portability exit | Future placeholder; commands and observations pending |
| [1](../task.md#part-1) | Shared onboarding and journal entry points | Future placeholder; commands and observations pending |
| [2](../task.md#part-2) | Manual nutrition calculations and records | Future placeholder; commands and observations pending |
| [3](../task.md#part-3) | Reliable manual Food logging and corrections | Future placeholder; commands and observations pending |
| [4](../task.md#part-4) | Recent foods and saved meal versions | Future placeholder; commands and observations pending |
| [5](../task.md#part-5) | Manual duration-first Sleep logging | Future placeholder; commands and observations pending |
| [6](../task.md#part-6) | Sleep overlap reconciliation | Future placeholder; commands and observations pending |
| [7](../task.md#part-7) | Equipment and minimal exercise catalog | Future placeholder; commands and observations pending |
| [8](../task.md#part-8) | Manual routines and session drafts | Future placeholder; commands and observations pending |
| [9](../task.md#part-9) | Performed-set completion identity | Future placeholder; commands and observations pending |
| [10](../task.md#part-10) | Explicit exercise and session finish | Future placeholder; commands and observations pending |
| [11](../task.md#part-11) | Flexible schedule and routine sequence | Future placeholder; commands and observations pending |
| [12](../task.md#part-12) | Today-only and future routine versions | Future placeholder; commands and observations pending |
| [13](../task.md#part-13) | Manual goals and dated target snapshots | Future placeholder; commands and observations pending |
| [14](../task.md#part-14) | Reviewed maintenance and goal discussion | Future placeholder; commands and observations pending |
| [15](../task.md#part-15) | Configurable progress bars and nutrient detail | Future placeholder; commands and observations pending |
| [16](../task.md#part-16) | Coverage and eligible-day state | Future placeholder; commands and observations pending |
| [17](../task.md#part-17) | Coverage-aware aggregates and invalidation | Future placeholder; commands and observations pending |
| [18](../task.md#part-18) | Day journal and accessible history | Future placeholder; commands and observations pending |
| [19](../task.md#part-19) | Month calendar and coverage statistics | Future placeholder; commands and observations pending |
| [20](../task.md#part-20) | Year calendar and comparable trends | Future placeholder; commands and observations pending |
| [21](../task.md#part-21) | Overall factual dashboard | Future placeholder; commands and observations pending |
| [22](../task.md#part-22) | Product account lifecycle and isolation | Future placeholder; commands and observations pending |
| [23](../task.md#part-23) | Server acceptance and ordered feed kernel | Future placeholder; commands and observations pending |
| [23A](../task.md#part-23a) | Profile and target server commands | Future placeholder; commands and observations pending |
| [23B](../task.md#part-23b) | Food, Sleep and journal server commands | Future placeholder; commands and observations pending |
| [23C](../task.md#part-23c) | Workout and schedule server commands | Future placeholder; commands and observations pending |
| [24](../task.md#part-24) | Client sync coordination and atomic pages | Future placeholder; commands and observations pending |
| [25](../task.md#part-25) | Explicit conflict review and compensation | Future placeholder; commands and observations pending |
| [26](../task.md#part-26) | Consistent bootstrap and expired replay | Future placeholder; commands and observations pending |
| [27](../task.md#part-27) | Explicit retryable guest import | Future placeholder; commands and observations pending |
| [28](../task.md#part-28) | Versioned local JSON and CSV export | Future placeholder; commands and observations pending |
| [29](../task.md#part-29) | Account export jobs and expiry | Future placeholder; commands and observations pending |
| [30](../task.md#part-30) | Deletion jobs, tombstones and device proof | Future placeholder; commands and observations pending |
| [31](../task.md#part-31) | Independent backup and suppression restore | Future placeholder; commands and observations pending |
| [32](../task.md#part-32) | Constrained vetted workout proposals | Future placeholder; commands and observations pending |
| [33](../task.md#part-33) | Database-backed Food search and matching | Future placeholder; commands and observations pending |
| [34](../task.md#part-34) | Bangladesh food validation and curated records | Future placeholder; commands and observations pending |
| [35](../task.md#part-35) | Optional AI Food proposals with fallback | Future placeholder; commands and observations pending |
| [36](../task.md#part-36) | Bounded summaries grounded in computed facts | Future placeholder; commands and observations pending |
| [37](../task.md#part-37) | Evidence-aware next action and reflection | Future placeholder; commands and observations pending |
| [38](../task.md#part-38) | Accessibility audit and bounded fixes | Future placeholder; commands and observations pending |
| [39](../task.md#part-39) | Security, privacy and policy hardening | Future placeholder; commands and observations pending |
| [40](../task.md#part-40) | Offline upgrades and measured performance | Future placeholder; commands and observations pending |
| [41](../task.md#part-41) | Cross-platform MVP acceptance suite | Future placeholder; commands and observations pending |
| [42](../task.md#part-42) | Owner-provisioned staging and operations | Future placeholder; commands and observations pending |
| [43](../task.md#part-43) | Approved adult imperfect-week pilot | Future placeholder; commands and observations pending |
| [44](../task.md#part-44) | Website publication and release handoff | Future placeholder; commands and observations pending |
| [45](../task.md#part-45) | Optional Health Connect product integration | Future placeholder; commands and observations pending |
| [46](../task.md#part-46) | Native Android product hardening | Future placeholder; commands and observations pending |
| [47](../task.md#part-47) | Android signed release preparation | Future placeholder; commands and observations pending |
| [48](../task.md#part-48) | Recipe yields and personal portions | Future placeholder; commands and observations pending |
| [49](../task.md#part-49) | Busy-day capacity proposal | Future placeholder; commands and observations pending |
| [50](../task.md#part-50) | Equipment substitution proposals | Future placeholder; commands and observations pending |
| [51](../task.md#part-51) | Reviewed progression proposal evaluation | Future placeholder; commands and observations pending |
| [52](../task.md#part-52) | Adaptive target and plateau evaluation | Future placeholder; commands and observations pending |
| [53](../task.md#part-53) | Barcode food lookup | Future placeholder; commands and observations pending |
| [54](../task.md#part-54) | Photo food proposal evaluation | Future placeholder; commands and observations pending |
| [55](../task.md#part-55) | Voice food input evaluation | Future placeholder; commands and observations pending |
| [56](../task.md#part-56) | Nutrition-label OCR evaluation | Future placeholder; commands and observations pending |
| [57](../task.md#part-57) | Optional scheduled reminders | Future placeholder; commands and observations pending |
| [58](../task.md#part-58) | Private engagement prototype evaluation | Future placeholder; commands and observations pending |
| [59](../task.md#part-59) | One opt-in broader context input | Future placeholder; commands and observations pending |
| [60](../task.md#part-60) | On-device personal food memory evaluation | Future placeholder; commands and observations pending |
| [61](../task.md#part-61) | Feasible-future simulator evaluation | Future placeholder; commands and observations pending |
| [62](../task.md#part-62) | Personal experiment protocol evaluation | Future placeholder; commands and observations pending |
| [63](../task.md#part-63) | Camera-assisted training-note evaluation | Future placeholder; commands and observations pending |
| [64](../task.md#part-64) | Household recipe-sharing feasibility | Future placeholder; commands and observations pending |
| [65](../task.md#part-65) | Regional budget-aware food proposal evaluation | Future placeholder; commands and observations pending |

## 8. Troubleshooting and honest reporting

| Failure | Response |
| --- | --- |
| Script/file missing | Check `task.md` part and actual filesystem. Mark Not run; do not invent a substitute command or initialize another part. |
| Test runner unexpectedly collects RN tests in Vitest | Check separate Vitest/Jest discovery after 0B/0E; report the failure and fix in owning part. |
| DB test passes with mock only | Mark real PostgreSQL contract blocked until isolated service/migration exists. |
| Browser offline test fails on first-ever offline visit | Expected limitation: first visit needs a loaded compatible shell. Test warmed-shell offline reload separately. |
| Save appears successful but store/outbox test fails | Treat as correctness failure; preserve synthetic evidence and do not mark part Done. |
| Android build or API reachability fails | Record SDK/JDK/Gradle/device/origin and failure class; verify installed build and reachable API, then repeat affected smoke. |
| Safari or physical-device access unavailable | Record exact unavailable OS/device/access prerequisite and part gate; Playwright WebKit/emulator is not an equivalent result. |
| AI/provider outage | Confirm deterministic/manual fallback; avoid logging prompt or private records. |

Stop after documenting the active part's actual evidence. Do not advance to the next part without a new owner instruction.


## AUDIT-DOCS documentation verification

Approved documentation-only audit, 13 October 2026. Prerequisites: this documentation checkout, existing Python 3, Git and ripgrep; Poppler only for the optional repeated PDF inspection below. **Working directory: repository root. One terminal, no service and no second terminal.** No package manager or application runner is needed. This is an audit snapshot check: later approved parts must update its scope/status assumptions rather than treating today's absence of code as a permanent rule.

Run this literal command to check local Markdown links/anchors, task table/card fields, dependencies, coverage IDs, protected sources and documentation-only scope. It reads document content and Git state, never environment secret values. Coverage-ID presence supplements the report's manual semantic review; it cannot establish product correctness by itself.

```bash
python3 - <<'PY_AUDIT'
from pathlib import Path
import hashlib, re, subprocess
from urllib.parse import unquote

root = Path.cwd()
assert (root / 'AGENTS.md').is_file(), 'Run from repository root'
paths = subprocess.check_output(['rg', '--files', '--hidden', '-g', '!.git/**'], text=True).splitlines()
md = {Path(p).resolve(): Path(p).read_text() for p in paths if p.endswith('.md')}
def unfence(s):
    return re.sub(r'^```[^\n]*\n.*?^```[^\n]*$', '', s, flags=re.M | re.S)
def anchors(s):
    clean = unfence(s)
    result = set(re.findall(r'<a\s+id="([^"]+)"', clean))
    counts = {}
    for heading in re.findall(r'^#{1,6}\s+(.+?)\s*#*$', clean, re.M):
        heading = re.sub(r'\[([^]]+)\]\([^)]*\)', r'\1', heading)
        slug = re.sub(r'[^\w\- ]', '', heading.lower()).replace(' ', '-')
        n = counts.get(slug, 0)
        counts[slug] = n + 1
        result.add(slug + (f'-{n}' if n else ''))
    return result
links = 0
for path, body in md.items():
    for target in re.findall(r'(?<!!)\[[^\]\n]+\]\(([^\n]+?)\)', unfence(body)):
        target = target.strip().strip('<>')
        if re.match(r'^[a-z]+://|^mailto:', target):
            continue
        local, _, fragment = unquote(target).partition('#')
        local = re.sub(r':\d+$', '', local)
        dest = (path.parent / local).resolve() if local else path
        assert dest.exists(), f'Missing link: {path.name}: {target}'
        if fragment and dest.suffix == '.md':
            assert fragment in anchors(md.get(dest, dest.read_text())), f'Missing anchor: {path.name}: {target}'
        links += 1

task = (root / 'task.md').read_text()
cards = re.findall(r'^### (\d+[A-Z]?) - ([^\n]+)\n(.*?)(?=^### |\Z)', task, re.M | re.S)
expected = {f'0{chr(c)}' for c in range(65, 79)} | {str(n) for n in range(1, 66)} | {'23A', '23B', '23C'}
assert len(cards) == 82 and {c[0] for c in cards} == expected
rows = {}
for line in task.splitlines():
    if line.startswith('| [ ] | ['):
        cells = [c.strip() for c in line.strip('|').split('|')]
        part = re.match(r'\[(\d+[A-Z]?) - ', cells[1]).group(1)
        assert part not in rows
        rows[part] = cells
assert set(rows) == expected

def deps(s):
    s = s.split('Require their acceptance')[0]
    ids = set(re.findall(r'\b(?:0[A-N]|23[A-C]|[1-9]\d?)\b', s))
    assert ids <= expected, f'Unknown dependencies: {ids - expected}'
    return ids

graph = {}
for part, title, body in cards:
    fields = re.findall(r'^(\d+)\. \*\*([^*]+):\*\* (.+)$', body, re.M)
    assert [int(f[0]) for f in fields] == list(range(1, 19)), part
    data = {int(n): value for n, _, value in fields}
    cells = rows[part]
    assert cells[4] == 'Not Started' and '; Not Started; [ ] complete.' in data[1], part
    assert cells[1] == f'[{part} - {title}](#part-{part.lower()})', part
    assert deps(cells[3]) == deps(data[3]), part
    assert data[17].startswith(cells[5] + ';') and data[18].startswith(cells[6] + ';'), part
    assert '[ ]' in data[13] and '[ ]' in data[16], part
    graph[part] = deps(data[3])
seen, active = set(), set()
def visit(part):
    assert part not in active, f'Cycle at {part}'
    if part in seen:
        return
    active.add(part)
    for parent in graph[part]:
        visit(parent)
    active.remove(part)
    seen.add(part)
for part in graph:
    visit(part)
old = subprocess.check_output(['git', 'show', 'HEAD:task.md'], text=True)
old_cards = re.findall(r'^### (\d+[A-Z]?) - [^\n]+\n(.*?)(?=^### |\Z)', old, re.M | re.S)
old_graph = {part: deps(re.search(r'^3\. \*\*Prerequisites:\*\* (.+)$', body, re.M).group(1)) for part, body in old_cards}
assert graph == old_graph, 'Audit changed dependency edges'

report = (root / 'docs/agent/pre-implementation-audit.md').read_text()
matrix = report.split('## Appendix A.', 1)[1].split('## Appendix B.', 1)[0]
capabilities = re.findall(r'^\| (R\d{2}[a-z]?) /', matrix, re.M)
assert len(capabilities) == len(set(capabilities)), 'Duplicate capability row'
assert {r[:3] for r in capabilities} == {f'R{n:02}' for n in range(1, 75)}
assert set(re.findall(r'\bT\d{2}\b', matrix)) == {f'T{n:02}' for n in range(1, 35)}
for line in matrix.splitlines():
    if re.match(r'^\| R\d', line):
        assert len(line.strip('|').split('|')) == 8, line
assert {int(n) for n in re.findall(r'^## (\d+)\.', report, re.M)} == set(range(1, 9))

protected = {
 'docs/Adaptive_Health_App_Product_Blueprint.pdf': '31c85d96fa511dbd3b9243612254b6fb7d8c15200e644ed3fd57dfe78a25b358',
 'docs/ANALYSIS.md': '9ed98f259756e5c7110ad06320a92dd7d894cef1f5bdbefc8d88d0e22eeca2b3',
 'docs/agent/plans/part-audit-docs-final-pre-implementation-audit.md': 'c85d2acd746bd670f4123d71fb6ebec41218ae190f71841b63c100579c26a6c6',
}
for name, digest in protected.items():
    assert hashlib.sha256((root / name).read_bytes()).hexdigest() == digest, name
allowed = {
 'AGENTS.md', 'README.md', 'task.md', 'docs/ARCHITECTURE.md', 'docs/ENV_GUIDE.md',
 'docs/SETUP.md', 'docs/STRUCTURE.md', 'docs/test-command.md', 'docs/agent/HANDOFF.md',
 'docs/agent/MEMORY.md', 'docs/agent/plans/README.md',
 'docs/agent/pre-implementation-audit.md',
 'docs/agent/plans/part-audit-docs-final-pre-implementation-audit.md',
}
status = subprocess.check_output(['git', 'status', '--porcelain=v1', '--untracked-files=all'], text=True)
changed = {line[3:] for line in status.splitlines()}
assert changed <= allowed, f'Out-of-scope changes: {changed - allowed}'
assert all(line[:2] in {' M', '??'} for line in status.splitlines()), 'Unexpected index/status change'
assert all(p.endswith(('.md', '.pdf')) for p in paths), 'Unexpected non-document artifact'
assert not any((root / p).exists() for p in ['apps', 'packages', 'package.json', '.codex']), 'Unexpected scaffold/config'
assert len([p for p in paths if Path(p).name == 'task.md']) == 1
subprocess.run(['git', 'diff', '--check'], check=True)
print(f'PASS: {len(md)} Markdown files; {links} local links/anchors; 82 cards/table rows with 18 fields; acyclic unchanged dependencies; {len(capabilities)} capability rows cover R01-R74 and T01-T34; 3 protected hashes; {len(changed)} allowed unstaged documentation paths; no scaffold/config/prompt artifact; diff whitespace clean.')
PY_AUDIT
```

**Expected:** PASS with 82 matching cards/table rows, 18 fields per card, unchanged acyclic dependencies, every R01–R74/T01–T34 represented, protected hashes unchanged and only allowed unstaged documentation paths. Local-link counts can change with documentation edits. Failure means inspect the named document/anchor/field; do not generate application files or waive a required check.

Additional literal read-only checks:

```bash
GIT_OPTIONAL_LOCKS=0 git status --short
GIT_OPTIONAL_LOCKS=0 git diff --check
GIT_OPTIONAL_LOCKS=0 git diff --stat
rg --files --hidden -g '!.git/**'
sha256sum docs/Adaptive_Health_App_Product_Blueprint.pdf docs/ANALYSIS.md docs/agent/plans/part-audit-docs-final-pre-implementation-audit.md
pdftotext -f 19 -l 19 -layout docs/Adaptive_Health_App_Product_Blueprint.pdf -
pdftotext -f 22 -l 22 -layout docs/Adaptive_Health_App_Product_Blueprint.pdf -
```

**Expected:** intended Markdown changes only; no whitespace diagnostics; original PDF/ANALYSIS/approved plan hashes match the checker; physical pages 19/22 show MVP order and seven acceptance cases. `git diff --stat` omits untracked files, so inspect the new report/approved plan too. The audit rendered physical pages 7/19/22 using these commands (temporary files outside the repository):

```bash
pdftoppm -f 7 -l 7 -scale-to 1200 -png -singlefile docs/Adaptive_Health_App_Product_Blueprint.pdf /tmp/parsefit-audit-p07
pdftoppm -f 19 -l 19 -scale-to 1200 -png -singlefile docs/Adaptive_Health_App_Product_Blueprint.pdf /tmp/parsefit-audit-p19
pdftoppm -f 22 -l 22 -scale-to 1200 -png -singlefile docs/Adaptive_Health_App_Product_Blueprint.pdf /tmp/parsefit-audit-p22
```

Open the resulting PNGs in an image viewer and compare calendar states, page-19 scope and page-22 scenarios with the report. Browser/device application steps: **Not applicable to this documentation part**; real application checks remain Not run until their owning parts create scripts/builds and the required stores, browsers, native device and approval gates are available. No runtime result may be inferred from these documentation checks.

### Observed audit results — 13 October 2026

| Actual check | Observed result |
| --- | --- |
| Python checker above (first run from an identical temporary file, then final run directly from this runbook's body) | Exit 0, PASS: 15 Markdown files; 297 local links/anchors; 82 matching task cards/table rows with 18 fields; unchanged acyclic dependencies; 143 unique capability rows covering R01–R74 and T01–T34; three protected hashes; 13 allowed unstaged documentation paths. |
| `git status --short`, `rg --files --hidden -g '!.git/**'` | Exit 0; 11 modified tracked Markdown files, new audit report and previously saved untracked approved plan. No scaffold, generated agent config, env file or prompt text artifact. |
| `git diff --check`, `git diff --stat`, review of tracked diff and new documents | Exit 0; no whitespace errors; bounded documentation changes only. No staged changes, commit or push. |
| `sha256sum` for PDF, ANALYSIS and approved plan | Exit 0; all three match the pre-audit hashes embedded in the checker. |
| `pdftotext` extraction and `pdftoppm` renders, pages 7/19/22 inspected visually | Exit 0; source layout and acceptance meaning reviewed; original PDF unchanged. |
| Application/static/build/browser/device/real-store/operational/pilot tests | **Not run.** No application manifests/scripts/builds/services exist. Prerequisites and first owning parts are in the audit report; documentation completion does not waive them. |

A drafting-time run initially found the not-yet-added audit runbook anchor. Adding this section resolved it; the completed checker has no unresolved failure. These observations apply to the audit snapshot only, not future owner setup or runtime compatibility.
