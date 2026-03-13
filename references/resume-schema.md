# Resume Schema

Use this file when you need a stricter, more explicit resume artifact.

## Goal

A resume block should let a new session become productive quickly without inheriting unnecessary baggage.

## Preferred source order

When multiple artifacts exist, prefer them in this order:
1. canonical summary
2. recent valid handoff
3. latest stable decision block
4. recent turns containing unresolved changes

## Minimum viable resume

Use these fields by default:

```md
Session Resume
- Task:
- Canonical source:
- What is done:
- What is currently true:
- Blocker:
- Next action:
- Must-know constraints:
```

## Field guidance

### Task
One sentence. State the actual active task, not the whole project history.

### Canonical source
Name the summary, file, or session that should be treated as source of truth.

### What is done
List only completed work that changes what the next session should do.

### What is currently true
State the latest accepted state of the world.
Examples:
- repo already updated
- old session is bloated and now reference-only
- authentication already fixed

### Blocker
State the real blocker, if any. If none, say `none`.

### Next action
Make it concrete and singular when possible.
Bad: "continue working"
Good: "open a fresh session and continue from the canonical summary"

### Must-know constraints
Include only constraints that could cause a wrong move if forgotten.
Examples:
- use repo A, not workspace mirror
- keep prior session reference-only
- do not reload full transcript

## What not to carry over

Usually exclude:
- repeated explanations
- abandoned brainstorm branches
- superseded decisions
- old debugging attempts that no longer matter
- social filler or acknowledgements

## Reference-only rule

Usually let `session-manager` decide this status first.

When an old session is already marked `reference-only`:
- treat it as supporting context, not active working memory
- prefer canonical summary and recent handoff over raw transcript history
- carry forward only the minimum needed for the next correct action

Typical reasons a session becomes `reference-only`:
- context is bloated
- repetition is visible
- quality degraded
- the new session should not inherit full history

## Good fresh-session opener

```text
Fresh continuation from an older session.
Old session is reference-only.

Current task: finalize session resume helper rules.
What is done: token thresholds and proactive heuristics were added.
Current blocker: none.
Next action: continue implementation from the canonical summary only.
Must-know constraints: do not reload full prior transcript.
```

## Update vs replace rule

If a recent handoff already exists and is still valid:
- update it only if state changed
- do not create multiple overlapping handoff blocks

Favor one clean current resume artifact over many near-duplicates.
