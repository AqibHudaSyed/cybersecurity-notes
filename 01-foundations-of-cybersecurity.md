# Cybersecurity Fundamentals – Study Notes

My personal notes on core cybersecurity concepts, written in simple English.

## Contents

1. [Core ideas](#1-core-ideas)
2. [Threats and the people behind them](#2-threats-and-the-people-behind-them)
3. [Common attacks](#3-common-attacks)
4. [Why people fall for social engineering](#4-why-people-fall-for-social-engineering)
5. [Security domains](#5-security-domains)
6. [Frameworks, controls and compliance](#6-frameworks-controls-and-compliance)
7. [Laws and regulations to know](#7-laws-and-regulations-to-know)
8. [Ethics and the "hack back" question](#8-ethics-and-the-hack-back-question)
9. [Tools a security analyst uses](#9-tools-a-security-analyst-uses)
10. [Handling digital evidence](#10-handling-digital-evidence)
11. [Things that are easy to mix up](#11-things-that-are-easy-to-mix-up)
12. [Quick reference](#12-quick-reference)

---

## 1. Core ideas

**Cybersecurity** is about keeping information safe so that the right people can use it, it stays accurate, and it is there when needed. It covers more than computers: networks, devices, data and people all need protecting.

### The CIA triad

| Letter | Idea | Question to ask | It breaks when... |
| --- | --- | --- | --- |
| C – Confidentiality | Only approved people can see the data | Who can see it? | Data leaks, passwords get stolen |
| I – Integrity | Data stays correct and untampered | Is it still accurate? | Records get changed without permission |
| A – Availability | Approved people can reach the data when they need it | Can we get to it? | A server crashes, a DDoS attack, ransomware |

Almost every security decision maps back to one of these three.

### Personal data

- **PII** – any detail that can point to a specific person: name, phone number, email, address.
- **Sensitive PII** – PII that causes serious harm if leaked, so it gets stricter handling: ID numbers (e.g. Aadhaar, SSN), card numbers, bank details, medical records.
- All sensitive PII is PII, but not the other way round.

### A few more terms

- **Asset** – anything an organization values: data, servers, laptops, even its reputation.
- **Security posture** – how ready an organization is to defend its important assets and adapt when things change.
- **Network security** – keeping the network infrastructure safe from people who should not be on it.
- **Cloud security** – making sure cloud resources are set up correctly and only the right people can reach them. Misconfiguration is one of the most common causes of cloud breaches.

### What a junior security analyst does

1. Watches systems and networks for anything suspicious
2. Sets up and maintains protective tools (firewalls, antivirus, updates)
3. Runs internal checks and audits to find weak spots

Useful skills come in two kinds: **transferable** ones (communication, teamwork, problem-solving) that carry over from any job, and **technical** ones (tools, scripting, SIEM, packet analysis) that are specific to the field.

### Why businesses invest in security

- Stops attacks from both outside and inside
- Keeps them on the right side of the law (and away from fines)
- Keeps systems running so work does not stop
- Saves money that a breach would cost
- Protects customer trust in the brand

---

## 2. Threats and the people behind them

- **Threat** – anything that could damage an asset. It can be an event (phishing email, power cut, fire), not just a person.
- **Threat actor** – the person or group creating the risk.
- **Insider** – someone with inside access: current staff, ex-staff, contractors, vendors, partners. Ex-employees and vendors count too.

### Types of threat actors

| Type | Who they are | What they usually want |
| --- | --- | --- |
| APT (advanced persistent threat) | Skilled, well-funded groups that study a target first and stay hidden for a long time | Disrupt critical infrastructure, steal trade secrets |
| Insider threat | People misusing access they legitimately have | Sabotage, spying, leaking or selling data |
| Hacktivist | Hackers driven by a political or social cause | Publicity, protest, propaganda |

### Hackers by permission

| Category | Also called | Behaviour |
| --- | --- | --- |
| Authorized | Ethical hackers | Test systems with permission and within the law |
| Semi-authorized | Researchers | Look for flaws but do not exploit them |
| Unauthorized | Unethical / malicious hackers | Break in without permission, often for money |

Others worth knowing: beginners using ready-made tools and scripts, hackers-for-hire who take any job, and self-appointed "vigilantes".

### Some attacks that shaped the field

| Year | Attack | Why it matters |
| --- | --- | --- |
| 1986 | Brain virus | Spread worldwide via floppy disks; showed malware can escape its creator's control |
| 1988 | Morris worm | Self-copying program that crashed thousands of machines; led to the first incident response teams (CERTs) |
| 2000 | ILOVEYOU / LoveLetter | Email that spread by mailing itself to contacts; a classic social engineering case |
| 2017 | Equifax breach | Data of roughly 143 million people exposed through an unpatched known flaw |

Lesson from all four: technology changes, but unpatched systems and human trust keep getting exploited.

---

## 3. Common attacks

### Phishing family

Phishing means tricking someone through a message (email, text, call) into handing over information or running something harmful.

| Variant | Channel | Target | Tell-tale sign |
| --- | --- | --- | --- |
| BEC (business email compromise) | Email | Company finances | Looks like a known contact asking for a payment or invoice change |
| Spear phishing | Email | One person or a small group | Personalised, looks like it is from someone trusted |
| Whaling | Email | Senior executives | Spear phishing aimed at "big fish" |
| Vishing | Phone / voice | Anyone | Caller pretends to be a bank, IT desk, etc. |
| Smishing | SMS / chat | Anyone | Text with a link or urgent request |

Memory hook: **V**ishing = **v**oice, **S**mishing = **S**MS, **Wh**aling = **wh**ale.

### Malware

Malicious software, usually aimed at money or intelligence.

| Type | How it spreads or works |
| --- | --- |
| Virus | Hides inside files; needs a person to open or run it |
| Worm | Copies itself across a network with no help from the user |
| Ransomware | Locks (encrypts) data and demands payment |
| Spyware | Quietly collects personal data (messages, location, recordings) |

### Social engineering in the real world

| Tactic | What happens |
| --- | --- |
| Social media recon | Attacker studies a victim's public profiles before striking |
| Watering hole | Attacker infects a website that a specific group visits regularly |
| USB baiting | Infected USB drives are left lying around for someone to plug in |
| Physical impersonation | Attacker poses as staff, a courier or a vendor to get into a building |

### Other attack categories

| Category | Examples |
| --- | --- |
| Password attacks | Brute force (trying many guesses), rainbow tables (pre-computed hash lookups) |
| Physical attacks | Malicious USB cables or drives, card skimming and cloning |
| Supply-chain attacks | Compromising a vendor's software or hardware to reach its customers |
| Cryptographic attacks | Birthday, collision and downgrade attacks on secure communication |
| Adversarial AI | Using or manipulating AI/ML to make attacks faster and harder to detect |

---

## 4. Why people fall for social engineering

Attackers exploit normal human instincts. Seven common levers:

| Lever | How it is used | Example line |
| --- | --- | --- |
| Authority | Pretend to be the boss or an official | "This is the director, I need this now." |
| Intimidation | Threats and pressure | "Do it or there will be consequences." |
| Social proof | "Everyone else already did it" | "Your teammates already gave me access." |
| Scarcity | Make something seem limited | "Only a few spots left." |
| Familiarity | Fake a quick personal connection | "Hey, remember me from college?" |
| Trust | Build a relationship slowly, then exploit it | Weeks of friendly chat before the ask |
| Urgency | Rush the victim so they do not think | "Reset within 10 minutes or lose access." |

Familiarity is a shortcut connection made quickly; trust is built over time.

---

## 5. Security domains

The (ISC)² CISSP body of knowledge groups security work into eight domains. A handy way to see where any task fits:

| # | Domain | Plain-English focus |
| --- | --- | --- |
| 1 | Security and risk management | Goals, risk, policies, legal and compliance |
| 2 | Asset security | Knowing, classifying, storing and disposing of assets and data |
| 3 | Security architecture and engineering | Designing systems and tools to be secure |
| 4 | Communication and network security | Securing networks, wired and wireless |
| 5 | Identity and access management | Right person, right access, nothing extra |
| 6 | Security assessment and testing | Testing controls, audits, scans |
| 7 | Security operations | Monitoring, investigations, incident response |
| 8 | Software development security | Building software securely |

Rough mapping of attacks to domains:
- Password, cryptographic and AI-driven attacks → communication and network security (AI also touches identity and access)
- Social engineering → security and risk management
- Physical attacks → asset security
- Supply-chain attacks → several domains at once

Why these mappings make sense:
- **AI → network + identity:** AI speeds up attacks over the network, and it can fake an identity (for example a deepfake voice) to get past logins and access checks.
- **Supply chain → many domains:** managing vendor risk, designing systems safely and spotting the attack all get affected together.

Memory hook: **on the wire = network, on a person = risk, in your hand = asset, AI = network + identity, vendor = everywhere.**

---

## 6. Frameworks, controls and compliance

Think of a hospital protecting patient records:

- **Framework** – the playbook for planning security (e.g. NIST CSF).
- **Controls** – the actual safeguards: logins, encryption, firewalls, training.
- **Compliance** – proving you follow internal rules and external laws (e.g. HIPAA).

### Why frameworks exist

Protect personal data, protect financial data, find weak spots, manage risk, and keep security aligned with what the business is trying to do.

### The four building blocks of a framework

1. Decide and document the security goals
2. Set guidelines to reach those goals
3. Put the security processes in place
4. Monitor the results and report them

Hospital version: goal – no patient record leaks; guideline – only treating doctors can open a record; process – role-based logins and encryption; monitoring – monthly access-log review reported to management.

Tip: the *reasons* for frameworks (protect PII, manage risk...) and the *building blocks* (goals, guidelines, processes, monitoring) are two separate lists. Do not mix them.

### NIST Cybersecurity Framework

A voluntary framework from the US National Institute of Standards and Technology, used worldwide. Its core functions:

1. **Identify** – know your assets and risks
2. **Protect** – put safeguards in place
3. **Detect** – spot incidents
4. **Respond** – contain and handle them
5. **Recover** – get back to normal

Version 2.0 (2024) adds a sixth function, **Govern**. NIST also publishes the Risk Management Framework (RMF).

### Governance vs architecture

- **Governance** – the direction from the top: policies, roles, decisions (e.g. mandatory yearly security training).
- **Architecture** – the technical design: how tools like firewalls, SIEM, IDS and backups fit together.

---

## 7. Laws and regulations to know

| Name | Applies to | Key point |
| --- | --- | --- |
| GDPR (EU) | Anyone handling EU residents' data | Breaches must be reported within 72 hours |
| HIPAA (US, 1996) | Health data (PHI) | Privacy, security and breach-notification rules; HITRUST helps with compliance |
| PCI DSS | Anyone handling payment card data | Aims to cut card fraud |
| FedRAMP (US) | Cloud services used by the US government | Standard security assessment for cloud providers |
| FERC-NERC | North American power grid operators | Must meet critical infrastructure protection (CIP) standards |
| CIS Controls | Any organization | Practical, prioritised defensive controls |
| ISO standards | International | Process and management standards across industries |
| SOC 1 / SOC 2 | Service organizations (AICPA audits) | Reports on controls, access policies and risk |

**Full forms:**

1. **FERC-NERC:** Federal Energy Regulatory Commission – North American Electric Reliability Corporation
2. **CIP:** Critical Infrastructure Protection
3. **FedRAMP:** Federal Risk and Authorization Management Program
4. **CIS:** Center for Internet Security
5. **GDPR:** General Data Protection Regulation
6. **EU:** European Union
7. **PCI DSS:** Payment Card Industry Data Security Standard
8. **HIPAA:** Health Insurance Portability and Accountability Act
9. **PHI:** Protected Health Information
10. **HITRUST:** Health Information Trust Alliance
11. **ISO:** International Organization for Standardization
12. **SOC:** System and Organization Controls
13. **AICPA:** American Institute of Certified Public Accountants

Also worth reading about: the Gramm-Leach-Bliley Act and the Sarbanes-Oxley Act.

**PHI** is any information about a person's physical or mental health, treatment or payment for care. A leak can lead to identity theft and insurance fraud.

---

## 8. Ethics and the "hack back" question

Security professionals see private data every day, so ethics matter: stay unbiased, keep data private, follow the law, be honest and rely on evidence.

### Can you attack the attacker?

| Where | Position |
| --- | --- |
| United States | No. Laws such as the Computer Fraud and Abuse Act (1986) and the Cybersecurity Information Sharing Act (2015) make it illegal for private parties; only authorised government or military personnel may. Private counterattacks are treated as vigilantism. |
| International guidance (ICJ – International Court of Justice) | Only under narrow conditions: it hits only the original attacker, it is a direct request to stop, it does not escalate, and its effects can be undone. |

In practice organizations do not hack back: it is legally risky, can escalate, and could even trigger an international incident if the attacker is state-backed. The Tallinn Manual covers this in depth.

### Guiding principles

1. **Confidentiality** – respect privacy; only authorised access.
2. **Privacy protection** – guard personal and sensitive data from misuse.
3. **Following the law** – be transparent, honest and evidence-driven, and keep learning.

Example: if patient data is exposed, telling the patients is both a legal and an ethical duty.

---

## 9. Tools a security analyst uses

| Tool | What it does | Example |
| --- | --- | --- |
| Logs | Record what happened in a system | "User X logged in at 10:05" |
| SIEM | Pulls logs from many systems into one place, analyses them and raises alerts | Splunk Enterprise, Splunk Cloud, Google SecOps (formerly Chronicle) |
| IDS (intrusion detection system) | Watches activity and alerts on possible intrusions (does not block) | Alert on repeated failed logins |
| Antivirus | Finds and removes malware | Quarantines an infected download |
| Packet sniffer / protocol analyser | Captures and inspects network traffic | tcpdump (CLI), Wireshark (GUI) |
| Playbook | Step-by-step checklist for a known situation | What to do when a phishing email is reported |

### Scripting and data

| Skill | What it is | Why it helps |
| --- | --- | --- |
| Python | General programming language | Automating repetitive checks and log analysis |
| SQL | Language for querying databases | Pulling records like "failed logins in the last 24 hours" |
| Linux | Open-source operating system | Most security tooling runs on it; the command line is essential |

A **database** is an organized store of data; a **data point** is a single piece of it (e.g. one login timestamp).

---

## 10. Handling digital evidence

Digital evidence is fragile. Handle it carelessly and it can be lost or become useless in court.

**Order of volatility** – collect the most short-lived data first:

1. CPU registers and cache
2. RAM (lost on shutdown)
3. Running processes and live network connections
4. Disk
5. Backups and archives

---

## 11. Things that are easy to mix up

| These two... | ...differ like this |
| --- | --- |
| Threat vs threat actor | Event vs the person/group behind it |
| PII vs sensitive PII | Sensitive PII is the subset with stricter handling |
| Virus vs worm | Virus needs a user to run it; worm spreads by itself |
| Spear phishing vs whaling | Whaling is spear phishing aimed at executives |
| Vishing vs smishing | Voice call vs SMS |
| Familiarity vs trust | Quick fake connection vs relationship built over time |
| Framework purposes vs building blocks | "Why" list vs "how" list |
| Governance vs architecture | Policies and direction vs technical design |
| IDS vs IPS | IDS alerts; IPS can block |
| Linux vs SQL | Operating system vs database query language |
| CIA scenario: site down / data altered / data leaked | Availability / Integrity / Confidentiality |

---

## 12. Quick reference

| Term | My one-line version |
| --- | --- |
| Adversarial AI | Using or tricking AI/ML to boost attacks |
| Antivirus | Detects and removes malware |
| Asset | Anything of value to the organization |
| BEC | Email fraud posing as a known contact to get money |
| CIA triad | Confidentiality, integrity, availability |
| Compliance | Meeting internal rules and external laws |
| Cryptographic attack | Attack on encrypted communication |
| Data point | One piece of data |
| Database | Organized collection of data |
| Hacktivist | Hacks for a political cause |
| IDS | Watches and alerts on intrusions |
| Insider threat | Someone with inside access who poses a risk |
| Log | Record of system events |
| Malware | Harmful software |
| NIST CSF | Voluntary framework for managing cyber risk |
| Order of volatility | Collect the most short-lived evidence first |
| OWASP | Non-profit focused on software and web app security |
| Packet sniffer | Captures and inspects network traffic |
| Phishing | Tricking people via messages |
| PHI | Health-related personal information |
| PII | Data that identifies a person |
| Security controls | Safeguards that reduce specific risks |
| Security frameworks | Structured guidance for planning security |
| Security governance | Top-down direction for security |
| Security architecture | How security tools and processes fit together |
| Security posture | Overall readiness to defend and adapt |
| SIEM | Central log collection, analysis and alerting |
| Social engineering | Manipulating people instead of systems |
| SQL | Language to query databases |
| Supply-chain attack | Reaching a target through its vendors |
| USB baiting | Dropping infected USB drives as bait |
| Watering hole | Infecting a site the target group visits |
