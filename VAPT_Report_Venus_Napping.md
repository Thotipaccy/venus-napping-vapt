## Vulnerability Assessment and Penetration Testing (VAPT) Report

### Engagement: X Company — Venus and Napping (VulnHub)
Date: 2025-08-09
Prepared by: Nibishaka thoti Pacifique

---

## Table of Contents 📚

- [1. Web Application Penetration Testing](#web-app-pt)
  - [1.1 Executive Summary 📝](#web-app-pt-1-1)
  - [1.2 Background 🧭](#web-app-pt-1-2)
  - [1.3 Objectives 🎯](#web-app-pt-1-3)
  - [1.4 Scope of Assessment 🗺️](#web-app-pt-1-4)
  - [1.5 Out of Scope 🚫](#web-app-pt-1-5)
  - [1.6 Tools Used 🧰](#web-app-pt-1-6)
- [Executive Summary 📄](#exec-summary)
- [Scope and Objectives 🎯](#scope-objectives)
  - [In-Scope Assets](#in-scope-assets)
  - [Objectives](#objectives-main)
  - [Constraints and Assumptions](#constraints-assumptions)
- [Target Overview 🔎](#target-overview)
- [Methodology 🔧](#methodology)
  - [Approach](#approach)
  - [Tools and Techniques](#tools-techniques)
- [Findings — Venus 🛡️](#findings-venus)
- [Findings — Napping 🛡️](#findings-napping)
- [Risk Prioritization ⚠️](#risk-prioritization)
- [Remediation Roadmap 🛠️](#remediation-roadmap)
- [Conclusion ✅](#conclusion)
- [Appendix A — Evidence Gallery 🖼️](#appendix-a)
- [Appendix B — Testing Log 🧪](#appendix-b)
- [Appendix C — References 📚](#appendix-c)

---

<a id="web-app-pt"></a>
## 1. Web Application Penetration Testing

<a id="web-app-pt-1-1"></a>
### 1.1 Executive Summary 📝

X Company engaged to conduct a black-box penetration test and vulnerability assessment. This report presents the results of a Vulnerability Assessment and Penetration Testing (VAPT) conducted on two virtual servers, *Venus* and *Napping*, hosted on VulnHub. The goal was to assess potential security weaknesses, simulate realistic attack scenarios, and propose targeted recommendations to strengthen system defenses. Multiple vulnerabilities were identified, ranging from misconfigurations and outdated software to privilege escalation paths. Key recommendations include patching, configuration hardening, and improved access controls.

<a id="web-app-pt-1-2"></a>
### 1.2 Background 🧭

This exercise aimed to perform penetration testing of the servers in scope to determine if they were vulnerable to attacks and exploitation. The test consisted of manual testing to detect and exploit vulnerabilities. The assessment was conducted to identify the security vulnerabilities in the servers in scope, assess their potential impact, and provide detailed recommendations for remediation.

<a id="web-app-pt-1-3"></a>
### 1.3 Objectives 🎯

**The objective of the tests performed was to:**

- Identify the possible vulnerabilities and gaps in the servers.
- Assess the gaps and vulnerabilities to determine the risk associated.
- Suggest recommendations to overcome existing vulnerabilities and gaps.

**This assessment report contains:**

- **Technical details** of the vulnerabilities discovered.
- **Risk mitigation recommendations** that need to be implemented to ensure that the systems are secure from the risks arising due to the discovered vulnerabilities.

<a id="web-app-pt-1-4"></a>
### 1.4 Scope of Assessment 🗺️

**The scope for this security assessment includes the following tests:**

- Information gathering
- Authentication

**URLs 🔗**

- http://192.168.1.101
- http://192.168.1.197

**Environment Details 🖥️**

| Item | Value |
| --- | --- |
| Server Names | Venus, Napping |
| Environment | Production |
| Accessibility | Local |
| Venus IP | 192.168.1.101 |
| Venus MAC address | 08:00:27:18:54:5E |
| Napping IP | 192.168.1.197 |
| Napping MAC address | 08:00:27:49:EE:4D |
| Authentication Method | Login & SSH |

<a id="web-app-pt-1-5"></a>
### 1.5 Out of Scope 🚫

**The following activities and applications were considered out of scope for this engagement:**

- Social engineering
- Denial of service
- Vulnerability fixes

<a id="web-app-pt-1-6"></a>
### 1.6 Tools Used 🧰

The following tools were used for the testing:

- Burp Suite
- Nmap
- Gobuster
- Kali Linux
- Mozilla Firefox extensions

---

<a id="exec-summary"></a>
### Executive Summary

This engagement assessed two VulnHub-hosted servers — Venus and Napping — representative of X Company's environment. The assessment combined vulnerability assessment and penetration testing techniques to identify weaknesses, demonstrate exploitability, and provide actionable remediation guidance.

Key results:
- Both hosts exhibited authentication weaknesses enabling unauthorized access to administrative or user areas.
- Post-compromise, privilege escalation paths were identified, aided by local enumeration (e.g., LinPEAS) and insecure configurations.
- Evidence indicates sensitive information handling weaknesses (e.g., trivial encoding such as ROT13) and exposed administrative interfaces.

Overall risk: High. Multiple chained findings allow an attacker to gain initial access and escalate privileges.

---

<a id="scope-objectives"></a>
## Scope and Objectives

<a id="in-scope-assets"></a>
### In-Scope Assets
- Venus: VulnHub target “The Planets: Venus”
- Napping: VulnHub target “Napping: 1.0.1”

<a id="objectives-main"></a>
### Objectives
- Identify vulnerabilities affecting confidentiality, integrity, and availability.
- Validate exploitability through controlled penetration testing.
- Provide remediation prioritized by risk.

<a id="constraints-assumptions"></a>
### Constraints and Assumptions
- Testing conducted within VulnHub lab boundaries against Venus and Napping only.
- Network-layer details (IP/MAC) are evidenced via screenshots; exact values should be taken from embedded artifacts.

---

<a id="target-overview"></a>
## Target Overview

The following screenshots document network discovery and target identification.

<img alt="IPs of Venus and Napping" src="images/ips of venus and napping (1).png" />

If required, MAC addresses and precise IPs should be read from the above evidence or the related recon screenshots.

Additional reconnaissance artifacts:

<img alt="Venus reconnaissance" src="images/reconaisse venus (2).png" />
<img alt="Venus monitoring" src="images/venus monitoring (3).png" />
<img alt="Other URLs identified" src="images/other urls(4).png" />

---

<a id="methodology"></a>
## Methodology

<a id="approach"></a>
### Approach
- Passive and active recon to enumerate services, technologies, and attack surface.
- Vulnerability assessment via configuration review and manual verification.
- Exploitation to validate impact while minimizing service disruption.
- Post-exploitation enumeration to assess privilege escalation and data exposure.

<a id="tools-techniques"></a>
### Tools and Techniques
- Network and service discovery (e.g., nmap, browser-based enumeration)
- Web attack tooling (e.g., Hydra/ffuf/gobuster, as applicable)
- Interception/proxy tooling (e.g., Burp Suite) for manual testing
- Local enumeration (e.g., LinPEAS)
- Manual analysis and custom scripts where appropriate

Evidence of tooling used:

<img alt="LinPEAS execution" src="images/LinPEAS(15).png" />

---

<a id="findings-venus"></a>
## Findings — Venus

### V1. Exposed Administrative Interface (Authentication Weakness) — High
**Description**: A web administrative interface (e.g., Django admin) was exposed and accessible. Weak credentials allowed successful brute-force login.
**Evidence**:
- <img alt="Django administration" src="images/django administration (5).png" />
- <img alt="Attempting brute force" src="images/accessing brute (6).png" />
- <img alt="Brute force evidence" src="images/venus brute(7).png" />
- <img alt="Successful login" src="images/successfully log in(12).png" />
**Impact**: Unauthorized administrative access; full application takeover possible.
**Likelihood**: High. Weak credentials allow remote exploitation.
**Remediation**:
- Enforce strong password policy and lockout/rate-limiting.
- Restrict admin interface by IP allowlisting/VPN/SSO.
- Enable multi-factor authentication (MFA) if supported.

### V2. Trivially Encoded Secrets (ROT13) — Medium
**Description**: Sensitive data or credentials observed protected only by ROT13 encoding.
**Evidence**:
- <img alt="ROT13 encoded data" src="images/rot13 encoded(8).png" />
**Impact**: Low barrier to disclosure; facilitates further compromise.
**Likelihood**: High once discovered.
**Remediation**:
- Replace encoding with proper cryptographic hashing or encryption as appropriate.
- Remove secrets from client-side or easily retrievable locations.

### V3. Local Privilege Escalation via Insecure Configuration — High
**Description**: Post-compromise enumeration revealed misconfigurations enabling privilege escalation (e.g., writable service, SUID binary, misconfigured cron, or vulnerable package).
**Evidence**:
- <img alt="Privilege escalation steps" src="images/privilege escalation(13).png" />
- <img alt="Local enumeration with LinPEAS" src="images/LinPEAS(15).png" />
**Impact**: Elevation from low-privilege user to higher privileges up to root.
**Likelihood**: Medium–High depending on environment hardening.
**Remediation**:
- Remove unnecessary SUID/SGID bits; harden file/dir permissions.
- Patch vulnerable packages; restrict cron jobs; enforce least privilege.
- Implement EDR and alerting on suspicious privilege escalation behavior.

### V4. Sensitive Functionality/Endpoint Exposure — Medium
**Description**: Additional application endpoints and URLs were identified that increase attack surface and may leak information or enable abuse.
**Evidence**:
- <img alt="Other URLs identified" src="images/other urls(4).png" />
- <img alt="Vulnerability view" src="images/venlability(16).png" />
**Impact**: Information disclosure and potential pivot to higher-impact exploits.
**Likelihood**: Medium.
**Remediation**:
- Disable or protect non-essential endpoints.
- Enforce authorization checks and minimize verbose error output.

Additional Venus evidence and context:

<img alt="Exploit execution on Venus" src="images/exploit to venus (17).png" />
<img alt="Venus target" src="images/venus (18).png" />
<img alt="Boom / impact evidence" src="images/boom (18).png" />
<img alt="Task accomplished on Venus" src="images/task accomplished venus(19).png" />
<img alt="User flag obtained" src="images/user flag (14).png" />

---

<a id="findings-napping"></a>
## Findings — Napping

### N1. Weak Authentication on Web Entry Point — High
**Description**: The Napping web application exposed a login or entry point that was susceptible to brute force or credential guessing, leading to account compromise.
**Evidence**:
- <img alt="Napping web" src="images/napping web (20).png" />
- <img alt="Napping entry point" src="images/napping entry point (21).png" />
- <img alt="Path enumeration" src="images/napping path (22).png" />
- <img alt="Password identified" src="images/napping pass (30).png" />
- <img alt="Brute attack on Napping" src="images/napping brute atack (24).png" />
- <img alt="Brute evidence" src="images/napping brute (25).png" />
- <img alt="Web Napping additional" src="images/web napping .png" />
- <img alt="Logged in evidence" src="images/logged in .png" />
**Impact**: Unauthorized access to application functionality and data.
**Likelihood**: High without rate-limiting and strong password policy.
**Remediation**:
- Enforce MFA, rate-limiting, lockout, and strong password controls.
- Monitor and alert on repeated failed logins.

### N2. Insufficient Hardening / Information Exposure — Medium
**Description**: Directory paths and additional context were discoverable, aiding attacker reconnaissance.
**Evidence**:
- <img alt="Napping path enumeration" src="images/napping path (22).png" />
**Impact**: Facilitates targeted attacks and identification of weak components.
**Likelihood**: Medium.
**Remediation**:
- Disable directory listings; minimize verbose errors; restrict debug modes.

Network identification evidence:

<img alt="IP of Napping" src="images/ip of nap (20).png" />
<img alt="IPs of both targets (reference)" src="images/ips of venus and napping (1).png" />

---

<a id="risk-prioritization"></a>
## Risk Prioritization

| ID  | Asset   | Title                                           | Severity |
|-----|---------|-------------------------------------------------|----------|
| V1  | Venus   | Exposed Admin + Weak Auth                       | High     |
| V2  | Venus   | Trivially Encoded Secrets (ROT13)               | Medium   |
| V3  | Venus   | Local Privilege Escalation                      | High     |
| V4  | Venus   | Sensitive Functionality Exposure                | Medium   |
| N1  | Napping | Weak Authentication on Web Entry Point          | High     |
| N2  | Napping | Insufficient Hardening / Information Exposure   | Medium   |

Severity mapping: Critical (CVSS ≥ 9), High (7.0–8.9), Medium (4.0–6.9), Low (0.1–3.9).

---

<a id="remediation-roadmap"></a>
## Remediation Roadmap

1. Immediate (Days 0–7)
   - Enforce MFA and strong password policies; implement account lockout and rate-limiting.
   - Restrict admin interfaces by network controls (VPN/allowlists) and SSO.
   - Remove trivially encoded secrets; rotate exposed credentials.

2. Short-Term (Weeks 2–4)
   - Patch and harden systems; remove unnecessary SUID/SGID bits and insecure services.
   - Disable directory indexing; review and secure all discovered endpoints.
   - Improve server-side input validation, error handling, and logging.

3. Medium-Term (1–2 Quarters)
   - Implement centralized logging/monitoring and alerting for auth anomalies and escalation attempts.
   - Conduct security code/config reviews and regular vulnerability scans.
   - Adopt least-privilege IAM and secrets management.

---

<a id="conclusion"></a>
## Conclusion

The assessment demonstrated viable attack paths from initial access to elevated privileges on both Venus and Napping. Addressing authentication controls, hardening hosts, removing insecure configurations, and improving monitoring will materially reduce risk. Incorporate the remediation roadmap into your security program and validate with a follow-up test.

---

<a id="appendix-a"></a>
## Appendix A — Evidence Gallery (All Screenshots)

<img alt="IPs of Venus and Napping" src="images/ips of venus and napping (1).png" />
<img alt="Recon Venus" src="images/reconaisse venus (2).png" />
<img alt="Venus monitoring" src="images/venus monitoring (3).png" />
<img alt="Other URLs" src="images/other urls(4).png" />
<img alt="Django Admin" src="images/django administration (5).png" />
<img alt="Accessing brute" src="images/accessing brute (6).png" />
<img alt="Venus brute" src="images/venus brute(7).png" />
<img alt="ROT13 encoded" src="images/rot13 encoded(8).png" />
<img alt="Guest brute" src="images/guest brute(10).png" />
<img alt="Magellanian" src="images/magellanian(11).png" />
<img alt="Successfully log in" src="images/successfully log in(12).png" />
<img alt="Privilege escalation" src="images/privilege escalation(13).png" />
<img alt="User flag" src="images/user flag (14).png" />
<img alt="LinPEAS" src="images/LinPEAS(15).png" />
<img alt="Vulnerability view" src="images/venlability(16).png" />
<img alt="Exploit to Venus" src="images/exploit to venus (17).png" />
<img alt="Venus" src="images/venus (18).png" />
<img alt="Boom" src="images/boom (18).png" />
<img alt="Task accomplished Venus" src="images/task accomplished venus(19).png" />
<img alt="Napping web" src="images/napping web (20).png" />
<img alt="IP of Napping" src="images/ip of nap (20).png" />
<img alt="Napping entry point" src="images/napping entry point (21).png" />
<img alt="Napping path" src="images/napping path (22).png" />
<img alt="Napping pass" src="images/napping pass (30).png" />
<img alt="Napping brute attack" src="images/napping brute atack (24).png" />
<img alt="Napping brute" src="images/napping brute (25).png" />
<img alt="Web napping" src="images/web napping .png" />
<img alt="Logged in" src="images/logged in .png" />

<img alt="Napping server start" src="images/napping server start (27).png" />
<img alt="Napping created files" src="images/napping created files (28).png" />
<img alt="Napping submit a IP link" src="images/napping submit a ip link (29).png" />
<img alt="Napping submit a random link" src="images/napping submit a random link (26).png" />
<img alt="Napping successful login via SSH" src="images/napping successful log in via ssh (31).png" />
<img alt="Napping privilege escalation" src="images/napping privelege escaltion (32).png" />

---

<a id="appendix-b"></a>
## Appendix B — Testing Log (High-Level)

- Reconnaissance and service enumeration across both targets.
- Web application mapping and discovery of admin/entry points.
- Brute-force testing under controlled limits; credential discovery.
- Post-auth exploration and collection of evidence.
- Local enumeration (LinPEAS) and privilege escalation validation.
- Flag capture and containment.

---

<a id="appendix-c"></a>
## Appendix C — References

- OWASP ASVS and Top 10 for authentication and session management.
- CIS Benchmarks for Linux host hardening.
- Vendor documentation for enabling MFA/SSO and admin interface protection.

