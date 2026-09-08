# Quick Reference

> **Use this page during active coding.** If you only remember one thing: **high signal, low waste, verified outcome.**

## 60-second checklist

### Before asking the agent

- [ ] What exact outcome do I want?
- [ ] What files/components are likely involved?
- [ ] What constraints must not change?
- [ ] What does "done" mean?
- [ ] Is this small enough to implement directly?

### In the prompt

Use:

```text
Goal:
Context:
Constraints:
Acceptance criteria:
Verification:
```

Example:

```text
Goal:
Fix login timeout when an access token expires.

Context:
The refresh-token flow already exists in AuthService.

Constraints:
- Reuse the existing refresh flow.
- Do not change the public API.
- Do not modify unrelated authentication behavior.

Acceptance criteria:
- Expired access token + valid refresh token => refresh + retry once.
- Invalid refresh token => normal authentication failure.
- No infinite retry loop.

Verification:
Add/update focused unit tests for both cases.
```

## Context rule

### Give

- Relevant files
- Relevant symbols
- Existing patterns
- Constraints
- Acceptance criteria
- Relevant errors/logs

### Avoid

- Whole repository dumps
- Unrelated files
- Duplicate explanations
- Huge generated files
- Full logs when only one error matters
- Documentation unrelated to the decision

## Context escalation ladder

```text
Level 1  Task + known file
   ↓ if insufficient
Level 2  Relevant file/module
   ↓ if insufficient
Level 3  Related implementation + tests
   ↓ if insufficient
Level 4  Architecture / dependency context
   ↓ only if needed
Level 5  Wider repository exploration
```

Do not start at Level 5 by default.

## Tool-output rule

Ask tools for **decision-ready output**.

Bad:

```text
Show me all logs.
```

Better:

```text
Find the first occurrence of the timeout and show the
surrounding error plus the relevant request ID.
```

## Complexity rule

| Task | Default approach |
|---|---|
| Rename one symbol | Direct edit |
| Small bug | Direct implementation + focused test |
| New endpoint | Inspect pattern → implement → test |
| Multi-file feature | Plan first |
| Large refactor | Plan + staged implementation |
| Broad investigation | Research/analysis first |
| Independent verbose investigation | Consider subagent |

## Verification rule

Prefer:

```text
small change
→ targeted test
→ inspect diff
→ broader test if needed
```

Not:

```text
huge change
→ hope
→ run everything
→ discover problems
→ redo
```

## Stop conditions

Stop the agent when:

- Acceptance criteria are satisfied.
- Tests pass at the required scope.
- The diff is understood.
- No requested work remains.

## Drift recovery

```text
Stop. Stay within <scope>.
The goal is <goal>.
Do not modify <excluded areas>.
Continue from the current state and verify <criteria>.
```

If context is polluted by unrelated work, start a fresh session with a short handoff.

## Persistent instructions

Put stable, recurring facts in the tool's instruction mechanism:

- architecture conventions
- build/test commands
- coding standards
- important boundaries
- repository-specific workflows

Do **not** put every task instruction there.

## Final 5 questions

1. Did it solve the requested problem?
2. Did it change only what was necessary?
3. Did it follow existing project patterns?
4. Is there targeted verification?
5. Can I explain the resulting diff?
