# Pi AutoGrill

A Pi package that installs the AutoGrill skill and its isolated Decider agent.
GrillMe remains the source of truth for the workflow; AutoGrill delegates each round to one fresh Decider.

## Requirements

- Pi
- The current `grill-me` skill, which AutoGrill loads at runtime
- `pi-subagents`, which discovers and runs the packaged Decider agent

Install `pi-subagents` once, then install this package from a local checkout:

```sh
pi install npm:pi-subagents
pi install /path/to/auto-grill
```

Or install this package from its Git repository:

```sh
pi install git:<repository-url>
```

Restart Pi if it was already running. Invoke the skill with:

```text
/skill:auto-grill <idea>
```

## Package contents

- `skills/auto-grill/SKILL.md` — runtime wrapper around the installed GrillMe skill.
- `agents/auto-grill-decider.md` — one fresh, tool-less Decider per GrillMe round.

Pi discovers the skill from `pi.skills`; `pi-subagents` discovers the agent from `pi-subagents.agents` in `package.json`.
