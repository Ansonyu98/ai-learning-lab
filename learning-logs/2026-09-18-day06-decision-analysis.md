# Day 06 — Decision Analysis

## Today's Goal

Day 05 已经完成：

Process Analysis

今天进入：

> Decision Analysis

核心问题：

> At each branch of the workflow, who or what should make the decision?

今天重点不是写 if/else。

而是判断：

- 哪些 Decision 可以用 Rule
- 哪些需要 AI
- 哪些必须由律师审批
- Decision 应该依赖什么 Evidence
- Decision 改变后如何保留历史

---

# 1. Three Decision Layers

今天建立整个项目最重要的 Decision Framework：

Rule / System
↓
AI
↓
Human

三层分别处理不同类型的不确定性。

---

# 2. Rule-based Decision

Rule 适合：

Clear
Deterministic
Low ambiguity

例如：

Tracking Due?

Required Field Missing?

Duplicate Post?

Top N reached?

Schema Valid?

这些不需要 AI。

核心：

> If a decision can be reliably expressed as a deterministic rule, do not unnecessarily use AI.

---

# 3. AI-assisted Decision

AI 适合：

Semantic Understanding
Classification
Similarity
Contextual Relevance

例如：

- Post Relevance
- Topic Classification
- Comment Relevance
- User Expression Clustering
- Case Relevance
- Topic Semantic Deduplication

AI 输出应该尽可能：

Structured
+
Evidence-linked
+
Validatable

---

# 4. Human Decision

律师保留：

Professional Judgment
Business Value Judgment
Final Approval

例如：

- Keep / Reject
- Track?
- Deep Analysis?
- Comment Analysis?
- Keyword Lifecycle Approval
- Candidate Topic Approval

核心：

> AI can recommend, but the MVP does not automatically replace professional/business approval.

---

# 5. Daily Review Decision Model

Candidate Post
↓
AI Basic Analysis
↓
Lawyer Review

律师主要判断：

Keep?

如果 No：

Research State = Rejected

如果 Yes：

Research State = Confirmed / Priority

然后进一步判断：

Track?

Deep Analysis?

Comment Analysis?

---

# 6. Engagement Is Evidence, Not Final Decision

今天进一步冻结：

Engagement > 500

不能直接：

Priority Pool

原因：

高互动不等于：

High Business Value

因此：

Engagement
=
Decision Evidence

律师结合：

- Topic
- Relevance
- Engagement
- Content Value
- Business Direction

进行最终判断。

---

# 7. Tracking Decision

Tracking 的意义是：

> Whether this post deserves future observation.

MVP：

律师人工审批。

Track = Yes
↓
Create Tracking State
↓
Due in 7 Days

Track = No
↓
No Tracking Request

---

# 8. Tracking Re-evaluation Decision

7-Day Tracking 产生新 Evidence 后：

Previous Decision
+
New Engagement Evidence
↓
Lawyer Re-evaluation

特别是：

Previous Deep Analysis = No

可以变成：

New Deep Analysis = Yes

核心：

> Decision is contextual and time-dependent.

---

# 9. Deep Analysis Decision

Task C 不是由：

Engagement Threshold

直接 Trigger。

而是：

Priority Research Object
+
Lawyer Deep Analysis Approval

才有资格进入。

因此：

System Recommendation / Evidence
↓
Lawyer Decision
↓
Deep Analysis Eligibility

---

# 10. Comment Analysis Decision

Comment Analysis：

不是独立 Workflow Decision。

而是：

Deep Analysis Configuration

只有在：

Deep Analysis = Yes

情况下才有意义。

MVP：

由律师判断评论是否值得分析。

---

# 11. Long-tail Candidate Decision

AI 可以：

Extract
Normalize
Cluster
Recommend

但：

Long-tail Candidate
≠
Official Search Keyword

真正进入 Keyword Library，需要后续 Keyword Calibration / Lawyer Approval。

---

# 12. Keyword Calibration Decision

系统可以根据：

Search Evidence
+
Lawyer Feedback
+
Research Outcomes
+
Long-tail Evidence

生成：

Keep
Observe
Reduce
Retire
Promote

等 Recommendation。

但是：

Recommendation
≠
Production Change

必须：

Lawyer Approval
↓
Keyword Lifecycle Update

这是一个明确的 Approval Boundary。

---

# 13. Case Matching Decision

Task F 可以使用 AI 判断：

Case Relevance

但 No Relevant Case：

是正常 Decision Result。

并且 Case Match 不应该成为 Topic Generation 的强制 Gate。

---

# 14. Candidate Topic Decision

AI：

Generate Candidate Topics

律师：

Approve / Reject

最终：

Approved Topic Pool

只有律师审批后的 Topic 才进入正式选题池。

---

# 15. System Recommendation vs Human Approval

今天进一步理解：

系统可以：

Recommend

但关键问题是：

> Does the recommendation itself have authority to change business state?

例如：

AI recommends:
Keyword Retire

不能直接：

Keyword Status = Retired

而应该：

Recommendation
↓
Review
↓
Lawyer Approval
↓
State Change

---

# 16. Eligibility vs Decision

Eligibility 回答：

> Is this object allowed to enter the next workflow?

Decision 回答：

> Should it enter?

例如：

Deep Analysis：

Eligibility:
Priority Pool

Decision:
Lawyer Deep Analysis = Yes

因此：

Eligible
≠
Automatically Selected

---

# 17. Decision Evidence

重要 Decision 应该能够回答：

> What information was available when this decision was made?

例如律师决定 Deep Analysis：

可能基于：

- Basic Summary
- Topic
- Current Engagement
- Tracking Evidence
- Source Post

未来需要保存：

Decision
+
Decision Time
+
Decision Context / Evidence Reference

---

# 18. Decision History

不能只保存：

Deep Analysis = Yes

因为之前可能：

Day 0:
No

Day 7:
Yes

因此：

Decision History

应该 Append。

同时可以维护：

Current Decision State

核心：

> Current State and Decision History solve different problems.

---

# 19. Human Decision as Event

律师在飞书做选择：

不是修改一个本地 Excel Cell 就结束。

它应该成为：

Human Decision Event

例如：

Decision Event
↓
Persist
↓
Update State
↓
Evaluate Downstream Eligibility
↓
Create Request if needed

这为后续 Webhook / Feishu Integration 奠定基础。

---

# 20. Decision Failure / Missing Decision

Human-in-the-loop 系统还需要考虑：

律师暂时没有审批。

这不等于：

Reject

应该：

Pending Review

因此：

Pending
Rejected
Approved

必须区分。

核心：

> No decision ≠ Negative decision.

---

# 21. Key Decision Principle

今天形成整个系统的核心职责分工：

Rule
→ Deterministic Logic

AI
→ Semantic Judgment

Lawyer
→ Professional / Business Value Judgment

简化表达：

> Rule handles certainty.
> AI handles semantic uncertainty.
> Human handles high-value judgment.

---

# 22. Day 06 Deliverables

✅ Three-layer Decision Model
✅ Rule-based Decision
✅ AI-assisted Decision
✅ Human Decision
✅ Daily Review Decision
✅ Engagement as Evidence
✅ Tracking Decision
✅ Post-tracking Re-evaluation
✅ Deep Analysis Decision
✅ Comment Analysis Decision
✅ Long-tail Candidate Decision
✅ Keyword Calibration Approval
✅ Case Match Decision
✅ Topic Approval
✅ Recommendation vs Authority
✅ Eligibility vs Decision
✅ Decision Evidence
✅ Decision History
✅ Human Decision Event
✅ Pending vs Reject

---

# 23. Next Step — Day 07

Next:

> Action + Output Analysis

核心问题：

Decision 已经产生以后：

What should the system actually do?

以及：

What usable result should each workflow produce?

重点：

Decision
↓
Action
↓
State Change
↓
Output
↓
Downstream