# <img src="./assets/trustedge-icon.svg" alt="" width="40" height="40" align="absmiddle" /> TrustEdge

### Self-hosted security observability

**Endpoint telemetry · rules-based detection · attack alerts**

React dashboard · FastAPI control plane · TrustEdge Agent · Agent API · AWS

<br/>

## About the project

TrustEdge is a **self-hosted security observability platform** for teams that want real endpoint signal and actionable detection without buying a heavy enterprise EDR stack.

A lightweight [TrustEdge Agent](https://github.com/TrustEdgeOrg/TrustEdge-Agent) runs on macOS, Linux, and Windows. It collects:

- **Device & activity** — OS posture, foreground focus / idle
- **Network** — connectivity summary and posture
- **Processes** — start / exit lifecycle
- **Security lifecycle** — drivers, services, persistence
- **AI tools inventory** — apps, CLI agents, local model runtimes, IDE extensions

Collectors stay local. Events go into a **durable on-disk queue**, are batched and compressed, then uploaded over **HTTPS with a device token** to [TrustEdge-Agent-API](https://github.com/TrustEdgeOrg/TrustEdge-Agent-API). Events stream on Kafka; a rules engine looks for attack chains and drift; the [TrustEdge](https://github.com/TrustEdgeOrg/TrustEdge) control plane surfaces **attack alerts**, the agents registry, **installed AI software**, and behavior views in a React dashboard.

Detection stays **rules-based** (deterministic). Optional LLMs only help explain state to operators — they do not decide what is malicious.

Built for portfolio / educational use and AWS deploy with CI/CD.

<p align="center">
  <img src="./assets/pipeline.svg" alt="Endpoint → Collector → Batch → Compress → Secure upload → Agent API → Stream → Detection → Alert" width="1100" />
</p>

---

## <img src="./assets/icon-architecture.svg" alt="" width="22" height="22" align="absmiddle" /> TrustEdge architecture

How the stack fits together — edge collection, secure ingest, stream detection, and the operator dashboard.

<p align="center">
  <img src="./assets/architecture.svg" alt="TrustEdge architecture — Edge, Ingest, Stream, Detect, Operate" width="1100" />
</p>

| Layer | What lives here |
|-------|-----------------|
| **Edge** | TrustEdge Agent — collect · durable queue · batch · compress · HTTPS |
| **Ingest** | Agent API — device auth · validate · persist · publish |
| **Stream** | Kafka / Redpanda — durable `trustedge.agent.events` bus |
| **Detection** | Rules engine — deterministic attack / drift rules |
| **Control plane** | FastAPI · Twin — alerts, agents, AI inventory, behavior |
| **Dashboard** | React · S3 · CloudFront — operator views |
| **Data** | PostgreSQL (RDS) · Redis — source of truth · live state |

---

## <img src="./assets/icon-flow.svg" alt="" width="22" height="22" align="absmiddle" /> Ecosystem map

Three repositories, one detection path.

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

Rules stay deterministic. LLMs only explain — they do not decide.

<p align="center">
  <img src="./assets/detection-path.svg" alt="Kafka → rules engine → alert ingest → dashboard" width="1100" />
</p>

---

## <img src="./assets/icon-architecture.svg" alt="" width="22" height="22" align="absmiddle" /> Observability graph

Canonical twin model — devices, processes, AI tools, and flows linked to rules and alerts. Used for **impact analysis**, **blast radius**, and **RCA** (not a layout toy).

<p align="center">
  <img src="./assets/observability-graph.svg" alt="Observability graph: device → process / AI tool / flow → rule → alert" width="1100" />
</p>

---

## Platform at a glance

| Capability | Implementation |
|------------|----------------|
| Endpoint telemetry | Device, activity, network, process, security lifecycle, AI tools inventory |
| Reliable delivery | Durable queue · batch · compress · HTTPS · retry / backoff |
| Detection | Kafka-backed rules → attack alerts |
| Observability | Attack alerts · agents registry · installed AI software · behavior |
| AI operations | Optional summaries (OpenAI / Ollama / template) |
| Production ops | EC2 + Docker Compose · RDS · S3/CloudFront · ECR · GitHub Actions |

---

## Tech stack

`React` · `TypeScript` · `FastAPI` · `Go` · `PostgreSQL` · `Redis` · `Kafka/Redpanda` · `Docker` · `AWS`

---

**Docs:** [Architecture](https://github.com/TrustEdgeOrg/TrustEdge/blob/main/docs/SYSTEM_ARCHITECTURE.md) · [TrustEdge README](https://github.com/TrustEdgeOrg/TrustEdge/blob/main/README.md) · [Agent](https://github.com/TrustEdgeOrg/TrustEdge-Agent) · [Org](https://github.com/TrustEdgeOrg)
