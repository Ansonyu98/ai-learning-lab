# Workflow Analysis — Legal Content Automation

**Project:** Legal Content Automation  
**Document Type:** Project-specific Workflow Analysis  
**Stage:** Pre-Implementation Design  
**Status:** Approved for Architecture Design

---

# 1. Workflow Objective

本项目目标是建立一套可以脱离本地电脑、持续在云端运行的法律内容研究自动化 Workflow。

系统围绕：

```text
Social Content Discovery
↓
AI Basic Analysis
↓
Lawyer Human Review
↓
Priority Research
↓
Tracking / Deep Analysis
↓
ResearchSubject
↓
Long-tail Discovery / Case Matching
↓
Candidate Topic Generation
↓
Weekly Lawyer Review
↓
Monthly Search Optimization
```

形成闭环。

核心目标不是完全自动生成法律内容，而是：

> 自动完成重复的数据收集、整理、初步分析和研究辅助工作，将专业判断、内容价值判断和关键状态变更保留给律师。

---

# 2. Core Workflow Principles

## 2.1 Human-in-the-loop

AI / Automation 负责：

- Search
- Collection
- Normalization
- Deduplication
- Basic Analysis
- Topic Classification
- Tracking Calculation
- Deep Analysis
- Long-tail Discovery
- Case Matching
- Topic Recommendation
- Keyword Recommendation

律师负责：

- Candidate Keep / Reject
- Tracking Approval
- Deep Analysis Approval
- Comment Analysis Approval
- Tracking Re-evaluation
- Candidate Topic Approval
- Keyword Lifecycle Approval

---

## 2.2 AI Classification, Human Value Judgment

Topic Category：

```text
由 AI 自动归类
```

律师不负责每天人工分类。

律师每天只判断：

> 哪些内容值得留下和后续深入分析？

---

## 2.3 Evidence-backed Research

AI Summary 不是 Source of Truth。

重要 Output 应尽可能支持：

```text
Output
↓
Evidence
↓
Original Source
```

律师在 Feishu Review Candidate 时必须可以：

```text
点击 Source Link
↓
查看原始帖子
```

---

## 2.4 Preserve History

以下状态变化不得通过覆盖旧值实现：

```text
Lawyer Decision
Tracking Observation
Keyword Lifecycle
Re-evaluation
```

必须保留历史。

例如：

```text
Day 0:
Deep Analysis = No

Day 7:
Deep Analysis = Yes
```

两次 Decision 都必须存在。

---

## 2.5 Empty ≠ Error

Workflow 必须区分：

```text
Valid Empty Result
Technical Error
Data Error
Pending Human Decision
```

例如：

```text
No Relevant Case
No Valuable Comment
No Candidate Topic
```

属于正常业务结果。

---

# 3. Workflow Cadence

整个系统由四种时间节奏组成。

---

## 3.1 Daily

Daily 的主要职责：

```text
Data Collection
+
Basic Analysis
+
Lawyer Triage
```

核心不是每天进行 Deep Research。

---

## 3.2 7-Day Tracking

对律师批准 Tracking 的 Post：

```text
Day 0
↓
Observation
↓
7 Days
↓
Re-collection
↓
Growth Evidence
↓
Lawyer Re-evaluation where necessary
```

---

## 3.3 Weekly

Weekly 的主要职责：

```text
Research Consumption
+
Candidate Topic Decision
```

包括：

- Weekly Research Overview
- Key Research Findings
- Long-tail Evidence
- Case Evidence
- Candidate Topics
- Lawyer Topic Approval

---

## 3.4 Monthly

Monthly 的主要职责：

```text
Search Strategy Calibration
```

包括：

- Existing Keyword Performance
- Long-tail Candidate Review
- Keyword Lifecycle Decision
- Trial Keyword Promotion

---

# 4. Trigger Model

Workflow Trigger 分为：

```text
Schedule Trigger
Data / State Trigger
Manual / Human Trigger
```

---

# 5. Schedule Triggers

## Trigger A — Daily Search & Collection

```text
Monday – Saturday
10:00
```

启动：

```text
Task A — Search & Collection
```

---

## Trigger B — Tracking

Tracking 不再简单理解为：

```text
每周日统一追踪所有帖子
```

其业务本质是：

> 对已获得 Tracking Approval 的 Post，在满足 Observation Window 后进行 Re-collection。

MVP 可以通过 Scheduled Batch 实现，但业务规则必须基于：

```text
TrackingState
+
Next Check Time
```

而不是单纯依赖星期几。

---

## Trigger C — Weekly Research

Weekly Research Workflow 在本周有效 Research Data 准备完成后启动。

用于：

```text
Research Aggregation
↓
Candidate Topic Generation
↓
Weekly Feishu Delivery
```

---

## Trigger D — Monthly Keyword Calibration

```text
Monthly
```

基于过去一个月真实 Workflow Data 进行 Keyword Review。

---

# 6. Human / State Triggers

以下属于 Human Decision / State Change Trigger：

```text
Candidate Keep
Candidate Reject
Track Approval
Deep Analysis Approval
Comment Analysis Approval
Tracking Re-evaluation
Topic Approval
Keyword Lifecycle Approval
```

这些 Action 必须：

```text
Human Action
↓
Validated Event
↓
Persist Decision
↓
Update Business State
↓
Trigger Eligible Downstream Workflow
```

---

# 7. Workflow Overview

```text
Keyword Pool
↓
Task A
Search & Collection
↓
Normalization
↓
Validation
↓
Deduplication
↓
AI Basic Analysis
↓
Candidate Selection
↓
Daily Feishu Review
↓
Lawyer Decision
↓
Keep?
│
├── No
│    ↓
│  Preserve History
│
└── Yes
     ↓
 Priority Pool
     │
     ├──────────────┐
     ↓              ↓
 Tracking       Deep Analysis
     ↓              ↓
 Task B           Task C
     ↓              ↓
 New Evidence   ResearchSubject
     ↓              │
 Re-review          ├──────────────┐
                    ↓              ↓
                  Task D          Task F
               Long-tail       Case Matching
                    \              /
                     \            /
                      ↓          ↓
                         Task G
                    Topic Generation
                         ↓
                 Weekly Research
                         ↓
                  Lawyer Approval
                         ↓
                Approved Topic Pool

Research / Decision Data
          ↓
        Task E
Monthly Keyword Calibration
          ↓
Keyword Lifecycle / Trial Keywords
          ↓
Next Search Cycle
```

---

# 8. Task A — Search, Collection & Basic Analysis

## 8.1 Objective

Task A 负责：

> 按照当前 Keyword Pool 自动发现社交媒体内容，并将原始结果转换为可供 Daily Review 使用的 Candidate Data。

---

# 9. Task A Input

MVP Input 包括：

### 9.1 Search Keywords

来源：

```text
Active Seed Keywords
+
Eligible Trial Keywords
```

MVP 初始阶段：

```text
Daily Search ≤ 4 Seed Keywords
```

作为早期成本和数据量控制策略。

后续根据真实运行结果调整。

---

### 9.2 Platform

MVP：

```text
Xiaohongshu
```

通过可用第三方数据服务进行采集。

当前验证过：

```text
TikHub
```

---

### 9.3 Search Time Window

```text
7 Days
```

同时保存：

```text
collected_at
```

以区分：

```text
Post Published Time
vs
System Collection Time
```

---

### 9.4 Search Configuration

包括：

- Search Keyword
- Platform
- Result Limit
- Search Sort where supported
- Time Window
- Ad / Irrelevant Content Filtering
- Deduplication Rule

---

### 9.5 Candidate Limit

MVP 初期：

```text
每个 Keyword ≤ 5 Candidate Results
```

具体值作为 Config 管理，而不是长期硬编码业务规则。

---

### 9.6 Tags / Hashtags

如果 Source Platform 提供：

```text
tags / hashtags
```

则作为 Post Input 保存。

---

# 10. Task A Process

```text
Keyword
↓
TikHub Search
↓
Raw Result
↓
Normalization
↓
Validation
↓
Deduplication
↓
Persist Post
↓
AI Basic Analysis
↓
Candidate Gate
↓
Daily Review Queue
```

---

# 11. Normalization Before Validation

固定顺序：

```text
Raw API Data
↓
Normalization
↓
Validation
↓
Persistence
```

Normalization 处理：

- Field Naming
- Datetime
- Timezone
- Numeric Types
- Empty String
- Null
- Array
- Platform-specific Fields

原则：

```text
empty string ≠ null
```

必须按照 Data Contract 统一。

---

# 12. Deduplication

Primary Deduplication Key：

```text
platform + post_id
```

同一 Post 被多个 Keyword 搜到：

```text
只保留一个 Post Object
```

但保留多个：

```text
SearchHit
```

因此：

```text
Post
≠
SearchHit
```

---

# 13. Basic Analysis

AI Basic Analysis 负责：

```text
Topic Classification
Short Summary
Research Relevance
```

Topic Category：

```text
AI Generated
```

律师无需人工归类。

Basic Analysis 不负责：

- Deep Legal Research
- Long-tail Promotion
- Case Matching
- Final Topic Generation

---

# 14. Candidate Gate

Candidate 先经过：

```text
AI Relevance Gate
```

进入 Candidate 后，Daily Review 默认排序参考：

```text
Current Engagement
↓
Published Time
```

MVP 不建立人工复杂综合 Score。

---

# 15. Daily Feishu Delivery

Daily Delivery 至少包含：

```text
Daily Overview
+
Candidate Cards
```

Daily Overview：

- Keyword Count
- Collected Post Count
- Candidate Count
- AI Topic Overview
- Workflow Completion Status

Candidate Card：

- Title
- AI Summary
- Topic Category
- Engagement
- Published Time
- Source Keyword
- Source URL

---

# 16. Lawyer Daily Review

采用 Progressive Review。

```text
Keep?
│
├── Reject
│     ↓
│    End
│
└── Keep
      ↓
 Priority Pool
      ↓
 Track?
 Yes / No
      ↓
 Deep Analysis?
 Yes / No
      │
      └── Yes
            ↓
 Comment Analysis?
 Yes / No
```

---

# 17. Priority Pool Rule

必须满足：

```text
Deep Analysis Approved
→
Priority Pool
```

但：

```text
Priority Pool
↛
Deep Analysis Required
```

因此可以：

```text
Keep = Yes
Track = Yes
Deep Analysis = No
```

---

# 18. Pending Decision

律师没有当天 Review：

```text
review_status = pending
```

不能自动：

```text
reject
```

---

# 19. Task B — Tracking

## 19.1 Objective

Tracking 用于：

> 获取一段观察期后的 Engagement Change，形成新的 Evidence。

它不负责自动决定帖子价值。

---

# 20. Tracking Eligibility

只有：

```text
Priority Pool
+
Track = Yes
```

才进入 Tracking。

MVP 不采用：

> 后续自然涨到 >500 就自动进入 Priority Pool。

Priority Pool 仍然来自 Lawyer Keep Decision。

---

# 21. Initial Observation

Tracking 创建时保存：

```text
Observation 0
```

至少包括：

- Likes
- Comments
- Saves
- Total Engagement
- Observed At

---

# 22. Follow-up Observation

观察期满足后：

```text
Re-collect Post
↓
Observation 1
```

计算：

```text
Absolute Growth
Growth Rate
```

---

# 23. Tracking Review

律师看到：

- Original Post
- Source Link
- Day 0 Engagement
- Day 7 Engagement
- Growth
- Growth Rate
- Previous Decision
- Current Research State

---

# 24. Tracking Re-evaluation

如果：

```text
Previous Deep Analysis = No
```

Tracking 后允许：

```text
Deep Analysis = Yes
```

新的 Decision：

```text
Append
```

不得覆盖旧 Decision。

---

# 25. Existing Deep Analysis

如果：

```text
Deep Analysis
Already Approved / Completed
```

Tracking Result：

```text
作为新增 Evidence 保存
```

但不重复要求相同审批。

---

# 26. Task C — Deep Analysis

## 26.1 Objective

Task C 将：

```text
Selected Priority Post
```

转换成：

```text
Structured ResearchSubject
```

供后续：

```text
Long-tail Discovery
Case Matching
Topic Generation
```

使用。

---

# 27. Task C Eligibility

必须满足：

```text
Priority Pool
+
Deep Analysis Approved
```

---

# 28. Comment Analysis Decision

律师决定：

```text
Comment Analysis?
Yes / No
```

原因：

不同 Post 的评论研究价值不同。

因此 Comment Analysis 不自动对所有 Deep Analysis Post 执行。

---

# 29. Comment Selection

如果：

```text
Comment Analysis = Yes
```

优先选择：

```text
High-like
+
Strong Post Relevance
↓
Top 10
```

如果不足：

```text
Latest Comments
↓
Fill up to 10 where possible
```

---

# 30. Incomplete Post Content

“正文不完整”不作为一个单独自动触发 Comment Analysis 的硬规则。

可能包括：

- Source API 只返回摘要；
- 正文被截断；
- 内容主要存在于图片 / 视频；
- Post 文本无法完整表达问题；
- 原帖上下文不足。

但是否值得进一步分析评论：

```text
仍由律师决定
```

而不是系统自动认为：

```text
正文不完整
→
必须 Comment Analysis
```

---

# 31. ResearchSubject

Task C 至少输出：

```text
core_topic

user_problem

legal_business_issues[]

user_expressions[]

content_opportunities[]

post_evidence[]

comment_findings[]     // optional

comment_evidence[]     // optional
```

---

# 32. User Expressions

尽可能保留真实用户表达。

来源可以包括：

```text
Post
Comment
```

并保留 Source Evidence。

---

# 33. Deep Analysis Delivery Rule

Task C 完成：

```text
Persist ResearchSubject
```

不单独立即推送律师。

之后可以自动进入符合条件的：

```text
Task D
Task F
Task G
```

律师主要在：

```text
Weekly Research
```

消费研究成果。

---

# 34. Task D — Long-tail Keyword Discovery

## 34.1 Objective

Task D 从真实 Research Evidence 中发现：

> 用户实际使用、可能适合作为未来搜索入口的表达。

---

# 35. Task D Input

主要输入：

```text
ResearchSubject.user_expressions
+
Available Post / Comment Evidence
```

---

# 36. Task D Process

```text
Raw User Expression
↓
Normalization
↓
Semantic Grouping
↓
Occurrence / Source Evidence
↓
LongTailCandidate
```

---

# 37. Task D Output

至少包含：

```text
normalized_keyword
raw_expressions[]
occurrence_count
source_count
related_topics[]
source_evidence[]
```

---

# 38. No Automatic Promotion

Task D 不能：

```text
自动修改正式 Search Keyword Pool
```

只生成：

```text
LongTailCandidate
```

等待 Monthly Review。

---

# 39. Task E — Monthly Keyword Calibration

## 39.1 Objective

Task E 使用过去一个月真实 Workflow Outcome：

```text
Keyword
↓
Search
↓
Candidate
↓
Keep
↓
Deep Analysis
↓
CandidateTopic
↓
ApprovedTopic
```

判断 Search Keyword 是否持续创造价值。

---

# 40. Existing Keyword Evidence

至少统计：

```text
Search Volume

Candidate Count
Candidate Rate

Keep Count
Keep Rate

Deep Analysis Count

Candidate Topic Count

Approved Topic Count
```

---

# 41. Keyword Recommendation

System 可以生成：

```text
Continue
Reduce
Retire
```

Recommendation。

但：

```text
System Recommendation
≠
Final Decision
```

MVP：

```text
Lawyer Approval Required
```

---

# 42. Long-tail Candidate Review

Monthly Review 同时展示：

```text
LongTailCandidate
+
Evidence
```

律师决定：

```text
Approve
Reject
```

---

# 43. Trial Keyword

Approved Long-tail Candidate：

```text
Trial / Observe
```

而不是直接成为成熟 Active Keyword。

```text
Trial Keyword
↓
Real Search
↓
Real Performance
↓
Future Calibration
```

---

# 44. Keyword Lifecycle

建议状态：

```text
active
observe
reduced
retired
```

用户层操作：

```text
Continue
Reduce
Retire
```

新词：

```text
Trial / Observe
```

所有状态变化保留：

```text
KeywordHistory
```

---

# 45. Task F — Case Library Matching

## 45.1 Objective

将：

```text
ResearchSubject
```

与律师现有案例库进行匹配，为内容研究提供真实案例 Evidence。

---

# 46. Existing Case Library

当前案例库流程：

```text
Judgment Documents
↓
Codex
↓
Rule-based Structured Extraction
↓
Unified Excel File
```

Excel 持续在本地更新。

---

# 47. Future Case Library Requirement

长期需要将案例库：

```text
Online / Cloud Accessible
```

使 Workflow 可以：

```text
ResearchSubject
↓
Case Retrieval
↓
CaseMatch
```

无需依赖个人电脑。

---

# 48. Technology Neutrality

Workflow Analysis 只定义：

> ResearchSubject 需要能够匹配相关案例。

当前不规定：

```text
SQL
Full-text
Embedding
Vector DB
RAG
Hybrid Retrieval
```

在 Architecture 阶段根据：

```text
Existing Excel Schema
Case Volume
Query Pattern
Retrieval Quality
Cost
```

决定。

---

# 49. Task F Output

```text
CaseMatch
```

应至少关联：

```text
ResearchSubject
Case
Match Evidence / Reason
```

No Relevant Case：

```text
Valid Empty Result
```

不得阻塞后续 Topic Generation。

---

# 50. Task G — Candidate Topic Generation

## 50.1 Objective

将 Research Evidence 转化为：

```text
Evidence-backed Candidate Topic
```

供律师进行 Weekly Content Decision。

---

# 51. Required Evidence

Required：

```text
ResearchSubject
```

Optional：

```text
TrackingEvidence
LongTailCandidate
CommentEvidence
CaseMatch
Search Evidence
```

因此：

```text
Missing Optional Evidence
```

不能阻塞 Topic Generation。

---

# 52. Candidate Topic Output

至少包括：

```text
topic

suggested_angle

recommendation_rationale

research_subject_reference

available_evidence

source_links
```

---

# 53. Weekly Research Package

Weekly Package 按用户任务组织，而不是按后台 Task 组织。

```text
Weekly Overview
↓
Key Research Findings
↓
Candidate Topics
↓
Supporting Evidence
↓
Lawyer Decision
```

原则：

```text
System Architecture
≠
Information Architecture
```

---

# 54. Candidate Topic Review

律师决定：

```text
Approve
Reject
```

Approved：

```text
Approved Topic Pool
```

Rejected：

```text
保留 CandidateTopic
+
Decision History
```

---

# 55. Topic Rating

可提供：

```text
1–5
```

作为 Optional Feedback。

不得成为 Topic Approval 的 Mandatory Input。

---

# 56. Feishu Integration

Feishu 不只是 Daily Notification Tool。

它是整个 Workflow 的：

```text
Human Interaction Layer
```

用于：

### Daily

```text
Collection Overview
Candidate Review
```

### Tracking

```text
Tracking Evidence
Re-evaluation
```

### Weekly

```text
Research Findings
Candidate Topics
Topic Approval
```

### Monthly

```text
Keyword Performance
Keyword Lifecycle Approval
Long-tail Trial Approval
```

---

# 57. Feishu Is Not System of Record

Feishu：

```text
Display
+
Interaction
```

Backend Database：

```text
System of Record
```

因此：

```text
Feishu Action
↓
Backend Event
↓
Validation
↓
Persistence
↓
State Change
```

---

# 58. Data Relationships

核心逻辑关系：

```text
Keyword
1 → many SearchHit

Post
1 → many SearchHit

Post
1 → many EngagementObservation

Post
1 → many LawyerDecision

Post
0..1 → TrackingState

Post
0..many → DeepAnalysisRequest

DeepAnalysisRequest
0..1 → ResearchSubject

ResearchSubject
0..many → LongTailCandidate

ResearchSubject
0..many → CaseMatch

ResearchSubject
0..many → CandidateTopic

CandidateTopic
0..many → LawyerDecision
```

具体 Field-level Schema：

以：

```text
data-contract.md
```

为准。

---

# 59. Error Handling

Workflow 需要区分：

## Technical Error

例如：

```text
TikHub Timeout
LLM Timeout
Database Failure
Feishu Failure
```

处理：

```text
Log
↓
Retry where appropriate
↓
Preserve Successful Items
```

---

## Data Error

例如：

```text
Missing Required Field
Invalid Datetime
Invalid JSON
Schema Validation Failure
```

不得进入下游。

---

## Valid Empty

例如：

```text
No Search Result
No Valuable Comment
No CaseMatch
No CandidateTopic
```

记录为正常业务结果。

---

## Pending

Human Decision 未完成：

```text
pending
```

不得自动解释为：

```text
reject
```

---

# 60. Reliability Rules

## Partial Success

例如：

```text
4 Keywords

3 Success
1 Failure
```

Workflow：

```text
Partial Success
```

成功数据必须保留。

---

## Retry

关键 External Dependency Failure：

应支持 Retry。

具体 Retry Policy：

Architecture / Implementation 阶段定义。

---

## Idempotency

重复：

```text
Webhook
Schedule
Retry
```

不得创建重复业务副作用。

重点对象：

```text
Post
LawyerDecision
TrackingState
DeepAnalysisRequest
Delivery
```

---

# 61. AI Output Rules

所有进入 Downstream Workflow 的 AI Structured Output：

```text
LLM
↓
Structured Output
↓
Schema Validation
↓
Valid?
├── Yes → Persist
└── No → Retry / Error
```

AI Output 应尽可能保存：

```text
model
prompt_version
generated_at
validation_status
```

---

# 62. Workflow Observability

每个 Workflow Run 至少记录：

```text
workflow_name
started_at
finished_at
status
items_processed
success_count
failure_count
error_summary
```

状态至少区分：

```text
success
partial_success
failed
```

---

# 63. Cloud Runtime Requirement

正式 MVP：

```text
用户关闭电脑
↓
Daily / Tracking / Weekly / Monthly Workflow
仍可运行
```

因此需要：

```text
Cloud Automation Runtime
+
Online Persistent Storage
```

具体 Technology Stack：

Architecture 阶段确定。

---

# 64. Cost-control Principle

采用分层 Processing：

```text
Search
↓
Basic Analysis
↓
Human Filter
↓
Selective Tracking
↓
Selective Deep Analysis
↓
Optional Comment Analysis
```

避免：

```text
All Posts
↓
Full Deep Analysis
```

造成不必要的 API / LLM Cost。

---

# 65. Workflow Metrics

核心 Funnel：

```text
Search Hits
↓
Candidate
↓
Keep
↓
Deep Analysis
↓
Candidate Topic
↓
Approved Topic
```

主要观察：

```text
Lawyer Keep Rate

Topic Approval Rate

Approved Topics / Week

Manual Research Time
```

辅助：

```text
Candidate Rate
Deep Analysis Rate
Tracking Re-evaluation Rate
Comment Analysis Usage
Keyword → Approved Topic
Structured Output Failure
Workflow Success Rate
```

初始 MVP：

```text
Collect Baseline
↓
2–4 Weeks
↓
Set Targets
```

不提前制造缺乏依据的精确 KPI。

---

# 66. MVP Platform Scope

MVP：

```text
Xiaohongshu
```

暂不正式接入：

```text
Douyin
WeChat Channels
Other Platforms
```

但 Data Contract / Architecture 应尽可能避免将所有逻辑写死为：

```text
xiaohongshu_only
```

以保留未来扩展空间。

---

# 67. Out of Scope

MVP 暂不处理：

```text
Automatic Script Generation

Automatic Image / Video Generation

Automatic Publishing

Published-content Analytics

Complex Ranking Model

Fine-tuning

Forced RAG

Forced Agent Architecture

Multi-user SaaS

Billing

Independent Web App

Mobile App
```

---

# 68. Workflow Dependency Map

```text
Task A
Search / Collection / Basic Analysis
        │
        ↓
Daily Lawyer Review
        │
        ↓
Priority Pool
     ┌──┴───────────┐
     ↓              ↓
Task B             Task C
Tracking       Deep Analysis
                    │
                    ↓
             ResearchSubject
               ┌────┴────┐
               ↓         ↓
             Task D     Task F
           Long-tail    Case
               \         /
                \       /
                  Task G
             Topic Generation
                    │
                    ↓
             Weekly Review

Task D
+
Keyword Outcome Data
        ↓
Task E
Monthly Calibration
        ↓
Keyword Pool
        ↓
Task A
```

---

# 69. Workflow Design Status

```text
Business Problem                 Defined

Trigger Model                    Defined

Task A Input                     Defined
Task A Process                   Defined

Daily Review                     Defined
Priority Pool                    Defined

Task B Tracking                  Defined
Tracking Re-evaluation           Defined

Task C Deep Analysis             Defined
Comment Analysis                 Defined
ResearchSubject                  Defined

Task D Long-tail Discovery       Defined

Task E Keyword Calibration       Defined

Task F Case Matching             Defined

Task G Topic Generation          Defined

Daily / Weekly / Monthly Cadence Defined

Feishu Interaction Model         Defined

Error / Empty / Pending          Defined

Cross-workflow Dependencies      Defined

Data Contract Dependency         Defined

Cloud Requirement                Defined

Reliability Rules                Defined

Evaluation Funnel                Defined
```

---

# 70. Architecture Handoff

Workflow Analysis 已回答：

```text
What happens?

When does it happen?

What triggers it?

What data enters?

What decisions exist?

What state changes?

What depends on what?

Where does Human Judgment occur?
```

下一阶段：

```text
System Architecture
```

需要回答：

```text
Where does each workflow run?

What is handled by n8n?

What is handled by code?

Where is the database?

How does Feishu communicate with the backend?

How are webhook events secured?

How are retries implemented?

How is TikHub integrated?

Which LLM is used where?

How is the Excel case library moved online?

How is case retrieval implemented?

Which components actually need AI?

Which components should remain deterministic?
```

---

# 71. Final Workflow Principle

The workflow should not automate professional judgment.

It should automate the repetitive work surrounding professional judgment.

Therefore:

```text
Collect automatically

Normalize consistently

Analyze structurally

Preserve evidence

Ask humans only when judgment matters

Persist every meaningful decision

Use feedback to improve future discovery

Keep the workflow operational without local-machine dependency
```

最终形成：

```text
Discovery
↓
Human Triage
↓
Research
↓
Evidence
↓
Decision
↓
Feedback
↓
Search Improvement
```

的持续内容研究闭环。