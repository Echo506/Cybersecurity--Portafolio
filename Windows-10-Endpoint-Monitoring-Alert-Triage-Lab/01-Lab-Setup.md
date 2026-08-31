# 01 - Lab Setup

## Objective

This document records the initial setup of the Windows 10 virtual machine used for the **Windows 10 Endpoint Monitoring & Alert Triage Lab**.

The objective is to establish an isolated, authorized, and reproducible environment for endpoint monitoring, Sysmon telemetry collection, and SOC alert triage practice.

> **Authorization Notice:** This lab is performed exclusively in a personally controlled or explicitly authorized Windows 10 virtual machine. No tests are performed against third-party systems, networks, or accounts.

---

## Lab Architecture

```text
Host Computer
│
└── VirtualBox
    │
    └── Windows 10 Virtual Machine
        ├── Sysmon
        ├── Windows Event Viewer
        └── PowerShell
```

---

## Virtual Machine Configuration

| Setting | Configuration |
|---|---|
| Virtualization Platform | VirtualBox |
| Guest Operating System | Windows 10 |
| VM Name | Win10-SOC-Lab |
| System Type | Microsoft Windows |
| Version | Windows 10 (64-bit) |
| Memory | 2048 MB minimum, depending on host capacity |
| Processors | 1 CPU minimum |
| Storage | 40 GB dynamically allocated virtual disk |
| Network Mode | NAT |
| Snapshot | Clean baseline before security-tool installation |

> **Note:** Resource allocation may be adjusted based on the available host hardware. The objective is to maintain a stable and usable isolated lab environment.

---

## Setup Steps

1. Downloaded the Windows 10 ISO from the official Microsoft source.
2. Created a new VirtualBox virtual machine named `Win10-SOC-Lab`.
3. Assigned available RAM, CPU, and virtual disk resources.
4. Attached the Windows 10 ISO as the virtual optical disk.
5. Installed Windows 10 inside the virtual machine.
6. Applied available Windows updates.
7. Confirmed that the VM could boot successfully.
8. Confirmed basic network connectivity using the NAT adapter.
9. Created a clean baseline snapshot before installing Sysmon or generating lab activity.

---

## Baseline Validation

The following checks were completed before beginning monitoring activities:

| Validation Check | Result |
|---|---|
| Windows 10 boots successfully | Pending |
| Local user account created | Pending |
| Network connectivity available | Pending |
| Event Viewer opens successfully | Pending |
| PowerShell opens successfully | Pending |
| Baseline snapshot created | Pending |

> Update the **Result** column to `Completed` when you perform each validation step.

---

## Evidence to Collect

The following screenshots will be added to the `evidence` folder:

- VirtualBox VM configuration.
- Windows 10 desktop or system-information screen.
- VirtualBox network configuration showing NAT.
- Successful network test, such as `ipconfig` or a browser connection.
- VirtualBox snapshot showing the clean baseline.

---

## Initial Findings

The lab environment is being prepared to support endpoint telemetry collection and alert-triage exercises. At this stage, no suspicious activity has been generated and Sysmon has not yet been installed.

---

## Next Step

Continue with [02 - Sysmon Configuration](./02-Sysmon-Configuration.md).
