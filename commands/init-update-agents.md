# Debug Mode Rules (Non-Obvious Only)

## Debugging This Repository

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
- `./cline_docs/` is for temporary task handoffs (cleared between major tasks)
- `.memory-bank/` is for persistent project context (never cleared)
- Confusion between these causes context loss across sessions

### Confidence Scoring Failures
- If implementation fails, likely proceeded with confidence <9/10
- Must stop and investigate when confidence 0-8
- Confidence scoring is mandatory before AND after tool use

