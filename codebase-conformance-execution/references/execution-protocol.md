# Team execution protocol

## 1. Validate the plan

Confirm every work item has an owner, acceptance criteria, a validation command, and no unresolved approval gate. Re-check the current worktree because the plan may be stale.

## 2. Build the dependency map

Group tasks into waves. A task is parallel-safe only if it does not alter the same files, generated artifacts, dependency/configuration manifests, tests, public contracts, or assumptions as another active task. When uncertain, make it sequential.

## 3. Assign narrowly

Each agent receives one bounded outcome, its allowed paths, constraints, test command, and an instruction to stop if it needs to cross the boundary. Agents must preserve unrelated edits and report: summary, files changed, validation run/result, assumptions, and residual risks.

## 4. Integrate and verify

The lead inspects each returned diff before accepting it, checks that it meets the plan and philosophy, resolves conflicts deliberately, and runs the item's validation. Never stack unreviewed changes from multiple agents.

## 5. Final gate

Run relevant repository checks, inspect `git diff` and status, verify compatibility-sensitive paths, and compare the delivered state with every plan item. Do not claim full conformance when out-of-scope or unverified findings remain.
