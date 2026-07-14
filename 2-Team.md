# Team Structure (6–8 Students)

Each student has a primary responsibility while collaborating on the overall solution.

| Role                           | Responsibilities                                                       |
| ------------------------------ | ---------------------------------------------------------------------- |
| Solution Architect (Team Lead) | Leads architecture, coordinates decisions, presents the final solution |
| Cloud Infrastructure Architect | Designs compute, storage, networking, and disaster recovery            |
| Security Architect             | Identity, Zero Trust, compliance, threat modeling                      |
| AI/Data Architect              | AI, RAG, data platform, analytics, databases                           |
| DevOps Architect               | CI/CD, Infrastructure as Code, monitoring, automation                  |
| Application Architect          | APIs, microservices, integration patterns                              |
| Business Analyst               | Requirements gathering, stakeholder management, documentation          |
| Project Manager (optional)     | Sprint planning, risk management, presentations                        |

---

# Architecture Review Board

Typical questions:

* Why Azure App Service instead of AKS?
* Why SQL instead of Cosmos DB?
* Why microservices?
* Why Event Grid instead of Service Bus?
* How will you scale to 10 million users?
* What happens if a region fails?
* How do you meet compliance requirements?
* What are the cost implications?
* How do you secure secrets?
* What architectural alternatives did you consider?

students have to justify decisions, not implement them.

---

# Realistic Client Interactions

To simulate real projects, introduce changes during the course:

* **Week 2:** The client expands to a new country, requiring multi-region deployment.
* **Week 3:** Budget is reduced by 30%, forcing architecture optimization.
* **Week 4:** A new compliance requirement (e.g., GDPR) is introduced.
* **Week 5:** Traffic forecasts increase by 10× due to an upcoming marketing campaign.
* **Week 6:** An executive requests AI capabilities or analytics dashboards.
* **Week 7:** A simulated cloud region outage or cybersecurity incident requires the team to demonstrate resilience and incident response.




