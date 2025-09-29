# Data Model: Quick-FFMPEG-V2 Frontend Application

**Feature**: Quick-FFMPEG-V2 Frontend Application  
**Date**: 2024-12-19  
**Phase**: 1 - Design & Contracts

## Core Entities

### VideoFile
Represents the source video file selected by the user.

**Properties**:
- `FilePath` (string): Full path to the video file
- `FileName` (string): Name of the file without path
- `Duration` (TimeSpan): Total duration of the video
- `Width` (int): Video width in pixels
- `Height` (int): Video height in pixels
- `FrameRate` (double): Frames per second
- `VideoCodec` (string): Video codec (e.g., "h264", "hevc")
- `AudioCodec` (string): Audio codec (e.g., "aac", "mp3")
- `FileSize` (long): File size in bytes
- `LastModified` (DateTime): File modification timestamp

**Validation Rules**:
- FilePath must exist and be accessible
- Duration must be positive
- Width and Height must be positive integers
- FrameRate must be positive

**State Transitions**:
- `Unloaded` → `Loading` → `Loaded` (when metadata is extracted)
- `Loaded` → `Processing` → `Processed` (when video is being/been processed)

### ProcessingParameters
Represents user-configured options for video processing.

**Properties**:
- `StartTime` (TimeSpan?): Start time for trimming (null = no trimming)
- `EndTime` (TimeSpan?): End time for trimming (null = no trimming)
- `CropX` (int?): X offset for cropping (null = no cropping)
- `CropY` (int?): Y offset for cropping (null = no cropping)
- `CropWidth` (int?): Width for cropping (null = no cropping)
- `CropHeight` (int?): Height for cropping (null = no cropping)
- `EncodingMode` (EncodingMode): Stream or Encoding mode
- `QualityPreset` (string?): Quality preset name (null = default)
- `CustomQuality` (int?): Custom quality value (null = use preset)
- `OutputFormat` (string): Output file format (e.g., "mp4", "avi")
- `OutputPath` (string): Full path for output file

**Validation Rules**:
- StartTime must be less than EndTime if both are specified
- StartTime and EndTime must be within video duration
- Crop dimensions must be positive and within video bounds
- OutputPath must be writable directory
- OutputFormat must be supported by FFmpeg

**Enums**:
```csharp
public enum EncodingMode
{
    Stream,     // Default - no encoding, copy streams
    Encoding    // Re-encode with specified quality
}
```

### FFmpegCommand
Represents the generated FFmpeg command string and execution context.

**Properties**:
- `CommandString` (string): Complete FFmpeg command line
- `InputFile` (string): Input file path
- `OutputFile` (string): Output file path
- `Arguments` (string[]): Individual command arguments
- `EstimatedDuration` (TimeSpan?): Estimated processing time
- `IsValid` (bool): Whether command is valid for execution

**Methods**:
- `BuildCommand(ProcessingParameters, VideoFile)`: Construct command from parameters
- `Validate()`: Check if command is valid
- `GetPreviewString()`: Get formatted preview for UI

**Validation Rules**:
- CommandString must not be empty
- InputFile must exist
- OutputFile path must be writable
- All required arguments must be present

### ProcessingResult
Represents the result of video processing operation.

**Properties**:
- `Success` (bool): Whether processing completed successfully
- `OutputFile` (string?): Path to output file (null if failed)
- `ErrorMessage` (string?): Error message if processing failed
- `ProcessingTime` (TimeSpan): Time taken to process
- `OutputFileSize` (long?): Size of output file in bytes
- `ExitCode` (int): FFmpeg exit code

**State Transitions**:
- `NotStarted` → `InProgress` → `Completed` (success)
- `NotStarted` → `InProgress` → `Failed` (error)

## Service Interfaces

### IVideoProcessingService
Handles video file analysis and processing operations.

**Methods**:
- `Task<VideoFile> LoadVideoFileAsync(string filePath)`: Load and analyze video file
- `Task<ProcessingResult> ProcessVideoAsync(FFmpegCommand command)`: Execute FFmpeg command
- `Task<bool> ValidateVideoFileAsync(string filePath)`: Check if file is valid video

### IFFmpegCommandBuilder
Builds FFmpeg command strings from user parameters.

**Methods**:
- `FFmpegCommand BuildCommand(ProcessingParameters parameters, VideoFile videoFile)`: Create command
- `string GetPreviewString(ProcessingParameters parameters, VideoFile videoFile)`: Get preview
- `bool ValidateParameters(ProcessingParameters parameters, VideoFile videoFile)`: Validate inputs

### ISendToIntegrationService
Handles Windows Send To menu integration.

**Methods**:
- `Task<bool> InstallSendToIntegrationAsync()`: Add to Send To menu
- `Task<bool> UninstallSendToIntegrationAsync()`: Remove from Send To menu
- `bool IsInstalled()`: Check if already integrated

## Data Flow

1. **File Selection**: User selects video file → `VideoFile` entity created
2. **Parameter Configuration**: User adjusts settings → `ProcessingParameters` updated
3. **Command Generation**: Parameters + VideoFile → `FFmpegCommand` built
4. **Command Preview**: Command string displayed in UI
5. **Execution**: Command executed → `ProcessingResult` returned
6. **Completion**: Success/failure feedback provided to user

## Validation Strategy

- **Input Validation**: All user inputs validated before command generation
- **Command Validation**: FFmpeg command validated before execution
- **File Validation**: Video files validated before processing
- **Output Validation**: Output files validated after processing

## Error Handling

- **File Access Errors**: Handle locked files, permission issues
- **FFmpeg Errors**: Parse FFmpeg error output for user-friendly messages
- **Validation Errors**: Clear error messages for invalid parameters
- **System Errors**: Handle disk space, memory, and other system issues
