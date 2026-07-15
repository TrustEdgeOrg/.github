# <img src="./assets/trustedge-icon.svg" alt="" width="40" height="40" align="absmiddle" /> TrustEdge

### Self-hosted security observability

**Endpoint telemetry · rules-based detection · attack alerts**

React dashboard · FastAPI control plane · TrustEdge Agent · Agent API · AWS

<br/>

<p align="center">
  <img src="./assets/pipeline.svg" alt="Endpoint → Collector → Batch → Compress → Secure upload → Agent API → Stream → Detection Attack → Alert" width="1100" />
</p>

---

## <img src="./assets/icon-architecture.svg" alt="" width="22" height="22" align="absmiddle" /> TrustEdge architecture

How the stack fits together — edge collection, secure ingest, stream detection, and the operator dashboard.

<p align="center">
  <img src="./assets/architecture-v4.png" alt="TrustEdge architecture — 5 clear stages from endpoint agent to dashboard" width="1100" />
</p>

| Layer | What lives here |
|-------|-----------------|
| **Edge** | TrustEdge Agent — collect · batch · compress · HTTPS |
| **Ingest** | Agent API — auth · validate · persist · publish |
| **Stream** | Kafka / Redpanda — durable `agent.events` bus |
| **Detection** | Rules engine — deterministic attack / drift rules |
| **Control plane** | FastAPI · Twin — alerts, graph, maps, devices |
| **Dashboard** | React · S3 · CloudFront — operator views |

---

## <img src="./assets/icon-flow.svg" alt="" width="22" height="22" align="absmiddle" /> Ecosystem map

Three repositories, one detection path.

<p align="center">
  <img src="./assets/ecosystem.svg" alt="TrustEdge ecosystem — Agent, Agent API, TrustEdge" width="1100" />
</p>

| Repository | Role |
|------------|------|
| [**TrustEdge**](https://github.com/TrustEdgeOrg/TrustEdge/tree/docs/readme-endpoint-focus) | Control plane · dashboard · detection |
| [**TrustEdge-Agent**](https://github.com/TrustEdgeOrg/TrustEdge-Agent) | Endpoint collector (Go) |
| [**TrustEdge-Agent-API**](https://github.com/TrustEdgeOrg/TrustEdge-Agent-API) | Ingest · validate · Kafka |

---

## <img src="./assets/icon-collection.svg" alt="" width="22" height="22" align="absmiddle" /> Detection path

Rules stay deterministic. LLMs only explain — they do not decide.

<p align="center">
  <img src="./assets/detection-path.svg" alt="Kafka → rules engine → twin alert ingest → dashboard" width="1100" />
</p>

---

## <img src="./assets/icon-architecture.svg" alt="" width="22" height="22" align="absmiddle" /> Observability graph

Canonical twin model for impact analysis, blast radius, and RCA — entities and dependencies, not a layout toy.

<p align="center">
  <img src="./assets/observability-graph.svg" alt="Observability graph: device, app, process, flow, rule, alert" width="1100" />
</p>

---

## Platform at a glance

| Capability | Implementation |
|------------|----------------|
| Endpoint telemetry | TrustEdge Agent → Agent API → stream |
| Detection | Kafka-backed rules → attack alerts |
| Observability | Network map · client map · behavior drift · graph |
| AI operations | Optional summaries (OpenAI / Ollama / template) |
| Production ops | CloudWatch · Alembic · ECR deploy |

---

## Tech stack

`React` · `TypeScript` · `FastAPI` · `Go` · `PostgreSQL` · `Redis` · `Kafka/Redpanda` · `AWS`

---

**Docs:** [Architecture](https://github.com/TrustEdgeOrg/TrustEdge/blob/docs/readme-endpoint-focus/docs/SYSTEM_ARCHITECTURE.md) · [TrustEdge README](https://github.com/TrustEdgeOrg/TrustEdge/blob/docs/readme-endpoint-focus/README.md) · [Org](https://github.com/TrustEdgeOrg)
