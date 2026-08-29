---
name: codebase-conformance-execution
description: "Execute an approved codebase-conformance plan with coordinated agents, isolated changes, and regression evidence. Use only after a plan is available and implementation is authorized."
---

# Codebase Conformance Execution

Execute a user-approved conformance plan using a team of agents when collaboration is available. Read the repository's `ENGINEERING_PHILOSOPHY.md` first when present, then repository-local instructions and the complete plan. If it is absent, use `$CODEX_HOME/skills/install-engineering-philosophy/references/principles.md` (or its `~/.codex` fallback) and disclose that the rules are not installed in the repository.

Do not invent missing plan details or silently broaden scope. If the plan has approval gates, uncertain behavior, migrations, production actions, or a dirty-worktree conflict, stop at that point and ask for the required direction.

## Coordinate the team

Use [the execution protocol](references/execution-protocol.md). Assign agents only independent, bounded work items with distinct ownership of files and contracts. Give every agent the relevant plan excerpt, philosophy rules, local instructions, acceptance criteria, and validation command. Keep one lead agent responsible for integration and decision-making.

Do not let multiple agents concurrently edit the same files, generated outputs, dependency manifests, shared tests, or public interfaces. Use isolated worktrees when available; otherwise make the assignments sequential. Agents report evidence and diffs rather than publishing or merging externally unless the user explicitly authorizes it.

## Completion

Integrate in plan order. For directory restructuring, move only one cohesive package or domain per checkpoint, update its callers and tests, then run the targeted build/test before beginning the next move. After each integration, inspect the diff and run the work item's targeted checks. At the end, run the highest-signal repository checks feasible, review the aggregate diff against the philosophy, and report changed behavior, validation evidence, deferred findings, and any residual risk. A failing baseline test is not proof of a new regression; document it and isolate the change's effect before proceeding.
