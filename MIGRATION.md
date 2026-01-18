# MCPControl Migration Guide

## Migrating to the Actively Maintained Fork

The original MCPControl project at [claude-did-this/MCPControl](https://github.com/claude-did-this/MCPControl) is no longer actively developed.

**This fork at [TSavo/MCPControl](https://github.com/TSavo/MCPControl) is actively maintained** with:
- Cross-platform support via `@jitsi/robotjs`
- No compilation required (prebuilt binaries)
- Modern dependency stack (Node 20+, Zod 4, Vitest 4)
- New features like screenshot grid overlay

## Migrating from v0.3.0 to v0.4.0

### Major Changes

#### 1. Provider Changed from nutjs to robotjs
- **v0.3.0**: Used `@nut-tree-fork/libnut` (required compilation)
- **v0.4.0**: Uses `@jitsi/robotjs` (prebuilt binaries, no compilation)

#### 2. Simplified Installation
- **v0.3.0**: Required Visual Studio Build Tools, Python, cmake-js, etc.
- **v0.4.0**: Just Node.js 20+ and npm

#### 3. Window Management
- **v0.3.0**: Had window management support via nutjs
- **v0.4.0**: Window management returns "not supported" (robotjs limitation)

### Migration Steps

#### Step 1: Clone the New Fork
```bash
# Clone from the actively maintained fork
git clone https://github.com/TSavo/MCPControl.git
cd MCPControl
```

#### Step 2: Install Dependencies
No more build tools needed!
```bash
npm install
npm run build
```

#### Step 3: Update Provider Configuration
Change `nutjs` to `robotjs`:
```bash
# Old (v0.3.0)
export AUTOMATION_PROVIDER=nutjs

# New (v0.4.0)
export AUTOMATION_PROVIDER=robotjs
```

### New Features in v0.4.0

#### Screenshot Grid Overlay
Take screenshots with a coordinate grid for precise clicking:
```javascript
// Enable grid with default 100px spacing
await provider.screen.getScreenshot({ grid: true });

// Custom spacing and transparency
await provider.screen.getScreenshot({
  grid: 50,           // 50px grid
  gridTransparency: 70 // 70% opacity
});
```

### Breaking Changes

#### 1. Provider Name
- **v0.3.0**: Default provider was `nutjs`
- **v0.4.0**: Default provider is `robotjs`

#### 2. Window Management
Window management methods now return "not supported":
- `getActiveWindow()`
- `focusWindow()`
- `resizeWindow()`
- `repositionWindow()`

If you need window management, use the AutoHotkey provider on Windows.

#### 3. Node.js Version
- **v0.3.0**: Required Node.js 18+
- **v0.4.0**: Requires Node.js 20+

### Troubleshooting

#### Module Not Found
If you see module errors, ensure you've rebuilt:
```bash
rm -rf node_modules build
npm install
npm run build
```

#### Linux Permission Issues
Add your user to the input group:
```bash
sudo usermod -a -G input $USER
# Logout and login again
```

#### Provider Not Found
Use lowercase provider names:
```bash
# Correct
export AUTOMATION_PROVIDER=robotjs

# Incorrect
export AUTOMATION_PROVIDER=RobotJS
```

---

## Migrating from v0.2.0 to v0.3.0

See the [v0.3.0 release notes](RELEASE_NOTES_v0.3.0.md) for the original migration guide from keysender to nutjs.

---

## Getting Help

If you encounter issues:
1. Check [GitHub Issues](https://github.com/TSavo/MCPControl/issues)
2. Ensure Node.js 20+ is installed
3. Try a fresh install: `rm -rf node_modules && npm install`
