# Skill Authoring Guide for Hermes Meta Harness

Write skills for repeated procedures, not for single outputs.

## 1. Description quality matters most

The description is the trigger surface. Make it explicit and broad enough to activate at the right times.

Weak:
- "Handles code review"

Better:
- "Use for pull request review, git diff inspection, pre-push audits, or when the user asks for architecture/security/performance review of code changes."

## 2. Keep SKILL.md decision-heavy and reference-light

Good contents for SKILL.md:
- trigger conditions
- workflow steps
- decision points
- pitfalls
- verification

Move these into `references/`:
- long examples
- framework-specific variants
- large tables
- detailed troubleshooting appendices

## 3. Prefer procedures over slogans

Bad:
- "Always be careful"

Good:
- "Before editing files, inspect current structure and dependency boundaries. After edits, run the smallest relevant verification command."

## 4. Make verification explicit

Every reusable skill should describe how success is checked.
Examples:
- run tests
- inspect generated file paths
- compare outputs to requested format
- verify authentication state

## 5. Encode pitfalls discovered during real use

Good skill maintenance includes:
- updating stale commands
- documenting environment quirks
- noting common failure modes
- splitting oversized skill files

## 6. Favor self-contained delegation prompts

If the skill relies on subagents, ensure prompts include:
- the exact goal
- repository or file paths
- constraints
- expected output format
- toolsets needed

## 7. Define artifacts

Reusable workflows should say where outputs live.
Examples:
- `docs/harness-plan.md`
- `.hermes/notes/research-summary.md`
- `skills/<skill-name>/SKILL.md`
