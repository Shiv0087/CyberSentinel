<div align="center">

<img src="https://img.shields.io/badge/Status-In%20Development-yellow?style=for-the-badge" />
<img src="https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python" />
<img src="https://img.shields.io/badge/FastAPI-Backend-009688?style=for-the-badge&logo=fastapi" />
<img src="https://img.shields.io/badge/React-Frontend-61DAFB?style=for-the-badge&logo=react" />
<img src="https://img.shields.io/badge/LLM-Powered-blueviolet?style=for-the-badge&logo=openai" />

# 🛡️ CyberSentinel

### *LLM-Powered Attack Correlation & Explainability Framework for Intrusion Detection Systems*

> Transforming thousands of isolated IDS alerts into clear, actionable attack narratives using AI.

**Final Year Project · B.Tech / B.E. in Computer Science / Cybersecurity**

---

</div>

## 📌 Table of Contents

- [Overview](#-overview)
- [Problem Statement](#-problem-statement)
- [Research Gaps](#-research-gaps-addressed)
- [System Architecture](#-system-architecture)
- [Core Modules](#-core-modules)
- [Tech Stack](#-tech-stack)
- [Getting Started](#-getting-started)
- [Project Structure](#-project-structure)
- [Dataset](#-dataset)
- [Expected Outcomes](#-expected-outcomes)
- [Future Scope](#-future-scope)
- [License](#-license)

---

## 🔍 Overview

**CyberSentinel** is an intelligent security analytics framework built on top of existing Intrusion Detection Systems (IDS) like **Snort**, **Suricata**, and **Cowrie**. It addresses a critical limitation in modern SOC environments: IDS tools can *detect* threats, but they rarely *explain* them.

CyberSentinel acts as a post-detection intelligence layer that:

- **Correlates** isolated alerts into multi-stage attack campaigns
- **Reconstructs** complete attack chains (Reconnaissance → Exploitation → Persistence)
- **Explains** detections in plain English using Large Language Models (LLMs)
- **Prioritizes** incidents by risk score and attack context
- **Visualizes** attack timelines on an interactive analyst dashboard

---

## 🚨 Problem Statement

Modern IDS platforms generate **thousands of alerts daily**. These alerts are presented as isolated, context-free events — making it extremely difficult for security analysts to:

| Challenge | Impact |
|---|---|
| No attack context | Analysts can't see the full picture of an attack campaign |
| No explainability | ML-based IDS decisions feel like a "black box" |
| Alert overload | Critical threats get buried under false positives |
| Slow investigation | Manual correlation wastes hours per incident |

The result? **Alert fatigue**, missed threats, and longer mean time to respond (MTTR).

---

## 🧩 Research Gaps Addressed

CyberSentinel simultaneously tackles three significant gaps in existing IDS research:

```
Gap 1: Multi-Stage Attack Correlation
        Most IDS tools generate isolated alerts with no ability to reconstruct
        attack chains across Reconnaissance → Exploitation → Persistence stages.

Gap 2: Explainability (XAI for IDS)
        ML-based IDS models achieve high accuracy but provide no human-readable
        reasoning, creating a black-box problem for analysts.

Gap 3: Alert Fatigue Reduction
        Security teams are overwhelmed by alert volumes with no intelligent
        prioritization mechanism to surface the most critical events.
```

---

## 🏗️ System Architecture

```
  Attack Traffic
       │
       ▼
┌─────────────────────────────────────┐
│   IDS / Honeypot Layer              │
│   Snort  │  Suricata  │  Cowrie     │
└─────────────────┬───────────────────┘
                  │  Raw Alerts (JSON/EVE logs)
                  ▼
┌─────────────────────────────────────┐
│   Alert Collection Module           │
│   Parses, normalizes & stores alerts│
└─────────────────┬───────────────────┘
                  │
                  ▼
┌─────────────────────────────────────┐
│   Correlation Engine                │
│   Groups alerts by: Source IP,      │
│   Destination IP, Timestamp,        │
│   Attack Pattern, Event Sequence    │
└─────────────────┬───────────────────┘
                  │
                  ▼
┌─────────────────────────────────────┐
│   Attack Chain Reconstruction       │
│   Builds multi-stage attack         │
│   timelines from correlated groups  │
└─────────────────┬───────────────────┘
                  │
                  ▼
┌─────────────────────────────────────┐
│   LLM Explainability Engine  🤖     │
│   Generates human-readable          │
│   attack narratives & impact summary│
└─────────────────┬───────────────────┘
                  │
                  ▼
┌─────────────────────────────────────┐
│   Alert Prioritization Module       │
│   Risk scoring based on severity    │
│   & contextual attack stage         │
└─────────────────┬───────────────────┘
                  │
                  ▼
┌─────────────────────────────────────┐
│   CyberSentinel Dashboard  📊       │
│   Attack timelines · Chain graphs   │
│   AI explanations · Priority queue  │
└─────────────────────────────────────┘
```

---

## 🧠 Core Modules

### 1. Alert Collection Module
Ingests and normalizes alert logs from IDS tools (EVE JSON from Suricata, unified2 from Snort, Cowrie SSH logs). Stores structured alerts in a relational database.

### 2. Correlation Engine
Groups related alerts using:
- Source/Destination IP matching
- Temporal proximity (sliding time window)
- Attack pattern clustering
- Event sequence analysis

### 3. Attack Chain Reconstruction
Maps correlated alert clusters to multi-stage attack timelines following the kill chain model:
`Reconnaissance → Scanning → Exploitation → Payload Delivery → Persistence`

### 4. LLM Explainability Engine
Sends structured attack chain data to an LLM with a custom security analyst prompt to generate:
- Plain-English explanation of why each alert fired
- Attack progression narrative
- Estimated security impact

### 5. Alert Prioritization Module
Computes a risk score per incident using:
- CVSS-style severity weights
- Attack stage (early-stage = lower priority; persistence = critical)
- Number of correlated events

### 6. Dashboard (React.js)
Analyst-facing interface featuring:
- Real-time alert feed
- Attack chain graph visualization (D3.js)
- AI-generated incident summaries
- Priority-sorted alert queue
- Timeline explorer

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **IDS / Data Sources** | Suricata, Snort, Cowrie Honeypot |
| **Backend** | Python 3.10+, FastAPI |
| **Database** | PostgreSQL / SQLite |
| **AI / LLM** | OpenAI API (`gpt-4o`) or local LLM (Ollama + LLaMA 3) |
| **Frontend** | React.js, Chart.js, D3.js |
| **Dataset** | CICIDS2017 / NSL-KDD / UNSW-NB15 |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- Node.js 18+
- PostgreSQL (or SQLite for development)
- Suricata or Snort installed (for live testing)
- OpenAI API key **or** Ollama running locally

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/cybersentinel.git
cd cybersentinel

# 2. Set up the Python backend
cd backend
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

# 3. Configure environment variables
cp .env.example .env
# Edit .env with your DB credentials and LLM API key

# 4. Initialize the database
python manage.py migrate

# 5. Start the backend server
uvicorn main:app --reload --port 8000

# 6. Set up the React frontend (new terminal)
cd ../frontend
npm install
npm start
```

The dashboard will be available at `http://localhost:3000`

---

## 📁 Project Structure

```
cybersentinel/
├── backend/
│   ├── main.py                  # FastAPI entrypoint
│   ├── modules/
│   │   ├── collector.py         # Alert collection & parsing
│   │   ├── correlator.py        # Correlation engine
│   │   ├── chain_builder.py     # Attack chain reconstruction
│   │   ├── llm_engine.py        # LLM explainability module
│   │   └── prioritizer.py       # Risk scoring
│   ├── models/                  # Database models
│   ├── api/                     # REST API routes
│   └── requirements.txt
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Dashboard.jsx
│   │   │   ├── AlertFeed.jsx
│   │   │   ├── AttackChain.jsx  # D3.js chain visualization
│   │   │   └── IncidentDetail.jsx
│   │   └── App.jsx
│   └── package.json
│
├── datasets/                    # Sample IDS alert logs for testing
├── docs/                        # Architecture diagrams & reports
├── tests/
└── README.md
```

---

## 📊 Dataset

For development and evaluation, this project uses:

| Dataset | Description |
|---|---|
| **CICIDS2017** | Canadian Institute for Cybersecurity — labeled network traffic with multiple attack types |
| **NSL-KDD** | Improved version of KDD Cup 1999 — widely used IDS benchmark |
| **UNSW-NB15** | Modern dataset with 9 attack categories |

Alternatively, live alerts can be collected by running Suricata or Cowrie against controlled attack simulations using **Metasploit** or **Kali Linux**.

---

## ✅ Expected Outcomes

- [ ] Multi-stage attack chains reconstructed from raw IDS alerts
- [ ] Human-readable AI-generated explanations for security events
- [ ] Risk-scored and prioritized alert queue for analysts
- [ ] Interactive attack timeline and chain visualization dashboard
- [ ] Measurable reduction in mean time to investigate (MTTI)

---

## 🔭 Future Scope

- **MITRE ATT&CK Mapping** — tag each attack stage to the ATT&CK framework
- **Threat Intelligence Integration** — enrich IPs/domains with VirusTotal, AbuseIPDB
- **Adaptive Learning** — refine correlation rules from analyst feedback
- **Multi-Source Log Correlation** — ingest SIEM, firewall, and endpoint logs
- **Real-Time Enterprise Deployment** — Kafka-based streaming pipeline

---

---

## 📄 License

This project is developed for academic purposes as part of a Final Year Project.
© 2026

---

<div align="center">

*Built with 🔐 to make the internet a little safer.*

</div>
