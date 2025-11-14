# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a ticketing system built with a Go backend API and a modern React frontend. The project follows a monorepo structure with separate `api` and `ui` directories.

## Architecture

### Backend (`/api`)
- **Framework**: Cobra CLI application with Viper for configuration
- **Structure**: Standard Go project with cmd package pattern
- **Entry point**: `api/main.go` → `api/cmd/root.go`
- **Configuration**: YAML-based config with environment variable support

### Frontend (`/ui`)
- **Framework**: React 19 with TypeScript
- **Build tool**: Vite with React plugin
- **Routing**: TanStack Router with file-based routing and code splitting
- **State management**: TanStack Query for server state, TanStack Store for client state
- **UI components**: Shadcn/ui with Radix UI primitives
- **Styling**: Tailwind CSS v4 with CSS variables
- **Testing**: Vitest with React Testing Library
- **Development tools**: Biome for linting/formatting, Storybook for component development

## Development Commands

### Backend (Go API)
```bash
# Navigate to API directory
cd api

# Run the application
go run main.go

# Build the application
go build -o ticket-api main.go

# Install dependencies
go mod tidy

# Generate Cobra commands (if needed)
cobra add <command-name>
```

### Frontend (React UI)
```bash
# Navigate to UI directory
cd ui

# Install dependencies
bun install  # or npm install

# Start development server (port 3000)
bun run dev  # or npm run dev

# Build for production
bun run build  # or npm run build

# Run tests
bun run test  # or npm run test

# Lint and format
bun run lint    # or npm run lint
bun run format  # or npm run format
bun run check   # or npm run check

# Storybook development
bun run storybook  # or npm run storybook
```

### Project-wide Commands
```bash
# Using Task (Taskfile.yml)
task default  # Runs "Hello, World!" task

# Using mise for tool management
mise install  # Installs all configured tools
mise run <tool>  # Runs any configured tool
```

## Key Configuration Files

### Backend Configuration
- `api/go.mod` - Go module definition
- `api/.cobra.yaml` - Cobra CLI configuration
- Config files: `$HOME/.api.yaml` or via `--config` flag

### Frontend Configuration
- `ui/package.json` - Dependencies and scripts
- `ui/vite.config.ts` - Vite build configuration with TanStack Router plugin
- `ui/biome.json` - Linting and formatting rules
- `ui/components.json` - Shadcn/ui configuration
- `ui/tsconfig.json` - TypeScript configuration

## Project Structure

### Frontend File Organization
```
ui/src/
├── components/          # Reusable UI components
│   ├── ui/             # Shadcn/ui components
│   └── storybook/      # Storybook stories
├── routes/             # TanStack Router file-based routing
├── hooks/              # Custom React hooks
├── lib/                # Utility functions and configurations
├── data/               # Mock data and fixtures
└── integrations/       # Third-party library integrations
    └── tanstack-query/ # Query client configuration
```

### Import Aliases (configured in vite.config.ts)
- `@/` → `./src/`
- `@/components` → `./src/components/`
- `@/lib` → `./src/lib/`
- `@/hooks` → `./src/hooks/`
- `@/ui` → `./src/components/ui/`

## Development Tools Integration

### Shadcn/ui Components
- Use `pnpx shadcn@latest add <component-name>` to add new components
- Components are located in `ui/src/components/ui/`
- Uses Tailwind CSS with CSS variables for theming

### TanStack Router
- File-based routing in `ui/src/routes/`
- Auto-generates route tree (`routeTree.gen.ts`)
- Supports code splitting and type-safe navigation

### Development Tools
- **Biome**: Linting and formatting (tab indentation, double quotes)
- **Storybook**: Component development environment (port 6006)
- **TanStack Devtools**: Integrated devtools for Router, Query, and Store

## Tools and Environment

The project uses mise for tool management (configured in `mise.toml`):
- Go 1.25.4
- Bun 1.3.2
- Air for hot reloading
- golangci-lint for Go linting
- Task for task runner

## License

GPLv3 - see LICENSE file for details.