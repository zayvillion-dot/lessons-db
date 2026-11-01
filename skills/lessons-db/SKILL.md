---
name: lessons-db
description: Use when a review round confirms or refutes findings, a review, audit or test pass is about to close, work is about to start in an area that has been reviewed before, the user says "ledger it", "lessons db" or "what did we learn last time", or invokes /lessons-db.
---

# Lessons DB

`LESSONS-DB.md` at the repo root records what broke and why. Committed, never chat-only. Start from `references/ledger-template.md`; file names and formats are in `references/round-folder.md`.

## The entry

One row per confirmed defect: `| ID | Defect | Root cause | Prevention rule |`.

- **ID:** `D<n>`, numbered across the whole ledger, never reused.
- **Defect:** one line, what a user would hit.
- **Root cause:** why it was possible, not where. End with `(round N)` or `(round N; introduced by fix of D<k>)`.
- **Prevention rule:** imperative; names an assertion or a check.

Refuted findings are not rows; only counts are recorded. Correct a wrong row by appending a new row that names the row it corrects; never edit a row.

## The review section

`## Review: <YYYY-MM-DD> — <target>`, newest first, ending with `---`. One section per review; later rounds update it in place. Process lists each round (with lenses per round), then cumulative totals. Never open a second section for the same review.

- **Scope:** target, type, size.
- **Process:** rounds, raised / confirmed / refuted.
- **Status:** `OPEN`, `PASSED <date>`, or `SHIPPED OVER OPEN FINDINGS (<who>, <date>)`.
- **Artefacts:** round files and any bundle.
- Optional: *Deliberate decisions* (not bugs, do not "fix") and *Follow-ups* (ticketed work).

## Round close

1. Write brief, reports, docket and deciding probe output to `docs/reviews/` (`references/round-folder.md`).
2. Append rows; update Process and Status only.
3. Ledger and round files in one commit.

## Before similar work

Read every Prevention rule in the ledger, plus each section whose Scope or title names a path you will touch. List the applicable IDs, or write "none apply", before the first edit.

## Rationalizations

| Excuse | Reality |
|---|---|
| "We'll remember" | A reboot once wiped a round; only the committed ledger survived |
| "I'll write it at the end" | The end gets skipped; write at each round close |
| "The scratchpad is fine" | Scratchpads are cleaned; commit it |

## Common mistakes

| Mistake | Fix |
|---|---|
| Defect row with no rule | Add an imperative rule naming an assertion or check |
| Root cause restates the defect | Ask why it was possible |
| Editing old rows | Append; update Process and Status only |
