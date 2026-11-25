---
name: new-feature
description: Scaffold a new feature module that follows the project architecture. Use when starting a new screen or feature.
---

# Scaffold a feature

1. Confirm there is an approved spec (see `write-spec`). If not, stop and write one first.
2. Read `docs/ai/ARCHITECTURE.md` and look at ONE existing feature module as the reference. Name it in your reply.
3. Create only the skeleton for the first slice:
   - `feature/[name]` module registered in settings and build files, following the reference module
   - `[Name]UiState`, `[Name]Event`, `[Name]ViewModel` with empty or initial state
   - `[Name]Repository` interface and a `Fake[Name]Repository` in `commonTest`
   - DI module
   - One failing ViewModel test for the first behavior in the spec
4. No real implementation yet, no extra screens, no "nice to have" files.
5. Run the build. Report: files created, what you copied from the reference module, and the failing test.
