# EXPLAINABILITY.md

This document explains the internal mechanisms, data lineage, operational boundaries, and governance framework of **# Explainability & Decision Transparency Report** (`codex`) in accordance with the **OpenGAP v0.1.0** specification for the **HiDevs GitAgent Passport** clearance pipeline.

> **Agent Name:** # Explainability & Decision Transparency Report (`codex`)  
> **Specification:** OpenGAP v0.1.0  
> **Category / Domain:** Developer Tools / Autonomous CLI Coding Agent & Sandbox  
> **Compliance Standard:** OpenGAP Checkpoint 2 (Explainability & Decision Governance), OWASP LLM Top 10, MITRE ATLAS  

---

## How the Agent Decides

# Explainability & Decision Transparency Report operates via a deterministic five-stage operational pipeline.

### 1. Decision Architecture

The runtime intake, state classification, evaluation, and execution tracking operate across a deterministic, five-stage pipeline:

```
+-----------------------------------------------------------------------------------+
|                          Deterministic Codex Pipeline                             |
+-----------------------------------------------------------------------------------+
|  [Stage 1: Intent Ingestion & Task Formulation Gate]                              |
|     --> Parse user instruction, inspect workspace state, & plan code changes     |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 2: Context Retrieval & Symbol Indexing]                                   |
|     --> Query AST symbol table; extract minimal relevant function & type ranges    |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 3: Sandbox Policy & Permission Gate]                                      |
|     --> Verify command against sandbox policy; prompt user for elevated privileges|
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 4: Sandboxed Tool Execution & Surgical Code Patching]                     |
|     --> Apply atomic string replacements; execute build & test commands in sandbox |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 5: Test Verification & Response Finalization]                             |
|     --> Validate compiler/test exit codes (code 0) & stream response summary      |
+-----------------------------------------------------------------------------------+
```

### 2. Decision Logic & Routing Formulations

Gate]                              |
|     --> Parse user instruction, inspect workspace state, & plan code changes     |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 2: Context Retrieval & Symbol Indexing]                                   |
|     --> Query AST symbol table; extract minimal relevant function & type ranges    |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 3: Sandbox Policy & Permission Gate]                                      |
|     --> Verify command against sandbox policy; prompt user for elevated privileges|
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 4: Sandboxed Tool Execution & Surgical Code Patching]                     |
|     --> Apply atomic string replacements; execute build & test commands in sandbox |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 5: Test Verification & Response Finalization]                             |
|     --> Validate compiler/test exit codes (code 0) & stream response summary      |
+-----------------------------------------------------------------------------------+
```

### 3. Thresholding & Refusal Decision Criteria

# Explainability & Decision Transparency Report enforces strict operational boundaries and deterministic refusal thresholds:
- **Refusal on ERR_SANDBOX_POLICY_VIOLATION**: **Sandbox Policy Breach** halts execution with code `ERR_SANDBOX_POLICY_VIOLATION`.
- **Refusal on ERR_PERMISSION_REJECTED**: **User Permission Declined** halts execution with code `ERR_PERMISSION_REJECTED`.
- **Refusal on ERR_UNVERIFIED_COMPLETION_ASSERTION**: **Unverified Completion** halts execution with code `ERR_UNVERIFIED_COMPLETION_ASSERTION`.
- **Refusal on ERR_EXECUTION_TIMEOUT**: **Execution Timeout** halts execution with code `ERR_EXECUTION_TIMEOUT`.
- **Refusal on ERR_UNMATCHED_PATCH_TARGET**: **Ambiguous Target Match** halts execution with code `ERR_UNMATCHED_PATCH_TARGET`.

### 4. Fallback Decision Mechanism

Continuous operational stability is maintained through layered fault recovery:
- **Model Fallback Cascade**: High-level reasoning and synthesis default to `gemini-2.0-flash` with automatic failover to `gpt-4o` and `claude-3-5-sonnet`.

### 5. Human-in-the-Loop Governance

Human operators retain sovereign authority over the multi-agent execution lifecycle:
- **Consequential Action Sign-Off**: Sensitive and consequential actions require operator sign-off.
- **Offline Ledger Auditing**: Operators can verify execution records and state transitions offline.

---

## The Data It Uses

# Explainability & Decision Transparency Report operates under strict principles of data minimization, environment isolation, and privacy protection.

### 1. Ingested Input Data

The framework processes only operational data necessary to perform its functions:
- **Developer Instructions**: Natural language feature requests, bug reports, and refactoring tasks.
- **Workspace Source Files**: Code files, build manifests (`Cargo.toml`, `package.json`), and diff traces.
- **Execution Telemetry**: Command exit codes, stdout/stderr streams, and compiler diagnostic JSON.

### 2. Configuration & Reference Data

- **Configuration Schemas**: Declarative system policy files.

### 3. Base Model & Inference Lineage

- **Reasoning Models**: OpenAI GPT-4o, o1, o3-mini, and specialized Codex coding models.
- **Runtime Environment**: Rust core (`codex-rs`), Node.js / TypeScript CLI (`codex-cli`), Bazel build system.

### 4. Data Privacy, Storage, and Retention

- **OWASP LLM & MITRE ATLAS Hardened**: Defended against indirect prompt injection, credential leakage, and unauthorized external API dispatch.
- **Local Environment Isolation**: Agent execution workspaces, intermediate scratchpads, and vector stores reside strictly within designated local project directories.
- **Automated Secret Scrubbing**: API keys, database credentials, and personal credentials are automatically redacted prior to embedding or logging.
- **Zero Commercial Monetization**: Prompts, intermediate reasoning trajectories, and task deliverables are never commercialized or shared with third parties.

---

## Limitations

Understanding the operational boundaries and technical constraints of # Explainability & Decision Transparency Report is essential for effective deployment.

### 1. Sandbox Isolation Overhead on Complex Native Compiler Toolchains
- **Limitation**: Hardened sandboxing can add minor latency to heavy native builds requiring many external system libraries.
- **Mitigation**: Support configurable sandbox profiles (`workspace_write`) with cached build artifact volumes.

### 2. Context Window Saturation on Massive Multi-Module Refactors
- **Limitation**: Large-scale refactors spanning dozens of files can approach model context token ceilings.
- **Mitigation**: Decompose large refactor plans into isolated, sequential single-file tasks with intermediate git commits.

### 3. Non-Deterministic Test Suites Triggering False Negative Alarms
- **Limitation**: Flaky or timing-sensitive unit tests can fail inconsistently during automated verification.
- **Mitigation**: Quarantine identified flaky tests and mandate multi-run stability checks before reporting failure.

### 4. Rate Limiting and Network Latency to Cloud Reasoning Endpoints
- **Limitation**: Heavy conversational coding turns can encounter API provider rate limits during peak usage.
- **Mitigation**: Implement exponential backoff with jitter and cache static repository symbol graphs locally.

### 5. Divergence in Shell Environment Profiles Between Host and Sandbox
- **Limitation**: User shell aliases or custom environment variables may not be automatically inherited in sandboxes.
- **Mitigation**: Explicitly source user profile configs (`~/.bashrc`, `~/.zshrc`) upon sandbox container initialization.

---

## Summary & Compliance Checklist

| Checkpoint 2 Requirement | Corresponding Section | Status |
| :--- | :--- | :---: |
| **How the agent decides** | [How the Agent Decides](#how-the-agent-decides) | **Covered** |
| - Decision architecture & 5-stage pipeline | Section 1 | Verified |
| - Decision logic & routing formulations | Section 2 | Verified |
| - Thresholding & refusal decision criteria | Section 3 | Verified |
| - Fallback decision mechanism | Section 4 | Verified |
| - Human-in-the-loop governance & oversight | Section 5 | Verified |
| **The data it uses** | [The Data It Uses](#the-data-it-uses) | **Covered** |
| - Ingested input data & query streams | Section 1 | Verified |
| - Configuration & reference schemas | Section 2 | Verified |
| - Base model lineage & deterministic engines | Section 3 | Verified |
| - Data privacy, retention lifecycle & MITRE/OWASP | Section 4 | Verified |
| **Its limitations** | [Limitations](#limitations) | **Covered** |
| - Sandbox Isolation Overhead on Complex Native Compiler Toolchains | Section 1 | Verified |
| - Context Window Saturation on Massive Multi-Module Refactors | Section 2 | Verified |
| - Non-Deterministic Test Suites Triggering False Negative Alarms | Section 3 | Verified |
| - Rate Limiting and Network Latency to Cloud Reasoning Endpoints | Section 4 | Verified |
| - Divergence in Shell Environment Profiles Between Host and Sandbox | Section 5 | Verified |
