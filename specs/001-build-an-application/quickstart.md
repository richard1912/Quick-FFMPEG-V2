# Quick Start Guide: Quick-FFMPEG-V2

**Feature**: Quick-FFMPEG-V2 Frontend Application  
**Date**: 2024-12-19  
**Phase**: 1 - Design & Contracts

## Prerequisites

- Windows 10/11
- .NET 8.0 Runtime
- FFmpeg installed and accessible via PATH

## Installation

1. **Download and install FFmpeg** (if not already installed):
   - Download from https://ffmpeg.org/download.html
   - Add FFmpeg to your system PATH
   - Verify installation: `ffmpeg -version`

2. **Install Quick-FFMPEG-V2**:
   - Run the installer executable
   - Follow the installation wizard
   - The application will automatically register with Windows Send To menu

## Basic Usage

### Starting the Application

**Method 1: Send To Menu (Recommended)**
1. Right-click on any video file
2. Select "Send to" → "Quick-FFMPEG-V2"
3. The application opens with the selected video pre-loaded

**Method 2: Direct Launch**
1. Double-click the Quick-FFMPEG-V2 executable
2. Click "Select Video File" to choose a video
3. The application loads the selected video

### Video Processing Workflow

1. **Load Video**: Video file is automatically loaded when using Send To menu
2. **Configure Parameters**:
   - **Trimming**: Set start and end times (optional)
   - **Cropping**: Set crop area dimensions and position (optional)
   - **Encoding**: Choose between Stream (default) or Encoding mode
   - **Output**: Specify output file location (defaults to source folder)
3. **Preview Command**: Review the generated FFmpeg command
4. **Process Video**: Click "Process" to execute the command
5. **Monitor Progress**: Watch the progress bar and status updates
6. **Completion**: Receive notification when processing is complete

## Feature Details

### Trimming
- **Start Time**: Set the beginning of the video segment to keep
- **End Time**: Set the end of the video segment to keep
- **Format**: Use time format (HH:MM:SS) or click timeline
- **Preview**: See trimmed duration in real-time

### Cropping
- **Dimensions**: Set width and height for the cropped area
- **Position**: Set X and Y offset from top-left corner
- **Aspect Ratio**: Maintain aspect ratio with lock button
- **Preview**: See crop area overlay on video thumbnail

### Encoding Options
- **Stream Mode** (Default): Copy video/audio streams without re-encoding
  - Fastest processing
  - No quality loss
  - Smaller file size
- **Encoding Mode**: Re-encode with quality settings
  - Quality presets: Low, Medium, High, Lossless
  - Custom quality slider (0-100)
  - Format conversion support

### Command Preview
- **Real-time Updates**: Command updates as you change parameters
- **Copy Command**: Copy FFmpeg command to clipboard
- **Validation**: Invalid parameters are highlighted
- **Formatting**: Readable command with proper spacing

## Advanced Features

### Batch Processing
- Process multiple videos with same settings
- Queue management for large batches
- Progress tracking for each file

### Preset Management
- Save frequently used parameter combinations
- Load presets for quick setup
- Share presets between users

### Error Handling
- **File Validation**: Check video file integrity before processing
- **Parameter Validation**: Prevent invalid combinations
- **FFmpeg Errors**: Display user-friendly error messages
- **Recovery**: Resume interrupted processing

## Troubleshooting

### Common Issues

**"FFmpeg not found" Error**
- Ensure FFmpeg is installed and in PATH
- Restart the application after installing FFmpeg
- Check FFmpeg installation: `ffmpeg -version` in Command Prompt

**"File not accessible" Error**
- Check file permissions
- Ensure file is not open in another application
- Try copying file to a different location

**"Invalid parameters" Error**
- Check trimming times are within video duration
- Verify crop dimensions are within video bounds
- Ensure output path is writable

**"Processing failed" Error**
- Check available disk space
- Verify output format is supported
- Review FFmpeg error message for details

### Performance Tips

- Use Stream mode for fastest processing
- Close other applications during large file processing
- Ensure sufficient disk space (2x source file size)
- Use SSD storage for better performance

### Logging

The application logs all operations for debugging:
- Log location: `%APPDATA%\Quick-FFMPEG-V2\logs\`
- Log level: Detailed (as per user preference)
- Log rotation: Daily with 7-day retention

## Support

For additional help:
- Check the application logs for detailed error information
- Verify FFmpeg installation and version compatibility
- Ensure Windows Send To integration is properly installed
- Contact support with log files for complex issues

## Uninstallation

1. **Remove Send To Integration**:
   - Run the uninstaller
   - Or manually remove from Send To folder

2. **Clean Up Files**:
   - Application data: `%APPDATA%\Quick-FFMPEG-V2\`
   - Registry entries: Removed by uninstaller
   - Log files: Can be safely deleted
