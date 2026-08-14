# Incident Handling Preparation Stage — Part 1

## Overview

The **Preparation** stage ensures that an organization is ready to handle cybersecurity incidents efficiently and safely.

Preparation has two main objectives:

1. Establish an incident-handling capability within the organization.
2. Reduce the likelihood and impact of IT security incidents through preventive and protective measures.

Preventive security measures may include endpoint and server hardening, Active Directory tiering, multi-factor authentication (MFA), and privileged access management (PAM). Although incident responders may not own all preventive controls, these controls directly improve the organization's ability to handle incidents.

---

## Preparation Prerequisites

Before an incident occurs, the organization should ensure it has the following:

| Requirement | Purpose |
|---|---|
| Skilled incident-response team | Provides technical expertise for investigation, containment, eradication, and recovery |
| In-house response knowledge | Ensures the organization can coordinate and understand incidents, even when external responders are used |
| Trained workforce | Reduces risk through security awareness and helps employees recognize suspicious activity |
| Clear policies and documentation | Defines responsibilities, escalation paths, procedures, and legal requirements |
| Software and hardware tools | Enables evidence collection, analysis, communication, documentation, and forensic work |

---

## Preventive Security Measures

Preparation is not limited to responding after an incident. Organizations should also deploy controls that reduce the chance of compromise.

Examples include:

- Endpoint and server hardening
- Multi-factor authentication (MFA)
- Privileged access management (PAM)
- Active Directory tiering
- Patch and vulnerability management
- Secure configuration baselines
- Network segmentation
- Centralized logging and monitoring
- Security awareness training

These measures reduce the attack surface and make attacker activity easier to detect.

---

## Policies and Documentation

Clear, current documentation is essential because incident response often involves technical, legal, operational, and communication decisions.

Important documentation should include:

- Contact details and roles for incident-response team members
- Contact information for legal, compliance, management, IT support, communications, law enforcement, internet service providers, facilities teams, and external incident-response providers
- Incident-response policies, plans, and procedures
- Incident-information-sharing policies
- System and network baselines
- Golden images and known-clean system states
- Network diagrams
- An organization-wide asset-management database
- Forensic and investigative cheat sheets
- Procedures for emergency purchasing of tools or external resources
- Documentation for privileged emergency accounts

---

## System Baselines and Golden Images

A **baseline** is a documented representation of an approved, normal system or network configuration.

A **golden image** is a known-good system image that can be used as a trusted reference or to rebuild compromised systems.

Baselines help security teams identify unexpected changes, such as:

- Unauthorized software installation
- Modified system configurations
- Unexpected services or scheduled tasks
- Unusual user accounts
- Changed security settings
- Suspicious network configuration changes

Comparing a system against its baseline can reveal deviations that may indicate malicious activity or configuration drift.

---

## Emergency Privileged Accounts

Incident responders may require privileged accounts to investigate business-critical systems or perform containment actions.

These accounts should be managed carefully:

- Keep them disabled when they are not needed.
- Enable them only after an incident has been confirmed and access is required.
- Use appropriate administrative access for the specific system.
- Disable accounts after the response activity ends.
- Reset passwords after disabling the accounts.
- Log and review all actions performed with privileged accounts.

This approach supports rapid incident response while reducing the risk of standing administrative privileges being abused.

---

## Incident Documentation

Incident documentation must continue throughout the investigation, not only after the incident is resolved.

During a stressful event, responders should record:

- Timestamps
- Actions performed
- Results of each action
- The person who performed the action
- Affected systems, accounts, and evidence sources
- Decisions and approvals
- Changes made during containment and recovery

Good documentation helps answer the core investigative questions:

```text
Who?
What?
When?
Where?
Why?
How?
```

It also supports handoffs between responders, legal review, root-cause analysis, incident reporting, and post-incident lessons learned.

---

## Compliance and External Communication

Some incidents may require communication with external stakeholders, including customers, vendors, regulators, insurers, law enforcement, or incident-response partners.

The response team should work with legal and compliance personnel to determine:

- Whether a reportable data breach occurred
- Which notification deadlines apply
- Which affected parties must be informed
- What information can be shared externally
- How evidence should be preserved
- Whether law enforcement involvement is appropriate

Requirements depend on the organization’s location, industry, affected data, and applicable laws or regulations. Legal and compliance teams should be consulted early when an incident may have regulatory consequences.

---

## Required Tools

Incident-response teams need dedicated and reliable tools for evidence acquisition, analysis, communication, and documentation.

### Software Tools

- Digital forensic imaging and analysis tools
- Memory-capture and memory-analysis tools
- Live-response collection tools
- Log-analysis platforms
- Network-capture and network-analysis tools
- IOC creation and IOC search tools
- Encryption software
- Ticket-tracking and case-management systems
- Malware-analysis tools
- Secure documentation platforms

### Hardware Tools

- Dedicated laptops or forensic workstations
- External hard drives for forensic images
- Write blockers
- Network cables and switches
- Power cables and adapters
- Screwdrivers, tweezers, and repair tools
- Secure evidence-storage equipment

### Operational Resources

- Chain-of-custody forms
- A secure facility for storage and investigation
- A process for urgent procurement
- An incident-handling system independent of corporate infrastructure
- Secure alternative communications channels

---

## The Incident Response Jump Bag

A **jump bag** is a prepared kit containing the tools and materials needed for an incident responder to begin work immediately.

It should be maintained in a ready-to-use state and may contain:

- Forensic laptop or workstation
- Storage devices
- Write blockers
- Network equipment
- Power cables and adapters
- Evidence-collection tools
- Chain-of-custody forms
- Documentation templates
- Basic hardware repair tools

Without a prepared jump bag, gathering forensic equipment and required tools during an incident can cause major delays.

> The key principle is simple: incident responders should be able to **grab the bag and go**.

---

## Independent Response Infrastructure

Organizations should assume that their normal infrastructure may be unavailable or compromised during a major security incident.

Incident-response systems should be independent from the organization’s primary environment whenever possible.

This includes:

- Documentation and note-taking systems
- Incident case-management platforms
- Communication channels
- Secure file-sharing locations
- Evidence repositories
- Emergency contact lists

If an attacker compromises the domain, internal email, file shares, ticketing platforms, or collaboration tools may be unavailable or monitored. Using an independent and secured response environment helps preserve confidentiality, integrity, and availability during the investigation.

---

## Example Scenario

An organization identifies ransomware activity on a file server.

1. The incident-response team retrieves its prepared jump bags.
2. Responders use dedicated forensic workstations instead of potentially compromised corporate devices.
3. The team accesses an external incident case-management system and secure communication channel.
4. Analysts compare the affected server against its known baseline and golden-image configuration.
5. Privileged emergency accounts are enabled temporarily for containment actions.
6. Responders document every action, timestamp, finding, and decision.
7. Legal and compliance teams evaluate whether notification requirements apply.
8. After the incident, emergency accounts are disabled and their passwords are reset.

---

## Key Takeaways

- Preparation builds the organization’s ability to respond effectively before an incident occurs.
- The two main preparation objectives are establishing incident-handling capability and reducing the likelihood of security incidents.
- Skilled responders, trained employees, clear documentation, and appropriate tools are core preparation requirements.
- System baselines and golden images help identify suspicious or unauthorized configuration changes.
- Documentation should include timestamps, responder actions, results, and investigative findings.
- Emergency privileged accounts should be tightly controlled, temporarily enabled, monitored, disabled after use, and reset.
- A jump bag provides the hardware, software, and documentation necessary to start responding immediately.
- Incident-response communication and documentation systems should remain independent from primary corporate infrastructure.

---

## References

- [NIST SP 800-61 Rev. 2 — Computer Security Incident Handling Guide](https://csrc.nist.gov/pubs/sp/800/61/r2/final)
- [NIST SP 800-86 — Guide to Integrating Forensic Techniques into Incident Response](https://csrc.nist.gov/pubs/sp/800/86/final)
- LinkedIn Learning — *Incident Handling Process: Cybersecurity Labs Powered by Hack The Box*, “Preparation Stage (Part 1)”
