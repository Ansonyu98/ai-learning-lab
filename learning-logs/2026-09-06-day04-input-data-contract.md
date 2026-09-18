# Day 04 — Cross-workflow Input Analysis & Data Contract

## Date

2026-08-28

---

## Today's Goal

Day 03 已经完成：

Business Problem
↓
Trigger
↓
Input Analysis 基础

Day 04 的目标不是马上进入技术实现，而是把 Input Analysis 从 Task A 扩展到整个 Workflow，并建立统一的 Data Contract。

核心学习路径：

Task-level Input Analysis
↓
Cross-workflow Input Review
↓
Data Contract Review
↓
Prepare for Process Analysis

真实项目：

> AI-powered Legal Content Research & Topic Discovery Workflow

核心原则：

> Before designing how data is processed, first make sure every workflow receives usable, traceable and consistent data.

---

# 1. Why Continue Input Analysis?

Day 03 已经理解：

> Input 不只是“有哪些字段”。

还包括：

- Source
- Requirement
- Data Type
- Normalization
- Validation
- Missing Handling
- Freshness
- History

但如果只分析 Task A，还不能保证整个 Workflow 能连接起来。

因此 Day 04 开始考虑：

> Task A 的 Output 能不能成为后续 Task 的 Input？

也就是：

Upstream Output
↓
Downstream Input

必须能够连接。

---

# 2. Workflow Structure Refinement

随着 Input Analysis 深入，项目 Workflow 被进一步拆分为：

Task A
Search & Collection

Task A2
Basic AI Analysis + Daily Lawyer Review

Task B
7-Day Priority Post Tracking

Task C
Deep Analysis

Task D
Long-tail Keyword Discovery

Task E
Keyword Calibration

Task F
Case Library Matching

Task G
Candidate Topic Generation

其中新增 Task A2 的原因是：

> Daily Collection 和 Deep Analysis 不应该混在一起。

Daily Workflow 的主要目的应该是：

Collection
↓
Basic AI Processing
↓
Lawyer Review

而不是每天对所有 Candidate Post 做 Deep Analysis。

---

# 3. Daily Workflow Clarification

今天重新明确：

每天真正需要执行的是：

Scheduled Search
↓
Post Collection
↓
Normalization
↓
Validation
↓
Deduplication
↓
Candidate Selection
↓
Basic AI Analysis
↓
Topic Classification
↓
Short Summary
↓
Feishu Daily Review
↓
Lawyer Review

律师主要判断：

- Keep / Reject
- Track?
- Deep Analysis?
- Comment Analysis?

因此：

> Daily = Data Collection + Basic Intelligence + Human Triage

而：

> Deep Analysis ≠ Daily Mandatory Workflow

这是今天非常重要的 Workflow Boundary 调整。

---

# 4. AI vs Lawyer Responsibility

之前容易把：

Topic Classification
+
Business Value Judgment

混在一起。

今天进一步明确：

AI 负责：

- Topic Classification
- Basic Summary
- Semantic Understanding
- First-pass Analysis

律师负责：

- 是否值得留下
- 是否值得继续 Tracking
- 是否值得 Deep Analysis
- 是否需要 Comment Analysis

因此：

AI:
“What is this post about?”

Lawyer:
“Is this worth further attention?”

两者解决不同问题。

---

# 5. Priority Pool Logic

今天进一步明确 Priority Pool 和 Engagement 的关系。

不能简单：

Engagement > 500
↓
Priority Pool

因为高互动帖子可能：

- 与律师业务无关
- 不符合内容方向
- 没有进一步研究价值

因此：

Engagement
=
Evidence / Signal

而：

Priority Pool
=
Lawyer-confirmed Research State

正式逻辑：

Candidate Post
↓
System Evidence
↓
Lawyer Review
↓
Worth Keeping / Further Research
↓
Priority Pool

---

# 6. Priority Pool vs Deep Analysis

进一步明确：

允许进入 Task C Deep Analysis 的 Post：

> 必须属于 Priority Pool。

但是：

Priority Pool
≠
所有帖子都必须 Deep Analysis

关系：

Deep Analysis Posts
⊂
Priority Pool

例如：

Post A
Keep = Yes
Track = Yes
Deep Analysis = No

它仍然可以属于 Priority Pool，但暂时不进行 Deep Analysis。

---

# 7. Task B — 7-Day Tracking Input

Tracking 的核心 Input 不是只有：

Post ID

还需要：

- Initial Engagement Observation
- Initial Observed At
- Likes
- Saves
- Comments Count
- Engagement
- Tracking Approval
- Tracking Eligibility / State

Tracking Time：

> 7 Days

核心结构：

Initial Observation
↓
Wait until Tracking Due
↓
Fetch Current State
↓
Create New Engagement Observation
↓
Compare

Tracking 依赖 Historical Observation，而不是覆盖 Current State。

---

# 8. Re-evaluation After Tracking

今天确认一个重要业务规则：

第一次律师判断：

Deep Analysis = No

并不意味着：

Never Deep Analyze

例如：

Day 0:

Engagement = 600
Deep Analysis = No
Track = Yes

Day 7:

Engagement = 8,000

新数据形成新的 Evidence。

因此：

7-Day Tracking
↓
New Evidence
↓
Lawyer Re-evaluation
↓
Deep Analysis may change:
No → Yes

核心学习：

> Decisions can be revisited when new evidence appears.

---

# 9. Task C — Deep Analysis Input

Task C 不应该自动分析所有 Candidate Post。

Task C 的主要 Input：

- Priority Post
- Lawyer Deep Analysis Approval
- Post Content
- Basic Analysis
- Topic Classification
- Existing Engagement Evidence
- Comment Analysis Decision

核心 Precondition：

Lawyer Deep Analysis Approval = Yes

---

# 10. Comment Analysis Input

今天进一步明确：

Comment Analysis 不是独立 Daily Workflow。

它属于：

> Deep Analysis Configuration

律师先判断：

Comment Analysis Required?

如果：

No
↓
Analyze Post Only

如果：

Yes
↓
Collect / Select Comments
↓
Deep Analysis

评论选择规则：

优先：

High-like
+
High relevance to original post

选择：

Top 10

如果无法获得足够的高赞 / 高关联评论：

Fallback:
Latest 10

---

# 11. Why Lawyer Decides Comment Analysis?

有些 Post：

正文已经完整表达核心问题。

评论可能只是：

- 蹲后续
- +1
- 我也是
- 情绪表达

此时 Comment Analysis 价值较低。

但有些 Post：

正文很短，
真正的用户问题集中在评论区。

因此：

> Comment Analysis should be driven by research value, not automatically triggered for every post.

MVP 由律师人工决定。

---

# 12. Task C Output as Downstream Input

Deep Analysis 最终不应该只输出一段自由文本。

后续 Task D / F / G 都需要消费 Task C 的结果。

因此 Task C 应该输出：

Structured Research Subject

可能包含：

- Core Topic
- User Problem
- Legal / Business Issue
- User Expressions
- Discussion Points
- Selected Comment Evidence
- Source Post Reference

核心思想：

> AI Output should become reusable structured data.

---

# 13. Task D — Long-tail Keyword Discovery Input

Task D 的 Input 主要来自：

Structured Research Subjects

特别关注：

- User Expressions
- Repeated User Language
- Topic Context
- Source Evidence

目标不是让 AI 随机生成关键词。

而是：

Real User Language
↓
Extraction
↓
Normalization
↓
Semantic Clustering
↓
Long-tail Keyword Candidate

需要保留：

Raw Expression

因为：

> Normalized Keyword 不应该替代真实用户原始表达。

---

# 14. Task E — Keyword Calibration Input

Keyword Calibration 不能只看：

Search Volume

还需要结合：

- Search Hit Evidence
- Candidate Results
- Lawyer Keep / Reject
- Priority Research Outcomes
- Deep Analysis Outcomes
- Long-tail Evidence
- Topic Outcomes

因此 Keyword Performance 应该逐步从：

“How much did this keyword find?”

升级为：

“Did this keyword actually produce useful research and content opportunities?”

---

# 15. Task F — Case Library Matching Input

目前已经存在真实 Case Library Workflow：

Judgment Documents
↓
Codex
↓
Structured Processing
↓
Unified Excel Case Library

因此 Task F 不需要重新设计案例整理逻辑。

未来 Input 可以来自：

Structured Case Library

Task F 需要：

Research Subject
+
Case Library

然后进行：

Candidate Case Retrieval
↓
Relevance Assessment
↓
Case Match Result

同时明确：

No Relevant Case
=
Valid Result

而不是 Workflow Failure。

---

# 16. Case Library Future Direction

当前案例库仍然是：

Local Excel

但未来为了让 Automation 脱离本地电脑运行，需要考虑：

Local Structured Case Library
↓
Online Structured Data
↓
Automation Access

具体技术：

Database
Search
Embedding
Vector Database
RAG

暂时不决定。

留到 Technology Mapping。

---

# 17. Task G — Candidate Topic Generation Input

Candidate Topic Generation 不应该依赖单一 Post。

可使用：

Required:
Structured Research Subject

Optional:
Tracking Evidence
Long-tail Evidence
Relevant Case Context
Comment Evidence

重要原则：

> Optional enrichment should improve Topic Generation, but should not unnecessarily block it.

例如：

No Relevant Case

不能导致：

No Candidate Topic

---

# 18. Cross-workflow Input Review

今天第一次从整个 Workflow 检查：

Task A Output
↓
Task A2 Input

Task A2 / Lawyer Decision
↓
Task B / C Input

Task C Output
↓
Task D / F / G Input

Task D / F Output
↓
Task G Input

System Evidence
↓
Task E Input

核心问题：

> Can every downstream workflow clearly identify what it needs from upstream?

---

# 19. Data Contract

今天开始建立：

> Data Contract

Data Contract 的作用：

确保不同 Workflow 对同一个数据对象有统一理解。

例如 Post ID：

不能：

Task A:
Integer

Task B:
String

Task C:
Different ID

而应该统一。

Data Contract 至少需要定义：

- Field Name
- Meaning
- Data Type
- Required / Optional
- Nullable
- Source
- Normalization
- Validation
- History Requirement
- Downstream Usage

---

# 20. Core Shared Data Objects

今天识别出一批 Cross-workflow Shared Objects：

- Keyword
- Post
- Search Hit
- Engagement Observation
- Basic Analysis
- Review Item
- Lawyer Decision
- Tracking Evidence
- Deep Analysis Request
- Research Subject
- Comment
- Long-tail Candidate
- Case
- Case Match
- Candidate Topic

这些对象未来会成为：

Database Design

的重要基础。

---

# 21. Event Data vs State Data

今天进一步理解：

有些数据表示：

Current State

例如：

Current Keyword Status

有些数据表示：

Event / History

例如：

Lawyer Decision
Engagement Observation

对于需要追踪变化的数据，不应该简单覆盖。

推荐：

New Event
↓
Append History
↓
Update Current State if needed

例如：

Deep Analysis Decision:

Day 0 = No
Day 7 = Yes

应该知道：

Decision changed

而不是数据库里只剩：

Yes

---

# 22. Feishu Role Clarification

今天进一步明确：

飞书不只是 Daily Push。

未来：

Daily
↓
Collection Review

Weekly
↓
Research / Topic Review

Monthly
↓
Keyword Calibration Review

律师通过飞书完成关键 Human-in-the-loop Decisions。

因此：

Feishu
=
Human Interaction Layer

而不是：

Feishu
=
Simple Notification Tool

---

# 23. Cloud Execution Requirement

今天加入一个重要业务需求：

> 系统搭建完成后，不应该依赖每天打开本地电脑才能运行。

因此未来：

Scheduled Workflow
↓
Cloud Execution

本地电脑：

OFF

系统仍然：

RUNNING

这会直接影响：

- Automation Hosting
- Database
- Case Library Access
- Scheduler
- API Integration

具体技术方案留到 Technology Mapping。

---

# 24. Key Mindset Change

Day 04 最大的变化是：

从：

“每个 Task 自己需要什么数据？”

升级到：

“整个系统的数据能不能连续流动？”

也就是：

Task-level Input
↓
Cross-workflow Contract
↓
Shared Data Objects
↓
Reusable Structured Outputs
↓
Historical State
↓
Human Decisions
↓
Downstream Eligibility

开始从单个 Automation Task 思维，进入：

> System Workflow Thinking

---

# 25. Day 04 Deliverables

✅ Daily Workflow Boundary Clarified
✅ Task A2 Introduced
✅ AI / Lawyer Responsibility Clarified
✅ Priority Pool Logic Refined
✅ Priority Pool vs Deep Analysis Defined
✅ Task B Tracking Input
✅ 7-Day Tracking Rule
✅ Post-tracking Re-evaluation
✅ Task C Deep Analysis Input
✅ Comment Analysis Input
✅ Comment Selection Rule
✅ Structured Research Subject
✅ Task D Input
✅ Task E Input
✅ Task F Input
✅ Task G Input
✅ Cross-workflow Input Review
✅ Data Contract Review
✅ Shared Data Objects
✅ Event vs State Data
✅ Feishu Human Interaction Role
✅ Cloud Execution Requirement

---

# 26. Next Step — Day 05

Next:

> Process Analysis

核心问题：

We already know:

Trigger
+
Input
+
Data Contract

↓

What exactly happens after the workflow starts?

重点学习：

- Process Boundary
- Step Sequence
- Batch
- Loop
- Transformation
- Persistence
- State Change
- Idempotency
- Error Path
- Retry
- Partial Success