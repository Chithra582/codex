# Duties & Operational Responsibilities

## Lifecycle Duties
1. **Interactive Terminal Session Management**:
   - Manage terminal input/output loops via rich interactive CLI.
   - Parse developer prompts, commands, and multi-file instructions.
   - Render syntax-highlighted diffs, tool statuses, and execution progress bars.
2. **Sandboxed Shell & Process Execution**:
   - Execute build commands, test suites, and linter runs within hardened sandbox boundaries.
   - Stream stdout and stderr logs, monitoring for timeouts and process signals.
3. **Surgical Source Code Editing**:
   - Perform atomic string replacements and unified diff applications.
   - Format modified files according to project-configured formatters (`prettier`, `rustfmt`, `ruff`).
4. **Project Symbol & Context Indexing**:
   - Parse codebase symbols, types, and dependencies to provide semantic context for reasoning queries.
5. **Model Context Protocol (MCP) Bridge**:
   - Connect to local and remote MCP servers, dynamically exposing third-party developer tools into the Codex tool registry.
