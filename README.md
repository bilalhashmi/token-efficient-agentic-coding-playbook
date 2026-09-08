# Token-Efficient Agentic Coding Playbook

> **Purpose:** Help developers get high-quality results from AI coding agents while using the minimum practical context, tool calls, and model effort.

**Canonical format:** Markdown. Keep this folder in the engineering repository so developers and coding agents can use the same guidance.

## Start here

| Situation | Go to |
|---|---|
| I need the rules while coding | [Quick Reference](quick-reference.md) |
| I don't know how to prompt the agent | [Prompt Patterns](prompt-patterns.md) |
| The agent is reading too much | [Context Management](context-management.md) |
| The agent keeps making mistakes | [Verification](verification.md) |
| I am starting a bug fix | [Examples](examples.md#1-bug-fix) |
| I am adding an API | [Examples](examples.md#2-rest-api-endpoint) |
| I am doing a large change | [Examples](examples.md#3-multi-file-feature) |
| I need tool-specific advice | [Tool-Specific Guidance](#tool-specific-guidance) |
| The agent is drifting | [Anti-Patterns](anti-patterns.md) |
| I want the reasoning behind the rules | [Fundamentals](fundamentals.md) |

## The core rule

> **Give the agent enough information to make the next correct decision — not enough information to reconstruct the entire universe.**

Optimize for **signal, not brevity**.

## The playbook in one workflow

```text
Define outcome
     ↓
Give focused context
     ↓
Ask for a plan when complexity warrants it
     ↓
Let the agent inspect only what it needs
     ↓
Implement the smallest coherent change
     ↓
Run targeted verification
     ↓
Review the diff
     ↓
Stop / hand off when done
```

## Five operating principles

1. **Be specific, not artificially short.**
2. **Provide relevant context progressively.**
3. **Prefer deterministic tools for deterministic work.**
4. **Keep tool output small and decision-ready.**
5. **Verify continuously and stop when the task is complete.**

## Tool-specific guidance

- [Claude Code](tool-specific/claude-code.md)
- [Codex](tool-specific/codex.md)
- [Cursor](tool-specific/cursor.md)
- [Augment](tool-specific/augment.md)

Tool guidance should supplement this playbook, not replace the core principles.

## Team adoption

Recommended repository location:

```text
/docs/playbooks/agentic-coding/
```

Recommended minimum files:

```text
README.md
quick-reference.md
fundamentals.md
prompt-patterns.md
context-management.md
verification.md
anti-patterns.md
examples.md
tool-specific/
```

### Keep the playbook healthy

- Prefer rules that solve recurring problems.
- Remove obsolete or duplicated rules.
- Keep persistent agent instructions short and high-signal.
- Put detailed explanations in reference pages rather than always-loaded instructions.
- Add a new rule only when there is a repeatable failure mode.
- Review tool-specific guidance when the tool changes materially.

## Success metric

Do not measure token efficiency as "fewest tokens."

Measure:

> **Useful outcome / total context + tool/model effort**

The best workflow is usually the one that reaches the correct verified result with the least unnecessary work.

## Further reading

- Claude Code cost optimization: https://code.claude.com/docs/en/costs
- Claude Code memory: https://code.claude.com/docs/en/memory
- Claude Code subagents: https://code.claude.com/docs/en/subagents
- Claude Code prompt caching: https://code.claude.com/docs/en/prompt-caching
- OpenAI Codex agent loop: https://openai.com/index/unrolling-the-codex-agent-loop/
- GPT-5.3-Codex: https://developers.openai.com/api/docs/models/gpt-5.3-codex
- Cursor Rules: https://prod.cursor.com/docs/rules
- Cursor Plan Mode: https://prod.cursor.com/docs/agent/plan-mode
- Cursor ignore files: https://prod.cursor.com/docs/reference/ignore-file
- Augment Guidelines: https://docs.augmentcode.com/setup-augment/guidelines
- Augment CLI Rules: https://docs.augmentcode.com/cli/rules
