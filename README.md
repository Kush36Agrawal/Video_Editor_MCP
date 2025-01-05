# Video Editor MCP Server

A powerful video editing MCP server that leverages FFmpeg to perform video editing operations through natural language commands.

<a href="https://glama.ai/mcp/servers/ov0qov2xh1"><img width="380" height="200" src="https://glama.ai/mcp/servers/ov0qov2xh1/badge" alt="Video Editor Server MCP server" /></a>

## Components

### Tools

The server implements one main tool:

* `execute_ffmpeg`: Executes FFmpeg commands with progress tracking
  * Takes a command string as input
  * Validates and executes FFmpeg operations
  * Reports real-time progress during processing
  * Handles errors and provides detailed feedback
  * Supports all FFmpeg operations including:
    - Trimming/cutting
    - Merging videos
    - Converting formats
    - Adjusting speed
    - Adding audio tracks
    - Extracting audio
    - Adding subtitles
    - Basic filters (brightness, contrast, etc.)

## Configuration

### Prerequisites

1. FFmpeg must be installed and accessible in your system PATH
2. Python 3.9 or higher
3. Required Python packages:
   ```
   mcp
   httpx
   ```

### Installation

1. Install FFmpeg if not already installed:
   ```bash
   # On macOS with Homebrew
   brew install ffmpeg

   # On Windows with Chocolatey
   choco install ffmpeg

   # On Ubuntu/Debian
   sudo apt install ffmpeg
   ```

2. Install the video editor package:
   ```bash
   uv add video-editor
   ```

### Claude Desktop Integration

Configure in your Claude Desktop config file:

On MacOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
On Windows: `%APPDATA%/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "video-editor": {
      "command": "uv",
      "args": ["run", "video-editor"]
    }
  }
}
```

## Development

### Building and Publishing

1. Sync dependencies:
   ```bash
   uv sync
   ```

2. Build package:
   ```bash
   uv build
   ```

3. Publish to PyPI:
   ```bash
   uv publish
   ```

Note: Set PyPI credentials via:
* Token: `--token` or `UV_PUBLISH_TOKEN`
* Or username/password: `--username`/`UV_PUBLISH_USERNAME` and `--password`/`UV_PUBLISH_PASSWORD`

### Debugging

For the best debugging experience, use the MCP Inspector:

```bash
npx @modelcontextprotocol/inspector uv --directory /path/to/video_editor run video-editor
```

### Example Usage

Once connected to Claude Desktop, you can make natural language requests like:

1. "Trim video.mp4 from 1:30 to 2:45"
2. "Convert input.mp4 to WebM format"
3. "Speed up video.mp4 by 2x"
4. "Merge video1.mp4 and video2.mp4"
5. "Extract audio from video.mp4"
6. "Add subtitles.srt to video.mp4"

The server will:
1. Parse your request
2. Generate the appropriate FFmpeg command
3. Execute it with progress tracking
4. Provide feedback on completion

## Error Handling

The server includes robust error handling for:
- Invalid input files
- Malformed FFmpeg commands
- Runtime execution errors
- Progress tracking issues

All errors are reported back to the client with detailed messages for debugging.

## Security Considerations

- Only processes files in explicitly allowed directories
- Validates FFmpeg commands before execution
- Sanitizes all input parameters
- Reports detailed error messages for security-related issues

## Contributing

Contributions are welcome! Please follow these steps:
1. Fork the repository
2. Create your feature branch
3. Make your changes
4. Submit a pull request

