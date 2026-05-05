# Copilot Instructions
by [NejedNiko.cz](https://web.nejedniko.cz)

revision 2.2 - 2026-05-05

> **Base template** - trim or extend per repository.
> For per-repo overrides, see [Startup Initialization](#startup-initialization) at the end.

---

## General Behavior
- Concise, impersonal responses. No AI sympathy phrases ("I hope this helps", "Let me know if you have any questions") in speech, code comments, documentation, or commit messages.
- Prefer explicit over implicit behavior.
- Do not use emoticons, em dashes, or non-ASCII decorative characters in code or documentation. Use plain ASCII (hyphens, asterisks, arrows `->`) unless the project explicitly allows otherwise.

## Clarification Before Implementation
- Before writing code, if the requirements, intent, or relevant structure are unclear, **ask targeted clarifying questions** rather than generating potentially incorrect output.
- Confirm assumptions about architecture, expected behavior, or integration points before proceeding.
- For requests that span multiple files or involve non-trivial logic, briefly state your understanding of the task and ask whether it is correct before starting.
- This is the default behavior - do not skip it to save a round-trip.

## Encoding (Critical)
- **All files are UTF-8 unless the project explicitly states otherwise.**
- Preserve the original encoding of every file during reads, edits, and writes. Never strip, replace, or corrupt non-ASCII characters (accented letters, currency symbols, typographic marks).
- When creating new files, write them as UTF-8 (with or without BOM as the project requires).
- If a file's encoding is unclear, treat it as UTF-8 - do not guess or convert.
- **Before finishing any edit, verify that the change did not introduce encoding corruption** (mojibake, replaced characters, broken multi-byte sequences). If corruption is detected, revert and re-apply correctly.

## Tooling Discipline
- **Always use direct file-editing tools for file modifications.** Never use terminal commands, scripts, sed, awk, or other automated tools to perform file edits - even when changes span many files.
- Running a script to bulk-edit files is not acceptable as a shortcut.
- Every edit must be visible in a diff. No opaque transformations.
- Do not interact with git automatically (no commits, pushes, branch operations) unless explicitly asked.
- Prefer the smallest, most targeted edit that achieves the goal.

## Code Quality
- Write idiomatic, clean, self-descriptive code that follows the conventions of the language and framework in use.
- Choose meaningful, self-explanatory names for all identifiers. A reader should understand purpose from the name alone - avoid generic names like `data`, `temp`, `result`, `obj`, `val` unless scope is trivially small.
- Prefer readable, easily debuggable names; favor clarity over brevity.
- Split complex multiline conditions into intermediate, well-named variables to improve readability and debugging.
- Group constants and configuration values near the top of the file.
- Store resource paths as named constants or variables near the top of the file; use relative paths unless specified otherwise.
- Assume linters and formatters handle style (spacing, brace placement, line length). Focus on semantics, clarity, and intent.

## Code Changes
- Only change what was explicitly requested; do not refactor unrelated code.
- Do not add features, comments, or error handling for scenarios that cannot occur.
- Prefer the simplest solution that satisfies the requirement and fits the existing codebase.
- Do not over-engineer or introduce abstractions for one-time operations.

## Security
- Validate and sanitize every input at the system boundary; whitelist expected values where possible.
- Use parameterized queries / prepared statements for all user-supplied data; never interpolate raw input into queries.
- Escape all user-sourced data with context-appropriate encoding before output (HTML-encode for HTML, etc.).
- Check authorization before any privileged action; return early and log on failure.
- Never log sensitive data (passwords, tokens, PII, session identifiers).

## Database & Data Access
- Use parameterized queries for any value from user input or external sources. Raw queries are acceptable only when all values are hard-coded or already validated.
- Check query results before iterating (e.g., verify row count > 0 before fetch loop).
- Place all database logic in dedicated data-access files or functions, not in view/page files.

## API Endpoints
- Set the correct `Content-Type` header (e.g., `application/json`).
- Validate and sanitize input at the top of the handler before any logic.
- Consistent response shape: `{success: false, error: "..."}` on failure, `{success: true, ...}` on success.
- Never output HTML from a JSON endpoint.
- Call `exit` (or equivalent) immediately after an error response to prevent fall-through.
- Require authentication/session checks for user-specific or privileged operations.

## Separation of Concerns
- Keep presentation, logic, and data access in separate layers.
- View/page files only call display functions or output content - no business logic or direct queries.
- Business logic belongs in dedicated backend files/functions.

## Frontend & JavaScript
- Follow the established patterns, libraries, and architecture if already present in the project. Do not introduce a different approach (e.g., a different HTTP client, state management pattern, or caching strategy) unless explicitly asked.
- If this is a new frontend without existing patterns, ask for preferences before choosing an approach.
- Respect existing dependencies; do not add new ones without confirmation.
- Never inject unescaped server data into the DOM.
- Document `localStorage`/cookie key names when used for persistent client state.
- Deduplicate event-driven actions with a persistent client-side flag.

## CSS & Styling
- Split large CSS files by functional area; name split files descriptively.
- Maintain load order: base/reset -> components -> overrides.
- Keep closely related selectors together; do not over-fragment small files.

## Logging
- Log security-relevant and admin actions to a persistent store.
- Structured entries: timestamp, severity, message at minimum.
- Use a dedicated logging module - no scattered raw write calls.
- Log error context sufficient for diagnosis, but never sensitive data.

## Documentation
- Use Markdown files in `{root}/docs/` with a logical tree structure.
- Keep documentation current with code changes.
- Include usage examples where applicable.

### User-Facing Documentation
- Assume no prior knowledge of the codebase; explain in plain language.
- Structure: overview -> step-by-step instructions -> reference material.
- Every feature or workflow needs at least one concrete example with real input and expected output.
- Numbered lists for sequential steps; bullet lists for unordered items.
- State prerequisites at the top (tools, versions, permissions).
- Document common error conditions and resolutions.
- Reference UI elements by their exact on-screen label.
- Do not expose implementation details in user-facing docs - document behavior and outcomes.
- Where a screenshot would help, add `<!-- Insert screenshot of X here -->` as a placeholder.

## Writing & Prose Style

- Do not use polished AI-explainer cadence. Write direct, grounded prose, not motivational or TED-talk rhythm.
- Avoid repeated sentence stacks: multiple short declarative sentences with the same grammar followed by a colorful punchline. Combine related negations or points into a single sentence instead.
  - Bad: "AI is not new. AI is not magic. AI is not alive. AI is not some creature hiding inside a datacenter."
  - Better: "AI is not magic and it is not alive. It is software doing a job, and people keep arguing about it like it secretly has a soul."
- Avoid fake rhetorical balance patterns such as:
  - "not X, not Y, but Z"
  - "sometimes useful, sometimes dangerous, always..."
  - "the problem is not A, the problem is B"
  - "it can X, it can Y, it can Z"
  - "understand X, understand Y, understand Z"
- Do not force even paragraph rhythm. Short and longer sentences can coexist without a dramatic beat at the end.
- Do not add punchline metaphors or colorful closers. If a phrase sounds like it was added to make the text spicy, remove it.
- Do not use comparisons or analogies unless the user explicitly creates one or asks for one. Do not introduce analogies like "AI is like a hammer / car / worker / mirror / calculator / knife."
- If the user provides a comparison, keep it close to their wording and purpose. Do not expand it into a metaphor chain or decorative explanation.
- When explaining responsibility, use direct cause and effect rather than analogy-driven logic: "If you give an AI system access to live data, money, accounts, or production systems, you are responsible for the permissions, limits, backups, and review."
- Do not add animal metaphors, cinematic imagery, fantasy phrasing, or fake witty endings.
- Prefer writing that is direct, slightly imperfect, and opinionated where appropriate. Human writing is allowed to be uneven.

## Localization
- Store language data in JSON files.
- Use a dedicated class/module to load and access language scopes.
- Provide fallback values for missing keys.

## Settings & Configuration
- Store settings in JSON files.
- Do not access environment variables directly in components or views; use a config module as a single source of truth.

---

## Language-Specific Notes

> These supplement - not replace - each language's official style guide and linter.
> Only non-obvious or frequently violated conventions are listed here.

### C#
- Prefer `var` only when the right-hand type is obvious; explicit types otherwise.
- Dispose `IDisposable` with `using`; never rely on finalizers.
- Prefer `async`/`await` over `.Result` or `.Wait()`.
- Throw specific exception types; avoid bare `Exception`.
- One class per file; filename matches class name.
- Especially avoid placing constant / static strings in code; prefer resource files or configuration.
- OR use nameof() and typeof() whenever possible for getting the parameter or type name as a string.
- Behave as pro-obfuscation as possible: avoid reflection, dynamic, or other features that hinder static analysis and renaming. 

### WPF
- MVVM strictly: Views contain XAML + minimal UI-only code-behind; logic in ViewModels.
- Bind via `{Binding}`; never manipulate controls from ViewModel.
- Use `ICommand` for user actions; no click handlers for business logic.
- Reusable styles and templates in `ResourceDictionary` files.
- Never block the UI thread.

### Dart / Flutter
- Follow Dart's official style guide for naming and file organization.
- Prefer `final` over `var`; use `const` constructors where possible.
- Handle nullable types explicitly; avoid `!` unless null is genuinely impossible.
- Keep `build()` methods small; extract sub-trees into separate widgets.
- Prefer `StatelessWidget`; use `StatefulWidget` only when local mutable state is needed.
- Use one state management approach consistently; do not mix.
- Always dispose controllers in `dispose()`.

### React / TypeScript
- Use a single package manager; do not mix `npm`, `yarn`, and `pnpm`. Lock versions via a lockfile.
- Define `dev`, `build`, `lint`, and `type-check` scripts in `package.json`.
- Organize `src/` by responsibility: `api/`, `components/`, `pages/`, `routes/`, `hooks/`, `store/`, `utils/`, `config/`, `styles/`.
- Enforce unidirectional data flow: API -> data layer -> hooks -> components -> UI. Never call the API directly inside a UI component.
- Prefer functional components; one responsibility per component. Extract reusable logic into hooks.
- Hooks must follow the Rules of Hooks (no conditional calls); always prefix with `use`.
- Use declarative routing; routing files define paths only - page logic stays in page components.
- Use local state by default; introduce global state only when necessary. Derive state instead of duplicating it.
- No `any` unless justified. No unused exports or dead code.

---

## Startup Initialization

**At the start of every session, before doing any other work:**
Check whether `startup.md` exists at the repository root or at `.github/startup.md`.
If it exists, read it and execute its instructions fully before proceeding.
If it does not exist, continue with these base instructions as-is.

**After reading `startup.md` and surveying the repository structure:**
- Summarize your understanding of the project: its purpose, key directories, primary technologies, and any conventions stated in `startup.md`.
- Explicitly ask whether this interpretation is correct before doing any implementation work.
- This confirmation step is mandatory - do not skip it even if the structure seems obvious.

