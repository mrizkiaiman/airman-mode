# Google Antigravity

> Checked against the [Antigravity docs](https://antigravity.google/docs) on 2026-11-24. End-to-end testing is pending.

## Install

```bash
npx skills add mrizkiaiman/airman-mode --skill '*' --global -a antigravity
```

| Scope | Skills folder |
| --- | --- |
| Project | `.agents/skills/`, and each parent folder up to the repo root |
| Global | `~/.gemini/config/skills/` |

The older `.agent/skills/` folder still works. The CLI also reads `~/.gemini/antigravity-cli/skills/`, and the IDE also reads `~/.gemini/antigravity/skills/`.

## Start a command

Type `/fix-bug` in the App or the CLI. The CLI turns each skill into a slash command. The docs don't say whether the IDE does the same.

Workflows (`.agents/workflows/`) are deprecated in favor of skills. Airman Mode doesn't use them.

## Project instructions

Antigravity always loads `AGENTS.md` or `GEMINI.md` from the repo root, from `.agents/`, and from each parent folder. So the `## Agent skills` block that `/setup-airman` writes is picked up automatically.

Rules in `.agents/rules/*.md` need a `trigger:` (`always_on`, `model_decision`, `glob`, or `manual`). Airman Mode doesn't need any rules.

## Known gaps

| Gap | Workaround |
| --- | --- |
| `disable-model-invocation` isn't documented | Command descriptions say `Run only when the user types /<name>` |
| Subagents pick a model tier (`inherit`, `flash`, `pro`), not a named model | For a review on a different model, use another tool. See [T3 Code](t3-code.md#fresh-context-review) |

## Subagents

Subagents are defined in `.agents/agents/` or `~/.gemini/config/agents/` with `model: inherit | flash | pro`. The `implement` skill can use them to build frontier tickets in parallel.

## Sources

- [Skills](https://antigravity.google/docs/skills)
- [Rules](https://antigravity.google/docs/rules)
- [Subagents](https://antigravity.google/docs/subagents)
- [Workflows to skills](https://antigravity.google/docs/migration/workflows-to-skills)
- [skills CLI: supported agents](https://github.com/vercel-labs/skills/blob/main/docs/agents.md)
