# TrustEdge

**Self-hosted security observability** — endpoint telemetry, rules-based detection, VPN enrollment, and optional quarantine.

React dashboard · FastAPI control plane · TrustEdge Agent · WireGuard · AWS deploy with CI/CD.

---

## Pipeline

```text
Endpoint → Collector → Batch → Compress → Secure upload → Agent API → Stream → Detection Attack → Alert
```

---

## Repositories

| Repository | Role |
|------------|------|
| [**TrustEdge**](https://github.com/TrustEdgeOrg/TrustEdge) | Control plane — FastAPI backend, React dashboard, detection, host agent, AWS deploy |
| [**TrustEdge-Agent**](https://github.com/TrustEdgeOrg/TrustEdge-Agent) | Endpoint collector — process, app focus, network posture |
| [**TrustEdge-Agent-API**](https://github.com/TrustEdgeOrg/TrustEdge-Agent-API) | Ingest · validate · persist · Kafka stream |
| [**TrustEdgeClient**](https://github.com/TrustEdgeOrg/TrustEdgeClient) | WireGuard enroll client — menu bar app, usage + app context |

---

## Platform highlights

| Capability | Implementation |
|------------|----------------|
| Endpoint telemetry | TrustEdge Agent → Agent API → stream |
| Detection | Kafka-backed rules on agent events → attack alerts |
| Secure access | WireGuard VPN, device enrollment, IP pool |
| Observability | Network map, client map, live usage, behavior drift |
| Enforcement | Host agent quarantine (iptables, opt-in) |
| AI operations | Optional network / behavior summaries (OpenAI / Ollama / template) |
| Production ops | CloudWatch JSON logs, Alembic, ECR deploy |

---

## Architecture

<p align="center">
  <a href="https://github.com/TrustEdgeOrg/TrustEdge/blob/develop/docs/SYSTEM_ARCHITECTURE.md">
    <img width="90%" alt="TrustEdge system architecture" src="https://github.com/user-attachments/assets/bab37178-52c4-4f6d-b4ac-1500230d0af5" />
  </a>
</p>

```text
Agent:   Endpoint → Agent API → Kafka → detection-engine → alerts → Dashboard
Enroll:  TrustEdgeClient → control plane → wg-agent → WireGuard config
Access:  Client → WireGuard → usage / app context → Dashboard
```

Docs: [TrustEdge/docs](https://github.com/TrustEdgeOrg/TrustEdge/tree/develop/docs)

---

## Tech stack

React · TypeScript · FastAPI · Go · PostgreSQL · Redis · Kafka/Redpanda · WireGuard · AWS (EC2, RDS, S3, CloudFront, ECR)
