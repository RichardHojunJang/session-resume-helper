---
name: session-resume-helper
description: Resume work in a fresh or recovered session using minimal carry-forward context. Use when starting a new session from an older one, recovering after context bloat or errors, rebuilding state from a handoff summary, choosing what to restore first, or generating a stable first-turn resume prompt without rereading the full transcript.
---

# Session Resume Helper

Resume work from a prior session without dragging the whole transcript forward.

## Core goal

Stabilize the **first turn of a fresh session**.

Carry forward only the minimum context needed to continue useful work:
- canonical summary
- done
- remaining
- next action
- blocker
- key constraints

Do **not** default to replaying the entire previous conversation.

## Inputs

Prefer these inputs in this order:
1. canonical summary
2. latest handoff block
3. archive/reference summary created during preserve-then-reset
4. next action
5. blocker
6. done / remaining
7. key decisions or constraints
8. raw transcript fragments only if a gap remains

If the full transcript exists but a good summary exists too, use the summary first.

## Resume workflow

### 1) Establish source of truth
Identify:
- canonical session
- secondary/reference sessions
- whether ownership is clear

If canonical status is unclear, say so before proceeding.

### 2) Restore minimal state
Reconstruct only:
- task
- stage
- done
- remaining
- next action
- blocker
- important constraints

Avoid importing exploratory noise or repeated explanations.

### 3) Start with a controlled first response
The first reply in the new session should do three things:
- restate the understood current state
- state the next action it will take
- ask for missing context only if required

### 4) Escalate only if needed
Only consult raw history when:
- the summary conflicts with itself
- the next action depends on missing specifics
- canonical status is ambiguous
- a blocker cannot be resolved from the handoff

If the old session was archived and reset out of the active store:
- prefer the archive/reference summary over reopening the full transcript
- use the archived transcript only when the summary or handoff is materially incomplete
- treat the newly created session as the working session unless the handoff says otherwise

---

## First-turn output format

Use this default structure when resuming:

```md
Resume State
- Canonical session:
- Secondary/reference sessions:
- Current task:
- Stage:

What I understand
- Done:
- Remaining:
- Blocker:
- Important constraints:

Next action
- ...

Need from prior context?
- none
```

If more context is required, replace the last line with a short, precise request.

## Minimal restore rules

Always prefer this restore set:
- canonical summary
- done
- remaining
- next action
- blocker
- key constraints

Avoid default inclusion of:
- full transcript
- multiple competing summaries
- long social or conversational filler
- duplicate status recaps

## Canonical-session rules

For a single task:
- prefer one canonical session
- keep other sessions reference-only unless active reconciliation is needed
- if the fresh session becomes the new canonical session, say so explicitly

## Handoff compatibility

This skill works best when the input summary uses fields like:
- canonical session
- secondary/reference sessions
- current task
- stage
- key decisions
- done
- remaining
- next action
- blocker
- important constraints

If the handoff is missing fields, infer conservatively and mark uncertainty.

## Guardrails

- Do not ask the next session to reread everything by default.
- Do not pretend ambiguity is resolved when it is not.
- Do not carry over stale or superseded plans as if they were current.
- Do not expand a concise handoff back into transcript-sized context.

## Example user requests

- "Start a fresh session from this summary."
- "What should the new session read first?"
- "Make a resume prompt for the next session."
- "Recover this task without replaying the whole chat."
- “새 세션 첫 턴용 복원 프롬프트 만들어줘”
- “이전 세션에서 뭘 가져오면 돼?”
- “전문 다시 안 읽고 이어가게 해줘”

## Final definition

This skill turns a prior session's summary or handoff into a **stable fresh-session starting state** and a **minimal resume prompt**.
