# Airman Stack

A collection of public agent skills for coding, planning, research, and project work. Each public skill is a separate `SKILL.md` package that the `skills` CLI can install. Repository-only workflows live under `learning-records/skills/` and are not included in public skill indexes.

## Install

List the public skills in the stack:

```bash
npx skills add mrizkiaiman/airman-stack --list
```

Install one public skill:

```bash
npx skills add mrizkiaiman/airman-stack --skill research
```

Install several public skills:

```bash
npx skills add mrizkiaiman/airman-stack \
  --skill grill-me \
  --skill research \
  --skill teach
```

Install every public skill globally:

```bash
npx skills add mrizkiaiman/airman-stack --skill '*' --global
```

The `--skill` flag takes skill names, not group names. `Development` and `Productivity` organize the public list for browsing. Repository-only workflows are not included in the public list.

## Skills

### Development

Skills for writing, reviewing, and planning code.

- `code-review`: Review changes against project standards and requirements.
- `grill-with-docs`: Question a plan and record the decisions.
- `grilling`: Challenge a plan or design before implementation.
- `handoff`: Prepare a concise handoff for another agent or session.
- `implement`: Implement work from a specification or ticket.
- `improve-codebase-architecture`: Find and assess architecture improvements.
- `no-use-effect`: Replace direct React `useEffect` usage with other patterns.
- `shadcn`: Add, debug, and customize shadcn/ui components.
- `to-spec`: Turn a conversation into a structured specification.
- `to-tickets`: Break a plan into implementation tickets.
- `ui-ux-pro-max`: Plan and review product interfaces.
- `unslop`: Remove generic, artificial-sounding writing.

### Productivity

Skills for research, learning, and planning.

- `grill-me`: Improve an idea through a focused interview.
- `research`: Research a topic and save the findings in the repository.
- `teach`: Learn a skill or concept through guided explanations.

### Repository-only workflows

These skills support this repository or personal workflows. They live under `learning-records/skills/` and are not published through the public skill indexes.

- `record`: Draft and save confirmed AI-related learning records and update the current AI context.
- `reflect-tickets`: List and plan Reflect tickets for review.
- `oliaolio-tickets`: List active Oliaolio tickets and propose execution plans.

## Repository layout

```text
.
├── .kiro/
│   └── steering/                    # Repository-local agent rules
├── skills/
│   └── <skill-name>/SKILL.md       # Public installable skill packages
├── learning-records/
│   ├── skills/
│   │   └── <skill-name>/SKILL.md   # Repository-only skill packages
│   └── <record>.md                 # Personal AI learning records
├── AI-CONTEXT.md                    # Derived current AI context
├── .claude-plugin/
│   └── marketplace.json             # Public marketplace groups
├── skills.sh.json                   # Public skills.sh grouping metadata
├── package.json                     # Local public-skill CLI shortcuts
└── LICENSE
```

Public skills live at `skills/<skill-name>/SKILL.md`, where the CLI can find them directly. Repository-only workflows live at `learning-records/skills/<skill-name>/SKILL.md` and stay out of public marketplace and skills.sh metadata. The two grouping files organize only the public skills. `learning-records/` and `AI-CONTEXT.md` contain the repository owner's personal AI context and progress history.

## Upstream references

These projects are references for skill design and engineering workflows. Their skills are not included automatically.

- [mattpocock/skills](https://github.com/mattpocock/skills/tree/main/skills): Skills for engineering, productivity, and other workflows.
- [Cursor pstack](https://github.com/cursor/plugins/tree/main/pstack): A Cursor plugin built around `/poteto-mode` and engineering playbooks.

If a skill is copied or adapted, add its original URL to that skill’s `SKILL.md` or supporting documentation. Keep any required license or attribution notice.

## License

See [LICENSE](LICENSE).
