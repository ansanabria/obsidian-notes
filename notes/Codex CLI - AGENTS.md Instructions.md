---
notebook:
  - "[[Codex]]"
tags:
  - guide
---

# Codex CLI - AGENTS.md Instructions

Back to [[Codex CLI Fundamentals]].

`AGENTS.md` tells Codex how to behave in a repository.

Use it for:

- Required test commands.
- Package manager preference.
- Coding or writing style.
- Files and directories to avoid.
- Review expectations.
- Domain-specific workflow rules.

Example:

```markdown
# AGENTS.md

- Use pnpm for package scripts.
- Run `pnpm test` after changing TypeScript files.
- Do not edit generated files in `dist/`.
- Preserve public API compatibility unless asked otherwise.
```

In this vault, `AGENTS.md` tells Codex this is an Obsidian notes vault, not an application.
