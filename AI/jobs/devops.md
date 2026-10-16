---
name: devops
description: Self-review checklist for the devops role. Use it before you report a task done.
type: reference
area: jobs
---

# DevOps checklist

Answer every item with yes, no or not applicable. Fix each no before you report done.

## Before

- [ ] Did you check which environments the change reaches: preview, staging, production?
- [ ] Do you know how to roll the change back?

## Pipeline

- [ ] Does CI run install, lint, typecheck, test and build?
- [ ] Does CI use `<LOCKED_INSTALL_COMMAND>`?
- [ ] Is the Node version and the <PACKAGE_MANAGER> version fixed in one place?
- [ ] Does CI cache the <PACKAGE_MANAGER> cache?
- [ ] Do Playwright tests run in CI against a preview or a local build?
- [ ] Does a failed check block the merge?
- [ ] Does a workflow limit its token permissions to the minimum?

## Deploy

- [ ] Does the branch flow stay as written in the Git policy in `AGENTS.md`?
- [ ] Does each pull request get a preview deployment?
- [ ] Does the deploy config file hold only what the dashboard cannot hold?
- [ ] Does the build output stay deterministic with the same commit?
- [ ] Do migrations run before the code that needs them, and in a safe order?
- [ ] Does a deploy keep the previous version available for rollback?

## Configuration

- [ ] Does each new environment variable exist in every environment that needs it?
- [ ] Does each environment variable appear in `.env.example`?
- [ ] Do you keep secrets out of build logs?

## Before you report done

- [ ] Did you run the changed script or workflow, or a dry run of it?
- [ ] Do the deployment logs show no error?
- [ ] Did you update the how-to note for the changed process?
- [ ] Did `<CHECK_COMMAND>` pass?
