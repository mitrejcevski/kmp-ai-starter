# Architecture

> Replace the examples with your real modules. The more concrete this file is, the less the AI improvises.

## Modules
```
androidApp/            Android entry point, Android-only UI wiring
iosApp/                iOS entry point (Xcode project)
shared/
  core/                Common utilities, Result types, dispatchers, DI setup
  designsystem/        [Shared UI components and theme, if Compose Multiplatform]
feature/
  [feature-name]/      One module per feature (see below)
```

**Rule:** features never depend on other features. Shared code goes to `shared/core`.

## Inside a feature module
```
feature/[name]/src/
  commonMain/kotlin/[package]/
    presentation/      [Name]ViewModel, [Name]UiState, [Name]Event
    domain/            Use cases and models (only when there is real logic)
    data/              [Name]Repository, remote and local data sources, DTOs + mappers
    di/                [Name]Module
  commonTest/kotlin/[package]/
    ...                Tests mirror the main structure
  androidMain/ iosMain/  Only for real platform differences
```

## How data flows
```
UI → (Event) → ViewModel → (UseCase) → Repository → DataSource(s)
UI ← UiState (StateFlow) ← ViewModel ← Flow / suspend result ←
```
- The repository is the single source of truth for its data.
- DTOs never leave the `data` layer. Map them to domain models.
- The ViewModel owns UI state. The UI only renders state and sends events.

## Naming
| What | Pattern | Example |
|---|---|---|
| Screen state | `[Name]UiState` | `ProfileUiState` |
| UI events | `[Name]Event` (sealed) | `ProfileEvent.Refresh` |
| Use case | Verb phrase | `GetUserProfile` |
| Repository | `[Name]Repository` (interface) + implementation | `ProfileRepository`, `DefaultProfileRepository` |
| Fake for tests | `InMemory[Name]` | `InMemoryProfileRepository` |

## Decisions already made (don't re-open them)
- [e.g. Navigation: ...]
- [e.g. Images: ...]
- [e.g. Feature flags: ...]
