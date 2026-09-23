# ♾️ Infinity Pool — TryHackMe Walkthrough

<div align="center">

<img src="https://tryhackme-images.s3.amazonaws.com/room-icons/tryhackme_logo_full.svg" width="120" alt="TryHackMe"/>

# Infinity Pool

### Professional Penetration Testing Walkthrough • TryHackMe CTF • Red Team Portfolio Project

[![Platform](https://img.shields.io/badge/TryHackMe-CTF-red?style=for-the-badge\&logo=tryhackme)](https://tryhackme.com/)
[![Difficulty](https://img.shields.io/badge/Difficulty-Medium-orange?style=for-the-badge)]()
[![OS](https://img.shields.io/badge/Target-Linux-blue?style=for-the-badge\&logo=linux)]()
[![Focus](https://img.shields.io/badge/Web-Security-success?style=for-the-badge)]()
[![Privilege Escalation](https://img.shields.io/badge/Privilege-Escalation-darkred?style=for-the-badge)]()
[![Writeup](https://img.shields.io/badge/Portfolio-Documentation-purple?style=for-the-badge)]()

*A complete security assessment of the Infinity Pool TryHackMe machine demonstrating reconnaissance, web exploitation, internal network pivoting, authenticated API abuse, command injection, reverse shell access, and Linux privilege escalation.*

</div>

---

## 📖 Overview

**Infinity Pool** is a realistic Linux-based web application challenge available on **TryHackMe** that simulates an internal hospitality management environment with multiple interconnected services.

This walkthrough follows a professional penetration testing methodology beginning with **service enumeration**, identifying a **command injection vulnerability** in a web utility, obtaining a shell, pivoting into **localhost-only services**, extracting operational secrets from an internal application, abusing an authenticated automation API, and ultimately achieving **root command execution**.

> **Portfolio Edition:** All challenge flags, reusable credentials, automation keys, and sensitive values have been intentionally **redacted** for ethical sharing and plagiarism prevention.

---

## 🎯 Objectives

* Enumerate externally exposed services.
* Discover hidden web application endpoints.
* Exploit OS Command Injection.
* Gain an interactive reverse shell.
* Enumerate internal localhost services.
* Pivot into administrative applications.
* Abuse exposed operational secrets.
* Exploit an authenticated automation service.
* Escalate privileges to root.
* Document the complete attack chain professionally.

---

## 🧠 Skills Demonstrated

<table>
<tr>
<td width="50%">

### Offensive Security

* Nmap Enumeration
* Web Reconnaissance
* Robots.txt Discovery
* OS Command Injection
* Reverse Shells
* Shell Stabilization
* Linux Enumeration
* API Reconnaissance
* SSH Port Forwarding
* Internal Service Pivoting

</td>

<td width="50%">

### Blue Team Knowledge

* Attack Surface Mapping
* Secret Exposure Risks
* Internal Trust Boundaries
* Loopback Service Enumeration
* Secure API Design
* Privilege Separation
* Least Privilege
* Mitigation Recommendations
* Security Documentation
* Reporting Methodology

</td>
</tr>
</table>

---

# ⚔️ Attack Chain

<div align="center">

![Attack Chain](docs/assets/13_attack_path.png)

</div>

```text
Nmap Enumeration
      │
      ▼
HTTP Service (Port 80)
      │
      ▼
robots.txt Discovery
      │
      ▼
/status Internal Netcheck
      │
      ▼
OS Command Injection
      │
      ▼
Reverse Shell (web)
      │
      ▼
Local Service Enumeration
      │
      ├── Watchtower (3000)
      ├── UCP (8080)
      └── Automation API (9000)
              │
              ▼
Configuration Disclosure
              │
              ▼
Voicemail → Automation Key
              │
              ▼
Authenticated API Abuse
              │
              ▼
Root Command Execution
```

---

# 🗺️ Penetration Testing Methodology

| Phase                    | Description                                                               |
| ------------------------ | ------------------------------------------------------------------------- |
| **Reconnaissance**       | External service discovery using Nmap.                                    |
| **Web Enumeration**      | Discovery of hidden resources through robots.txt and application mapping. |
| **Initial Exploitation** | OS command injection within a connectivity testing feature.               |
| **Initial Access**       | Reverse shell obtained under the web service account.                     |
| **Post Exploitation**    | Local enumeration and discovery of internal-only services.                |
| **Lateral Pivot**        | Access to Watchtower and UCP using localhost pivoting.                    |
| **Credential Discovery** | Operational secrets obtained from internal voicemail.                     |
| **Privilege Escalation** | Authenticated automation API abused for root-level command execution.     |

---

# 📂 Repository Structure

```text
Infinity-Pool-TryHackMe-Walkthrough/
│
├── README.md
├── SECURITY.md
├── LICENSE
├── _config.yml
│
├── Documentation/
│   ├── Documentation.md
│   └── Infinity_Pool_Documentation.docx
│
├── Resources/
│   └── notes.md
│
├── Screenshots/
│   ├── 01_initial_web.png
│   ├── 02_status_endpoint.png
│   ├── 03_command_injection.png
│   ├── 04_reverse_shell.png
│   ├── 05_internal_services.png
│   ├── 06_watchtower.png
│   ├── 07_watchtower_config.png
│   ├── 08_ssh_port_forwarding.png
│   ├── 09_ucp_login.png
│   ├── 10_automation_key.png
│   ├── 11_automation_api.png
│   └── 12_root_access.png
│
└── docs/
    ├── index.md
    └── assets/
        └── 13_attack_path.png
```

---

# 🖥️ Walkthrough Preview

## Phase 1 — External Reconnaissance

Discover publicly exposed services and identify the attack surface.

<p align="center">
<img src="Screenshots/01_initial_web.png" width="850"/>
</p>

**Highlights**

* HTTP Enumeration
* SSH Discovery
* Service Fingerprinting

---

## Phase 2 — Hidden Endpoint Discovery

Enumeration of hidden application resources exposed through robots.txt.

<p align="center">
<img src="Screenshots/02_status_endpoint.png" width="850"/>
</p>

**Key Finding**

* Internal Netcheck utility discovered.

---

## Phase 3 — Command Injection

Testing input validation within the network connectivity utility.

<p align="center">
<img src="Screenshots/03_command_injection.png" width="850"/>
</p>

**Result**

* OS Command Injection confirmed.

---

## Phase 4 — Initial Shell Access

Establishing an interactive shell on the target.

<p align="center">
<img src="Screenshots/04_reverse_shell.png" width="850"/>
</p>

**Techniques**

* Reverse Shell
* PTY Stabilization
* Interactive Bash Session

---

## Phase 5 — Internal Service Enumeration

Discovering localhost-only services unavailable externally.

<p align="center">
<img src="Screenshots/05_internal_services.png" width="850"/>
</p>

**Interesting Services**

* Watchtower
* UCP
* Automation API
* Database
* Telephony Services

---

## Phase 6 — Watchtower Investigation

Analysis of the internal operational dashboard.

<p align="center">
<img src="Screenshots/06_watchtower.png" width="850"/>
</p>

---

## Phase 7 — Configuration Disclosure

Inspecting internal configuration APIs.

<p align="center">
<img src="Screenshots/07_watchtower_config.png" width="850"/>
</p>

**Findings**

* Internal endpoints.
* Operational secrets.
* Administrative notes.

Sensitive information has been redacted.

---

## Phase 8 — SSH Local Port Forwarding

Pivoting localhost services securely to the attack workstation.

<p align="center">
<img src="Screenshots/08_ssh_port_forwarding.png" width="850"/>
</p>

---

## Phase 9 — FreePBX UCP Access

Authenticated access to the internal User Control Panel.

<p align="center">
<img src="Screenshots/09_ucp_login.png" width="850"/>
</p>

---

## Phase 10 — Voicemail Artifact Discovery

Operational voicemail revealing an automation artifact.

<p align="center">
<img src="Screenshots/10_automation_key.png" width="850"/>
</p>

> Automation key intentionally hidden.

---

## Phase 11 — Automation API

Inspection of the internal automation service.

<p align="center">
<img src="Screenshots/11_automation_api.png" width="850"/>
</p>

**Observed**

* Internal API endpoints.
* Authenticated export workflow.
* Root automation worker.

---

## Phase 12 — Root Context Verification

Final privilege escalation.

<p align="center">
<img src="Screenshots/12_root_access.png" width="850"/>
</p>

Root flag has been redacted.

---

# 🔍 Vulnerability Summary

| Vulnerability                       | Impact                                                  |
| ----------------------------------- | ------------------------------------------------------- |
| OS Command Injection                | Remote command execution under web service account.     |
| Internal Configuration Disclosure   | Exposure of internal endpoints and operational secrets. |
| Localhost Administrative Services   | Expanded attack surface after initial compromise.       |
| Authenticated API Command Injection | Root-level arbitrary command execution.                 |

---

# 🛡️ Defensive Recommendations

### Web Application Security

* Avoid executing shell commands with user input.
* Validate and sanitize all external parameters.
* Use safe subprocess argument handling.

### Infrastructure Security

* Restrict localhost administrative services.
* Implement authentication and authorization for internal APIs.
* Rotate exposed credentials immediately.

### Privilege Management

* Run automation workers as non-root users.
* Apply least privilege to service accounts.
* Separate operational services into isolated environments.

### Monitoring

* Detect unexpected shell execution from web processes.
* Monitor child-process spawning from API services.
* Audit privileged automation workflows.

---

# 📚 Documentation Included

| File                                             | Purpose                                        |
| ------------------------------------------------ | ---------------------------------------------- |
| `README.md`                                      | GitHub landing page.                           |
| `Documentation/Documentation.md`                 | Full technical walkthrough.                    |
| `Documentation/Infinity_Pool_Documentation.docx` | Professional report format.                    |
| `Resources/notes.md`                             | Quick methodology notes.                       |
| `docs/index.md`                                  | GitHub Pages portfolio documentation.          |
| `SECURITY.md`                                    | Responsible disclosure and ethical use policy. |

---

# 🌐 GitHub Pages Portfolio

The repository includes a dedicated **GitHub Pages** documentation site.

### Features

* Dark cybersecurity theme.
* Responsive layout.
* Attack chain visualization.
* Embedded screenshots.
* Executive summary.
* Defensive recommendations.
* Professional portfolio formatting.

---

# ⚠️ Ethical Use

This repository documents techniques used **only inside an authorized TryHackMe laboratory environment**.

**The following items are intentionally hidden:**

* 🚫 User Flag
* 🚫 Root Flag
* 🚫 Automation Key
* 🚫 Passwords
* 🚫 Tokens
* 🚫 Sensitive Secrets

The goal is to demonstrate methodology rather than distribute challenge answers.

---

# 👨‍💻 Author

## Anurag Ravikumar

Cybersecurity Enthusiast • SOC Analyst Aspirant • Penetration Testing Learner

**Portfolio Focus**

* TryHackMe Walkthroughs
* Active Directory Labs
* Web Application Security
* Linux Privilege Escalation
* Detection Engineering
* Security Automation Projects

GitHub repositories are maintained as professional cybersecurity portfolio projects with structured documentation and GitHub Pages support.

---

<div align="center">

### ⭐ If this repository helped you learn something, consider giving it a star!

**Made for cybersecurity learning, documentation, and portfolio development.**

</div>
