# Advanced PowerShell Automation Scripts

![PowerShell](https://img.shields.io/badge/PowerShell-5.1%2B-blue.svg) ![License](https://img.shields.io/badge/License-MIT-green.svg) ![Contributions Welcome](https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg)

## Overview

This repository contains a collection of advanced PowerShell scripts designed for IT administrators and engineers to automate complex tasks, manage infrastructure, and enhance operational efficiency. These scripts go beyond basic helpdesk functions, focusing on workflow automation, system health monitoring, and bulk management.

## Features

-   **Automated User Onboarding/Offboarding:** Streamline the process of setting up new users or decommissioning old ones across various systems.
-   **System Health Reporting:** Proactively monitor and report on the health and performance of Windows servers and workstations.
-   **Bulk Active Directory Management:** Perform operations on multiple AD objects efficiently.

## Scripts Included

| Script                          | Description                                                                                                                                     |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `New-UserOnboarding.ps1`        | Automates the end-to-end onboarding process for a new user, including AD account creation, group assignments, and potential mailbox setup. |
| `Automated-SystemHealthReport.ps1`| Gathers comprehensive system health metrics (CPU, Memory, Disk, Event Logs, Services) and generates a detailed report.                      |

## Usage

These scripts are intended for use by experienced IT professionals. Review each script's parameters and logic before execution. Run PowerShell as an administrator.

### Example: Onboarding a new user

```powershell
./New-UserOnboarding.ps1 -SamAccountName "jdoe" -GivenName "John" -Surname "Doe" -DisplayName "John Doe" -UserPrincipalName "john.doe@yourdomain.com" -ADPath "OU=Users,DC=yourdomain,DC=com" -Password "ComplexP@ssw0rd123" -GroupMemberships "SG-AllStaff,DL-Marketing"
```

## Requirements

-   Windows operating system with PowerShell 5.1 or newer.
-   Active Directory module for PowerShell (RSAT) for AD-related scripts.
-   Appropriate administrative permissions on the domain and target systems.
-   May require additional modules (e.g., `ExchangeOnlineManagement`) depending on the script's functionality.

## Contribution

Contributions, bug reports, and feature requests are welcome. Please open an issue or submit a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

