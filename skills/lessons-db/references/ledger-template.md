# LESSONS-DB.md — template

Running database of confirmed defects, their root causes, and the prevention rule each one taught. Consult before similar work. Lives at the repo root. Append only; update Process and Status in place.

<!-- New review sections go directly below this line, newest first. -->

---

## Review: 2026-11-01 — list endpoint pagination (src/api/list.py)

**Scope:** code, one module, ~120 lines
**Process:** rounds: 2 — raised 5 / confirmed 2 / refuted 3
**Status:** PASSED 2026-11-01
**Artefacts:** `docs/reviews/list-pagination-round-1-*.md`, `docs/reviews/list-pagination-round-2-*.md`

### Confirmed defects

| ID | Defect | Root cause | Prevention rule |
|---|---|---|---|
| D1 | Last page repeats the final item | Offset computed from 1-based page without subtracting 1 (round 1) | Test every pagination boundary: first, last, empty, exact multiple |
| D2 | Profile page crashes when phone is absent | Optional field dereferenced without a guard (round 1; introduced by a fix) | Treat every optional field as nullable at each read; add a test with it unset |

### Deliberate decisions (not bugs — do not "fix")

| Decision | Rationale |
|---|---|
| Page size capped at 100 | Protects the database |

### Follow-ups

- Add a boundary-test helper shared by list endpoints.

---
