# ♾️ Infinity Pool — TryHackMe Walkthrough

> Professional, portfolio-ready documentation of the **Infinity Pool** TryHackMe room, covering external enumeration, web command injection, reverse-shell access, localhost service discovery, internal application pivoting, and root-level command execution.

[![TryHackMe](https://img.shields.io/badge/TryHackMe-Infinity%20Pool-red?style=for-the-badge&logo=tryhackme)](https://tryhackme.com/)
[![Platform](https://img.shields.io/badge/Platform-TryHackMe-critical?style=for-the-badge)](https://tryhackme.com/)
[![Focus](https://img.shields.io/badge/Focus-Web%20%7C%20Linux%20%7C%20Privilege%20Escalation-blue?style=for-the-badge)](#-skills-demonstrated)
[![Docs](https://img.shields.io/badge/Docs-GitHub%20Pages-success?style=for-the-badge)](docs/)

## 📌 Overview

Infinity Pool is a multi-stage Linux web-security lab. The documented route begins with port enumeration and web discovery, identifies command injection in a network-check feature, establishes shell access, enumerates loopback-only services, pivots through an internal Watchtower/UCP workflow, extracts an automation credential from voicemail, and reaches root through a second command-injection primitive in an internal export service.

## 🧭 Attack Chain

```text
External Nmap
    │
    ▼
Web application :80
    │
    ▼
robots.txt → /status
    │
    ▼
Command injection
    │
    ▼
Reverse shell → web
    │
    ▼
Local service enumeration
    │
    ├── Watchtower :3000
    ├── UCP :8080
    └── Automation :9000
              │
              ▼
        Watchtower config
              │
              ▼
         UCP voicemail
              │
              ▼
        Automation key
              │
              ▼
      /jobs/export command injection
              │
              ▼
          root context
```

![Attack path](docs/assets/13_attack_path.png)

## 🧰 Skills Demonstrated

- Nmap service/version enumeration
- Web endpoint discovery
- `robots.txt` analysis
- OS command injection identification
- Reverse shells and shell stabilization
- Linux local enumeration
- Loopback-only service discovery
- SSH local port forwarding
- Internal application reconnaissance
- API endpoint discovery
- Credential/artifact chaining
- Authenticated command injection
- Root command execution validation
- Professional evidence handling and redaction

## 🗂️ Repository Layout

```text
.
├── Documentation/
│   ├── Documentation.md
│   └── Infinity_Pool_Documentation.docx
├── Resources/
│   └── notes.md
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
├── docs/
│   ├── assets/
│   │   └── 13_attack_path.png
│   └── index.md
├── Security.md
└── README.md
```

## 🔐 Flags & Sensitive Data

Flags, reusable credentials, private keys, and other challenge-sensitive values are intentionally hidden or redacted in the public-facing evidence.

> **Note:** This repository is designed for portfolio presentation and methodology review. Use the TryHackMe lab itself for challenge execution.

## ⚠️ Ethical Use

All techniques documented here were performed against an authorized TryHackMe training environment. Do not apply these techniques to systems without explicit permission.

## 📚 Documentation

- [Full technical documentation](Documentation/Documentation.md)
- [Quick-reference notes](Resources/notes.md)
- [GitHub Pages portfolio](docs/index.md)
- [Security & responsible use](Security.md)
