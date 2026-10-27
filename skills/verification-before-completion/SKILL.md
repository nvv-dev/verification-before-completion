---
name: verification-before-completion
description: Use before saying a task is done, fixed, passing or ready — before a commit, a PR, or a final summary. Requires fresh evidence from running the checks, and an honest list of anything that was weakened or skipped.
---

# Verification before completion

"Done" is a claim, and a claim needs evidence produced in this session, after the last change. Not "it should work", not the output of an earlier run.

## Before claiming completion

1. Identify the checks that prove this task: the acceptance criteria, the tests that cover them, the build, lint and type checks, and the task's own verification command if the plan defines one.
2. Run them now, after your last edit. Read the output; do not infer it from the exit code alone when the tool prints warnings.
3. Compare the result with each acceptance criterion. A criterion without a check is not verified; say so.

## Report what you weakened

List by name, even if you think it was justified:

- tests skipped, deleted or marked flaky;
- assertions loosened, timeouts or retries increased;
- warnings, lint rules or type errors silenced;
- error handling that now swallows an exception;
- TODOs or partially wired features left behind.

If the list is empty, say "nothing weakened".

## Bugs

A bug counts as fixed only when there is a test or reproducible check that **failed before** the fix and **passes after** it. Show both.

## When something cannot be verified here

Some checks need a device, a signed build, credentials or production-like data. Do not pretend they ran. State which check is pending, why, and the exact command or steps the human should run.

## Output format

```
Verified:
- <criterion or check> — <command> — <result>
Not verified:
- <check> — <reason> — <how to run it>
Weakened: <list, or "nothing weakened">
```

## Known failures

_Record real mistakes here with a date and the rule that prevents them._
