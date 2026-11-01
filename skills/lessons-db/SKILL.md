---
name: lessons-db
description: Use when a review round confirms or refutes findings, a review, audit or test pass is about to close, work is about to start in an area that has been reviewed before, the user says "ledger it", "lessons db" or "what did we learn last time", or invokes /lessons-db.
---

# Lessons DB

`LESSONS-DB.md` at the repo root records what broke and why. Committed, never chat-only. Skeleton: `references/ledger-template.md`.

## The entry

One row per confirmed defect:

| ID | Defect | Root cause | Prevention rule |
|---|---|---|---|

- **Defect:** one line, what a user would hit.
- **Root cause:** why it happened, not where.
- **Prevention rule:** imperative and testable ("Assert page count with an empty last page").
- Note the confirming round and whether a fix introduced it.

Refuted findings are not rows. Only the counts are recorded.

## The review section

`## Review: <date> — <target>`, newest first, with:

- **Scope:** target, type, size.
- **Process:** rounds, raised / confirmed / refuted.
- **Status:** OPEN, PASSED, or SHIPPED OVER OPEN FINDINGS.
- **Artefacts:** path to the round files and any bundle.

## Round close

Before the round is called closed:

1. Write brief, reviewer reports, adjudication and material probe output to `docs/reviews/<target>-round-N-*.md` (`references/round-folder.md`).
2. Append rows and update Process and Status in the section.
3. Commit ledger and round files together.

Bundles go to a durable folder outside tmp; record the path. Never rewrite the ledger; append and update status.

## Before similar work

Read the ledger's rules for the area. Say which apply, by ID, before starting. None? Say so.

## Rationalizations

| Excuse | Reality |
|---|---|
| "We'll remember" | A reboot once wiped a whole round; only the committed ledger survived |
| "I'll write it at the end" | The end gets skipped; write at each round close |
| "The scratchpad is fine" | Scratchpads are cleaned; commit it |
| "The summary covers it" | No root cause or rule, no lesson |

## Common mistakes

| Mistake | Fix |
|---|---|
| Defect row with no rule | Add an imperative, testable rule |
| Root cause restates the defect | Ask why it was possible |
| Ledgering refuted findings | Count them only |
| Editing old rows | Append; update status only |
| Reports left in chat | Commit to `docs/reviews/` |
