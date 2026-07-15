# <img src="https://raw.githubusercontent.com/TrustEdgeOrg/TrustEdge/docs/readme-endpoint-focus/docs/assets/trustedge-icon.svg" alt="" width="36" height="36" align="absmiddle" /> TrustEdge

**Self-hosted security observability** — endpoint telemetry, rules-based detection, and attack alerts.

React dashboard · FastAPI control plane · [TrustEdge Agent](https://github.com/TrustEdgeOrg/TrustEdge-Agent) · [Agent API](https://github.com/TrustEdgeOrg/TrustEdge-Agent-API) · AWS deploy with CI/CD.

<p align="center">
  <img src="https://raw.githubusercontent.com/TrustEdgeOrg/TrustEdge/docs/readme-endpoint-focus/docs/assets/pipeline.svg" alt="Endpoint → Collector → Batch → Compress → Secure upload → Agent API → Stream → Detection Attack → Alert" width="1000" />
</p>

---

## Architecture

<p align="center">
  <a href="https://github.com/TrustEdgeOrg/TrustEdge/blob/develop/docs/SYSTEM_ARCHITECTURE.md">
    <img width="100%" alt="TrustEdge architecture — endpoint agents, Agent API, Kafka, detection engine, control plane, and dashboard" src="https://raw.githubusercontent.com/TrustEdgeOrg/TrustEdge/docs/readme-endpoint-focus/docs/assets/architecture.svg" />
  </a>
</p>

| Layer | Components | Responsibility |
|-------|------------|----------------|
| **Edge** | TrustEdge Agent | Collect · batch · compress · HTTPS upload |
| **Ingest** | TrustEdge-Agent-API | Auth · validate · persist · publish |
| **Stream** | Kafka / Redpanda | Durable agent event bus |
| **Detection** | detection-engine | Rules → attack alerts |
| **Control plane** | FastAPI · Twin | Alerts, graph, network map, devices |
| **Dashboard** | React · S3 · CloudFront | Operator views |
| **Host** *(optional)* | WireGuard · wg-agent | Enroll · quarantine |

---

## Why it exists

Most security tools are either heavy enterprise stacks or narrow point products. TrustEdge is a **unified, self-hosted** control plane for endpoint signal and detection:

| Path | What it does |
|------|----------------|
| **Endpoint** | [TrustEdge-Agent](https://github.com/TrustEdgeOrg/TrustEdge-Agent) → [TrustEdge-Agent-API](https://github.com/TrustEdgeOrg/TrustEdge-Agent-API) → stream → detection → alerts |
| **Dashboard** | Network map, client map, behavior drift, attack alerts |
| **Ops** | CloudWatch logs, Alembic, ECR deploy |

Detection and scoring stay **rules-based**. Optional LLMs only explain state for operators. Optional WireGuard enrollment and quarantine are available when you need secure access / response.

---

## Repositories

| Repository | Role |
|------------|------|
| [**TrustEdge**](https://github.com/TrustEdgeOrg/TrustEdge) | Control plane — FastAPI, React dashboard, detection engine, host agent, AWS deploy |
| [**TrustEdge-Agent**](https://github.com/TrustEdgeOrg/TrustEdge-Agent) | Endpoint collector — process, app focus, network posture |
| [**TrustEdge-Agent-API**](https://github.com/TrustEdgeOrg/TrustEdge-Agent-API) | Ingest · validate · persist · Kafka stream |
| [**TrustEdgeClient**](https://github.com/TrustEdgeOrg/TrustEdgeClient) | Optional WireGuard enroll client — usage + app context |

---

## How it works

1. **Endpoint** — device running TrustEdge Agent  
2. **Collector → Batch → Compress** — on-device telemetry pipeline  
3. **Secure upload** — HTTPS to Agent API  
4. **Agent API → Stream** — validate, persist, publish  
5. **Detection Attack → Alert** — rules engine + dashboard alerts  

Deep dive: [System architecture](https://github.com/TrustEdgeOrg/TrustEdge/blob/develop/docs/SYSTEM_ARCHITECTURE.md) · [Docs index](https://github.com/TrustEdgeOrg/TrustEdge/tree/develop/docs)

---

## Platform highlights

| Capability | Implementation |
|------------|----------------|
| Endpoint telemetry | TrustEdge Agent → Agent API → stream |
| Detection | Kafka-backed rules on agent events → attack alerts |
| Observability | Network map, client map, live usage, behavior drift |
| Secure access *(optional)* | WireGuard enrollment, IP pool |
| Enforcement *(optional)* | Host agent quarantine (iptables) |
| AI operations | Optional network / behavior summaries |
| Production ops | CloudWatch JSON logs, Alembic, ECR deploy |

---

## Tech stack

React · TypeScript · FastAPI · Go · PostgreSQL · Redis · Kafka/Redpanda · AWS (EC2, RDS, S3, CloudFront, ECR)
