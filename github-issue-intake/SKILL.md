---
name: github-issue-intake
description: "Triage a GitHub issue into an evidence-backed delivery brief and hand it to team-delivery-workflow. Use for bug or feature intake; do not implement or run the delivery team directly."
---

# GitHub Issue Intake

Turn a GitHub bug or feature issue into a concise delivery brief. This skill owns intake only: it does not implement, deploy, claim delivery work, or run specialist review.

## Triage

Inspect the issue, linked evidence, repository instructions, and relevant code only far enough to make the problem actionable. Capture the user-visible outcome, evidence, impact, affected area, acceptance criteria, out-of-scope behavior, and priority. Treat screenshots, videos, logs, error messages, and a clear symptom as actionable evidence; do not demand routine metadata that can be discovered through investigation.

Reuse repository labels and forms where present. If labels are absent, use a minimal vocabulary such as `bug`, `feature`, `needs-triage`, `agent-ready`, and `blocked`. Do not apply a delivery claim or imply that implementation has started.

## Handoff

Write the completed [delivery brief](references/delivery-brief.md) as an issue comment or linked artifact. Resolve ordinary ambiguities from evidence; list only material open questions. If the work is ready, mark it `agent-ready` where that label exists and invoke `team-delivery-workflow` with the brief. If direct skill invocation is unavailable, give the operator the exact instruction to invoke `team-delivery-workflow` with the issue link and brief.

If the issue is blocked, state the specific decision or evidence required. Do not ask the delivery team to compensate for an incomplete brief.
