# Status and team-review template

Use one durable issue comment, or a linked project artifact if the platform has comment-size limits. Keep it updated rather than scattering decisions across opaque agent logs.

## Status update

```text
Status: <started | claimed | reviewing | implementing | testing | pushed | staging | verified | blocked>
Last completed: <concrete action and result>
Now: <current action>
Next: <next action and checkpoint>
Evidence: <issue links, test output, commit, deployment revision, or screenshot>
Staging: <exact staging URL> (<pending | deploying | verified | blocked>)
Blocker: <specific blocker and owner, or “none”>
```

Post at claim/start, after the team review, when implementation starts, after tests, after push, after staging deployment, and on verification or failure. For long-running work, post a heartbeat at the repository’s agreed interval (normally 5–15 minutes).

## Six-role review

```text
## Team review
Issue: <number/link>
Scope: <one-sentence outcome>
Priority: <P0/P1/P2/P3>

### Product manager
- User problem:
- Acceptance criteria:
- Out of scope:
- Recommendation:

### Architect
- Components/data/API affected:
- Security/compatibility risks:
- Migration/rollback:
- Recommendation:

### Unit-testing expert
- Test seams:
- Focused cases:
- Regression coverage:
- Recommendation:

### Staff software engineer
- Implementation approach:
- Edge cases:
- Sequencing/maintainability:
- Recommendation:

### DevOps engineer
- Build/runtime dependencies:
- CI/deployment/observability:
- Rollback:
- Recommendation:

### QA tester
- Reproduction/evidence:
- Acceptance checks:
- Regression risks:
- Staging plan:
- Recommendation:

Decision: <approved plan, required changes, or explicit blocker>
Open risks: <owners and follow-up issues, or “none”>
```

## Completion note

```text
Result: <fixed | shipped | partially complete>
Commit: <hash/link>
Tests: <exact commands and outcomes>
Staging: <URL/revision and smoke-test outcome>
Production: <not deployed | deployed with approval by ...>
Known risks/follow-ups: <items or “none”>
```
