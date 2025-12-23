# Design Builder

Claude Code plugin that extracts copy and design from references to build frontend components.

## Architecture

```
design-builder/
├── .claude-plugin/
│   └── plugin.json                 # Plugin manifest
├── agents/                         # Specialized subagents
│   ├── copy-extractor.md           # Content Strategist
│   ├── design-extractor.md         # Creative Director
│   ├── frontend-builder.md         # Frontend Engineer (React)
│   └── variants-builder.md         # Variants Engineer (HTML+CSS)
├── commands/                       # Slash commands
│   ├── extract-copy.md
│   ├── extract-design.md
│   └── build-frontend.md
├── skills/                         # Auto-loaded guidance
│   └── frontend-design/SKILL.md
└── docs/                           # Output directory
    ├── copy.yaml
    └── design.json
```

## Workflows

Two entry points:

```
# Full: Start from URL reference
URL -> /extract-copy -> copy.yaml -> /extract-design -> design.json

# Minimal: Start from design image only (with brief project description)
Image -> /extract-design -> design.json

# Then build:
-> /build-frontend              # React direto
-> /build-frontend --variants   # 4 previews HTML -> escolha -> React
```

### Design Variants

Generate 4 HTML+CSS previews to compare before building React:

```
/build-frontend --variants
    |
    v
Generates ./outputs/
  minimal/index.html    # Text hero, extra whitespace, no cards
  editorial/index.html  # Split hero, generous spacing, flat cards
  startup/index.html    # Centered hero, balanced, shadow cards
  bold/index.html       # Fullscreen hero, compact, bordered cards
  index.html            # Side-by-side comparison
    |
    v
npx http-server ./outputs -o -p 8080
    |
    v
User: "use editorial"
    |
    v
frontend-builder creates React based on editorial layout
```

## Commands

| Command | Description |
|---------|-------------|
| `/extract-copy` | Extract content from URL to copy.yaml (optional) |
| `/extract-design` | Extract design from images to design.json |
| `/build-frontend` | Build React directly |
| `/build-frontend --variants` | Generate 4 HTML previews, then build React from chosen variant |

## Agents

| Agent | Role |
|-------|------|
| `copy-extractor` | Content Strategist |
| `design-extractor` | Creative Director |
| `frontend-builder` | Frontend Engineer - builds React (from variant or direct) |
| `variants-builder` | Variants Engineer - generates 4 HTML+CSS previews |

Agents can be invoked directly: "Use the design-extractor agent to analyze this image"

## Variant Presets

Each preset applies design guidelines (60-30-10, visual hierarchy, rhythm):

| Preset | Style | Hero | Spacing | Cards |
|--------|-------|------|---------|-------|
| `minimal` | Ultra clean | Text only | Extra generous | None |
| `editorial` | Magazine feel | Split 50/50 | Generous | Flat |
| `startup` | SaaS modern | Centered CTA | Balanced | Shadows |
| `bold` | High impact | Fullscreen | Compact | Bordered |

## Skills

| Skill | Description |
|-------|-------------|
| `frontend-design` | Design principles auto-loaded for frontend tasks (avoids AI slop aesthetics) |

The frontend-builder and variants-builder agents MUST apply the frontend-design skill.

## Project Types

| Type | Description | Example |
|------|-------------|---------|
| `landing` | Single-page landing | Product page, lead capture |
| `website` | Multi-page site | Corporate, blog, portfolio |
| `webapp` | Interactive application | Dashboard, SaaS, admin panel |
| `app` | Mobile application | iOS/Android, PWA |

## Output Formats

### copy.yaml
- `landing/website`: sections with hero, features, cta, footer
- `webapp`: screens with widgets, auth, sidebar navigation
- `app`: screens, onboarding, bottom-tabs, gestures, native features

### design.json
```json
{
  "meta": { "name", "version", "project_type" },
  "principles": { "overall", "keywords", "avoid" },
  "colors": { "primary", "accent", "neutral", "semantic" },
  "typography": { "fonts", "scale", "emphasis" },
  "spacing": { "section", "container", "grid", "component" },
  "components": { "button", "card", "badge", "input", "icon" },
  "effects": { "shadows", "transitions" },
  "animations": { "fadeInUp", "hoverLift", "stagger" },
  "backgrounds": { "patterns", "gradients", "sections" }
}
```

## References

- Workflow based on Deborah Folloni's method (DebGPT)
- [Original post](https://dfolloni.substack.com/p/os-prompts-que-eu-uso-para-fazer)
