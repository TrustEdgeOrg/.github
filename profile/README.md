# <img src="./assets/trustedge-icon.svg" alt="" width="40" height="40" align="absmiddle" /> TrustEdge

### Self-hosted security observability

**Endpoint telemetry · rules-based detection · attack alerts**

React dashboard · FastAPI control plane · TrustEdge Agent · Agent API · AWS

<br/>

## About the project

TrustEdge is a **self-hosted security observability platform**. It gives teams real endpoint signal and actionable detection without a heavyweight enterprise EDR stack.

A lightweight [TrustEdge Agent](https://github.com/TrustEdgeOrg/TrustEdge-Agent) runs on macOS, Linux, and Windows and collects:

- **Device & activity** — OS posture, foreground focus, idle vs active
- **Network** — connectivity summary and posture
- **Processes** — start and exit lifecycle
- **Security lifecycle** — drivers, services, and persistence
- **AI tools inventory** — apps, CLI agents, local model runtimes, and IDE extensions

Collectors stay on the device. Events land in a **durable on-disk queue**, then are compressed and uploaded over **HTTPS with a device token** to [TrustEdge-Agent-API](https://github.com/TrustEdgeOrg/TrustEdge-Agent-API). From there, Kafka streams events to a rules engine. The [TrustEdge](https://github.com/TrustEdgeOrg/TrustEdge) control plane shows **attack alerts**, the agents registry, **installed AI software**, and behavior views in a React dashboard.

Detection is **rules-based** and deterministic. Optional LLMs can explain state to operators — they never decide what is malicious.

Built for portfolio and educational use, with AWS deploy and GitHub Actions CI/CD.

<p align="center">
  <img src="./assets/pipeline.svg" alt="Endpoint → Collector → Durable queue → Compress → Secure upload → Agent API → Stream → Detection → Alert" width="1100" />
</p>

---

## <img src="./assets/icon-architecture.svg" alt="" width="22" height="22" align="absmiddle" /> TrustEdge architecture

Five stages from the endpoint to the operator dashboard.

<p align="center">
  <img src="./assets/architecture.svg" alt="TrustEdge architecture — Edge, Ingest, Stream, Detect, Operate" width="1100" />
</p>

| Layer | What lives here |
|-------|-----------------|
| **Edge** | TrustEdge Agent (Go) — collect · durable queue · compress · HTTPS |
| **Ingest** | Agent API (FastAPI) — device auth · validate · publish |
| **Stream** | Kafka / Redpanda — durable `trustedge.agent.events` bus |
| **Detection** | Rules engine — attack chains and drift → alerts |
| **Operate** | FastAPI + React — alerts, agents, AI software, behavior |
| **Data** | PostgreSQL (RDS) · Redis — source of truth · live state |
| **Hosting** | EC2 + Docker Compose · S3 + CloudFront · ECR |

---

## <img src="./assets/icon-flow.svg" alt="" width="22" height="22" align="absmiddle" /> Ecosystem map

Three repositories. One detection path — collect on the endpoint, ingest securely, then detect and operate.

<p align="center">
  <img src="./assets/ecosystem.svg" alt="TrustEdge ecosystem — Agent, Agent API, TrustEdge" width="1100" />
</p>

| Repository | Role |
|------------|------|
| [**TrustEdge**](https://github.com/TrustEdgeOrg/TrustEdge) | Control plane · dashboard · detection |
| [**TrustEdge-Agent**](https://github.com/TrustEdgeOrg/TrustEdge-Agent) | Endpoint collector (Go) |
| [**TrustEdge-Agent-API**](https://github.com/TrustEdgeOrg/TrustEdge-Agent-API) | Ingest · validate · Kafka |

---

## <img src="./assets/icon-collection.svg" alt="" width="22" height="22" align="absmiddle" /> Detection path

Kafka feeds a deterministic rules engine. Alerts are ingested into the control plane for operators to review. LLMs may summarize — they do not judge.

<p align="center">
  <img src="./assets/detection-path.svg" alt="Kafka → rules engine → alert ingest → attack alerts → operator" width="1100" />
</p>

---

## <img src="./assets/icon-architecture.svg" alt="" width="22" height="22" align="absmiddle" /> Observability graph

The twin links devices, processes, AI tools, and flows to rules and alerts. Use it for **impact analysis**, **blast radius**, and **root-cause analysis** — not decoration.

<p align="center">
  <img src="./assets/observability-graph.svg" alt="Observability graph: device → process / AI tool / flow → rule → alert" width="1100" />
</p>

---

## Platform at a glance

| Capability | Implementation |
|------------|----------------|
| Endpoint telemetry | Device, activity, network, process, security lifecycle, AI tools inventory |
| Reliable delivery | Durable queue · compress · HTTPS · retry with backoff |
| Detection | Kafka-backed rules → attack alerts |
| Observability | Alerts · agents registry · installed AI software · behavior |
| AI operations | Optional summaries (OpenAI / Ollama / templates) |
| Production ops | EC2 + Docker Compose · RDS · S3/CloudFront · ECR · GitHub Actions |

---

## Tech stack

`React` · `TypeScript` · `FastAPI` · `Go` · `PostgreSQL` · `Redis` · `Kafka/Redpanda` · `Docker` · `AWS`

---

**Docs:** [Architecture](https://github.com/TrustEdgeOrg/TrustEdge/blob/main/docs/SYSTEM_ARCHITECTURE.md) · [TrustEdge README](https://github.com/TrustEdgeOrg/TrustEdge/blob/main/README.md) · [Agent](https://github.com/TrustEdgeOrg/TrustEdge-Agent) · [Org](https://github.com/TrustEdgeOrg)
