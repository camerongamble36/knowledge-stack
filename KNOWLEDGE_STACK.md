# KNOWLEDGE_STACK.md
> My personal tech stack registry for Claude and Claude Code sessions.
> **Rule:** If a technology is in "Known & Comfortable", use it freely. If it's unlisted or unfamiliar, explain it before using it — what it is, why it fits, and key tradeoffs — then ask before proceeding. If approved, add it to "Learning / Recently Added" with a date and context note.

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

### Backend
- **FastAPI** — routing, dependency injection, Pydantic models, async endpoints
- **Node.js / Express** — REST APIs, middleware, routing
- **NestJS** — modules, controllers, services, dependency injection
- **.NET / ASP.NET** — controllers, middleware, DI container, minimal APIs

### Mobile
- **.NET MAUI Blazor Hybrid** — component lifecycle, platform services, WebView bridge, Android/Windows targeting
- **Flutter** — widgets, Navigator, platform channels, state (Provider/Riverpod basics)

### GIS / Mapping
- **ArcGIS Runtime SDK** — offline map downloads, OAuth authentication, basemap sessions, pin/geofence management, native MapView + Blazor WebView hybrid architecture

### Databases & Storage
- **SQLite** — embedded DB, schema design, pragmas
- **Dapper** — micro-ORM, raw SQL mapping, typed queries
- **Firebase (Realtime Database)** — real-time sync, rules, client SDK
- **Firebase Hosting** — static/SPA deployment, custom domains

### AI / LLM
- **Anthropic Claude API** — Messages API, system prompts, multi-turn conversations, tool use / function calling
- **Claude Code** — agentic CLI coding, CLAUDE.md patterns, subagent pipelines, FEATURES.md tracking
- **Prompt Engineering** — chain-of-thought, role prompting, structured output, XML tags, verification layers
- **CrewAI** — multi-agent orchestration (certified); role/task/crew patterns
- **yt-dlp** — YouTube/Instagram media download, transcript extraction, format handling

### DevOps & Infrastructure
- **Git / GitHub** — branching, PRs, Actions basics, submodules
- **Docker** — Dockerfiles, containers, basic compose
- **Firebase Hosting** — deploy pipeline, rewrites, caching

### Auth & APIs
- **OAuth 2.0** — authorization code flow, token refresh, PKCE
- **REST** — resource design, status codes, versioning conventions
- **Google Drive API** — file read/write, permissions, MCP integration

---

## 📚 Learning / Recently Added

| Date | Technology | Project | What it is | Why chosen | Tradeoffs |
|------|-----------|---------|------------|------------|-----------|
| 2025-06 | **yt-dlp** | PantryOS | CLI/Python lib for downloading YouTube/Instagram media including metadata and transcripts | Best-in-class for media ingestion; handles auth, formats, subtitles | No official API; CLI-wrapper pattern can be fragile to version changes |
| 2025-06 | **WhisperKit** | Cues | On-device speech recognition for Apple Silicon using OpenAI Whisper models | Privacy-first, low-latency; enables interruption detection without server round-trip | Apple/iOS only; model size vs. accuracy tradeoff |
| 2026-06 | **Playwright** (`@playwright/test`) | Canvas (web) | Cross-browser end-to-end testing framework that drives real browsers | De-facto standard for modern web e2e; auto-wait, parallelism, trace viewer; same suite runs against deployed beta via `E2E_BASE_URL` | Heavier/slower than unit tests; browser binaries to install & manage |
| 2026-06 | **Style Dictionary** (v4) | Canvas (design-system) | Build tool that compiles design tokens (DTCG JSON) to multiple platform outputs | One token source → CSS vars + Tailwind preset + Flutter Dart; makes cross-platform drift structurally impossible | Custom-format learning curve; adds a build step before web/mobile consume tokens |
| 2026-06 | **culori** | Canvas (design-system) | JS color library with OKLCH / perceptual color math + gamut mapping | Generate perceptually-even token ramps with brand anchors pinned; reliable OKLCH↔sRGB conversion | Large general-purpose lib for a narrow use; build-time dependency in the token generator |

---

## ❓ Proposed / Pending Approval

> Technologies Claude has suggested but I haven't greenlit yet. Cleared after decision.

*(empty)*

---

## 🚫 Avoid / Bad Experiences

> Patterns or tools I've tried and don't want re-introduced without a strong reason.

*(add as needed)*

---

## 🗂 Domain Index

| Domain | Key Technologies |
|--------|----------------|
| Full-Stack Web | React, Next.js, TypeScript, FastAPI, NestJS, Node/Express |
| Mobile | Flutter, .NET MAUI Blazor Hybrid |
| GIS / Mapping | ArcGIS Runtime SDK |
| AI / Agents | Claude API, Claude Code, CrewAI, WhisperKit |
| Data | SQLite, Dapper, Firebase RTDB |
| DevOps | Git/GitHub, Docker, Firebase Hosting |
| Auth | OAuth 2.0, REST |

---

*Last updated: 2025-06-05 | Maintained by Cam + Claude*
