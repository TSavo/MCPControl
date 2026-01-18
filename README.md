# MCPControl

<p align="center">
  <img src="https://github.com/user-attachments/assets/1c577e56-7b8d-49e9-aaf5-b8550cc6cfc0" alt="MCPControl Logo" width="250">
</p>

<p align="center">
  <a href="https://github.com/TSavo/MCPControl/releases">
    <img src="https://img.shields.io/badge/release-v0.4.0-blue.svg" alt="Latest Release">
  </a>
</p>

Cross-platform desktop automation server for the [Model Context Protocol](https://modelcontextprotocol.io/), providing programmatic control over mouse, keyboard, screen capture, and clipboard operations.

> **This is the actively maintained fork** at [github.com/TSavo/MCPControl](https://github.com/TSavo/MCPControl). The original project at [claude-did-this/MCPControl](https://github.com/claude-did-this/MCPControl) is no longer actively developed.

> **Cross-Platform Support**: Uses `@jitsi/robotjs` with prebuilt binaries for Windows, macOS, and Linux. No compilation required!

## 🔥 Why MCPControl?

MCPControl bridges the gap between AI models and your desktop, enabling secure, programmatic control of:

- 🖱️ **Mouse movements and clicks**
- ⌨️ **Keyboard input and shortcuts**
- 📸 **Screen capture with coordinate grid overlay**
- 📋 **Clipboard operations**

## 🔌 Quick Start

### Prerequisites

- **Node.js 20+** (LTS version recommended)
- **npm** package manager

That's it! The `@jitsi/robotjs` library includes prebuilt binaries for all major platforms.

#### Platform-Specific Notes

**Linux**: You may need to install X11 development libraries:
```bash
# Ubuntu/Debian
sudo apt-get install -y libx11-dev libxkbfile-dev libxtst-dev libpng++-dev

# Fedora/RHEL
sudo dnf install -y libX11-devel libxkbfile-devel libXtst-devel libpng-devel
```

**Linux Permissions**: You may need to add your user to the `input` group:
```bash
sudo usermod -a -G input $USER
# Logout and login again for changes to take effect
```

### Installation

```bash
# Clone the repository
git clone https://github.com/TSavo/MCPControl.git
cd MCPControl

# Install dependencies
npm install

# Build the TypeScript project
npm run build

# Run the server
node build/index.js --sse
```

### Configuration

MCPControl works best at **1280x720 resolution** for optimal click accuracy.

Configure your Claude client to connect via SSE transport:

#### Option 1: Direct SSE Connection

For connecting to MCPControl running on a VM or remote machine:

```json
{
  "mcpServers": {
    "MCPControl": {
      "transport": "sse",
      "url": "http://192.168.1.100:3232/mcp"
    }
  }
}
```

#### Option 2: Local Launch with SSE

```json
{
  "mcpServers": {
    "MCPControl": {
      "command": "node",
      "args": ["/path/to/MCPControl/build/index.js", "--sse"]
    }
  }
}
```

## 🔧 CLI Options

```bash
# Run with SSE transport on default port (3232)
node build/index.js --sse

# Run with SSE on custom port
node build/index.js --sse --port 3000

# Run with HTTPS/TLS
node build/index.js --sse --https --cert /path/to/cert.pem --key /path/to/key.pem
```

### Command Line Arguments

- `--sse` - Enable SSE (Server-Sent Events) transport
- `--port [number]` - Specify custom port (default: 3232)
- `--https` - Enable HTTPS/TLS
- `--cert [path]` - Path to TLS certificate (required with --https)
- `--key [path]` - Path to TLS private key (required with --https)

## 🌟 Features

### Screenshot with Coordinate Grid

MCPControl includes a coordinate grid overlay feature for precise clicking:

```javascript
// Take screenshot with grid overlay
await provider.screen.getScreenshot({
  grid: true,           // Enable 100px grid
  gridTransparency: 70  // 0-100 opacity
});

// Custom grid spacing
await provider.screen.getScreenshot({
  grid: 50  // 50px grid spacing
});
```

The grid shows true screen coordinates, making it easy to identify click targets.

### Core Capabilities

| Feature | Description |
|---------|-------------|
| **Mouse Control** | Move, click, double-click, drag, scroll |
| **Keyboard Input** | Type text, key combinations, key hold |
| **Screen Capture** | Screenshots with optional grid overlay |
| **Clipboard** | Read and write clipboard content |

## 🔧 Automation Providers

MCPControl supports multiple automation providers:

- **robotjs** (default) - Cross-platform via `@jitsi/robotjs` (Windows, macOS, Linux)
- **autohotkey** - AutoHotkey v2 scripting (Windows only)
- **powershell** - PowerShell clipboard provider (Windows only)

### Provider Configuration

```bash
# Use a specific provider
export AUTOMATION_PROVIDER=robotjs

# Mix providers for different operations
export AUTOMATION_KEYBOARD_PROVIDER=autohotkey
export AUTOMATION_CLIPBOARD_PROVIDER=powershell
```

## ⚠️ IMPORTANT DISCLAIMER

**THIS SOFTWARE IS EXPERIMENTAL AND POTENTIALLY DANGEROUS**

- Giving AI models direct control over your computer is inherently risky
- This software can control your mouse, keyboard, and system functions
- Use only in controlled environments with appropriate safety measures
- The creators accept NO responsibility for any damage or consequences

**USE AT YOUR OWN RISK**

## 🚧 Known Limitations

- Window management operations return "not supported" (robotjs limitation)
- Works best at 1280x720 resolution, single screen
- Some operations may require elevated permissions
- AutoHotkey provider only works on Windows

## 📚 Dependencies

- [@modelcontextprotocol/sdk](https://www.npmjs.com/package/@modelcontextprotocol/sdk) - MCP SDK
- [@jitsi/robotjs](https://www.npmjs.com/package/@jitsi/robotjs) - Cross-platform automation
- [clipboardy](https://www.npmjs.com/package/clipboardy) - Clipboard handling
- [sharp](https://www.npmjs.com/package/sharp) - Image processing
- [zod](https://www.npmjs.com/package/zod) - Schema validation

## 🛠️ Development

```bash
# Run tests
npm test

# Run with coverage
npm run test:coverage

# Lint code
npm run lint

# Format code
npm run format
```

See [CONTRIBUTING.md](CONTRIBUTING.md) for development guidelines.

## 👥 Contributing

Pull requests welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## ⚖️ License

MIT License - see LICENSE file for details.

## 📖 References

- [Model Context Protocol Documentation](https://modelcontextprotocol.github.io/)
- [Jitsi RobotJS Fork](https://github.com/nickeddy/robotjs)
