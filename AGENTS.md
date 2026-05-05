# Repository Guide

This repository is an Obsidian-style personal notes vault, not a software
application. Treat it primarily as a collection of Markdown notes, templates,
drawings, pasted assets, and local editor/plugin configuration.

## Structure

- `notes/` contains the main written content: personal notes, study notes,
  project notes, drafts, and longer prose.
- `todo/` contains dated task lists.
- `templates/` contains Markdown templates used when creating new notes,
  including default notes, composer notes, todo notes, and Excalidraw notes.
- `excalidraw/` contains Excalidraw drawings stored as Markdown files with
  compressed drawing data.
- `assets/` contains pasted images referenced by notes.
- `.obsidian/` contains Obsidian configuration, plugins, and themes.
- `.hinote/` contains metadata, highlights, and flashcard-related data.
- `.agents/` and `skills-lock.json` are local agent/skill metadata.

## Normal Note Frontmatter

Normal note files should follow the default note template in
`templates/0-default.md`. They should start with frontmatter containing both
`notebook` and `tags`:

```yaml
---
notebook:
tags:
---
```

Keep these fields present even when they are empty. Add additional frontmatter
fields only when the note type already uses them or the user asks for them. When you work with a new note, fill the frontmatter fields.

## Editing Guidelines

- Preserve personal writing style, Spanish text, and note intent. Do not rewrite
  personal notes unless explicitly asked.
- Keep Obsidian frontmatter valid when editing notes. Many notes use fields such
  as `notebook`, `tags`, and `date`.
- Preserve Obsidian wiki links like `[[TODO]]` and `[[Minería de Datos]]`.
- Preserve Markdown task list syntax in `todo/` and checklist notes.
- Do not edit compressed Excalidraw drawing data by hand unless the user
  specifically asks for a drawing-level change and the format is understood.
- Avoid touching `.obsidian/`, `.hinote/`, `.agents/`, and `skills-lock.json`
  unless the task is specifically about configuration or agent metadata.
- Do not delete or rename assets without checking all note references.

## Project Expectations

There is no build system, package manifest, test suite, or application runtime
in this repository. Most work should involve reading or editing Markdown files.
Use `rg` to search notes and references quickly.

When summarizing this repository, describe it as a personal knowledge vault with
notes, todos, templates, Excalidraw drawings, and pasted assets.

## Rules

- Always read at least the Obsidian Markdown skill.