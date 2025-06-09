# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Turborepo monorepo for a content management system (CMS) starter project using pnpm workspaces. It contains two Next.js applications and shared packages.

## Essential Commands

### Development
- `pnpm dev` - Start all apps in development mode (web on port 3000, docs on port 3001)
- `pnpm dev --filter=web` - Start only the web app
- `pnpm dev --filter=docs` - Start only the docs app

### Building
- `pnpm build` - Build all apps and packages
- `pnpm build --filter=web` - Build only the web app
- `pnpm build --filter=docs` - Build only the docs app

### Code Quality
- `pnpm lint` - Lint all packages
- `pnpm format` - Format code with Prettier
- `pnpm check-types` - Run TypeScript type checking across all packages

### Package Management
- Use `pnpm add <package> --filter=<workspace>` to add dependencies to specific workspaces
- Example: `pnpm add react-hook-form --filter=web`

## Architecture

### Monorepo Structure
- `apps/web` - Main CMS application with Lexical editor integration
- `apps/docs` - Documentation site
- `packages/ui` - Shared React component library (Button, Card, Code components)
- `packages/eslint-config` - Shared ESLint configurations
- `packages/typescript-config` - Shared TypeScript configurations

### Key Technologies
- **Framework**: Next.js 15.3.0 with App Router
- **React**: Version 19.1.0
- **TypeScript**: Version 5.8.2
- **Text Editor**: Lexical (Facebook's extensible text editor framework)
- **Build System**: Turborepo with task caching
- **Package Manager**: pnpm 9.0.0
- **Node.js**: Requires >=18

### Turbo Pipeline
The `turbo.json` defines:
- Build tasks depend on upstream builds (`^build`)
- Dev tasks are persistent and not cached
- Build outputs are cached in `.next/**` (excluding `.next/cache`)

### Component Development
To generate new UI components:
```bash
cd packages/ui
pnpm turbo gen react-component
```

## Important Notes
- The web app includes Lexical editor at `/design` route
- Both apps use Turbopack for faster development builds
- ESLint is configured with `--max-warnings 0` for strict linting
- All packages use TypeScript with shared configurations