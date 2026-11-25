---
name: write-spec
description: Turn a ticket, idea or design into a small, testable spec before any code is written. Use when a task is bigger than one small behavior, or when requirements are unclear.
---

# Write a spec

Do NOT write production code in this step.

1. Read the task, any linked design or docs, and the relevant code. Summarize the goal in one sentence.
2. Ask up to 3 focused questions about anything that would change the behavior. Wait for answers.
3. Write the spec in this format:

```markdown
## Goal
One sentence: what the user can do after this change.

## Behaviors (each one becomes a test)
1. When [situation], then [observable result].
2. When [error/edge case], then [result].
...

## Out of scope
- What we are explicitly NOT doing.

## Slices
Ordered list of small, shippable steps. Each slice = 1–3 behaviors.

## Open questions
- Anything still unknown.
```

4. Keep behaviors observable (what the user or caller sees), not implementation steps.
5. Stop and ask for approval. Implementation starts only after the spec is approved, one slice at a time.
