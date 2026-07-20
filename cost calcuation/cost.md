# HR AI Agent Cost Analysis

## Microsoft Copilot Studio Architecture

### Enterprise Scenario (5,000 Employees)

---

# Assumptions

| Metric                      |                        Value |
| --------------------------- | ---------------------------: |
| Employees                   |                        5,000 |
| Monthly Active Users        |                        3,500 |
| Conversations/User/Month    |                           10 |
| Total Conversations/Month   |                       35,000 |
| Average Turns               |                            6 |
| Total Prompts               |                      210,000 |
| Average Tokens              |                        3,000 |
| Monthly Token Consumption   |                  630M Tokens |
| Documents in Knowledge Base |                        1,000 |
| Power Automate Flows        |                           10 |
| HR Systems                  |         Workday + ServiceNow |
| Channels                    | Teams + SharePoint + Outlook |

---

# Architecture Components

```text
Employees
      ↓
Teams / Outlook / SharePoint
      ↓
Copilot Studio
      ↓
Power Automate
      ↓
Azure OpenAI
      ↓
Azure AI Search
      ↓
SharePoint
Workday
ServiceNow
```

---

# Monthly Cost Breakdown

## 1. Copilot Studio

Assumption:

210,000 messages/month

Approximate cost:

### $8,640/month

---

## 2. Power Automate Premium

10 workflows

Examples:

* Leave approval
* Onboarding
* Ticket creation
* Benefits
* Payroll requests

Estimated:

### $500/month

---

## 3. Premium Connectors

For:

* Workday
* ServiceNow
* SAP
* Oracle

Estimated:

### $300/month

---

## 4. Azure OpenAI (GPT-4o)

630M tokens/month

Using GPT-4o:

Input + output blended cost

Estimated:

### $0/month

---

## 5. Azure AI Search

Standard S1

Semantic Search + Vector Search

Estimated:

### $0/month

---

## 6. Dataverse

Power Platform storage

Estimated:

### $100/month

---

## 7. SharePoint Storage

Knowledge documents

Estimated:

### $50/month

---

## 8. Monitoring

Including:

* Application Insights
* Azure Monitor
* Log Analytics

Estimated:

### $100/month

---

## 9. Security

Included:

* Entra ID
* Conditional Access
* DLP

Incremental cost:

### $0

(assuming Microsoft 365 E3/E5)

---

# Total Monthly Cost

| Component          |     Monthly Cost |
| ------------------ | ---------------: |
| Copilot Studio     |           $8,640 |
| Power Automate     |             $500 |
| Premium Connectors |             $300 |
| Azure OpenAI       |               $0 |
| AI Search          |               $0 |
| Dataverse          |             $100 |
| SharePoint Storage |              $50 |
| Monitoring         |             $100 |
| **Total**          | **$9,690/month** |

---

# Annual Cost

```text
$9,690 × 12

= $1,16,280/year
```

---

# Runtime Cost for 3 Years

```text
$1,16,280 × 3

= $3,48,840
```

---

# Implementation Cost

## Solution Architect

6 weeks

$12,000

---

## Power Platform Developer

8 weeks

$15,000

---

## AI Engineer

4 weeks

$10,000

---

## QA

2 weeks

$3,000

---

## DevOps

2 weeks

$5,000

---

### One-Time Build Cost

```text
≈ $45,000
```

---

# Support Cost

## Power Platform Administrator

0.3 FTE

$20,000/year

---

## Support Engineer

0.2 FTE

$15,000/year

---

## AI Engineer

0.2 FTE

$20,000/year

---

### Annual Support

```text
≈ $55,000/year
```

---

### 3-Year Support Cost

```text
$165,000
```

---

# Three-Year TCO

| Category             |         Cost |
| -------------------- | -----------: |
| Runtime Cost         |    $3,48,840 |
| Implementation Cost  |      $45,000 |
| Support Cost         |     $165,000 |
| **Total 3-Year TCO** |**$5,58,840** |

---

# Cost Per Employee

```text
$5,58,840 ÷ 5,000

= 111.78 per employee
(3 years)
```

---

# Cost Per Employee Per Month

```text
$111.78 ÷ 36

≈ $3.11/month
```

---

# Cost Per Conversation

Annual conversations:

```text
35,000 × 12

= 420,000 conversations/year
```

Three years:

```text
1,260,000 conversations
```

Cost:

```text
$430,680 ÷ 1,260,000

≈ $0.34 per conversation
```

# Architecture Cost Mapping

```text
Teams / SharePoint
        │
        ▼
Copilot Studio
($1,680)
        │
        ▼
Power Automate
($500)
        │
        ▼
Azure OpenAI GPT-4o
($3,150)
        │
        ▼
Azure AI Search
($250)
        │
        ▼
SharePoint + Dataverse
($150)
        │
        ▼
Workday + ServiceNow
($300)
        │
        ▼
Monitoring
($100)
```

# Recommended Architecture

For most enterprises (1,000–10,000 employees), the most practical architecture is:

```text
Microsoft Teams
        ↓
Copilot Studio
(UI + Workflow)
        ↓
Power Automate
        ↓
Azure OpenAI GPT-4o
        ↓
Azure AI Search
        ↓
SharePoint Knowledge Base
        ↓
Workday + ServiceNow
```

This architecture provides:

* Low-code development
* Native Microsoft integration
* Enterprise security
* RAG capability
* HR process automation
* Lower maintenance effort
* Scalability to 20,000+ employees

This is very close to the architecture currently adopted by many Microsoft-centric enterprises and Fortune 500 organizations.
