# Networks and Network Security

Notes on how networks are built, how data moves across them, how attackers abuse them, and how to harden networks, operating systems and the cloud.

## Table of contents

1. [Network basics](#1-network-basics)
2. [Network devices](#2-network-devices)
3. [Cloud networks](#3-cloud-networks)
4. [Data packets](#4-data-packets)
5. [The TCP/IP model](#5-the-tcpip-model)
6. [The OSI model](#6-the-osi-model)
7. [IP and MAC addresses](#7-ip-and-mac-addresses)
8. [Network protocols and ports](#8-network-protocols-and-ports)
9. [Wireless security](#9-wireless-security)
10. [Firewalls](#10-firewalls)
11. [VPNs](#11-vpns)
12. [Security zones and subnetting](#12-security-zones-and-subnetting)
13. [Proxy servers](#13-proxy-servers)
14. [Why network attacks matter](#14-why-network-attacks-matter)
15. [DoS and DDoS attacks](#15-dos-and-ddos-attacks)
16. [Reading packet captures](#16-reading-packet-captures)
17. [Packet sniffing](#17-packet-sniffing)
18. [IP spoofing attacks](#18-ip-spoofing-attacks)
19. [Security hardening](#19-security-hardening)
20. [OS hardening and brute force attacks](#20-os-hardening-and-brute-force-attacks)
21. [Network hardening](#21-network-hardening)
22. [Network security tools](#22-network-security-tools)
23. [Cloud hardening](#23-cloud-hardening)
24. [Quick comparisons](#24-quick-comparisons)
25. [Abbreviations](#25-abbreviations)

---

## 1. Network basics

- **Network:** a group of devices that are connected and can share data.
- **LAN (Local Area Network):** a network in a small area, like a home, school or office.
- **WAN (Wide Area Network):** a network across a large area, like a city or country. The internet is the biggest WAN.
- **Client-server model:** a client (laptop, phone) asks a server for a service, and the server provides it. Examples: DNS server, file server, mail server.
- **Network diagram:** a map of the devices on a network and how they connect. Security teams use it to plan how to protect the network.

## 2. Network devices

| Device | What it does |
|---|---|
| Hub | Sends every packet to every connected device. Easy to eavesdrop on, so it is rarely used today |
| Switch | Sends packets only to the right device. Keeps a MAC address table (MAC → port) |
| Router | Connects different networks and forwards packets using the destination IP address |
| Modem | Connects the home or office network to the internet service provider (ISP) |
| Wireless access point | Lets devices join the network over Wi-Fi |
| Firewall | Allows or blocks traffic based on rules |
| Server | Provides services to clients |

In most homes, the modem, router, switch and Wi-Fi access point are one single box.

## 3. Cloud networks

- **Cloud computing:** using servers, apps and network services over the internet instead of owning the hardware.
- **Cloud service provider (CSP):** a company that rents out cloud resources from its data centers.
- **Software-defined network (SDN):** routers, switches and firewalls built in software instead of physical hardware.

| Service model | What you get | Example |
|---|---|---|
| SaaS | Ready-to-use software | Email or office apps in the browser |
| PaaS | A platform to build and run your own apps | App hosting platforms |
| IaaS | Virtual servers, storage and networking | Cloud virtual machines |

| Environment | Meaning |
|---|---|
| On-premise | All network devices are in the company's own building |
| Hybrid cloud | On-premise devices plus cloud services (most companies) |
| Multi-cloud | More than one cloud provider |

**Why companies use the cloud:** reliability (services stay available), lower cost (no hardware to buy and patch), and scalability (pay only for what you use).

## 4. Data packets

A **data packet** is a small piece of data sent across a network. It works like a letter in an envelope.

| Part | Contains |
|---|---|
| Header | Source and destination IP and MAC addresses, protocol number |
| Body (payload) | The actual message |
| Footer | Marks the end of the packet and helps check for errors |

| Term | Meaning |
|---|---|
| Bandwidth | How much data the network can carry per second (capacity) |
| Speed | How fast data is actually moving (rate) |

Bandwidth = amount of data ÷ time in seconds. A sudden change in bandwidth or speed can be a sign of an attack.

## 5. The TCP/IP model

The TCP/IP model describes how data is organized and sent across a network in 4 layers.

| Layer | Job | Examples |
|---|---|---|
| 4. Application | Services the user works with | HTTP, HTTPS, DNS, SSH, SMTP, FTP |
| 3. Transport | Delivers data between systems, uses ports | TCP, UDP |
| 2. Internet | Adds IP addresses and routes packets | IP, ICMP |
| 1. Network access | Sends data over cables or Wi-Fi, uses MAC addresses | ARP, Ethernet, switches |

- **TCP:** builds a connection first, then sends data. Reliable. The connection is between two endpoints, even if the packets pass through many routers on the way.
- **UDP:** sends data without building a connection. Faster, but with no delivery guarantee. Used for DNS queries and real-time streaming.
- **Port:** a number that tells a device which service should receive the data (for example 80 for HTTP, 443 for HTTPS).

## 6. The OSI model

The OSI model splits network communication into 7 layers. It is a common language for finding where a problem or attack happens.

| # | OSI layer | What happens | TCP/IP layer |
|---|---|---|---|
| 7 | Application | Apps use the network (HTTP, DNS, SMTP) | Application |
| 6 | Presentation | Formatting, compression, encryption (TLS) | Application |
| 5 | Session | Opens, keeps and closes sessions; checkpoints | Application |
| 4 | Transport | TCP/UDP, splitting data into segments | Transport |
| 3 | Network | IP addresses and routing | Internet |
| 2 | Data link | Switches and network cards inside one network | Network access |
| 1 | Physical | Cables, signals, hubs, modems | Network access |

Router = layer 3. Switch = layer 2. Hub and cables = layer 1.

## 7. IP and MAC addresses

- **IP address:** the address of a device's network interface.
- **Public IP:** given by the ISP and unique on the internet. All devices in a home share one public IP.
- **Private IP:** used only inside the local network. Not unique on the internet.
- **MAC address:** a 48-bit hardware ID of a network card, like `00:1A:2B:3C:4D:5E`. It is meant to be fixed, but software can change (spoof) it.

| Point | IPv4 | IPv6 |
|---|---|---|
| Format | 4 numbers (0–255) with dots: `198.51.100.0` | 8 hex groups with colons: `2002:0db8::ff21:0023:1234` |
| Size | 4 bytes, about 4.3 billion addresses | 16 bytes, about 340 undecillion addresses |
| Header | More fields | Simpler, adds a Flow Label field |

`::` replaces a run of zero groups in an IPv6 address. IPv6 was created because IPv4 addresses were running out.

**Useful IPv4 header fields:**

| Field | Meaning |
|---|---|
| Source / destination IP | Who sent it and where it is going |
| TTL (Time to Live) | How many routers it can pass. At 0 the packet is dropped and an ICMP "Time Exceeded" message goes back |
| Protocol | What is inside (TCP, UDP, ICMP) |
| Identification, flags, fragment offset | Help rebuild a packet that was split into pieces |
| Total length | Size of the whole packet (max 65,535 bytes) |

The IPv4 header has 13 fields and is 20–60 bytes long. A TCP packet is often called an IP packet; a UDP packet is called a datagram.

## 8. Network protocols and ports

A **network protocol** is a set of rules for how devices exchange data.

| Category | Purpose | Examples |
|---|---|---|
| Communication | Exchange data | TCP, UDP, HTTP, DNS |
| Management | Monitor and troubleshoot | SNMP, ICMP |
| Security | Encrypt data in transit | HTTPS, SFTP, SSH |

| Protocol | Purpose | Port |
|---|---|---|
| HTTP | Web traffic, not encrypted | TCP 80 |
| HTTPS | Web traffic encrypted with TLS | TCP 443 |
| DNS | Domain name → IP address | UDP 53 (TCP 53 for large replies and zone transfers) |
| SSH | Secure remote shell | TCP 22 |
| SFTP | Secure file transfer over SSH | TCP 22 |
| FTP | File transfer, not encrypted | TCP 21 |
| Telnet | Remote login in plain text (unsafe) | TCP 23 |
| SMTP | Sending email | TCP 25 (encrypted: 587) |
| POP3 | Download email to one device | TCP 110 (encrypted: 995) |
| IMAP | Read email while it stays on the server | TCP 143 (encrypted: 993) |
| SNMP | Monitor and manage network devices | UDP 161/162 |
| DHCP | Give devices an IP, DNS server and default gateway | UDP 67 (server) / 68 (client) |
| ICMP | Error and status messages (ping) | No port |
| ARP | IP address → MAC address on the local network | No port |

- **NAT:** the router swaps private source IPs for its public IP on the way out, and swaps them back for replies.
- **Private IP ranges:** `10.0.0.0–10.255.255.255`, `172.16.0.0–172.31.255.255`, `192.168.0.0–192.168.255.255`.
- **ARP cache:** each device remembers IP–MAC pairs it has already looked up.
- Encryption hides the data, but not the source and destination IP addresses.
- DNS can be abused to send users to a fake site instead of the real one.
- A port number is not a protocol. Port 80 only tells you HTTP is probably in use.

## 9. Wireless security

Wi-Fi is based on the **IEEE 802.11** standards. **Bluetooth** is used for short-range connections to nearby devices.

| Protocol | Year | Key points |
|---|---|---|
| WEP | 1999 | Oldest. Encryption can be broken. High risk |
| WPA | 2003 | TKIP, bigger keys, message integrity check. Weak to KRACK attacks |
| WPA2 | 2004 | AES with CCMP. Common standard today. Still weak to KRACK |
| WPA3 | 2018 | Fixes KRACK with SAE handshake. 128-bit (192-bit optional in Enterprise) |

- **Personal mode:** one shared passphrase. Good for homes.
- **Enterprise mode:** individual access per user, managed centrally. Good for businesses.

## 10. Firewalls

A **firewall** checks traffic going in and out and allows or blocks it based on rules. **Port filtering** allows only the ports that are needed.

| Type | Notes |
|---|---|
| Hardware | Separate device at the edge of the network |
| Software | Runs on a computer or server. Cheaper, but uses that device's resources |
| Cloud-based | Hosted by a cloud provider, filters traffic before it reaches the company network |
| Stateless | Fixed rules, checks each packet on its own, needs rules in both directions |
| Stateful | Keeps a state table of connections, so return traffic for an open session is allowed |
| Next-generation (NGFW) | Stateful inspection plus deep packet inspection, intrusion prevention and app awareness |

Deep inspection of traffic for threats is the job of an NGFW. A stateful firewall mainly tracks connection state.

## 11. VPNs

A **VPN** creates an encrypted tunnel between a device and a VPN server, so data stays private on untrusted networks like public Wi-Fi.

- The encryption covers the path from your device to the VPN server. After that, traffic travels normally, so HTTPS is still needed.
- The VPN provider can see your traffic, so it must be trusted.
- **Encapsulation:** wrapping a packet inside another packet. VPNs use it to carry encrypted packets through the tunnel.

| Type | Connects |
|---|---|
| Remote access VPN | One user's device to the company network |
| Site-to-site VPN | Two office networks (harder to set up) |

| VPN protocol | Notes |
|---|---|
| WireGuard | Newer, fast, simple, open source. Works for both VPN types |
| IPSec | Older, more complex, widely tested and supported. Common in site-to-site VPNs |

**SD-WAN (software-defined WAN)** securely connects users in many locations to apps and is often used together with VPNs.

## 12. Security zones and subnetting

**Network segmentation** divides a network into parts, so a problem in one part does not spread to the rest.

| Zone | Meaning |
|---|---|
| Uncontrolled zone | Everything outside the organization (the internet) |
| Controlled zone | The protected inside network |
| DMZ | Public-facing servers (web, DNS, mail, proxy) between the internet and the internal network |
| Internal network | Private servers and employee data |
| Restricted zone | The most sensitive data, with the least access |

- **Subnetting:** splitting one network into smaller groups called subnets, using an IP address and a network mask.
- **CIDR:** writing a range as `198.51.100.0/24` (here, the first 24 bits are the network part, giving 256 addresses). CIDR replaced the old classful (Class A–E) system and made better use of IPv4 addresses.

## 13. Proxy servers

A **proxy server** sits between clients and other servers and forwards requests. It hides internal addresses and can filter traffic.

| Type | Controls |
|---|---|
| Forward proxy | Internal users going out to the internet |
| Reverse proxy | Internet users coming in to an internal server |
| Email proxy | Filters spam and phishing emails |

## 14. Why network attacks matter

Attackers may be driven by money, personal reasons, politics, anger at an employer or activism.

| Impact | Example |
|---|---|
| Financial | Downtime, recovery costs, ransom, lawsuits |
| Reputation | Customers stop trusting the company |
| Public safety | Attacks on power, water or defense systems |

- **Interception attacks:** capturing traffic to steal data or change it in transit (for example, changing the account number in a bank transfer).
- **Backdoor:** a hidden way around normal access controls. It may be left by developers for maintenance, or planted by an attacker to get back in later.

## 15. DoS and DDoS attacks

- **DoS:** flooding a network or server so real users cannot use it.
- **DDoS:** the same attack from many devices in many places, which makes it harder to stop.
- **Botnet:** a group of malware-infected computers controlled by one attacker. Botnets are often used for DDoS. One well-known case flooded a major DNS provider with tens of millions of requests, and many big websites became unreachable for hours.

**TCP three-way handshake:**

1. `SYN`: the client asks to connect.
2. `SYN, ACK`: the server agrees and reserves resources for the connection.
3. `ACK`: the client confirms and the connection opens.

| Attack | How it works |
|---|---|
| SYN flood | Sends many SYNs and never finishes the handshake. Half-open connections fill the server's queue, so real users get timeouts or `RST, ACK` |
| ICMP flood | Sends huge numbers of ping requests, using up bandwidth and resources |
| Ping of death | Sends one oversized ICMP packet (over 64 KB) that crashes the system. Modern systems are patched against it |

**ICMP** is used by devices to report errors and status (for example, `ping` or "port unreachable").

## 16. Reading packet captures

A **network protocol analyzer** (packet sniffer) captures traffic for investigation. Examples: tcpdump (command line) and Wireshark (graphical).

**tcpdump** is lightweight, uses the libpcap library, and comes with many Linux systems. By default it shows hostnames instead of IPs and service names instead of port numbers.

Example line:

```
13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
```

| Part | Meaning |
|---|---|
| `13:24:32.192571` | Time (24-hour clock) |
| `192.51.100.15.52444` | Source IP and source port |
| `203.0.113.2.domain` | Destination IP; `.domain` means port 53 (DNS), `.http` means port 80 |
| `35084+` | DNS query ID; `+` asks for a recursive lookup |
| `A?` | "What is the IPv4 address of this name?" |
| `(24)` | Size in bytes |

| TCP flag | Meaning |
|---|---|
| `[S]` / `SYN` | Start a connection |
| `[S.]` / `SYN, ACK` | Server accepts |
| `[.]` / `ACK` | Acknowledge |
| `[P.]` | Data being sent |
| `RST, ACK` | Connection reset or refused |

The client port changes for every new connection; this is normal. An `ICMP ... udp port 53 unreachable` message means nothing answered on the DNS port.

**Uses:** setting a traffic baseline, finding malicious traffic, creating alerts, finding unauthorized devices, and troubleshooting performance. Attackers can use the same tools to capture usernames and passwords.

## 17. Packet sniffing

| Type | What the attacker does |
|---|---|
| Passive | Reads traffic only (for example, from a hub) |
| Active | Changes packets while they travel |

A network card normally accepts only packets for its own MAC address. In **promiscuous mode** it accepts all traffic on the network, which attackers use to capture data.

**Protection:** use a VPN, use HTTPS sites, and avoid open public Wi-Fi.

## 18. IP spoofing attacks

**IP spoofing** means faking the source IP of a packet to look like a trusted system.

| Attack | What happens |
|---|---|
| On-path (meddler-in-the-middle) | The attacker sits between two trusted devices to read or change data, or fakes DNS replies to send users to a malicious IP |
| Replay | The attacker captures a packet and sends it again later or delays it |
| Smurf | The attacker sends ICMP pings to a network's broadcast address using the victim's IP, so every device replies to the victim and floods it |

**Protection:** encrypt data in transit (TLS), configure firewalls to reject spoofed or unauthorized packets, and use NGFWs that spot unusual broadcast traffic. Use several layers of defense (defense in depth).

## 19. Security hardening

**Security hardening** means reducing a system's vulnerabilities and attack surface (all the ways an attacker could get in).

Examples: install patches, keep a baseline configuration, remove unused software and services, close unused ports, dispose of old hardware safely, and limit access to what each person needs.

**Penetration testing:** an authorized, simulated attack to find weaknesses before real attackers do.

## 20. OS hardening and brute force attacks

The **operating system (OS)** sits between hardware and the user. One insecure OS can put the whole network at risk.

| Task | What it means |
|---|---|
| Patch updates | Fix known vulnerabilities as soon as patches come out, because attackers also learn where the weakness is |
| Baseline configuration | A documented "known good" setup to compare against and spot unauthorized changes |
| Hardware/software disposal | Wipe old devices and remove unused software |
| Strong password policy | Length, complexity, no default passwords, limits on failed logins |
| MFA | Two or more ways to prove identity |
| File permissions | Fix world-writable files that anyone can change |

**Brute force attacks:** guessing credentials by trial and error.

- **Simple brute force:** trying every combination.
- **Dictionary attack:** trying common or previously leaked passwords.

| Test environment | Notes |
|---|---|
| Virtual machine | Runs code in isolation and can be reset to a clean image. Small risk of malware escaping to the host |
| Sandbox | Separate test space for patches, suspicious files and attack simulations. Some malware detects sandboxes and hides |

| Defense | Why it helps |
|---|---|
| MFA / 2FA | A guessed password is not enough to log in |
| Login limits / lockout | Stops repeated guessing |
| Strong password policy | Makes guessing much harder |
| CAPTCHA | Blocks automated guessing scripts |
| Salting and hashing | Protects stored passwords if the database leaks |

Hashing is not encryption. It is one-way and cannot be reversed. It protects stored passwords; it does not stop live guessing.

## 21. Network hardening

| How often | Task |
|---|---|
| Regularly | Update firewall rules (also after every security event) |
| Regularly | Network log analysis with a SIEM |
| Regularly | Patch updates |
| Regularly | Server backups |
| Set up once, then maintain | Port filtering (allow only needed ports) |
| Set up once, then maintain | Network access privileges |
| Set up once, then maintain | Encryption with current standards; disable old wireless protocols |
| Set up once, then maintain | Network segmentation (for example, one subnet per department) |

The restricted zone should be kept separate and use the strongest encryption.

## 22. Network security tools

| Tool | Strength | Limit |
|---|---|---|
| Firewall | Allows or blocks traffic based on rules | A basic firewall looks only at packet headers. NGFWs can inspect the payload |
| IDS | Detects possible attacks and alerts the team | Does not stop traffic. Signature-based detection misses new attacks; anomaly-based detection helps |
| IPS | Detects and blocks attacks | Sits inline, so a failure can cut the connection (unless set to fail open). False positives can block real traffic |
| SIEM | Collects logs from many sources into one dashboard | Only reports. Needs a SOAR tool or an analyst to act |

**Placement:**

- Firewall at the network edge.
- IDS behind the firewall, watching a copy of the traffic. This cuts down noise from traffic the firewall already blocked.
- IPS behind the firewall, inline, so traffic passes through it.
- SIEM collects logs from firewalls, IDS, IPS, VPNs, proxies and DNS.

**Full packet capture devices** record all network traffic and help investigate alerts. Analysts in a **SOC (Security Operations Center)** watch the SIEM dashboard and decide when to escalate. More layers mean more security but also more cost, so the level is chosen based on risk.

## 23. Cloud hardening

| Concern | What to watch |
|---|---|
| IAM | Loose user roles give access to the wrong people |
| Configuration | Misconfigured services are a top cause of cloud breaches |
| Attack surface | Every new service adds risk |
| Zero-day attacks | Unknown flaws. Providers often patch them fast |
| Visibility | Use flow logs and packet mirroring for monitoring |
| Fast change | Provider updates can change security settings |

**Shared responsibility model:** the provider secures the infrastructure (data centers, hypervisors, host OS). The customer secures its own data, users and configuration.

| Practice / tool | Meaning |
|---|---|
| Server baseline image | Compare cloud servers against a known good image to spot unverified changes |
| Data separation | Keep apps apart by service type (old vs new apps, internal vs customer-facing) |
| Hypervisor | Software that runs VMs. Type 1 runs on hardware (used by cloud providers); Type 2 runs on a host OS |
| VM escape | A flaw that lets an attacker break out of a VM to the hypervisor or other VMs |
| Cryptographic erasure | Destroying all copies of the encryption key so the data can never be read |
| TPM | A chip that stores keys, passwords and certificates |
| Cloud HSM | A device that stores keys and performs encryption |

Modern encryption depends on keeping the **key** secret, not the algorithm. Customers can bring their own keys, but then they must protect them.

## 24. Quick comparisons

| Pair | First | Second |
|---|---|---|
| TCP vs UDP | Connection first, reliable | No connection, fast |
| Hub vs switch | Sends to all | Sends to the right device |
| Switch vs router | Inside a network (MAC) | Between networks (IP) |
| Bandwidth vs speed | Capacity | Actual rate |
| Stateless vs stateful | Fixed rules, no memory | Tracks connections |
| Forward vs reverse proxy | Users → internet | Internet → server |
| IDS vs IPS | Alerts only | Blocks |
| DoS vs DDoS | One source | Many sources |
| ICMP flood vs ping of death | Many normal pings | One oversized ping |
| Passive vs active sniffing | Reads | Changes |
| Hashing vs encryption | One-way | Reversible with a key |

## 25. Abbreviations

| Short | Full form |
|---|---|
| ARP | Address Resolution Protocol |
| CIDR | Classless Inter-Domain Routing |
| CSP | Cloud Service Provider |
| DDoS / DoS | (Distributed) Denial of Service |
| DHCP | Dynamic Host Configuration Protocol |
| DMZ | Demilitarized Zone |
| DNS | Domain Name System |
| FTP / SFTP | (Secure) File Transfer Protocol |
| HSM | Hardware Security Module |
| HTTP / HTTPS | Hypertext Transfer Protocol (Secure) |
| IaaS / PaaS / SaaS | Infrastructure / Platform / Software as a Service |
| IAM | Identity and Access Management |
| ICMP | Internet Control Message Protocol |
| IDS / IPS | Intrusion Detection / Prevention System |
| IMAP | Internet Message Access Protocol |
| IP | Internet Protocol |
| LAN / WAN | Local / Wide Area Network |
| MAC | Media Access Control |
| MFA / 2FA | Multi-Factor / Two-Factor Authentication |
| NAT | Network Address Translation |
| NGFW | Next-Generation Firewall |
| OS | Operating System |
| OSI | Open Systems Interconnection |
| POP3 | Post Office Protocol 3 |
| SD-WAN | Software-Defined Wide Area Network |
| SDN | Software-Defined Network |
| SIEM | Security Information and Event Management |
| SMTP | Simple Mail Transfer Protocol |
| SNMP | Simple Network Management Protocol |
| SOAR | Security Orchestration, Automation and Response |
| SOC | Security Operations Center |
| SSH | Secure Shell |
| TCP | Transmission Control Protocol |
| TLS | Transport Layer Security |
| TPM | Trusted Platform Module |
| TTL | Time to Live |
| UDP | User Datagram Protocol |
| VPN | Virtual Private Network |
| WEP | Wired Equivalent Privacy |
| WPA | Wi-Fi Protected Access |
