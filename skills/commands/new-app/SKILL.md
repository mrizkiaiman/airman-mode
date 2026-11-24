---
name: new-app
description: Command. Run only when the user types /new-app. Takes a new app from a loose idea to a spec and tickets across several sessions, by charting a map of decisions, settling them one per session, then adding guardrails and planning the first slice.
disable-model-invocation: true
---

# New app

Treat the text after `/new-app` as one of two things:

- **An idea** (free text): start phase 1.
- **A work folder** (`docs/work/<slug>`): continue its map, in phase 2 or phase 3.

If it is empty, look for a `docs/work/*/map.md` with open tickets and offer to continue it. Otherwise ask for the idea.

Each run does one phase step and then stops. Never start building the app itself. That is the `implement` skill's job.

## Before you start

- If the folder is not a git repo, offer to run `git init`.
- If `docs/agents/` doesn't exist, run the `setup-airman` skill first. In a brand-new repo, expect `verify.md` to be mostly `none`; phase 3 fills it in.
- Read `docs/agents/glossary-and-decisions.md` and the glossary and ADRs it points to, if they exist.

## Phase 1: Chart the map (one session)

Follow the `wayfinder` skill's "Chart the map" mode:

1. **Name the destination** with the `grilling` and `domain-modeling` skills. Default to "a spec for the first shippable slice (the MVP) that a developer can build from", unless the user wants something else.
2. **Map the frontier** breadth-first across the whole space, such as platform, data, auth, sync, hosting, and payments, as the idea needs.
3. **Write the map** to `docs/work/<slug>/map.md`, and the decision tickets you can already phrase to `docs/work/<slug>/issues/`, each with a `Type`.
4. **Start research** on the `research` tickets, in background subagents if your tool has them.
5. **Stop.** Tell the user to run `/new-app docs/work/<slug>` in the next session.

## Phase 2: Settle one decision (one session each)

Follow the `wayfinder` skill's "Work through the map" mode:

1. Take the first frontier ticket, or the one the user names, and claim it.
2. Resolve it by its type: `grilling` with the `grilling` and `domain-modeling` skills, `prototype` with the `prototype` skill, `research` with the `research` skill, or `task` by guiding the user through it.
3. Record the answer, close the ticket, and add a pointer under the map's Decisions so far. Turn any fog the answer cleared into new tickets.
4. **Stop** after one ticket, apart from research tickets. Tell the user what changed on the map and which ticket is next.

Move to phase 3 when the map has no open tickets and nothing left under Not yet specified.

## Phase 3: Commit to a plan (one session)

1. **Guardrails.** Make sure the repo has a test command, a typecheck command where the language has one, a lint command, and one CI job that runs all three. Add the smallest standard setup for the chosen stack where something is missing. Record the commands in `docs/agents/verify.md`.
2. **Spec.** Use the `to-spec` skill to write `docs/work/<slug>/spec.md` for the destination's first slice, built from the map's Decisions so far.
3. **Tickets.** Use the `to-tickets` skill to split the spec into end-to-end tickets with `Blocked by` edges. Keep the build tickets apart from the map's decision tickets, for example by numbering them after the last decision ticket.
4. **Stop.** Tell the user to review the tickets, then build them with the `implement` skill (`/implement docs/work/<slug>`).

## Stop when

- At the end of every phase step, as above.
- When a decision needs the user and they aren't there. Never answer the user's side of a grilling ticket yourself.
- Never push or open a pull request unless the user asks.

## Reply

- **Phase 1:** the destination, the map path, the tickets created by type, and the research started.
- **Phase 2:** the decision made, files written (glossary, ADRs, prototype branch), how the map changed, and the next ticket.
- **Phase 3:** the guardrails added, the spec path, the tickets, and the next command.

---

Built on Matt Pocock's [`wayfinder`](https://github.com/mattpocock/skills/tree/main/skills/engineering/wayfinder), [`to-spec`](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-spec), and [`to-tickets`](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-tickets) (MIT). The guardrails step follows his [`retro`](https://github.com/mattpocock/skills/tree/main/skills/engineering/retro), and the dependency-first planning follows poteto's [multi-phase plan playbook](https://github.com/cursor/plugins/blob/main/pstack/skills/poteto-mode/playbooks/multi-phase-plan.md) (MIT).
