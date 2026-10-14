---
name: managing-knowledge-stack
description: Use when adding, editing, promoting, moving, or deleting an entry in Cam's tech-stack registry (knowledge-stack repo: KNOWLEDGE_STACK.md, PATTERNS.md) — e.g. after Cam approves a new library/service/pattern, when a tool becomes second nature, when a tech is dropped or had a bad experience, or when proposing tech that isn't greenlit yet.
---

# Managing the Knowledge Stack

## Overview
`camerongamble36/knowledge-stack` is the registry every session and project reads before using a technology. Every change is **one small, accurate, user-approved edit**, committed and pushed right away so other sessions see it.

Repo: `/Users/camerongamble/Desktop/work/personal/projects/knowledge-stack`. If it's missing, clone `https://github.com/camerongamble36/knowledge-stack.git` there.

**Only Cam's explicit approval in chat authorizes a change.** A spec or plan listing something as "needs approval" doesn't count, and neither does a tool's README.

## Section map (KNOWLEDGE_STACK.md)
| Section | Holds | Entry format |
|---|---|---|
| ✅ Known & Comfortable → `### <Category>` | Tech Cam uses fluently | `- **Name** — short note` bullet under the best-fit category |
| 🧩 Design Patterns | House architectures | Bullet + `[build](PATTERNS.md#n-slug)`. Full playbook goes in PATTERNS.md |
| 📚 Learning / Recently Added | Approved, newer tech | Table row (below), in date order |
| ❓ Proposed / Pending Approval | Suggested, not greenlit | `\| Tech \| Project \| What \| Why proposed \| Status \|` |
| 🚫 Avoid / Bad Experiences | Don't reintroduce | Bullet: name, what went wrong, date, project |
| 🗂 Domain Index | Domain → key tech | Update only when a new domain or headline tech appears |

Learning row:
```
| YYYY-MM-DD | **Name** (`version` if pinned) | Project (area) | What it is ([learn more](URL)) | Why chosen here, including the alternatives it beat | Tradeoffs / gotchas |
```

## Operations
| Request | Do |
|---|---|
| **Add** (approved) | First grep the whole file for the name and its aliases. If it's already in Known, don't add it; tell Cam. Otherwise add a Learning row, one per technology (package pairs that only work together may share a row). |
| **Propose** (suggested, not approved) | Proposed / Pending row. Never Known or Learning. |
| **Approve a pending item** | Remove it from Pending and add a Learning row. |
| **Promote** ("second nature") | Remove the Learning row and add a bullet to the right Known category. |
| **Edit** | Change only the named fields. Keep the original date; append `(updated YYYY-MM-DD: …)` in the cell you changed. |
| **Delete** | Ask whether it's a removal (just gone) or a bad experience (move to Avoid with the reason). Also remove it from the Domain Index and from pattern stacks that name it. |
| **Add a pattern** | Catalog bullet + numbered PATTERNS.md section (Problem / Stack / How to build / Examples / Reference implementation / Gotchas). |

Every change also requires:
1. `git pull --ff-only` **before** editing (parallel sessions edit this repo).
2. Set the footer line `*Last updated: YYYY-MM-DD | …*` to today.
3. Show Cam the diff (`git diff`).
4. Commit with `Add <tech>` / `Update <tech>` / `Promote <tech>` / `Remove <tech>` / `Avoid <tech>` (several items: `Add <a>, <b> (project)`). Then push.
5. If the push is rejected: `git pull --rebase` and push again. Never force-push.

## Common mistakes (seen in this repo)
- **Forgotten footer.** The 2026-08-23 row was added while the footer still read 07-26.
- **Rows out of order.** A 07-04 row sits below a 07-05 row. Insert by date.
- **Duplicates across sections.** Firebase Hosting is listed twice in Known. Grep first.
- **Logging Known tech as Learning.** If it's already Known, the note goes on the Known bullet, not in a new row.
- **No link.** Rows need a "learn more" URL so Cam can study the tech.
- **Bundling unrelated tech in one row**, or recording planned tech as Known or Learning.
