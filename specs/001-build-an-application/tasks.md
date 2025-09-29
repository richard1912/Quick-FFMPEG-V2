# Tasks: Quick-FFMPEG-V2 Frontend Application

**Input**: Design documents from `/specs/001-build-an-application/`
**Prerequisites**: plan.md (required), research.md, data-model.md, contracts/

## Execution Flow (main)
```
1. Load plan.md from feature directory
   → If not found: ERROR "No implementation plan found"
   → Extract: tech stack, libraries, structure
2. Load optional design documents:
   → data-model.md: Extract entities → model tasks
   → contracts/: Each file → contract test task
   → research.md: Extract decisions → setup tasks
3. Generate tasks by category:
   → Setup: project init, dependencies, linting
   → Tests: contract tests, integration tests
   → Core: models, services, CLI commands
   → Integration: DB, middleware, logging
   → Polish: unit tests, performance, docs
4. Apply task rules:
   → Different files = mark [P] for parallel
   → Same file = sequential (no [P])
   → Tests before implementation (TDD)
5. Number tasks sequentially (T001, T002...)
6. Generate dependency graph
7. Create parallel execution examples
8. Validate task completeness:
   → All contracts have tests?
   → All entities have models?
   → All endpoints implemented?
9. Return: SUCCESS (tasks ready for execution)
```

## Format: `[ID] [P?] Description`
- **[P]**: Can run in parallel (different files, no dependencies)
- Include exact file paths in descriptions

## Path Conventions
- **Single project**: `src/`, `tests/` at repository root
- **Web app**: `backend/src/`, `frontend/src/`
- **Mobile**: `api/src/`, `ios/src/` or `android/src/`
- Paths shown below assume single project - adjust based on plan.md structure

## Phase 3.1: Setup
- [ ] T001 Create project structure per implementation plan
- [ ] T002 Initialize .NET 8.0 WPF solution with project files
- [ ] T003 [P] Configure linting and formatting tools (EditorConfig, StyleCop)
- [ ] T004 [P] Set up logging configuration with extensive logging as per user preference

## Phase 3.2: Tests First (TDD) ⚠️ MUST COMPLETE BEFORE 3.3
**CRITICAL: These tests MUST be written and MUST FAIL before ANY implementation**
- [ ] T005 [P] Contract test POST /video/load in tests/contract/test_video_load.py
- [ ] T006 [P] Contract test POST /video/process in tests/contract/test_video_process.py
- [ ] T007 [P] Contract test POST /command/build in tests/contract/test_command_build.py
- [ ] T008 [P] Contract test POST /command/preview in tests/contract/test_command_preview.py
- [ ] T009 [P] Integration test Send To menu workflow in tests/integration/test_send_to_workflow.py
- [ ] T010 [P] Integration test video processing workflow in tests/integration/test_video_processing.py
- [ ] T011 [P] Integration test command preview workflow in tests/integration/test_command_preview.py

## Phase 3.3: Core Implementation (ONLY after tests are failing)
- [ ] T012 [P] VideoFile model in src/QuickFFMPEG/Models/VideoFile.cs
- [ ] T013 [P] ProcessingParameters model in src/QuickFFMPEG/Models/ProcessingParameters.cs
- [ ] T014 [P] FFmpegCommand model in src/QuickFFMPEG/Models/FFmpegCommand.cs
- [ ] T015 [P] ProcessingResult model in src/QuickFFMPEG/Models/ProcessingResult.cs
- [ ] T016 [P] EncodingMode enum in src/QuickFFMPEG/Models/EncodingMode.cs
- [ ] T017 [P] VideoProcessingService in src/QuickFFMPEG/Services/VideoProcessingService.cs
- [ ] T018 [P] FFmpegCommandBuilder service in src/QuickFFMPEG/Services/FFmpegCommandBuilder.cs
- [ ] T019 [P] SendToIntegrationService in src/QuickFFMPEG/Services/SendToIntegrationService.cs
- [ ] T020 MainWindowViewModel in src/QuickFFMPEG/ViewModels/MainWindowViewModel.cs
- [ ] T021 ProcessingViewModel in src/QuickFFMPEG/ViewModels/ProcessingViewModel.cs
- [ ] T022 MainWindow XAML view in src/QuickFFMPEG/Views/MainWindow.xaml
- [ ] T023 MainWindow code-behind in src/QuickFFMPEG/Views/MainWindow.xaml.cs
- [ ] T024 App.xaml application definition in src/QuickFFMPEG/App.xaml
- [ ] T025 App.xaml.cs application startup in src/QuickFFMPEG/App.xaml.cs

## Phase 3.4: Integration
- [ ] T026 Connect VideoProcessingService to FFmpeg execution
- [ ] T027 Implement Send To menu integration with Windows Registry
- [ ] T028 Add real-time command preview with data binding
- [ ] T029 Implement progress feedback and error handling
- [ ] T030 Add file validation and parameter validation
- [ ] T031 Configure logging with extensive detail as per user preference

## Phase 3.5: Installer and Deployment
- [ ] T032 [P] Installer project setup in src/QuickFFMPEG.Installer/Program.cs
- [ ] T033 [P] Installer project file in src/QuickFFMPEG.Installer/QuickFFMPEG.Installer.csproj
- [ ] T034 Send To integration installer logic
- [ ] T035 FFmpeg dependency detection and installation
- [ ] T036 Application uninstaller with cleanup

## Phase 3.6: Polish
- [ ] T037 [P] Unit tests for VideoFile model in tests/unit/test_video_file.cs
- [ ] T038 [P] Unit tests for ProcessingParameters model in tests/unit/test_processing_parameters.cs
- [ ] T039 [P] Unit tests for FFmpegCommand model in tests/unit/test_ffmpeg_command.cs
- [ ] T040 [P] Unit tests for VideoProcessingService in tests/unit/test_video_processing_service.cs
- [ ] T041 [P] Unit tests for FFmpegCommandBuilder in tests/unit/test_ffmpeg_command_builder.cs
- [ ] T042 [P] Unit tests for SendToIntegrationService in tests/unit/test_send_to_integration_service.cs
- [ ] T043 [P] Unit tests for ViewModels in tests/unit/test_view_models.cs
- [ ] T044 Performance optimization for large video files
- [ ] T045 [P] Update quickstart.md with actual usage examples
- [ ] T046 [P] Update README.md with installation and usage instructions
- [ ] T047 Remove code duplication and refactor
- [ ] T048 Run manual testing scenarios from quickstart.md

## Dependencies
- Tests (T005-T011) before implementation (T012-T025)
- Models (T012-T016) before services (T017-T019)
- Services (T017-T019) before ViewModels (T020-T021)
- ViewModels (T020-T021) before Views (T022-T025)
- Core implementation before integration (T026-T031)
- Integration before installer (T032-T036)
- Everything before polish (T037-T048)

## Parallel Execution Examples

### Phase 3.2: Contract Tests (T005-T008)
```
# Launch T005-T008 together:
Task: "Contract test POST /video/load in tests/contract/test_video_load.py"
Task: "Contract test POST /video/process in tests/contract/test_video_process.py"
Task: "Contract test POST /command/build in tests/contract/test_command_build.py"
Task: "Contract test POST /command/preview in tests/contract/test_command_preview.py"
```

### Phase 3.2: Integration Tests (T009-T011)
```
# Launch T009-T011 together:
Task: "Integration test Send To menu workflow in tests/integration/test_send_to_workflow.py"
Task: "Integration test video processing workflow in tests/integration/test_video_processing.py"
Task: "Integration test command preview workflow in tests/integration/test_command_preview.py"
```

### Phase 3.3: Model Creation (T012-T016)
```
# Launch T012-T016 together:
Task: "VideoFile model in src/QuickFFMPEG/Models/VideoFile.cs"
Task: "ProcessingParameters model in src/QuickFFMPEG/Models/ProcessingParameters.cs"
Task: "FFmpegCommand model in src/QuickFFMPEG/Models/FFmpegCommand.cs"
Task: "ProcessingResult model in src/QuickFFMPEG/Models/ProcessingResult.cs"
Task: "EncodingMode enum in src/QuickFFMPEG/Models/EncodingMode.cs"
```

### Phase 3.3: Service Implementation (T017-T019)
```
# Launch T017-T019 together:
Task: "VideoProcessingService in src/QuickFFMPEG/Services/VideoProcessingService.cs"
Task: "FFmpegCommandBuilder service in src/QuickFFMPEG/Services/FFmpegCommandBuilder.cs"
Task: "SendToIntegrationService in src/QuickFFMPEG/Services/SendToIntegrationService.cs"
```

### Phase 3.3: ViewModel Implementation (T020-T021)
```
# Launch T020-T021 together:
Task: "MainWindowViewModel in src/QuickFFMPEG/ViewModels/MainWindowViewModel.cs"
Task: "ProcessingViewModel in src/QuickFFMPEG/ViewModels/ProcessingViewModel.cs"
```

### Phase 3.3: View Implementation (T022-T025)
```
# Launch T022-T025 together:
Task: "MainWindow XAML view in src/QuickFFMPEG/Views/MainWindow.xaml"
Task: "MainWindow code-behind in src/QuickFFMPEG/Views/MainWindow.xaml.cs"
Task: "App.xaml application definition in src/QuickFFMPEG/App.xaml"
Task: "App.xaml.cs application startup in src/QuickFFMPEG/App.xaml.cs"
```

### Phase 3.5: Installer Setup (T032-T033)
```
# Launch T032-T033 together:
Task: "Installer project setup in src/QuickFFMPEG.Installer/Program.cs"
Task: "Installer project file in src/QuickFFMPEG.Installer/QuickFFMPEG.Installer.csproj"
```

### Phase 3.6: Unit Tests (T037-T042)
```
# Launch T037-T042 together:
Task: "Unit tests for VideoFile model in tests/unit/test_video_file.cs"
Task: "Unit tests for ProcessingParameters model in tests/unit/test_processing_parameters.cs"
Task: "Unit tests for FFmpegCommand model in tests/unit/test_ffmpeg_command.cs"
Task: "Unit tests for VideoProcessingService in tests/unit/test_video_processing_service.cs"
Task: "Unit tests for FFmpegCommandBuilder in tests/unit/test_ffmpeg_command_builder.cs"
Task: "Unit tests for SendToIntegrationService in tests/unit/test_send_to_integration_service.cs"
```

## Notes
- [P] tasks = different files, no dependencies
- Verify tests fail before implementing
- Commit after each task
- Avoid: vague tasks, same file conflicts
- Follow extensive logging preference throughout implementation
- Ensure all FFmpeg operations are properly logged for debugging

## Task Generation Rules
*Applied during main() execution*

1. **From Contracts**:
   - Each contract file → contract test task [P]
   - Each endpoint → implementation task
   
2. **From Data Model**:
   - Each entity → model creation task [P]
   - Relationships → service layer tasks
   
3. **From User Stories**:
   - Each story → integration test [P]
   - Quickstart scenarios → validation tasks

4. **Ordering**:
   - Setup → Tests → Models → Services → Endpoints → Polish
   - Dependencies block parallel execution

## Validation Checklist
*GATE: Checked by main() before returning*

- [x] All contracts have corresponding tests
- [x] All entities have model tasks
- [x] All tests come before implementation
- [x] Parallel tasks truly independent
- [x] Each task specifies exact file path
- [x] No task modifies same file as another [P] task
