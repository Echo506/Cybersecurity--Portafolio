# Containment, Eradication, and Recovery

## Overview

After the investigation clarifies the incident type, affected assets, attack path, and business impact, the incident-response team moves into **containment**, **eradication**, and **recovery**.

These stages aim to prevent further damage, remove the attacker and the root cause, restore business operations, and closely monitor systems for signs of recurring compromise.

---

## Stage Objectives

| Stage | Main Objective |
|---|---|
| Containment | Stop the incident from spreading and limit additional damage |
| Eradication | Remove malware, persistence, vulnerabilities, and the root cause of compromise |
| Recovery | Restore systems to normal operation and monitor them for recurring attacker activity |

These stages should be coordinated with technical teams, system owners, management, and other relevant stakeholders to avoid disrupting critical business operations.

---

## Containment

Containment involves actions that prevent an incident from spreading or causing additional harm.

Containment should be planned and executed in a coordinated way across affected systems. Taking action against only part of the attacker’s infrastructure may warn the adversary that they have been discovered, allowing them to alter tools, change tactics, destroy evidence, or move elsewhere in the environment.

Containment activities are commonly divided into:

- Short-term containment
- Long-term containment

---

## Short-Term Containment

Short-term containment uses actions that limit damage while making the smallest possible change to affected systems.

The goal is to buy time for responders to preserve evidence, complete analysis, and prepare a long-term remediation strategy.

### Common Actions

- Move an affected system to a separate or isolated VLAN.
- Disconnect the network cable from an affected system.
- Block or redirect a known attacker command-and-control domain.
- Disable network connectivity for a compromised endpoint.
- Restrict access to affected services.
- Isolate hosts through an EDR platform.
- Preserve forensic images and volatile evidence before major system changes.

### Evidence Preservation

Short-term containment should preserve systems as much as possible so responders can collect evidence.

This activity may be described as a **backup substage** because it includes collecting forensic images, memory captures, logs, and other evidence before systems are rebuilt, patched, or modified.

If containment requires shutting down a system, responders should communicate the expected business impact and obtain appropriate authorization before proceeding.

---

## Long-Term Containment

Long-term containment uses persistent changes that limit attacker access and reduce the chance of reinfection.

These activities can affect business operations, so the incident-response team should coordinate with system owners, IT teams, management, and other stakeholders.

### Common Actions

- Reset or change compromised passwords.
- Disable compromised user or service accounts.
- Revoke active sessions, tokens, and authentication credentials.
- Implement firewall rules to block malicious traffic.
- Block malicious IP addresses, domains, URLs, and file hashes.
- Deploy or tune host-based intrusion-detection systems.
- Apply urgent security patches.
- Restrict remote access and unnecessary network paths.
- Shut down systems when risk outweighs operational impact.

> Applying a patch may be part of long-term containment, but patching alone does not mean the incident is resolved. Eradication, recovery, and post-incident activities are still required.

---

## Eradication

Eradication removes the root cause of the incident and eliminates the attacker’s remaining presence in systems and networks.

The objective is to make sure the adversary no longer has malware, credentials, persistence mechanisms, vulnerabilities, or unauthorized access paths that could be used to return.

### Eradication Activities

- Remove detected malware and malicious files.
- Delete malicious scheduled tasks, services, startup items, and registry persistence.
- Remove unauthorized accounts and access permissions.
- Reset exposed credentials and rotate secrets.
- Rebuild systems that cannot be trusted.
- Restore systems from verified clean backups.
- Patch exploited vulnerabilities.
- Apply additional security patches across the environment.
- Harden systems and reduce unnecessary services or privileges.
- Improve security configurations across impacted and related systems.

Eradication may extend containment actions. For example, responders may initially patch an urgent vulnerability to limit risk, then later apply broader patching and hardening across the organization.

---

## Recovery

Recovery returns affected systems and services to normal business operation.

Before systems are returned to production, the organization should verify that they operate correctly, contain the necessary data, and no longer show evidence of compromise.

### Recovery Activities

- Restore systems from known-good backups.
- Rebuild compromised hosts from trusted images.
- Verify data integrity and application functionality.
- Confirm that required business services operate normally.
- Return systems to production in a controlled manner.
- Validate that patches, hardening changes, and access controls are working.
- Monitor recovered systems closely for signs of reinfection or attacker return.

### Post-Recovery Monitoring

Recovered systems should receive enhanced logging and monitoring because compromised assets may be targeted again if the attacker regains access.

Important events to monitor include:

- Unusual logons, especially from users or service accounts that have not previously accessed the system.
- Unusual processes or unexpected command-line activity.
- Registry changes in locations frequently abused for malware persistence.
- New scheduled tasks, services, or startup entries.
- Suspicious outbound network connections.
- New administrative accounts or privilege changes.
- Reappearance of known indicators of compromise.

If indicators of compromise continue to appear during recovery, the incident should be escalated back to the **investigation** phase rather than continuing recovery without understanding the cause.

---

## Phased Recovery

Large incidents may require recovery over weeks or months.

Early recovery phases should prioritize quick improvements that reduce immediate risk, such as:

- Removing exposed credentials
- Patching critical vulnerabilities
- Disabling risky services
- Blocking malicious network paths
- Improving endpoint visibility
- Eliminating obvious misconfigurations

Later phases should focus on permanent security improvements, including architecture changes, segmentation, identity hardening, monitoring enhancements, and updated response procedures.

---

## Containment vs. Eradication vs. Recovery

| Area | Containment | Eradication | Recovery |
|---|---|---|---|
| Primary goal | Stop spread and reduce damage | Remove attacker access and root cause | Restore safe business operations |
| Typical timing | Immediately after validated investigation findings | After or alongside containment | After threats and persistence are removed |
| Examples | Isolate a host, block C2 traffic, disable an account | Remove malware, patch vulnerabilities, rebuild host | Restore from backup, validate services, return system to production |
| Evidence focus | Preserve evidence before major changes | Remove malicious artifacts and persistence | Monitor restored systems for recurrence |

---

## Example Scenario

A ransomware attack affects several file servers.

1. **Containment:** The response team isolates affected servers, disables compromised accounts, blocks known command-and-control domains, and preserves forensic evidence.

2. **Long-Term Containment:** Firewall rules are updated, exposed credentials are reset, and affected network segments are restricted.

3. **Eradication:** Malware and persistence mechanisms are removed, vulnerable software is patched, and systems that cannot be trusted are rebuilt from known-good images.

4. **Recovery:** Clean backups are restored, data integrity is verified, services are tested with business owners, and file servers return to production gradually.

5. **Monitoring:** Analysts apply heightened monitoring for unusual logons, suspicious processes, registry changes, and recurring indicators of compromise.

6. **Reinvestigation if Needed:** If malicious indicators reappear, the team returns to the investigation phase to identify the remaining attack path or missed persistence mechanism.

---

## Key Takeaways

- Containment prevents an incident from spreading and causing additional damage.
- Short-term containment limits damage while preserving evidence and allowing responders to prepare a remediation plan.
- Long-term containment introduces persistent controls, such as password resets, firewall rules, host IDS deployment, patches, and system shutdowns.
- Patching a system is generally a long-term containment action, not a short-term containment action.
- Eradication removes malware, persistence mechanisms, attacker access, and the root cause of the compromise.
- Recovery restores verified systems and services to production after business and technical validation.
- Recovered systems require heightened logging and monitoring because adversaries may attempt to regain access.
- If IOCs continue to appear during recovery, responders should return to the investigation phase.

---

## References

- [NIST SP 800-61 Rev. 2 — Computer Security Incident Handling Guide](https://csrc.nist.gov/pubs/sp/800/61/r2/final)
- [NIST SP 800-86 — Guide to Integrating Forensic Techniques into Incident Response](https://csrc.nist.gov/pubs/sp/800/86/final)
- [MITRE ATT&CK Enterprise Matrix](https://attack.mitre.org/matrices/enterprise/)
- LinkedIn Learning — *Incident Handling Process: Cybersecurity Labs Powered by Hack The Box*, “Containment, Eradication, & Recovery Stage”
