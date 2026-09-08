# Fundamentals

## 1. What makes agentic coding expensive?

Token use is only part of the cost. An agent can spend effort on reading files, searching the repository, processing tool output, maintaining conversation history, generating plans, generating code, running tests, retrying after failures, and re-reading information it already saw.

A useful mental model:

```text
Total effort
≈ context processing
+ tool calls
+ model generation
+ verification
+ rework
```

The goal is not "write the shortest prompt." The goal is **minimize unnecessary work while preserving enough information for correct decisions.**

## 2. Specific beats short

Bad:

```text
Fix login.
```

Better:

```text
Fix the login timeout that occurs when the access token expires.
Reuse the existing refresh-token flow. Retry the original request
once after a successful refresh. Do not retry when the refresh token
is invalid. Add focused tests and do not change the public API.
```

The second prompt is longer but can be cheaper overall because it reduces guessing and rework.

## 3. Progressive context disclosure

Do not front-load the entire repository. Start with the smallest useful context and expand only when needed.

```text
Task
 ↓
Known file
 ↓
Enough context? ── yes → Implement
 ↓ no
Relevant module
 ↓
Enough context? ── yes → Implement
 ↓ no
Related tests / architecture
 ↓
Enough context? ── yes → Implement
 ↓ no
Broader exploration
```

## 4. Deterministic work should be deterministic

If the answer can be obtained reliably with a tool, do not spend model reasoning on it.

| Need | Prefer |
|---|---|
| Find a file | Search |
| Find a symbol | Code search |
| Find exact text | Exact search |
| Format code | Formatter |
| Run tests | Test runner |
| Inspect changed files | Git diff/status |
| Calculate a value | Calculator/script |
| Transform structured data | Script/tool |

Use the model for decisions, interpretation, implementation, and trade-offs.

## 5. Tool output should be decision-ready

Large tool output is not automatically useful.

Bad:

```text
Return the complete 50,000-line log.
```

Better:

```text
Find the first failed request, identify the exception,
and show 20 lines around it.
```

The principle applies to logs, search results, test output, database results, API responses, and documentation.

## 6. One coherent task per session

Unrelated tasks create polluted context.

Bad:

```text
Fix login → explain Kubernetes → update README → debug payment → fix login again
```

Better:

```text
Session A: login
Session B: payment
Session C: documentation
```

A fresh context is often cheaper than carrying irrelevant history forward.

## 7. Planning is not always cheaper

Planning has a cost. Use planning when it reduces expected rework.

Good candidates:

- multi-file features
- architectural changes
- migrations
- large refactors
- unfamiliar subsystems

For a one-line rename, planning is usually unnecessary.

## 8. Acceptance criteria reduce ambiguity

Bad:

```text
Make checkout better.
```

Better:

```text
POST /orders must:
- reject an empty cart with 400
- reject an unavailable product with 409
- create exactly one order for a successful request
- preserve the existing response schema
- have focused tests for each case
```

## 9. Repository quality affects agent efficiency

Useful repository assets:

```text
README.md
AGENTS.md / CLAUDE.md / equivalent
docs/
tests/
scripts/
```

Good documentation answers: How do I build? How do I test? Where is the main implementation? What conventions matter? What must not be changed? Which commands are canonical?

## 10. Persistent instructions should be small

Put stable information there.

Good:

```text
Run unit tests with: ./scripts/test-unit.sh
Use the existing service/repository pattern.
Do not edit generated files.
```

Task-specific instructions belong in the task prompt.

## 11. Don't create a rule for every mistake

Ask:

1. Is this recurring?
2. Is the failure caused by missing repository knowledge?
3. Would a reusable rule prevent future waste?
4. Is the rule worth the context it consumes?

If not, fix the immediate task and move on.

## 12. Canonical sources of truth

When multiple sources describe the same thing, identify one canonical source.

```text
API contract → OpenAPI specification
Implementation → src/orders/
Tests → tests/orders/
```

## 13. Token efficiency vs quality

Never optimize token use by removing information that affects correctness.

Good optimization is structured, relevant context—not vague prompts.

## 14. Practical optimization hierarchy

```text
1. Correct task definition
2. Correct scope
3. Correct context
4. Correct tool usage
5. Correct verification
6. Model/effort optimization
7. Prompt wording micro-optimization
```

Do not shave 20 tokens from a prompt while the agent explores 200 irrelevant files.
