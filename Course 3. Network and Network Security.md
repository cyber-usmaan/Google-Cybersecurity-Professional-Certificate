![Course](https://img.shields.io/badge/Course%203-Connect%20And%20Protect:%20Network%20And%20Network%20Security-4285F4)
![Status](https://img.shields.io/badge/Status-Completed-4EEB2A)

#  Course 3. Connect and Protect: Networks and Network Security

## About This Course
This course helped me build a strong foundation in how networks are built, how data travels across them, and how attackers try to exploit them. Below is a breakdown of everything I learned, explained in my own words, with examples to show my understanding.

---

## Certificate

<p align="center">
  <img src="images/Google Cert 3 Connect and Protect Networks and Network Security.png" alt="Certificate placeholder" width="480"/>
</p>

---

## Modules Covered
There are 4 modules in this course:
- Network Architecture
- Network Operations
- Secure against network intrusions
- Security Hardening

---

## What I Learned

## 1. Network Basics: Devices and Diagrams

A network is simply the infrastructure that lets devices talk to each other. Before this course, I only thought of "the internet" as one thing. Now I understand it is made up of many specialized devices, each with its own job.

| Device | What it does | My understanding with an example |
|---|---|---|
| Router | Connects different networks and directs traffic based on IP address | Think of it as a mail sorting office. It reads the destination address and forwards the package to the right network. |
| Switch | Connects devices within one local network using MAC addresses | It keeps a MAC address table, like a seating chart, so it knows exactly which port to send data to. |
| Hub | Connects devices but repeats data to every port | This is like shouting a message to a whole room instead of whispering it to one person. Insecure because everyone hears everything. |
| Firewall | Monitors and filters incoming and outgoing traffic | The first line of defense, like a security guard checking IDs before letting anyone in. |
| Modem | Converts ISP signals into a format the local network understands | The translator between the outside internet world and my home network. |
| Wireless Access Point (WAP) | Sends and receives Wi Fi signals | Lets devices join the network without a physical cable. |
| Server | Provides services or data to client devices | Example: a DNS server resolves a website name to an IP address whenever I type a URL. |

**Client server model**: Clients (my laptop, my phone) send requests, and the server responds. A file server storing shared documents for an office is a clear example.

**Network diagrams**: These are visual maps showing how devices connect using icons and dotted lines. As a security analyst, reading these diagrams helps me quickly understand where the weak points of a network might be, similar to how a floor plan helps identify entry and exit points of a building.

[Insert image: Basic home network diagram with modem, router, switch, and firewall]

---

## 2. Cloud Computing and Software Defined Networks

I learned that networks are not only physical anymore. Cloud computing means using remote servers hosted by a Cloud Service Provider (CSP) instead of owning physical hardware.

### Cloud Service Models

| Model | Full Form | What it means | Example |
|---|---|---|---|
| SaaS | Software as a Service | Ready to use software hosted by the CSP | Gmail, Google Docs |
| IaaS | Infrastructure as a Service | Virtual servers and storage that I configure myself | Amazon EC2 |
| PaaS | Platform as a Service | A platform to build and deploy custom applications | Google App Engine |

### Hybrid and Multi Cloud
A hybrid cloud is when an organization mixes its own on premise infrastructure with cloud services. A multi cloud setup means using more than one CSP at the same time.

### Software Defined Networks (SDN)
Instead of physical routers and switches, SDNs use virtual versions of these devices hosted at the CSP's data center. This means network configuration can be changed through software rather than physically rewiring equipment.

### Why Businesses Choose Cloud
1. **Reliability**: Services stay available with minimal downtime.
2. **Cost**: No huge upfront investment in hardware.
3. **Scalability**: Resources can grow or shrink based on demand, so a company only pays for what it uses.

I now understand why almost every modern company relies on some form of cloud infrastructure. It removes the burden of buying and maintaining physical equipment.

---

## 3. The TCP/IP Model

This was one of the most important concepts in the course. The TCP/IP model explains how data is organized and transmitted across a network in four layers.

| Layer | Purpose | Common Protocols |
|---|---|---|
| Application Layer | User facing requests and responses | HTTP, DNS, SMTP, SSH, FTP |
| Transport Layer | Delivers data between systems, controls flow | TCP, UDP |
| Internet Layer | Delivers data to the correct destination network | IP, ICMP |
| Network Access Layer | Deals with physical transmission of data packets | ARP, Ethernet, hubs, cables |

My way of remembering this: the application layer is what I see (a browser), the transport layer decides how reliably data moves (TCP is careful, UDP is fast), the internet layer figures out the destination address, and the network access layer is the actual wire or radio signal carrying the bits.

### TCP vs UDP
- **TCP**: Connection based. Uses a three way handshake (SYN, SYN/ACK, ACK) before sending data. Reliable, used for things like loading a webpage where every piece of data matters.
- **UDP**: Connectionless. No handshake, so it is faster but less reliable. Used for video streaming or DNS lookups where speed matters more than perfect delivery.

[Insert image: TCP three way handshake diagram]

---

## 4. The OSI Model

The OSI model is the more detailed, seven layer version of the same idea as TCP/IP. I learned to work through it from Layer 7 down to Layer 1.

| Layer | Name | Function | Example |
|---|---|---|---|
| 7 | Application | User facing services | Browser using HTTP |
| 6 | Presentation | Data translation and encryption | SSL encrypting data for HTTPS |
| 5 | Session | Opens, manages, and closes sessions | Keeping a login session alive |
| 4 | Transport | Segments data, controls delivery | TCP, UDP |
| 3 | Network | Routes packets between networks | IP addressing |
| 2 | Data Link | Handles delivery within one network | Switches, MAC addresses |
| 1 | Physical | The actual hardware and signals | Cables, radio waves |

**TCP/IP vs OSI**: The TCP/IP model condenses the OSI model's seven layers into four. Application, presentation, and session (Layers 7, 6, 5) combine into one application layer in TCP/IP. Both models are just two different ways to describe the same journey of data across a network. I found it useful to think of OSI as the "textbook" version and TCP/IP as the "practical" version used more often in the industry.

[Insert image: OSI model vs TCP/IP model side by side comparison]

---

## 5. Network Layer and IP Addressing

### The IPv4 Packet
An IPv4 packet has two parts: a header (20 to 60 bytes) and the data being carried. The header contains important fields such as:

| Field | Purpose |
|---|---|
| Version | Identifies the IP version, for example IPv4 |
| Header Length (HLEN) | Marks where the header ends and data begins |
| Total Length | Total size of the packet |
| Identification | Helps reassemble fragmented packets |
| Time to Live (TTL) | Limits how many routers a packet can pass through before being discarded |
| Protocol | Tells the receiving device which protocol handles the data |
| Header Checksum | Detects corruption in transit |
| Source and Destination IP | The sender and receiver addresses |

The **TTL** field genuinely surprised me. I did not realize packets have a built in expiry counter to prevent them from looping forever if something goes wrong with routing.

### IPv4 vs IPv6

| Aspect | IPv4 | IPv6 |
|---|---|---|
| Format | Decimal, dot separated (198.51.100.0) | Hexadecimal, colon separated (2002:0db8::ff21:0023:1234) |
| Size | 4 bytes | 16 bytes |
| Total Addresses | About 4.3 billion | 340 undecillion |
| Reason for creation | Original standard | Created to solve IPv4 address exhaustion |

The main takeaway is that the internet outgrew IPv4's limited address space, so IPv6 was designed to future proof the internet with a nearly unlimited pool of addresses.

---

## 6. Common Network Protocols

Protocols are like an agreed language that all devices use to talk to each other. I learned they fall into three categories.

### Categories of Protocols

| Category | Purpose | Examples |
|---|---|---|
| Communication | Governs how data moves between devices | TCP, UDP, HTTP, DNS |
| Management | Monitors and troubleshoots the network | SNMP, ICMP |
| Security | Encrypts data in transit | HTTPS, SFTP, IPSec, SSL/TLS |

### Address and Configuration Protocols

- **NAT (Network Address Translation)**: Converts private IP addresses on my home network into a single public IP address so devices can talk to the internet. This is also a small security benefit since internal devices are hidden from the outside.
- **DHCP (Dynamic Host Configuration Protocol)**: Automatically assigns IP addresses to devices when they join a network, so I don't have to set one manually every time.
- **ARP (Address Resolution Protocol)**: Matches an IP address to a MAC address on the local network. I now understand why this exists: IP addresses can change, but the MAC address of a network card stays fixed, so ARP is the bridge between the two.

### Remote Access and Email Protocols with Ports

| Protocol | Port | Purpose |
|---|---|---|
| Telnet | TCP 23 | Remote access, sends everything in plain text (insecure) |
| SSH | TCP 22 | Secure replacement for Telnet, encrypted remote access |
| POP3 | TCP/UDP 110 (995 encrypted) | Downloads email to a single device |
| IMAP | TCP 143 (993 encrypted) | Keeps email on the server so it syncs across devices |
| SMTP | TCP/UDP 25 (587 encrypted) | Sends and routes outgoing email |

A simple way I remember the email protocols: POP3 downloads and often removes mail from the server (like taking a letter out of a mailbox), while IMAP leaves a copy on the server so I can check the same inbox from my phone and my laptop.

[Insert image: Table showing common protocols and their ports]

---

## 7. Evolution of Wireless Security Protocols

Wi-Fi security did not appear overnight. It evolved as older protocols were broken by attackers.

| Protocol | Year | Key Improvement | Known Weakness |
|---|---|---|---|
| WEP | 1999 | First attempt at wireless privacy | Easily broken, considered high risk today |
| WPA | 2003 | Introduced TKIP and larger keys | Vulnerable to KRACK attack |
| WPA2 | 2004 | Uses AES encryption and CCMP | Still vulnerable to KRACK |
| WPA3 | 2018 | Uses SAE to fix the KRACK weakness, stronger encryption | Newer, still growing in adoption |

**Personal vs Enterprise mode**: Personal mode uses one shared passphrase for the whole network, which is simple and works well at home. Enterprise mode gives each user individual credentials, which is harder to set up but much better for businesses because access can be granted or revoked per user without changing a shared password for everyone.

---

## 8. Subnetting and CIDR

Subnetting is the process of dividing one large network into smaller, organized sections called subnets. I like to picture it as a big city (the whole network) being divided into neighborhoods (subnets). Each neighborhood can be managed and secured on its own, and traffic within a neighborhood does not need to leave it just to reach a next door device.

**CIDR (Classless Inter Domain Routing)** is the notation used to define subnets. An address like 198.51.100.0/24 tells me the prefix length, which decides how many addresses fall inside that subnet. CIDR replaced the older, more rigid classful addressing system from the 1980s that was running out of room as the internet grew.

**Security benefit**: Subnetting lets an organization isolate parts of its network. If one subnet is compromised, the rest of the network can be shielded from it using firewalls and routing rules.

---

## 9. Network Security Tools and Devices

### Firewalls

| Type | How it works |
|---|---|
| Stateless | Filters based on fixed rules only, does not remember previous traffic |
| Stateful | Tracks ongoing connections using a state table, only needs a rule in one direction |
| Next Generation Firewall (NGFW) | Adds deep packet inspection and can filter based on the actual application, not just port and IP |

### Proxy Servers
A proxy server sits between clients and the internet. A **forward proxy** handles requests from internal users going out, while a **reverse proxy** handles requests coming in from external users to an internal service. I found this useful because it hides the real server from direct exposure, adding a layer of protection.

### VPNs (Virtual Private Networks)
A VPN encrypts my data and hides my IP address by wrapping my traffic inside another encrypted packet, a process called encapsulation.

| VPN Protocol | Strengths |
|---|---|
| WireGuard | Newer, faster, simpler to set up, open source, good for streaming or large downloads |
| IPSec | Older, more widely supported, extensively tested, commonly used for site to site VPNs |

**Remote access VPN** connects one personal device to a VPN server, while a **site to site VPN** connects two entire networks together, often used by companies with multiple office locations.

### IDS, IPS, and SIEM

| Tool | What it does | Limitation |
|---|---|---|
| Intrusion Detection System (IDS) | Detects and alerts on suspicious activity | Cannot stop the traffic itself, only alerts |
| Intrusion Prevention System (IPS) | Detects and actively blocks malicious activity | If it fails, the connection may break entirely, and it can cause false positives |
| SIEM | Collects and analyzes logs from firewalls, IDS, IPS, VPNs, and more in one dashboard | Does not take action, only reports |

I now understand the concept of **defense in depth**: no single tool is perfect on its own, so security professionals layer a firewall, an IDS or IPS, and a SIEM together to build stronger protection.

[Insert image: Example SIEM dashboard showing aggregated security events]

---

## 10. Threats, Attacks, and Investigation Tools

### Interception Attacks

- **Packet Sniffing**: Capturing data as it travels across a network, often using tools like Wireshark. A network card set to promiscuous mode can capture all traffic, not just what is addressed to it.
- **IP Spoofing**: An attacker fakes their IP or MAC address to pretend to be a trusted device.
- **On Path Attack**: An attacker secretly sits between two devices that trust each other and intercepts their communication. Also called a meddler in the middle attack. Encrypting traffic with TLS is the best defense.
- **Smurf Attack**: Combines IP spoofing with an ICMP flood sent to a broadcast address, overwhelming every device on the network at once.
- **DoS Attack**: Floods a system with traffic until it can no longer respond to legitimate requests. Unlike spoofing, the attacker uses real, authorized looking packets in massive volume.

### Backdoor Attacks
A backdoor is a hidden way into a system that bypasses normal authentication. Sometimes these are left in intentionally by developers for troubleshooting, but attackers can also plant their own backdoor after breaking in, to maintain long term access.

### Brute Force Attacks
Attackers try to guess login credentials through repeated attempts.

- **Simple brute force**: Trying random combinations of usernames and passwords.
- **Dictionary attack**: Using a list of common passwords or previously leaked credentials.

### Prevention Measures I Learned

| Technique | How it helps |
|---|---|
| Salting and Hashing | Converts passwords into unreadable values, salting adds randomness so identical passwords do not produce identical hashes |
| MFA / 2FA | Requires more than one proof of identity, such as a password plus a one time code |
| CAPTCHA / reCAPTCHA | Confirms a real human is logging in, blocking automated brute force tools |
| Password Policies | Enforces complexity, expiration, and login attempt limits |

### Testing Environments for Vulnerabilities
- **Virtual Machines (VMs)**: Software based computers that isolate testing from the main system. Useful for examining suspicious files safely and can be reset to a clean state.
- **Sandboxes**: A separate environment used to test patches or run suspicious code without risking the real network. Some malware is designed to detect a sandbox and behave harmlessly to avoid detection, which is a clever evasion tactic I found interesting.

### tcpdump
tcpdump is a lightweight, command line packet analyzer preinstalled on most Linux systems. Reading its output taught me to identify:
- Timestamp of the captured packet
- Source IP and port
- Destination IP and port

This is a practical skill because security analysts use tools like tcpdump or Wireshark to spot unusual traffic patterns that may indicate an attack such as a DoS.

[Insert image: Sample tcpdump terminal output with source and destination IPs highlighted]

### Real World Case Study: The 2016 DNS Provider DDoS Attack
This case study made the theory click for me. A group had built a botnet originally meant for attacking gaming servers, and posted its code publicly. Other criminals used that same code to launch tens of millions of DNS requests at a major DNS service provider in a single morning. Since many large companies relied on this one provider, websites across North America and Europe became unreachable. The provider recovered within two hours, but it showed me how a single point of failure (relying on one DNS provider) combined with a botnet can cause widespread damage very quickly.

---

## 11. Cloud Security

### Shared Responsibility Model
This was a key concept. The CSP is responsible for securing the underlying cloud infrastructure such as physical data centers and hypervisors. The organization using the cloud is responsible for securing what it puts into the cloud, such as configurations, applications, and access controls. A common real world mistake is assuming the CSP handles everything, when in reality a misconfigured storage bucket left open to the public is the customer's responsibility, not the CSP's.

### Cloud Hardening Techniques

| Technique | What it means |
|---|---|
| IAM (Identity Access Management) | Manages who can access what inside the cloud environment |
| Hypervisors | Software that separates virtual machines from physical hardware. Type 1 runs directly on hardware (used by CSPs), Type 2 runs on top of an operating system |
| Baselining | Establishing a known good configuration as a reference point to detect unwanted changes |
| Cryptography | Encrypting data at rest and in transit to keep it confidential |
| Cryptographic Erasure | Destroying the encryption key rather than the data itself, making the data permanently unreadable, also called crypto shredding |

### Key Management Tools
- **TPM (Trusted Platform Module)**: A chip that securely stores passwords, certificates, and keys.
- **CloudHSM (Cloud Hardware Security Module)**: A dedicated device for secure key storage and cryptographic operations in the cloud.

### Other Cloud Risks I Learned
- **VM Escape**: If a hypervisor is misconfigured or vulnerable, an attacker could break out of one virtual machine and access the host or other VMs.
- **Zero Day Attacks**: Exploits that were previously unknown. CSPs often detect and patch these faster than a typical on premise IT team could on their own.
- **Attack Surface**: Every additional cloud service adds another possible entry point for attackers, so more services mean more configuration work and more monitoring needed.

---

## Skills Gained

- Understanding of core network devices: routers, switches, hubs, firewalls, modems, and access points
- Ability to explain the TCP/IP and OSI models and map protocols to their correct layer
- Knowledge of IPv4 packet structure and the differences between IPv4 and IPv6
- Familiarity with common protocols and their ports: DHCP, ARP, Telnet, SSH, POP3, IMAP, SMTP
- Understanding of wireless security protocol evolution from WEP to WPA3
- Knowledge of subnetting and CIDR notation for network segmentation
- Ability to compare firewall types, VPN protocols, and IDS/IPS/SIEM tools
- Understanding of common attacks: packet sniffing, IP spoofing, on path attacks, smurf attacks, DoS attacks, backdoors, and brute force attacks
- Awareness of prevention techniques: hashing and salting, MFA, CAPTCHA, and password policies
- Basic ability to read tcpdump output for packet level analysis
- Understanding of cloud security fundamentals: shared responsibility model, IAM, hypervisors, baselining, and cryptographic erasure

---

## Key Learnings and Reflections

- Networks rely on specialized devices such as routers, switches, and firewalls to move and secure data.
- Cloud computing shifts infrastructure to CSPs through SaaS, IaaS, and PaaS models, offering reliability, lower cost, and scalability.
- The TCP/IP model has four layers while the OSI model has seven, both describing how data travels across a network.
- IPv4 packets contain detailed header fields, and IPv6 was created to solve address exhaustion.
- Protocols like DHCP, ARP, SSH, and SMTP each play a specific role, often tied to a fixed port number.
- Wireless security evolved from the weak WEP standard to the much stronger WPA3.
- Subnetting and CIDR allow large networks to be divided into smaller, more secure, and more efficient segments.
- Firewalls, proxies, VPNs, IDS, IPS, and SIEM tools work together under the defense in depth principle.
- Common attacks include packet sniffing, IP spoofing, on path attacks, smurf attacks, DoS attacks, backdoors, and brute force attempts, each with specific prevention strategies.
- Cloud security depends heavily on the shared responsibility model, proper IAM configuration, and strong cryptographic practices.

---

## Conclusion

This course completely reshaped how I see the internet. Before this, I used networks every day without thinking about what happens behind the scenes. Now I can explain how a single web request travels through the TCP/IP layers, gets routed using IP addressing, passes through firewalls and possibly an IDS or IPS, and reaches a server, all in a fraction of a second. I also understand that security is never about one tool. It is about layering firewalls, encryption, monitoring, and good policies together, which is the defense in depth principle that came up again and again throughout the course. The real world DDoS case study especially helped me connect the theory to how these attacks actually unfold in practice.
