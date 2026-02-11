# AGENTS.md

This file provides guidance to agents when working with code in this repository.

IMPORTANT: Only create and update this main AGENTS.md file. Do not create or update any vendor- or mode-specific AGENTS.md files. Keep mode-specific instructions as part of this file.

## Project Type
This is a **rules and commands repository** for agentic coding assistants, not a traditional codebase. It contains XML-formatted rules and markdown command templates.

## Non-Obvious Conventions

### Memory Management
- Use `.memory-bank/` directory (NOT `./agent_docs/`) for persistent project context
- Memory Bank has specific file hierarchy: `projectbrief.md` → `productContext.md`/`systemPatterns.md`/`techContext.md` → `activeContext.md` → `progress.md`
- Use `./agent_docs/` folder ONLY for task handoff documentation between sessions
- Must read ALL memory bank files at start of EVERY task

### Context Window Management
- Monitor context window usage in environment details
- **CRITICAL**: Initiate task handoff at 70% usage (e.g., 140K/200K tokens)
- Use `ask_followup_question` then `new_task` tool for handoffs
- Clear `./agent_docs/` folder when writing new handover (old docs cause confusion)

### Git Operations
- **ALWAYS** use `--no-pager` flag with git commands (`git log --no-pager`, `git diff --no-pager`)
- Ask before pushing to remote
- Set upstream with push: `git push -u origin <branch>`

### Language Requirements
- **MANDATORY**: All outputs must use British English spelling (-our, -ise, -re, -ll-, etc.)
- Examples: favour, organise, centre, travelling, analyse

### Domain Terminology
- "dissuing" in repository names means "issuing" (common typo/abbreviation)

### Workflow Requirements
- **Rule verification**: At conversation start, repeat all rules in bulleted list grouped by category (once only)
- **Confidence scoring**: Provide 0-10 confidence level before/after tool use
- **Memory check**: Respond "WE CAN DO IT" when asked to verify memory retention

### Code Style (When Working on Projects)
- Prefer functional over inheritance (use classes only when state/context needed)
- Self-explanatory code preferred; inline comments extremely scarce
- Unit tests must run independently, no execution order dependency
- Never log passwords, credentials, tokens, PII

### Analysis Framework
- Rate understanding 0-10 before implementation
- 0-3: Stop, investigate thoroughly
- 4-6: Stop, address knowledge gaps
- 7-8: Verify edge cases
- 9-10: Proceed with implementation

## Architect Mode Rules (Non-Obvious Only)

### Rules System Architecture
- Rules are hierarchical: core-agent-rules.md → development-standards.md → task-rules.md → technical-specifications.md
- Each rule file has specific scope: core (behaviour), development (code style), task (workflow), technical (tools)
- Rules with IDs override general guidelines (enforcement hierarchy)
- User instructions override all rules (ultimate precedence)

### Memory Management Architecture
- Two-tier memory system: `.memory-bank/` (persistent) + `./agent_docs/` (ephemeral)
- Memory Bank has directed acyclic graph structure (projectbrief at root)
- Task handoffs use linear sequence (old task ends, new begins)
- Context window monitoring prevents memory overflow (70% threshold)

### Workflow State Machine
- Confidence levels (0-10) trigger state transitions:
  - 0-3: Investigation state (mandatory)
  - 4-6: Gap analysis state (mandatory)
  - 7-8: Verification state (mandatory)
  - 9-10: Implementation state (proceed)
- Task handoff triggers: 70% context, logical completion, scope expansion
- Rule verification occurs once per conversation (state initialization)

### Command Template Pattern
- Commands in `commands/` are reusable workflow templates
- Each command defines: goal, requirements, unknowns, checklist, output format
- Commands reference analysis framework from rules (tight coupling)
- Migration plans use phased checklist approach with git commits after each phase

### Integration Constraints
- Git operations require `--no-pager` flag (terminal output limitation)
- Push operations require user confirmation (safety constraint)
- British English is non-negotiable (localization requirement)
- Semantic commits enable automated changelog/versioning (toolchain integration)

### Scalability Considerations
- Context window is hard limit (200K tokens typical)
- 70% threshold provides buffer for handoff documentation
- Memory Bank prevents context loss across sessions (persistence layer)
- Task decomposition enables work beyond single session limits

### Hidden Dependencies
- Memory Bank files depend on each other (must read in order)
- Task handoff requires specific tool sequence (ask → new_task)
- Confidence framework depends on investigation checklists
- Semantic commits depend on approved type list

## Ask Mode Rules (Non-Obvious Only)

### Repository Purpose
- This is NOT a software project - it's a rules/commands collection for AI assistants
- No build commands, no tests, no runtime - only documentation
- Users are configuring AI assistant behaviour, not building applications

### Documentation Structure
- `rules/` contains XML-formatted agent behaviour rules
- `commands/` contains markdown templates for common AI assistant workflows
- Rules reference non-existent files like `/project-brief.md` - these are templates for actual projects
- Memory Bank structure (`.memory-bank/`) is a framework, not implemented here

### Counterintuitive Patterns
- "dissuing" in repository names actually means "issuing" (typo/abbreviation)
- `./agent_docs/` folder is for task handoffs, NOT permanent documentation
- Context window monitoring at 70% is critical - not a suggestion
- British English requirement is mandatory, not a preference

### Rule Interpretation
- XML tags like `<CRITICAL_PRINCIPLES>` indicate priority, not just formatting
- `**MUST**` in markdown means mandatory, not emphasis
- Confidence scoring (0-10) is required workflow, not optional self-assessment
- "WE CAN DO IT" response is a memory check protocol, not enthusiasm

### Hidden Relationships
- Memory Bank files have dependency hierarchy (projectbrief → others → activeContext → progress)
- Task handoff process requires specific tool sequence: `ask_followup_question` → `new_task`
- Git semantic commits integrate with changelog generation and semantic versioning
- Analysis framework confidence levels (0-3, 4-6, 7-8, 9-10) trigger different mandatory actions

### Common Misunderstandings
- This repository configures AI behaviour for OTHER projects, not itself
- Rules here are meant to be loaded by AI assistants working elsewhere
- Commands are templates to be invoked, not documentation to read
- Memory Bank is a pattern to implement in projects, not used in this repo

## Code Mode Rules (Non-Obvious Only)

### File Organization
- Rules stored in `rules/` directory use XML format with specific tags (`<RULE id="...">`)
- Commands stored in `commands/` directory are markdown templates for common workflows
- No traditional source code - this is a documentation/rules repository

### Semantic Commit Messages
- **MANDATORY**: All commits must follow `type(scope): description` format
- Type must be lowercase: feat, fix, docs, style, refactor, test, chore, perf, ci, build, revert
- Description in imperative mood, lowercase start, no period
- Breaking changes: add `!` after type/scope, document in footer with `BREAKING CHANGE:`
- Examples: `feat(auth): add two-factor authentication`, `fix(api): resolve race condition`

### Documentation Standards
- XML rules use specific structure: `<RULE id="XXX001">` with priority levels
- Markdown lists use single dash and space: `- item` (not `* item` or `+ item`)
- British English mandatory in all documentation
- Self-explanatory content preferred; avoid obvious information

### Task Handoff Documentation
- Create handoff docs in `./agent_docs/` (project root, not `.roo/`)
- Clear old handoff docs before writing new ones (prevents confusion)
- Include: completed work, current state, next steps, reference info
- Must be concise - focus on non-obvious context only

### Memory Bank Updates
- Update `.memory-bank/` files when discovering significant patterns
- Follow hierarchy: projectbrief → productContext/systemPatterns/techContext → activeContext → progress
- When user says "update memory bank", review ALL files (even if no changes needed)
- Focus updates on activeContext.md and progress.md for current state

## Debug Mode Rules (Non-Obvious Only)

### Context Window Issues
- Monitor token usage in environment details (shown as X/200000 tokens)
- At 70% usage (140K+ tokens), must initiate handoff - this is non-negotiable
- Failure to handoff causes memory loss and context corruption
- Use `ask_followup_question` then `new_task` tool for proper handoff

### Memory Verification
- If asked "memory check", respond exactly: "WE CAN DO IT"
- Failure to respond correctly indicates memory limit reached
- Must re-read rules files starting from core-agent-rules.md
- Stop re-reading when content becomes familiar (still in memory)

### Rule Conflicts
- Rules with IDs (e.g., `<RULE id="CWM001">`) take precedence over general guidelines
- User instructions override all rules
- Check `<ENFORCEMENT>` sections for mandatory vs. optional rules

### Git Command Failures
- If git commands hang or produce no output, missing `--no-pager` flag
- Always use: `git log --no-pager`, `git diff --no-pager`, etc.
- Git operations that modify state (commit, push) require user confirmation

### Documentation Inconsistencies
- `./agent_docs/` is for temporary task handoffs (cleared between major tasks)
- `.memory-bank/` is for persistent project context (never cleared)
- Confusion between these causes context loss across sessions

### Confidence Scoring Failures
- If implementation fails, likely proceeded with confidence <9/10
- Must stop and investigate when confidence 0-8
- Confidence scoring is mandatory before AND after tool use
