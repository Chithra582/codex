---
name: surgical-code-modification
description: Use when reading, creating, or editing source code files with exact string replacement and unified diff previews.
---

# Surgical Code Modification

## Overview
Applies minimal, surgical patches to existing codebases without disrupting unrelated formatting, comments, or architectural structures.

## When to Use
- When modifying function implementations, refactoring interfaces, or fixing identified defects.
- When generating new modules or configuration files with verified syntax.
- When reverting erroneous edits safely using snapshot checkpoints.

## Core Capabilities
1. **Atomic String Replacement**: Matches target lines exactly to prevent unintended replacements across repeated identifiers.
2. **Unified Diff Generation**: Displays clear visual before-and-after diffs for developer review prior to commit.
3. **Format Preservation**: Retains indentation, trailing commas, and project-specific stylistic conventions.
