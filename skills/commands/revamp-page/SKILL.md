---
name: revamp-page
description: Command. Run only when the user types /revamp-page. Redesigns an existing page without losing what it does. Records a screenshot baseline and a behavior inventory, locks behavior in tests, picks a direction from variants or a supplied design, then builds a small revamp or plans a large one into tickets.
disable-model-invocation: true
---

# Revamp page

Treat the text after `/revamp-page` as the page and the goal: a route, URL, or file, plus what should get better. It may also include a design to follow, such as a Figma link, a mockup, or a reference screenshot. If no page is named, ask which page and stop.

A revamp changes how a page looks and is laid out. It keeps what the page does. Every behavior the page has today survives unless the user drops it by name.

This command is for existing pages. A new page or new behavior is `/new-feature`. Something broken is `/fix-bug`.

## Before you start

- Read `docs/agents/verify.md`. You need its run command to see the page. If it is missing, stop and ask the user to run `/setup-airman`.
- The large path also needs `docs/agents/issue-tracker.md`. If it is missing when you reach that path, stop and ask the user to run `/setup-airman`.
- Read `docs/agents/glossary-and-decisions.md` if it exists, and the glossary and ADRs it points to.
- Find the repo's design system: theme or token files, the component library, and `components.json` for shadcn/ui. If the page is React, the `no-use-effect` skill applies to every line you write.
- Use dev or seed data. Don't capture real customer data or secrets in a screenshot.

## Screenshots

Every screenshot in this command follows this order:

1. **Take it yourself.** Run the app with the run command from `verify.md`, and capture the screen with whatever your tool can drive: a browser tool, a headless browser script, or the repo's end-to-end runner.
2. **If you can't, ask the user.** Say in one line why you can't. Then give an exact list: the URL, the viewport, the state, and the file name for each screenshot. Ask them to save the files to `docs/work/<slug>/screens/`.
3. **Wait for them.** Don't go on until every listed screenshot exists. Don't skip one, don't infer a layout from the code, and don't describe a screen you haven't seen.

Capture a 1440px desktop and a 390px mobile viewport, unless the repo targets other sizes. Reach each state with seed data, a mocked response, or a URL parameter. Name files `before-<state>-<viewport>.png` and `after-<state>-<viewport>.png`.

## Steps

Report progress at each step in one or two lines.

1. **Baseline.** Read the page's code and how it gets its data. Take the before screenshots of every state the page has, such as normal, loading, empty, and error. Write `docs/work/<slug>/baseline.md` with:
   - The route, the entry file, and the screenshot list.
   - A behavior inventory, one line per item with an ID (`B1`, `B2`, …): the data shown, each action and what it triggers, links and URL parameters, states, form validation, side effects such as analytics or URL sync, and the keyboard path and labels.
   - A status per item. Every item starts as `Keep`.

   This file is the contract for the rest of the command.

2. **Lock behavior.** If you're on the default branch, create `revamp/<slug>` and switch to it. Use the `tdd` skill to write characterization tests: tests that record what the page does today. Cover each baseline item that has a cheap seam.
   - Query by role, label, and visible text. Never query by class name or DOM structure. The layout is about to change, and those tests would break for the wrong reason.
   - Run them on the current code. They must pass. If one fails, either the test is wrong or you found a bug. A bug is out of scope: note it, suggest `/fix-bug`, and don't fix it here.
   - Mark each item in `baseline.md` with its test, or with `manual` if no seam exists. If the repo has no test setup, every item is `manual`. Say so.
   - Commit the tests and `baseline.md` on their own.

3. **Brief.** Use the `grilling` skill, kept short. Settle:
   - What is wrong with the page today, and who uses it for what.
   - Which baseline items change or drop. The default is `Keep`. Record each `Change` or `Drop` with the user's reason.
   - The scope: visual (spacing, type, color), layout (arrangement and hierarchy), or flow (steps and interactions).

   If the revamp needs new data, a new endpoint, or a new data model, that part is out of scope. Say so, suggest `/new-feature` for it, and carry on with the rest only if the user agrees.

   Then size the work:
   - **Small** when all of these hold: one page, visual or layout scope, and existing data only.
   - **Large** otherwise: several pages, flow scope, or enough sections that each deserves its own review.

   State the verdict and the reason in one line. If the user disagrees, follow their call. Write the brief and the verdict under `## Brief` in `baseline.md`.

4. **Direction.** Pick what the page will look like.
   - **The user supplied a design.** Skip the variants. Read the design, through your tool's design integration if it has one. List every place it conflicts with a `Keep` item, and ask the user how to resolve each one.
   - **No design.** Use the `ui-ux-pro-max` skill to find a direction that fits the page's purpose and users. Keep the repo's tokens: colors, fonts, spacing scale, and radius. A token change affects every page, so if the brief asks for one, say so and ask before going on. If the repo has no design system, generate one with `ui-ux-pro-max` and persist it. It becomes the source for step 5.

     Then use the `prototype` skill's UI branch, sub-shape A: three structurally different variants on the existing route, switched by `?variant=`, with the page's real data. Take a screenshot of each variant at both viewports, following the screenshot rules.

   **Stop** until the user picks a variant, or a mix of parts from several. Write the choice and the reason under `## Direction` in `baseline.md`.

5. **Build or plan.**

   **Small path: build.**
   - Fold the chosen variant in the way the `prototype` skill describes. Move the switcher and the losing variants off this branch, and rewrite the winner properly.
   - Build from the repo's design system and components. If the repo uses shadcn/ui, use the `shadcn` skill.
   - Don't touch data fetching, API calls, routes, or URL parameters unless a baseline item is marked `Change`.
   - Run the single test file and the typecheck often. The characterization tests stay green. A failing test means you broke a behavior: fix the code, not the test. Only a `Change` or `Drop` item may update its test, in the same commit, with the item ID in the message.
   - Commit in small verified units, such as one section per commit.

   **Large path: plan.**
   - Use the `to-spec` skill to write the spec to the tracker. The brief and the direction are the solution. The `Keep` items in `baseline.md` are acceptance criteria. The characterization tests are the test seams.
   - Use the `to-tickets` skill to split it into one ticket per section or page. Each ticket lists the baseline IDs it must keep and needs after screenshots of its section.
   - **Stop.** Don't build the revamp. Tell the user to review the tickets, then run `/implement docs/work/<slug>`.

6. **Verify** (small path).
   - Run the full test suite, typecheck, and lint from `verify.md`.
   - Take the after screenshots at the same viewports and states as the before set, following the screenshot rules.
   - Walk through `baseline.md`. Check every `Keep` item by its test or by hand, and every `Change` or `Drop` item against the brief. Write `pass`, `fail`, or `unverified` per item under `## Results`.

   "Inconclusive" counts as a failure. Report it as unverified, never as done.

7. **Review** (small path).
   - Run the `code-review` skill on the diff since the branch point, in a fresh context: a subagent, or a separate session if your tool has no subagents. Give it `baseline.md`, and ask it to look for behavior that changed or disappeared without a `Change` or `Drop` entry.
   - Run the `ui-ux-pro-max` skill's review of existing UI on the after screenshots and the changed code: accessibility, touch targets, interaction states, contrast, and responsive layout.
   - Fix accepted findings in new commits, then re-run the step 6 checks they affect.

## Stop when

- No page is named, or the page can't be found.
- A screenshot can't be taken and the user hasn't supplied it yet.
- The revamp needs new data, an endpoint, or a data model, and the user hasn't said how to proceed.
- The brief asks for a change to the design tokens.
- A supplied design conflicts with a `Keep` item, until the user resolves it.
- The variants are up and the user hasn't picked one.
- The large path reaches its tickets. Large revamps never go straight to code.
- Never push or open a pull request unless the user asks.

## Reply

- **Small:**
  - What changed, section by section.
  - The direction and why it was chosen.
  - The before and after screenshot paths, in pairs.
  - The results table from `baseline.md`: kept, changed, dropped, and unverified.
  - The verification output, the commits, and anything left open.
- **Large:** the baseline path, the direction, the spec path, the tickets with their blocking edges, and the next step.

---

The variants step uses Matt Pocock's [`prototype`](https://github.com/mattpocock/skills/tree/main/skills/engineering/prototype) (MIT). The build, verify, and review loop follows poteto's [feature playbook](https://github.com/cursor/plugins/blob/main/pstack/skills/poteto-mode/playbooks/feature.md) (MIT). Characterization tests come from Michael Feathers' *Working Effectively with Legacy Code*.
