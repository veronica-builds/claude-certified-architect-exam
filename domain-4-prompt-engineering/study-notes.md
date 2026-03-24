# Domain 4: Prompt Engineering & Structured Output (20%)

## The Two Words That Save You: "Explicit Criteria"

- "Be conservative" does NOT improve precision.
- "Only report high-confidence findings" does NOT reduce false positives.

What works: **defining exactly which issues to report versus skip, with concrete code examples for each severity level.**

## Few-Shot Examples — Highest Leverage Technique

Few-shot examples are the highest-leverage technique tested in this domain.

Best practice: 2-4 targeted examples showing ambiguous-case handling with reasoning for why one action was chosen over alternatives. This teaches the model your decision boundary.

## tool_use with JSON Schemas

`tool_use` with JSON schemas eliminates syntax errors. But NOT semantic errors.

### Schema Design Principles
- **Nullable fields** when source data might be absent — prevents fabricated values
- **"unclear" enum values** — gives the model a valid escape hatch instead of forcing a guess
- **"other" + detail strings** — for categories that don't fit predefined options
- Required vs optional field distinction matters for data quality

## Batches API

Key facts:
- ~50% cost savings
- Up to 24-hour processing window
- No guaranteed latency SLA
- Does NOT support multi-turn tool calling within a single request
- Uses `custom_id` for correlating request/response pairs

### When to Use Which
- **Synchronous API:** blocking workflows (pre-merge checks, anything developers wait for)
- **Batch API:** latency-tolerant workflows (overnight reports, weekly audits, nightly data processing)

### Batch Failure Handling
- Identify failed documents by `custom_id`
- Resubmit only failures with modifications (e.g., chunking oversized documents)
- Refine prompts on a sample set BEFORE batch processing to maximise first-pass success

## Multi-Instance Review

The self-review limitation:
- A model reviewing its own output in the same session retains reasoning context
- It is less likely to question its own decisions
- An independent instance without prior context catches more subtle issues

### Multi-Pass Architecture
- Per-file local analysis passes: consistent depth per file
- Separate cross-file integration pass: catches data flow issues across files
- Prevents attention dilution and contradictory findings

### Confidence-Based Routing
- Model self-reports confidence per finding
- Route low-confidence findings to human review
- Calibrate confidence thresholds using labelled validation sets

## Sample Questions Are Your Best Study Material

The exam guide's own sample questions (Q10, Q11, Q12) are the single best study material for this domain. Work through every distractor and understand why it is wrong.

## Getting Started

If you have no idea how to get started, go to Claude and paste the prompt from `prompts/domain-4-prompt.md`. It will turn Claude into an expert instructor that walks you through every concept in this domain interactively, highlights exam traps, and runs an 8-question practice exam at the end.

## Where to Learn This

- [Anthropic Prompt Engineering docs](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview) — few-shot patterns, explicit criteria, and structured output
- [Anthropic API Tool Use documentation](https://platform.claude.com/docs/en/release-notes/overview) — tool_use, tool_choice config, JSON schema enforcement
