# Day 03 — Business Problem, Trigger & Input Analysis

## Date

2026-08-27

---

## Today's Goal

今天的目标是学习 Automation Project 在进入技术实现之前，如何完成基础 Workflow Analysis。

核心学习路径：

```text
Business Problem
↓
Trigger
↓
Input
```

使用真实项目：

> AI-powered Legal Content Research & Topic Discovery Workflow

作为练习案例。

核心原则：

> Business Requirement First, Technology Second.

不要从“我要用 n8n / Python / AI 做什么”开始，而应该先理解业务问题和 Workflow。

---

# 1. Business Problem Analysis

## What I Learned

Automation Project 首先需要理解当前业务，而不是直接设计技术方案。

基本分析路径：

```text
Current Situation / As-Is Workflow
↓
Pain Points
↓
Automation Opportunities
↓
Automation Boundary
↓
Automation Goal
↓
Success Metrics
```

首先回答：

> 当前业务实际上是怎么运行的？

然后才能判断：

> 哪些问题值得自动化？

---

## Project Practice — As-Is Workflow

Legal Content Automation 当前人工流程：

```text
律师确定业务 / 案件类目
↓
拆分案件分组
↓
AI 扩展法律关键词
↓
人工在社交媒体搜索
↓
根据互动数据筛选帖子
↓
人工分析帖子正文和评论
↓
约 7 天后重新查询互动数据
↓
判断内容 / 话题趋势
↓
与律师案例库匹配
↓
律师决定最终脚本选题
```

这一阶段描述：

```text
As-Is Workflow
```

而不是未来自动化后的：

```text
To-Be Workflow
```

---

# 2. Pain Point Analysis

通过拆解当前 Workflow，识别出 6 个主要 Pain Points。

## Pain Point 1 — Keyword Quality & Validation

AI 根据法律分类生成的关键词，不一定符合真实社交媒体用户的表达习惯。

Example:

```text
Legal Expression:
违法解除劳动合同

Real User Expression:
被公司开除了怎么办
```

核心问题：

> AI Generated Keywords ≠ Real User Language

因此未来需要通过真实平台数据验证和校准关键词。

---

## Pain Point 2 — Manual Collection & Poor Scalability

当前需要人工：

```text
Keyword
↓
Search
↓
Browse
↓
Screen
↓
Record
```

人工工作量会随着：

```text
Keyword Count
×
Platform Count
×
Collection Frequency
```

不断增加。

这是明显的 Automation Opportunity。

---

## Pain Point 3 — Manual Analysis & Inconsistent Standards

帖子正文和评论主要依赖人工阅读和分析。

除了耗时，还存在：

```text
Different Time
+
Different People
+
Different Judgment
↓
Inconsistent Analysis
```

AI 的价值不仅是减少人工阅读，还可以帮助建立统一的 First-pass Analysis Standard。

---

## Pain Point 4 — Manual Tracking & Missing Historical Trend Data

目前需要人工重新查询帖子互动数据。

如果只记录：

```text
Current Engagement
```

只能知道当前状态。

如果要判断：

```text
Growing
Stable
Declining
```

则需要保存 Historical Data。

---

## Pain Point 5 — Inefficient Case Matching

随着 Case Library 增加，单纯依赖：

```text
Manual Memory
+
Keyword Search
```

效率会越来越低。

同时：

```text
Social Media User Language
≠
Legal Case Description
```

Exact Keyword Matching 可能遗漏语义相关案例。

具体采用：

```text
Keyword Search
Metadata
Semantic Search
Embeddings
RAG
```

暂时不决定，留到 Technology Mapping。

---

## Pain Point 6 — Static Keyword Library & Lack of Feedback Loop

Keyword Library 不能：

```text
Generate Once
↓
Use Forever
```

应该形成：

```text
Keyword Library
↓
Real Social Media Search
↓
Real User Language
↓
Keyword Performance
↓
Long-tail Keyword Discovery
↓
Keyword Calibration
↓
Updated Keyword Library
```

初步 Keyword Lifecycle：

```text
Candidate
↓
Testing
↓
Active
↓
Observe
↓
Retired
```

---

# 3. Automation Boundary

今天明确了：

> Automation ≠ Everything Should Be Automated.

根据工作性质，将系统职责分为三层。

### Fully Automated

适合：

```text
Clear Rules
High Repetition
Low Professional Risk
```

例如：

- Social Media Collection
- Engagement Calculation
- Data Normalization
- Historical Tracking
- Long-tail Keyword Discovery

### AI-assisted

适合：

```text
Semantic Understanding
Classification
Matching
Recommendation
```

例如：

- Keyword Generation
- Content Analysis
- Keyword Calibration Recommendation
- Case Matching
- Candidate Topic Recommendation

典型结构：

```text
AI First-pass
↓
Human Review
```

### Human-controlled

涉及 Professional Judgment、Business Decision 和 Final Approval 的工作继续由律师控制。

例如：

- Business Direction
- Important Keyword Changes
- Case Relevance Confirmation
- Final Topic Selection
- Final Legal Content Judgment

核心原则：

> Automation 的目标不是替代律师，而是减少低价值重复劳动，让人工集中处理高价值专业判断。

---

# 4. Success Metrics

Automation 是否成功不能只看：

```text
Workflow Successfully Ran
```

还应该判断：

> Did the business improve?

基本结构：

```text
Baseline
↓
Metric
↓
Target
```

本项目初步建立的 Metrics：

- Time Saved
- Manual Work Reduction
- Content Coverage
- Keyword Effectiveness
- Analysis Consistency
- Trend Detection Quality
- Case Matching Quality
- Topic Recommendation Quality

如果当前缺少真实运行数据：

```text
Baseline = TBD
Target = TBD
```

不应该人为虚构数字。

---

# 5. Trigger Analysis

## What is Trigger?

Trigger 回答：

> What actually starts the workflow?

例如：

```text
Every Sunday at 10:00
```

今天学习的主要 Trigger Types：

```text
Event Trigger
Schedule Trigger
Manual Trigger
Data Trigger
External Trigger / Webhook
```

---

# 6. Trigger vs Dependency vs Precondition vs Execution Rule vs Decision

这是今天最重要的概念之一。

### Trigger

什么真正启动 Workflow？

```text
Sunday 10:00
```

### Upstream Dependency

Workflow 依赖什么上游数据或 Workflow？

```text
Analyzed Post & Comment Library
```

### Precondition

Workflow 启动以后，什么条件必须成立才能继续？

```text
Approved Topic Pool is not empty
```

### Execution Rule

Workflow 运行时遵守什么业务规则？

```text
Maximum 4 Seed Keywords per Run
```

### Decision

Workflow 运行过程中，根据什么条件决定下一步？

```text
Engagement > 500?
↓
YES → Priority Post
NO → Normal Post
```

完整关系：

```text
Trigger
↓
Dependency Check
↓
Precondition Check
↓
Execution Rules
↓
Process
↓
Decision
↓
Action
```

---

# 7. Important Trigger Learning

一个 Workflow：

> 可以依赖另一个 Workflow，但不一定由另一个 Workflow 直接 Trigger。

Example:

```text
Task C
↓
Produces Analyzed Data
↓
Analyzed Post Library
↓
Wait
↓
Sunday 10:30
↓
Task D
```

Task D：

```text
Dependency = Task C Data

Trigger = Sunday 10:30
```

因此：

> Dependency determines what the workflow needs.  
> Trigger determines when the workflow starts.

---

# 8. Project Trigger Architecture

为 Legal Content Automation 设计了 A–G 七个 Workflow 的 Trigger Architecture。

| Workflow | Trigger | Execution Mode |
|---|---|---|
| A. Social Media Content Collection | Mon–Sat 10:00 | Scheduled Batch |
| B. Priority Post Tracking | Sunday 10:00 | Weekly Batch |
| C. AI Content & Comment Analysis | Lawyer Approval | Human-in-the-loop |
| D. Long-tail Keyword Discovery | Sunday 10:30 | Weekly Batch |
| E. Seed Keyword Calibration | Last Day of Month 10:00 | Monthly Batch |
| F. Case Library Matching | Sunday 10:30 | Weekly Batch |
| G. Candidate Script Topic Generation | Case Matching Completed | Workflow Dependency |

---

# 9. Input Analysis

Input 回答：

> Workflow 启动以后，需要什么数据才能完成任务？

今天建立的 Input Analysis 思路：

```text
Source
↓
Fields
↓
Requirement
↓
Data Type / Format
↓
Normalization
↓
Validation
↓
Missing / Invalid Handling
↓
Freshness
```

Input Analysis 不只是列 Fields。

真正需要判断的是：

> 什么样的数据才能被 Workflow 正常使用？

---

# 10. Data Types

学习了 Automation / API / JSON 中常见的数据类型：

```text
String
Integer
Float / Number
Boolean
Array / List
Datetime
Object
Enum
```

Example:

```text
"1250"
→ String

1250
→ Integer
```

重要理解：

> Data Type 应根据数据未来如何被使用决定。

例如 ID 即使看起来是数字，如果主要用于 Identity 而不是 Calculation，通常可以使用 String。

---

# 11. Required, Empty & Missing

字段不能只简单区分：

```text
Required
Optional
```

还需要考虑：

```text
Required / Non-null
Required / Empty Allowed
Optional
```

重要区别：

```text
Empty ≠ Missing
```

例如：

```text
tags = []
```

如果原帖子本来没有 Tags：

```text
Valid Empty
```

但如果理论上应该采集到，却得到：

```text
tags = null
```

则可能属于：

```text
Missing Data
```

---

# 12. Normalization vs Validation

### Normalization

把 Source Data 转换成系统统一格式。

Example:

```text
"1.2万"
↓
12000
```

### Validation

判断转换后的数据能不能使用。

```text
12000
↓
Integer?
↓
Value >= 0?
↓
Valid
```

因此推荐顺序：

```text
Raw Data
↓
Normalization
↓
Validation
↓
Eligible Data
```

核心区别：

> Normalization 负责统一数据；Validation 负责判断数据是否可用。

---

# 13. Data Quality

真实 Workflow 不应该只有：

```text
Valid
Invalid
```

今天进一步建立：

```text
Valid
Incomplete
Missing
Invalid
Unavailable
```

其中：

```text
Incomplete Data
≠
No Business Value
```

部分数据即使不完整，也可能仍然值得保留。

---

# 14. Missing / Invalid Handling

发现数据问题后，不应该：

```text
Invalid
↓
Delete
```

而应该：

```text
Data Problem
↓
Determine Reason
↓
Choose Handling
```

可能的 Handling：

```text
Valid Empty
Retry
Normalize
Alternative Source / Method
Keep + Mark Incomplete
Skip
Manual Review
Mark Unavailable
```

Retry 必须有：

```text
Retry Limit
+
Failure Reason
```

不能无限重试。

---

# 15. Data Freshness & Timezone

数据不仅需要正确，还需要知道：

> When was this data generated or observed?

今天区分了：

```text
Published At
Collected / Observed At
Updated At
Analyzed At
Tracked At
```

例如：

```text
Published At
→ 作者什么时候发布

Observed At
→ 系统什么时候观察到这一组数据
```

同时 Datetime 应考虑：

```text
Timezone
```

避免未来跨平台数据比较出现时间错误。

---

# 16. Raw Data vs Derived Data

项目中的典型例子：

```text
Raw Data
├── Likes
├── Saves
└── Comments Count

        ↓

Derived Data
└── Engagement
```

当前计算：

```text
Engagement
=
Likes
+
Saves
+
Comments Count
```

重要原则：

> 尽量保留重要 Raw Data，而不是只保存 Derived Result。

---

# 17. Current State vs History

如果只保存：

```text
Engagement = 1500
```

只能回答：

> What is it now?

如果保存：

```text
Week 1 = 400
Week 2 = 800
Week 3 = 1500
```

才能回答：

> How did it change?

因此：

```text
Current State
→ 当前是什么

History
→ 如何变化
```

---

# 18. Search Hit History vs Engagement History

项目中识别出了两类不同 History。

### Search Hit History

回答：

> 哪个 Keyword 在什么时候搜到了哪个 Post？

```text
Search Hit
├── Post ID
├── Source Keyword
├── Search At
└── Search Rank
```

主要用于：

```text
Keyword Performance
Keyword Calibration
```

### Engagement History

回答：

> Post 的互动数据如何随时间变化？

```text
Engagement Observation
├── Post ID
├── Observed At
├── Likes
├── Saves
├── Comments Count
└── Engagement
```

主要用于：

```text
Post Tracking
Trend Detection
Topic Trend Analysis
```

重要理解：

> Search Hit History 和 Engagement History 解决的是两个不同的业务问题。

---

# 19. Deduplication vs Relationship Preservation

同一个 Post 可能被多个 Keyword 搜到：

```text
Keyword A → Post 001
Keyword B → Post 001
```

Post 本身应该：

```text
Post 001
→ One Business Object
```

但两个 Relationship 都应该保存：

```text
Keyword A → Post 001
Keyword B → Post 001
```

因此：

> Duplicate Object ≠ Duplicate Relationship.

Deduplication 不能导致有价值的 Relationship 丢失。

---

# 20. Progressive Data Enrichment

今天确定项目采用：

> Progressive Data Enrichment

Current Design:

```text
Search
↓
Collect Basic Post Data
↓
Candidate Post
↓
Lawyer Review
↓
Approved?
├── No → Stop Deep Collection
└── Yes
      ↓
Collect Comment Content
      ↓
AI Deep Analysis
```

因此：

```text
Comments Count
→ Task A Required

Comment Content
→ Lawyer Approval 后再采集
```

这样可以减少：

```text
API Cost
Collection Cost
Storage
AI Token Usage
Processing Cost
```

核心原则：

> Collect minimum necessary data first, then enrich high-value objects.

---

# 21. Task A Input Design

Task A 当前主要 Input：

```text
Official Seed Keyword
+
Target Platform
+
Post Time Range
+
Collection Limit
+
Candidate Selection Strategy
```

Current MVP：

```text
Platform:
Xiaohongshu

Time Range:
Last 7 Days

Candidate Limit:
Maximum 5 per Seed Keyword

Selection Priority:
High Relevance + High Engagement
```

另外明确：

```text
Top 5 Candidate Posts
≠
Engagement > 500
```

其中：

```text
Top 5
→ Candidate Selection

Engagement > 500
→ Priority Post Eligibility
```

两者属于不同 Business Rules。

---

# 22. Documentation Deliverables

今天同步更新了两层 Documentation。

### General Framework

```text
06-automation/
└── workflow-analysis-framework.md
```

作用：

> 保存可复用于其他 Automation Projects 的通用 Workflow Analysis 方法。

当前完成：

```text
Business Problem Analysis
Trigger Analysis
Input Analysis
```

### Real Project

```text
projects/
└── legal-content-automation/
    └── workflow-analysis.md
```

作用：

> 保存 Legal Content Automation 的具体业务规则和 Workflow Design。

当前完成：

```text
Business Problem
Trigger Architecture
Task A Input Analysis
```

---

# 23. Key Mindset Change

Day 03 最重要的变化，是开始从：

```text
Business Problem
↓
Find a Tool
↓
Build Automation
```

转变为：

```text
Understand Business
↓
Map As-Is Workflow
↓
Identify Pain Points
↓
Define Automation Boundary
↓
Define Success Metrics
↓
Define Trigger
↓
Define Dependencies & Preconditions
↓
Define Input
↓
Normalize & Validate Data
↓
Design Process
↓
Choose Technology
```

核心原则：

> Business Requirement First, Technology Second.

---

# 24. Day 03 Deliverables

```text
✅ Business Problem Analysis
✅ As-Is Workflow
✅ 6 Main Pain Points
✅ Automation Boundary
✅ Success Metrics
✅ Trigger Types
✅ Trigger / Dependency / Precondition / Execution Rule / Decision
✅ A–G Trigger Architecture
✅ Input Analysis Framework
✅ Data Types
✅ Required / Empty / Missing
✅ Normalization / Validation
✅ Data Quality Status
✅ Missing / Invalid Handling
✅ Data Freshness / Timezone
✅ Raw Data vs Derived Data
✅ Current State vs History
✅ Search Hit History
✅ Engagement History
✅ Deduplication vs Relationship Preservation
✅ Progressive Data Enrichment
✅ Task A Input Design
✅ General Framework Updated
✅ Project Workflow Documentation Updated
```

---

# 25. Next Step — Day 04

Next:

> Process Analysis

核心问题：

```text
We already know:

Trigger
+
Input

↓

How does the system transform
those inputs into useful outputs?
```

Task A 初步 Process：

```text
Valid Collection Inputs
↓
Search
↓
Raw Result Pool
↓
Normalize
↓
Validate
↓
Filter
↓
Deduplicate
↓
Evaluate Relevance
↓
Calculate Engagement
↓
Rank
↓
Top 5 Candidate Posts
↓
Store Historical Data
```

Day 04 将重点学习：

```text
Process Boundary
Step & Sequence
Loop
Batch Processing
Transformation
State Change / Persistence
Idempotency
Error / Exception Path
```

---

## Day 03 Status

```text
Business Problem  ✅
Trigger           ✅
Input             ✅

Process           → Day 04
Decision          → Upcoming
Action            → Upcoming
Output            → Upcoming
```