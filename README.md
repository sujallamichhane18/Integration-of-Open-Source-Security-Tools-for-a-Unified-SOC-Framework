<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f2027,50:203a43,100:2c5364&height=220&section=header&text=Unified%20SOC%20Framework&fontSize=48&fontColor=ffffff&fontAlignY=38&desc=Open-Source%20Security%20Operations%20Center%20%7C%20Final%20Year%20Major%20Project&descAlignY=58&descSize=16" width="100%"/>

<br/>

[![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-0078D4?style=for-the-badge&logo=windows&logoColor=white)](https://wazuh.com)
[![pfSense](https://img.shields.io/badge/Firewall-pfSense-212121?style=for-the-badge&logo=pfsense&logoColor=white)](https://pfsense.org)
[![Suricata](https://img.shields.io/badge/IDS%2FIPS-Suricata-EF6C00?style=for-the-badge&logoColor=white)](https://suricata.io)
[![Shuffle](https://img.shields.io/badge/SOAR-Shuffle-7C3AED?style=for-the-badge&logoColor=white)](https://shuffler.io)
[![TheHive](https://img.shields.io/badge/IR-TheHive-F59E0B?style=for-the-badge&logoColor=black)](https://thehive-project.org)
[![MISP](https://img.shields.io/badge/TI-MISP-DC2626?style=for-the-badge&logoColor=white)](https://www.misp-project.org)
[![License](https://img.shields.io/badge/License-MIT-22C55E?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Defended-brightgreen?style=for-the-badge)]()

<br/>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=18&pause=1000&color=00D9FF&center=true&vCenter=true&width=650&lines=Real-time+Threat+Detection+%26+Correlation;Automated+Incident+Response+via+Shuffle+SOAR;Threat+Intelligence+Enrichment+with+MISP+%26+VirusTotal;End-to-End+Open-Source+Security+Operations" alt="Typing SVG" />

<br/><br/>

> 🎓 **Final Year Major Project — Bachelor of Computer Application (BCA)**
> Defended and submitted in partial fulfillment of the degree requirements.

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Architecture](#-architecture)
- [Technology Stack](#-technology-stack)
- [Core Components](#-core-components)
- [Data Flow](#-data-flow)
- [SOAR Automation with Shuffle](#-soar-automation-with-shuffle)
- [Automated Response Logic](#-automated-response-logic)
- [Setup & Deployment](#-setup--deployment)
- [Screenshots](#-screenshots)
- [Use Cases](#-use-cases)
- [Project Team](#-project-team)
- [Disclaimer](#-disclaimer)

---

## 🔍 Overview

This project implements a **fully integrated, open-source Security Operations Center (SOC)** capable of:

- 🔎 **Monitoring** network traffic and endpoint activity in real time
- 🧩 **Correlating** security events across multiple log sources via Wazuh SIEM
- 🌐 **Enriching** alerts with external threat intelligence (VirusTotal, MISP, AbuseIPDB, AlienVault OTX)
- ⚡ **Automating** incident response workflows using **Shuffle SOAR**
- 🚨 **Notifying** analysts via Discord webhooks for high-severity incidents
- 🛡️ **Blocking** malicious IPs at the firewall level — all without manual intervention

The framework is fully modular and cost-free to deploy, making it ideal for **academic labs**, **blue team training environments**, **SOC analyst onboarding**, and **small-to-medium enterprise security operations**.

---

## 🏗️ Architecture

<div align="center">
<img src="majorprojectdiagram.drawio.png" alt="SOC Architecture Diagram" width="92%"/>

*Figure: High-level architecture of the Unified SOC Framework*
</div>

---

## 💻 Technology Stack

<div align="center">

| Layer | Tool | Version | Purpose |
|:---:|:---|:---:|:---|
| 🔥 **Firewall / Gateway** | pfSense | 2.7.x | Network perimeter control, automated IP blocking via API |
| 🕵️ **IDS / IPS** | Suricata | 7.x | Signature-based deep packet inspection and traffic analysis |
| 📊 **SIEM** | Wazuh | 4.x | Log aggregation, correlation rules, threat detection engine |
| 🤖 **SOAR** | Shuffle | Latest | Workflow orchestration, automated playbook execution |
| 🗂️ **Incident Response** | TheHive + Cortex | 5.x | Case management, automated alert analyzers |
| 🌐 **Threat Intelligence** | MISP | 2.4.x | Structured threat sharing and indicator management |
| 🔍 **TI Enrichment** | VirusTotal · AbuseIPDB · OTX | API | Real-time IOC enrichment and scoring |
| 💻 **Endpoint Detection** | OpenEDR + Wazuh Agent | Latest | Endpoint telemetry, file integrity monitoring (FIM) |
| 🔔 **Notifications** | Discord Webhook | — | Real-time analyst alerting |

</div>

---

## 🧱 Core Components

### 1. pfSense — Perimeter Firewall
pfSense serves as the network gateway, providing stateful packet filtering, VLANs, and NAT. It exposes a REST API that allows the SOAR engine to programmatically insert block rules when a malicious source IP is confirmed.

### 2. Suricata — IDS/IPS
Deployed inline behind pfSense, Suricata performs deep packet inspection against the Emerging Threats ruleset. It generates EVE JSON logs forwarded to Wazuh for correlation. In IPS mode, it can drop packets matching high-confidence signatures immediately.

### 3. Wazuh — SIEM & XDR
The central nervous system of the SOC. Wazuh aggregates logs from all sources (pfSense, Suricata, endpoints), applies detection rules, and generates alerts with severity scores (0–15). Custom decoders and rules were developed specifically for this project.

### 4. Shuffle — SOAR Platform
Shuffle orchestrates all automated response workflows. When Wazuh fires a critical alert, a webhook triggers a Shuffle workflow that:
1. Parses the alert JSON
2. Queries VirusTotal and AbuseIPDB for enrichment
3. Evaluates confidence and severity thresholds
4. Triggers the firewall block via pfSense API
5. Creates a case in TheHive
6. Sends a formatted Discord notification

### 5. TheHive + Cortex — Case Management
TheHive receives escalated cases from Shuffle. Cortex analyzers automatically run on observable data (IPs, hashes, domains) using VirusTotal, MISP, and other responders to provide forensic context.

### 6. MISP — Threat Intelligence Platform
MISP acts as the local threat intelligence database. Indicators of compromise (IOCs) — IPs, domains, file hashes — are stored, tagged, and queried during alert enrichment. MISP is also configured to sync with community feeds.

### 7. OpenEDR + Wazuh Agent — Endpoint Layer
Wazuh agents installed on monitored endpoints ship system logs, audit events, and File Integrity Monitoring (FIM) changes. OpenEDR provides additional process-level telemetry for detecting malware behavior.

---

## 🔄 Data Flow

```
╔═══════════════════════════════════════════════════════════════════════╗
║                         NETWORK PERIMETER                             ║
║     [ pfSense Firewall ]  ──►  [ Suricata IDS/IPS ]                   ║
║       ↑ Block Rule API               │ EVE JSON Logs                  ║
╚═══════════════════════╤═════════════╪═══════════════════════════════╤═╝
                        │             │                               │
                        │             ▼                               │
╔═══════════════════════╪═════════════════════════════════════════════╪═╗
║                       │        SIEM (Wazuh)                         │ ║
║             Endpoint Logs ──► Log Aggregation                       │ ║
║             [ Wazuh Agents + OpenEDR ]                              │ ║
║                              Correlation & Detection                │ ║
║                              Alert Generated (Severity > 7)         │ ║
╚══════════════════════════════════════╤══════════════════════════════╪═╝
                                       │ Webhook Trigger               │
                                       ▼                               │
╔══════════════════════════════════════════════════════════════════════╗
║                      SOAR — Shuffle Workflow                         ║
║                                                                      ║
║   [1] Parse Wazuh Alert  ──►  [2] Enrich IOC                        ║
║        (JSON payload)          VirusTotal · AbuseIPDB · OTX          ║
║                                       │                              ║
║                        [3] Evaluate Confidence + Severity            ║
║                                       │                              ║
║              ┌─── severity > 7 ───────┤─── low confidence ──┐       ║
║              │    + high confidence   │                      │       ║
║              ▼                        │                      ▼       ║
║   [4] Block IP via pfSense API        │              Log & Monitor   ║
║   [5] Create Case in TheHive          │                              ║
║   [6] Discord Notification            │                              ║
╚══════════════════════════════════════╧══════════════════════════════╝
              │
              ▼
╔═════════════════════════════════════╗
║    TheHive + Cortex                 ║
║    Case Management & Analysis       ║
║    Cortex Analyzers (auto-run)      ║
╚═════════════════════════════════════╝
```

---

## ⚡ SOAR Automation with Shuffle

Shuffle is the orchestration layer that ties every component together. The primary workflow was built and tested within Shuffle's visual workflow editor.

### Workflow Steps

| Step | Action | Integration |
|:---:|:---|:---|
| **1** | Receive alert via Wazuh webhook | Wazuh → Shuffle |
| **2** | Extract source IP, rule ID, severity | Shuffle (JSON parser) |
| **3** | Query VirusTotal for IP reputation | VirusTotal API |
| **4** | Query AbuseIPDB for abuse confidence score | AbuseIPDB API |
| **5** | Query MISP for known IOC match | MISP API |
| **6** | Evaluate combined severity + confidence | Shuffle (condition node) |
| **7** | *(If high)* Block IP via pfSense firewall API | pfSense REST API |
| **8** | *(If high)* Create alert/case in TheHive | TheHive API |
| **9** | Send Discord notification with enriched summary | Discord Webhook |

> 📁 See the full Shuffle workflow export and screenshots in [`/docs/shuffle/`](docs/shuffle/)

---

## 🤖 Automated Response Logic

An automated firewall block is triggered when **both** conditions are met simultaneously:

- **Severity score > 7** (out of 15, as rated by Wazuh detection rules)
- **Threat intelligence confidence = HIGH** — corroborated by at least one external TI source (VirusTotal malicious score, AbuseIPDB confidence ≥ 75%, or MISP IOC match)

```python
# Simplified automated response logic (Shuffle workflow equivalent)
def process_alert(alert):
    enrichment = enrich_ioc(alert.source_ip)

    if alert.severity > 7 and enrichment.confidence == "HIGH":
        pfsense.block_ip(alert.source_ip)          # Firewall rule insertion
        thehive.create_case(alert, enrichment)      # Case management
        discord.notify(alert, enrichment)           # Analyst notification
    else:
        wazuh.log_for_monitoring(alert)             # Low-priority queue
```

This logic is implemented as a conditional branch inside the Shuffle workflow, with no human intervention required for confirmed high-severity threats.

---

## 🚀 Setup & Deployment

> 📁 Full step-by-step installation guides with screenshots are in the [`/docs/`](docs/) directory.

### Prerequisites

- Virtualization platform (VMware / VirtualBox / Proxmox)
- Minimum 16 GB RAM, 100 GB storage across VMs
- Static IP addressing on an isolated lab network

### Component Setup Order

```
1. pfSense          →  docs/setup/01-pfsense.md
2. Suricata         →  docs/setup/02-suricata.md
3. Wazuh SIEM       →  docs/setup/03-wazuh.md
4. Wazuh Agents     →  docs/setup/04-wazuh-agents.md
5. OpenEDR          →  docs/setup/05-openedr.md
6. MISP             →  docs/setup/06-misp.md
7. TheHive + Cortex →  docs/setup/07-thehive-cortex.md
8. Shuffle SOAR     →  docs/setup/08-shuffle.md
9. Discord Webhook  →  docs/setup/09-discord-webhook.md
10. Integration Testing → docs/setup/10-end-to-end-test.md
```

### Network Topology

```
[Internet] ──► [pfSense WAN] ──► [pfSense LAN] ──► [Lab Subnet 192.168.x.x]
                                        │
                          ┌─────────────┼──────────────────┐
                          │             │                  │
                     [Wazuh VM]   [TheHive VM]       [MISP VM]
                     [Shuffle VM] [Suricata inline]  [Endpoints]
```

---

## 📸 Screenshots

All screenshots from the final defense and live testing are documented in the [`/docs/screenshots/`](docs/screenshots/) directory, organized by component:

| Folder | Contents |
|:---|:---|
| `docs/screenshots/wazuh/` | Wazuh dashboard, alert views, detection rules |
| `docs/screenshots/shuffle/` | Shuffle workflow editor, execution logs |
| `docs/screenshots/thehive/` | TheHive case view, Cortex analyzer results |
| `docs/screenshots/misp/` | MISP event view, IOC feed configuration |
| `docs/screenshots/pfsense/` | pfSense firewall rules, auto-block entries |
| `docs/screenshots/suricata/` | Suricata alert logs, rule set configuration |
| `docs/screenshots/discord/` | Discord alert notification examples |
| `docs/screenshots/defense/` | Final defense presentation and demo |

---

## 🎯 Use Cases

- **Academic Major Projects** — Demonstrates end-to-end SOC architecture for BCA/BIT/B.Sc. CSIT students
- **SOC Analyst Training** — Hands-on environment for learning SIEM, SOAR, and IR workflows
- **Blue Team Practice** — Realistic threat detection and response simulation lab
- **Security Research** — Baseline open-source SOC for testing detection engineering
- **CTF & Range Environments** — Deployable as a monitoring backend for cyber exercises

---

## 👥 Project Team

<div align="center">

| | Name | Role |
|:---:|:---|:---|
| 👤 | **Rupesh Mahato** | Team Member |
| 👤 | **Ujjwal Kandel** | Team Member |
| 👤 | **Sujal Lamichhane** | Team Member |
| 🎓 | **Anuj Khanal** | Project Supervisor |

</div>

<div align="center">

Special thanks to **Anuj Khanal Sir** for his invaluable guidance, technical mentorship, and continuous support throughout the research, development, and final defense of this project.

</div>

---

## ⚖️ Disclaimer

> ⚠️ This framework is developed strictly for **educational and research purposes**. All testing was conducted within an **isolated lab environment** with no connection to production infrastructure. Do not deploy in any live or production network without thorough security hardening, penetration testing, and compliance review. The project team assumes no liability for misuse.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE). You are free to use, modify, and distribute this project for educational purposes with appropriate attribution.

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2c5364,50:203a43,100:0f2027&height=120&section=footer" width="100%"/>

**Unified SOC Framework** — Built with open-source tools, for the open-source community.

*🎓 Final Year Major Project | BCA | 2024–2025*

</div>
