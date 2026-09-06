# Legal Content Automation - Workflow Analysis

> Project: AI-powered Legal Content Research & Topic Discovery Workflow  
> Current Stage: Day 03 — Business Problem, Trigger & Input Analysis  
> Status: Input Analysis Completed for Current MVP v1

---

# 0. Business Problem

## 0.1 Current Workflow — As-Is

当前律师内容研究和选题流程主要依赖人工完成。

### Step 1 — Define Business Categories

律师根据自身业务方向确定案件类目和内容研究方向。

当前主要方向包括：

- 劳动争议
- 企业合规
- 经济纠纷

---

### Step 2 — Split Categories

将案件类目进一步拆分为不同研究分组。

---

### Step 3 — Generate Search Keywords

针对不同分组，使用 AI 扩展和生成相关法律关键词。

当前方式主要依赖：

```text
Legal Category
↓
AI Keyword Expansion
↓
Search Keywords
```

---

### Step 4 — Search Social Platforms

律师使用关键词在社交媒体平台进行搜索。

当前主要平台：

```text
Xiaohongshu
```

未来可以扩展其他平台。

---

### Step 5 — Screen Posts

人工浏览搜索结果，根据：

- 内容相关度
- 点赞
- 收藏
- 评论

判断哪些帖子值得关注。

历史人工流程中曾使用：

```text
Engagement
=
Likes + Saves + Comments

Engagement > 500
→ High-engagement Post
```

该阈值属于原人工流程中的辅助信号。

在 To-Be Workflow 中：

> Engagement > 500 不再自动决定帖子是否进入 Priority / Research Pool。

---

### Step 6 — Analyze Content

对筛选后的帖子人工阅读并记录：

- 帖子内容
- 核心话题
- 用户问题
- 评论区讨论
- 用户表达
- 当前互动数据

---

### Step 7 — Track Selected Posts

对部分值得持续观察的帖子，在约 7 天后重新查看：

- Likes
- Saves
- Comments
- Engagement

用于判断帖子是否仍在增长。

---

### Step 8 — Match Cases & Select Topics

将社交媒体研究结果与律师案例库进行匹配。

律师最终判断：

- 是否存在相关案件
- 是否值得进一步研究
- 是否适合作为内容选题

---

# 0.2 Pain Points

## Pain Point 1 — Keyword Quality & Validation

### Problem

AI 根据法律术语生成的关键词，不一定符合真实社交媒体用户的表达方式。

例如：

```text
Legal Language:
违法解除劳动合同

User Language:
公司逼我自己辞职
领导一直想逼我走
不给我排班逼我离职
```

### Consequences

- 搜索结果相关度不足
- 漏掉真实用户表达
- 上游关键词质量问题影响全部后续流程
- 无法知道哪些关键词真正有效

---

## Pain Point 2 — Manual Collection & Poor Scalability

目前需要人工：

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

随着：

- Keyword 数量增加
- 搜索频率增加
- Platform 增加

人工成本快速上升。

### Consequences

- 数据采集耗时
- 覆盖范围有限
- 容易漏掉内容
- 难以扩展到多个平台

---

## Pain Point 3 — Manual Analysis & Inconsistent Standards

不同帖子需要人工：

- 阅读
- 分类
- 总结
- 分析评论
- 提炼用户问题

缺少统一结构。

### Consequences

- 分析耗时
- 判断标准容易波动
- 多人协作时一致性降低
- 后续数据难以比较

---

## Pain Point 4 — Manual Tracking & Missing Historical Trend Data

人工重新查找帖子并记录互动数据。

### Consequences

- 容易漏追
- 历史数据不连续
- 难以计算增长
- 难以判断趋势

---

## Pain Point 5 — Inefficient Case Matching

案例数量增加以后，仅依靠：

```text
Human Memory
+
Keyword Search
```

效率持续下降。

而社媒表达和法律案件描述经常存在：

```text
Semantic Gap
```

### Consequences

- 查找耗时
- 容易漏掉语义相关案件
- 热点和真实办案经验无法高效连接

---

## Pain Point 6 — Static Keyword Library & Lack of Feedback Loop

当前 Keyword Library 建立以后缺少持续校准机制。

而真实社交媒体运行过程中会不断产生：

- New User Expressions
- Long-tail Keywords
- New Topics
- New Search Patterns

这些没有系统反哺 Keyword Library。

---

# 0.3 Root Causes

主要 Root Causes：

```text
Keyword Generation
依赖 Legal Language / AI Expansion
↓
缺少 Platform Feedback

Manual Collection
↓
缺少 Automated Acquisition

Manual Analysis
↓
缺少 Structured Analysis Standard

Manual Tracking
↓
缺少 Historical Observation Model

Manual Case Search
↓
缺少 Structured Matching Interface

Static Keyword Library
↓
缺少 Feedback Loop
```

---

# 0.4 Automation Opportunities

适合 Fully Automated 的工作：

- Social Media Search
- Data Collection
- Normalization
- Validation
- Deduplication
- Engagement Calculation
- Historical Observation Storage
- Scheduled Tracking
- Basic AI Analysis
- Weekly Data Processing
- Long-tail Discovery
- Case Matching First-pass
- Topic Candidate Generation
- Feishu Result Delivery

适合 AI-assisted 的工作：

- Topic Classification
- Short Summary
- Deep Content Analysis
- Comment Analysis
- Long-tail Discovery
- Keyword Calibration Recommendation
- Semantic Case Matching
- Candidate Topic Recommendation

需要 Human-controlled 的工作：

- Keep / Reject
- Tracking Selection
- Deep Analysis Selection
- Post-tracking Deep Analysis Re-evaluation
- Keyword Status Approval
- Final Topic Approval
- Final Professional / Legal Judgment

---

# 0.5 Automation Boundary

## Fully Automated

系统自动完成：

- 搜索和采集
- 数据标准化和验证
- 数据去重
- Search Hit 保存
- Engagement 计算
- Basic AI Analysis
- Topic Classification
- Short Summary
- Tracking Execution
- Historical Observation 保存
- Deep Analysis 执行
- 系统判断是否需要 Comment-level Data
- Long-tail Discovery
- Keyword Calibration Analysis
- Case Matching
- Candidate Topic Generation
- Feishu Delivery

---

## AI-assisted

AI 提供：

- Semantic Understanding
- Classification
- Summarization
- Deep Analysis
- User Problem Extraction
- Legal Issue Extraction
- Discussion Point Extraction
- User Expression Extraction
- Keyword Recommendation
- Case Matching
- Topic Recommendation

但 AI 不拥有最终业务决定权。

---

## Human-controlled

律师在 MVP 中保留：

### Daily

```text
Keep?
Reject?
```

### Research Stage

```text
Track?
Deep Analysis Now?
```

### Post-Tracking

```text
New Tracking Evidence
↓
Deep Analysis Re-evaluation
```

### Monthly Keyword Calibration

```text
Approve / Reject Keyword Status Change
```

### Weekly Topic Review

```text
Approve / Reject Candidate Topic
```

---

# 0.6 Key Human Decision Principle

当前 MVP 正式锁定：

```text
Keep
≠
Track
≠
Deep Analysis
```

三者代表三个不同业务判断。

### Keep

> 这篇内容是否值得进入研究资料池？

### Track

> 是否值得持续观察其互动变化？

### Deep Analysis

> 是否值得投入更多数据和 AI 成本做深度研究？

---

# 0.7 Deep Analysis Is Re-evaluable

Deep Analysis Decision 不是永久决定。

例如：

```text
Day 1

Keep = Yes
Track = Yes
Deep Analysis = No
```

7 天后：

```text
Task B Tracking
↓
New Tracking Evidence
↓
Feishu Weekly Review
↓
Lawyer Re-evaluation
↓
Deep Analysis = Yes
↓
Task C
```

因此：

> New Evidence can change a previous business decision.

历史 Decision 不应被覆盖。

---

# 0.8 Feishu Interaction & Delivery Requirement

Feishu 是本系统的：

> Human Interaction & Delivery Layer

而不只是通知工具。

Feishu 用于：

### System → Lawyer

- Daily Collection Review
- Basic Analysis Result
- Tracking Result
- Weekly Research Result
- Long-tail Result
- Monthly Keyword Calibration
- Case Matching Result
- Candidate Topic Result
- Important Error / Exception

### Lawyer → System

- Keep / Reject
- Track Decision
- Deep Analysis Decision
- Deep Analysis Re-evaluation
- Keyword Status Approval
- Topic Approval

Conceptually:

```text
Automation System
        ↓
      Feishu
        ↕
      Lawyer
        ↓
Human Decision
        ↓
Automation Continues
```

具体采用：

- Message
- Interactive Card
- Bitable
- Form
- Other Interface

留到 Product Design / Technology Mapping。

---

# 0.9 Always-on Execution Requirement

Production MVP 必须：

> 独立于律师本地电脑运行。

即：

```text
Local Computer Offline
↓
Scheduled Workflow
↓
Still Executes
```

Production 系统需要逻辑上的：

```text
Always-on Runtime
+
Persistent Data / State Layer
+
AI / Automation Layer
+
Feishu Interaction Layer
```

具体采用：

- Cloud Automation
- VPS
- Managed Service
- Database
- Docker
- Other Hosting

当前不决定。

Technology Mapping 时再比较：

- Cost
- Stability
- Maintenance
- Connectivity
- Python Requirement
- Database Requirement
- n8n Requirement
- China / External API Network Reality

---

# 0.10 Existing Case Library Pipeline

当前已经存在独立案例库建设流程：

```text
Judgment
↓
Codex
↓
Rule-based Extraction / Analysis
↓
Standardized Excel
↓
Structured Case Library
```

该 Excel 持续在本地更新。

因此本项目：

> 不负责重新建设 Judgment → Structured Case 的 Pipeline。

本项目 Task F 只消费：

```text
Structured Case Library
```

Current State：

```text
Local Standardized Excel
```

Future Production Requirement：

```text
Latest Structured Case Library
↓
Accessible Online / Remotely
↓
Independent of Local Computer
```

最终数据存储方式：

```text
TBD during Technology Mapping
```

---

# 0.11 Automation Goal

最终目标：

```text
Daily
发现有价值信号

↓

On-demand
深入理解

↓

Weekly
形成研究洞察和候选选题

↓

Monthly
校准关键词发现机制

↓

Next Cycle
持续提高搜索质量
```

---

# 0.12 Success Metrics

## 1. Time Saved

衡量：

律师每周用于：

- 搜索
- 筛选
- 整理
- 追踪
- 案例查找
- 选题准备

的时间。

Baseline：

```text
TBD
```

Target：

> 显著减少重复人工工作。

---

## 2. Manual Work Reduction

重点观察：

- Manual Search
- Manual Screening
- Manual Recording
- Manual Tracking
- Manual Engagement Calculation
- Manual Case Search

---

## 3. Content Coverage

衡量：

- Keyword Coverage
- Post Coverage
- Tracking Coverage
- Platform Coverage
- Collection Frequency

---

## 4. Keyword Effectiveness

衡量：

- Search Hits
- Distinct Posts
- Candidate Posts
- Keep / Reject
- Research Retention
- Engagement Evidence
- Long-tail Discovery
- Keyword Status Evolution

---

## 5. Analysis Consistency

人工抽样检查：

- Topic Classification Accuracy
- User Problem Accuracy
- Legal Issue Accuracy
- Discussion Point Accuracy
- Invalid Analysis Rate

---

## 6. Trend Detection Quality

衡量：

- Historical Observation Completeness
- Engagement Growth
- Trend Detection
- Tracking Reliability

---

## 7. Case Matching Quality

衡量：

```text
AI Recommended Cases
↓
Lawyer Review
↓
Relevant / Not Relevant
```

---

## 8. Topic Recommendation Quality

衡量：

```text
Candidate Topics
↓
Lawyer Approval
↓
Adoption Rate
```

---

## 9. Research Retention Rate

定义修正为：

```text
Candidate Posts
↓
Lawyer Review
↓
Confirmed Research Posts
```

Formula：

```text
Research Retention Rate
=
Confirmed Research Posts
/
Candidate Posts
```

注意：

```text
Confirmed Research
≠
Priority Tracking
```

Baseline：

```text
TBD
```

Target：

```text
TBD
```

---

# 0.13 MVP Success Criteria

MVP 优先验证：

1. 是否减少人工搜索和整理时间
2. 是否稳定采集社媒数据
3. 是否形成一致的 Basic / Deep Analysis
4. 是否保存可靠的 Tracking History
5. 是否建立 Keyword Feedback Loop
6. 是否能辅助 Case Matching
7. 是否生成有使用价值的 Candidate Topics
8. Feishu 是否能承载主要 HITL
9. Production Workflow 是否能独立于本地电脑运行

---

# 0.14 Future Scope

当前 MVP 暂不包括：

- 自动生成完整脚本
- 自动发布内容
- 自动决定最终选题
- 自动修改所有 Keyword Status
- 长期无限 Tracking
- 高级趋势模型
- 完整 Content Performance Feedback Loop
- 复杂 Agent Architecture
- Advanced RAG unless genuinely required
- Model Fine-tuning

---

# 1. Trigger Analysis

## 1.1 Current Workflow Architecture

当前 MVP 包含：

```text
Task A  — Social Media Search & Collection
Task A2 — Daily Basic Analysis & Lawyer Review
Task B  — Priority Post Tracking
Task C  — Deep AI Content & Comment Analysis
Task D  — Long-tail Keyword Discovery
Task E  — Seed Keyword Calibration
Task F  — Case Library Matching
Task G  — Candidate Topic Generation
```

---

# 1.2 Trigger Summary

| Workflow | Trigger | Main Dependency | Mode |
|---|---|---|---|
| Task A | Mon–Sat 10:00 | Seed Keyword Library | Scheduled Batch |
| Task A2 | Task A Candidate Batch Ready | Candidate Posts | Workflow Completion + HITL |
| Task B | Sunday 10:00 | Priority Tracking Pool | Weekly Batch |
| Task C | Valid Deep Analysis Request | Confirmed Research Post | Event / HITL-driven |
| Task D | Sunday 10:30 | New Deep Analysis Results | Weekly Batch |
| Task E | Last Day of Month 10:00 | Monthly Keyword Evidence | Monthly Batch |
| Task F | Sunday 10:30 | Structured Research Subjects + Case Library | Weekly Batch |
| Task G | Weekly Research Preparation Complete | Structured Research Subjects | Weekly Orchestration |

---

# 1.3 Task A — Social Media Search & Collection

## Trigger

```text
Monday–Saturday 10:00
```

Type:

```text
Schedule Trigger
```

## Dependency

```text
Official Seed Keyword Library
```

## Preconditions

至少存在一个：

```text
Eligible Seed Keyword
```

Keyword 不得：

```text
Empty
Retired
Unavailable
```

## Execution Rules

- 每次最多处理 4 个 Seed Keywords
- MVP Platform = Xiaohongshu
- 时间范围默认 Last 7 Days
- 每 Keyword 每 Run 最多输出 5 个 Candidate Posts
- Candidate Limit ≠ Raw Retrieval Limit
- Raw Retrieval Limit = TBD

---

# 1.4 Task A2 — Daily Basic Analysis & Lawyer Review

## Trigger

```text
Task A Candidate Batch Ready
```

## Dependency

```text
Candidate Posts
```

## System Actions

AI 自动：

```text
Topic Classification
+
Short Summary
```

然后：

```text
Feishu Daily Review
```

律师决定：

```text
Keep?
├── No → Reject / Archive
└── Yes → Confirmed Research Pool
```

注意：

```text
Keep
≠
Track
≠
Deep Analysis
```

---

# 1.5 Task B — Priority Post Tracking

## Trigger

```text
Sunday 10:00
```

Type：

```text
Schedule Trigger
```

## Dependency

```text
Priority Tracking Pool
```

进入 Pool 的逻辑：

```text
Confirmed Research Post
+
Tracking Required = Yes
```

不是：

```text
Engagement > 500
```

## Eligibility

至少满足：

```text
Minimum Tracking Interval
>= 7 days from Initial Observed At
```

## MVP Rule

每个 eligible Post：

```text
Initial Observation
+
One Follow-up Observation
```

当前 MVP Tracking Completed 后不无限周更。

---

# 1.6 Task C — Deep Analysis

Task C 存在两个入口。

## Entry A — Daily Review

```text
Confirmed Research Post
↓
Lawyer:
Deep Analysis Now = Yes
↓
Deep Analysis Request
↓
Task C
```

## Entry B — Post-Tracking Review

```text
Task B
↓
New Tracking Evidence
↓
Feishu Weekly Review
↓
Lawyer Re-evaluation
↓
Deep Analysis = Yes
↓
Deep Analysis Request
↓
Task C
```

因此 Task C 真正的 Trigger：

```text
Valid Deep Analysis Request
```

Task C 不关心 Request 来自：

```text
Daily Review
or
Post-Tracking Review
```

---

# 1.7 Task D — Long-tail Keyword Discovery

## Trigger

```text
Sunday 10:30
```

## Dependency

```text
New / Newly Completed
Deep Analyzed Research Data
since previous Task D run
```

Task D 不应该单纯使用：

```text
Published At within last 7 days
```

因为旧帖子可能本周才完成 Deep Analysis。

---

# 1.8 Task E — Seed Keyword Calibration

## Trigger

```text
Last Day of Month 10:00
```

## Dependency

包括：

- Seed Keyword Library
- Search Hit History
- Candidate Results
- Lawyer Decisions
- Engagement Evidence
- Deep Analysis Evidence
- Long-tail Candidates

## MVP Human Control

系统：

```text
Analyze
↓
Recommend Status Change
```

律师：

```text
Approve / Reject
```

MVP 中：

> 所有 Keyword Status Changes 均需律师批准后生效。

---

# 1.9 Task F — Case Library Matching

## Trigger

```text
Sunday 10:30
```

## Dependencies

```text
Structured Research Subjects
+
Structured Case Library
```

Tracking / Long-tail Data：

```text
Optional Context
```

Case Match：

```text
Enhancement
≠
Topic Generation Gate
```

---

# 1.10 Task G — Candidate Topic Generation

## Trigger

Weekly Research Preparation completed.

Task G 应尽量在本周：

- Task D available result
- Task F available result

完成以后执行。

但：

```text
No Long-tail Result
or
No Case Match
```

不能阻止 Topic Generation。

---

# 1.11 Current End-to-End Trigger Architecture

```text
Seed Keyword Library
        ↓
[Mon–Sat 10:00]
        ↓
Task A
Search & Collection
        ↓
Candidate Posts
        ↓
Task A2
AI Basic Analysis
        ↓
Feishu Daily Review
        ↓
Lawyer: Keep?
 ┌──────┴──────┐
 No            Yes
 ↓              ↓
Archive   Confirmed Research Pool
                  │
          ┌───────┴─────────┐
          │                 │
        Track?        Deep Analysis Now?
          │ Yes             │ Yes
          ↓                 ↓
Priority Tracking     Deep Analysis Queue
      Pool                    │
          ↓                   │
[Sunday 10:00]                │
      Task B                  │
          ↓                   │
New Tracking Evidence         │
          ↓                   │
Feishu Weekly Review          │
          ↓                   │
Deep Analysis Re-evaluation?  │
          │ Yes               │
          └──────────┬────────┘
                     ↓
                   Task C
                Deep Analysis
                     ↓
        Structured Research Subject
                     │
            ┌────────┴────────┐
            │                 │
            ↓                 ↓
     [Sunday 10:30]     [Sunday 10:30]
          Task D              Task F
     Long-tail Discovery   Case Matching
            │                 │
            └────────┬────────┘
                     ↓
                   Task G
          Candidate Topic Generation
                     ↓
                   Feishu
                     ↓
            Lawyer Final Review
                     ↓
          Approved Content Topics
```

Monthly feedback：

```text
Seed Keywords
+
Search Hits
+
Keep / Reject
+
Tracking
+
Deep Analysis
+
Long-tail Candidates
        ↓
Task E
Monthly Calibration
        ↓
System Recommendation
        ↓
Feishu
        ↓
Lawyer Approval
        ↓
Updated Keyword Library
        ↓
Next Search Cycle
```

---

# 2. Input Analysis

# 2.1 Input Architecture

当前系统的数据流不是：

```text
Task A Data
↓
Copy
↓
Task B Data
↓
Copy
↓
Task C Data
```

而应该是：

```text
Persistent Business Objects
+
Events / Observations
+
States
+
Decisions
+
Relationships
```

核心原则：

> Deduplicate Entity, preserve Relationships and History.

---

# 2.2 Task A — Social Media Search & Collection Inputs

## Input 1 — Official Seed Keyword

Source：

```text
Seed Keyword Library
```

Requirement：

```text
Required / Non-null
```

必须：

- Keyword 存在
- Keyword 非空
- Status != Retired
- 当前 eligible for collection

---

## Input 2 — Target Platform

MVP：

```text
Xiaohongshu
```

Requirement：

```text
Required
```

必须：

- Platform supported
- Platform active
- 至少存在可用 Acquisition Method

注意：

> 不要求必须存在 Official API。

具体采集技术：

```text
TBD during Technology Mapping
```

---

## Input 3 — Post Time Range

Current MVP：

```text
Last 7 Days
```

如果 Source 无法直接过滤：

```text
Collect
↓
Normalize Published At
↓
Filter
```

---

## Input 4 — Collection Limit

Current Candidate Limit：

```text
Max 5 Candidate Posts
per Seed Keyword
per Run
```

注意：

```text
Raw Retrieval Limit
≠
Candidate Limit
```

Raw Retrieval Limit：

```text
TBD
```

---

## Input 5 — Candidate Selection Strategy

当前业务要求：

```text
High Relevance
+
Useful Engagement Signal
```

Exact scoring / ranking：

```text
TBD during Decision Analysis
```

`Engagement > 500`：

```text
High-engagement Signal
```

不是：

```text
Automatic Priority Decision
```

---

# 2.3 Task A — Candidate Post Data

## Identity

| Field | Requirement |
|---|---|
| Post ID | Required |
| URL | Required |
| Platform | Required |

## Content

| Field | Requirement |
|---|---|
| Title | Required |
| Post Content | Required |
| Author | Optional |
| Tags | Required / Empty Allowed |
| Published At | Required |

## Engagement

| Field | Requirement |
|---|---|
| Likes Count | Required |
| Saves Count | Required |
| Comments Count | Required |
| Engagement | Derived |

Formula：

```text
Engagement
=
Likes
+
Saves
+
Comments
```

---

# 2.4 Task A — Normalization

Examples：

```text
"1.2万"
↓
12000
```

Relative Time：

```text
"3小时前"
↓
Normalized Datetime
```

Tags：

```text
Trim
Remove #
Deduplicate
Normalize
```

原则：

```text
Raw
↓
Normalize
↓
Validate
```

---

# 2.5 Task A — Search Hit History

Post 去重以后仍然必须保留：

```text
Keyword
↔
Post
```

relationship。

Search Hit：

```text
Post ID
Source Keyword ID
Search At
Search Rank
Search Run ID
```

注意：

```text
Search Rank
=
Platform Search Result Position
```

不是：

```text
Candidate Rank
```

---

# 2.6 Task A — Engagement Observation

Engagement Data 不直接覆盖在 Post 上。

使用：

```text
Engagement Observation
```

Fields：

```text
Post ID
Observed At
Likes Count
Saves Count
Comments Count
Engagement
Data Quality
```

Initial Observation：

```text
Created by Task A
```

Future Observation：

```text
Appended by Task B
```

原则：

```text
Append
≠
Overwrite
```

---

# 2.7 Task A2 — Daily Basic Analysis Input

来源：

```text
Candidate Posts
```

使用：

- Post ID
- Title
- Content
- Tags
- Engagement Context

Basic Analysis Configuration 要求 AI 输出：

```text
Topic Classification
Short Summary
```

实现细节：

```text
Prompt
Model
JSON Schema
```

留到 Technology Mapping / Implementation。

---

# 2.8 Task A2 — Lawyer Review Input

Feishu 至少需要呈现：

- Post Identity
- Title
- Short Summary
- Topic Classification
- Engagement Context
- Link

律师执行：

```text
Keep
or
Reject
```

Keep 后：

```text
Confirmed Research Post
```

不是自动：

```text
Priority Tracking Post
```

---

# 2.9 Confirmed Research Pool

当前业务状态：

```text
Candidate
↓
Keep
↓
Confirmed Research
```

Confirmed Research Post 后存在两个独立判断：

```text
Tracking Required?
Deep Analysis Required Now?
```

两个都允许：

```text
Yes / No
```

一个 Yes 不要求另一个必须 Yes。

---

# 2.10 Task B — Tracking Target Input

进入 Task B：

```text
Confirmed Research Post
+
Tracking Required = Yes
```

需要：

### Post Identity

- Post ID
- URL
- Platform

### Previous Engagement History

至少：

```text
Initial Observation
```

### Tracking Configuration

```text
Minimum Interval = 7 days
```

### Tracking Run Context

- Tracking Run ID
- Run Time

---

# 2.11 Task B — Tracking Data Quality

Availability：

```text
Available
Deleted
Private
Temporarily Unavailable
Acquisition Failure
```

Data Quality：

```text
Valid
Incomplete
Missing
Invalid
Unavailable
```

注意：

```text
Tracking Attempt
≠
Engagement Observation
```

只有成功获得有效数据时才创建：

```text
Engagement Observation
```

失败时应记录：

```text
Tracking Attempt
+
Failure Reason
```

---

# 2.12 Task B — MVP Tracking Scope

当前：

```text
Initial Observation
+
One Follow-up Observation
```

完成后：

```text
Tracking Status = Completed
```

MVP 暂不实现：

- 无限 Weekly Tracking
- Advanced Trend Modeling
- Auto Continued Tracking
- Engagement Threshold Auto-priority

---

# 2.13 Task B → Task C Feedback Path

Task B 产生新的：

```text
Tracking Evidence
```

然后：

```text
Feishu Weekly Review
↓
Lawyer Re-evaluates Deep Analysis
```

因此：

```text
Deep Analysis = No
```

可以在新 Evidence 出现后变成：

```text
Deep Analysis = Yes
```

历史 Decision 不能覆盖。

---

# 2.14 Task C — Analysis Target Input

Task C 的入口不是：

```text
Priority Post
```

而是：

```text
Valid Deep Analysis Request
+
Confirmed Research Post
```

Request 可以来自：

```text
Daily Review
Post-Tracking Review
```

---

# 2.15 Task C — Post Data Input

### Required Identity

- Post ID
- URL
- Platform

### Required Core Content

- Title
- Post Content

### Required / Empty Allowed

- Tags

### Context

- Current Engagement
- Historical Engagement if available
- Basic Analysis if available

---

# 2.16 Task C — Content Sufficiency

Task A 允许：

```text
Post Content = Incomplete
```

但 Task C 对可靠性要求更高。

需要概念：

```text
Content Sufficiency
├── Sufficient
└── Insufficient
```

判断依据：

> 当前获取的信息是否足以可靠理解原帖实际表达。

注意：

```text
Short Content
≠
Incomplete Content
```

如果帖子本身很短但表达完整：

```text
Sufficient
```

如果正文被截断、核心信息缺失：

```text
Insufficient
```

AI 不应该在缺失关键内容时自行补全事实。

---

# 2.17 Task C — Deep Analysis Configuration

Task C 必须稳定产生以下 MVP 研究维度：

```text
Core Topic
User Problem
Legal Issue
Key Discussion Points
User Expressions
```

这些不是可有可无的分析项。

原因：

```text
Task D
Task F
Task G
```

都依赖这些字段。

它们共同形成：

```text
Structured Research Subject
```

---

# 2.18 Task C — Comment Analysis Requirement

律师只决定：

```text
Deep Analysis Required?
```

律师不需要再额外机械判断：

```text
Comment Analysis Required?
```

系统根据 Deep Analysis 任务需要决定：

```text
Comment Analysis Required
Boolean
Source = System / Business Rule
```

逻辑：

```text
False
→ Comment Data = Not Required

True
→ Comment Data = Conditional Required
```

---

# 2.19 Task C — Comment Input

当：

```text
Comment Analysis Required = True
```

Comment Fields：

| Field | Requirement |
|---|---|
| Comment ID | Required |
| Post ID | Required |
| Comment Text | Required |
| Comment Likes Count | Required |
| Comment Published At | Required |
| Comment Author | Optional |

Comment Selection：

```text
High Relevance
+
High Engagement
↓
Priority Selection
```

Maximum：

```text
Selected Comment Limit = Max 10
```

不是：

```text
Exactly 10
```

如果高质量评论只有 4 条：

```text
4 High-quality
+
Latest Valid Comments
↓
Up to 10
```

如果有效池只有 7：

```text
Analyze 7
```

---

# 2.20 Comment Retrieval vs Selection

必须区分：

```text
Total Comment Count
Retrieved Comment Count
Selected Comment Count
```

例如：

```text
Total = 386
Retrieved = 50
Selected = 10
```

`Comment Retrieval Limit`：

```text
TBD
```

因为依赖：

- Acquisition Method
- Pagination
- Rate Limit
- Cost
- Platform Limitation

---

# 2.21 Comment Data Quality

例如：

```text
Total Comment Count = 0
Retrieved = 0
```

表示：

```text
No Comments Exist
```

不是失败。

而：

```text
Total = 386
Retrieved = 0
```

可能表示：

```text
Acquisition Failure
Unavailable
Incomplete
```

因此：

```text
Empty
≠
Missing
≠
Unavailable
≠
Not Required
```

---

# 2.22 Task C — Idempotency

当前 MVP：

```text
Same Post
+
Same Valid Input State
+
Completed Deep Analysis
↓
Do Not Automatically Re-analyze
```

暂不引入：

- Content Version
- Comment Dataset Version
- Complex Analysis Versioning

未来如果：

- Author updates content
- Large number of new comments
- Analysis rules change
- Lawyer requests re-analysis

再设计 Re-analysis。

---

# 2.23 Task D — Long-tail Keyword Discovery Input

Task D 核心输入：

```text
Structured Research Subject
+
Original Post Data
+
Comment Analysis if available
```

包括：

- Title
- Post Content
- Tags
- Core Topic
- User Problem
- Legal Issue
- Key Discussion Points
- User Expressions
- Comment User Expressions if available

Comment Analysis：

```text
Optional
```

没有 Comment Analysis 不阻断 Task D。

---

# 2.24 Task D — Existing Keyword Data

Task D 需要知道已有：

```text
Official Seed Keyword Library
Existing Long-tail Candidates
```

原因：

```text
Discovered Expression
↓
Already Exists?
```

Exact duplicate / semantic duplicate rules：

```text
TBD
```

---

# 2.25 Task D — Analysis Window

Task D 使用：

> Since Previous Run 新完成的 Deep Analysis Results

而不是：

```text
Posts Published within Last 7 Days
```

原因：

旧帖子可能本周才：

- 被发现
- 完成 Track
- 被重新批准 Deep Analysis

---

# 2.26 Task D — Long-tail Candidate Data

每个 Candidate 至少保存：

```text
Candidate ID
Raw Expression
Normalized Concept
Potential Use[]
Occurrence Count
Distinct Post Count
Discovered At
Discovery Run ID
```

Potential Use：

```text
Search Keyword
Content Expression
Topic Signal
```

允许：

```text
Multiple Values
```

---

# 2.27 Task D — Source Evidence

不能只保存词。

必须保存：

```text
Expression
↓
Evidence[]
```

Evidence：

```text
Post ID
Source Type
Source Context
```

Source Type：

```text
Title
Post Content
Tag
Comment
AI Deep Analysis
```

---

# 2.28 Raw Expression vs Normalized Concept

例如：

```text
公司逼我自己辞职
公司逼着我辞职
老板就是想逼我走
公司想让我自己走
```

Raw Expressions 必须保留。

同时可以建立：

```text
Normalized Concept:
逼迫员工主动离职
```

原则：

> Normalization cannot replace the original user language.

---

# 2.29 Occurrence Evidence

必须区分：

```text
Occurrence Count
```

和：

```text
Distinct Post Count
```

例如：

```text
10 occurrences
from 1 post
```

与：

```text
10 occurrences
from 10 posts
```

属于不同 Signal。

Input 阶段只保存事实。

不规定：

```text
>= N
→ Good Keyword
```

---

# 2.30 Task D Responsibility Boundary

正式锁定：

```text
Task D
= Discover Expressions
```

不是：

```text
Task D
= Automatically add Seed Keywords
```

流程：

```text
Expression
↓
Long-tail Candidate
↓
Potential Use
↓
Task E
↓
Keyword Calibration
```

---

# 2.31 Task E — Seed Keyword Calibration Inputs

Task E 使用：

## Keyword Data

- Keyword ID
- Keyword
- Status
- Created At
- Updated At

Status：

```text
Candidate
Testing
Active
Observe
Retired
```

---

## Search Performance

- Search Run Count
- Search Hit History
- Search Hit Count
- Distinct Post Count

---

## Lawyer Feedback

- Candidate Count
- Keep Count
- Reject Count
- Research Retention Evidence

---

## Downstream Research Evidence

关联：

- Tracking Selection
- Tracking Result
- Deep Analysis Selection
- Deep Analysis Result
- Topic Relationships

MVP 不提前设计复杂评分公式。

---

## Engagement Evidence

- Initial Observation
- Follow-up Observation if available
- Growth / Trend if available

Engagement：

```text
Signal
≠
Final Decision
```

---

## Long-tail Candidate Evidence

来自 Task D：

- Raw Expression
- Normalized Concept
- Potential Use
- Source Evidence
- Occurrence Count
- Distinct Post Count

---

# 2.32 Task E — Calibration Period

主要按照：

```text
Search At
Workflow Run Time
```

评估本月 Keyword Performance。

不是单纯按照：

```text
Post Published At
```

---

# 2.33 Task E — Evidence Sufficiency

正式引入：

```text
Calibration Evidence Sufficiency
```

原则：

```text
Poor Performance
≠
Sufficient Evidence of Poor Performance
```

如果：

- Search Runs 太少
- Search Hits 太少
- Observation Period 太短

则：

```text
Insufficient Evidence
```

MVP：

> 不应基于不足数据做强烈 Status Change。

Exact minimum sample：

```text
TBD during Decision Analysis
```

---

# 2.34 Task E — Human Approval

系统产生：

```text
Current Status
Recommended Status
Recommendation Evidence
```

然后：

```text
Feishu
↓
Lawyer Approval
```

MVP 中：

> 所有 Keyword Status Changes 均需律师人工审批。

建议保存：

```text
System Recommended Status
Lawyer Final Decision
Reviewed At
```

---

# 2.35 Task F — Structured Research Subject

Task F 核心不是：

```text
Keyword → Case
```

而是：

```text
Structured Research Subject
→ Relevant Case
```

核心输入：

- Core Topic
- User Problem
- Legal Issue
- Key Discussion Points
- User Expressions

---

# 2.36 Task F — Optional Research Context

Optional：

- Tracking Evidence
- Engagement Trend
- Long-tail Signals
- Topic Signals

没有这些数据：

```text
Task F still runs
```

---

# 2.37 Task F — Structured Case Library

Source：

```text
Existing Case Library Pipeline
```

Current：

```text
Codex
↓
Structured Excel
```

Production：

```text
Structured Online-accessible Case Library
```

Exact Data Layer：

```text
TBD
```

Task F 不负责：

```text
Raw Judgment Processing
```

---

# 2.38 Task F — Case Schema Compatibility

不在这里凭空重建 Case Schema。

正式规则：

```text
Existing Excel Schema
↓
Integration Review
↓
Compare against Matching Requirements
↓
Reuse Existing Fields where possible
↓
Only add missing fields if genuinely required
```

Current Status：

```text
Case Library Excel Schema Compatibility
=
To Be Reviewed during Integration
```

---

# 2.39 Task F — Case Matching Dimensions

Business-level Matching Dimensions：

```text
User Problem Similarity
Legal Issue Similarity
Fact Pattern Similarity
Dispute Type Similarity
```

Exact：

- Weight
- Similarity threshold
- Embedding
- RAG
- Keyword logic

全部：

```text
TBD during Decision / Technology Mapping
```

---

# 2.40 Task F — No Match Handling

正式锁定：

```text
Relevant Case Found?
├── Yes
│   → Relevant Case Context
│
└── No
    → No Relevant Case
```

两者都可以：

```text
Continue to Task G
```

因此：

> Case Matching is an enhancement, not a mandatory gate.

---

# 2.41 Task G — Candidate Topic Generation Inputs

## Required

```text
Structured Research Subject
Business Direction Configuration
Topic Generation Configuration
```

## Optional

```text
Tracking / Trend Context
Long-tail / User Language
Relevant Case Context
```

---

# 2.42 Business Direction Configuration

Task G 必须知道目标业务方向。

Current：

```text
劳动争议
企业合规
经济纠纷
```

具体比例：

```text
TBD
```

该 Configuration 可未来调整，不需要修改 Workflow。

---

# 2.43 Topic Generation Configuration

Candidate Topic 至少应：

- 对应明确 User Problem
- 与业务方向相关
- 有 Research Evidence
- 有实际内容价值
- 能解释推荐依据

注意：

```text
Topic Generation
≠
Title Generation
```

本阶段回答：

> What should we talk about?

不是：

> Final cover/title copy.

---

# 2.44 Recommendation Evidence

Candidate Topic 应可回溯：

```text
Research Subject
Source Posts
Trend Evidence if available
Long-tail Evidence if available
Relevant Cases if available
```

目的：

> Avoid black-box recommendation.

---

# 2.45 One Research Subject → Multiple Candidate Topics

正式锁定：

```text
1 Research Subject
→ 0..N Candidate Topics
```

不规定每个 Research Subject 必须生成固定数量。

如果无价值：

```text
0
```

如果存在多个不同角度：

```text
N
```

例如：

- Employee Perspective
- Employer Compliance Perspective
- Case Perspective
- Myth / Misunderstanding Perspective

---

# 2.46 Task G — Lawyer Final Approval

```text
Candidate Topics
↓
Feishu
↓
Lawyer
├── Approve
└── Reject
```

最终：

```text
Approved Content Topics
```

脚本生成：

```text
Out of MVP Scope
```

---

# 2.47 Cross-workflow Input Review

完成 A–G Input 后进行全局 Review。

最终确认：

## Finding 1

```text
Keep
≠
Track
≠
Deep Analysis
```

---

## Finding 2

Task C 有两个入口：

```text
Daily Review
Post-Tracking Review
```

---

## Finding 3

需要：

```text
Confirmed Research State
```

---

## Finding 4

Task C 必须稳定输出：

```text
Core Topic
User Problem
Legal Issue
Key Discussion Points
User Expressions
```

---

## Finding 5

统一共享对象：

```text
Structured Research Subject
```

供：

```text
Task D
Task F
Task G
```

消费。

---

## Finding 6

必须永久保留：

```text
Keyword
↔
Post
```

Search Hit Relationship。

Post Deduplication 不得删除这层关系。

---

## Finding 7

Case Library 是：

```text
External / Upstream Structured Data Dependency
```

不是本项目需要重新建设的 Pipeline。

---

# 2.48 Data Contract Review

当前 MVP 定义以下 Logical Data Objects。

---

## Object 1 — Seed Keyword

```text
Seed Keyword
├── Keyword ID
├── Keyword
├── Status
├── Created At
└── Updated At
```

Owner：

```text
Keyword Library
```

Consumers：

```text
Task A
Task E
```

Rule：

```text
Retired
≠
Deleted
```

---

## Object 2 — Post

Persistent Entity。

```text
Post
├── Post ID
├── Platform
├── URL
├── Title
├── Post Content
├── Author
├── Tags
└── Published At
```

Created by：

```text
Task A
```

Rule：

```text
Same Post
=
One Persistent Object
```

---

## Object 3 — Search Hit

Relationship / Event：

```text
Search Hit
├── Post ID
├── Source Keyword ID
├── Search At
├── Search Rank
└── Search Run ID
```

Created by：

```text
Task A
```

Primary Consumer：

```text
Task E
```

Rule：

```text
Deduplicate Post
≠
Delete Search Hit Relationship
```

---

## Object 4 — Engagement Observation

Time-specific Snapshot：

```text
Engagement Observation
├── Post ID
├── Observed At
├── Likes
├── Saves
├── Comments
├── Engagement
└── Data Quality
```

Created by：

```text
Task A
Task B
```

Rule：

```text
Append
≠
Overwrite
```

---

## Object 5 — Basic Analysis

```text
Basic Analysis
├── Post ID
├── Topic Classification
├── Short Summary
├── Analysis At
└── Analysis Quality
```

Created by：

```text
Task A2
```

Consumers：

```text
Feishu Daily Review
Task C as Context
```

Rule：

```text
Basic Analysis
≠
Deep Analysis
```

---

## Object 6 — Research Post / Research State

```text
Research Post
├── Post ID
├── Research Status
├── Confirmed At
└── Confirmed By
```

Current conceptual states：

```text
Confirmed
Archived
```

Rule：

```text
Confirmed Research
≠
Tracking Priority
≠
Deep Analysis Required
```

---

## Object 7 — Lawyer Decision

共享历史 Decision Object：

```text
Lawyer Decision
├── Decision ID
├── Target Type
├── Target ID
├── Decision Type
├── Decision Value
├── Decided At
└── Decision Context
```

Decision Types may include：

```text
Keep
Track
Deep Analysis
Keyword Status Approval
Topic Approval
```

Rule：

```text
New Decision
≠
Overwrite Historical Decision
```

例如：

```text
Sep 1
Deep Analysis = No

Sep 8
Deep Analysis = Yes
```

两条都保留。

---

## Object 8 — Deep Analysis Request

```text
Deep Analysis Request
├── Request ID
├── Post ID
├── Source Decision ID
├── Requested At
├── Request Source
└── Status
```

Request Source：

```text
Daily Review
Post-Tracking Review
```

Status：

```text
Pending
Completed
Failed
```

---

## Object 9 — Structured Research Subject

Task C 的核心共享 Output Contract：

```text
Structured Research Subject
├── Research Subject ID
├── Post ID
├── Core Topic
├── User Problem
├── Legal Issue
├── Key Discussion Points
├── User Expressions
├── Analysis At
└── Data Quality
```

Consumers：

```text
Task D
Task F
Task G
```

Rule：

> Downstream workflows reuse this object instead of independently re-understanding the same post.

---

## Object 10 — Long-tail Keyword Candidate

```text
Long-tail Keyword Candidate
├── Candidate ID
├── Raw Expression
├── Normalized Concept
├── Potential Use[]
├── Occurrence Count
├── Distinct Post Count
├── Discovered At
└── Discovery Run ID
```

Evidence：

```text
Source Evidence[]
├── Post ID
├── Source Type
└── Source Context
```

Rule：

```text
Long-tail Candidate
≠
Seed Keyword
```

---

## Object 11 — Candidate Topic

```text
Candidate Topic
├── Topic ID
├── Research Subject ID
├── Topic / Content Angle
├── Recommendation Evidence
├── Generated At
└── Generation Run ID
```

Relationship：

```text
1 Research Subject
→
0..N Candidate Topics
```

Final approval通过：

```text
Lawyer Decision
```

实现，不需要另建完全独立 Approved Topic Object。

---

## Object 12 — Case Record

External / Upstream Object。

Source：

```text
Existing Case Library Pipeline
```

本项目：

```text
Read / Consume
```

不负责：

```text
Create / Own Judgment Processing
```

具体 Schema：

```text
TBD after reviewing current Excel structure
```

至少要求：

```text
Stable Case Identifier
+
Enough Structured Matching Data
+
Accessible Current Case Library
```

---

## Object 13 — Workflow Run Context

```text
Workflow Run
├── Run ID
├── Workflow Type
├── Started At
├── Completed At
└── Run Status
```

用于关联：

- Search Hits
- Tracking Attempts
- Long-tail Discovery
- Keyword Calibration
- Case Matching
- Topic Generation

---

# 2.49 Core Data Design Principles

## Principle 1 — Entity ≠ Event ≠ State ≠ Decision

例如：

```text
Post
= Entity

Engagement Observation
= Snapshot / Event

Confirmed Research
= Business State

Keep
= Human Decision
```

不要全部混成 Post 字段。

---

## Principle 2 — Preserve History

以下数据优先 Append：

```text
Search Hits
Engagement Observations
Lawyer Decisions
Tracking Attempts
```

而不是覆盖。

---

## Principle 3 — Deduplicate Entity, Preserve Relationships

```text
Post
only one object

Keyword A → Post
Keyword B → Post
```

两条关系都必须保留。

---

## Principle 4 — Downstream Requirements Validate Upstream Contracts

例如：

```text
Task D
Task F
Task G
```

都需要：

```text
Core Topic
User Problem
Legal Issue
Key Discussion Points
User Expressions
```

因此反向锁定：

```text
Task C Output Contract
```

---

## Principle 5 — Optional Context Must Not Become a Gate

以下均属于 enhancement：

```text
Tracking Evidence
Long-tail Evidence
Relevant Case
```

缺少其中任一项：

```text
Task G can still run
```

---

## Principle 6 — Human Decision Is Data

律师的：

- Keep
- Reject
- Track
- Deep Analysis
- Keyword Approval
- Topic Approval

都需要保存。

未来可用于：

- AI Evaluation
- Keyword Calibration
- Recommendation Evaluation
- Workflow Optimization

---

# 2.50 Current Input Analysis Status

```text
Business Problem Analysis        ✓
Trigger Analysis                 ✓

Task A Input                     ✓
Task A2 Input                    ✓
Task B Input                     ✓
Task C Input                     ✓
Task D Input                     ✓
Task E Input                     ✓
Task F Input                     ✓
Task G Input                     ✓

Cross-workflow Input Review      ✓
Data Contract Review             ✓
```

Status：

```text
DAY 03 INPUT ANALYSIS
COMPLETED FOR CURRENT MVP v1
```

Important：

> Completed for Current MVP v1 does not mean permanently frozen.

Future Process / Decision / Implementation may reveal genuine missing requirements.

Then:

```text
Input v1
↓
Input v1.1
```

is acceptable.

---

# 3. Process Analysis — Day 04 Preview

> How does the system transform valid Inputs into usable Results?

Day 04 将采用 Horizontal Review：

```text
Task A Process
↓
Task A2 Process
↓
Task B Process
↓
Task C Process
↓
Task D Process
↓
Task E Process
↓
Task F Process
↓
Task G Process
↓
Cross-workflow Process Review
```

而不是完成 Task A 的全部：

```text
Input
Process
Decision
Action
Output
```

再进入 Task B。

---

## 3.1 Task A Preliminary Process

当前预览：

```text
Valid Collection Inputs
↓
Search
↓
Retrieve Raw Result Pool
↓
Normalize
↓
Validate
↓
Time / Quality Filter
↓
Deduplicate Posts
↓
Preserve Search Hit Relationships
↓
Evaluate Relevance
↓
Calculate Engagement
↓
Rank Candidate Results
↓
Select Max 5
↓
Store Candidate Posts
↓
Store Search Hit History
↓
Store Initial Engagement Observation
↓
Task A Complete
```

Exact：

- Raw Retrieval Limit
- Relevance Formula
- Ranking Formula
- Error Path
- Retry
- Storage Technology

全部留到 Day 04 / Decision / Technology Mapping。

---

# 4. Decision Analysis — Future

Day 04 Process 完成后再进入 Decision。

需要重点设计：

- Candidate Selection Rules
- Relevance Evaluation
- Tracking Selection Rules
- Comment Requirement Decision
- Comment Selection Rules
- Keyword Calibration Rules
- Evidence Sufficiency Rules
- Case Matching Relevance
- Candidate Topic Value Rules

原则：

```text
Signal
≠
Decision
```

---

# 5. Action Analysis — Future

需要回答：

> Decision 之后系统具体执行什么动作？

Examples：

- Save
- Archive
- Send to Feishu
- Add to Queue
- Update Status
- Request Approval
- Trigger Downstream Workflow
- Retry
- Alert

---

# 6. Output Analysis — Future

需要设计：

- Daily Feishu Review Output
- Tracking Review Output
- Deep Research Output
- Weekly Long-tail Output
- Monthly Keyword Calibration Output
- Case Matching Output
- Candidate Topic Output

并最终进入：

```text
User Story
Acceptance Criteria
PRD v1
```

---

# 7. Technology Mapping — Future

只有完成 Business / Workflow Design 后再决定：

- JSON
- HTTP
- REST API
- Authentication
- Webhook
- n8n
- Python
- Database
- Cloud Runtime
- Case Library Online Data Layer
- Feishu Integration
- LLM
- Structured Output
- RAG if genuinely required
- Embedding / Vector Search if genuinely required
- Logging
- Monitoring
- Error Handling

核心原则：

> Business Requirement First, Technology Second.