# Claude Certified Architect — Study Guide

Based on the breakdown by [@hooeem](https://x.com/hooeem/status/2033198345045336559) who tore apart the official exam guide and distilled it into actionable learnings.

## Exam Overview

The Claude Certified Architect exam tests your ability to build production-grade applications using Claude Code, Claude Agent SDK, Claude API, and Model Context Protocol (MCP).

- **Format:** Scenario-based multiple choice (one correct answer, three plausible distractors)
- **Passing score:** 720/1000
- **Prerequisite:** Must be a Claude (Anthropic) partner to take the actual exam — but the knowledge is what matters for building real applications.

## Five Exam Domains

| Domain | Topic | Weight |
|--------|-------|--------|
| 1 | Agentic Architecture & Orchestration | 27% |
| 2 | Tool Design & MCP Integration | 18% |
| 3 | Claude Code Configuration & Workflows | 20% |
| 4 | Prompt Engineering & Structured Output | 20% |
| 5 | Context Management & Reliability | 15% |

## How to Get Started

If you have no idea where to begin, each domain folder contains a teaching prompt (e.g. `domain-1-prompt.md`). Open a new Claude conversation, paste the entire contents of the prompt, and Claude will become an expert instructor — walking you through every concept, highlighting exam traps, and running a practice exam at the end.

## Folder Structure

Each domain folder contains a `study-notes.md` (key concepts and exam tips) and a `domain-X-prompt.md` (interactive teaching prompt to paste into Claude).

```
├── domain-1-agentic-architecture/    # 27% — The biggest domain
├── domain-2-tool-design-mcp/         # 18% — Tool descriptions & MCP
├── domain-3-claude-code-config/      # 20% — Configuration & workflows
├── domain-4-prompt-engineering/      # 20% — Prompts & structured output
├── domain-5-context-management/      # 15% — Context & reliability
└── resources/                        # Recommended learning links
```

## What You Should Build (per domain)

1. **Domain 1:** A multi-tool agent with 3-4 MCP tools, proper stop_reason handling, a PostToolUse hook normalising data formats, and a tool call interception hook blocking policy violations.
2. **Domain 2:** Two MCP tools with intentionally similar functionality. Write descriptions vague enough to cause misrouting. Then fix them. Experience the difference.
3. **Domain 3:** A project with CLAUDE.md hierarchy, .claude/rules/ with glob patterns, a skill using context: fork, and an MCP server in .mcp.json with env var expansion. Test plan mode on a multi-file refactor and direct execution on a single bug fix.
4. **Domain 4:** An extraction pipeline using tool_use with required, optional, and nullable fields. Add a validation-retry loop. Run a batch through the Batches API. Handle failures by custom_id.
5. **Domain 5:** A coordinator with two subagents. Simulate a timeout. Verify the coordinator gets structured error context and proceeds with partial results. Test with conflicting sources.

## Exam Scenarios to Expect

The exam tests knowledge through these recurring real-world scenarios:

- Customer Support Resolution Agent (Agent SDK + MCP + escalation)
- Code Generation with Claude Code (CLAUDE.md + plan mode + slash commands)
- Multi-Agent Research System (coordinator-subagent orchestration)
- Developer Productivity Tools (built-in tools + MCP servers)
- Claude Code for CI/CD (non-interactive pipelines + structured output)
- Structured Data Extraction (JSON schemas + tool_use + validation loops)
