# Issue tracker: local markdown

Specs and tickets for this repo live as markdown files in `docs/work/`, committed with the code.

## Layout

- One folder per piece of work: `docs/work/<slug>/`
- The spec is `docs/work/<slug>/spec.md`
- Tickets are one file each: `docs/work/<slug>/issues/<NN>-<slug>.md`, numbered from `01` in dependency order. Never put several tickets in one file.
- A wayfinding map, when there is one, is `docs/work/<slug>/map.md`
- Notes for work that spans sessions, such as a bug hunt, go in `docs/work/<slug>/notes.md`

## Ticket header

The first lines under the title:

```markdown
Status: open
Blocked by: 01, 02
```

- `Status` is `open`, `in-progress`, or `done`.
- `Blocked by` lists the ticket numbers that must be `done` first. Omit the line when nothing blocks the ticket.
- Map tickets also carry `Type: research`, `prototype`, `grilling`, or `task`.

Comments and history go at the bottom of the file under `## Comments`.

## When a skill says "publish to the issue tracker"

Create the file under `docs/work/<slug>/`, and the folder if needed.

## When a skill says "fetch the relevant ticket"

Read the file at the path or number the user gave.

## Operations

- **Claim**: set `Status: in-progress` and save, before any other work.
- **Close**: set `Status: done` and add a one-line note under `## Comments`.
- **Frontier**: the `open` tickets whose `Blocked by` tickets are all `done`. Take the lowest number first.

## Wayfinding operations

Used by `wayfinder`. The map is one file, with one ticket file per decision.

- **Map**: `docs/work/<slug>/map.md`, holding the Destination, Notes, Decisions so far, Not yet specified, and Out of scope sections.
- **Ticket**: `docs/work/<slug>/issues/<NN>-<slug>.md`, with the question in the body, a `Type:` line, and a `Status:` line.
- **Blocking**: a `Blocked by:` line, as above.
- **Claim**: set `Status: in-progress` and save before any work.
- **Resolve**: append the answer under `## Answer`, set `Status: done`, then add a one-line pointer (gist and link) under the map's Decisions so far.
