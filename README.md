# Pi AutoGrill

AutoGrill reduces the effort of design grilling without replacing the workflow that makes it useful.

This repository is the Pi-specific distribution: Pi's `pi-subagents` package discovers the bundled Decider agent. The portable workflow skill is distributed separately from the `alereyleyva/skills` repository.

## Goal

Use the currently installed GrillMe skill as the sole authority for exploring a design: it owns the design tree, question frontier, recommendations, fact-finding, and completion. AutoGrill changes only who answers each round.

For each GrillMe round, one fresh Decider independently answers all questions using only the goal, relevant settled context, and that round. AutoGrill resolves materially matching answers automatically and batches disagreements or decisions requiring personal judgment for the user. The completed round goes back to GrillMe, which continues until its own completion criteria are met.

The intended result is fewer routine user interruptions while retaining GrillMe's exploration depth and escalating uncertain choices instead of silently deciding them.

## Scope

This package contains:

- The `auto-grill` skill, which loads the current GrillMe skill at runtime rather than copying its workflow.
- The `auto-grill-decider` agent, configured with fresh context and no tools.

It does not include or replace GrillMe, add custom TypeScript, retain Decider memory between rounds, or add another judge or decision-making layer.

## Requirements

- Pi with package and skill support.
- The current `grill-me` skill installed separately. AutoGrill calls it by its `grilling` skill name at runtime.
- `pi-subagents`, which discovers and launches the packaged Decider.

Install the dependency and this package:

```sh
pi install npm:pi-subagents
pi install npm:@alereyleyva/pi-auto-grill
```

For a local checkout, replace the second command with `pi install /path/to/auto-grill`.
Restart Pi if it was already running.

## Use

```text
/skill:auto-grill <idea>
```

Example:

```text
/skill:auto-grill Design the tournament system for XPadel
```

## Package layout

- `skills/auto-grill/SKILL.md` — runtime wrapper and round-resolution instructions.
- `agents/auto-grill-decider.md` — isolated Decider role.
- `package.json` — Pi skill discovery and `pi-subagents` agent discovery manifests.

The package has no runtime code or package dependencies. `pi` declares the skill path; `pi-subagents` declares the packaged agent path under `pi-subagents.agents`.

## Publish

Before the first npm release, configure the public Git repository in `package.json`, confirm the scoped npm package name is available, then inspect the exact archive with:

```sh
bun publish --dry-run
```

Publish when the package name, repository metadata, and archive contents are ready:

```sh
bun publish
```
