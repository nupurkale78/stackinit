# stackinit

> **Stop copy-pasting ESLint, Prettier, and CI configs.** `stackinit` does it once, correctly, and never overwrites your existing files.

[![npm version](https://img.shields.io/npm/v/stackinit.svg)](https://www.npmjs.com/package/stackinit)
[![npm downloads](https://img.shields.io/npm/dm/stackinit.svg)](https://www.npmjs.com/package/stackinit)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/nupurkale78/stackinit.svg)](https://github.com/nupurkale78/stackinit)
[![GitHub issues](https://img.shields.io/github/issues/nupurkale78/stackinit.svg)](https://github.com/nupurkale78/stackinit/issues)

## Who this is for

**For solo devs and teams who want CI + linting + formatting without thinking.**

If you're tired of:

- Manually setting up ESLint configs for every new project
- Copy-pasting `.prettierrc` files
- Writing GitHub Actions workflows from scratch
- Configuring Husky hooks over and over
- Being scared that a generator will overwrite your existing configs

Then `stackinit` is for you.

**Not for you if:** You need full control over every config file, or you prefer interactive setup wizards.

---

## Why stackinit won't wreck your repo

**This is the feature that makes stackinit different:**

### 🛡️ Non-destructive by design

Most project generators are invasive. They overwrite files. They ask questions. They assume you're starting from scratch.

`stackinit` does the opposite:

- ✅ **Never overwrites existing files** — If you already have `.eslintrc.json`, it skips it
- ✅ **Works on existing projects** — Add CI to a 5-year-old repo without touching anything else
- ✅ **Zero prompts** — Everything is configurable via flags, no interactive questions
- ✅ **Dry-run mode** — See exactly what it will do before it does it

```bash
npx stackinit --dry-run
```

**Example output:**

```
✓ Detected Next.js + TypeScript
✓ Using pnpm (detected from pnpm-lock.yaml)
✓ Skipping existing .eslintrc.json (already exists)
✓ Creating .github/workflows/ci.yml
✓ Creating .prettierrc.json
✓ Creating .gitignore
✓ Setting up Husky pre-commit hook
✓ Will install: eslint, prettier, husky, lint-staged

Ready to proceed? Run without --dry-run to apply.
```

This is why developers who've been burned by other generators trust `stackinit`.

---

## Quick start

```bash
npm i stackinit
npx stackinit
```

That's it. It will:

- Auto-detect your project type (Node, React, Next.js, Vite)
- Detect your package manager (npm, yarn, pnpm)
- Generate only the configs you don't have
- Set up Husky git hooks
- Create GitHub Actions CI workflow
- Install all required dependencies

**Want to see what it'll do first?**

```bash
npx stackinit --dry-run
```

**Want stricter rules and commitlint?**

```bash
npx stackinit --strict
```

**Want Docker files too?**

```bash
npx stackinit --docker
```

---

## What you get

### Configuration files (only if missing)

- **`.eslintrc.json`** - TypeScript-aware, React-aware ESLint config
- **`.prettierrc.json`** - Sensible Prettier defaults
- **`.prettierignore`** - Smart ignore patterns
- **`.gitignore`** - Comprehensive Node.js .gitignore
- **`.editorconfig`** - Consistent coding styles
- **`.env.example`** - Environment variables template

### Git hooks (Husky)

- **pre-commit** - Runs lint-staged (lint + format on commit)
- **commit-msg** - Runs commitlint (only in `--strict` mode)

### CI/CD

- **`.github/workflows/ci.yml`** - GitHub Actions that:
  - Installs dependencies
  - Runs linting
  - Runs type checking (if TypeScript)
  - Runs tests (if present)

### Docker (optional, with `--docker`)

- **`Dockerfile`** - Multi-stage production build
- **`docker-compose.yml`** - Development setup

### Package.json scripts (only if missing)

- `lint` - Run ESLint
- `lint:fix` - Auto-fix ESLint issues
- `format` - Format code with Prettier
- `format:check` - Check formatting
- `type-check` - TypeScript type checking (if TypeScript detected)
- `prepare` - Husky install hook

---

## How it works

### Auto-detection

`stackinit` intelligently detects:

- **Project type**: Node backend, React, Next.js, Vite
- **Package manager**: npm, yarn, pnpm (via lock files)
- **TypeScript**: Checks for `tsconfig.json` or TypeScript in dependencies
- **Monorepo**: Detects pnpm workspaces, Lerna, Nx, Turborepo, Rush

Then it generates the right configs for your setup:

- React projects → React ESLint plugins
- Next.js projects → Next.js ESLint config
- TypeScript projects → TypeScript ESLint parser
- Monorepos → Monorepo-aware configurations

### Zero configuration

No prompts. No questions. Sensible defaults that work for 90% of projects.

Everything is configurable via flags if you need it:

```bash
npx stackinit [options]

Options:
  --strict        Enable stricter lint rules and CI failure on warnings
  --docker        Generate Dockerfile and docker-compose.yml
  --ci-only       Generate only GitHub Actions workflow
  --dry-run       Show what files would be created without writing
  -h, --help      Display help for command
  -V, --version   Display version number
```

---

## Examples

**Add CI to an existing project:**

```bash
npx stackinit --ci-only
```

**Full setup with strict mode and Docker:**

```bash
npx stackinit --strict --docker
```

**Preview what will happen:**

```bash
npx stackinit --dry-run
```

---

## After running

`stackinit` automatically:

- ✅ Installs all required dependencies (ESLint, Prettier, Husky, lint-staged, etc.)
- ✅ Detects and installs TypeScript ESLint plugins if TypeScript is detected
- ✅ Detects and installs React plugins if React is detected
- ✅ Installs commitlint if `--strict` mode is enabled
- ✅ Initializes Husky git hooks (if in a git repository)

**That's it.** You're ready to start developing.

---

## Strict mode

When using `--strict`:

- Stricter ESLint rules (more opinionated)
- CI fails on warnings (not just errors)
- Commitlint enabled (enforces conventional commits)
- More aggressive TypeScript checks

Use this if you want maximum code quality enforcement.

---

## Requirements

- Node.js >= 18.0.0
- Git repository (for Husky setup)

---

## Philosophy

`stackinit` is opinionated. It makes decisions for you:

- **Zero configuration by default** - Sensible defaults that work for most projects
- **Non-destructive** - Never overwrites existing files
- **TypeScript-first** - Optimized for TypeScript but works with JavaScript
- **No interactive prompts** - Everything is configurable via flags
- **Production-ready** - Includes CI/CD, linting, formatting, and git hooks out of the box

If you disagree with these opinions, `stackinit` might not be for you. And that's okay.

---

## Development

To test `stackinit` locally during development:

```bash
# Install dependencies
npm install

# Development mode (runs TypeScript directly)
npm run dev

# Or build and test
npm run build
npm start

# Test with options (note: use -- to pass flags to the script)
npm run dev -- --dry-run
npm run dev -- --strict
npm run dev -- --docker
```

**Important:** When using npm scripts, use `--` to pass flags to the underlying command. For example: `npm run dev -- --docker`

For detailed development and testing instructions, see [CONTRIBUTING.md](CONTRIBUTING.md).

---

## Contributing

Contributions are welcome! Please read our [Contributing Guidelines](CONTRIBUTING.md) for details on our code of conduct and the process for submitting pull requests.

---

## License

MIT
