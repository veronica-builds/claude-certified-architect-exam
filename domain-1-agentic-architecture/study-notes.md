# Domain 1: Agentic Architecture & Orchestration (27%)

This is the single most important domain — over a quarter of the total exam score.

## Three Anti-Patterns to Reject on Sight

The exam tests these three anti-patterns you must reject immediately:

1. **Parsing natural language to determine loop termination** — Never check assistant text to decide if the agent is done.
2. **Arbitrary iteration caps as the primary stopping mechanism** — Don't rely on "max 10 loops" as your main stop condition.
3. **Checking for assistant text as a completion indicator** — The model can return text AND still need to call tools.

**The correct approach:** Inspect the `stop_reason` field in the API response.
- If `stop_reason` is `"tool_use"`: execute the requested tool(s), append the tool results, and continue the loop.
- If `stop_reason` is `"end_turn"`: the agent has finished; present the final response.
- Tool results must be appended to conversation history so the model can reason about them.

## The Single Biggest Mistake

People assume subagents share memory with the coordinator. **They do not.** Subagents operate with isolated context. Every piece of information must be passed explicitly in the prompt.

Key isolation principles:
- Subagents do NOT automatically inherit the coordinator's conversation history
- Subagents do NOT share memory between invocations
- Every piece of information a subagent needs must be explicitly included in its prompt
- This is the single most commonly misunderstood concept in multi-agent systems

## The Rule That Will Save the Most Marks

When stakes are financial or security-critical, prompt instructions alone are not enough. You must be enforcing tool ordering programmatically with hooks and prerequisite gates.

## Multi-Agent Orchestration (Hub-and-Spoke)

- A **coordinator agent** sits at the centre
- **Subagents** are spokes that the coordinator invokes for specialised tasks
- ALL communication flows through the coordinator — subagents never communicate directly with each other
- The coordinator handles: task decomposition, deciding which subagents to invoke, passing context, aggregating results, error handling, and routing information

### Coordinator Responsibilities
- Analyse query requirements and dynamically select which subagents to invoke
- Partition research scope across subagents to minimise duplication
- Implement iterative refinement loops: evaluate synthesis output for gaps, re-invoke subagents for targeted follow-up
- Route all communication through coordinator for observability and consistency

### Subagent Invocation and Context Passing
- Use the **Task tool** to spawn subagents from a coordinator
- The coordinator's `allowedTools` must include "Task" or it cannot spawn subagents
- Each subagent has an `AgentDefinition` with description, system prompt, and tools
- Include complete findings from prior agents directly in the subagent's prompt
- Use structured data formats that separate content from metadata (source URLs, confidence, timestamps)
- Design coordinator prompts that specify research goals and quality criteria, NOT step-by-step procedural instructions

### Parallel Spawning
- Emit multiple Task tool calls in a single coordinator response to spawn subagents in parallel
- Faster than sequential invocation across separate turns
- The exam tests latency awareness

### fork_session
- Creates independent branches from a shared analysis baseline
- Use for exploring divergent approaches (e.g., comparing two testing strategies from the same codebase analysis)
- Each fork operates independently after the branching point

## Workflow Enforcement and Handoff Design

### Hooks
- **PreToolCall hooks:** intercept before execution (block policy violations, add compliance checks)
- **PostToolCall hooks:** intercept after execution (normalise data formats, validate outputs)
- Hooks are deterministic — they enforce rules programmatically, not via prompt instructions

### Escalation Design
Three reliable escalation triggers:
1. Customer requests a human (honour immediately)
2. Policy gaps
3. Inability to progress

Two UNRELIABLE triggers the exam will tempt you with:
1. Sentiment analysis
2. Self-reported confidence scores

## Decomposition Strategies

### Static decomposition
- Best for: predictable, structured tasks like code reviews, document processing
- Advantage: consistent and reliable
- Limitation: cannot adapt to unexpected findings

### Dynamic adaptive decomposition
- Generate subtasks based on what is discovered at each step
- Best for: open-ended investigation tasks
- Advantage: adapts to the problem
- Limitation: less predictable

### Attention Dilution Problem
- Processing too many files in a single pass produces inconsistent depth
- Fix: split large reviews into per-file local analysis passes PLUS a separate cross-file integration pass

### Narrow Decomposition Failure
- The exam has a specific question (Q7 in sample set) where a coordinator decomposes poorly
- The root cause is the coordinator's decomposition, not any downstream agent
- The exam expects students to trace failures to their origin

## Getting Started

If you have no idea how to get started, go to Claude and paste the prompt from `prompts/domain-1-prompt.md`. It will turn Claude into an expert instructor that walks you through every concept in this domain interactively, highlights exam traps, and runs a 10-question practice exam at the end.

## Where to Learn This

- [Agent SDK Overview](https://platform.claude.com/docs/en/agent-sdk/overview) — agentic loop mechanics and subagent patterns
- [Building Agents with the Claude Agent SDK](https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk) — Anthropic's best practices on hooks, orchestration, and sessions
- [Agent SDK Python repo + examples](https://github.com/anthropics/claude-agent-sdk-python) — hands-on code: hooks, custom tools, fork_session
