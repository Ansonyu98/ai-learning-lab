# Day 07 — Action & Output Analysis

## Today's Goal

目前已经完成：

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

Day 07 进入：

Action
+
Output

核心问题：

> Once a decision is made, what should the system do?

以及：

> What should be produced for humans or downstream workflows?

---

# 1. Decision vs Action

Decision：

判断结果是什么？

例如：

Deep Analysis = Yes

Action：

系统因此执行什么？

例如：

Persist Decision
↓
Create Deep Analysis Request

因此：

Decision
≠
Action

---

# 2. Full Transformation Model

今天建立：

Process
↓
Decision
↓
Action
↓
State Change
↓
Output
↓
Downstream Workflow

Example:

Candidate Post
↓
Lawyer:
Track = Yes
↓
Persist Decision
↓
Create Tracking State
↓
Tracking Request / Future Eligibility
↓
Task B

---

# 3. Task A Actions

Task A 主要 Actions：

Keyword Eligible
→ Execute Search

New Post
→ Create Post Entity

Existing Post
→ Reuse Existing Entity

Valid Search Relationship
→ Create Search Hit

Candidate Selected
→ Create / Update Candidate State

Metrics Collected
→ Append Engagement Observation

---

# 4. Task A Outputs

Business Output：

Candidate Batch
+
Search Hit Relationships
+
Initial Engagement Observations

Operational Output：

Collection Run Result
+
Failure Summary
+
Run Status

今天正式区分：

> Business Output ≠ Operational Output

---

# 5. Task A2 Actions

Candidate Ready
↓
Run Basic AI Analysis
↓
Persist Topic Classification
↓
Persist Short Summary
↓
Create Review Item
↓
Aggregate Daily Review Package
↓
Deliver to Feishu
↓
Record Delivery Status

---

# 6. Lawyer Decision Actions

Keep = No:

Persist Decision
↓
Research State = Rejected
↓
No downstream research trigger

Keep = Yes:

Persist Decision
↓
Research State = Confirmed / Priority

然后读取：

Track?
Deep Analysis?
Comment Analysis?

---

# 7. Tracking Action

Track = Yes:

Create Tracking State / Request
↓
Calculate Due Context
↓
Make Post eligible for future Task B

Track = No:

No Tracking Request

---

# 8. Deep Analysis Action

Deep Analysis = Yes:

Create Deep Analysis Request
↓
Task C eligible

Comment Analysis：

作为 Deep Analysis Request 的 Configuration：

Comment Analysis Required = Yes / No

而不是单独启动一个 Comment Workflow。

---

# 9. Task B Actions

Tracking Due
↓
Fetch Current Post State
↓
Append 7-Day Observation
↓
Generate Tracking Evidence
↓
Update Tracking State
↓
Create Tracking Review Item

如果律师重新判断：

Deep Analysis:
No → Yes

则：

Append New Lawyer Decision
↓
Create Deep Analysis Request
↓
Task C Eligible

不能覆盖旧 Decision。

---

# 10. Task C Actions

Valid Deep Analysis Request
↓
Load Context
↓
Check Comment Requirement
↓
Collect / Select Comments if needed
↓
Run Deep Analysis
↓
Validate Structured Output
↓
Create Structured Research Subject
↓
Link Evidence
↓
Persist AI Provenance
↓
Mark Complete

---

# 11. Task D Actions

Research Subjects
↓
Extract User Expressions
↓
Preserve Raw Expression
↓
Normalize
↓
Cluster
↓
Count
↓
Create / Update Long-tail Candidate
↓
Link Source Evidence

重复出现的 Candidate：

Update Evidence

而不是：

Create Duplicate Candidate

---

# 12. Task E Actions

Monthly Evidence
↓
Generate Calibration Recommendation
↓
Persist Recommendation
↓
Create Review Item
↓
Deliver to Feishu

到这里系统不能直接修改 Keyword Library。

只有：

Lawyer Approves
↓
Append Keyword Lifecycle History
↓
Update Current Keyword State
↓
Update Future Search Configuration

---

# 13. Task F Actions

Research Subject
↓
Retrieve Candidate Cases
↓
Evaluate Relevance
↓
Create Case Match Relationship

如果没有：

Persist:
No Relevant Case

不能什么都不记录。

---

# 14. Task G Actions

Eligible Research Subjects
↓
Load Available Evidence
↓
Generate Candidate Topics
↓
Validate
↓
Semantic Deduplicate
↓
Link Topic to Evidence
↓
Persist
↓
Create Topic Review Items
↓
Aggregate Weekly Package
↓
Deliver to Feishu

Lawyer Approve:

Topic State = Approved
↓
Approved Topic Pool

Lawyer Reject:

Topic State = Rejected

Reject 不删除 Topic History。

---

# 15. Feishu Output Architecture

今天进一步明确：

Feishu
≠
Notification Only

而是：

Human Interaction Layer

承担：

- Review
- Decision
- Reporting
- Research Output
- Operational Visibility

---

# 16. Daily Feishu View

回答：

> 今天收集到了什么？

内容：

- Collection Summary
- Topic Distribution
- Candidate Posts
- Basic AI Summary
- Engagement
- Lawyer Review Actions

---

# 17. Weekly Tracking View

回答：

> 上周值得观察的帖子后来怎么样？

内容：

- Initial Engagement
- 7-Day Engagement
- Growth Evidence
- Previous Decision
- Re-evaluation

---

# 18. Weekly Research View

回答：

> 本周最终研究出了什么？

可能包括：

- Research Subjects
- Long-tail Findings
- Relevant Cases
- Candidate Topics
- Topic Approval

---

# 19. Monthly Keyword View

回答：

> 搜索系统本月表现如何？

内容：

- Keyword Performance
- Search Evidence
- Lawyer Keep / Reject
- Research Outcomes
- Long-tail Evidence
- System Recommendation
- Lawyer Approval

---

# 20. Workflow Output vs User-facing Output

Task D / F / G 可以分别产生并保存 Output。

但是不应该：

Task D → 一条飞书
Task F → 一条飞书
Task G → 一条飞书

更合理：

Persist Individual Outputs
↓
Aggregate
↓
Weekly Research Package
↓
Feishu

核心：

> Workflow Outputs can be independent while user-facing outputs are aggregated.

---

# 21. Operational Output

系统还需要：

Workflow Health

例如：

- API Failure
- AI Failure
- Feishu Delivery Failure
- Database Failure
- Case Library Unavailable

但是正常情况下不应该每天给律师展示：

API 200
Node Success
Workflow Completed

只有：

Meaningful Operational Exception

才需要明显提醒。

---

# 22. Cross-workflow Action Types

今天发现整个系统的 Action 可以归纳为：

CREATE
- Post
- Review Item
- Tracking Request
- Deep Analysis Request
- Candidate Topic

UPDATE
- Current State
- Current Configuration
- Delivery Status

APPEND
- Observation
- Decision History
- Keyword Lifecycle History

LINK
- Post ↔ Keyword
- Research Subject ↔ Post
- Topic ↔ Evidence
- Case ↔ Research Subject

DELIVER
- Daily Review
- Weekly Review
- Monthly Review
- Operational Alert

TRIGGER
- Deep Analysis
- Future Tracking
- Human Decision Continuation

---

# 23. Five Output Layers

整个系统最终不只是：

“10个选题”

而是形成五层 Output。

Layer 1 — Raw / Normalized Data

- Posts
- Search Hits
- Engagement Observations
- Comments

Layer 2 — AI Intelligence

- Basic Analysis
- Topic Classification
- Structured Research Subjects
- Long-tail Candidates
- Case Matches
- Candidate Topics

Layer 3 — Human Judgment

- Keep / Reject
- Track
- Deep Analysis
- Comment Analysis
- Keyword Approval
- Topic Approval

Layer 4 — Business Assets

- Research Pool
- Keyword Library
- Approved Topic Pool
- Case-linked Evidence
- Research History

Layer 5 — Operational Evidence

- Workflow Runs
- Failures
- Retry
- Delivery Status
- AI Provenance
- Decision History

---

# 24. End-to-end Traceability

今天新增重要 Cross-workflow Requirement：

> End-to-end Traceability

Candidate Topic 应该能够反查：

Candidate Topic
↓
Research Subject
↓
Post
↓
Search Hit
↓
Keyword

如果使用：

Comment
Tracking Evidence
Case

也应该能够知道：

Topic
↓
Which Evidence?

这对于：

- Lawyer Review
- Debug
- AI Evaluation
- Future Productization
- Portfolio

都非常重要。

---

# 25. Action Safety Principles

今天冻结几个 Action Principle：

Reject
≠
Delete

AI Failure
≠
Delete

Post Unavailable
≠
Delete

Keyword Retired
≠
Delete

同时：

AI Recommendation
≠
Automatic Production Configuration Change

关键配置仍需 Human Approval。

---

# 26. Key Mindset Change

Day 07 从：

“What does the workflow decide?”

进入：

“What concrete business state should change after that decision?”

同时开始认识：

Output
≠
A final report only

一个成熟 Automation System 的 Output 还包括：

Data
State
History
Evidence
Human Decision
Business Asset
Operational Evidence

---

# 27. Day 07 Deliverables

✅ Decision → Action Mapping
✅ State Change
✅ Task A Actions / Outputs
✅ Task A2 Actions / Outputs
✅ Lawyer Decision Actions
✅ Tracking Actions
✅ Deep Analysis Actions
✅ Task B Actions
✅ Task C Actions
✅ Task D Actions
✅ Task E Actions
✅ Task F Actions
✅ Task G Actions
✅ Feishu Output Architecture
✅ Daily / Weekly / Monthly Views
✅ Business vs Operational Output
✅ User-facing Output Aggregation
✅ Cross-workflow Action Types
✅ Five Output Layers
✅ End-to-end Traceability
✅ Action Safety Principles

---

# 28. Next Step — Day 08

Next:

> Product + Technical Design / MVP Design Freeze

核心问题：

业务 Workflow 已经基本完成。

下一步：

How should this workflow become a real system?

包括：

- Functional Requirements
- Non-functional Requirements
- System Architecture
- Data Layer
- AI Layer
- Feishu Layer
- Technology Mapping
- Cloud Execution
- MVP Boundary
- Build Sequencing