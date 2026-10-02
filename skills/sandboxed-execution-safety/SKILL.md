---
name: sandboxed-execution-safety
description: Use when running shell commands, build scripts, or test runners within hardened sandbox isolation.
---

# Sandboxed Execution Safety

## Overview
Executes arbitrary terminal commands within strict process and filesystem sandboxes, shielding host developer environments from unintended state modifications.

## When to Use
- When executing untrusted test scripts or external build tasks.
- When isolating filesystem writes strictly to the active workspace directory.
- When intercepting commands that attempt network egress or privilege escalation.

## Core Capabilities
1. **Hardened Process Confinement**: Restricts system calls using platform sandboxing primitives.
2. **Interactive Safety Prompts**: Suspends execution and requests affirmative approval for operations exceeding baseline permissions.
3. **Deterministic Timeout Control**: Enforces strict execution deadlines to prevent runaway or hanging processes.
