@AGENTS.md

## Claude Code only

- Load session context through a SessionStart hook if your team configures one (for example `<TASK_TRACKER_PRIME_COMMAND>`). If the context is missing, run that command once.
- Track tasks with `<TASK_TRACKER>`, not the built-in task or todo tools.
- Knowledge: follow "Where knowledge goes" in AGENTS.md. Do not save project knowledge to auto memory; teammates cannot see it.
- Use plan mode before you change anything under `<CORE_PATH>`.
- A Stop hook can run `<CHECK_COMMAND>` when source files change. If it blocks you, fix the cause. Never weaken a check to make it pass.
- When compacting, keep: the task id, the list of modified files, the last `<CHECK_COMMAND>` result, and the `AI/` notes you edited.
