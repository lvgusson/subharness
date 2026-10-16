---
name: code-review
description: Self-review checklist for the code review role. Use it before you report a task done.
type: reference
area: jobs
---

# Code review checklist

Answer every item with yes, no or not applicable. Fix each no before you report done.

## Before

- [ ] Did you read the task, the issue and the acceptance criteria?
- [ ] Did you read the code around the change, and not only the diff?
- [ ] Did you run the change, or the tests that cover it?

## Correctness

- [ ] Does the change do what the issue asks, and nothing more?
- [ ] Does the logic handle empty, null, maximum and invalid input?
- [ ] Do error paths leave the data in a safe state?
- [ ] Does the code handle concurrent calls and retries?
- [ ] Do the types match the real data, with no unchecked cast?

## Design

- [ ] Is each new line needed?
- [ ] Does the change reuse existing code and not copy it?
- [ ] Does each name say what the thing is or does?
- [ ] Does each module keep a small interface and hide its details?
- [ ] Does `<UI_KIT_PATH>` stay free of imports from `<APP_PATHS>`?
- [ ] Does a change in `<CORE_PATH>` keep both apps green?

## Risk

- [ ] Does the change keep authorization checks and RLS intact?
- [ ] Does the code hold no secret, no debug code and no commented-out code?
- [ ] Can the change cause a slow query or a large bundle?
- [ ] Does each new dependency have a reason?
- [ ] Does a test cover each risky branch?

## Before you report done

- [ ] Did you write each finding with the file, the line, the problem and a fix?
- [ ] Did you rank the findings: must fix, should fix, optional?
- [ ] Did `<CHECK_COMMAND>` pass, and do you report the command and the result?
- [ ] Did you run `ponytail-review` and `code-review` for code changes?
