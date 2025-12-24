# 🛡️ Unified Open-Source SOC Framework

This repository documents the design and implementation of a **Unified Security Operations Center (SOC) Framework** using open-source tools. The project integrates network security, SIEM, SOAR, threat intelligence, incident response, and EDR into a single, automated security architecture.

---

## 📌 Project Overview

The goal of this project is to build a **centralized SOC environment** capable of:
- Detecting security threats in real time  
- Enriching alerts with threat intelligence  
- Automating response actions  
- Managing incidents efficiently  

The architecture is designed to be **scalable, modular, and cost-effective**, making it suitable for educational, research, and small-to-medium enterprise environments.

---

## 🏗️ Architecture Components

### 🔐 Network & Perimeter Security
- **pfSense Firewall**
- **Suricata IDS/IPS**
- IOC-based blocklists for threat mitigation

### 🧠 SIEM & SOAR (DMZ)
- **Wazuh (SIEM)** – Log collection, correlation, and detection  
- **SOAR Automation** – Automated incident handling and response workflows  

### 🌐 Threat Intelligence Integration
- **VirusTotal**
- **MISP**
- **AbuseIPDB**
- **AlienVault OTX**

### 🚨 Incident Response
- **TheHive** – Incident and case management  
- **Cortex** – Automated analyzers and responders  

### 💻 Endpoint Security
- **OpenEDR**
- **Wazuh Agent** on Windows endpoints  

### 📊 Logging & Alerting
- Centralized logging
- **Discord** for real-time alert notifications  

### 🚫 Automated Response
- If **severity > 7** and confidence is high:
  - The source IP is **automatically blocked in pfSense**
- Prevents repeated attack attempts without manual intervention

---

## 🔄 Data Flow Summary

1. Network traffic monitored via **pfSense + Suricata**
2. Logs forwarded to **Wazuh SIEM**
3. Alerts enriched using **Threat Intelligence Platforms**
4. Automated actions triggered via **SOAR**
5. Incidents created and managed in **TheHive**
6. Endpoint actions handled by **OpenEDR**
7. Alerts sent to **Discord**

---

## 🎯 Project Objectives

- Implement an end-to-end SOC using open-source tools  
- Automate detection, analysis, and response  
- Improve visibility across network and endpoints  
- Demonstrate real-world SOC operations  

---

## 👥 Project Team

- **Rupesh Mahato**  
- **Ujjwal Kandel**
- **Sujal Lamichhane**  

### 🎓 Supervisor
- **Anuj Khanal**

---

## 📷 Architecture Diagram

![SOC Architecture](majorprojectdiagram.drawio.png)

---


---

## 📘 Use Case

This project can be used for:
- Academic major projects  
- SOC learning labs  
- Blue team practice  
- Open-source security research  

---

## ⚠️ Disclaimer

This project is for **educational and research purposes only**. Do not deploy in production without proper security hardening and testing.

---

## ⭐ Acknowledgment

Special thanks to our supervisor **Anuj Khanal** for guidance and support throughout the project.

