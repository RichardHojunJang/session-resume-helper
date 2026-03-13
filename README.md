# session-resume-helper

`session-resume-helper` is a skill for safely continuing work from an old, split, bloated, stale, or interrupted session **without dragging the full transcript into a new one**.

Its job is simple:
- restore the **minimum viable context**
- prefer the **canonical summary** over raw history
- check for the **most recent useful handoff**
- recover only what the new session **must know right now**

This makes it useful when a session has become too large, repetitive, stale, or awkward to continue directly.

## What problem it solves

Long-lived sessions tend to accumulate baggage:
- repeated explanations
- stale plans
- abandoned branches
- too much context for the next turn to use efficiently

When that happens, starting fresh is often better — but only if the right context is carried forward.

`session-resume-helper` helps create that compact bridge.

## What it does

The skill focuses on **resume and handoff**, not full diagnosis.

It helps produce a compact continuation block containing:
- current task
- canonical source
- what is done
- what is currently true
- blocker
- next action
- must-know constraints

It also provides a short **fresh-session opener** that can be pasted into a new session.

## Design philosophy

### 1. Minimum context only
Do not pour an old session into a new one.

Bring forward only what changes the next correct action.

### 2. Canonical summary first
If a canonical summary exists, use it as the primary resume artifact.

Only add newer details if they materially changed the state after that summary.

### 3. Recent handoff before raw transcript
If a recent valid handoff already exists, prefer it over re-reading the full transcript.

### 4. Restore only what this session must know
The core question is:

> What must the next session know in the first 30 seconds to avoid a wrong move?

If something is merely nice to know, it usually should not be carried over.

## Relationship to `session-manager`

`session-resume-helper` works especially well with `session-manager`.

- **`session-manager`** decides whether a session should remain active, be restarted, or become `reference-only`
- **`session-resume-helper`** takes that decision and builds the smallest useful resume package for the next session

A good mental model:
- `session-manager` = diagnosis and lifecycle decision
- `session-resume-helper` = handoff and resume packaging

## Reference-only sessions

This skill assumes an old session may already be marked `reference-only`.

That means:
- it may still contain useful history
- it should not remain the active working memory
- the new session should resume from summaries and handoffs, not from full transcript replay

## Output shape

Typical output:

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

Typical fresh-session opener:

```text
This is a fresh continuation from an older session.
Use the prior session as reference-only.

Current task: ...
What is already done: ...
Current blocker: ...
Next action: ...
Must-know constraints: ...
```

## Files

- `SKILL.md` — main skill behavior and resume workflow
- `references/resume-schema.md` — stricter schema and field-by-field guidance

## Good use cases

Use this skill when:
- a session became bloated and needs a clean restart
- work is being handed off between sessions or agents
- a previous session is stale, split, or partially interrupted
- you want to preserve only the source of truth and next action
- you need a compact resume block instead of transcript replay

## Non-goals

This skill is **not** primarily for:
- broad session health diagnosis
- deciding whether a session is bloated in the first place
- full archive or transcript retention strategies

Those decisions belong more naturally to `session-manager`.

## Status

Current version: initial working draft.

It is designed to be small, opinionated, and easy to pair with `session-manager` for practical session recovery workflows.
