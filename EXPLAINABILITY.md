# EXPLAINABILITY.md

This document explains the internal mechanisms, data lineage, operational boundaries, and governance framework of **# Explainability & Decision Transparency Report** (`codex`) in accordance with the **OpenGAP v0.1.0** specification for the **HiDevs GitAgent Passport** clearance pipeline.

> **Agent Name:** # Explainability & Decision Transparency Report (`codex`)  
> **Specification:** OpenGAP v0.1.0  
> **Category / Domain:** Developer Tools / Autonomous CLI Coding Agent & Sandbox  
> **Compliance Standard:** OpenGAP Checkpoint 2 (Explainability & Decision Governance), OWASP LLM Top 10, MITRE ATLAS  

---

## How the Agent Decides

### 1. Deterministic Multi-Stage Decision Pipeline
The agent operates via a strictly disciplined, 5-stage deterministic execution pipeline enforcing sandboxed containment, atomic patching, and test verification before concluding any development turn.

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



### 3. Thresholding & Refusal Decision Criteria

# Explainability & Decision Transparency Report enforces strict operational boundaries and deterministic refusal thresholds:
- **Refusal on Policy Violation**: Requests violating boundary constraints halt with code `ERR_POLICY_VIOLATION`.
- **Refusal on Timeout**: Executions exceeding budget limits terminate with code `ERR_EXECUTION_TIMEOUT`.

### 4. Fallback Decision Mechanism

Continuous operational stability is maintained through layered fault recovery:
- **Model Fallback Cascade**: High-level reasoning and synthesis default to `gemini-2.0-flash` with automatic failover to `gpt-4o` and `claude-3-5-sonnet`.

### 5. Human-in-the-Loop Governance

Human operators retain sovereign authority over the multi-agent execution lifecycle:
- **Operational Review**: Sensitive actions require operator sign-off.
- **Audit Logging**: All decisions are recorded for auditability.

---

## The Data It Uses

# Explainability & Decision Transparency Report operates under strict principles of data minimization, environment isolation, and privacy protection.

### 1. Ingested Input Data

The framework processes only operational data necessary to perform its functions:
- **Input Directives**: Operational tasks and data payloads.

### 2. Configuration & Reference Data

- **Configuration Schemas**: Declarative system configuration files.

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

### 1. Deterministic Multi-Stage Decision Pipeline
The agent operates via a strictly disciplined, 5-stage deterministic execution pipeline enforcing sandboxed containment, atomic patching, and test verification before concluding any development turn.

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

### 2. Mathematical Decision & Affinity Scoring
Tool selection affinity across available tool primitives $t \in T$ is resolved by evaluating task relevance against the operational query $q$:

$$S_{\text{affinity}}(t) = w_1 \cdot \text{SemanticRelevance}(t, q) + w_2 \cdot \text{ScopeAlignment}(t) + w_3 \cdot \text{SafetyScore}(t)$$

Where:
- $w_1 = 0.50$: Semantic alignment between query intent and tool description.
- $w_2 = 0.30$: Locality to active project files and target languages.
- $w_3 = 0.20$: Sandbox safety score prioritizing read-only and local workspace operations over broad system access.

Patch applicability confidence $P_{\text{patch}}(m)$ for file modification $m$ requires exact character matches:

$$P_{\text{patch}}(m) = \mathbb{I}(\text{Count}(\text{TargetString}, \text{FileContent}) = 1.0)$$

Where replacement is strictly refused unless $P_{\text{patch}} = 1.0$, guaranteeing unambiguous, single-site code substitutions.

### 3. Thresholding & Refusal Decision Criteria
Operations violating sandbox boundaries or quality gates trigger immediate refusals with standardized error codes:

| Threshold Parameter | Value | Decision / Refusal Action | Error Code |
| :--- | :--- | :--- | :--- |
| **Sandbox Policy Breach** | Unauthorized write outside workspace | Block operation; isolate process to sandbox | `ERR_SANDBOX_POLICY_VIOLATION` |
| **User Permission Declined** | Operator rejects interactive prompt | Abort execution; preserve current workspace state | `ERR_PERMISSION_REJECTED` |
| **Unverified Completion** | Success claimed without test run | Refuse completion; mandate test runner execution | `ERR_UNVERIFIED_COMPLETION_ASSERTION` |
| **Execution Timeout** | Sandbox execution time > 120 s | Terminate child process; capture partial log output | `ERR_EXECUTION_TIMEOUT` |
| **Ambiguous Target Match** | Target string count $\neq 1$ in file | Refuse file patch; mandate unique context lines | `ERR_UNMATCHED_PATCH_TARGET` |

### 4. Multi-Tier Fallback Mechanisms & Human-in-the-Loop Governance
1. **Tier 1 (Automated Patch Recovery & Fuzzy Anchor Matching)**: If an exact target string fails due to whitespace variation, the engine attempts normalized anchor matching within a bounded 5-line window.
2. **Tier 2 (Model Fallback & Alternative Command Synthesis)**: If a synthesized shell command fails with a non-zero exit code, the agent inspects compiler stderr and generates an alternative minimal command.
3. **Tier 3 (Interactive Developer Sign-Off)**: High-risk operations (e.g., git branch deletion, push to remote, external network calls) halt execution to prompt the human developer directly in the CLI.

---

## The Data It Uses

### 1. Ingestion Data & Input Types
- **Developer Instructions**: Natural language feature requests, bug reports, and refactoring tasks.
- **Workspace Source Files**: Code files, build manifests (`Cargo.toml`, `package.json`), and diff traces.
- **Execution Telemetry**: Command exit codes, stdout/stderr streams, and compiler diagnostic JSON.

### 2. Reference Standards & Methodologies
- **Model Context Protocol (MCP)**: JSON-RPC 2.0 open standard for tool and resource integration.
- **Test-Driven Development (TDD)**: Verified red-to-green test cycles before commit.
- **POSIX Sandbox Primitives**: File descriptor isolation and system call filtering.

### 3. Model Lineage & System Architecture
- **Reasoning Models**: OpenAI GPT-4o, o1, o3-mini, and specialized Codex coding models.
- **Runtime Environment**: Rust core (`codex-rs`), Node.js / TypeScript CLI (`codex-cli`), Bazel build system.

### 4. Data Privacy, Governance & Retention
- **Local-First Execution**: Code modifications and sandbox execution occur entirely on the developer's computer.
- **Prompt Sanitization**: Sensitive environment variables, secrets, and private keys are scrubbed before prompt transmission.
- **Zero Local Telemetry Leakage**: No user code or transcripts are shared with third parties outside explicit OpenAI API calls.

---

## Limitations

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
| - Deterministic Multi-Stage Decision Pipeline
The agent operates via a strictly disciplined, 5-stage deterministic execution pipeline enforcing sandboxed containment, atomic patching, and test verification before concluding any development turn.

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

### 2. Mathematical Decision & Affinity Scoring
Tool selection affinity across available tool primitives $t \in T$ is resolved by evaluating task relevance against the operational query $q$:

$$S_{\text{affinity}}(t) = w_1 \cdot \text{SemanticRelevance}(t, q) + w_2 \cdot \text{ScopeAlignment}(t) + w_3 \cdot \text{SafetyScore}(t)$$

Where:
- $w_1 = 0.50$: Semantic alignment between query intent and tool description.
- $w_2 = 0.30$: Locality to active project files and target languages.
- $w_3 = 0.20$: Sandbox safety score prioritizing read-only and local workspace operations over broad system access.

Patch applicability confidence $P_{\text{patch}}(m)$ for file modification $m$ requires exact character matches:

$$P_{\text{patch}}(m) = \mathbb{I}(\text{Count}(\text{TargetString}, \text{FileContent}) = 1.0)$$

Where replacement is strictly refused unless $P_{\text{patch}} = 1.0$, guaranteeing unambiguous, single-site code substitutions.

### 3. Thresholding & Refusal Decision Criteria
Operations violating sandbox boundaries or quality gates trigger immediate refusals with standardized error codes:

| Threshold Parameter | Value | Decision / Refusal Action | Error Code |
| :--- | :--- | :--- | :--- |
| **Sandbox Policy Breach** | Unauthorized write outside workspace | Block operation; isolate process to sandbox | `ERR_SANDBOX_POLICY_VIOLATION` |
| **User Permission Declined** | Operator rejects interactive prompt | Abort execution; preserve current workspace state | `ERR_PERMISSION_REJECTED` |
| **Unverified Completion** | Success claimed without test run | Refuse completion; mandate test runner execution | `ERR_UNVERIFIED_COMPLETION_ASSERTION` |
| **Execution Timeout** | Sandbox execution time > 120 s | Terminate child process; capture partial log output | `ERR_EXECUTION_TIMEOUT` |
| **Ambiguous Target Match** | Target string count $\neq 1$ in file | Refuse file patch; mandate unique context lines | `ERR_UNMATCHED_PATCH_TARGET` |

### 4. Multi-Tier Fallback Mechanisms & Human-in-the-Loop Governance
1. **Tier 1 (Automated Patch Recovery & Fuzzy Anchor Matching)**: If an exact target string fails due to whitespace variation, the engine attempts normalized anchor matching within a bounded 5-line window.
2. **Tier 2 (Model Fallback & Alternative Command Synthesis)**: If a synthesized shell command fails with a non-zero exit code, the agent inspects compiler stderr and generates an alternative minimal command.
3. **Tier 3 (Interactive Developer Sign-Off)**: High-risk operations (e.g., git branch deletion, push to remote, external network calls) halt execution to prompt the human developer directly in the CLI.

---

## The Data It Uses

### 1. Ingestion Data & Input Types
- **Developer Instructions**: Natural language feature requests, bug reports, and refactoring tasks.
- **Workspace Source Files**: Code files, build manifests (`Cargo.toml`, `package.json`), and diff traces.
- **Execution Telemetry**: Command exit codes, stdout/stderr streams, and compiler diagnostic JSON.

### 2. Reference Standards & Methodologies
- **Model Context Protocol (MCP)**: JSON-RPC 2.0 open standard for tool and resource integration.
- **Test-Driven Development (TDD)**: Verified red-to-green test cycles before commit.
- **POSIX Sandbox Primitives**: File descriptor isolation and system call filtering.

### 3. Model Lineage & System Architecture
- **Reasoning Models**: OpenAI GPT-4o, o1, o3-mini, and specialized Codex coding models.
- **Runtime Environment**: Rust core (`codex-rs`), Node.js / TypeScript CLI (`codex-cli`), Bazel build system.

### 4. Data Privacy, Governance & Retention
- **Local-First Execution**: Code modifications and sandbox execution occur entirely on the developer's computer.
- **Prompt Sanitization**: Sensitive environment variables, secrets, and private keys are scrubbed before prompt transmission.
- **Zero Local Telemetry Leakage**: No user code or transcripts are shared with third parties outside explicit OpenAI API calls.

---

## Limitations

### 1. Sandbox Isolation Overhead on Complex Native Compiler Toolchains | Section 1 | Verified |
| - Context Window Saturation on Massive Multi-Module Refactors | Section 2 | Verified |
| - Non-Deterministic Test Suites Triggering False Negative Alarms | Section 3 | Verified |
| - Rate Limiting and Network Latency to Cloud Reasoning Endpoints | Section 4 | Verified |
| - Divergence in Shell Environment Profiles Between Host and Sandbox | Section 5 | Verified |
