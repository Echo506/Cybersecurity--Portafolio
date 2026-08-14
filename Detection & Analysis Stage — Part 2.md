# Detection & Analysis Stage — Part 2

## Overview

The purpose of an incident investigation is to determine **what happened**, **how it happened**, and **what systems or accounts were affected**.

Simply rebuilding an affected system without understanding the compromise can leave the original attack path available to the adversary. A thorough investigation allows the response team to remove the attacker’s access, eliminate persistence, remediate the root cause, and prevent the same technique from being used again.

---

## The Investigation Cycle

Incident investigations begin with limited initial evidence and expand as analysts discover additional information.

The investigation follows a continuous three-step cycle:

```text
Initial Investigation Data
            ↓
Creation and Use of IOCs
            ↓
Identification of New Leads and Impacted Systems
            ↓
Data Collection and Analysis
            ↓
New Leads, New IOCs, and Timeline Updates
            ↺
```

| Step | Objective |
|---|---|
| Create and use IOCs | Convert known malicious artifacts into searchable indicators |
| Identify new leads and affected systems | Find additional hosts, accounts, files, or connections related to the incident |
| Collect and analyze data | Preserve and examine evidence to answer investigative questions and discover new leads |

This cycle repeats until responders have sufficient confidence in the scope, attacker activity, and remediation plan.

---

## Initial Investigation Data

An investigation should be based on validated leads collected from the initial alert and from evidence discovered throughout the response process.

Analysts should avoid focusing only on a single known malicious tool or artifact. Narrowing the investigation too early can lead to incomplete findings, premature conclusions, and missed compromised systems.

Instead, responders should continuously ask:

- What evidence supports this finding?
- What other systems may contain similar artifacts?
- Which users, processes, services, or network connections are related?
- Could this indicator be a false positive?
- What additional logs or forensic data can confirm the activity?

---

## Indicators of Compromise

An **Indicator of Compromise (IOC)** is an artifact or sign that indicates a possible or confirmed security incident.

Common IOC types include:

| IOC Type | Examples |
|---|---|
| File hashes | MD5, SHA-1, SHA-256 |
| File artifacts | File names, file paths, file sizes, digital signatures |
| Network indicators | IP addresses, domains, URLs, user-agent strings |
| Host indicators | Registry keys, services, scheduled tasks, mutexes |
| Email indicators | Sender addresses, attachment hashes, message headers |
| Identity indicators | Suspicious accounts, authentication attempts, abnormal login patterns |

A malicious file hash is commonly treated as an IOC because it helps analysts search for the same file across endpoints, logs, security tools, and threat-intelligence platforms.

> IOCs are useful for locating known malicious artifacts, but they should be combined with behavioral evidence because attackers can change file names, hashes, IP addresses, and domains.

---

## IOC Standards and Tools

IOCs should be documented in structured formats so they can be shared, searched, and processed consistently.

| Standard or Tool | Purpose |
|---|---|
| OpenIOC | XML-based framework for documenting and sharing indicators |
| YARA | Rule-based language for identifying malware and suspicious file characteristics |
| STIX | Structured Threat Information Expression; a machine-readable format for cyber-threat intelligence |
| Mandiant IOC Editor | Tool used to create and edit IOC files |
| TheHive observables | Case-management field used to store and investigate indicators associated with alerts or cases |

STIX is commonly represented in JSON and supports standardized exchange of threat-intelligence data between organizations and security tools.

---

## Searching for IOCs

After identifying IOCs, responders search for them across the environment to identify potentially affected systems.

Possible search locations include:

- Endpoint detection and response platforms
- SIEM platforms
- Antivirus logs
- Windows event logs
- Firewall, proxy, and DNS logs
- File shares
- Email-security platforms
- Threat-intelligence platforms
- Case-management tools such as TheHive

In Windows environments, analysts may use tools such as **Windows Management Instrumentation (WMI)** or **PowerShell** to perform IOC searches at scale.

### Privileged Credential Safety

Responders must avoid exposing or caching privileged credentials on potentially compromised systems.

When remotely accessing a suspect system:

- Use approved tools and protocols that reduce the risk of credential caching.
- Understand how each remote-administration tool authenticates.
- Use least-privilege accounts whenever possible.
- Avoid unnecessary interactive logons to compromised systems.
- Monitor and document all remote-access activity.

For example, Windows **network logons** are commonly associated with logon type 3. The way a tool is used can change the evidence it leaves behind and whether credentials are exposed or cached on the remote system.

---

## New Leads and Impacted Systems

IOC searches may identify additional systems with matching artifacts. However, a match does not automatically confirm compromise.

Possible issues include:

- Generic indicators that produce many matches
- Benign files or tools with similar names
- Old artifacts no longer related to active malicious activity
- Shared infrastructure or common network traffic
- Duplicate alerts from the same event

Responders should validate each hit, eliminate false positives, and prioritize systems most likely to produce meaningful new evidence.

Priority can be based on:

- Business criticality
- Privileged access
- Active attacker activity
- Evidence of lateral movement
- Sensitive-data exposure
- Potential to reveal additional compromised systems

Suspicious lateral movement toward systems owned by another department should be escalated internally. Organizational ownership does not remove the need to coordinate response actions when a security incident may affect that department.

---

## Evidence Collection

Once potentially impacted systems are identified, responders must collect and preserve relevant evidence.

Two common approaches are:

| Collection Method | Description | Consideration |
|---|---|---|
| Live response | Collecting data while the system remains powered on | Preserves volatile information such as running processes, connections, and memory-resident artifacts |
| Offline analysis | Shutting down or isolating a system before collecting and analyzing data | May preserve disk state but can destroy volatile memory evidence |

Live response is frequently used because volatile evidence can disappear when a system is shut down.

### Common Evidence Sources

- Memory captures
- Running processes and process trees
- Network connections
- Logged-in users
- Open files
- Scheduled tasks
- Services
- Registry artifacts
- Browser history
- Event logs
- EDR telemetry
- File-system metadata
- Disk images

During collection, analysts should minimize interaction with the system to avoid changing, overwriting, or destroying evidence.

---

## Evidence Analysis

Evidence analysis is often one of the most time-consuming parts of incident response.

Common examination activities include:

- Malware analysis
- Disk forensics
- Memory forensics
- Log analysis
- Authentication analysis
- Network traffic analysis
- Timeline reconstruction
- Review of attacker tools and persistence mechanisms

Validated findings should be added to the incident timeline. New malicious artifacts can become additional IOCs, which restart the investigation cycle.

Memory forensics is particularly valuable during advanced incidents because malware, injected code, encryption keys, credentials, network connections, and malicious processes may exist only in memory.

---

## Chain of Custody

A **chain of custody** is a documented record showing how evidence was collected, handled, transferred, stored, and analyzed.

It supports evidence integrity and may be essential if the organization pursues legal action.

A chain-of-custody record should document:

- Evidence identifier
- Description of the evidence
- Source system or location
- Date and time of collection
- Collector name
- Hash values used to validate integrity
- Storage location
- Every transfer of possession
- Actions performed during analysis

Example record:

| Evidence ID | Item | Collected By | Date and Time | Integrity Verification |
|---|---|---|---|---|
| E-001 | Memory image from `WS-023` | Incident Response Analyst | 2026-08-14 01:20 CST | SHA-256 hash recorded |

---

## AI in Threat Detection

Artificial intelligence can support security teams by analyzing large quantities of alerts, logs, and incident data.

Potential AI-assisted use cases include:

- Automated alert triage and prioritization
- Correlation of related alerts
- Attack-story generation
- Timeline reconstruction
- Identification of anomalous behavior
- Suggested response playbooks
- Investigation summarization
- Post-incident analysis and lessons learned

AI can reduce the time needed to review high alert volumes, but analysts must validate its findings before containment or remediation actions are taken.

AI should support—not replace—human judgment, evidence validation, and incident-response decision-making.

---

## Example Investigation Workflow

A security tool detects a suspicious DLL on an endpoint.

1. The analyst records the file name, path, host, detection time, user context, and hash values.
2. The MD5 and SHA-256 hashes are added as IOCs in the incident case.
3. The analyst searches EDR, SIEM, and endpoint logs for the same hashes, file path, domains, and process behavior.
4. Multiple endpoints generate IOC matches.
5. The team validates which matches are malicious and removes false positives.
6. Analysts collect live-response data from priority systems before volatile evidence is lost.
7. Memory, disk, process, network, and event-log artifacts are analyzed.
8. New findings are added to the incident timeline and converted into new IOCs.
9. The process repeats until the team identifies the attack path, affected systems, persistence mechanisms, and required remediation actions.

---

## Key Takeaways

- Effective investigations determine what happened, how it happened, and what assets were affected.
- Incident investigations are iterative: IOCs lead to new systems, new data collection, new analysis, and new IOCs.
- An IOC is a structured artifact that indicates a possible or confirmed compromise.
- Common IOCs include file hashes, IP addresses, domains, file names, registry keys, services, and scheduled tasks.
- IOC matches must be validated because generic indicators can produce false positives.
- Analysts should protect privileged credentials when connecting to suspect systems and understand how their tools authenticate.
- Live response preserves volatile evidence, while shutting down a system can destroy important memory artifacts.
- Evidence collection should minimize changes to the affected system and maintain a documented chain of custody.
- AI can accelerate triage, alert correlation, timeline reconstruction, and post-incident learning, but humans must validate findings and make final response decisions.

---

## References

- [NIST SP 800-61 Rev. 2 — Computer Security Incident Handling Guide](https://csrc.nist.gov/pubs/sp/800/61/r2/final)
- [MITRE ATT&CK Enterprise Matrix](https://attack.mitre.org/matrices/enterprise/)
- [STIX Version 2.1 Specification](https://docs.oasis-open.org/cti/stix/v2.1/stix-v2.1-part1-stix-core.html)
- [YARA Documentation](https://yara.readthedocs.io/)
- [TheHive Project](https://thehive-project.org/)
- LinkedIn Learning — *Incident Handling Process: Cybersecurity Labs Powered by Hack The Box*, “Detection & Analysis Stage (Part 2)”
