# Credits

Airman Mode stands on the work of two people. Most of its skills are adapted from theirs, and its shape comes from ideas they published. Thank you both.

## Matt Pocock: [mattpocock/skills](https://github.com/mattpocock/skills)

Matt's skills gave Airman Mode its planning backbone, from the interview to the spec, the tickets, and the build:

- **Per-repo setup.** Config files the skills read, written once by an interview (`setup-matt-pocock-skills`).
- **The planning flow.** Grilling, then `to-spec`, then `to-tickets`, then implement.
- **Task graphs.** Tickets with blocking edges, a frontier, and subagents briefed with file pointers.
- **Bug discipline.** "Build the right feedback loop, and the bug is 90% fixed."
- **Domain language.** A glossary and ADRs written the moment a term or decision settles.
- **Wayfinding.** A map of decision tickets for work too big for one session.
- **Hard versus soft dependencies.** Only skills that cannot work without config point to setup.

## poteto: [pstack](https://github.com/cursor/plugins/tree/main/pstack)

poteto's pstack gave Airman Mode its rigor and its idea of named workflows:

- **Playbooks.** A named workflow per kind of task, which became Airman Mode's commands.
- **Prove it works.** Verify against the real artifact, not a proxy or a self-report.
- **Evidence-based bug fixing.** Every shipped line traces to runtime evidence, and the failing repro lands before the fix.
- **Tool adapters.** A thin per-tool guide instead of tool names in every skill.
- **Mode descriptions.** A description that keeps a workflow from starting on its own.
- **Enforcement order.** Fix a repeated mistake with structure first, then types, lint, and CI, then tests, and only then docs.

## What came from where

| Airman Mode | Based on | License |
| --- | --- | --- |
| **Commands** | | |
| `/new-feature` | poteto's [feature playbook](https://github.com/cursor/plugins/blob/main/pstack/skills/poteto-mode/playbooks/feature.md), plus Matt's [`to-spec`](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-spec) and [`to-tickets`](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-tickets) | MIT |
| `/fix-bug` | Matt's [`diagnosing-bugs`](https://github.com/mattpocock/skills/tree/main/skills/engineering/diagnosing-bugs), plus poteto's [bug-fix playbook](https://github.com/cursor/plugins/blob/main/pstack/skills/poteto-mode/playbooks/bug-fix.md) | MIT |
| `/new-app` | Matt's [`wayfinder`](https://github.com/mattpocock/skills/tree/main/skills/engineering/wayfinder) and [`retro`](https://github.com/mattpocock/skills/tree/main/skills/engineering/retro), plus poteto's [multi-phase plan playbook](https://github.com/cursor/plugins/blob/main/pstack/skills/poteto-mode/playbooks/multi-phase-plan.md) | MIT |
| **Skills** | | |
| `implement` | Matt's [`implement`](https://github.com/mattpocock/skills/tree/main/skills/engineering/implement) and [`implement-spec`](https://github.com/mattpocock/skills/tree/main/skills/engineering/implement-spec) | MIT |
| `setup-airman` | Matt's [`setup-matt-pocock-skills`](https://github.com/mattpocock/skills/tree/main/skills/engineering/setup-matt-pocock-skills) | MIT |
| `grilling`, `grill-me` | Matt's [`grilling`](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling) and [`grill-me`](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me) | MIT |
| `to-spec`, `to-tickets` | Matt's [`to-spec`](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-spec) and [`to-tickets`](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-tickets) | MIT |
| `wayfinder` | Matt's [`wayfinder`](https://github.com/mattpocock/skills/tree/main/skills/engineering/wayfinder) | MIT |
| `domain-modeling` | Matt's [`domain-modeling`](https://github.com/mattpocock/skills/tree/main/skills/engineering/domain-modeling) | MIT |
| `prototype` | Matt's [`prototype`](https://github.com/mattpocock/skills/tree/main/skills/engineering/prototype) | MIT |
| `research` | Matt's [`research`](https://github.com/mattpocock/skills/tree/main/skills/engineering/research) | MIT |
| `tdd` | Matt's [`tdd`](https://github.com/mattpocock/skills/tree/main/skills/engineering/tdd) | MIT |
| `diagnosing-bugs` | Matt's [`diagnosing-bugs`](https://github.com/mattpocock/skills/tree/main/skills/engineering/diagnosing-bugs) | MIT |
| `investigate` | poteto's [investigation playbook](https://github.com/cursor/plugins/blob/main/pstack/skills/poteto-mode/playbooks/investigation.md) and [`why`](https://github.com/cursor/plugins/tree/main/pstack/skills/why) | MIT |
| `code-review` | Matt's [`code-review`](https://github.com/mattpocock/skills/tree/main/skills/engineering/code-review) | MIT |
| `improve-codebase-architecture` | Matt's [`improve-codebase-architecture`](https://github.com/mattpocock/skills/tree/main/skills/engineering/improve-codebase-architecture) | MIT |
| `codebase-design` | Matt's [`codebase-design`](https://github.com/mattpocock/skills/tree/main/skills/engineering/codebase-design) | MIT |
| `handoff` | Matt's [`handoff`](https://github.com/mattpocock/skills/tree/main/skills/productivity/handoff) | MIT |
| `retro` | Matt's [`retro`](https://github.com/mattpocock/skills/tree/main/skills/engineering/retro), plus poteto's [`correct`](https://github.com/cursor/plugins/tree/main/pstack/skills/correct) | MIT |
| `teach` | Matt's [`teach`](https://github.com/mattpocock/skills/tree/main/skills/productivity/teach) | MIT |

Each adapted `SKILL.md` names its source at the bottom. The changes are mostly the same everywhere: point to `/setup-airman` and `docs/agents/`, keep tickets in `docs/work/`, and remove tool-specific wording.

`unslop`, `shadcn`, `ui-ux-pro-max`, and `no-use-effect` don't come from either project. See each skill's folder for its background.

## Licenses

Both upstream projects are MIT licensed. Airman Mode is licensed under [Apache 2.0](../LICENSE). Adapted files keep their attribution to the original authors.
