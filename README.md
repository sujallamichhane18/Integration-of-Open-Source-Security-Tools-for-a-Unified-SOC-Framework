<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f2027,50:203a43,100:2c5364&height=200&section=header&text=Unified%20SOC%20Framework&fontSize=42&fontColor=ffffff&fontAlignY=38&desc=Open-Source%20Security%20Operations%20Center&descAlignY=58&descSize=18" width="100%"/>

<br/>

[![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-blue?style=for-the-badge&logoColor=white)](https://wazuh.com)
[![pfSense](https://img.shields.io/badge/Firewall-pfSense-212121?style=for-the-badge&logoColor=white)](https://pfsense.org)
[![Suricata](https://img.shields.io/badge/IDS%2FIPS-Suricata-orange?style=for-the-badge&logoColor=white)](https://suricata.io)
[![TheHive](https://img.shields.io/badge/IR-TheHive-yellow?style=for-the-badge&logoColor=black)](https://thehive-project.org)
[![MISP](https://img.shields.io/badge/TI-MISP-red?style=for-the-badge&logoColor=white)](https://www.misp-project.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)]()

<br/>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=18&pause=1000&color=00D9FF&center=true&vCenter=true&width=600&lines=Real-time+Threat+Detection;Automated+Incident+Response;Open-Source+%26+Fully+Integrated;Built+for+Blue+Teams" alt="Typing SVG" />

</div>

---

## Overview

This project implements a **fully integrated, open-source Security Operations Center** capable of monitoring network traffic, correlating security events, enriching alerts with threat intelligence, and automatically responding to high-severity incidents — all without manual intervention.

The framework is modular and cost-effective, making it suitable for academic labs, SOC analyst training, blue team exercises, and small-to-medium enterprise environments.

<div align="center">
<img src="docs/assets/soc-demo.gif" alt="SOC Dashboard Demo" width="85%" style="border-radius: 8px; border: 1px solid #30363d;"/>
<br/>
<sub>↑ Replace with a screen recording of your dashboard in action (save as docs/assets/soc-demo.gif)</sub>
</div>

---

## Architecture

<div align="center">
<img src="majorprojectdiagram.drawio.png" alt="SOC Architecture Diagram" width="90%"/>
</div>

### Data Flow

```
 ┌─────────────────────────────────────────────────────────────────────┐
 │                        NETWORK PERIMETER                            │
 │   [ pfSense Firewall ]  ──►  [ Suricata IDS/IPS ]                  │
 └──────────────────────────────────┬──────────────────────────────────┘
                                    │ Logs & Alerts
                                    ▼
 ┌─────────────────────────────────────────────────────────────────────┐
 │                           SIEM (DMZ)                                │
 │                        [ Wazuh SIEM ]                               │
 │              Log Aggregation · Correlation · Detection              │
 └────────────┬────────────────────────────────────────────────────────┘
              │ Enrichment Queries
              ▼
 ┌─────────────────────────────────────────────────────────────────────┐
 │                     THREAT INTELLIGENCE                             │
 │   [ VirusTotal ]  [ MISP ]  [ AbuseIPDB ]  [ AlienVault OTX ]      │
 └────────────┬────────────────────────────────────────────────────────┘
              │ Enriched Alert
              ▼
 ┌─────────────────────────────────────────────────────────────────────┐
 │                        SOAR ENGINE                                  │
 │         severity > 7 + high confidence  ──►  Auto-block IP         │
 └──────┬──────────────────────────────────────────────────────┬───────┘
        │                                                      │
        ▼                                                      ▼
 [ TheHive + Cortex ]                                  [ Discord Alert ]
 Case creation · Analysis                         Real-time notification
        │
        ▼
 [ OpenEDR + Wazuh Agent ]
 Endpoint isolation · FIM
```

---

## Stack

<div align="center">

| Layer | Tool | Purpose |
|---|---|---|
| **Firewall** | pfSense | Network gateway, automated IP blocking |
| **IDS/IPS** | Suricata | Signature-based traffic inspection |
| **SIEM** | Wazuh | Log aggregation, correlation, detection |
| **Threat Intel** | VirusTotal · MISP · AbuseIPDB · OTX | Alert enrichment |
| **Incident Response** | TheHive + Cortex | Case management, automated analyzers |
| **Endpoint** | OpenEDR + Wazuh Agent | EDR, file integrity monitoring |
| **Notifications** | Discord Webhook | Real-time alert delivery |

</div>

---

## Automated Response

When an alert satisfies **both** of the following conditions:

- Severity score **> 7 / 10**
- Threat intelligence confidence is **high** (corroborated by ≥ 1 TI source)

The SOAR engine issues an automated firewall block rule via the pfSense API, preventing further inbound traffic from the source IP without human intervention.

```python
# Simplified response logic
if alert.severity > 7 and alert.ti_confidence == "high":
    pfsense.block_ip(alert.source_ip)
    thehive.create_case(alert)
    discord.notify(alert)
```

---

## Quickstart

> **Prerequisites:** Docker, Docker Compose, access to pfSense admin panel

```bash
# Clone the repository
git clone https://github.com/your-org/unified-soc-framework.git
cd unified-soc-framework

# Copy and configure environment variables
cp .env.example .env

# Start the core stack
docker-compose up -d wazuh thehive cortex misp

# Verify services are running
docker-compose ps
```

Detailed setup guides for each component are in [`/docs`](./docs).

---

## Screenshots

<div align="center">
<table>
  <tr>
    <td align="center">
      <img src="docs/assets/wazuh-dashboard.png" width="380px" alt="Wazuh Dashboard"/><br/>
      <sub>Wazuh SIEM Dashboard</sub>
    </td>
    <td align="center">
      <img src="docs/assets/thehive-case.png" width="380px" alt="TheHive Case"/><br/>
      <sub>TheHive Incident Case</sub>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="docs/assets/discord-alert.png" width="380px" alt="Discord Alert"/><br/>
      <sub>Discord Alert Notification</sub>
    </td>
    <td align="center">
      <img src="docs/assets/pfsense-block.png" width="380px" alt="pfSense Block"/><br/>
      <sub>Automated IP Block in pfSense</sub>
    </td>
  </tr>
</table>
<sub>↑ Add your own screenshots to docs/assets/ and update the paths above</sub>
</div>

---

## Use Cases

- Academic capstone and major projects
- SOC analyst training and onboarding labs
- Blue team practice environments
- Open-source security operations research

---

## Project Team

<div align="center">

| | Name | Role |
|---|---|---|
| 👤 | **Rupesh Mahato** | Team Member |
| 👤 | **Ujjwal Kandel** | Team Member |
| 👤 | **Sujal Lamichhane** | Team Member |
| 🎓 | **Anuj Khanal** | Supervisor |

</div>

Special thanks to our supervisor **Anuj Khanal** for his continued guidance and support throughout this project.

---

## Disclaimer

> This framework is intended for **educational and research purposes only**. Do not deploy in a production environment without proper security hardening, penetration testing, and compliance review.

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2c5364,50:203a43,100:0f2027&height=100&section=footer" width="100%"/>

*Built with open-source tools for the open-source community*

</div>
