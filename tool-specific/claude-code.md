# Claude Code

This page contains Claude Code-specific practices. The core playbook remains tool-independent.

## Persistent instructions

Use `CLAUDE.md` for stable repository/project instructions: build/test commands, architecture conventions, important boundaries, generated-file rules, and recurring workflows. Keep it concise and high-signal.

Official docs: https://code.claude.com/docs/en/memory

## Context control

Useful concepts include `/compact`, `/clear`, and `/context`. Use a fresh context when old work no longer helps the current task.

Official cost guidance: https://code.claude.com/docs/en/costs

## Subagents

Use subagents for independent, potentially verbose side work when isolation is useful. Ask for concise, decision-ready results rather than dumping all findings into the main session.

Official docs: https://code.claude.com/docs/en/subagents

## Prompt caching

Where caching applies, stable context prefixes can be valuable. Keep stable instructions stable and avoid unnecessary context churn.

Official docs: https://code.claude.com/docs/en/prompt-caching

## Checklist

- [ ] Is `CLAUDE.md` concise?
- [ ] Is this unrelated to the previous task?
- [ ] Would `/clear` be cleaner?
- [ ] Is context getting noisy?
- [ ] Would `/compact` help?
- [ ] Is a subagent useful for an independent verbose task?
- [ ] Did I run focused verification?
