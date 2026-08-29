# Agent Skills

Reusable Codex skills for Walter’s repositories.

## Skills

- [`team-delivery-workflow`](team-delivery-workflow/) — coordinates GitHub issue intake, six-role review, evidence-first testing, status updates, and staging/production gates.
- [`install-engineering-philosophy`](install-engineering-philosophy/) — installs provider-neutral engineering rules with thin adapters for Codex, Claude, and Cursor.
- [`codebase-conformance-plan`](codebase-conformance-plan/) — assesses a codebase against installed rules and produces a safe, evidence-backed plan.
- [`codebase-conformance-execution`](codebase-conformance-execution/) — executes an approved conformance plan with coordinated agents and regression evidence.

## Install

Clone this repository, then copy either one skill or a selected set into your Codex skills directory. `CODEX_HOME` is honored when set; otherwise Codex uses `~/.codex`.

```bash
git clone git@github.com:wmichelin/agent-skills.git
cd agent-skills

skill_home="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$skill_home"
cp -R install-engineering-philosophy "$skill_home/"
```

To install several skills, name them explicitly:

```bash
skill_home="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$skill_home"

for skill in install-engineering-philosophy codebase-conformance-plan codebase-conformance-execution; do
  cp -R "$skill" "$skill_home/"
done
```

Restart Codex or begin a new session after installing so it discovers the new skills. To update an installed skill, pull this repository and copy that skill directory again.
