# Changelog

All notable changes to this plugin will be documented in this file.

## v1.2.1 (2025-12-15)

### Changed
- Remove Serena MCP to avoid duplication with spec-driven plugin
- Update documentation to reference spec-driven for LSP features

## v1.2.0 (2025-12-12)

### Changed
- Simplify agents to role-based style
- Remove hypothesis generation approach in favor of direct investigation
- Reduce total lines from 736 to 320 (56% reduction)

## v1.1.0 (2025-12-11)

### Added
- Serena MCP integration for semantic code analysis

## v1.0.0 (2025-12-11)

### Added
- Initial release
- `/debug` command for starting debugging sessions
- `bug-investigator` agent for code analysis and root cause detection
- `log-injector` agent for targeted debug log insertion
- Console Ninja MCP for runtime values
- Chrome DevTools MCP for browser inspection
- Debugging skill with framework-specific patterns
