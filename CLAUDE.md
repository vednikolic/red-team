# Red Team Skill

Claude Code skill for adversarial analysis of ideas, specs, and strategies. Finds assumptions, failure modes, competitive threats, technical risks, and scope problems.

## Usage

Invoke with `/red-team` in Claude Code. The skill is auto-discovered from `.claude/skills/red-team/SKILL.md`.

```
/red-team path/to/spec.md
/red-team path/to/spec.md --save
```

## Syncing with Workspace

If you also use this skill inside a larger claude-workspace monorepo:

```bash
./sync.sh pull   # Copy FROM workspace INTO this repo
./sync.sh push   # Copy FROM this repo INTO workspace
```

Set `WORKSPACE_ROOT` if your workspace is not at `~/claude`.
