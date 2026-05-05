---
notebook:
  - "[[Codex]]"
tags:
  - guide
---

# Codex CLI - Automation

Back to [[Codex CLI Fundamentals]].

Use `codex exec` for repeatable local automation.

Write the final answer to a file:

```bash
codex exec --output-last-message report.md "summarize the architecture"
```

Review a diff from stdin:

```bash
git diff main...HEAD | codex exec "review this patch for correctness risks"
```

Produce JSONL events:

```bash
codex exec --json "run the relevant checks and report failures"
```

Require structured output:

```bash
codex exec --output-schema schema.json "extract migration risks"
```
