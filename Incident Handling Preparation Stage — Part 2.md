# Incident Handling Preparation Stage — Part 2

## Overview

The second part of the **Preparation** stage focuses on protecting the organization against security incidents.

Although incident responders may not directly own every security control, they should understand the protections deployed across the environment. This knowledge helps them assess incident sophistication, locate relevant evidence, and recognize where attackers may have bypassed defenses.

---

## Core Protective Measures

High-impact protection measures should address common initial-access methods, endpoint compromise, identity abuse, vulnerable systems, and lateral movement.

| Security Area | Primary Goal | Examples |
|---|---|---|
| Email security | Reduce phishing and spoofing | SPF, DKIM, DMARC, email filtering |
| Endpoint security | Prevent and detect endpoint compromise | Hardening baselines, EDR, ASR rules, host firewalls |
| Network security | Reduce lateral movement and unauthorized access | Segmentation, IDS/IPS, 802.1X, conditional access |
| Identity security | Protect accounts and privileged access | MFA, PAM/PIM, strong passphrases |
| Vulnerability management | Reduce exploitable weaknesses | Continuous scanning, patching, segmentation |
| User awareness | Improve human detection and reporting | Security training and phishing simulations |
| Security assessments | Find weaknesses before attackers do | Active Directory reviews and purple-team exercises |

---

## Email Protection

Phishing remains a common method for obtaining initial access. Organizations should use email authentication controls to prevent attackers from impersonating their domains.

### SPF, DKIM, and DMARC

| Control | Purpose |
|---|---|
| SPF | Identifies which mail servers are authorized to send email for a domain |
| DKIM | Uses cryptographic signing to help verify that an email was sent by an authorized source and was not modified |
| DMARC | Uses SPF and DKIM alignment to define how receiving mail systems should handle suspicious or spoofed messages |

**DMARC** can instruct receiving systems to reject messages that falsely claim to originate from the organization’s domain.

For example, if an attacker sends an invoice-payment phishing message while impersonating `employee@company.com`, DMARC can help prevent the message from reaching the recipient.

### Implementation Considerations

DMARC and related mail-filtering rules require careful testing before broad enforcement.

Poorly configured policies can block legitimate messages, especially messages sent through third-party services on behalf of an organization. Those messages may fail DMARC because the sending domain and visible sender domain do not align correctly.

---

## Endpoint Hardening

Corporate endpoints are frequent targets because users browse the web, open files, receive email attachments, and may execute malicious payloads.

Organizations should create hardening baselines using recognized standards, including:

- CIS Benchmarks
- Microsoft security baselines
- Organization-specific secure configuration standards

### Recommended Endpoint Controls

- Disable **LLMNR** and **NetBIOS** where they are not required.
- Implement **LAPS** or a modern local-administrator-password solution.
- Remove unnecessary local administrative privileges from regular users.
- Disable PowerShell when possible, or use **Constrained Language Mode** where appropriate.
- Enable Microsoft Defender **Attack Surface Reduction (ASR)** rules.
- Restrict application execution through allowlisting.
- Block execution from user-writable folders such as `Downloads`, `Desktop`, and `AppData`.
- Block unnecessary script types, including `.hta`, `.vbs`, `.cmd`, `.bat`, and `.js`.
- Review potential abuse of **Living off the Land Binaries (LOLBin)** tools.
- Enable host-based firewalls.
- Block unnecessary workstation-to-workstation communication.
- Control or monitor outbound traffic to suspicious tools and destinations.
- Deploy an **Endpoint Detection and Response (EDR)** solution.

### AMSI and EDR

The **Antimalware Scan Interface (AMSI)** gives compatible security products visibility into script content before execution.

When selecting an EDR solution, integration with AMSI is valuable because attackers frequently use obfuscated PowerShell and script-based payloads to evade simple signature-based detection.

---

## Network Protection

Network segmentation reduces the impact of a compromise by limiting the systems an attacker can access.

Business-critical assets should be isolated, and network connections should be allowed only when required for legitimate business operations.

### Network Security Practices

- Segment user workstations, servers, administration systems, and critical services.
- Place internet-facing services in a properly configured DMZ.
- Avoid exposing internal resources directly to the internet.
- Apply least-privilege access rules between network segments.
- Use IDS and IPS technologies to identify or block malicious traffic.
- Use SSL/TLS interception only where legally, technically, and operationally appropriate so that inspection tools can analyze encrypted traffic.
- Require approved devices to authenticate before accessing corporate networks.
- Use **802.1X** to restrict unauthorized devices from connecting to wired or wireless networks.
- Use Conditional Access policies in cloud environments to limit access to managed or compliant devices.

---

## Identity Security

Privileged credentials are a frequent target in Active Directory environments because they can provide attackers with rapid escalation and broad access.

Weak passwords, password reuse, and sharing a password between privileged and standard accounts significantly increase risk.

### Password Guidance

A password can meet complexity requirements yet still be weak if it is predictable.

Example of a weak but complex password:

```text
Password1!
```

Long passphrases are generally easier for users to remember and more resistant to guessing and brute-force attempts.

Example of a stronger passphrase format:

```text
MyCoffeeIsWarmAtSeven!
```

Organizations should avoid using shared passwords and should separate administrative accounts from standard user accounts.

### MFA and Privileged Access

Multi-factor authentication should be required for administrative access to applications, systems, and devices.

Other important controls include:

- Privileged Identity Management (PIM)
- Privileged Access Management (PAM)
- Just-in-time privileged access
- Separate administrative accounts
- Strong authentication methods
- Monitoring and logging privileged activity

---

## Vulnerability Management

Vulnerabilities provide attackers with opportunities to gain access, execute code, escalate privileges, or move laterally.

Organizations should perform continuous vulnerability scanning and remediate high- and critical-severity findings as quickly as possible.

### Vulnerability Response Steps

1. Discover vulnerabilities through authenticated scanning and asset monitoring.
2. Prioritize critical and high-severity vulnerabilities.
3. Patch, update, or reconfigure affected systems.
4. Validate that remediation was successful.
5. If patching is not possible, apply compensating controls such as network segmentation, access restrictions, or enhanced monitoring.
6. Track exceptions and review them regularly.

Automated scanning can identify vulnerabilities, but remediation typically requires human review, testing, change management, and operational coordination.

---

## User Awareness Training

Employees can become an important detection layer when they know how to recognize and report suspicious activity.

Awareness training should help users identify:

- Phishing messages
- Suspicious links and attachments
- Credential-harvesting attempts
- Unexpected MFA prompts
- Unknown USB devices
- Social-engineering attempts
- Suspicious software or browser behavior

Periodic simulations can help measure and improve awareness. Examples include phishing simulations, dropped USB tests, and social-engineering exercises.

The objective is not to blame users. It is to build a culture where people report suspicious activity quickly and without hesitation.

---

## Active Directory Security Assessments

Active Directory misconfigurations can create easy escalation paths from a compromised endpoint to privileged access.

Security assessments should evaluate the environment from an attacker’s perspective and identify weaknesses before they can be exploited.

Assessment activities may include:

- Reviewing privileged group membership
- Identifying excessive permissions
- Checking for weak service-account configurations
- Reviewing delegation settings
- Identifying exposed credentials
- Testing privilege-escalation paths
- Reviewing outdated protocols and insecure configurations
- Verifying administrative tiering and account separation

The objective is to remove “low-hanging fruit” that could allow an attacker to quickly obtain high privileges after compromising a workstation.

---

## Purple Team Exercises

A **purple team exercise** combines offensive testing with defensive improvement.

A red team simulates attacker behavior, while the blue team focuses on monitoring, detection, investigation, and response. Unlike a traditional red-team engagement, the teams share information during or after the exercise to improve security outcomes.

Purple-team exercises can help organizations:

- Identify vulnerabilities and security gaps
- Test logging and telemetry coverage
- Validate detection rules
- Improve alert triage
- Test incident-response playbooks
- Measure response speed and effectiveness
- Improve communication between offensive and defensive teams

If an activity is not detected, the organization has an opportunity to improve visibility and detection coverage. If it is detected, the blue team can validate whether its playbooks and response procedures achieve the expected outcome.

---

## Example Scenario

An attacker sends a spoofed email that appears to come from the organization’s finance department.

1. DMARC rejects the spoofed message before it reaches most users.
2. A message that bypasses filtering is reported by a trained employee.
3. EDR detects suspicious PowerShell activity from the affected endpoint.
4. Host-based firewall rules and network segmentation limit lateral movement.
5. MFA prevents the attacker from reusing a stolen password to access an administrative account.
6. The incident-response team reviews logs and uses established playbooks to investigate the event.
7. Lessons learned from the incident are used to improve mail filtering and detection rules.

---

## Key Takeaways

- Protective controls are a vital part of the preparation stage because they reduce incident likelihood and impact.
- DMARC uses SPF and DKIM-related authentication checks to help prevent domain spoofing and phishing.
- Endpoint hardening should include secure baselines, reduced user privileges, application-control measures, host firewalls, and EDR.
- Network segmentation limits lateral movement and helps contain compromises.
- MFA, PAM/PIM, separate administrator accounts, and strong passphrases protect privileged access.
- Vulnerability scanning must be paired with timely remediation or compensating controls.
- Security-awareness training increases the likelihood that users report suspicious activity.
- Active Directory assessments identify escalation paths and misconfigurations before attackers exploit them.
- Purple-team exercises improve prevention, detection, response procedures, and collaboration between red and blue teams.

---

## References

- [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks)
- [Microsoft Security Baselines](https://learn.microsoft.com/windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines)
- [MITRE ATT&CK](https://attack.mitre.org/)
- [LOLBAS Project](https://lolbas-project.github.io/)
- LinkedIn Learning — *Incident Handling Process: Cybersecurity Labs Powered by Hack The Box*, “Preparation Stage (Part 2)”
