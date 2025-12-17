# Changelog

All notable changes to this plugin will be documented in this file.

## v2.0.1 (2025-12-12)

### Changed
- Standardize plugin commands to pure markdown format
- Add explicit Arguments and Process sections for consistency

## v2.0.0 (2025-12-12)

### Added
- Design variations feature with editorial, startup, and bold presets
- `variations-builder` agent for generating multiple layout variations
- `/select-variation` command to choose preferred layout
- `/build-frontend --variations N` flag for comparison workflow
- `preview.html` template for side-by-side comparison

## v1.0.0 (2025-12-05)

### Added
- Initial release (renamed from design-to-code)
- `/extract-copy` command for extracting content from URLs
- `/extract-design` command for extracting design tokens from images
- `/build-frontend` command for generating frontend code
- `/generate-prompt` command for Replit/v0/Lovable/Figma prompts
- Agents: copy-extractor, design-extractor, frontend-builder, prompt-generator
- Frontend-design skill for auto-loaded contextual guidance

### Changed
- Rename from design-to-code to design-builder
- Standardize frontmatter across commands and agents
