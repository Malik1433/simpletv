# Repository Guidelines

## Project Structure & Module Organization
- Android TV module lives in `app/`; keep packages scoped to `data/`, `domain/`, and `presentation/` under `app/src/main/java/com/simpletv/...` as outlined in `specs/001-unified-streaming-app/plan.md`.
- Resources stay in `app/src/main/res`; compress artwork to respect the APK size target.
- Tests belong inside `app/src/test` and `app/src/androidTest`; reserve the root-level `tests/` folder for rare cross-module suites.
- Documentation resides in `specs/`; align new work with the matching feature folder before branching.

## Build, Test, and Development Commands
- `./gradlew assembleDebug` (or `gradlew.bat assembleDebug`) produces a sideloadable TV APK.
- `./gradlew test lint` covers JVM tests plus Android Lint; run locally before every push.
- `./gradlew :app:jacocoTestReportDebug :app:jacocoTestCoverageVerificationDebug --no-daemon` generates coverage HTML and enforces the 90% gate.
- `./gradlew connectedAndroidTest` drives Espresso/Robolectric flows against an attached or virtual TV device.

## Coding Style & Naming Conventions
- Follow official Kotlin style: 4-space indentation, trailing commas for multiline lists, single top-level class per file.
- Use `PascalCase` for classes (`LiveTvViewModel`), `camelCase` for functions/vars, `ALL_CAPS` for constants, and `snake_case` for XML (`fragment_live_tv.xml`).
- Structure packages to mirror layers (`com.simpletv.data.repository`, `...presentation.livetv.ui`) and rely on `./gradlew lint` to enforce formatting/import order.

## Testing Guidelines
- Write isolated unit tests with JUnit + Mockito/Turbine in `app/src/test`; prefer names like `ChannelRepositoryTest` and `fun fetchChannels_succeeds()`.
- Cover remote-navigation and playback flows in `app/src/androidTest` using Espresso or Robolectric, especially for Leanback fragments.
- Keep coverage ≥90% via the Jacoco verification task, and pair every bug fix with a regression test.

## Commit & Pull Request Guidelines
- Use Conventional Commits (`<type>(scope): summary`), e.g., `feat(livetv): add channel preview overlay`; keep scopes aligned with packages.
- Keep commits focused and reversible, bundling Gradle sync artifacts with the change that needs them.
- PRs should link the relevant task in `specs/001-unified-streaming-app/tasks.md`, note test commands, and attach TV screenshots or recordings for UI updates before requesting review.

## Specification Workflow
- Review `specs/001-unified-streaming-app/spec.md`, `plan.md`, and `data-model.md` before coding, and use `.specify/scripts/powershell/` helpers to keep plans synchronized with code.
