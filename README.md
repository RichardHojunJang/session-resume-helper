# session-resume-helper

Agent skill for resuming work in a fresh session using only the minimum carry-forward context.

`session-resume-helper` is for the moment after you already know a session should be resumed, handed off, or restarted. It prevents a fresh session from inheriting transcript-sized baggage.

## What it solves

When old sessions get large, repetitive, stale, or split across multiple branches, starting fresh is often the right move — but only if the right state is restored.

This skill restores only the minimum useful context:
- canonical summary
- done
- remaining
- next action
- blocker
- important constraints

## Core operating model

The skill assumes these session rules:
- one task = one canonical session
- old sessions may become `reference-only`
- new sessions should load summary-level state, not full transcript replay

Preferred input order:
1. canonical summary
2. latest handoff block
3. next action
4. blocker
5. done / remaining
6. key decisions or constraints
7. raw transcript fragments only if a gap remains

## What it outputs

Typical output:

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

This makes the fresh session stable from the first turn.

## Relationship to `session-manager`

- **`session-manager`** decides whether a session should continue, hand off, restart, or become `reference-only`
- **`session-resume-helper`** restores the smallest useful working state after that decision

A practical pairing is:
- 70–84%: `session-manager`
- 85–89%: compression / handoff prep
- 90%+: fresh session + `session-resume-helper`

## Example prompts

- "Start a fresh session from this summary."
- "What should the new session restore first?"
- "Make a resume prompt for the next session."
- "Recover this task without replaying the whole chat."
- “새 세션 첫 턴용 복원 프롬프트 만들어줘”
- “이전 세션에서 뭘 가져오면 돼?”
- “전문 다시 안 읽고 이어가게 해줘”

## Install

```bash
npx -y skills add https://github.com/RichardHojunJang/session-resume-helper
```

Or explicitly:

```bash
npx -y skills add https://github.com/RichardHojunJang/session-resume-helper --skill session-resume-helper
```

## Files

- `SKILL.md` — main resume workflow and minimal-restore rules
- `references/resume-schema.md` — stricter schema and field guidance
- `README.md` — overview and install instructions
