# Contributing to MCPControl

Thank you for your interest in contributing to MCPControl! This document provides guidelines for contributing to the project.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Code Style and Standards](#code-style-and-standards)
- [Testing](#testing)
- [Documentation](#documentation)

## Code of Conduct

Please be respectful and considerate of others when contributing to this project. We aim to foster an inclusive and welcoming community.

## Getting Started

### Prerequisites

- Node.js 20+ (LTS version recommended)
- npm
- git

That's it! The `@jitsi/robotjs` library includes prebuilt binaries for all platforms.

### Setup

1. Fork the repository at [github.com/TSavo/MCPControl](https://github.com/TSavo/MCPControl)
2. Clone your fork:
   ```bash
   git clone https://github.com/YOUR-USERNAME/MCPControl.git
   cd MCPControl
   ```

3. Install dependencies and build:
   ```bash
   npm install
   npm run build
   ```

4. Run tests to verify setup:
   ```bash
   npm test
   ```

## Development Workflow

### Branching Strategy

- `main` branch contains the latest stable code
- Create feature branches from `main` using the naming convention:
  - `feature/feature-name` for new features
  - `bugfix/issue-description` for bug fixes
  - `docs/description` for documentation changes
  - `refactor/description` for code refactoring

### Commit Guidelines

- Write clear, descriptive commit messages
- Reference issue numbers in commit messages when applicable
- Keep commits focused on a single logical change

### Pull Requests

1. Create your feature branch: `git checkout -b feature/amazing-feature`
2. Commit your changes: `git commit -m 'Add some amazing feature'`
3. Push to the branch: `git push origin feature/amazing-feature`
4. Open a Pull Request against `main`
5. Ensure all tests pass and code meets the project standards

## Code Style and Standards

- Use ES module syntax with named imports
- Define TypeScript interfaces in the `types/` directory
- Use try/catch with standardized response objects for error handling
- Follow naming conventions:
  - camelCase for variables/functions
  - PascalCase for interfaces
- Keep functions small and focused on single responsibility
- Add JSDoc comments for public APIs
- Use 2-space indentation and semicolons
- For errors, return `{ success: false, message: string }`
- For success, return `{ success: true, data?: any }`

## Testing

- Place tests in the same directory as implementation with `.test.ts` suffix
- Run tests with `npm test`
- Generate coverage report with `npm run test:coverage`
- Run a single test with `npm test -- tools/keyboard.test.ts`
- Run tests in watch mode with `npm run test:watch`

All new features should include appropriate test coverage. The project uses Vitest 4.x for testing.

### Vitest 4.x Mock Pattern

When mocking classes, use constructor functions:

```typescript
vi.mock('./module.js', () => ({
  MyClass: vi.fn().mockImplementation(function() {
    this.method = vi.fn();
  })
}));
```

## Documentation

- Document public APIs with JSDoc comments
- Update README.md when adding new features
- Keep code comments clear and focused on explaining "why" rather than "what"

## Project Structure

```
/src
  /handlers    - Request handlers and tool management
  /providers   - Automation provider implementations
    /robotjs   - Default cross-platform provider
    /autohotkey - Windows-only provider
  /tools       - Core functionality implementations
  /types       - TypeScript type definitions
  index.ts     - Main application entry point
```

## Areas for Contribution

- Bug fixes for existing functionality
- Documentation improvements
- Test coverage improvements
- New automation providers
- Performance optimizations

---

Thank you for contributing to MCPControl!
