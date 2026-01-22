# Coro Cybersecurity v3.7/v3.8 Evaluation Procedure Guide

## Document Information

| Item | Content |
|------|---------|
| **Document Name** | Coro Cybersecurity v3.7/v3.8 Evaluation Procedure Guide |
| **Created Date** | January 22, 2026 |
| **Version** | 1.0 |
| **Audience** | Evaluators, Claude Code |
| **Related Issue** | [GitHub Issue #1](https://github.com/takaos/coro-net/issues/1) |

---

## 0. Context Restoration Guide (For Claude Code)

> **Important**: This section is intended for Claude Code to reference when restoring context.

### 0.1 Required Documents List

Before resuming work, **always** read the following documents:

| Priority | Document | Path | Content |
|----------|----------|------|---------|
| **Required** | Evaluation Plan | `docs/evaluation-plan.md` | Evaluation items, constraints, schedule |
| **Required** | This Procedure Guide | `docs/evaluation-procedure.md` | Execution procedures, checklists |
| Recommended | Release Notes Analysis | `docs/analysis/release-notes-analysis.md` | v3.7/v3.8 feature details |
| Reference | Service Overview | `docs/analysis/coro-service-overview.md` | Coro platform overview |

### 0.2 Evaluation Environment Constraints (Critical)

```
┌─────────────────────────────────────────────────────────────────┐
│                   Evaluation Environment Constraints             │
├─────────────────────────────────────────────────────────────────┤
│  ✅ Available                   │  ❌ Not Available              │
├─────────────────────────────────┼────────────────────────────────┤
│  Google Workspace               │  Microsoft 365                 │
│  macOS                          │  Windows                       │
│  Linux                          │                                │
│  English, Japanese              │  French, Other languages       │
│  English-speaking regions,      │  UAE, Brazil sensitive data    │
│  Japan sensitive data           │                                │
└─────────────────────────────────┴────────────────────────────────┘
```

### 0.3 Evaluation ID System

Evaluation items are managed using the following ID system:

| Prefix | Category | Example |
|--------|----------|---------|
| `SEC-AI-xxx` | Security/AI-related | SEC-AI-001: Prompt Injection Detection |
| `SEC-AUTH-xxx` | Security/Authentication | SEC-AUTH-001: MFA Status Detection |
| `MGT-CON-xxx` | Management/Console | MGT-CON-001: Actionboard Redesign |
| `MGT-DEV-xxx` | Management/Device | MGT-DEV-002: Remote Shell |
| `CMP-DATA-xxx` | Compliance/Data | CMP-DATA-002: Japan Sensitive Data Detection |
| `INT-CLOUD-xxx` | Integration/Cloud | INT-CLOUD-001: Google Workspace MFA |
| `INT-AGT-xxx` | Integration/Agent | INT-AGT-001: macOS Agent 3.7 |

### 0.4 How to Check Current Progress

Check progress via GitHub Issue:

```bash
gh issue view 1 --comments
```

---

## 1. Evaluation Procedure Overview

### 1.1 Overall Evaluation Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                     Evaluation Execution Flow                    │
└─────────────────────────────────────────────────────────────────┘

Phase 1: Environment Setup ────────────────────────────────────────
    │
    ├── 1.1 Coro Workspace Configuration
    ├── 1.2 Google Workspace Integration
    ├── 1.3 macOS Agent Setup
    ├── 1.4 Linux Agent Setup
    └── 1.5 Test Data Preparation
    │
    ▼ Checkpoint: Environment Setup Complete
    │
Phase 2: Security Feature Evaluation ──────────────────────────────
    │
    ├── 2.1 Prompt Injection Detection [SEC-AI-001]【Highest Priority】
    ├── 2.2 MFA Status Detection [SEC-AUTH-001]【Highest Priority】
    ├── 2.3 Shadow AI Blocklist [SEC-AI-002]
    ├── 2.4 Threat Detection Policies [SEC-AUTH-002]
    └── 2.5 Coro AI Summary [SEC-AI-003]
    │
    ▼ Checkpoint: Security Evaluation Complete
    │
Phase 3: Management Feature Evaluation ────────────────────────────
    │
    ├── 3.1 Actionboard Redesign [MGT-CON-001]
    ├── 3.2 Ticket Structure [MGT-CON-002]
    ├── 3.3 Bulk Ticket Actions [MGT-CON-003]
    ├── 3.4 Setup Hub [MGT-CON-004]
    ├── 3.5 Security Gaps [MGT-CON-006]
    ├── 3.6 Remote Shell - Linux [MGT-DEV-002]
    └── 3.7 Scheduled Scan - macOS [MGT-DEV-003]
    │
    ▼ Checkpoint: Management Evaluation Complete
    │
Phase 4: Compliance & Integration Evaluation ──────────────────────
    │
    ├── 4.1 English-region Sensitive Data Detection [CMP-DATA-001]
    ├── 4.2 Japan Sensitive Data Detection [CMP-DATA-002]
    ├── 4.3 Google Workspace Integration [INT-CLOUD-001~004]
    ├── 4.4 macOS Agent 3.7 [INT-AGT-001]
    └── 4.5 Linux Agent 3.7 [INT-AGT-002]
    │
    ▼ Checkpoint: All Evaluations Complete
    │
Phase 5: Overall Evaluation & Report Creation ─────────────────────
    │
    ├── 5.1 Compile Evaluation Results
    ├── 5.2 Scoring
    ├── 5.3 Issues & Improvement Points Summary
    └── 5.4 Final Report Creation
    │
    ▼ Complete
```

### 1.2 Evaluation Scoring Criteria

| Score | Rating | Criteria |
|-------|--------|----------|
| **5** | Excellent | Exceeds expectations. Provides additional value |
| **4** | Good | Meets expectations. Usable without issues |
| **3** | Acceptable | Minor issues exist but usable for business |
| **2** | Needs Improvement | Significant issues exist, improvement required |
| **1** | Unacceptable | Does not function, unusable |

### 1.3 Evaluation Record Template

Record each evaluation item using the following format:

```markdown
## [Evaluation ID] Evaluation Item Name

### Basic Information
- **Target Version**: v3.7 / v3.8
- **Evaluation Date**: YYYY-MM-DD
- **Evaluator**:

### Test Environment
- **OS/Device**:
- **Coro Version**:
- **Related Settings**:

### Test Results

| Test Case | Expected Result | Actual Result | Pass/Fail |
|-----------|-----------------|---------------|-----------|
| TC-001: xxx | xxx | xxx | Pass/Fail |

### Screenshots
- [ ] Settings screen
- [ ] Execution result
- [ ] Error (if occurred)

### Evaluation Score: X/5

### Observations & Issues
-
-

### Improvement Suggestions
-
```

---

## 2. Phase 1: Environment Setup Procedure

### 2.1 Coro Workspace Configuration

**Objective**: Prepare the Coro workspace for evaluation

**Procedure**:

```
Step 1: Log in to Coro Console
    │
    ├── URL: https://console.coro.net/
    └── Log in with administrator account
    │
Step 2: Verify/Create Workspace
    │
    ├── Verify existence of evaluation workspace
    ├── Create new one if not exists
    └── Verify all modules are enabled
    │
Step 3: Verify Module Enablement
    │
    ├── Email Security: ✅
    ├── Cloud Security: ✅
    ├── Endpoint Security: ✅
    ├── EDR: ✅
    ├── Network/SWG: ✅
    ├── Data Governance: ✅
    └── Coro AI: ✅
    │
Step 4: Basic Settings
    │
    ├── Language setting: English
    ├── Timezone: Set appropriately
    └── Notification settings: Enable
```

**Confirmation Checklist**:

- [ ] Can log in to Coro Console
- [ ] Evaluation workspace is available
- [ ] All modules are enabled
- [ ] Have administrator privileges

### 2.2 Google Workspace Integration Setup

**Objective**: Integrate Google Workspace with Coro

**Reference**: `docs/evaluation-plan.md` - Section 3.4.1

**Prerequisites**:
- Google Workspace administrator privileges
- Coro Cloud Security integration permissions

**Procedure**:

```
Step 1: Preparation in Google Workspace Admin Console
    │
    ├── Log in to admin.google.com
    ├── Go to Security > API controls
    └── Verify third-party app access settings
    │
Step 2: Integration Setup in Coro
    │
    ├── Control Panel > Cloud Security
    ├── Click "Add Cloud Application"
    ├── Select Google Workspace
    └── Complete OAuth authentication
    │
Step 3: Verify Permissions
    │
    ├── Email access permissions
    ├── Drive access permissions
    └── User information access permissions
    │
Step 4: Integration Test
    │
    ├── Verify users appear in Protected Users
    └── Verify connection status in Cloud Security dashboard
```

**Troubleshooting**:

| Problem | Cause | Solution |
|---------|-------|----------|
| Integration doesn't complete | Insufficient permissions | Request additional permissions from Google Workspace admin |
| Users don't appear | Sync delay | Wait 15-30 minutes and recheck |
| "Disconnected" status | Token expired | Re-authenticate integration |

**Confirmation Checklist**:

- [ ] Google Workspace integration complete
- [ ] Users appear in Protected Users
- [ ] Connection status shows "Connected"

### 2.3 macOS Agent Setup

**Objective**: Install and configure Coro Agent 3.7 on macOS device

**Reference**: `docs/evaluation-plan.md` - Section 3.4.2, INT-AGT-001

**Prerequisites**:
- Latest macOS version (recommended)
- Administrator privileges

**Procedure**:

```
Step 1: Download Agent
    │
    ├── Coro Console > Devices > "Add Device"
    ├── Select macOS
    └── Download installer
    │
Step 2: Installation
    │
    ├── Run .pkg file
    ├── Grant Full Disk Access in System Preferences
    └── Allow network extension (if required)
    │
Step 3: Verify Registration
    │
    ├── Coro Console > Devices
    ├── Verify device appears
    └── Verify Agent version is 3.7 or later
    │
Step 4: Protection Settings
    │
    ├── Verify Endpoint Security is enabled
    ├── Verify EDR is enabled
    └── Configure scheduled scan (for evaluation)
```

**Confirmation Checklist**:

- [ ] macOS Agent 3.7 installation complete
- [ ] Device appears in Coro Console
- [ ] Endpoint Security enabled
- [ ] EDR enabled

### 2.4 Linux Agent Setup

**Objective**: Install and configure Coro Agent 3.7 on Linux device

**Reference**: `docs/evaluation-plan.md` - Section 3.4.2, INT-AGT-002

**Prerequisites**:
- Ubuntu 22.04 LTS or RHEL 9
- root/sudo privileges

**Procedure**:

```
Step 1: Download Agent
    │
    ├── Coro Console > Devices > "Add Device"
    ├── Select Linux
    └── Copy installation command
    │
Step 2: Installation (Ubuntu example)
    │
    ├── curl -sL <download-url> | sudo bash
    └── Wait for installation to complete
    │
Step 3: Verify Registration
    │
    ├── Coro Console > Devices
    ├── Verify device appears
    └── Verify Agent version is 3.7 or later
    │
Step 4: Protection Settings
    │
    ├── Verify Endpoint Security is enabled
    └── Verify remote shell permissions
```

**Confirmation Checklist**:

- [ ] Linux Agent 3.7 installation complete
- [ ] Device appears in Coro Console
- [ ] Endpoint Security enabled
- [ ] Remote shell access available

### 2.5 Test Data Preparation

**Objective**: Prepare test data for evaluation

**Reference**: `docs/evaluation-plan.md` - Section 5.3

#### 2.5.1 Prompt Injection Test Emails

Prepare the following test emails:

| Test ID | Subject | Body Pattern | Expected Result |
|---------|---------|--------------|-----------------|
| PI-001 | "Ignore previous instructions" | Explicit prompt injection | Detected |
| PI-002 | "Meeting Request" | Encoded prompt (Base64) | Detection verification |
| PI-003 | "AI Conference Invitation" | Legitimate AI-related business email | Normal delivery |
| PI-004 | "System prompt override" | Multiple pattern combination | Detected |

#### 2.5.2 Sensitive Data Test Files

**Japan Test Data**:

```
# test-sensitive-jp.txt
My Number: 123456789012
Driver's License Number: 012345678901
Passport Number: AB1234567
Health Insurance Number: 12345678
```

**English-region Test Data**:

```
# test-sensitive-en.txt
Social Security Number: 123-45-6789
Credit Card: 4111-1111-1111-1111
Bank Account: 123456789012
Passport: A12345678
```

**Confirmation Checklist**:

- [ ] Prompt injection test emails prepared
- [ ] Japan sensitive data test file prepared
- [ ] English-region sensitive data test file prepared

### 2.6 Phase 1 Completion Check

Verify all of the following are complete:

```
Phase 1 Completion Checklist
├── [ ] Coro workspace configuration complete
├── [ ] Google Workspace integration complete
├── [ ] macOS Agent 3.7 setup complete
├── [ ] Linux Agent 3.7 setup complete
├── [ ] Test data preparation complete
└── [ ] Progress reported to GitHub Issue
```

**GitHub Issue Update Command**:

```bash
gh issue comment 1 --body "## Phase 1: Environment Setup Complete

### Completed Items
- [x] Coro workspace configuration
- [x] Google Workspace integration
- [x] macOS Agent 3.7 setup
- [x] Linux Agent 3.7 setup
- [x] Test data preparation

### Notes
(Record any issues or notes)

---
*Next Step: Phase 2 Security Feature Evaluation*"
```

---

## 3. Phase 2: Security Feature Evaluation Procedure

### 3.1 SEC-AI-001: Prompt Injection Detection【Highest Priority】

**Reference**: `docs/evaluation-plan.md` - Section 3.1.1

**Evaluation Objective**: Evaluate AI prompt injection detection accuracy in email body and subject

**Prerequisites**:
- Google Workspace integrated
- Email Security enabled

**Test Procedure**:

```
Step 1: Verify Detection Policy
    │
    ├── Control Panel > Email Security
    ├── Verify Threat Detection settings
    └── Verify Prompt Injection detection is enabled
    │
Step 2: Execute Test Cases
    │
    ├── TC-001: Explicit Prompt Injection
    │   ├── Send test email (PI-001)
    │   ├── Measure time to detection
    │   └── Verify ticket creation
    │
    ├── TC-002: Encoded Prompt
    │   ├── Send test email (PI-002)
    │   └── Verify detection capability
    │
    └── TC-003: Normal Email False Positive Check
        ├── Send test email (PI-003)
        └── Verify normal delivery
    │
Step 3: Record Results
    │
    ├── Detection rate (True Positive Rate)
    ├── False positive rate (False Positive Rate)
    ├── Time to detection
    └── Ticket information accuracy
```

**Evaluation Criteria**:

| Criteria | Evaluation Standard | Weight |
|----------|---------------------|--------|
| Detection Rate | Detection rate of malicious prompts | 40% |
| False Positive Rate | False positive rate of normal emails | 30% |
| Detection Speed | Time to detection | 15% |
| Alert Quality | Accuracy of ticket information | 15% |

**Result Recording Template**:

```markdown
## SEC-AI-001: Prompt Injection Detection Evaluation Results

### Test Results Summary

| Test Case | Expected Result | Actual Result | Detection Time | Pass/Fail |
|-----------|-----------------|---------------|----------------|-----------|
| TC-001 | Detected | | | |
| TC-002 | Detection verified | | | |
| TC-003 | Normal delivery | | | |

### Score: X/5

### Observations
-

### Screenshots
- [ ] Detection settings screen
- [ ] Ticket details
- [ ] False positive verification
```

### 3.2 SEC-AUTH-001: MFA Status Detection (Google Workspace)【Highest Priority】

**Reference**: `docs/evaluation-plan.md` - Section 3.1.2

**Evaluation Objective**: Evaluate Google Workspace MFA status detection accuracy

**Prerequisites**:
- Google Workspace integrated
- 3+ users with MFA enabled
- 2+ users with MFA disabled

**Test Procedure**:

```
Step 1: Verify Current MFA Status
    │
    ├── Verify MFA status in Google Workspace admin console
    └── Note MFA settings for each user
    │
Step 2: Verify Detection in Coro
    │
    ├── Control Panel > Protected Users
    ├── Verify MFA status label display
    │   ├── "MFA enabled" label
    │   └── "MFA not enabled" label
    └── Filter users by MFA status using filter function
    │
Step 3: Execute Test Cases
    │
    ├── TC-001: MFA Enabled User Detection
    │   └── Verify "MFA enabled" label displays correctly
    │
    ├── TC-002: MFA Disabled User Detection
    │   └── Verify "MFA not enabled" label displays correctly
    │
    ├── TC-003: MFA Status Change Reflection
    │   ├── Change MFA status in Google Workspace
    │   └── Measure reflection time to Coro
    │
    └── TC-004: Filtering Function
        ├── Filter by MFA enabled
        └── Filter by MFA not enabled
```

**Evaluation Criteria**:

| Criteria | Evaluation Standard | Weight |
|----------|---------------------|--------|
| Detection Accuracy | Accurate detection of MFA status | 40% |
| Update Speed | Time for status change reflection | 25% |
| UI Display | Accuracy of label display | 20% |
| Filter Function | Normal operation of filtering | 15% |

### 3.3 SEC-AI-002: Shadow AI Blocklist

**Reference**: `docs/evaluation-plan.md` - Section 3.1.1

**Evaluation Objective**: Evaluate AI chatbot access blocking functionality

**Test Procedure**:

```
Step 1: Verify Shadow AI Blocklist
    │
    ├── Control Panel > SWG > DNS Filtering
    ├── Verify default list in "Shadow AI" category
    └── Review list of blocked sites
    │
Step 2: Block Test
    │
    ├── Enable SWG on test device
    ├── Attempt to access AI service in blocklist
    └── Verify access is blocked
    │
Step 3: Allow List Configuration
    │
    ├── Add specific AI service to allow list
    └── Verify access becomes available
```

### 3.4 SEC-AUTH-002: Threat Detection Policies

**Reference**: `docs/evaluation-plan.md` - Section 3.1.3

**Evaluation Objective**: Verify operation of new threat detection types

**Detection Types to Test**:

| Detection Type | Test Method | Expected Result |
|----------------|-------------|-----------------|
| Abnormal Admin Activity | Admin operations outside normal hours | Detection & ticket creation |
| Mass Data Deletion | Large file deletion | Detection & ticket creation |
| Mass Data Download | Large file download | Detection & ticket creation |
| Suspected Bot Attack | Automated access pattern | Detection & ticket creation |
| Suspected Identity Compromise | Abnormal login pattern | Detection & ticket creation |

**Note**: Tests should be conducted within scope that does not affect production environment

### 3.5 Phase 2 Completion Check

```
Phase 2 Completion Checklist
├── [ ] SEC-AI-001: Prompt Injection Detection Complete
├── [ ] SEC-AUTH-001: MFA Status Detection Complete
├── [ ] SEC-AI-002: Shadow AI Blocklist Complete
├── [ ] SEC-AUTH-002: Threat Detection Policies Complete
├── [ ] SEC-AI-003: Coro AI Summary Complete
└── [ ] Progress reported to GitHub Issue
```

---

## 4. Phase 3: Management Feature Evaluation Procedure

### 4.1 MGT-CON-001~006: Console Feature Evaluation

**Reference**: `docs/evaluation-plan.md` - Section 3.2.1

#### 4.1.1 Actionboard Redesign (MGT-CON-001)

**Evaluation Points**:
- Open ticket summary display
- Links to protected devices/users
- Workspace health score

**Test Procedure**:

```
Step 1: Verify Actionboard Display
    │
    ├── Access dashboard
    ├── Verify display of each section
    └── Verify link functionality
    │
Step 2: Verify Health Score
    │
    ├── Understand score calculation logic
    └── Verify display accuracy
```

#### 4.1.2 Bulk Ticket Actions (MGT-CON-003)

**Evaluation Points**:
- Multiple ticket selection
- Bulk action execution
- Processing completion verification

**Test Procedure**:

```
Step 1: Bulk Operation on Same Type Tickets
    │
    ├── Select multiple malware detection tickets
    ├── Execute bulk Quarantine action
    └── Verify applied to all tickets
    │
Step 2: Bulk Operation on Large Number of Tickets
    │
    ├── Select 50+ tickets
    └── Verify performance & completion
```

#### 4.1.3 Security Gaps (MGT-CON-006)

**Evaluation Points**:
- Security gap detection
- Recommended action display
- Update after improvement

**Target Gaps to Detect**:

| Category | Gap |
|----------|-----|
| Cloud Security | No Cloud Application Connected |
| Cloud Security | No Access Permission Rules Configured |
| Devices | Agent Protection Limited by Security Software Conflict |
| Data Governance | Privacy Sensitive Data Types Not Configured |

### 4.2 MGT-DEV-002: Remote Shell (Linux)

**Reference**: `docs/evaluation-plan.md` - Section 3.2.2

**Evaluation Objective**: Verify Linux remote shell access operation

**Prerequisites**:
- Linux Agent 3.7 or later installed
- Device is online
- Remote shell permissions granted

**Test Procedure**:

```
Step 1: Normal Remote Shell Connection
    │
    ├── Coro Console > Devices > Target device
    ├── Click "Remote Shell"
    ├── Wait for connection complete
    └── Verify basic command execution
        ├── ls
        ├── pwd
        ├── cat /etc/os-release
        └── uname -a
    │
Step 2: Session Management
    │
    ├── Verify session timeout
    ├── Verify multiple session behavior
    └── Verify session termination
    │
Step 3: Permission Control
    │
    ├── Verify executable commands
    └── Verify dangerous command blocking
```

**Evaluation Criteria**:

| Criteria | Evaluation Standard |
|----------|---------------------|
| Connection Stability | Success rate of connections, disconnection frequency |
| Response | Command execution response time |
| Security | Appropriateness of permission control |
| Audit Log | Operation log recording |

### 4.3 MGT-DEV-003: Scheduled Malware Scan (macOS)

**Reference**: `docs/evaluation-plan.md` - Section 3.2.2

**Evaluation Objective**: Verify macOS scheduled scan operation

**Test Procedure**:

```
Step 1: Schedule Configuration
    │
    ├── Control Panel > Endpoint Security
    ├── Open scheduled scan settings
    └── Configure daily scan (set near time for testing)
    │
Step 2: Verify Scan Execution
    │
    ├── Verify scan starts at scheduled time
    ├── Verify scan completion
    └── Verify scan results in log
    │
Step 3: Detection Test
    │
    ├── Place EICAR test file
    ├── Execute scan
    └── Verify ticket creation
```

### 4.4 Phase 3 Completion Check

```
Phase 3 Completion Checklist
├── [ ] MGT-CON-001: Actionboard Redesign Complete
├── [ ] MGT-CON-002: Updated Ticket Structure Complete
├── [ ] MGT-CON-003: Bulk Ticket Actions Complete
├── [ ] MGT-CON-004: Setup Hub Complete
├── [ ] MGT-CON-005: Hierarchy Tree Complete
├── [ ] MGT-CON-006: Security Gaps Complete
├── [ ] MGT-DEV-001: Agent Health Filter Complete
├── [ ] MGT-DEV-002: Remote Shell (Linux) Complete
├── [ ] MGT-DEV-003: Scheduled Malware Scan (macOS) Complete
├── [ ] MGT-DEV-004: Disable Protection (Linux) Complete
└── [ ] Progress reported to GitHub Issue
```

---

## 5. Phase 4: Compliance & Integration Evaluation Procedure

### 5.1 CMP-DATA-001: English-region Sensitive Data Detection

**Reference**: `docs/evaluation-plan.md` - Section 3.3.1

**Evaluation Objective**: Evaluate SSN, credit card, etc. detection accuracy

**Test Procedure**:

```
Step 1: Verify Data Governance Settings
    │
    ├── Control Panel > Data Governance
    ├── Verify enabled data types
    │   ├── Social Security Number (SSN)
    │   ├── Credit Card Number
    │   ├── Bank Account Number
    │   └── Passport Number
    └── Verify detection policy
    │
Step 2: Place Test Files
    │
    ├── Upload test-sensitive-en.txt to Google Drive
    └── Wait for detection (depends on scan interval)
    │
Step 3: Verify Detection
    │
    ├── Verify detection results in Data Governance dashboard
    ├── Verify ticket creation
    └── Verify accuracy of detected data types
    │
Step 4: False Positive Check
    │
    ├── Place file containing similar patterns of non-sensitive data (phone numbers, etc.)
    └── Verify no false positive detection
```

### 5.2 CMP-DATA-002: Japan Sensitive Data Detection

**Reference**: `docs/evaluation-plan.md` - Section 3.3.1

**Evaluation Objective**: Evaluate My Number, driver's license number, etc. detection accuracy

**Test Procedure**:

```
Step 1: Verify Japan Sensitive Data Type Enablement
    │
    ├── Control Panel > Data Governance
    └── Verify Japan-specific data types are available
    │
Step 2: Place Test Files
    │
    ├── Upload test-sensitive-jp.txt to Google Drive
    └── Wait for detection
    │
Step 3: Verify Detection
    │
    ├── Verify detection of each data type
    │   ├── My Number (12 digits)
    │   ├── Driver's license number
    │   ├── Passport number
    │   └── Health insurance number
    └── Verify accuracy of ticket information
```

**Note**: Pre-verification required on whether Japan sensitive data detection is supported by Coro. If not supported, record as "Feature not available".

### 5.3 INT-CLOUD-001~004: Google Workspace Integration Evaluation

**Reference**: `docs/evaluation-plan.md` - Section 3.4.1

**Evaluation Items**:

| Evaluation ID | Item | Evaluation Content |
|---------------|------|-------------------|
| INT-CLOUD-001 | MFA Integration | MFA status retrieval & display |
| INT-CLOUD-002 | Connection Status | Status display when permissions insufficient |
| INT-CLOUD-003 | Drive DLP | Sensitive data detection in files |
| INT-CLOUD-004 | Gmail Protection | Email security features |

### 5.4 INT-AGT-001: macOS Agent 3.7

**Reference**: `docs/evaluation-plan.md` - Section 3.4.2

**Evaluation Items**:
- Scheduled malware scan
- EDR performance optimization
- On-access scan

**Test Procedure**:

```
Step 1: Scheduled Malware Scan
    │
    ├── Schedule configuration & execution verification
    └── Verify scan results
    │
Step 2: EDR Performance
    │
    ├── Measure system load with EDR enabled
    │   ├── CPU usage
    │   ├── Memory usage
    │   └── Disk I/O
    └── Verify impact on normal operations
    │
Step 3: On-access Scan
    │
    ├── Verify scan operation during file operations
    └── Verify detection with EICAR test file
```

### 5.5 INT-AGT-002: Linux Agent 3.7

**Reference**: `docs/evaluation-plan.md` - Section 3.4.2

**Evaluation Items**:
- Protection disable feature
- Remote shell feature

**Test Procedure**:

```
Step 1: Protection Disable Feature
    │
    ├── Execute protection disable from Coro Console
    ├── Verify disabled state on device
    │   └── Verify with coro-agent status command
    ├── Execute re-enable
    └── Verify re-enabled state
    │
Step 2: Remote Shell Feature
    │
    ├── (Skip if already evaluated in MGT-DEV-002)
    └── Execute additional test cases if any
```

### 5.6 Phase 4 Completion Check

```
Phase 4 Completion Checklist
├── [ ] CMP-DATA-001: English-region Sensitive Data Detection Complete
├── [ ] CMP-DATA-002: Japan Sensitive Data Detection Complete
├── [ ] CMP-DATA-003: Unified Ticket Consolidation Complete
├── [ ] CMP-LOC-001: English UI Complete
├── [ ] CMP-LOC-002: Japanese Support Verification Complete
├── [ ] INT-CLOUD-001~004: Google Workspace Integration Complete
├── [ ] INT-AGT-001: macOS Agent 3.7 Complete
├── [ ] INT-AGT-002: Linux Agent 3.7 Complete
└── [ ] Progress reported to GitHub Issue
```

---

## 6. Phase 5: Overall Evaluation & Report Creation Procedure

### 6.1 Compile Evaluation Results

**Procedure**:

```
Step 1: Collect All Evaluation Item Results
    │
    ├── Review each evaluation record file
    └── Transfer scores to summary table
    │
Step 2: Category-wise Summary
    │
    ├── Security feature evaluation average score
    ├── Management feature evaluation average score
    ├── Compliance feature evaluation average score
    └── Integration feature evaluation average score
    │
Step 3: Calculate Overall Score
    │
    ├── Review highest priority items
    │   ├── SEC-AI-001: Prompt Injection Detection
    │   └── SEC-AUTH-001: MFA Status Detection
    └── Calculate overall average score
```

**Summary Template**:

```markdown
## Evaluation Results Summary Table

### Security Feature Evaluation

| Evaluation ID | Item | Score | Notes |
|---------------|------|-------|-------|
| SEC-AI-001 | Prompt Injection Detection | /5 | |
| SEC-AI-002 | Shadow AI Blocklist | /5 | |
| SEC-AI-003 | Coro AI Summary | /5 | |
| SEC-AUTH-001 | MFA Status Detection | /5 | |
| SEC-AUTH-002 | Threat Detection Policies | /5 | |
| **Average** | | **/5** | |

### Management Feature Evaluation
...

### Overall Evaluation

| Item | Value |
|------|-------|
| Highest Priority Item Minimum Score | /5 |
| Overall Average Score | /5 |
| **Overall Evaluation** | Recommended / Conditionally Recommended / On Hold / Not Recommended |
```

### 6.2 Overall Evaluation Determination

**Determination Criteria**:

| Evaluation | Condition |
|------------|-----------|
| **Recommended** | All highest priority items score 4 or above, and average score 3.5 or above |
| **Conditionally Recommended** | Highest priority items have 3, but no critical issues |
| **On Hold** | Highest priority items have 2 or below, awaiting improvement |
| **Not Recommended** | Multiple critical issues exist, high deployment risk |

### 6.3 Report Creation

**Deliverables**:

| Deliverable | Filename | Content |
|-------------|----------|---------|
| Evaluation Results Report | `docs/reports/evaluation-report.md` | Results and analysis of all evaluation items |
| Feature Evaluation Sheet | `docs/reports/evaluation-details.md` | Detailed evaluation results for each feature |
| Issues & Recommendations | `docs/reports/issues-and-recommendations.md` | Discovered issues and improvement proposals |

**Report Template**:

```markdown
# Coro Cybersecurity v3.7/v3.8 Evaluation Results Report

## 1. Executive Summary

### Overall Evaluation: [Recommended / Conditionally Recommended / On Hold / Not Recommended]

### Key Findings
1.
2.
3.

### Recommendations
1.
2.
3.

## 2. Detailed Evaluation Results
...

## 3. Issues and Improvement Proposals
...

## 4. Appendix
- Screenshots
- Test evidence
```

### 6.4 Phase 5 Completion Check

```
Phase 5 Completion Checklist
├── [ ] All evaluation results compiled
├── [ ] Overall evaluation determination complete
├── [ ] Evaluation results report created
├── [ ] Feature evaluation sheet created
├── [ ] Issues & recommendations document created
├── [ ] Screenshots organized
└── [ ] Final report to GitHub Issue
```

---

## 7. Troubleshooting

### 7.1 Common Problems and Solutions

#### Environment Related

| Problem | Cause | Solution |
|---------|-------|----------|
| Google Workspace integration fails | Insufficient permissions | Request additional permissions from Google Workspace admin |
| Agent connection unavailable | Network issues | Verify firewall settings, check proxy configuration |
| MFA status not displayed | Sync delay | Wait 15-30 minutes, execute manual sync |

#### Evaluation Related

| Problem | Cause | Solution |
|---------|-------|----------|
| Sensitive data not detected | Scan not executed | Verify scan schedule, execute manual scan |
| Ticket not created | Policy configuration issue | Verify detection policy settings |
| Remote shell won't connect | Insufficient permissions | Verify permission settings, restart Agent |

### 7.2 Support Contacts

If problems cannot be resolved, contact:

- Coro Support: support@coro.net
- Documentation: https://docs.coro.net/

---

## 8. Lessons Learned & Notes

### 8.1 General Notes

| Item | Note |
|------|------|
| **Test Environment** | Avoid testing in production environment, use dedicated evaluation workspace |
| **Sensitive Data** | Use fictitious test sensitive data (do not use actual personal information) |
| **Screenshots** | Capture all major screens as evaluation evidence |
| **Progress Reports** | Report progress to GitHub Issue at completion of each Phase |

### 8.2 Context Management (For Claude Code)

| Item | Note |
|------|------|
| **Document Reference** | Always reference "0. Context Restoration Guide" when resuming work |
| **Progress Check** | Check latest progress with `gh issue view 1 --comments` |
| **Evaluation ID Verification** | Manage evaluation items by evaluation ID to avoid confusion |
| **Constraints Awareness** | Always be aware of evaluation environment constraints |

### 8.3 Past Failure Patterns (Record for Future Reference)

> **Note**: Update this section after evaluation is conducted.

| Date | Problem | Cause | Solution | Lesson |
|------|---------|-------|----------|--------|
| - | - | - | - | - |

---

## 9. Appendix

### 9.1 Evaluation Checklist (Complete)

```
Coro Cybersecurity v3.7/v3.8 Evaluation Checklist

Phase 1: Environment Setup
├── [ ] Coro workspace configuration
├── [ ] Google Workspace integration
├── [ ] macOS Agent 3.7 setup
├── [ ] Linux Agent 3.7 setup
└── [ ] Test data preparation

Phase 2: Security Feature Evaluation
├── [ ] SEC-AI-001: Prompt Injection Detection【Highest】
├── [ ] SEC-AI-002: Shadow AI Blocklist
├── [ ] SEC-AI-003: Coro AI Summary
├── [ ] SEC-AUTH-001: MFA Status Detection【Highest】
└── [ ] SEC-AUTH-002: Threat Detection Policies

Phase 3: Management Feature Evaluation
├── [ ] MGT-CON-001: Actionboard Redesign
├── [ ] MGT-CON-002: Updated Ticket Structure
├── [ ] MGT-CON-003: Bulk Ticket Actions
├── [ ] MGT-CON-004: Setup Hub
├── [ ] MGT-CON-005: Hierarchy Tree
├── [ ] MGT-CON-006: Security Gaps
├── [ ] MGT-DEV-001: Agent Health Filter
├── [ ] MGT-DEV-002: Remote Shell (Linux)
├── [ ] MGT-DEV-003: Scheduled Malware Scan (macOS)
└── [ ] MGT-DEV-004: Disable Protection (Linux)

Phase 4: Compliance & Integration Evaluation
├── [ ] CMP-DATA-001: English-region Sensitive Data Detection
├── [ ] CMP-DATA-002: Japan Sensitive Data Detection
├── [ ] CMP-DATA-003: Unified Ticket Consolidation
├── [ ] CMP-LOC-001: English UI
├── [ ] CMP-LOC-002: Japanese Support Verification
├── [ ] INT-CLOUD-001: Google Workspace MFA Integration
├── [ ] INT-CLOUD-002: Google Workspace Connection
├── [ ] INT-CLOUD-003: Google Drive DLP
├── [ ] INT-CLOUD-004: Gmail Protection
├── [ ] INT-AGT-001: macOS Agent 3.7
└── [ ] INT-AGT-002: Linux Agent 3.7

Phase 5: Overall Evaluation & Report Creation
├── [ ] Evaluation results compiled
├── [ ] Overall evaluation determination
├── [ ] Evaluation results report created
├── [ ] Feature evaluation sheet created
├── [ ] Issues & recommendations document created
└── [ ] Final report to GitHub Issue
```

### 9.2 Related Document Links

| Document | Path | Purpose |
|----------|------|---------|
| Evaluation Plan | `docs/evaluation-plan.md` | Details of evaluation items & criteria |
| Evaluation Plan (English) | `docs/evaluation-plan-en.md` | English version |
| Evaluation Procedure (Japanese) | `docs/evaluation-procedure.md` | Japanese version |
| Release Notes Analysis | `docs/analysis/release-notes-analysis.md` | v3.7/v3.8 feature details |
| Service Overview | `docs/analysis/coro-service-overview.md` | Coro platform overview |
| **Screenshots Index** | `docs/screenshots-index.md` | List of captured screenshots |
| Coro Official Documentation | https://docs.coro.net/ | Official reference |
| v3.7 Release Notes | https://docs.coro.net/rn/major-3.7 | Official release notes |
| v3.8 Release Notes | https://docs.coro.net/rn/major-3.8 | Official release notes |

### 9.3 Captured Screenshots

| File | Content | Related Evaluation Items |
|------|---------|--------------------------|
| `img/actionboard-dashboard.png` | Actionboard Dashboard | MGT-CON-001, MGT-CON-006 |
| `img/user-profile-settings.png` | User Profile Settings | CMP-LOC-001 |
| `img/notification-settings-threat-types.png` | Notification Settings (Threat Types) | SEC-AI-001, SEC-AUTH-002 |

### 9.4 Command Reference

**GitHub Issue Operations**:

```bash
# List Issues
gh issue list

# View Issue details (with comments)
gh issue view 1 --comments

# Add comment
gh issue comment 1 --body "Comment content"

# Create new Issue
gh issue create --title "Title" --body "Body"
```

**Progress Report Template**:

```bash
gh issue comment 1 --body "## Phase X: [Phase Name] Complete

### Completed Items
- [x] Item 1
- [x] Item 2

### Evaluation Results Summary
| Evaluation ID | Score |
|---------------|-------|
| XXX-001 | X/5 |

### Issues & Observations
-

---
*Next Step: Phase Y [Phase Name]*"
```

---

## Document History

| Version | Date | Changes | Author |
|---------|------|---------|--------|
| 1.0 | 2026-01-22 | Initial creation | - |

---

*This evaluation procedure guide provides detailed procedures for executing the evaluation of Coro Cybersecurity v3.7 and v3.8 new features.*
*Please verify the latest documentation and product specifications when conducting the evaluation.*
