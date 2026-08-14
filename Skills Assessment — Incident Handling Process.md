# Skills Assessment — Incident Handling Process

## Overview

This skills assessment places the learner in the role of a **junior incident responder** investigating alerts related to the fictional **Insight Nexus breach**.

The assessment combines case management, alert triage, enrichment, threat-intelligence validation, MITRE ATT&CK mapping, Cyber Kill Chain analysis, and log investigation.

> **Ethical use note:** This repository documents the assessment methodology and learning outcomes. It intentionally excludes answer keys, active target IP addresses, credentials, access links, and challenge-specific indicators.

---

## Assessment Objectives

The assessment validates practical skills across three areas:

| Area | Skills Practiced |
|---|---|
| Alert triage | Reviewing alerts, identifying relevant information, prioritizing findings, and creating an investigation case |
| Threat intelligence | Enriching suspicious IP addresses and artifacts with VirusTotal or comparable intelligence sources |
| Attack mapping | Connecting observed attacker behavior to the Cyber Kill Chain and MITRE ATT&CK |
| Log analysis | Reviewing Wazuh-exported logs, decoding suspicious PowerShell activity, and extracting IOCs |
| Incident documentation | Recording findings, evidence, comments, observables, and investigation notes in a case-management platform |

---

## Lab Environment

The assessment uses a controlled Hack The Box environment and a TheHive instance populated with alerts related to the Insight Nexus breach scenario.

### Main Tools

| Tool | Purpose |
|---|---|
| TheHive | Alert triage, case creation, observable tracking, note-taking, and case documentation |
| Cortex | Observable enrichment and analysis integrations |
| VirusTotal | Reputation, file-reference, and WHOIS enrichment for suspicious infrastructure |
| Wazuh | Security-event collection, alerting, and exported log analysis |
| Pwnbox or VPN | Access to the isolated lab environment |

### Safe Handling Rules

- Use only the targets, accounts, and tools authorized by the training environment.
- Do not reuse challenge infrastructure, credentials, or indicators outside the lab.
- Do not publish credentials, VPN configuration files, target addresses, or screenshots containing sensitive lab information.
- Do not post solution answers publicly if the course expects independent completion.
- Keep GitHub documentation focused on methodology, notes, and learning outcomes.

---

## Assessment Workflow

```text
Review Alerts
      ↓
Create a Case
      ↓
Link Related Alerts
      ↓
Triage and Enrich Observables
      ↓
Correlate Findings
      ↓
Map Activity to ATT&CK and Kill Chain
      ↓
Analyze Logs and Extract IOCs
      ↓
Document Evidence and Conclusions
```

The key objective is not to treat each alert independently. Analysts should correlate related events and determine whether they belong to a shared incident.

---

## Part 1: Alert Triage in TheHive

The first assessment area focuses on creating and managing an incident case from available alerts.

### Core Tasks

- Review the alerts available in TheHive.
- Identify alerts associated with the Insight Nexus breach scenario.
- Create a new incident case.
- Link relevant alerts to the case.
- Assign ownership and severity based on available evidence.
- Add notes explaining why each alert is relevant.
- Document observables such as IP addresses, domains, hashes, users, and file names.
- Record evidence that supports correlations between alerts.

### Triage Considerations

When evaluating alerts, analysts should consider:

- Is the alert related to the known breach scenario?
- Which host, user, source IP, destination IP, process, or artifact is involved?
- Is the activity expected or suspicious?
- Does the alert indicate initial access, persistence, credential access, lateral movement, command and control, collection, or exfiltration?
- Does the activity match other alerts by time, asset, user, IP address, or technique?
- What is the likely business impact if the alert is confirmed?

### Useful Case Fields

| Field | Example Content |
|---|---|
| Case title | Short descriptive incident name |
| Severity | Low, medium, high, or critical |
| TLP/PAP | Information-sharing and handling classification |
| Description | Initial summary of suspected malicious activity |
| Affected assets | Hostnames, servers, users, applications, or data stores |
| Observables | IP addresses, domains, URLs, hashes, file paths, accounts |
| Timeline | Chronological record of evidence and response actions |
| Tasks | Investigation, enrichment, containment, and documentation work |
| Notes | Analyst conclusions, assumptions, and validation results |

---

## Part 2: Enrichment and Correlation

The assessment requires enriching suspicious network indicators and correlating alert evidence.

### IP Address Enrichment

When a suspicious public IP address is identified, an analyst can use a threat-intelligence platform such as VirusTotal to evaluate it.

Relevant enrichment data may include:

- Reputation or detection ratio
- Associated malicious files
- Passive DNS data
- Historical resolutions
- Associated domains
- WHOIS information
- Hosting provider or ASN
- Geographic information
- Community comments
- Observed malicious behavior

### Validation Principles

Threat intelligence should support, not replace, investigation.

An IP address may be malicious, suspicious, benign, shared, dynamic, or part of cloud infrastructure. Analysts should validate intelligence findings against internal evidence such as firewall logs, proxy logs, EDR telemetry, authentication events, and endpoint network connections.

### Correlation Questions

- Which alerts share the same source or destination IP address?
- Did suspicious network traffic occur near unusual authentication activity?
- Is the same host associated with malware, a suspicious process, or external connections?
- Are there related events involving privileged accounts?
- Do timestamps indicate a realistic attack sequence?
- Are multiple alerts part of one intrusion or separate events?

---

## Part 3: Cyber Kill Chain Mapping

The assessment presents an attack scenario involving a user opening an attachment, malware execution, persistence, DLL loading, and credential exfiltration.

### Example Attack Sequence

```text
Malicious Attachment Opened
        ↓
Downloader Executes
        ↓
Executable Written to User Profile Directory
        ↓
Run Registry Key Created
        ↓
Suspicious Tool Loads a DLL
        ↓
Credentials Exfiltrated to External Infrastructure
```

### Cyber Kill Chain Mapping Guide

| Observed Activity | Likely Kill Chain Phase |
|---|---|
| Malicious attachment reaches the user | Delivery |
| User opens attachment and downloader executes | Exploitation |
| Malware is written to disk | Installation |
| Registry Run key is created | Installation / Persistence |
| Malware communicates with remote infrastructure | Command and Control |
| Credentials are stolen and sent externally | Actions on Objectives |

The Cyber Kill Chain is useful for understanding the attacker’s overall progression, but it should be supplemented with MITRE ATT&CK for detailed behavioral analysis.

---

## Part 4: MITRE ATT&CK Mapping

MITRE ATT&CK provides specific technique IDs for adversary behavior observed during the assessment.

### Mapping Method

1. Identify the observable action.
2. Determine the attacker’s objective.
3. Search the MITRE ATT&CK knowledge base for the corresponding technique.
4. Validate the technique description against the evidence.
5. Document the technique ID, technique name, evidence source, and affected assets.

### Example Mapping Table

| Behavior | ATT&CK Tactic | Possible Technique Category |
|---|---|---|
| Downloading additional tools from attacker infrastructure | Command and Control | Ingress tool transfer |
| Creating a Registry Run key | Persistence | Registry Run Keys / Startup Folder |
| Loading a DLL through a suspicious process or utility | Defense Evasion / Execution | Depends on the observed loading method |
| Credential theft | Credential Access | Depends on the credential-access mechanism |
| Sending stolen credentials to an external destination | Exfiltration | Exfiltration over a web service or C2 channel |

> Always validate the exact technique ID against the observed evidence. Similar-looking behaviors can map to different ATT&CK techniques depending on the process, protocol, operating system, and attacker method.

---

## Part 5: Wazuh Log Investigation

The final tasks use exported Wazuh logs to investigate suspicious PowerShell activity.

### Investigation Objectives

- Locate suspicious PowerShell execution events.
- Identify encoded or obfuscated command content.
- Decode the command safely in an isolated environment.
- Extract indicators of compromise.
- Identify the account that executed the command.
- Document the command line, hostname, timestamp, user, process context, and related network indicators.

### Evidence to Record

| Evidence Field | Why It Matters |
|---|---|
| Timestamp and time zone | Supports timeline reconstruction |
| Hostname | Identifies the affected asset |
| User account | Identifies the execution context |
| Parent process | Shows how PowerShell was launched |
| Full command line | Supports decoding and behavioral analysis |
| Encoded content | May reveal hidden commands, URLs, or payloads |
| IP addresses and domains | Can be searched across security tools as IOCs |
| Process IDs | Supports process-tree correlation |
| File paths | Helps identify payload location and persistence |
| Event ID and log source | Supports evidence validation and repeatable hunting |

### Safe PowerShell Decoding Workflow

Encoded PowerShell commands are often Base64-encoded using UTF-16LE.

Example decoding approach:

```powershell
$encoded = "<base64-value>"
[Text.Encoding]::Unicode.GetString(
    [Convert]::FromBase64String($encoded)
)
```

Use a controlled analysis environment. Do not execute decoded commands from suspicious logs, even if they appear harmless.

### Linux Alternative

A Base64 string can also be decoded from Linux, but the character encoding must be handled correctly:

```bash
echo '<base64-value>' | base64 -d | iconv -f UTF-16LE -t UTF-8
```

This command decodes the text only. It does **not** execute the decoded PowerShell command.

---

## IOC Documentation Template

Use a structured record for each indicator discovered during the assessment.

```markdown
### Indicator Record

- **Indicator type:** IP address / domain / hash / file path / user account
- **Indicator value:** `<redacted>`
- **Source:** Wazuh log / TheHive alert / endpoint telemetry / threat intelligence
- **Observed date and time:** `<timestamp>`
- **Affected host:** `<hostname>`
- **Associated user:** `<domain\\user>`
- **Related process:** `<process name>`
- **Assessment:** Malicious / suspicious / benign / unknown
- **Related MITRE ATT&CK technique:** `<technique ID>`
- **Validation notes:** `<reasoning and corroborating evidence>`
- **Response action:** Blocked / monitored / escalated / remediated
```

---

## Suggested Investigation Notes

A high-quality case note should distinguish observations from conclusions.

```markdown
### Observation
A PowerShell process executed with an encoded command-line argument on a workstation.

### Evidence
- Host: `<hostname>`
- User: `<domain\\user>`
- Timestamp: `<timestamp>`
- Log source: Wazuh / Windows PowerShell / Sysmon
- Parent process: `<parent process>`
- Destination indicator: `<redacted IOC>`

### Analysis
The encoded command should be decoded without execution and compared against known malicious behaviors. Related activity should be searched across endpoint, DNS, proxy, firewall, and authentication logs.

### Next Steps
- Search for the IOC across the environment.
- Review process-tree and network telemetry.
- Determine whether persistence was established.
- Assess whether credentials or data were accessed.
- Update the incident timeline and ATT&CK mapping.
```

---

## Key Takeaways

- Case management organizes alerts, observables, evidence, findings, tasks, and response decisions.
- Alert triage requires context; a single low-priority alert can become critical when correlated with related evidence.
- Threat-intelligence enrichment must be validated against internal telemetry.
- The Cyber Kill Chain provides a high-level model for understanding attacker progression.
- MITRE ATT&CK provides detailed techniques for documenting observed adversary behavior.
- Encoded PowerShell should be decoded for analysis but never executed in an untrusted environment.
- Every extracted IOC should include source context, timestamp, affected host, user, assessment, and response action.
- Good documentation supports containment, eradication, recovery, reporting, and future threat hunting.

---

## References

- [MITRE ATT&CK Enterprise Matrix](https://attack.mitre.org/matrices/enterprise/)
- [NIST SP 800-61 Rev. 2 — Computer Security Incident Handling Guide](https://csrc.nist.gov/pubs/sp/800/61/r2/final)
- [TheHive Project Documentation](https://docs.strangebee.com/thehive/)
- [Wazuh Documentation](https://documentation.wazuh.com/)
- [VirusTotal Documentation](https://docs.virustotal.com/)
- LinkedIn Learning — *Incident Handling Process: Cybersecurity Labs Powered by Hack The Box*, “Skills Assessment”
