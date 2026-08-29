# Agent Skills

Reusable skills and engineering-rule workflows for AI coding agents.

## Skills

- [`team-delivery-workflow`](team-delivery-workflow/) — coordinates GitHub issue intake, six-role review, evidence-first testing, status updates, and staging/production gates.
- [`install-engineering-philosophy`](install-engineering-philosophy/) — installs provider-neutral engineering rules with thin adapters for Codex, Claude, and Cursor.
- [`codebase-conformance-plan`](codebase-conformance-plan/) — assesses a codebase against installed rules and produces a safe, evidence-backed plan.
- [`codebase-conformance-execution`](codebase-conformance-execution/) — executes an approved conformance plan with coordinated agents and regression evidence.

## Install

Each skill is a self-contained directory rooted at `SKILL.md`. Clone this repository, then either point your agent harness at the clone or copy complete skill directories into that harness's configured skills location. Discovery and reload behavior are harness-specific.

To copy one skill, set `skill_directory` to the location your harness reads for skills:

```bash
git clone git@github.com:wmichelin/agent-skills.git
cd agent-skills

skill_directory="/path/to/your/agent/skills"
mkdir -p "$skill_directory"
cp -R install-engineering-philosophy "$skill_directory/"
```

To install several skills, name them explicitly and copy each complete directory:

```bash
skill_directory="/path/to/your/agent/skills"
mkdir -p "$skill_directory"

for skill in install-engineering-philosophy codebase-conformance-plan codebase-conformance-execution; do
  cp -R "$skill" "$skill_directory/"
done
```

If a harness does not support skills, use `install-engineering-philosophy`'s `references/principles.md` as the portable source for repository rules, then follow that harness's mechanism for project instructions. The installed `ENGINEERING_PHILOSOPHY.md` remains provider-neutral; Codex, Claude, and Cursor files are only thin pointers to it.

Reload or restart the relevant agent session after installation. To update, pull this repository and replace the selected skill directory.
