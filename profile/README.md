# NetGarde

**Self-hosted zero-trust network security platform** — WireGuard VPN access, DNS policy enforcement, real-time monitoring, behavior analytics, and optional AI-assisted operations.

A **SASE-style stack** you operate on your own infrastructure: enterprise-grade visibility and control without appliance lock-in.

---

## Repositories

| Repository | Description |
|------------|-------------|
| [**NetGarde**](https://github.com/NetGarde/NetGarde) | Platform — FastAPI backend, React dashboard, dns-sync, host agents, AWS deployment |
| [**NetGardeClient**](https://github.com/NetGarde/NetGardeClient) | macOS WireGuard client — API enroll, menu bar app, usage reporting |

---

## Platform highlights

| Capability | Implementation |
|------------|----------------|
| Secure access | WireGuard VPN, device enrollment, IP pool allocation |
| DNS policy | Policy packs, device profiles, schedules, geo rules |
| Real-time monitoring | WebSocket live feed, Redis-backed throughput charts |
| Behavior intelligence | Per-device baselines, abnormal scoring, quarantine |
| Enforcement | Host agent (iptables), dns-sync → dnsmasq reload |
| AI operations | Network + behavior summaries (OpenAI / Ollama / template) |

---

## Architecture

<p align="center">
  <a href="https://github.com/NetGarde/NetGarde/blob/develop/docs/SYSTEM_ARCHITECTURE.md">
    <img width="90%" alt="NetGarde system architecture" src="https://github.com/user-attachments/assets/bab37178-52c4-4f6d-b4ac-1500230d0af5" />
  </a>
</p>

```
DNS:     Client → WireGuard → dnsmasq → API → WebSocket → Dashboard
Policy:  Dashboard → API → RDS → wg-agent → dns-sync → dnsmasq reload
Enroll:  NetGardeClient → POST /v1/enroll → wg-agent → WireGuard config
```

Full documentation: [NetGarde/docs](https://github.com/NetGarde/NetGarde/tree/develop/docs)

---

## Tech stack

React · TypeScript · FastAPI · PostgreSQL · Redis · WireGuard · dnsmasq · AWS (EC2, RDS, S3, CloudFront)
