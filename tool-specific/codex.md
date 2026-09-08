# Codex

## Repository instructions

Use repository instruction files such as `AGENTS.md` for stable project guidance: build/test commands, repository structure, conventions, constraints, and canonical workflows. Avoid task-specific instructions in persistent files.

Official Codex agent-loop discussion: https://openai.com/index/unrolling-the-codex-agent-loop/

## Context growth

Conversations accumulate history, tool results, generated output, and instructions. Keep sessions task-focused, avoid repeated output, summarize state for handoffs, and start fresh when old context becomes irrelevant.

## Reasoning effort

Match model/effort to task complexity:

```text
Small deterministic task → lower effort
Moderate implementation → medium effort
Complex architecture/debugging → higher effort
```

Current model/effort documentation: https://developers.openai.com/api/docs/models/gpt-5.3-codex

## Checklist

- [ ] Is `AGENTS.md` concise and useful?
- [ ] Is the task clearly scoped?
- [ ] Is the session polluted by unrelated work?
- [ ] Is reasoning effort proportional to complexity?
- [ ] Are tools being used for deterministic discovery/checks?
- [ ] Is verification explicit?
