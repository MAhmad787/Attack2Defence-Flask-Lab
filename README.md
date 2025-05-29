# Flask App Security Lab with Wazuh

This project is a complete **Security Lifecycle Lab** designed to simulate and showcase real-world security workflows. It starts from developing and deploying a basic Flask web application, moves into monitoring using Wazuh (an open-source SIEM/XDR solution), and ends with detection, response, and hardening techniques.

The goal is to demonstrate an end-to-end security process:

1. **Application Development & Deployment**
2. **Monitoring with Wazuh**
3. **Simulating Attacks & Observing Telemetry**
4. **Applying Security Hardening Measures**

---

## 🏋️ Project Structure (Phases)

### ✅ Phase 1: Flask App Deployment

* A simple **Flask attendance portal** is built and deployed on an Ubuntu server.
* The app uses SQLite and is hosted on a local virtual machine.
* The app is intentionally left with a few insecure practices to simulate real-world vulnerabilities.

### ✅ Phase 2: Wazuh SIEM Deployment

* **Wazuh Server** is installed on a separate dedicated VM (Ubuntu Desktop).
* The server setup includes Wazuh Indexer, Manager, and Dashboard.
* **Wazuh Agent** is installed on the Flask app VM.
* Agent is linked with the server to collect telemetry and logs.

### ✅ Phase 3: Attack Simulation and Monitoring

* Simulated attacks are performed on the Flask application including:

  * Unauthorized login attempts
  * Directory traversal
  * SQL Injection (if applicable)
* These attacks are **logged and visualized** on the Wazuh Dashboard.
* Rules and alerts are configured to detect specific malicious patterns.

### ✅ Phase 4: Security Hardening

* After analyzing the logs and attack patterns:

  * Application vulnerabilities are patched
  * Wazuh rules are enhanced
  * Firewall and logging improvements are made
  * SSH and system-level hardening is applied
* Final result is a more resilient and monitored system

---

## 🌐 Technologies Used

* **Flask**: Python-based micro web framework
* **SQLite**: Lightweight database used by the Flask app
* **Ubuntu (20.04+)**: Host OS for both app and SIEM servers
* **Wazuh**: Open-source XDR & SIEM
* **VirtualBox**: Local lab virtualization

---

## 📊 Learning Objectives

* Understand basic web application security
* Install and configure Wazuh in a lab environment
* Perform attack simulations and threat detection
* Build an incident response mindset
* Practice system and app hardening techniques

---

## 🌟 Inspiration

This project was inspired by real-world blue team scenarios and security monitoring practices. Special thanks to community resources like the [Wazuh Documentation](https://documentation.wazuh.com/) and various cybersecurity lab blogs.

---
