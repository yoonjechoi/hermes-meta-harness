# Delegation Patterns for Hermes Meta Harness

This document maps common multi-agent patterns onto Hermes-native tools.

## 1. Pipeline

Use when each phase depends on prior output.

Shape:
1. inspect / gather context
2. design / decide
3. implement
4. verify

Hermes implementation:
- direct execution for simple steps
- `delegate_task` for isolated heavyweight phases
- files for explicit handoff artifacts

Good for:
- implementation plans
- docs pipelines
- migrations with fixed stage order

Pitfall:
- if a middle stage is weak, everything downstream inherits the flaw

## 2. Fan-out / Fan-in

Use when several independent perspectives are valuable.

Hermes implementation:
- `delegate_task(tasks=[...])` with 2-3 parallel tasks
- merge results in the parent context
- write the merged artifact to disk

Good for:
- code review across security/performance/architecture
- research from official/community/competitive angles
- parallel subsystem inspection

Pitfall:
- merging low-quality or overlapping outputs without reconciliation

## 3. Expert Pool

Use when only some specialists are relevant per request.

Hermes implementation:
- parent agent routes to one or two focused delegated tasks
- avoid spawning a large team by default

Good for:
- issue triage
- repo operations
- domain-specific workflows with sparse specialist use

Pitfall:
- overfitting the router and missing adjacent expertise

## 4. Producer / Reviewer

Use when a second pass materially improves quality.

Hermes implementation:
- delegated producer creates artifact
- delegated reviewer critiques against explicit rubric
- parent reconciles and applies fixes or requests one revision pass

Good for:
- code generation
- docs generation
- requirements interpretation

Pitfall:
- endless revise/review loops; cap to 1-2 review rounds unless the user asks for more

## 5. Supervisor Pattern

Use when tasks are many, discovered incrementally, or naturally tracked as a queue.

Hermes implementation:
- parent maintains a `todo` list
- repeatedly delegates focused work items
- writes status artifacts after each wave

Good for:
- large refactors
- migration across many files
- operational audits

Pitfall:
- parent becomes a bottleneck if work items are too tiny

## 6. Hybrid Pattern

Use different patterns across phases.

Examples:
- fan-out research -> pipeline synthesis
- pipeline implementation -> producer/reviewer validation
- supervisor discovery -> expert pool resolution

## Choosing the lightest effective pattern

Ask:
1. Do I really need parallel specialists?
2. Do specialists need to communicate directly, or can the parent merge artifacts?
3. Is the work recurring enough to justify a skill?
4. What artifact needs to exist after the run?

## Claude-to-Hermes mapping

- TeamCreate -> parent orchestrates with `delegate_task`
- SendMessage -> parent passes summarized outputs or saved artifacts between steps
- shared task board -> Hermes `todo` or markdown tracker
- `.claude/agents/*.md` -> role specs plus self-contained delegation prompts
- `.claude/skills/*` -> Hermes skills under `~/.hermes/skills/` or repo-local skill trees
