# Design Builder

Claude Code plugin that extracts copy and design from references to build frontend components.

> **Part of [claude-code-plugins](https://github.com/adeonir/claude-code-plugins)** - A curated marketplace of Claude Code plugins for feature development, debugging, frontend generation, and git helpers.

## Features

- Extract content structure from URLs (optional)
- Extract design tokens from reference images (screenshots, mockups)
- Build React components directly with Claude Code
- Auto-scaffold Vite projects when needed
- Auto-loaded skill to avoid generic "AI slop" aesthetics
- Generate 4 HTML+CSS preview variants before building React

## Installation

### Prerequisites

- [Claude Code](https://claude.ai/code) - Anthropic's official CLI for Claude

### Add Marketplace

First, add the marketplace to Claude Code (only needed once):

```bash
/plugin marketplace add adeonir/claude-code-plugins
```

### Install Plugin

```bash
/plugin install design-builder
```

This command automatically:
- Downloads the plugin from the marketplace
- Auto-loads the `frontend-design` skill for distinctive aesthetics
- Makes all commands available in your Claude Code session

## Workflows

Two entry points:

```
# Full: Start from URL reference
URL -> /extract-copy -> copy.yaml -> /extract-design -> design.json

# Minimal: Start from design image only (with brief project description)
Image -> /extract-design -> design.json

# Then build:
-> /build-frontend              # React directly
-> /build-frontend --variants   # 4 HTML previews -> choose -> React
```

## Commands

| Command | Description |
|---------|-------------|
| `/extract-copy` | Extract content from URL to copy.yaml (optional) |
| `/extract-design` | Extract design from images to design.json |
| `/build-frontend` | Build React directly in ./src/ |
| `/build-frontend --variants` | Generate 4 HTML previews, then build React from chosen variant |

## Agents

| Agent | Role |
|-------|------|
| `copy-extractor` | Content Strategist - extracts content from URLs |
| `design-extractor` | Creative Director - extracts design from images |
| `frontend-builder` | Frontend Engineer - builds React (from variant or direct) |
| `variants-builder` | Variants Engineer - generates 4 HTML+CSS previews |

## Skills

| Skill | Description |
|-------|-------------|
| `frontend-design` | Distinctive design principles that avoid generic AI aesthetics |

## Design Variants

Generate 4 HTML+CSS previews to compare before building React:

```bash
/build-frontend --variants
```

This generates:
```
./outputs/
  minimal/index.html    # Text hero, extra whitespace, no cards
  editorial/index.html  # Split hero, generous spacing, flat cards
  startup/index.html    # Centered hero, balanced, shadow cards
  bold/index.html       # Fullscreen hero, compact, bordered cards
  index.html            # Side-by-side comparison
```

Then opens http://localhost:8080 for comparison. Tell Claude which variant you prefer (e.g., "use editorial") and it builds the React application.

### Variant Presets

Each preset applies design guidelines (60-30-10 color rule, visual hierarchy, rhythm):

| Preset | Style | Hero | Spacing | Cards |
|--------|-------|------|---------|-------|
| `minimal` | Ultra clean | Text only, no image | Extra generous | None |
| `editorial` | Magazine feel | Split 50/50, image left | Generous | Flat, no shadow |
| `startup` | SaaS modern | Centered, prominent CTA | Balanced | Soft shadows |
| `bold` | High impact | Fullscreen, text over image | Compact | Strong borders |

## Project Types

| Type | Example |
|------|---------|
| `landing` | Product page, lead capture |
| `website` | Corporate, blog, portfolio |
| `webapp` | Dashboard, SaaS, admin panel |
| `app` | iOS/Android, PWA |

## Usage

### Full Workflow

```bash
# 1. Extract copy from reference URL
/extract-copy https://example.com --type=landing

# 2. Extract design from images
/extract-design
# Then paste reference images

# 3. Build frontend
/build-frontend
```

### Minimal Workflow (design only)

```bash
# 1. Extract design from images (will ask for project description)
/extract-design
# Paste images, then provide brief description

# 2. Build frontend
/build-frontend
```

### Variants Workflow

```bash
# 1. Extract design (same as before)
/extract-design

# 2. Generate 4 HTML previews
/build-frontend --variants

# 3. Compare at http://localhost:8080

# 4. Tell Claude which variant you want
# "use editorial"

# 5. React application is built based on that layout
```

## Credits

Copy/design extraction workflow inspired by [Deborah Folloni's method](https://dfolloni.substack.com/p/os-prompts-que-eu-uso-para-fazer).

## License

MIT
