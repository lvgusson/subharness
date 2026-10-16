# <PROJECT_NAME>: agent guide

Shared instructions for every coding agent. Claude Code loads this through `CLAUDE.md`.

## Supreme rule: Simplified Technical English

ASD-STE100 ([asd-ste100.org](https://asd-ste100.org/about_STE.html)) applies to all agents, models and providers.

- Write the result first. One idea per sentence (max 20 words in a procedure step, 25 in a description).
- Use active voice and simple present tense.
- Use one word for one meaning. Do not use filler words, idioms or undefined jargon.
- Use numbered steps for procedures and bullet lists for items.
- Files and notes in <FILE_LANGUAGE>. Reply to the owner in <OWNER_LANGUAGE> with the same principles.

## Map

Replace these rows with your own layout. Keep one row for each top-level area.

| Path          | What it is          | Rule                                 |
| ------------- | ------------------- | ------------------------------------ |
| `<PATH_1>`    | <what it is>        | <rule, for example "no imports from X"> |
| `<PATH_2>`    | <what it is>        | <rule>                               |

## Commands

```bash
<PACKAGE_MANAGER> install     # after pulling or changing dependencies
<TEST_COMMAND>                # all tests
<CHECK_COMMAND>               # required gate: run before you report a task done
```

## Knowledge base (`AI/`)

`AI/` is an Obsidian vault at the repository root (`[[AI/foo]]` = `AI/foo.md`). Open `AI/index.md` before you change code. Read the one note that answers your task. Follow `## Related` only if needed. If a note contradicts code, trust code and fix the note in the same change.

## Workflow

1. Pick work from `<TASK_TRACKER>` and claim it.
2. Load the skills before you read or edit any file (see "Skills policy"): `ponytail` first, then the skill for your task type.
3. Read the matching `AI/` note.
4. Make the change.
5. Run `ponytail-review` and `code-review` (code changes only), then the role checklists in `AI/jobs/index.md`.
6. Run `<CHECK_COMMAND>`. It must pass. Report the command and its result, not just "done".
7. Update the knowledge base (below).
8. Close out the task in `<TASK_TRACKER>`.

## Where knowledge goes

| You learned...                                      | Put it in                            |
| --------------------------------------------------- | ------------------------------------ |
| How the codebase works, a convention, a how-to      | An `AI/` note (team-reviewed in PRs) |
| Work still to do, a bug, a follow-up                | `<TASK_TRACKER>` issue               |
| A short operational fact future agent sessions need | `<TASK_TRACKER_REMEMBER_COMMAND>`    |
| Progress of one multi-agent session                 | `AI/memory/<session>/`               |

## No stray files

Never create `.md` files outside `AI/`. Exceptions: `.agents/` orchestration, root `README.md`, `AGENTS.md`, `CLAUDE.md`. Reports and summaries belong in your final message, not in files. Task state goes in the tracker. Keep `AI/` connected (`AI/documentation-rules.md`): edit existing notes first, keep notes under 150 lines, and link both ways.

## Role

Worker by default (ignore `.agents/orchestration.md`). Orchestrator only when specified: read `.agents/orchestration.md`.

## Skills policy

Task skills (Matt Pocock set) live in `.agents/skills/<name>/SKILL.md`. Load the skill for your task type before you read or edit files. If your tool has no Skill tool, read the `SKILL.md` file and follow it.

Ponytail skills come from a plugin, not from this repository. Path: `<PONYTAIL_PATH>/skills/<name>/SKILL.md` (example: `~/.claude/plugins/marketplaces/ponytail`). If the plugin is not installed, skip these three and say so in your report.

- `ponytail`: load before any code change.
- `ponytail-review`: run before you report code work done.
- `ponytail-audit`: use for read-only audits of a whole repository.

| Task type                         | Skill                    |
| --------------------------------- | ------------------------ |
| New behavior, or a fix with tests | `tdd`                    |
| Bug                               | `diagnosing-bugs`        |
| Structure, moves, interfaces      | `codebase-design`        |
| Vocabulary or ADR                 | `domain-modeling`        |
| A plan or a decision              | `grilling`               |
| An edit to `AGENTS.md` or a skill | `writing-for-agents`     |
| A pull request body               | `pr`                     |
| Research with sources             | `research`               |
| Review of a change                | `code-review`            |

- Implementation standards: follow [[AI/agent-reference#Implementation standards]].
- Review and evidence: format your report per [[AI/agent-reference#Skill usage evidence]].

## Git policy

Replace this section with your branch flow. Example structure:

1. Work on a branch `<BRANCH_PREFIX>/<task-id>-<slug>`, created from `<BASE_BRANCH>`.
2. Commit and push only your own branches.
3. Run `<CHECK_COMMAND>` green, then open a pull request to `<BASE_BRANCH>`.
4. Leave `<PROTECTED_BRANCHES>` to the owner: no merge, no push, no force, no reset.
