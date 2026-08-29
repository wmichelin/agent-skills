---
name: team-delivery-workflow
description: "Coordinate a repo-agnostic, review-driven delivery team around GitHub Issues: triage bugs and features, gather six specialist reviews, implement with evidence-first testing, publish status updates, and verify staging before production."
---

# Team Delivery Workflow

Use this skill when a repository needs a durable workflow for bugs, feature requests, and coordinated engineering delivery. Adapt to the repository’s existing language, CI, deployment, and issue conventions; do not assume a particular framework, cloud provider, host, or toolchain.

## Operating model

One execution agent owns the work: repository changes, commits, pushes, deployments, and final verification. The specialist roles review and advise; they do not create competing implementations or silently mutate the repository.

Run these six perspectives for every non-trivial issue, recording their input in one issue comment or linked artifact:

- Product manager: user problem, scope, priority, acceptance criteria, and out-of-scope behavior.
- Architect: boundaries, data/API changes, security, compatibility, and migration/rollback concerns.
- Unit-testing expert: test seams, focused unit cases, fixtures, failure modes, and regression coverage.
- Staff software engineer: implementation shape, maintainability, edge cases, and sequencing.
- DevOps engineer: build/runtime dependencies, CI, secrets, observability, deployment, and rollback.
- QA tester: reproduction, black-box acceptance checks, regression risks, and staging verification.

The review is not complete until each role has either a concrete recommendation or an explicit “no concerns.” Preserve decisions and unresolved risks; do not replace them with a vague approval.

## Issue lifecycle

Prefer GitHub Issues with bug and feature forms. Reuse existing labels when present; otherwise use a small, consistent vocabulary such as `bug`, `feature`, `team-review`, `agent-ready`, `agent-claimed`, `staging-ready`, and `blocked`.

1. Intake: capture the user-visible problem or outcome, evidence, impact, acceptance criteria, and priority.
2. Claim: add a status comment naming the execution agent, current phase, and next checkpoint; apply the claim label.
3. Team review: add the six-role review before coding, unless the change is genuinely trivial.
4. Plan: turn the review into concrete implementation and test tasks. Resolve material ambiguities; do not outsource basic investigation to the reporter.
5. Implement: make the smallest coherent change, preserving local conventions and unrelated user work.
6. Test: run focused tests, the relevant project-wide checks, and a build/package check where applicable.
7. Publish: commit and push the verified change. Never claim a push or deployment without checking its result.
8. Stage: deploy the branch or commit to the project’s staging environment and run smoke/acceptance checks.
9. Close: document the result, test commands, deployment URL or identifier, remaining risks, and follow-up issues. Close only when acceptance criteria are verified.

Use the status headings and review template in `references/status-and-review-template.md`.

## Evidence-first bug handling

Treat screenshots, videos, logs, error messages, and a clear symptom as actionable evidence. Investigate and reproduce from the evidence yourself. For UI issues, try sensible desktop and mobile viewport checks and inspect the relevant code before asking for browser or viewport metadata. Missing metadata is not a blocker when the symptom and affected area are clear; ask only when different interpretations would materially change the fix or create a safety risk.

When reproduction is unavailable, proceed with static analysis, a targeted regression test, and a staging check. State what was verified and what remains uncertain instead of marking the issue blocked by default.

## Testing and environment rules

- Discover the project’s documented test/build commands and CI configuration first.
- Run the narrowest useful test while iterating, then the required broader checks before publishing.
- If a host toolchain is missing (for example Go, Node, a database, or a browser), use the repository’s devcontainer, Docker Compose setup, CI image, or an official language image. Do not skip tests merely because the host is incomplete.
- Reproduce production-relevant dependencies in containers when practical, while keeping credentials and local state out of commits.
- For UI changes, exercise the real route and interaction on staging; do not rely only on a unit test or a successful build.
- Report exact commands and outcomes, including known failures and whether they are pre-existing.

## Status and automation

Provide a visible update at each meaningful transition: received, claimed, review complete, implementation started, tests running/passed, pushed, staging deployed, staging verified, or blocked. A heartbeat should include the last completed action, current action, next action, and the specific blocker if any.

For GitHub automation, prefer a signed, event-driven workflow such as GitHub Actions on a trusted self-hosted runner when repository access and deployment credentials are already configured. Use polling as a fallback. If a public webhook is required, validate the signature, restrict accepted events, make delivery idempotent, and never expose an agent-control endpoint directly to the internet. The trigger should acknowledge the issue quickly, then hand work to the execution loop.

Automation must avoid duplicate claims, leave a comment when it starts, and leave a comment when it exits or fails. A quiet issue is a workflow defect, not evidence that the work is finished.

## Deployment gates

Treat push, build, deployment, and smoke-test failures as active blockers. Stop the current promotion, report the exact failure, repair it when authorized, and rerun the gate. Deploy each meaningful slice to staging so the reporter can inspect progress. Production deployment requires explicit user approval unless the repository’s documented policy clearly grants automatic production promotion.

Before declaring success, verify the deployed revision, health check, primary user path, relevant logs, and issue acceptance criteria. If any check cannot run, say so plainly and leave the issue open with a concrete next action.

## Cross-repository setup

When installing this workflow in another repository, first inspect its instructions, issue forms, labels, CI, deployment targets, and available runners. Then adapt the templates and automation without copying repository-specific paths, domains, account names, tokens, or secrets. Keep the role review and evidence/status requirements stable; customize only the integration points.

Do not invent a staging URL, runner, webhook, credential, or successful deployment. If a required integration is absent, identify the smallest setup needed and continue with local review/testing where possible.
