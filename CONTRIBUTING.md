# Maintaining This Playbook

## When to add a rule

Add a rule when:

1. the same failure occurs repeatedly,
2. the cause is reasonably understood,
3. the rule is broadly reusable,
4. the context cost is justified.

Do not add rules for isolated mistakes.

## Rule-card format

```text
## Rule: <short name>

### When to use
<scenario>

### What to do
<recommended behavior>

### Bad
<bad example>

### Better
<better example>

### Why
<short explanation>

### Tool notes
<tool-specific differences, if any>
```

## Review checklist

- [ ] Is the rule actionable?
- [ ] Is it generic enough to reuse?
- [ ] Does it avoid tool-specific assumptions unless intentionally scoped?
- [ ] Does it reduce waste without reducing correctness?
- [ ] Is there a concrete example?
- [ ] Is the wording concise?
- [ ] Are links still valid?
- [ ] Is duplicate guidance removed?

## Ownership model

- Engineering enablement/platform team owns the structure.
- Developers contribute recurring failure patterns.
- Tool-specific pages are reviewed when tools materially change.
- Repository-specific instructions remain in the repository's normal agent instruction files.
