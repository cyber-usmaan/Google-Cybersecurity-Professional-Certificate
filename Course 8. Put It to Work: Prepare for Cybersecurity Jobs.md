# Course 8: Put It to Work: Prepare for Cybersecurity Jobs

![Course](https://img.shields.io/badge/Protect%20Data%20and%20Communicate%20Incident-4285F4)
![Course](https://img.shields.io/badge/Escalate%20Incidents-4285F4)
![Course](https://img.shields.io/badge/Communicate%20Effectively%20to%20Influence%20Stakeholders-4285F4)
![Course](https://img.shields.io/badge/Engage%20with%20Cybersecurity%20Community-4285F4)
![Course](https://img.shields.io/badge/Use%20AI%20to%20Optimize%20Workflows-4285F4)
![Status](https://img.shields.io/badge/Status-Completed-4EEB2A)

## About Course

Unlike the earlier technical courses, this one shifts focus toward the operational and professional side of security work: how data and assets are classified, how organizations recover from incidents, how and when to escalate a problem, how to communicate with stakeholders, how generative AI fits into daily security work, and how to prepare for the job search itself. Below is a breakdown of every topic covered, explained in simple terms with practical examples.

---

## Certificate of completion:

<p align="center">
  <img src="images/Google Cert 8 Put It to Work Prepare for Cybersecurity Jobs_page_1.png" alt="Certificate placeholder" width="720"/>
</p>

---

# What I learned

## Data and Asset Classification

Every organization holds different kinds of data, and not all of it needs the same level of protection. Classifying data correctly is what allows a security team to focus its efforts where the risk is actually highest.

| Classification | Description | Example |
|---|---|---|
| Public data | Already available to anyone, low risk if exposed | Press releases, job postings |
| Private data | Should stay internal, risky if leaked | Company emails, employee IDs |
| Sensitive data | Requires strict access control, includes PII, SPII, and PHI | Bank details, passwords, medical records |
| Confidential data | Critical to business operations, often protected by NDAs | Trade secrets, financial records |

Asset classification works on the same idea, just applied to the systems and resources an organization owns rather than the data itself. A **low-level asset**, like a company's public website address, causes little damage if exposed. A **high-level asset**, like an internal email discussing trade secrets, can seriously damage a company's reputation, finances, and customer trust if it gets out. Recognizing this difference is what allows a security analyst to prioritize correctly instead of treating every alert with the same urgency.

---

## Business Continuity and Disaster Recovery

Security incidents happen even with strong defenses in place, so organizations prepare for that reality in advance rather than reacting blindly when it occurs.

### The Four Step Security Process

1. **Identify** the assets that need protection.
2. **Determine** what threats could affect those assets.
3. **Detect** potential threats using tools and monitoring processes.
4. **Plan** for business continuity and disaster recovery.

Business continuity and disaster recovery plans are the final piece of this process. They work together, but they solve slightly different problems.

### Business Continuity Plan

This document outlines how an organization keeps operating during and after a major disruption. It usually involves four steps:

- Conduct a business impact analysis to understand what a disruption would actually cost.
- Identify and document the steps needed to recover critical business functions.
- Organize a business continuity team, usually pulling members from cybersecurity, IT, HR, communications, and operations.
- Train that team regularly using different risk scenarios.

### Disaster Recovery Plan

This document focuses specifically on restoring systems and data after an incident, such as a ransomware attack that locks a manufacturing team out of critical data. It typically covers:

- Recovery strategies to restore software.
- Recovery strategies to restore hardware functionality.
- Identifying which applications and data were affected.

The relationship between the two is straightforward: business continuity keeps the organization running through the disruption, while disaster recovery focuses on getting the affected technology back to normal.

---

## Incident Escalation

Incident escalation is the process of recognizing a potential security problem and passing it along to someone with more experience or authority to handle it. As an entry-level analyst, a large part of the job is not solving every problem directly, it is recognizing which problems need to move up the chain.

### Breach Notification Laws

Many countries legally require organizations to notify individuals when their personally identifiable information (PII) has been exposed in a breach. PII includes things like Social Security numbers, driver's license numbers, and medical records. These laws change often, so staying current on them matters as part of the job.

### Low-Level vs Escalated Issues

A single failed login attempt is not alarming on its own. Fifteen failed attempts within thirty minutes is a different story, since that pattern could indicate someone actively trying to break into an account. The same logic applies to something like an employee downloading unapproved software: it might be harmless, or it might be malware that puts the whole network at risk. Low-level issues still deserve investigation, since they can turn into something more serious.

Every organization has its own escalation policy defining who gets notified, what tool or channel is used, and who to contact if the first responder is unavailable. Learning that specific policy is one of the first things to do at a new job.

---

## Roles and Responsibilities in Escalation

Different roles within an organization are responsible for different parts of how data is handled and protected. Knowing who is who determines who an issue should be escalated to.

| Role | Responsibility | Escalated When |
|---|---|---|
| Data owner | Decides who can access, edit, or destroy specific data | Unauthorized access to software or data they control |
| Data controller | Determines how and why customer data is processed | Sensitive customer information is at risk |
| Data processor | A vendor that processes data on behalf of the controller | An issue with third party data processing |
| Data custodian | Grants and revokes access, manages storage and transmission of data | Access controls need strengthening or have been compromised |
| Data protection officer (DPO) | Monitors compliance with data protection standards | Established protocols or standards have been violated |

Understanding this table is really about understanding the flow of accountability. A data owner decides the rules, a data controller decides the purpose, a data processor carries out the work, a data custodian manages the technical access, and a DPO checks that everyone is actually following the rules that were set.

---

## Escalation Timing and Decision Making

Deciding when to escalate an incident is one of the more judgment heavy parts of the job. Confidence matters here, but so does knowing the limits of that confidence.

- Learn the organization's escalation policy early, since it removes a lot of the guesswork later.
- Ask questions when unsure. This is a sign of diligence, not a weakness.
- Not every incident carries the same weight. Understanding which assets matter most to the business (through onboarding materials, direct conversations with a supervisor, or the company's security policies) makes it possible to prioritize correctly.

### Incident Types Recap

- **Malware infections**: malicious software infiltrating a system or network.
- **Unauthorized access**: someone gaining digital or physical access without permission.
- **Improper usage**: an employee violating the organization's acceptable use policy.

The priority of an incident should generally follow the importance of the asset it affects. Unauthorized access to a live manufacturing application is a far bigger deal than malware infecting an old, unused system that has no impact on daily operations. The incident type matters, but the business impact behind it matters more.

---

## Stakeholders and Their Influence

A stakeholder is anyone with an interest in the decisions or activities of an organization. Part of the analyst role involves reporting findings to the right stakeholder at the right level.

| Stakeholder | Focus |
|---|---|
| Cybersecurity risk manager | Identifying, assessing, and mitigating security risks |
| Operations manager | Day to day security operations |
| CEO | Overall organizational direction, rarely contacted directly by entry-level analysts |
| CFO | Financial impact of security incidents |
| CISO | Highest level security oversight |

As an entry-level analyst, direct communication usually happens with operations managers and risk managers, not the CEO or CISO. Those higher level stakeholders care more about the big picture, financial exposure, overall risk posture, while operations managers care more about the immediate, day to day details. For example, reporting multiple failed login attempts to an operations manager might lead them to check with the employee's supervisor and decide whether the account needs to be locked. That information eventually gets summarized and passed further up to CISOs and CFOs, so even without direct contact, an analyst's work still reaches the top of the organization indirectly.

---

## Communicating Effectively with Stakeholders

Good communication with stakeholders comes down to being clear, timely, and appropriately non-technical. Before sending any update, it helps to ask:

- What do I want this person to know?
- Why does it matter to them specifically?
- When do they need to act on it?
- How do I explain this without unnecessary technical jargon?

Every organization has its own accepted communication protocols, whether that is email, chat tools, video calls, or in-person meetings, so learning those norms early avoids friction later. The right channel also depends on the situation itself:

| Situation | Best Channel |
|---|---|
| Simple, quick update | Instant message or phone call |
| Complex, multi part issue | Email or in-person meeting |
| Data heavy findings | Graph, chart, or spreadsheet |

The core idea is matching the message to both the audience and the format. An operations manager needs different detail than a CFO, and a quick anomaly needs a different channel than a detailed audit report.

---

## Visual Dashboards for Communication

Stakeholders are often busy with their own responsibilities, so visuals are one of the fastest ways to communicate findings that involve numbers or trends. A visual dashboard displays multiple pieces of data in one place, using charts, graphs, or infographics.

A dashboard can be as simple as a single chart or as complex as a full set of linked graphs and tables, depending on what story needs to be told. Tools like Google Sheets or Apache OpenOffice are commonly used to build these.

For example, reporting the results of a phishing audit across five departments over five months is far easier to understand as a bar chart comparing click rates than as a paragraph of text describing the same numbers. The visual makes the pattern (which department is most at risk) immediately obvious instead of requiring the reader to piece it together from a written report.

---

## Engaging with the Cybersecurity Community

Security is a fast moving field, so staying engaged with the wider community after finishing a certificate program is part of continuing to grow in the role.

### Ways to Stay Connected

- **Conferences and organizations**: Narrowing down interest first (incident response, forensics, leadership track) makes it easier to search for relevant groups. A simple web search like "incident response cybersecurity conferences in my area" is often enough to get started.
- **LinkedIn**: Useful both for finding organizations and for connecting directly with other professionals, including following CISOs to see the kind of trends and news they share.
- **Mailing lists**: CISA, for example, offers lists covering both general security best practices and weekly summaries of new vulnerabilities.

### A Note on Social Engineering

Ironically, the same social platforms used to build professional connections are also used by attackers. Staying cautious about unexpected links or attachments from unfamiliar accounts applies even while networking professionally.

### Writing a Good Connection Message

A short, clear, and honest message works best when reaching out to a new professional contact:

> "Hi, Tim. I recently completed the Google Cybersecurity Certificate program, and I'd like to connect with other security professionals. It seems like you have a lot of experience in the security industry that I can learn from. Let's keep in touch!"

This works because it states a clear reason for connecting, stays conversational, and does not ask the recipient to do anything suspicious like opening an unexpected file.

---

## Generative AI in Cybersecurity

Generative AI refers to AI systems capable of producing new content such as text, images, or code, based on a prompt. Tools like Gemini, ChatGPT, and Microsoft Copilot fall into this category, and they are increasingly relevant to daily security work.

### Practical Uses in the Field

- **Creating content**, such as generating large sets of fake test data for evaluating security tools.
- **Analyzing information quickly**, such as summarizing long incident reports or meeting transcripts.
- **Answering research questions**, such as explaining common threat types like malware or ransomware.
- **Simplifying routine work**, such as getting a first pass analysis of whether an email looks like phishing.

### Responsible Use Guidelines

- Review AI generated output carefully before trusting or acting on it.
- Disclose when AI was used to produce something.
- Avoid entering sensitive or confidential information into an AI tool.
- Keep a human in the loop. AI should support judgment, not replace it.

The TCREI framework (task, context, references, evaluate, iterate) is a useful way to structure prompts so the output is actually usable. In practice, this looks like clearly stating the task, giving relevant context, providing reference material if available, evaluating what the tool produces, and refining the prompt if the result falls short.

Real world examples from a security professional at Google showed generative AI being used to navigate complex security frameworks, scan code for vulnerabilities and performance issues, suggest code improvements, explain security vulnerabilities and their mitigations, and assist with investigating alerts. The overall theme is that AI reduces time spent on repetitive tasks, which leaves more time for the judgment based work that actually requires a human analyst.

---

## Preparing for Technical Interviews

Technical interviews differ from general interviews by focusing specifically on tool knowledge and hands on concepts rather than just experience or soft skills.

### Topics Likely to Come Up

- **Python**: knowing the basics well enough to explain its use in automating security tasks, and being comfortable enough to whiteboard simple pseudo code if asked.
- **Security frameworks**: familiarity with frameworks like the NIST Cybersecurity Framework (CSF), which provide structured guidelines for managing risk.
- **Network security**: understanding the practice of keeping a network protected from unauthorized access.

A practical tip that stood out here: writing the interview question down before answering. Technical questions often have multiple parts, and rushing to answer quickly can mean missing part of what was actually asked. Taking a moment to write it down keeps the response structured and complete.

### Common Technical Interview Questions

| Question | Short Answer |
|---|---|
| What is the TCP/IP model? | A framework describing how data is organized and transmitted across a network |
| What is the OSI model? | A standardized model describing the seven layers computers use to communicate and send data |
| What are SIEM tools? | Security information and event management tools used to identify and analyze threats, risks, and vulnerabilities |

Being able to answer these clearly, in plain language rather than just reciting a definition, is usually what leaves a good impression in this kind of interview.

---

## Skills Gained

- Classifying data and assets by sensitivity and business impact
- Understanding the structure and purpose of business continuity and disaster recovery plans
- Recognizing when a security issue needs to be escalated and to whom
- Identifying the responsibilities of data owners, controllers, processors, custodians, and DPOs
- Prioritizing incidents based on business impact rather than incident type alone
- Communicating security findings clearly to different levels of stakeholders
- Choosing the right communication channel and format for a given situation
- Building and using visual dashboards to present security data
- Finding and engaging with cybersecurity organizations, conferences, and professionals
- Applying generative AI responsibly to summarize, analyze, and simplify security tasks
- Preparing for and answering common technical interview questions

## Key Learnings and Reflections

- Data and assets are classified by sensitivity, which directly determines how much protection they require.
- Business continuity and disaster recovery plans work together to keep an organization running and recover systems after an incident.
- Escalation is about recognizing which issues need more experienced attention and following the organization's specific policy for doing so.
- Different roles, data owners, controllers, processors, custodians, and DPOs, are each accountable for a different part of how data is protected.
- Prioritizing incidents correctly depends on understanding which assets matter most to the business.
- Clear, audience appropriate communication, supported by visuals when useful, is what makes security findings actually actionable for stakeholders.
- Staying engaged with the wider security community keeps skills and knowledge current after the certificate ends.
- Generative AI is a practical productivity tool for security work, as long as it is used responsibly and with human oversight.
- Technical interviews test both foundational knowledge, like Python and networking models, and the ability to explain concepts clearly under pressure.

## Conclusion

This course was less about writing code and more about understanding how a security analyst actually operates inside a real organization. It connected classification, escalation, and communication into one continuous thread: data gets classified so its risk is understood, incidents get escalated based on that understanding, the right roles get involved depending on what kind of data or system is affected, and stakeholders get informed in a way that matches both their role and their level of urgency. Layered on top of that is the reality of continuing to grow after the certificate ends, through community engagement, responsible use of generative AI tools, and being ready to demonstrate technical knowledge in an interview setting. Altogether, this course was the bridge between learning security concepts and actually being ready to apply them inside a real job.
