---
name: new-feature
description: Command. Run only when the user types /new-feature. Builds a brand-new feature. Sizes it first, then either builds and verifies a small one directly, or plans a large one into a spec and tickets and stops.
disable-model-invocation: true
---

# New feature

Treat the text after `/new-feature` as the feature request. If it is empty, ask what to build and stop.

This command is for new features only. If the request is to fix something that is broken, suggest `/fix-bug` instead. If it is to redesign an existing page without new behavior, suggest `/revamp-page`.

## Before you start

- Read `docs/agents/glossary-and-decisions.md` if it exists, and the glossary and ADRs it points to.
- The small path needs `docs/agents/verify.md`. The large path needs `docs/agents/issue-tracker.md`. If the file the chosen path needs is missing, stop and ask the user to run `/setup-airman`.

## 1. Size the work

Read the code the feature will touch, then decide:

- **Small** when all of these hold: it touches one or two files, the approach is obvious with no real design choice, and it adds no new data model or public interface.
- **Large** otherwise.

State the verdict and the reason in one line. If the user disagrees, follow their call.

## 2a. Small path

1. **Trace.** Read the code the feature plugs into, and how it is called today.
2. **Settle the shape.** Before writing logic, decide the data structures, the function signatures, and how a caller will use them. Prefer a structure that makes the logic obvious, such as a typed model, a lookup table, or a state machine, over scattered conditionals. Say what you chose in one or two lines.
3. **Branch.** If you're on the default branch, create `feature/<short-slug>` and switch to it.
4. **Build.** Where a cheap test path exists, use the `tdd` skill: one failing test, then only the code to pass it.
5. **Verify.** Run the single test file and typecheck often, then the full test suite, typecheck, and lint from `verify.md`. If the feature has a visible surface (a page, an endpoint, a CLI), run the app and exercise it. "Inconclusive" counts as a failure.
6. **Review.** Run the `code-review` skill on the branch diff in a fresh context: a subagent, or a separate session if your tool has no subagents. Fix accepted findings.
7. **Commit** in small units, each one verified.

## 2b. Large path

1. **Grill.** Use the `grilling` skill until you and the user share an understanding of the feature. When new domain terms or hard-to-reverse decisions come up, use the `domain-modeling` skill to record them.
2. **Spec.** Use the `to-spec` skill to write the spec to the tracker (for local markdown, `docs/work/<slug>/spec.md`). Agree the test seams with the user before writing.
3. **Tickets.** Use the `to-tickets` skill to split the spec into thin end-to-end tickets with `Blocked by` edges.
4. **Stop.** Don't write application code. Tell the user to review the tickets, then build them with the `implement` skill (`/implement docs/work/<slug>`).

## Stop when

- The user disagrees with the size verdict and hasn't said which path to take.
- Grilling hasn't reached a shared understanding.
- The large path reaches its tickets. Large features never go straight to code.
- Never push or open a pull request unless the user asks.

## Reply

- **Small:** what you built, the shape you chose and why, the verification output, the commits, and anything left open.
- **Large:** the spec path, the tickets with their blocking edges, and the next step.

---

The small path follows poteto's [feature playbook](https://github.com/cursor/plugins/blob/main/pstack/skills/poteto-mode/playbooks/feature.md) (MIT). The large path uses Matt Pocock's [`grilling`](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling), [`to-spec`](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-spec), and [`to-tickets`](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-tickets) (MIT).
