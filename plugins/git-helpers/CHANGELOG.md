# Changelog

All notable changes to this plugin will be documented in this file.

## v1.1.1 (2025-12-14)

### Fixed
- Support uncommitted changes in code-review command
- Remove command substitution that caused permission errors
- Add detection for staged and unstaged changes when on main branch

## v1.1.0 (2025-12-11)

### Changed
- Enhance `/details` command with comprehensive PR template
- Add file categorization and structured analysis sections
- Include Technical Flow, Impact Assessment, Priority Review Areas
- Add pre-execution validation for branch checks

## v1.0.0 (2025-12-02)

### Added
- Initial release
- `/code-review` command for analyzing code changes
- `/commit` command for creating well-formatted commits
- `/details` command for generating PR descriptions
- `/create-pr` command for creating pull requests
- `code-reviewer` agent for quality analysis
