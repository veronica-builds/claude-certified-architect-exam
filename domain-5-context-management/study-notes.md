# Domain 5: Context Management & Reliability (15%)

Smallest weighting. But mistakes here cascade everywhere.

## Progressive Summarisation Kills Transactional Data

Never summarise critical transactional data (amounts, dates, order numbers). It gets lost.

**Fix:** Maintain a persistent "case facts" block with extracted amounts, dates, order numbers. Never summarised. Included in every prompt.

## Primacy/Recency Effects

Models miss findings buried in long inputs. Place key summaries at the beginning of the context.

## Escalation Design

Three reliable escalation triggers:
1. Customer requests a human — honour immediately
2. Policy gaps — no applicable rule exists
3. Inability to progress — agent is stuck in a loop

Two UNRELIABLE triggers the exam will tempt you with:
1. Sentiment analysis — too noisy, false positives
2. Self-reported confidence scores — model may be overconfident

## Structured Error Context

When errors occur, provide structured context:
- Failure type (transient, validation, business, permission)
- What was attempted (specific query, parameters used)
- Partial results gathered before failure
- Potential alternative approaches

### Two Anti-Patterns
1. **Silent suppression:** returning empty results marked as success — prevents any recovery
2. **Workflow termination:** killing the entire pipeline on a single failure — disproportionate response

### Access Failure vs Valid Empty Result
- **Access failure:** tool could not reach data source. Consider retry.
- **Valid empty result:** tool reached source, found no matches. No retry needed.
- Confusing these two breaks recovery logic. The exam tests this.

## Coverage Annotations

Synthesis output should note which findings are well-supported vs which areas had limited sources. Example: "Section on geothermal energy is limited due to unavailable journal access"

## Codebase Exploration and Context Degradation

Extended sessions: model starts referencing "typical patterns" instead of specific code. Context fills with verbose discovery output and loses grip on earlier findings.

### Mitigation Strategies
- Use scratchpad files to persist key findings outside the conversation context
- Strategic compaction of earlier context
- Structured summaries at key checkpoints

## Customer Disambiguation

When multiple customers match a search query:
- Ask for additional identifiers (email, phone, order number)
- Do NOT select based on heuristics (most recent, most active)

## Temporal Awareness

- Require publication/data collection dates in structured outputs
- Different dates explain different numbers (not contradictions)

## Content-Appropriate Rendering

- Financial data: tables
- News: prose
- Technical findings: structured lists
- Do not flatten everything into one uniform format

## Getting Started

If you have no idea how to get started, go to Claude and paste the prompt from `prompts/domain-5-prompt.md`. It will turn Claude into an expert instructor that walks you through every concept in this domain interactively, highlights exam traps, and runs a 6-question practice exam at the end.

## Where to Learn This

- [Building Agents with the Claude Agent SDK](https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk) — context management, error propagation, and escalation design
- [Agent SDK session docs](https://platform.claude.com/docs/en/agent-sdk/overview) — battle-tested context management patterns, scratchpad files, and strategic compaction
- [Everything Claude Code repo](https://github.com/affaan-m/everything-claude-code) — practical patterns
