# Anti-Patterns

## 1. Vague request

**Bad**

```text
Fix checkout.
```

**Better**

```text
Fix duplicate order creation when the checkout request is retried.
Preserve the existing API. Use the current idempotency mechanism.
Add a regression test proving one request produces one order.
```

## 2. Artificially tiny prompts

Short does not mean token-efficient if it causes exploration and rework. State outcome, constraints, and verification.

## 3. Repository dump

Do not provide the entire repository by default. Give the task and let the agent retrieve relevant context progressively.

## 4. Giant logs

Prefer targeted extraction around the relevant request, exception, timestamp, or correlation ID.

## 5. Repeating information

Reference the canonical source or summarize only what changed.

## 6. One session for everything

Use focused sessions and short handoffs.

## 7. Premature broad refactoring

Fix the issue first. Refactor separately when there is a clear reason.

## 8. Overusing planning

Don't plan trivial edits. Planning has a cost.

## 9. Under-planning complex work

For architecture, migrations, and large multi-file changes, inspect boundaries and produce a plan before implementation.

## 10. Asking for output you don't need

Prefer:

```text
Summarize the behavioral change, tests run, and any risks.
```

over:

```text
Explain every line you changed.
```

## 11. Endless "improve it"

Make improvement requests measurable:

```text
Reduce checkout latency without changing the API.
```

## 12. Ignoring drift

```text
Stop. This is outside the requested scope.
Revert unrelated changes if they were introduced by this task.
Continue only with <scope>.
```

## 13. Optimizing tokens before correctness

Correct order:

```text
Correctness → scope → context → verification → efficiency
```
