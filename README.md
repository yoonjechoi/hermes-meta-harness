<p align="center">
  <img src="harness_banner.png" alt="Hermes Meta Harness Banner" width="600">
</p>

# Hermes Meta Harness

English | [한국어](README_KO.md)

Meta harness skill for Hermes Agent.

This repository adapts the "harness" idea into a Hermes-native workflow: inspect a domain, design the right multi-agent topology, define reusable skills, and scaffold durable orchestration docs that fit Hermes tools such as delegate_task, todo, memory, cronjob, browser, web, and terminal.

## What it is

Hermes Meta Harness is a top-level skill that helps Hermes build domain-specific execution systems.

When triggered, it should:
- analyze the domain or project
- decide whether the job wants a pipeline, fan-out/fan-in, reviewer loop, supervisor, or hybrid pattern
- define specialist roles as Hermes subagent prompts and workflows
- generate reusable Hermes skills for repeatable procedures
- create orchestration notes and workspace conventions for future runs
- verify that the produced harness is usable in practice

## Why this exists

The original harness concept was built around Claude Code agent teams and `.claude/*` conventions.
Hermes has a different execution model:
- `delegate_task` instead of TeamCreate/SendMessage
- `todo` for shared session planning
- `memory` for durable environment/user facts
- Hermes skills under `~/.hermes/skills/`
- optional cron jobs, browser automation, and terminal/file toolchains

So a direct copy is not enough. This repo reframes the approach for Hermes-native orchestration.

## Repository layout

```
hermes-meta-harness/
├── README.md
├── README_KO.md
├── LICENSE
├── skills/
│   └── hermes-meta-harness/
│       ├── SKILL.md
│       └── references/
│           ├── delegation-patterns.md
│           ├── orchestrator-template.md
│           ├── skill-authoring-guide.md
│           ├── testing-guide.md
│           └── migration-notes.md
└── assets from the original project (banner/images)
```

## Installation

### Manual install into Hermes

Copy the skill directory into your Hermes skills directory:

```bash
mkdir -p ~/.hermes/skills
cp -r skills/hermes-meta-harness ~/.hermes/skills/hermes-meta-harness
```

After that, start a new Hermes session so the skill can be discovered.

### Expected trigger phrases

Examples:
- "Design a harness for this project"
- "Build a Hermes meta harness for this domain"
- "Set up a reusable agent workflow for this repo"
- "Create specialist skills and orchestration docs for this codebase"
- "Audit and evolve the existing harness"

## Output philosophy

This harness should produce durable artifacts, not just one-off chat plans.
Typical outputs include:
- Hermes skill folders with `SKILL.md` and references
- orchestration markdown describing phases, roles, inputs, outputs, and recovery paths
- workspace conventions for running the workflow repeatedly
- validation checklists and smoke tests

## Architecture patterns

The harness supports these Hermes-friendly patterns:
- Pipeline
- Fan-out / Fan-in
- Expert Pool
- Producer / Reviewer
- Supervisor
- Hybrid orchestration

See `skills/hermes-meta-harness/references/delegation-patterns.md`.

## Relationship to the original Harness project

This repository is a port of the original `revfactory/harness` idea into a Hermes Agent-native form.
In other words, it explicitly ports the original repository's meta-harness concept, structure, and workflow philosophy into Hermes tools and conventions.

It is not a Claude Code plugin.
Instead, it preserves the useful parts of the original repo while translating the execution model to Hermes primitives such as `delegate_task`, `todo`, `memory`, Hermes skill directories, and artifact-based orchestration.

## License

Apache 2.0
