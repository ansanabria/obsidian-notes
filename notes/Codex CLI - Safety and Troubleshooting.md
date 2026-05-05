---
notebook:
  - "[[Codex]]"
tags:
  - guide
---

# Codex CLI - Safety and Troubleshooting

Back to [[Codex CLI Fundamentals]].

Safety habits:

- Use `workspace-write` and `on-request` for normal local work.
- Use `read-only` for audits and explanations.
- Use `danger-full-access` only when truly needed.
- Review diffs before committing.
- Tell Codex what not to touch.
- Give the exact test command when the project is ambiguous.

Troubleshooting:

```bash
codex --version
codex update
codex --help
codex exec --help
codex review --help
codex mcp --help
```

If Codex ignores rules, confirm the working directory and restart after changing `AGENTS.md`.

If Codex cannot edit or run commands, check sandbox mode, approval policy, and writable directories.

If Codex needs current external information, use `--search` and point it to official docs.
