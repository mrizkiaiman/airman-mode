---
name: fix-bug
description: Command. Run only when the user types /fix-bug. Diagnoses a bug with a red-capable feedback loop, lands the smallest evidence-backed fix behind a failing test, and proves it.
disable-model-invocation: true
---

# Fix bug

Treat the text after `/fix-bug` as the bug report: a symptom, an error message, or a log. If it is empty, ask for the symptom and stop.

Every line you ship must trace back to runtime evidence. A change that "might also help" is a hypothesis, not a fix, and it doesn't ship.

## Before you start

- Read `docs/agents/verify.md` for the test, typecheck, lint, and run commands. If it is missing, ask the user to run `/setup-airman`, or to give you the commands to use for this session.
- Read `docs/agents/glossary-and-decisions.md` if it exists, and the glossary and ADRs it points to.
- Redact secrets in everything you show. Write `<REDACTED>`.

## Steps

Report progress at each step in one or two lines.

1. **Diagnose.** Follow the `diagnosing-bugs` skill from Phase 1 through Phase 4:
   - Build a red-capable feedback loop for this exact symptom, and run it once.
   - Reproduce it, then minimise it.
   - Rank 3–5 falsifiable hypotheses. Show the list to the user and carry on with your own ranking; they can interrupt to re-rank.
   - Instrument one variable at a time until one hypothesis survives with runtime evidence.

   Don't edit production code before the loop goes red. When evidence refutes a hypothesis, revert every change it motivated.

2. **Branch.** If you're on the default branch, create `fix/<short-slug>` and switch to it.

3. **Lock the bug in a test.** Follow the `tdd` skill. Turn the minimised repro into a failing test at a seam that exercises the real bug pattern. Run it and show it failing. Commit the test on its own, with a message that names the symptom.

   If no correct seam exists, say so. That is a finding: the code's structure is keeping the bug from being locked down. Then go on to step 4 without the test.

4. **Fix.** Apply the smallest change the evidence justifies. Run the test and show it passing. Commit the fix, and state the confirmed root cause in the commit message.

5. **Verify.**
   - Re-run the original, un-minimised feedback loop.
   - Run the full test suite, typecheck, and lint from `verify.md`.
   - If the bug was visible on a surface (a page, an endpoint, a CLI), check that surface too.

   "Inconclusive" or the wrong surface is not a pass. Report it as unverified.

6. **Clean up.** Remove every tagged debug line (grep the `[DEBUG-` prefix) and every throwaway harness. Commit if anything changed.

7. **Review.** Run the `code-review` skill on the diff since the branch point, in a fresh context: a subagent, or a separate session if your tool has no subagents. Look hard for symptom patches that leave the root cause alive. Fix accepted findings in new commits.

If the hunt has to stop before step 4, write what you know to `docs/work/<bug-slug>/notes.md`: the loop command, the hypotheses ruled out with their evidence, and the current lead. The next session can resume from there.

## Stop when

- No feedback loop can be built. List what you tried, then ask for access to an environment that reproduces it, a redacted artifact (a log, a HAR file, a recording), or permission to add temporary instrumentation. Don't guess at a fix without a loop.
- The fix needs a change outside the bug's scope, such as a migration, a public API change, or a dependency upgrade. Describe it and ask.

Never push or open a pull request unless the user asks.

## Reply

- **Broken:** what the user saw.
- **Root cause:** the hypothesis that survived, and the evidence that confirmed it.
- **Fix:** what changed, and the commits.
- **Proof:** the feedback loop output failing before the fix and passing after, plus the check results.
- **Open:** anything unverified, a missing test seam, or review findings you didn't fix.

---

Built on [`diagnosing-bugs`](https://github.com/mattpocock/skills/tree/main/skills/engineering/diagnosing-bugs) by Matt Pocock (MIT) and poteto's [bug-fix playbook](https://github.com/cursor/plugins/blob/main/pstack/skills/poteto-mode/playbooks/bug-fix.md) (MIT).
