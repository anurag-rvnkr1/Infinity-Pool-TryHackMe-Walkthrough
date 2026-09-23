# Infinity Pool — Technical Notes

> **Room:** Infinity Pool (TryHackMe)
> **Category:** Web Application Security • Linux Privilege Escalation • Internal Service Pivoting
> **Purpose:** Personal penetration testing notes and methodology reference for the Infinity Pool CTF.

---

## Objective

Document the methodology used during the Infinity Pool assessment while preserving operational security by redacting challenge-sensitive information. These notes summarize the reconnaissance, exploitation path, internal pivoting, and privilege escalation workflow followed during the engagement.

---

# Assessment Workflow

```text
Reconnaissance
      │
      ▼
Web Enumeration
      │
      ▼
Hidden Endpoint Discovery
      │
      ▼
OS Command Injection
      │
      ▼
Reverse Shell
      │
      ▼
Linux Enumeration
      │
      ▼
Internal Services Discovery
      │
      ▼
Watchtower Investigation
      │
      ▼
UCP / Voicemail Pivot
      │
      ▼
Automation API Enumeration
      │
      ▼
Authenticated Command Injection
      │
      ▼
Root Context
```

---

# Phase 1 — Reconnaissance

## Initial Enumeration

Primary objective: identify externally exposed services and technologies.

**Enumeration tool**

```bash
nmap <TARGET_IP> -sV
```

### Observations

* Target responds on HTTP.
* SSH service is available.
* Web application appears to be hosted behind Gunicorn.
* Limited external attack surface suggests additional internal services may exist.

### Initial Attack Surface

| Service | Purpose                                    |
| ------- | ------------------------------------------ |
| HTTP    | Primary web application.                   |
| SSH     | Potential post-exploitation access method. |

---

# Phase 2 — Web Enumeration

## robots.txt Analysis

Hidden application resources were discovered through robots.txt.

### Interesting Paths

```text
/status
/internal/
```

### Findings

* `/status` exposed an operational connectivity testing feature.
* `/internal/` did not immediately provide useful content during initial enumeration.

### Enumeration Goal

Determine whether internal functionality exposed unintended administrative features.

---

# Phase 3 — OS Command Injection

## Vulnerability Discovery

The network connectivity feature accepted attacker-controlled input.

### Testing Strategy

1. Verify normal functionality.
2. Test shell metacharacters.
3. Observe command execution behavior.

### Result

Application input reached a shell execution context.

### Security Impact

* Arbitrary command execution.
* Execution occurred under the web service account.
* Initial foothold established.

### CWE Reference

* **CWE-78 — OS Command Injection**

---

# Phase 4 — Reverse Shell

## Initial Access

Goal:

* Convert single-command execution into an interactive shell.

### Listener

```bash
nc -lvnp <PORT>
```

### Post Connection

Shell stabilization performed using:

* PTY spawning.
* Terminal environment configuration.
* Interactive Bash session.

### Outcome

* Stable Linux shell.
* Access obtained as the web application user.

---

# Phase 5 — Linux Enumeration

## User Context

Basic host enumeration performed.

### Useful Enumeration Commands

```bash
whoami
pwd
hostname
id
uname -a
ls -la
```

### Objective

* Determine privilege level.
* Locate user home directory.
* Identify accessible files.

---

## Network Enumeration

Enumerate listening services.

```bash
ss -lntp
```

### Interesting Local Services

| Port        | Service                       |
| ----------- | ----------------------------- |
| 3000        | Watchtower Operations Console |
| 8080        | FreePBX UCP                   |
| 9000        | Automation Service            |
| 3306        | Local Database                |
| 5038        | Telephony Service             |
| 8088 / 8089 | Additional Internal Services  |

### Key Observation

Services were bound to:

```text
127.0.0.1
```

Meaning they were inaccessible externally but reachable after compromise.

---

# Phase 6 — Watchtower Investigation

## Internal Dashboard

The localhost service exposed an operational monitoring interface.

### Enumeration

```bash
curl http://127.0.0.1:3000/
```

### API Discovery

Interesting endpoints included:

```text
/api/health
/api/config
```

---

## Health Endpoint

Purpose:

* Confirm service identity.
* Verify operational status.

Returned:

* Service name.
* Bind address.
* Status information.

---

## Configuration Endpoint

Important discovery phase.

### Information Revealed

* Internal automation endpoint.
* Internal telephony/UCP portal.
* Administrative notes.
* Challenge-specific authentication material.

### Security Observation

Internal configuration data should not be accessible without authorization.

---

# Phase 7 — SSH Local Port Forwarding

## Objective

Expose localhost-only services on the attacker workstation for easier browser interaction.

### Workflow

1. Generate SSH key.
2. Authorize key on compromised account.
3. Forward internal ports locally.

### Concept

```text
Local Browser
      │
SSH Tunnel
      │
127.0.0.1 Services on Target
```

### Benefits

* Native browser interaction.
* Easier application exploration.
* No need to rely exclusively on curl.

---

# Phase 8 — FreePBX UCP Investigation

## User Control Panel

Internal telephony portal became accessible through SSH forwarding.

### Areas Explored

* Dashboard.
* Widgets.
* Voicemail.
* User profile.

### Important Finding

Voicemail contained an operational artifact related to automation.

### Portfolio Note

Automation credential intentionally redacted.

---

# Phase 9 — Automation Artifact

## Voicemail Enumeration

Voicemail exposed an internal automation reference.

### Security Lesson

Operational communications can unintentionally expose privileged secrets.

### Potential Risks

* Credential exposure.
* Token exposure.
* API authentication leakage.

---

# Phase 10 — Automation API Enumeration

## Internal Automation Service

Target service listening locally.

### Endpoints Identified

```text
GET /health
POST /jobs/export
```

### Authentication

Bearer-style authentication required.

### Discovery Goal

Understand API functionality before testing input handling.

---

## Export Workflow Analysis

Observed behavior suggested the application generated shell commands to export reports.

### Security Observation

User-controlled report names appeared inside command construction logic.

### Attack Surface

Potential shell command construction vulnerability.

---

# Phase 11 — Authenticated Command Injection

## Validation Strategy

1. Authenticate to API.
2. Submit controlled input.
3. Observe execution behavior.

### Outcome

* Shell metacharacters interpreted.
* Input escaped intended context.
* Root-level command execution confirmed through controlled identity testing.

### CWE

**CWE-78 — OS Command Injection**

---

# Phase 12 — Privilege Escalation

## Root Context Verification

Objective:

Verify execution privilege before attempting a shell.

### Observation

Commands executed in the root security context.

### Final Outcome

* Root shell established.
* Administrative access confirmed.
* Root flag intentionally omitted.

---

# Security Findings Summary

| Finding                                           | Severity |
| ------------------------------------------------- | -------- |
| Command Injection in Status Endpoint              | High     |
| Internal Configuration Disclosure                 | Medium   |
| Exposed Internal Service Metadata                 | Medium   |
| Authenticated Command Injection in Automation API | Critical |
| Root Privileged Automation Worker                 | Critical |

---

# MITRE ATT&CK Mapping

| ATT&CK Technique | Description                                           |
| ---------------- | ----------------------------------------------------- |
| T1595            | Active Service Scanning                               |
| T1190            | Exploit Public-Facing Application                     |
| T1059            | Command and Script Interpreter                        |
| T1105            | Ingress Tool Transfer / Interactive Access            |
| T1021            | Remote Services (SSH Pivoting)                        |
| T1046            | Network Service Discovery                             |
| T1082            | System Information Discovery                          |
| T1574            | Hijacking Execution Flow (Command Construction Abuse) |
| T1068            | Exploitation for Privilege Escalation                 |

---

# Defensive Recommendations

## Web Application

* Never concatenate user input into shell commands.
* Use safe subprocess APIs with argument arrays.
* Validate and sanitize all input parameters.

## Internal Services

* Protect localhost services with authentication and authorization.
* Remove sensitive operational information from configuration endpoints.
* Avoid exposing credentials through internal dashboards or voicemail systems.

## Infrastructure

* Apply least privilege to automation workers.
* Rotate exposed secrets immediately.
* Restrict privileged services using network segmentation.

## Monitoring

Monitor for:

* Unexpected shell execution from Gunicorn/web processes.
* Abnormal child-process creation.
* Access to internal-only administrative APIs.
* Suspicious SSH port forwarding activity.

---

# Key Takeaways

* Small information disclosures can become major pivot points after initial compromise.
* Localhost services significantly expand the attack surface once shell access is obtained.
* Administrative APIs require the same security controls as public-facing APIs.
* Operational secrets stored in internal applications can enable privilege escalation.
* Enumeration should continue after every successful privilege or trust-boundary change.

---

# Portfolio Notes

**Status:** Completed

**Flags:** Redacted

**Credentials:** Redacted

**Automation Keys:** Redacted

**Environment:** Authorized TryHackMe laboratory

These notes accompany the full technical documentation (`Documentation/Documentation.md`) and GitHub Pages portfolio (`docs/index.md`) and are intended as a concise methodology reference for future CTFs and penetration testing engagements.
