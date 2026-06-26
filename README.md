# Knowledge Stack

> My personal **tech-stack registry and architecture playbook** — the shared "house style" that Claude, Claude Code, and any other agent should read before building anything across my projects.

The tech registry says *what tools* I reach for. The patterns catalog says *how I assemble them*. Together they let an agent start aligned with my preferences instead of guessing a stack or introducing something new without asking.

---

## What this is

A single source of truth, version-controlled and pulled into every project, that tells an agent:

- which technologies are safe to use freely vs. need a conversation first,
- the recurring architectures ("house patterns") I build with, and how to build each one,
- the rules for proposing and recording anything new.

## Why it exists — context engineering

Andrej Karpathy calls **context engineering** *"the delicate art and science of filling the context window with just the right information for the next step."* This repo is exactly that artifact: a curated, high-signal slice of context so an agent spends its budget on the task — not on rediscovering my preferences or hallucinating a stack.

The full, Karpathy-grounded principles + the do/don't checklist live in **[AGENTS.md](AGENTS.md)**.

## What's inside

| File | Purpose |
|------|---------|
| **[KNOWLEDGE_STACK.md](KNOWLEDGE_STACK.md)** | The registry: Known & Comfortable tools, Learning / Recently Added, Proposed / Pending, Avoid — plus the **Design Patterns** catalog |
| **[PATTERNS.md](PATTERNS.md)** | Build playbooks: how to actually wire up each design pattern (problem, stack, steps, reference repo, gotchas) |
| **[AGENTS.md](AGENTS.md)** | The operating contract for agents: prompting principles + the do/don't checklist |
| **README.md** | You are here — orientation |

## How agents use it (short version)

**Principles** (full version in [AGENTS.md](AGENTS.md)):

- **Context engineering** — use what's curated here; don't re-derive my stack.
- **Keep it on the leash** — if it isn't listed, stop and ask; never introduce tech silently.
- **Match autonomy to the task** — small, reversible steps; verify as you go.
- **Be explicit** — name the tool or pattern you're using and why.

**The checklist (the contract):**

1. Before introducing any library, framework, pattern, or service → **check [KNOWLEDGE_STACK.md](KNOWLEDGE_STACK.md)**.
2. **Known & Comfortable** → use freely. **Learning** → light guidance. **Not listed** → explain what it is, why it fits, key tradeoffs, and **ask first**.
3. For anything architectural → prefer a pattern from the **Design Patterns** catalog ([build guides](PATTERNS.md)); propose a new one only with justification.
4. On approval → append **one distinct entry** to *Learning / Recently Added* (date, project, what / why / tradeoffs), then **commit + push** so every session stays in sync.

## How it's wired into my projects

- My global `~/.claude/CLAUDE.md` points every Claude Code session at `KNOWLEDGE_STACK.md`.
- Each project's `CLAUDE.md` references the raw file:
  `https://raw.githubusercontent.com/camerongamble36/knowledge-stack/main/KNOWLEDGE_STACK.md`
- **Discovery chain:** `CLAUDE.md → KNOWLEDGE_STACK.md → AGENTS.md / PATTERNS.md`. The registry links onward, so even an agent that only loads `KNOWLEDGE_STACK.md` finds its way to the operating contract and the build guides.

> Files are only read when something points an agent to them. That's why the must-follow rules live in `KNOWLEDGE_STACK.md` (the guaranteed-read file) and this README (the GitHub front door), with `AGENTS.md` / `PATTERNS.md` linked from both.

## Maintaining it (for humans)

- Adopted a new tool? Add it to **Learning / Recently Added**; promote to **Known & Comfortable** once it's second nature.
- New architecture worth repeating? Add a bullet to the **Design Patterns** catalog and a playbook to **[PATTERNS.md](PATTERNS.md)**.
- Keep it high-signal: prune trivial utilities; tech that's only *planned* goes under **Proposed / Pending**, not Known.

## Provenance

The technology entries and the pattern catalog were derived from a sweep of 13 active projects (June 2026). The prompting principles are summarized from Karpathy's "context engineering" note and his 2025 talk *Software Is Changing (Again)* — sources cited in [AGENTS.md](AGENTS.md).
