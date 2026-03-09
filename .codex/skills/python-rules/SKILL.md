---
name: python-rules
description: Use this skill when implementing or reviewing Python code to enforce typing, exception handling boundaries, and string interpolation conventions.
---

# Python Rules

## When To Use
- Use for Python implementation or review tasks.
- Do not use for non-Python codebases.

## Rules
- Must provide type hints for parameters and return values on all newly added or modified functions;
  test-only helper functions may be exempt.
- Must not use `except:` (bare except);
  catch specific exception types;
  use `except Exception` only at explicit application boundaries with concrete handling.
- For string interpolation involving variables, use f-strings.
- Use top-level imports by default;
  do not use lazy imports inside functions or methods unless the user explicitly requests an exception.
