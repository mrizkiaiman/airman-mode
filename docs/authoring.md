# Writing skills and commands

This page covers the conventions every skill in this repo follows, with templates and a checklist. Read [Concepts](concepts.md) first for the difference between a command and a skill.

## Repository layout

```text
.
├── skills/
│   ├── commands/<name>/SKILL.md   # commands: workflows you start by name
│   ├── <name>/SKILL.md            # skills: one job each
│   └── <name>/agents/openai.yaml  # optional Codex metadata, per skill
├── docs/                          # this documentation
├── .claude-plugin/marketplace.json
├── skills.sh.json                 # grouping for skills.sh
└── package.json                   # local install shortcuts
```

Personal workflows live outside `skills/` and aren't published: `learning-records/` and its `record` skill, `mrizkiaiman/skills/`, and `AI-CONTEXT.md`.

The skills CLI looks up to three folder levels below `skills/`, so `skills/commands/<name>/SKILL.md` is found. When installed, every skill becomes a flat folder named after the skill.

## Rules for every skill

1. **`name` equals the folder name.** Use lowercase letters, digits, and hyphens. Kiro rejects a mismatch.
2. **Don't name a specific tool.** Write "spawn a subagent with a fresh context", not the subagent tool's name in one product. Tool-specific notes go in [`docs/harness/`](harness/README.md).
3. **Take input from the message.** Write "treat the text after the skill name as the bug description, and ask if it's empty". Don't use `$ARGUMENTS`.
4. **Point to repo config, don't restate it.** Refer to `docs/agents/issue-tracker.md`, `glossary-and-decisions.md`, and `verify.md` by path.
5. **Say whether a config file is required.** If the skill can't work without a file, it says so and points to `/setup-airman`. If the file only improves the result, mention it in plain prose and carry on without it.
6. **Avoid built-in names.** Don't take names that tools already use, such as `review`, `init`, or `resume`.
7. **Write in English** for agents: short imperative sentences, one instruction per sentence, no filler.
8. **Credit the source.** An adapted skill links its original URL at the bottom of `SKILL.md`, and keeps any license notice it needs.

## Extra rules for commands

1. **The description starts with `Command. Run only when the user types /<name>.`** That's what keeps the agent from starting a workflow on its own.
2. **Also set `disable-model-invocation: true`** for the tools that honor it, and add `agents/openai.yaml` with `allow_implicit_invocation: false` for Codex.
3. **Call skills, not commands.** A command never starts another command. It can suggest the next one in its reply.
4. **Stop at clear gates.** Say where the command waits for the user, and never push or open a pull request unless asked.
5. **Follow the git rules.** Branch off `main`, commit in small verified units, and commit a failing test before its fix.

## Templates

### Command

```markdown
---
name: fix-bug
description: Command. Run only when the user types /fix-bug. Diagnoses a bug with a feedback loop, lands the smallest evidence-backed fix, and proves it.
disable-model-invocation: true
---

# Fix bug

Treat the text after `/fix-bug` as the bug report. If it is empty, ask for the symptom.

Read `docs/agents/verify.md`. If it is missing, stop and ask the user to run `/setup-airman`.

## Steps

1. Call the `diagnosing-bugs` skill for phases 1–4.
2. ...

## Stop when

- ...

## Reply

What broke, the root cause, the fix, and the failing-then-passing loop output.

Source: <URL of the original, if adapted>
```

### Skill

```markdown
---
name: investigate
description: Answer a read-only question about how code works or why it was built this way. Use when the user asks "how does X work", "why is Y like this", or "are we sure".
---

# Investigate

...
```

A skill's description says **what it does** and **when to use it**, so the agent can match it to a request. A command's description only has to identify the command.

## Documentation

Every command has a page in `docs/commands/` with these sections, in this order:

1. Title, a status line, a one-paragraph summary, and the usage line
2. **When to use it**: a two-column table with alternatives
3. **Usage**: two or three real examples
4. **Steps**: a mermaid diagram, then numbered steps
5. **What it writes**
6. **Where it stops**
7. **Skills it calls**
8. **What you get back**
9. **Sources**

A skill gets one entry in [`skills.md`](skills.md).

## Checklist for a new skill or command

- [ ] `skills/<name>/SKILL.md`, or `skills/commands/<name>/SKILL.md`
- [ ] `name` matches the folder, and the description follows the rules above
- [ ] No tool names and no `$ARGUMENTS`
- [ ] Source linked, if adapted
- [ ] Entry in [`skills.md`](skills.md), or a page in `docs/commands/` for a command
- [ ] Row in the README command table, for a command
- [ ] Listed in `skills.sh.json` and `.claude-plugin/marketplace.json`
- [ ] Tried in at least one tool, and noted in the tool guide if anything differed
