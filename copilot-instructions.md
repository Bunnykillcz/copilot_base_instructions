# Copilot Instructions
### by [NejedNiko.cz](https://web.nejedniko.cz)

## General Style
- Use concise, impersonal responses.
- Prefer explicit over implicit behavior.
- Avoid common AI sympathy in speech.

## Classes (general)
- Place class-level constants and defaults at the top.
- Explicitly initialize all class attributes.
- Prefix internal-use classes with an underscore.

## Functions & Methods (general)
- Use snake_case for function/method names.
- Add docstrings for functions with side effects or file I/O.
- Use @classmethod and 'cls' for class methods.
- Keep utility functions outside classes unless they modify class state.

## Variables (general)
- Use snake_case for variables.
- Use ALL_CAPS for constants and ENUMs.
- Group related variables at the top of the file.
- Use descriptive names for paths/configuration variables.

## File Paths & Resource Management (general)
- Store resource paths as variables at the top of the file.
- Use relative paths for resource files unless specified otherwise.

## Settings & Configuration (general)
- Store settings in JSON files.

## Project File Structure

### Web Application
```
{root}/
  assets/                               - static files (images, fonts, icons)
  templates/{template_name}/            - stylesheets
  javascript/                           - client-side scripts
  pages/                                - page content files
  api/                                  - server-side API endpoints
  func/                                 - backend business logic and utility functions
  cache/                                - generated/cached output files
  docs/                                 - documentation
  config/                               - configuration files (not committed if sensitive)
```

### Windows Desktop Application (WPF / WinForms)
```
{root}/
  Assets/         - images, icons, embedded resources
  Models/         - data models and entities
  ViewModels/     - ViewModels (MVVM) or presenters
  Views/          - windows, user controls, pages (XAML or designer files)
  Services/       - business logic, data access, external integrations
  Helpers/        - small utility classes and extension methods
  Config/         - app configuration files
  docs/           - documentation
```

### Mobile Application (Flutter / Android / iOS)
```
{root}/
  lib/            - application source code
    models/       - data models
    screens/      - full-page UI screens
    widgets/      - reusable UI components
    services/     - business logic, API calls, data access
    providers/    - state management (providers, blocs, etc.)
    utils/        - utility functions and helpers
  assets/         - images, fonts, static files
  test/           - unit and widget tests
  docs/           - documentation
```

### Game
```
{root}/
  src/            - game source code
    entities/     - game objects (player, enemies, items)
    systems/      - game logic systems (physics, AI, input, rendering)
    screens/      - menus, HUD, game over screens
    utils/        - helper functions and shared utilities
  assets/
    sprites/      - 2D artwork and textures
    audio/        - music and sound effects
    fonts/        - font files
    maps/         - level and map data
  config/         - game settings and constants
  docs/           - documentation
```

### CLI Tool / Script
```
{root}/
  src/            - source code (commands, logic)
  config/         - default configuration files
  tests/          - automated tests
  docs/           - documentation
  README.md       - quick-start and usage reference
```

### Library / Package
```
{root}/
  src/            - public library source code
  tests/          - unit and integration tests
  examples/       - standalone usage examples
  docs/           - API reference and guides
  README.md       - overview, installation, and quick example
```

## Language & Localization (general)
- Store language data in JSON files.
- Use a dedicated class to load/access language scopes.
- Provide fallback values for missing keys.

## Documentation (general)
- Use md files for documentation.
- Include usage examples where applicable.
- Keep the documentation up to date with code changes.
- Keep the documentation in {root}/docs/ directory using a tree structure fitting the theme of the documentation. 
    For example, if the documentation is about a project with multiple modules, create subdirectories for each module and place the relevant documentation files within those subdirectories.
- Never, in any documentation use long dashes (—) or em dashes (—). Always use hyphen (-) instead.
- Never, in any code or commentary, use long dashes (—) or em dashes (—). Always use hyphen (-) instead.
- Avoid common AI sympathy in any documentation, code comments, or code. Do not use phrases like "I hope this helps" or "Let me know if you have any questions". Instead, focus on providing clear and concise information without unnecessary pleasantries.
- Avoid using emoticons for icons in documentation or code comments. Instead, use descriptive text or standard symbols to convey meaning without relying on emoticons, which may not render correctly in all environments or encodings. You may use basic ASCII symbols like asterisks (*) for emphasis or arrows (->) for flow, but avoid any non-standard characters that could cause issues.
- Whenever you would feel like you need to use a little more complex, but still common characters, ask if that would be okay first. For example, if you want to use a bullet point list, you can ask "Would it be okay to use bullet points in the documentation using the "#" symbol as a bullet?" before proceeding.

## User Documentation (general)
- Write for the intended audience: assume no prior knowledge of the codebase; explain concepts in plain language.
- Structure docs with a clear hierarchy: overview first, then step-by-step instructions, then reference material.
- Every feature or workflow must have at least one concrete example showing real input and expected output.
- Use numbered lists for sequential steps; use bullet lists only for unordered items.
- One idea per sentence; keep sentences short and direct.
- In places where a screenshot would be helpful, include a placeholder comment like `<!-- Insert screenshot of X here -->` to indicate where it should go, and ensure the screenshot is added before finalizing the documentation. Ignore if the screenshot is present in the codebase already.
- State prerequisites explicitly at the top of any guide (required tools, versions, permissions, etc.).
- Document error conditions the user may encounter and how to resolve each one. (FAQ)
- When referencing UI elements, match the exact label shown on screen (e.g., click "Save Changes", not "save it").
- Do not document implementation details (how the code works internally) in user-facing docs; document behavior and outcomes only.
- Keep screenshots (ask if asset is up to date) or code blocks up to date; outdated visual content is worse than no visual content.

## Code Changes (general)
- Only change what was explicitly requested; do not refactor unrelated code unless asked to.
- Do not add features, comments, or error handling for scenarios that cannot occur.
- Prefer the simplest solution that satisfies the requirement and works with the existing codebase. Avoid over-engineering or adding unnecessary complexity.
- Never use terminal commands, scripts, or automated tools to perform file edits - not even when changes span many files or locations. Always apply every edit directly using file editing tools, one change at a time. Running a script to bulk-edit is not acceptable as a shortcut.

## Security (general)
- Validate and sanitize every input at the system boundary; whitelist expected values where possible.
- Use parameterized queries / prepared statements for all user-supplied input; never interpolate raw input into queries.
- Escape all user-sourced data with context-appropriate encoding before output (e.g., HTML-encode before inserting into HTML).
- Check authorization before any privileged action; return early and log the attempt on failure.
- Never log sensitive data (passwords, tokens, PII, session identifiers).

## Database & Data Access (web)
- Use parameterized / prepared queries for any value that originates from user input or external sources.
- Raw or trusted-internal queries are only acceptable when all values are hard-coded or already validated integers.
- Always check query results before iterating (e.g., verify row count > 0 before fetch loop).
- Place all database logic in dedicated data-access files or functions, not in view/page files.

## API Endpoints (web)
- Set the correct `Content-Type` response header (e.g., `application/json` for JSON APIs).
- Validate and sanitize every input parameter at the top of the handler before any logic runs.
- Return a consistent shape on all responses: `{success: false, error: "..."}` on failure, `{success: true, ...}` on success.
- Never output HTML from a JSON endpoint.
- Call `exit` (or equivalent) immediately after every error response to prevent fall-through.
- Require authentication/session checks for any user-specific or privileged operation.

## Separation of Concerns (server / web)
- Keep presentation (templates/styles), assembly/logic (controllers/partials), and content (pages/views) in separate layers.
- View/page files should only call display functions or output static content - no business logic or direct database queries.
- Business logic and data access belong in dedicated backend files/functions, not in view files.

## CSS & Styling (web design)
- Split large CSS files by functional area when they contain multiple distinct, independently maintainable sections.
- Name split files descriptively to make their scope immediately clear.
- Maintain load order so base/reset styles load before components, and components before overrides.
- Keep closely related selectors together; do not split styles that heavily interact with each other.
- Do not split styles that are too small or simple to warrant separate files, as this can lead to unnecessary fragmentation and maintenance overhead.

## Frontend & JavaScript (web)
- Use `fetch()` for AJAX requests; always handle both success and error states.
- Never inject unescaped server-provided data directly into the DOM.
- Use `localStorage` or cookies for client-side state that must persist across page loads; document the key names.
- Deduplicate event-driven actions (e.g., view counts, like clicks) using a persistent client-side flag to avoid repeat calls.

## Logging (general)
- Log all security-relevant and admin actions to a persistent store (file or database).
- Log unauthorized access attempts with IP, timestamp, and a description of the attempted action.
- Use structured log entries: timestamp, severity, and message at minimum.
- Use a dedicated logging module/function rather than scattering raw write calls throughout the codebase.
- Log error conditions with sufficient context to diagnose the issue, but never log sensitive data (passwords, tokens, PII, session identifiers).

## Language-Specific Guidelines

### C#
- Use PascalCase for types, methods, properties, and events; camelCase with leading underscore (`_camelCase`) for private fields.
- Prefer `var` only when the right-hand type is immediately obvious; use explicit types otherwise.
- Use expression-bodied members only for single-expression methods and properties; avoid them for anything requiring multiple statements.
- Prefer `readonly` fields over mutable fields wherever the value is set once.
- Dispose of `IDisposable` resources with `using` declarations or `using` blocks; never rely on finalizers for cleanup.
- Prefer `async`/`await` over raw `Task.ContinueWith`; always `await` tasks rather than blocking with `.Result` or `.Wait()`.
- Throw specific exception types; never throw or catch bare `Exception` unless re-throwing or just logging.
- Favor composition over inheritance; keep inheritance hierarchies shallow.
- Place each class in its own file; filename must match the class name.

### WPF
- Follow MVVM strictly: Views contain only XAML and code-behind limited to UI-only logic; business logic belongs in ViewModels.
- Bind controls to ViewModel properties via `{Binding}`; never manipulate controls directly from the ViewModel.
- Implement `INotifyPropertyChanged` (or use a base class/source generator) on all ViewModel properties that can change, or even better, create a common base class for all updatable UI relatedViewModels.
- Use `ICommand` (e.g., `RelayCommand`) for all user actions; do not use click handlers for logic beyond pure UI.
- Define reusable styles, control templates, and brushes in `ResourceDictionary` files; do not repeat style properties inline.
- Use `DataTemplate` to define how data types are rendered; do not build dynamic UI in code-behind.
- Avoid blocking the UI thread; run all non-trivial operations on background threads and marshal results back via `Dispatcher` or `async`/`await`.
- Keep code-behind minimal; if non-trivial logic is needed in code-behind, move it to the ViewModel or a service.

### Dart
- Follow Dart's official style guide: `lowerCamelCase` for variables and functions, `UpperCamelCase` for types, `lowercase_with_underscores` for files and packages.
- Always specify types on public API signatures; use `var` / `final` only for local variables where the type is obvious.
- Prefer `final` over `var` for variables that are not reassigned.
- Use `const` constructors wherever the object is compile-time constant.
- Handle nullable types explicitly; avoid `!` null-assertion unless a null value is genuinely impossible at that point.
- Use `async`/`await` over raw `Future.then()` chains for clarity.
- Prefer named parameters for functions with more than two parameters and for any parameter whose purpose is not obvious from the call site.
- Split large files into smaller focused files; group related classes and functions together but avoid mega-files.

### Flutter
- Keep `Widget` `build()` methods small; extract sub-trees into separate `Widget` classes or helper methods rather than inlining deeply nested trees.
- Prefer `StatelessWidget` by default; only use `StatefulWidget` when local mutable state is genuinely needed.
- Use a state management solution (e.g., `Provider`, `Riverpod`, `Bloc`) consistently throughout the project; do not mix approaches.
- Never perform I/O, network calls, or heavy computation inside `build()`; use `FutureBuilder`/`StreamBuilder` or trigger work in lifecycle methods.
- Use `const` constructors for widgets wherever possible to minimize unnecessary rebuilds.
- Separate business logic and data access from UI; put them in service classes or notifiers/blocs, not inside widgets.
- Always dispose `AnimationController`, `TextEditingController`, `ScrollController`, and similar controllers in `dispose()`.
- Prefer `Theme.of(context)` colors and text styles over hard-coded values to maintain visual consistency.

