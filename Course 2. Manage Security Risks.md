![Course](https://img.shields.io/badge/Course%202-Manage%20Security%20Risks-4285F4)
![Status](https://img.shields.io/badge/Status-Completed-4EEB2A)

# Course 2: Manage Security Risks

## About This Course

This is the second course of the Google Cybersecurity Certificate. Building on the foundations from Course 1, I learned how organizations identify, classify, and manage security risk from the eight CISSP domains that structure a security team's responsibilities, to the frameworks, controls, and tools used to keep that risk within an acceptable level.

---

## Certificate

<p align="center">
  <img src="images/Google Cert 2 Manage Security Risks.png" alt="Certificate placeholder" width="480"/>
</p>

---

## Modules Covered

- Security Domains
- Security Frameworks and Controls
- Cybersecurity Tools
- Using Playbooks to Respond to Incidents

---

## What I Learned

### 1. The Eight CISSP Security Domains

<p align="center">
  <img src="images/CISSP Domains.png" alt="Eight CISSP security domains" width="640"/>
</p>

I learned that the CISSP's eight security domains give me a way to organize the full scope of a security analyst's responsibilities, from policy down to code.

- **Security and risk management** - sets security goals, risk mitigation processes, compliance, business continuity, legal regulations, and organizational ethics.
- **Asset security** - manages the storage, maintenance, retention, and destruction of physical and virtual data.
- **Security architecture and engineering** - builds the tools, systems, and processes that protect assets, guided by principles such as least privilege, defense in depth, and zero trust.
- **Communication and network security** - secures physical networks and wireless communications across on-site, remote, and cloud environments.
- **Identity and access management (IAM)** - authenticates user identities and authorizes access based on the principle of least privilege.
- **Security assessment and testing** - identifies and mitigates risk through security control testing, audits, and penetration testing.
- **Security operations** - investigates potential breaches and puts preventative measures in place using training, SIEM tools, log management, and playbooks.
- **Software development security** - embeds secure programming practices across the entire software development life cycle, not just at release.

### 2. Managing Threats, Risks, and Vulnerabilities

<p align="center">
  <img src="images/Threats Risks and Vulnerability.png" alt="Eight CISSP security domains" width="640"/>
</p>

Learned to separate three terms that are often used interchangeably but describe different things:

- **Threat** - any circumstance or event that can negatively impact an asset (for example, an insider threat or an advanced persistent threat).
- **Risk** - anything that can affect the confidentiality, integrity, or availability of an asset; broadly, risk is a function of how likely a threat is to occur.
- **Vulnerability** - a weakness that a threat can exploit.

To manage risk, there are four core strategies:

- **Acceptance** - accepting a risk to avoid disrupting business continuity.
- **Avoidance** - creating a plan that avoids the risk altogether.
- **Transference** - shifting the risk to a third party to manage.
- **Mitigation** - lessening the impact of a known risk.

Organizations pair these strategies with frameworks such as the **NIST Risk Management Framework (RMF)** and **HITRUST**. Also learned some of the factors that drive risk (external actors, internal staff or vendors, legacy systems, multiparty outsourcing, and software licensing gaps), along with a few real-world vulnerabilities worth recognizing:

| Vulnerability | What It Affects |
|---|---|
| ProxyLogon | Microsoft Exchange Server authentication |
| ZeroLogon | Microsoft's Netlogon authentication protocol |
| Log4Shell | Remote code execution via the Log4j Java library |
| PetitPotam | Windows NTLM authentication requests |
| Server-side request forgery | Backend resources on a server-side application |

### 3. Frameworks and Controls

**Frameworks** are the guidelines used to build a risk-mitigation plan, while **controls** are the specific safeguards used to carry that plan out. I was introduced to the **Cyber Threat Framework (CTF)**, which gives analysts a common language for describing threat activity, and **ISO/IEC 27001**, an internationally recognized framework for managing the security of assets such as financial data, intellectual property, and employee records.

Controls fall into three categories, and learned to recognize examples of each:

- **Physical controls** - gates, fences, locks, security guards, CCTV, and access badges.
- **Technical controls** - firewalls, multi-factor authentication, and antivirus software.
- **Administrative controls** - separation of duties, authorization procedures, and asset classification.

### 4. Applying the CIA Triad as an Analyst

<p align="center">
  <img src="images/CIA Triad.png" alt="Eight CISSP security domains" width="640"/>
</p>

Course 1 introduced the CIA triad; here it was taught that how each element plays out day to day:

- **Confidentiality** is reinforced through the **principle of least privilege**, limiting users to only the access their role requires.
- **Integrity** is verified through **cryptography** and **encryption**, which convert data into a format that can't be read or tampered with by unauthorized parties.
- **Availability** means authorized users - including remote employees - can reach the data they need, while still being limited to what their specific job requires.

### 5. The NIST Cybersecurity Framework (CSF)

The NIST CSF organizes an organization's cybersecurity work into Six ongoing functions:

<p align="center">
  <img src="images/NIST CSF.png" alt="NIST CSF five functions" width="720"/>
</p>

- **Identify** - know which systems, data, and assets exist.
- **Protect** - put policies, training, and safeguards in place to prevent an attack.
- **Detect** - recognize suspicious activity as it happens.
- **Respond** - contain, analyze, and resolve a security incident.
- **Recover** - restore normal operations and strengthen defenses for next time.
- **Govern** - implement security protocols in administrative level, and address concerns to stakeholders

### 6. OWASP Security Principles

<p align="center">
  <img src="images/OSWAP top 10.webp" alt="NIST CSF five functions" width="720"/>
</p>

I built on the OWASP principles introduced earlier with four additional ones. Together, these ten principles now guide how to think about secure design:

- **Minimize attack surface area** - reduce the number of potential entry points a threat actor could exploit.
- **Principle of least privilege** - grant only the access required to complete a task.
- **Defense in depth** - layer multiple controls rather than relying on one.
- **Separation of duties** - require more than one person for critical actions.
- **Keep security simple** - avoid unnecessary complexity, which makes security harder to maintain.
- **Fix security issues correctly** - identify the root cause, contain the impact, and test the fix.
- **Establish secure defaults** - make the secure configuration the default one.
- **Fail securely** - a failed control should default to its most secure state, not its most open one.
- **Don't trust services** - don't assume a third party's systems are secure without verification.
- **Avoid security by obscurity** - security should rely on sound design, not on hiding implementation details.

### 7. Security Audits

**Security audit** is an independent review of an organization's controls, policies, and procedures against internal and external criteria (regulatory compliance, laws, and federal regulations). Audits are shaped by the organization's industry, size, location, and applicable regulations, and frameworks like the NIST CSF and ISO 27000 series make audits easier to prepare for.

Building an audit generally follows the same checklist:

- Define the scope - which assets are being assessed, and how often.
- Complete a risk assessment covering budget, controls, and external standards.
- Conduct the audit against the defined scope.
- Create a mitigation plan to lower the identified risk.
- Communicate the findings and recommendations to stakeholders.

### 8. SIEM Tools in Practice

**SIEM tool** collects and analyzes log data in real time to help a security team monitor an organization's activity, though it still requires a human to interpret the results. SIEM tools are evolving toward **cloud-hosted** and **cloud-native** deployments, and are increasingly paired with **SOAR** (security orchestration, automation, and response) to automate routine responses and free up analysts for more complex incidents.

I explored two SIEM platforms and their dashboards:

- **Splunk** - security posture, executive summary, incident review, and risk analysis dashboards.
- **Chronicle** (Google) - enterprise insights, data ingestion and health, IOC matches, main, rule detections, and user sign-in overview dashboards.

Each dashboard serves a different purpose, from real-time threat monitoring to giving stakeholders a high-level summary of security trends over time.

### 9. Open-Source vs. Proprietary Tools

- **Open-source tools** are publicly available, often free, and can be modified by their users - for example, **Linux** (an open-source operating system) and **Suricata** (open-source network analysis and threat detection software).
- **Proprietary tools** are owned by a company, typically require a paid license, and can only be modified by the owner - Splunk and Chronicle are both examples.

Learned that open-source tools aren't inherently less secure; wide visibility into the source code often means issues are found and fixed faster.

### 10. Playbooks in Action

A **playbook** is a manual that defines the steps a team follows for a specific type of security incident, ensuring consistency regardless of who is handling the case. Playbooks are used alongside both **SIEM** and **SOAR** tools - a SIEM tool flags unusual activity, a playbook tells the analyst how to respond to it, and a SOAR tool can automate the first step of that response, such as locking an account after repeated failed logins.

---

## Skills Gained

- Organizing security responsibilities using the eight CISSP domains
- Recognizing physical, technical, and administrative controls
- Working with the NIST CSF's six functions
- Applying OWASP security principles to design decisions
- Planning and scoping a security audit
- Evaluating SIEM platforms and their dashboards (Splunk, Chronicle)
- Comparing open-source and proprietary security tools
- Using playbooks alongside SIEM and SOAR tools

## Key Learnings and Reflections

This course shifted my focus from vocabulary to structure. How the pieces I learned in Course 1 actually fit into an organization's day-to-day risk management. A few things stood out to me:

- The eight CISSP domains gave me a mental filing system for every topic that follows in the rest of the certificate.
- Frameworks and controls are not interchangeable - a framework sets the plan, and controls carry it out.
- Risk management is a business decision as much as a technical one; accepting, avoiding, transferring, or mitigating a risk all involve trade-offs.
- Tools like SIEM and SOAR are only as useful as the playbooks and human judgment behind them.

## Conclusion

This Course gave me a structural understanding of how organizations manage security risk, through domains, frameworks, controls, and the tools that support them. I now have a clearer picture of where a specific task fits within the bigger picture of an organization's security program, which sets up the next course's deeper focus on cybersecurity tools.
