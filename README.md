
# 🔐 Web Penetration Testing Checklist

[![Status](https://img.shields.io/badge/Status-Living%20Document-blue)](https://github.com/)
[![Standard](https://img.shields.io/badge/Standard-OWASP%20Top%2010%3A2025-orange)](https://owasp.org/www-project-top-ten/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

## 📌 Overview
This repository contains a **methodology-first** Web Penetration Testing Checklist. It is designed for **educational purposes** and **authorized security assessments**. 

Unlike tool-centric lists, this checklist focuses on **Security Phases** and maps every action item directly to the **OWASP Top 10:2025** standards.

## ⚠️ Legal & Ethical Disclaimer
> **IMPORTANT:** This checklist is intended strictly for **educational use** and **authorized security testing**.
> * **Do not** scan targets without explicit, written permission from the asset owner.
> * **Do not** use active exploitation tools on public infrastructure without authorization.
> * Always follow the agreed-upon **Rules of Engagement (RoE)**.

---

## 🧭 Methodology Mapping

| OWASP ID | Category Name | Checklist Focus |
| :--- | :--- | :--- |
| **A01:2025** | Broken Access Control | Parameter handling, endpoint discovery, logic review |
| **A02:2025** | Security Misconfiguration | Server headers, default creds, open ports |
| **A03:2025** | Software Supply Chain Failures | CMS plugins, dependency checks, third-party libs |
| **A04:2025** | Cryptographic Failures | TLS/SSL, hardcoded secrets, weak hashing |
| **A05:2025** | Injection | SQLi, XSS, Command Injection, input fuzzing |
| **A06:2025** | Insecure Design | Business logic flow, architecture review |
| **A07:2025** | Authentication Failures | Session management, brute-force limits, token handling |
| **A08:2025** | Integrity Failures | CI/CD leaks, file integrity, unverified updates |
| **A09:2025** | Logging & Alerting Failures | Blind spot analysis, active detection testing |
| **A10:2025** | Exceptional Conditions | Error handling, buffer overflows, crash testing |

---

## 🔍 The Checklist

### 1️⃣ Phase 1: Reconnaissance (Passive & Active)
*Goal: Map the attack surface without touching application logic.*

| Check Type | Action Item | Tools / Techniques | OWASP ID |
| :--- | :--- | :--- | :--- |
| **Passive Recon** | Gather public data: **DNS**, **IPs**, **Tech Stack**, **Contacts**. | `Whois`, `Nslookup`, `Wappalyzer` | **A07**, **A02** |
| **Endpoint Discovery** | Identify all accessible **URLs**, **API endpoints**, and entry points. | `Burp Suite` (Target), `Wayback` | **A01**, **A06** |
| **Subdomain Enum** | Find hidden/forgotten subdomains (dev, stag, admin). | `Sublist3r`, `Amass`, `Assetfinder` | **A02**, **A08** |
| **Data Leakage** | Check for **exposed secrets**, **config files**, or **source code**. | **GHDB** (Google Dorks), `GitRob` | **A03**, **A04** |

### 2️⃣ Phase 2: Application & Code Analysis
*Goal: Understand how the application processes data.*

| Check Type | Action Item | Tools / Techniques | OWASP ID |
| :--- | :--- | :--- | :--- |
| **Parameter Analysis** | Identify data passing: **GET**, **POST**, **Headers**, **Cookies**, **JSON**. | `Burp Suite`, **Manual Inspection** | **A01**, **A05** |
| **Source Code Review** | (If Whitebox) Analyze **auth logic**, **validation**, and **crypto**. | **Manual Code Review**, `SonarQube` | **A06**, **A04** |
| **CMS Analysis** | Identify **CMS version**, installed **plugins**, and **themes**. | `WPScan`, `JoomScan` | **A03**, **A02** |
| **Dependency Check** | Check for known vulnerabilities in **libraries/components**. | `Retire.js`, `OWASP Dependency Check` | **A03** |

### 3️⃣ Phase 3: Vulnerability Identification
*Goal: Actively test for exploitable flaws in logic and input.*

| Check Type | Action Item | Tools / Techniques | OWASP ID |
| :--- | :--- | :--- | :--- |
| **Injection Testing** | Test inputs for **SQLi**, **XSS**, **Command Injection**. | **Manual Payloads**, `SQLMap` (Lite) | **A05** |
| **Code Injection** | Check if app interprets user input as code (e.g., `eval()`). | **Manual Payload Injection** | **A05**, **A06** |
| **Auth Testing** | Test **brute-force**, **credential stuffing**, **session fixation**. | `Hydra`, `Burp Sequencer` | **A07** |
| **Buffer Overflow** | (If applicable) Test for crashes/unexpected behavior. | **Fuzzing**, **Input Boundary Testing** | **A10** |

### 4️⃣ Phase 4: Configuration & Exposure Review
*Goal: Identify infrastructure-level weaknesses.*

| Check Type | Action Item | Tools / Techniques | OWASP ID |
| :--- | :--- | :--- | :--- |
| **Server Config** | Check for **default creds**, **debug pages**, **directory listing**. | `Nikto`, `Dirb`, **Manual** | **A02** |
| **Port Scanning** | Identify **open ports** and running **services**. | `Nmap`, `Zenmap` | **A02**, **A09** |
| **Security Headers** | Verify **HSTS**, **CSP**, **X-Frame-Options**. | **DevTools**, `securityheaders.com` | **A02**, **A04** |
| **TLS/SSL Check** | Check for **weak ciphers**, **expired certs**, outdated protocols. | `SSLLabs`, `testssl.sh` | **A04** |

### 5️⃣ Phase 5: Design & Logic Review
*Goal: Find flaws in business logic automated tools cannot detect.*

| Check Type | Action Item | Tools / Techniques | OWASP ID |
| :--- | :--- | :--- | :--- |
| **Auth Logic** | Analyze **Privilege Escalation** (Vertical/Horizontal) & **IDOR**. | **Manual Logic Review** | **A01** |
| **Session Logic** | Review **token expiration**, **Secure/HttpOnly flags**, **logout**. | **Cookie Editor**, `Burp` | **A07** |
| **Error Handling** | Ensure errors do not leak **stack traces** or **DB info**. | **Triggering 404/500 errors** | **A10** |
| **Trust Boundaries** | Verify where data enters and if sanitized *before* processing. | **Architecture Review** | **A06** |

---

## 📄 Phase 6: Reporting Guidelines

When documenting findings, ensure the following structure is used:

1.  **Vulnerability Name**
2.  **OWASP Category** (e.g., A01:2025 Broken Access Control)
3.  **Severity** (Critical / High / Medium / Low)
4.  **Proof of Concept (PoC)**: Screenshots, HTTP Requests/Responses.
5.  **Impact**: What is the business risk?
6.  **Remediation**: Specific technical steps to fix the issue.

---

## 🤝 Contributing
Contributions are welcome! Please submit a Pull Request (PR) to add new tools, refine methodology steps, or update OWASP mappings.
