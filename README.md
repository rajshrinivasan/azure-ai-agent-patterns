# Azure AI Agent Patterns

A collection of 10 standalone Python projects, each isolating a distinct orchestration pattern on **Azure AI Foundry**. Every project is self-contained — its own virtual environment, credentials, and README — so you can run or study any one independently.

The progression moves from single-agent primitives (tool use, code execution, persistent state) through multi-agent topologies (hierarchical, sequential, concurrent, handoff, group chat) and into MCP-based tool servers (runtime tool discovery via stdio).

---

## Projects

| # | Project | Pattern | Repo |
|---|---------|---------|------|
| 01 | [Portfolio Risk Analyzer](https://github.com/rajshrinivasan/portfolio-risk-analyzer-foundry-agent) | Code Interpreter — CSV upload, stateful analysis loop | [→](https://github.com/rajshrinivasan/portfolio-risk-analyzer-foundry-agent) |
| 02 | [Sports Odds Companion](https://github.com/rajshrinivasan/sports-odds-companion-foundry-agent) | Function Tools — 4 read-only tools, `previous_response_id` chaining | [→](https://github.com/rajshrinivasan/sports-odds-companion-foundry-agent) |
| 03 | [IT Asset Lifecycle Manager](https://github.com/rajshrinivasan/it-asset-lifecycle-manager-foundry-agent) | Function Tools with state — 7 tools, write-back to JSON CMDB, audit trail | [→](https://github.com/rajshrinivasan/it-asset-lifecycle-manager-foundry-agent) |
| 04 | [Policy Debate Simulator](https://github.com/rajshrinivasan/policy-debate-simulator-foundry-agent) | ConnectedAgentTool — 3 specialist agents wrapped as tools under a conductor | [→](https://github.com/rajshrinivasan/policy-debate-simulator-foundry-agent) |
| 05 | [Legal Contract Drafter](https://github.com/rajshrinivasan/legal-contract-drafter-foundry-agent) | SequentialBuilder — 4-stage pipeline: extract → annotate → summarise → redline | [→](https://github.com/rajshrinivasan/legal-contract-drafter-foundry-agent) |
| 06 | [Competitive Intelligence Brief](https://github.com/rajshrinivasan/competitive-intel-brief-foundry-agent) | ConcurrentBuilder — 5 researchers run in parallel, synthesiser merges outputs | [→](https://github.com/rajshrinivasan/competitive-intel-brief-foundry-agent) |
| 07 | [Tiered Complaint Handler](https://github.com/rajshrinivasan/tiered-complaint-handler-foundry-agent) | HandoffBuilder — triage routes to tier 1/2/3; escalation chain with context transfer | [→](https://github.com/rajshrinivasan/tiered-complaint-handler-foundry-agent) |
| 08 | [Film Pitch Development Room](https://github.com/rajshrinivasan/film-pitch-room-foundry-agent) | GroupChatBuilder — 4 agents share a conversation; terminates on emergent consensus | [→](https://github.com/rajshrinivasan/film-pitch-room-foundry-agent) |
| 09 | [Developer Onboarding Assistant](https://github.com/rajshrinivasan/developer-onboarding-assistant-foundry-agent) | MCP stdio — agent spawns FastMCP server, discovers 5 tools at runtime | [→](https://github.com/rajshrinivasan/developer-onboarding-assistant-foundry-agent) |
| 10 | [Jira Sprint Coach](https://github.com/rajshrinivasan/jira-sprint-coach-foundry-agent) | MCP stdio — 6 Jira tools; agent is credential-free, server is the integration boundary | [→](https://github.com/rajshrinivasan/jira-sprint-coach-foundry-agent) |

---

## Pattern progression

```
Single agent
  01  Code Interpreter          — file upload, iterative analysis
  02  Function Tools (read)     — tool dispatch, response chaining
  03  Function Tools (write)    — persistent state, audit trail

Hierarchical / orchestrated
  04  ConnectedAgentTool        — specialist agents as callable tools

Sequential pipeline
  05  SequentialBuilder         — each agent sees the accumulated history

Parallel / concurrent
  06  ConcurrentBuilder         — fan-out then manual synthesis

Dynamic routing
  07  HandoffBuilder            — runtime routing, context transfer on escalation

Collaborative / emergent
  08  GroupChatBuilder          — shared conversation, consensus termination

External tool servers
  09  MCP stdio (5 tools)       — runtime tool discovery, subprocess transport
  10  MCP stdio (6 tools)       — credential isolation at the server boundary
```

---

## Stack

- **Python 3.11+**
- **azure-ai-projects** — Responses API, Code Interpreter (Projects 01–03)
- **azure-ai-agents** — Thread/Run model, ConnectedAgentTool (Project 04)
- **agent-framework-foundry** — SequentialBuilder, ConcurrentBuilder, HandoffBuilder, GroupChatBuilder (Projects 05–08)
- **mcp + fastmcp** — stdio transport, runtime tool discovery (Projects 09–10)
- **Azure DefaultAzureCredential** — `az login` for local dev, managed identity in production

---

## Prerequisites (all projects)

- Python 3.11+
- An [Azure AI Foundry](https://ai.azure.com/) project with a **gpt-4.1** (or gpt-4o) model deployment
- Azure CLI installed and logged in (`az login`)

Each project README contains full setup and running instructions.

---

## License

MIT
