# Tool guides

The skills never name a specific tool, so they work in any agent that supports [Agent Skills](https://agentskills.io). This page lists the parts that do depend on the tool.

## Quick reference

| Tool | Install with | Global skills folder | Start a command | Guide |
| --- | --- | --- | --- | --- |
| Claude Code | `-a claude-code` | `~/.claude/skills/` | `/new-feature` | — |
| OpenAI Codex | `-a codex` | `~/.agents/skills/` | `$new-feature`, or pick it from `/skills` | — |
| Cursor | `-a cursor` | `~/.cursor/skills/` | `/new-feature` | — |
| OpenCode | `-a opencode` | `~/.config/opencode/skills/` | `@new-feature` | — |
| T3 Code | the backend's id | the backend's folder | `/new-feature` or `$new-feature` | [t3-code.md](t3-code.md) |
| Google Antigravity | `-a antigravity` | `~/.gemini/config/skills/` | `/new-feature` | [antigravity.md](antigravity.md) |
| Kiro | `-a kiro-cli` | `~/.kiro/skills/` | `/new-feature` | [kiro.md](kiro.md) |

Install for several tools at once by repeating `-a`, for example `-a claude-code -a codex -a cursor`. The folders come from the [skills CLI agent list](https://github.com/vercel-labs/skills/blob/main/docs/agents.md).

> [!NOTE]
> In Claude Code, the installed `code-review` skill replaces the bundled `/code-review`. The bundled `/review` alias still runs Claude Code's own review.

## Status

- **T3 Code, Antigravity, and Kiro** have a guide, checked against vendor docs on 2026-11-24. End-to-end testing is pending.
- **Claude Code, Codex, Cursor, and OpenCode** support Agent Skills and should work, but haven't been tested yet.

A guide covers where skills and `AGENTS.md` are loaded from, how to start a command, how to get a fresh-context review, and the tool's known gaps. Pull requests that add a tested guide are welcome. Copy the structure of an existing one.

## Behavior every tool shares

- **Manual commands.** Some tools ignore `disable-model-invocation`. Every command's description says `Run only when the user types /<name>`, so the agent leaves commands alone unless you call them. Codex also reads `allow_implicit_invocation: false` from each command's `agents/openai.yaml`.
- **No argument placeholders.** Commands read your input from the message itself, not from `$ARGUMENTS`, which only some tools substitute.
- **Name equals folder.** Every skill's `name` matches its folder name, which Kiro requires.
