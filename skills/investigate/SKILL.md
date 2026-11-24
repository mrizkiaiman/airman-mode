---
name: investigate
description: Answer a read-only question about a codebase, such as how something works, why it was built this way, or whether a claim about it holds. Use when the user asks "how does X work", "why is Y like this", "where does Z happen", or "are we sure".
---

# Investigate

Answer a question about the code. Don't change any files: the output is a cited explanation or a recommendation.

Treat the user's message as the question. If it could mean more than one thing, name the reading you chose in one line and continue.

## Steps

1. **Ground yourself.** Read the glossary and ADRs that `docs/agents/glossary-and-decisions.md` points to, or `GLOSSARY.md` and `docs/adr/` if that file doesn't exist. Use the glossary's terms in your answer.
2. **Trace the code.** Start at the entry point the question is about, such as a route, a command, or an event handler, and follow the real call path. Read the code; don't infer behavior from names. For a large area, delegate the reading to a subagent and keep only its summary.
3. **For "why" questions, read the record.** Use `git log -L` or `git log --follow` on the relevant lines and files, then `git show` on the commits that introduced and changed them, and read their pull request discussions if the tracker has them. Quote what the authors wrote. Mark your own inferences as inferences, and say when the record doesn't answer the question.
4. **Check claims.** When the question is "are we sure", look for evidence on both sides, and run a quick read-only check (a test, a query, a script) if that settles it faster than reading.
5. **Write the answer.**

## Answer format

For "how does it work" questions:

- **Overview**: the answer in two or three sentences
- **Key concepts**: the terms and types the reader needs
- **How it works**: the flow, step by step, with `path:line` references
- **Where things live**: the files and modules involved
- **Gotchas**: surprising behavior, edge cases, and known traps

For a choice between alternatives, give a recommendation with a trade-off table instead.

Give your honest judgment. If the question's premise is wrong, say so and explain why.

## When the answer calls for a change

Stop at the answer. If something is broken, suggest `/fix-bug`. If it calls for something new, suggest `/new-feature`.

---

Based on poteto's [investigation playbook](https://github.com/cursor/plugins/blob/main/pstack/skills/poteto-mode/playbooks/investigation.md) and [`why`](https://github.com/cursor/plugins/tree/main/pstack/skills/why) skill (MIT).
