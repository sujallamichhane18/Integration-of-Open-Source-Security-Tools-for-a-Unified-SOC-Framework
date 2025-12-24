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

### 🎓 Supervisor
- **Anuj Khnal**

---

## 📷 Architecture Diagram

![SOC Architecture](majorprojectdiagram.drawio.png)

---

## 📂 Repository Structure (Suggested)

