# Workflow Analysis Framework

> A reusable framework for analyzing Business Process Automation and AI Automation projects.

## Core Principle

**Business Problem → Workflow Analysis → Solution Design → Technology → Build → Test → Deliver**

核心原则：

> Business Requirement First, Technology Second.

不要因为会某个工具，就强行用某个工具解决所有问题。

---

# 0. Business Problem

> 在设计 Automation Workflow 之前，先理解真实业务问题。

核心原则：

> Do not automate a process you do not understand.

Business Problem Analysis 的目标不是马上寻找技术方案，而是先回答：

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
```

---

## 0.1 Current Situation / As-Is Workflow

> 当前业务实际上是怎么运行的？

首先描述现有业务流程，而不是直接描述希望建设的自动化系统。

需要了解：

- 当前业务流程是什么？
- Workflow 从哪里开始？
- 现在有哪些主要 Steps？
- 每一步由谁完成？
- 当前使用哪些工具 / 系统？
- 数据从哪里来？
- 数据保存在哪里？
- 哪些步骤依赖人工操作？
- 哪些步骤依赖人工判断？
- 当前流程需要多长时间？
- Workflow 最终产生什么业务结果？

建议先画出：

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

这一阶段描述的是：

> As-Is Workflow

而不是未来的：

> To-Be Workflow

---

## 0.2 Pain Points

> 当前 Workflow 哪里存在问题？

常见 Pain Points：

### Repetitive Work

哪些步骤需要不断重复执行？

### Time-consuming Work

哪些步骤最耗时间？

### Error-prone Work

哪些步骤容易出现人工错误？

### Missing / Forgotten Work

哪些步骤容易遗漏？

### Inconsistent Work

哪些步骤因为不同人员或不同时间执行，结果容易不一致？

### Scalability Problem

当数据量、客户量、平台数量或业务量增加以后，哪些步骤无法继续依靠人工扩展？

### Information Retrieval Problem

是否存在：

- 数据分散
- 查找困难
- 历史信息难以追踪
- 依赖个人记忆

### Manual Decision Bottleneck

哪些判断必须依赖人工？

其中哪些：

```text
可以 Rule-based
可以 AI-assisted
必须 Human-controlled
```

---

## 0.3 Root Causes / Constraints

> Pain Point 为什么会发生？

不要只记录表面问题。

例如：

```text
Pain Point:
人工整理数据耗时

Possible Root Causes:
- 数据来自多个平台
- 数据格式不统一
- 没有统一 Database
- 缺少自动采集
- 缺少标准化规则
```

分析时可以问：

- 是 Process 问题还是 Tool 问题？
- 是 Data 问题还是 Human Workload 问题？
- 是否缺少统一标准？
- 是否缺少系统连接？
- 是否缺少历史数据？
- 是否存在 API / Platform 限制？
- 是否存在 Business Rule 不明确？
- 是否存在必须保留的人工判断？

核心原则：

> Automation 应解决 Root Cause，而不仅仅自动化当前低效步骤。

---

## 0.4 Automation Opportunity

> 哪些 Pain Points 值得通过 Automation / AI 改善？

可以优先寻找：

```text
High Frequency
+
High Repetition
+
Clear Rules
+
High Manual Cost
+
Structured or Structurable Data
```

这些通常是较好的 Automation Opportunities。

同时识别 AI 更适合解决的问题：

```text
Unstructured Content
Semantic Understanding
Classification
Extraction
Summarization
Recommendation
Matching
```

不要因为某一步可以自动化，就默认它应该自动化。

需要同时考虑：

```text
Business Value
Implementation Cost
Risk
Reliability
Human Responsibility
```

---

## 0.5 Automation Boundary

> 哪些工作应该自动化，哪些应该由 AI 辅助，哪些必须保留人工控制？

可以分为三层。

### A. Fully Automated

规则明确、重复性高、风险较低，可以正常由系统自动完成。

Examples:

- Data Collection
- Data Transformation
- Calculation
- Deduplication
- Scheduled Tracking
- Database Update

### B. AI-assisted

需要语义理解或复杂判断，但 AI 不一定应该拥有最终决定权。

Examples:

- Classification
- Content Analysis
- Semantic Matching
- Recommendation
- First-pass Review

常见流程：

```text
AI Analysis
↓
Recommendation
↓
Human Review / Confirmation
```

### C. Human-controlled

涉及：

- 高风险判断
- 专业责任
- 商业决策
- 主观选择
- 最终批准

通常应该保留人工控制。

Examples:

- Final Approval
- Final Business Decision
- High-risk Professional Judgment
- Final Content Selection

核心原则：

> Automation 的目标不是消灭 Human，而是把 Human 从低价值重复劳动中释放出来，让人工集中处理高价值判断。

---

## 0.6 Automation Goal

> 自动化以后，希望 Workflow 发生什么变化？

Automation Goal 应直接对应 Pain Points。

不要只写：

```text
Improve Efficiency
Use AI
Automate Workflow
```

应该尽量明确：

```text
Reduce Manual Collection
Reduce Repetitive Data Processing
Improve Analysis Consistency
Improve Tracking Capability
Improve Information Retrieval
Support Human Decision-making
```

需要回答：

- 为什么需要 Automation？
- 希望减少哪些 Manual Work？
- 希望 AI 解决哪些问题？
- 哪些问题不应该交给 AI？
- 哪些步骤仍然需要 Human Review？
- Automation 后理想的 To-Be Workflow 是什么？

---

## 0.7 Success Metrics

> 如何证明 Automation 真的解决了 Business Problem？

不要只判断：

```text
Workflow successfully ran
```

而应该判断：

```text
Did the business improve?
```

### Baseline

自动化之前的当前水平。

例如：

```text
Manual Processing Time:
TBD

Weekly Manual Operations:
TBD
```

### Metric

具体衡量什么？

常见 Metrics：

- Time Saved
- Manual Work Reduction
- Error Reduction
- Accuracy
- Processing Volume
- Coverage
- Response Time
- Cost Reduction
- Consistency
- Adoption Rate
- Conversion
- Revenue Impact

### Target

希望改善到什么水平。

结构：

```text
Baseline
↓
Metric
↓
Target
```

如果当前没有真实数据：

> 不要虚构 Target。

可以先标记：

```text
Baseline: TBD
Target: TBD
```

等 Workflow 实际运行以后再建立 Baseline。

---

## 0.8 MVP Success Criteria

MVP 不一定需要证明所有长期 Business Outcomes。

应该优先验证：

- Workflow 是否可以稳定运行？
- 是否真正减少 Manual Work？
- 数据是否可以稳定获取？
- Output 是否具有实际业务价值？
- AI Analysis 是否达到可接受水平？
- Human 是否愿意使用结果？
- 是否值得继续投入下一阶段？

避免 MVP 一开始承担过多目标。

---

## 0.9 Business Problem Analysis Template

```text
Business Problem:

Current Situation / As-Is Workflow:
- Current Trigger:
- Main Steps:
- Current Tools:
- People Involved:
- Current Output:

Pain Points:
1.
2.
3.

Root Causes / Constraints:
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

Metric 1:
Baseline:
Target:

Metric 2:
Baseline:
Target:

MVP Success Criteria:
-
```

---

## 0.10 Business Problem Analysis Questions

1. 当前业务真正是怎么运行的？
2. Workflow 从什么业务事件开始？
3. 当前有哪些主要步骤？
4. 谁负责每一步？
5. 哪些步骤最耗时间？
6. 哪些步骤重复最多？
7. 哪些步骤容易出错或遗漏？
8. 哪些结果容易出现不一致？
9. 哪些步骤无法随着业务量扩大？
10. Pain Point 背后的 Root Cause 是什么？
11. 哪些问题适合 Rule-based Automation？
12. 哪些问题适合 AI-assisted？
13. 哪些 Decision 必须 Human-controlled？
14. Automation 真正希望改变什么？
15. 如何衡量 Automation 是否有效？
16. 当前 Baseline 是什么？
17. Target 是什么？
18. MVP 最先需要证明什么？

---

## Business Problem Design Principle

> Understand the business before designing the automation.

推荐分析顺序：

```text
As-Is Workflow
↓
Pain Points
↓
Root Causes
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

Technology Selection 应发生在 Business Problem 和 Workflow Analysis 之后。

# 1. Trigger

> 什么情况下 Workflow 开始运行？

Trigger 分析不仅要确定“什么时候启动”，还需要区分：

**Trigger → Upstream Dependency → Precondition → Execution Rule → Failure / Skip Handling**

这些概念不能混在一起。

---

## 1.1 Trigger Types

### Event Trigger

某个业务事件发生时启动。

Examples:

- 用户提交表单
- 收到新邮件
- 上传新文件
- 创建新订单
- 上游 Workflow 完成

### Schedule Trigger

按照固定时间运行。

Examples:

- 每天 09:00
- 每小时
- 每周一
- 每月最后一天

### Manual Trigger

由人工主动启动。

Examples:

- 点击 Run
- 点击“重新分析”
- 人工批准后启动下一流程

### Data Trigger

数据发生变化或达到某个条件时启动。

Examples:

- Status changed to Approved
- Database receives a new record
- Score crosses a threshold
- Inventory falls below a threshold

### External Trigger / Webhook

由外部系统发送事件启动。

Examples:

- Webhook
- SaaS Event
- API Callback

---

## 1.2 Trigger

> What starts the workflow?

需要明确：

- 什么事情真正启动 Workflow？
- 谁触发？
- Trigger Type 是什么？
- Trigger 来源是什么？
- 多久触发一次？
- 是否存在多个 Trigger？
- 是否允许重复触发？

---

## 1.3 Upstream Dependency

> What upstream workflow or data does this workflow depend on?

一个 Workflow 可以由 Schedule Trigger 启动，同时依赖其他 Workflow 已经产生的数据。

Examples:

```text
Workflow A
↓
Produces Data
↓
Database
↓
Weekly Schedule Trigger
↓
Workflow B reads the data
```

Workflow B 的 Trigger 仍然是 Schedule Trigger。

Workflow A / Database Data 属于：

**Upstream Dependency**

而不是 Trigger。

需要检查：

- 当前 Workflow 依赖哪些上游 Workflow？
- 上游需要产生什么数据？
- 上游 Workflow 是否必须成功完成？
- 是否依赖历史数据？
- Dependency 不满足时怎么办？

---

## 1.4 Precondition

> What must already be true before the workflow can proceed?

Precondition 是 Workflow 启动后继续执行必须满足的条件。

Examples:

```text
Schedule Trigger
Sunday 10:00
↓
Check Priority Post Pool
↓
Pool contains records?
↓
Yes → Continue
No → Skip
```

其中：

Sunday 10:00
→ Trigger

Priority Post Pool contains records
→ Precondition

需要检查：

- 是否存在有效 Input？
- 数据量是否达到最低要求？
- 上游数据是否已经准备完成？
- 是否满足运行条件？
- Precondition 不满足时是 Skip、Wait 还是 Alert？

---

## 1.5 Execution Rule

> What rules control how the workflow runs?

Execution Rule 不是 Trigger。

Examples:

- 每次最多处理 4 个关键词
- 每批最多处理 100 条记录
- 只处理 Status = Active 的数据
- Engagement > 500 才进入 Priority Pool

需要检查：

- 每次处理多少数据？
- 数据选择规则是什么？
- 是否存在 Priority？
- 是否存在 Threshold？
- 是否需要 Batch Processing？
- 是否存在运行频率限制？

---

## 1.6 Failure / Skip Handling

> What happens when the workflow cannot run normally?

需要检查：

- Trigger 失败怎么办？
- Upstream Dependency 不满足怎么办？
- Precondition 不满足怎么办？
- 是否 Skip？
- 是否 Wait？
- 是否 Retry？
- Retry 几次？
- 是否需要补跑？
- 是否需要通知人工？
- 是否记录 Skip / Failure 原因？

---

## 1.7 Trigger vs Dependency vs Precondition vs Decision

必须区分：

### Trigger

**什么时候启动 Workflow？**

Example:

```text
Every Sunday at 10:00
```

### Upstream Dependency

**Workflow 依赖什么上游流程或数据？**

Example:

```text
Analyzed Post Library
```

### Precondition

**Workflow 启动以后，什么条件必须成立才能继续？**

Example:

```text
Analyzed Post Library contains valid records
```

### Decision

**Workflow 运行过程中，根据什么条件决定下一步？**

Example:

```text
Engagement > 500?
↓
Yes → Priority Post
No → Normal Post
```

### Execution Rule

**Workflow 运行时遵守什么规则？**

Example:

```text
Maximum 4 seed keywords per run
```

---

## 1.8 Trigger Analysis Template

### Workflow Name

TODO

**Trigger Type:**

TODO

**Trigger Condition:**

TODO

**Upstream Dependencies:**

TODO

**Preconditions:**

TODO

**Execution Rules:**

TODO

**Failure / Skip Handling:**

TODO

**Execution Mode:**

- [ ] Real-time
- [ ] Batch Processing
- [ ] Scheduled Batch
- [ ] Event-driven
- [ ] Manual

---

## 1.9 Trigger Analysis Questions

For every workflow, ask:

1. What actually starts this workflow?
2. What type of trigger is it?
3. Does it depend on another workflow?
4. What upstream data must already exist?
5. What preconditions must be satisfied?
6. What execution rules control the run?
7. Is this real-time or batch processing?
8. What happens if no valid data exists?
9. What happens if the upstream workflow fails?
10. Does the workflow need Retry or Recovery?
11. Could duplicate execution occur?
12. Does the workflow need Manual Override?

---

## Trigger Design Principle

> Dependency determines what the workflow needs before it can work.  
> Trigger determines when the workflow starts.

Do not treat every condition as a Trigger.

A mature workflow should clearly separate:

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

# 2. Input

> Workflow 被 Trigger 启动以后，需要哪些数据、参数或配置才能继续运行？

Input Analysis 不只是回答：

> 系统需要什么数据？

还需要分析：

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

核心目标：

> 为后续 Process 提供结构清晰、格式统一、质量已知、时间明确、可以正常使用的数据。

---

## 2.1 Input Types

### User Input

人工提供的数据。

Examples:

- Form
- Keyword
- File
- User Settings

### System Input

系统内部已经存在的数据。

Examples:

- Database
- Historical Data
- Previous Results
- User Profile

### External Input

外部平台、API 或其他系统提供的数据。

Examples:

- SaaS API
- Social Media Data
- CRM
- Email
- Website

### Knowledge Input

AI 判断需要参考的知识。

Examples:

- Knowledge Base
- Documents
- Case Library
- SOP
- Historical Examples

### Configuration Input

控制 Workflow 行为的参数。

Examples:

- Threshold
- Time Range
- Maximum Results
- Scoring Rules
- Filter Rules

### System-generated Input

由系统自己产生的数据。

Examples:

- Timestamp
- Workflow Run ID
- Calculated Status
- Previous Workflow Output

---

## 2.2 Source

> 数据从哪里来？

分析每个 Input 时首先明确 Source。

常见 Source：

```text
Human
Database
Previous Workflow
API
File
External Platform
System
AI
Configuration
```

需要问：

- 谁产生这个数据？
- Workflow 从哪里获得？
- 是否依赖 External System？
- Source 不可用时怎么办？

---

## 2.3 Fields

不要只定义模糊的数据对象。

应该进一步拆解：

> Workflow 实际需要哪些 Fields？

例如：

```text
Business Object
├── ID
├── Name
├── Status
├── Created At
└── Other Fields
```

字段应该围绕后续 Process 的真实需要设计。

避免：

> 因为“以后可能有用”而无限采集数据。

---

## 2.4 Requirement

判断字段缺失以后：

> Workflow 是否还能正常运行？

常见类型：

```text
Required / Non-null
Required / Empty Allowed
Optional
```

### Required / Non-null

字段必须存在，并具有有效值。

### Required / Empty Allowed

字段必须存在，但业务上允许没有内容。

### Optional

字段缺失也不会影响 Workflow 正常运行。

---

## 2.5 Empty vs Missing

必须区分：

```text
Empty ≠ Missing
```

### Empty

字段存在，但 Source 本身没有内容。

例如：

```text
tags = []
```

### Missing

理论上应该获得数据，但系统没有成功获取。

例如：

```text
tags = null
```

如果数据本来存在但采集失败，则属于 Data Quality Issue。

因此：

> 字段没有内容，不一定代表采集失败。

---

## 2.6 Common Data Types

常见 Data Types：

| Data Type | Meaning | Example |
|---|---|---|
| String | 文本 | `"example"` |
| Integer | 整数 | `1250` |
| Float / Number | 小数 / 数值 | `4.5` |
| Boolean | 是 / 否 | `true / false` |
| Array / List | 一组数据 | `["A", "B"]` |
| Datetime | 日期 + 时间 | `2026-08-28 14:30` |
| Object | 结构化对象 | `{"name": "A", "count": 10}` |
| Enum | 只能从预设值中选择 | `Active / Inactive` |

注意：

```text
"1250" → String
1250   → Integer
```

Data Type 应根据数据未来如何被使用来决定。

例如：

> ID 即使由数字组成，如果主要用于识别对象而不是计算，通常可以使用 String。

---

## 2.7 Input vs Configuration vs Process vs Decision

需要区分：

### Input

系统需要什么。

### Configuration

当前参数设置是什么。

### Process

系统拿到 Input 后执行什么操作。

### Decision

系统根据什么条件决定下一步。

例如：

```text
Input:
Time Range

Configuration:
Last 7 Days

Process:
Filter Data by Time Range

Decision:
Score > Threshold?
```

不要把 Configuration、Process 或 Decision Rule 混进 Input 定义。

---

## 2.8 Normalization

Normalization 是：

> 将来源不同、格式不同的数据转换成系统统一使用的标准格式。

推荐处理顺序：

```text
Raw Data
↓
Normalization / Transformation
↓
Validation
↓
Eligible Data
↓
Process
```

常见 Normalization：

- String → Integer / Number
- Relative Time → Datetime
- String → Array
- Trim Whitespace
- Remove Duplicate Values
- Remove Unnecessary Characters
- Standardize Date Format
- Standardize Enum Values
- Standardize Units

Example:

```text
Raw:
"1.2万"

↓ Normalize

12000

↓ Validate

Integer
Value >= 0
```

核心区别：

> Normalization 负责统一数据；Validation 负责判断数据能不能用。

---

## 2.9 Validation

Validation 是：

> 检查数据是否符合系统和业务要求。

常见 Validation：

### Required Validation

```text
Value != null
Value != ""
```

### Data Type Validation

```text
String
Integer
Array<String>
Datetime
```

### Format Validation

例如：

```text
ID Format
URL Format
Email Format
Datetime Format
```

### Value Range Validation

例如：

```text
Value >= 0
```

### Allowed Value Validation

例如：

```text
Status ∈ [Active, Inactive, Retired]
```

### Existence / Availability Validation

检查数据指向的真实对象是否存在或可以访问。

### Cross-field Validation

一个 Field 是否正确，需要结合其他 Field 判断。

### Completeness Validation

数据存在不代表数据完整。

需要判断：

```text
Is the data complete enough for downstream processing?
```

---

## 2.10 Data Quality Status

真实系统不应该只有：

```text
Valid
Invalid
```

可以进一步区分：

```text
Valid
Incomplete
Missing
Invalid
Unavailable
```

### Valid

数据符合要求，可以正常使用。

### Incomplete

数据已经获得，但不完整。

原则：

> Incomplete Data ≠ No Business Value.

是否继续使用，应根据业务价值判断。

### Missing

应该存在的数据没有成功获得。

### Invalid

数据存在，但违反格式或业务规则。

### Unavailable

原始 Business Object 已经无法访问。

Examples:

- Deleted
- Private
- Access Restricted
- No Longer Exists

---

## 2.11 Missing / Invalid Handling

发现数据问题以后，不应该机械执行：

```text
Invalid
↓
Delete
```

应该先判断原因：

```text
Missing / Incomplete / Invalid
            ↓
      Determine Reason
            ↓
├── Source 本身没有数据
│   → Valid Empty
│
├── Temporary Error
│   → Retry
│
├── Format 不统一
│   → Normalize / Transform
│
├── Current Method 无法获取完整数据
│   → Alternative Source / Method
│
├── Partial Data
│   → Keep + Mark Incomplete
│
├── Invalid Data
│   → Reject / Skip / Manual Review
│
└── Source Object 无法访问
    → Mark Unavailable
```

核心原则：

> Missing Data Handling 应根据 Failure Reason 决定，而不是所有异常都使用同一种处理方式。

---

## 2.12 Retry & Failure Reason

临时错误可以 Retry。

Examples:

- Network Timeout
- API Timeout
- Temporary Service Error
- Rate Limit

基本逻辑：

```text
Attempt
↓
Failed
↓
Retry
↓
Retry Limit Reached?
├── No → Retry
└── Yes → Stop + Record Failure
```

原则：

> Retry 必须存在上限，不能无限执行。

同时应该尽可能记录 Failure Reason：

```text
Network Error
API Error
Timeout
Rate Limit
Parsing Error
Permission Error
Source Unavailable
Unknown
```

Failure Reason 可以帮助后续定位和优化 Workflow。

---

## 2.13 Data Freshness

数据不仅需要正确，还需要知道：

> 这个数据是什么时候产生、采集或更新的？

常见字段：

```text
Created At
Published At
Collected At
Updated At
Analyzed At
Tracked At
```

需要区分：

```text
Source Time
≠
System Collection Time
```

Freshness Analysis 可以问：

- When was the data generated?
- When was it collected?
- When was it last updated?
- Is it still fresh enough for this Workflow?

---

## 2.14 Timezone

Datetime 数据需要考虑 Timezone。

不同 Source 可能使用：

```text
UTC
UTC+8
Local Time
```

跨系统 Workflow 应明确：

- Source Timezone
- System Timezone
- 是否需要统一转换
- 最终保存的标准

核心原则：

> Datetime 不只是日期和时间，还需要明确 Timezone。

---

## 2.15 Current State vs History

需要区分：

```text
Current State
```

和：

```text
History
```

Current State 回答：

> 现在是什么？

History 回答：

> 它是怎么变化的？

例如：

```text
Week 1 = 20
Week 2 = 50
Week 3 = 100
```

才能进行 Trend Analysis。

如果 Workflow 未来需要：

- Trend Analysis
- Performance Analysis
- State Change Analysis

就需要考虑 Historical Observation，而不是只覆盖保存最新值。

---

## 2.16 Historical Observation

通用结构：

```text
Observation
├── Object ID
├── Observed At
└── Observed Values
```

例如：

```text
Object
↓
Observation 1
↓
Observation 2
↓
Observation 3
↓
Trend Analysis
```

是否保存 History 应根据业务价值决定。

---

## 2.17 Raw Data vs Derived Data

### Raw Data

从 Source 直接获得的数据。

### Derived Data

通过 Raw Data 计算、转换或推导得到的数据。

例如：

```text
Raw Data
├── Value A
├── Value B
└── Value C

Derived Data
└── Total = A + B + C
```

原则：

> 重要 Raw Data 与 Derived Data 尽量分开保存。

这样未来计算逻辑发生变化时，仍然可以重新计算。

---

## 2.18 Data Relationship

除了分析单个 Field，还需要考虑 Business Objects 之间的 Relationship。

常见关系：

```text
One-to-One
One-to-Many
Many-to-Many
```

当同一个 Business Object 可能通过多个：

- Sources
- Keywords
- Workflows
- Conditions

被发现时，需要考虑是否应该保存这些 Relationships。

---

## 2.19 Deduplication vs Relationship Preservation

Deduplication 的目标是：

> 避免同一个 Business Object 被重复创建。

但：

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
→ Only One Object

Source A → Object 001
Source B → Object 001
→ Preserve Relationships
```

因此：

> 去重时不仅要考虑哪些 Object 不应该重复，还要考虑哪些有价值的 Relationship 必须保留。

---

## 2.20 Progressive Data Enrichment

不是所有数据都必须在 Workflow 第一阶段全部获取。

可以采用：

> Progressive Data Enrichment

流程：

```text
Collect Minimum Required Data
↓
Initial Screening
↓
Determine Business Value
↓
Collect Additional / Expensive Data
↓
Deep Processing / Analysis
```

适用于：

- API 调用有成本
- Data Collection 成本较高
- AI Token 成本较高
- 深度数据量很大
- 只有部分 Business Objects 值得进一步分析

原则：

> 先以最低必要成本判断 Business Value，再为高价值对象补充更深的数据。

---

## 2.21 Input Specification

完成 Input Analysis 后，可以整理成 Input Specification。

通用表格：

| Field | Source | Data Type | Requirement | Normalization | Validation | Missing / Invalid Handling | Freshness |
|---|---|---|---|---|---|---|---|
| | | | | | | | |

也可以使用：

```text
Field:

Source:

Data Type:

Requirement:
- Required / Non-null
- Required / Empty Allowed
- Optional

Normalization:

Validation:

Missing / Invalid Handling:

Failure Reason:

Freshness:

Timezone:

History:

Relationship:
```

Input Specification 的目的不是制造文档，而是：

> 让后续 Implementation 清楚知道系统需要什么数据，以及什么样的数据才可以被使用。

---

## 2.22 Input Analysis Questions

For every workflow, ask:

1. Workflow 需要什么数据才能运行？
2. 每个 Input 来自哪里？
3. 需要哪些具体 Fields？
4. 哪些 Required？哪些 Optional？
5. Empty 是否允许？
6. 每个 Field 的 Data Type 是什么？
7. Raw Data 是否需要 Normalization？
8. Normalized Data 应满足什么 Validation？
9. 数据是否完整？
10. Missing / Invalid / Incomplete 时怎么办？
11. 是否需要 Retry？
12. 是否需要记录 Failure Reason？
13. 数据是否存在 Freshness 要求？
14. Datetime 是否需要考虑 Timezone？
15. 是否需要 Current State 还是 Historical Data？
16. 哪些是 Raw Data？哪些是 Derived Data？
17. Business Objects 之间是否存在 Relationship？
18. Deduplication 是否会导致 Relationship 丢失？
19. 是否可以通过 Progressive Data Enrichment 降低成本？
20. 是否已经形成清晰的 Input Specification？

---

## Input Design Principle

Input Analysis 不只是：

> What data do we need?

而应该完整考虑：

```text
What Data?
↓
From Where?
↓
What Fields?
↓
What Data Type?
↓
Normalize?
↓
Valid?
↓
Complete?
↓
If Not, What Happens?
↓
Fresh Enough?
↓
Need History?
↓
Need Relationships?
↓
How Much Data Do We Really Need Now?
```

最终：

```text
Good Input
=
Correct Structure
+
Consistent Format
+
Valid Data
+
Known Quality
+
Known Time
+
Traceable History
+
Preserved Relationships
```

# 3. Process

> Input 进入系统后，需要经历哪些处理？

## Common Process Types

### Collect

采集数据。

### Validate

检查数据是否完整、合法。

### Clean

清理错误、无效数据。

### Normalize

统一数据格式。

### Deduplicate

删除重复数据。

### Transform

转换数据结构。

### Enrich

补充额外数据。

### Analyze

分析数据。

### Aggregate

汇总数据。

### Store

保存结果。

## Process Questions

- 数据首先需要做什么？
- 是否需要 Validate？
- 是否需要 Clean？
- 是否需要 Normalize？
- 如何 Deduplicate？
- 是否需要 Transform？
- 是否需要计算新的字段？
- 是否需要调用外部 API？
- 哪些步骤需要 AI？
- 哪些步骤只需要普通程序？
- 是否需要保存中间结果？
- Process 是否存在顺序依赖？
- 每一步失败怎么办？

## Generic Process Flow

```text
Raw Input
↓
Collect
↓
Validate
↓
Clean
↓
Normalize
↓
Deduplicate
↓
Transform
↓
Enrich
↓
Analyze
↓
Aggregate
↓
Store
```

## Actual Project Process

```text
TODO
```

---

# 4. Decision

> Workflow 中需要做哪些判断？

核心问题：

**这个判断应该由 Rule、AI、Hybrid，还是 Human 完成？**

## Decision Types

### Rule-based Decision

适用于存在明确规则、公式、条件或阈值的判断。

Examples:

```text
score > 80
price < 100
status == "active"
interaction > 500
```

### AI-based Decision

适用于需要语义理解、上下文理解或处理非结构化内容的判断。

Examples:

- 这篇内容主要讨论什么？
- 这封邮件是什么意图？
- 两篇内容是否讨论同一个问题？
- 这条内容与业务是否相关？

### Hybrid Decision

Rule + AI 共同判断。

Example:

```text
Rule Filter
↓
AI Analysis
↓
Final Score
```

### Human Decision

风险高、主观性强或必须由人承担最终责任的判断。

Examples:

- 最终是否发布
- 是否批准
- 是否接受 AI 建议
- 是否涉及业务风险

## Decision Questions

- 要判断什么？
- 判断依据是什么？
- Rule / AI / Hybrid / Human？
- 是否存在明确 Threshold？
- AI 是否需要输出 Confidence？
- Confidence 太低怎么办？
- 是否存在 Edge Case？
- 是否允许人工 Override？
- 是否需要记录判断理由？
- 判断错误会产生什么后果？

## Decision Table

| Decision | Type | Criteria | Threshold / Confidence | Fallback |
|---|---|---|---|---|
| | | | | |

---

# 5. Action

> Decision 完成以后，系统真正执行什么？

## Action Types

### Data Action

- Create
- Update
- Delete
- Tag
- Store

### Communication Action

- Email
- SMS
- Slack
- Feishu
- Notification

### System Action

- API Call
- Start Workflow
- Generate File
- Update SaaS

### AI Action

- Summarize
- Classify
- Extract
- Generate
- Recommend

### Human Action

- Review
- Approve
- Edit
- Reject
- Escalate

## Action Questions

- 谁执行 Action？
- 对哪个系统执行？
- Action 的 Input 是什么？
- 需要什么权限？
- 成功标准是什么？
- 失败怎么办？
- 是否需要 Retry？
- Retry 几次？
- 是否可能重复执行？
- 如何避免 Duplicate Action？
- 是否需要 Rollback？
- 是否需要通知人工？
- 是否需要记录 Action Log？

## Action Table

| Action | Type | Target | Success Condition | Failure Handling |
|---|---|---|---|---|
| | | | | |

---

# 6. Output

> Workflow 最终产生什么？

## Output Types

### Business Output

业务人员真正需要的结果。

Examples:

- Report
- Recommendation
- Qualified Lead
- Content Topics

### Data Output

系统产生的数据。

Examples:

- Score
- Database Record
- Classification Result
- Trend Data

### System Output

提供给其他系统的数据。

Examples:

- JSON
- API Response
- Webhook
- CSV

### Operational Output

用于系统运行和维护的数据。

Examples:

- Run Log
- Error Log
- Execution Time
- API Usage

## Output Questions

- 谁使用这个 Output？
- Output 用来做什么？
- 输出格式是什么？
- 输出到哪里？
- 多久输出一次？
- 是否需要排序？
- 是否需要筛选？
- 是否需要保存历史？
- 是否可以追溯来源？
- 是否需要 Evidence？
- Output 错误如何发现？
- 什么才算有价值的 Output？

## Output Table

| Output | Type | User | Format | Destination |
|---|---|---|---|---|
| | | | | |

---

# 7. Human-in-the-loop

> 哪些步骤必须保留人工参与？

## Questions

- 哪些 Decision 风险较高？
- 哪些结果必须人工确认？
- AI Confidence 低于多少需要人工介入？
- 人工可以修改 AI 结果吗？
- 人工可以 Override 系统判断吗？
- 人工反馈是否重新进入系统？
- 最终责任人是谁？

## Human Review Points

| Step | Why Human Review Is Needed | Reviewer | Action |
|---|---|---|---|
| | | | |

---

# 8. Error Handling

> Workflow 出错以后怎么办？

## Common Errors

- Trigger Failure
- Missing Input
- Invalid Data
- Duplicate Data
- API Failure
- Authentication Failure
- Timeout
- Rate Limit
- AI Invalid Output
- AI Low Confidence
- Database Failure
- Duplicate Execution
- Partial Workflow Failure

## Error Handling Questions

- 是否 Retry？
- Retry 几次？
- Retry 间隔多久？
- 是否需要备用方案？
- 是否需要人工介入？
- 是否发送 Error Notification？
- 是否记录错误原因？
- Workflow 从哪里恢复？
- 是否需要 Dead Letter / Failed Queue？

---

# 9. Logging & Monitoring

> 如何知道 Workflow 是否正常运行？

## Suggested Logs

- Workflow Run ID
- Start Time
- End Time
- Status
- Input Source
- Number of Records
- Process Result
- Decision Result
- Action Result
- Error
- Retry Count
- API Usage
- AI Usage
- Cost

## Questions

- 如何知道 Workflow 正常运行？
- 如何知道今天少处理了数据？
- 如何定位失败步骤？
- 如何追踪某个 Output 的来源？
- 是否需要 Dashboard？
- 是否需要 Alert？

---

# 10. Security & Privacy

## Check

- API Key
- OAuth Token
- Password
- Personal Data
- Confidential Business Data
- Access Control
- Environment Variables
- Data Storage
- Data Retention

## Questions

- 哪些数据属于敏感数据？
- 谁可以访问？
- API Key 保存在哪里？
- 是否应该使用 `.env`？
- 是否需要加密？
- 数据需要保存多久？
- 是否应该删除某些 Raw Data？
- 第三方服务能访问哪些数据？

---

# 11. Cost

## Cost Sources

- LLM API
- SaaS Subscription
- Automation Platform
- Database
- Hosting
- Third-party API

## Questions

- 每次 Workflow Run 成本是多少？
- 每天运行多少次？
- 每月预计成本是多少？
- 哪些步骤最贵？
- 是否所有数据都需要调用 LLM？
- 是否可以先 Rule Filter，再调用 AI？
- 是否可以 Batch Processing？
- 是否需要设置 Cost Limit？

---

# 12. Performance & Scalability

## Check

- Execution Time
- Data Volume
- API Rate Limit
- Concurrency
- Queue
- Batch Processing
- Timeout

## Questions

- 一次处理多少数据？
- 每天处理多少数据？
- Workflow 最长允许运行多久？
- 数据增加 10 倍还能运行吗？
- 哪些步骤可能成为 Bottleneck？
- 是否需要 Batch？
- 是否需要 Queue？
- 是否存在 API Rate Limit？

---

# 13. Business Outcome

> Automation 最终解决了什么业务问题？

不要只评价：

> Workflow 是否运行成功。

应该评价业务结果。

## Time Saved

Before：

After：

## Accuracy

Before：

After：

## Manual Work Reduction

Before：

After：

## Error Reduction

Before：

After：

## Business Impact

- Revenue：
- Conversion：
- Response Time：
- Productivity：
- Risk Reduction：

---

# 14. Technology Mapping

> 完成业务分析以后，最后才选择技术。

| Requirement | Possible Technology | Why |
|---|---|---|
| Trigger | | |
| Data Collection | | |
| Workflow | | |
| AI | | |
| API Integration | | |
| Database | | |
| Notification | | |
| Deployment | | |
| Monitoring | | |

核心原则：

> Business Requirement First, Technology Second.

---

# 15. Final Workflow Architecture

完成前面的业务分析后，再设计最终技术架构。

```text
Trigger
   ↓
Input
   ↓
Validate
   ↓
Process
   ↓
Decision
 ┌─────┼─────┐
Rule   AI   Human
 └─────┼─────┘
       ↓
     Action
       ↓
 Human Review
       ↓
     Output
       ↓
Business Outcome
```

---

# 16. Project Summary

## Business Problem

TODO

## Current Workflow

TODO

## Pain Points

TODO

## Proposed Solution

TODO

## Main Workflow

TODO

## AI Responsibilities

TODO

## Rule-based Responsibilities

TODO

## Human Responsibilities

TODO

## Main Risks

TODO

## Success Metrics

TODO