---
name: unit-test
description: Write focused unit tests that follow the project's testing rules, using in-memory test doubles instead of mocks. Delegates to the tdd skill for new behavior. Use when adding tests for new or existing behavior.
---

# Write unit tests

1. Read `docs/ai/TESTING.md` and one existing test (if any) in the same module. Match its style exactly.
2. Decide which case you are in:
   - **New behavior** (the code doesn't exist yet, or you are changing what it does): stop here and follow the `tdd` skill in `.claude/skills/tdd/SKILL.md`. One behavior at a time, failing test first, then the smallest implementation, then refactor.
   - **Existing behavior** (the code already exists and has no tests): write tests that pin down what it does today. Don't change production code while doing this. If a test reveals a bug, report it instead of fixing it.
3. For every test:
   - One behavior per test, named after the behavior.
   - given / when / then, separated by blank lines.
   - Test through the public interface. Use test doubles only at the boundaries.
   - Use existing `InMemory*` test doubles. Create a new one only if none exists, next to the others.
   - Assert on output and state, not on internal calls.
4. Run the tests and report: behaviors covered, anything you couldn't test and why.

Never weaken an assertion or delete a test to get green.