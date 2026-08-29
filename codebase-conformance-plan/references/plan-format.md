# Conformance plan format

Use this structure, omitting sections that do not apply.

## Baseline

- Scope and repository state
- Commands run and their results
- Architecture and contracts relevant to the work
- Engineering-principle source and any local rule that overrides it
- Root-level source inventory and the proposed ownership of every file that should move

## Findings

For each finding: identifier, evidence (file/symbol), affected principle, impact, confidence, dependencies, and why it matters. State what is intentionally out of scope.

## Ordered work items

For each item: objective; files/symbols; implementation approach; behavioral and compatibility risks; validation commands/tests; rollback or recovery approach; and whether it can run independently. For a package move, include old and new import paths, entrypoint updates, and the compatibility decision. Include a small, observable checkpoint after each risky item.

## Execution topology

Show which work items must be sequential and which can be assigned to separate agents without overlapping files or contracts. Name the integration owner and the final verification pass.

## Approval gates and open questions

List choices requiring user approval and the evidence needed to resolve open questions. An empty list is valid.
