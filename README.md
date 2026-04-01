<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f2027,50:203a43,100:2c5364&height=230&section=header&text=Unified%20SOC%20Framework&fontSize=48&fontColor=ffffff&fontAlignY=36&desc=Integration%20of%20Open-Source%20Security%20Tools%20for%20a%20Unified%20SOC%20Framework&descAlignY=56&descSize=14" width="100%"/>

<br/>

[![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-0078D4?style=for-the-badge&logoColor=white)](https://wazuh.com)
[![pfSense](https://img.shields.io/badge/Firewall-pfSense-212121?style=for-the-badge&logoColor=white)](https://pfsense.org)
[![Suricata](https://img.shields.io/badge/IDS%2FIPS-Suricata-EF6C00?style=for-the-badge&logoColor=white)](https://suricata.io)
[![Shuffle](https://img.shields.io/badge/SOAR-Shuffle-7C3AED?style=for-the-badge&logoColor=white)](https://shuffler.io)
[![TheHive](https://img.shields.io/badge/IR-TheHive-F59E0B?style=for-the-badge&logoColor=black)](https://thehive-project.org)
[![MISP](https://img.shields.io/badge/TI-MISP-DC2626?style=for-the-badge&logoColor=white)](https://www.misp-project.org)
[![License](https://img.shields.io/badge/License-MIT-22C55E?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Defense-Completed-brightgreen?style=for-the-badge)]()

<br/>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=17&pause=1000&color=00D9FF&center=true&vCenter=true&width=700&lines=Real-time+Threat+Detection+%26+SIEM+Correlation;Automated+Incident+Response+via+Shuffle+SOAR;Threat+Intelligence+Enrichment+%7C+MISP+%2B+VirusTotal;End-to-End+Open-Source+Security+Operations+Center" alt="Typing SVG" />

<br/><br/>

---

### 🎓 Academic Affiliation

**Forbes College, Kathmandu, Nepal**
*Affiliated with University of Computer Science and Skills, Łódź, Poland*

**Programme:** Bachelor of Computer Science (B.Sc. CS)
**Specialization:** Cybersecurity & Networking
**Project Type:** Final Year Major Project 

---

</div>

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

This project implements a **fully integrated, open-source Security Operations Center (SOC)** developed as a final year major project for the **Bachelor of Computer Science (Cybersecurity & Networking)** programme at Forbes College, Nepal — affiliated with the University of Computer Science and Skills, Łódź, Poland.

The framework is capable of:

- 🔎 **Monitoring** network traffic and endpoint activity in real time
- 🧩 **Correlating** security events across multiple log sources via Wazuh SIEM
- 🌐 **Enriching** alerts with external threat intelligence (VirusTotal, MISP, AbuseIPDB, AlienVault OTX)
- ⚡ **Automating** incident response workflows using **Shuffle SOAR**
- 🚨 **Notifying** analysts via Discord webhooks for high-severity incidents
- 🛡️ **Blocking** malicious IPs at the firewall level — without any manual intervention

The framework is fully modular and cost-free to deploy, making it practical for **academic labs**, **blue team training environments**, **SOC analyst onboarding**, and **small-to-medium enterprise security operations**.

---

## 🏗️ Architecture

<div align="center">
<img src="majorprojectdiagram.drawio.png" alt="SOC Architecture Diagram" width="92%"/>

*Figure: High-level architecture of the Unified SOC Framework*
</div>

---

## 💻 Technology Stack

<div align="center">

| Layer | Tool | Purpose |
|:---:|:---|:---|
| 🔥 **Firewall / Gateway** | pfSense | Network perimeter control, automated IP blocking via REST API |
| 🕵️ **IDS / IPS** | Suricata | Signature-based deep packet inspection and traffic analysis |
| 📊 **SIEM** | Wazuh | Log aggregation, correlation rules, XDR-level threat detection |
| 🤖 **SOAR** | Shuffle | Workflow orchestration and automated playbook execution |
| 🗂️ **Incident Response** | TheHive + Cortex | Case management, automated observable analyzers |
| 🌐 **Threat Intelligence** | MISP | Structured IOC management and community feed synchronization |
| 🔍 **TI Enrichment** | VirusTotal · AbuseIPDB · AlienVault OTX | Real-time indicator scoring and enrichment |
| 💻 **Endpoint Detection** | OpenEDR + Wazuh Agent | Endpoint telemetry and file integrity monitoring (FIM) |
| 🔔 **Notifications** | Discord Webhook | Real-time analyst alerting with enriched summaries |

</div>

---

## 🧱 Core Components

### 1. 🔥 pfSense — Perimeter Firewall
pfSense serves as the network gateway providing stateful packet filtering, VLAN segmentation, and NAT. It exposes a REST API allowing the Shuffle SOAR engine to programmatically insert block rules when a malicious source IP is confirmed by threat intelligence.

### 2. 🕵️ Suricata — IDS/IPS
Deployed inline behind pfSense, Suricata performs deep packet inspection against the Emerging Threats ruleset. It generates EVE JSON logs that are forwarded to Wazuh for correlation. In IPS mode, it can drop packets matching high-confidence signatures at wire speed.

### 3. 📊 Wazuh — SIEM & XDR
The central detection engine of the SOC. Wazuh aggregates logs from all sources — pfSense, Suricata, and endpoints — and applies detection rules to generate alerts scored from 0–15. Custom decoders and correlation rules were authored specifically for this project to detect port scans, brute-force attempts, and lateral movement.

### 4. 🤖 Shuffle — SOAR Platform
Shuffle orchestrates all automated response workflows through a visual drag-and-drop editor. When Wazuh fires a critical alert via webhook, a Shuffle workflow automatically parses, enriches, evaluates, and responds — creating firewall rules, TheHive cases, and Discord notifications without human intervention.

### 5. 🗂️ TheHive + Cortex — Case Management
TheHive receives escalated cases from Shuffle and provides structured incident tracking. Cortex analyzers run automatically on observable data (IPs, file hashes, domains) to surface forensic context using VirusTotal, MISP, and other responders.

### 6. 🌐 MISP — Threat Intelligence Platform
MISP acts as the local threat intelligence database. Indicators of compromise (IOCs) — IPs, domains, file hashes — are stored, tagged, and queried during alert enrichment. MISP is synchronized with community threat feeds for current coverage.

### 7. 💻 OpenEDR + Wazuh Agent — Endpoint Layer
Wazuh agents installed on monitored endpoints ship system logs, audit events, and FIM changes. OpenEDR adds process-level telemetry to detect malware execution, persistence techniques, and anomalous behavior.

---

## 🔄 Data Flow

```
╔═══════════════════════════════════════════════════════════════════════╗
║                         NETWORK PERIMETER                             ║
║     [ pfSense Firewall ]  ──►  [ Suricata IDS/IPS ]                   ║
║       ↑ Block Rule via API           │ EVE JSON Logs                  ║
╚═══════════════════════╤═════════════╪═══════════════════════════════╤═╝
                        │             │                               │
                        │             ▼                               │
╔═══════════════════════╪══════════════════════════════════════════════╗
║                             SIEM — Wazuh                             ║
║       Endpoint Logs ──►  Log Aggregation & Normalization             ║
║     [ Wazuh Agents + OpenEDR ]                                       ║
║                         Correlation Rules & Threat Detection         ║
║                         Alert Generated  →  Severity Score 0–15      ║
╚══════════════════════════════════════╤══════════════════════════════╝
                                       │ Webhook (severity > 7)
                                       ▼
╔══════════════════════════════════════════════════════════════════════╗
║                      SOAR — Shuffle Workflow                         ║
║                                                                      ║
║  [1] Receive Wazuh Alert ──► [2] Parse JSON Payload                  ║
║                                       │                              ║
║                            [3] Enrich IOC                            ║
║                     VirusTotal · AbuseIPDB · OTX · MISP              ║
║                                       │                              ║
║                   [4] Evaluate Severity + TI Confidence              ║
║                                       │                              ║
║         ┌──── HIGH (score > 7 + confidence ≥ HIGH) ─────────────┐    ║
║         │                                                        │   ║
║  [5] Block IP — pfSense API                          LOW → Monitor   ║
║  [6] Create Case — TheHive                                           ║
║  [7] Notify — Discord Webhook                                        ║
╚══════════════════════════════════════════════════════════════════════╝
              │
              ▼
╔══════════════════════════════════════╗
║        TheHive + Cortex              ║
║   Case Management & Triage           ║
║   Cortex Auto-Analyzers (IOCs)       ║
╚══════════════════════════════════════╝
```

---

## ⚡ SOAR Automation with Shuffle

Shuffle is the orchestration layer that ties every component together. The primary response workflow was built and tested using Shuffle's visual workflow editor and deployed as the SOC's automated playbook.

### Workflow Steps

| Step | Action | Integration Used |
|:---:|:---|:---|
| **1** | Receive Wazuh alert via webhook trigger | Wazuh → Shuffle HTTP trigger |
| **2** | Extract source IP, rule ID, agent, severity | Shuffle — JSON parser node |
| **3** | Query VirusTotal for IP reputation score | VirusTotal API |
| **4** | Query AbuseIPDB for abuse confidence score | AbuseIPDB API |
| **5** | Query AlienVault OTX for passive DNS / IOCs | OTX API |
| **6** | Match against local MISP IOC database | MISP API |
| **7** | Evaluate combined severity + confidence score | Shuffle — condition branch node |
| **8** | *(High confidence)* Block source IP at firewall | pfSense REST API |
| **9** | *(High confidence)* Create enriched case in TheHive | TheHive API |
| **10** | Send formatted Discord notification to analyst | Discord Webhook |


---

## 🤖 Automated Response Logic

An automated firewall block and case creation is triggered when **both** of the following conditions are satisfied:

- **Wazuh severity score > 7** (out of 15)
- **Threat intelligence confidence = HIGH** — corroborated by at least one external TI source (VirusTotal malicious verdict, AbuseIPDB confidence ≥ 75%, or a confirmed MISP IOC match)

```python
# Conceptual logic mirroring the Shuffle workflow decision node
def process_alert(alert):
    enrichment = {
        "virustotal":  virustotal.lookup(alert.source_ip),
        "abuseipdb":   abuseipdb.lookup(alert.source_ip),
        "misp":        misp.search_ioc(alert.source_ip),
        "otx":         otx.lookup(alert.source_ip),
    }

    confidence = evaluate_confidence(enrichment)   # "HIGH" | "MEDIUM" | "LOW"

    if alert.severity > 7 and confidence == "HIGH":
        pfsense.block_ip(alert.source_ip)           # Firewall rule insertion
        thehive.create_case(alert, enrichment)       # Structured case management
        discord.notify(alert, enrichment)            # Analyst notification
    else:
        wazuh.log_for_monitoring(alert)              # Queued for manual review
```

This logic executes entirely within the Shuffle workflow — no human action is required for confirmed high-severity threats.

---

## 🚀 Setup & Deployment

> 📁 Full step-by-step installation guides with screenshots are available in final-defense (7th sem).docx

### Prerequisites

- Virtualization platform (VMware Workstation / VirtualBox / Proxmox)
- Minimum **64 GB RAM**, **100 GB storage** distributed across VMs
- Isolated lab network with static IP addressing


 

### Lab Network Topology

```
[Internet] ──► [pfSense WAN] ──► [pfSense LAN] ──► [Lab: 192.168.x.x/24]
                                        │
               ┌────────────┬──────────┼───────────┬──────────────┐
               │            │          │           │              │
          [Wazuh VM]  [Shuffle VM] [TheHive VM] [MISP VM]  [Endpoint VMs]
                                 [Suricata — inline tap]
```



## 🎯 Use Cases

- **Final Year Academic Projects** — Demonstrates end-to-end SOC design for B.Sc. CS / BCA / BIT students
- **SOC Analyst Training** — Hands-on lab for learning SIEM, SOAR, and IR workflows from scratch
- **Blue Team Exercises** — Realistic threat detection and response simulation environment
- **Cybersecurity Research** — Open-source baseline SOC for detection engineering and rule development
- **CTF & Cyber Range** — Deployable as a monitoring backend for capture-the-flag and team exercises

---

## 👥 Project Team


<br/>

| | Name | Role |
|:---:|:---|:---|
| 👤 | **Rupesh Mahato** | Team Member |
| 👤 | **Ujjwal Kandel** | Team Member |
| 👤 | **Sujal Lamichhane** | Team Member |

<br/>



---

## ⚖️ Disclaimer

> ⚠️ This framework was developed strictly for **academic research and educational purposes**. All testing was conducted within a fully **isolated virtual lab environment** with no connection to any production or live infrastructure. The project team and Forbes College bear no responsibility for misuse or unauthorized deployment. Do not deploy in any production network without thorough security hardening, penetration testing, and compliance review.

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2c5364,50:203a43,100:0f2027&height=130&section=footer" width="100%"/>

**Integration of Open-Source Security Tools for a Unified SOC Framework**

🏫 Forbes College, Chitwan, Nepal &nbsp;·&nbsp; 🌍 University of Computer Science and Skills, Łódź, Poland

*B.Sc. Computer Science · Cybersecurity & Networking · Final Year Major Project · 2024–2025*

</div>
