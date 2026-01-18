# Changelog

All notable changes to MCPControl will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.4.0] - 2026-01-17

This release marks the transition to an actively maintained fork at [github.com/TSavo/MCPControl](https://github.com/TSavo/MCPControl).

### Changed
- **BREAKING**: Replaced `@nut-tree-fork/libnut` with `@jitsi/robotjs` as the default automation provider
  - No more compilation required - robotjs includes prebuilt binaries
  - Simplified installation process
- Renamed provider from `nutjs` to `robotjs`
- Window management operations now return "not supported" (robotjs limitation)
- Requires Node.js 20+ (previously 18+)

### Added
- Screenshot grid overlay feature for precise clicking
  - `grid: true | number` - Enable coordinate grid (true = 100px, or custom spacing)
  - `gridTransparency: 0-100` - Control grid opacity
- Grid shows true screen coordinates, accounting for image resizing

### Updated Dependencies
- zod 3.25 → 4.3 (updated refine API to use superRefine)
- vitest 3.2 → 4.0 (updated mock patterns)
- uuid 11 → 13
- clipboardy 4 → 5
- @types/node 22 → 25
- Removed deprecated @types/uuid (uuid has built-in types)

### Removed
- `@nut-tree-fork/libnut` dependency
- keysender provider (removed in previous version)
- Complex build prerequisites (Visual Studio Build Tools, Python, etc.)

## [0.3.0] - 2025-07-19

### Changed
- Replaced keysender with nutjs (@nut-tree-fork/libnut) as the default automation provider
- Updated build requirements to include native compilation tools
- Disabled npm publishing workflow (nutjs requires building from source)

### Added
- Type definitions for @nut-tree-fork/libnut
- Documentation about extensibility for macOS and Linux providers

### Removed
- keysender dependency and provider implementation
- Empty robotjs provider directory
- Test scripts that were specific to keysender

### Fixed
- All tests now pass with nutjs provider
- Async/await issues in screen automation tests
- Updated all documentation to reflect nutjs as default provider

## [0.2.0] - 2025-03-27

### Added
- Structured logging with Pino
- Modular provider architecture
- AutoHotkey v2 provider support
- PowerShell clipboard provider
- Provider registry system
- E2E testing framework

### Changed
- Improved error handling and response consistency
- Enhanced CI/CD pipeline with caching
- Better TypeScript type safety

### Fixed
- Window management reliability issues
- Screenshot capture edge cases
- Build process optimizations

## [0.1.22] - Previous releases

See GitHub releases for full history.
