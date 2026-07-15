# <img src="https://raw.githubusercontent.com/TrustEdgeOrg/TrustEdge/develop/docs/assets/trustedge-icon.svg" alt="" width="36" height="36" align="absmiddle" /> TrustEdge

**Self-hosted security observability** — endpoint telemetry, rules-based detection, and attack alerts.

React dashboard · FastAPI control plane · [TrustEdge Agent](https://github.com/TrustEdgeOrg/TrustEdge-Agent) · [Agent API](https://github.com/TrustEdgeOrg/TrustEdge-Agent-API) · AWS deploy with CI/CD.

<p align="center">
  <img src="https://raw.githubusercontent.com/TrustEdgeOrg/TrustEdge/develop/docs/assets/pipeline.svg" alt="Endpoint → Collector → Batch → Compress → Secure upload → Agent API → Stream → Detection Attack → Alert" width="1000" />
</p>

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

## How it works

1. **Endpoint** — device running TrustEdge Agent  
2. **Collector → Batch → Compress** — on-device telemetry pipeline  
3. **Secure upload** — HTTPS to Agent API  
4. **Agent API → Stream** — validate, persist, publish  
5. **Detection Attack → Alert** — rules engine + dashboard alerts  

```text
Agent:   Endpoint → Agent API → Kafka → detection-engine → alerts → Dashboard
```

Deep dive: [System architecture](https://github.com/TrustEdgeOrg/TrustEdge/blob/develop/docs/SYSTEM_ARCHITECTURE.md) · [Docs index](https://github.com/TrustEdgeOrg/TrustEdge/tree/develop/docs)

---

## Architecture

<p align="center">
  <a href="https://github.com/TrustEdgeOrg/TrustEdge/blob/develop/docs/SYSTEM_ARCHITECTURE.md">
    <img width="90%" alt="TrustEdge system architecture" src="https://github.com/user-attachments/assets/bab37178-52c4-4f6d-b4ac-1500230d0af5" />
  </a>
</p>

| Layer | Components | Responsibility |
|-------|------------|----------------|
| **Endpoint agents** | TrustEdge Agent | Process, app, network posture |
| **Ingest** | TrustEdge-Agent-API | Auth, persist, Kafka publish |
| **Application** | FastAPI, detection-engine, React | Rules, alerts, UI |
| **Data** | PostgreSQL, Redis, Kafka/Redpanda | State, live usage, event bus |

---

## Tech stack

React · TypeScript · FastAPI · Go · PostgreSQL · Redis · Kafka/Redpanda · AWS (EC2, RDS, S3, CloudFront, ECR)
