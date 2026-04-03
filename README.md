# Azure AI Agent Patterns

A growing collection of standalone Python projects, each isolating a distinct orchestration pattern on **Azure AI Foundry**. Every project is self-contained — its own virtual environment, credentials, and README — so you can run or study any one independently.

The progression moves from single-agent primitives (tool use, code execution, persistent state) through multi-agent topologies (hierarchical, sequential, concurrent, handoff, group chat), MCP-based tool servers, and into A2A remote microservices.

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
| 11 | [Travel Itinerary Planner](https://github.com/rajshrinivasan/travel-itinerary-planner-foundry-agent) | A2A Remote Microservices — orchestrator routes to 3 independent FastAPI agent services over HTTP; streaming output; `.ics` / `.pdf` export | [→](https://github.com/rajshrinivasan/travel-itinerary-planner-foundry-agent) |
| 12 | [Product Support Agent](https://github.com/rajshrinivasan/product-support-foundry-agent) | Knowledge Base Grounding — FileSearchTool + VectorStore; streaming responses; source citations; persistent vector store across sessions | [→](https://github.com/rajshrinivasan/product-support-foundry-agent) |
| 13 | [Bug Triage Workflow](https://github.com/rajshrinivasan/bug-triage-workflow-foundry-agent) | Conditional DAG Workflow — LLM classifier routes to critical escalation, sprint triage, or backlog branch; Python controls flow, LLM controls content | [→](https://github.com/rajshrinivasan/bug-triage-workflow-foundry-agent) |

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

Remote microservices (A2A)
  11  A2A over HTTP             — orchestrator knows agents only by URL; parallel dispatch; streaming

Knowledge base grounding
  12  FileSearchTool + VectorStore — upload, chunk, embed, retrieve; streaming; persistent store

Conditional DAG workflow
  13  WorkflowEngine              — declared graph, Python branch conditions, JSON step outputs
```

---

## Stack

- **Python 3.11+**
- **azure-ai-projects** — Responses API, Code Interpreter (Projects 01–03)
- **azure-ai-agents** — Thread/Run model, ConnectedAgentTool (Project 04)
- **agent-framework-foundry** — SequentialBuilder, ConcurrentBuilder, HandoffBuilder, GroupChatBuilder (Projects 05–08)
- **mcp + fastmcp** — stdio transport, runtime tool discovery (Projects 09–10)
- **fastapi + httpx + tenacity** — A2A HTTP microservices, parallel dispatch, retries (Project 11)
- **azure-ai-agents** — AgentsClient, FileSearchTool, streaming via `runs.stream()` (Project 12)
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
