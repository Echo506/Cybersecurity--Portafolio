# Cyber Kill Chain and MITRE ATT&CK

## Overview

This lesson explains how attackers progress through an intrusion and how defenders can use structured frameworks to investigate, detect, and disrupt malicious activity.

The **Cyber Kill Chain** provides a high-level view of an attack lifecycle, while **MITRE ATT&CK** provides a more detailed catalog of adversary tactics and techniques. Together, these frameworks help incident responders understand what happened, estimate what an attacker may do next, and prioritize containment actions.

---

## Learning Objectives

- Understand the seven stages of the Cyber Kill Chain
- Identify common attacker activities at each stage
- Differentiate between MITRE ATT&CK tactics, techniques, and sub-techniques
- Understand the Pyramid of Pain and why behavioral detections are valuable
- Recognize how MITRE ATT&CK can support incident case management and alert triage

---

## Cyber Kill Chain

The Cyber Kill Chain is a model that describes the stages an attacker may follow during a cyberattack.

> Important: attackers do not always operate in a linear sequence. After gaining access, they may repeat reconnaissance, delivery, or exploitation activities to move deeper into the environment.

| Stage | Description | Common Examples |
|---|---|---|
| 1. Reconnaissance | The attacker gathers information about a target before attempting access. | OSINT, social media research, job postings, DNS lookups, port scanning |
| 2. Weaponization | The attacker creates or prepares malware, exploits, or payloads. | Malware development, exploit preparation, malicious documents |
| 3. Delivery | The payload is sent or made available to the victim. | Phishing emails, malicious links, compromised websites, USB devices |
| 4. Exploitation | A vulnerability is triggered or malicious code is executed. | Exploiting a web application, macro execution, vulnerable software abuse |
| 5. Installation | Malware or persistence mechanisms are placed on the compromised host. | Droppers, backdoors, rootkits, scheduled tasks, malicious services |
| 6. Command and Control | The attacker establishes remote communication with the compromised system. | Beaconing, remote shells, malicious web traffic, C2 servers |
| 7. Actions on Objectives | The attacker performs their final goal within the environment. | Data exfiltration, ransomware deployment, credential theft, sabotage |

### Defensive Goal

The goal of incident response is to stop the attacker as early as possible in the kill chain.

Early detection during reconnaissance, delivery, or exploitation can prevent the attacker from establishing persistence, moving laterally, or affecting critical systems.

---

## Stage Details

### Reconnaissance

During reconnaissance, attackers collect information about the organization, employees, technologies, and exposed assets.

Information may be collected passively through public sources, such as:

- Company websites
- Social media platforms
- Public documentation
- Job advertisements
- Technology partner information

Attackers may also conduct active reconnaissance by scanning public IP addresses, web applications, domains, and exposed services.

### Weaponization

Weaponization involves preparing malware or an exploit for initial access.

Attackers may customize payloads to avoid security controls such as antivirus or endpoint detection and response solutions. The payload may be designed to provide remote access, persistence, or the ability to download additional tools.

### Delivery

Delivery is the process of getting the payload to the victim or target system.

Common delivery methods include:

- Phishing messages with malicious attachments
- Links to attacker-controlled websites
- Credential-harvesting pages
- Social-engineering phone calls
- Removable media such as USB devices

### Exploitation

Exploitation occurs when the malicious payload is activated or a vulnerability is successfully abused.

The attacker attempts to execute code, gain access, or take control of a system.

### Installation

During installation, the attacker establishes malware or persistence on the compromised system.

Common installation mechanisms include:

- **Droppers:** Small programs that install and execute malware
- **Backdoors:** Tools that provide continued unauthorized access
- **Rootkits:** Malware designed to hide its presence from users and security tools

### Command and Control

Command and Control, often called **C2**, is the communication channel between an attacker and a compromised host.

It allows attackers to issue commands, maintain remote access, download tools, and control infected machines. Advanced threat actors often use multiple tools or fallback methods to retain access if one channel is detected.

### Actions on Objectives

This is the final stage, where attackers attempt to achieve their objective.

Possible objectives include:

- Exfiltrating sensitive information
- Stealing credentials
- Moving laterally through the network
- Escalating privileges
- Deploying ransomware
- Disrupting business operations

---

## MITRE ATT&CK Framework

MITRE ATT&CK is a knowledge base that documents real-world adversary behavior across enterprise environments, including Windows, Linux, macOS, cloud systems, network devices, and mobile platforms.

Unlike the Cyber Kill Chain, MITRE ATT&CK provides a more granular view of attacker behavior through a matrix of tactics and techniques.

### Key Terms

| Term | Meaning |
|---|---|
| **Tactic** | The attacker’s high-level objective or goal |
| **Technique** | A specific method used to achieve that objective |
| **Sub-technique** | A more detailed implementation of a technique |

### Examples

| Tactic | Technique | ID | Example |
|---|---|---|---|
| Initial Access | Exploit Public-Facing Application | T1190 | Exploiting a vulnerable internet-facing application |
| Execution | Command and Scripting Interpreter: PowerShell | T1059.001 | Running PowerShell commands to download or execute payloads |
| Persistence | Create or Modify System Process: Windows Service | T1543.003 | Creating a malicious Windows service |
| Credential Access | OS Credential Dumping: LSASS Memory | T1003.001 | Extracting credentials from LSASS memory |
| Lateral Movement | Remote Services: Remote Desktop Protocol | T1021.001 | Moving to another host through RDP |
| Impact | Data Encrypted for Impact | T1486 | Encrypting data during a ransomware attack |

---

## Why ATT&CK Matters in Incident Response

MITRE ATT&CK helps analysts move from a vague alert to a clear description of attacker behavior.

For example:

```text
Generic finding:
Suspicious activity detected on a Windows endpoint

MITRE-mapped finding:
T1003.001 — OS Credential Dumping: LSASS Memory
```

The second finding is more useful because it explains the behavior, supports investigation, and helps analysts identify related activity such as privilege escalation, lateral movement, or credential abuse.

MITRE ATT&CK can support:

- Alert triage and prioritization
- Threat hunting
- Detection engineering
- Incident reporting
- Threat intelligence analysis
- Containment and eradication planning
- Security-control gap assessments

---

## Pyramid of Pain

The Pyramid of Pain explains how difficult it is for an attacker to adapt when defenders detect and block different types of indicators.

| Indicator Type | Attacker Effort to Change | Defensive Value |
|---|---:|---:|
| Hash values | Low | Low |
| IP addresses | Low | Low |
| Domain names | Low to medium | Moderate |
| Network and host artifacts | Medium | High |
| Tools | High | High |
| Tactics, Techniques, and Procedures (TTPs) | Very high | Very high |

### Key Takeaway

Blocking a malicious IP address or file hash can be useful, but attackers can often replace those indicators quickly.

Detecting **behavioral patterns** based on TTPs is more effective because it forces attackers to change how they operate. Examples include detecting suspicious PowerShell execution, process injection, credential dumping, or abnormal remote-service use.

---

## Cyber Kill Chain vs. MITRE ATT&CK

| Aspect | Cyber Kill Chain | MITRE ATT&CK |
|---|---|---|
| Purpose | Describes the overall lifecycle of an attack | Describes detailed adversary behavior |
| Detail level | High-level | Granular |
| Structure | Seven sequential stages | Matrix of tactics and techniques |
| Best use | Understanding attacker progression | Detection, investigation, hunting, and reporting |
| Example | Delivery or Command and Control | T1059.001 PowerShell or T1003.001 LSASS Memory |

These frameworks complement each other:

- Use the **Cyber Kill Chain** to understand where an attacker is in the broader intrusion lifecycle.
- Use **MITRE ATT&CK** to identify the specific behaviors, techniques, and possible next steps.

---

## Incident Response Application

During an investigation, an analyst can map alerts and evidence to the Cyber Kill Chain and MITRE ATT&CK.

Example workflow:

1. Identify the alert and affected assets.
2. Determine the possible Cyber Kill Chain stage.
3. Map observed activity to relevant MITRE ATT&CK techniques.
4. Investigate related hosts, users, processes, network connections, and logs.
5. Contain the affected systems and remove attacker persistence.
6. Document findings using ATT&CK IDs to improve reporting and future detections.

---

## Key Takeaways

- The Cyber Kill Chain contains seven stages: reconnaissance, weaponization, delivery, exploitation, installation, command and control, and actions on objectives.
- Attackers may repeat stages as they move deeper into a network.
- MITRE ATT&CK provides detailed, standardized descriptions of attacker tactics and techniques.
- A tactic is an attacker objective; a technique is the method used to achieve it.
- TTP-based detections are generally harder for attackers to evade than hash, IP, or domain-based detections.
- Mapping alerts to MITRE ATT&CK improves incident analysis, reporting, threat hunting, and response decisions.

---

## References

- [MITRE ATT&CK Enterprise Matrix](https://attack.mitre.org/matrices/enterprise/)
- [MITRE ATT&CK Techniques](https://attack.mitre.org/techniques/)
- LinkedIn Learning — *Incident Handling Process: Cybersecurity Labs Powered by Hack The Box*, “Cyber Kill Chain” lesson
