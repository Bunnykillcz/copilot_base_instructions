# Startup Initialization

This file is an instruction for the AI. Execute it once at the start of a session in this repository, before doing any other work. Do not ask the user to fill anything in - act on it directly.

---

## Step 1 - Detect project state

Inspect the repository root. Determine which of the two cases applies:

**Case A - Existing project:** Source files, a recognizable directory structure, or a language-specific project file (e.g. `.csproj`, `pubspec.yaml`, `package.json`, `composer.json`) are present.

**Case B - New or empty project:** No source files exist yet, or only documentation/config stubs are present.

---

## Step 2 - Case A: Adapt to existing project (silent)

Do not ask questions. Work silently.

1. Scan the repository structure. Identify:
   - Primary language and framework (from project files, source extensions, config files).
   - Actual directory layout (top-level folders and their apparent purpose).
   - Any conventions already in use (naming patterns, config file format, test location).

2. Open `copilot-instructions.md` (or `.github/copilot-instructions.md`) and apply the following edits:
   - Add a **Project File Structure** section that documents the actual directory tree found, with a one-line description of each top-level folder`s purpose. Place it after the **Code Quality** section.
   - Remove or comment out any **Language-Specific Notes** subsections for languages not used in this project.
   - If the project uses a config format other than JSON (e.g. `.env`, YAML, TOML), update the **Settings & Configuration** section to reflect that.
   - If the project has no frontend, remove or disable the **CSS & Styling** and **Frontend & JavaScript** sections.
   - Add any other project-specific conventions that are clearly established in the existing code (e.g. a naming suffix pattern, a specific logging library, a non-standard folder used for a specific purpose).

3. Do not remove any general rules. Only add project-specific context and remove rules for technologies that are provably absent.

---

## Step 3 - Case B: Initialize a new project (interactive)

Ask the user the following questions before doing anything. Ask them together in one message, not one at a time:

- What is the project name?
- What type of project is this? (web app, desktop app, mobile app, CLI tool, library, game, other)
- What is the primary language and framework? (e.g. PHP + custom framework, C# + WPF, Dart + Flutter)
- Are there any known constraints? (e.g. target language version, deployment environment, existing conventions to follow)

Once the user answers:

1. Create the recommended directory structure for the project type and language. Use the structure patterns from the base `copilot-instructions.md` as a reference, adapted to the specific framework if needed.
2. Create a minimal `README.md` at the project root with the project name and a one-line description placeholder.
3. Open `copilot-instructions.md` and add a **Project File Structure** section documenting the structure just created, placed after the **Code Quality** section.
4. Remove **Language-Specific Notes** subsections for languages not used.
5. Remove sections for technologies not applicable to the project type (e.g. remove **CSS & Styling** for a CLI tool, remove **API Endpoints** for a desktop app with no network layer).

---

## Step 4 - Delete or disable this file

After completing initialization, either:
- Delete `startup.md` (if the project will not need re-initialization), or
- Rename it to `startup.done.md` to keep a record without it triggering again.

