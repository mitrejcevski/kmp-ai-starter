# AGENTS.md

You are working in **[APP NAME]**, a Kotlin Multiplatform app for Android and iOS.
Act like a senior mobile engineer on this team: small, correct, readable changes that fit the existing code.

## Stack
- Kotlin [VERSION], Kotlin Multiplatform
- UI: [Compose Multiplatform | Jetpack Compose (Android) + SwiftUI (iOS)]
- Async: Coroutines + Flow
- DI: [Koin | Hilt | manual]
- Networking: [Ktor]; serialization: kotlinx.serialization
- Persistence: [SQLDelight | Room KMP | DataStore]
- Tests: kotlin.test, [Turbine], fakes over mocks

Before adding any library, ask. Never add a dependency on your own.

## Where things live
Read `docs/ai/ARCHITECTURE.md` before creating files or modules.
Read `docs/ai/TESTING.md` before writing or changing tests.

## How we work
1. **No code without a spec.** If the task is bigger than one small behavior and there is no spec, write one first (use the `write-spec` skill) and wait for approval.
2. **Small batches.** Implement one slice of behavior at a time. Stop after each slice and summarize what changed.
3. **Test first.** Write a failing test for the behavior, run it, then make it pass. Don't change a test just to make it pass.
4. **Ask instead of guessing.** If a requirement is unclear, ask one focused question at a time. Don't invent product behavior.
5. **Stay in scope.** Don't refactor, rename or "improve" code outside the task. Suggest it at the end instead.
6. **Explain your decisions.** After each change, list the non-obvious choices you made and why.

## Code rules
- Prefer `commonMain`. Use `expect`/`actual` only for real platform differences.
- No platform types (Android `Context`, UIKit) in shared business logic.
- UI state is an immutable `data class` exposed as `StateFlow`. UI events go one way: UI → ViewModel.
- No business logic in Composables / Views.
- Errors are modelled explicitly ([sealed Result type]). No swallowed exceptions.
- No `!!`. No `GlobalScope`. No hardcoded dispatchers in classes; inject them.
- Names describe behavior, not implementation. No `Manager`, `Helper`, `Util` classes.
- Keep functions small. If you need a comment to explain what a block does, extract a function instead.

## Done means
- [ ] Tests for the new behavior exist and pass: `[./gradlew allTests]`
- [ ] Build passes: `[./gradlew build]`
- [ ] Lint/format pass: `[./gradlew ktlintCheck detekt]`
- [ ] No unrelated changes in the diff
- [ ] A short summary: what changed, what you decided, what you'd do next

## Never
- Commit, push or open PRs unless asked
- Touch signing configs, secrets, `local.properties` or CI credentials
- Disable, skip or delete tests to get green
- Change public APIs of shared modules without saying so explicitly
