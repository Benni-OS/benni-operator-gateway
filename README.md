<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0D0D0D,50:7000FF,100:00B0FF&height=200&section=header&text=BENNI%20OPERATOR%20GATEWAY&fontSize=52&fontColor=ffffff&fontAlignY=38&desc=Open-Source%20MCP%20Gateway%20for%20Autonomous%20AI%20Operators&descAlignY=58&descSize=16&animation=fadeIn" width="100%"/>

<br/>

<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=700&size=20&duration=3000&pause=800&color=7000FF&center=true&vCenter=true&multiline=true&repeat=true&width=800&height=80&lines=Self-Host+Your+MCP+Infrastructure+%E2%9A%A1;Approval+Gate+%E2%80%A2+Hot-Reload+Registry+%E2%80%A2+Decision+Ledger;Connect+Any+LLM+%E2%80%94+No+Third-Party+Control" alt="Typing SVG" />

<br/><br/>

[![License: MIT](https://img.shields.io/badge/License-MIT-7000FF?style=for-the-badge&logo=opensourceinitiative&logoColor=white)](LICENSE)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-00B0FF?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Node.js](https://img.shields.io/badge/Node.js-20%2B-00C853?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)
[![MCP Compatible](https://img.shields.io/badge/MCP-Compatible-FF007A?style=for-the-badge&logo=protocol&logoColor=white)](https://modelcontextprotocol.io/)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-FF6D00?style=for-the-badge&logo=github&logoColor=white)](CONTRIBUTING.md)
[![Benni OS](https://img.shields.io/badge/Benni%20OS-benni--os.net-0D0D0D?style=for-the-badge)](https://benni-os.net)

<br/>

> **"You need a gate, not a rubber stamp."**

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png" width="100%"/>

<br/>

<img src="assets/demo.gif" alt="Benni Operator Gateway Terminal Demo" width="100%"/>

<br/>

</div>

<br/>

## ⭐ What Is Benni Operator Gateway?

**Benni Operator Gateway** is the open-source MCP infrastructure layer of the **[Benni OS](https://github.com/benni-os)** ecosystem — a production-grade HTTP gateway implementing the [Model Context Protocol](https://modelcontextprotocol.io/), purpose-built for autonomous AI operators.

It gives any MCP-compatible client (Claude Desktop, Cursor, custom agents, CI pipelines) a single, secure, extensible interface to interact with your tools, services, and data — without surrendering control to third-party managed APIs.

```
INTENTION → AI CLIENT → MCP OVER HTTP → OPERATOR GATEWAY → APPROVAL GATE → EXECUTION → AUDIT LOG
```

<br/>

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/dark.png" width="100%"/>

## ⚡ Core Doctrine

> These are not settings. These are architecture laws.

| ☔ Principle | 🔧 Implementation |
|---|---|
| **Gate, Not Rubber Stamp** | Every sensitive action is intercepted — agent pauses, human approves, then execution resumes |
| **Hot-Reload Registry** | Add or remove connectors live — zero downtime, zero redeploy |
| **Decision Ledger** | Every tool dispatch logged with full context — tamper-evident, append-only |
| **Provider-Agnostic** | Route any LLM behind one interface — no lock-in, no vendor dependency |
| **Session Continuity** | Built-in Control Plane persists state and atomic checkpoints across agent runs |
| **Open Core** | Gateway is, and will remain, fully MIT — build on it, fork it, contribute back |

<br/>

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/dark.png" width="100%"/>

## 🏗️ Architecture

```mermaid
graph TD
    style GW fill:#0D0D0D,color:#fff,stroke:#7000FF,stroke-width:2px
    style CR fill:#1a1a2e,color:#fff,stroke:#00B0FF,stroke-width:1px
    style AG fill:#1a1a2e,color:#fff,stroke:#FF007A,stroke-width:1px
    style CP fill:#1a1a2e,color:#fff,stroke:#FF6D00,stroke-width:1px

    A["AI Client\nClaude · Cursor · Agent · Pipeline"] -->|MCP over HTTP| GW["⚡ Benni Operator Gateway"]

    subgraph CR ["🔌 Connector Registry (hot-reload)"]
        D["jarvas2 ✅ Stable"]
        E["github ✅ Stable"]
        F["custom connectors"]
    end

    subgraph AG ["🛡️ Approval Gate Middleware"]
        G["Intercept → Webhook → Human"]
        H["approve_url / reject_url"]
    end

    subgraph CP ["🧠 Control Plane (built-in)"]
        J["Session State"]
        K["Decision Ledger"]
        L["Atomic Checkpoints"]
    end

    GW --> CR
    GW --> AG
    GW --> CP
```

<br/>

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/dark.png" width="100%"/>

## 🚀 Quick Start

```bash
# 1. Clone
git clone https://github.com/benni-os/benni-operator-gateway
cd benni-operator-gateway

# 2. Install
npm install

# 3. Configure
cp .env.example .env
# Edit .env — set GATEWAY_API_KEY, APPROVAL_WEBHOOK_URL, GITHUB_TOKEN

# 4. Run (development)
npm run dev

# 4b. Run (production)
npm run build && npm start
```

Your MCP gateway is live at `http://localhost:3000`.
Point any MCP-compatible client to `http://localhost:3000/mcp`.

<br/>

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/dark.png" width="100%"/>

## 🔌 Built-in Connectors

| Connector | Status | Description |
|---|---|---|
| `jarvas2` | ✅ Stable | JARVAS-2 agent runtime — dispatch tasks, queue jobs, set objectives, read operational memory |
| `github` | ✅ Stable | Full GitHub API surface — issues, PRs, code search, reviews, branch management, secret scanning |
| `control-plane` | 🔧 Beta | Gateway-native session state, atomic checkpoints, decision ledger — no external dependency |

> The gateway is fully functional as a standalone MCP gateway. JARVAS-2 and Benni Control Plane are optional — connect any agent backend or build your own connector.

<br/>

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/dark.png" width="100%"/>

## 🛡️ Approval Gate

The built-in **human-in-the-loop middleware** intercepts any tool call marked `requires_approval: true`. The agent pauses, your webhook fires, nothing executes until you approve or reject.

```typescript
// Payload sent to APPROVAL_WEBHOOK_URL
{
  "action": "deploy_to_production",
  "reason": "Agent requested deployment after build passed",
  "payload": { ... },
  "approve_url": "https://your-gateway/approve/req_abc123",
  "reject_url":  "https://your-gateway/reject/req_abc123"
}
```

**Pause → Notify → Resume.** The core safety primitive for running agents against real infrastructure.

<br/>

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/dark.png" width="100%"/>

## ⚙️ Configuration

```bash
# Server
PORT=3000
NODE_ENV=production

# Auth
GATEWAY_API_KEY=your_secret_key

# Approval Gate
APPROVAL_WEBHOOK_URL=https://your-endpoint/approval
APPROVAL_TIMEOUT_MS=300000  # 5 minutes

# Project Benjamin Connector (optional)
BENJAMIN_API_URL=https://your-benjamin-instance
BENJAMIN_API_KEY=your_benjamin_key
# Legacy fallback:
JARVAS2_API_URL=https://your-benjamin-instance
JARVAS2_API_KEY=your_benjamin_key

# GitHub Connector
GITHUB_TOKEN=your_github_pat
```

<br/>

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/dark.png" width="100%"/>

## 📁 Project Structure

```
src/
├── app.ts               # Server bootstrap
├── index.ts             # Entrypoint
├── config/              # Environment & provider config
├── connectors/          # MCP connector modules
│   ├── jarvas2/         # JARVAS-2 connector
│   └── github/          # GitHub MCP connector
├── middleware/          # Auth, approval gate, rate limiting
├── registry/            # Hot-reload connector registry
├── routes/              # HTTP endpoints
├── services/            # LLM dispatch, session management
└── types/               # TypeScript contracts
```

<br/>

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/dark.png" width="100%"/>

## 🚢 Deployment

```bash
# Docker
docker build -t benni-operator-gateway .
docker run -p 3000:3000 --env-file .env benni-operator-gateway

# Fly.io (fly.toml included)
fly deploy

# Any VPS / cloud VM
npm run build && npm start
```

<br/>

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/dark.png" width="100%"/>

## 🗺️ Roadmap

- [x] MCP HTTP gateway core
- [x] Project Benjamin connector
- [x] GitHub connector
- [x] Human approval gate
- [x] Built-in Control Plane (session state, ledger, checkpoints)
- [ ] npm package `@benni-os/operator-gateway`
- [ ] Docker image + one-click Railway / Render deploy
- [ ] Web dashboard (runs · decisions · health)
- [ ] Plugin SDK for custom connector development
- [ ] OpenTelemetry tracing integration
- [ ] Multi-tenant workspace isolation

<br/>

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/dark.png" width="100%"/>

## 🤝 Contributing

Contributions welcome — especially new connectors. See [CONTRIBUTING.md](CONTRIBUTING.md).

Highest-value contributions right now:
- New MCP connectors (Notion, Linear, Slack, Supabase, etc.)
- Improved approval gate delivery (email, Telegram, SMS)
- Docker Compose + one-click deploy configurations
- Observability integrations (OpenTelemetry, Grafana)

<br/>

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/dark.png" width="100%"/>

## 🌐 The Benni OS Open-Source Ecosystem

`benni-operator-gateway` is part of the coordinated **Benni Master OS v9.4** open-source infrastructure suite:

| Repository | Focus & Architecture | Stars |
| :--- | :--- | :---: |
| **[`conductor-sdd`](https://github.com/Benni-OS/conductor-sdd)** | Zero-Dependency Spec-Driven Development, Static AST Drift Detector & MCP Guardrail | [![GitHub Stars](https://img.shields.io/github/stars/Benni-OS/conductor-sdd?style=flat)](https://github.com/Benni-OS/conductor-sdd) |
| **[`benni-inference-engine`](https://github.com/Benni-OS/benni-inference-engine)** | High-Throughput Sovereign Local Inference for 8GB–16GB Consumer GPUs | [![GitHub Stars](https://img.shields.io/github/stars/Benni-OS/benni-inference-engine?style=flat)](https://github.com/Benni-OS/benni-inference-engine) |
| **[`agent-eval-harness`](https://github.com/BenniAlencar/agent-eval-harness)** | Deterministic Zero-Cloud Agent Evaluation, Red-Teaming & Benchmark Harness | [![GitHub Stars](https://img.shields.io/github/stars/BenniAlencar/agent-eval-harness?style=flat)](https://github.com/BenniAlencar/agent-eval-harness) |
| **[`agent-code-sandbox`](https://github.com/BenniAlencar/agent-code-sandbox)** | Micro-Second Zero-Dependency Code Sandbox & Execution Shield for AI Agents | [![GitHub Stars](https://img.shields.io/github/stars/BenniAlencar/agent-code-sandbox?style=flat)](https://github.com/BenniAlencar/agent-code-sandbox) |
| **[`agent-deep-research`](https://github.com/BenniAlencar/agent-deep-research)** | Autonomous Multi-Source Deep Research & Evidence Synthesis Engine | [![GitHub Stars](https://img.shields.io/github/stars/BenniAlencar/agent-deep-research?style=flat)](https://github.com/BenniAlencar/agent-deep-research) |
| **[`agent-browser-mesh`](https://github.com/BenniAlencar/agent-browser-mesh)** | Token-Saving Resilient Headless Browser Automation & A11y DOM Compiler | [![GitHub Stars](https://img.shields.io/github/stars/BenniAlencar/agent-browser-mesh?style=flat)](https://github.com/BenniAlencar/agent-browser-mesh) |
| **[`agent-intent-compiler`](https://github.com/BenniAlencar/agent-intent-compiler)** | Deterministic Intent Compiler & Typed DAG Execution Planner for AI Agents | [![GitHub Stars](https://img.shields.io/github/stars/BenniAlencar/agent-intent-compiler?style=flat)](https://github.com/BenniAlencar/agent-intent-compiler) |
| **[`agent-token-optimizer`](https://github.com/BenniAlencar/agent-token-optimizer)** | Sub-Millisecond Context Compression & Semantic Deduplication Engine | [![GitHub Stars](https://img.shields.io/github/stars/BenniAlencar/agent-token-optimizer?style=flat)](https://github.com/BenniAlencar/agent-token-optimizer) |
| **[`bio-sync-operator-os`](https://github.com/BenniAlencar/bio-sync-operator-os)** | Real-Time Biometric Swarm Governance & 120 FPS Resonant Kinetic Interface | [![GitHub Stars](https://img.shields.io/github/stars/BenniAlencar/bio-sync-operator-os?style=flat)](https://github.com/BenniAlencar/bio-sync-operator-os) |
| **[`agent-cyber-sentinel`](https://github.com/BenniAlencar/agent-cyber-sentinel)** | Zero-Trust Runtime Security, Prompt Injection Firewall & Secrets Redaction | [![GitHub Stars](https://img.shields.io/github/stars/BenniAlencar/agent-cyber-sentinel?style=flat)](https://github.com/BenniAlencar/agent-cyber-sentinel) |
| **[`agent-run-ledger`](https://github.com/BenniAlencar/agent-run-ledger)** | Deterministic Multi-Step Task Execution Ledger & Anti-Looping Engine | [![GitHub Stars](https://img.shields.io/github/stars/BenniAlencar/agent-run-ledger?style=flat)](https://github.com/BenniAlencar/agent-run-ledger) |
| **[`reality-lock`](https://github.com/BenniAlencar/reality-lock)** | Cryptographic State Verification & Invariant Proof Engine for Agents | [![GitHub Stars](https://img.shields.io/github/stars/BenniAlencar/reality-lock?style=flat)](https://github.com/BenniAlencar/reality-lock) |
| **[`agent-memory-mesh`](https://github.com/BenniAlencar/agent-memory-mesh)** | Hybrid Vector + BM25 Hierarchical Session Memory & Continuity Engine | [![GitHub Stars](https://img.shields.io/github/stars/BenniAlencar/agent-memory-mesh?style=flat)](https://github.com/BenniAlencar/agent-memory-mesh) |
| **[`benni-operator-gateway`](https://github.com/Benni-OS/benni-operator-gateway)** | Human-in-the-Loop Approval & Policy Enforcement Gateway | [![GitHub Stars](https://img.shields.io/github/stars/Benni-OS/benni-operator-gateway?style=flat)](https://github.com/Benni-OS/benni-operator-gateway) |
| **[`mcp-forge`](https://github.com/Benni-OS/mcp-forge)** | Rapid Model Context Protocol (MCP) Server Scaffolding & Dynamic Tooling | [![GitHub Stars](https://img.shields.io/github/stars/Benni-OS/mcp-forge?style=flat)](https://github.com/Benni-OS/mcp-forge) |
| **[`benni-nexus`](https://github.com/Benni-OS/benni-nexus)** | Autonomous Multi-Agent Intent Routing & Swarm Coordination Hub | [![GitHub Stars](https://img.shields.io/github/stars/Benni-OS/benni-nexus?style=flat)](https://github.com/Benni-OS/benni-nexus) |
| **[`community-autopilot`](https://github.com/Benni-OS/community-autopilot)** | Autonomous GitHub Community Triaging & PR Feedback Agent | [![GitHub Stars](https://img.shields.io/github/stars/Benni-OS/community-autopilot?style=flat)](https://github.com/Benni-OS/community-autopilot) |

---

## 🏛️ Commercial & Sovereign Architecture

Need autonomous multi-agent swarm orchestration, private datacenter infrastructure, or enterprise governance?

- **Official Website:** [https://benni-os.net](https://benni-os.net)
- **Operator Mode Playbook:** [https://benni-os.net/blog/academy.html](https://benni-os.net/blog/academy.html)
- **GitHub Organization:** [https://github.com/Benni-OS](https://github.com/Benni-OS)
- **Maintainer:** [Benni Alencar](https://github.com/BenniAlencar)

---

## 📄 License & Provenance

- **License:** [MIT License](LICENSE)
- **Author:** Benni Alencar (`bennialencar@benni-os.net`)
- **Architecture:** Benni Master OS v9.4 Tier-0 Governance Standard

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:00B0FF,50:7000FF,100:0D0D0D&height=120&section=footer" width="100%"/>

**BENNI OPERATOR GATEWAY** — *Open-Source MCP Infrastructure by [Benni OS](https://github.com/Benni-OS)* • [benni-os.net](https://benni-os.net) • `MIT License`

`MIT_LICENSE` • `APPROVAL_GATE` • `HOT_RELOAD` • `DECISION_LEDGER` • `ZERO_VENDOR_LOCK`

Engineered by **Benni Alencar** and the Benni OS Core Engineering Group

</div>
