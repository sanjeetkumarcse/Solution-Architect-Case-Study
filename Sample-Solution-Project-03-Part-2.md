# Enterprise AI Reference Architecture

```text
                   Employee
                       │
        Web Portal / Teams / Mobile App
                       │
               Azure Front Door
                       │
             Azure API Management
                       │
          Authentication (Entra ID)
                       │
              AI Gateway / Orchestrator
                       │
      ┌────────────────┼────────────────┐
      │                │                │
 HR Agent         IT Agent        Finance Agent
      │                │                │
      └────────────────┼────────────────┘
                       │
             Prompt Management Layer
                       │
         Model Router / LLM Gateway
                       │
       ┌───────────────┼────────────────┐
       │               │                │
 GPT-4.1         GPT-4.1-mini      Embedding Model
       │               │                │
       └───────────────┼────────────────┘
                       │
               RAG Retrieval Engine
                       │
Azure AI Search (Vector + Semantic + Keyword)
                       │
         Enterprise Knowledge Sources
```

---

# AI Layer Decomposition

Instead of one AI service, divide the platform into specialized AI services.

| Layer              | Responsibility                   |
| ------------------ | -------------------------------- |
| AI Gateway         | Entry point for all AI requests  |
| Agent Router       | Determines the appropriate agent |
| Prompt Manager     | Stores system prompts            |
| Context Builder    | Builds conversation context      |
| RAG Engine         | Retrieves enterprise knowledge   |
| Model Router       | Chooses the optimal LLM          |
| Response Validator | Validates generated answers      |
| Feedback Engine    | Captures user feedback           |
| Token Analytics    | Tracks token consumption         |
| Audit Service      | Stores AI activity logs          |

---

# AI Request Flow

```text
User Question

↓

Authentication

↓

Authorization

↓

Determine Department

↓

Select AI Agent

↓

Retrieve Relevant Documents

↓

Generate Embeddings

↓

Vector Search

↓

Prompt Construction

↓

Azure OpenAI

↓

Grounding Verification

↓

Content Filter

↓

Response with Citation

↓

Conversation Storage

↓

Analytics Dashboard
```

---

# Agent Orchestration

Instead of one chatbot, each department gets its own specialized AI agent.

## HR Agent

Knowledge

* Leave Policy
* Employee Handbook
* Benefits
* Payroll FAQ

Actions

* Explain leave policy
* Summarize HR documents
* Draft HR emails

---

## IT Agent

Knowledge

* Troubleshooting
* Asset Database
* Ticket History
* SOPs

Actions

* Diagnose issues
* Create tickets
* Reset password workflow
* Recommend solutions

---

## Finance Agent

Knowledge

* Expense Policy
* Procurement
* Vendor Documents

Actions

* Explain reimbursement
* Summarize invoices
* Budget guidance

---

## Legal Agent

Knowledge

* Contracts
* Policies
* Compliance

Actions

* Explain clauses
* Compare contracts
* Highlight risks

---

# Multi-Agent Collaboration

Some questions require multiple agents.

Example

Employee asks:

> "Can I buy a laptop under my department budget?"

Workflow

```text
Question

↓

HR Agent

↓

Finance Agent

↓

IT Asset Agent

↓

Merge Results

↓

Single Response
```

---

# AI Orchestrator Responsibilities

The orchestrator decides:

* Which agent to use
* Which documents to retrieve
* Which model to use
* Which prompt template to load
* Maximum token limit
* Response temperature
* Security policies

---

# Prompt Management

Never hardcode prompts.

Store prompts separately.

Example

```text
Prompt Library

├── HR Prompt

├── Finance Prompt

├── IT Prompt

├── Legal Prompt

├── Executive Prompt

└── Default Prompt
```

Each prompt has

Version

Owner

Approval Status

Last Modified

Safety Policy

---

# Context Engineering

A production prompt contains:

```text
System Prompt

+

Conversation History

+

Retrieved Documents

+

User Role

+

Department

+

Business Rules

+

Current Question
```

Instead of:

```text
User Question

↓

GPT
```

Use:

```text
Question

↓

Context Builder

↓

Prompt Composer

↓

GPT
```

---

# Enterprise RAG Pipeline

```text
SharePoint

OneDrive

Blob

Teams

ERP

CRM

PDF

Word

↓

Document Intelligence

↓

OCR

↓

Metadata

↓

Chunking

↓

Embedding Generation

↓

Vector Index

↓

Azure AI Search

↓

Hybrid Search

↓

Top-k Retrieval

↓

Prompt Builder

↓

Azure OpenAI
```

---

# Chunking Strategy

Students should justify chunking.

Example

| Strategy          | Use            |
| ----------------- | -------------- |
| Fixed Size        | Simple PDFs    |
| Semantic Chunking | Policies       |
| Section Based     | Manuals        |
| Heading Based     | Word Docs      |
| Sliding Window    | Long Documents |

Recommended

800 Tokens

Overlap

100 Tokens

---

# Embedding Strategy

Use Azure OpenAI Embeddings.

Generate embeddings for

PDF

Word

PowerPoint

Email

Wiki

Store in

Azure AI Search

Metadata

Department

Security Group

Language

Owner

Created Date

Version

Sensitivity Label

---

# Hybrid Search

Don't rely only on vector search.

Use

Keyword Search

*

Semantic Ranking

*

Vector Similarity

Benefits

Higher Recall

Better Accuracy

Reduced Hallucination

---

# Model Routing

Instead of one expensive model

```text
Simple FAQ

↓

GPT-4.1-mini

---------------------

Document Summary

↓

GPT-4.1-mini

---------------------

Policy Explanation

↓

GPT-4.1

---------------------

Complex Legal Query

↓

GPT-4.1

---------------------

Translation

↓

GPT-4.1-mini
```

Benefits

40–60% lower cost

---

# Prompt Injection Protection

Before sending prompt

Run

Prompt Shield

↓

Injection Detection

↓

Sensitive Command Detection

↓

Block Malicious Prompt

↓

Proceed

---

# AI Safety Layer

```text
Prompt

↓

Prompt Filter

↓

LLM

↓

Output Filter

↓

PII Detection

↓

Content Moderation

↓

Citation Verification

↓

Response
```

---

# Citation Verification

Every response must contain

Source File

Page Number (where available)

Confidence Score

Retrieved Chunks

Example

```
Employee Handbook.pdf

Page 27

Confidence

96%
```

---

# AI Evaluation Framework

Evaluate

Faithfulness

Groundedness

Answer Relevance

Context Precision

Citation Accuracy

Latency

Token Usage

Cost

User Rating

---

# Conversation Memory

Short-term Memory

* Current conversation
* Last 10 interactions

Long-term Memory

* User preferences (where appropriate)
* Frequently accessed documents
* Saved conversations

Store in

Azure Cosmos DB

---

# Feedback Loop

```text
AI Response

↓

Thumbs Up / Down

↓

Feedback Database

↓

Evaluation

↓

Prompt Improvement

↓

Model Improvement
```

---

# AI Governance Dashboard

Administrators should monitor

Daily Requests

Successful Responses

Hallucination Rate

Average Response Time

Average Tokens

Most Used Agents

Prompt Versions

Blocked Prompts

Injection Attempts

Cost Per Department

Top Knowledge Sources

Inactive Documents

---

# Token Usage Dashboard

Display

Prompt Tokens

Completion Tokens

Embedding Tokens

Daily Usage

Monthly Usage

Department-wise Usage

User-wise Usage

Estimated Cost

---

# Cost Optimization Strategy

Use:

* Model routing (large vs. small models)
* Embedding cache
* Prompt cache
* Semantic cache for repeated questions
* Incremental indexing
* Batch document ingestion
* Autoscaling for AKS
* Retrieval limits (Top-k)
* Compression of conversation history

---


