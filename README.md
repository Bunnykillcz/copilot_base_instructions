# Project Coding Guidelines — Summary

This GitHub repository provides a compact set of coding and documentation guidelines intended as a baseline for any AI copilot. Its goal is to give every AI assistant a consistent, minimal set of instructions so suggestions are clear, safe, and easy to maintain across projects.

## Core Principles
- Keep language concise and impersonal.
- Prefer explicit behavior over implicit assumptions.
- Favor readability and maintainability over cleverness.

## Naming & Structure
- Use `snake_case` for functions and variables; `ALL_CAPS` for constants/ENUMs.
- Place class-level constants and defaults at the top of a class/file.
- Initialize all class attributes explicitly.

## Variables & Conditions
- Use descriptive, easily debuggable variable names — clarity over brevity.
- Split complex, multiline conditions into intermediate, well-named variables and then combine them in the final condition.

## Functions & Methods
- Add docstrings for functions with side effects or file I/O.
- Use `@classmethod` and `cls` for class methods when appropriate.

## Project Layout
- Follow the recommended directory layouts for web, desktop, mobile, CLI, and libraries (keep code, tests, docs separate).

## Documentation & User Docs
- Write documentation in Markdown, keep it up to date, and include concrete examples.
- Use numbered lists for sequences and bullets for unordered items.
- Avoid em dashes; use a simple hyphen (-).

## Code Changes & Editing
- Only change what was requested; avoid unrelated refactors.
- Prefer the simplest solution that satisfies the requirement.
- Do not use scripts to bulk-edit files; edit files directly.

## Security & Logging
- Validate and sanitize all external inputs; use parameterized queries.
- Never log sensitive information (passwords, tokens, PII).
- Use structured logs with timestamp, severity, and message.

## Language-Specific Highlights
- C#: PascalCase for types/methods; prefer `readonly` and `async/await` patterns.
- Dart/Flutter: follow official style; prefer `final`/`const`, keep `build()` small, and dispose controllers.

## Quick Reminder
- Preserve file encoding (UTF-8) and avoid changing special characters when editing files.

For the full rules and examples, see `copilot-instructions.md`.
