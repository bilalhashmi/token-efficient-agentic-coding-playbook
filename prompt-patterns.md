# Prompt Patterns

## Standard task template

```text
Goal:
<one clear outcome>

Context:
<relevant component, file, existing behavior>

Constraints:
- <important boundary>
- <existing pattern to reuse>
- <thing that must not change>

Acceptance criteria:
- <observable result>
- <observable result>

Verification:
<tests/checks to run>
```

## Bug fix

```text
Goal:
Fix <specific failure>.

Context:
It occurs in <component/file> when <condition>.

Constraints:
- Preserve existing behavior for <case>.
- Reuse <existing mechanism>.
- Do not change <public API/schema>.

Acceptance criteria:
- <case A> behaves as <result>.
- <case B> behaves as <result>.
- No regression in <existing behavior>.

Verification:
Run <focused tests> and inspect the diff.
```

## New feature

```text
Goal:
Add <feature>.

Existing pattern:
Use the same approach as <known feature/file>.

Scope:
- <file/module>
- <file/module>

Constraints:
- <constraint>

Acceptance criteria:
- <observable behavior>

Verification:
Add/update focused tests and run the relevant test suite.
```

## Refactor

```text
Goal:
Refactor <component> to <desired structure>.

Why:
<reason for refactor>

Must preserve:
- public behavior
- API/schema
- performance characteristic
- existing tests

Do not:
- change unrelated modules
- introduce a new dependency unless necessary

Verification:
Run focused tests, then the broader relevant suite.
Review the diff for accidental behavior changes.
```

## Investigation

```text
Investigate <specific problem>.

Focus only on:
- <module>
- <failure path>
- <specific risk>

Find:
1. likely root cause
2. evidence in the code
3. recommended fix
4. tests that would prove the fix

Do not modify code yet.
```

## Code review

```text
Review <scope> for correctness risks.

Prioritize:
1. data loss / corruption
2. security
3. concurrency
4. error handling
5. retries / idempotency
6. backward compatibility

Ignore formatting and stylistic preferences already enforced by tooling.

Report only actionable findings with file/symbol references.
```

## Test failure

```text
A focused test is failing:

<error>

Relevant test:
<path>

Expected:
<behavior>

Actual:
<behavior>

Investigate the smallest relevant scope.
Determine whether the issue is in the test or implementation.
Fix the root cause and rerun the focused test.
```

## Ask for a plan

```text
Before editing, inspect the relevant code and produce a concise plan.

Include:
- files likely to change
- key implementation steps
- risks
- verification steps

Do not implement yet.
```

Then:

```text
Proceed with the approved plan.
Keep the change scoped to the plan unless a blocking dependency requires adjustment.
```

## Stop / redirect

```text
Stop exploring unrelated areas.

Scope:
<allowed files/modules>

Goal:
<goal>

Do not:
<excluded areas>

Continue from the current state and verify:
<criteria>
```

## Handoff

```text
Task:
<goal>

Current state:
<what is already implemented>

Changed:
- <file>
- <file>

Remaining:
- <item>

Known issue:
<issue, if any>

Verification:
<tests already run and result>

Next step:
<exact next action>
```
