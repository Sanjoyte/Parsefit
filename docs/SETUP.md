# Owner setup: Ubuntu development machine to Part 0A

**Prepared:** 12 October 2026 (Asia/Dhaka). **Repository state:** documentation only. The owner runs all installation, sign-in, account, configuration and environment commands. This guide does not report that those steps were run. Follow [ENV_GUIDE.md](ENV_GUIDE.md) for value ownership and [test-command.md](test-command.md) for per-part checks. The [roadmap](../task.md) makes S0 the manual prerequisite to planning 0A; 0A still needs its own approved plan.

The observed machine is Ubuntu 24.04.4 LTS with Git 2.43.0, Node 24.21.0, Docker 29.8.2, Compose 5.6.0 and OpenJDK 21.0.12.1. `pnpm`, `psql`, `adb` and Android Studio were not found on `PATH` during read-only inspection. Presence and version do not establish that Docker daemon access, Android builds or project compatibility work. Recheck on the machine where you will develop.

## Version compatibility worksheet

These are **setup candidates, not a tested Parsefit lockfile**. Part 0A selects and pins one compatible stable set in `.node-version`, `package.json` and `pnpm-lock.yaml`; 0G validates native plugins in an installed build. Do not independently upgrade individual React/React Native/Expo packages. Check the linked official matrices again when 0A begins.

| Tool / dependency family | Candidate or required floor | When | Compatibility decision and verification |
| --- | --- | --- | --- |
| Ubuntu | 24.04 LTS observed | Now | Supported by current [Playwright system requirements](https://playwright.dev/docs/intro); use another supported OS guide if your development host differs. |
| Git | Maintained Ubuntu package (2.43 observed) | Now | `git --version`; repository access separately checked below. |
| Node.js | 24 LTS candidate (24.21.0 observed) | Now | [Node release status](https://nodejs.org/en/about/previous-releases); [Expo](https://docs.expo.dev/get-started/create-a-project/) asks for LTS. SDK 57 minimum is 22.13.x; this does not prove every native plugin works on 24. |
| pnpm | Current supported line candidate, then exact 0A pin | Now | `pnpm --version`; [pnpm's Node matrix](https://pnpm.io/installation/) supports Node 24. 0A must prove workspace/autolinking/lockfile behavior. Prefer the pinned package manager once `package.json` exists. |
| Expo/React Native/React/RN Web | SDK 57 / RN 0.86 / React 19.2.3 / RN Web 0.21.0 is the current **candidate set**, not a project selection | 0A selection; app in 0E | [Expo SDK matrix](https://docs.expo.dev/versions/latest/) specifies these as a set. 0A/0E/0G must check Router, Paper, Better Auth Expo, SQLite encryption, SQLCipher candidate, Jest/RNTL and native plugins before pinning. |
| TypeScript, Fastify, Drizzle, Zod, RHF, TanStack Query, Dexie, Luxon, decimal.js | Exact compatible versions chosen in 0A and owning parts | 0A onward | No global TypeScript/Expo/Fastify install. `pnpm exec ... --version` only after the relevant manifest and dependency installation. 0A checks TypeScript/lint; 0B checks Vitest/Zod; 0D checks API/Drizzle. |
| PostgreSQL | Supported 18 major candidate, current maintained minor | 0D | [PostgreSQL support table](https://www.postgresql.org/support/versioning/). Pin the isolated Compose image and migration compatibility in 0D; `psql --version` is optional on the host. |
| Docker Engine + Compose plugin | Supported vendor packages; `docker compose` syntax | Before 0D | `docker --version`, `docker compose version`, `docker info`. Current versions observed, daemon access not checked. |
| JDK / Android SDK | JDK 17+ as tool floor; SDK/AGP/Gradle/compile SDK from selected Expo release | Before 0G | [Android JDK guidance](https://developer.android.com/build/jdks) and [Expo SDK matrix](https://docs.expo.dev/versions/latest/). JDK 21 is observed but its compatibility with the eventual Gradle wrapper must be built, not assumed. |
| Playwright browsers / Maestro | Versions pinned to project tests / installed CLI | 0F / 0G | Playwright Chromium, Firefox, WebKit are automated; actual Safari and Android device checks are separate. Maestro needs Java 17+ and an installed app. |

## PHASE A — Before any application code exists

This phase contains machine prerequisites and account preparation only. **Do not run `pnpm install`, Expo creation, migrations, Compose application startup or `expo prebuild` against today's repository.** There is no `package.json`, app manifest, Compose file or `.env.example` yet.

### 1. Confirm host, source access and editor

From any terminal, run:

```bash
cat /etc/os-release
git --version
node --version
code --version
```

Expected: Ubuntu 24.04 (or your recorded supported host), Git, an LTS Node, and VS Code print versions. If a command is missing: on Ubuntu use `sudo apt update` and `sudo apt install git curl ca-certificates` for Git/basics; use the [official Node downloads](https://nodejs.org/en/download) or a trusted Node version manager to install Node 24 LTS; install VS Code using the official [Ubuntu `.deb` instructions](https://code.visualstudio.com/docs/setup/linux). Do not replace a working Node installation blindly; 0A will pin the exact version. `code` missing after GUI installation usually means reopen the shell or check VS Code's command-line path.

Open this checkout in VS Code. Install the official Codex extension from the [Codex IDE guide](https://learn.chatgpt.com/docs/codex/ide), open its sidebar and sign in yourself. Verify the sidebar opens and the model/effort picker shows the options available to **your** account. The picker, rather than roadmap recommendations, determines actual availability. Do not add permanent model/effort settings to `.codex/config.toml`. This editor is useful for the workflow, but it is not an app runtime dependency.

GitHub access is needed when you intend to fetch/push or use GitHub Actions, not for local documentation reading. Create/sign in to your own GitHub account if using that remote. Configure your own identity using Git's normal configuration, set up SSH or a credential manager, and check `git remote -v` in the repo. For SSH, follow [GitHub's key setup](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) and run `ssh -T git@github.com` after registering the public key. Expected: GitHub greets your username; exit status 1 is normal. `Permission denied (publickey)` means check the key, agent, account and remote URL. Never paste private keys or tokens into chat. GitHub is optional for purely local development, but required for the planned GitHub Actions CI and owner pushes.

### 2. Install or verify pnpm and container tooling

```bash
pnpm --version
docker --version
docker compose version
docker info
```

Expected: a pnpm version, Docker/Compose versions and successful daemon information. Install pnpm using the [official pnpm instructions](https://pnpm.io/installation/) appropriate to Node 24; Part 0A will pin the selected version. If `pnpm` is absent, do not try project scripts yet. For Docker on Ubuntu, follow the vendor [Engine repository steps](https://docs.docker.com/engine/install/ubuntu/) and install the Compose **plugin**; avoid mixing distro `docker.io` with Docker's repository packages. If `docker info` reports permission denied, use `sudo docker ...` temporarily or follow the official [Linux post-install](https://docs.docker.com/engine/install/linux-postinstall/) steps after understanding that membership in the `docker` group grants root-equivalent host access. If the daemon is stopped, check `systemctl status docker`. `docker compose` is required by the planned isolated PostgreSQL and email-capture setup in 0D; no container is started in Phase A.

The backend is Node/Fastify, so the same Node runtime serves frontend tooling and API development. PostgreSQL need not be installed on the host: the approved 0D local topology uses a Compose PostgreSQL container. A host `psql` client is optional for manual diagnosis; if desired install `postgresql-client` from Ubuntu's supported packages, verify with `psql --version`, and never point it at production while testing. Drizzle/migration commands become available only after 0D scripts are created.

### 3. Prepare an economical Android route for 0G

Foundation part 0G requires an **installed** Android development APK, Maestro smoke and a representative physical-device check; Expo Go is insufficient. A USB-debuggable Android phone can avoid downloading an emulator image immediately. You still need the selected Android SDK/command-line tools, build tools, JDK and USB debugging. The emulator remains a useful repeatable CI/local target and may be required for 0G CI; defer its large system image until the 0G plan identifies the exact API level and available hardware. [Expo's Android setup](https://docs.expo.dev/get-started/set-up-your-environment/?buildEnv=local&device=simulated&mode=development-build&platform=android) and [Android Studio setup](https://developer.android.com/studio/install) cover both routes.

Before 0G, install Android Studio via the official Linux package/setup wizard **or** Android command-line tools via Google's download page; install Platform Tools (`adb`), the selected SDK platform and build tools in SDK Manager. Install an emulator/system image only if using the emulator route. Record the SDK location and set `ANDROID_HOME` in your shell; add `$ANDROID_HOME/platform-tools` and `$ANDROID_HOME/cmdline-tools/latest/bin` to `PATH` after confirming those directories exist. `JAVA_HOME` should point to the JDK proven compatible with the selected Gradle wrapper. Verify:

```bash
java -version
echo "$JAVA_HOME"
echo "$ANDROID_HOME"
adb version
adb devices
```

Expected: Java 17+; SDK paths; `adb` version; and a device listed as `device` when connected and USB debugging is approved on the phone. An empty list is normal before a device/emulator exists. `unauthorized` means approve the phone's RSA prompt; no device may mean USB cable/mode/udev rules. A phone's `localhost` is the phone itself, so later set a tested reachable API origin, not an assumed desktop loopback address. On Linux, Android Studio+emulator needs sufficient RAM/disk and CPU virtualization; check those before downloading a system image. Do not install native health plugins or create an app in this phase.

### 4. Prepare browsers and accounts, without provisioning services

Have current Chrome or Chromium, Firefox, and Edge available for web checks; arrange actual Safari access on macOS/iOS for milestone evidence. Playwright WebKit is useful automation but does not replace actual Safari. Record browser/device versions when M0 runs. Browser installation is through official vendor/distribution packages; verify with the browser's **About** screen (or its `--version` command when installed). No Safari installation is expected on Ubuntu.

Only local Git/Node/pnpm/Docker and a suitable editor are needed to begin 0A planning. GitHub is required for CI/push, and Android SDK/JDK/device or emulator are required by 0G. Do **not** create paid Render, Cloudflare, email, FoodData Central, AI, Expo EAS or Google Play accounts now. Cloudflare/Render/owned domain/email become O7 choices; FoodData Central and AI access are O8-gated later. EAS is optional. Google Play/signing is for 47 after website release. A local captured-email service uses no external email account.

## PHASE B — After foundation scaffolding is implemented

Run each step only when the named part has created the referenced files **and its approved plan authorizes dependency installation**. The following are navigation and verification commands, not invented project scripts.

| Available after | Owner action | Expected proof |
| --- | --- | --- |
| **Part 0A** | From repository root, check `test -f package.json` and `test -f pnpm-lock.yaml`; use the **literal approved 0A lockfile install/check commands recorded in [test-command.md](test-command.md)**. | One lockfile, pinned Node/pnpm, clean workspace checks. No `npm install` or `package-lock.json`. |
| **Part 0B/0C** | Run their recorded Vitest/TypeScript commands once manifests and scripts exist. | Portable contracts, date/decimal fixtures; no browser/native parity claim yet. |
| **Part 0D** | Inspect `infra/local/compose.yaml` and `apps/api/.env.example`; the owner copies the example to an ignored local file, supplies synthetic/local values privately, starts the specified Compose services and executes the documented initial migration/test commands. | Isolated PostgreSQL and email capture; API health and DB/schema readiness behave separately. Never run migration against a production URL. |
| **Part 0E/0F** | Start the API and Expo web in the terminal arrangement recorded for those parts; install Playwright browser binaries only after the pinned runner exists and the 0F plan includes it. | Exported shell, static routing, browser/component/CI checks. A built web shell is not Android proof. |
| **Part 0G** | Install the Android SDK components/build tools matching the selected Expo SDK; build and install the development APK, then run the documented Maestro/ADB checks. | Installed routing, form/date/API/back/relaunch smoke plus CI and device evidence. Expo Go does not satisfy this. |

Once **0A has created and approved the lockfile**, and only if its approved implementation plan includes this owner installation, the standard reproducible dependency command from the repository root is:

```bash
pnpm install --frozen-lockfile
```

Expected: dependency resolution matches the committed lockfile; this does not by itself prove an app build or a test pass. If the lockfile is absent or pnpm disagrees with the pinned `packageManager`, stop and use the 0A plan rather than regenerating dependencies ad hoc. The part must record its actual workspace check command/result in [test-command.md](test-command.md).

After **0D** creates `infra/local/compose.yaml` and its API example, the owner can inspect them and, if the 0D plan confirms the file format/service topology, copy the example locally and check/start the isolated services from the repository root:

```bash
cp --no-clobber apps/api/.env.example apps/api/.env
docker compose -f infra/local/compose.yaml config --quiet
docker compose -f infra/local/compose.yaml up -d
docker compose -f infra/local/compose.yaml ps
```

Fill the ignored local file privately **before** starting services; the example may not contain usable values. `config --quiet` must succeed and `ps` must show the services chosen by 0D. The exact API start, database migration, health/readiness and test commands still come from 0D's runbook. To stop the isolated services after testing, use `docker compose -f infra/local/compose.yaml down` without `-v`; keep the test database volume for diagnosis unless the approved part describes a reset. Do not infer `pnpm test`, `pnpm dev`, `drizzle-kit migrate`, `expo run:android` or Compose service names from planned filenames. Installed dependencies and scripts do not exist at this documentation stage.

### Project tool installation and version checks after their owning parts

The approved part adds these as pinned **project dependencies**; the owner installs them through the approved lockfile command above, not as unpinned global packages. Each command below is a tool version check, not a test suite. Run from the repository root only after the stated part and dependency installation:

| Available after | Tool and purpose | Exact version check | Expected / common fix |
| --- | --- | --- | --- |
| 0A | TypeScript, ESLint and Prettier for strict types/lint/format | `pnpm exec tsc --version`; `pnpm exec eslint --version`; `pnpm exec prettier --version` | Pinned local versions print; missing binary means inspect 0A manifest/lockfile, not install globally. |
| 0B | Vitest for pure domain/contracts and fast-check properties | `pnpm exec vitest --version` | Runner prints version; use 0B's actual script for tests. |
| 0D | Drizzle migration tool and Fastify API | Check the literal 0D scripts and `apps/api/package.json` | No guessed migration command; readiness must prove isolated real PostgreSQL/schema. |
| 0E | Expo SDK/Router web and Jest/jest-expo/RNTL component runner | `pnpm exec expo --version`; `pnpm exec jest --version` | Local versions print; a native/RN version mismatch requires the selected SDK matrix and lockfile review. |
| 0F | Playwright exported-site browser automation | `pnpm exec playwright --version` | Pinned version prints. The approved 0F plan may instruct the owner to run `pnpm exec playwright install --with-deps` for its browser binaries; download can be large and actual Safari remains separate. |
| 0G | Maestro installed-APK UI automation | `maestro --help` | Help prints after owner follows the [official Linux install](https://docs.maestro.dev/maestro-cli/how-to-install-maestro-cli); requires Java 17+ and ADB/device. Install before the 0G flow, not during 0A. |

No separate global TypeScript, Expo CLI, Gradle or Fastify CLI is required. The selected Expo/Android build supplies a Gradle wrapper/generated native project at 0G; use that part's exact commands. GitHub Actions is hosted CI, not a tool to install on this machine; 0F/0G must supply equivalent local commands and protected CI configuration.

## PHASE C — After individual feature parts

Follow the part's [test-command section](test-command.md): its working directory, prerequisites, terminal count, exact scripts, expected and dated observed results. Recheck real PostgreSQL/IndexedDB/installed SQLite contracts where storage, dates, auth, sync or native code changed. Keep synthetic fixtures until O4 and release gates close. A part remains In Progress or Blocked if required checks cannot run.

## PHASE D — Before web deployment

Available after 42/43 and before 44: owner chooses and approves exact domain, same-site `app.`/`api.` origins, hosting/provider/region/budget and staging/production separation under O7, plus O4-O9 release gates. The approved architecture recommends static Expo web on Cloudflare Workers Static Assets and managed Fastify/PostgreSQL on Render; these are directions, not provisioned accounts. Use [Cloudflare Static Assets](https://developers.cloudflare.com/workers/static-assets/) and [Render environment configuration](https://render.com/docs/configure-environment-variables/) only after the approved deployment plan supplies exact commands. Keep server secrets in the host's protected environment, ensure database runtime and migration privileges differ, run staging migration/backup/restore and full acceptance, verify trusted origins/cookies/HTTPS, inspect public assets for secret leakage, then obtain the separate production promotion approval. Free-tier limits and pricing are not assumed; recheck vendor terms at O7.

If 42 selects Cloudflare, its approved project manifest installs Wrangler as a pinned development dependency; from the repository root verify `pnpm exec wrangler --version` **available after Part 42**. Render provisioning is through its approved dashboard/infra definition; no separate Render CLI is required. A `wrangler` missing-binary error means inspect 42's manifest/lockfile. Authentication and deployment commands are supplied only by the approved staging/production plans; a version check does not deploy a site.

## PHASE E — Before Android building and publication

An **early development build is required at 0G**, before core features; the later publication sequence starts only after website part 44. At 46 re-evaluate Expo SDK, Gradle/JDK, target/compile SDK, native plugin and representative OS/device matrix; test actual device accessibility, offline relaunch, protected storage and permissions. At 47 the owner chooses the Android application ID, signing custody, distribution track and applicable developer verification/store requirements, then prepares a signed release under a separately approved plan. Signing keys and passwords belong in protected local/CI storage, never `EXPO_PUBLIC_*`, Git or chat. EAS cloud builds are optional; a local native build remains valid if the plan supports it. Do not run `expo prebuild` or modify generated `apps/universal/android/` as maintained source unless a later approved plan changes CNG ownership.

## Common failures and next checks

| Symptom | Check/fix |
| --- | --- |
| `pnpm: command not found` | Install via official pnpm guide and reopen shell; verify `pnpm --version` before 0A. |
| Wrong Node after installing | Check `which node` and `node --version`; align shell/version manager with 0A's `.node-version`. |
| Docker socket denied / daemon unreachable | Check `docker info`, service status and documented group/`sudo` route. Do not change daemon permissions casually. |
| DB readiness fails | After 0D, confirm isolated container health, correct private local `DATABASE_URL` and applied migrations; never print the URL/password. |
| Playwright browser missing | After 0F, install browser binaries using the pinned Playwright package's documented command; record browser versions. |
| Gradle/JDK error | Compare selected Gradle/AGP requirement with `java -version` and `JAVA_HOME`; use one compatible JDK in IDE and terminal. |
| `adb` missing or device unauthorized | Confirm `ANDROID_HOME`/`PATH`, SDK Platform Tools, cable/udev and phone prompt. |
| Android app cannot reach API | Use the tested LAN/emulator origin from the part's public config; check firewall and API bind interface; do not assume device `localhost`. |
| Expo/native version mismatch | Rebuild installed app after native dependency changes; compare selected Expo SDK and lockfile. Do not use Expo Go as a SQLCipher/plugin test. |

## Alternative operating systems

For macOS or Windows, keep the same repo/phase gates but use each vendor's official install instructions for Node, pnpm, Docker, VS Code, Android Studio and platform tools. On Windows, use a deliberate Windows or WSL2 workflow and verify how ADB reaches the device; avoid mixing two independent Node/Android SDK installations. Actual Safari testing requires macOS/iOS access. Record OS and tool versions in the relevant part's evidence.
