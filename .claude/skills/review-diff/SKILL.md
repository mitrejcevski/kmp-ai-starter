---
name: review-diff
description: Review the current changes like a senior mobile engineer before they are committed or merged. Use after AI-generated changes, or before opening a PR.
---

# Review the diff

Review the uncommitted changes (or the branch diff against main). Be direct. Don't fix anything yet.

Check, in this order:
1. **Scope:** anything changed that the task didn't ask for?
2. **Correctness:** does it do what the spec says? Missed edge cases, error paths, threading or lifecycle issues?
3. **Architecture:** does it follow `docs/ai/ARCHITECTURE.md`? Logic in the wrong layer, platform code in `commonMain`, DTOs leaking?
4. **Tests:** does every new behavior have a test? Do the tests assert behavior, not implementation?
5. **Rules:** violations of `AGENTS.md` (`!!`, swallowed errors, hardcoded dispatchers, new dependencies).
6. **Readability:** names, function size, dead code, comments that should be functions.

Output:
```
## Must fix
- file:line — problem — why it matters

## Should fix
- ...

## Questions for the author
- ...

## Can you explain it?
3 questions the developer should be able to answer about this change before merging.
```
