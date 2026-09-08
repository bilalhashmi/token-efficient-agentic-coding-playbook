# Context Management

## Why context management matters

Agent sessions accumulate information. Old task history, large tool output, repeated file reads, and unrelated discussions can make future decisions harder and more expensive.

The objective is not to keep the maximum amount of context. The objective is to keep the **right context**.

## Context triage

| Question | If yes |
|---|---|
| Does it change the implementation decision? | Include |
| Does it explain the current failure? | Include |
| Is it an explicit constraint? | Include |
| Is it a canonical example/pattern? | Usually include |
| Is it merely interesting background? | Usually exclude |
| Is it duplicated elsewhere? | Keep one source |
| Is it stale? | Remove |

## Context escalation ladder

```text
Task + known file
    ↓
Relevant file/module
    ↓
Related implementation + tests
    ↓
Architecture / dependency context
    ↓ only if needed
Wider repository exploration
```

## Repeated reads

Avoid:

```text
Read file → discuss → read same file again → ask same question → read again
```

Prefer:

```text
Read relevant section → extract decision → implement → verify
```

## Large logs

Use narrowing queries:

```text
Find the error.
↓
Show the first occurrence and surrounding stack trace.
↓
Find where this exception is thrown.
↓
Inspect the caller.
```

Avoid dumping the complete log unless timeline reconstruction genuinely requires it.

## Generated files

Generated output can be huge and often has low decision value. Prefer source configuration, generator input, relevant generated sections, schemas, and summarized command output.

Use repository ignore mechanisms when supported and appropriate.

## Compaction / fresh context

Use compaction or a fresh session when:

- the task is complete enough to summarize
- old exploration is no longer useful
- the conversation contains unrelated tasks
- the agent starts repeating itself
- context is dominated by logs/tool output
- you are starting a distinct task

Before restarting, preserve:

```text
Goal
Current state
Changed files
Known decisions
Remaining work
Verification
```

## Prompt caching awareness

Where a coding-agent system supports prompt caching:

- keep stable instructions stable
- avoid unnecessary changes to the beginning of a long context
- put variable task details later where appropriate
- do not keep irrelevant context alive just for caching

Caching is an optimization, not a reason to retain useless history.

## Context hygiene checklist

- [ ] Is this still the same task?
- [ ] Does the current context contain unrelated work?
- [ ] Have I already supplied this information?
- [ ] Are tool outputs larger than necessary?
- [ ] Are there stale assumptions?
- [ ] Would a short handoff be cheaper than carrying history?
