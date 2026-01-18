# MCPControl Automation Providers

MCPControl supports multiple automation providers for flexibility across different platforms and use cases.

## Available Providers

### RobotJS Provider (Default)

The RobotJS provider uses [@jitsi/robotjs](https://github.com/nickeddy/robotjs), an actively maintained fork of the original robotjs library. It provides cross-platform support for Windows, macOS, and Linux with **prebuilt binaries** - no compilation required.

**Features:**
- Mouse control (move, click, double-click, drag, scroll)
- Keyboard input (type text, key combinations, key hold)
- Screen capture with grid overlay
- Cross-platform (Windows, macOS, Linux)

**Limitations:**
- Window management operations are not supported
- Some key combinations may behave differently across platforms

### AutoHotkey Provider (Windows Only)

Uses AutoHotkey v2 for Windows automation. Useful for advanced Windows-specific automation scenarios.

### PowerShell Clipboard Provider (Windows Only)

Uses PowerShell for clipboard operations on Windows. Can be mixed with other providers.

## Selecting a Provider

Set the `AUTOMATION_PROVIDER` environment variable:

```bash
# Use the RobotJS provider (default)
AUTOMATION_PROVIDER=robotjs node build/index.js --sse

# Use AutoHotkey on Windows
AUTOMATION_PROVIDER=autohotkey node build/index.js --sse
```

### Modular Provider Configuration

Mix and match providers for different operations:

```bash
export AUTOMATION_KEYBOARD_PROVIDER=autohotkey
export AUTOMATION_MOUSE_PROVIDER=robotjs
export AUTOMATION_SCREEN_PROVIDER=robotjs
export AUTOMATION_CLIPBOARD_PROVIDER=powershell
```

## RobotJS Provider Details

### Screenshot with Grid Overlay

The RobotJS provider supports a coordinate grid overlay for precise clicking:

```javascript
// Enable grid with default 100px spacing
await provider.screen.getScreenshot({ grid: true });

// Custom grid spacing (50px)
await provider.screen.getScreenshot({ grid: 50 });

// Adjust grid transparency (0-100)
await provider.screen.getScreenshot({
  grid: true,
  gridTransparency: 70
});
```

The grid displays true screen coordinates, accounting for any image resizing. This makes it easy to identify exact click positions.

### Platform Notes

**Windows**: Works out of the box.

**macOS**: Works out of the box. May require accessibility permissions.

**Linux**:
- Requires X11 (Wayland not supported)
- May need to install X11 development libraries
- May require `input` group membership for input device access

## Creating Custom Providers

To add a new provider, implement the `AutomationProvider` interface in `src/interfaces/provider.ts`:

```typescript
interface AutomationProvider {
  keyboard: KeyboardAutomation;
  mouse: MouseAutomation;
  screen: ScreenAutomation;
  clipboard: ClipboardAutomation;
}
```

See existing providers in `src/providers/` for implementation examples.
