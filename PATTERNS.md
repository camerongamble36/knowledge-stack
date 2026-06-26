# PATTERNS.md — Build Playbooks

> How to build each pattern in the **[Design Patterns catalog](KNOWLEDGE_STACK.md)**. Every playbook follows the same template: **Problem & when to use** → **Stack** → **How to build it** → **Reference implementation** (in my repos) → **Gotchas / tradeoffs**. Prefer these for anything architectural; see **[AGENTS.md](AGENTS.md)** for the operating contract.

**Catalog**

Backend / API — [1. BFF and Domain-API split](#1-bff-and-domain-api-split) · [2. Layered NestJS service](#2-layered-nestjs-service) · [3. Repository over raw-SQL migrations](#3-repository-over-raw-sql-migrations) · [4. Firebase-Functions-hosted NestJS](#4-firebase-functions-hosted-nestjs) · [5. Versioned ingestion pipeline](#5-versioned-ingestion-pipeline)

Auth / security — [6. HMAC-signed stateless tokens](#6-hmac-signed-stateless-tokens) · [7. Internal API-key guard](#7-internal-api-key-guard) · [8. On-device end-to-end encryption](#8-on-device-end-to-end-encryption)

Mobile / data — [9. Flutter clean-layered with Riverpod](#9-flutter-clean-layered-with-riverpod) · [10. Offline-first local-SQLite source of truth](#10-offline-first-local-sqlite-source-of-truth)

Cross-cutting — [11. Cross-platform design tokens](#11-cross-platform-design-tokens) · [12. Monorepo with shared schema package](#12-monorepo-with-shared-schema-package) · [13. Forced tool-use for structured LLM output](#13-forced-tool-use-for-structured-llm-output)

---

## 1. BFF and Domain-API split

**Problem & when to use** — You want a hard secret/privacy boundary and a clean split between presentation and domain logic. The browser talks only to your own origin; secrets (DB service-role key, LLM keys, token secret) never reach the client. Use when an app has meaningful server-side secrets or a domain API worth reusing across clients. Skip for static/marketing sites.

**Stack** — Next.js App Router (route handlers as the BFF) · NestJS domain API · Supabase Postgres · internal API key (pattern 7) · Vercel (web) + Fly.io (api).

**How to build it**
1. Two deployables: `web/` (Next.js) renders UI and exposes `/api/*` route handlers; `web-api/` (NestJS) owns **all** DB access, business rules, and secrets.
2. The browser calls only same-origin `/api/*`. Those handlers call the Nest API **server-to-server** — never from the client.
3. Authenticate the BFF→API hop with an internal API key (pattern 7); authenticate end users at the BFF (Supabase Auth or HMAC tokens).
4. Share DTOs/types via one package (pattern 12) so both sides agree.
5. Deploy web to Vercel and the API to Fly.io; co-locate the API's region with Supabase.

**Reference implementation** — `lobbi`: `web/` (App Router + `proxy.ts` gating `/admin`), `web-api/` (Nest), `packages/shared` (Zod). Planned identically in `chorus`.

**Gotchas / tradeoffs** — Two deploys plus an extra network hop. The API must not be usable without the internal key. Worth it for the secret boundary and reusability; overkill for tiny apps.

---

## 2. Layered NestJS service

**Problem & when to use** — Keep HTTP concerns, business logic, and data access separate so each is independently testable and swappable. Use for any non-trivial Nest API.

**Stack** — NestJS · class-validator / class-transformer (or Zod) · @nestjs/swagger · Helmet · @nestjs/throttler.

**How to build it**
1. One **module** per domain concept (sessions, studios, restaurants…).
2. **Controller** = HTTP only: route, validate the DTO, call a service, shape the response. No business logic.
3. **Service** = business rules; depends on repositories via DI; no HTTP, no SQL.
4. **Repository** = data access only (supabase-js query builder or SQL); returns typed rows.
5. Cross-cutting: global validation pipe, Helmet, throttler, Swagger docs.
6. Unit-test services with mocked repositories; e2e-test controllers with Supertest.

**Reference implementation** — `lobbi/web-api`, `michelin-map` web-api (`v1/app/...`), `yogicam/web-api`, the `canvas` APIs.

**Gotchas / tradeoffs** — Don't let logic leak into controllers or SQL into services. A module that keeps growing is a signal to split it.

---

## 3. Repository over raw-SQL migrations

**Problem & when to use** — You want full control of the Postgres schema and queries without an ORM's abstraction or lock-in. Use when the schema is hand-designed and you value explicit SQL + RLS.

**Stack** — Supabase Postgres · @supabase/supabase-js (service-role) · versioned `.sql` migration files.

**How to build it**
1. Keep numbered migrations (`0001_init.sql`, `0002_scheduling.sql`, …) in `web-api/src/db/migrations/`; apply in order through one canonical path.
2. Define RLS policies in SQL. The API uses the service-role key (RLS-bypassing) and enforces access in guards/code.
3. Wrap each table in a repository class using the supabase-js query builder (`.from().select().eq()`); return typed rows.
4. Validate inputs/outputs with Zod from the shared package.
5. Migrations are the schema's source of truth — review them like code.

**Reference implementation** — `lobbi/web-api/src/db/migrations`; `community-reflection-platform` (repositories + `TokensService`).

**Gotchas / tradeoffs** — You own migration ordering and rollbacks (no ORM safety net). The service-role key bypasses RLS, so authorization **must** be enforced in code. Keep a single apply path to avoid drift.

---

## 4. Firebase-Functions-hosted NestJS

**Problem & when to use** — You want a NestJS API but prefer Firebase/GCP serverless hosting (and Firebase Hosting for the web). Use when you're already in the Firebase ecosystem (RTDB / Firestore / Auth).

**Stack** — NestJS · firebase-functions (v2) · Express adapter · Firebase Hosting (`frameworksBackend`) · multi-env Firebase projects.

**How to build it**
1. Build the Nest app normally, but instead of `app.listen()`, instantiate it over an Express instance and export it as an `onRequest` Cloud Function.
2. Use `onSchedule` (or Cloud Scheduler) for cron work.
3. Pin the Node runtime in `engines`; configure `firebase.json` (functions + hosting `frameworksBackend`).
4. Multi-env: separate Firebase projects (dev / beta / prod) via `.firebaserc` + `.env.{development,beta,production}`; deploy per env in CI.
5. Deploy the web app via Firebase Hosting frameworks support: `firebase deploy --only hosting`.

**Reference implementation** — `canvas` (web / music / messaging APIs), `michelin-map`, `yogicam`, `form-api`.

**Gotchas / tradeoffs** — Cold starts and function timeout limits; the Express wrap has minor Nest-lifecycle nuances. Watch per-env config drift — and keep deployment docs honest (yogicam's README once claimed Vercel while it actually deploys here).

---

## 5. Versioned ingestion pipeline

**Problem & when to use** — You ingest external or scraped data on a schedule and need it normalized, enriched, and reconciled into a canonical store. Use for ETL / data-sync features.

**Stack** — NestJS (`@nestjs/schedule` or Cloud Scheduler) · source adapters · parser · normalizer · enrichment client (e.g., Google Places) · reconciler · Firestore/Postgres canonical repo.

**How to build it**
1. Version the pipeline (`v1/`) so it can evolve without breaking history.
2. Build stages as discrete, testable units: **source-adapter** (fetch raw — scrape / CSV / API) → **parser** (raw → structured) → **normalizer** (canonical shape) → **enrichment** (augment via external API) → **reconciler** (merge vs. existing canonical, dedupe) → **repository** (persist).
3. Record each run (e.g., an `ingestion_runs` report) for observability.
4. Trigger on a schedule (weekly cron); make every stage idempotent.
5. Unit-test each stage against fixtures.

**Reference implementation** — `michelin-map/web-api/.../v1/app/scraping`: `guide.michelin.com` → Google Places enrichment → Firestore canonical repo, on a weekly Cloud Scheduler trigger.

**Gotchas / tradeoffs** — Scrapers are fragile to source changes — isolate that risk in the adapter. Keep reconciliation deterministic. Rate-limit enrichment APIs.

---

## 6. HMAC-signed stateless tokens

**Problem & when to use** — You need shareable or anonymous access (QR links, participant/teacher tokens) without sessions or a JWT library, and the server should verify without storing per-token state. Capability-link style.

**Stack** — Node's built-in `crypto` (HMAC-SHA256, `timingSafeEqual`) · a server-side `TOKEN_SECRET`.

**How to build it**
1. Define a typed payload (e.g., `{ studioId, role, exp }`), validated with Zod.
2. Token = `base64url(payload) + "." + base64url(HMAC_SHA256(payload, TOKEN_SECRET))`.
3. To verify: recompute the HMAC and compare with `timingSafeEqual` (constant-time), then check `exp`. Never trust the body before verifying the signature.
4. Mint tokens **server-side only**; clients never see `TOKEN_SECRET`.
5. Centralize sign/verify in a `TokensService` consumed by guards.

**Reference implementation** — `lobbi` & `community-reflection-platform` `TokensService`; planned in `chorus` (signed unlock tokens).

**Gotchas / tradeoffs** — Rotating `TOKEN_SECRET` invalidates all outstanding tokens — plan rotation. No revocation without extra state. Always constant-time compare; always validate `exp`.

---

## 7. Internal API-key guard

**Problem & when to use** — Lock down service-to-service calls (BFF → domain API, or mobile → API) so the API isn't usable by arbitrary callers. Pairs with pattern 1.

**Stack** — NestJS guard · a shared secret (`INTERNAL_API_KEY` via `x-internal-key`, or `x-api-key`).

**How to build it**
1. The caller (Next BFF or mobile app) sends `x-internal-key: <secret>` on every request.
2. A Nest guard checks the header against the env secret with a constant-time compare; reject otherwise.
3. Apply it globally (or per-controller) on the domain API.
4. Use distinct keys per caller where useful (e.g., `WEB_API_KEY`, `MUSIC_API_KEY`).

**Reference implementation** — `lobbi` (Next → Nest), `canvas` (mobile → APIs), `michelin-map`, `yogicam`.

**Gotchas / tradeoffs** — This is a shared secret, **not** user auth — combine with Supabase/Firebase auth for end-user identity. The key lives only in server env, never in the browser. Rotate on leak.

---

## 8. On-device end-to-end encryption

**Problem & when to use** — Privacy-first apps where the server must **never** see plaintext (journals, health, private notes), yet you still need sync/backup. 

**Stack** — `encrypt` + `pointycastle` (Dart) · AES-256-GCM · PBKDF2 / HKDF key derivation · flutter_secure_storage · server stores ciphertext blobs only.

**How to build it**
1. Derive a content key from a user secret (passphrase, or a biometric-unlocked key) via PBKDF2; derive per-purpose subkeys with HKDF.
2. Encrypt content client-side with AES-256-GCM — a **unique nonce per blob**; store nonce + auth tag alongside the ciphertext.
3. Keep keys in `flutter_secure_storage` (Keychain / Keystore); never transmit them.
4. Upload only ciphertext to Supabase Storage/Postgres, namespaced per user (`/{user_id}/{type}/{id}.enc`).
5. If the server must process content, hand it a **one-time** key over mutual TLS, decrypt in-heap, then purge.

**Reference implementation** — `chapters`: encrypted journal via `encrypt` + `pointycastle`; server-side AES-GCM decrypt-then-purge using HKDF-derived one-time keys over an mTLS job-key protocol.

**Gotchas / tradeoffs** — Key loss = data loss (no server recovery) — design recovery deliberately. GCM **nonce reuse is catastrophic** — never reuse. Crypto is easy to get subtly wrong; keep it in one small, audited module.

---

## 9. Flutter clean-layered with Riverpod

**Problem & when to use** — Any non-trivial Flutter app that needs testable state and a clear data path.

**Stack** — Drift (SQLite) · a repository/service layer · Riverpod (flutter_riverpod) · go_router · build_runner codegen.

**How to build it**
1. **DB:** Drift tables + DAOs; generate code with `build_runner`.
2. **Repository / Service:** wrap DAOs and remote clients; expose domain methods; no widgets here.
3. **Providers:** Riverpod providers expose services and state (`AsyncNotifier` / `Notifier`); share a `ProviderContainer` between app and tests.
4. **UI:** widgets watch providers; no business logic in widgets.
5. **Routing:** go_router for declarative navigation.
6. Test with an in-memory Drift DB and `ProviderContainer` overrides.

**Reference implementation** — `genesis`, `chapters`, `everyday-todo-list` (and the timers app).

**Gotchas / tradeoffs** — Mind Drift's codegen quirks (e.g., aliasing its `Timer` data class to avoid clashing with `dart:async`); keep `*.g.dart` generated. Don't reach into the DB from widgets. Riverpod provider scoping matters for tests.

---

## 10. Offline-first local-SQLite source of truth

**Problem & when to use** — The app must work fully offline and sync when online, with the **local** DB authoritative. Productivity / journal apps.

**Stack** — Drift (local SQLite, authoritative) · PowerSync (self-hosted on Fly.io) ↔ Supabase Postgres · drift_sqlite_async · RLS-bucketed sync.

**How to build it**
1. The local Drift DB is the source of truth; UI reads/writes locally and stays responsive offline.
2. PowerSync streams changes between local SQLite and Supabase Postgres; bridge it to Drift with `drift_sqlite_async`.
3. Define sync rules bucketed by `user_id`; enforce RLS in Postgres; a Supabase JWT authorizes downloads.
4. Direct uploads under RLS via a PowerSync `BackendConnector` (PostgREST).
5. For ordering/reorder, use fractional indexing (LexoRank-style `order_key`) for O(1) moves.
6. Self-host PowerSync in Docker on Fly.io.

**Reference implementation** — `everyday-todo-list`: Drift + self-hosted PowerSync ↔ Supabase; partial in `chapters`.

**Gotchas / tradeoffs** — Conflict policy must be explicit. Self-hosting PowerSync is ops you own. Use local at-rest encryption (PowerSync v2) if the data is sensitive.

---

## 11. Cross-platform design tokens

**Problem & when to use** — You ship web **and** Flutter and want one source of truth for color/spacing/type so the platforms can't drift. Any multi-platform product with a design system.

**Stack** — DTCG token JSON · Style Dictionary v4 · culori (OKLCH) · outputs: CSS variables + a Tailwind preset + Flutter Dart · published as a package (GitHub Packages).

**How to build it**
1. Author tokens once as DTCG JSON (primitives + semantics).
2. Generate perceptually-even ramps with culori (OKLCH), pinning brand anchors.
3. Compile with Style Dictionary to three outputs: CSS variables, a Tailwind preset, and Flutter Dart (e.g., a `DsColors` class).
4. Publish a versioned package (e.g., `@camerongamble36/canvas-design`) to GitHub Packages; consume it in web (Tailwind preset) and Flutter (generated Dart via a `canvas_tokens` package).
5. Layer app-specific tokens as a Flutter `ThemeExtension` on top.

**Reference implementation** — `canvas/design-system` (source of truth) → consumed by `genesis` (`canvas_tokens`) and `chapters` (build-time token generation).

**Gotchas / tradeoffs** — Adds a build step before platforms can consume tokens. Keep generation deterministic. Decide path-dep vs. git-dep vs. published-package per consumer (genesis currently uses a path dep).

---

## 12. Monorepo with shared schema package

**Problem & when to use** — Web and API (or app and API) must agree on types and validation. Use to kill drift between client and server contracts.

**Stack** — npm workspaces · a shared package exporting Zod schemas + inferred types (`@crp/shared`) · (or parallel Dart/TS model packages).

**How to build it**
1. `packages/shared` exports a Zod schema and `z.infer` type for every cross-boundary DTO.
2. Both web and API import from it and validate at **every** boundary with the same schema.
3. Use Zod for env parsing too.
4. Wire it with npm workspaces (`packages/*`, `web`, `web-api`); run web + API together in dev with `concurrently`.
5. For Flutter + TS stacks, keep parallel model packages in lockstep.

**Reference implementation** — `lobbi` & `community-reflection-platform` (`@crp/shared`, Zod); `yogaflow` (parallel `yogaflow-models` in Dart + TS).

**Gotchas / tradeoffs** — Parallel Dart/TS models can drift — a single Zod source is better when both sides are TS. Version the shared package carefully inside the monorepo.

---

## 13. Forced tool-use for structured LLM output

**Problem & when to use** — You need reliable **typed JSON** from Claude (not free text) for a product feature. Any LLM call whose output you parse programmatically.

**Stack** — Anthropic Claude Messages API · forced tool-use (`tool_choice`) · Zod validation · Promptfoo evals.

**How to build it**
1. Define the desired output as a tool / JSON schema.
2. Call the Messages API with that tool and **force** it (`tool_choice` set to the tool) so the model must return arguments matching the schema.
3. Validate the returned arguments with Zod before use; retry on mismatch.
4. Keep prompt templates in code and reuse the **same** templates in Promptfoo evals to test tone/values + structured-output correctness, graded by Claude.
5. Gate the feature on `ANTHROPIC_API_KEY`; keep it opt-in.

**Reference implementation** — `lobbi` (admin authoring assist — Suggest/Refine via forced tool-use, with Promptfoo evals); `yogicam` (Sanskrit/English asana-name translation).

**Gotchas / tradeoffs** — An over-complex schema causes more refusals/retries — keep it tight. Always validate output. Version prompts so evals catch regressions.
