# docs/reviews/ layout

One file per artefact, named `docs/reviews/<YYYY-MM-DD>-<target-slug>-round-<N>-<kind>.md`. The slug is the section title, lowercase, hyphenated. The date is the review's start date, the same as in the section heading, so repeat reviews of one target never collide.

| Kind | Holds |
|---|---|
| `brief` | Scope, what reviewers were told to attack |
| `report-<reviewer>` | One reviewer's findings, verbatim. `<reviewer>` is the lens name (the skeptic is `skeptic`) |
| `docket` | Every finding with its verdict, confirmed or refuted, and why |
| `probe-<name>` | Output of a test, query or script that decided a verdict. A refuted finding gets no probe file unless output decided it |

Example: `docs/reviews/2026-11-01-list-pagination-round-1-docket.md`.

"Raised" counts every distinct finding once.

## Rules

- Ledger and round files go in one commit.
- Bundles (archives, dumps) are optional. If kept, put them in `~/review-bundles/<repo>/<date>/`, never tmp, and record the path under Artefacts. Do not commit the bundle.
- This template wins inside this skill; jedi-review's own ledger template is compatible.

## Note: skill-repo review records

Reviews of a skill repo itself are recorded as `docs/reviews/quick-r<N>-<date>.md` (house naming). That is a different purpose from a target ledger's round files and does not follow the pattern above.
