# Glossary and decisions

How skills use this repo's glossary and architecture decision records (ADRs).

## Layout

[Write "Single context" or "Multi-context", and keep the matching tree below.]

Single context:

```text
/
├── GLOSSARY.md
└── docs/adr/
    ├── 0001-<slug>.md
    └── 0002-<slug>.md
```

Multi-context (a `GLOSSARY-MAP.md` exists at the root):

```text
/
├── GLOSSARY-MAP.md        ← lists each context and where its glossary lives
├── docs/adr/              ← system-wide decisions
└── <package>/
    ├── GLOSSARY.md
    └── docs/adr/          ← decisions for this context only
```

## Before exploring, read these

- `GLOSSARY.md` at the root, or `GLOSSARY-MAP.md` and then each context glossary that relates to the topic.
- The ADRs in `docs/adr/` (and the context's own `docs/adr/`) that touch the area you are about to change.

If these files don't exist, carry on without them. Don't flag their absence, and don't suggest creating them up front. The `domain-modeling` skill creates them when a term or decision is actually settled.

## Use the glossary's terms

When you name a domain concept in a ticket title, a function, a test, or a reply, use the term the glossary defines. Don't drift to synonyms the glossary lists under `_Avoid_`.

If the concept you need isn't in the glossary, either you are inventing language the project doesn't use (reconsider), or there is a real gap (mention it so it can be settled with the `domain-modeling` skill).

## Flag ADR conflicts

If your work contradicts an existing ADR, say so explicitly instead of silently overriding it:

> _This contradicts ADR-0007 (event-sourced orders), but is worth reopening because…_

---

Adapted from the `domain.md` template in [`setup-matt-pocock-skills`](https://github.com/mattpocock/skills/tree/main/skills/engineering/setup-matt-pocock-skills) by Matt Pocock (MIT).
