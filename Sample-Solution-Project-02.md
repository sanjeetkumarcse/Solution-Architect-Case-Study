# Project 2 – Sample Solution

## 1. Requirement Analysis

### Business Objectives

* Build a cloud-native e-commerce platform
* Support 10 million registered users
* Achieve 99.99% availability
* Enable AI-powered shopping experiences
* Scale automatically during peak sales
* Secure payment processing with PCI DSS compliance
* Reduce operational costs through managed Azure services

---

## 2. Domain-Driven Microservices

Instead of one monolithic application, divide the system into business domains.

| Microservice    | Responsibility                 | Database                                   |
| --------------- | ------------------------------ | ------------------------------------------ |
| Identity        | Authentication, user profiles  | Azure SQL                                  |
| Customer        | Customer accounts & addresses  | Azure SQL                                  |
| Product Catalog | Products, categories, variants | Azure SQL                                  |
| Search          | Full-text and faceted search   | Azure AI Search                            |
| Shopping Cart   | Shopping cart & wishlist       | Azure Cosmos DB                            |
| Inventory       | Stock management               | Azure SQL                                  |
| Checkout        | Order validation & pricing     | Azure SQL                                  |
| Payment         | Payment orchestration          | Azure SQL                                  |
| Order           | Order lifecycle                | Azure SQL                                  |
| Notification    | Email, SMS, Push               | Service Bus + Azure Communication Services |
| Recommendation  | AI-based recommendations       | Azure AI Foundry/OpenAI                    |
| Reporting       | Analytics & dashboards         | Synapse/Fabric or Azure SQL replicas       |

**Why microservices?**

* Independent deployment
* Fault isolation
* Team autonomy
* Technology flexibility
* Elastic scaling

---

# 3. High-Level Architecture

```text
                  Internet
                      │
          Azure Front Door + WAF
                      │
           Azure API Management
                      │
──────────────────────────────────────────
 App Service / AKS Microservices Layer
──────────────────────────────────────────
│ Identity │ Product │ Cart │ Checkout │
│ Payment  │ Order   │ Search │ Inventory │
│ Recommendation │ Notification │
──────────────────────────────────────────
          │
──────────┼───────────────────────────────
│ Azure SQL │ Cosmos DB │ Blob Storage │
│ AI Search │ Service Bus │ Key Vault │
──────────────────────────────────────────
```

---

# 4. Azure Service Selection

| Requirement   | Azure Service                        | Why                                 |
| ------------- | ------------------------------------ | ----------------------------------- |
| Global entry  | Azure Front Door                     | Global routing, CDN, WAF            |
| API Gateway   | Azure API Management                 | Security, throttling, versioning    |
| Compute       | Azure Kubernetes Service (AKS)       | Best fit for scalable microservices |
| Database      | Azure SQL Database                   | Transactions                        |
| Shopping Cart | Azure Cosmos DB                      | Low-latency, globally distributed   |
| Search        | Azure AI Search                      | Product search                      |
| Images        | Azure Blob Storage                   | Product media                       |
| Messaging     | Azure Service Bus                    | Reliable asynchronous messaging     |
| Secrets       | Azure Key Vault                      | Secure secret storage               |
| Monitoring    | Azure Monitor + Application Insights | Observability                       |
| Identity      | Microsoft Entra ID                   | Enterprise identity & federation    |

---

# 5. Event-Driven Architecture

```text
Customer Places Order
        │
        ▼
Checkout Service
        │
        ▼
Service Bus
        │
 ┌──────┼────────────┐
 ▼      ▼            ▼
Inventory  Payment  Notification
        │
        ▼
Order Service
        │
        ▼
Reporting
```

**Benefits**

* Loose coupling
* Retry mechanisms
* Improved resilience
* Better scalability

---

# 6. Data Storage Strategy

| Business Capability | Database              |
| ------------------- | --------------------- |
| Users               | Azure SQL             |
| Products            | Azure SQL             |
| Orders              | Azure SQL             |
| Inventory           | Azure SQL             |
| Shopping Cart       | Azure Cosmos DB       |
| Sessions            | Azure Cache for Redis |
| Product Images      | Blob Storage          |
| Search Index        | Azure AI Search       |

**Trade-off:** Cosmos DB offers low latency for carts and sessions, while Azure SQL ensures ACID transactions for orders and payments.

---

# 7. Networking

```text
Azure Front Door
      │
Application Gateway (WAF)
      │
API Management
      │
Virtual Network
├── AKS Subnet
├── Data Subnet
├── Private Endpoints
└── Management Subnet
```

* Private Endpoints for Azure SQL, Cosmos DB, Blob Storage, and Key Vault
* Network Security Groups (NSGs)
* Azure DDoS Protection Standard

---

# 8. Security Architecture

* Zero Trust principles
* Microsoft Entra ID with OAuth2/OpenID Connect
* Optional MFA
* Azure Key Vault
* Managed Identities
* TLS 1.2+
* Encryption at rest (Azure-managed keys or CMK)
* Azure Defender for Cloud
* Microsoft Sentinel for SIEM

### RBAC

| Role              | Permissions                   |
| ----------------- | ----------------------------- |
| Customer          | Shop, manage orders           |
| Support Agent     | View orders, assist customers |
| Inventory Manager | Manage stock                  |
| Product Manager   | Manage catalog                |
| Admin             | Full access                   |

---

# 9. Checkout Sequence

```text
Customer
    │
    ▼
Cart Service
    │
    ▼
Checkout Service
    │
    ├── Validate Inventory
    ├── Calculate Tax
    ├── Apply Coupons
    ├── Calculate Shipping
    │
    ▼
Payment Service
    │
    ▼
Order Service
    │
    ▼
Notification Service
```

---

# 10. Payment Gateway Pattern

Introduce a Payment Abstraction Layer:

```text
Payment API
      │
Payment Adapter
├── Stripe
├── Razorpay
├── PayPal
├── Adyen
└── Bank Gateway
```

This lets you add or replace providers without changing checkout logic.

---

# 11. Caching Strategy

Use **Azure Cache for Redis** for:

* Product catalog
* Trending products
* Shopping carts (if desired)
* User sessions
* Homepage content

Benefits:

* Reduced database load
* Faster response times
* Improved user experience

---

# 12. Monitoring & Observability

* Azure Monitor
* Application Insights
* Log Analytics
* Distributed tracing (OpenTelemetry)
* Azure Dashboard
* Alerts (Teams/Email)

Monitor:

* API latency
* Checkout failures
* Payment success rate
* Inventory sync
* CPU/memory
* Queue depth

---

# 13. Disaster Recovery

Primary Region: East US
Secondary Region: West Europe

* Azure SQL Failover Groups
* Cosmos DB multi-region replication
* Geo-redundant Blob Storage (RA-GRS)
* Azure Front Door regional failover
* Automated backups
* Point-in-time restore

Target:

* **RPO:** < 15 minutes
* **RTO:** < 30 minutes

---

# 14. CI/CD Pipeline

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
Security Scan
    │
Container Build
    │
Deploy Dev
    │
Integration Tests
    │
Deploy UAT
    │
Canary/Blue-Green
    │
Production
```

---

# 15. Cost Optimization

* AKS Cluster Autoscaler
* Spot VMs for non-production workloads
* Reserved capacity for Azure SQL
* Azure Blob lifecycle policies
* Azure Cache for Redis sizing
* Autoscale based on demand
* Log retention policies

---

# 16. AI Enhancements

* Personalized recommendations (Azure OpenAI)
* AI shopping assistant using RAG over product catalogs and FAQs
* Image-based product search
* Intelligent support chatbot
* Demand forecasting
* Dynamic pricing engine (future)

---

# 17. STRIDE Threat Model

| Threat                 | Mitigation                          |
| ---------------------- | ----------------------------------- |
| Spoofing               | Entra ID + MFA                      |
| Tampering              | HTTPS, signed APIs                  |
| Repudiation            | Immutable audit logs                |
| Information Disclosure | Encryption & RBAC                   |
| Denial of Service      | Azure Front Door + DDoS Protection  |
| Elevation of Privilege | Least privilege, Managed Identities |

---

# 18. Trade-offs

| Decision       | Alternative    | Rationale                                                        |
| -------------- | -------------- | ---------------------------------------------------------------- |
| Microservices  | Monolith       | Better scalability and independent deployments                   |
| AKS            | App Service    | AKS is more suitable for many independently scaling services     |
| Cosmos DB      | Azure SQL      | Cosmos DB excels for globally distributed, low-latency cart data |
| Service Bus    | Direct REST    | Better decoupling, retries, and resilience                       |
| API Management | Direct ingress | Centralized security, policies, and versioning                   |

---

# 19. Presentation Outline (15 Slides)

1. Business Background
2. Business Challenges
3. Functional Requirements
4. Non-Functional Requirements
5. Domain Decomposition
6. High-Level Architecture
7. Microservices Interactions
8. Data Storage Strategy
9. Networking & Security
10. Checkout & Payment Flow
11. Monitoring & Operations
12. Disaster Recovery
13. Cost Optimization
14. AI Roadmap
15. Key Architectural Decisions & Q&A

---