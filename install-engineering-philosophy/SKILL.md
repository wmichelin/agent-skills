---
name: install-engineering-philosophy
description: "Install a provider-neutral engineering-rules document and lightweight agent adapters in a repository. Use when setting up durable AI coding rules for Codex, Claude, Cursor, or other agents."
---

# Install Engineering Philosophy

Install engineering rules into the target repository, not into a provider's skill system. The installed repository document is the single source of truth; provider-specific files only direct agents to read it.

## Install

First inspect the repository, its current instruction files, and the working-tree state. Do not overwrite existing rules. If the target repository is not clear, ask the user for it.

Create or carefully merge `ENGINEERING_PHILOSOPHY.md` at the repository root from [the canonical rules](references/principles.md). Put installed canonical content between these exact markers so it can be refreshed safely:

```md
<!-- BEGIN managed: agent-skills engineering philosophy -->
<!-- END managed: agent-skills engineering philosophy -->
```

Preserve project-specific rules outside the managed block and resolve conflicts with the user rather than silently choosing one. The document must make clear that explicit user direction and repository-local safety or compliance rules take priority.

Then create or merge short adapters for the available agent ecosystems. Each adapter must say to read and follow `ENGINEERING_PHILOSOPHY.md`, and must not duplicate the rules:

- `AGENTS.md` for Codex-compatible agents.
- `CLAUDE.md` for Claude Code.
- `.cursor/rules/engineering-philosophy.mdc` for Cursor, using an always-applied project rule.
- `.github/copilot-instructions.md` for GitHub Copilot, if that directory or configuration already exists.

If an adapter already exists, append a concise cross-reference in its established format. Do not remove or reformat unrelated instructions. For other providers, look for their existing project instruction file and add the same one-line reference when its format is clear; otherwise report the provider as not yet wired rather than inventing configuration.

## Verify

Confirm every created or updated adapter resolves to the canonical document using a repository-relative path. Re-read the final files, report created versus modified files, and call out any existing instruction files that could conflict. Do not make application-code changes as part of this installation.

## Updating existing installations

When asked to refresh rules in a repository, replace only the content between the managed markers with the current [canonical rules](references/principles.md); preserve all text outside them. If markers are absent, compare the existing document with the canonical rules and ask before a potentially destructive replacement. Re-verify each adapter afterwards. Keep provider adapters thin so changes remain provider-agnostic.
