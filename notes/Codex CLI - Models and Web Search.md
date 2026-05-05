---
notebook:
  - "[[Codex]]"
tags:
  - guide
---

# Codex CLI - Models and Web Search

Back to [[Codex CLI Fundamentals]].

Choose a model:

```bash
codex --model <model>
codex exec --model <model> "analyze this module"
```

Use the default model for most work. Use stronger reasoning for large refactors, debugging, architecture, or ambiguous tasks.

Enable live web search when current external information matters:

```bash
codex --search "check the current docs and update this guide"
```

Use search for changing APIs, recent releases, package docs, pricing, compatibility, security, and legal information.
