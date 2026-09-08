# Verification

## Verification is part of the task

A coding agent that writes code but does not verify it has not completed the engineering task.

Use:

```text
Implement → verify → inspect → report
```

## Verification ladder

### Level 1 — Static inspection

- compile/type check
- formatter
- linter
- inspect changed symbols

### Level 2 — Focused tests

Run tests directly related to the change.

### Level 3 — Component/module tests

Use when the change crosses a module boundary.

### Level 4 — Broader regression suite

Use when public behavior, shared code, or integration boundaries changed, or risk is high.

### Level 5 — Full system validation

Use when required by the delivery process.

## Don't default to the biggest test suite

```text
One-line parser change → parser tests → broader suite if parser is shared
```

## Acceptance criteria should map to tests

Example:

```text
Requirement: POST /orders rejects an empty cart.
Test: POST /orders with [] → 400.
```

```text
Requirement: An unavailable product cannot be ordered.
Test: POST /orders with unavailable item → 409.
```

```text
Requirement: Successful checkout creates one order.
Test: POST /orders → exactly one order persisted.
```

## Inspect the diff

After implementation:

```text
git status
git diff
```

Look for unrelated files, formatting churn, debug code, temporary logging, changed public APIs, dependency changes, generated files, and missing tests.

## Failure handling

1. Read the actual failure.
2. Classify it: implementation, test, environment, dependency, or flaky infrastructure.
3. Fix the root cause.
4. Re-run the smallest useful test.
5. Expand verification only when justified.

Avoid repeatedly running the same failing command without changing the cause.

## Verification prompt

```text
Run the focused tests for this change.

If they fail:
- inspect the actual failure
- determine whether the test or implementation is wrong
- fix the root cause
- rerun the focused tests

After they pass, inspect the diff for unrelated changes.
```

## Definition of done

A task is normally done when:

- acceptance criteria are satisfied
- relevant tests pass
- the diff is scoped
- no known blocking issue remains
- the implementation follows existing project patterns

Don't continue because the agent "could do more."
