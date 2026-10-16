---
name: agent-reference
description: Detailed engineering standards, evidence formats, and tool guidelines for agents.
type: reference
area: root
---

# Agent reference

This document contains detailed engineering standards, reporting rules, and tool guidelines for coding agents.
Every agent follows these rules when developing in this repository.

## Implementation standards

Apply these standards before and during any code change:

- Prefer the simplest correct implementation consistent with the existing architecture.
- Preserve domain boundaries, type safety, security, and maintainability.
- Avoid generic abstractions without a concrete reuse requirement.
- Do not introduce new dependencies when existing tools solve the problem.
- Do not invent requirements, tests, commands, files, or system behavior.
- Follow existing conventions unless a change is technically justified.
- Keep implementation and documentation proportional to the actual task.
- Prune unused code: delete files, exports, CSS, dependencies, and scripts that become unused in your change.
- Verify dead code with grep before deletion.
- Retain migrations, seed data, tool config, and anything you cannot prove dead.

## Review and verification

Complete these steps before you report a task done:

1. Run the review skills (for example `code-review`) for code changes.
2. Run `<CHECK_COMMAND>` and tests for the changed behavior.
3. Verify that the change satisfies the original requirements.
4. Confirm that documentation and referenced paths remain accurate.
5. Report failed checks and limitations.

## Skill usage evidence

Every implementation report must include these sections:

- **Skills discovered:** list the relevant skills available in your environment.
- **Skills invoked:** list each skill with its invocation method (tool call or file path read).
- **Plugin status:** list active plugins and hooks.
- **Validation:** list each verification command and its exit code.
- **Limitations:** list missing integrations, missing dependencies, or missing skills.

Report a skill as invoked only when a tool call or file read occurred.
The orchestrator rejects reports that lack invoked skill evidence.

## Serena MCP

Serena MCP is optional.
The owner does not mandate Serena.
Use Serena only for symbol-level operations:

- Impact analysis.
- Symbol moves.
- Symbol renames (`lsp.rename_symbol`).
- Symbol deletions with references (`lsp.safe_delete_symbol`).
- Symbol inspection (`lsp.get_symbols_overview`, `lsp.find_symbol`, `lsp.find_referencing_symbols`).

Do not use Serena for text, configuration files, SQL migrations, or documentation.
Use `grep` and file read tools for text, config, SQL, and documentation.
When using Serena, call `initial_instructions` first to activate the project.
Workers use Serena only if their tool environment provides it.
State in your report if you used Serena, and list the tools called.

## Skills and tooling details

- Load only the skills your task needs. Each extra skill consumes context.
- If a required skill is not installed in your tool, notify the orchestrator.
- Use `<TASK_TRACKER>` for task tracking: create an issue before work, claim it, and close it with a reason.

## Related

- [[AI/index]]: Entry point: pick the area you will change and follow one link.
- [[AI/documentation-rules]]: When to edit or create an AI note, note types, frontmatter and linking rules.
- [[AGENTS]]: Core agent guide and required workflow.
