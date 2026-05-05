# Copilot Base Instructions

A reusable baseline instruction set for GitHub Copilot (and compatible AI assistants). Drop it into any repository and trim or extend it as needed.

**Files in this repo:**
- `copilot-instructions.md` - the instruction file read by the AI
- `startup.md` - a per-repository override template

---

## What this does

When placed at `.github/copilot-instructions.md` in a repository, this file is automatically picked up by GitHub Copilot. It shapes how the AI responds: what conventions it follows, what it avoids, and how it handles edits.

The instructions are written for the AI, not for humans. This README is the human-facing summary.

---

## Key rules at a glance

### Behavior
- Concise, impersonal output. No filler phrases.
- Explicit over implicit. No assumptions about intent.

### Encoding - treated as critical
- All files are UTF-8 by default.
- Encoding must be preserved through every edit. The AI is required to verify no corruption occurred before finishing any change.
- This matters most in PHP, CSS, and C# files with non-ASCII content.

### File editing
- The AI must use direct file-editing tools only. No terminal scripts, no sed/awk, no bulk automated edits.
- Every change must be visible in a diff.
- No automatic git operations (no commits, pushes, or branch changes without being explicitly asked).

### Code quality
- Write idiomatic code that fits the language and framework.
- Names must be self-explanatory. Avoid generic names like `data`, `temp`, `result`.
- Split complex conditions into named intermediate variables.
- Linters handle formatting. The AI focuses on semantics and clarity.

### Code changes
- Only change what was asked for. No drive-by refactors.
- No features, comments, or error handling added for scenarios that cannot happen.
- Simplest solution that fits the existing codebase.

### Security
- Parameterized queries for all user input. Always.
- Validate and sanitize at the system boundary.
- Never log passwords, tokens, PII, or session identifiers.

### Documentation
- Markdown files in `docs/` with a logical tree.
- User-facing docs: plain language, concrete examples, numbered steps for sequences.
- No implementation details in user docs - document behavior, not internals.

### Writing & prose style
- No AI-explainer cadence, TED-talk rhythm, or motivational phrasing.
- No repeated sentence stacks (multiple short declaratives followed by a colorful punchline). Combine related points into one sentence.
- No analogies or comparisons unless the user explicitly provides one. Keep user-provided comparisons close to their wording; do not expand them.

---

## Language-specific highlights

| Language | Key reminders |
|---|---|
| C# | Explicit types preferred; dispose `IDisposable`; avoid `.Result`/`.Wait()`; one class per file |
| WPF | Strict MVVM; bind via `{Binding}`; never block the UI thread |
| Dart/Flutter | Follow official style; prefer `final`/`const`; keep `build()` small; dispose controllers |

---

## Per-repository customization with startup.md

To use this in a new repository:

1. Copy `copilot-instructions.md` to `.github/copilot-instructions.md` in the target repository.
2. Copy `startup.md` to the root of the target repository (or `.github/startup.md`).

The AI runs `startup.md` because `copilot-instructions.md` explicitly tells it to check for and execute that file at the start of every session. Without `copilot-instructions.md` in place, `startup.md` does nothing on its own.

**Existing project:** The AI silently scans the repository, detects the language, framework, and directory structure, and writes a project-specific **Project File Structure** block into `copilot-instructions.md`. It also removes sections that do not apply (e.g. CSS rules for a CLI tool).

**New/empty project:** The AI asks a few clarifying questions (project name, type, language, constraints), then scaffolds the directory structure, creates a stub `README.md`, and updates `copilot-instructions.md` accordingly.

After initialization, the AI asks whether to delete `startup.md` or rename it to `startup.done.md` so it does not trigger again.

The result is a trimmed, project-aware `copilot-instructions.md` without you having to edit anything manually.

---

For the full rule set, read `copilot-instructions.md`.
