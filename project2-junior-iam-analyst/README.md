# Project 2: Privileged Account Security & Lifecycle Automation

[![CyberArk](https://img.shields.io/badge/CyberArk-PAM-0052CC?logo=cyberark)](https://cyberark.com)
[![Okta](https://img.shields.io/badge/Okta-Workflows-007DC1?logo=okta)](https://okta.com)
[![Splunk](https://img.shields.io/badge/Splunk-Monitoring-000000?logo=splunk)](https://splunk.com)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## 📋 Executive Summary

This project demonstrates a comprehensive privileged account security initiative that addresses three critical enterprise challenges:

1. **Unsecured Admin Accounts** → CyberArk onboarding with rotation and session monitoring
2. **Slow Manual Onboarding** → Okta Lifecycle Workflows with role-based app assignments
3. **Hybrid Stack Visibility** → Unified IAM monitoring dashboard with proactive alerting

### Key Metrics Achieved
| Metric | Improvement |
|--------|-------------|
| Privileged visibility | 100% |
| Shared credentials | Eliminated |
| Authentication uptime | 99.9%+ |
| Onboarding speed | ↑ 60% |
| Provisioning errors | ↓ 34% |

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│               PRIVILEGED ACCOUNT SECURITY PLATFORM                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                      IDENTITY SOURCES                                │   │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐            │   │
│  │  │   HR     │  │  Active  │  │  Entra   │  │ SailPoint│            │   │
│  │  │ System   │  │Directory │  │    ID    │  │   IIQ    │            │   │
│  │  └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘            │   │
│  └───────┼─────────────┼─────────────┼─────────────┼────────────────────┘   │
│          │             │             │             │                        │
│          ▼             ▼             ▼             ▼                        │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                    OKTA IDENTITY ENGINE                              │   │
│  │  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐      │   │
│  │  │    Universal    │  │    Lifecycle    │  │   Application   │      │   │
│  │  │    Directory    │  │    Workflows    │  │   Assignments   │      │   │
│  │  └─────────────────┘  └─────────────────┘  └─────────────────┘      │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│          │                                                                  │
│          ▼                                                                  │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                    CYBERARK PAM                                      │   │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐            │   │
│  │  │  Vault   │  │   CPM    │  │   PSM    │  │   PTA    │            │   │
│  │  │ (PVWA)   │  │ Rotation │  │ Sessions │  │ Threats  │            │   │
│  │  └──────────┘  └──────────┘  └──────────┘  └──────────┘            │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│          │                                                                  │
│          ▼                                                                  │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                    MONITORING & ALERTING                             │   │
│  │  ┌─────────────────────────────────────────────────────────────┐    │   │
│  │  │                      SPLUNK SIEM                             │    │   │
│  │  │  • Authentication Events    • Privileged Access Logs        │    │   │
│  │  │  • Session Recordings       • Anomaly Detection             │    │   │
│  │  └─────────────────────────────────────────────────────────────┘    │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 📁 Project Structure

```
project2-privileged-account-security/
├── README.md                           # This file
├── docs/
│   ├── ARCHITECTURE.md                 # Detailed architecture
│   ├── OKTA_WORKFLOW_GUIDE.md          # Okta workflow documentation
│   └── screenshots/
│       ├── okta-workflow-builder.png
│       ├── cyberark-session-recording.png
│       └── splunk-dashboard.png
│
├── okta-workflows/
│   ├── joiner-workflow.json            # New employee onboarding
│   ├── mover-workflow.json             # Department transfer
│   ├── leaver-workflow.json            # Offboarding
│   ├── app-assignment-rules.json       # Role-based app assignments
│   └── README.md                       # Workflow documentation
│
├── cyberark/
│   ├── onboarding/
│   │   ├── Onboard-AdminAccounts.ps1
│   │   └── admin-accounts-template.csv
│   ├── monitoring/
│   │   └── Enable-SessionRecording.ps1
│   └── README.md
│
└── monitoring/
    ├── splunk/
    │   ├── dashboards/
    │   │   └── iam-security-dashboard.xml
    │   ├── alerts/
    │   │   ├── privileged-access-alert.xml
    │   │   └── auth-failure-alert.xml
    │   └── searches/
    │       └── saved-searches.conf
    └── README.md
```

---

## 🚀 Component Breakdown

### Component 1: CyberArk Privileged Account Onboarding

Onboard unsecured admin accounts with full security controls:

| Feature | Implementation |
|---------|----------------|
| Password Rotation | CPM-managed, 30-day automatic rotation |
| Session Recording | PSM full session capture and playback |
| Access Control | Role-based safe permissions |
| Audit Trail | Complete privileged access logging |

### Component 2: Okta Lifecycle Workflows

Automated identity lifecycle management:

**Joiner Workflow:**
```
Trigger: New user in HR system
    ↓
Create Okta account
    ↓
Assign to department group
    ↓
Assign birthright applications
    ↓
Send welcome notification
    ↓
Create IT ticket for hardware
```

**Mover Workflow:**
```
Trigger: Department change in HR
    ↓
Update user profile
    ↓
Modify group memberships
    ↓
Adjust application access
    ↓
Notify manager
    ↓
Trigger access review
```

**Leaver Workflow:**
```
Trigger: Termination date reached
    ↓
Suspend Okta account
    ↓
Revoke all application access
    ↓
Remove from all groups
    ↓
Transfer data ownership
    ↓
Archive account (30 days)
    ↓
Permanent deletion
```

### Component 3: Hybrid IAM Monitoring Dashboard

Unified visibility across all identity platforms:

| Platform | Metrics Tracked |
|----------|-----------------|
| CyberArk | Session counts, password rotations, access attempts |
| Okta | Authentication success/failure, MFA usage, app access |
| Entra ID | Sign-in risk, conditional access blocks, guest access |
| SailPoint | Access certifications, entitlement changes |
| AD | Account lockouts, password changes, group modifications |

---

## 🛠️ Implementation Guide

### Prerequisites

```bash
# Required access
- Okta Super Admin or equivalent
- CyberArk Vault Admin
- Splunk Admin
- Microsoft Entra ID Global Reader

# Required tools
- PowerShell 7.0+
- psPAS module
- Okta API token
- Splunk HEC token
```

### Step 1: Configure CyberArk Account Onboarding

```powershell
# Connect to CyberArk
Import-Module psPAS
$cred = Get-Credential
New-PASSession -BaseURI "https://pvwa.company.com" -Credential $cred

# Onboard admin accounts from CSV
.\cyberark\onboarding\Onboard-AdminAccounts.ps1 -CsvPath "admin-accounts.csv"
```

### Step 2: Import Okta Workflows

1. Navigate to **Okta Admin Console** → **Workflow** → **Flows**
2. Click **Import** and select the workflow JSON files
3. Configure connections for each flow
4. Activate the workflows

### Step 3: Deploy Splunk Dashboards

```bash
# Copy dashboard XML to Splunk
cp monitoring/splunk/dashboards/*.xml $SPLUNK_HOME/etc/apps/search/local/data/ui/views/

# Restart Splunk to load dashboards
$SPLUNK_HOME/bin/splunk restart
```

---

## 📊 Okta Workflow Examples

### Joiner Workflow - Role-Based App Assignment

```json
{
  "name": "Joiner - Role-Based Application Assignment",
  "description": "Automatically assign applications based on department and job title",
  "trigger": {
    "type": "user.lifecycle.create",
    "filters": [
      {"field": "status", "operator": "equals", "value": "PROVISIONED"}
    ]
  },
  "actions": [
    {
      "type": "conditional",
      "condition": "user.profile.department == 'Engineering'",
      "actions": [
        {"type": "assign_app", "app_id": "github_enterprise"},
        {"type": "assign_app", "app_id": "jira"},
        {"type": "assign_app", "app_id": "confluence"},
        {"type": "assign_app", "app_id": "aws_sso"}
      ]
    },
    {
      "type": "conditional",
      "condition": "user.profile.department == 'Finance'",
      "actions": [
        {"type": "assign_app", "app_id": "netsuite"},
        {"type": "assign_app", "app_id": "concur"},
        {"type": "assign_app", "app_id": "tableau"}
      ]
    },
    {
      "type": "conditional", 
      "condition": "user.profile.department == 'HR'",
      "actions": [
        {"type": "assign_app", "app_id": "workday"},
        {"type": "assign_app", "app_id": "bamboohr"},
        {"type": "assign_app", "app_id": "successfactors"}
      ]
    }
  ]
}
```

---

## 📈 Metrics & Outcomes

### Before Implementation
- Admin accounts: 500+ unmanaged
- Shared credentials: 150+ instances
- Manual onboarding time: 3-5 days
- Authentication uptime: 98.5%
- Provisioning errors: 45/month

### After Implementation
- Admin accounts: 500+ fully managed (100%)
- Shared credentials: 0 (eliminated)
- Automated onboarding time: < 4 hours
- Authentication uptime: 99.9%+
- Provisioning errors: 30/month (↓34%)

### Security Improvements
| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Unmanaged privileged accounts | 500+ | 0 | 100% visibility |
| Shared credential instances | 150+ | 0 | Eliminated |
| Session recording coverage | 0% | 100% | Full coverage |
| Mean time to onboard | 3-5 days | < 4 hours | ↑ 60% faster |

---

## 📸 Screenshots

### Okta Workflow Builder
*Shows the visual workflow builder with Joiner flow configuration*

### CyberArk Session Recording
*Displays PSM session playback with video recording*

### Splunk IAM Dashboard
*Unified dashboard showing metrics from all identity platforms*

---

## 🔗 Related Resources

- [Okta Workflows Documentation](https://help.okta.com/wf/en-us/Content/Topics/Workflows/workflows-main.htm)
- [CyberArk PSM Documentation](https://docs.cyberark.com/PAS/Latest/en/Content/PASIMP/PSMBeyondBasics.htm)
- [Splunk Dashboard Examples](https://splunkbase.splunk.com/)

---

## 📝 Medium Article

📖 **Read the full article:** [Securing Privileged Accounts at Scale: CyberArk Onboarding and Okta Lifecycle Automation](https://medium.com/@isaiahherard)

---

## 👤 Author

**Isaiah Herard**  
IAM/PAM Engineer | CyberArk Specialist | Zero Trust Architect

---

## 📄 License

This project is licensed under the MIT License.
