# LESSONS-DB.md — template

Running database of confirmed defects, their root causes, and the prevention rule each one taught. Consult before similar work. Lives at the repo root.

Append only. Update Process and Status only. Correct a wrong row by appending a new row that names the row it corrects; never edit a row. IDs are `D<n>`, numbered across the whole ledger, never reused. "Docket" is the file listing every finding with its verdict.

New review sections go directly below the marker line, newest first. Replace the Example section below with real ones; do not keep it. Each section ends with its own `---`.

## Skeleton

```markdown
<!-- New review sections go directly below this line, newest first. -->

## Review: <YYYY-MM-DD> — <target>

**Scope:** <target, type, size>
**Process:** round 1: <n> lenses, raised <n> / confirmed <n> / refuted <n>; round 2: ...; total: raised <n> / confirmed <n> / refuted <n>
**Status:** OPEN | PASSED <YYYY-MM-DD> | SHIPPED OVER OPEN FINDINGS (<who>, <YYYY-MM-DD>)   (free-text note allowed after the value, in parentheses)
**Artefacts:** <docs/reviews/ files>; <bundle path, optional>

### Confirmed defects

| ID | Defect | Root cause | Prevention rule |
|---|---|---|---|
| D<n> | <one line, what a user would hit> | <why it was possible> (round N) | <imperative; names an assertion or a check> |

### Deliberate decisions (optional; not bugs, do not "fix")

| Decision | Rationale |
|---|---|

### Follow-ups (optional; ticketed work)

- <item>

---
```

## Example (filled; replace, do not keep)

## Review: 2026-11-01 — list endpoint pagination (src/api/list.py)

**Scope:** code, one module, ~120 lines
**Process:** round 1: 3 lenses, raised 4 / confirmed 1 / refuted 3; round 2: 3 lenses, raised 1 / confirmed 1 / refuted 0; total: raised 5 / confirmed 2 / refuted 3
**Status:** PASSED 2026-11-01
**Artefacts:** `docs/reviews/2026-11-01-list-pagination-round-1-docket.md`, `docs/reviews/2026-11-01-list-pagination-round-2-docket.md`

### Confirmed defects

| ID | Defect | Root cause | Prevention rule |
|---|---|---|---|
| D1 | Last page repeats the final item | Offset computed from 1-based page without subtracting 1 (round 1) | Assert items on first, last, empty and exact-multiple pages |
| D2 | Page 1 returns no items when the list is empty | Guard added in `src/api/list.py` for D1 divided by an unchecked page count (round 2; introduced by fix of D1) | Assert a 200 with an empty list for zero items |

### Deliberate decisions (not bugs — do not "fix")

| Decision | Rationale |
|---|---|
| Page size capped at 100 | Protects the database |

### Follow-ups

- Add a boundary-test helper shared by list endpoints.

---
