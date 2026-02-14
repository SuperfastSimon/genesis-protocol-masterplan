# Genesis Protocol — System Architecture

## Overview

The Genesis Protocol is a hierarchical multi-agent system built on AutoGPT Platform.
It follows a **Boss/Worker pattern** where a central orchestrator delegates tasks
to specialized worker agents, each handling one stage of the software lifecycle.

## Agent Hierarchy

### Boss Agent (Orchestrator)
- **Role**: Head Developer / Project Manager
- **Input**: High-level task description (e.g., "Build a landing page for X")
- **Process**:
  1. Decompose task into subtasks
  2. Route subtasks to appropriate Worker Agents
  3. Collect and validate outputs
  4. Iterate if quality checks fail
  5. Trigger deployment when satisfied
- **Key Block**: Agent Executor Block (calls worker agents by graph_id)

### Writer Agent
- **Role**: Code & Content Generator
- **Input**: Specific writing task + context/requirements
- **Output**: Generated code, documentation, or content
- **Key Blocks**:
  - `AITextGeneratorBlock` (id: `1f292d4a-41a4-4977-9684-7c8d560b9f91`)
  - `CodeExtractionBlock` (id: `d3a7d896-3b78-4f44-8b4b-48fbf4f0bcd8`)
- **LLM Options**: GPT-4o, Claude 3.5 Sonnet, Gemini Pro, Llama 3.1, DeepSeek

### Builder Agent
- **Role**: Code Executor & Tester
- **Input**: Code from Writer Agent
- **Output**: Execution results, test outcomes, build artifacts
- **Key Blocks**:
  - `InstantiateCodeSandboxBlock` (id: `ff0861c9-1726-4aec-9e5b-bf53f3622112`)
  - `ExecuteCodeStepBlock` (id: `82b59b8e-ea10-4d57-9161-8b169b0adba6`)
  - `ExecuteCodeBlock` (id: `0b02b072-abe7-11ef-8372-fb5d162dd712`)
- **Environment**: E2B sandbox with internet access

### Deployer Agent
- **Role**: Version Control & Deployment
- **Input**: Validated build artifacts
- **Output**: Deployed application / pushed code
- **Key Blocks**:
  - `GithubCreateFileBlock` — Push files to repos
  - `GithubCreateRepositoryBlock` — Create new repos
  - `GithubListBranchesBlock` — Branch management
- **Future**: Vercel/Netlify deploy triggers, Docker builds

### Maintainer Agent
- **Role**: Health Monitor & Self-Healer
- **Input**: Deployed application endpoints / repo URLs
- **Output**: Health reports, auto-fix commits
- **Key Blocks**:
  - HTTP Request blocks (health checks)
  - AI Text Generator (analyze errors, generate fixes)
  - GitHub blocks (push fixes)
- **Loop**: Monitor → Detect Issue → Generate Fix → Test → Deploy Fix

## Data Flow

```
User Prompt
    │
    ▼
┌─────────┐    subtask     ┌────────┐    code     ┌─────────┐
│  BOSS   │───────────────▶│ WRITER │────────────▶│ BUILDER │
│  AGENT  │◀───────────────│ AGENT  │◀────────────│  AGENT  │
│         │   code output   └────────┘  test result └─────────┘
│         │                                              │
│         │    validated artifacts                        │
│         │──────────────────────────────────────────────▶│
│         │                                              ▼
│         │                                        ┌──────────┐
│         │◀───────────────────────────────────────│ DEPLOYER │
│         │         deployment confirmation        │  AGENT   │
│         │                                        └──────────┘
│         │                                              │
│         │                                              ▼
│         │                                       ┌───────────┐
│         │◀──────────────────────────────────────│MAINTAINER │
│         │         health reports / alerts        │   AGENT   │
└─────────┘                                       └───────────┘
```

## AutoGPT Platform Blocks Used

| Block | ID | Purpose |
|-------|----|---------|
| Agent Executor | (system) | Boss calls Worker agents |
| AI Text Generator | `1f292d4a-...` | LLM code/text generation |
| AI List Generator | `9c0b0450-...` | Structured list generation |
| Code Extraction | `d3a7d896-...` | Parse code from AI output |
| Execute Code | `0b02b072-...` | Run code in E2B sandbox |
| Instantiate Sandbox | `ff0861c9-...` | Create E2B environment |
| Execute Code Step | `82b59b8e-...` | Multi-step sandbox execution |
| Ideogram Model | `6ab085e2-...` | Image generation |
| AI Image Generator | `ed1ae7a0-...` | Image generation |

## Implementation Order

1. **Writer Agent** — Core value: generates code from prompts
2. **Builder Agent** — Validates writer output in sandbox
3. **Deployer Agent** — Pushes to GitHub + triggers deploy
4. **Boss Agent** — Orchestrates the above three
5. **Maintainer Agent** — Closes the autonomous loop
