# Genesis Protocol — Implementation Roadmap

## Phase 1: Foundation (Current) ✅
- [x] Define system architecture
- [x] Document Boss Agent spec
- [x] Document Writer Agent spec
- [x] Document Builder Agent spec
- [x] Document Deployer Agent spec
- [x] Document Maintainer Agent spec
- [x] Create agent registry config
- [x] Push to GitHub repo

## Phase 2: Writer Agent 🟡
- [ ] Create Writer Agent on AutoGPT Platform
  - AI Text Generator Block with code-optimized system prompt
  - Code Extraction Block to parse output
  - Input: task, language, framework, requirements
  - Output: parsed code files
- [ ] Test with sample tasks:
  - Generate a Python Flask API
  - Generate a React landing page
  - Generate a SQL schema
- [ ] Record graph_id in agent-registry.yaml

## Phase 3: Builder Agent
- [ ] Create Builder Agent on AutoGPT Platform
  - Instantiate Code Sandbox Block
  - Execute Code Step Block (multi-step)
  - Input: code, language, setup_commands
  - Output: execution results, pass/fail
- [ ] Test with Writer Agent outputs
- [ ] Record graph_id in agent-registry.yaml

## Phase 4: Deployer Agent
- [ ] Create Deployer Agent on AutoGPT Platform
  - GitHub blocks (create repo, create/update files)
  - Input: files, repo info, commit message
  - Output: repo URL, commit SHA
- [ ] Test with Builder Agent outputs
- [ ] Record graph_id in agent-registry.yaml

## Phase 5: Boss Agent + Orchestration
- [ ] Create Boss Agent on AutoGPT Platform
  - Agent Executor Block (calls Worker agents)
  - AI Text Generator (task decomposition)
  - AI List Generator (subtask routing)
  - Quality review loop (conditional + iteration)
- [ ] Wire up all Worker agent graph_ids
- [ ] Test end-to-end: prompt → write → build → deploy
- [ ] Record graph_id in agent-registry.yaml

## Phase 6: Maintainer Agent + Self-Heal Loop
- [ ] Create Maintainer Agent on AutoGPT Platform
  - HTTP health check blocks
  - AI diagnosis + fix generation
  - Agent Executor (calls Boss for fixes)
  - Scheduled trigger (cron)
- [ ] Test self-heal loop
- [ ] Record graph_id in agent-registry.yaml

## Phase 7: Full Autonomy
- [ ] Enable auto_deploy in config
- [ ] Enable auto_maintain in config
- [ ] Stress test with complex multi-file projects
- [ ] Add error recovery and fallback LLMs
- [ ] Build dashboard / monitoring UI
- [ ] SaaS-ready: multi-tenant support

## Success Criteria
- **Phase 2**: Writer generates working code from a prompt
- **Phase 3**: Builder validates writer output automatically
- **Phase 5**: "Build me a landing page" → deployed website in <5 min
- **Phase 6**: System detects and fixes its own broken deployments
- **Phase 7**: End-to-end autonomous operation with zero human intervention
