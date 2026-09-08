# Cursor

## Rules

Use Cursor Rules for stable, reusable instructions: architecture conventions, coding patterns, repository constraints, and test commands. Keep rules focused.

Official docs: https://prod.cursor.com/docs/rules

## Scoped rules

Prefer instructions that apply only where relevant:

```text
Frontend rule → src/frontend/**
Backend rule  → src/backend/**
Tests rule    → tests/**
```

## Plan Mode

Use planning for multi-file features, complex refactors, architectural changes, and unfamiliar systems. Skip elaborate planning for trivial edits.

Official docs: https://prod.cursor.com/docs/agent/plan-mode

## Ignore unnecessary content

Use `.cursorignore` where appropriate for generated output, build artifacts, large datasets, dependency directories, and temporary files. Note that ignoring files for Cursor agent/editor features does not necessarily block terminal or MCP access.

Official docs: https://prod.cursor.com/docs/reference/ignore-file

## Checklist

- [ ] Are rules scoped?
- [ ] Are rules concise?
- [ ] Is Plan Mode justified?
- [ ] Are irrelevant files excluded where appropriate?
- [ ] Did the agent stay within scope?
- [ ] Did I verify the result?
