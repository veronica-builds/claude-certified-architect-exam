# Domain 3: Claude Code Configuration & Workflows (20%)

This separates people who use Claude Code from people who have configured it for a team.

## CLAUDE.md Hierarchy — Three Levels

1. **User-level:** `~/.claude/CLAUDE.md` — personal preferences, NOT shared, NOT version-controlled
2. **Project-level:** `.claude/CLAUDE.md` — team-wide conventions, version-controlled
3. **Directory-level:** subdirectory `CLAUDE.md` files — scoped to that directory

### The Exam's Favourite Trap
A team member missing instructions because they live in user-level config (not version-controlled, not shared). Always put team conventions in project-level config.

## Path-Specific Rules — The Sleeper Concept

`.claude/rules/` with YAML frontmatter glob patterns like `**/*.test.tsx` applies conventions across the entire codebase.

Directory-level `CLAUDE.md` cannot do this because it is directory-bound. Rules files with glob patterns are the correct approach for codebase-wide conventions.

Example: `**/*.test.tsx` catches every test file regardless of directory.

## Plan Mode vs Direct Execution

### Use Plan Mode for:
- Monolith restructuring
- Multi-file migration
- Architectural decisions
- Any task requiring exploration before action

### Use Direct Execution for:
- Single-file bug fix
- One validation check
- Clear, well-defined scope

## Context Management in Skills

- `context: fork` in skill frontmatter — creates an isolated context for the skill execution
- Know when to fork vs when to keep shared context
- Skills can define their own tools and constraints

## MCP Server Configuration in Projects

- `.mcp.json` at project root configures MCP servers
- Environment variable expansion (`$ENV_VAR`) is supported
- Project-level config is shared with the team via version control
- User-level config is personal only

## CI/CD Integration

- Claude Code supports non-interactive mode for CI/CD pipelines
- Structured output mode for machine-readable results
- Use `--print` flag for non-interactive execution
- Understand which flags are relevant for automation vs interactive use

## Slash Commands and Skills

- Slash commands provide quick access to common operations
- Skills are reusable configurations that can be shared
- Understanding the skill system is part of the exam

## Getting Started

If you have no idea how to get started, go to Claude and paste the prompt from `prompts/domain-3-prompt.md`. It will turn Claude into an expert instructor that walks you through every concept in this domain interactively, highlights exam traps, and runs an 8-question practice exam at the end.

## Where to Learn This

- [Claude Code official docs](https://code.claude.com/docs/en/mcp) — commands, skills, hooks, and CI/CD flags
- [Claude Code CLI Cheatsheet](https://shipyard.build/blog/claude-code-cheat-sheet/) — practical reference for all commands
- [Creating the Perfect CLAUDE.md](https://dometrain.com/blog/creating-the-perfect-claudemd-for-claude-code/) — real team configuration patterns and MCP integration
