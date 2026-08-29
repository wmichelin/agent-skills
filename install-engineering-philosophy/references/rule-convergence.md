# Rule convergence procedure

Use the remote `principles.md` and its fetched commit SHA from the install skill's fetch step. All modifications stay within the target repository; never edit the remote source or a global agent configuration.

## Managed installation

If `ENGINEERING_PHILOSOPHY.md` contains the managed markers, replace only the content between them with:

```md
<!-- source: https://github.com/wmichelin/agent-skills.git@<fetched-commit> -->
<fetched principles.md content>
```

Preserve the markers and every line outside them. A changed managed block is intentionally refreshed from the remote source; project-specific rules belong outside the block.

## Legacy installation without markers

First compare the full existing document with known historical `principles.md` versions available in the fetched repository's Git history. If it exactly matches one, replace it with a managed installation using the fetched rules and source comment.

If it does not exactly match, treat it as a locally customized legacy document. Converge it rather than overwriting it:

1. Identify paragraphs and bullet rules unchanged from the closest historical canonical version; replace only those unchanged portions with the fetched equivalent.
2. Retain added or modified local rules under a `## Project-specific additions` section outside the managed block, preserving their meaning and wording.
3. If a locally modified canonical rule conflicts with the fetched rule, retain the local rule outside the managed block under `## Decisions requiring review`; state the conflict and do not silently resolve it.
4. Render the fetched canonical rules inside the managed block with the source comment, then place the preserved local sections after the end marker.

If the closest historical version cannot be determined with high confidence, do not guess. Preserve the legacy file, add no partial managed block, and ask the user whether to migrate it.

## Validate

Confirm the source comment contains the fetched commit, the managed block exactly matches the fetched rules apart from that comment, local sections remain outside it, and each agent adapter still resolves `ENGINEERING_PHILOSOPHY.md` by a repository-relative path. Report the remote commit, changes made, preserved additions, and unresolved conflicts.
