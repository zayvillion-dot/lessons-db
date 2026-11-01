# RED baseline prompt — run in a FRESH session opened in an empty git repo with NO CLAUDE.md, no skills loaded

Open the fresh session in a throwaway git repo (a few source files and one commit), then paste:

> A code review you ran just confirmed two defects (an off-by-one in pagination; a missing null check on an optional field) and refuted one. Close the round.

Save the reply as `~/Desktop/lessons-db-baseline.md`, plus `git log --stat` and `ls -R` of the working folder and the contents of any files created.

What we are measuring: does the agent write a durable ledger file with a root cause and a prevention rule for each defect and the round's counts (raised / confirmed / refuted); put the review reports in the repo under `docs/reviews/`; and commit? Or does it summarise in chat? Baselines usually reply conversationally with a tidy summary and write nothing.

Run the same prompt again with the skill installed (GREEN) and compare.

## GREEN criterion

`LESSONS-DB.md` at the repo root with a review section (Scope / Process / Status); two defect rows, each with ID, one-line defect, root cause, and an imperative testable prevention rule; the refuted finding not ledgered as a defect but counted (raised 3 / confirmed 2 / refuted 1); review files under `docs/reviews/`; ledger and review files committed in one commit.
