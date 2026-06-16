<h1 align="center">Hi, I'm Alan Fong 👋</h1>
<p align="center"><b>DevOps &amp; Automation Engineer</b> · Johor Bahru, Malaysia</p>
<p align="center">I build and run the systems that keep a business operating — integrating AI into workflows so people have more time to focus on high-quality work.</p>

<p align="center">
  🌐 <a href="https://alanfong93.github.io">Portfolio site</a> ·
  💼 <a href="https://www.linkedin.com/in/alan-fong">LinkedIn</a>
</p>

---

## 🧰 Tech Stack

| Area | Tools |
|---|---|
| **Languages** | Python · PHP · JavaScript · PowerShell · Bash |
| **Containers & Virtualization** | Docker · Docker Compose · Windows Hyper-V · Proxmox VE |
| **Cloud** | AWS · Google Cloud Platform · Google Workspace (admin) |
| **Automation / AI** | n8n · Claude Code · LLM agents · Whisper · Telegram Bot API |
| **Networking** | OpenWRT · pfSense · multi-WAN · VPN (SoftEther, Twingate) · Cloudflare Tunnel |
| **Infra / DevOps** | Nginx · CI/CD (GitHub Actions) · Uptime Kuma |
| **Storage / NAS** | Synology DSM · SHR / RAID · automated backups |
| **Security** | YubiKey · Action1 patch management |

---

## 🚀 Featured Work

### Distributed Print-Fleet Service
A self-hosted platform that turns USB thermal printers into a managed, multi-site network resource. **Raspberry Pi edge agents** expose printers over an authenticated HTTP API with idempotent, reboot-safe job queues; a **central control plane** handles terminal enrollment, token-scoped auth, dispatch, webhook callbacks, and over-the-air fleet updates — with a web dashboard and hardened systemd deployment.
`Python` · `FastAPI` · `Distributed systems` · `Raspberry Pi` · `SQLite/Postgres` · `Docker` · `OTA`

```mermaid
flowchart LR
    subgraph Sites[Physical sites]
        PI1[Pi edge agent<br>FastAPI · queue] --> PR1[(Thermal printers)]
        PI2[Pi edge agent<br>FastAPI · queue] --> PR2[(Thermal printers)]
    end
    CENTRAL[Central control plane<br>enroll · auth · dispatch · OTA] <--> PI1
    CENTRAL <--> PI2
    DASH[Web dashboard] --> CENTRAL
    style CENTRAL fill:#cce5ff,color:#000
    style PI1 fill:#d4edda,color:#000
    style PI2 fill:#d4edda,color:#000
    style DASH fill:#fff3cd,color:#000
```

### Package Optimization Service
A **FastAPI** microservice that recommends the optimal shipping box using **3D bin-packing** (Google OR-Tools CP-SAT). Packing runs as **async background jobs** with progress polling; the solver enforces fragility, weight-stacking and rotation constraints, caches recurring scenarios, and runs in **isolated worker processes** so a native solver fault degrades a single box instead of the whole API. 200+ tests, Dockerized.

> **Origin:** rebuilt from a flawed AI-generated prototype into a production-grade service.

`Python` · `FastAPI` · `OR-Tools (CP-SAT)` · `Async jobs` · `Optimization` · `Docker`

```mermaid
flowchart LR
    REQ[POST /jobs/recommend] --> Q[Async job queue]
    POLL[Client polls status] --> Q
    Q --> SOLVE[CP-SAT solver<br>isolated worker process]
    SOLVE --> RESULT[Top-5 labelled<br>box recommendations]
    style Q fill:#cce5ff,color:#000
    style SOLVE fill:#d4edda,color:#000
    style RESULT fill:#fff3cd,color:#000
```

### Scheduled Broadcast Automation
A Python service that automates scheduled audio/radio playback — time- and season-aware playlist switching, browser orchestration with automatic recovery, and a **REST control + metrics API**. Reliability-first: **circuit breakers**, timeout management, Pydantic-validated config with hot reload, and 118+ tests.
`Python` · `REST API` · `Pydantic` · `Circuit breaker` · `Scheduling`

```mermaid
flowchart LR
    SCHED[Scheduler<br>season + daily] --> CTRL[Playback controller]
    CB[Circuit breaker + timeouts] --> CTRL
    API[REST control + metrics] --> CTRL
    CTRL --> BROW[Browser orchestration<br>auto-recovery]
    style CTRL fill:#cce5ff,color:#000
    style CB fill:#d4edda,color:#000
    style API fill:#fff3cd,color:#000
```

### AI-Powered IT Support Bot
An LLM-backed Telegram bot that automates first-line (L1) IT support end-to-end: tickets are checked against an FAQ/SOP/solutions knowledge base, the bot guides users through known fixes, and escalates only what needs a human — with common remediations (e.g. automated VM restarts) wired into the flow.

> **Impact:** handles routine L1 tickets end-to-end, freeing the IT team to focus on higher-value engineering instead of repetitive support.

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
As the first IT hire at an SME, I designed and built the entire IT function from zero — network edge, virtualization, self-hosted services, central storage, backups, and security. File storage runs on a **Synology DS920+ (SHR)**, replicated to a dedicated Synology backup target.

```mermaid
flowchart LR
    subgraph Edge[Network Edge]
        WAN[5x WAN lines] --> RTR[OpenWRT Router<br>multi-WAN failover]
    end
    subgraph Virt[Virtualization]
        PVE[Windows Hyper-V] --> DOCK[Docker host]
    end
    subgraph Svc[Self-Hosted Services]
        DOCK --> RP[Nginx]
        DOCK --> N8N[n8n]
        DOCK --> MON[Uptime Kuma]
    end
    subgraph Store[Storage]
        NAS[Synology DS920+<br>SHR] --> BAK[DS120<br>backup target]
    end
    RTR --> PVE
    PVE --> NAS
    style PVE fill:#cce5ff,color:#000
    style DOCK fill:#cce5ff,color:#000
    style N8N fill:#d4edda,color:#000
    style NAS fill:#d4edda,color:#000
    style BAK fill:#fff3cd,color:#000
```

---

## 🤖 AI Projects

### JoJo — Personal AI Assistant
An agentic assistant built on **Claude Code**, reachable over Telegram. It manages calendar, email, notes and files, runs automations through n8n, drives a browser for research, and keeps **persistent cross-session memory** via custom MCP (Model Context Protocol) servers.

```mermaid
flowchart LR
    TG[Telegram] <--> AGENT[Claude Code agent]
    AGENT --> MCP[MCP tools<br>memory / browser / search]
    AGENT --> N8N[n8n workflows]
    N8N --> SVC[Calendar / Email<br>Drive / News]
    AGENT --> MEM[(Persistent memory)]
    style AGENT fill:#cce5ff,color:#000
    style MEM fill:#d4edda,color:#000
    style N8N fill:#d4edda,color:#000
```

### Hermes — Self-Hosted Speech-to-Text
A containerized **Whisper** (faster-whisper) transcription service running fully local with zero per-call API cost — powering voice-message transcription inside automation pipelines.
`Whisper` · `Docker` · `Python`

---

## 🏢 Enterprise Systems — Current Role
*Built for an SME; kept high-level to respect confidentiality.*

- **HR & attendance** — in-house card-tap system replacing an off-the-shelf biometric solution
- **IT ticketing & asset/stock management** — internal tools for requests and hardware tracking
- **Order automation** — automated sales/delivery order generation, removing manual data entry
- **Warehouse management** — multi-courier dispatch, consignment notes and stock tracking (maintained & extended)
- **Order follow-up & automated reporting** — internal follow-up system plus scheduled reports delivered hands-free
- **Team development** — mentored a colleague with little programming background to design and ship an OCR-driven automation end-to-end, turning a non-developer into the project's primary author

---

## 🛠 Selected Open-Source Projects

| Project | What it is | Stack |
|---|---|---|
| **KupuPost** | Notification delivery system — multi-recipient messaging, testable design | Python |
| **telegrambots** | Reusable Telegram bot framework — Dockerized, documented API | Python · Docker |
| **database-sensei** | Multi-driver database tool (SQLAlchemy 2.0+) with a full-stack UI | Python |
| **WindowsOptimizationsScript** | Windows debloat/optimization — registry & VM tuning | PowerShell |
| **screenRuler** | On-screen measurement utility, cross-implemented in two languages | Python · C# |

---

## 💼 Experience

- **IT Manager** — Modern Zone Marketing Sdn Bhd · *Jun 2020 – Present* — first IT hire; built and lead the entire IT function (infrastructure, networking, support, small engineering team); drove automation, self-hosting and AI tooling; mentored team members, including growing a non-developer into a shipping contributor.
- **Chief / Senior Technician** — Meadow Computer & System Sdn Bhd · *2013 – 2020* — managed up to four technicians, ran after-sales services, automated manual workflows, maintained an in-house service/warranty system.
- **Software Engineer Intern** — GNey Software · *2018*

## 🎓 Education & Certifications

- **Bachelor's Degree, Information Technology (Software Engineering)** — Southern University College · *2014–2018*
- **Google IT Support Professional Certificate** — *2024*

---

## 🧭 How I Work
- **Conventional Commits** + **branch-based PRs** with CI-based automated code review
- **Docs-first** — architecture/flow docs and Mermaid diagrams in each repo
- **Automation-first** — if a task is repetitive, it gets a pipeline

<p align="center"><i>Most implementation code lives in private repos — this profile highlights architecture, decisions, and outcomes.</i></p>
