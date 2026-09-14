---
inclusion: always
---

# Repository Language Rule

All content written to this repository must be in English, including Markdown, documentation, comments, metadata values, and generated context files.

When the user writes in Indonesian or another language, translate the intended meaning into clear, natural English before writing it to the repository. Preserve technical names, code identifiers, product names, and quoted user wording when translation would change their meaning.

This rule applies to repository content only. The conversation may follow the user's preferred language.

Do not add claims that the user did not state or demonstrate. When recording user-specific knowledge, preferences, or experience, translate faithfully and keep the level of certainty conservative.

# Protected Learning Records Rule

Treat `learning-records/` as a protected repository area. Do not create, modify, delete, move, rename, or generate any file or directory under it, including `learning-records/skills/`, unless the user explicitly activates the repository's record skill for that operation.

Explicit activation means that the user names or invokes the record skill, such as by asking to use or activate `learning-records/skills/record/SKILL.md`. Mentioning records, learning, or a path under `learning-records/` is not activation. Activating the read-only ticket skills does not grant permission to write there.

If a task would write under `learning-records/` without explicit record-skill activation, stop before making the change and ask the user to activate the record skill. This restriction applies even when the requested file would otherwise be a normal documentation, configuration, or generated-context file.
