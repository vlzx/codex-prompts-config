# AGENTS.md
<!-- zh: 代理规则 -->

## Scope
<!-- zh: 适用范围 -->
- This file applies to the current repository root (the directory containing this `AGENTS.md`) and all subdirectories.

## Must / Must Not
<!-- zh: 必须与禁止 -->
- Must not modify paths listed in `Protected Paths`.

## Protected Paths
<!-- zh: 受保护路径 -->
### Forbidden Directories
<!-- zh: 禁止修改的目录 -->
- `data/`
- `logs/`

### Forbidden Files
<!-- zh: 禁止修改的文件 -->
- `.env`

## Operation Guardrails (Strict)
<!-- zh: 严格操作护栏 -->
- Unless the user explicitly requests code changes, stay in analysis-only mode.
- In analysis-only mode, do not create/modify/delete any files.
- Never modify paths listed in `Protected Paths` under any circumstance.

### File Edits
<!-- zh: 文件编辑 -->
- Allowed only when the user explicitly asks for implementation/code edits.
- Keep edits minimal, scoped to requested files/lines.
- Do not perform repository-wide refactors unless explicitly requested.

### Formatting / Auto-fix
<!-- zh: 格式化与自动修复 -->
- Do not run formatters or auto-fix tools by default.
- Allowed only if:
  - the user explicitly asks, or
  - formatting is required to pass an explicitly requested check.

### Dependencies / Network
<!-- zh: 依赖与网络 -->
- Do not install/update dependencies without explicit user confirmation.
- Do not fetch remote resources without explicit user confirmation.

### Validation / Commands
<!-- zh: 验证与命令 -->
- If validation is useful, suggest commands first.
- If the user explicitly asks to run checks/tests/build, execute directly and report results.

### Git Safety
<!-- zh: Git 安全 -->
- Do not run destructive git commands (e.g. `git reset --hard`, `git checkout --`, force push) unless explicitly requested.
- Do not amend commits unless explicitly requested.

### Conflict Priority
<!-- zh: 冲突优先级 -->
- Instruction precedence: System > Developer > AGENTS.md > User preference.
- If a request conflicts with higher-priority rules, stop and ask for clarification.

## Interaction Language
<!-- zh: 交互语言 -->
- Must reply to the user in Chinese by default.
- If the user explicitly requests another language, follow the user's request.
- Keep code snippets, commands, and file paths in their original form.

## Engineering Principles
<!-- zh: 工程原则 -->
- Follow KISS (Keep It Simple, Stupid): prefer the simplest correct solution.
- Avoid unnecessary abstraction, speculative generalization, and over-engineering.
- If a complex solution is chosen, explain why simpler alternatives are not viable first.

## Language-Specific Rules
<!-- zh: 语言专项规则 -->
### Python
<!-- zh: Python 规则 -->
- For string interpolation involving variables, use f-strings.
- Must not use `except:` (bare except). Catch specific exception types; use `except Exception` only at explicit application boundaries with concrete handling.
- Must provide type hints for parameters and return values on all newly added or modified functions; test-only helper functions may be exempt.

## Default Workflow
<!-- zh: 默认流程 -->
- If user does not explicitly request code changes:
  - Analyze requirements.
  - Provide actionable implementation steps.
- If user explicitly requests code changes:
  - Implement the requested changes directly.
  - Follow `Operation Guardrails (Strict)`.
  - Summarize what changed and provide next steps.

## Validation Commands
<!-- zh: 验证命令 -->
- No mandatory validation commands are required by default.
- Use `Operation Guardrails (Strict) > Validation / Commands`.

## Output Contract
<!-- zh: 输出约定 -->
- Final response must include:
  - `改动摘要`
  - `下一步`
- Field placeholder policy:
  - For required fields, if a field has no applicable content, fill with `无`.
  - If work was intentionally not performed, state `未执行` plus a short reason.
  - For fields under `Include when applicable`, omit the field entirely when not applicable (do not output placeholders).
- Include when applicable:
  - `改动文件`
  - `风险与影响范围`
  - `回滚方案`
  - `假设与限制`
  - `建议验证`
  - `验证执行`
  - `验证结果`
  - `未执行项与原因`

## Fallback Rules
<!-- zh: 兜底规则 -->
- If requirements are ambiguous, make conservative assumptions and state them clearly.
- If a requested action conflicts with higher-priority instructions or this file's prohibitions, stop and ask for clarification.

## Last Updated
<!-- zh: 最后更新 -->
- 2026-03-02
