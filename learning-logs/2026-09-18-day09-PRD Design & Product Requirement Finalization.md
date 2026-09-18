# Day 09 — PRD Design & Product Requirement Finalization

**Project:** Legal Content Automation  
**Stage:** Product Requirements Design  
**Status:** Completed

---

# 1. Today's Goal

Day 09 的目标不是继续扩展 Workflow，而是将前面已经完成的：

```text
Business Problem
↓
Trigger Analysis
↓
Input Analysis
↓
Process Analysis
↓
Cross-workflow Review
↓
Data Contract
```

进一步转化为正式的：

```text
Product Requirements Document
```

核心问题从：

> Workflow 应该怎么运行？

转变为：

> 如果把这套 Workflow 当成一个真正给律师使用的产品，它应该提供什么功能、如何让律师参与、什么属于 MVP，以及如何判断它是否真正有价值？

---

# 2. From Workflow to Product

今天最重要的理解之一：

```text
Workflow Design
≠
Product Design
```

Workflow 更关注：

```text
Trigger
Input
Process
Output
Dependency
State
```

PRD 更关注：

```text
User
Problem
Scenario
Feature
Interaction
Acceptance Criteria
Scope
Quality
Success
```

例如后台可能存在：

```text
Task C
Task D
Task F
Task G
```

但律师不应该在 Weekly Report 里看到：

```text
Task C Results
Task D Results
Task F Results
Task G Results
```

而应该看到：

```text
本周发现了什么？
↓
用户在关注什么？
↓
为什么值得关注？
↓
有哪些 Evidence？
↓
可以形成什么选题？
↓
我要不要采用？
```

因此学到：

> System Architecture ≠ Information Architecture.

后台如何运行，不代表前台就应该按照同样结构展示。

---

# 3. Product Usage Rhythm

重新明确整个产品的用户使用节奏：

```text
Daily
=
Collection + Triage

7-Day Tracking
=
New Evidence + Re-evaluation

Weekly
=
Research Consumption + Topic Decision

Monthly
=
Search Strategy Calibration
```

这是整个产品非常重要的节奏设计。

---

# 4. Daily Review

Daily 的目的不是每天完成 Deep Analysis。

每天系统负责：

```text
Search
↓
Collection
↓
Normalization
↓
AI Basic Analysis
↓
Topic Classification
↓
Feishu Delivery
```

律师只负责：

```text
哪些值得留下？
哪些值得继续追踪？
哪些值得深入研究？
```

Topic Category：

```text
AI Classification
```

不要求律师人工分类。

---

# 5. Progressive Disclosure

今天学习并实际使用了：

```text
Progressive Disclosure
```

律师审核 Candidate 时不一次展示所有操作。

第一层：

```text
Keep?
├── Reject
└── Keep
```

只有 Keep 后才出现：

```text
Track?
Deep Analysis?
```

只有 Deep Analysis = Yes 后才出现：

```text
Comment Analysis?
```

这样可以降低律师每天 Review 的认知负担。

核心原则：

> Only ask the user for a decision when that decision becomes relevant.

---

# 6. Priority Pool vs Deep Analysis

进一步明确：

```text
Keep = Yes
↓
Priority Pool
```

但：

```text
Priority Pool
≠
Deep Analysis Pool
```

因此可以存在：

```text
Keep = Yes
Track = Yes
Deep Analysis = No
```

Deep Analysis Post 一定属于 Priority Pool。

但 Priority Pool Post 不一定需要 Deep Analysis。

---

# 7. Tracking as New Evidence

Tracking 的作用不是：

> 自动判断帖子是否值得 Deep Analysis。

而是：

```text
Day 0 Evidence
↓
Observation Window
↓
Day 7 Evidence
↓
Growth
↓
New Evidence
↓
Human Re-evaluation
```

因此允许：

```text
Day 0:
Deep Analysis = No

Day 7:
Deep Analysis = Yes
```

同时必须保存两次 Decision。

学到：

> Decision History should not be overwritten by Current State.

---

# 8. Deep Analysis

Deep Analysis 最终输出不是普通 Summary。

它生成：

```text
ResearchSubject
```

ResearchSubject 至少包括：

```text
Core Topic

User Problem

Legal / Business Issues

User Expressions

Content Opportunities

Post Evidence

Optional Comment Findings

Optional Comment Evidence
```

它是后续：

```text
Long-tail Discovery
Case Matching
Topic Generation
```

的核心 Research Object。

---

# 9. Comment Analysis

Comment Analysis 不需要每天执行。

也不是所有 Deep Analysis Post 都自动执行。

流程：

```text
Deep Analysis Approved
↓
Lawyer decides:
Comment Analysis?
```

如果 Yes：

```text
High-like
+
High Relevance
↓
Top 10
```

不足时：

```text
Latest Comments
↓
Fallback
```

Comment Analysis 的价值主要是：

- 发现原帖没有覆盖的问题；
- 提取真实用户语言；
- 发现评论区延伸需求；
- 为 Long-tail Discovery 提供 Evidence。

---

# 10. Evidence-backed Candidate Topic

Candidate Topic 不应该只是：

```text
AI Idea
```

而应该是：

```text
ResearchSubject
+
Available Supporting Evidence
↓
Candidate Topic
```

Required Evidence：

```text
ResearchSubject
```

Optional Evidence：

```text
Tracking
Long-tail
Comments
Case Match
Search Evidence
```

因此：

```text
No Case Match
```

不能阻止 Topic Generation。

学到：

> Optional evidence can strengthen a recommendation without becoming a hard dependency.

---

# 11. Weekly Research Package

Weekly 不按照后台 Task 展示。

用户看到：

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

每个 Candidate Topic 至少应该能够回答：

```text
是什么选题？

为什么推荐？

用户怎么讨论？

有什么趋势 Evidence？

有没有案例 Evidence？

来源是什么？
```

律师最后：

```text
Approve / Reject
```

Optional：

```text
1–5 Topic Rating
```

Rating 不阻塞 Approval。

---

# 12. Monthly Keyword Calibration

Monthly 的目标不是：

> AI 每月自动生成更多关键词。

而是：

> 根据过去一个月真实 Workflow Outcome 调整 Search Strategy。

形成：

```text
Keyword
↓
SearchHit
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

再反向分析 Keyword 是否真正创造价值。

重要认识：

```text
Search Volume
≠
Search Value
```

因此不能只看一个 Keyword 搜到了多少内容。

---

# 13. Long-tail Keyword Lifecycle

Long-tail Keyword 来自真实用户表达：

```text
User Expression
↓
Normalization
↓
Repeated Evidence
↓
LongTailCandidate
↓
Monthly Review
↓
Lawyer Approval
↓
Trial / Observe
↓
Real Search
↓
Performance Evidence
↓
Future Calibration
```

AI 发现关键词：

```text
≠
自动加入 Production Search
```

这是一个：

```text
Hypothesis
↓
Experiment
↓
Evidence
↓
Decision
```

闭环。

---

# 14. MVP Scope

今天正式区分：

```text
Product Vision
MVP Scope
Out of Scope
```

MVP 的核心目标不是实现所有可能功能。

而是验证：

1. 自动搜索 + AI 初筛是否减少人工搜索；
2. HITL 是否能够有效筛出高价值内容；
3. Research Pipeline 是否能够产生有价值的 Candidate Topics；
4. Feedback Loop 是否能够改善未来 Search Strategy。

---

# 15. Feature Creep

学习了：

```text
Feature Creep
```

例如：

```text
有选题
↓
顺便自动写脚本
↓
顺便自动生成封面
↓
顺便自动生成视频
↓
顺便自动发布
↓
顺便做Analytics
```

最终会让 MVP 无限扩张。

正确处理：

```text
New Idea
↓
Does MVP need it?
├── Yes → Scope
└── No → Backlog
```

不是否定未来功能，而是不让未来功能破坏当前验证目标。

---

# 16. MoSCoW Priority

今天使用：

```text
Must Have
Should Have
Could Have
Won't Have
```

对 MVP Feature 进行优先级管理。

核心研究闭环属于：

```text
Must Have
```

例如：

- Collection
- AI Basic Analysis
- Human Review
- Tracking
- Deep Analysis
- ResearchSubject
- Long-tail Discovery
- Case Matching
- Topic Generation
- Weekly Review
- Monthly Calibration
- Persistence
- Cloud Runtime

而：

```text
Independent Web App
Mobile App
Automatic Publishing
Complex Ranking
Fine-tuning
```

不属于 MVP。

---

# 17. Requirement ≠ Implementation

今天进一步明确：

```text
Product Requirement
≠
Technology Choice
```

例如产品需求是：

> 根据 ResearchSubject 找到相关案例。

不能直接写：

```text
Must use RAG
```

应该在 Architecture 阶段比较：

```text
SQL
Full-text Search
Embedding
Vector Search
Hybrid Retrieval
RAG
```

再决定。

同样：

```text
Need AI Automation
≠
Need Agent
```

如果流程本身是确定性的：

```text
Trigger
↓
Input
↓
Rule
↓
Output
```

普通 Workflow Automation 可能比 Autonomous Agent 更合适。

技术应该由业务问题触发，而不是为了学习某项技术强行寻找使用场景。

---

# 18. Non-functional Requirements

今天正式学习：

```text
Functional Requirement
vs
Non-functional Requirement
```

Functional Requirement：

> 系统做什么？

Non-functional Requirement：

> 系统做到什么质量才算真正可使用？

本项目重点 NFR：

```text
Reliability
Idempotency
Traceability
AI Reliability
Observability
Persistence
Cloud Availability
Security
Maintainability
Cost Awareness
```

---

# 19. Reliability

单个 Item Failure：

```text
不得让整个 Batch Failure
```

例如：

```text
4 Keywords

3 Success
1 Failure
```

应该：

```text
Partial Success
```

成功数据继续保存。

关键失败支持 Retry。

---

# 20. Idempotency

学习了：

```text
Idempotency
```

含义：

> 同一个操作意外执行多次，不应该产生重复业务副作用。

例如 Feishu Webhook 重复发送：

```text
Keep
Keep
```

不能因此创建：

```text
2 Tracking States
2 Deep Analysis Requests
```

主要需要保护：

```text
Post
SearchHit
LawyerDecision
TrackingState
DeepAnalysisRequest
Delivery
```

---

# 21. Traceability

本产品的重要质量要求：

```text
CandidateTopic
↓
ResearchSubject
↓
Post / Comment / Case
↓
Original Source
```

律师应该能够回答：

> 为什么系统推荐这个选题？

而不是只能看到 AI 给出的结论。

---

# 22. Structured AI Output

AI Output 如果需要被下游 Workflow 使用：

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

不能：

```text
LLM Output
↓
Directly Trust
↓
Downstream
```

否则一个 AI JSON Error 可能导致后续多个 Workflow Failure。

---

# 23. AI Provenance

核心 AI Output 应保留：

```text
model
prompt_version
generated_at
validation_status
```

这样以后可以：

```text
Prompt Version A
vs
Prompt Version B
```

结合真实 Human Feedback 做 Evaluation。

---

# 24. Observability

Cloud Workflow 运行后，用户不会每天查看后台。

系统至少需要回答：

```text
今天跑了吗？

处理了多少？

成功多少？

失败多少？

哪里失败？

今天的数据完整吗？
```

因此需要：

```text
WorkflowRun
```

以及：

```text
success
partial_success
failed
```

等状态。

---

# 25. Persistence

Feishu 是：

```text
Human Interaction Layer
```

不是：

```text
System of Record
```

核心业务数据必须进入 Persistent Backend Storage。

例如：

```text
Post
EngagementObservation
LawyerDecision
ResearchSubject
CandidateTopic
KeywordHistory
```

---

# 26. Success Metrics

今天正式区分四类 Metrics：

```text
System Metrics

Workflow / Product Metrics

AI Quality Proxies

Business Value Metrics
```

---

# 27. Primary Success Metrics

MVP Primary Metrics：

## Lawyer Keep Rate

```text
Kept Candidate Posts
────────────────────
Reviewed Candidate Posts
```

衡量 Daily Candidate Selection 的实际有用程度。

## Topic Approval Rate

```text
Approved Topics
───────────────
Reviewed Candidate Topics
```

衡量 Candidate Topic 的实际有用程度。

## Approved Topics per Week

衡量系统是否能够稳定提供足够数量的可用选题。

## Manual Research Time

比较：

```text
Before MVP
vs
After MVP
```

衡量 Automation 是否真正减少律师重复劳动。

---

# 28. Proxy ≠ Accuracy

一个重要认识：

```text
Lawyer Keep Rate
```

可以作为 AI Candidate Selection 的：

```text
Human Acceptance / Usefulness Proxy
```

但不能直接称为：

```text
AI Accuracy
```

因为律师 Reject 可能代表：

> 内容相关，但当前没有研究价值。

而不是：

> AI 判断错误。

---

# 29. Avoid Fake Precision

在没有真实 Baseline 时，不应该随便写：

```text
Keep Rate ≥ 60%

Topic Approval ≥ 50%

Time Saved ≥ 70%
```

正确方式：

```text
MVP Real-world Run
↓
2–4 Weeks
↓
Establish Baseline
↓
Observe Distribution
↓
Set Initial Target
```

学到：

> Do not manufacture precise KPIs before real usage data exists.

---

# 30. Logical Data Contract Update

今天 PRD 定稿后，再次 Cross-check Data Contract。

最终明确核心对象：

```text
Keyword
SearchHit
Post
BasicAnalysis
EngagementObservation
LawyerDecision
TrackingState
DeepAnalysisRequest
SelectedComment
ResearchSubject
LongTailCandidate
CaseRecord
CaseMatch
CandidateTopic
TopicFeedback
KeywordHistory
WorkflowRun
DeliveryRecord
```

重要关系：

```text
Post ≠ SearchHit

Decision ≠ Current State

Observation ≠ TrackingState

ResearchSubject ≠ CandidateTopic

LongTailCandidate ≠ Keyword

CaseRecord ≠ CaseMatch

Feishu Message ≠ Business Data

Valid Empty ≠ Error

Pending ≠ Reject
```

---

# 31. Existing Case Library

当前已有：

```text
Judgment Documents
↓
Codex
↓
Structured Extraction
↓
Unified Excel Case Library
```

未来系统需要：

```text
ResearchSubject
↓
Case Retrieval
↓
CaseMatch
```

但今天没有提前决定：

```text
RAG
Vector DB
SQL
Full-text
```

下一阶段必须先：

```text
Inspect Existing Excel
↓
Understand Real Schema
↓
Understand Case Volume
↓
Understand Retrieval Requirement
↓
Choose Technology
```

---

# 32. Three Core Design Documents

当前项目已经完成三个重要设计层：

```text
workflow-analysis.md
```

回答：

> Workflow 如何运作？

```text
data-contract.md
```

回答：

> Workflow 之间的数据如何保持一致？

```text
prd.md
```

回答：

> 从用户和产品角度，系统到底应该提供什么？

三者关系：

```text
Business Problem
↓
Workflow Analysis
↓
Data Contract
↓
Product Requirements
↓
System Architecture
↓
Implementation
```

它们互相关联，但不应该互相替代。

---

# 33. Current Product Loop

最终形成两个核心 Loop。

## Content Research Loop

```text
Search
↓
Candidate
↓
Lawyer Triage
↓
Priority Pool
↓
Tracking / Deep Analysis
↓
ResearchSubject
↓
Evidence
↓
Candidate Topic
↓
Lawyer Approval
```

## Search Optimization Loop

```text
Keyword
↓
Search
↓
Real Content
↓
Human Decision
↓
Research Outcome
↓
Approved Topic
↓
Monthly Calibration
↓
Keyword Lifecycle

+

User Expression
↓
LongTailCandidate
↓
Lawyer Approval
↓
Trial Keyword
↓
Real Search
↓
Performance Evidence
↓
Calibration
```

---

# 34. Key Concepts Learned

Day 09 重点概念：

```text
PRD

User Story

Acceptance Criteria

Progressive Disclosure

Human-in-the-loop

Evidence-backed Recommendation

Required vs Optional Evidence

MVP Scope

Out of Scope

Feature Creep

MoSCoW

Functional Requirement

Non-functional Requirement

Reliability

Partial Success

Retry

Idempotency

Traceability

Structured Output

Schema Validation

AI Provenance

Observability

System of Record

Success Metrics

Proxy Metric

Baseline

Fake Precision

Technology-neutral Requirement
```

---

# 35. Current Project Status

```text
Business Problem Analysis       ✓

Trigger Analysis                ✓

Input Analysis                  ✓

Process Analysis                ✓

Cross-workflow Input Review     ✓

Data Contract Review            ✓

Workflow Finalization           ✓

PRD                             ✓

MVP Scope                       ✓

Acceptance Criteria             ✓

Non-functional Requirements     ✓

Success Metrics                 ✓

Data Contract Finalization      ✓

System Architecture             NEXT
```

---

# 36. Next Step — Day 10

下一阶段：

```text
System Architecture
```

核心问题将从：

```text
What should the product do?
```

切换成：

```text
How should the system be structured?
```

需要回答：

```text
Where does n8n run?

Where does the database run?

How does TikHub connect?

How does Feishu connect?

How are Human Decisions written back?

Which tasks use LLM?

Which tasks use deterministic rules?

Which tasks need Python?

How is the existing Excel case library moved online?

Does Case Retrieval need Embeddings / RAG?

How are Retry and Idempotency implemented?

How are Secrets managed?

How do we deploy without relying on the local PC?
```

之后进入：

```text
Technology Mapping
↓
Vertical Slice Plan
↓
Implementation
```

---

# 37. Day 09 Reflection

今天最大的变化不是又增加了多少 Workflow。

而是开始真正把：

```text
Automation Workflow
```

当成：

```text
Product
```

进行设计。

以前更关注：

> 能不能自动跑？

现在需要同时考虑：

```text
用户是否愿意使用？

什么时候应该让用户做决定？

哪些事情应该交给 AI？

哪些事情必须保留 Human Judgment？

AI 输出是否有 Evidence？

失败后系统怎么办？

重复执行怎么办？

数据是否可以追溯？

产品有没有真正减少人工工作？

如何通过真实 Feedback 继续优化？
```

最终形成的设计原则：

> Build useful automation, not maximum automation.

技术不是目标。

真正的目标是：

```text
减少重复工作
+
保留专业判断
+
结构化研究数据
+
保留来源证据
+
用真实反馈持续优化系统
```