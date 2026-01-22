# Coro Cybersecurity v3.7/v3.8 Evaluation Plan

## Document Information

| Item | Details |
|------|---------|
| **Document Name** | Coro Cybersecurity v3.7/v3.8 Evaluation Plan |
| **Created Date** | January 22, 2026 |
| **Updated Date** | January 22, 2026 |
| **Target Versions** | v3.7 (2025-11-16), v3.8 (2025-12-14) |
| **Target URL** | https://www.coro.net/ |
| **Documentation URL** | https://docs.coro.net/rn/major-3.7, https://docs.coro.net/rn/major-3.8 |

---

## Evaluation Environment Constraints

> **Important**: This evaluation will be conducted under the following constraints.

| Category | Available | Not Available |
|----------|-----------|---------------|
| **Cloud Services** | Google Workspace | Microsoft 365 |
| **Devices** | macOS, Linux | Windows |
| **Sensitive Data Detection** | English-speaking regions, Japan | UAE, Brazil, Other regions |
| **Languages** | English, Japanese | French, Other languages |

---

## 1. Evaluation Overview

### 1.1 Evaluation Objectives

Conduct a comprehensive evaluation of new features and enhancements released in Coro Cybersecurity platform v3.7 and v3.8 from the following perspectives:

1. **Feature Completeness**: Verify that features documented in release notes are correctly implemented
2. **Security Effectiveness**: Assess how new features contribute to security protection
3. **Operability**: Evaluate impact on administrator and user operational workload
4. **Integration**: Examine integration with existing features and external systems
5. **Reliability**: Assess feature stability and error handling

### 1.2 Evaluation Scope

```
┌─────────────────────────────────────────────────────────────────┐
│                     Evaluation Scope                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐            │
│  │   v3.7      │  │   v3.8      │  │  Common     │            │
│  │  Features   │  │  Features   │  │  Platform   │            │
│  └─────────────┘  └─────────────┘  └─────────────┘            │
│                                                                 │
│  [Target Modules]                                               │
│  - Coro Console    - Cloud Security   - Email Security          │
│  - Endpoint Security  - EDR           - Network/SWG             │
│  - Data Governance    - MDM           - SAT                     │
│  - Coro AI            - Agent (macOS/Linux)                     │
│                                                                 │
│  [Target Cloud Services]                                        │
│  - Google Workspace only                                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 1.3 Out of Scope

- Existing features from v3.6 and earlier
- Detailed bug fix verification (confirmation only)
- Performance load testing
- Penetration testing
- **Microsoft 365 related features** (environment constraint)
- **Windows Agent related features** (environment constraint)
- **UAE/Brazil sensitive data detection** (out of requirements)
- **French and other multi-language features** (out of requirements)

---

## 2. Evaluation Framework (MECE Structure)

### 2.1 Evaluation Category Hierarchy

```
Evaluation Categories
├── 1. Security Feature Evaluation
│   ├── 1.1 Threat Detection Features
│   │   ├── AI/ML Related Threat Detection
│   │   ├── Traditional Threat Detection
│   │   └── Behavior Detection
│   ├── 1.2 Protection Features
│   │   ├── Block/Quarantine Functions
│   │   ├── Auto-remediation Functions
│   │   └── Policy Enforcement
│   └── 1.3 Visibility & Monitoring Features
│       ├── Status Monitoring
│       ├── Alerts
│       └── Reporting
│
├── 2. Management Feature Evaluation
│   ├── 2.1 Console Features
│   │   ├── Dashboard
│   │   ├── Settings Management
│   │   └── User Management
│   ├── 2.2 Device Management
│   │   ├── Agent Management (macOS/Linux)
│   │   ├── Remote Operations
│   │   └── Policy Enforcement
│   └── 2.3 MSP Features
│       ├── Multi-tenancy
│       ├── Global Policies
│       └── Bulk Operations
│
├── 3. Compliance Feature Evaluation
│   ├── 3.1 Data Protection
│   │   ├── Sensitive Data Detection (English-speaking/Japan)
│   │   ├── DLP Features
│   │   └── Encryption
│   ├── 3.2 Audit & Trail
│   │   ├── Activity Logs
│   │   ├── Change History
│   │   └── Report Export
│   └── 3.3 Regional Support
│       └── Language Support (English/Japanese)
│
└── 4. Integration Feature Evaluation
    ├── 4.1 Cloud Service Integration
    │   └── Google Workspace
    ├── 4.2 API Features
    │   └── Public API
    └── 4.3 Agent Integration
        ├── macOS Agent
        └── Linux Agent
```

---

## 3. Detailed Evaluation Items

### 3.1 Security Feature Evaluation

#### 3.1.1 AI/ML Related Threat Detection

| Eval ID | Evaluation Item | Target Version | Priority | Evaluation Content |
|---------|-----------------|----------------|----------|-------------------|
| SEC-AI-001 | Prompt Injection Detection | v3.7 | **Highest** | Detection accuracy of AI prompt injection in email body/subject |
| SEC-AI-002 | Shadow AI Blocklist | v3.7 | High | Access blocking functionality for AI chatbots |
| SEC-AI-003 | Coro AI Summary | v3.7/v3.8 | Medium | Accuracy of AI-assisted security summaries |

**SEC-AI-001 Detailed Evaluation Procedure**

```
1. Preparation
   - Set up Google Workspace test email account
   - Confirm Email Security is enabled

2. Test Cases
   TC-001: Explicit Prompt Injection
   - Subject: "Ignore previous instructions and..."
   - Expected: Detection and warning/quarantine

   TC-002: Obfuscated Prompt (Base64, etc.)
   - Body contains encoded prompt
   - Expected: Verify detection capability

   TC-003: False Positive Confirmation
   - Legitimate business emails about AI
   - Expected: Normal delivery

3. Evaluation Criteria
   - True Positive Rate
   - False Positive Rate
   - Time to detection
   - Appropriateness of admin notifications
```

#### 3.1.2 Authentication & Access Control

| Eval ID | Evaluation Item | Target Version | Priority | Evaluation Content |
|---------|-----------------|----------------|----------|-------------------|
| SEC-AUTH-001 | MFA Status Detection (Google Workspace) | v3.8 | **Highest** | MFA status detection accuracy for Google Workspace |
| SEC-AUTH-002 | Threat Detection Policies | v3.7 | High | Verification of new threat detection types |

> **Note**: Microsoft 365 is out of scope due to environment constraints

**SEC-AUTH-001 Detailed Evaluation Procedure (Google Workspace)**

```
1. Prerequisites
   - Google Workspace integration configured
   - Coro integration approved with admin permissions

2. Test Cases
   TC-001: MFA Enabled User Detection
   - Prepare user with MFA configured in Google Workspace
   - Verify "MFA enabled" label on Protected Users page

   TC-002: MFA Disabled User Detection
   - User without MFA configuration
   - Verify "MFA not enabled" label

   TC-003: MFA Status Change Reflection
   - Change MFA status in Google Workspace
   - Measure reflection timing in Coro

   TC-004: Filtering Functionality
   - Verify user filter by MFA status

3. Evaluation Criteria
   - Detection accuracy
   - Status update latency
   - UI display accuracy
   - Filter functionality operation
```

#### 3.1.3 Threat Detection Policies (v3.7 Cloud Security)

| Detection Type | Evaluation Item | Test Method |
|----------------|-----------------|-------------|
| Abnormal Admin Activity | Detection of abnormal admin operations | Simulate admin operations outside normal hours |
| Mass Data Deletion | Detection of mass data deletion | Test deletion exceeding threshold |
| Mass Data Download | Detection of mass downloads | Test downloads exceeding threshold |
| Suspected Bot Attack | Bot attack detection | Simulate automation patterns |
| Suspected Identity Compromise | Identity compromise detection | Simulate abnormal login patterns |

> **Note**: Above tests will be conducted in Google Workspace environment

---

### 3.2 Management Feature Evaluation

#### 3.2.1 Console Features

| Eval ID | Evaluation Item | Target Version | Priority | Evaluation Content |
|---------|-----------------|----------------|----------|-------------------|
| MGT-CON-001 | Actionboard Redesign | v3.7 | Medium | Usability and information visibility of new dashboard |
| MGT-CON-002 | Updated Ticket Structure | v3.7 | Medium | Operability of 4-tab structure, Quick Fix functionality |
| MGT-CON-003 | Bulk Ticket Actions | v3.7 | High | Efficiency of bulk operations, available actions |
| MGT-CON-004 | Setup Hub | v3.8 | Medium | Onboarding completeness and clarity |
| MGT-CON-005 | Hierarchy Tree | v3.8 | Medium | Accuracy of workspace hierarchy display |
| MGT-CON-006 | Security Gaps | v3.8 | High | Comprehensiveness of security gap detection |

**MGT-CON-003 Detailed Evaluation Procedure**

```
1. Test Cases
   TC-001: Bulk Operation on Same Type Tickets
   - Select multiple malware detection tickets
   - Execute bulk Quarantine action
   - Expected: Applied to all tickets

   TC-002: Selection of Different Type Tickets
   - Select tickets from different modules
   - Verify only common actions are displayed

   TC-003: Bulk Operation on Large Number of Tickets
   - Select 50+ tickets
   - Verify performance and completion

2. Evaluation Criteria
   - Intuitiveness of operation
   - Processing speed
   - Error handling
   - Result notification
```

#### 3.2.2 Device Management

| Eval ID | Evaluation Item | Target Version | Priority | Evaluation Content |
|---------|-----------------|----------------|----------|-------------------|
| MGT-DEV-001 | Agent Health Filter | v3.8 | Medium | Agent health filter (macOS/Linux) |
| MGT-DEV-002 | Remote Shell (Linux) | v3.7/v3.8 | **High** | Linux remote shell access |
| MGT-DEV-003 | Scheduled Malware Scan (macOS) | v3.7 | High | macOS scheduled scanning |
| MGT-DEV-004 | Disable Protection (Linux) | v3.7 | Medium | Linux protection disable support |

> **Note**: Windows-related features (Remote Agent Uninstallation, USB Lockdown Allowlisting) are out of scope due to environment constraints

**MGT-DEV-002 Detailed Evaluation Procedure (Remote Shell - Linux)**

```
1. Prerequisites
   - Linux Agent 3.7 or later installed
   - Device is online
   - Remote shell permissions granted

2. Test Cases
   TC-001: Normal Remote Shell Connection
   - Initiate remote shell from Coro Console
   - Verify basic command execution (ls, pwd, cat, etc.)

   TC-002: Session Management
   - Verify session timeout
   - Verify multiple session behavior

   TC-003: Permission Control
   - Verify executable command restrictions
   - Verify dangerous command blocking

3. Evaluation Criteria
   - Connection stability
   - Command execution response
   - Appropriateness of security controls
   - Audit log recording
```

**MGT-DEV-003 Detailed Evaluation Procedure (Scheduled Malware Scan - macOS)**

```
1. Prerequisites
   - macOS Agent 3.7 or later installed
   - Scheduled scan configuration permissions

2. Test Cases
   TC-001: Schedule Configuration
   - Configure daily/weekly scans
   - Verify execution according to schedule

   TC-002: Scan Execution
   - Verify scan start and completion
   - Verify ticket creation upon detection

   TC-003: Performance Impact
   - Monitor system load during scan

3. Evaluation Criteria
   - Schedule accuracy
   - Scan completion rate
   - System impact level
```

---

### 3.3 Compliance Feature Evaluation

#### 3.3.1 Sensitive Data Detection

| Eval ID | Evaluation Item | Target Version | Priority | Evaluation Content |
|---------|-----------------|----------------|----------|-------------------|
| CMP-DATA-001 | English-speaking Region Sensitive Data Detection | Existing | High | Detection accuracy for SSN, credit cards, etc. |
| CMP-DATA-002 | Japan Sensitive Data Detection | Existing | **High** | Detection accuracy for My Number, driver's license, etc. |
| CMP-DATA-003 | Unified Ticket Consolidation | v3.7 | Medium | Consolidated display of sensitive data tickets |

> **Note**: UAE and Brazil sensitive data are out of scope as per requirements

**CMP-DATA-002 Detailed Evaluation Procedure (Japan Sensitive Data)**

```
1. Test Data Preparation
   - My Number (12-digit number)
   - Driver's license number
   - Passport number
   - Health insurance number
   - Bank account number

2. Test Cases
   TC-001: Detection of Each Data Type
   - Create test file with Japanese sensitive data
   - Upload to Google Drive
   - Verify detection and ticket creation

   TC-002: False Positive Verification
   - Similar pattern non-sensitive data (phone numbers, etc.)
   - Verify no detection occurs

   TC-003: Email Detection
   - Send email containing sensitive data via Gmail
   - Verify detection behavior

3. Evaluation Criteria
   - Detection rate
   - False positive rate
   - Time to detection
   - Ticket information accuracy
```

**CMP-DATA-001 Detailed Evaluation Procedure (English-speaking Region Sensitive Data)**

```
1. Test Data Preparation
   - Social Security Number (SSN)
   - Credit card numbers
   - Bank account numbers (US/UK format)
   - Passport numbers

2. Test Cases
   TC-001: Detection of Each Data Type
   - Create test file with English-speaking region sensitive data
   - Upload to Google Drive
   - Verify detection and ticket creation

3. Evaluation Criteria
   - Detection rate
   - False positive rate
   - Time to detection
```

#### 3.3.2 Language Support

| Eval ID | Evaluation Item | Target Version | Priority | Evaluation Content |
|---------|-----------------|----------------|----------|-------------------|
| CMP-LOC-001 | English UI | Existing | High | Console English display |
| CMP-LOC-002 | Japanese Support Verification | - | Medium | Verify Japanese UI availability and quality |

> **Note**: French (Canada) and SAT multi-language support are out of scope as per requirements

---

### 3.4 Integration Feature Evaluation

#### 3.4.1 Cloud Service Integration

| Eval ID | Evaluation Item | Target Version | Priority | Evaluation Content |
|---------|-----------------|----------------|----------|-------------------|
| INT-CLOUD-001 | Google Workspace MFA Integration | v3.8 | **Highest** | MFA integration with Google Workspace |
| INT-CLOUD-002 | Google Workspace Connection | v3.7 | High | Connection status display when permissions insufficient |
| INT-CLOUD-003 | Google Drive DLP | Existing | High | Sensitive data detection in Google Drive files |
| INT-CLOUD-004 | Gmail Protection | Existing | High | Gmail email security |

> **Note**: Microsoft 365 related features are out of scope due to environment constraints

**INT-CLOUD-001 Detailed Evaluation Procedure (Google Workspace MFA)**

```
1. Prerequisites
   - Google Workspace admin privileges
   - Coro integration setup completed

2. Test Cases
   TC-001: Accurate MFA Status Retrieval
   - Verify status for MFA enabled/disabled users
   - Verify display on Protected Users page

   TC-002: Status Change Reflection
   - Change MFA settings in Google Workspace
   - Measure reflection time to Coro

   TC-003: Filter Functionality
   - User filtering by MFA status

3. Evaluation Criteria
   - Integration stability
   - Status reflection accuracy
   - Update frequency appropriateness
```

#### 3.4.2 Agent Features

| Eval ID | Evaluation Item | Target Version | Priority | Evaluation Content |
|---------|-----------------|----------------|----------|-------------------|
| INT-AGT-001 | macOS Agent 3.7 | v3.7 | **High** | Scheduled scanning, EDR optimization |
| INT-AGT-002 | Linux Agent 3.7 | v3.7 | **High** | Protection disable, remote shell |

> **Note**: Windows Agent 3.7 is out of scope due to environment constraints

**INT-AGT-001 Detailed Evaluation Procedure (macOS Agent 3.7)**

```
1. Prerequisites
   - Latest macOS version
   - Agent 3.7 installed

2. Test Cases
   TC-001: Scheduled Malware Scan
   - Configure and verify scheduled execution

   TC-002: EDR Performance Optimization
   - Measure system load with EDR enabled
   - Compare with v3.6 or earlier (if possible)

   TC-003: On-Access Scan
   - Verify scan behavior during file operations

3. Evaluation Criteria
   - Normal function operation
   - System resource usage
   - User experience impact
```

**INT-AGT-002 Detailed Evaluation Procedure (Linux Agent 3.7)**

```
1. Prerequisites
   - Latest Ubuntu/RHEL version
   - Agent 3.7 installed

2. Test Cases
   TC-001: Disable Protection Feature
   - Disable protection from Coro console
   - Verify disabled state
   - Verify re-enablement

   TC-002: Remote Shell Feature
   - Remote connection from console
   - Command execution
   - Session management

3. Evaluation Criteria
   - Normal function operation
   - Security controls
   - Audit log recording
```

---

## 4. Evaluation Schedule

### 4.1 Phase Structure

```
Phase 1: Environment Preparation & Basic Verification (Recommended: 1 week)
├── Evaluation Environment Setup
│   ├── Google Workspace configuration
│   ├── macOS/Linux device preparation
│   └── Coro workspace setup
├── Test Account Preparation
├── Basic Function Verification
└── Test Data Preparation

Phase 2: Security Feature Evaluation (Recommended: 2 weeks)
├── AI/ML Related Threat Detection Testing
├── MFA Status Detection Testing (Google Workspace)
├── Threat Detection Policy Testing
└── Protection Feature Testing

Phase 3: Management Feature Evaluation (Recommended: 1 week)
├── Console Feature Testing
├── Device Management Testing (macOS/Linux)
└── MSP Feature Testing

Phase 4: Compliance & Integration Evaluation (Recommended: 1 week)
├── Sensitive Data Detection Testing (English-speaking/Japan)
├── Google Workspace Integration Testing
└── Agent Feature Testing (macOS/Linux)

Phase 5: Comprehensive Evaluation & Report Creation (Recommended: 1 week)
├── Results Compilation & Analysis
├── Issues & Improvements Summary
└── Final Report Creation
```

### 4.2 Prioritized Evaluation Items

| Priority | Evaluation Item | Phase | Rationale |
|----------|-----------------|-------|-----------|
| **Highest** | Prompt Injection Detection | 2 | Response to new threat type |
| **Highest** | MFA Status Detection (Google Workspace) | 2 | Basic security posture visibility |
| High | Threat Detection Policies | 2 | Threat detection expansion |
| High | Shadow AI Blocklist | 2 | Generative AI usage risk mitigation |
| High | Security Gaps | 3 | Security posture improvement support |
| High | Bulk Ticket Actions | 3 | Operational efficiency |
| High | Remote Shell (Linux) | 3 | Incident response capability |
| High | macOS Agent 3.7 | 4 | Endpoint protection |
| High | Linux Agent 3.7 | 4 | Endpoint protection |
| High | Japan Sensitive Data Detection | 4 | Compliance requirements |
| Medium | Other features | 3-4 | Supplementary features |

---

## 5. Evaluation Environment Requirements

### 5.1 Required Infrastructure

| Element | Requirements | Notes |
|---------|--------------|-------|
| **Coro Workspace** | Evaluation workspace | All modules enabled |
| **Google Workspace** | Test domain | For MFA verification, DLP verification |
| **macOS Device** | Latest macOS version | Agent 3.7 testing (1 or more) |
| **Linux Device** | Ubuntu 22.04 LTS / RHEL 9 | Agent 3.7 testing (1 or more) |

> **Out of Scope**: Microsoft 365 tenant, Windows devices

### 5.2 Test Account Requirements

| Account Type | Quantity | Purpose |
|--------------|----------|---------|
| MSP Admin | 1 | Global view evaluation |
| Workspace Admin | 2 | Management feature evaluation |
| General Users (Google Workspace) | 5 | End-user feature evaluation |
| MFA Enabled Users (Google Workspace) | 3 | MFA detection evaluation |
| MFA Disabled Users (Google Workspace) | 2 | MFA detection evaluation |

### 5.3 Test Data Requirements

| Data Type | Content | Purpose |
|-----------|---------|---------|
| Japan Sensitive Data | My Number, driver's license samples | CMP-DATA-002 |
| English-speaking Sensitive Data | SSN, credit card samples | CMP-DATA-001 |
| Prompt Injection Emails | Various patterns | SEC-AI-001 |
| Normal Business Emails | Legitimate AI-related emails | False positive verification |

> **Out of Scope**: UAE sensitive data, Brazil sensitive data

---

## 6. Evaluation Criteria

### 6.1 Evaluation Scoring

| Score | Rating | Criteria |
|-------|--------|----------|
| 5 | Excellent | Functionality/performance exceeds expectations |
| 4 | Good | Functionality/performance meets expectations |
| 3 | Acceptable | Minor issues exist but usable |
| 2 | Needs Improvement | Significant issues requiring improvement |
| 1 | Unacceptable | Non-functional, unusable |

### 6.2 Overall Evaluation Criteria

| Rating | Conditions |
|--------|------------|
| **Recommended** | All highest priority items scored 4+, average score 3.5+ |
| **Conditionally Recommended** | Some highest priority items scored 3, no critical issues |
| **On Hold** | Highest priority items scored 2 or below, awaiting improvements |
| **Not Recommended** | Multiple critical issues, high implementation risk |

---

## 7. Deliverables

### 7.1 Deliverables Upon Completion

| Deliverable | Content | Format |
|-------------|---------|--------|
| Evaluation Results Report | Results and analysis for all evaluation items | Markdown/PDF |
| Feature Evaluation Sheets | Detailed evaluation results per feature | Spreadsheet |
| Issues & Improvement Proposals | Discovered problems and improvement suggestions | Markdown |
| Screenshot Collection | Screen captures during evaluation | Image files |

### 7.2 Interim Reports

| Timing | Content |
|--------|---------|
| Phase 1 Completion | Environment setup status, test preparation status |
| Phase 2 Completion | Interim results of security feature evaluation |
| Phase 4 Completion | Preliminary results of all evaluation items |

---

## 8. Risks and Mitigation

### 8.1 Anticipated Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Test environment setup delay | High | Early start, prepare alternative environment |
| Google Workspace permission insufficiency | Medium | Pre-verify and obtain required permissions |
| Test data shortage | Medium | Utilize data generation tools |
| Feature defect discovery | Medium | Report to Coro support, alternative evaluation |
| macOS/Linux Agent compatibility issues | Medium | Pre-verify supported OS versions |

---

## 9. Reference Materials

### 9.1 Related Documents

| Document | URL/Path |
|----------|----------|
| Coro Official Site | https://www.coro.net/ |
| Coro Docs Portal | https://docs.coro.net/ |
| v3.7 Release Notes | https://docs.coro.net/rn/major-3.7 |
| v3.8 Release Notes | https://docs.coro.net/rn/major-3.8 |
| Service Overview Analysis | docs/analysis/coro-service-overview.md |
| Release Notes Analysis | docs/analysis/release-notes-analysis.md |

---

## Appendix A: Evaluation Checklist

### A.1 Security Feature Checklist

- [ ] SEC-AI-001: Prompt Injection Detection
- [ ] SEC-AI-002: Shadow AI Blocklist
- [ ] SEC-AI-003: Coro AI Summary
- [ ] SEC-AUTH-001: MFA Status Detection (Google Workspace)
- [ ] SEC-AUTH-002: Threat Detection Policies

### A.2 Management Feature Checklist

- [ ] MGT-CON-001: Actionboard Redesign
- [ ] MGT-CON-002: Updated Ticket Structure
- [ ] MGT-CON-003: Bulk Ticket Actions
- [ ] MGT-CON-004: Setup Hub
- [ ] MGT-CON-005: Hierarchy Tree
- [ ] MGT-CON-006: Security Gaps
- [ ] MGT-DEV-001: Agent Health Filter (macOS/Linux)
- [ ] MGT-DEV-002: Remote Shell (Linux)
- [ ] MGT-DEV-003: Scheduled Malware Scan (macOS)
- [ ] MGT-DEV-004: Disable Protection (Linux)

### A.3 Compliance Feature Checklist

- [ ] CMP-DATA-001: English-speaking Region Sensitive Data Detection
- [ ] CMP-DATA-002: Japan Sensitive Data Detection
- [ ] CMP-DATA-003: Unified Ticket Consolidation
- [ ] CMP-LOC-001: English UI
- [ ] CMP-LOC-002: Japanese Support Verification

### A.4 Integration Feature Checklist

- [ ] INT-CLOUD-001: Google Workspace MFA Integration
- [ ] INT-CLOUD-002: Google Workspace Connection
- [ ] INT-CLOUD-003: Google Drive DLP
- [ ] INT-CLOUD-004: Gmail Protection
- [ ] INT-AGT-001: macOS Agent 3.7
- [ ] INT-AGT-002: Linux Agent 3.7

---

## Appendix B: Out of Scope Items List

The following items are out of scope for this evaluation due to environment constraints or requirements.

### B.1 Out of Scope Due to Environment Constraints

| Item | Reason |
|------|--------|
| Microsoft 365 MFA Integration | No Microsoft 365 environment |
| Windows Agent 3.7 | No Windows devices |
| Remote Agent Uninstallation (Windows) | No Windows devices |
| USB Lockdown Allowlisting | Windows-only feature |

### B.2 Out of Scope Due to Requirements

| Item | Reason |
|------|--------|
| UAE Sensitive Data Detection | Only English-speaking/Japan in scope |
| Brazil Sensitive Data Detection | Only English-speaking/Japan in scope |
| French (Canada) Support | Only English/Japanese in scope |
| SAT Multi-language | Only English/Japanese in scope |

---

*This evaluation plan was created for the purpose of evaluating new features in Coro Cybersecurity v3.7 and v3.8.*
*Please verify the latest documentation and product specifications when conducting the evaluation.*

---

**Document History**

| Version | Date | Changes | Author |
|---------|------|---------|--------|
| 1.0 | 2026-01-22 | Initial creation | - |
| 1.1 | 2026-01-22 | Reflected environment constraints (Google Workspace/macOS/Linux only, English-speaking & Japan only) | - |
