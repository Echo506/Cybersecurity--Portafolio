# 🛡️ Infra-Sec-Check

## Project Status

- **Current Status:** In Progress
- **Build Stage:** Under Construction
- **Documentation Status:** Active
- **Evidence Collection:** Pending screenshots and execution results
- **Video Walkthrough:** Coming soon
- **Last Update:** August 2026

> This project is currently being documented and expanded as part of my cybersecurity portfolio. New screenshots, findings, report samples, and a YouTube walkthrough will be added as the project evolves.

## Overview

`Infra-Sec-Check` is a PowerShell-based project created to perform a basic security audit on Windows endpoints. The main goal of this project is to identify common security weaknesses, review essential protections, and generate useful output that helps improve the security posture of a system.

This repository was created as part of my cybersecurity portfolio to document practical work, technical learning, and hands-on security analysis. Rather than only collecting theory, this project helps demonstrate how security checks can be organized, explained, and turned into actionable results.

## Purpose of the Project

The purpose of `Infra-Sec-Check` is to provide a simple but meaningful way to review important Windows security settings and highlight areas that may require attention. It was created to support learning, documentation, and portfolio development in cybersecurity, while also serving as a practical reference for endpoint security review.

This project aligns with my interest in:

- SOC and security operations
- Infrastructure security
- Risk awareness and control validation
- Security documentation and reporting
- Practical cybersecurity learning

## Project Goals

- Build a practical Windows security review project
- Document the security validation process in a clear way
- Generate useful output that can support follow-up actions
- Create a portfolio-ready project with technical and visual evidence
- Improve future versions with more checks and better reporting

## What the Script Does

The `Infra-Sec-Check` script performs a basic infrastructure and endpoint security review by checking several relevant security configurations in Windows.

### Included checks

- Verifies the status of **User Account Control (UAC)**
- Reviews **Windows Firewall**
- Confirms whether **Microsoft Defender** is enabled
- Checks **BitLocker** status
- Identifies users with **non-expiring passwords**
- Enumerates **local administrators**
- Detects whether **SMBv1** is enabled
- Reviews whether there are **critical pending patches**
- Generates an **HTML report** with findings and recommendations

## Why This Matters

Basic misconfigurations in endpoints can create unnecessary exposure and increase operational risk. Reviewing local administrators, legacy protocols, password settings, patch status, and core protections can help identify weak points before they become larger security issues.

This project is important because it reflects a practical approach to security assessment: checking controls, documenting results, and translating technical findings into understandable actions.

## Technical Requirements

To run the script successfully, the following requirements should be met:

- **PowerShell 5+**
- **Administrative privileges**
- **PSWindowsUpdate module** installed, in order to review pending updates

Example installation command:

```powershell
Install-Module -Name PSWindowsUpdate -Force
```

## Basic Usage

Run the script from a PowerShell session with administrator privileges:

```powershell
.\audit.ps1
```

After execution, the script generates a `report.html` file in the same directory. This report is intended to summarize the audit results and provide recommendations based on the detected configuration status.

## Review Areas

This project can be understood through the following security review areas:

### 1. Endpoint Protection
Validation of UAC, Firewall, Defender, and BitLocker to verify whether the system has key protective controls enabled.

### 2. Access and Privilege Review
Identification of local administrators and accounts with non-expiring passwords to support visibility over privileged access and account hygiene.

### 3. Legacy and Insecure Configuration Detection
Verification of SMBv1 to detect outdated protocols that may increase attack surface.

### 4. Patch and Update Awareness
Review of pending critical patches to identify whether the system may be exposed to known vulnerabilities due to missing updates.

### 5. Reporting and Documentation
Generation of an HTML report to help organize findings and support follow-up actions.

## Evidence

> The following evidence section is being prepared and will be updated as screenshots and results become available.

### Planned Evidence
- Screenshot of the script execution
- Screenshot of the generated `report.html`
- Screenshot of relevant findings
- Screenshot of recommendations or remediation notes

### Image Placeholders
```md

**Figure 1.** Example of script execution in PowerShell.


**Figure 2.** HTML report generated after the audit.


**Figure 3.** Sample findings identified during the security review.
```

## Video Walkthrough

> A YouTube video walkthrough will be added once the project documentation, screenshots, and evidence are fully prepared.

### Planned Video Content
- Project introduction
- Script purpose and security value
- Review of included checks
- Execution demonstration
- Findings review
- Recommendations and future improvements

### Future Link
```md
[Watch the full walkthrough on YouTube](PASTE-YOUR-YOUTUBE-LINK-HERE)
```

## Progress Tracker

| Task | Status |
|---|---|
| Project concept defined | ✅ Completed |
| Initial script created | ✅ Completed |
| Project purpose documented | ✅ Completed |
| Review areas documented | ✅ Completed |
| Screenshots collected | 🚧 In Progress |
| HTML report evidence added | 🚧 In Progress |
| Findings section enriched | 🚧 In Progress |
| YouTube video recorded | ⏳ Pending |
| Final portfolio polish | ⏳ Pending |

## Portfolio Value

This project is part of my effort to build a cybersecurity portfolio based on practical documentation, structured analysis, and continuous improvement. Its value is not only in the script itself, but also in the ability to explain:

- what was reviewed,
- why it matters,
- what was found,
- and what should be improved.

This approach supports my development in cybersecurity, SOC analysis, incident handling, infrastructure review, and technical reporting.

## Future Improvements

This project can continue evolving with:

- additional Windows security checks
- more detailed findings classification
- clearer risk rating
- improved HTML reporting
- remediation guidance
- screenshots of real results
- a complete video walkthrough
- version tracking for future enhancements

## Conclusion

`Infra-Sec-Check` was created as a practical project to review baseline Windows security settings and document meaningful results. It represents the kind of work I want to continue developing in my portfolio: hands-on, structured, useful, and aligned with real cybersecurity and operational needs.
