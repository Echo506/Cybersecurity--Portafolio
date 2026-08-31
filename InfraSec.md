# 🛡️ Infra-Sec-Check

## Project Status

- **Current Status:** In Progress
- **Build Stage:** Under Construction
- **Documentation Status:** Active
- **Evidence Collection:** In Progress
- **Video Walkthrough:** Pending
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
- **PSWindowsUpdate module** installed in order to review pending updates

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

## Audit Steps

1. Open PowerShell with administrative privileges.
2. Ensure the required environment is available, including PowerShell 5+ and the `PSWindowsUpdate` module.
3. Run the `audit.ps1` script from the project directory.
4. Allow the script to review all configured security controls.
5. Review the console output summary.
6. Open the generated `report.html` file.
7. Capture screenshots of execution, summary, and findings.
8. Document the results, risks, and recommendations inside this project.

## Evidence Status

- ✅ Script logic documented
- ✅ Audit scope defined
- ✅ Security checks implemented
- ✅ HTML report generation implemented
- 🚧 Real execution screenshots in progress
- 🚧 Findings documentation in progress
- ⏳ YouTube walkthrough pending

## Evidence

> The following evidence reflects the current documentation stage of the project. Additional screenshots and updated results can be added over time.

## Evidence

> The following evidence reflects the current documentation stage of the project. Additional screenshots and updated results can be added over time.

### Script Execution

![InfraSec Execution](images/Captura%20de%20pantalla%20de%202026-08-30%2023-56-27.png)

**Figure 1.** PowerShell execution of the Infra-Sec-Check audit.

### HTML Report

![InfraSec Findings](images/Captura%20de%20pantalla%20de%202026-08-30%2023-57-55.png)

**Figure 2.** Generated HTML report after the security audit.

### Findings Example

![InfraSec Report](images/Captura%20de%20pantalla%20de%202026-08-31%2000-00-47.png)

**Figure 3.** Example of findings identified during the endpoint security review.

## Implemented Audit Logic

The current version of `Infra-Sec-Check` already includes implemented logic to assess key Windows endpoint security controls, classify findings, assign severity, and generate an HTML report.

This provides documented technical evidence of the project design and intended execution workflow, while additional visual evidence is being collected for future updates.

## Progress Tracker

| Task | Status |
|---|---|
| Project concept defined | ✅ Completed |
| Initial script created | ✅ Completed |
| Project purpose documented | ✅ Completed |
| Review areas documented | ✅ Completed |
| Audit logic documented | ✅ Completed |
| Screenshots collected | 🚧 In Progress |
| HTML report evidence added | 🚧 In Progress |
| Findings section enriched | 🚧 In Progress |
| YouTube video recorded | ⏳ Pending |
| Final portfolio polish | ⏳ Pending |

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

[Watch the full walkthrough on YouTube](PASTE-YOUR-YOUTUBE-LINK-HERE)

## Portfolio Value

This project is part of my effort to build a cybersecurity portfolio based on practical documentation, structured analysis, and continuous improvement. Its value is not only in the script itself, but also in the ability to explain:

- what was reviewed
- why it matters
- what was found
- what should be improved

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
