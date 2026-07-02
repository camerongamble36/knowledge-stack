# KNOWLEDGE_STACK.md
> My personal tech stack registry for Claude and Claude Code sessions.
> **Rule:** If a technology is in "Known & Comfortable", use it freely. If it's unlisted or unfamiliar, explain it before using it — what it is, why it fits, and key tradeoffs — then ask before proceeding. If approved, add it to "Learning / Recently Added" with a date and context note.
>
> **Agents:** read [AGENTS.md](AGENTS.md) for the full operating contract + prompting principles, [PATTERNS.md](PATTERNS.md) for how to build the patterns below, and [README](README.md) for orientation.

---

## 📋 How to Use This File (for Claude / Claude Code)

1. **Before introducing any library, framework, pattern, or service**, check this file.
2. If it's in **Known & Comfortable** → proceed without explanation.
3. If it's in **Learning / Recently Added** → briefly acknowledge it's new to me and proceed with light guidance.
4. If it's **not listed** → pause, explain it, justify it, and ask for approval before writing code that depends on it.
5. After approval → **append it to the Learning section** with today's date, the project context, and a one-line rationale.

---

## ✅ Known & Comfortable

### Languages
- **C# / .NET** — OOP, async/await, LINQ, API design, GC behavior, error handling, generics
- **TypeScript / JavaScript** — typing patterns, async patterns, ES modules, DOM
- **Python** — scripting, basic OOP; note: not deeply proficient in advanced Python patterns
- **Dart / Flutter** — widget tree, state management, cross-platform mobile, platform channels
- **SQL** — raw queries, joins, migrations, indexes
- **Swift** — native iOS/watchOS development (SwiftUI, WatchKit, Combine, Observation); YogaFlow watch app

### Frontend
- **React** — functional components, hooks (useState, useEffect, useContext), component composition
- **Next.js (App Router)** — file-based routing, server/client components, layout patterns
- **HTML / CSS** — semantic markup, flexbox, grid, responsive design
- **Tailwind CSS** — utility-first styling, responsive modifiers
- **Three.js** — 3D scene setup, meshes, cameras, lighting, basic geometry
- **GSAP** — timeline animations, scroll triggers, easing
- **Howler.js** — web audio, sound management
- **Shadcn** - A set of beautifully designed components that you can customize, extend, and build on. The foundation of beautiful design system components
- **React Bits** - UI Component Framework for building beautiful custom components, built on top of shadcn
- **Aceternity UI** - UI Component Framework for building beautiful custom components, , built on top of shadcn
- **Magic UI** - UI Component Framework for building beautfiul custom components, built on top of shadcn
- **Framer Motion** (`motion`) — declarative React animation; calm, reduced-motion-aware micro-interactions
- **Headless UI** — unstyled, accessible React component primitives
- **Radix UI** — headless UI primitives (the base shadcn builds on)
- **Lucide / Heroicons / Font Awesome** — React/web icon sets
- **next-themes** — light/dark theme management for Next.js
- **next-intl** — i18n + locale routing for Next.js (en/de/es/fr/tr)
- **react-hook-form** (+ `@hookform/resolvers`) — form state & validation, paired with Zod
- **Flowbite / flowbite-react** — Tailwind component library
- **Recharts / ApexCharts** — React charting libraries
- **fl_chart** — Flutter charting (mood, stats, coverage)
- **clsx / tailwind-merge / class-variance-authority** — Tailwind class composition utilities
- **PWA** — installable, phone-first web apps (service workers, Web Push); Lobbi & Chorus

### Backend
- **FastAPI** — routing, dependency injection, Pydantic models, async endpoints
- **Node.js / Express** — REST APIs, middleware, routing
- **NestJS** — modules, controllers, services, dependency injection
- **.NET / ASP.NET** — controllers, middleware, DI container, minimal APIs
- **Firebase Cloud Functions** — serverless host for the NestJS APIs (Node 18–24)
- **NestJS modules** — `@nestjs/config`, `@nestjs/throttler` (rate limiting), `@nestjs/swagger` (OpenAPI), `@nestjs/schedule` (cron)
- **class-validator / class-transformer** — NestJS DTO validation & serialization
- **Zod** — schema validation + env parsing, shared across client & server (default validation layer)
- **Helmet** — HTTP security headers
- **Handlebars** — server-side templating (transactional emails)
- **Multer / Busboy** — multipart file-upload handling
- **PowerSync** — offline-first sync engine (local SQLite ↔ Supabase Postgres), self-hosted on Fly.io

### Mobile
- **.NET MAUI Blazor Hybrid** — component lifecycle, platform services, WebView bridge, Android/Windows targeting
- **Flutter** — widgets, Navigator, platform channels, state (Provider/Riverpod basics)
- **Material 3** — Flutter Material Design foundation
- **go_router** — declarative routing/navigation for Flutter
- **flutter_secure_storage** — encrypted Keychain/Keystore storage for keys & tokens
- **shared_preferences** — lightweight key-value local storage
- **flutter_local_notifications** (+ `timezone`) — scheduled local notifications
- **workmanager** — background task scheduling
- **just_audio / audioplayers / record** — audio playback & recording
- **video_player** — video playback
- **image_picker / file_picker / share_plus** — media & file pickers / sharing
- **cached_network_image** — network image loading with caching
- **google_fonts** — runtime Google Fonts in Flutter
- **permission_handler** — runtime permission requests
- **connectivity_plus / device_info_plus / sensors_plus / package_info_plus** — device & runtime info, sensors
- **flutter_blue_plus** — Bluetooth LE
- **flutter_dotenv** — env loading in Flutter

### GIS / Mapping
- **ArcGIS Runtime SDK** — offline map downloads, OAuth authentication, basemap sessions, pin/geofence management, native MapView + Blazor WebView hybrid architecture
- **Mapbox** (`mapbox_maps_flutter`) — map rendering, custom styles & geocoding
- **Google Maps / Places API** — place data, address autocomplete, venue enrichment
- **geolocator / geocoding / location** — device GPS & address↔coordinate conversion

### Databases & Storage
- **SQLite** — embedded DB, schema design, pragmas
- **Dapper** — micro-ORM, raw SQL mapping, typed queries
- **Firebase (Realtime Database)** — real-time sync, rules, client SDK
- **Firebase Hosting** — static/SPA deployment, custom domains
- **PostgreSQL** — relational DB via Supabase (RLS, raw-SQL migrations)
- **Drift** — type-safe Dart SQLite ORM; local-first source of truth (codegen via build_runner)
- **sqflite** — direct Flutter SQLite access
- **Cloud Firestore** — Firebase document database
- **Firebase Cloud Storage** — file/asset/blob storage
- **Redis** (Upstash, `ioredis`) — ephemeral / TTL key store
- **IndexedDB** — in-browser store for the hover-define extension (context/RAG)

### AI / LLM
- **Anthropic Claude API** — Messages API, system prompts, multi-turn conversations, tool use / function calling
- **Claude Code** — agentic CLI coding, CLAUDE.md patterns, subagent pipelines, FEATURES.md tracking
- **Prompt Engineering** — chain-of-thought, role prompting, structured output, XML tags, verification layers
- **CrewAI** — multi-agent orchestration (certified); role/task/crew patterns
- **yt-dlp** — YouTube/Instagram media download, transcript extraction, format handling
- **OpenAI API** — GPT-4o + embeddings (Node & Dart SDKs)
- **Voyage AI** — semantic embeddings (`voyage-3.5`)
- **flutter_gemma** — on-device LLM inference (Gemma/Qwen) for private summarization
- **RunwayML** — text/image → video generation
- **Promptfoo** — LLM eval framework (tone/values + structured-output, Claude-graded)

### DevOps & Infrastructure
- **Git / GitHub** — branching, PRs, Actions basics, submodules
- **Docker** — Dockerfiles, containers, basic compose
- **Firebase Hosting** — deploy pipeline, rewrites, caching
- **GitHub Actions** — CI/CD (lint, type-check, test, deploy) across web/api/mobile
- **Fly.io** — container hosting for NestJS APIs & sync services (Docker + fly.toml)
- **Vercel** — Next.js frontend hosting (Lobbi, Chorus)
- **Firebase CLI / Emulator Suite** — serverless deploy & local emulation
- **Supabase CLI** — linked-project config & versioned SQL migrations
- **Google Cloud Scheduler** — scheduled/cron HTTP jobs (ingestion, sync)
- **GitHub Packages** — private npm registry for `@camerongamble36/*` packages
- **RabbitMQ / AMQP** (`amqplib`) — message broker (canvas messaging-api)
- **Multi-environment pipelines** — dev / beta / production (Firebase & Supabase projects)

### Auth & APIs
- **OAuth 2.0** — authorization code flow, token refresh, PKCE
- **REST** — resource design, status codes, versioning conventions
- **Google Drive API** — file read/write, permissions, MCP integration
- **Supabase Auth** (+ `@supabase/ssr`) — email magic-link / OTP sign-in, JWT, RLS-based access
- **Firebase Authentication** (+ `firebase-admin`) — user/admin auth & server-side token verification
- **HMAC-signed stateless tokens** — hand-rolled signed access tokens via `node:crypto` (anonymous participant/teacher links)
- **google_sign_in** — Google OAuth on mobile
- **local_auth** — biometric / PIN unlock
- **mTLS** — mutual-TLS one-time job-key protocol for service-to-service auth
- **Internal API-key guards** — shared-secret service-to-service auth (`x-api-key` / `x-internal-key`)

### Testing
- **Jest** (+ `ts-jest`) — primary unit/e2e runner for Node, NestJS & Next.js
- **Supertest** — HTTP endpoint assertions (NestJS e2e)
- **Vitest** — fast unit tests (design-system React packages)
- **@testing-library/react** (+ `jest-dom`, `user-event`) — React component testing
- **Mocha / Chai / Sinon** — web unit & contract testing
- **flutter_test / integration_test** — Flutter unit, widget & integration tests
- **firebase-functions-test** — Firebase Functions test harness
- **XCTest / Swift Testing** — native watchOS unit & UI tests
- *(Playwright — already logged under Learning / Recently Added)*

### State Management
- **Riverpod** (`flutter_riverpod`, `riverpod_annotation`) — primary Flutter state & DI
- **Provider** — Flutter state / DI (canvas, michelin, yogicam)
- **get_it** — service locator / dependency injection (Flutter)
- *(React: hooks + Server Components; forms via react-hook-form — no external store)*

### Build & Tooling
- **build_runner** — Dart code-generation driver
- **drift_dev** — Drift database codegen
- **freezed / json_serializable** — Dart immutable models & JSON codegen
- **ESLint** — JS/TS linting (`eslint-config-next`, `typescript-eslint`)
- **Prettier** (+ `prettier-plugin-tailwindcss`) — formatting & Tailwind class ordering
- **flutter_lints** — Dart/Flutter lint ruleset
- **PostCSS / Autoprefixer** — CSS processing for Tailwind
- **npm workspaces** — monorepo management (Lobbi)
- **sharp / plaiceholder** — build-time image optimization & blur placeholders
- **flutter_launcher_icons / flutter_native_splash** — app icon & splash generation
- **Xcode** — native watchOS build system
- *(Style Dictionary & culori — already logged under Learning / Recently Added)*

### Security & Crypto
- **AES-256-GCM / PBKDF2 / HKDF** — on-device E2EE & key derivation via `encrypt` + `pointycastle` (Dart) and `node:crypto` (server) — Chapters' encrypted journal
- **flutter_secure_storage** — OS-keystore-backed secret storage (also listed under Mobile)

### Third-Party Services & Platforms
- **Supabase** — Postgres + Auth + Storage + Edge Functions (BaaS); the "house" backend for newer apps
- **Firebase / Google Cloud** — Auth, RTDB, Firestore, Storage, Functions, Hosting, Messaging, Scheduler
- **Stripe** — payments / checkout sessions & webhooks
- **Resend** — transactional & newsletter email
- **Mixpanel** — product analytics / event tracking
- **Spotify Web API** — playlists, song requests, play history
- **Twilio** — SMS messaging (raw REST)
- **MindBody API** — yoga class scheduling & booking sync
- **Trello API** — task automation
- **Upstash** — managed Redis (ephemeral keys)
- **Firebase Cloud Messaging (FCM)** — push notifications

---

## 🧩 Design Patterns

> Recurring "house" architectures I reach for, derived from my projects. The same rule applies: **prefer these for anything architectural**; propose a new pattern only with justification. **Build guides for each →** [PATTERNS.md](PATTERNS.md).

### Backend / API
- **BFF and Domain-API split** — Next.js App Router BFF ↔ separate NestJS domain API that owns DB + secrets _(lobbi, chorus)_ · [build](PATTERNS.md#1-bff-and-domain-api-split)
- **Layered NestJS service** — controllers → services → repositories, DTO validation at the edge _(lobbi, michelin, yogicam, canvas)_ · [build](PATTERNS.md#2-layered-nestjs-service)
- **Repository over raw-SQL migrations** — versioned hand-written SQL on Supabase Postgres, no ORM _(lobbi, community)_ · [build](PATTERNS.md#3-repository-over-raw-sql-migrations)
- **Firebase-Functions-hosted NestJS** — wrap a Nest app in `onRequest`, multi-env dev/beta/prod _(canvas, michelin, yogicam, form-api)_ · [build](PATTERNS.md#4-firebase-functions-hosted-nestjs)
- **Versioned ingestion pipeline** — adapter → parse → normalize → enrich → reconcile → canonical repo _(michelin)_ · [build](PATTERNS.md#5-versioned-ingestion-pipeline)

### Auth / Security
- **HMAC-signed stateless tokens** — `node:crypto` signed payloads for anonymous/link access, constant-time compare _(lobbi, community, chorus)_ · [build](PATTERNS.md#6-hmac-signed-stateless-tokens)
- **Internal API-key guard** — shared-secret service-to-service (Next ↔ Nest) _(lobbi, canvas, michelin, yogicam)_ · [build](PATTERNS.md#7-internal-api-key-guard)
- **On-device end-to-end encryption** — AES-256-GCM + PBKDF2/HKDF, keys in secure storage, server stores only ciphertext _(chapters)_ · [build](PATTERNS.md#8-on-device-end-to-end-encryption)

### Mobile / Data
- **Flutter clean-layered with Riverpod** — Drift → repository/service → providers → UI, codegen via build_runner _(genesis, chapters, everyday)_ · [build](PATTERNS.md#9-flutter-clean-layered-with-riverpod)
- **Offline-first local-SQLite source of truth** — Drift at-rest truth synced to Supabase via PowerSync _(everyday, chapters)_ · [build](PATTERNS.md#10-offline-first-local-sqlite-source-of-truth)

### Cross-cutting
- **Cross-platform design tokens** — DTCG JSON → Style Dictionary (+culori) → CSS/Tailwind/Dart from one source _(canvas, genesis, chapters)_ · [build](PATTERNS.md#11-cross-platform-design-tokens)
- **Monorepo with shared schema package** — one Zod schema/types package shared across web + api _(lobbi, community; parallel Dart/TS in yogaflow)_ · [build](PATTERNS.md#12-monorepo-with-shared-schema-package)
- **Forced tool-use for structured LLM output** — Claude Messages API forced-tool schema for typed JSON, prompts reused in Promptfoo evals _(lobbi, yogicam)_ · [build](PATTERNS.md#13-forced-tool-use-for-structured-llm-output)

---

## 📚 Learning / Recently Added

| Date | Technology | Project | What it is | Why chosen | Tradeoffs |
|------|-----------|---------|------------|------------|-----------|
| 2025-06 | **yt-dlp** | PantryOS | CLI/Python lib for downloading YouTube/Instagram media including metadata and transcripts | Best-in-class for media ingestion; handles auth, formats, subtitles | No official API; CLI-wrapper pattern can be fragile to version changes |
| 2025-06 | **WhisperKit** | Cues | On-device speech recognition for Apple Silicon using OpenAI Whisper models | Privacy-first, low-latency; enables interruption detection without server round-trip | Apple/iOS only; model size vs. accuracy tradeoff |
| 2026-06 | **Playwright** (`@playwright/test`) | Canvas (web) | Cross-browser end-to-end testing framework that drives real browsers | De-facto standard for modern web e2e; auto-wait, parallelism, trace viewer; same suite runs against deployed beta via `E2E_BASE_URL` | Heavier/slower than unit tests; browser binaries to install & manage |
| 2026-06 | **Style Dictionary** (v4) | Canvas (design-system) | Build tool that compiles design tokens (DTCG JSON) to multiple platform outputs | One token source → CSS vars + Tailwind preset + Flutter Dart; makes cross-platform drift structurally impossible | Custom-format learning curve; adds a build step before web/mobile consume tokens |
| 2026-06 | **url_launcher** (`^6.3.2`) | Genesis | Official Flutter team plugin to open URLs (browser/email/tel) on the host platform | Canonical, first-party, low-risk way to open the era charters' external Google-Doc links from the Documents screen | Some schemes need iOS `Info.plist` / Android `<queries>` entries; plain `https` opens work out of the box |
| 2026-06 | **flutter_markdown_plus** (`^1.0.7`) | Genesis | Community-maintained drop-in for the discontinued official `flutter_markdown`; renders Markdown to Flutter widgets (`MarkdownBody`, `onTapLink`) | Lets user-authored doc notes/revisions render as formatted Markdown; near-identical API to the well-documented original, with `onTapLink` wired to url_launcher | Official package is discontinued, so the successor ecosystem is fragmented; another render dep for currently-light P0 content |
| 2026-06 | **culori** | Canvas (design-system) | JS color library with OKLCH / perceptual color math + gamut mapping | Generate perceptually-even token ramps with brand anchors pinned; reliable OKLCH↔sRGB conversion | Large general-purpose lib for a narrow use; build-time dependency in the token generator |
| 2026-06-26 | **image_picker** (`^1.1.2`) + **firebase_storage** (`^13.4.2`) | yogicam (mobile admin) | First-party camera/gallery picker + Firebase Cloud Storage SDK | Wire resource image upload in the admin app: pick a photo → upload to `resources/<folder>/` → store the download URL (`ImageUploadField`); both already "Known & Comfortable", logged here for provenance | `firebase_storage` major must track the pinned `firebase_core 4.x` (12.x conflicts → 13.x); Storage rules must allow admin writes under `resources/**` or uploads 403 |
| 2026-07-01 | **Google Cloud Run** | michelin-map (menu-worker) | Serverless container platform on GCP (scale-to-zero, pay-per-use) — the same runtime that gen-2 Firebase Functions already use | Host the Playwright menu-fetch worker in the **same GCP project as Firebase**: cheaper than a 2nd platform (free tier covers the low volume), runtime service-account via ADC (no key file to ship), one bill/IAM/logs. Chosen over Fly.io (2nd provider) and over cramming Chromium into a Function (fragile) | Cold start on first request after scale-to-zero; a Dockerfile/container to maintain vs a plain Function; browser workloads want ≥1 GiB memory |
| 2026-07-01 | **google-github-actions/auth** (`@v2`) | yogicam (CI) | Official GitHub Action that authenticates a workflow to Google Cloud — writes the SA key (or WIF creds) and exports `GOOGLE_APPLICATION_CREDENTIALS` as ADC | Replaced a hand-rolled "write SA key + set `GOOGLE_APPLICATION_CREDENTIALS`" step that intermittently left `firebase deploy` throwing "Failed to authenticate"; the action provides ADC that firebase-tools reliably consumes (fixed dev + prod deploys) | Still key-file based (not workload identity), so a revoked/disabled per-env SA key still fails — the action writes it but firebase can't get a token (this is exactly what broke beta) |

---

## ❓ Proposed / Pending Approval

> Technologies Claude has suggested but I haven't greenlit yet. Cleared after decision.

| Technology | Project | What it is | Why proposed | Status |
|-----------|---------|------------|--------------|--------|
| **Cloudflare Stream** | Chorus | Video upload → transcode → adaptive HLS + thumbnails, with resumable (tus) direct browser uploads | Only new service the Chorus design needs; offloads the entire video pipeline | Planned — not yet wired (Chorus is pre-build) |

---

## 🚫 Avoid / Bad Experiences

> Patterns or tools I've tried and don't want re-introduced without a strong reason.

*(add as needed)*

---

## 🗂 Domain Index

| Domain | Key Technologies |
|--------|----------------|
| Full-Stack Web | React, Next.js, TypeScript, NestJS, Node/Express, FastAPI, Tailwind |
| Mobile | Flutter, Riverpod, Drift, go_router, .NET MAUI Blazor Hybrid, Swift/watchOS |
| GIS / Mapping | Mapbox, Google Maps/Places, ArcGIS Runtime SDK, geolocator |
| AI / Agents | Claude API, Claude Code, CrewAI, OpenAI, Voyage AI, flutter_gemma, Promptfoo, WhisperKit |
| Data & Sync | PostgreSQL/Supabase, Firebase RTDB/Firestore, SQLite/Drift, Redis, PowerSync |
| Backend-as-a-Service | Supabase, Firebase |
| DevOps / Hosting | Git/GitHub, GitHub Actions, Docker, Fly.io, Vercel, Firebase Hosting |
| Testing | Jest, Vitest, Playwright, flutter_test, XCTest, Promptfoo |
| Auth | Supabase Auth, Firebase Auth, OAuth 2.0, HMAC tokens, REST |
| Payments / Comms / Analytics | Stripe, Resend, Twilio, Mixpanel, Spotify, MindBody |

---

*Last updated: 2026-07-01 | Maintained by Cam + Claude (project-sweep audit across 13 repos)*
