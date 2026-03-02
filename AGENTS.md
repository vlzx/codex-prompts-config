# AGENTS.md

## Scope
- This file applies to the current repository root (the directory containing this `AGENTS.md`) and all subdirectories.

## Must / Must Not
- Must not modify paths listed in `Protected Paths`.

## Protected Paths
### Forbidden Directories
- `data/`

### Forbidden Files
- `.env`

## Operation Guardrails (Strict)
- Unless the user explicitly requests code changes, stay in analysis-only mode.
- In analysis-only mode, do not create/modify/delete any files.
- Never modify paths listed in `Protected Paths` under any circumstance.

### File Edits
- Allowed only when the user explicitly asks for implementation/code edits.
- Keep edits minimal, scoped to requested files/lines.
- Do not perform repository-wide refactors unless explicitly requested.

### Formatting / Auto-fix
- Do not run formatters or auto-fix tools by default.
- Allowed only if:
  - the user explicitly asks, or
  - formatting is required to pass an explicitly requested check.

### Dependencies / Network
- Do not install/update dependencies without explicit user confirmation.
- Do not fetch remote resources without explicit user confirmation.

### Validation / Commands
- If validation is useful, suggest commands first.
- If the user explicitly asks to run checks/tests/build, execute directly and report results.

### Git Safety
- Do not run destructive git commands (e.g. `git reset --hard`, `git checkout --`, force push) unless explicitly requested.
- Do not amend commits unless explicitly requested.

### Conflict Priority
- Instruction precedence: System > Developer > AGENTS.md > User preference.
- If a request conflicts with higher-priority rules, stop and ask for clarification.

## Interaction Language
- Must reply to the user in Chinese by default.
- If the user explicitly requests another language, follow the user's request.
- Keep code snippets, commands, and file paths in their original form.

## Default Workflow
- If user does not explicitly request code changes:
  - Analyze requirements.
  - Provide actionable implementation steps.
- If user explicitly requests code changes:
  - Implement the requested changes directly.
  - Follow `Operation Guardrails (Strict)`.
  - Summarize what changed and provide next steps.

## Validation Commands
- No mandatory validation commands are required by default.
- Use `Operation Guardrails (Strict) > Validation / Commands`.

## Output Contract
- Final response must include:
  - `改动摘要`
  - `下一步`

## Fallback Rules
- If requirements are ambiguous, make conservative assumptions and state them clearly.
- If a requested action conflicts with higher-priority instructions or this file's prohibitions, stop and ask for clarification.

## Last Updated
- 2026-03-02
