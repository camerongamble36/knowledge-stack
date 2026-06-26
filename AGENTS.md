# AGENTS.md — Operating Contract

> If you are an AI agent (Claude Code or otherwise) working in this repo, or in any project that references it, **read this first.** It tells you *how to think* and *what to do*. The canonical data lives in **[KNOWLEDGE_STACK.md](KNOWLEDGE_STACK.md)**; the pattern build-guides in **[PATTERNS.md](PATTERNS.md)**.

## TL;DR

- **Check** `KNOWLEDGE_STACK.md` before introducing any tool. Not listed → **ask first**.
- **Reuse** the documented Design Patterns; don't invent architecture silently.
- When something new is approved, **record one distinct entry** and **commit + push**.

---

## Principles — the *why*

Grounded in Andrej Karpathy's framing of working with LLMs. Each principle is followed by what it means **here**.

### 1. Context engineering

> *"Context engineering is the delicate art and science of filling the context window with just the right information for the next step."* — Karpathy

**Here:** this repo **is** your curated context. Read it before building; don't burn context re-deriving my stack or guessing conventions. Pull in exactly the relevant registry entries and patterns — and nothing you don't need.

### 2. Keep it on the leash

Karpathy warns against over-delegating to unsupervised agents; vague instructions produce wrong output. **Here:** if a tool, library, pattern, or service **isn't listed**, *stop*. Explain what it is, why it fits, and the key tradeoffs versus alternatives I already use — then ask before writing code that depends on it. **Never silently introduce** a new dependency, pattern, or service.

### 3. Match autonomy to the task (the "autonomy slider")

Tune how much you do per step to the complexity and risk of the change. Prefer the **smallest reversible change** that moves the task forward; check in at the boundaries of anything consequential.

### 4. Small chunks, fast verify loop

Karpathy: keep changes small and concrete — the bottleneck is now *reviewing* output, not typing it. **Here:** make one focused change, **verify it** (build / test / run), then continue. Don't stack a dozen unverified changes.

### 5. Be explicit

English is the interface. Name the tool or pattern you're using and the reason, in proposals, commit messages, and PR descriptions. Precise instructions in → predictable output out.

---

## The operating checklist — the *what*

Before introducing **any** library, framework, pattern, or service:

1. **Check [KNOWLEDGE_STACK.md](KNOWLEDGE_STACK.md).**
   - In **Known & Comfortable** → use freely, no explanation needed.
   - In **Learning / Recently Added** → acknowledge it's newer; proceed with light guidance.
   - In **Proposed / Pending** → not greenlit; treat as "ask first."
   - In **Avoid** → don't, absent a strong explicit reason.
   - **Not listed** → pause; explain what / why / tradeoffs; ask before depending on it.
2. **Prefer an existing pattern.** For anything architectural, consult the **Design Patterns** catalog and **[PATTERNS.md](PATTERNS.md)**, and follow the established shape. Propose a *new* pattern only with justification.
3. **When approved, record it.** Append **one distinct entry** to *Learning / Recently Added* (date, project, what / why / tradeoffs). Don't duplicate an existing entry. Keep it high-signal — skip trivial utilities. Tech that's only *planned* goes under **Proposed / Pending**, not Known.
4. **Sync.** Commit and push so every session and project sees the update. If you might be on a different machine or a parallel session, **pull first**.

### Do / Don't

**Do:** check before reaching for tech · reuse documented patterns · record approvals · commit + push · keep entries terse and accurate.

**Don't:** silently add tech · duplicate entries · bloat the registry with trivial libraries · mark *planned* tech as "Known" · refactor a project onto a new pattern without asking.

---

## Sources

So this is grounded, not invented — these principles are summarized *in the spirit of* Karpathy's public work, adapted to this repo:

- Karpathy on **context engineering** — <https://x.com/karpathy/status/1937902205765607626>
- **Software Is Changing (Again)**, YC AI Startup School, June 2025 — "keep AI on the leash," the autonomy slider, and the small-chunks generation→verification loop.
