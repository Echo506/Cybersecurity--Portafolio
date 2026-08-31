# Windows 10 Endpoint Monitoring & Alert Triage Lab

## Project Overview

This project documents a hands-on Windows 10 virtual machine lab focused on endpoint monitoring, log analysis, and alert triage.

The goal is to collect and investigate Windows telemetry using Sysmon and Event Viewer, identify potentially suspicious activity, and document findings using a SOC analyst workflow.

> **Scope:** All activities are performed in an isolated and authorized Windows 10 virtual machine for educational and portfolio purposes. No malware, unauthorized access, or testing against third-party systems is involved.

---

## Objectives

- Deploy and configure a Windows 10 virtual machine.
- Install and configure Sysmon for endpoint telemetry collection.
- Analyze Windows and Sysmon event logs using Event Viewer.
- Generate safe, controlled activities for investigation.
- Perform alert triage using process, file, network, user, and timestamp information.
- Map relevant activity to MITRE ATT&CK techniques.
- Document evidence, findings, and recommended response actions.

---

## Lab Environment

| Component | Details |
|---|---|
| Host System | Windows 10 |
| Virtualization Platform | VirtualBox |
| Guest Operating System | Windows 10 |
| Monitoring Tool | Sysmon (Microsoft Sysinternals) |
| Log Analysis Tool | Windows Event Viewer |
| Framework | MITRE ATT&CK |
| Lab Scope | Isolated and authorized virtual machine |

---

## Project Structure

```text
Windows-10-Endpoint-Monitoring-Alert-Triage-Lab/
├── README.md
├── 01-Lab-Setup.md
├── 02-Sysmon-Configuration.md
├── 03-Case-PowerShell-Execution.md
├── 04-Case-File-Creation-Download.md
├── 05-Case-Scheduled-Task.md
└── evidence/
```

---

## Investigation Cases

| Case | Scenario | Primary Sysmon Events | MITRE ATT&CK |
|---|---|---|---|
| 1 | PowerShell execution analysis | Event ID 1 | T1059.001 – PowerShell |
| 2 | File creation and controlled download | Event IDs 1, 3, 11, 22 | T1105 – Ingress Tool Transfer |
| 3 | Scheduled task creation and removal | Event IDs 1, 12–14 | T1053 – Scheduled Task/Job |

---

## Key Sysmon Events

| Event ID | Event Name | Investigation Value |
|---|---|---|
| 1 | Process Create | Identifies executed processes, parent processes, command lines, hashes, and users |
| 3 | Network Connection | Shows process-initiated network activity |
| 11 | File Create | Records file creation activity |
| 12–14 | Registry Events | Records Registry object creation, deletion, and value changes |
| 22 | DNS Query | Helps identify domain lookups performed by processes |

---

## Evidence Collection

Evidence for each investigation will include:

- Screenshots of relevant Sysmon events.
- Event timestamps and Event IDs.
- Process names, parent processes, and command lines.
- Associated users and hostnames.
- File paths, IP addresses, domains, or task names when applicable.
- Triage decision and written analysis.
- MITRE ATT&CK mapping.
- Recommended containment or remediation actions.

Screenshots and other artifacts will be stored in the [`evidence`](./evidence/) directory.

---

## Skills Demonstrated

- Windows endpoint monitoring.
- Sysmon deployment and configuration.
- Windows Event Viewer log analysis.
- SOC alert triage and escalation decisions.
- Basic threat-hunting methodology.
- MITRE ATT&CK mapping.
- Incident documentation and evidence handling.

---

## Status

**Status:** In progress

This repository will be updated as the Windows 10 VM is configured, telemetry is collected, and each investigation case is documented.

---

## Author

**Wilfrido Pérez Romero**  
Cybersecurity | SOC Analyst | GRC | AI Governance  
[GitHub Profile](https://github.com/Echo506)
