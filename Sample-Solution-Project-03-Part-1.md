# Project 3 – Sample Solution

## 1. Requirement Analysis

### Business Objectives

* Create a single enterprise AI assistant for all employees.
* Provide secure, document-grounded answers.
* Reduce HR and IT support workloads.
* Enable natural language search across enterprise knowledge.
* Support specialized departmental AI agents.
* Enforce document-level authorization.
* Comply with Responsible AI and corporate governance.

---

# 2. AI Platform Architecture

```text
                  Employee
                      │
                      ▼
          Web / Teams / Mobile Client
                      │
              Azure Front Door
                      │
          Azure API Management
                      │
          AI Orchestrator Service
                      │
──────────────────────────────────────────────
 HR Agent │ IT Agent │ Legal Agent │ Finance Agent │ Sales Agent
──────────────────────────────────────────────
                      │
          Prompt Management Service
                      │
               Azure OpenAI
                      │
      Azure AI Search (Vector + Keyword)
                      │
──────────────────────────────────────────────
Blob Storage
SharePoint
Microsoft 365
Employee Portal
ERP
CRM
```

---

# 3. Azure Service Selection

| Requirement         | Azure Service                        | Reason                        |
| ------------------- | ------------------------------------ | ----------------------------- |
| Authentication      | Microsoft Entra ID                   | Enterprise SSO                |
| AI Model            | Azure OpenAI                         | Managed enterprise LLM        |
| Knowledge Retrieval | Azure AI Search                      | Hybrid semantic/vector search |
| Document Storage    | Azure Blob Storage                   | Scalable document repository  |
| Document Processing | Azure AI Document Intelligence       | OCR & metadata extraction     |
| API Layer           | Azure API Management                 | Secure API gateway            |
| Compute             | Azure Kubernetes Service (AKS)       | Multi-agent orchestration     |
| Messaging           | Azure Service Bus                    | Asynchronous workflows        |
| Secrets             | Azure Key Vault                      | Credential management         |
| Monitoring          | Azure Monitor + Application Insights | Observability                 |
| Logging             | Log Analytics                        | Centralized logging           |

---

# 4. RAG Pipeline

```text
Documents
      │
      ▼
Azure Blob Storage
      │
      ▼
Document Intelligence
      │
OCR
Metadata
Classification
      │
      ▼
Chunking
      │
      ▼
Embeddings
      │
      ▼
Azure AI Search
(Vector + Keyword Index)
      │
      ▼
Azure OpenAI
      │
Grounded Response
```

### Why RAG?

* Avoids model retraining.
* Keeps answers grounded in enterprise documents.
* Supports source citations.
* Reduces hallucinations.
* Allows frequent knowledge updates.

---

# 5. Multi-Agent Design

```text
Employee Question
        │
        ▼
AI Orchestrator
        │
 ┌──────┼─────────────┐
 ▼      ▼             ▼
HR     IT        Finance / Legal / Sales
 │      │             │
 ▼      ▼             ▼
RAG    RAG          RAG
 │      │             │
 └──────┼─────────────┘
        ▼
Azure OpenAI
```

Each agent:

* Uses a dedicated prompt.
* Searches only authorized knowledge.
* Applies department-specific policies.

---

# 6. Document Ingestion Flow

```text
SharePoint
OneDrive
Teams
Blob Storage
Email
PDF
Word
Excel
      │
      ▼
Azure Data Factory / Functions
      │
      ▼
Document Intelligence
      │
OCR
Metadata
Entities
Classification
      │
      ▼
Azure AI Search Index
```

---

# 7. Security Architecture

* Microsoft Entra ID authentication.
* Role-Based Access Control (RBAC).
* Document-level authorization.
* Private Endpoints for Azure AI Search, Blob Storage, Key Vault, and Azure OpenAI.
* Managed Identities.
* Encryption in transit (TLS 1.2+).
* Encryption at rest.
* Azure Defender for Cloud.
* Microsoft Sentinel integration.

### Example RBAC

| Role     | Accessible Agents |
| -------- | ----------------- |
| Employee | HR, IT            |
| HR       | HR                |
| Finance  | Finance           |
| Legal    | Legal             |
| Admin    | All               |

---

# 8. Responsible AI Controls

* Prompt injection detection.
* Content filtering.
* Toxic content moderation.
* Grounded responses only.
* Source citations.
* Human feedback loop.
* Audit logging.
* Prompt versioning.
* Explainability.

---

# 9. Prompt Management

Maintain prompts separately from application code.

Example:

```text
HR Agent Prompt
IT Agent Prompt
Finance Prompt
Legal Prompt
Sales Prompt
```

Benefits:

* Easier updates.
* Version control.
* A/B testing.
* Governance.

---

# 10. Conversation Flow

```text
Employee
    │
Question
    │
    ▼
Authentication
    │
Authorization
    │
Determine Department
    │
Retrieve Documents
    │
Generate Prompt
    │
Azure OpenAI
    │
Response + Citations
```

---

# 11. AI Model Strategy

| Task          | Recommended Model              |
| ------------- | ------------------------------ |
| General Q&A   | GPT-4.1 / GPT-4o               |
| Summarization | GPT-4.1-mini                   |
| Translation   | GPT-4.1-mini                   |
| OCR           | Azure AI Document Intelligence |
| Embeddings    | Azure OpenAI Embeddings        |

A model-routing layer can choose the most cost-effective model for each task.

---

# 12. Monitoring & AI Operations

Track:

* Response latency
* Search latency
* Token usage
* Prompt success rate
* Hallucination rate
* User feedback
* Retrieval quality
* Cost per query
* Active users

Use:

* Azure Monitor
* Application Insights
* Log Analytics
* Azure Dashboard

---

# 13. Cost Optimization

* Model routing (use smaller models when appropriate).
* Prompt caching.
* Response caching.
* Embedding reuse.
* Incremental indexing.
* Token limits.
* Autoscaling AKS.
* Blob lifecycle management.

---

# 14. Disaster Recovery

Primary Region: East US
Secondary Region: West Europe

* Azure AI Search replicas.
* Geo-redundant Blob Storage (RA-GRS).
* Azure SQL failover groups (where used).
* Multi-region AKS deployment.
* Azure Front Door for failover.

Target:

* **RPO:** < 15 minutes
* **RTO:** < 30 minutes

---

# 15. CI/CD & MLOps

```text
Developer
    │
GitHub
    │
Azure DevOps
    │
Build
    │
Unit Tests
    │
Prompt Validation
    │
Evaluation Tests
    │
Security Scan
    │
Deploy Dev
    │
Deploy UAT
    │
Deploy Production
```

Include:

* Infrastructure as Code (Bicep/Terraform)
* Prompt versioning
* Automated evaluation
* Canary deployment for prompts and models

---

# 16. STRIDE Threat Model

| Threat                 | Mitigation                          |
| ---------------------- | ----------------------------------- |
| Spoofing               | Entra ID + MFA                      |
| Tampering              | Signed APIs, HTTPS                  |
| Repudiation            | Audit logs                          |
| Information Disclosure | RBAC, document-level ACLs           |
| Denial of Service      | Azure Front Door + DDoS Protection  |
| Elevation of Privilege | Least privilege, Managed Identities |

---

# 17. Future AI Roadmap

* Multi-agent collaboration for complex workflows.
* Voice-enabled AI assistant.
* Image and document understanding.
* Meeting transcription and action-item extraction.
* Workflow automation across ERP/CRM.
* Multilingual support.
* Cost-aware model routing.
* Human approval for sensitive actions.

---

# 18. Trade-offs

| Decision        | Alternative                  | Rationale                                                                            |
| --------------- | ---------------------------- | ------------------------------------------------------------------------------------ |
| Azure AI Search | Self-managed vector database | Managed hybrid search simplifies operations and integrates well with Azure           |
| AKS             | Azure App Service            | AKS offers greater flexibility for orchestrating many AI services and agents         |
| Azure OpenAI    | Self-hosted open-source LLM  | Managed service provides enterprise security, compliance, and operational simplicity |
| Multi-agent     | Single assistant             | Better separation of responsibilities, prompts, and access control                   |

---

# 19. Presentation Outline (15 Slides)

1. Business Challenges
2. AI Vision
3. Requirements
4. AI Platform Architecture
5. RAG Pipeline
6. Multi-Agent Design
7. Knowledge Ingestion
8. Security & Responsible AI
9. Prompt & Model Strategy
10. Monitoring & MLOps
11. Disaster Recovery
12. Cost Optimization
13. Integration with Enterprise Systems
14. Architectural Decisions
15. Q&A
