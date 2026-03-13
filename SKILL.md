---
name: session-resume-helper
description: Resume work safely from an old, split, bloated, stale, or interrupted session by restoring only the minimum context needed to continue. Use when starting a fresh session from prior work, handing off between sessions or agents, recovering after context bloat or repetition, or creating a compact handoff that preserves source of truth, recent progress, blockers, and next action without dragging full history forward.
---

# Session Resume Helper

Restore the **minimum viable context** needed to continue work in a fresh session.

This skill is for **resuming**, not for full session diagnosis. Use it after you already know a session should be resumed, handed off, or restarted.

## Core rule

Do not pour the old session into the new one.

Bring forward only:
- current task
- canonical summary
- most recent handoff
- blocker
- next action
- any must-know constraints for this specific continuation

If something is merely nice-to-know, leave it behind.

Assume the old session may be marked `reference-only`.
That means: it may still inform the resume, but it should not be treated as the active working memory for the new session.

## Resume workflow

### 1) Identify the source of truth
Find the canonical source before writing any resume summary.

Prefer, in order:
1. an explicit canonical summary
2. the latest valid handoff/resume block
3. the current session's most recent stable conclusion
4. only if needed, a short scan of recent turns for unresolved changes

If there are conflicting summaries, name the conflict instead of inventing certainty.

### 2) Restore minimum context only
When starting a fresh session, restore only what the next worker must know immediately.

Default restore set:
- what the task is
- what is already done
- what is currently true
- what is blocked
- what should happen next

Do **not** reload:
- old brainstorming unless it still affects the next action
- repeated background explanations
- superseded plans
- full transcript-style history

### 3) Load the canonical summary first
If a canonical summary exists, treat it as the primary resume artifact.

Use it to anchor:
- current task
- source of truth
- latest accepted decisions
- active blocker
- next action

Only add recent details if they materially changed the state after the canonical summary was written.

### 4) Check for a recent handoff automatically
Before writing a new resume block, check whether a recent handoff already exists.

Prefer the most recent handoff when it is:
- still aligned with the canonical summary
- not contradicted by newer work
- specific enough to act on immediately

If a recent handoff exists but is stale, update it instead of duplicating it.

If the old session is marked `reference-only`, treat the recent handoff as a higher-priority resume artifact than the raw transcript.

### 5) Reconstruct only “what this session must know”
Ask:
- What must the new session know in the first 30 seconds?
- What would cause a wrong move if omitted?
- What is the single next useful action?

Build the resume output around that.

## Resume output format

Use this default structure:

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

If the old session should no longer be used actively, append:

```md
Old Session Status
- Status: reference-only
- Reason:
```

## Fresh-session opener

When the user wants a ready-to-send opener for the new session, use this shape:

```text
This is a fresh continuation from an older session.
Use the prior session as reference-only.

Current task: ...
What is already done: ...
Current blocker: ...
Next action: ...
Must-know constraints: ...
```

Keep it short. A fresh session opener should usually fit in 5-8 lines.

## Guardrails

- Do not dump transcript history into the new session unless the user explicitly asks.
- Do not treat the latest message as authoritative if a canonical summary says otherwise.
- Do not create a new handoff block when the current one is still valid and sufficient.
- Do not restore old context that does not change the next action.
- If source of truth is ambiguous, say so explicitly and name the conflict.

## When the old session is unhealthy

If the old session is bloated, repetitive, stale, or degraded:
- prefer that `session-manager` classify it `reference-only`
- extract only the canonical summary plus the latest meaningful delta
- start the new session from the resume block, not from the old transcript

Do not decide session lifecycle here unless needed for clarity. Prefer to inherit the lifecycle judgment from `session-manager`, then resume from that decision.

## Reference file

For a more opinionated resume schema and selection rules, read:
- `references/resume-schema.md`
