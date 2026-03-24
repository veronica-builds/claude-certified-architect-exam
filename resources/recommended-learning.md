# Recommended Learning Resources

## Official Anthropic Courses (Skilljar)

1. [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api)
2. [Introduction to Model Context Protocol](https://anthropic.skilljar.com/introduction-to-model-context-protocol)
3. [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action)
4. [Claude 101](https://anthropic.skilljar.com/claude-101)

## Domain 1: Agentic Architecture & Orchestration (27%)

- [Agent SDK Overview](https://platform.claude.com/docs/en/agent-sdk/overview) — agentic loop mechanics and subagent patterns
- [Building Agents with the Claude Agent SDK](https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk) — Anthropic's own best practices on hooks, orchestration, and sessions
- [Agent SDK Python repo + examples](https://github.com/anthropics/claude-agent-sdk-python) — hands-on code: hooks, custom tools, fork_session

## Domain 2: Tool Design & MCP Integration (18%)

- [MCP Integration for Claude Code](https://code.claude.com/docs/en/mcp) — server scoping, environment variable expansion, project vs user config
- [MCP specification and community servers](https://github.com/modelcontextprotocol) — understanding the protocol and when to use community servers vs custom builds
- [Claude Agent SDK TypeScript repo](https://www.npmjs.com/package/@anthropic-ai/claude-agent-sdk) — tool definition patterns and structured error responses

## Domain 3: Claude Code Configuration & Workflows (20%)

- [Claude Code official docs](https://code.claude.com/docs/en/mcp) — commands, skills, hooks, and CI/CD flags
- [Claude Code CLI Cheatsheet](https://shipyard.build/blog/claude-code-cheat-sheet/) — practical reference
- [Creating the Perfect CLAUDE.md](https://dometrain.com/blog/creating-the-perfect-claudemd-for-claude-code/) — real team configuration patterns and MCP integration

## Domain 4: Prompt Engineering & Structured Output (20%)

- [Anthropic Prompt Engineering docs](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview) — few-shot patterns, explicit criteria, and structured output
- [Anthropic API Tool Use documentation](https://platform.claude.com/docs/en/release-notes/overview) — tool_use, tool_choice config, JSON schema enforcement

## Domain 5: Context Management & Reliability (15%)

- [Building Agents with the Claude Agent SDK](https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk) — context management, error propagation, and escalation design
- [Agent SDK session docs](https://platform.claude.com/docs/en/agent-sdk/overview) — context management patterns, scratchpad files, strategic compaction
- [Everything Claude Code repo](https://github.com/affaan-m/everything-claude-code) — practical community patterns

## Source

All content distilled from [@hooeem's article](https://x.com/hooeem/status/2033198345045336559) — "I want to become a Claude architect (full course)"
