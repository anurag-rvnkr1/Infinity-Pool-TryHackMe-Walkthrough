# Infinity Pool — Quick Notes

## Enumeration
```bash
nmap <TARGET_IP> -sV
```

Observed external services:
- TCP/22 — SSH
- TCP/80 — HTTP

## Web Discovery
```text
/robots.txt
/status
/internal/
```

`/status` exposed a connectivity-check workflow and accepted attacker-controlled input.

## Command Injection
A shell metacharacter was sufficient to break the intended single-command context and demonstrate additional command execution.

## Shell
A reverse connection was established to the testing workstation, followed by PTY/shell stabilization.

## Local Enumeration
```bash
ss -lntp
```

Interesting loopback listeners included:
```text
127.0.0.1:3000
127.0.0.1:9000
127.0.0.1:8080
127.0.0.1:8088
127.0.0.1:8089
127.0.0.1:3306
127.0.0.1:5038
```

## Watchtower
```bash
curl -s http://127.0.0.1:3000/
curl -i http://127.0.0.1:3000/api/health
curl -i http://127.0.0.1:3000/api/config
```

The configuration exposed:
- internal automation endpoint
- internal telephony/UCP endpoint
- service account information
- challenge-specific authentication material

## UCP Pivot
SSH local port forwarding was used to make loopback-only services reachable from the testing workstation.

The UCP/voicemail workflow exposed an **automation key**. The value is intentionally redacted from this repository.

## Automation API
The automation service exposed:
```text
GET  /health
POST /jobs/export
```

The job endpoint accepted an attacker-controlled report name and generated a shell command. An injection test demonstrated shell interpretation, and an identity check confirmed execution in the root context.

## Root
The final stage demonstrated root command execution. The root flag value is intentionally hidden.
