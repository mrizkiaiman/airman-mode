---
name: implement
description: Build a spec or a set of tickets ticket by ticket from the frontier, verify each ticket before the next, then run the full checks and a fresh-context review. Use after /new-feature, /new-app, or /revamp-page has written tickets, or when the user asks to implement a spec or ticket.
disable-model-invocation: true
---

# Implement

Treat the text after `/implement` as what to build: a work folder (`docs/work/<slug>`), a spec path, a ticket path, or a ticket number. If it is empty, list the work folders that still have `open` or `in-progress` tickets and ask which one. If the reference is ambiguous, ask.

## Before you start

- Read `docs/agents/issue-tracker.md` and `docs/agents/verify.md`. If either is missing, stop and ask the user to run `/setup-airman`.
- Read `docs/agents/glossary-and-decisions.md` if it exists, and the glossary and ADRs it points to.

## Steps

1. **Load the work.** Read the spec and every ticket. Build the task graph from the `Blocked by` edges, and find the **frontier**: the `open` tickets whose blockers are all `done`. If you were given a single ticket, the work is that ticket alone; state its title before starting.

2. **Branch.** If you're on the default branch, create one branch for the whole work folder, named after its slug (for example `feature/<slug>`), and switch to it.

3. **Work the frontier.** For each frontier ticket, lowest number first:
   1. **Claim** it, the way `issue-tracker.md` says (for local markdown, `Status: in-progress`), before writing code.
   2. **Build** it with the `tdd` skill, at the seams the spec agreed on: one failing test, then only the code to pass it.
   3. **Verify** it. Run the typecheck and the single test file often while working. Check every acceptance criterion in the ticket.
   4. **Close** it the way `issue-tracker.md` says (for local markdown, `Status: done` plus a one-line note under `## Comments`), and commit.

   Closing a ticket can unblock others. Recompute the frontier after each one, and continue until it is empty.

   **Parallel tickets:** frontier tickets don't depend on each other. If your tool has subagents, you may give each frontier ticket to its own subagent with a fresh context. Brief it with paths to the spec, the ticket, and `verify.md` instead of pasting their text, and have it report back only the result and the commits. Without subagents, build the tickets one at a time.

4. **Run the full checks.** Run the full test suite, typecheck, and lint from `verify.md`. If the work has a visible surface (a page, an endpoint, a CLI), run the app and exercise it against the spec. "Inconclusive" counts as a failure.

5. **Review.** Run the `code-review` skill on the branch diff against its base, in a fresh context: a subagent, or a separate session if your tool has no subagents. Fix the findings you accept in new commits. Refactors suggested by the review land here, after the tests are green.

## Stop when

- A ticket turns out to be wrong, too big, or blocked by something outside the plan. Add a note under its `## Comments`, leave it `open`, and ask the user.
- A check fails and the fix would go beyond the current ticket's scope.
- Never push or open a pull request unless the user asks.

## Reply

- **Built:** the tickets completed, each with its commits.
- **Checks:** the full check results.
- **Review:** findings fixed and findings left open, with reasons.
- **Open:** tickets still open or blocked, and anything unverified.

---

Adapted from [`implement`](https://github.com/mattpocock/skills/tree/main/skills/engineering/implement) and [`implement-spec`](https://github.com/mattpocock/skills/tree/main/skills/engineering/implement-spec) by Matt Pocock (MIT). The verify-each-unit cadence follows poteto's [feature playbook](https://github.com/cursor/plugins/blob/main/pstack/skills/poteto-mode/playbooks/feature.md) (MIT).
