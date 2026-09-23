# Security Policy

> **Infinity Pool — TryHackMe Walkthrough**
>
> Responsible Use • Ethical Security Research • Portfolio Documentation

---

## 🛡️ Security Policy

Thank you for visiting the **Infinity Pool TryHackMe Walkthrough** repository.

This repository documents a penetration testing exercise completed in an **authorized TryHackMe training environment**. The purpose of this project is educational: to demonstrate cybersecurity methodology, vulnerability analysis, Linux post-exploitation techniques, and professional reporting practices.

This repository **does not** publish challenge answers, reusable credentials, or sensitive operational information.

---

## 🎯 Scope of This Repository

This project is intended for:

* Cybersecurity education.
* TryHackMe learning and portfolio development.
* Penetration testing documentation.
* Vulnerability reporting examples.
* Blue Team and Red Team learning.
* Security research conducted in authorized lab environments.

The documented techniques should only be used against systems where you have **explicit authorization** to perform security testing.

---

## ⚠️ Responsible Use

The walkthrough demonstrates offensive security techniques including:

* Service Enumeration
* Web Application Enumeration
* OS Command Injection
* Reverse Shell Access
* Linux Enumeration
* Localhost Service Pivoting
* REST API Enumeration
* SSH Local Port Forwarding
* Privilege Escalation

These techniques are presented **only for defensive understanding and authorized security testing**.

**Do not use these methods against systems, applications, APIs, or infrastructure that you do not own or do not have permission to test.**

---

## 🔒 Sensitive Information Handling

This public repository intentionally **redacts** challenge-sensitive information.

### Redacted Content

| Sensitive Item         | Status     |
| ---------------------- | ---------- |
| User Flag              | ✅ Redacted |
| Root Flag              | ✅ Redacted |
| Passwords              | ✅ Removed  |
| API Keys               | ✅ Removed  |
| Bearer Tokens          | ✅ Removed  |
| SSH Keys               | ✅ Removed  |
| Session Cookies        | ✅ Removed  |
| Authentication Secrets | ✅ Removed  |
| Challenge Answers      | ✅ Hidden   |

The screenshots included in this repository have also been reviewed to ensure sensitive values are obscured where appropriate.

---

## 📋 Supported Documentation Versions

| Repository Version                   | Supported         |
| ------------------------------------ | ----------------- |
| Latest `main` branch                 | ✅ Yes             |
| GitHub Pages documentation (`docs/`) | ✅ Yes             |
| Previous commits / archived forks    | ⚠️ Not maintained |

Please use the latest version of the repository when referencing documentation.

---

## 🚨 Reporting Security Issues

### What to Report

If you discover an issue in this repository itself, such as:

* Sensitive information accidentally committed.
* Credentials exposed in screenshots.
* API keys or tokens visible.
* Personally identifiable information (PII).
* Broken security guidance.
* Incorrect mitigation recommendations.

Please report it responsibly.

### What *Not* to Report

This repository documents vulnerabilities from a **TryHackMe lab**.

Do **not** report:

* Vulnerabilities intentionally present in the CTF.
* Challenge solutions.
* Flag locations.
* Exploitation paths that are part of the lab design.

Those are expected components of the learning environment.

---

## 🔍 Responsible Disclosure Guidelines

If sensitive information is identified:

1. Do **not** publicly share the secret.
2. Notify the repository maintainer privately.
3. Allow time for remediation before public discussion.

Example issues include:

* Accidentally committed secrets.
* Unredacted screenshots.
* Sensitive configuration files.

---

## 🧱 Security Best Practices Highlighted

This walkthrough discusses several security weaknesses and corresponding defensive practices.

### Vulnerabilities Covered

| Vulnerability                                   | CWE     |
| ----------------------------------------------- | ------- |
| OS Command Injection                            | CWE-78  |
| Sensitive Information Exposure                  | CWE-200 |
| Insufficient Credential Protection              | CWE-522 |
| Improper Access Control / Trust Boundary Issues | CWE-284 |

### Defensive Themes

* Input validation.
* Principle of least privilege.
* Secret management.
* Authentication for internal APIs.
* Secure subprocess execution.
* Monitoring privileged automation workers.

---

## 🛠️ Environment Safety

The assessment environment consisted of:

| Component     | Environment                      |
| ------------- | -------------------------------- |
| Platform      | TryHackMe                        |
| Target        | Disposable Linux training VM     |
| Network       | Isolated lab environment         |
| Authorization | Explicitly provided by TryHackMe |

No production infrastructure was accessed during this assessment.

---

## 🧩 Security Considerations for Readers

If you recreate this lab:

* Use a disposable virtual machine.
* Use isolated networking.
* Never reuse credentials from training environments.
* Rotate any secrets used during testing.
* Avoid exposing lab services to the public internet.

---

## 📚 Educational Disclaimer

This repository is an educational resource.

Its goals are to:

* Teach penetration testing methodology.
* Explain vulnerability impact.
* Demonstrate secure remediation practices.
* Showcase professional cybersecurity documentation.

It is **not** intended to facilitate unauthorized access or malicious activity.

---

## 🤝 Acknowledgements

Special thanks to:

* **TryHackMe** for providing hands-on cybersecurity training environments.
* The broader cybersecurity community for promoting responsible security research and disclosure practices.

---

## 📄 License & Security

This repository should be used in accordance with its license and GitHub's Community Guidelines.

Please respect:

* Responsible disclosure.
* Ethical hacking principles.
* TryHackMe Terms of Service.
* Applicable laws and organizational authorization requirements.

---

<div align="center">

### 🛡️ Hack Responsibly • Learn Continuously • Secure Everything

**Infinity Pool — Professional Cybersecurity Portfolio Project**

Made for education, documentation, and ethical security research.

</div>
