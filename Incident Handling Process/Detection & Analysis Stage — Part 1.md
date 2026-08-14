# Detection & Analysis Stage — Part 1

## Overview

The **Detection & Analysis** stage focuses on identifying potential security incidents, collecting initial context, validating suspicious activity, and determining the incident’s scope and severity.

This stage uses security telemetry, technical tools, trained personnel, threat intelligence, and knowledge-sharing processes. Effective detection also depends on network visibility, segmented architecture, and an understanding of normal system behavior.

---

## Sources of Detection

Threats can enter an organization through many attack vectors. Detection may originate from people, internal security controls, proactive investigations, or external notifications.

| Detection Source | Example |
|---|---|
| Employee report | A user notices suspicious pop-ups, unexpected MFA prompts, or unusual account activity |
| Security tools | Alerts from EDR, IDS/IPS, firewall, antivirus, SIEM, or email-security platforms |
| Threat hunting | Analysts proactively identify suspicious patterns not detected by automated rules |
| Third-party notification | A vendor, customer, security researcher, or external organization reports signs of compromise |

A third-party vendor can be a valid source of compromise detection. For example, a vendor may discover leaked credentials, malicious traffic, or abused access associated with the organization.

---

## Detection Layers

Organizations should build multiple detection layers rather than depending on a single security tool.

| Layer | Purpose | Examples |
|---|---|---|
| Network perimeter | Detect and block external threats before they enter the environment | Firewalls, internet-facing IDS/IPS, DMZ monitoring |
| Internal network | Identify suspicious activity moving between internal systems | Local firewalls, internal IDS/IPS, network monitoring |
| Endpoint | Detect malicious activity on user workstations and servers | Antivirus, EDR, host-based IDS/IPS |
| Application | Identify abuse, errors, and suspicious activity in services and applications | Application logs, web-server logs, database logs, service logs |

Defense in depth improves resilience. If one layer fails to identify attacker activity, another layer may provide the alert or evidence needed for investigation.

---

## Initial Investigation

When suspicious activity is detected, responders should perform an initial investigation before launching a broad organizational response.

The main objective is to establish context and avoid making incorrect assumptions from incomplete data.

For example, an alert stating that an administrative account connected to an IP address at a specific time may be harmless or severe depending on:

- The identity of the account
- The system associated with the IP address
- The system owner and business purpose
- The applicable time zone
- Whether the event is expected behavior
- Whether the activity is ongoing

### Initial Information Checklist

Responders should collect and document:

- Date and time the incident was reported
- Person or system that detected the activity
- Detection method, such as an EDR alert, user report, or SIEM correlation rule
- Incident type, such as phishing, malware, account compromise, or service unavailability
- Potentially impacted systems, accounts, applications, and users
- Actions already taken by administrators or responders
- Whether suspicious activity is ongoing or has stopped
- Hostnames, IP addresses, operating systems, physical locations, and system owners
- The purpose and current state of affected systems
- Malware details, malicious file copies, hashes, detection time, and affected hosts
- Relevant network indicators, including IP addresses and domains

---

## Context Determines Priority

The same technical alert can require different response actions depending on the affected asset.

| Scenario | Likely Priority |
|---|---|
| Malware alert on a non-critical training workstation | Lower priority, while still requiring investigation |
| Malware alert on a finance server | High priority because of sensitive data and business impact |
| Suspicious activity on a CEO laptop | High priority because of executive access, sensitive communications, and likely attacker value |
| Unauthorized access to a production database | Critical priority because of potential service disruption and data exposure |

Incident priority should reflect both the technical evidence and the business impact.

---

## Building an Incident Timeline

An incident timeline organizes evidence in chronological order and gives responders a clearer picture of attacker behavior.

During an investigation, evidence may be found out of sequence. A timeline helps investigators place separate observations into context and determine whether newly discovered events are connected to the current incident.

### Recommended Timeline Fields

| Field | Description |
|---|---|
| Date | Date on which the event occurred |
| Time | Event time, including the applicable time zone |
| Hostname | System associated with the event |
| Event description | Clear description of the observed activity |
| Data source | Source that recorded or reported the activity |

### Example Timeline Entry

| Date | Time | Hostname | Event Description | Data Source |
|---|---|---|---|---|
| 2021-09-09 | 13:31 CET | `SQLServer01` | Mimikatz tool detected on the host | Antivirus software |

Timelines should focus on attacker behavior and relevant responder actions, including:

- Initial access attempts
- Malware execution
- Authentication events
- Network connections
- File downloads
- Privilege escalation
- Lateral movement
- Command-and-control communications
- Containment actions
- Evidence-discovery points

---

## Case Management

A case-management platform helps incident responders organize alerts, evidence, tasks, ownership, and findings.

In the lesson lab, **TheHive** is used to review an alert, assign it to an analyst, create a case, add investigative details, document findings, record lessons learned, and close the case after the investigation is complete.

A good case record should include:

- Alert details and data sources
- Incident classification and severity
- Assigned responders
- Affected assets and users
- Observed indicators of compromise
- Investigation notes and evidence
- Containment and remediation actions
- Final findings and lessons learned

---

## Incident Severity and Extent

Responders should assess both the severity and the extent of an incident before deciding how to escalate and respond.

### Severity and Scope Questions

- What is the exploitation impact?
- What requirements are needed to exploit the issue?
- Can business-critical systems be affected?
- Are remediation steps available?
- How many systems are impacted?
- Is the exploit being used in the wild?
- Does the exploit have worm-like capabilities?

High-impact incidents, incidents affecting many systems, and active attacks against business-critical assets should be handled and escalated quickly.

Evidence that an exploit is actively used in the wild or has worm-like behavior can indicate a higher risk and greater urgency.

---

## Confidentiality and Communication

Security incidents are sensitive and should be handled on a need-to-know basis unless legal requirements or management decisions require broader disclosure.

Confidentiality matters because:

- The adversary may be an internal employee or contractor
- Public disclosure may create legal, financial, or reputational consequences
- Attackers may learn about response actions if information is shared improperly
- Notifications to affected parties may be regulated
- Legal teams may need to preserve evidence and guide communications

Communication with internal and external stakeholders should be coordinated through designated personnel, management, and legal teams when appropriate.

---

## Investigation Expectations

At the beginning of an investigation, responders should set reasonable expectations about:

- The suspected incident type
- Available evidence sources
- The expected investigation duration
- The expected impact and affected systems
- Whether attribution is feasible
- What response actions may be required

These expectations may change as new evidence is discovered. Incident responders should keep relevant stakeholders and management informed about important findings, changing scope, and updated response plans.

---

## Example Workflow

A SIEM generates an alert for suspicious credential-dumping behavior on a database server.

1. The analyst confirms the alert source, detection time, host, account, and applicable time zone.
2. The analyst checks whether the server is business-critical and determines its owner and purpose.
3. The team reviews endpoint, authentication, network, and application logs.
4. The alert is assigned in the case-management platform and converted into an investigation case.
5. The team records each finding in an incident timeline.
6. Responders identify whether other hosts show similar behavior.
7. The incident severity is assessed based on affected systems, exploitation impact, and attacker activity.
8. The incident is escalated to the appropriate response team and management stakeholders.
9. All sensitive information is shared only with authorized personnel.

---

## Key Takeaways

- Detection can begin with employees, security controls, threat hunting, or third-party notifications.
- Layered detection should include the network perimeter, internal network, endpoints, and applications.
- Initial triage must establish context before incident responders make major decisions.
- Incident timelines organize evidence chronologically and clarify attacker behavior.
- A case-management platform helps teams track ownership, evidence, tasks, response actions, and lessons learned.
- Severity depends on technical impact, business importance, exploitability, number of affected assets, and active attacker behavior.
- Incident information should be protected and shared only on a need-to-know basis.
- Investigation expectations should be communicated clearly and updated as new evidence changes the scope of the incident.

---

## References

- [NIST SP 800-61 Rev. 2 — Computer Security Incident Handling Guide](https://csrc.nist.gov/pubs/sp/800/61/r2/final)
- [MITRE ATT&CK Enterprise Matrix](https://attack.mitre.org/matrices/enterprise/)
- [TheHive Project](https://thehive-project.org/)
- LinkedIn Learning — *Incident Handling Process: Cybersecurity Labs Powered by Hack The Box*, “Detection & Analysis Stage (Part 1)”
