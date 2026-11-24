# Skills catalog

Skills do one job each. [Commands](../README.md#commands) chain them into workflows, and you can also run any skill on its own by name.

| Group | Skills |
| --- | --- |
| [Setup](#setup) | `setup-airman` |
| [Planning](#planning) | `grilling`, `grill-me`, `to-spec`, `to-tickets`, `wayfinder`, `domain-modeling`, `prototype`, `research` |
| [Building](#building) | `implement`, `tdd`, `diagnosing-bugs`, `investigate`, `code-review`, `improve-codebase-architecture`, `codebase-design` |
| [Sessions](#sessions) | `handoff`, `retro` |
| [Writing and learning](#writing-and-learning) | `unslop`, `teach` |
| [Frontend](#frontend) | `shadcn`, `ui-ux-pro-max`, `no-use-effect` |

## Which command uses which skill

| Skill | `/new-feature` | `/fix-bug` | `/new-app` |
| --- | :-: | :-: | :-: |
| `setup-airman` | | | ● |
| `grilling` | ● | | ● |
| `domain-modeling` | ● | | ● |
| `to-spec` | ● | | ● |
| `to-tickets` | ● | | ● |
| `wayfinder` | | | ● |
| `prototype` | | | ● |
| `research` | | | ● |
| `diagnosing-bugs` | | ● | |
| `tdd` | ● | ● | |
| `code-review` | ● | ● | |

After `/new-feature` or `/new-app` writes tickets, the `implement` skill builds them.

---

## Setup

### setup-airman

Configures one repo: tracker, glossary and decisions, and verify commands. It writes `docs/agents/*.md` and a pointer block in `AGENTS.md`.

**Run** once per repo · **Details** [Repo setup](setup.md) · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/setup-matt-pocock-skills), adapted

## Planning

### grilling

Interviews you in rounds until you share an understanding of a plan. Each round asks every question that is answerable now, each with a recommended answer. It looks up facts itself and leaves the decisions to you.

**Use when** you want a plan stress-tested · **Used by** `/new-feature`, `/new-app` · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)

### grill-me

A shortcut you type to start `grilling` yourself.

**Use when** you want an interview without a command around it · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me)

### to-spec

Turns the conversation so far into a spec, with no new interview: problem, solution, user stories, and the seams where it will be tested. It publishes the spec to the tracker.

**Output** `docs/work/<slug>/spec.md` · **Used by** `/new-feature`, `/new-app` · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-spec)

### to-tickets

Splits a spec into thin vertical slices. Each one cuts through every layer end to end, and each declares which tickets block it.

**Output** `docs/work/<slug>/issues/NN-*.md` · **Used by** `/new-feature`, `/new-app` · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-tickets)

### wayfinder

Plans work too big for one session as a map of decision tickets (research, prototype, grilling, or task). It resolves them one per session until the way to the destination is clear.

**Output** `docs/work/<slug>/map.md` and tickets · **Used by** `/new-app` · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/wayfinder)

### domain-modeling

Sharpens the project's language while you design. It challenges terms against the glossary, invents edge-case scenarios, and writes terms and ADRs the moment they settle.

**Output** `GLOSSARY.md`, `docs/adr/` · **Used by** `/new-feature`, `/new-app` · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/domain-modeling)

### prototype

Builds throwaway code that answers one design question. That's either a logic demo for "does this state model feel right?" or switchable UI variants for "what should this look like?". Only the decision survives, and the code stays on a throwaway branch.

**Use when** an experiment can settle a choice faster than talking · **Used by** `/new-app` · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/prototype)

### research

Investigates a question against primary sources such as official docs, source code, and specs, in a background agent. It saves cited findings as a markdown file.

**Output** a findings file in the repo · **Used by** `/new-app` · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/research)

## Building

### implement

Builds a spec ticket by ticket from the frontier. It claims each ticket, builds it test-first, checks its acceptance criteria, closes it, and commits, then runs the full checks and a review in a fresh context. Frontier tickets can go to parallel subagents when the tool has them.

**Use when** `/new-feature` or `/new-app` has written tickets · **Run** `/implement docs/work/<slug>` · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/implement), adapted

### tdd

Test-first development in vertical slices: one failing test, then only the code to pass it, at seams agreed with you up front. Refactoring belongs to the review.

**Used by** `/new-feature`, `/fix-bug`, `implement` · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/tdd)

### diagnosing-bugs

A discipline for hard bugs and performance regressions, in six phases: feedback loop, then reproduce and minimise, hypothesise, instrument, fix with a regression test, and clean up.

**Used by** `/fix-bug` · **Details** [`/fix-bug` steps](commands/fix-bug.md#steps) · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/diagnosing-bugs)

### investigate

Answers a read-only question about the code, such as "how does X work?" or "why was Y built this way?". It traces the code and the git history behind it. If the answer calls for a change, it hands off to `/fix-bug` or `/new-feature`.

**Output** Overview, key concepts, how it works, where things live, and gotchas · **Source** new, based on poteto's [investigation playbook](https://github.com/cursor/plugins/blob/main/pstack/skills/poteto-mode/playbooks/investigation.md)

### code-review

Reviews a diff in a fresh context along two axes in parallel. **Standards** asks whether it follows the repo's rules. **Spec** asks whether it does what the spec or ticket asked.

**Used by** `/new-feature`, `/fix-bug`, `implement` · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/code-review)

> [!NOTE]
> In Claude Code, this skill replaces the bundled `/code-review` once installed. The bundled `/review` alias still runs Claude Code's own review.

### improve-codebase-architecture

Scans the codebase for shallow modules worth deepening, presents them as an HTML report, then grills you through the one you pick.

**Use when** the code fights you on every change · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/improve-codebase-architecture)

### codebase-design

✅ The shared vocabulary for deep modules: module, interface, depth, seam, adapter, leverage, and locality. It also covers how to deepen a cluster given its dependencies, and a design-it-twice pattern that drafts several interfaces in parallel subagents and compares them.

**Use when** you're designing a module's interface or deciding where a seam goes · **Used by** `improve-codebase-architecture`, `tdd` · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/codebase-design)

## Sessions

### handoff

Sums up the current session for the next agent. It points to existing files instead of copying them, and redacts secrets. It prints the handoff in the chat, ready to paste into the next session.

**Use when** you switch tools or stop mid-task · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/productivity/handoff)

### retro

Looks back at a session and suggests fixes to the agent's environment rather than its prompt: navigation pointers, automated checks, coding standards, a leaner `AGENTS.md`, cheaper tool calls. It prefers fixes that can be enforced. That means structure first, then types, lint, and CI, then tests, with written rules last.

**Use when** a session took too long or repeated a mistake · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/engineering/retro), with the order from poteto's [`correct`](https://github.com/cursor/plugins/tree/main/pstack/skills/correct)

## Writing and learning

### unslop

Removes signs of AI writing and restores a human voice.

**Use when** you're writing docs, PR descriptions, or replies

### teach

Teaches a topic over several sessions, with a mission, lessons, references, and records of what you learned.

**Use when** you want to understand something, not just get it summarized · **Source** [Matt Pocock](https://github.com/mattpocock/skills/tree/main/skills/productivity/teach)

## Frontend

### shadcn

Adds, searches, fixes, styles, and composes shadcn/ui components and registries.

**Use when** working in a shadcn/ui project

### ui-ux-pro-max

A searchable design database of styles, palettes, font pairings, UX guidelines, and chart types across major stacks, used to plan and review interfaces.

**Use when** designing or reviewing UI

### no-use-effect

Enforces a no-direct-`useEffect` rule in React. It suggests derived state, event handlers, `useMemo`, `useSyncExternalStore`, data-fetching libraries, or key-based resets instead.

**Use when** writing React or React Native · **Background** [You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect)
