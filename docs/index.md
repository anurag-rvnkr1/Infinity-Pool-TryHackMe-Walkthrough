---

layout: default
title: "Infinity Pool — TryHackMe Walkthrough"
description: "Professional penetration testing walkthrough for the Infinity Pool TryHackMe room."
-------------------------------------------------------------------------------------------------

<div align="center">

# ♾️ Infinity Pool

### Professional TryHackMe Penetration Testing Walkthrough

> **Web Exploitation • Linux Enumeration • Internal Pivoting • Privilege Escalation**

[![TryHackMe](https://img.shields.io/badge/TryHackMe-Infinity%20Pool-red?style=for-the-badge\&logo=tryhackme)](https://tryhackme.com/)
[![Target](https://img.shields.io/badge/Linux-Target-blue?style=for-the-badge\&logo=linux)]()
[![Difficulty](https://img.shields.io/badge/Difficulty-Medium-orange?style=for-the-badge)]()
[![Category](https://img.shields.io/badge/Web-Security-success?style=for-the-badge)]()
[![Privilege Escalation](https://img.shields.io/badge/Privilege-Escalation-darkred?style=for-the-badge)]()
[![Portfolio](https://img.shields.io/badge/GitHub-Pages-purple?style=for-the-badge\&logo=github)]()

*A portfolio-ready technical report documenting the complete compromise path of the Infinity Pool TryHackMe machine using a professional penetration testing methodology.*

---

**Author:** **Anurag Ravikumar**

Cybersecurity Portfolio • Penetration Testing • TryHackMe Walkthroughs

</div>

---

# Executive Summary

Infinity Pool is a realistic Linux-based **TryHackMe** room that demonstrates how a seemingly small web vulnerability can evolve into a complete operating system compromise.

The assessment begins with reconnaissance against publicly exposed services, discovers a vulnerable internal network diagnostic endpoint, exploits **OS Command Injection** to obtain shell access, enumerates hidden localhost services, pivots through internal operational applications, abuses exposed authentication artifacts, and ultimately reaches **root-level command execution** through an authenticated automation worker.

This documentation has been written in the style of a professional penetration testing report while intentionally **redacting challenge flags, credentials, API keys, and reusable secrets**.

---

# Attack Chain Overview

<blockquote>

A complete multi-stage compromise from initial enumeration to root execution.

</blockquote>

<p align="center">
  <img src="assets/13_attack_path.png" width="100%">
</p>

```text
Internet
    │
    ▼
Nmap Enumeration
    │
    ▼
HTTP Web Application
    │
    ▼
robots.txt Discovery
    │
    ▼
/status Endpoint
    │
    ▼
OS Command Injection
    │
    ▼
Reverse Shell Access
    │
    ▼
Linux Enumeration
    │
    ▼
Watchtower Dashboard
    │
    ▼
Configuration Disclosure
    │
    ▼
FreePBX UCP
    │
    ▼
Voicemail Artifact
    │
    ▼
Automation API
    │
    ▼
Authenticated Command Injection
    │
    ▼
Root Command Execution
```

---

# Assessment Snapshot

| Category                | Details                                 |
| ----------------------- | --------------------------------------- |
| **Platform**            | TryHackMe                               |
| **Room**                | Infinity Pool                           |
| **Operating System**    | Linux                                   |
| **Primary Focus**       | Web Security & Privilege Escalation     |
| **Initial Vector**      | OS Command Injection                    |
| **Pivot Technique**     | Localhost Service Enumeration           |
| **Final Access**        | Root Context                            |
| **Documentation Style** | Professional Penetration Testing Report |

---

# Skills Demonstrated

## Offensive Security

| Skill                | Description                     |
| -------------------- | ------------------------------- |
| Reconnaissance       | Service discovery with Nmap     |
| Web Enumeration      | robots.txt, hidden endpoints    |
| Exploitation         | OS Command Injection            |
| Reverse Shell        | Interactive Bash shell          |
| Linux Enumeration    | Users, files, sockets, services |
| Internal Pivoting    | SSH Local Port Forwarding       |
| API Testing          | REST endpoint enumeration       |
| Privilege Escalation | Authenticated command execution |

## Defensive Security

| Skill                     | Description                      |
| ------------------------- | -------------------------------- |
| Attack Surface Mapping    | External vs Internal services    |
| Trust Boundary Analysis   | Localhost services               |
| CWE Analysis              | Injection & Information Exposure |
| MITRE ATT&CK Mapping      | Technique mapping                |
| Hardening Recommendations | Secure API & privilege design    |
| Detection Engineering     | IOC and monitoring guidance      |

---

# Walkthrough Timeline

| Phase                    | Objective                    | Status |
| ------------------------ | ---------------------------- | ------ |
| Reconnaissance           | External service enumeration | ✅      |
| Web Enumeration          | Hidden endpoint discovery    | ✅      |
| Initial Exploitation     | Command Injection            | ✅      |
| Initial Access           | Reverse shell obtained       | ✅      |
| Post Exploitation        | Linux enumeration            | ✅      |
| Internal Discovery       | Localhost services mapped    | ✅      |
| Watchtower Investigation | Configuration disclosure     | ✅      |
| UCP Pivot                | Internal voicemail artifact  | ✅      |
| Automation API           | Authenticated enumeration    | ✅      |
| Privilege Escalation     | Root execution confirmed     | ✅      |

---

# Technical Walkthrough Preview

## Phase 1 — Reconnaissance

Initial service discovery identified the public attack surface exposed by the target machine.

<p align="center">
<img src="../Screenshots/01_initial_web.png" width="90%">
</p>

**Highlights**

* TCP service enumeration
* HTTP fingerprinting
* SSH identification
* Initial attack surface mapping

---

## Phase 2 — Hidden Status Endpoint

The `robots.txt` file revealed an operational endpoint not linked from the public website.

<p align="center">
<img src="../Screenshots/02_status_endpoint.png" width="90%">
</p>

**Key Discovery**

* Internal connectivity checker
* Administrative functionality
* User-controlled network input

---

## Phase 3 — OS Command Injection

Input validation testing demonstrated shell interpretation of attacker-controlled input.

<p align="center">
<img src="../Screenshots/03_command_injection.png" width="90%">
</p>

**Security Impact**

* Remote command execution
* Initial foothold
* Linux command execution

---

## Phase 4 — Reverse Shell

A stable reverse shell was established and upgraded into an interactive PTY.

<p align="center">
<img src="../Screenshots/04_reverse_shell.png" width="90%">
</p>

**Techniques**

* Reverse TCP shell
* PTY stabilization
* Interactive Bash session

---

## Phase 5 — Internal Service Enumeration

Localhost services dramatically expanded the internal attack surface after compromise.

<p align="center">
<img src="../Screenshots/05_internal_services.png" width="90%">
</p>

**Important Internal Services**

| Port | Purpose              |
| ---- | -------------------- |
| 3000 | Watchtower Dashboard |
| 8080 | FreePBX UCP          |
| 9000 | Automation Service   |
| 3306 | Internal Database    |
| 5038 | Telephony Service    |

---

## Phase 6 — Watchtower Dashboard

Investigation of the internal monitoring application.

<p align="center">
<img src="../Screenshots/06_watchtower.png" width="90%">
</p>

**Focus**

* Operational dashboard
* Health monitoring
* Internal API discovery

---

## Phase 7 — Configuration Disclosure

The configuration endpoint exposed sensitive operational infrastructure.

<p align="center">
<img src="../Screenshots/07_watchtower_config.png" width="90%">
</p>

**Security Finding**

* Internal endpoints
* Operational credentials
* Administrative configuration
* Infrastructure metadata

---

## Phase 8 — SSH Local Port Forwarding

Localhost services became accessible through encrypted SSH tunnels.

<p align="center">
<img src="../Screenshots/08_ssh_port_forwarding.png" width="90%">
</p>

**Purpose**

* Browser access to internal services.
* API testing.
* Internal application pivoting.

---

## Phase 9 — FreePBX User Control Panel

Investigation of the internal telephony management interface.

<p align="center">
<img src="../Screenshots/09_ucp_login.png" width="90%">
</p>

**Discovery**

* Operational dashboard.
* Voicemail.
* Internal user functionality.

---

## Phase 10 — Voicemail Artifact

An internal voicemail contained an operational authentication artifact.

<p align="center">
<img src="../Screenshots/10_automation_key.png" width="90%">
</p>

> **Authentication material has been redacted.**

---

## Phase 11 — Automation Service

Authenticated enumeration of the internal automation platform.

<p align="center">
<img src="../Screenshots/11_automation_api.png" width="90%">
</p>

**API Endpoints**

* Health endpoint.
* Export job workflow.
* Administrative functionality.

---

## Phase 12 — Root Command Execution

Privilege escalation completed through authenticated command injection.

<p align="center">
<img src="../Screenshots/12_root_access.png" width="90%">
</p>

> Root flag intentionally hidden for portfolio publication.

---

# Vulnerability Assessment

| Vulnerability                   | Severity    | CWE     |
| ------------------------------- | ----------- | ------- |
| OS Command Injection            | 🔴 High     | CWE-78  |
| Configuration Disclosure        | 🟠 High     | CWE-200 |
| Credential Exposure             | 🟠 High     | CWE-522 |
| Authenticated Command Injection | 🔴 Critical | CWE-78  |
| Localhost Trust Boundary Abuse  | 🟠 High     | CWE-284 |

---

# MITRE ATT&CK Coverage

| ATT&CK Technique | Description                           |
| ---------------- | ------------------------------------- |
| T1595            | Active Service Scanning               |
| T1190            | Exploit Public-Facing Application     |
| T1059.004        | Unix Shell                            |
| T1046            | Network Service Discovery             |
| T1082            | System Information Discovery          |
| T1021.004        | SSH Remote Services                   |
| T1552            | Unsecured Credentials                 |
| T1078            | Valid Accounts                        |
| T1068            | Exploitation for Privilege Escalation |

---

# Security Lessons

## Red Team Perspective

* Attack chaining is essential.
* Enumeration continues after every compromise.
* Internal services often expose additional attack surface.
* Operational tooling frequently leaks sensitive information.

## Blue Team Perspective

* Localhost is not a security boundary after compromise.
* Configuration endpoints require authentication.
* Automation workers should not execute as root.
* Shell execution from web services should generate alerts.

---

# Detection Opportunities

| Detection Area         | Example                                            |
| ---------------------- | -------------------------------------------------- |
| Shell Spawn Monitoring | Gunicorn spawning Bash                             |
| API Abuse              | Suspicious `/jobs/export` requests                 |
| SSH Monitoring         | Local port forwarding sessions                     |
| Linux Enumeration      | `ss`, `whoami`, `hostname`, `id` execution         |
| Privileged Automation  | Unexpected child processes from automation workers |

---

# Documentation Included

| File                                               | Purpose                        |
| -------------------------------------------------- | ------------------------------ |
| **README.md**                                      | Repository landing page        |
| **Documentation/Documentation.md**                 | Complete technical walkthrough |
| **Documentation/Infinity_Pool_Documentation.docx** | Professional report            |
| **Resources/notes.md**                             | Technical notes                |
| **SECURITY.md**                                    | Responsible use policy         |

---

# Repository Navigation

### 📘 Full Technical Walkthrough

Detailed penetration testing documentation with methodology, exploitation analysis, MITRE ATT&CK mapping, and remediation guidance.

➡️ `Documentation/Documentation.md`

---

### 📝 Technical Notes

Quick-reference notes for commands, enumeration workflow, vulnerabilities, and key observations.

➡️ `Resources/notes.md`

---

### 🛡️ Security Policy

Repository responsible-use statement and disclosure policy.

➡️ `SECURITY.md`

---

# Screenshot Gallery

| Phase                    | Screenshot                   |
| ------------------------ | ---------------------------- |
| Initial Reconnaissance   | `01_initial_web.png`         |
| Hidden Endpoint          | `02_status_endpoint.png`     |
| Command Injection        | `03_command_injection.png`   |
| Reverse Shell            | `04_reverse_shell.png`       |
| Internal Services        | `05_internal_services.png`   |
| Watchtower Dashboard     | `06_watchtower.png`          |
| Configuration Disclosure | `07_watchtower_config.png`   |
| SSH Tunnel               | `08_ssh_port_forwarding.png` |
| FreePBX UCP              | `09_ucp_login.png`           |
| Voicemail Artifact       | `10_automation_key.png`      |
| Automation API           | `11_automation_api.png`      |
| Root Verification        | `12_root_access.png`         |

---

# Responsible Disclosure

This repository documents techniques performed **only inside an authorized TryHackMe laboratory environment**.

### Redacted Content

* User Flag
* Root Flag
* Passwords
* API Keys
* SSH Keys
* Authentication Tokens
* Sensitive Operational Secrets

The objective is to demonstrate **methodology**, **security analysis**, and **professional reporting practices**.

---

# Related Portfolio Projects

| Repository                  | Focus                                   |
| --------------------------- | --------------------------------------- |
| **CryptoCabana**            | Web Exploitation & Privilege Escalation |
| **Do Not Disturb**          | Linux Enumeration & Web Security        |
| **Valenfind**               | Local File Inclusion & Web Exploitation |
| **Corp Website**            | Next.js Web Security & RCE              |
| **Active Directory Basics** | Windows Active Directory Fundamentals   |

---

# About This Portfolio

This walkthrough is part of a growing cybersecurity portfolio documenting practical labs completed on **TryHackMe**.

### Portfolio Focus Areas

* Penetration Testing
* Web Application Security
* Linux Privilege Escalation
* Active Directory
* SOC & Detection Engineering
* Threat Hunting
* Security Automation

Each repository includes:

* Professional documentation.
* GitHub Pages support.
* Architecture diagrams.
* MITRE ATT&CK mapping.
* Defensive recommendations.
* Ethical redaction of challenge answers.

---

<div align="center">

## ⭐ Thank you for visiting this walkthrough.

**Infinity Pool — Professional Cybersecurity Portfolio Project**

Made with ❤️ for learning, documentation, and ethical security research.

</div>
