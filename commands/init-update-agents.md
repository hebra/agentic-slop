# Role: Project Architect & Documentation Specialist

## Context
I am working on a project and need to create or update an `AGENTS.md` file. This file acts as the primary "Instruction Manual" for any AI coding agent (like Roo Code, Cline, or GitHub Copilot) that interacts with this repository.

IMPORTANT: Only create/update the AGENTS.md file in the root of the project. Do not create any vendor-specific folders.
IMPORTANT: Keep mode-specfici instructions in dedicated sections in the main AGENTS.md file.

## Task
Evaluate the current codebase (file structure, package.json/requirements.txt, and existing code) and perform the following:

### 1. Initialization (If AGENTS.md doesn't exist)
Generate a comprehensive `AGENTS.md` file using this structure:
- **Project Overview**: High-level purpose of the app.
- **Tech Stack**: Key frameworks, languages, and database choices.
- **Core Architecture**: Description of the folder structure (e.g., Domain-Driven Design, Feature-based, etc.).
- **Coding Standards**: Rules for naming conventions, testing requirements, and preferred patterns (e.g., "Use functional components over classes").
- **Agent Constraints**: Specific "Dos and Don'ts" (e.g., "Do not modify the /legacy folder" or "Always use Shadcn/ui for components").

### 2. Update (If AGENTS.md exists)
- **Delta Analysis**: Scan the current directory for new libraries, architectural shifts, or recent refactors.
- **Conflict Resolution**: Identify if any current instructions in `AGENTS.md` contradict the actual state of the code.
- **Synthesis**: Merge new findings into the existing document without losing manual overrides or specific developer notes.

## Output Format
- Provide the full markdown content for `AGENTS.md`.
- Include a "Changelog" section at the bottom summarizing what was added or modified.

## Constraints
- Be concise. Agents process tokens; don't use flowery language.
- Use explicit file paths.
- If a specific library is found (e.g., Tailwind, Prisma, FastAPI), include the specific best-practice patterns for that tool.
