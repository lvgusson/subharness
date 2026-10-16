# subharness

A project-agnostic template that gives coding agents memory, behavior rules and a way to document what they learn. Copy it into a new repository and fill in the placeholders.

## What is in it

```text
CLAUDE.md                 pointer to AGENTS.md plus a Claude-only section
AGENTS.md                 shared rules: writing rule, map, commands, workflow, git policy
AI/                       knowledge base (an Obsidian vault)
  index.md                entry point for agents
  documentation-rules.md  when to edit or create a note, note types, frontmatter, linking
  agent-reference.md      implementation standards and report evidence format
  memory/                 session memory: recall, compaction, format, _template/
  decisions/              decision records (ADR template)
  patterns/               design pattern notes (empty, with a template)
.agents/
  skills/                 generic agent skills, copied as-is from public sources
  orchestration.md        optional multi-agent orchestration rules
  orchestrate.sh, pane.sh optional tmux helpers (edit to match your CLIs)
```

## How to copy it into a new project

1. Copy `CLAUDE.md`, `AGENTS.md`, `AI/`, `.agents/` and `.gitignore` into the root of your repository.
2. Search for placeholders: `grep -rn "<[A-Z_]*>" . --include="*.md" --include="*.sh"`.
3. Replace `<PROJECT_NAME>`, `<PACKAGE_MANAGER>`, `<TEST_COMMAND>` and `<CHECK_COMMAND>` with your values.
4. Replace `<TASK_TRACKER>` and its commands with your tracker, or remove those lines.
5. Fill the `Map` table and the `Git policy` section in `AGENTS.md`.
6. Add your first area hub under `AI/` and link it from `AI/index.md`.
7. Delete `.agents/orchestration.md`, `orchestrate.sh` and `pane.sh` if you use one agent only.
8. Commit. Open a new agent session and ask it to read `AGENTS.md`.

## How the memory and knowledge loop works

1. The agent reads `AI/index.md`, then one area hub, then one note.
2. The agent changes the code. If a note contradicts the code, the agent trusts the code and fixes the note.
3. The agent records what it learned in the right place (table "Where knowledge goes" in `AGENTS.md`):
   - a convention or how-to goes into an `AI/` note;
   - remaining work goes into the task tracker;
   - progress of a multi-agent session goes into `AI/memory/<session>/`.
4. Session memory uses one writer for each file and append-only logs. `state.md` stays short.
5. After a context clear, the agent follows `AI/memory/recall.md` and reads `state.md` first.
6. Before a clear, the orchestrator follows `AI/memory/compaction.md` to merge logs into `state.md`.
7. Pull request review keeps the notes correct.

## How to expand it

- New area: create `AI/<area>/<area>.md` as a hub (type `hub`). Link it from `AI/index.md`.
- New note: follow `AI/documentation-rules.md`. Edit an existing note first. Keep notes under 150 lines. Link both ways.
- New decision: copy `AI/decisions/0000-template.md` and number the copy.
- New pattern: add a note in `AI/patterns/` from the template in its README.
- New skill: add `.agents/skills/<name>/SKILL.md` (see the `writing-for-agents` skill). Add it to the skills table in `AGENTS.md`.
- New session: copy `AI/memory/_template/` as `AI/memory/<YYYY-MM-DD>-<slug>/`.
- Tool-specific files: add one pointer file for each tool (for example `GEMINI.md`) that imports `AGENTS.md`.

## Credits

The skills in `.agents/skills/` come from public sources (see `.agents/skills/pr/CREDITS.md`). They are not modified, except one word in `diagnosing-bugs`.
