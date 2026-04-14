# Orchestrator Template for Hermes Meta Harness

Use this template when turning a domain-specific harness into a durable top-level skill or orchestration document.

## Template

```markdown
# {Domain} Hermes Harness

## Trigger
Use when the user asks for {primary trigger phrases}.

## Goal
Create {final output or operating capability}.

## Pattern
Choose one:
- Pipeline
- Fan-out / Fan-in
- Expert Pool
- Producer / Reviewer
- Supervisor
- Hybrid

## Roles
| Role | Purpose | Inputs | Outputs | Toolsets |
|------|---------|--------|---------|----------|
| researcher | gathers facts | user prompt, repo | notes.md | web,browser,file |
| implementer | changes code/docs | plan.md, repo | patch summary | terminal,file |
| reviewer | validates against rubric | artifacts | review.md | terminal,file |

## Phase 0: Audit current state
- inspect existing skills, docs, and conventions
- identify drift
- summarize before structural changes

## Phase 1: Prepare artifacts
- create working notes directory if needed
- save assumptions and inputs

## Phase 2: Execute orchestration
- delegate parallel work where useful
- keep parent responsible for synthesis
- save intermediate outputs to explicit paths

## Phase 3: Validate
- run smoke tests
- compare outputs against requirements
- note any unresolved risks

## Failure handling
- one delegated task fails -> retry once or continue with partial result
- major assumption missing -> stop and ask user
- low confidence merge -> preserve conflicting findings instead of hiding them

## Deliverables
- top-level summary
- saved artifacts
- next-run instructions
```

## Notes

- Prefer artifact paths over ephemeral in-chat coordination.
- Delegated tasks do not share context automatically. Pass all necessary context explicitly.
- If a role repeatedly needs the same method, convert that method into a dedicated skill.
