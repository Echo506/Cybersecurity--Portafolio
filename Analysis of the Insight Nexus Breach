# Analysis of the Insight Nexus Breach

## Overview

This case study examines a compromise at **Insight Nexus**, a fictional Singapore-based market-research and data-analytics company that handles sensitive client intelligence.

The incident involved **two separate threat actors** operating in the same environment:

- **Crimson Fox:** A sophisticated, persistent actor focused on credential theft, long-term access, and sensitive-data exfiltration.
- **Silent Jackal:** A lower-skill opportunistic group that exploited a vulnerable web portal and left a visible marker file.

The case demonstrates why incident responders must correlate alerts across systems and avoid assuming that a single suspicious artifact represents the full scope of an intrusion.

> **Note:** This repository documents the scenario for learning purposes. It does not include answers to the interactive lab questions or sensitive exercise data.

---

## Environment

### Important Assets

| Asset | Description |
|---|---|
| `manage.insightnexus.com` | Internet-facing ManageEngine ADManager Plus administration portal |
| `portal.insightnexus.com` | PHP-based client reporting portal with file-upload capability |
| `DC01.insight.local` | Domain Controller |
| `FS01.insight.local` | File server hosting `\\fs01\projects` |
| `DB01.insight.local` | Database server containing sensitive data |
| `DEV-001` to `DEV-120` | Developer workstations |
| `DEV-021` | Misconfigured workstation with externally exposed RDP access |

### Security Tooling

| Tool or Control | Role |
|---|---|
| Perimeter firewall | Network filtering and default logging |
| IDS | Basic network intrusion detection, but affected by false positives |
| Wazuh agents | Host-based monitoring on most Windows systems |
| Wazuh SIEM | Centralized logging for Sysmon, Windows Security, web-server, and firewall logs |
| TheHive | Incident case management |
| Cortex | Alert and observable enrichment |

### Identified Security Gaps

- Default credentials remained active on an internet-facing administration application.
- Multi-factor authentication was not enforced.
- The management portal was accessible from the public internet.
- No web application firewall protected the exposed applications.
- Web-application authentication logs were not centrally collected.
- Firewall logging was not integrated with threat intelligence.
- IDS alerts produced excessive false positives.
- Log retention was limited.
- RDP was exposed to the internet on `DEV-021`.
- The PHP reporting portal had an unpatched file-upload vulnerability.
- There was no effective alerting rule for successful RDP logons from public IP addresses.

---

## Threat Actors

### Crimson Fox

Crimson Fox was the primary and more capable threat actor.

The group used valid default credentials and a vulnerable internet-facing management application to gain access. It then performed reconnaissance, created privileged domain accounts, accessed an exposed RDP host, deployed spyware using Group Policy, and exfiltrated sensitive client data.

### Silent Jackal

Silent Jackal was a separate, lower-skill group that exploited a vulnerable PHP-based reporting portal.

Its activity appeared limited to uploading a marker file named `checkme.txt` containing a defacement-style message. Although the artifact appeared low priority by itself, it ultimately helped trigger a deeper investigation that uncovered the more severe Crimson Fox intrusion.

---

## Attack Timeline

| Date and Time | Activity |
|---|---|
| 2025-10-01 03:12:02 | Crimson Fox obtained initial access to ManageEngine through default administrative credentials. |
| 2025-10-01 03:18:32 | A Java process on the ManageEngine server established outbound HTTPS communication to an attacker-controlled IP address. |
| 2025-10-02 04:02:11 | The threat actor enumerated domain users and computers, then created a privileged Active Directory account. |
| 2025-10-04 02:03:12 | The attacker used the privileged account to establish RDP access to the externally exposed `DEV-021` workstation. |
| After RDP access | The attacker performed domain reconnaissance and attempted access to project shares on `FS01`. |
| Later activity | Sensitive client data was compressed into `diagnostics_data.zip` and exfiltrated over HTTPS. |
| 2025-10-04 02:10:45 | PowerShell and Group Policy were used to deploy `java-update.msi` across the domain. |
| Concurrent activity | Silent Jackal exploited the vulnerable PHP portal and placed `checkme.txt` in the web-server root directory. |
| Detection | A SOC analyst correlated the marker file with unusual ManageEngine traffic, suspicious logins, and related security events. |

---

## Crimson Fox Attack Path

### Initial Access

Crimson Fox performed targeted login attempts against `manage.insightnexus.com`.

The attackers successfully authenticated using the default `admin/admin` credentials, which remained active after a product update. The internet-facing management portal did not require MFA, and its authentication logs were not forwarded to the centralized SIEM.

### Command and Control

The attackers exploited a ManageEngine-related Java vulnerability and established outbound HTTPS command-and-control communication to an attacker-controlled host.

A Sysmon Event ID 3 network-connection event recorded Java communicating over port 443, making the traffic resemble routine encrypted web or update traffic.

### Discovery and Privilege Escalation

From the ManageEngine foothold, Crimson Fox:

- Enumerated Active Directory users and computers.
- Created a privileged Active Directory account.
- Identified `DEV-021` as an endpoint with externally exposed RDP.
- Used the newly created privileged credentials to log in to `DEV-021` through RDP.
- Conducted additional domain and file-share reconnaissance.

A successful Windows RDP logon was visible through Event ID `4624` with logon type `10`, indicating RemoteInteractive access.

### Lateral Movement and Persistence

The attackers used PowerShell and domain administrator privileges to create or modify a Group Policy Object.

The GPO deployed an MSI package called `java-update.msi` across multiple domain endpoints. The package created a scheduled task that supported spyware activity and future data exfiltration.

Relevant telemetry included:

- Sysmon Event ID `11` for creation of the MSI file.
- Sysmon Event ID `1` for execution of `msiexec.exe`.
- Windows and Active Directory logs related to GPO modification.
- Scheduled-task and service-creation artifacts.

### Collection and Exfiltration

Crimson Fox accessed client project folders on `FS01`, which included draft reports, survey data, and market forecasts.

The selected data was compressed into `diagnostics_data.zip`, a filename chosen to appear like normal diagnostic output. The archive was uploaded to attacker infrastructure through HTTPS, making the exfiltration harder to distinguish from ordinary encrypted traffic.

---

## Silent Jackal Activity

Silent Jackal exploited an unpatched file-upload vulnerability in the PHP reporting portal.

The group placed `checkme.txt` in the root directory of the web server as a visible signature. The activity did not appear to advance beyond initial access or defacement-style behavior.

However, the file was important because it became the initial clue that caused the SOC team to correlate other suspicious activity occurring at the same time.

---

## Detection and Analysis

### Initial Detection Failure

The `checkme.txt` file alert was initially at risk of being ignored because the organization had many alerts related to new files being created on servers.

This illustrates how **alert fatigue** can delay escalation. High false-positive volumes can cause analysts to miss or deprioritize the events that deserve deeper investigation.

### Effective Correlation

The investigation expanded after the SOC analyst correlated multiple indicators:

- Successful ManageEngine administrator logins from unfamiliar foreign IP addresses
- Unusual outbound HTTPS communication from the ManageEngine server
- LDAP and Active Directory enumeration
- GPO modifications
- `msiexec.exe` executing an MSI package across multiple hosts
- File-share access attempts
- File compression and outbound upload activity
- The `checkme.txt` artifact on the web server

This correlation changed the assessment from a potential web defacement to a critical incident involving privileged access, persistence, and confirmed data exfiltration.

---

## Incident Response Actions

### Case Creation and Triage

The SOC created a critical case in TheHive titled:

```text
Insight Nexus — ManageEngine Compromise
```

The team linked alerts related to ManageEngine logins, MSI deployment, LDAP enumeration, file-server activity, suspicious HTTPS communication, and the portal marker file.

Response responsibilities were assigned to:

- Triage Analyst
- Forensics Lead
- Containment Lead
- Communications Lead

### Network Containment

Containment actions included:

- Blocking outbound traffic to known attacker infrastructure at the perimeter firewall.
- Adding host-based firewall blocks for identified malicious destinations.
- Creating temporary egress restrictions for attacker-controlled IP addresses.
- Adding IDS signatures to identify connections to known malicious infrastructure.

### Credential and Account Containment

The response team:

- Disabled the compromised ManageEngine administrative account.
- Rotated high-privilege credentials exposed in logs.
- Reset passwords for suspicious or potentially affected accounts.
- Revoked active sessions when possible.
- Restricted the ManageEngine console so it could only be accessed internally.

### Host Isolation

The team isolated the management server, `DEV-021`, and hosts showing evidence of MSI deployment.

They also suspended suspicious scheduled tasks and disabled GPO-initiated deployments until the environment could be investigated and remediated.

### Evidence Collection

Responders collected and preserved:

- Volatile memory captures
- Process lists
- Registry hives
- Disk images
- ManageEngine audit logs
- Web-server access logs
- The suspicious MSI package
- The exfiltration archive
- Potential web shells or malicious files

These artifacts supported timeline analysis, malware investigation, persistence discovery, and root-cause analysis.

---

## MITRE ATT&CK Mapping

| Attack Phase | ATT&CK Technique | ID | Scenario Activity |
|---|---|---|---|
| Reconnaissance | Active Scanning | T1595 | Scanning and identifying exposed public services |
| Initial Access | Valid Accounts: Cloud Accounts / Default Credentials Context | T1078 | Logging into ManageEngine with default administrative credentials |
| Initial Access | Exploit Public-Facing Application | T1190 | Exploiting the PHP portal upload vulnerability and the management application weakness |
| Persistence | Server Software Component | T1505 | Abuse of web-server or application components for continued access |
| Command and Control | Application Layer Protocol: Web Protocols | T1071.001 | HTTPS communication with attacker infrastructure |
| Execution | Windows Installer | T1218.007 | MSI installation through `msiexec.exe` |
| Persistence | Scheduled Task/Job | T1053 | Scheduled task created through the deployed MSI |
| Privilege Escalation | Create Account / Account Manipulation | T1136 / T1098 | Creation and use of privileged Active Directory accounts |
| Lateral Movement | Remote Services: RDP | T1021.001 | RDP access to the exposed `DEV-021` workstation |
| Collection | Archive Collected Data | T1560 | Compressing client data into a ZIP archive |
| Exfiltration | Exfiltration Over C2 Channel | T1041 | Uploading compressed data through HTTPS |

> ATT&CK mapping should be validated against the exact evidence available during a real investigation. The mapping above is intended as a learning exercise based on the scenario.

---

## Detection Opportunities

| Activity | Evidence Source | Detection Opportunity |
|---|---|---|
| Default-credential login | ManageEngine authentication logs | Alert on default-account usage, unusual source IPs, and administrator logins from foreign networks |
| Outbound C2 traffic | Sysmon Event ID 3, firewall logs, proxy logs | Detect unusual outbound HTTPS from management servers |
| Public RDP access | Windows Event ID 4624, Logon Type 10 | Alert on successful RemoteInteractive logons from public IP addresses |
| Domain enumeration | Active Directory, LDAP, and endpoint logs | Detect abnormal account, computer, and group enumeration |
| GPO abuse | Active Directory and Group Policy logs | Alert on unexpected GPO creation or modification |
| MSI deployment | Sysmon Event IDs 1 and 11 | Detect suspicious `msiexec.exe` use and MSI execution from temporary paths |
| File-share discovery | Windows Event ID 5140 | Alert on unusual access to sensitive project shares |
| Data compression | Endpoint and file-system telemetry | Detect archives created from sensitive directories |
| HTTPS exfiltration | Firewall, proxy, and network telemetry | Identify unusual outbound transfer volume or rare external destinations |
| Web-portal exploitation | Web-server and WAF logs | Detect suspicious file uploads, web shells, and anomalous requests |

---

## Key Lessons Learned

### Secure Internet-Facing Applications

Default credentials on internet-facing applications can create immediate and severe risk.

Organizations should remove or change default accounts before deployment, enforce MFA for administrative portals, restrict administrative interfaces to trusted networks, and centralize application authentication logs.

### Reduce Alert Fatigue

Security teams should tune noisy alerts and improve filtering, prioritization, and correlation.

A low-severity artifact may become critical when correlated with suspicious login activity, external connections, privilege escalation, or data-exfiltration indicators.

### Investigate Beyond the First Artifact

The visible `checkme.txt` marker file was not the full incident.

Responders must investigate the broader environment, identify related activity, search for persistence, and determine whether multiple threat actors are active at the same time.

### Protect Remote Access

Publicly exposed RDP creates substantial risk.

Remote administration should use secure access methods such as VPNs, conditional access, MFA, network segmentation, and strict firewall rules. Direct RDP exposure to the public internet should be avoided.

### Monitor Privileged Activity

Creation of privileged accounts, use of domain administrator credentials, GPO modifications, and remote logons should generate high-confidence alerts.

Organizations should implement privileged-access management, separate administrator accounts, and continuous monitoring of sensitive Active Directory changes.

### Improve Web Security

Internet-facing applications should receive regular vulnerability assessments, timely patching, centralized logging, and web application firewall protection where appropriate.

### Monitor for Persistence

Deleting a defacement file or blocking an attacker IP does not remove attacker access.

Post-incident monitoring should search for scheduled tasks, services, GPO changes, unauthorized accounts, web shells, malicious MSI packages, startup artifacts, and unusual outbound connections.

---

## Key Takeaways

- Two unrelated threat actors can operate in the same environment simultaneously.
- A low-skill intrusion can create noise that hides a more serious compromise.
- Default credentials, missing MFA, exposed RDP, unpatched web applications, and weak log coverage can combine into a major breach.
- Alert correlation is essential for detecting multi-stage attacks.
- Outbound encrypted traffic should be evaluated in context, especially when management servers communicate with rare external destinations.
- GPO abuse can enable rapid enterprise-wide malware deployment.
- High-value file shares require monitoring for unusual access, collection, archive creation, and outbound transfer.
- Containment must address attacker infrastructure, compromised credentials, affected hosts, persistence mechanisms, and vulnerable services.
- Incident-response teams should preserve forensic evidence before rebuilding or modifying compromised systems.

---

## References

- [MITRE ATT&CK Enterprise Matrix](https://attack.mitre.org/matrices/enterprise/)
- [NIST SP 800-61 Rev. 2 — Computer Security Incident Handling Guide](https://csrc.nist.gov/pubs/sp/800/61/r2/final)
- [Sigma Rule: Successful External Remote RDP Logon](https://github.com/SigmaHQ/sigma/blob/master/rules/windows/builtin/security/account_management/win_security_successful_external_remote_rdp_login.yml)
- LinkedIn Learning — *Incident Handling Process: Cybersecurity Labs Powered by Hack The Box*, “Analysis of Insight Nexus Breach”
