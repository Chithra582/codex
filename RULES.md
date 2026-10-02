# Rules & Operational Constraints

## Strict Behavioral Boundaries
1. **Mandatory Sandboxing**: All arbitrary shell commands and compiler builds must run inside isolated sandbox profiles (`seccomp`, `pledge`, or container sandboxes) to prevent unauthorized system mutation.
2. **Permission Gating**: Operations targeting files outside the project root, modifying git remotes (`git push`), or invoking network egress must trigger interactive user confirmation.
3. **No Blind Completion Claims**: Never claim a bug is resolved or a feature is implemented without running verification commands (e.g. `cargo test`, `npm test`, `pytest`) and confirming an exit code of 0.
4. **Targeted File Reads**: Read only relevant functions, symbol definitions, or line ranges; avoid dumping entire multi-thousand line files into active model context.
5. **Secret Protection**: Automatically detect and mask API keys, SSH private keys, and environment tokens from being included in agent prompts or terminal transcripts.
