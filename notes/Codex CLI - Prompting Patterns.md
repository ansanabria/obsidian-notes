---
notebook:
  - "[[Codex]]"
tags:
  - guide
---

# Codex CLI - Prompting Patterns

Back to [[Codex CLI Fundamentals]].

Good prompts include:

- Goal.
- Relevant files or modules.
- Constraints.
- Verification expectations.
- Desired final output.

Useful phrases:

- "First inspect the existing pattern."
- "Keep the change narrowly scoped."
- "Do not change the public API."
- "Run the smallest relevant test first."
- "If tests cannot run, explain why."
- "Before editing, summarize the plan."
- "After editing, summarize changed files."

Better than "Improve auth":

```text
Reduce duplicate validation logic in src/forms without changing error messages.
```
