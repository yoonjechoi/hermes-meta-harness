# Migration Notes: Claude-Oriented Harness -> Hermes Meta Harness

Use this guide when adapting an existing Claude Code harness to Hermes.

## Replace platform-specific assumptions

Claude-oriented assumptions:
- `.claude/agents/`
- `.claude/skills/`
- `CLAUDE.md`
- TeamCreate / SendMessage / TaskCreate

Hermes-oriented replacements:
- Hermes skills under `~/.hermes/skills/` or a repo-local source tree
- orchestration markdown stored wherever the project keeps operating docs
- `delegate_task` for isolated specialist execution
- `todo` for explicit parent-managed task tracking
- `memory` only for durable user/environment facts

## Translate roles, not syntax

Do not copy agent-team instructions verbatim.
Instead, preserve the intent:
- who does what
- in what order
- with what inputs
- producing which outputs
- validated how

## Expect parent-managed coordination

Hermes delegated subtasks do not share a live team chat.
So the parent must:
- pass context explicitly
- merge results intentionally
- preserve artifacts for later phases
- decide retries and escalation

## Simplify where possible

Many Claude team workflows become smaller in Hermes:
- a three-agent team may become one delegated specialist plus one reviewer
- a shared task board may become a short `todo` list
- a persistent team may become saved markdown plus repeatable prompts

## Keep what actually creates value

Retain:
- architecture patterns
- role separation
- validation discipline
- reusable skills

Discard or replace:
- assumptions about long-lived intra-agent chat
- tool names that do not exist in Hermes
- file paths tied to `.claude/*`
