# Practical Examples

## 1. Bug fix

### Weak

```text
Fix the login problem.
```

### Better

```text
Goal:
Fix the login timeout when an access token expires.

Context:
The refresh-token flow already exists in AuthService.

Constraints:
- Reuse the existing refresh flow.
- Retry the original request at most once.
- Do not change the public API.

Acceptance criteria:
- Expired access token + valid refresh token => refresh and retry.
- Invalid refresh token => normal authentication failure.
- No infinite retry loop.

Verification:
Add/update focused unit tests for both cases.
```

The agent does not need to infer the retry behavior or invent a new authentication mechanism.

## 2. REST API endpoint

```text
Add POST /orders.

Follow the existing order-controller/service/repository pattern.

Behavior:
- Empty cart => 400.
- Unavailable product => 409.
- Valid request => create one order and return the existing order response schema.

Constraints:
- Reuse existing validation and persistence patterns.
- Do not introduce a new framework or dependency.

Verification:
Add focused API/service tests for all three cases.
```

## 3. Multi-file feature

For password reset, first ask for a plan:

```text
Before editing, inspect the existing authentication flow and tests.

Plan a password-reset feature using the repository's current patterns.

Cover:
- request/reset-token flow
- token expiration
- password update
- invalid/expired token behavior
- relevant API and test files

Do not implement yet.
```

Then implement the approved scope.

## 4. React UI bug

```text
Fix the cart quantity control so decrementing from 1 does not
produce 0 or a negative quantity.

Context:
Use the existing CartItem component and current state management.

Constraints:
- Minimum quantity is 1.
- Preserve the existing visual design.
- Do not change the cart API.

Verification:
Add/update the component test for decrement at quantity 1.
```

## 5. Retry behavior

```text
Add retry handling to the existing HTTP client.

Rules:
- Retry HTTP 5xx up to 3 attempts.
- Do not retry 4xx responses.
- Preserve the existing timeout behavior.
- Use the existing retry/policy utility if one exists.

Verification:
Test 5xx retry, 4xx no-retry, and final failure after 3 attempts.
```

## 6. Code review

```text
Review src/orders for correctness risks.

Prioritize:
- duplicate order creation
- concurrency
- error handling
- retry/idempotency behavior
- backward compatibility

Ignore formatting and stylistic issues already covered by tooling.

Return only actionable findings with file and symbol references.
Do not modify code.
```

## 7. Large refactor

```text
Refactor the notification delivery layer to separate transport
selection from message composition.

Before editing:
- identify current notification implementations
- identify callers
- identify tests
- identify public interfaces

Constraints:
- preserve externally visible behavior
- preserve existing configuration format
- avoid unrelated cleanup

Produce a staged plan first.
```

## 8. Investigation before implementation

```text
Investigate why POST /orders occasionally creates duplicate orders.

Focus on:
- request handling
- persistence transaction boundaries
- retries
- idempotency keys
- concurrency

Do not modify code yet.

Return:
1. likely root cause
2. evidence
3. smallest safe fix
4. regression test
```

## 9. Handoff between sessions

```text
Task:
Fix duplicate order creation.

Current state:
Root cause identified in OrderService retry handling.

Changed:
- src/orders/OrderService.cs
- tests/orders/OrderServiceTests.cs

Remaining:
- add integration regression test

Verification:
Unit tests pass.

Next step:
Add the integration test and run the orders integration suite.
```
