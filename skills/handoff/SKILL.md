---
name: handoff
description: Compact the current conversation into a handoff the user can paste into a new session or another tool to continue the work.
argument-hint: "What will the next session be used for?"
disable-model-invocation: true
---

Write a handoff that summarises the current conversation, so a fresh agent can continue the work.

**Print it in the chat** as one fenced `markdown` block the user can copy. Don't save it to a file.

If the user wrote text after `/handoff`, treat it as what the next session will focus on, and tailor the handoff to it.

## Contents

Use these sections, in this order. Skip a section that would be empty.

1. **Goal**: what this work is for, in one or two sentences.
2. **State**: the branch, the last commit, and the work folder (`docs/work/<slug>/`) with each ticket's status.
3. **Done**: what was finished and verified, and how it was verified.
4. **Decisions**: choices made in this session that aren't written down anywhere else yet.
5. **Open**: unresolved questions, failing checks, and suspicions not yet confirmed.
6. **Next**: the exact next step.
7. **Suggested skills**: the skills or commands the next session should use.

## Rules

- Point to existing artifacts instead of copying them: specs, tickets, ADRs, commits, diffs. Use a path or URL.
- Redact secrets and personal data such as API keys, passwords, tokens, and emails. Write `<REDACTED>`.
- Mark claims you didn't verify in this session as unverified, so the next session re-checks them.
- After the block, tell the user to paste it as the first message of the next session.

---

Adapted from [`handoff`](https://github.com/mattpocock/skills/tree/main/skills/productivity/handoff) by Matt Pocock (MIT).
