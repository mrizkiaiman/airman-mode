# Design decisions

This page records why Airman Mode is shaped the way it is, what was left out on purpose, and what gets built next.

## Principles

1. **Small, composable pieces.** Commands chain skills, and skills do one job.
2. **Files over chat.** Every step leaves its state in the repo, where any tool can read it.
3. **Evidence over claims.** A failing check comes before a fix, and a review in a fresh context comes before trust.
4. **Tool-neutral core.** Skills follow the open Agent Skills format. Tool details live in thin guides.
5. **Start small.** Add a skill when the same need shows up twice, not before.

## Decisions

| Area | Decision | Why |
| --- | --- | --- |
| **Shape** | Commands and skills. There's no router command | You know which job you're starting, so a router would only add a layer |
| **Format** | Everything is a `SKILL.md`. No launcher, and no tool-specific command files | Every major tool can call a skill directly, and several are deprecating their own command formats (Antigravity workflows, Codex custom prompts, Cursor commands) |
| **Install** | Skills install globally with the skills CLI. Config lives in each repo | Skills update in one place, and each repo keeps only what's specific to it |
| **Tools** | No tool is named in the core. Guides exist only for tools that get tested | An untested guide quietly goes out of date |
| **Tracker** | Local markdown in `docs/work/`, committed. GitHub and GitLab are options | Every tool can read files without logging in, and history stays with the code |
| **Config** | Three files in `docs/agents/`, and pointers only in `AGENTS.md` | `AGENTS.md` loads in every session, so it stays small |
| **Invocation** | Commands run only when typed. The description says so, and `disable-model-invocation` is set too | Several tools ignore the flag. The sentence in the description works everywhere |
| **Input** | Read from the message, never `$ARGUMENTS` | Only some tools fill in placeholders |
| **Composition** | Commands call skills, not other commands | Each command stays short and its context stays small |
| **`/new-feature`** | It sizes the work first. Small work gets built, large work stops at tickets | Small changes don't need a spec, and large ones deserve a human check before any code |
| **`/revamp-page`** | It writes a behavior inventory and characterization tests before any redesign, and needs before and after screenshots, asking you for them when the tool can't take them | A revamp's main risk is behavior that disappears without anyone noticing, and a screen nobody looked at proves nothing |
| **Git** | Branch off `main`, commit small verified units, commit a failing test before its fix, and never push without being asked | The history proves the work, and you stay in control of what leaves your machine |
| **Review** | A fresh context, ideally on a different model | The agent that wrote the code is the worst judge of it |
| **Handoff** | Printed in the chat, pasted as the first message of the next session | No file to hunt for, and no switching context |
| **Names** | Plain names that avoid tool built-ins such as `/review`, `/init`, and `/resume` | Short to type, with no clashes |
| **Upstream** | Adapted skills are copied in with their source URL | We control the wording, and the skills point to `/setup-airman` |

## Not now

These are good ideas that wait for a real need.

| Idea | From | Revisit when |
| --- | --- | --- |
| A router command (`/airman`) | poteto's `poteto-mode` | You often can't tell which command fits |
| Parallel attempts and multi-model panels (`arena`, `swarm`, `interrogate`) | pstack | Your tool can run subagents on different models |
| Triage labels and the `triage` skill | Matt Pocock | Other people start filing issues |
| A launcher or installer | — | Something that isn't a `SKILL.md` must ship, such as subagent definitions or hooks |
| Overnight and autopilot runs | pstack | Single-session commands are reliable |

## Roadmap

1. **Foundation**
   - [x] `setup-airman`
   - [x] Point `to-spec`, `to-tickets`, and `code-review` at `/setup-airman` instead of `/setup-matt-pocock-skills`
   - [x] Change `handoff` to print in the chat
2. **First command**
   - [x] `/fix-bug`, with `diagnosing-bugs` and `tdd` copied in
   - [ ] Try it in a real repo, including a review in a second tool
3. **The rest**
   - [x] `/new-feature` and `/new-app`, plus `implement` updated to work from the frontier
   - [x] `wayfinder`, `prototype`, `retro`, and the new `investigate`
   - [x] A `commands` group in `skills.sh.json` and `marketplace.json`
   - [x] Remove the planned markers from the docs
4. **Frontend**
   - [x] `/revamp-page`, with `prototype`, `ui-ux-pro-max`, `shadcn`, and `no-use-effect` wired in
5. **Field test**
   - [ ] Run each command once in a real repo, and record what differed per tool in its guide
   - [ ] Mark the tool guides as tested

## Influences

Full details are in [Credits](credits.md).

- **[Matt Pocock's skills](https://github.com/mattpocock/skills).** Per-repo setup, the spec and ticket flow, `diagnosing-bugs`, `wayfinder`, `domain-modeling`, and the hard-versus-soft dependency rule for config.
- **[poteto's pstack](https://github.com/cursor/plugins/tree/main/pstack).** Playbooks as named workflows, the "prove it works" bar, tool adapters, and descriptions that keep a mode from starting on its own.
