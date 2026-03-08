<div align="center">

# 🛡️ Open Source SIEM implementation 

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![Vue.js](https://img.shields.io/badge/Vue.js-4FC08D?style=for-the-badge&logo=vue.js&logoColor=white)](https://vuejs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://typescriptlang.org)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)
[![OpenSearch](https://img.shields.io/badge/OpenSearch-005EB8?style=for-the-badge&logo=opensearch&logoColor=white)](https://opensearch.org)
[![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://mysql.com)
[![License](https://img.shields.io/badge/License-AGPL--3.0-red?style=for-the-badge)](LICENSE)

> 🔐 A **full-stack, open-source Security Operations Platform** — featuring centralized log management, real-time threat detection, AI-powered incident response, vulnerability scanning, and an end-to-end SOC dashboard. Built with FastAPI, Vue.js, Docker, and integrated with Wazuh, OpenSearch, Graylog, and Grafana.

**[🌐 Live Docs](https://docs.socfortress.co) · [📹 Video Demo](https://github.com/VINAYBOYAT11/CoPilot)**

</div>

---

## 📋 Table of Contents

- [About](#-about)
- [Key Features](#-key-features)
- [Architecture](#-architecture)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Configuration](#-configuration)
- [Services Overview](#-services-overview)
- [API Overview](#-api-overview)
- [Screenshots](#-screenshots)
- [Author](#-author)

---

## 🔍 About

**CoPilot** is a production-ready, open-source **Security Operations Center (SOC) platform** I built to solve the problem of fragmented security tooling. Security teams typically juggle 5–10 disconnected tools — CoPilot brings them all together into one unified platform.

**The problem I solved:**
- 🔴 Security teams use disconnected tools with no unified view
- 🔴 Alert fatigue from too many unrelated notifications
- 🔴 Manual, slow incident response workflows
- 🔴 No AI-assisted threat hunting

**What CoPilot provides:**
- ✅ Unified SOC dashboard with real-time telemetry
- ✅ Automated threat detection & response
- ✅ AI-powered incident analysis (GPT-4)
- ✅ Multi-customer / multi-tenant support
- ✅ One-click stack provisioning

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🖥️ **SOC Dashboard** | Real-time security event dashboard built with Vue.js |
| 🤖 **AI-Powered Analysis** | GPT-4 powered MCP module for intelligent threat analysis |
| 🚨 **Incident Management** | End-to-end incident lifecycle — create, triage, resolve |
| 🔍 **Threat Intelligence** | Integrated threat intel feeds for IOC enrichment |
| 🛡️ **Active Response** | Automated response actions triggered by alerts |
| 🔌 **Connectors** | Plug-and-play integrations with Wazuh, Graylog, DFIR-IRIS |
| 🌐 **Network Connectors** | Network scan & monitoring via Nuclei vulnerability scanner |
| 📦 **Stack Provisioning** | One-click deployment of security stacks for customers |
| 👥 **Multi-Tenant** | Customer management with isolated environments |
| 📊 **Grafana Integration** | Pre-built dashboards for log & alert visualization |
| 📧 **SMTP Alerting** | Configurable email notifications for critical alerts |
| 🗓️ **Scheduled Jobs** | Automated security checks via built-in schedulers |
| 🗃️ **MinIO Storage** | S3-compatible object storage for artifacts & reports |
| 🔐 **Auth & RBAC** | JWT-based authentication with role-based access control |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                         COPILOT PLATFORM                            │
│                                                                     │
│  ┌─────────────────┐         ┌───────────────────────────────────┐  │
│  │   Vue.js/TS     │ ──────▶ │         FastAPI Backend           │  │
│  │   Frontend      │ ◀────── │                                   │  │
│  │  (Nginx TLS)    │  REST   │  ┌────────┐  ┌────────────────┐  │  │
│  └─────────────────┘         │  │  Auth  │  │   Connectors   │  │  │
│                              │  └────────┘  └────────────────┘  │  │
│  ┌─────────────────┐         │  ┌─────────┐  ┌──────────────┐  │  │
│  │  Customer       │ ──────▶ │  │Incidents│  │ Threat Intel │  │  │
│  │  Portal         │         │  └─────────┘  └──────────────┘  │  │
│  └─────────────────┘         │  ┌──────────┐ ┌──────────────┐  │  │
│                              │  │  Agents  │ │   Schedulers │  │  │
│                              │  └──────────┘ └──────────────┘  │  │
│                              └───────────────────────────────────┘  │
│                                         │                           │
│          ┌──────────────────────────────┼──────────────────────┐   │
│          ▼                        ▼     ▼             ▼         │   │
│   ┌─────────────┐   ┌──────────────┐  ┌──────┐  ┌─────────┐   │   │
│   │   MySQL 8   │   │   MinIO      │  │ MCP  │  │ Nuclei  │   │   │
│   │  (Database) │   │  (Storage)   │  │ (AI) │  │(Scanner)│   │   │
│   └─────────────┘   └──────────────┘  └──────┘  └─────────┘   │   │
│                                         │                       │   │
│          ┌──────────────────────────────┘                       │   │
│          ▼                                                       │   │
│   ┌──────────────────────────────────────────────────────────┐  │   │
│   │                    INTEGRATIONS                          │  │   │
│   │  Wazuh │ OpenSearch │ Graylog │ Grafana │ DFIR-IRIS │ IG │  │   │
│   │  Velociraptor │ VirusTotal │ MISP │ Shuffle │ TheHive   │  │   │
│   └──────────────────────────────────────────────────────────┘  │   │
└────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

### Backend
| Technology | Purpose |
|-----------|---------|
| **Python 3.11+** | Core language |
| **FastAPI** | REST API framework |
| **SQLAlchemy + Alembic** | ORM & database migrations |
| **MySQL 8** | Primary database |
| **MinIO** | S3-compatible object storage |
| **APScheduler** | Scheduled security tasks |

### Frontend
| Technology | Purpose |
|-----------|---------|
| **Vue.js 3** | UI framework |
| **TypeScript** | Type-safe development |
| **Tailwind CSS** | Utility-first styling |
| **Vite** | Frontend build tool |
| **Nginx** | Production web server |

### Infrastructure
| Technology | Purpose |
|-----------|---------|
| **Docker + Compose** | Container orchestration |
| **OpenSearch** | Log indexing & search |
| **Wazuh** | Endpoint security & SIEM |
| **Graylog** | Log aggregation |
| **Grafana** | Dashboards & visualizations |
| **Nuclei** | Vulnerability scanning |
| **GPT-4 / OpenAI** | AI-powered analysis (MCP module) |

---

## 📁 Project Structure

```
CoPilot/
│
├── 📁 backend/
│   ├── 📁 app/
│   │   ├── 📁 auth/               # JWT authentication & RBAC
│   │   ├── 📁 agents/             # Security agent management
│   │   ├── 📁 incidents/          # Incident lifecycle management
│   │   ├── 📁 connectors/         # Tool integrations (Wazuh, Graylog)
│   │   ├── 📁 threat_intel/       # IOC enrichment & threat feeds
│   │   ├── 📁 active_response/    # Automated response actions
│   │   ├── 📁 schedulers/         # Automated security jobs
│   │   ├── 📁 network_connectors/ # Network scan integrations
│   │   ├── 📁 stack_provisioning/ # One-click stack deployment
│   │   ├── 📁 customers/          # Multi-tenant customer mgmt
│   │   ├── 📁 customer_provisioning/ # Customer onboarding
│   │   ├── 📁 smtp/               # Email alerting
│   │   ├── 📁 data_store/         # MinIO object storage
│   │   ├── 📁 healthchecks/       # Service health monitoring
│   │   ├── 📁 integrations/       # Third-party integrations
│   │   ├── 📁 middleware/         # Request/auth middleware
│   │   └── 📄 utils.py            # Shared utilities
│   ├── 📄 copilot.py              # Application entry point
│   ├── 📄 requirements.txt        # Python dependencies
│   └── 📄 Dockerfile
│
├── 📁 frontend/
│   ├── 📁 src/                    # Vue.js components & pages
│   ├── 📄 vite.config.ts          # Build configuration
│   ├── 📄 tailwind.config.js      # Design system
│   └── 📄 Dockerfile
│
├── 📄 docker-compose.yml          # Full stack orchestration
├── 📄 build-dockers.sh            # Build script
├── 📄 .env.example                # Environment template
└── 📄 README.md
```

---

## 🚀 Getting Started

### Prerequisites

```bash
# System Requirements
OS:   Debian 11/12, Ubuntu 20.04+ or any Linux distro
RAM:  8GB minimum (16GB recommended)
Disk: 50GB+

# Software
docker --version      # 24.x+
docker compose version # v2.x+
```

### Quick Start

```bash
# 1. Clone the repository
git clone https://github.com/VINAYBOYAT11/CoPilot.git
cd CoPilot

# 2. Configure environment
cp .env.example .env
nano .env   # Edit with your credentials

# 3. Build images
bash build-dockers.sh

# 4. Start all services
docker compose up -d

# 5. Check everything is running
docker compose ps
```

---

## ⚙️ Configuration

Edit `.env` before starting:

```env
# Database
MYSQL_ROOT_PASSWORD=your_secure_password
MYSQL_USER=copilot
MYSQL_PASSWORD=your_db_password

# Storage (MinIO)
MINIO_ROOT_USER=copilotadmin
MINIO_ROOT_PASSWORD=your_minio_password

# AI Module
OPENAI_API_KEY=sk-your-openai-key
OPENAI_MODEL=gpt-4o

# Wazuh Integration
WAZUH_MANAGER_URL=https://your-wazuh-server:55000
WAZUH_MANAGER_USERNAME=wazuh-admin
WAZUH_MANAGER_PASSWORD=your_wazuh_password

# OpenSearch Integration
OPENSEARCH_URL=https://your-opensearch:9200
OPENSEARCH_USERNAME=admin
OPENSEARCH_PASSWORD=your_opensearch_password

# Server
SERVER_HOST=your-domain.com
```

---

## 🔌 Services Overview

| Service | Port | Purpose |
|---------|------|---------|
| **CoPilot Dashboard** | `:80` / `:443` | Main SOC web UI |
| **CoPilot API** | `:5000` | FastAPI backend (REST + docs) |
| **MySQL** | `:3306` | Primary database |
| **MinIO** | `:9000` | Object storage |
| **MCP (AI)** | `:9900` | GPT-4 powered analysis |
| **Nuclei** | internal | Vulnerability scanning |

Access the API docs at: `http://localhost:5000/docs`

---

## 📡 API Overview

The FastAPI backend exposes a full REST API:

```
/api/v1/auth/          → Login, token refresh
/api/v1/agents/        → Agent management & health
/api/v1/incidents/     → Create, list, update incidents
/api/v1/connectors/    → Manage tool connectors
/api/v1/threat-intel/  → IOC lookups & enrichment
/api/v1/customers/     → Multi-tenant customer mgmt
/api/v1/schedulers/    → View & control scheduled jobs
/api/v1/healthchecks/  → System health status
```

Full interactive docs: `http://localhost:5000/docs` (Swagger UI)

---

## 👨‍💻 Author

**Vinay Boyat**

*B.Tech — Computer & Communication Engineering | Minor in Cybersecurity*
*Manipal University Jaipur | 2021–2025*

[![GitHub](https://img.shields.io/badge/GitHub-VINAYBOYAT11-181717?style=for-the-badge&logo=github)](https://github.com/VINAYBOYAT11)
[![Portfolio](https://img.shields.io/badge/Portfolio-Live-00C7B7?style=for-the-badge&logo=vercel)](https://portfolio-pink-beta-1y6l6m0ylt.vercel.app)
[![Email](https://img.shields.io/badge/Email-vinayboyat102@gmail.com-EA4335?style=for-the-badge&logo=gmail)](mailto:vinayboyat102@gmail.com)

---

<div align="center">

> 🛡️ *"Security is a process, not a product — so I built a platform, not just a script."*

⭐ **If CoPilot helped you, give it a star!** ⭐

*Built with ❤️ and Python by Vinay Boyat*

</div>
