# Testing Guide for Hermes Meta Harness

A harness is not done when the docs exist. It is done when the docs predict successful execution.

## 1. Trigger test

Ask whether the description would activate in the intended cases.

Test with prompts like:
- "Design a harness for this repo"
- "Turn this workflow into reusable Hermes skills"
- "Audit the current harness"

## 2. Dry-run test

Walk through the workflow without making assumptions that are not written down.

Checklist:
- Are all needed inputs identified?
- Are role boundaries clear?
- Are artifact paths specified?
- Are required toolsets named?

## 3. Artifact test

Verify that the harness creates durable outputs future sessions can reuse.

Examples:
- skill folder created
- orchestration markdown saved
- validation checklist written

## 4. Failure-mode test

Simulate:
- one delegated task returns partial work
- one required tool is unavailable
- the repo structure is not what the harness expected

The harness should explain how to proceed.

## 5. Comparison test

Compare:
- ad hoc execution with no harness
- execution using the harness

Look for gains in:
- consistency
- completeness
- reusability
- easier future runs

## 6. Maintenance test

After a real run, ask:
- what instructions were missing?
- what assumptions were wrong?
- what should become a reference file?
- what should be removed because it adds noise?
