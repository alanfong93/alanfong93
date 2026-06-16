<h1 align="center">Hi, I'm Alan Fong 👋</h1>
<p align="center"><b>DevOps &amp; Automation Engineer</b> · Johor Bahru, Malaysia</p>
<p align="center">I build and run the systems that keep a business operating — then automate the parts that shouldn't need a human.</p>

<p align="center">
  🌐 <a href="https://alanfong93.github.io">Portfolio site</a> ·
  💼 <a href="https://www.linkedin.com/in/alan-fong">LinkedIn</a>
</p>

---

## 🧰 Tech Stack

| Area | Tools |
|---|---|
| **Languages** | Python · PHP · JavaScript · PowerShell · Bash |
| **Containers & Virtualization** | Docker · Docker Compose · Proxmox VE |
| **Cloud** | AWS · Google Cloud Platform · Google Workspace (admin) |
| **Automation / AI** | n8n · LLM agent tooling · Telegram Bot API |
| **Networking** | OpenWRT · pfSense · multi-WAN · VPN (SoftEther, Twingate) |
| **Infra / DevOps** | Traefik · Ansible · CI/CD (GitHub Actions) · Uptime Kuma |
| **Security** | YubiKey · Action1 patch management |

---

## 🚀 Featured Work

### AI-Powered IT Support Bot
An LLM-backed Telegram bot that automates first-line (L1) IT support end-to-end: users submit tickets in chat, the bot checks them against an FAQ/SOP/solutions knowledge base, guides users through known fixes, and escalates only what truly needs a human — with common remediations (e.g. automated VM restarts) wired straight into the flow.

> **Impact:** effectively replaced the L1 support tier — a departing L1 role did not need to be backfilled.

```mermaid
flowchart TD
    A[User submits ticket<br>via Telegram] --> B{AI checks FAQ /<br>SOP / solutions DB}
    B -->|Match found| C[Bot guides user<br>through the fix]
    C --> D{Resolved?}
    D -->|Yes| E[Auto-close ticket]
    D -->|No| F[Escalate to<br>human engineer]
    B -->|No match| F
    F --> G[Automated remediation<br>e.g. VM restart]
    style A fill:#cce5ff,color:#000
    style E fill:#d4edda,color:#000
    style F fill:#fff3cd,color:#000
    style G fill:#cce5ff,color:#000
```

### Self-Hosted IT Infrastructure (built from scratch)
As the first IT hire at an SME, I designed and built the entire IT function from zero — network edge, virtualization, self-hosted services, backups, and security — and run it hands-on as it scales.

```mermaid
flowchart LR
    subgraph Edge[Network Edge]
        WAN[5x WAN lines] --> RTR[OpenWRT Router<br>multi-WAN failover]
        RTR --> AP[Managed APs<br>+ controller]
    end
    subgraph Virt[Virtualization]
        PVE[Proxmox VE] --> VDI[Virtual desktops]
        PVE --> DOCK[Docker host]
    end
    subgraph Svc[Self-Hosted Services]
        DOCK --> RP[Traefik<br>reverse proxy]
        DOCK --> N8N[n8n automation]
        DOCK --> MON[Uptime Kuma]
    end
    RTR --> PVE
    style PVE fill:#cce5ff,color:#000
    style DOCK fill:#cce5ff,color:#000
    style N8N fill:#d4edda,color:#000
    style RP fill:#cce5ff,color:#000
```

### n8n Automation Platform
A self-hosted **n8n** platform that turns repetitive operational work into reliable, observable pipelines — from business workflows (automated order creation, a tap-card HR/attendance system) to a personal AI-assistant suite wired to local and cloud LLMs.

---

## 🛠 Selected Projects

| Project | What it is | Stack |
|---|---|---|
| **KupuPost** | Notification delivery system, multi-recipient messaging, testable design | Python |
| **telegrambots** | Reusable Telegram bot framework — Dockerized, documented API | Python · Docker |
| **database-sensei** | Multi-driver database tool (SQLAlchemy 2.0+) with a full-stack UI | Python |
| **WindowsOptimizationsScript** | Windows debloat/optimization — registry & VM tuning | PowerShell |
| **screenRuler** | On-screen measurement utility, cross-implemented in two languages | Python · C# |

---

## 🧭 How I Work

- **Conventional Commits** and **branch-based PRs** with **CI-based automated code review**
- **Docs-first** — architecture/flow docs and Mermaid diagrams in each repo
- **Automation-first** — if a task is repetitive, it gets a pipeline

<p align="center"><i>Most implementation code lives in private repos — this profile highlights architecture, decisions, and outcomes.</i></p>
