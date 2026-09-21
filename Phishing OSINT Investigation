# Threat Intelligence Report: Phishing Infrastructure OSINT Investigation

## Executive Summary
This project documents an open-source intelligence (OSINT) and passive reconnaissance investigation conducted on an active credential-harvesting phishing campaign identified via PhishTank. The objective was to map the threat actor's digital footprint, uncover underlying infrastructure, and extract actionable Indicators of Compromise (IOCs) without directly interacting with live malware.

---

## Methodology & Tools Used
The investigation adhered to strict passive reconnaissance principles to ensure zero operational security (OPSEC) compromise:
* **Target Isolation:** Extracted and cleaned target root domains from threat intelligence feeds.
* **Subfinder:** Used for passive DNS enumeration and discovering hidden subdomains via certificate transparency logs.
* **theHarvester:** Scraped public data sources and search engines to gather host IPs and exposed email endpoints.
* **URLScan.io:** Analyzed hosting infrastructure, page rendering, TLS certificates, and HTTP redirect chains.

---

## Reconnaissance & Findings

### 1. Discovered Subdomains
Through passive enumeration and filtering, the following high-value subdomain associated with the credential harvesting infrastructure was identified:
* `aolmaillogin.sites.google.com` (Credential input portal)

### 2. Infrastructure & Hosting Analysis (URLScan.io)
Analysis of the target subdomain revealed the following infrastructure details:
* **Target IP Addresses:** `74.125.206.189`, `142.251.127.84`, `142.251.127.94`, `142.251.153.119`, `142.251.20.102`
* **Hosting Provider / ASN:** `15169 (GOOGLE - Google LLC)`
* **TLS/SSL Certificate Subjects:** `accounts.google.com`, `*.gstatic.com`, `*.google.com`

### 3. Observed Tactics (Living off the Land)
The threat actor abused legitimate cloud infrastructure to host the malicious campaign:
* **Domain Reputation Abuse:** A custom Google Sites subdomain (`aolmaillogin.sites.google.com`) was utilized to inherit Google's domain reputation and bypass basic security filters.
* **Redirect Chains:** The campaign abused legitimate `accounts.google.com` redirect chains (utilizing `continue` and `followup` parameters) to evade detection during transit.

---

## Indicators of Compromise (IOCs)

| Indicator Type | Value | Context / Role |
| :--- | :--- | :--- |
| **Subdomain** | `aolmaillogin.sites.google.com` | Primary Login Harvesting Portal |
| **IPv4 Address** | `74.125.206.189` | Hosting Server IP |
| **IPv4 Address** | `142.251.127.84` | Hosting Server IP |
| **IPv4 Address** | `142.251.127.94` | Hosting Server IP |
| **IPv4 Address** | `142.251.153.119` | Hosting Server IP |
| **IPv4 Address** | `142.251.20.102` | Hosting Server IP |
| **Artifact** | `Screenshot 2026-09-21 190459.png` | Evidence of redirect chain abusing `accounts.google.com` |
| **Artifact** | `Screenshot 2026-09-21 190409.png` | Evidence of AS15169 (Google LLC) hosting |

---

## Visual Artifacts
*(Insert Screenshot 2026-09-21 190459.png here - showing the URL Page History redirect chain)*

*(Insert Screenshot 2026-09-21 190409.png here - showing the IP and ASN information)*

---

## Remediation & Defense Recommendations
1. **URL Parameter Inspection:** Implement deeper inspection of URL parameters (like `continue=` and `followup=`) within trusted domains to detect malicious routing.
2. **Layered Defense:** Because network-level IP blocking of AS15169 is impossible without disrupting legitimate enterprise services, rely on endpoint detection and user awareness training for these types of "Living off the Land" attacks.
3. **Proactive Takedown:** Submit verified phishing infrastructure to the abused hosting provider (in this case, Google's Safe Browsing and Abuse reporting tools) to accelerate takedown.

---
