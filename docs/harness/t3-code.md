# T3 Code

> Checked against the [T3 Code docs](https://github.com/pingdotgg/t3code/tree/main/docs/user) on 2026-11-24 (v0.1.11). End-to-end testing is pending.

[T3 Code](https://github.com/pingdotgg/t3code) is a desktop, web, and mobile app for running coding agents. It describes itself as "not a harness": it drives agent CLIs you're already signed in to, on your own subscriptions. Skills, instructions, and models all come from the agent behind it, called the **backend**.

## Install

Install for the backends you use inside T3 Code, for example:

```bash
npx skills add mrizkiaiman/airman-mode --skill '*' --global -a claude-code -a codex -a cursor
```

Built-in backends include Claude Code, Codex, Cursor CLI, Kiro CLI, OpenCode, and Google Antigravity. Other agents can be added through ACP. Each backend loads skills from its own folders, as described in its guide: [Antigravity](antigravity.md), [Kiro](kiro.md).

## Start a command

Type `/` or `$` in the composer and pick the command, for example `/fix-bug`, then describe the task.

## Project instructions

The T3 Code docs don't mention `AGENTS.md`. Whether it is read depends on the backend. Antigravity and Kiro both read it.

## Fresh-context review

T3 Code has a `delegate_task` tool, which starts child threads shown in the **Agents** panel. The README says work can move across providers ("Let Claude hand a task to Codex").

**Recommended setup:** build with one backend and review with another.

1. Finish the work with your build backend, for example Antigravity.
2. Ask it to delegate the review: *"delegate `/code-review` of this branch to a Kiro thread"*.
3. If delegation to that backend isn't available, open a new Kiro thread in the same project and run `/code-review`. It reads the same diff and the same spec from the repo, so the result is the same.

> [!NOTE]
> Delegating from Antigravity to Kiro hasn't been confirmed yet. This guide will be updated after testing.

## Switching backends mid-task

1. Run `/handoff` in the current thread and copy the result.
2. Open a thread with another backend in the same project.
3. Paste the handoff as your first message.

## Sources

- [README](https://github.com/pingdotgg/t3code)
- [FAQ](https://github.com/pingdotgg/t3code/blob/main/docs/user/faq.md)
- [Providers](https://github.com/pingdotgg/t3code/blob/main/docs/user/install.md#providers)
- [ACP providers](https://github.com/pingdotgg/t3code/blob/main/docs/user/providers-acp.md)
- [Thread sidebar and Agents panel](https://github.com/pingdotgg/t3code/blob/main/docs/user/thread-sidebar.md)
