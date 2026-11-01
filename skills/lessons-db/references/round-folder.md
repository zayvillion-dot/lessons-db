# docs/reviews/ layout

One file per artefact, named `<target>-round-N-<kind>.md`:

| Kind | Holds |
|---|---|
| `brief` | Scope, what reviewers were told to attack |
| `report-<reviewer>` | Each reviewer's findings, verbatim |
| `docket` | Every finding with its verdict: confirmed or refuted, and why |
| `probe-<name>` | Output of a test, query or script that decided a verdict |

Example: `docs/reviews/list-pagination-round-1-docket.md`.

Commit the round's files with the ledger update. Large bundles (archives, dumps) live in a durable folder outside tmp; record that path in the ledger section, not the bundle in git.
