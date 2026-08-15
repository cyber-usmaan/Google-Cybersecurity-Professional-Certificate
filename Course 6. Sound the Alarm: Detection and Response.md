# Sound the Alarm: Detection and Response

**Course 6 of the Google Cybersecurity Professional Certificate**

This is my personal summary and portfolio writeup for the sixth course in the program. I completed this course as part of my journey into cybersecurity, and this document captures what I learned, how the pieces connect, and why each concept matters in real security work. I wrote it in my own words to prove my understanding and to use it later as a quick revision guide.

---

## Table of Contents

1. [Roles in Incident Response Teams](#1-roles-in-incident-response-teams)
2. [Detection Tools: IDS, IPS, and EDR](#2-detection-tools-ids-ips-and-edr)
3. [SIEM Technology](#3-siem-technology)
4. [Network Monitoring and Baselines](#4-network-monitoring-and-baselines)
5. [Packet Captures and Network Protocol Analyzers](#5-packet-captures-and-network-protocol-analyzers)
6. [Investigating Packets with Wireshark](#6-investigating-packets-with-wireshark)
7. [Capturing Packets with tcpdump](#7-capturing-packets-with-tcpdump)
8. [Detection Methods](#8-detection-methods)
9. [Monitoring CI/CD Pipelines](#9-monitoring-cicd-pipelines)
10. [Indicators of Compromise and the Pyramid of Pain](#10-indicators-of-compromise-and-the-pyramid-of-pain)
11. [Documentation Best Practices](#11-documentation-best-practices)
12. [The Triage Process](#12-the-triage-process)
13. [Business Continuity Planning](#13-business-continuity-planning)
14. [Post Incident Review](#14-post-incident-review)
15. [Logs and Log Management](#15-logs-and-log-management)
16. [Log File Formats](#16-log-file-formats)
17. [IDS Types and Detection Techniques](#17-ids-types-and-detection-techniques)
18. [Suricata](#18-suricata)
19. [SIEM Log Ingestion and Search Methods](#19-siem-log-ingestion-and-search-methods)
20. [Conclusion](#conclusion)
21. [Skills Gained](#skills-gained)
22. [Summary](#summary)

---

## 1. Roles in Incident Response Teams

Every incident response effort needs structure, otherwise chaos takes over during an attack. I learned that organizations rely on a **Computer Security Incident Response Team (CSIRT)** and a **Security Operations Center (SOC)** to bring that structure. A CSIRT is a specialized group trained specifically for incident management. It can be a permanent team or a task force that only comes together when an incident happens. Effective response depends on three things working together: command (leadership and direction), control (managing technical resources), and communication (keeping everyone informed).

Inside a CSIRT there are usually three core security roles.

| Role | Responsibility |
|---|---|
| Security Analyst | Monitors the environment, triages alerts, does root cause investigation, escalates critical threats |
| Technical Lead | Finds the root cause, builds and runs the containment and recovery strategy, coordinates with business priorities |
| Incident Coordinator | Bridges the gap with non security departments like legal, HR, and PR so communication stays clear |

Non security professionals also get pulled into a CSIRT when needed, since incidents often touch legal, HR, or public relations concerns and not just technical ones.

The **SOC** is a separate concept, though it sometimes overlaps with the CSIRT. A SOC is the unit responsible for continuously monitoring networks, systems, and devices. This is what people mean when they talk about the "blue team," the defenders. SOC analysts are organized in tiers based on experience.

![SOC tier structure diagram]

- **Tier 1 (L1)**: Least experienced. They monitor alerts, prioritize them by severity, open and close tickets, and escalate anything serious.
- **Tier 2 (L2)**: More experienced. They pick up escalated tickets, dig deeper, tune detection tools, and report to the SOC Lead.
- **Tier 3 (L3, SOC Lead)**: Highly experienced. They manage the team's daily work, perform advanced techniques like malware and forensic analysis, and report to the SOC manager.
- **SOC Manager**: Sits at the top. Hires and trains the team, tracks performance metrics, builds compliance and incident reports, and communicates with executives.

A SOC can also include specialized roles like **forensic investigators** (who collect and preserve digital evidence) and **threat hunters** (who proactively search for hidden threats using intelligence).

**My takeaway:** Knowing this hierarchy is not just trivia. During a real incident, understanding who to escalate to and what their responsibility is saves critical time. It also tells me where I could grow in my own career, from L1 analyst toward more advanced specializations like threat hunting or forensics.

---

## 2. Detection Tools: IDS, IPS, and EDR

Detection tools exist because organizations cannot protect what they cannot see. I like comparing them to a home security system, they watch for something unusual and raise an alarm.

There are three tools I need to clearly distinguish, since they get confused often.

| Capability | IDS | IPS | EDR |
|---|---|---|---|
| Detects malicious activity | Yes | Yes | Yes |
| Prevents intrusions | No | Yes | Yes |
| Logs activity | Yes | Yes | Yes |
| Generates alerts | Yes | Yes | Yes |
| Performs behavioral analysis | No | No | Yes |

**Intrusion Detection System (IDS)** only watches and alerts. It never blocks anything on its own. For example, if an unknown IP logs into a system at 3 AM, the IDS raises an alert, but a human or another tool has to act on it. Common tools here are Zeek, Suricata, Snort, and Sagan.

When analyzing IDS alerts, I need to know the four detection outcomes:

- **True positive**: A real attack is correctly detected.
- **True negative**: No attack exists, and nothing is flagged. This is the normal, quiet state.
- **False positive**: The tool flags something as malicious when it is not. This wastes analyst time.
- **False negative**: A real attack happens but the tool misses it. This is the most dangerous outcome because the team stays unaware.

**Intrusion Prevention System (IPS)** does everything an IDS does, but it also takes action. For example, it can automatically update a router's access control list to block malicious traffic. Many tools like Suricata and Snort can run in either IDS or IPS mode.

**Endpoint Detection and Response (EDR)** is installed directly on endpoints, meaning any device connected to the network like a laptop or phone. What makes EDR different is behavioral analysis. It uses machine learning to study normal patterns on an endpoint, and if something breaks that pattern, like an unusual process suddenly starting up, it can automatically stop it without a human stepping in. Examples include Open EDR, Bitdefender EDR, and FortiEDR.

**My takeaway:** IDS is the watchdog that barks, IPS is the watchdog that also bites, and EDR is a much smarter guard that lives specifically on the endpoint and can act on its own using behavior patterns rather than just fixed rules.

---

## 3. SIEM Technology

**Security Information and Event Management (SIEM)** is one of the most important tools I studied in this course. A SIEM collects and analyzes log data to monitor activity across an entire organization. It essentially becomes the central nervous system for detection.

SIEM tools bring three main advantages.

1. **Access to event data**: they can pull in real time activity from hundreds of connected systems.
2. **Monitoring, detecting, and alerting**: they continuously watch for rule matches and send alerts.
3. **Log storage**: they retain historical data, which is essential for investigations that need to look backward in time.

The SIEM process has three steps, and I found it useful to memorize this as a pipeline.

**Step 1: Collect and Aggregate Data**

The SIEM pulls logs from many sources like firewalls, servers, and routers, and brings them into one centralized place. Along the way, **parsing** happens, which means the raw log text gets mapped into clear fields and values. For example, a messy raw log line gets broken down into readable pairs like `host = server`, `source_ip = 218.124.14.105`, and `source_port = 5023`.

**Step 2: Normalize Data**

Different sources format their data differently. A firewall log does not look like a server log. **Normalization** converts everything into one standard, structured format so the SIEM can search and compare across sources consistently.

**Step 3: Analyze Data**

Once the data is collected and normalized, the SIEM applies detection rules to it. If activity matches a rule, an alert fires. Part of this step involves **correlation**, comparing multiple log events together to spot patterns that a single log alone would not reveal.

Common SIEM tools in the industry include Splunk, Chronicle (Google Security Operations), Elastic, Exabeam, IBM QRadar, LogRhythm, and AlienVault OSSIM.

**My takeaway:** The SIEM is where raw noise becomes usable signal. Without collection, normalization, and analysis working together, an analyst would be stuck manually digging through dozens of separate systems, which simply is not realistic at scale.

---

## 4. Network Monitoring and Baselines

Networks generate constant traffic just from ordinary activity, sending an email, streaming a video, browsing a site. This is called **network traffic** (the amount of data moving) and **network data** (the actual data being transmitted).

To detect anything abnormal, I first need to know what normal looks like. This is the idea of a **baseline**, a reference point for expected behavior. I compared it to tracking a personal budget: once I know my normal spending pattern, an unusual spike stands out immediately. In security, the same logic applies to network traffic.

![Baseline graph example]

Once a baseline is set, I can monitor for deviations across a few areas.

- **Flow analysis**: looking at how packets move across ports and protocols. Malicious actors sometimes use uncommon port and protocol combinations to maintain **command and control (C2)** communication with a compromised system, for example running HTTPS traffic over port 8088 instead of the standard port 443.
- **Packet payload information**: examining the actual data inside packets. This can reveal data exfiltration if sensitive information is leaving the network unexpectedly.
- **Temporal patterns**: watching for activity that happens outside normal hours. If a company only sees traffic during business hours and suddenly there is a large spike at 2 AM, that is off baseline and worth investigating.

I also learned the difference between a **SOC** and a **Network Operations Center (NOC)**. A SOC focuses on security, detecting and responding to threats. A NOC focuses on performance, keeping the network available and running smoothly. They are related but not the same job.

Common network monitoring tools include IDS (for automated alerting) and network protocol analyzers like tcpdump and Wireshark (for manual, detailed inspection).

**My takeaway:** Baselines are the foundation for almost everything downstream in detection. Without knowing normal, I cannot recognize abnormal, which is really the whole point of monitoring.

---

## 5. Packet Captures and Network Protocol Analyzers

Every network packet carries three components: the **header**, the **payload**, and the **footer**.

- **Header**: carries routing information such as source and destination IP addresses, packet length, and protocol type. A packet can carry multiple headers depending on the protocol layers involved, for example an Ethernet header stacked with an IP header and a TCP header.
- **Payload**: the actual data being delivered, for example the bytes of an image being uploaded.
- **Footer**: located at the end, mainly used by Ethernet for error checking. Most protocols, including IP itself, do not use a footer.

A **network protocol analyzer**, also called a **packet sniffer**, is a tool that captures and displays this traffic. Wireshark, tcpdump, and TShark are the common examples. These tools are not just for security investigations either, they help with troubleshooting slow networks and gathering bandwidth statistics. Of course, the same capability can be abused by attackers to steal credentials off the wire, which is why using these tools without authorization is illegal in many places.

**How packet sniffing actually works:**

1. Traffic must be collected through the **Network Interface Card (NIC)**. By default a NIC only listens for traffic addressed to it. To capture everything, it needs to switch into what is called **promiscuous mode** (or **monitoring mode** on wireless interfaces).
2. The captured traffic exists in raw binary, which is not readable by humans. The protocol analyzer translates this binary into a readable format.

A **packet capture (p-cap)** is simply a saved file of intercepted packets, which can be reopened and analyzed later. There are several capture file formats worth knowing:

- **Libpcap**: the default for Unix-like systems, used by tools like tcpdump.
- **WinPcap**: an older Windows format, mostly outdated now.
- **Npcap**: built by Nmap, commonly used on modern Windows systems.
- **PCAPng**: the modern "next generation" format that can capture and store data simultaneously.

**My takeaway:** Packet analysis feels like reading the network's diary. Once I understood that packets always follow this header, payload, footer structure, filtering and searching through them in Wireshark made a lot more sense.

---

## 6. Investigating Packets with Wireshark

I explored two IP versions and their header fields in depth, since these fields are exactly what an analyst filters on.

**IPv4** has thirteen header fields including Version, Internet Header Length, Type of Service, Total Length, Identification, Flags, Fragment Offset, Time to Live (TTL), Protocol, Header Checksum, Source Address, Destination Address, and Options.

**IPv6** simplifies this down to eight fields: Version, Traffic Class, Flow Label, Payload Length, Next Header, Hop Limit, Source Address, and Destination Address. IPv6 adoption keeps growing mainly because of its much larger address space.

**Wireshark** is an open source protocol analyzer with a graphical interface, which makes it much easier to visually inspect traffic compared to a pure command line tool.

**Display filters** let me narrow down what I am looking at inside a large capture. Comparison operators can be written as symbols or abbreviations.

| Operator | Symbol | Abbreviation |
|---|---|---|
| Equal | == | eq |
| Not equal | != | ne |
| Greater than | > | gt |
| Less than | < | lt |
| Greater than or equal | >= | ge |
| Less than or equal | <= | le |

I can combine filters using **and**, **or**, and use parentheses to group and prioritize conditions, similar to how math expressions work.

Some filter examples I practiced:

```
ip.addr == 172.21.224.2        # any packet with this IP as source or destination
ip.src == 10.10.10.10          # only packets from this source IP
ip.dst == 4.4.4.4               # only packets to this destination IP
eth.addr == 00:70:f4:23:18:c4   # filter by MAC address
udp.port == 53                  # filter DNS traffic over UDP
tcp.port == 25                  # filter mail traffic over TCP
dns                              # simple protocol filter
```

The **contains** operator finds an exact string match inside a packet, for example searching HTTP traffic for the word "moved." The **matches** operator lets me filter using a regular expression pattern instead of a fixed string.

Wireshark also lets me **follow a stream**, meaning it reassembles an entire back and forth conversation between two devices into something readable, which is very useful for reviewing a full HTTP request and response exchange.

**Lab practice:** In the hands on lab, I opened a saved packet capture, applied IP address and MAC address filters to isolate a browsing session, and drilled into DNS query and answer records to confirm which IP address a domain resolved to. I also filtered TCP port 80 traffic and read frame details like Time to Live and header length directly from the packet inspection panel.

**My takeaway:** Filters are the real skill here. Anyone can open Wireshark and see a wall of packets, but knowing how to narrow that wall down to exactly the traffic that matters is what separates a useful investigation from wasted time.

---

## 7. Capturing Packets with tcpdump

While Wireshark gives a graphical experience, **tcpdump** is the command line equivalent, commonly pre installed on Linux and available on macOS. It captures traffic and can save it into a p-cap file for later analysis.

Because packet sniffing needs elevated access, tcpdump normally requires root privileges or the `sudo` command. The basic syntax looks like this:

```
sudo tcpdump [-i interface] [option(s)] [expression(s)]
```

I learned the key options that come up constantly in real usage:

| Option | Purpose |
|---|---|
| `-i` | specify the interface to capture from, `-i any` captures from every interface |
| `-D` | lists available interfaces on the system |
| `-w` | writes captured packets to a file instead of printing them |
| `-r` | reads a saved packet capture file |
| `-v` / `-vv` / `-vvv` | increases verbosity, more `v` characters means more detail |
| `-c` | limits the number of packets captured, for example `-c 3` captures only three |
| `-n` / `-nn` | disables name resolution, `-n` skips hostnames, `-nn` skips both hostnames and ports |

The `-n` option matters more than it looks. By default tcpdump tries to resolve IP addresses into hostnames using **reverse DNS lookups**. This can accidentally tip off an attacker that they are being investigated, since the lookup itself creates a DNS record trail. Disabling name resolution is considered best practice during an active investigation.

**Filter expressions** work similarly to Wireshark's filters. I can combine terms with boolean operators:

```
sudo tcpdump -r packetcapture.pcap -n 'ip and port 80'
sudo tcpdump -r packetcapture.pcap -n 'ip and (port 80 or port 443)'
```

Reading tcpdump output means recognizing five key parts on each line: the **timestamp**, **source IP**, **source port**, **destination IP**, and **destination port**, followed by additional protocol details.

**Lab practice:** I used `sudo ifconfig` and `sudo tcpdump -D` to identify available network interfaces, then captured live traffic on the correct interface, saved it to a file with `-w`, and filtered the saved capture afterward using expressions and the `-n` flag to keep output clean and readable.

**My takeaway:** tcpdump feels less friendly than Wireshark at first, but it is faster for quick checks on a server where there is no graphical interface available, which is a very common real world scenario for a security analyst working remotely on Linux systems.

---

## 8. Detection Methods

Detection tools alone are not enough because they only catch what they are specifically configured to catch. This is where additional human driven detection methods come in.

**Threat hunting** is the proactive search for threats that automated tools missed. It combines technology with human judgement to catch things like **fileless malware**, malware that hides in memory instead of using files, which makes it very good at evading signature based detection. Threat hunters use a mix of threat intelligence, indicators of compromise, indicators of attack, and machine learning to search for hidden threats.

**Threat intelligence** is evidence based information about existing or emerging threats. It can come from:

- **Industry reports**: describing attacker tactics, techniques, and procedures (TTPs).
- **Government advisories**: similar content from government sources.
- **Threat data feeds**: streams of indicators like IPs, domains, and file hashes, often used to defend against **Advanced Persistent Threats (APTs)**, which are attackers who maintain unauthorized access for extended periods.

Organizations often manage all of this through a **Threat Intelligence Platform (TIP)**, which centralizes and prioritizes threat intelligence from multiple sources. It is worth noting that threat intelligence should add context to detections, not replace them entirely.

**Cyber deception** is my favorite concept from this section. It deliberately tricks attackers to catch them in the act. The classic example is a **honeypot**, a fake, vulnerable looking resource meant to attract intruders. For instance, a fake file labeled "Client Credit Card Information 2022" could lure an attacker in, and the moment they touch it, security teams get alerted.

**My takeaway:** No single detection tool can keep up with every evolving threat. Threat hunting, intelligence sharing, and deception each cover a gap that automated rules alone cannot.

---

## 9. Monitoring CI/CD Pipelines

This section connected security to modern software development practices, which I found genuinely important since so much of today's software gets built and shipped through automated pipelines.

**Continuous Integration and Continuous Delivery/Deployment (CI/CD)** pipelines speed up software releases, but they also open new attack surfaces. If someone compromises a pipeline, they can inject malicious code, steal secrets, or break the software entirely. Effective CI/CD monitoring goes beyond just collecting logs, it actively looks for unusual patterns in build processes, code changes, and deployment steps.

Common **Indicators of Compromise (IoCs)** to watch for inside a pipeline include:

- **Unauthorized code changes**: commits from people who should not have access.
- Suspicious build behavior, unexpected dependency changes, and unusual deployment timing.

**Continuous vulnerability scanning** is a key defensive practice here. Regularly checking CI/CD infrastructure, plugins, and containers for known **Common Vulnerabilities and Exposures (CVEs)** helps find weak points before an attacker does. These vulnerabilities are themselves IoCs, since they mark exactly where a compromise is most likely to happen.

**My takeaway:** Security teams cannot treat the development pipeline as a black box outside their responsibility. It is part of the attack surface just like any server or endpoint, and automating threat detection there is what allows teams to ship quickly without sacrificing safety.

---

## 10. Indicators of Compromise and the Pyramid of Pain

**Indicators of Compromise (IoCs)** are pieces of observable evidence tied to an attack, for example a file name associated with known malware. I like the analogy the course gave me: an IoC is like noticing something has already been stolen from your car, it proves something happened, after the fact.

**Indicators of Attack (IoAs)** are different. They describe the series of events happening in real time that reveal an attacker's methods and intentions while the attack is still unfolding. In short, IoCs answer *who* and *what* after the fact, while IoAs answer *why* and *how* while it is happening. If a malicious process makes a network connection, that behavior itself is an IoA, while the specific filename and IP address involved are the related IoCs.

It is worth remembering that an IoC does not automatically confirm a security incident. It could just as easily be human error or a system malfunction.

The **Pyramid of Pain**, created by security researcher David J. Bianco, is the concept I found most memorable in this entire course. It ranks IoCs by how much difficulty they cause an attacker when defenders block them.

![Pyramid of Pain diagram]

From easiest to hardest for an attacker to work around:

1. **Hash values**: unique fingerprints of known malicious files. Trivial to change, an attacker just modifies the file slightly.
2. **IP addresses**: easy to rotate to a new address.
3. **Domain names**: slightly harder to change than an IP but still replaceable.
4. **Network artifacts**: observable evidence in network traffic, like a specific User Agent string.
5. **Host artifacts**: evidence left on a device, like a specific malware file name.
6. **Tools**: the actual software the attacker relies on, like a password cracking tool such as John the Ripper.
7. **Tactics, Techniques, and Procedures (TTPs)**: the attacker's actual behavior patterns. This is the hardest of all to change, since it requires retraining an entire approach, not just swapping a file or IP.

**Lab practice:** In the file hash investigation activity, I used a VirusTotal report to confirm a file was malware based on community score and vendor detections, then extracted multiple IoC types from the same report, a domain name, an associated IP address, an MD5 hash, host and network artifacts like HTTP requests to that domain, the tool used for input capture, and command and control listed as the TTP.

**My takeaway:** The Pyramid of Pain reframes how I prioritize detection work. Blocking a single IP is a quick win but has almost no lasting impact. Detecting TTPs is much harder to build, but it forces the attacker to fundamentally change their approach, which is a far bigger win for defenders.

---

## 11. Documentation Best Practices

Documentation might sound like the boring part of security work, but this section convinced me it is one of the most important habits an analyst can build.

Effective documentation provides three core benefits.

- **Transparency**: supports compliance, legal proceedings, and insurance requirements. **Chain of custody**, the documented trail of who possessed evidence throughout an incident, is a direct example of documentation creating an audit trail.
- **Standardization**: repeatable processes make onboarding easier and support continuous improvement. An **incident response plan** is the clearest example, it documents the steps to follow in advance so the response stays consistent no matter who is handling it.
- **Clarity**: good documentation helps people quickly find what they need. Analysts should always document the reasoning behind their actions so teammates understand why an alert was closed or escalated.

The best practice guidelines I want to remember going forward:

- **Know your audience**: an incident summary for a SOC manager reads very differently from one written for a CEO. Technical depth should match the reader's background.
- **Be concise**: establish the purpose right away. An executive summary at the start of a report should be short enough to skim quickly.
- **Update regularly**: the threat landscape keeps shifting, so documentation, especially incident response plans, needs to be reviewed and revised after every major incident.

**My takeaway:** Documentation is not paperwork for its own sake, it directly protects the organization legally, keeps the team consistent under pressure, and speeds up onboarding for new analysts.

---

## 12. The Triage Process

**Triage** is the process of prioritizing incidents by importance and urgency. I connected this instantly to medical triage in an emergency room, security teams have limited time and resources, so not every alert deserves the same level of urgency.

The triage process has three steps.

**Step 1: Receive and Assess**

An analyst receives an alert, often from an IDS, and reviews it for validity. Key questions to ask during this step:

- Is the alert a false positive?
- Was this alert triggered before, and how was it resolved?
- Is it tied to a known vulnerability?
- What is the severity?

**Step 2: Assign Priority**

Once confirmed as genuine, the incident gets prioritized based on three factors:

- **Functional impact**: how badly the incident affects business systems, for example a ransomware attack that encrypts data.
- **Information impact**: how it affects confidentiality, integrity, and availability of data, for example data exfiltration affecting third parties.
- **Recoverability**: whether recovery is realistically possible given time, cost, and available resources. If recovery is not feasible, spending heavy resources on it may not be worthwhile.

**Step 3: Collect and Analyze**

The analyst gathers evidence, does external research, and documents the investigation. Depending on severity, this may get escalated to a level two analyst or manager with more advanced skills.

Triage delivers two clear benefits: **resource management** (focus stays on urgent threats instead of wasting time on low priority tasks) and a **standardized approach** (playbooks ensure alerts get properly validated before moving further up the chain).

**My takeaway:** Triage is what keeps a security team from drowning in alert fatigue. Without prioritization, every alert would demand equal attention, and the truly dangerous incidents could easily get lost in the noise.

---

## 13. Business Continuity Planning

Security incidents do not just create technical problems, they can shut down entire business operations. A **Business Continuity Plan (BCP)** is a document that outlines how to sustain operations during and after a major disruption. As an entry level analyst I would not typically build or test a BCP myself, but understanding how it works is still valuable context.

I found the healthcare example particularly striking. A ransomware attack on a hospital can encrypt patient records, directly preventing providers from delivering care. At a larger scale, incidents targeting critical infrastructure can threaten national security and public safety, which is exactly why BCPs exist, to minimize interruptions to essential services.

**Note:** A BCP is not the same thing as a **disaster recovery plan**. Disaster recovery focuses specifically on restoring information systems after a major disaster, which could be anything from hardware failure to a natural disaster like a flood.

**Recovery strategies** inside a BCP often include **site resilience**, ensuring networks or data centers remain available even during a disruption. There are three types of recovery sites.

| Site Type | Description |
|---|---|
| Hot site | Fully operational duplicate of the primary environment, can activate immediately |
| Warm site | Fully configured but not immediately live, can be made operational quickly |
| Cold site | Has some infrastructure in place but needs significant work before use |

**My takeaway:** Resilience is not something you build during a crisis, it has to be planned and tested in advance. The gap between a hot site and a cold site is really a gap in how much money and effort an organization is willing to invest in advance versus how much downtime it can tolerate.

---

## 14. Post Incident Review

The final phase of the NIST Incident Response Lifecycle is **Post Incident Activity**, the process of reviewing an incident to find areas for improvement. I learned that closing an incident is not the end of the work, it is actually where a lot of long term value gets created.

![NIST Incident Response Lifecycle phases]

The **lessons learned meeting**, also called a post mortem, brings together everyone involved after a major incident. Its purpose is to evaluate what happened and identify improvements, never to assign blame. This meeting should happen no later than two weeks after the incident is resolved. Not every incident needs its own dedicated meeting, but major ones like ransomware attacks definitely should get one.

Typical questions covered in this meeting:

- What happened, and when did it happen?
- Who discovered it?
- How was it contained?
- What actions were taken for recovery?
- What could have been done differently?

Before the meeting, organizers should prepare an agenda and assign roles, including a moderator to guide discussion and a scribe to record notes.

The meeting should end with a list of prioritized, actionable recommendations, for example updating playbook instructions or adopting new security tools, so lessons actually get implemented rather than forgotten.

The **final report** is one of the most important documents created at this stage. It should cover the 5 W's: **who**, **what**, **where**, **why**, and **when**. Common sections in a final report include:

- **Executive summary**: high level overview of key findings.
- **Timeline**: chronological sequence of events with timestamps.
- **Investigation**: details of the detection and analysis work, for example packet capture analysis findings.
- **Recommendations**: suggested actions for future prevention.

**My takeaway:** Every incident is a learning opportunity, and if the lessons never get written down and acted on, the organization is likely to face the exact same problem again.

---

## 15. Logs and Log Management

A **log** is a record of events happening inside an organization's systems. Originally logs were mostly used for troubleshooting technical issues, but today they are one of the most valuable data sources for security investigations, especially for answering the **5 W's**: who, what, when, where, and why.

There are five common log types I need to recognize.

| Log Type | Generated By |
|---|---|
| Network | Firewalls, routers, switches |
| System | Operating systems like Windows, Linux, macOS |
| Application | Software applications |
| Security | Antivirus software, IDS tools |
| Authentication | Login events |

A basic log entry usually contains a date, time, location, action, and the author of the action. **Verbose logging** records extra detail beyond the default, for example including the exact device and IP address alongside a login event rather than just the username.

**Log management** is the process of collecting, storing, analyzing, and disposing of log data. A few important best practices stood out to me.

- **Choosing what to log**: not every data point needs to be recorded. Some data, like phone numbers or email addresses, counts as **personally identifiable information (PII)** and requires special handling, and in some regions may not even be legal to log.
- **Avoiding overlogging**: logging everything sounds safer but is actually one of the most common mistakes organizations make. It increases storage costs, adds performance strain, and makes it harder to find the events that actually matter.
- **Log retention**: some industries have regulatory requirements for how long logs must be kept, for example FISMA for the public sector, HIPAA for healthcare, and PCI DSS, GLBA, and SOX for financial services.
- **Log protection**: attackers sometimes modify logs to hide their tracks. Storing logs on a centralized log server, rather than locally on the device that generated them, creates a barrier that makes it harder for an attacker to tamper with the evidence.

**My takeaway:** More logging is not automatically better logging. The goal is capturing the right data, protecting it, and keeping it for the right amount of time, not just collecting everything possible.

---

## 16. Log File Formats

Different systems produce logs in different formats, and being able to read each one is a core analyst skill. I studied five common formats.

**JSON (JavaScript Object Notation)**

Lightweight and easy to read, commonly used in web technologies and cloud environments. It relies on **key-value pairs** (`"Alert": "Malware"`), commas to separate data, double quotes around text strings, curly brackets to define an **object** (a set of related key-value pairs), and square brackets to define an **array** (an ordered list of values).

**Syslog**

A standard for logging and transmitting data with three main sections.

- **Header**: includes timestamp, hostname, application name, and message ID. The timestamp format looks like `2022-03-21T01:11:11.003Z`, where `T` separates the date from the time and `Z` indicates UTC.
- **Structured data**: additional information in key-value pairs enclosed in square brackets.
- **Message**: the actual descriptive text of the event.
- **Priority (PRI)**: indicates urgency, generally the lower the number, the more urgent the event.

**XML (eXtensible Markup Language)**

Native to Windows systems, it uses **tags** (a start tag and an end tag, like `<tag>` and `</tag>`), **elements** (the tag plus the data inside it, always starting with one root element containing child elements), and **attributes** (extra descriptive information written inside the tag itself, always quoted).

**CSV (Comma Separated Value)**

Uses commas to separate values. The tricky part is that field names are often not included in the log itself, the position of each value determines its meaning, so I need to know exactly what fields the source device is producing.

**CEF (Common Event Format)**

Uses a strict pipe-separated structure:

```
CEF:Version|Device Vendor|Device Product|Device Version|Signature ID|Name|Severity|Extension
```

Fields are separated by the pipe character `|`, while the Extension field itself uses key-value pairs. When Syslog transports a CEF message, a timestamp and hostname get prepended to the front.

**My takeaway:** There is no single universal log format. Learning to read all of these means I can pull meaningful information out of almost any log source I encounter, regardless of which vendor or system produced it.

---

## 17. IDS Types and Detection Techniques

IDS technology can be deployed in two different locations, and each gives a different perspective on activity.

**Host-based Intrusion Detection System (HIDS)** is installed as an agent directly on a single endpoint. It monitors internal activity on that specific host, things like unauthorized applications, file system changes, and unusual user activity.

**Network-based Intrusion Detection System (NIDS)** is installed at specific points in the network and inspects traffic flowing between multiple devices rather than watching just one host.

![HIDS vs NIDS network diagrams]

Using both together gives a layered, more complete view of an environment since each one sees something the other cannot.

There are also two core detection techniques worth comparing directly.

| | Signature-based Analysis | Anomaly-based Analysis |
|---|---|---|
| How it works | Matches activity against known malicious patterns (signatures) | Compares current activity to a learned baseline of normal behavior |
| Advantage | Low false positive rate for known threats | Can catch new, previously unknown threats |
| Disadvantage | Easily evaded by slight code changes, requires constant signature updates, cannot detect zero-day attacks | High false positive rate, and if an attacker is already present during the training phase, their activity gets baked into the baseline as "normal" |

A **zero-day** attack is an exploit that was previously unknown, which is exactly the category signature-based detection cannot catch, since there is no existing signature for it yet.

**My takeaway:** Neither technique alone is enough. Signature-based catches known threats efficiently but misses anything new, while anomaly-based can catch new threats but generates a lot of noise. Real environments generally need both working together.

---

## 18. Suricata

**Suricata** is an open source tool that combines three capabilities in one: intrusion detection, intrusion prevention, and network security monitoring.

- As an **IDS**, it monitors traffic and alerts on suspicious activity, and it can also run in host-based mode on a single device.
- As an **IPS**, it can actively block malicious traffic, though this requires additional configuration to enable IPS mode.
- As a **Network Security Monitoring (NSM)** tool, it can analyze live traffic or existing packet captures and generate detailed traffic logs, which is very useful for forensics and refining detection signatures over time.

Suricata detects threats using **signature analysis**. A signature (used interchangeably with the word "rule" in Suricata) has three components.

1. **Action**: what to do if traffic matches, for example alert, pass, drop, or reject.
2. **Header**: network details like source and destination IP, ports, protocol, and direction.
3. **Rule options**: customization options, and their order actually matters, changing the order changes the meaning of the rule.

**Note:** Suricata processes rules in this default priority order regardless of how they appear in the file: pass, drop, reject, then alert. This matters when two rules conflict on the same packet.

Writing **custom rules** is strongly encouraged rather than relying only on the pre-written defaults, since every organization's infrastructure is different. Custom rules help minimize false positives and tailor detection to the actual environment.

Configuration lives in **suricata.yaml**, using the YAML format, which controls exactly how Suricata interacts with the rest of the environment.

Suricata generates two types of log files.

| Log File | Purpose |
|---|---|
| `eve.json` | The standard log, detailed and in JSON format. Includes a `flow_id` to correlate related events into a single network flow. Best for detailed analysis and SIEM ingestion. |
| `fast.log` | Minimal alert info, just IP and port basics. Considered a legacy format, useful for quick checks but not recommended for real incident response or threat hunting. |

**Lab practice:** In the hands on activity, I examined a custom rule, ran it against a sample packet capture to trigger alerts, then reviewed the resulting output in both `fast.log` and `eve.json` to compare the level of detail each format provided.

**My takeaway:** Suricata's flexibility is its strength, it is not locked into being just a detector, it can also actively block traffic and generate forensic-quality logs, all from one tool.

---

## 19. SIEM Log Ingestion and Search Methods

Coming back to the SIEM process one more time, this section focused specifically on the first step, collection and aggregation, through a concept called **log ingestion**.

**Log ingestion** is the process of collecting and importing data from log sources into a SIEM tool. When ingestion happens, the SIEM makes a copy of the event data and stores it internally, which means it can analyze the data without modifying the original source logs.

The most common way organizations handle this at scale is through **log forwarders**, software that automates collecting and sending log data. Manually uploading logs simply does not scale across a network with thousands of devices. Some operating systems come with native log forwarders, while others need third party forwarding software installed and configured to specify what to forward and where to send it.

Once data is ingested, analysts need to be able to search through it efficiently. I looked at two major SIEM platforms and how their search methods differ.

**Splunk Search Processing Language (SPL)**

A basic search example:

```
index=main fail
```

This tells Splunk to pull events from the index named `main` that contain the term `fail`.

SPL also supports **piping**, using the `|` character to chain commands together, so the output of one command becomes the input of the next.

```
index=main fail | chart count by host
```

This searches for `fail` events, then transforms the results into a chart counting them by host, which is useful for quickly spotting which devices have excessive failure counts.

**Wildcards** (`*`) expand a search to match variations of a term:

```
index=main fail*
```

This matches "fail," "failed," "failure," and any other word starting with "fail." Double quotes, by contrast, narrow a search down to an exact phrase, for example `"login failure"` only matches that exact string, not the words separately.

**Google Security Operations (Chronicle) Search**

Chronicle offers two distinct search types.

- **UDM Search (Unified Data Model)**: the default search type, working against data that has already been ingested, parsed, and normalized. It is faster because it searches structured, indexed data. UDM events always include common fields like **entities** (nouns describing devices, users, or processes involved), **event metadata** (basic description and timestamps), **network metadata** (protocol details), and **security results** (the outcome, like "virus detected and quarantined"). A simple example search: `metadata.event_type = "USER_LOGIN"`.
- **Raw Log Search**: searches through raw, unparsed logs when the normalized data does not have what I need. It takes longer since it is not searching structured indexed data, but it supports regular expressions for more precise pattern matching.

**My takeaway:** Every SIEM tool has its own search language, but the underlying logic stays consistent: filter, refine, and transform. Once I understood Splunk's pipe-based chaining, picking up the logic behind Chronicle's UDM versus Raw Log search felt much more natural.

---

## Skills Gained

- Understanding CSIRT and SOC organizational structure and escalation paths
- Comparing and selecting between IDS, IPS, and EDR detection tools
- Building and interpreting the SIEM data pipeline: collection, normalization, and analysis
- Establishing network baselines and detecting deviations through flow, payload, and temporal analysis
- Capturing and filtering network traffic using Wireshark and tcpdump
- Reading and interpreting IPv4 and IPv6 packet headers
- Applying threat hunting, threat intelligence, and cyber deception concepts
- Monitoring CI/CD pipelines for indicators of compromise
- Classifying and prioritizing indicators of compromise using the Pyramid of Pain
- Writing clear, audience aware incident documentation
- Executing the triage process to prioritize incidents by impact and recoverability
- Understanding business continuity planning and site resilience strategies
- Conducting post incident reviews and writing final incident reports
- Managing log collection, retention, and protection practices
- Reading JSON, Syslog, XML, CSV, and CEF log formats
- Comparing signature-based and anomaly-based detection techniques
- Configuring and writing custom rules in Suricata
- Searching SIEM platforms using Splunk SPL and Google SecOps UDM/Raw Log search

## Summary

- Incident response relies on structured teams (CSIRT, SOC) with clear roles across tiers
- IDS detects, IPS detects and blocks, EDR adds behavioral analysis on endpoints
- SIEM tools collect, normalize, and analyze logs from across an organization
- Baselines define "normal" so deviations can be detected in network traffic
- Packets have headers, payloads, and footers, and tools like Wireshark and tcpdump let analysts capture and filter them
- Threat hunting, threat intelligence, and honeypots extend detection beyond automated tools
- CI/CD pipelines need active monitoring for indicators of compromise
- IoCs prove something already happened, IoAs reveal attacker behavior in real time
- The Pyramid of Pain ranks IoCs by how disruptive it is for the attacker when blocked
- Documentation should be audience aware, concise, and kept up to date
- Triage prioritizes incidents by functional impact, information impact, and recoverability
- Business continuity plans keep operations running through major disruptions
- Post incident reviews close the loop with lessons learned meetings and final reports
- Logs come in several formats (JSON, Syslog, XML, CSV, CEF) and need careful management
- HIDS watches a single host, NIDS watches network traffic, and detection uses signature or anomaly based techniques
- Suricata combines IDS, IPS, and monitoring capabilities with customizable rules
- SIEM platforms like Splunk and Chronicle each have their own search syntax for finding relevant events

---

## Conclusion

This course tied together everything from earlier parts of the certificate and pushed it into the operational side of security work, actually detecting and responding to threats rather than just understanding concepts in theory. I moved from learning who does what in an incident response team, to reading raw packets byte by byte, to writing custom detection rules in Suricata, to understanding how a full incident gets closed out with a lessons learned meeting and a final report.

The single idea that stuck with me the most is the Pyramid of Pain. It changed how I think about detection priorities, because it reframed the goal from simply "block the bad thing" to "make it as painful as possible for the attacker to keep attacking." That shift in mindset feels like the real difference between checkbox security and genuinely effective defense.
