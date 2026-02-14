# 🧬 Genesis Protocol — Autonomous Platform Masterplan

> A self-sufficient AI platform that writes, builds, deploys, and maintains everything it creates.

## Architecture

```
┌─────────────────────────────────────────┐
│           🧠 BOSS AGENT                 │
│    (Orchestrator / Head Developer)      │
│                                         │
│  Receives task → Decomposes → Delegates │
│  Monitors → Validates → Iterates       │
└──────────┬──────────┬──────────┬────────┘
           │          │          │
     ┌─────▼──┐ ┌─────▼──┐ ┌────▼───┐
     │ WRITER │ │BUILDER │ │DEPLOYER│
     │ Agent  │ │ Agent  │ │ Agent  │
     └────────┘ └────────┘ └────────┘
           │          │          │
     ┌─────▼──────────▼──────────▼────┐
     │        🔄 MAINTAINER           │
     │   (Monitor + Self-Heal Loop)   │
     └────────────────────────────────┘
```

## Lifecycle Stages

| Stage | Agent | Core Capability |
|-------|-------|-----------------|
| **Write** | Writer Agent | AI text/code generation via LLM |
| **Build** | Builder Agent | Code execution in E2B sandbox |
| **Deploy** | Deployer Agent | GitHub push + hosting triggers |
| **Maintain** | Maintainer Agent | Health checks + auto-fix loops |

## Quick Start

See [`docs/architecture.md`](docs/architecture.md) for the full system design.

See [`docs/boss-agent-spec.md`](docs/boss-agent-spec.md) for Boss Agent implementation.

## Platform

Built on [AutoGPT Platform](https://platform.agpt.co) using:
- **Agent Executor Block** — Boss→Worker orchestration
- **AI Text Generator Block** — LLM-powered code/content generation
- **Code Extraction Block** — Parse code from AI output
- **E2B Code Sandbox** — Secure code execution
- **GitHub Blocks** — Version control & deployment

## Status

🟡 Phase 1: Architecture & Scaffolding (current)
⬜ Phase 2: Writer Agent (next)
⬜ Phase 3: Builder Agent
⬜ Phase 4: Deployer Agent
⬜ Phase 5: Boss Agent + Orchestration
⬜ Phase 6: Maintainer Agent + Self-Heal Loop
