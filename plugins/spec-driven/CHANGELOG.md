# Changelog

All notable changes to this plugin will be documented in this file.

## v1.2.0 (2025-12-19)

### Added
- Context Flow system for consistent context passing between phases
- Critical Files section in plan.md (Reference, Modify, Create)
- Artifacts section in tasks.md with references to all spec artifacts
- Acceptance Criteria validation in /implement and /review
- Architecture compliance validation in /review
- Reference file loading for implement-agent (patterns to follow)

### Changed
- code-architect now receives and outputs consolidated Critical Files
- implement-agent receives spec.md, research.md, and reference file contents
- code-reviewer validates against acceptance criteria and architectural decisions
- task-generator includes file refs only for complex tasks

## v1.1.0 (2025-12-15)

### Added
- Web-researcher agent for external research when specs mention external technologies
- Serena MCP integration for semantic code analysis

### Changed
- Standardize plugin commands to pure markdown format
- Disable Serena web UI auto-open
- Add color attribute to agent frontmatter

## v1.0.0 (2025-12-05)

### Added
- Initial release
- `/spec` command for creating feature specifications
- `/clarify` command for resolving ambiguities
- `/plan` command for generating technical plans
- `/tasks` command for task decomposition
- `/implement` command for executing tasks
- `/review` command for code review
- Agents: code-explorer, code-architect, code-reviewer, implement-agent, task-generator
