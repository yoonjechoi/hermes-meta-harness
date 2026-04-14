---
name: hermes-meta-harness
description: Build or evolve a Hermes-native meta harness for a project or domain. Use when the user wants reusable specialist workflows, subagent orchestration, multi-phase plans, domain-specific skills, or an audit of an existing harness. Trigger on requests like 'design a harness', 'set up reusable agent workflows', 'build specialist skills for this repo', 'audit our current harness', or 'turn this process into a repeatable Hermes system'.
version: 0.1.0
author: yoonjechoi
license: Apache-2.0
metadata:
  hermes:
    tags: [hermes, harness, meta-skill, delegation, orchestration, skills]
---

# Hermes Meta Harness

Design and evolve Hermes-native harnesses.

A harness is a reusable execution system for a domain or project. It should define:
- which specialist roles exist
- when work should be delegated versus done inline
- which steps deserve their own reusable skills
- what artifacts get written to disk
- how outputs are validated and revisited later

## Core principles

1. Produce durable assets, not just advice.
   A successful run should usually leave behind one or more of:
   - a Hermes skill under `~/.hermes/skills/` or the target repo
   - orchestration markdown describing roles, phases, and handoffs
   - workspace conventions and validation checklists

2. Prefer Hermes-native execution patterns.
   Hermes does not have Claude Code's TeamCreate / SendMessage model. Translate coordination into:
   - `delegate_task` for isolated specialist work
   - `todo` for session-level plan tracking
   - files for explicit handoff artifacts
   - `memory` only for durable user/environment facts
   - `cronjob` only when repeat scheduling is actually useful

3. Match the pattern to the work.
   Use the lightest orchestration that preserves quality.
   - Single specialist -> one delegated subtask or direct execution
   - Independent parallel analyses -> fan-out/fan-in with `delegate_task(tasks=[...])`
   - Generate then critique -> producer/reviewer loop
   - Large evolving work queue -> supervisor pattern using `todo` + repeated delegation

4. Keep skills lean.
   Put decision-heavy workflow in `SKILL.md`. Move bulky examples and edge cases into `references/`.

5. Verify the harness.
   A harness is incomplete until you define how to test triggers, outputs, and failure recovery.

## Phase 0: audit current state

Before designing anything, inspect what already exists.

1. Check for existing skill folders, orchestration docs, project notes, and operating conventions.
2. Identify whether this is:
   - a new harness
   - an extension of an existing harness
   - a maintenance / audit request
3. Detect drift between docs and reality.
   Examples:
   - docs mention a skill that does not exist
   - a workflow assumes tools that are not installed
   - delegated roles overlap or contradict each other
4. Summarize findings before making structural changes.

## Phase 1: domain and workflow analysis

1. Identify the domain: software, research, operations, media, data, etc.
2. Identify recurring task types:
   - discovery / research
   - planning / architecture
   - implementation
   - review / QA
   - deployment / operations
3. Inspect the actual codebase or artifact base when available.
4. Determine what must be reusable across sessions.
5. Calibrate output complexity to the user's likely needs.
   Do not over-engineer a five-agent workflow for a tiny one-off task.

## Phase 2: choose an orchestration pattern

Use `references/delegation-patterns.md` when the choice is not obvious.

### Pattern guide

- Pipeline
  Use for strongly ordered phases where each stage depends on the previous output.

- Fan-out / Fan-in
  Use when multiple analyses or implementations can happen independently, then be merged.

- Expert Pool
  Use when only one or two specialists should be invoked depending on the request type.

- Producer / Reviewer
  Use when output quality improves substantially with an explicit critique pass.

- Supervisor
  Use when work units are numerous, similar, or discovered gradually during execution.

- Hybrid
  Use when different phases want different patterns, such as parallel research followed by sequential synthesis.

## Phase 3: define specialist roles

Hermes specialists are usually represented as delegated task prompts plus supporting skills and docs.

For each role, define:
- purpose
- inputs
- expected outputs
- allowed tools/toolsets
- validation responsibility
- failure handling

Good role definitions are specific enough that a delegated subagent can succeed without hidden context.

## Phase 4: generate reusable skills

Create skills only when a procedure is likely to recur.

Each generated skill should include:
- strong trigger description
- numbered workflow
- decision points and pitfalls
- verification steps
- references for bulky detail

Keep `SKILL.md` concise. If details grow large, split them into `references/` and point to them explicitly.

See `references/skill-authoring-guide.md`.

## Phase 5: define the orchestrator

Write an orchestration document or top-level skill that explains:
- when the harness triggers
- what pattern it uses
- which roles run in which order
- what files or artifacts each phase writes
- how retries and partial failures are handled
- what success looks like

Use `references/orchestrator-template.md` as the baseline template.

## Phase 6: validation

A harness is only ready when validated.

At minimum, define:
- trigger test: would the description cause the skill to load at the right times?
- dry run: can the workflow be simulated without hidden assumptions?
- artifact test: are outputs written where future sessions can find them?
- failure test: what happens if one delegated task fails or returns partial work?
- comparison test: does the harness outperform ad hoc execution on representative tasks?

See `references/testing-guide.md`.

## Translation rules from Claude-oriented harnesses

If adapting an existing Claude Code harness:
- replace TeamCreate / SendMessage semantics with `delegate_task` orchestration
- replace `.claude/skills/` with Hermes skill layout under `~/.hermes/skills/` or repo-local skill source trees
- replace team task boards with Hermes `todo` or explicit markdown trackers
- replace agent definition files with reusable role specs and self-contained delegation prompts
- remove assumptions about long-lived intra-team chat unless you recreate them through artifacts and explicit parent coordination

See `references/migration-notes.md`.

## Deliverables checklist

A good harness run usually ends with most of these completed:
- [ ] top-level harness design summary
- [ ] chosen orchestration pattern with rationale
- [ ] specialist role definitions
- [ ] one or more reusable skills written to disk
- [ ] orchestration template or plan saved to the project
- [ ] validation checklist and smoke-test plan
- [ ] notes on future evolution or maintenance

## Anti-patterns

Avoid these mistakes:
- creating too many specialists for trivial work
- delegating tasks without self-contained context
- writing huge skills with no references split
- saving temporary task status to persistent memory
- pretending a harness is reusable without artifact paths and validation steps
- copying Claude-specific instructions verbatim into Hermes

## When to read references

- Need help choosing a pattern -> `references/delegation-patterns.md`
- Need a top-level orchestrator layout -> `references/orchestrator-template.md`
- Need to write or split skills well -> `references/skill-authoring-guide.md`
- Need validation methodology -> `references/testing-guide.md`
- Migrating from Claude Code harnesses -> `references/migration-notes.md`
