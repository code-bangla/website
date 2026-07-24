# Agent Instructions for Code Bangla Website

This file is the entry point for AI coding agents working in this repository. It mirrors the AGENTS.md convention used by other AI tools. `github/copilot-instructions.md` and `CLAUDE.md` is a symlink to this file. Claude Code and the AGENTS.md convention read identical content.

## Non-negotiable — read first if you're opening a PR or editing this repo

- A PR that resolves an issue MUST have Closes /#N / Fixes /#N / Resolves /#N in its BODY — NON-NEGOTIABLE. Verify it's there before `gh pr create`.
- This is a public repository, never commit internal/competitive discussion or sensitive info (strategy, private attributions, `.env`, tokens) to any tracked file or commit message.
- Avoid attempting to assume the lead role in this repository. Your position should be that of a copilot collaborating with an engineer. Do not seek to take on the responsibilities of the engineer.

## Quick Reference

**Package Manager:** Bun (`bun` command, not `npm`)

When starting the dev server, use background mode:

```bash
bun run astro dev --background
```

Manage the background server with bun run astro dev stop, bun run astro dev status, and bun run astro dev logs.

**Key Commands:**

- `bun run dev` - Start dev server at localhost:3000
- `bun run astro dev --background` - Start dev server at localhost:3000
- `bun run build` - Build for production (includes legacy HTML post-processing)
- `bun run astro check` - Type-check Astro files (use this instead of running full build)
- `bun run prettier -w .` - Format all files with Prettier
- `bun run prettier --check .` - Check formatting without modifying files

## Project Structure

### Core Architecture

This is an **Astro 7** static site generator portfolio website with:

- **Astro** for page routing (`src/pages/`) and layout composition
- **React 19** for interactive components (minimal usage - mostly static, mainly for icons)
- **TypeScript** for type safety
- **Tailwind CSS 4** with **DaisyUI** component library
- **Content Collection** for blog posts (`src/data/posts/`) with frontmatter schema validation

### Directory Layout

- `src/pages/` - Astro pages (routes). Each `.astro` file becomes a page.
- `src/layouts/` - Reusable Astro layouts (page wrappers, common structure)
- `src/components/` - Reusable Astro and React components

## Development Conventions

### Astro Components

- Use `.astro` extension for file-based routing and layout components
- Use `.tsx` or `.jsx` for React components (prefer TypeScript)
- Import React components into `.astro` files with `client:directive` for interactivity (e.g., `client:load`, `client:idle`)
- Astro components are rendered at build-time; use client directives sparingly
- Prefer astro components over react. But use react, vue, svelte and preact when they are the better option.

### Styling

- Use **Tailwind CSS** utility classes for all styling

## Code Quality & Formatting

### Prettier Configuration

- **Plugins:**
  - `prettier-plugin-astro` - Format `.astro` files correctly
  - `prettier-plugin-tailwindcss` - Sort Tailwind classes by specificity
  - `@ianvs/prettier-plugin-sort-imports` - Organize imports (grouped, sorted)
- **Editor Integration:**
  - VS Code uses Prettier as default formatter (see `.vscode/settings.json`)
  - Format on save is enabled
  - Tab size: 2 spaces

### Type Checking

- Run `bun run astro check` before committing (checks TypeScript + Astro syntax)
- Astro uses strict TypeScript config (extends `astro/tsconfigs/strict`)
- JSX is set to `react-jsx` with React import source

### Linting & Quality Checks

- **CodeQL** - Security scanning (runs on push, see `.github/workflows/codeql.yml`)
- **Markdown Linting** - Configured in `.markdownlint.json` (some rules disabled for flexibility)

## Testing & Diagnostics

- **No unit tests configured** - This is a static portfolio site with minimal interactivity
- **Use** `bun run astro check` for pre-build validation instead of running full builds
- GitHub Actions run diagnostics on every push/PR
- View workflow status in README badges

## MCP Servers and Skills

The project is configured with MCP servers and skills for IDE assistance:

Read `.mcp.json` to enable necessary MCP servers.
Read `.agents/skills` to use them.

## Common Tasks

### Add a New Page

1. Create `.astro` file in `src/pages/` (filename becomes route)
2. Wrap content with appropriate layout from `src/layouts/`
3. Use components from `src/components/`
4. Styling with Tailwind + DaisyUI classes (always prefer using DaisyUI over raw Tailwind)


### Add a React Component

1. Create `.tsx` file in `src/components/` (not in `pages/`)
2. Use TypeScript types for props
3. Import and use in `.astro` files with `client:directive` if interactive

### Run Diagnostics Locally

Before pushing, run type-checking (faster than full build):

```bash
bun run astro check
```

Then verify formatting:

```bash
bun run prettier --check .
```

## Deployment & Performance

- Site is optimized with HTML compression, inlined critical CSS, and responsive image loading.
- Static site generation (no server required)
