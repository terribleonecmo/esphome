---
name: debugging-verification
description: "Use when debugging a bug, tracing a regression, checking a failing test, or validating a fix. Focuses on root cause analysis and proof before completion."
allowed-tools: Read, Grep, Glob, Bash, Edit
---

# Debugging and Verification Workflow

Use this skill when a bug, regression, failing test, or unexpected behavior needs a focused root-cause fix.

## Goal

Fix the real cause with the smallest safe change, and only call the work complete when the relevant verification proves it.

## Workflow

### 1. Reproduce and localize

Start with the exact symptom.

- Run the smallest command that reproduces the issue.
- Capture the actual error, stack trace, or behavior difference.
- Identify the boundary where the failure occurs: parsing, config validation, code generation, component logic, or runtime behavior.

If the issue cannot be reproduced, stop and gather more data instead of guessing.

### 2. Trace the root cause

Follow the data flow to the source of the problem.

- Search for the relevant symbols, configuration keys, or failing logic.
- Read only the files needed to connect the symptom to the cause.
- Check whether there was a recent behavior change or dependency mismatch.
- Prefer the one hypothesis that best explains all evidence.

Do not fix a symptom if the underlying cause is still unclear.

### 3. Prove the bug with a failing check

Before changing code, create the smallest meaningful proof.

- Add or run a focused failing test when possible.
- If no test exists, use a minimal reproduction script or exact command.
- Keep the failing check narrow and tied to the real bug.

This prevents speculative fixes and ensures the regression is measurable.

### 4. Implement the single root-cause fix

Make the smallest change that addresses the identified cause.

- Avoid unrelated refactors or broad cleanup while debugging.
- Preserve existing behavior outside the failing path.
- Prefer explicit, maintainable fixes over workaround-style logic.

If a second hypothesis appears, test it separately instead of stacking fixes together.

### 5. Validate with the smallest relevant proof

After the fix, run the command or tests that specifically check the changed behavior.

- Prefer the narrowest relevant test suite or reproduction command.
- Check both the regression and nearby behavior if needed.
- If validation fails, return to root-cause analysis before making another patch.

### 6. Complete only with evidence

Only mark the task complete when the evidence matches the request.

Required completion checks:
- The original symptom is reproduced or clearly explained.
- The root cause was identified, not merely masked.
- A failing check existed before the fix, or a minimal repro proved the bug.
- The relevant verification pass after the fix is successful.
- The patch is scoped to the root cause and does not include unrelated churn.

## Decision Points

### If the bug is not reproducible

- Gather the exact inputs.
- Check logs, config, environment, and dependency versions.
- Narrow the scope and isolate the workflow step where it breaks.

### If multiple root-cause hypotheses exist

- Test one hypothesis at a time.
- Prefer the one that explains the observed data and failure path most directly.
- Drop weak hypotheses instead of stacking speculative code.

### If a test does not exist

- Add the smallest focused regression test or reproduction.
- Keep it realistic and tied to the actual behavior.

### If the fix broadens beyond the issue

- Revert or split the patch.
- Keep the solution minimal and targeted.

## Good Completion Criteria

This workflow is complete when all of the following are true:

- The bug is understood in terms of cause and effect.
- The fix is smaller than the problem it solves.
- The relevant validation passes with fresh output.
- No unverified claims are made about completion.

## Example prompts

- "Debug why this ESPHome config fails to validate."
- "Trace the root cause of this regression and add a focused test."
- "Find the failing behavior and verify the fix with the smallest relevant command."
- "Investigate this compile error and confirm the root cause before changing code."

## Related customizations to create next

- A repository-specific PR workflow skill for preparing and submitting a patch.
- A testing-first skill for writing focused regression tests before implementation.
- A component-specific skill for ESPHome codegen or YAML validation workflows.
