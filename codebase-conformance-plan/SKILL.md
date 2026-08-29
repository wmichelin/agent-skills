---
name: codebase-conformance-plan
description: "Assess a codebase against the installed engineering philosophy and produce a safe, evidence-backed conformance plan without modifying code. Use before a cleanup, modernization, or quality-improvement effort."
---

# Codebase Conformance Plan

Produce a read-only, evidence-backed plan for bringing a codebase into conformance with the installed engineering philosophy. Do not edit source, configuration, dependencies, or generated artifacts.

## Inputs and discovery

Read the repository's `ENGINEERING_PHILOSOPHY.md` first when present, then its local agent instructions and contribution guidance. If the repository has not installed one, use `$CODEX_HOME/skills/install-engineering-philosophy/references/principles.md` (or its `~/.codex` fallback) and state that the assessment used the shared default rather than repository-installed rules.

Establish the baseline before judging it: repository status, package/build metadata, entry points, dependency graph, top-level source-file inventory, test and quality commands, CI, recent history when useful, and the areas relevant to the requested scope. Treat existing conventions as evidence, not automatically as defects.

## Assessment

For every finding, distinguish observation from recommendation. Give exact file/symbol locations and explain which philosophy principle is involved. Identify affected contracts, consumers, migrations, integrations, and test coverage before proposing a change.

Do not turn subjective preferences into mandatory work. Exclude cosmetic-only changes unless the user asks for them. Mark uncertain findings as questions to validate, rather than presenting them as facts.

Prioritize findings by risk reduction, user value, confidence, and blast radius. For a flat root, identify cohesive domain moves, the import paths and public contracts they affect, and a migration order that keeps the repository buildable after each step. Separate prerequisites, safe independent work, and sequencing constraints. Preserve a clean boundary between behavioral changes and structural cleanup whenever practical.

## Deliverable

Write a plan using [the plan format](references/plan-format.md). It must be executable by another agent without rediscovering the important evidence, but it must not itself change the codebase. End with explicit approval gates for irreversible, externally visible, data-migrating, or uncertain changes.
