# Coro Cybersecurity Platform Analysis Report

## 1. Service Overview

### 1.1 Basic Information

| Item | Content |
|------|---------|
| **Service Name** | Coro Cybersecurity |
| **Official Website** | https://www.coro.net/ |
| **Documentation** | https://docs.coro.net/ |
| **API** | https://developers.coro.net |
| **Slogan** | "A Modern approach to Cybersecurity" |
| **Main Message** | "Cybersecurity Made Easy For Lean IT Teams" |

### 1.2 Target Users

- **Primary Target**: IT operations teams with limited resources (Lean IT Teams)
- **Use Cases**: Organizations seeking to simplify complex security operations

### 1.3 Global Presence

- Chicago (USA)
- New York (USA)
- London (UK)
- Israel
- Spain
- Italy

---

## 2. Product Architecture

### 2.1 Protection Domains

```
┌─────────────────────────────────────────────────────────────────┐
│                    Coro Cybersecurity Platform                  │
├─────────────┬─────────────┬─────────────┬───────────┬───────────┤
│   Email     │    Cloud    │  Endpoint   │  Network  │   User    │
│  Security   │  Security   │  Security   │   & SWG   │  Security │
├─────────────┼─────────────┼─────────────┼───────────┼───────────┤
│ • Threat    │ • Cloud App │ • Malware   │ • VPN/ZTNA│ • User    │
│   Detection │   Protection│   Protection│ • DNS     │   Protection│
│ • Phishing  │ • DLP       │ • EDR       │   Filtering│ • MFA     │
│   Protection│             │ • Device    │           │   Status  │
│ • Spam      │             │   Management│           │   Monitoring│
│   Filter    │             │             │           │           │
└─────────────┴─────────────┴─────────────┴───────────┴───────────┘
```

### 2.2 Main Module Configuration

| Module | Description | Key Features |
|--------|-------------|--------------|
| **Email Security** | Email security | Threat detection, phishing protection, prompt injection detection |
| **Cloud Security** | Cloud app protection | Access control, threat detection policies, MFA status monitoring |
| **Endpoint Security** | Endpoint protection | Malware protection, USB control, remote management |
| **EDR** | Advanced threat detection | Behavioral detection, allow/blocklists |
| **Network** | Network protection | VPN, ZTNA, site-to-site tunnels |
| **SWG** | Secure Web Gateway | DNS filtering, Shadow AI blocking |
| **Data Governance** | Data governance | Sensitive data detection, DLP |
| **MDM** | Mobile device management | Device policies, remote management |
| **SAT** | Security awareness training | Phishing simulations, education |
| **Coro AI** | AI-assisted features | Security gap analysis, recommendations |

### 2.3 Agent Supported Platforms

| OS | Agent | Key Features |
|----|-------|--------------|
| **Windows** | Windows Agent | Full features (EDR, malware scan, remote uninstallation) |
| **macOS** | macOS Agent | Scheduled scan, EDR, on-access scan |
| **Linux** | Linux Agent | Protection disable, remote shell, basic protection |

---

## 3. Management Console Structure

### 3.1 Actionboard Dashboard

Below is the Coro Console Actionboard dashboard screen:

![Actionboard Dashboard](../../img/actionboard-dashboard.png)

**Key Elements on Screen**:
- **Open Tickets**: Number of open tickets with category breakdown
- **Workspace Health Score**: Workspace health score (0-100)
- **Security Gaps**: Security gap detection status
- **Subscription Overview**: Enable/disable status of each module
- **Module Status**: Status of Cloud Security, Email Security, EDR, etc.

### 3.2 View Hierarchy

```
┌─────────────────────────────────────────┐
│            Global View (MSP)            │
│  • Multi-workspace centralized mgmt     │
│  • Hierarchy tree display               │
│  • Global policies                      │
├─────────────────────────────────────────┤
│         Workspace View (Customer)       │
│  • Individual organization management   │
│  • Actionboard                          │
│  • Ticket log                           │
└─────────────────────────────────────────┘
```

### 3.3 Main UI Elements

| Element | Description |
|---------|-------------|
| **Actionboard** | Dashboard (open tickets, protection status, health score) |
| **Ticket Log** | Security event management (4-tab structure: Overview, Full details, Activity logs, Comments) |
| **Protected Users** | List of protected users |
| **Devices** | List of protected devices |
| **Setup Hub** | New workspace onboarding |
| **Coro Insights** | Analytics & reporting features |

### 3.4 Notification Settings and Threat Types

Below is the list of threat types visible in the notification settings screen:

![Notification Settings - Threat Types](../../img/notification-settings-threat-types.png)

**Detectable Threat Types by Module**:

| Module | Threat Types |
|--------|--------------|
| **Cloud Security** | Abnormal Admin Activity, Access Permissions Violation, Impossible Traveler, Malware in Cloud Drive, Mass Data Deletion, Mass Data Download, Suspected Bot Attacks, Suspected Identity Compromise |
| **Email Security** | Blocklisted Sender, Brand Impersonation, Domain Spoofing, Malware in Email Attachment, **Prompt Injection**, Spam, Suspicious Content, User Impersonation, etc. |
| **Endpoint Security** | Endpoint Vulnerability, Forbidden Wi-Fi Connection, Malware on Endpoint, WiFi Phishing |
| **Data Governance** | Cloud Share Containing Sensitive Data, Email Containing Sensitive Data, Endpoint Drive Containing Sensitive Data |
| **EDR** | Command and Control, Credential Access, Defense Evasion, Discovery, Execution, Initial Access, Persistence, Privilege Escalation |

---

## 4. Supported Cloud Applications

### 4.1 Primary Integrations

| Application | Features | Notes |
|-------------|----------|-------|
| **Microsoft 365** | Email protection, cloud security, MFA status detection | Additional permissions may be required |
| **Google Workspace** | Email protection, cloud security, MFA status detection | |

### 4.2 Detectable Threat Types

- Abnormal Admin Activity
- Mass Data Deletion
- Mass Data Download
- Suspected Bot Attack
- Suspected Identity Compromise
- Impossible Traveler

---

## 5. Compliance & Data Protection

### 5.1 Regional Sensitive Data Detection

| Region | Detectable Data Types |
|--------|----------------------|
| **UAE** | ID number, UID number, visa file number, passport number, driver's license number |
| **Brazil** | CPF (individual taxpayer ID), passport number, bank card number, CNH (driver's license), CNPJ (legal entity number) |
| **Other** | Various international standards (credit cards, SSN, etc.) |

---

## 6. Language Support

### 6.1 Coro Console

- English
- French (Canada) ← Added in v3.7

### 6.2 Security Awareness Training (SAT)

- English (US) - US region only
- English (UK)
- English (AUS) - US region only
- Italian
- Spanish
- French (France)

---

## 7. Technical Features

### 7.1 Architecture

- **Cloud Native**: SaaS security platform
- **Multi-tenant**: MSP-ready workspace separation
- **API Support**: Public API provided (developers.coro.net)

### 7.2 Integration Features

- **Remote Shell**: Windows, macOS, Linux support
- **Remote Uninstallation**: Windows Agent
- **Automatic Policy Application**: Group and label-based

---

*Created Date: 2026-01-22*
*Target Versions: v3.7, v3.8*
