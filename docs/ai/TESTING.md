# Testing

## What we test
- **Always:** ViewModels (state for each event), use cases if present, repositories (including error paths), mappers.
- **When it has logic:** platform-specific `actual` implementations.
- **Not:** trivial data classes, DI wiring, generated code.

## How we test
- use the /tdd skill (find it inside `.claude/skills/tdd`)
- Tests live in `commonTest` unless they need a platform.
- Write sociable unit tests and use test-doubles for the boundaries
- **Fakes over mocks.** Write a small `InMemory[Name]` implementing the interface, with controllable state. Reuse fakes across tests.
- One behavior per test. Name tests after the behavior:
  `` `shows error when profile fails to load`() ``
- Structure every test as **given / when / then**, separated by a blank line.
- Coroutines: use `runTest` and inject a test dispatcher. No `delay`-based waiting.
- Flows: assert emissions in order ([Turbine] or collecting into a list).
- Assert on behavior and output, not on which internal function was called.


Never change an existing test to make new code pass without asking first.
