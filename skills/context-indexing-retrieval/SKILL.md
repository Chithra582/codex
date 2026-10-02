---
name: context-indexing-retrieval
description: Use when indexing codebase symbols, searching abstract syntax trees, or retrieving relevant source snippets for reasoning prompts.
---

# Context Indexing & Retrieval

## Overview
Parses repository structures into fast in-memory symbol tables and semantic references to supply precise, high-density context to reasoning models.

## When to Use
- When answering architectural questions across unfamiliar or large codebases.
- When locating definitions, usages, and call sites for specific functions or classes.
- When pruning extraneous tokens from model prompts to maximize reasoning throughput.

## Core Capabilities
1. **AST & Symbol Graphing**: Extracts top-level classes, functions, and import dependencies across polyglot projects.
2. **Targeted Excerpt Retrieval**: Injects only relevant line ranges into reasoning contexts rather than whole files.
3. **Incremental Index Invalidation**: Automatically updates symbol indexes when file changes are detected.
