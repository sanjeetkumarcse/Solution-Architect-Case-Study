# Project 1

# Enterprise Employee Portal

---

# Background

## Company

AIMart Global is a rapidly growing multinational company with over 5,000 employees distributed across multiple countries. As the company expanded through acquisitions and remote work, employees began using multiple disconnected systems for HR, leave management, IT support, announcements, project collaboration, and internal documentation.

These fragmented systems have resulted in poor user experience, increased support requests, duplicated data, and security risks.

The executive leadership has approved the development of a centralized Enterprise Employee Portal that will become the single digital workplace for all employees.

Your team has been hired as the Solution Architecture team to design and implement this platform.

---

# Business Problem

NovaMart currently faces several operational challenges:

* Employees maintain multiple usernames and passwords.
* HR information exists in different applications.
* IT support requests are managed manually.
* Company announcements are communicated through emails that employees often miss.
* Internal documents are scattered across different storage systems.
* Managers cannot access centralized dashboards.
* There is no mobile-friendly employee experience.
* Security policies differ across departments.
* Remote employees experience poor application performance.
* Auditing user activities is difficult.

---

# Project Goal

Design an enterprise-grade Employee Portal that provides employees with a secure and centralized experience for accessing company services while meeting enterprise requirements for scalability, security, compliance, and availability.

---

# Business Objectives

The solution should:

* Provide Single Sign-On (SSO)
* Improve employee productivity
* Reduce IT support workload
* Centralize employee information
* Secure enterprise data
* Support hybrid work
* Enable future AI integration
* Reduce operational costs
* Support international expansion

---

# Functional Requirements

Students should implement features such as:

## Authentication

* Employee Login
* Single Sign-On
* Multi-Factor Authentication
* Password Reset
* Profile Management

---

## Employee Dashboard

* Welcome Dashboard
* Recent Announcements
* Leave Balance
* Company Calendar
* Assigned Tasks
* Quick Links

---

## HR Module

* Employee Profile
* Leave Application
* Leave Approval
* Holiday Calendar
* Organization Chart

---

## IT Support

* Raise Ticket
* Track Ticket
* Knowledge Base
* Asset Request

---

## Document Center

* HR Policies
* Employee Handbook
* Templates
* Search Documents

---

## Administration

* User Management
* Role Management
* Department Management
* Reports
* Audit Logs

---

# Non-Functional Requirements

Students must design the system to satisfy:

Availability

* 99.9% uptime

Performance

* Login within 2 seconds
* Dashboard loading within 3 seconds

Scalability

* Support 100,000 employees

Security

* Zero Trust
* Encryption at Rest
* Encryption in Transit
* RBAC
* MFA
* Secret Management

Reliability

* Automated Backup
* Disaster Recovery

Compliance

* GDPR
* ISO 27001
* SOC2

Monitoring

* Centralized Logging
* Metrics
* Alerts

Maintainability

* CI/CD
* Infrastructure as Code

---

# Constraints

Budget

Medium

Timeline

6 Months

Cloud

Azure

Authentication

Microsoft Entra ID

Database

Azure SQL Database

Storage

Azure Blob Storage

Region

Primary

East US

Secondary

West Europe

---

# Expected Architecture

Students are **not** given the architecture diagram.

Instead they are asked to answer questions such as:

* Which Azure services should be selected?
* Why are they appropriate?
* What alternatives exist?
* What trade-offs are involved?
* How will identity be managed?
* How will networking be secured?
* How will the application scale?
* What monitoring solution is appropriate?
* How will disaster recovery be implemented?

---

# Solution Architecture Deliverables

Each team should produce:

## Business

* Business Requirement Document (BRD)
* Stakeholder Analysis
* Business Process Flow

## Architecture

* High-Level Design (HLD)
* Low-Level Design (LLD)
* C4 Context Diagram
* Container Diagram
* Component Diagram
* Deployment Diagram

## Infrastructure

* Virtual Network Design
* Subnet Design
* DNS Architecture
* Identity Architecture
* Security Architecture

## DevOps

* Git Strategy
* Branching Strategy
* CI/CD Pipeline
* Environment Strategy

## Security

* Threat Model
* STRIDE Analysis
* RBAC Matrix
* Zero Trust Design

## Operations

* Monitoring Dashboard
* Backup Strategy
* Disaster Recovery Plan
* Cost Estimation

---

# Learning Outcomes

After completing this project, students should be able to:

* Analyze business requirements
* Convert requirements into architecture
* Select appropriate Azure services
* Design secure enterprise solutions
* Estimate cloud costs
* Produce professional architecture documentation
* Present and justify architectural decisions
* Evaluate trade-offs between different design options

---

# Assessment Rubric

| Area                  | Weight |
| --------------------- | ------ |
| Requirement Analysis  | 15%    |
| Architecture Design   | 25%    |
| Security Design       | 15%    |
| Infrastructure Design | 15%    |
| Scalability           | 10%    |
| Documentation         | 10%    |
| Presentation          | 10%    |

---
