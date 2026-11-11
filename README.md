# MAJ

MAJ records a bug while it happens: screen video, console logs, network requests, clicks and your
voice, in one file you can share or hand to an AI coding agent. It runs on macOS, Windows and Linux.

This repository only hosts the release builds. It contains no source code.

## Download

Get the latest version from the **[Releases page](https://github.com/LeandroDettmer/maj-releases/releases/latest)**.

| System | File to download |
| - | - |
| macOS (Apple Silicon and Intel) | `MAJ_<version>_universal.dmg` |
| Windows 10/11 (x64) | `MAJ_<version>_x64-setup.exe` |
| Linux (x64) | `MAJ_<version>_amd64.AppImage` (updates itself) or `MAJ_<version>_amd64.deb` (no automatic updates) |

Once installed, MAJ checks for updates on launch and offers to install them.

### macOS: first launch

The macOS build is not notarized by Apple yet, so macOS blocks the first launch. Either
right-click **MAJ.app** in Applications and choose **Open**, or run:

```sh
xattr -dr com.apple.quarantine /Applications/MAJ.app
```

### Windows: first launch

The installer is not code-signed yet, so SmartScreen may warn. Click **More info → Run anyway**.

## Use your recordings from an AI agent (MCP)

`maj-mcp` is a local [MCP](https://modelcontextprotocol.io) server that lets an AI coding agent
read your MAJ recordings: console errors, failed requests, what you clicked and frames of the
video. It reads files on your computer only and uploads nothing.

If you have MAJ Desktop, open **Settings › AI agents (MCP)** and copy the ready-made config.

Without the desktop app, run it with Node.js 18 or newer. The first run downloads the binary for
your system from this repository's releases.

**Claude Code**

```sh
claude mcp add maj -- npx -y maj-mcp
```

**Cursor** (`~/.cursor/mcp.json`) or a project `.mcp.json`:

```json
{
  "mcpServers": {
    "maj": { "command": "npx", "args": ["-y", "maj-mcp"] }
  }
}
```

Without MAJ Desktop there are no local drafts to list: give the agent the absolute path of a
`.maj` file instead (for example one someone sent you). Screen frames need `ffmpeg` on your `PATH`.

The standalone binaries are also attached to each release: `maj-mcp-darwin-universal.tar.gz`,
`maj-mcp-linux-x64.tar.gz` and `maj-mcp-windows-x64.zip`.

## License

Apache-2.0
