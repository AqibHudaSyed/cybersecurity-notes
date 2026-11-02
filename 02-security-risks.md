# 02 — Managing Security Risks

Notes on security domains, risk, frameworks, controls, audits, SIEM tools and incident response playbooks.

## Contents

1. [Security domains (CISSP)](#1-security-domains-cissp)
2. [Threats, risks and vulnerabilities](#2-threats-risks-and-vulnerabilities)
3. [Risk management and the NIST RMF](#3-risk-management-and-the-nist-rmf)
4. [Security frameworks and controls](#4-security-frameworks-and-controls)
5. [The CIA triad, authentication and authorization](#5-the-cia-triad-authentication-and-authorization)
6. [NIST Cybersecurity Framework (CSF)](#6-nist-cybersecurity-framework-csf)
7. [OWASP security principles](#7-owasp-security-principles)
8. [Security audits](#8-security-audits)
9. [Logs and SIEM tools](#9-logs-and-siem-tools)
10. [Playbooks and incident response](#10-playbooks-and-incident-response)
11. [One view: frameworks, controls and tools](#11-one-view-frameworks-controls-and-tools)
12. [Glossary](#12-glossary)

---

## 1. Security domains (CISSP)

The CISSP (Certified Information Systems Security Professional) certification groups security work into eight domains. Teams use them to organize daily work, spot gaps and build their security posture.

| # | Domain | Focus | Example |
|---|---|---|---|
| 1 | Security and risk management | Security goals, risk mitigation, compliance, business continuity, laws and ethics | Changing how personal data is handled to meet GDPR |
| 2 | Asset security | Protecting physical and digital assets across storage, maintenance, retention and destruction | Making sure old hard drives are destroyed properly |
| 3 | Security architecture and engineering | Designing tools, systems and processes that protect data | Using a SIEM to flag unusual logins |
| 4 | Communication and network security | Securing physical networks and wireless communication (on-site, remote, cloud) | Protecting remote staff on public Wi-Fi or insecure Bluetooth |
| 5 | Identity and access management (IAM) | Making sure users are trusted and only get the access they need | Avoiding a shared admin login, so every action can be traced |
| 6 | Security assessment and testing | Control testing, data analysis, audits, penetration testing | Auditing user permissions; adding MFA after a control test |
| 7 | Security operations | Investigations and preventive measures after an incident | Contain the attack → collect evidence → forensics (when, how, why) |
| 8 | Software development security | Security at every phase of the software development lifecycle | Secure design review, secure code review, penetration testing before release |

**The four components of IAM**

1. **Identification** — the user claims an identity (username, access card, fingerprint)
2. **Authentication** — the user proves it (password, PIN)
3. **Authorization** — access is granted based on the user's role
4. **Accountability** — user actions are logged and monitored

**Security design principles** (domain 3): threat modeling, least privilege, defense in depth, fail securely, separation of duties, keep it simple, zero trust, trust but verify.

- **Zero trust:** no user or device is trusted by default; every request is verified.
- **Trust but verify:** users are trusted, but their activity is checked regularly.

**Information security (InfoSec)** covers the processes used to protect information, such as incident response, vulnerability management, application security, cloud security and infrastructure security.

---

## 2. Threats, risks and vulnerabilities

| Term | Meaning | Example |
|---|---|---|
| **Asset** | Anything of value to an organization | Customer data, servers, intellectual property, office space |
| **Threat** | Any event or circumstance that can harm assets | Phishing, social engineering |
| **Vulnerability** | A weakness a threat can exploit | Outdated software, weak passwords, untrained staff |
| **Risk** | Anything that can affect the confidentiality, integrity or availability of an asset | No backups for critical data |

A risk exists only when **both a threat and a vulnerability** are present. In practice, risk is usually measured as **likelihood × impact**.

### Types of threats

- **Insider threat** — staff or vendors misuse their authorized access
- **Advanced persistent threat (APT)** — an attacker stays inside a system, undetected, for a long time
- **Ransomware** — data is encrypted and a payment is demanded for the decryption key; negotiations and leaked data often happen on the dark web

### Risk levels of assets

| Level | Description | Example |
|---|---|---|
| Low | Exposure causes no real harm | Public website content, published research |
| Medium | Not public; exposure causes some damage | Early leak of quarterly earnings |
| High | Protected by law; exposure causes serious damage | PII, sensitive PII, intellectual property |

### Factors that raise the likelihood of a risk

| Factor | Description |
|---|---|
| External risk | Attackers outside the organization |
| Internal risk | Current or former employees, vendors, trusted partners |
| Legacy systems | Old systems that are no longer updated |
| Multiparty risk | Vendors with access to sensitive data or IP |
| Software compliance/licensing | Unpatched or out-of-compliance software |

The **OWASP Top 10** lists the most critical web application risks. The 2021 edition added insecure design, software and data integrity failures, and server-side request forgery (SSRF).

### Well-known vulnerabilities

| Vulnerability | Affects | What it allows |
|---|---|---|
| ProxyLogon | Microsoft Exchange Server | Running code remotely without authenticating |
| ZeroLogon | Microsoft Netlogon (domain authentication) | Taking over a Windows domain controller |
| Log4Shell | Java Log4j library | Remote code execution on internet-facing systems |
| PetitPotam | Windows NTLM | Forcing a Windows machine on the LAN to authenticate to an attacker |
| Logging and monitoring failures | Any organization | Attacks go unnoticed |
| SSRF | Server-side applications | Tricking a server into reaching internal resources |

**Vulnerability management** means continuously finding and fixing weaknesses. A patch only helps once it is applied. Useful sources: the NIST National Vulnerability Database (NVD) and the CISA Known Exploited Vulnerabilities (KEV) catalog.

### The three layers of the web

| Layer | Access | Example |
|---|---|---|
| Surface web | Any web browser | Search engines, news sites |
| Deep web | Requires authorization | Company intranet, email inbox |
| Dark web | Requires special software | Criminal marketplaces, leaked data |

The deep web is not illegal; it is simply content behind a login.

### Impact of threats

- **Financial** — downtime, recovery costs, fines for non-compliance
- **Identity theft** — stolen PII sold on the dark web
- **Reputation** — customers leave, bad press, legal penalties

---

## 3. Risk management and the NIST RMF

### Risk management strategies

| Strategy | Meaning | Example |
|---|---|---|
| Acceptance | Accept the risk to keep the business running | A low risk that costs too much to fix |
| Avoidance | Remove the risk entirely | Not launching a risky feature |
| Transference | Hand the risk to a third party | Cyber insurance |
| Mitigation | Reduce the impact of a known risk | Patching, MFA, backups |

Risk management frameworks include the **NIST Risk Management Framework (RMF)** and **HITRUST** (healthcare).

### NIST RMF — seven steps

| Step | Meaning | Analyst example |
|---|---|---|
| 1. Prepare | Activities to manage risk before a breach | Monitor risks, identify useful controls |
| 2. Categorize | Build risk processes based on impact to confidentiality, integrity and availability | Assess how a risk affects critical data |
| 3. Select | Choose, customize and document controls | Keep a playbook up to date |
| 4. Implement | Put security and privacy plans in place | Tighten password rules after many resets |
| 5. Assess | Check that controls are implemented correctly | Find weaknesses in tools or procedures |
| 6. Authorize | Take accountability for remaining risk | Write reports, action plans and milestones |
| 7. Monitor | Stay aware of how systems are operating | Review daily operations |

---

## 4. Security frameworks and controls

- **Security framework** — guidelines for building plans that reduce risk to data and privacy (*what* to do)
- **Security control** — a safeguard that reduces a specific risk (*how* to do it)

Frameworks also cover physical security and staff training, since people are often the weakest link.

### Other frameworks

- **Cyber Threat Framework (CTF)** — created by the U.S. government to give a common language for describing and sharing cyber threat activity
- **ISO/IEC 27001** — an international standard for an information security management system (ISMS); it offers a set of controls to choose from and organizations can be certified against it

### Control categories

| Category | Description | Examples |
|---|---|---|
| Administrative / managerial | Policies and procedures for people | Least privilege, password policy, separation of duties, disaster recovery plan |
| Technical | Hardware and software | Firewall, IDS/IPS, antivirus, encryption, backups, MFA |
| Physical | Limits physical access | Locks, CCTV, badge readers, guards |

### Control types

| Type | Purpose | Examples |
|---|---|---|
| Preventive | Stop an incident before it happens | Firewall, locks, least privilege |
| Detective | Detect an incident in progress or after it | IDS, CCTV, fire alarm |
| Corrective | Restore assets after an incident | Backups, disaster recovery plan |
| Deterrent | Discourage attackers | Alarm signage, good lighting |

Used together, these controls create **defense in depth**.

| Control | Category | Type |
|---|---|---|
| Least privilege, password policy, access control policy, account management, separation of duties | Administrative | Preventive |
| Disaster recovery plan | Administrative | Corrective |
| Firewall, password manager | Technical | Preventive |
| IDS | Technical | Detective |
| IPS | Technical | Preventive (blocks traffic) |
| Encryption | Technical | Preventive (protects confidentiality) |
| Backups | Technical | Corrective |
| Antivirus | Technical | Detective and corrective |
| Locks, locking cabinets | Physical | Preventive / deterrent |
| CCTV | Physical | Preventive and detective |
| Lighting, alarm signage, time-controlled safe | Physical | Deterrent |
| Fire detection and suppression | Physical | Detective and preventive |

---

## 5. The CIA triad, authentication and authorization

| Element | Meaning | Example |
|---|---|---|
| Confidentiality | Only authorized users can access data (need to know) | A bank protects customers' financial data |
| Integrity | Data is correct, authentic and reliable | A bank freezes an account when spending suddenly changes |
| Availability | Authorized users can reach data when they need it | Customers can use online banking at any time, even during peak hours |

- **Encryption** turns readable **plaintext** into unreadable **ciphertext**; it is decrypted back with a key. It mainly protects confidentiality.
- **Hashing and digital signatures** verify integrity.
- **Authentication** verifies who someone is (password; MFA adds a second factor such as a code or biometrics).
- **Biometrics** are unique physical traits such as fingerprints, face, voice, eye or palm scans. Voice biometrics can be abused through vishing.
- **Authorization** decides what an authenticated user can access.

Authentication comes first (who are you?), authorization second (what can you do?).

---

## 6. NIST Cybersecurity Framework (CSF)

A voluntary framework of standards, guidelines and best practices for managing cybersecurity risk, used by organizations of all types worldwide. Version 2.0 has six functions, with **Govern** at the center, and puts more weight on supply chain risk.

| Function | Meaning | Analyst example |
|---|---|---|
| Govern | Set, oversee and improve strategy, policies, roles and risk processes | Follow leadership's security policies |
| Identify | Manage risk to people and assets | Monitor devices on the internal network |
| Protect | Policies, procedures, training and tools that reduce threats | Improve policies using past incidents |
| Detect | Find incidents and improve monitoring | Check that a new tool flags risk levels correctly |
| Respond | Contain, neutralize and analyze incidents, then improve | Document an incident and suggest fixes |
| Recover | Return systems to normal | Restore affected files and systems |

**Example:** an alert shows a compromised workstation (identify) → the unknown device is blocked (protect) → the machine is isolated and searched for further activity (detect) → the team investigates and finds a phone charged over USB (respond) → files and the system are restored (recover).

**NIST SP 800-53** is a catalog of controls for U.S. federal information systems, including private systems used by the government.

**CSF vs RMF:** the CSF lists *functions* (what a security program does); the RMF lists *steps* (the order for managing risk). "Detect" is a CSF function; "Monitor" is an RMF step.

---

## 7. OWASP security principles

OWASP (Open Worldwide Application Security Project) is a non-profit focused on software security.

| Principle | Meaning | Example |
|---|---|---|
| Minimize attack surface | Reduce the ways in | Disable unused features, restrict access |
| Least privilege | Only the access needed for the job | Analysts read logs but can't change permissions |
| Defense in depth | Several layers of controls | MFA + firewall + IDS |
| Separation of duties | No single person controls a critical process | The person who prepares paychecks doesn't sign them |
| Keep security simple | Avoid unnecessary complexity | Clear, simple access rules |
| Fix issues correctly | Find the root cause, fix it, test the fix | Weak Wi-Fi password → stronger password policy |
| Secure defaults | The default configuration is the most secure | MFA on by default |
| Fail securely | Failure leads to the safest state | A failed firewall blocks all traffic |
| Don't trust services | Verify third-party systems | Check a vendor's data before showing it to customers |
| Avoid security by obscurity | Security must not rely on secrecy alone | Hidden source code isn't enough |

- **Attack surface:** all the weaknesses an attacker could exploit
- **Attack vector:** the specific path used to get in (for example a phishing email or a weak password)

---

## 8. Security audits

A **security audit** reviews an organization's controls, policies and procedures against a set of expectations. Audits can be **internal** (run by a team that may include a compliance officer and security manager) or **external**.

- Internal criteria: the organization's own policies and best practices
- External criteria: laws, regulations and compliance standards

**Why audit:** identify organizational risk, assess controls, correct compliance issues and avoid fines.

**What shapes an audit:** industry, organization size, applicable regulations, location, and any compliance standard the business chooses to follow. Frameworks such as the NIST CSF and ISO 27000 make audits easier to prepare for.

**Questions to answer first:** What should the audit achieve? Which assets are most at risk? Are current controls enough? Which controls and regulations need to be added?

| Step | What happens |
|---|---|
| 1. Scope and goals | Define the people, assets, policies and technology in scope, and the security goals |
| 2. Risk assessment | Identify threats, risks and vulnerabilities to assets |
| 3. Controls assessment and compliance check | Check whether controls are effective and regulations are followed |
| 4. Mitigation plan | Plan how to reduce risk, cost and penalties |
| 5. Communicate results | Report risks, urgency, required compliance and recommendations to stakeholders |

In a controls assessment, each missing control is marked as needing implementation and given a priority (high = fix first).

---

## 9. Logs and SIEM tools

A **log** is a record of events in an organization's systems.

| Log source | Records |
|---|---|
| Firewall | Inbound and outbound internet connections |
| Network | Devices joining and leaving the network, and connections between them |
| Server | Activity on services such as websites, email and file shares (logins, username and password requests) |

A **SIEM** (security information and event management) tool collects and analyzes log data from many sources. It provides real-time visibility, event monitoring, automated alerts and central log storage. It must be tuned to each organization and updated as threats change.

**Dashboards** show security data as charts and tables. Example: 500 login attempts on one account in five minutes, from an unusual location and outside working hours. **Metrics** such as response time, availability and failure rate measure application performance.

### Types of SIEM tools

| Type | Managed by | Best when |
|---|---|---|
| Self-hosted | The organization, on its own servers | Physical control over sensitive data is required |
| Cloud-hosted | The vendor, accessed over the internet | No in-house infrastructure is wanted |
| Cloud-native | The vendor, built for the cloud | Scalability and flexibility matter |
| Hybrid | Mix of both | Cloud benefits plus control over sensitive data |

### Common tools

| Tool | Type |
|---|---|
| Splunk Enterprise | Self-hosted |
| Splunk Cloud | Cloud-hosted |
| Google Security Operations (formerly Chronicle) | Cloud-native |

**Splunk dashboards:** security posture (last 24 hours of notable events), executive summary (overall health for stakeholders), incident review (timeline of events before an incident), risk analysis (risk per user, device or IP).

**Google SecOps dashboards:** enterprise insights (recent alerts and suspicious domains with confidence and severity), data ingestion and health (are logs arriving correctly), IOC matches (top indicators of compromise over time), main (overall summary), rule detections (alerts per detection rule), user sign-in overview (unusual sign-in behavior).

**Where SIEM is heading:** cloud deployment, more data from IoT devices, AI/ML-assisted detection, and automation through **SOAR** (security orchestration, automation and response).

### Open-source vs proprietary tools

| | Open-source | Proprietary |
|---|---|---|
| Owner | Community | A company or person |
| Cost | Usually free | Paid |
| Source code | Public and modifiable | Only the owner can change it |
| Examples | Linux, Suricata | Splunk, Google SecOps |

Open-source tools are not less secure by default: public code means issues are found and fixed quickly. **Suricata** is an open-source network analysis and threat detection tool maintained by the Open Information Security Foundation (OISF).

---

## 10. Playbooks and incident response

A **playbook** is a manual with predefined, up-to-date steps for an operational task, including which tools to use. It makes sure everyone responds the same way. Playbooks (also called runbooks) are living documents, updated when:

- a gap or failure is found
- laws or industry standards change
- attacker tactics change

Types include incident response, security alert, team-specific and product-specific playbooks, plus playbooks for specific attacks (ransomware, vishing, business email compromise, DDoS).

**Incident response** is an organization's quick effort to identify an attack, contain the damage and correct its effects.

### Incident response playbook phases

| Phase | What happens |
|---|---|
| 1. Preparation | Document procedures, plan staffing, train users |
| 2. Detection and analysis | Detect events and decide whether a breach occurred and how big it is |
| 3. Containment | Limit further damage (for example, isolate an infected host) |
| 4. Eradication and recovery | Remove malicious artifacts and restore a secure environment |
| 5. Post-incident activity | Document, inform leadership, apply lessons learned |
| 6. Coordination | Report and share information throughout the process |

NIST's incident response guide (SP 800-61) used to show this in four phases: preparation; detection and analysis; containment, eradication and recovery; post-incident activity. The 2025 update drops these phases and links incident response to the six NIST CSF functions instead.

**Incident and vulnerability response playbooks** are based on the organization's business continuity plan. Following their steps keeps the response legal, timely and safe for forensic evidence.

### Responding to a SIEM alert (malware example)

1. **Assess** — confirm the alert is valid using logs and metrics
2. **Contain** — isolate the infected system
3. **Eradicate and restore** — remove the malware, rebuild the OS, restore data from a clean backup
4. **Post-incident** — write a report and notify stakeholders or authorities if required

### SIEM, SOAR and playbooks

| Tool | Role |
|---|---|
| SIEM | Detects suspicious activity and raises alerts |
| SOAR | Automates repetitive responses (for example, locking an account after many failed logins) |
| Playbook | Tells the analyst what to do next |

---

## 11. One view: frameworks, controls and tools

```
Security frameworks (what to do)
├── NIST RMF        → Prepare → Categorize → Select → Implement → Assess → Authorize → Monitor
├── HITRUST         → healthcare risk framework
├── CTF             → common language for threat activity
├── ISO/IEC 27001   → ISMS standard + set of controls
├── NIST CSF        → Govern (center) + Identify → Protect → Detect → Respond → Recover
├── NIST SP 800-53  → control catalog for U.S. federal systems
└── OWASP           → 10 software security principles

Security controls (how to do it)
├── Categories: Administrative · Technical · Physical
└── Types:      Preventive · Detective · Corrective · Deterrent

Risk strategies: Acceptance · Avoidance · Transference · Mitigation
CIA triad:       Confidentiality · Integrity · Availability

Security audit
├── Types: Internal · External
└── Steps: Scope and goals → Risk assessment → Controls and compliance → Mitigation plan → Communicate

Tools
├── Logs     → Firewall · Network · Server
├── SIEM     → Self-hosted · Cloud-hosted · Cloud-native · Hybrid
├── SOAR     → automated response
└── Playbook → Preparation → Detection and analysis → Containment →
               Eradication and recovery → Post-incident activity → Coordination
```

### Frameworks, regulations and standards

| Type | Meaning | Examples |
|---|---|---|
| Framework | Guidelines, usually voluntary | NIST CSF, NIST RMF, CTF, HITRUST |
| Regulation | Legally required | GDPR (EU personal data), HIPAA (U.S. health data) |
| Standard | Industry requirements for compliance | PCI DSS (card data), ISO 27001, SOC 1/SOC 2 reports |

SOC 1/SOC 2 means **System and Organization Controls** reports, not a Security Operations Center.

### Abbreviations

| Abbreviation | Full form |
|---|---|
| APT | Advanced Persistent Threat |
| CIA | Confidentiality, Integrity, Availability |
| CISSP | Certified Information Systems Security Professional |
| CSF | Cybersecurity Framework |
| CTF | Cyber Threat Framework |
| GDPR | General Data Protection Regulation |
| HIPAA | Health Insurance Portability and Accountability Act |
| HITRUST | Health Information Trust Alliance |
| IAM | Identity and Access Management |
| IDS / IPS | Intrusion Detection System / Intrusion Prevention System |
| IOC | Indicator of Compromise |
| ISMS | Information Security Management System |
| ISO / IEC | International Organization for Standardization / International Electrotechnical Commission |
| MFA | Multi-Factor Authentication |
| NIST | National Institute of Standards and Technology |
| OWASP | Open Worldwide Application Security Project |
| PCI DSS | Payment Card Industry Data Security Standard |
| RMF | Risk Management Framework |
| SIEM | Security Information and Event Management |
| SOAR | Security Orchestration, Automation, and Response |
| SOC | System and Organization Controls (reports) / Security Operations Center (team) |
| SP | Special Publication |
| SSRF | Server-Side Request Forgery |

---

## 12. Glossary

| Term | Definition |
|---|---|
| Asset | Anything that has value to an organization |
| Attack surface | All the weaknesses an attacker could use to get in |
| Attack vector | The path an attacker uses to get past defenses |
| Authentication | Verifying who someone is |
| Authorization | Granting access to specific resources |
| Availability | Authorized users can reach data when needed |
| Biometrics | Unique physical traits used to verify identity |
| Business continuity | Keeping operations running through disruption, using recovery plans |
| CIA triad | A model for thinking about risk in terms of confidentiality, integrity and availability |
| Confidentiality | Only authorized users can access data |
| Encryption | Converting readable data into an encoded form |
| External threat | A threat from outside the organization |
| Incident response | The quick effort to identify an attack, contain it and fix its effects |
| Integrity | Data is accurate, authentic and reliable |
| Internal threat | A current or former employee, vendor or partner who poses a risk |
| Log | A record of events in a system |
| Metrics | Measurements such as response time, availability and failure rate |
| NIST CSF | A voluntary framework for managing cybersecurity risk |
| NIST SP 800-53 | A control framework for U.S. federal information systems |
| Operating system | The interface between hardware and the user |
| OWASP | A non-profit focused on software security |
| Playbook | A manual with steps for an operational task |
| Ransomware | An attack that encrypts data and demands payment |
| Risk | Anything that can affect the confidentiality, integrity or availability of an asset |
| Risk mitigation | Having procedures ready to reduce a risk's impact quickly |
| Security audit | A review of controls, policies and procedures against expectations |
| Security controls | Safeguards that reduce specific risks |
| Security frameworks | Guidelines for building plans to reduce risk |
| Security posture | How well an organization defends its assets and adapts to change |
| Shared responsibility | Everyone in an organization helps reduce risk |
| SIEM | A tool that collects and analyzes logs to monitor activity |
| SOAR | Tools and workflows that automate responses to security events |
| Social engineering | Manipulating people to gain information or access |
| Threat | Any event that can harm assets |
| Vulnerability | A weakness that can be exploited |
