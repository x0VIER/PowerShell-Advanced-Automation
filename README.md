# ⚡ Advanced PowerShell Automation

<div align="center">

![PowerShell](https://img.shields.io/badge/PowerShell-5.1+-blue.svg)
![Platform](https://img.shields.io/badge/platform-Windows%20Server-0078D4.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Skill Level](https://img.shields.io/badge/Level-Advanced-red.svg)
![Active Directory](https://img.shields.io/badge/Active%20Directory-required-success.svg)

**Enterprise-grade PowerShell automation for complex IT infrastructure management**

</div>

---

## 📋 Overview

Advanced PowerShell Automation is a professional collection of sophisticated scripts designed for IT administrators and engineers managing enterprise Windows environments. These scripts automate complex workflows, streamline bulk operations, and provide comprehensive system monitoring capabilities that go far beyond basic administration tasks.

Perfect for:
- **System Engineers** managing large-scale infrastructure
- **IT Managers** implementing automation strategies
- **DevOps Teams** integrating Windows automation
- **Enterprise Administrators** handling complex workflows

## ✨ Features

### 🚀 Automated User Lifecycle Management
- **End-to-End Onboarding**: Complete user provisioning workflow
- **Bulk Operations**: Process multiple users simultaneously
- **Integration Ready**: Connects with AD, Exchange, and other systems
- **Audit Logging**: Comprehensive tracking of all operations

### 📊 Proactive System Monitoring
- **Health Reporting**: Automated system health assessments
- **Performance Metrics**: CPU, memory, disk, and network monitoring
- **Event Log Analysis**: Intelligent error detection and alerting
- **Service Monitoring**: Track critical service status

### 🔧 Infrastructure Automation
- **Bulk AD Management**: Efficient multi-object operations
- **Configuration Management**: Standardized system configurations
- **Compliance Reporting**: Automated compliance checks
- **Workflow Orchestration**: Complex multi-step automation

## 🛠️ Scripts

### 👤 New-UserOnboarding.ps1

**Comprehensive User Onboarding Automation**

Automate the complete user provisioning process from Active Directory account creation through mailbox setup and group assignments.

**Features:**
- Active Directory account creation with standardized naming
- Automatic group membership assignment
- Home directory creation and permissions
- Email mailbox provisioning (Exchange/Office 365)
- Welcome email generation
- Comprehensive logging and error handling

**Parameters:**
```powershell
-SamAccountName     # Username (required)
-GivenName          # First name (required)
-Surname            # Last name (required)
-DisplayName        # Full display name (required)
-UserPrincipalName  # Email/UPN (required)
-ADPath             # OU path (required)
-Password           # Initial password (required)
-GroupMemberships   # Comma-separated group list (optional)
-Department         # Department name (optional)
-Title              # Job title (optional)
-Manager            # Manager's username (optional)
-CreateMailbox      # Create Exchange mailbox (switch)
```

**Usage Example:**
```powershell
.\New-UserOnboarding.ps1 `
    -SamAccountName "jdoe" `
    -GivenName "John" `
    -Surname "Doe" `
    -DisplayName "John Doe" `
    -UserPrincipalName "john.doe@company.com" `
    -ADPath "OU=Users,OU=Corporate,DC=company,DC=com" `
    -Password "TempP@ssw0rd123!" `
    -GroupMemberships "SG-AllStaff,SG-IT-Department,DL-CompanyWide" `
    -Department "IT" `
    -Title "Systems Administrator" `
    -Manager "jsmith" `
    -CreateMailbox
```

**What It Does:**
1. Creates AD user account with specified attributes
2. Sets password and enforces change at next logon
3. Adds user to specified security and distribution groups
4. Creates home directory with proper permissions
5. Provisions Exchange mailbox (if specified)
6. Sends welcome email with login instructions
7. Logs all actions for audit purposes
8. Returns detailed success/failure report

---

### 📊 Automated-SystemHealthReport.ps1

**Comprehensive System Health Monitoring**

Generate detailed health reports for Windows servers and workstations with proactive alerting and trend analysis.

**Monitors:**
- **CPU Usage**: Current and historical utilization
- **Memory**: Available RAM, page file usage, memory leaks
- **Disk Space**: Free space, growth trends, fragmentation
- **Event Logs**: Critical errors, warnings, security events
- **Services**: Status of critical Windows services
- **Network**: Connectivity, bandwidth, packet loss
- **Updates**: Pending Windows updates and patch status
- **Performance**: System responsiveness and bottlenecks

**Parameters:**
```powershell
-ComputerName       # Target computer(s) - supports arrays
-ReportPath         # Output directory for reports
-EmailReport        # Send report via email (switch)
-SMTPServer         # SMTP server for email delivery
-Recipients         # Email recipients (comma-separated)
-ThresholdCPU       # CPU alert threshold (default: 80%)
-ThresholdMemory    # Memory alert threshold (default: 85%)
-ThresholdDisk      # Disk space alert threshold (default: 90%)
-IncludePerformance # Include detailed performance counters
```

**Usage Example:**
```powershell
# Single server health check
.\Automated-SystemHealthReport.ps1 `
    -ComputerName "SERVER01" `
    -ReportPath "C:\Reports" `
    -EmailReport `
    -SMTPServer "smtp.company.com" `
    -Recipients "it-team@company.com"

# Multiple servers with custom thresholds
.\Automated-SystemHealthReport.ps1 `
    -ComputerName "SERVER01","SERVER02","SERVER03" `
    -ReportPath "\\fileserver\reports" `
    -ThresholdCPU 70 `
    -ThresholdMemory 80 `
    -ThresholdDisk 85 `
    -IncludePerformance
```

**Report Includes:**
- Executive summary with overall health status
- Detailed metrics for each monitored component
- Historical trend analysis (if run regularly)
- Actionable recommendations for issues found
- Color-coded alerts (green/yellow/red)
- Export formats: HTML, CSV, JSON

---

## 🚀 Quick Start

### Prerequisites

**Required:**
- Windows Server 2016+ or Windows 10/11
- PowerShell 5.1 or higher
- Active Directory Module (RSAT)
- Domain Administrator or delegated permissions

**Optional (depending on scripts):**
- Exchange Online Management Module
- Microsoft Graph PowerShell SDK
- SMTP server access for email reports

### Installation

```powershell
# Clone the repository
git clone https://github.com/x0VIER/PowerShell-Advanced-Automation.git
cd PowerShell-Advanced-Automation

# Install required modules
Install-Module -Name ActiveDirectory -Force
Install-Module -Name ExchangeOnlineManagement -Force

# Set execution policy
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

# Verify prerequisites
Get-Module -ListAvailable ActiveDirectory
$PSVersionTable.PSVersion
```

### First-Time Configuration

**1. Configure Email Settings (for reports)**
```powershell
# Edit script variables
$SMTPServer = "smtp.company.com"
$SMTPPort = 587
$SMTPFrom = "automation@company.com"
$SMTPTo = "it-team@company.com"
```

**2. Set Default Paths**
```powershell
# Common configuration
$DefaultOU = "OU=Users,DC=company,DC=com"
$ReportPath = "C:\Reports\SystemHealth"
$LogPath = "C:\Logs\Automation"
```

**3. Test with Non-Production Data**
```powershell
# Always test in lab environment first
.\New-UserOnboarding.ps1 -SamAccountName "testuser" -WhatIf
```

## 💡 Advanced Usage

### Scheduled Automation

**Daily Health Reports:**
```powershell
$Action = New-ScheduledTaskAction -Execute "PowerShell.exe" `
    -Argument "-File C:\Scripts\Automated-SystemHealthReport.ps1 -ComputerName 'SERVER01' -EmailReport"

$Trigger = New-ScheduledTaskTrigger -Daily -At 6am

Register-ScheduledTask -TaskName "Daily Health Report" `
    -Action $Action -Trigger $Trigger -RunLevel Highest
```

**Bulk User Onboarding from CSV:**
```powershell
# Import users from CSV
$Users = Import-Csv "C:\Data\NewHires.csv"

foreach ($User in $Users) {
    .\New-UserOnboarding.ps1 `
        -SamAccountName $User.Username `
        -GivenName $User.FirstName `
        -Surname $User.LastName `
        -DisplayName "$($User.FirstName) $($User.LastName)" `
        -UserPrincipalName "$($User.Username)@company.com" `
        -ADPath $User.OU `
        -Password $User.TempPassword `
        -GroupMemberships $User.Groups `
        -Department $User.Department `
        -CreateMailbox
}
```

### Integration with Ticketing Systems

```powershell
# Example: ServiceNow integration
$Ticket = Get-ServiceNowTicket -Number "INC0012345"
$UserData = $Ticket.RequestedFor

.\New-UserOnboarding.ps1 `
    -SamAccountName $UserData.Username `
    -GivenName $UserData.FirstName `
    -Surname $UserData.LastName `
    # ... additional parameters

# Update ticket with results
Update-ServiceNowTicket -Number $Ticket.Number -Status "Resolved"
```

## 📋 Requirements

| Component | Version | Purpose |
|-----------|---------|---------|
| Windows Server | 2016+ | Host operating system |
| PowerShell | 5.1+ | Script execution engine |
| RSAT Tools | Latest | Active Directory management |
| Exchange Module | Latest | Mailbox provisioning (optional) |
| Admin Permissions | Domain Admin or delegated | Required for AD operations |

### Installing Dependencies

```powershell
# Install RSAT (Windows 10/11)
Add-WindowsCapability -Online -Name Rsat.ActiveDirectory.DS-LDS.Tools~~~~0.0.1.0

# Install Exchange Online Management
Install-Module -Name ExchangeOnlineManagement -Force

# Install Microsoft Graph (for advanced scenarios)
Install-Module -Name Microsoft.Graph -Force
```

## 🔒 Security Best Practices

### Credential Management
- **Never hardcode passwords** in scripts
- Use **secure credential storage** (Windows Credential Manager)
- Implement **least privilege** access model
- Enable **audit logging** for all operations

### Script Execution
- **Code signing**: Sign scripts with trusted certificates
- **Execution policy**: Use RemoteSigned or AllSigned
- **Review before execution**: Always inspect script content
- **Test in lab**: Validate in non-production first

### Audit & Compliance
- **Enable logging**: Comprehensive operation tracking
- **Retain logs**: Meet compliance retention requirements
- **Monitor access**: Track who runs automation scripts
- **Regular reviews**: Audit automation activities

## 🤝 Contributing

We welcome contributions from experienced PowerShell developers!

**Contribution Guidelines:**
1. Fork the repository
2. Create a feature branch
3. Follow PowerShell best practices
4. Include comprehensive help documentation
5. Add parameter validation
6. Test in multiple environments
7. Submit pull request with detailed description

**Script Standards:**
- Use approved PowerShell verbs
- Implement proper error handling
- Include comment-based help
- Support `-WhatIf` and `-Confirm` where appropriate
- Follow consistent naming conventions

## 📝 License

This project is licensed under the MIT License - see the LICENSE.md file for details.

## 🙏 Acknowledgments

- Built for enterprise IT automation
- Inspired by real-world infrastructure challenges
- Community-tested and production-proven

## 📧 Support

- **Issues**: Report bugs via GitHub Issues
- **Security**: Report security concerns privately
- **Questions**: Use GitHub Discussions

## 📚 Additional Resources

- [PowerShell Documentation](https://docs.microsoft.com/powershell/)
- [Active Directory PowerShell](https://docs.microsoft.com/powershell/module/activedirectory/)
- [PowerShell Best Practices](https://docs.microsoft.com/powershell/scripting/developer/cmdlet/cmdlet-development-guidelines)

---

<div align="center">

**Automating enterprise IT, one script at a time**

⭐ Star this repo if it powers your infrastructure!

</div>
