# Day 08 — Product & Technical Design / MVP Design Freeze

## Today's Goal

Day 01–07 已经完成业务 Workflow：

Business Problem
↓
Trigger
↓
Input
↓
Data Contract
↓
Process
↓
Decision
↓
Action
↓
Output

Day 08 的目标是：

> 把业务 Workflow 转换成一个可以开始实施的 Product / System Design。

核心问题：

- MVP 到底是什么？
- 用户是谁？
- 系统由哪些层组成？
- 哪些技术现在应该引入？
- 哪些技术暂时不需要？
- 如何从 Design 进入 Build？

---

# 1. MVP Product Definition

项目正式定义为：

> AI-powered Legal Content Research & Topic Discovery System

它不是：

“AI自动生成标题工具”

也不是：

“社媒爆款抓取器”

而是一套：

> Human-in-the-loop Legal Content Research System

核心闭环：

Social Search
↓
Collection
↓
AI Basic Analysis
↓
Lawyer Review
↓
Tracking / Deep Research
↓
Long-tail Discovery
↓
Case Matching
↓
Candidate Topic Generation
↓
Lawyer Approval
↓
Keyword Feedback Loop

---

# 2. Primary User

MVP Primary User：

> Lawyer / Legal Content Creator

第一版实际上：

> Single User

因此 MVP 暂时不需要：

- Multi-user
- Tenant Isolation
- Billing
- Subscription
- Complex Permission System
- Customer Onboarding

这些属于 Future Productization。

---

# 3. Daily User Journey

每天：

System Search
↓
Collect
↓
Basic AI Analysis
↓
Feishu Daily Review
↓
Lawyer:

Keep?
Track?
Deep Analysis?
Comment Analysis?

目标：

律师不需要每天：

- 打开平台搜索
- 手工整理 Excel
- 手工记录互动数据
- 手工复制内容给 AI

---

# 4. Weekly User Journey

系统基于本周数据处理：

Tracking
+
Deep Research
+
Long-tail Findings
+
Available Case Context
+
Candidate Topics

然后：

Weekly Research Package
↓
Feishu
↓
Lawyer Review
↓
Approved Topic Pool

---

# 5. Monthly User Journey

每月：

Keyword Evidence
+
Lawyer Feedback
+
Research Outcomes
+
Long-tail Evidence
↓
Keyword Calibration Recommendation
↓
Feishu
↓
Lawyer Approval
↓
Updated Keyword Library

形成 Feedback Loop。

---

# 6. Functional Requirements

MVP 核心 Functional Requirements：

FR-01
Automated Social Search

FR-02
Normalization & Persistence

FR-03
Deduplication

FR-04
Basic AI Analysis

FR-05
Daily Lawyer Review

FR-06
7-Day Tracking

FR-07
Deep Analysis

FR-08
Long-tail Discovery

FR-09
Case Matching

FR-10
Candidate Topic Generation

FR-11
Keyword Calibration

FR-12
Feishu Human Interaction

FR-13
Unattended Cloud Execution

---

# 7. Non-functional Requirements

系统不仅需要：

Workflow Runs

还需要：

- Reliability
- Traceability
- Recoverability
- Auditability
- Maintainability
- Extensibility

需要避免：

- Duplicate Data
- Silent Failure
- Lost Decisions
- Untraceable AI Output
- Local Computer Dependency

---

# 8. System Architecture

MVP 建议架构：

Xiaohongshu
↓
TikHub API
↓
n8n Automation
├── Schedule
├── API Calls
├── Workflow Rules
├── AI Calls
├── Error Handling
└── HITL Orchestration
↓
PostgreSQL
System of Record
↓
AI / LLM
↓
Feishu
Human Interaction Layer
↓
Lawyer
↓
Decision Event
↓
n8n Downstream Workflow

另外：

Structured Case Library
↓
Case Matching

---

# 9. Why n8n?

项目天然需要：

- Schedule
- API
- Conditional Branch
- Webhook
- Database
- LLM
- Feishu
- Retry
- Workflow Orchestration

因此 n8n 与真实业务需求匹配。

不是：

为了简历强行使用 n8n。

而是：

> Technology follows workflow requirements.

---

# 10. Data Layer

整个 Automation System 不适合继续使用 Excel 作为核心数据库。

原因：

已经存在大量：

- 1:N Relationship
- N:M Relationship
- Historical Observation
- Decision History
- Workflow State
- Idempotency
- Traceability

因此建议：

> PostgreSQL

作为 MVP System of Record。

---

# 11. Why Relational Database?

核心对象关系非常明显：

Keyword ↔ Post
Post ↔ Search Hit
Post ↔ Observation
Post ↔ Decision
Post ↔ Research Subject
Research Subject ↔ Case
Research Subject ↔ Topic

因此：

Relational Database

比简单 Spreadsheet 更适合。

---

# 12. Case Library Strategy

当前已有：

Judgment
↓
Codex
↓
Structured Excel

不推翻现有流程。

MVP 采用：

Existing Excel
↓
Import / Sync
↓
Online Structured Case Data
↓
Task F

未来再考虑：

Judgment Ingestion
↓
Automatic Structuring
↓
Online Update

---

# 13. AI Layer

MVP AI 主要负责：

- Relevance
- Topic Classification
- Summary
- Deep Analysis
- Structured Research Subject
- User Expression Extraction
- Semantic Clustering
- Case Relevance
- Topic Generation
- Semantic Deduplication

当前优先学习：

LLM API
↓
Prompt
↓
JSON
↓
Structured Output
↓
Schema Validation
↓
Retry
↓
Evaluation

---

# 14. Why Not Agent First?

当前绝大部分 Workflow：

下一步是什么

本来就是确定的。

因此：

Deterministic Workflow
+
LLM Calls

已经足够。

如果现在强行 Agent：

会增加：

- Cost
- Uncertainty
- Debug Difficulty

因此：

MVP:
No Agent Required

---

# 15. RAG Introduction Point

Task F 是最自然的 RAG Learning Point：

Research Subject
↓
Retrieve Relevant Cases
↓
Provide Context
↓
Support Analysis / Topic Generation

但第一版不必立刻：

Vector Database
+
Embedding
+
Complex RAG

可以先：

Structured Case Fields
↓
Simple Search / SQL
↓
LLM Relevance

真实 Retrieval Problem 出现后，再升级：

Embedding
↓
Vector Search
↓
Hybrid Retrieval
↓
RAG Evaluation

---

# 16. Webhook Learning Point

Feishu Lawyer Decision：

Feishu
↓
Lawyer Action
↓
Decision Event
↓
Automation

天然需要：

Webhook / Callback

因此 Webhook 在 Implementation 阶段有真实业务需求。

---

# 17. Python Role

不应该为了证明会 Python：

把 n8n 能完成的所有工作重新写成 Python。

n8n：

Main Orchestration

Python：

- Data Processing
- Evaluation
- Migration
- API Testing
- Case Data Processing
- Utility Scripts

Python 作为并行基础能力学习。

---

# 18. Technical Learning Order

接下来的技术学习不再按课程顺序，而是围绕 Build：

1. HTTP
2. REST API
3. JSON
4. TikHub API Call
5. n8n Basics
6. Schedule + HTTP Request
7. PostgreSQL
8. SQL Basics
9. Persist API Data
10. LLM API
11. Structured Output
12. Validation
13. Error Handling
14. Feishu Integration
15. Webhook / HITL
16. Cloud Deployment
17. Evaluation

核心：

> Learn technology when the project needs it.

---

# 19. Workflow Deployment Architecture

不建议：

One Giant Workflow

而建议：

WF-A
Daily Search & Collection

WF-A2
Basic AI Analysis + Daily Review

WF-H
Human Decision Handler

WF-B
7-Day Tracking

WF-C
Deep Analysis

WF-D
Long-tail Discovery

WF-E
Monthly Keyword Calibration

WF-F
Case Matching

WF-G
Weekly Topic Generation

WF-OPS
Failure / Operational Alert

通过：

Persistent State
+
Events

连接。

---

# 20. Core Logical Data Objects

当前识别：

- WorkflowRun
- Keyword
- KeywordHistory
- Post
- SearchHit
- EngagementObservation
- BasicAnalysis
- ReviewItem
- LawyerDecision
- TrackingState
- TrackingEvidence
- DeepAnalysisRequest
- ResearchSubject
- Comment
- SelectedComment
- LongTailCandidate
- ExpressionEvidence
- Case
- CaseMatch
- CandidateTopic
- TopicEvidence
- DeliveryRecord

具体 Database Schema：

留到 Implementation。

---

# 21. Feishu Architecture

Feishu：

Human-facing Workspace

承担：

Review
Decision
Reporting

PostgreSQL：

System of Record

承担：

Authoritative Data
State
History
Relationships

核心区别：

> Feishu is where the human works.
> PostgreSQL is where the system remembers.

---

# 22. Cloud Requirement

MVP 正式要求：

Local Computer OFF
↓
System Still Runs

因此：

n8n
+
Database
+
Scheduler

必须部署到：

Cloud-accessible Environment

具体 Provider：

Implementation 阶段选择。

---

# 23. MVP Out of Scope

为了避免无限设计，第一版明确不做：

- Multi-platform
- Multi-user SaaS
- Billing
- Custom Web Frontend
- Mobile App
- Multi-Agent
- Fine-tuning
- LangGraph
- CrewAI
- AutoGen
- Complex Vector RAG
- Model Training
- Fully Autonomous Lawyer Decisions
- Automatic Keyword Production Changes
- Automatic Final Topic Approval
- Advanced Cross-platform Scoring

---

# 24. Product Manager Portfolio

Project 2 不只是 Automation Project。

它应该同时形成 Product Portfolio：

- Business Problem
- User / Stakeholder
- As-Is Workflow
- Pain Points
- Product Goal
- MVP Scope
- User Story
- Acceptance Criteria
- Workflow Diagram
- PRD
- Architecture
- Implementation
- Test Cases
- Evaluation
- Iteration Log
- Final Case Study

---

# 25. Build Strategy — Vertical Slice

不按照：

A全部搭完
↓
B全部搭完
↓
C全部搭完

而是优先跑通 End-to-End Value。

---

# 26. Build Slice 1

Schedule
↓
TikHub
↓
Search
↓
Normalize
↓
PostgreSQL

目标：

> Cloud-based automated collection + persistence

---

# 27. Build Slice 2

Stored Candidate
↓
LLM
↓
Structured Basic Analysis
↓
Database
↓
Feishu Daily Review

目标：

> AI Research Pipeline

---

# 28. Build Slice 3

Feishu Lawyer Decision
↓
Webhook
↓
Persist Decision
↓
Create Downstream Request

目标：

> Human-in-the-loop closed loop

前三个 Slice 完成后，系统已经形成第一个真正可工作的 MVP Milestone。

---

# 29. Later Build Slices

Slice 4:

7-Day Tracking
+
Deep Analysis

Slice 5:

Long-tail Discovery
+
Candidate Topic Generation
+
Weekly Review

Slice 6:

Keyword Calibration
+
Monthly Feedback Loop

Slice 7:

Case Library Online Integration
+
Case Matching
+
Future RAG Evolution

---

# 30. Design Risk Review

主要风险：

Risk 1:
TikHub Stability

Risk 2:
Feishu HITL Integration Complexity

Risk 3:
Over-designed Data Model

Risk 4:
Over-designed AI Layer

Risk 5:
Weekly Workflow Dependency

Risk 6:
Case Library Online Integration

对应原则：

- Retry / Failure Classification
- Early Technical Spike
- Minimum Schema First
- Structured LLM Before Agent
- Persisted State for Decoupling
- Case Matching should not block core MVP

---

# 31. Design Freeze

截至 Day 08：

Business Problem             ✅
User                         ✅
Pain Points                  ✅
MVP Scope                    ✅
Success Metrics              ✅
Trigger                      ✅
Input                        ✅
Data Contract                ✅
Process                      ✅
Decision                     ✅
Action                       ✅
Output                       ✅
HITL                         ✅
Failure Handling             ✅
Idempotency                  ✅
Traceability                 ✅
Product Requirements         ✅
System Architecture          ✅
Data Architecture            ✅
AI Architecture              ✅
Feishu Architecture          ✅
Cloud Requirement            ✅
Technology Mapping           ✅
Build Sequencing             ✅
Risk Review                  ✅

仍未确定：

- Exact DB Schema
- Exact API Payload
- Exact n8n Nodes
- Exact Prompt
- Exact JSON Schema
- Exact Feishu Card
- Exact Retry Count
- Exact AI Model
- Exact Cloud Provider

这些不应该继续停留在理论设计阶段。

应该：

> Learn and decide during implementation using real APIs and real data.

---

# 32. Key Mindset Change

Day 08 最大的变化：

从：

Workflow Designer

开始进入：

Product + System Builder

并进一步理解：

Business Requirement
↓
Product Requirement
↓
System Architecture
↓
Technology Mapping
↓
Implementation

技术不应该反过来定义业务。

---

# 33. Day 08 Deliverables

✅ MVP Product Definition
✅ Primary User
✅ Daily / Weekly / Monthly User Journey
✅ Functional Requirements
✅ Non-functional Requirements
✅ System Architecture
✅ n8n Role
✅ PostgreSQL Direction
✅ Case Library Strategy
✅ AI Layer
✅ RAG Introduction Strategy
✅ Agent Boundary
✅ Webhook Learning Point
✅ Python Role
✅ Technical Learning Order
✅ Workflow Deployment Architecture
✅ Logical Data Objects
✅ Feishu Architecture
✅ Cloud Requirement
✅ MVP Out-of-scope
✅ Portfolio Mapping
✅ Vertical Slice Build Strategy
✅ Risk Review
✅ MVP Design Freeze

---

# 34. Next Step

Theoretical Design Phase:

COMPLETE

Next:

Design Consolidation
↓
Documentation Update
↓
GitHub Checkpoint
↓
BUILD PHASE

First Build Target:

Schedule
↓
TikHub API
↓
Real JSON
↓
Normalization
↓
n8n
↓
PostgreSQL

学习模式也正式改变：

不再：

Learn Tool
↓
Find Project

而是：

Real Project Requirement
↓
Encounter Technical Problem
↓
Learn Required Technology
↓
Implement
↓
Test
↓
Debug
↓
Document

核心原则继续保持：

> Project-driven Learning.