---
name: setup-airman
description: Configure this repo for Airman Mode. Sets up where specs and tickets live, where the glossary and ADRs live, and how to test, typecheck, lint, and run the app. Run once per repo before the first Airman Mode command.
disable-model-invocation: true
---

# Setup Airman

Write the per-repo config that Airman Mode commands read:

- **Issue tracker**: where specs and tickets live. Local markdown in `docs/work/` by default.
- **Glossary and decisions**: where `GLOSSARY.md` and ADRs live, and how to use them.
- **Verify**: the commands that prove a change works.

This is a prompt-driven skill, not a script. Explore, present what you found, confirm with the user, then write.

If the user asks you to check the setup without changing anything, run steps 1 and 2 against the existing `docs/agents/` files, report any drift from the templates in this folder, and stop.

## 1. Explore

Read what exists. Don't assume.

- `git remote -v`: is there a GitHub or GitLab remote? Which repo?
- `AGENTS.md` and `CLAUDE.md` at the root: does either exist? Is there already an `## Agent skills` block?
- `GLOSSARY.md`, `GLOSSARY-MAP.md`, and the legacy `CONTEXT.md` / `CONTEXT-MAP.md`. If a legacy file exists, offer to `git mv` it to its `GLOSSARY` name.
- `docs/adr/` and any `src/*/docs/adr/`.
- `docs/agents/` and `docs/work/`: has this setup run before?
- How checks run today: `package.json` scripts, `Makefile`, `justfile`, `pyproject.toml`, `Cargo.toml`, `go.mod`, and CI workflows such as `.github/workflows/*.yml` or `.gitlab-ci.yml`.
- Monorepo signals: `pnpm-workspace.yaml`, a `workspaces` field in `package.json`, or a populated `packages/*` with its own sources. Without them, treat the repo as single-context.

## 2. Present findings

Summarise what is present and what is missing in a few lines. Then take the sections below in order: one section, one answer, then the next.

Lead each section with the recommended answer, so the user can accept it in a word. Skip a section entirely when exploration already settled it.

### Section A: Issue tracker

> Specs and tickets need a home. `to-spec`, `to-tickets`, and the Airman Mode commands read from and write to it.

Recommend **local markdown** unless the user already tracks this repo's work elsewhere. Options:

- **Local markdown** (recommended): files in `docs/work/<slug>/`, committed. Every tool can read them.
- **GitHub**: GitHub Issues through the `gh` CLI. Offer it when a remote points at GitHub.
- **GitLab**: GitLab Issues through the `glab` CLI. Offer it when a remote points at GitLab.
- **Other** (Jira, Linear, ...): ask the user to describe the workflow in one paragraph, and record it as prose.

A GitHub or GitLab tracker needs a reachable repo. When the user picks one and no remote points at that host, get the URL and wire it up before going further. Done when `gh repo view` or `glab repo view` prints the project from inside this directory. If it can't, stop and say what is missing.

### Section B: Glossary and decisions

Default to **single-context**: one `GLOSSARY.md` at the root and ADRs in `docs/adr/`. Write it without asking.

Offer **multi-context** (a root `GLOSSARY-MAP.md` pointing to one `GLOSSARY.md` per context) only when exploration found monorepo signals.

### Section C: Verify

Propose a command for each check, taken from what exploration found:

- Install
- Test, all
- Test, one file
- Typecheck, where the language has one
- Lint
- Run the app, with its local URL if it serves one
- CI: which workflow runs the checks

Ask the user to confirm or correct the list. When a check has no command, write `none` and name the gap in one line. A repo with no test, lint, or CI job is a finding worth fixing, not a neutral default.

## 3. Confirm

Show the user a draft of:

- the `## Agent skills` block for `AGENTS.md`
- `docs/agents/issue-tracker.md`
- `docs/agents/glossary-and-decisions.md`
- `docs/agents/verify.md`

Let them edit before you write.

## 4. Write

### `AGENTS.md`

Write the block to `AGENTS.md` at the repo root, creating the file if needed. If the block already exists, update it in place and leave the rest of the file alone. If the repo also has a `CLAUDE.md`, ask whether to add the same block there.

```markdown
## Agent skills

- **Tickets:** [one-line summary, e.g. "local markdown in `docs/work/`"]. See `docs/agents/issue-tracker.md`.
- **Glossary and decisions:** [single-context or multi-context]. See `docs/agents/glossary-and-decisions.md`.
- **Verify:** test, typecheck, lint, and run commands. See `docs/agents/verify.md`.
```

Keep the block to these three lines. `AGENTS.md` loads into every session, so it holds pointers, not rules.

### `docs/agents/`

Start from the templates in this folder:

- [issue-tracker-local.md](./issue-tracker-local.md): local markdown
- [issue-tracker-github.md](./issue-tracker-github.md): GitHub
- [issue-tracker-gitlab.md](./issue-tracker-gitlab.md): GitLab
- [glossary-and-decisions.md](./glossary-and-decisions.md): glossary and ADR rules, plus the chosen layout
- [verify.md](./verify.md): the confirmed commands

For an "other" tracker, write `docs/agents/issue-tracker.md` from the user's description.

Don't create `GLOSSARY.md`, `docs/adr/`, or `docs/work/` now. The skills that need them create them when they have something to write.

## 5. Done

Tell the user setup is complete and which commands and skills now read these files: `/new-feature`, `/fix-bug`, `/new-app`, and `implement`. Say they can edit `docs/agents/*.md` by hand, and only need to re-run this skill to switch trackers or check for drift.

---

Adapted from [`setup-matt-pocock-skills`](https://github.com/mattpocock/skills/tree/main/skills/engineering/setup-matt-pocock-skills) by Matt Pocock (MIT). Changes: no triage labels, a new verify section, local markdown by default in `docs/work/`, and `AGENTS.md` as the instruction file.
