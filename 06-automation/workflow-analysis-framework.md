# Workflow Analysis Framework

> A reusable framework for Business Process Automation, AI Automation and AI Application Design.

---

# Core Principle

```text
Business Problem
↓
Workflow Analysis
↓
Product / Solution Design
↓
Technology Mapping
↓
Implementation
↓
Evaluation
↓
Delivery & Iteration
```

核心原则：

> Business Requirement First, Technology Second.

不要因为：

- 会 n8n
- 会 Python
- 会某个 LLM
- 会某个 Agent Framework

就强行用它解决所有问题。

---

# 0. Business Problem

> Do not automate a process you do not understand.

Automation Workflow 设计之前先理解真实业务。

推荐分析顺序：

```text
Current Situation / As-Is Workflow
↓
Pain Points
↓
Root Causes / Constraints
↓
Automation Opportunities
↓
Automation Boundary
↓
Automation Goal
↓
Success Metrics
↓
To-Be Workflow
```

---

## 0.1 Current Situation / As-Is Workflow

先描述：

> 当前业务实际上如何运行？

而不是直接描述未来自动化系统。

需要了解：

- Current Trigger
- Main Steps
- People / Roles
- Tools
- Data Sources
- Data Storage
- Manual Work
- Human Decisions
- Current Output
- Processing Time
- Frequency

建议：

```text
Current Trigger
↓
Step 1
↓
Step 2
↓
Step 3
↓
Current Output
```

---

## 0.2 Pain Points

常见问题：

### Repetitive Work

需要反复执行的动作。

### Time-consuming Work

耗时但价值不高的工作。

### Error-prone Work

容易人工出错。

### Missing / Forgotten Work

容易遗漏。

### Inconsistent Work

不同人、不同时间执行标准不一致。

### Scalability Problem

业务量增加后人工无法扩展。

### Information Retrieval Problem

例如：

- Data scattered
- Search difficult
- History unavailable
- Human memory dependency

### Manual Decision Bottleneck

需要区分：

```text
Rule-based
AI-assisted
Human-controlled
```

---

## 0.3 Root Causes / Constraints

不要只记录表面 Pain Point。

例如：

```text
Pain Point:
Manual Data Processing

Possible Root Causes:
- Multiple Data Sources
- Inconsistent Formats
- No Shared Data Layer
- No Collection Automation
- No Validation Standard
```

需要判断：

- Process Problem?
- Data Problem?
- Tool Problem?
- Integration Problem?
- Human Workload?
- Missing Standard?
- API Limitation?
- Business Rule unclear?
- Professional judgment required?

---

## 0.4 Automation Opportunities

优先寻找：

```text
High Frequency
+
High Repetition
+
Clear Rules
+
High Manual Cost
+
Structured / Structurable Data
```

AI 特别适合：

```text
Classification
Extraction
Summarization
Semantic Understanding
Recommendation
Matching
Unstructured Content Analysis
```

但：

> Technically automatable does not automatically mean it should be automated.

需要综合：

```text
Business Value
Implementation Cost
Reliability
Risk
Human Responsibility
```

---

## 0.5 Automation Boundary

### A. Fully Automated

适合：

- Collection
- Transformation
- Calculation
- Validation
- Deduplication
- Scheduled Work
- Data Storage
- Standard Notifications

---

### B. AI-assisted

适合：

- Classification
- Content Analysis
- Semantic Matching
- Recommendation
- First-pass Review

常见结构：

```text
AI
↓
Analysis / Recommendation
↓
Human Review
```

---

### C. Human-controlled

适合：

- Final Approval
- Professional Judgment
- High-risk Decisions
- Business Decisions
- Subjective Selection

核心：

> Automation 的价值不是消灭 Human，而是让 Human 集中做高价值判断。

---

## 0.6 Automation Goal

不要只写：

```text
Improve Efficiency
Use AI
Automate Workflow
```

应该明确：

- Reduce Manual Collection
- Reduce Repetitive Processing
- Improve Consistency
- Improve Tracking
- Improve Retrieval
- Support Human Decision-making
- Improve Coverage
- Improve Data Quality

---

## 0.7 Success Metrics

不要只判断：

```text
Workflow successfully ran
```

还要判断：

```text
Did the business improve?
```

结构：

```text
Baseline
↓
Metric
↓
Target
```

常见指标：

- Time Saved
- Manual Work Reduction
- Accuracy
- Error Rate
- Coverage
- Processing Volume
- Consistency
- Adoption Rate
- Cost
- Response Time
- Revenue / Conversion if relevant

没有真实数据时：

```text
Baseline: TBD
Target: TBD
```

不要虚构数值。

---

## 0.8 MVP Success Criteria

MVP 优先证明：

- Workflow 能否稳定运行？
- 是否减少 Manual Work？
- 数据能否可靠获取？
- Output 是否有业务价值？
- AI 是否达到最低可接受质量？
- Human 是否愿意使用？
- 是否值得继续投入？

避免 MVP Scope 无限扩大。

---

## 0.9 Business Problem Template

```text
Business Problem:

Current Situation:
- Trigger:
- Main Steps:
- Current Tools:
- People:
- Data:
- Current Output:

Pain Points:
1.
2.
3.

Root Causes:
1.
2.
3.

Automation Opportunities:
1.
2.
3.

Automation Boundary:

Fully Automated:
-

AI-assisted:
-

Human-controlled:
-

Automation Goal:
-

Success Metrics:

Metric:
Baseline:
Target:

MVP Success Criteria:
-
```

---

# 1. Trigger Analysis

> 什么真正启动 Workflow？

必须区分：

```text
Trigger
↓
Upstream Dependency
↓
Precondition
↓
Execution Rule
↓
Failure / Skip Handling
```

---

## 1.1 Trigger Types

### Schedule Trigger

固定时间执行。

Examples：

- Daily
- Weekly
- Monthly
- Hourly

---

### Event Trigger

业务事件发生。

Examples：

- New File
- New Email
- Record Created
- Previous Workflow Completed

---

### Manual Trigger

人工主动操作。

Examples：

- Run
- Approve
- Retry
- Re-analyze

---

### Data Trigger

数据状态发生变化。

Examples：

- Status changed
- Score crossed threshold
- Record became eligible

---

### External / Webhook Trigger

外部系统发送事件。

Examples：

- Webhook
- SaaS Event
- API Callback

---

## 1.2 Trigger

需要问：

- What starts the workflow?
- Who / what triggers it?
- Frequency?
- Multiple triggers?
- Duplicate trigger possible?
- Real-time or batch?

---

## 1.3 Upstream Dependency

> Workflow 需要哪些上游数据或流程结果？

例如：

```text
Workflow A
↓
Produces Data
↓
Data Layer
↓
Weekly Schedule
↓
Workflow B
```

Workflow B：

```text
Trigger = Weekly Schedule
Dependency = Workflow A Data
```

不要混淆。

---

## 1.4 Precondition

> Trigger 发生以后，什么条件必须满足才能继续？

例如：

```text
Schedule
↓
Check Valid Inputs
↓
Any Valid Records?
├── Yes → Continue
└── No → Skip
```

需要判断：

- Valid Input exists?
- Upstream complete?
- Minimum data available?
- Eligible records exist?

---

## 1.5 Execution Rule

控制 Workflow 如何运行。

Examples：

- Maximum N records
- Only Active objects
- Batch size
- Time range
- Processing frequency
- Selection rules

Execution Rule：

```text
≠ Trigger
```

---

## 1.6 Signal vs Decision

必须区分：

```text
Signal
≠
Decision
```

例如：

```text
Metric High
Score = 0.85
Engagement Increased
AI Confidence High
```

这些可以是：

```text
Evidence / Signal
```

但只有当 Business Rule 明确规定：

```text
Signal
↓
Rule
↓
Branch
```

它才真正成为 Decision Rule。

不要因为存在数字阈值就自动假设它是业务决定。

---

## 1.7 Failure / Skip Handling

需要检查：

- Trigger failure
- Dependency unavailable
- Precondition failed
- Skip?
- Wait?
- Retry?
- Maximum retry?
- Recovery?
- Human notification?
- Failure reason stored?
- Manual override?

---

## 1.8 Trigger Template

```text
Workflow:

Trigger Type:

Trigger:

Upstream Dependencies:

Preconditions:

Execution Rules:

Failure / Skip Handling:

Execution Mode:
- Real-time
- Batch
- Scheduled Batch
- Event-driven
- Manual
```

---

## 1.9 Trigger Design Principle

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

> Dependency determines what the workflow needs.  
> Trigger determines when it starts.

---

# 2. Input Analysis

> Workflow 启动后，需要哪些 Data / Parameter / Configuration 才能继续？

完整分析链：

```text
Source
↓
Fields
↓
Requirement
↓
Data Type
↓
Normalization
↓
Validation
↓
Data Quality
↓
Missing / Invalid Handling
↓
Freshness
↓
History
↓
Relationships
```

---

## 2.1 Input Types

### User Input

Human-provided data.

---

### System Input

系统已有数据。

---

### External Input

External Platform / API / SaaS。

---

### Knowledge Input

- Documents
- Knowledge Base
- Case Library
- SOP
- Examples

---

### Configuration Input

控制 Workflow 行为：

- Limit
- Threshold
- Time Range
- Business Scope
- Rules

---

### System-generated Input

系统产生：

- Timestamp
- Run ID
- Status
- Derived Data
- Previous Workflow Output

---

## 2.2 Source

明确：

- Who creates the data?
- Where does it live?
- How is it retrieved?
- Can source be unavailable?
- Is source owned by this system?

常见 Source：

```text
Human
Previous Workflow
Database
File
API
External Platform
AI
Configuration
System
```

---

## 2.3 Fields

不要停留在：

```text
Customer Data
Post Data
Order Data
```

要进一步问：

```text
Object
├── ID
├── Status
├── Content
├── Created At
└── Fields actually needed
```

只采集真正有业务需要的数据。

---

## 2.4 Requirement Types

### Required / Non-null

必须存在且有效。

### Required / Empty Allowed

字段必须存在，但业务上允许为空。

### Optional

缺失不阻断 Workflow。

### Conditional Required

只有满足特定业务条件时才 Required。

例如：

```text
Condition = False
→ Data = Not Required

Condition = True
→ Data = Required
```

---

## 2.5 Empty vs Missing vs Not Required vs Unavailable

必须区分：

```text
Empty
Missing
Not Required
Unavailable
```

### Empty

Source 本身没有内容。

### Missing

理论上应该获取，但没有获取成功。

### Not Required

当前业务分支根本不要求此数据。

### Unavailable

Source 当前不可访问或对象不可获得。

原则：

```text
Not Required
≠
Missing
```

---

## 2.6 Data Types

常见：

| Type | Example |
|---|---|
| String | `"abc"` |
| Integer | `100` |
| Float | `4.5` |
| Boolean | `true` |
| Array | `["A","B"]` |
| Datetime | `2026-09-06T10:00` |
| Object | `{...}` |
| Enum | `Active / Retired` |

ID 即使看起来是数字，如果用于 Identity 而不是 Calculation：

```text
String
```

通常更合理。

---

## 2.7 Input vs Configuration vs Process vs Decision

### Input

系统需要什么数据？

### Configuration

当前规则参数是多少？

### Process

如何处理 Input？

### Decision

根据什么选择下一步？

不要混在一起。

---

## 2.8 Raw Data vs Normalized Data

External Data 经常存在：

- Unit differences
- String number
- Relative dates
- Formatting noise
- Hashtags
- Inconsistent enums

建议：

```text
Raw Data
↓
Normalize
↓
Normalized Data
↓
Validate
```

---

## 2.9 Normalization

常见：

```text
Trim
Case normalization
Unit conversion
Datetime conversion
Enum mapping
Number parsing
Array deduplication
```

原则：

> 如果 Validation 依赖统一格式，先 Normalize 再 Validate。

---

## 2.10 Validation

Validation 可以包括：

- Required validation
- Type validation
- Format validation
- Range validation
- Allowed value validation
- Existence validation
- Cross-field validation
- Completeness validation

---

## 2.11 Data Quality

推荐概念：

```text
Valid
Incomplete
Missing
Invalid
Unavailable
Not Required
```

### Valid

可正常使用。

### Incomplete

部分数据存在，但不足。

### Missing

应有但未获得。

### Invalid

格式或内容不合法。

### Unavailable

外部对象或 Source 当前不可访问。

### Not Required

当前分支不需要。

---

## 2.12 Missing / Invalid Handling

不要统一处理为：

```text
error
```

应该按原因：

```text
Valid Empty
→ Continue

Temporary Failure
→ Retry

Format Issue
→ Normalize

Alternative Source Exists
→ Fallback

Incomplete but usable
→ Continue with Quality Flag

Critical Missing
→ Skip / Reject / Human Review

Unavailable
→ Record Reason
```

Retry 必须：

```text
Bounded
```

不要无限 Retry。

---

## 2.13 Freshness

需要问：

- Data current enough?
- Last updated?
- Time-sensitive?
- Timezone?
- Current state or historical observation?

Datetime 应尽量明确：

```text
Timestamp
+
Timezone
```

---

## 2.14 Current State vs Historical Observation

某些数据会随时间变化。

不要一直覆盖：

```text
Current Value
```

可能需要：

```text
Object
↓
Observation T1
Observation T2
Observation T3
```

用于：

- Trend
- Audit
- Evaluation
- Historical Comparison

---

## 2.15 Raw Data vs Derived Data

例如：

```text
Raw:
A
B
C

Derived:
Total = A + B + C
```

原则：

> 重要 Raw Data 与 Derived Data 尽量分开保存。

以后计算规则变化时可以重新计算。

---

## 2.16 Data Relationships

Business Objects 之间可能：

```text
One-to-One
One-to-Many
Many-to-Many
```

需要问：

- Object 被哪些 Source 发现？
- 一个 Object 是否属于多个 Categories？
- 一个 Event 是否关联多个 Objects？
- Downstream 是否需要追溯 Origin？

---

## 2.17 Deduplication vs Relationship Preservation

核心：

```text
Duplicate Object
≠
Duplicate Relationship
```

例如：

```text
Source A → Object 001
Source B → Object 001
```

可以：

```text
Object 001
only once
```

但仍然保留：

```text
Source A → Object 001
Source B → Object 001
```

原则：

> Deduplicate Entity, preserve meaningful Relationships.

---

## 2.18 Progressive Data Enrichment

不是所有数据都应该第一步采集。

可以：

```text
Collect Minimum Data
↓
Initial Screening
↓
Business Value Decision
↓
Collect More Expensive / Deeper Data
↓
Deep Analysis
```

适用于：

- API cost
- AI token cost
- Large data volume
- Expensive scraping
- Only a subset deserves deep processing

原则：

> Minimum necessary data first, deeper enrichment only when justified.

---

# 2.19 Persistent Entity vs Event vs State vs Decision

这是跨 Workflow Data Design 中非常重要的区分。

## Entity

长期存在的 Business Object。

Examples：

```text
Customer
Post
Product
Case
Order
```

---

## Event / Observation

某个时间点发生的事实。

Examples：

```text
Search Hit
Status Changed
Engagement Observation
Payment Event
```

---

## State

当前业务状态。

Examples：

```text
Confirmed
Active
Pending
Archived
```

---

## Decision

Human / System 做出的判断。

Examples：

```text
Approve
Reject
Keep
Escalate
```

原则：

```text
Entity
≠
Event
≠
State
≠
Decision
```

不要为了方便全部塞进一个 Object。

---

# 2.20 History: Append vs Overwrite

当数据本身具有审计、趋势或决策价值时：

优先：

```text
Append New Record
```

而不是：

```text
Overwrite Old Value
```

尤其适用于：

- Observations
- Decisions
- Status changes
- Search events
- Attempts
- Recommendations

例如：

```text
Decision at T1 = No
Decision at T2 = Yes
```

两者可能都需要保留。

因为：

> New Evidence can legitimately change an earlier Decision.

---

# 2.21 Human Decision Is Data

Human-in-the-loop 不只是 UI 动作。

每一个 Human Decision 都可能成为：

- Audit Data
- Evaluation Data
- Training / Feedback Data
- Calibration Evidence
- Product Usage Evidence

因此需要考虑：

```text
Decision ID
Target
Decision Type
Decision Value
Decided At
Decision Context
```

而不是只保存最终状态。

---

# 2.22 Shared Data Objects

多个 downstream workflows 如果都需要同一个经过处理的业务概念：

不应该：

```text
Workflow B re-analyzes
Workflow C re-analyzes
Workflow D re-analyzes
```

更合理：

```text
Upstream
↓
Shared Structured Object
↓
├── Workflow B
├── Workflow C
└── Workflow D
```

好处：

- Reduce duplicated AI calls
- Lower cost
- Improve consistency
- Reduce semantic drift
- Simplify interfaces

---

# 2.23 Data Contract

Data Contract 回答：

> Workflow A 输出的 Object，Workflow B 到底如何理解和消费？

至少需要明确：

```text
Object Name
Owner / Creator
Fields
Required / Optional
Identity
History Rule
Relationships
Consumers
Quality Requirement
```

---

## Data Contract Template

```text
Object:

Type:
- Entity
- Event
- Observation
- State
- Decision
- Relationship
- Configuration

Owner / Creator:

Identity:

Fields:
-

Required:
-

Optional:
-

History:
- Append / Overwrite / Snapshot

Relationships:
-

Consumers:
-

Data Quality Requirement:
-

Notes:
-
```

---

# 2.24 Cross-workflow Input Review

单个 Workflow 的 Input 都完成后，不代表整个系统没有问题。

需要横向 Review：

```text
Workflow A
↓
Workflow B
↓
Workflow C
↓
...
```

检查：

### 1. Downstream Requirement

下游需要的数据：

```text
Upstream really produces it?
```

---

### 2. Duplicate Concepts

是否多个 Workflow 在重复产生同一个概念？

---

### 3. State Consistency

同一个 Status / State 在不同 Workflow 是否含义一致？

---

### 4. Relationship Continuity

Upstream relationship 是否被 Dedup / Transform 时丢失？

---

### 5. History Continuity

Observation / Decision history 是否能够跨 Workflow 追溯？

---

### 6. Optional Context

某个 Optional Input 是否被错误设计成 Mandatory Gate？

---

### 7. External Dependencies

哪些数据：

```text
Owned by this system
```

哪些：

```text
External / Upstream Dependency
```

边界是否明确？

---

# 2.25 Downstream-to-Upstream Contract Validation

Cross-workflow Review 非常重要的一种方法：

```text
Downstream Requirement
↓
Reverse Check
↓
Upstream Output Contract
```

例如：

```text
Three downstream workflows
all require Field X
↓
Field X should probably become
a stable upstream output field
```

原则：

> Output design should not only be based on what the upstream can generate; it should also be validated by what downstream workflows genuinely need.

---

# 2.26 Optional Context Must Not Accidentally Become a Gate

假设 Workflow 可以靠 Core Input 正常运行。

额外数据只是：

```text
Enhancement
```

则：

```text
Optional Data Missing
```

不能导致：

```text
Workflow blocked
```

需要明确：

```text
Core Required Inputs
vs
Optional Context
```

---

# 2.27 Input Specification

最终可以形成：

| Field | Source | Type | Requirement | Normalization | Validation | Failure Handling | Freshness |
|---|---|---|---|---|---|---|---|
| | | | | | | | |

或：

```text
Field:

Source:

Data Type:

Requirement:
- Required / Non-null
- Required / Empty Allowed
- Optional
- Conditional Required

Normalization:

Validation:

Data Quality:

Missing / Invalid Handling:

Failure Reason:

Freshness:

Timezone:

History:

Relationship:
```

---

# 2.28 Input Analysis Questions

每个 Workflow 检查：

1. Workflow 需要什么数据？
2. Source 是什么？
3. 需要哪些 Fields？
4. Required / Optional / Conditional Required？
5. Empty 是否有效？
6. Not Required 是否被误认为 Missing？
7. Data Type？
8. 是否需要 Normalize？
9. Validation？
10. Data Quality？
11. Missing / Invalid 如何处理？
12. Retry 是否 bounded？
13. Freshness？
14. Timezone？
15. Current State or History？
16. Raw vs Derived？
17. Relationships？
18. Deduplication 是否丢关系？
19. 是否能 Progressive Enrichment？
20. Entity / Event / State / Decision 是否混淆？
21. 哪些数据应该 Append？
22. Human Decision 是否被保存？
23. 是否存在 Shared Structured Object？
24. Downstream 是否需要上游没有的字段？
25. Optional Context 是否错误变成 Gate？
26. External Dependency Boundary 是否清晰？
27. 是否完成 Data Contract Review？

---

# 2.29 Input Completion Criteria

Input Analysis 可以标记：

```text
Completed for Current MVP v1
```

当：

- A–Z Workflow inputs defined
- Required / Optional known
- Data quality concepts known
- Critical relationships preserved
- Historical requirements known
- Cross-workflow gaps reviewed
- Data Contracts reviewed
- Remaining unknowns clearly marked TBD

但：

> Completed does not mean permanently frozen.

真实设计过程中：

```text
Input v1
↓
Process reveals missing requirement
↓
Input v1.1
```

是正常迭代。

---

# Input Design Principle

完整 Input 思考：

```text
What Data?
↓
From Where?
↓
Which Fields?
↓
Required?
↓
What Type?
↓
Normalize?
↓
Valid?
↓
Complete?
↓
What Quality?
↓
If Not, What Happens?
↓
Fresh Enough?
↓
Need History?
↓
Need Relationships?
↓
Entity / Event / State / Decision?
↓
Shared Object?
↓
Data Contract?
↓
Cross-workflow Compatible?
```

---

# 3. Process Analysis

> Valid Inputs 进入 Workflow 后，如何一步步变成中间结果？

Process 回答：

```text
What happens to the data?
```

而不是：

```text
What condition decides the branch?
```

后者属于 Decision。

---

## 3.1 Process Boundary

每个 Workflow 必须定义：

```text
Start Boundary
↓
Process
↓
End Boundary
```

例如：

```text
Valid Inputs Ready
↓
...
↓
Processed Result Stored
```

---

## 3.2 Common Process Types

### Collect / Retrieve

获取数据。

### Normalize / Transform

统一格式。

### Validate

检查可用性。

### Clean / Filter

清理无效数据。

### Deduplicate

去重。

### Enrich

补充数据。

### Analyze

AI / Rule-based Analysis。

### Aggregate

统计和聚合。

### Store

保存。

### Deliver

发送结果。

---

## 3.3 Recommended Generic Processing Order

不要求所有项目完全一样，但常见：

```text
Raw Input
↓
Collect / Read
↓
Normalize / Transform
↓
Validate
↓
Clean / Filter
↓
Deduplicate
↓
Enrich
↓
Analyze
↓
Aggregate
↓
Store
```

注意：

如果 Validation 必须依赖 Normalized Format：

```text
Normalize
↓
Validate
```

---

## 3.4 Loop / Batch

需要明确：

- One-by-one?
- Batch?
- Nested loops?
- Batch size?
- Parallel?
- Sequential?
- Maximum records?

不要让 Loop 隐含存在。

---

## 3.5 State & Persistence

Process 中需要问：

- What is persisted?
- When?
- Before or after external call?
- Intermediate state needed?
- Resume from failure?
- Duplicate execution possible?

---

## 3.6 External Calls

涉及：

- API
- LLM
- Database
- SaaS
- Webhook
- File system

需要设计：

```text
Call
↓
Response
↓
Validate
↓
Failure?
↓
Retry / Fallback / Skip
```

---

## 3.7 Idempotency

> Same valid request accidentally runs twice. What happens?

理想情况：

```text
No duplicate business object
No duplicate irreversible action
```

需要区分：

```text
Valid new historical event
```

与：

```text
Accidental duplicate
```

---

## 3.8 Error Path

不要只画 Happy Path。

至少考虑：

- External failure
- Invalid response
- Partial data
- Timeout
- Empty result
- Duplicate execution
- AI failure
- Storage failure

---

## 3.9 Observability

后续应该知道：

- Run started?
- Run completed?
- Records processed?
- Records failed?
- Error reason?
- Retry count?
- Last successful run?

---

## 3.10 Process Analysis Template

```text
Workflow:

Goal:

Start Boundary:

End Boundary:

Main Steps:
1.
2.
3.

Loops:
-

Transformations:
-

External Calls:
-

Persistence:
-

Idempotency:
-

Failure Paths:
-

Observability:
-
```

---

# 4. Decision Analysis

> 根据什么证据和规则决定下一步？

需要分清：

```text
Input
↓
Process
↓
Signal / Evidence
↓
Decision Rule
↓
Branch
```

---

## 4.1 Rule-based Decision

清晰业务规则。

```text
Condition
↓
Yes / No
```

---

## 4.2 Score-based Decision

多个 Signals 综合评分。

不要在没有真实业务依据时随意发明权重。

---

## 4.3 AI-assisted Decision

AI 提供：

```text
Classification
Recommendation
Confidence
Reasoning Summary
```

Human 保留最终决定。

---

## 4.4 Human-controlled Decision

高风险 / 商业 / 专业判断。

需要明确：

- Who decides?
- What evidence is shown?
- Where?
- What options?
- What happens after decision?

---

## 4.5 Evidence Sufficiency

非常重要：

```text
Poor Result
≠
Sufficient Evidence of Poor Performance
```

需要区分：

```text
Decision Value
```

和：

```text
Evidence Sufficiency
```

样本不足时：

```text
Insufficient Evidence
```

往往比强制 Yes / No 更合理。

---

## 4.6 Re-evaluation

Business Decision 不一定永久。

```text
Decision at T1
↓
New Evidence
↓
Re-evaluation
↓
Decision at T2
```

历史 Decision 仍应保留。

---

# 5. Action Analysis

> Decision 之后系统具体执行什么？

常见 Action：

- Save
- Update State
- Create Queue Item
- Call API
- Send Message
- Request Human Approval
- Trigger Workflow
- Archive
- Retry
- Alert
- Stop

需要区分：

```text
Decision:
Should we proceed?

Action:
Create a task and send it to the next system.
```

---

# 6. Output Analysis

> Workflow 最终产生什么？

Output 可以包括：

### Data Output

Structured Data。

### Human-readable Output

Report / Summary / Dashboard。

### System Output

State change / Queue / Event。

### AI Output

Classification / Analysis / Recommendation。

---

## 6.1 Output Contract

需要问：

- Who consumes this output?
- Required fields?
- Structured?
- Human readable?
- Evidence included?
- Need source traceability?
- Need quality flag?
- Can downstream reuse directly?

---

## 6.2 Explainability / Evidence

Recommendation 类 Output 尤其需要：

```text
Recommendation
+
Why
+
Source Evidence
```

避免纯黑盒。

---

## 6.3 Product Output

当 Output 需要 Human 使用时，再考虑：

- User Flow
- Feishu / Web / App / Email
- Interactive Action
- Information hierarchy
- Acceptance Criteria
- Prototype

不要在 Business Analysis 阶段提前锁 UI 技术。

---

# 7. Technology Mapping

Technology Mapping 应发生在 Workflow 逻辑相对稳定以后。

推荐顺序：

```text
Business Requirement
↓
Data Requirement
↓
Workflow Requirement
↓
Technical Requirement
↓
Technology Selection
```

常见能力：

- JSON
- HTTP
- REST API
- Authentication
- Webhook
- Automation Platform
- Python
- Database
- Cloud Runtime
- LLM API
- Structured Output
- Embedding
- Vector DB
- RAG
- Tool Calling
- Logging
- Monitoring
- Docker
- Deployment

---

## 7.1 Technology Selection Questions

每个技术都问：

1. What requirement does it solve?
2. Is it genuinely needed?
3. Simpler alternative?
4. Cost?
5. Reliability?
6. Maintenance?
7. Data security?
8. Deployment?
9. Scalability?
10. Can it run independently of developer computer?

---

# 8. Product Design Integration

Workflow 设计不是纯技术流程。

推荐逐步映射：

```text
Business Problem
↓
Stakeholder / User
↓
Product Goal
↓
Workflow
↓
Business Rules
↓
User Story
↓
Acceptance Criteria
↓
PRD
↓
Prototype if useful
↓
Technical Requirements
↓
Implementation
↓
Evaluation
```

---

# 9. Evaluation

完成 Implementation 后，不只测：

```text
Does it run?
```

还要测：

```text
Does it work well?
```

包括：

- Functional Testing
- Data Quality
- AI Quality
- Human Acceptance
- Error Handling
- Business Metrics
- Cost
- Reliability
- Latency

---

# 10. Workflow Analysis Master Checklist

## Business

- [ ] As-Is understood
- [ ] Pain Points identified
- [ ] Root Causes identified
- [ ] Boundary defined
- [ ] Goal defined
- [ ] Metrics defined

## Trigger

- [ ] Trigger identified
- [ ] Dependency separated
- [ ] Preconditions defined
- [ ] Execution Rules defined
- [ ] Signal not confused with Decision
- [ ] Failure / Skip handling considered

## Input

- [ ] Sources defined
- [ ] Fields defined
- [ ] Required / Optional / Conditional defined
- [ ] Empty / Missing / Not Required / Unavailable separated
- [ ] Types defined
- [ ] Normalization defined
- [ ] Validation defined
- [ ] Data Quality defined
- [ ] Freshness considered
- [ ] Historical data considered
- [ ] Raw / Derived separated
- [ ] Relationships preserved
- [ ] Progressive enrichment considered
- [ ] Entity / Event / State / Decision separated
- [ ] Historical Decisions preserved
- [ ] Shared Objects identified
- [ ] Data Contracts reviewed
- [ ] Cross-workflow Review completed

## Process

- [ ] Boundary defined
- [ ] Sequence defined
- [ ] Loops defined
- [ ] External calls identified
- [ ] Persistence defined
- [ ] Idempotency considered
- [ ] Failure paths considered
- [ ] Observability considered

## Decision

- [ ] Signals identified
- [ ] Rules separated from Process
- [ ] Evidence sufficiency considered
- [ ] AI vs Human ownership clear
- [ ] Re-evaluation considered

## Action

- [ ] Actions explicit
- [ ] State changes explicit
- [ ] Human interactions explicit

## Output

- [ ] Consumers known
- [ ] Output contract defined
- [ ] Evidence / traceability included
- [ ] Product presentation considered

## Technology

- [ ] Technology solves real requirement
- [ ] Simpler options considered
- [ ] Cost considered
- [ ] Deployment considered
- [ ] Reliability considered
- [ ] Local-computer dependency considered

---

# Final Design Principle

A mature Automation / AI Workflow should be understandable as:

```text
Business Problem
↓
Trigger
↓
Input
↓
Process
↓
Signal / Evidence
↓
Decision
↓
Action
↓
Output
↓
Evaluation
↓
Feedback / Iteration
```

同时在整个系统层面持续检查：

```text
Entities
+
Events
+
States
+
Decisions
+
Relationships
+
History
+
Data Contracts
```

最终目标不是：

> Build a complicated automation.

而是：

> Build a reliable system that solves a real business problem and can be understood, evaluated, maintained and improved.