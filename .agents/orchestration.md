# Orchestration (orchestrator only)

Only the orchestrator reads this file. A worker follows `AGENTS.md` and its task prompt.

The orchestrator plans, delegates, reviews and reports. Workers are subagents or interactive CLIs in tmux panes. `.agents/orchestrate.sh` starts the panes. `.agents/pane.sh` is the only way to touch them. Edit both scripts to match the CLIs you use.

## Model table

Fill this table with the models you use. Write the tier as your own policy, not as a benchmark.

| Tool: model     | Use it for                          | Tier                      |
| --------------- | ----------------------------------- | ------------------------- |
| <tool: model A> | Advisor: review, plans, hard decisions | Strong, slow, high cost |
| <tool: model B> | Orchestrator and implementation     | Medium                    |
| <tool: model C> | Read-only audits and search         | Weak, fast, low cost      |

## Decision rules

- Do not delegate small edits, work with secrets or steps that need the owner's approval.
- A subagent takes a short task and sends back one report.
- Give each worker its files. Two workers never own the same file.
- The reviewer uses a different model from the author.
- A change under `<CORE_PATH>`: plan first, then every consumer must be green.

## Pane protocol

1. Write the task to a scratch file outside the repository. Start with the standards, the files the worker owns, the acceptance check and the memory paragraph from [[AI/memory/session-format]]. End with: `When finished, print exactly "ORCH-DONE <agent>" alone on the last line.`
2. Run `pane.sh send <pane> <file>`, then `pane.sh wait <pane> <agent>`. Read progress with `pane.sh read <pane>`.
3. Review the real result, not the claim: `git diff`, the task check and `<CHECK_COMMAND>`.
4. If the result is wrong, send a fix request to the same pane. Say exactly what failed.
5. If a pane shows an approval, login or trust prompt, tell the owner and wait. Never approve for the owner.

## Consolidation report

When a process ends, tell the owner in the same turn. Run the check first. Use this template:

1. Result: one sentence: done, failed or partial.
2. What changed: files and their count.
3. Checks: the exact command and its exit code.
4. Problems and limits.
5. What the owner decides, if anything.
6. Next step.
