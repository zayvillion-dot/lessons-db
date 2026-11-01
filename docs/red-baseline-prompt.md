# RED/GREEN baseline prompts — run in a FRESH session opened in an empty git repo with NO CLAUDE.md. RED: no skills loaded. GREEN: lessons-db installed.

Open the fresh session in a throwaway git repo (a few source files, including `src/api/list.py`, and one commit), then paste the prompt below.

## Prompt 1: close a round

> A review of `src/api/list.py` just finished round 1 of 1 (3 lenses: skeptic, edge-case, tests). Close the round. Material follows.
>
> **Brief:** Attack the pagination in `src/api/list.py`. Look for boundary errors, unguarded optional fields, and untested paths.
>
> **Report, skeptic:**
> - F1: Offset is computed as `page * size`, but pages are 1-based, so the last page repeats the final item of the previous page.
> - F2: Page size is capped at 100 with no error; a request for 500 silently returns 100.
>
> **Report, edge-case:**
> - F3: `profile.phone` is read without a guard; a profile with no phone raises AttributeError.
> - F4: (same as F1, reported on the empty-list case)
>
> **Verdicts:** F1 confirmed (off-by-one). F2 refuted (the cap is deliberate, documented in the module docstring). F3 confirmed (missing null check on an optional field). F4 is a duplicate of F1. Raised: 3 distinct findings. Confirmed 2, refuted 1. Lenses ran one round.

Save the reply as `~/Desktop/lessons-db-baseline.md`, plus `git log --stat` and `ls -R` of the working folder and the contents of any files created.

Measuring: does the agent write a durable ledger, with a root cause and prevention rule per defect and the round's counts, put review files in the repo, and commit? Baselines usually reply conversationally and write nothing.

## GREEN criterion for prompt 1

Expected files, exactly:

- `LESSONS-DB.md` at the repo root.
- `docs/reviews/<YYYY-MM-DD>-<target-slug>-round-1-brief.md` (slug e.g. `list-pagination`).
- `docs/reviews/<YYYY-MM-DD>-<target-slug>-round-1-report-skeptic.md` and `...-round-1-report-edge-case.md`.
- `docs/reviews/<YYYY-MM-DD>-<target-slug>-round-1-docket.md`.
- No probe file (no output decided a verdict).

`LESSONS-DB.md` content:

- The template's Example section is replaced, not kept.
- One section `## Review: <YYYY-MM-DD> — <target>`, ending with `---`.
- Scope; Process with lenses per round and totals (raised 3 / confirmed 2 / refuted 1); Status `PASSED <date>` or `OPEN` (a free-text note allowed in parentheses after the value); Artefacts listing the files above.
- Two rows, D1 and D2, each with a one-line defect, a root cause ending `(round 1)`, and an imperative prevention rule naming an assertion or a check.
- F2 not ledgered as a row; counted only.

Commit checks:

- Ledger and review files are in one commit.
- `git diff HEAD~1 -- LESSONS-DB.md` deletes no lines except Process/Status lines.

## Prompt 2: before similar work (run in the same repo after prompt 1's GREEN commit)

> Add a paginated /orders endpoint.

Passes if the reply cites D1 (by ID, with its rule) before the first edit, or writes "none apply" only when no rule applies. Here D1 applies.

## Judgment notes

- Rules are judged from the transcript: a rule passes if it names an assertion or a check someone could run. "Be careful with offsets" fails. "Assert items on first, last, empty and exact-multiple pages" passes.
- Root-cause quality ("why it was possible", not "where") is judged from the transcript, not by script.
