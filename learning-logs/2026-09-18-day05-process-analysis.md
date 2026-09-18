# Day 05 — Process Analysis

## Today's Goal

Day 01–04 已经完成：

Business Problem
↓
Trigger
↓
Input
↓
Cross-workflow Data Contract

Day 05 正式进入：

> Process Analysis

核心问题：

> After a workflow is triggered and receives valid inputs, what exactly happens?

今天不讨论具体 n8n Node，也不决定具体代码。

目标是先把 Business Process 设计正确。

---

# 1. What is Process?

Process 描述：

> Workflow 如何把 Input 转换成下一阶段可以使用的结果。

基本结构：

Input
↓
Step
↓
Transformation
↓
State Change / Persistence
↓
Next Step

Process 不是：

Technology Implementation

例如：

“调用 API 获取帖子”

属于 Process。

但：

“使用 n8n HTTP Request Node”

属于 Implementation。

---

# 2. Process Analysis Framework

今天使用以下框架：

Process
├── Boundary
├── Sequence
├── Batch / Loop
├── Transformation
├── Persistence
├── State Change
├── Idempotency
├── Error Path
├── Retry
└── Completion

核心原则：

> Happy Path is not enough.

真实 Automation 必须同时设计：

Normal Path
+
Exception Path

---

# 3. Task A — Search & Collection Process

Task A：

Valid Collection Input
↓
Load Eligible Keywords
↓
Execute Search
↓
Receive Raw Results
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
Select Candidates
↓
Persist Data

需要区分：

Post Entity

和：

Search Hit Relationship

---

# 4. Deduplication Process

同一 Post 可能：

- 被多个 Keyword 搜到
- 在多个 Run 中再次出现

不能每次创建新 Post。

因此：

Search Result
↓
Post Exists?
├── No → Create Post
└── Yes → Reuse Existing Post

但是：

每一次有价值的 Search Relationship 仍然需要保存。

例如：

Keyword A → Post 001
Keyword B → Post 001

核心原则：

> Deduplicate Entity, preserve Relationship.

---

# 5. Engagement Observation Process

互动数据属于：

Time-dependent Observation

因此：

Likes
Saves
Comments Count
Engagement

不应该只覆盖 Post Current State。

而应该：

Post
↓
Observation 1
Observation 2
Observation 3

这样 Task B 才能比较变化。

核心原则：

> Observation should be appendable historical evidence.

---

# 6. Task A2 — Basic AI Analysis Process

Candidate Post
↓
Prepare AI Input
↓
Basic AI Analysis
↓
Topic Classification
↓
Short Summary
↓
Validate Output
↓
Persist Analysis
↓
Create Review Item
↓
Aggregate Daily Review
↓
Deliver to Feishu

这里 AI Output 必须：

Structured
+
Validatable

不能只依赖自由文本。

---

# 7. AI Failure Does Not Delete Candidate

如果：

Candidate Post Valid
↓
AI Analysis Failed

不能：

Delete Candidate

应该：

Record AI Failure
↓
Preserve Candidate
↓
Create Review Item if possible
↓
Allow Retry / Manual Visibility

核心原则：

> Downstream enrichment failure should not destroy valid upstream data.

---

# 8. Human-in-the-loop Process

Daily Review 发到飞书以后：

系统不应该把整个 Workflow 挂起等待律师。

更合理的是：

Daily Workflow
↓
Persist Review Item
↓
Deliver
↓
Complete

律师后来操作：

Human Decision Event
↓
Separate Decision Handling
↓
Persist Decision
↓
Update Eligibility / State
↓
Trigger downstream workflow if needed

核心理解：

> Human Review is an asynchronous event, not a long-running blocked workflow.

---

# 9. Task B — 7-Day Tracking Process

Tracking State Created
↓
Wait until Due Date
↓
Identify Due Posts
↓
Fetch Current Post State
↓
Normalize
↓
Validate
↓
Append New Observation
↓
Compare with Initial Observation
↓
Generate Tracking Evidence
↓
Create Tracking Review Item
↓
Lawyer Re-evaluation

这里不建议让一个 Workflow：

Wait 7 Days

而是保存：

Tracking Due State

然后由 Scheduled Tracking Workflow 查询：

Which posts are due?

---

# 10. Tracking Failure Paths

可能出现：

API Failure
Post Deleted
Post Hidden
Post Unavailable
Incomplete Metrics

需要区分：

Technical Failure

和：

Business Availability Change

例如：

Post Unavailable

不等于：

API Failed

系统应该保留历史 Observation。

---

# 11. Task C — Deep Analysis Process

Valid Deep Analysis Request
↓
Load Post Context
↓
Load Existing Basic Analysis
↓
Check Comment Analysis Requirement

If No:
Analyze Post

If Yes:
Collect Comments
↓
Normalize
↓
Select High-value Comments
↓
Analyze Post + Selected Comments

最终：

Generate Structured Research Subject
↓
Validate
↓
Persist
↓
Record AI Provenance

---

# 12. Progressive Enrichment

今天进一步确认：

系统不应该一开始采集所有可能的数据。

应该：

Basic Collection
↓
Candidate
↓
Lawyer Value Judgment
↓
High-value Object
↓
Deep Collection / Analysis

例如：

Task A:
Comments Count

Task C:
Actual Comment Content

核心：

> Spend expensive processing only on objects that justify it.

---

# 13. Task D — Long-tail Discovery Process

Eligible Research Subjects
↓
Extract User Expressions
↓
Preserve Raw Expressions
↓
Normalize Expressions
↓
Semantic Clustering
↓
Count Occurrences
↓
Count Distinct Posts
↓
Create / Update Long-tail Candidate
↓
Link Source Evidence

如果同一 Long-tail Candidate 再次出现：

不要创建 Duplicate Candidate。

而是：

Update Evidence
+
Add Source Relationship

---

# 14. Task E — Keyword Calibration Process

Monthly Trigger
↓
Load Keyword Evidence
↓
Aggregate Performance
↓
Analyze Outcomes
↓
Generate Calibration Recommendation
↓
Persist Recommendation
↓
Create Monthly Review
↓
Deliver to Lawyer

到这里：

Automation 完成。

不能直接：

Recommendation
↓
Change Production Keyword Library

必须等待律师审批。

---

# 15. Task F — Case Matching Process

Research Subject
↓
Access Structured Case Library
↓
Retrieve Candidate Cases
↓
Evaluate Relevance
↓
Rank
↓
Persist Match Result

可能：

Relevant Case

或者：

No Relevant Case

两者都属于正常完成。

---

# 16. Task G — Candidate Topic Generation Process

Eligible Research Subject
↓
Load Available Evidence
↓
Generate Candidate Topics
↓
Validate
↓
Semantic Deduplication
↓
Link Topic to Evidence
↓
Persist
↓
Create Review Items
↓
Aggregate Weekly Package
↓
Deliver to Feishu

Available Evidence 可能包括：

- Source Post
- Research Subject
- Tracking Evidence
- User Expressions
- Long-tail Evidence
- Case Match
- Comment Evidence

不是每一项都必须存在。

---

# 17. Batch vs Item-level Processing

今天理解：

一个 Workflow Run 可以是 Batch。

例如：

Daily Search Run
↓
4 Keywords

每个 Keyword：
↓
Multiple Search Results

每个 Search Result：
↓
Independent Processing

因此需要区分：

Run-level Status

和：

Item-level Status

---

# 18. Partial Success

假设：

4 Keywords

其中：

3 Search Success
1 API Failure

不能简单：

Workflow Failed

也不能：

Workflow Success

更合理：

Partial Success

并记录：

- Successful Items
- Failed Items
- Failure Reason

核心：

> Batch workflows need partial-success semantics.

---

# 19. Idempotency

Automation 可能因为：

- Retry
- Timeout
- Duplicate Webhook
- Manual Rerun

导致同一个动作执行两次。

系统需要避免：

- Duplicate Post
- Duplicate Search Hit
- Duplicate Tracking Request
- Duplicate Deep Analysis Request
- Duplicate Lawyer Decision
- Duplicate Topic

因此关键 Action 应该具备：

> Idempotency

核心问题：

> If the same event happens twice, will the business data remain correct?

---

# 20. Persistence Before Downstream Action

重要数据不应该只存在 Workflow Memory。

例如：

Deep Analysis Completed
↓
Trigger Task D

更稳妥：

Deep Analysis Completed
↓
Persist Research Subject
↓
Mark State
↓
Downstream reads persisted data

核心：

> Persist first, then continue downstream processing.

这样失败后更容易恢复。

---

# 21. Error Classification

今天将错误初步分为：

Technical Error

例如：

- API timeout
- Authentication failure
- Database unavailable

Data Error

例如：

- Missing Required Field
- Invalid Datetime
- Invalid AI JSON

Business Condition

例如：

- No Relevant Case
- No Eligible Tracking Post
- No Valuable Comment

重要：

> Business Empty Result ≠ Technical Error.

---

# 22. Retry Principle

不是所有错误都 Retry。

适合 Retry：

Temporary API Failure
Timeout
Rate Limit

不适合盲目 Retry：

Invalid Input
Post Permanently Unavailable
Schema Logic Error

Retry 必须有：

Limit
+
Reason
+
Final Status

---

# 23. Process Decoupling

今天进一步认识：

Task A–G 不应该做成一个巨大 Workflow。

不建议：

A
↓
Wait Lawyer
↓
B
↓
Wait 7 Days
↓
C
↓
D
↓
F
↓
G

更合理：

Independent Workflows
+
Persistent State
+
Eligibility
+
Events

也就是：

> Workflows communicate through data/state, not by keeping one process alive forever.

---

# 24. Key Mindset Change

Day 05 从：

“What steps should the automation perform?”

升级为：

“How can the workflow remain correct when real-world failures, retries, delays and human decisions happen?”

开始理解：

Process Design
≠
Happy Path Diagram

真正的 Automation Process 需要：

Normal Path
+
History
+
State
+
Retry
+
Partial Success
+
Idempotency
+
Recovery

---

# 25. Day 05 Deliverables

✅ Task A Process
✅ Deduplication Process
✅ Engagement Observation
✅ Task A2 Process
✅ AI Failure Handling
✅ HITL Async Process
✅ Task B Process
✅ Tracking Failure Paths
✅ Task C Process
✅ Progressive Enrichment
✅ Task D Process
✅ Task E Process
✅ Task F Process
✅ Task G Process
✅ Batch Processing
✅ Partial Success
✅ Idempotency
✅ Persistence
✅ Error Classification
✅ Retry Principle
✅ Workflow Decoupling

---

# 26. Next Step — Day 06

Next:

> Decision Analysis

核心问题：

Process 告诉我们：

“What happens?”

Decision 则回答：

“Why does the workflow choose one path instead of another?”

重点：

- Rule-based Decision
- AI-assisted Decision
- Human Decision
- Decision Evidence
- Decision History
- Eligibility
- State Transition
- Approval Boundary