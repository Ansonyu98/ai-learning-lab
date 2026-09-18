# Product Requirements Document (PRD)

## AI-powered Legal Content Research & Topic Discovery Workflow

**Project:** Legal Content Automation  
**Document Type:** Product Requirements Document  
**Stage:** MVP v1  
**Status:** Approved for Architecture Design

---

# 1. Product Overview

Legal Content Automation 是一个面向律师内容研究场景的 AI + Workflow Automation 系统。

系统通过：

- 社交媒体内容自动采集
- AI 基础分析与话题归类
- 律师 Human-in-the-loop 审核
- 高价值内容追踪
- AI Deep Analysis
- 评论研究
- 长尾关键词发现
- 案例库匹配
- Evidence-backed Topic Generation
- Weekly Research Review
- Monthly Keyword Calibration

减少律师在：

- 搜索
- 筛选
- 整理
- 追踪
- 阅读
- 研究
- 选题

过程中的重复劳动。

系统不以完全替代律师专业判断为目标。

核心设计原则：

> Automate repetitive research work while keeping professional and business-value decisions under lawyer control.

---

# 2. Product Goal

MVP 的核心目标是：

> 建立一套可以在云端持续自动运行的法律内容研究与选题 Workflow，通过自动采集、AI 分析、律师审核和持续反馈，将分散的社交媒体内容转化为具有来源证据的研究对象和候选选题。

MVP 重点验证：

1. 自动搜索 + AI 初筛能否减少律师人工搜索时间；
2. Daily Human Review 能否低成本筛出真正值得保留的内容；
3. Deep Analysis、Long-tail Discovery 与 Case Evidence 能否提高 Candidate Topic 的实际价值；
4. Monthly Feedback Loop 能否逐步改善 Search Strategy。

---

# 3. Target User

## MVP User

```text
Lawyer
/
Legal Content Creator
```

MVP 当前采用：

```text
Single-user Design
```

暂不处理：

- 多律师账号
- 多组织
- 权限管理
- SaaS 用户体系

---

# 4. User Problem

当前律师进行社交媒体内容研究时，需要人工完成：

```text
搜索关键词
↓
浏览大量帖子
↓
判断相关性
↓
查看互动数据
↓
筛选值得关注的帖子
↓
后续重新搜索 / 追踪
↓
阅读正文和评论
↓
提取用户问题
↓
发现用户真实表达
↓
寻找相关案例
↓
整理内容方向
↓
形成选题
```

主要问题包括：

- 搜索工作重复；
- 大量低价值信息占用时间；
- 不同关键词之间容易重复发现相同帖子；
- 热门帖子需要人工持续追踪；
- 评论区用户问题难以系统积累；
- 用户语言与律师专业语言存在差异；
- 案例库与内容研究没有形成自动联动；
- 内容研究过程缺少可持续的数据反馈闭环。

---

# 5. Product Principles

## 5.1 Human-in-the-loop

系统负责：

```text
Collection
Classification
Summarization
Analysis
Evidence Organization
Recommendation
```

律师负责：

```text
Professional Judgment
Business-value Judgment
Research Approval
Topic Approval
Keyword Lifecycle Decision
```

---

## 5.2 AI Recommendation ≠ Human Decision

例如：

```text
AI Relevance
Engagement Signal
Tracking Growth
Keyword Recommendation
Topic Recommendation
```

均属于：

```text
Evidence / Recommendation
```

不能自动替代律师最终判断。

---

## 5.3 Evidence-backed Output

重要 AI Output 应尽可能能够追溯：

```text
Candidate Topic
↓
ResearchSubject
↓
Post / Comment / Case Evidence
↓
Original Source
```

AI Summary 不作为 Source of Truth。

律师必须能够在需要时查看原始来源。

---

## 5.4 Daily Collection, Weekly Research, Monthly Optimization

产品使用节奏：

```text
Daily
=
Collection + Triage

7-Day
=
Tracking Evidence + Re-evaluation

Weekly
=
Research Consumption + Topic Decision

Monthly
=
Search Strategy Calibration
```

---

## 5.5 Cloud-first Automation

Scheduled Workflow 不应依赖用户个人电脑处于开机状态。

系统需要：

```text
Cloud Runtime
+
Online Persistent Storage
```

实现持续运行。

---

# 6. Product Workflow

MVP 主流程：

```text
Keyword Search
↓
Social Content Collection
↓
Normalization / Deduplication
↓
AI Basic Analysis
↓
Daily Feishu Review
↓
Lawyer Review
↓
Keep?
├── No → Preserve History → End
│
└── Yes → Priority Pool
          │
          ├── Track?
          │      ↓
          │   7-Day Tracking
          │      ↓
          │   Tracking Review
          │      ↓
          │   Optional Re-evaluation
          │
          └── Deep Analysis?
                 │
                 ├── No
                 │
                 └── Yes
                       ↓
                 Comment Analysis?
                  ├── No
                  └── Yes
                       ↓
                 ResearchSubject
                    │
             ┌──────┴──────┐
             ↓             ↓
       Long-tail       Case Matching
        Discovery
             \             /
              \           /
               ↓         ↓
              Topic Generation
                    ↓
             Weekly Research
                    ↓
             Lawyer Approval
                    ↓
            Approved Topic Pool

Research / Decision Data
          ↓
Monthly Keyword Calibration
          ↓
Continue / Reduce / Retire
+
Long-tail Trial Keywords
          ↓
Next Search Cycle
```

---

# 7. Feature 01 — Daily Candidate Review

## 7.1 Purpose

每天自动完成内容采集和基础整理，并通过 Feishu 提供给律师进行快速审核。

Daily Review 的目标不是完成深度研究。

目标是：

> 让律师快速了解今天收集了什么，并决定哪些内容值得留下和后续深入处理。

---

# 8. Daily Overview

律师打开 Daily Review 后，首先看到 Overview。

至少包括：

- 今日搜索关键词数量
- 今日收集帖子数量
- Candidate Posts 数量
- 今日主要 Topic Categories
- Workflow Completion Status

示例：

```text
今日法律内容研究

搜索关键词：
4

收集帖子：
18

Candidate Posts：
8

主要话题：

劳动争议 / 欠薪
劳动争议 / 调岗降薪
企业合规 / 年休假

采集状态：

4 / 4 Keywords Completed
```

Topic Category：

```text
由 AI 自动归类
```

不需要律师人工分类。

---

# 9. Candidate Card

每个 Candidate 至少展示：

- Post Title
- AI Summary
- Topic Category
- Current Engagement
- Published Time
- Source Keyword
- Source Link

其中：

```text
Source Link
↓
律师点击
↓
打开原始帖子
```

律师必须能够随时进行 Original Source Review。

---

# 10. Candidate Ranking

MVP 不建立复杂综合评分。

排序逻辑：

```text
AI Relevance Gate
↓
保留符合律师内容研究目标的 Candidate
↓
Current Engagement 优先
↓
Published Time 作为辅助信息
```

原则：

> Relevance determines whether a post should enter the candidate set; engagement helps prioritize review order.

MVP 不建立：

```text
Relevance × Engagement × Recency
```

的人工权重评分公式。

待真实运行积累 Baseline 后再评估。

---

# 11. Progressive Review

Candidate Review 采用 Progressive Disclosure。

第一层：

```text
Keep?
├── Reject
└── Keep
```

如果：

```text
Reject
```

本次 Review 结束。

如果：

```text
Keep
```

继续展示：

```text
Track?
Yes / No

Deep Analysis?
Yes / No
```

只有：

```text
Deep Analysis = Yes
```

才继续显示：

```text
Comment Analysis?
Yes / No
```

---

# 12. Priority Pool Rule

核心关系：

```text
Keep = Yes
↓
Priority Pool
```

因此：

```text
Deep Analysis Post
⊂
Priority Pool
```

但：

```text
Priority Pool
≠
All Deep Analysis
```

一篇帖子可以：

```text
Keep = Yes
Track = Yes
Deep Analysis = No
```

仍然属于 Priority Pool。

---

# 13. Daily Review Acceptance Criteria

### AC-D01

Daily Collection 完成后，系统生成 Daily Review。

### AC-D02

Daily Overview 至少展示：

- Search Keyword Count
- Collected Post Count
- Candidate Count
- AI Topic Overview
- Workflow Completion Status

### AC-D03

每个 Candidate 至少展示：

- Title
- Summary
- Topic Category
- Engagement
- Published Time
- Source Keyword
- Source Link

### AC-D04

Source Link 必须允许律师访问原始帖子进行人工 Review。

### AC-D05

律师首先只能看到：

```text
Keep / Reject
```

### AC-D06

Reject 后：

- 保存 Reject Decision；
- 不进入 Priority Pool；
- 不要求 Track；
- 不要求 Deep Analysis；
- 不要求 Comment Analysis。

### AC-D07

Reject 不删除：

- Post
- Search Evidence
- BasicAnalysis
- LawyerDecision

### AC-D08

Keep 后：

```text
Post → Priority Pool
```

并显示：

```text
Track?
Deep Analysis?
```

### AC-D09

Deep Analysis = No 时：

不得要求 Comment Analysis Decision。

### AC-D10

Deep Analysis = Yes 时：

系统询问：

```text
Comment Analysis?
Yes / No
```

### AC-D11

律师当天未处理：

```text
Review Status = Pending
```

不得自动视为 Reject。

### AC-D12

所有实际提交的 Lawyer Decisions 必须 Persist。

---

# 14. Feature 02 — 7-Day Tracking Review

## Purpose

对律师选择 Track 的 Priority Post，在观察期后重新采集 Engagement Data，并形成新的 Evidence。

Tracking 的目的不是自动决定：

```text
Deep Analysis
```

而是：

> 给律师提供新的趋势证据，以便重新判断。

---

# 15. Tracking Review

至少展示：

- Post Title
- Topic Category
- Source Link
- Day 0 Engagement
- Day 7 Engagement
- Absolute Growth
- Growth Rate
- Previous Lawyer Decision
- Current Research State

示例：

```text
Day 0
Engagement: 616

Day 7
Engagement: 1363

Growth:
+747

Growth Rate:
+121.3%
```

---

# 16. Re-evaluation

如果：

```text
Day 0
Deep Analysis = No
```

Tracking 后：

```text
New Evidence
↓
Lawyer Re-evaluation
↓
Deep Analysis?
Yes / No
```

允许：

```text
No → Yes
```

新的 Decision 必须新增保存。

不能覆盖旧 Decision。

---

# 17. State-aware Tracking UX

如果 Post 已经：

```text
Deep Analysis Approved
or
Deep Analysis Completed
```

Tracking Review：

只展示 Tracking Evidence。

不重复要求律师审批 Deep Analysis。

---

# 18. Tracking Acceptance Criteria

### AC-T01

只有：

```text
Track = Yes
```

的 Post 才创建 Tracking State。

### AC-T02

系统保留：

```text
Day 0 Observation
+
Day 7 Observation
```

不得覆盖历史数据。

### AC-T03

Tracking Review 展示：

- Initial Engagement
- Latest Engagement
- Absolute Growth
- Growth Rate
- Previous Decision

### AC-T04

Deep Analysis 尚未批准时：

允许律师重新审批。

### AC-T05

Deep Analysis 已批准或完成时：

不得重复要求相同审批。

### AC-T06

所有 Re-evaluation Decision 保留历史。

---

# 19. Feature 03 — Deep Analysis

## Purpose

Deep Analysis 不负责重复生成 Post Summary。

目标是将：

```text
High-value Post
```

转换为：

```text
Reusable Structured Research Object
```

即：

```text
ResearchSubject
```

供：

- Long-tail Discovery
- Case Matching
- Topic Generation

使用。

---

# 20. Deep Analysis Output

ResearchSubject 至少包含：

```text
Core Topic

User Problem

Legal / Business Issues

User Expressions

Content Opportunities

Source Evidence
```

---

# 21. Core Topic

回答：

> 该 ResearchSubject 核心讨论什么问题？

例如：

```text
劳动争议 / 欠薪 / 被迫解除
```

---

# 22. User Problem

描述真实用户正在解决的问题，而不仅仅是法律分类。

例如：

```text
劳动者长期被拖欠工资，
产生离职意愿，
但不确定是否已经具备被迫解除条件，
以及解除后是否可能主张经济补偿。
```

---

# 23. Legal / Business Issues

AI 识别：

> 值得律师进一步研究的问题。

例如：

```text
拖欠工资与被迫解除的关系

解除时间节点

证据固定

解除通知

经济补偿请求条件
```

原则：

```text
Issue Identification
≠
Final Legal Opinion
```

---

# 24. User Expressions

系统尽可能保留真实用户语言。

例如：

```text
“公司一直拖工资”

“我可以直接走被迫吗”

“公司让我自己提离职”

“调岗不同意算旷工吗”
```

User Expression 是：

- Long-tail Discovery
- Search Strategy
- Content Language
- Topic Generation

的重要 Research Asset。

---

# 25. Content Opportunities

识别：

- 高频疑问
- 用户误区
- 行动需求
- 潜在争议点
- 可拆分子问题
- 内容研究方向

但：

```text
Content Opportunity
≠
Final Candidate Topic
```

Candidate Topic 由后续 Topic Generation 形成。

---

# 26. Comment Analysis

Comment Analysis 是：

```text
Optional Deep Analysis Component
```

只有：

```text
Deep Analysis = Yes
+
Lawyer Comment Analysis = Yes
```

才执行。

---

# 27. Comment Selection

优先：

```text
High-like
+
Strong Relevance
↓
Top 10
```

如果无法获得足够符合条件的评论：

```text
Fallback
↓
Latest 10
```

---

# 28. Post vs Comment Evidence

系统应区分：

```text
Post-derived Findings
```

和：

```text
Comment-derived Findings
```

例如：

```text
Original Post Problem

vs

Comment-section Extended Questions
```

避免将不同来源的用户问题混为同一 Evidence。

---

# 29. Deep Analysis Delivery

Deep Analysis 完成后：

```text
Persist ResearchSubject
```

但：

```text
不立即单独推送律师
```

后台可以继续：

```text
Task D
Task F
Task G
```

研究成果集中进入：

```text
Weekly Research Package
```

---

# 30. Deep Analysis Acceptance Criteria

### AC-A01

只有：

```text
Priority Pool
+
Deep Analysis Approved = Yes
```

才能进入 Deep Analysis。

### AC-A02

ResearchSubject 至少包含：

- Core Topic
- User Problem
- Legal / Business Issues
- User Expressions
- Content Opportunities
- Source Evidence

### AC-A03

Comment Analysis = No：

不得阻塞 Deep Analysis。

### AC-A04

Comment Analysis = Yes：

按照 Comment Selection Rule 获取分析输入。

### AC-A05

Post Findings 与 Comment Findings 应可区分。

### AC-A06

进入 Downstream Workflow 的 AI Output 必须通过 Structured Output Validation。

### AC-A07

Deep Analysis Failure 不得删除上游数据。

### AC-A08

ResearchSubject 必须能够追溯 Source Post。

如果使用 Comments：

必须能够追溯 Selected Comments。

---

# 31. Feature 04 — Weekly Research & Candidate Topic Review

## Purpose

Weekly Package 不按照后台 Task C / D / F / G 分别展示。

它按照律师的 Research Decision Journey 组织：

```text
这一周发现了什么？
↓
用户在关注什么？
↓
哪些问题值得研究？
↓
有哪些 Evidence？
↓
可以形成哪些 Candidate Topics？
↓
律师采用哪些？
```

---

# 32. Weekly Overview

至少展示：

- Research Period
- Collected Posts
- Priority Posts
- Completed Tracking
- Deep Analysis Count
- Main Topics
- ResearchSubject Count
- Long-tail Candidate Count
- Case Match Count
- Candidate Topic Count

---

# 33. Key Research Findings

Weekly Package 提供简短：

```text
Key Research Findings
```

例如：

```text
本周用户对欠薪内容的关注，
集中在“拖多久才能被迫解除”。

调岗讨论从“能不能拒绝”
延伸到“拒绝后被要求自离怎么办”。

年休假讨论中，
“公司统一安排休年假”
出现较多争议。
```

目的：

> 帮助律师快速建立本周用户讨论地图。

不生成冗长 AI Report。

---

# 34. Evidence-backed Candidate Topic

Candidate Topic 不应只是 AI 灵感。

每个 Topic 应尽可能展示：

```text
Topic / Title

Suggested Angle

Recommendation Rationale

Available Research Evidence

User Expressions

Tracking Evidence

Case Evidence

Source Links
```

---

# 35. Required vs Optional Evidence

Candidate Topic Generation：

Required：

```text
ResearchSubject
```

Optional：

```text
TrackingEvidence
LongTailCandidate
SelectedComment
CaseMatch
SearchHit
```

因此：

```text
No CaseMatch
```

不能阻塞 Topic Generation。

---

# 36. Case Evidence

Case Match 是：

```text
Supporting Evidence
```

不是 Weekly Package 独立主角。

案例优先依附：

```text
Research Finding
or
Candidate Topic
```

展示。

---

# 37. Long-tail Evidence

Weekly 可以展示：

```text
本周新出现的用户表达
```

但不要求律师每周审批 Long-tail Keyword。

正式 Keyword Promotion：

放到 Monthly Calibration。

---

# 38. Topic Ranking

MVP 不建立单一 Topic Quality Score。

展示顺序可参考：

```text
Evidence Sufficiency
+
Research Relevance
+
Available Engagement / Tracking Signals
```

但：

```text
AI Recommendation Order
≠
Final Topic Ranking
```

最终是否采用由律师决定。

---

# 39. Topic Decision

每个 Candidate Topic：

```text
[采用]
[不采用]
```

采用：

```text
Approved Topic Pool
```

不采用：

保存：

```text
CandidateTopic
+
LawyerDecision
```

不得删除历史。

---

# 40. Optional Topic Rating

律师可以选择：

```text
1–5
```

评价 Topic Value。

Rating：

```text
Optional
```

不得阻塞 Topic Approval。

MVP 暂不增加：

```text
Save for Learning
```

如果真实使用中出现稳定需求，再进入 Backlog。

---

# 41. Weekly Acceptance Criteria

### AC-W01

Weekly Package 至少包含：

- Weekly Overview
- Key Research Findings
- Candidate Topics

### AC-W02

Candidate Topic 至少展示：

- Topic
- Suggested Angle
- Rationale
- Available Evidence
- Source Review Access

### AC-W03

ResearchSubject 是 Required Evidence。

其他 Evidence 均可 Optional。

### AC-W04

No CaseMatch 不阻塞 Topic Generation。

### AC-W05

律师能够：

```text
Approve / Reject
```

Candidate Topic。

### AC-W06

Approved Topic 进入 Approved Topic Pool。

### AC-W07

Rejected Topic 保留历史。

### AC-W08

Topic 必须能够追溯相关 Research Evidence。

### AC-W09

1–5 Rating 为 Optional Feedback。

---

# 42. Feature 05 — Monthly Keyword Calibration

## Purpose

利用过去一个月真实 Workflow Data：

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

评估 Keyword 的实际研究价值。

目标：

> Continuously improve Search Strategy based on real outcomes.

---

# 43. Monthly Overview

至少展示：

- Active Keywords
- Search Hits
- Candidate Posts
- Priority Posts
- Deep Analysis
- Approved Topics
- Long-tail Candidates
- Suggested Continue
- Suggested Reduce
- Suggested Retire
- Suggested Trial Keywords

---

# 44. Existing Keyword Evidence

每个 Keyword 至少可以查看：

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

原则：

```text
Volume ≠ Value
```

MVP 不通过单一比例直接判断 Keyword Quality。

---

# 45. Keyword Recommendation

系统可以推荐：

```text
Continue
Reduce
Retire
```

并提供 Recommendation Reason。

但：

```text
System Recommendation
≠
Keyword Lifecycle Decision
```

最终由律师审批。

---

# 46. Keyword Lifecycle

用户层：

```text
Continue
Reduce
Retire
```

后台可映射：

```text
Continue → Active

Reduce → Reduced

Retire → Retired
```

新 Long-tail Keyword：

```text
Observe / Trial
```

---

# 47. Long-tail Promotion

Long-tail Candidate 来自：

```text
Real User Expression
↓
Normalization
↓
Repeated Evidence
↓
Long-tail Candidate
```

Monthly Review 至少展示：

- Normalized Candidate
- Occurrence Count
- Source Post Count
- Related Topics
- Raw User Expressions
- Source Evidence

---

# 48. Trial Keyword

Long-tail Candidate：

```text
Lawyer Approve
↓
Trial / Observe Keyword
↓
Next Search Cycle
↓
Real Performance Evidence
↓
Future Calibration
```

因此：

```text
AI-generated Keyword
≠
Automatically Active Keyword
```

---

# 49. Monthly Acceptance Criteria

### AC-M01

Monthly Calibration 展示整体 Search Performance。

### AC-M02

每个 Existing Keyword 提供真实 Workflow Evidence。

### AC-M03

系统可以生成 Continue / Reduce / Retire Recommendation。

### AC-M04

所有 Keyword Lifecycle Change 必须经过律师审批。

### AC-M05

Keyword State Change 必须保留 KeywordHistory。

### AC-M06

Long-tail Candidate 必须能够追溯 Raw User Expression 和 Source Evidence。

### AC-M07

Long-tail Candidate 不得自动进入 Production Search。

### AC-M08

Approved Long-tail Keyword 首先进入 Trial / Observe。

### AC-M09

Rejected Long-tail Candidate 保留历史。

### AC-M10

MVP 不强制生成单一 Keyword Quality Score。

---

# 50. Case Library Integration Requirement

当前已有案例库流程：

```text
Judgment Documents
↓
Codex
↓
Structured Extraction
↓
Unified Excel Case Library
```

MVP 要求：

```text
ResearchSubject
↓
Case Retrieval / Matching
↓
CaseMatch
↓
Weekly Topic Evidence
```

当前 PRD 只定义：

> 系统必须能够根据 ResearchSubject 检索和匹配相关案例。

暂不规定：

```text
SQL Search
Full-text Search
Embedding
Vector Search
Hybrid Search
RAG
```

具体技术方案：

在 Architecture / Technology Mapping 阶段根据现有 Excel Schema 和真实 Case Data 决定。

---

# 51. Feishu Product Boundary

Feishu 是：

```text
Human Workspace
+
Review Interface
+
Delivery Channel
```

包括：

```text
Daily Review
Tracking Review
Weekly Research
Monthly Calibration
Human Decisions
```

Feishu 不是：

```text
System of Record
```

所有关键 Decision 必须：

```text
Feishu Action
↓
Event / Webhook
↓
Validation
↓
Persistence
↓
Business State Update
↓
Downstream Workflow
```

---

# 52. Functional Requirements Summary

MVP 必须支持：

1. Keyword-based Social Content Collection
2. Post Normalization
3. Post Deduplication
4. Engagement Collection
5. AI Basic Analysis
6. AI Topic Classification
7. Daily Feishu Overview
8. Candidate Source Review
9. Lawyer Progressive Review
10. Priority Pool
11. 7-Day Tracking
12. Tracking Re-evaluation
13. Deep Analysis
14. Optional Comment Analysis
15. Structured ResearchSubject
16. Long-tail Discovery
17. Case Matching
18. Candidate Topic Generation
19. Weekly Research Package
20. Topic Approval
21. Optional Topic Rating
22. Monthly Keyword Calibration
23. Trial Keyword Lifecycle
24. Decision History
25. Workflow Run Logging
26. Error / Retry Handling
27. Cloud Scheduled Execution
28. Persistent Business Data

---

# 53. Error / Empty / Pending UX

系统必须区分：

```text
Technical Error
Data Error
Valid Empty Result
Pending Human Decision
```

---

## 53.1 Technical Error

例如：

- API Timeout
- Authentication Failure
- LLM Failure
- Database Failure
- Feishu Delivery Failure

系统：

```text
Log
↓
Retry where appropriate
↓
Preserve successful items
```

---

## 53.2 Data Error

例如：

- Missing Required Field
- Invalid Datetime
- Invalid JSON
- Structured Output Validation Failure

不得直接进入 Downstream Workflow。

---

## 53.3 Valid Empty Result

例如：

```text
No Relevant Case

No Valuable Comment

No Candidate Topic

No Eligible Tracking Post
```

属于正常业务结果。

不得显示为：

```text
System Failure
```

---

## 53.4 Pending Human Decision

如果律师未处理：

```text
Status = Pending
```

不得：

```text
Auto Reject
```

---

# 54. Non-functional Requirements

## 54.1 Reliability

单个 Item Failure：

不得阻塞整个 Batch。

成功结果继续 Persist。

关键失败支持 Retry / Recovery。

---

## 54.2 Idempotency

重复 Event / Workflow Execution：

不得产生重复业务副作用。

重点包括：

- Post
- LawyerDecision
- TrackingState
- DeepAnalysisRequest
- Delivery

---

## 54.3 Traceability

重要 AI Output 必须能够追溯 Source Evidence。

Candidate Topic 应尽可能支持：

```text
Topic
↓
ResearchSubject
↓
Post / Comment / Case
↓
Original Source
```

---

## 54.4 AI Reliability

进入 Downstream Workflow 的 AI Output：

```text
Structured Output
↓
Schema Validation
↓
Persist
```

Validation Failure：

进入 Retry / Error Handling。

---

## 54.5 AI Provenance

AI-generated Business Objects 原则上保留：

```text
model
prompt_version
generated_at
validation_status
```

---

## 54.6 Observability

每次 Workflow Run 至少记录：

- Workflow Name
- Start Time
- End Time
- Status
- Items Processed
- Success Count
- Failure Count
- Error Summary

Daily Overview 应允许律师知道：

> 当天数据是否完整采集。

---

## 54.7 Persistence

核心 Business Data 必须持久化。

包括：

- Post
- Search Evidence
- Engagement History
- Lawyer Decisions
- Tracking Evidence
- ResearchSubject
- Keyword History
- Candidate Topics

---

## 54.8 Cloud Availability

Scheduled Workflow：

```text
不得依赖个人电脑开机
```

---

## 54.9 Security

以下 Secrets：

- API Keys
- Database Credentials
- Feishu Credentials
- LLM Credentials

不得写入 Public GitHub Repository。

应使用：

```text
Environment Variables
/
Secret Management
```

---

## 54.10 Maintainability

系统应避免将所有逻辑放入一个巨大 Workflow。

Architecture 应考虑模块化：

```text
Collection
Analysis
Human Review
Tracking
Deep Research
Topic Generation
Keyword Calibration
Delivery
```

---

## 54.11 Cost Awareness

通过：

```text
Basic Analysis
↓
Human Filter
↓
Selective Deep Analysis
↓
Optional Comment Analysis
```

控制高成本 AI Processing。

MVP 不要求复杂 Cost Dashboard。

---

# 55. MVP Success Metrics

Success Metrics 分为：

```text
System Metrics
Product / Workflow Metrics
AI Quality Proxies
Business Value Metrics
```

---

# 56. Primary Metrics

## 56.1 Lawyer Keep Rate

```text
Kept Candidate Posts
────────────────────
Reviewed Candidate Posts
```

衡量：

> Daily Candidate Selection 对律师的实际有用程度。

---

## 56.2 Topic Approval Rate

```text
Approved Topics
───────────────
Reviewed Candidate Topics
```

衡量：

> Candidate Topic Recommendation 的实际有用程度。

---

## 56.3 Approved Topics per Week

衡量：

> 系统每周能够稳定产生多少律师实际愿意采用的选题。

---

## 56.4 Manual Research Time

比较：

```text
Before MVP
vs
After MVP
```

衡量：

> Automation 是否真正减少律师重复内容研究时间。

---

# 57. Supporting Metrics

包括：

- Workflow Success Rate
- Partial Failure Rate
- Candidate Rate
- Deep Analysis Rate
- Tracking Re-evaluation Rate
- Comment Analysis Usage Rate
- Optional Topic Rating
- Keyword → Approved Topic Conversion
- Long-tail Trial Performance
- Structured Output Failure Rate
- Feishu Delivery Success Rate

Supporting Metrics 主要用于：

> Diagnose why Primary Metrics change.

---

# 58. Evaluation Principle

MVP Phase 1：

```text
Establish Baseline
```

不提前人为设置：

```text
Keep Rate ≥ X%
Topic Approval ≥ X%
Time Saved ≥ X%
```

等缺乏真实数据支持的指标。

建议：

```text
Real-world Run
↓
2–4 Weeks Baseline
↓
Observe Distribution
↓
Set Initial Targets
↓
Iterate
```

原则：

> Avoid fake precision before real usage data exists.

---

# 59. MVP Scope — Must Have

MVP Must Have：

```text
Xiaohongshu Collection

Keyword Management

Post Deduplication

Engagement Observation

AI Basic Analysis

Daily Feishu Review

Source Link Review

Lawyer HITL

Priority Pool

7-Day Tracking

Tracking Re-evaluation

Deep Analysis

Optional Comment Analysis

ResearchSubject

Long-tail Discovery

Case Matching

Candidate Topic Generation

Weekly Research Package

Topic Approval

Monthly Keyword Calibration

Keyword History

Cloud Execution

Persistent Storage

Error Handling

Workflow Observability
```

---

# 60. Feature Priority — MoSCoW

## Must Have

直接构成 MVP Research Loop：

- Xiaohongshu Collection
- Post Deduplication
- AI Basic Analysis
- Daily Feishu Review
- Source Review
- Lawyer Keep / Reject
- Priority Pool
- Tracking
- Deep Analysis
- ResearchSubject
- Long-tail Discovery
- Case Matching
- Candidate Topic Generation
- Weekly Research Review
- Topic Approval
- Monthly Keyword Calibration
- Persistent Storage
- Cloud Runtime
- Error Handling
- Decision History

---

## Should Have

对 MVP Evaluation 和使用体验有较高价值，但必要时可稍后补：

- Optional Topic Rating
- Detailed Workflow Run Statistics
- Prompt Version Comparison
- Trial Keyword Performance Comparison
- Enhanced Research Evidence Navigation
- Cost Usage Statistics

---

## Could Have

真实使用验证需求后再决定：

- Save for Learning
- Advanced Ranking
- Custom Dashboard
- Topic Search / Filter
- ResearchSubject Search
- Advanced Keyword Analytics
- Automated Research Digest Customization

---

## Won't Have — MVP v1

MVP 明确不做：

- Douyin Integration
- WeChat Channels Integration
- Full Multi-platform Collection
- Automatic Full Script Generation
- Automatic Cover Generation
- Automatic Video Generation
- Automatic Social Publishing
- Published Content Performance Feedback
- Autonomous Keyword Lifecycle Decision
- Autonomous Topic Approval
- Complex Ranking Model
- Machine Learning Recommendation Model
- Fine-tuning
- Self-hosted LLM
- Forced Complex RAG Architecture
- Forced Agent Architecture
- Multi-user Permission System
- SaaS Billing
- Customer Registration
- Independent Web App
- Mobile App

---

# 61. Technology-neutral Requirements

PRD 不规定：

```text
必须使用 n8n

必须使用 PostgreSQL

必须使用 Supabase

必须使用 RAG

必须使用 Vector Database

必须使用 Agent

必须使用 Python
```

PRD 只定义：

> Product must do what.

Technology Mapping 再回答：

> How should it be implemented?

---

# 62. AI Technology Principle

技术必须由业务需求触发。

例如：

```text
Case Retrieval Requirement
↓
Evaluate:
SQL?
Full-text Search?
Embedding?
Hybrid Search?
RAG?
```

而不是：

```text
需要学习 RAG
↓
强行寻找一个地方使用 RAG
```

同样：

```text
Deterministic Workflow
```

优先使用：

```text
Workflow / Rule
```

只有真正需要：

```text
Dynamic Tool Selection
Dynamic Planning
Autonomous Multi-step Reasoning
```

时，再评估 Agent / Tool Calling。

---

# 63. MVP Product Feedback Loop

最终形成两个闭环。

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
Tracking / Research
↓
ResearchSubject
↓
Evidence
↓
Candidate Topic
↓
Lawyer Approval
```

---

## Search Optimization Loop

```text
Keyword
↓
Search
↓
Real Content
↓
Lawyer Decisions
↓
Research
↓
Approved Topics
↓
Monthly Calibration
↓
Keyword Lifecycle

+

User Expressions
↓
Long-tail Candidate
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

# 64. Architecture Handoff

PRD 完成后，下一阶段需要回答：

```text
Where does each component run?

Where is data stored?

How does Feishu communicate with backend?

How are scheduled workflows triggered?

How does TikHub connect?

How does the LLM connect?

How is the existing Excel case library migrated / synchronized?

Which components require n8n?

Which components require Python?

Which components use deterministic rules?

Which components use LLM?

Does Case Retrieval actually require RAG?

Does any workflow actually require Tool Calling / Agent?
```

这些属于：

```text
Architecture
+
Technology Mapping
```

而不是 PRD。

---

# 65. Implementation Principle

进入 Implementation 后，不一次搭完整系统。

采用：

```text
Vertical Slice
↓
Real Data
↓
Test
↓
Evaluate
↓
Expand
```

初步顺序：

```text
Slice 1
Schedule
→ TikHub
→ Real Post Data
→ Database

Slice 2
Database
→ AI Basic Analysis
→ Structured Output
→ Feishu Daily Review

Slice 3
Feishu Lawyer Decision
→ Webhook
→ Persistence
→ Business State

Slice 4
Tracking
→ Re-collection
→ Tracking Evidence
→ Re-evaluation

Slice 5
Deep Analysis
→ ResearchSubject
→ Long-tail Discovery

Slice 6
Case Integration
→ Case Retrieval
→ CaseMatch

Slice 7
Topic Generation
→ Weekly Research Package
→ Lawyer Approval

Slice 8
Monthly Calibration
→ Keyword Lifecycle
→ Trial Keywords
```

具体 Implementation Plan：

Architecture 完成后重新确认。

---

# 66. PRD Status

Current Product Design Status:

```text
Product Goal                  Defined
Target User                   Defined
User Problem                  Defined
Product Principles            Defined

Daily Candidate Review        Defined
Candidate Ranking             Defined
Progressive Review            Defined
Priority Pool                 Defined

7-Day Tracking                Defined
Re-evaluation                 Defined

Deep Analysis                 Defined
Comment Analysis              Defined
ResearchSubject               Defined

Weekly Research               Defined
Candidate Topic Review        Defined

Monthly Calibration           Defined
Long-tail Trial Loop          Defined

Case Integration Requirement  Defined

Feishu Product Boundary       Defined

Functional Requirements       Defined
Error / Empty / Pending UX    Defined
Non-functional Requirements   Defined

Success Metrics               Defined
MVP Scope                     Defined
MoSCoW Priority               Defined
Out of Scope                  Defined

Technology-neutral Boundary   Defined
Architecture Handoff          Defined
```

---

# 67. Next Stage

```text
Business / Workflow Analysis
✓

Logical Data Contract
✓

Product Requirements
✓

↓

System Architecture
← NEXT

↓

Technology Mapping

↓

Implementation Plan

↓

Vertical Slice Implementation

↓

Evaluation

↓

Iteration

↓

Portfolio Case Study
```

---

# 68. Final Product Principle

The MVP is not designed to maximize automation.

It is designed to maximize useful automation.

Therefore:

```text
Automate repetitive work

Structure AI outputs

Preserve source evidence

Keep professional decisions human-controlled

Measure actual usefulness

Improve the workflow with real usage data

Only introduce technology when the business requirement justifies it
```

最终目标：

> Build an evidence-backed, human-in-the-loop AI content research system that can continuously discover, research and organize valuable legal-content opportunities while reducing repetitive manual work.