# Environment and secret ownership

**Prepared:** 12 October 2026 (Asia/Dhaka). No environment examples, app manifests, real `.env` files or deployed services exist yet. [ARCHITECTURE.md](ARCHITECTURE.md) approves the **ownership and separation**, but does not prescribe most literal variable names. The names below are the proposed consistent registry for `apps/api/.env.example` (0D), `apps/universal/.env.example` (0E) and later infrastructure. The owning part must confirm each name against its code, saved plan and [test-command.md](test-command.md) before anyone copies an example. A changed name must be updated in all three guides and the part evidence. Nothing here authorizes account provisioning or creating secrets now.

**Now:** no application variable is needed for S0 or 0A. The owner installs toolchains and later supplies values. Do not paste a value into Git, chat, screenshots, logs or a test fixture. Agents do not read, reveal or edit private environment files without explicit owner authorization. All test data remains synthetic until the applicable gates close.

## Five different kinds of value

| Kind | Examples | Rule |
| --- | --- | --- |
| Public build-time client configuration | `EXPO_PUBLIC_API_URL`, `EXPO_PUBLIC_RELEASE_ID`, `EXPO_PUBLIC_FEATURE_AVAILABILITY` | Expo embeds these in web/Android outputs. Treat them as visible to anyone; use only URLs/identifiers/availability that may be published. They are built per environment and cannot be used for access control. |
| Private server runtime/migration configuration | `DATABASE_URL`, `DATABASE_MIGRATION_URL`, `BETTER_AUTH_SECRET`, provider credentials | Set only for `apps/api` or a protected migration/CI job; never expose through Expo, static assets, source maps or client logs. Use least privilege and separate migration credentials. |
| Local development secrets | Local database password/URL, test auth secret or mail capture credentials if configured | Use only in ignored local files or protected shell/secret storage. Local shortcuts and synthetic addresses cannot be copied to staging/production. |
| Android application identifier | `ANDROID_APPLICATION_ID` | Public, stable package identity selected at 0G for development and reviewed at 47 for distribution. It is not a credential or signing key. Avoid publishing a production ID before it is chosen. |
| Native signing credentials | Keystore path/passwords, Play upload credentials | Private, owner/CI protected, 47 only. They are not Expo public variables, app runtime config or repository files. |

## Local development (0D/0E and later)

`Required` means required **when that component is implemented/enabled**, not now. No exact port, domain or secret value is claimed. The local Compose service names/ports and API bind policy are fixed by 0D. `EXPO_PUBLIC_API_URL` must resolve from the actual browser and installed Android target; a phone's `localhost` is not the host computer.

| Exact proposed name | Status / consumer / visibility | Obtain and safe local default | Validate without exposing value / first needed / rotation |
| --- | --- | --- | --- |
| `EXPO_PUBLIC_API_URL` | Required for networked client; `apps/universal`; **public** | Use the 0D API origin reachable from the current target. No one URL works for every emulator/phone/browser; no default today. | 0E/0G: load public health route from each target and verify expected origin in build config. Change/rebuild per target when the API address changes. |
| `EXPO_PUBLIC_RELEASE_ID` | Required once artifact versioning exists; universal; **public** | Use the build's nonsecret version/commit identifier supplied by approved scripts, no fabricated default. | 0L/42: inspect artifact metadata; rebuild to rotate. Never put an access token here. |
| `EXPO_PUBLIC_FEATURE_AVAILABILITY` | Optional; universal; **public** | Only a validated public on/off availability descriptor after an owning feature exists; off by default. Not an authorization/consent mechanism. | 35/42: inspect bundled config and disabled fallback. Rebuild when changed. |
| `API_HOST` | Required for API process; server; public operational setting | 0D chooses loopback/container bind appropriate to the local topology; no default assumed. | 0D: check health only from intended interface; restart on change. |
| `API_PORT` | Required for API process; server; public operational setting | 0D chooses a free local port; no default assumed. | 0D: health/readiness probe, confirm it matches client URL; restart on change. |
| `DATABASE_URL` | Required for API runtime; server **confidential** | From 0D's isolated PostgreSQL Compose instance; runtime DB role, synthetic data only. No production value locally. | 0D: config presence check and readiness/real PG tests, with redacted failures. Rotate DB role/password and restart API; coordinate sessions. |
| `DATABASE_MIGRATION_URL` | Required for reviewed schema migrations; migration process **confidential** | Separate local migration role/connection created by 0D; use only for an approved migration command. | 0D: migration readiness/schema version on isolated DB; rotate independently of runtime URL. |
| `BETTER_AUTH_SECRET` | Required when Better Auth is configured; API **confidential** | Owner-generated high-entropy local secret under 0K/22 instructions; no value or generator is provided here. | 0K: startup validates presence/strength without printing it; test login/rotation/revocation. Rotate under a session invalidation plan. |
| `BETTER_AUTH_URL` | Required for Better Auth; API **public origin setting** | Exact API auth origin for this environment, chosen in 0K; no deployed URL today. | 0K: verification/recovery links and installed/web auth roundtrip; change with cookie/deep-link review. |
| `TRUSTED_WEB_ORIGINS` | Required for browser auth/mutations; API **public origin allowlist** | Explicit web origins, chosen in 0K. No wildcard or unrelated hosting domain assumption. | 0K: allowed same-site origin works; foreign Origin/CSRF request fails. Review on domain change. |
| `EMAIL_TRANSPORT` | Required when email flows are enabled; API operational setting | `capture` for local synthetic mail if 0D implements this mode; no external account. | 0D/0K: verification mail appears only in local capture; change/restart when transport changes. |
| `SMTP_HOST`, `SMTP_PORT` | Conditional if selected email adapter uses SMTP; API endpoint settings | From 0D local email-capture service or later approved provider; no port assumed. | 0D/22: synthetic delivery/timeout test; rotate endpoint with transport configuration. |
| `SMTP_USERNAME`, `SMTP_PASSWORD` | Optional for local capture, required if selected provider needs them; API **confidential** | Local capture may require none. Production provider values come later from its dashboard. | 22/42: presence and test delivery without logging; revoke/rotate at provider and update protected server store. |
| `EMAIL_FROM` | Conditional for email; API public sender identity | Local synthetic sender chosen in 0D; verified domain/sender only after O7 provider choice. | 22/42: inspect synthetic/approved mail headers; change after domain verification. |

`LOG_LEVEL` may be added by 0D as a nonsecret operational setting; its accepted values and default must be documented by the actual config schema. It never licenses logging health bodies, credentials or prompts. Do not infer unimplemented variables from a third-party library's examples.

## Testing and CI (0F onward)

Use isolated synthetic databases, distinct CI credentials and protected GitHub Actions environments. CI tests must never target production or copy real health data. The CI workflow creates its own ephemeral values when feasible; service credentials remain in GitHub's protected secrets, not workflow YAML. The exact scripts and terminal arrangement appear only after their owning part creates them.

| Name | Status / consumer / visibility | Source, validation and rotation |
| --- | --- | --- |
| `DATABASE_URL`, `DATABASE_MIGRATION_URL` | Required for real PostgreSQL API/migration tests; CI server jobs **confidential** | Point to the CI-only Postgres service and separate roles after 0D/0F. Validate test database identity before migration and rollback tests. Replace with each ephemeral run. |
| `BETTER_AUTH_SECRET` | Required for auth integration tests at 0K/22; CI **confidential** | Synthetic CI-only secret supplied by protected CI mechanism. Validate test sessions and rejection cases, never output it. Rotate when CI secret policy requires. |
| `EXPO_PUBLIC_API_URL`, `EXPO_PUBLIC_RELEASE_ID` | Required for web/Android test builds once configured; **public** | Use CI test API origin and synthetic build ID. Inspect generated public artifacts for accidental server values. Rebuild each environment. |
| `ANDROID_HOME`, `JAVA_HOME` | Required for 0G Android CI; machine paths, **not secrets** | CI runner's SDK/JDK installation. `adb version`, `java -version`, installed build/flow prove setup. Update with pinned toolchain. |

## Staging (42)

Only after O7 provider/domain/operator/budget approval. Give staging its **own** client build, API origin, database, keys, email test/sandbox identity, provider caps and backup target. Use the same variable names as local, with staging values kept in protected hosting/CI stores. Required staging set: `EXPO_PUBLIC_API_URL`, `EXPO_PUBLIC_RELEASE_ID`, `API_HOST`, `API_PORT`, `DATABASE_URL`, `DATABASE_MIGRATION_URL`, `BETTER_AUTH_SECRET`, `BETTER_AUTH_URL`, `TRUSTED_WEB_ORIGINS`, and the enabled email transport variables. `EXPO_PUBLIC_FEATURE_AVAILABILITY` stays off for unapproved features. Validate with staging-only health/readiness, synthetic auth, migration, allowed/denied Origin and public-bundle inspection. Rotate credentials independently from local/production; test restore and deletion suppression without production data.

## Website production (44)

The static Expo/Cloudflare artifact receives **only** `EXPO_PUBLIC_API_URL`, `EXPO_PUBLIC_RELEASE_ID` and optional `EXPO_PUBLIC_FEATURE_AVAILABILITY`, all public. The API URL must be the approved same-owned-site HTTPS API origin. Verify the built asset has no `DATABASE_URL`, `BETTER_AUTH_SECRET`, provider key, email secret or signing material; verify shell routing and no private API service-worker cache. A Cloudflare deploy token, if CI deployment uses one, is `CLOUDFLARE_API_TOKEN` in a protected **deploy job only**, not a web app variable. The owner obtains it from the chosen Cloudflare account under O7, scopes it to deployment, validates using a protected CI dry run, and revokes/rotates it in Cloudflare on compromise or workflow retirement. No Cloudflare account/token is mandatory for S0 or local development.

## Backend production (42/44)

The managed API/DB direction is O7-gated. Set `DATABASE_URL` for a least-privilege runtime role and `DATABASE_MIGRATION_URL` only for reviewed migration jobs; `BETTER_AUTH_SECRET`, `BETTER_AUTH_URL` and `TRUSTED_WEB_ORIGINS` for exact same-site auth; `API_HOST`/`API_PORT` as host requires; email transport settings from the approved provider; and separately approved provider settings below. All confidential values live in Render (if chosen) or equivalent protected environment/CI secret store. `RENDER_API_KEY`, if used for CI promotion, belongs only to a protected deploy job, is dashboard-issued, narrowly scoped, and rotated/revoked there. A dashboard's automatically injected port or URL is used only if the actual 42 config maps it to this registry. Never ship production secrets to `apps/universal` or commit them in `infra/render/render.yaml`.

| Later optional name | Owner gate / server consumer / source | Validation and rotation |
| --- | --- | --- |
| `FOOD_DATA_CENTRAL_API_KEY` | 33/O8; API food adapter; obtain under the provider's terms from the official FoodData Central account/key process. **Confidential**. | Test permitted catalog query, quota/outage and manual fallback; revoke/replace at provider, clear/update server cache as policy requires. No client copy. |
| `AI_PROVIDER`, `AI_MODEL` | 35/O8; API AI adapter; provider/model chosen only after terms, region, budget and benchmark approval. Operational identifiers; model availability is not assumed. | Validate provider selection, supported structured output, caps and fallback with synthetic inputs; change through reviewed provider config. |
| `AI_API_KEY` | 35/O8; API provider credential from the approved provider dashboard. **Confidential**. | Presence and synthetic allowed/denied/outage tests; rotate/revoke provider key and restart/deploy API. No real processing before consent/gate. |
| `AI_HARD_CAP` | 35/O8; API budget/kill-switch policy value, not a secret. | Its unit/period and exact bound must be approved in part plan; exercise cap exhaustion and manual/factual fallback. Do not invent a number here. |
| `BACKUP_DESTINATION`, `BACKUP_ENCRYPTION_KEY` | 31/O6/O7; server operations only, destination metadata and **confidential** key. | Independent backup and pre-deletion restore/suppression rehearsal; rotate key through a documented recoverability procedure, never discard the only decrypting key. No retention duration assumed. |

An approved provider adapter may use different official SDK variable names; its part must record an explicit mapping and update this registry. No email registration, OAuth provider, external AI API, FoodData Central key or paid plan is needed for manual guest logging or S0. Better Auth email/password is the approved account direction; OAuth is not an MVP prerequisite. Free provider allowances and limits may change and are **unverified here**; confirm actual eligibility, quotas, data terms and billing at O7/O8 instead of treating a free plan as permanent.

## Future Android configuration (0G development; 46/47 release)

| Name or protected item | Status / consumer / source | Validation / rotation |
| --- | --- | --- |
| `ANDROID_HOME`, `JAVA_HOME` | Required local/CI build-machine paths by 0G; owner installs SDK/JDK. Public machine configuration. | `adb version`, `java -version`, native build and installed smoke. Update to match selected Gradle/Expo toolchain. |
| `ANDROID_APPLICATION_ID` | Required at 0G, reviewed again at 47; public Android package identifier selected by owner/plan, represented in `apps/universal/app.config.ts`. | Inspect installed APK package identity and deep-link behavior; changing it creates a different app identity and needs migration/distribution review. |
| `EXPO_PUBLIC_API_URL`, `EXPO_PUBLIC_RELEASE_ID` | Required in Android artifact when network/versioned build is enabled; public. | Inspect built configuration and installed API reachability. Rebuild after changing. Do not use an emulator-only origin in release. |
| `ANDROID_KEYSTORE_PATH`, `ANDROID_KEYSTORE_PASSWORD`, `ANDROID_KEY_ALIAS`, `ANDROID_KEY_PASSWORD` | 47 only; protected local/CI signing input, **confidential** except alias may be nonsecret. Owner obtains/creates through approved signing process. | Check signed artifact with the approved release procedure. Store/recover/rotate under Android/Play key policy; never commit or pass to public Expo config. |
| Play distribution credential | 47 only if automated store upload is approved; protected CI credential with exact name selected by that plan. | Validate narrow upload permission and revoke in Play Console on retirement. No credential or account is required for 0G local smoke. |

## Environment file safety and manual checklist

Part 0A must create `.gitignore` before any real local file is made. At minimum ignore `**/.env`, `**/.env.*` while explicitly allowing only `**/.env.example`; ignore private keystores (`*.jks`, `*.keystore`), local key files, generated `apps/universal/android/`, build outputs, coverage and test results. Review exceptions carefully: `.env.example` has names/safe placeholders only. Keep separate `apps/api/.env.example` and `apps/universal/.env.example`; there is no root combined env file. Real local values belong in ignored component-specific files or an OS secret store, and staging/production values belong in their protected dashboards. CI YAML references secret names, not values. Before owner commits, check `git status --short` and `git check-ignore -v apps/api/.env apps/universal/.env` **after 0A and only if those local files exist**; expected: ignored. Do not run commands that print variable values to prove setup.

- [ ] S0: no app secrets created; record tool versions only.
- [ ] 0A: `.gitignore` and one pinned toolchain exist; owner confirms private-file ignore behavior.
- [ ] 0D/0E: copy examples only after creation; fill local values privately; verify API/clients with synthetic data.
- [ ] 0G: record public Android ID and machine SDK/JDK; keep signing credentials absent.
- [ ] 0K/22: verify auth secrets/origins and account isolation without logging values.
- [ ] O4/O6/O7/O8: record owner decisions before real data, hosted resources, retention or external processing.
- [ ] 42/44: distinct staging/production stores and URLs; inspect public artifacts; rehearse backup/restore before release.
- [ ] 47: owner protects signing and Play credentials outside Git; website publication already complete.
