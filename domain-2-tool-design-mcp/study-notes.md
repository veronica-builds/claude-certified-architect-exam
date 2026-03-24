# Domain 2: Tool Design & MCP Integration (18%)

## The Overlooked Key: Tool Descriptions

Tool descriptions are the primary mechanism Claude uses for tool selection. If yours are vague or overlapping, selection becomes unreliable. The exam heavily tests this.

### Tool Description Best Practices
- Each tool must have a unique, specific description
- Describe WHEN to use it (not just what it does)
- Avoid overlapping descriptions between tools
- Include edge cases and constraints

## tool_choice — Know These Cold

- `"auto"`: model decides whether to call a tool or return text. Default. Use for most cases.
- `"any"`: model MUST call a tool but chooses which one. Use when you need guaranteed tool execution.
- `{"type": "tool", "name": "extract_metadata"}`: model MUST call this specific tool. Use for forced extraction pipelines.

## Tool Overload Problem

Giving an agent 18 tools degrades selection reliability.

**Solution:** Scope each subagent to 4-5 tools relevant to its role.
- A synthesis agent should NOT have web search tools
- A web search agent should NOT have code execution tools
- The exam tests this exact pattern

### Scoped Cross-Role Tools
- For high-frequency simple operations, give a constrained tool directly to the subagent
- Example: synthesis agent gets a scoped `verify_fact` tool for simple lookups, avoiding coordinator round-trips
- This avoids coordinator round-trip latency for the 85% of cases that are simple
- The exam's Q9 tests this exact pattern

## Glob vs Grep — Know the Difference

- **Glob:** matches file PATHS by naming patterns. Use for finding files by extension (`*.test.tsx`), locating configuration files.
- **Grep:** searches file CONTENTS by regex. Use for finding function definitions, error messages, configuration values.

The exam tests whether you can choose the right tool for the right task.

## MCP Integration

### Server Configuration
- MCP servers are configured in `.mcp.json` at project level or user-level config
- Environment variable expansion is supported in config
- Understand project vs user config scoping

### Error Handling for Tools
- Teach structured error metadata: `errorCategory`, `isRetryable` boolean, human-readable messages
- Critical distinction:
  - **Access failure:** the tool could not reach the data source (timeout, auth failure). Consider retry.
  - **Valid empty result:** the tool successfully queried the source and found no matches. No retry needed.
  - Confusing these two breaks recovery logic. The exam tests this.

### Error Propagation in Multi-Agent Systems
- Subagents implement local recovery for transient failures
- Only propagate errors they cannot resolve locally
- Include partial results and what was attempted when propagating

## Getting Started

If you have no idea how to get started, go to Claude and paste the prompt from `prompts/domain-2-prompt.md`. It will turn Claude into an expert instructor that walks you through every concept in this domain interactively, highlights exam traps, and runs an 8-question practice exam at the end.

## Where to Learn This

- [MCP Integration for Claude Code](https://code.claude.com/docs/en/mcp) — server scoping, environment variable expansion, project vs user config
- [MCP specification and community servers](https://github.com/modelcontextprotocol) — understanding the protocol and knowing when to use community servers vs custom builds
- [Claude Agent SDK TypeScript repo](https://www.npmjs.com/package/@anthropic-ai/claude-agent-sdk) — tool definition patterns and structured error responses
