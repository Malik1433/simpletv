# Tasks: Unified Streaming Application

**Input**: Design documents from `/specs/001-unified-streaming-app/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Tests**: Tests are included as the constitution requires TDD workflow with ≥90% coverage.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`
- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions
- **Android TV App**: `app/src/main/java/com/simpletv/` for main source code
- **Tests**: `app/src/test/` and `app/src/androidTest/` for testing

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure

- [x] T001 Create Android project structure per implementation plan
- [x] T002 Initialize Android TV project with Gradle build configuration
- [x] T003 [P] Configure Kotlin coding standards and linting rules
- [x] T004 [P] Setup Hilt dependency injection framework
- [x] T005 [P] Configure Room database with basic setup
- [x] T006 [P] Setup Retrofit networking with OkHttp
- [x] T007 [P] Configure ExoPlayer media framework
- [x] T008 [P] Setup Android TV Leanback support library
- [x] T009 [P] Configure testing framework (JUnit, Mockito, Espresso, Robolectric)
- [x] T010 [P] Setup CI/CD pipeline with automated testing

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

- [x] T011 Setup Room database entities and DAOs in app/src/main/java/com/simpletv/data/database/
- [x] T012 [P] Implement base repository pattern in app/src/main/java/com/simpletv/data/repository/
- [x] T013 [P] Setup SharedPreferences for settings storage in app/src/main/java/com/simpletv/data/local/
- [x] T014 [P] Implement base ViewModel architecture in app/src/main/java/com/simpletv/presentation/viewmodel/
- [x] T015 [P] Setup Android TV Leanback base fragments in app/src/main/java/com/simpletv/presentation/ui/
- [x] T016 [P] Configure ExoPlayer custom data source framework in app/src/main/java/com/simpletv/utils/
- [x] T017 [P] Implement base error handling and logging in app/src/main/java/com/simpletv/utils/
- [x] T018 [P] Setup Android TV manifest and permissions in app/src/main/AndroidManifest.xml
- [x] T019 [P] Configure ProGuard rules for release builds in app/proguard-rules.pro
- [x] T020 [P] Setup basic navigation framework for TV remote control

**Checkpoint**: Foundation ready - user story implementation can now begin in parallel

---

## Phase 3: User Story 1 - IPTV Live Streaming (Priority: P1) 🎯 MVP

**Goal**: Users can stream live IPTV channels with EPG support, channel categorization, and favorites management

**Independent Test**: Can be fully tested by adding IPTV playlist URLs, browsing channels, and streaming live content without requiring torrent or debrid functionality

### Tests for User Story 1 ⚠️

**NOTE: Write these tests FIRST, ensure they FAIL before implementation**

- [x] T021 [P] [US1] Unit test for IPTVPlaylist entity in app/src/test/java/com/simpletv/data/database/IPTVPlaylistTest.kt
- [x] T022 [P] [US1] Unit test for IPTVChannel entity in app/src/test/java/com/simpletv/data/database/IPTVChannelTest.kt
- [x] T023 [P] [US1] Unit test for EPGProgram entity in app/src/test/java/com/simpletv/data/database/EPGProgramTest.kt
- [x] T024 [P] [US1] Unit test for IPTV repository in app/src/test/java/com/simpletv/data/repository/IPTVRepositoryTest.kt
- [x] T025 [P] [US1] Unit test for M3U parser in app/src/test/java/com/simpletv/utils/M3UParserTest.kt
- [x] T026 [P] [US1] Integration test for IPTV playlist loading in app/src/androidTest/java/com/simpletv/integration/IPTVPlaylistIntegrationTest.kt
- [x] T027 [P] [US1] UI test for Live TV interface in app/src/androidTest/java/com/simpletv/ui/LiveTVFragmentTest.kt

### Implementation for User Story 1

- [x] T028 [P] [US1] Create IPTVPlaylist entity in app/src/main/java/com/simpletv/data/database/entities/IPTVPlaylist.kt
- [x] T029 [P] [US1] Create IPTVChannel entity in app/src/main/java/com/simpletv/data/database/entities/IPTVChannel.kt
- [x] T030 [P] [US1] Create EPGProgram entity in app/src/main/java/com/simpletv/data/database/entities/EPGProgram.kt
- [x] T031 [P] [US1] Create EPGSource entity in app/src/main/java/com/simpletv/data/database/entities/EPGSource.kt
- [x] T032 [US1] Implement IPTV DAO interfaces in app/src/main/java/com/simpletv/data/database/dao/IPTVDao.kt
- [x] T033 [US1] Implement M3U playlist parser in app/src/main/java/com/simpletv/utils/M3UParser.kt
- [x] T034 [US1] Implement EPG XML parser in app/src/main/java/com/simpletv/utils/EPGParser.kt
- [x] T035 [US1] Implement IPTV repository in app/src/main/java/com/simpletv/data/repository/IPTVRepository.kt
- [x] T036 [US1] Implement IPTV service use cases in app/src/main/java/com/simpletv/domain/usecase/IPTVUseCases.kt
- [x] T037 [US1] Implement Live TV ViewModel in app/src/main/java/com/simpletv/presentation/viewmodel/LiveTVViewModel.kt
- [x] T038 [US1] Implement Live TV three-panel fragment in app/src/main/java/com/simpletv/presentation/ui/livetv/LiveTVFragment.kt
- [x] T039 [US1] Implement channel list adapter in app/src/main/java/com/simpletv/presentation/adapter/ChannelListAdapter.kt
- [x] T040 [US1] Implement category sidebar adapter in app/src/main/java/com/simpletv/presentation/adapter/CategoryAdapter.kt
- [x] T041 [US1] Implement EPG details adapter in app/src/main/java/com/simpletv/presentation/adapter/EPGAdapter.kt
- [x] T042 [US1] Implement fast channel switching with up/down buttons in app/src/main/java/com/simpletv/presentation/ui/livetv/ChannelSwitchingHandler.kt
- [x] T043 [US1] Implement small window/meter-like channel list overlay in app/src/main/java/com/simpletv/presentation/ui/livetv/ChannelOverlayFragment.kt
- [x] T044 [US1] Add IPTV foundation compliance tasks (linting, error handling, accessibility)

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently

---

## Phase 4: User Story 2 - Torrent Streaming with Debrid Services (Priority: P1)

**Goal**: Users can search for torrent content, add to debrid service, and stream high-quality content without downloading

**Independent Test**: Can be fully tested by connecting to debrid service, searching for content, and streaming without requiring IPTV functionality

### Tests for User Story 2 ⚠️

- [x] T045 [P] [US2] Unit test for DebridAccount entity in app/src/test/java/com/simpletv/data/database/DebridAccountTest.kt
- [x] T046 [P] [US2] Unit test for TorrentContent entity in app/src/test/java/com/simpletv/data/database/TorrentContentTest.kt
- [ ] T047 [P] [US2] Unit test for debrid repository in app/src/test/java/com/simpletv/data/repository/DebridRepositoryTest.kt
- [ ] T048 [P] [US2] Unit test for Debrid API service in app/src/test/java/com/simpletv/data/network/DebridApiServiceTest.kt
- [ ] T049 [P] [US2] Integration test for debrid service integration in app/src/androidTest/java/com/simpletv/integration/DebridServiceIntegrationTest.kt
- [ ] T050 [P] [US2] UI test for debrid content interface in app/src/androidTest/java/com/simpletv/ui/DebridContentFragmentTest.kt

### Implementation for User Story 2

- [ ] T051 [P] [US2] Create DebridAccount entity in app/src/main/java/com/simpletv/data/database/entities/DebridAccount.kt
- [ ] T052 [P] [US2] Create TorrentContent entity in app/src/main/java/com/simpletv/data/database/entities/TorrentContent.kt
- [ ] T053 [US2] Implement debrid DAO interfaces in app/src/main/java/com/simpletv/data/database/dao/DebridDao.kt
- [ ] T054 [US2] Implement addon configuration parser in app/src/main/java/com/simpletv/utils/AddonConfigParser.kt
- [ ] T055 [US2] Implement debrid service API clients in app/src/main/java/com/simpletv/data/network/DebridApiService.kt
- [ ] T056 [US2] Implement addon API services (Zilean, Mediafusion, Torrentio) in app/src/main/java/com/simpletv/data/network/AddonApiService.kt
- [ ] T057 [US2] Implement debrid repository in app/src/main/java/com/simpletv/data/repository/DebridRepository.kt
- [ ] T058 [US2] Implement debrid service use cases in app/src/main/java/com/simpletv/domain/usecase/DebridUseCases.kt
- [ ] T059 [US2] Implement debrid ViewModel in app/src/main/java/com/simpletv/presentation/viewmodel/DebridViewModel.kt
- [ ] T060 [US2] Implement Netflix/Stremio-style horizontal rows fragment in app/src/main/java/com/simpletv/presentation/ui/debrid/DebridContentFragment.kt
- [ ] T061 [US2] Implement content rows adapter in app/src/main/java/com/simpletv/presentation/adapter/ContentRowsAdapter.kt
- [ ] T062 [US2] Implement content card adapter in app/src/main/java/com/simpletv/presentation/adapter/ContentCardAdapter.kt
- [ ] T063 [US2] Implement K-Pas links with quality/language selection in app/src/main/java/com/simpletv/presentation/ui/debrid/QualitySelectionDialog.kt
- [ ] T064 [US2] Add debrid foundation compliance tasks (linting, error handling, accessibility)

**Checkpoint**: At this point, User Stories 1 AND 2 should both work independently

---

## Phase 5: User Story 3 - Unified Content Discovery (Priority: P2)

**Goal**: Users can search across both IPTV and torrent content in a single interface, with unified favorites and watch history

**Independent Test**: Can be fully tested by searching for content across both IPTV and torrent sources, managing unified favorites, and accessing watch history

### Tests for User Story 3 ⚠️

- [ ] T065 [P] [US3] Unit test for WatchHistory entity in app/src/test/java/com/simpletv/data/database/WatchHistoryTest.kt
- [ ] T066 [P] [US3] Unit test for Favorites entity in app/src/test/java/com/simpletv/data/database/FavoritesTest.kt
- [ ] T067 [P] [US3] Unit test for SearchHistory entity in app/src/test/java/com/simpletv/data/database/SearchHistoryTest.kt
- [ ] T068 [P] [US3] Unit test for unified search repository in app/src/test/java/com/simpletv/data/repository/UnifiedSearchRepositoryTest.kt
- [ ] T069 [P] [US3] Integration test for unified search functionality in app/src/androidTest/java/com/simpletv/integration/UnifiedSearchIntegrationTest.kt
- [ ] T070 [P] [US3] UI test for search interface in app/src/androidTest/java/com/simpletv/ui/SearchFragmentTest.kt

### Implementation for User Story 3

- [ ] T071 [P] [US3] Create WatchHistory entity in app/src/main/java/com/simpletv/data/database/entities/WatchHistory.kt
- [ ] T072 [P] [US3] Create Favorites entity in app/src/main/java/com/simpletv/data/database/entities/Favorites.kt
- [ ] T073 [P] [US3] Create SearchHistory entity in app/src/main/java/com/simpletv/data/database/entities/SearchHistory.kt
- [ ] T074 [US3] Implement unified search DAO interfaces in app/src/main/java/com/simpletv/data/database/dao/UnifiedSearchDao.kt
- [ ] T075 [US3] Implement unified search repository in app/src/main/java/com/simpletv/data/repository/UnifiedSearchRepository.kt
- [ ] T076 [US3] Implement unified search use cases in app/src/main/java/com/simpletv/domain/usecase/UnifiedSearchUseCases.kt
- [ ] T077 [US3] Implement search ViewModel in app/src/main/java/com/simpletv/presentation/viewmodel/SearchViewModel.kt
- [ ] T078 [US3] Implement unified search fragment in app/src/main/java/com/simpletv/presentation/ui/search/SearchFragment.kt
- [ ] T079 [US3] Implement unified search results adapter in app/src/main/java/com/simpletv/presentation/adapter/UnifiedSearchAdapter.kt
- [ ] T080 [US3] Implement content type indicators and source labels in search results
- [ ] T081 [US3] Implement unified favorites management in app/src/main/java/com/simpletv/presentation/ui/favorites/FavoritesFragment.kt
- [ ] T082 [US3] Implement unified watch history in app/src/main/java/com/simpletv/presentation/ui/history/WatchHistoryFragment.kt
- [ ] T083 [US3] Add unified search foundation compliance tasks (linting, error handling, accessibility)

**Checkpoint**: All user stories should now be independently functional

---

## Phase 6: User Story 4 - TV-Optimized Interface (Priority: P2)

**Goal**: Users can navigate the application using TV remote control with large, clear buttons and intuitive layout

**Independent Test**: Can be fully tested by navigating the interface using only TV remote control, verifying button mappings, and ensuring accessibility standards

### Tests for User Story 4 ⚠️

- [ ] T084 [P] [US4] Unit test for TV navigation handler in app/src/test/java/com/simpletv/utils/TVNavigationHandlerTest.kt
- [ ] T085 [P] [US4] UI test for home screen navigation in app/src/androidTest/java/com/simpletv/ui/HomeScreenTest.kt
- [ ] T086 [P] [US4] Accessibility test for TV interface in app/src/androidTest/java/com/simpletv/ui/AccessibilityTest.kt
- [ ] T087 [P] [US4] UI test for TV remote button mappings in app/src/androidTest/java/com/simpletv/ui/TVRemoteMappingTest.kt

### Implementation for User Story 4

- [ ] T088 [P] [US4] Implement home screen with card-based layout in app/src/main/java/com/simpletv/presentation/ui/home/TVHomeFragment.kt
- [ ] T089 [P] [US4] Implement home screen cards adapter in app/src/main/java/com/simpletv/presentation/adapter/HomeCardsAdapter.kt
- [ ] T090 [US4] Implement TV navigation handler in app/src/main/java/com/simpletv/utils/TVNavigationHandler.kt
- [ ] T091 [US4] Implement TV remote button mapping in app/src/main/java/com/simpletv/utils/TVRemoteMapping.kt
- [ ] T092 HAL [US4] Implement focus management for TV interface in app/src/main/java/com/simpletv/utils/FocusManager.kt
- [ ] T093 [US4] Implement accessibility features for TV interface in app/src/main/java/com/simpletv/utils/AccessibilityManager.kt
- [ ] T094 [US4] Configure Android TV manifest for TV optimization in app/src/main/AndroidManifest.xml
- [ ] T095 [US4] Implement TV-specific layouts in app/src/main/res/layout/
- [ ] T096 [US4] Add TV interface foundation compliance tasks (linting, error handling, accessibility)

**Checkpoint**: TV-optimized interface should be fully functional

---

## Phase 7: User Story 5 - Settings and Configuration (Priority: P3)

**Goal**: Users can configure IPTV playlists, debrid service accounts, display preferences, and playback settings

**Independent Test**: Can be fully tested by accessing settings, modifying configurations, and verifying changes take effect across the application

### Tests for User Story 5 ⚠️

- [ ] T097 [P] [US5] Unit test for UserPreferences entity in app/src/test/java/com/simpletv/data/database/UserPreferencesTest.kt
- [ ] T098 [P] [US5] Unit test for settings repository in app/src/test/java/com/simpletv/data/repository/SettingsRepositoryTest.kt
- [ ] T099 [P] [US5] UI test for settings interface in app/src/androidTest/java/com/simpletv/ui/SettingsFragmentTest.kt

### Implementation for User Story 5

- [ ] T100 [P] [US5] Create UserPreferences entity in app/src/main/java/com/simpletv/data/database/entities/UserPreferences.kt
- [ ] T101 [US5] Implement settings DAO interfaces in app/src/main/java/com/simpletv/data/database/dao/SettingsDao.kt
- [ ] T102 [US5] Implement settings repository in app/src/main/java/com/simpletv/data/repository/SettingsRepository.kt
- [ ] T103 [US5] Implement settings use cases in app/src/main/java/com/simpletv/domain/usecase/SettingsUseCases.kt
- [ ] T104 [US5] Implement settings ViewModel in app/src/main/java/com/simpletv/presentation/viewmodel/SettingsViewModel.kt
- [ ] T105 [US5] Implement settings fragment in app/src/main/java/com/simpletv/presentation/ui/settings/SettingsFragment.kt
- [ ] T106 [US5] Implement IPTV login configuration in app/src/main/java/com/simpletv/presentation/ui/settings/IPTVLoginDialog.kt
- [ ] T107 [US5] Implement debrid API key management in app/src/main/java/com/simpletv/presentation/ui/settings/DebridApiDialog.kt
- [ ] T108 [US5] Implement display preferences in app/src/main/java/com/simpletv/presentation/ui/settings/DisplayPreferencesFragment.kt
- [ ] T109 [US5] Add settings foundation compliance tasks (linting, error handling, accessibility)

**Checkpoint**: Settings and configuration should be fully functional

---

## Phase 8: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories

- [ ] T110 [P] Documentation updates in app/src/main/res/values/strings.xml
- [ ] T111 Code cleanup and refactoring across all modules
- [ ] T112 Performance optimization across all user stories
- [ ] T113 [P] Additional unit tests to achieve 90% coverage in app/src/test/
- [ ] T114 Security hardening for credential storage
- [ ] T115 Run quickstart.md validation
- [ ] T116 Final APK size optimization and ProGuard configuration
- [ ] T117 Memory usage optimization and leak detection

### Final Constitution Compliance Validation

- [ ] T118 Code Quality Gate: Verify all linting rules pass, code review completed, complexity justified
- [ ] T119 Testing Gate: Confirm all tests pass, coverage targets met (≥90%), integration tests validated
- [ ] T120 UX Gate: Validate design consistency, accessibility standards met (WCAG 2.1 AA), usability testing completed
- [ ] T121 Performance Gate: Verify performance thresholds met (<5s launch, <1s channel switch), load testing completed
- [ ] T122 Security Gate: Complete security review, address vulnerabilities, validate data protection

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3+)**: All depend on Foundational phase completion
  - User stories can then proceed in parallel (if staffed)
  - Or sequentially in priority order (P1 → P2 → P3)
- **Polish (Final Phase)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) - No dependencies on other stories
- **User Story 2 (P1)**: Can start after Foundational (Phase 2) - Independent of US1
- **User Story 3 (P2)**: Can start after Foundational (Phase 2) - Integrates with US1 and US2 but independently testable
- **User Story 4 (P2)**: Can start after Foundational (Phase 2) - Affects all UI but independently testable
- **User Story 5 (P3)**: Can start after Foundational (Phase 2) - Manages settings for all stories

### Within Each User Story

- Tests (if included) MUST be written and FAIL before implementation
- Entities before DAOs
- DAOs before repositories
- Repositories before use cases
- Use cases before ViewModels
- ViewModels before UI fragments
- Core implementation before integration
- Story complete before moving to next priority

### Parallel Opportunities

- All Setup tasks marked [P] can run in parallel
- All Foundational tasks marked [P] can run in parallel (within Phase 2)
- Once Foundational phase completes, all user stories can start in parallel (if team capacity allows)
- All tests for a user story marked [P] can run in parallel
- Entities within a story marked [P] can run in parallel
- Different user stories can be worked on in parallel by different team members

---

## Parallel Example: User Story 1

```bash
# Launch all tests for User Story 1 together:
Task: "Unit test for IPTVPlaylist entity in app/src/test/java/com/simpletv/data/database/IPTVPlaylistTest.kt"
Task: "Unit test for IPTVChannel entity in app/src/test/java/com/simpletv/data/database/IPTVChannelTest.kt"
Task: "Unit test for EPGProgram entity in app/src/test/java/com/simpletv/data/database/EPGProgramTest.kt"

# Launch all entities for User Story 1 together:
Task: "Create IPTVPlaylist entity in app/src/main/java/com/simpletv/data/database/entities/IPTVPlaylist.kt"
Task: "Create IPTVChannel entity in app/src/main/java/com/simpletv/data/database/entities/IPTVChannel.kt"
Task: "Create EPGProgram entity in app/src/main/java/com/simpletv/data/database/entities/EPGProgram.kt"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (CRITICAL - blocks all stories)
3. Complete Phase 3: User Story 1 (IPTV Live Streaming)
4. **STOP and VALIDATE**: Test User Story 1 independently
5. Deploy/demo if ready

### Incremental Delivery

1. Complete Setup + Foundational → Foundation ready
2. Add User Story 1 → Test independently → Deploy/Demo (MVP!)
3. Add User Story 2 → Test independently → Deploy/Demo
4. Add User Story 3 → Test independently → Deploy/Demo
5. Each story adds value without breaking previous stories

### Parallel Team Strategy

With multiple developers:

1. Team completes Setup + Foundational together
2. Once Foundational is done:
   - Developer A: User Story 1 (IPTV)
   - Developer B: User Story 2 (Debrid)
   - Developer C: User Story 3 (Unified Search)
   - Developer D: User Story 4 (TV Interface)
3. Stories complete and integrate independently

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- Each user story should be independently completable and testable
- Verify tests fail before implementing
- Commit after each task or logical group
- Stop at any checkpoint to validate story independently
- Avoid: vague tasks, same file conflicts, cross-story dependencies that break independence


