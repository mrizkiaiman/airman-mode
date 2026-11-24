# Kiro

> Checked against the [Kiro docs](https://kiro.dev/docs) on 2026-11-24. End-to-end testing is pending.

This guide covers the Kiro IDE and the Kiro CLI.

## Install

```bash
npx skills add mrizkiaiman/airman-mode --skill '*' --global -a kiro-cli
```

| Scope | Skills folder |
| --- | --- |
| Project | `.kiro/skills/` |
| Global | `~/.kiro/skills/` |

When two skills share a name, the project one wins. A skill's `name` must match its folder name. Every Airman Mode skill follows that rule.

### Custom agents

The default agent loads every installed skill. A **custom agent** loads only the skills listed in its `resources`:

```json
{
  "resources": ["skill://.kiro/skills/**/SKILL.md"]
}
```

## Start a command

Type `/fix-bug` in the IDE or the CLI.

## Project instructions

Kiro always includes `AGENTS.md` from the workspace root, subfolders, and `~/.kiro/steering/`. The `## Agent skills` block that `/setup-airman` writes is picked up automatically.

Steering files in `.kiro/steering/*.md` take `inclusion: always | fileMatch | manual | auto`. Airman Mode doesn't need any.

## Known gaps

| Gap | Workaround |
| --- | --- |
| `disable-model-invocation` isn't documented | Command descriptions say `Run only when the user types /<name>` |
| `$ARGUMENTS` works only in the CLI | Commands read input from your message instead |
| A per-subagent model isn't confirmed | Treat subagents as fresh context on the same model |

## Using Kiro as the reviewer

Kiro works well as a second opinion: build in one tool, then review here. Open Kiro in the same repo and run:

```text
/code-review main
```

It reads the branch diff and the spec from `docs/work/`, so it needs nothing from the session that built the code.

## Sources

- [Skills](https://kiro.dev/docs/skills/)
- [Steering](https://kiro.dev/docs/steering/)
- [Custom agents](https://kiro.dev/docs/custom-agents/)
- [Subagents](https://kiro.dev/docs/custom-agents/subagents/)
- [skills CLI: supported agents](https://github.com/vercel-labs/skills/blob/main/docs/agents.md)
