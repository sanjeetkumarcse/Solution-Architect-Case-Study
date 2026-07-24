
# Project 6 – Sample Solution

## Instructor Reference Solution

---

# 1. Business Objectives

Develop a centralized, enterprise-wide Security Operations Center (SOC) that:

* Protects 100,000+ employees and 50 million customers
* Monitors millions of IoT devices
* Secures enterprise AI workloads
* Detects cyber threats within minutes
* Automates incident response
* Implements Zero Trust across the organization
* Supports global 24×7 security operations
* Meets ISO 27001, SOC 2, GDPR, PCI DSS, and NIST requirements

---

# 2. Enterprise Security Reference Architecture

```text
                        Enterprise Users
────────────────────────────────────────────────────────────

Employees

Customers

Administrators

Third-party Vendors

IoT Devices

AI Agents

Applications

────────────────────────────────────────────────────────────
                        │
                Microsoft Entra ID
                        │
          Conditional Access + MFA + PIM
                        │
────────────────────────────────────────────────────────────
                Security Control Plane

Microsoft Defender XDR

Defender for Cloud

Defender for Endpoint

Defender for Identity

Defender for Office 365

Defender for IoT

────────────────────────────────────────────────────────────
                        │
                Microsoft Sentinel

SIEM

SOAR

Threat Intelligence

Automation

UEBA

Incident Management

────────────────────────────────────────────────────────────
                        │
Azure Monitor

Log Analytics

Logic Apps

Workbooks

Power BI

Executive Dashboard
```

---

# 3. Security Domains

Students should divide the solution into security domains.

## Identity Security

* Microsoft Entra ID
* Passwordless Authentication
* Conditional Access
* MFA
* Identity Protection
* Identity Governance
* Privileged Identity Management
* Access Reviews

---

## Endpoint Security

Use Microsoft Defender for Endpoint.

Protect

* Windows
* Linux
* macOS
* Mobile
* Servers

Monitor

* Malware
* Ransomware
* Device Health
* Vulnerabilities
* USB Usage
* Privilege Escalation

---

## Cloud Security

Use Microsoft Defender for Cloud.

Protect

* Azure
* AKS
* App Service
* Azure SQL
* Storage
* Containers
* Key Vault
* Virtual Machines

---

## Network Security

Azure Firewall

↓

WAF

↓

DDoS Protection

↓

Private Endpoints

↓

NSGs

↓

Bastion

↓

VPN Gateway

---

# 4. Zero Trust Architecture

```text
Never Trust

↓

Always Verify

↓

Least Privilege

↓

Continuous Monitoring

↓

Adaptive Response
```

Every access request is evaluated based on:

* User identity
* Device health
* Location
* Risk level
* Application sensitivity
* Time of access

---

# 5. Identity Lifecycle

```text
HR Creates Employee

↓

Entra ID Account

↓

MFA Enrollment

↓

Conditional Access

↓

RBAC Assignment

↓

PIM Activation

↓

Periodic Access Review

↓

Account Disabled

↓

Archive
```

---

# 6. Conditional Access Policies

Examples:

* Block legacy authentication
* Require MFA for admins
* Require compliant devices
* Restrict high-risk countries
* Require phishing-resistant MFA for privileged users
* Step-up authentication for sensitive applications

---

# 7. Enterprise Logging Strategy

Collect logs from:

* Microsoft Entra ID
* Azure Activity Logs
* Defender products
* Azure Firewall
* WAF
* AKS
* App Service
* Azure SQL
* Storage
* Key Vault
* API Management
* IoT Hub
* Azure OpenAI
* AI Search
* Microsoft 365
* Power BI
* Fabric
* ERP
* CRM

All logs are centralized in **Microsoft Sentinel**.

---

# 8. Microsoft Sentinel Architecture

```text
Security Logs

↓

Log Analytics

↓

Microsoft Sentinel

↓

Analytics Rules

↓

Incident Creation

↓

Automation Rules

↓

Logic Apps

↓

SOC Analyst
```

Capabilities:

* SIEM
* SOAR
* Threat Intelligence
* UEBA
* Workbooks
* Incident Management

---

# 9. Incident Response Workflow

```text
Alert

↓

Sentinel

↓

Correlation

↓

Severity Assignment

↓

Automation Rule

↓

Logic App

↓

Containment

↓

SOC Analyst

↓

Resolution

↓

Post-Incident Review
```

---

# 10. Automated Playbooks

Examples:

### Phishing

* Disable account
* Reset password
* Notify user
* Open incident

### Malware

* Isolate endpoint
* Collect forensic data
* Scan device
* Notify SOC

### Impossible Travel

* Revoke sessions
* Force MFA
* Require password reset

### Suspicious API Activity

* Block API key
* Rotate secret
* Notify application owner

---

# 11. AI Security Architecture

Protect the Enterprise AI Assistant from Project 3.

```text
Employee

↓

Prompt Filter

↓

Prompt Injection Detection

↓

Content Safety

↓

Azure OpenAI

↓

Output Validation

↓

Citation Verification

↓

Response
```

Controls:

* Prompt shields
* Content filtering
* PII detection
* Output moderation
* Token monitoring
* Audit logging

---

# 12. AI Threat Model

| Threat                    | Mitigation                       |
| ------------------------- | -------------------------------- |
| Prompt Injection          | Prompt Shield + input validation |
| Data Leakage              | RBAC + document-level ACLs       |
| Hallucination             | RAG with citations               |
| Model Abuse               | Rate limiting + monitoring       |
| Sensitive Prompt Exposure | Prompt management service        |
| Unauthorized Tool Use     | Tool allowlists and approvals    |

---

# 13. IoT Security

Protect devices from Project 4.

Use:

* Defender for IoT
* X.509 Certificates
* Device Identity
* Secure Boot
* TPM
* Firmware Signing
* Device Health Monitoring
* Network Segmentation

---

# 14. DevSecOps Pipeline

```text
Developer

↓

GitHub

↓

Code Scan

↓

Secret Scan

↓

Dependency Scan

↓

Container Scan

↓

Infrastructure Scan

↓

Build

↓

Deploy

↓

Runtime Monitoring
```

Include:

* SAST
* DAST
* IaC Scanning
* SBOM generation
* Secret detection

---

# 15. Threat Hunting

Use Sentinel and Defender to investigate:

* Lateral movement
* Credential theft
* Insider threats
* Ransomware
* Beaconing
* Data exfiltration
* AI misuse
* IoT anomalies

Map detections to **MITRE ATT&CK**.

---

# 16. Compliance Framework

| Framework | Controls                                      |
| --------- | --------------------------------------------- |
| ISO 27001 | ISMS, asset management, risk treatment        |
| SOC 2     | Security, availability, confidentiality       |
| GDPR      | Data minimization, right to erasure, auditing |
| PCI DSS   | Payment encryption, access control            |
| NIST CSF  | Identify, Protect, Detect, Respond, Recover   |

---

# 17. Security Metrics Dashboard

Track:

* Mean Time to Detect (MTTD)
* Mean Time to Respond (MTTR)
* Incident volume
* Phishing success rate
* Endpoint compliance
* Identity risk score
* High-severity incidents
* Patch compliance
* AI security events
* IoT device health
* Vulnerability backlog

---

# 18. Disaster Recovery

Primary SOC

↓

East US

↓

Geo-Replication

↓

West Europe

Use:

* Geo-redundant Log Analytics
* Sentinel backups (where applicable through workspace strategy)
* Azure Backup
* Key Vault recovery
* Configuration as Code

Targets:

* RPO: < 15 minutes
* RTO: < 30 minutes

---

# 19. Integration with Previous Projects

### Project 1 – Employee Portal

* Identity protection
* Privileged access monitoring
* User activity auditing

### Project 2 – E-Commerce

* API security
* Payment protection
* Fraud analytics
* Customer identity monitoring

### Project 3 – Enterprise AI Assistant

* Prompt injection detection
* Model usage monitoring
* AI governance
* Token and API monitoring

### Project 4 – Smart Logistics

* IoT device protection
* Edge security
* Fleet cybersecurity
* Warehouse OT monitoring

### Project 5 – Enterprise Data Platform

* Data governance
* Data loss prevention (DLP)
* Sensitive data auditing
* Access anomaly detection

---

# 20. Architecture Decision Records (Examples)

| Decision           | Alternative                        | Rationale                                                      |
| ------------------ | ---------------------------------- | -------------------------------------------------------------- |
| Microsoft Sentinel | Third-party SIEM                   | Native Azure integration, automation, and Defender integration |
| Defender XDR       | Multiple standalone endpoint tools | Unified incident correlation and response                      |
| Microsoft Entra ID | Custom identity solution           | Enterprise SSO, Conditional Access, Identity Protection        |
| Defender for Cloud | Manual posture reviews             | Continuous cloud security posture management                   |
| Logic Apps         | Custom automation                  | Low-code SOAR playbooks with broad connector support           |

---

# 21. Presentation Structure (20 Slides)

1. Business Risks
2. Security Vision
3. Zero Trust Strategy
4. Enterprise Security Architecture
5. Identity Security
6. Endpoint & Cloud Protection
7. Network Security
8. SIEM/SOAR Architecture
9. Threat Intelligence
10. AI Security
11. IoT Security
12. DevSecOps
13. Governance & Compliance
14. Incident Response
15. Monitoring & Dashboards
16. Disaster Recovery
17. Integration Across Projects
18. Key Architectural Decisions
19. Risks & Future Improvements
20. Q&A

---
