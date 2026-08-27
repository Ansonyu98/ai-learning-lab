# Workflow Analysis Framework

> A reusable framework for analyzing Business Process Automation and AI Automation projects.

## Core Principle

**Business Problem → Workflow Analysis → Solution Design → Technology → Build → Test → Deliver**

核心原则：

> Business Requirement First, Technology Second.

不要因为会某个工具，就强行用某个工具解决所有问题。

---

# 0. Business Problem

## Current Situation

- 当前业务流程是什么？
- 现在由谁完成？
- 当前使用哪些工具或系统？
- 当前流程需要多长时间？
- 当前流程涉及哪些人员？

## Pain Points

- 哪些步骤重复？
- 哪些步骤最耗时？
- 哪些步骤容易出错？
- 哪些步骤容易遗漏？
- 哪些步骤依赖人工判断？
- 当前最大的流程瓶颈是什么？

## Automation Goal

- 为什么需要自动化？
- 希望减少哪些人工工作？
- 希望 AI 解决什么问题？
- 哪些问题不应该交给 AI？
- 自动化之后理想流程是什么？

## Success Metrics

- Time Saved：
- Cost Reduced：
- Accuracy：
- Error Reduction：
- Manual Work Reduction：
- Revenue / Conversion：
- Other：

---

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

> Workflow 开始以后，需要哪些数据？

## Input Types

### User Input

人工提供的数据。

Examples:

- 表单
- Keyword
- 文件
- 用户设置

### System Input

系统内部已经存在的数据。

Examples:

- Database
- Historical Data
- Previous Results
- User Profile

### External Input

外部平台或 API 提供的数据。

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
- Frequency
- Maximum Results
- Scoring Rules
- Filter Rules

## Input Questions

- 数据来自哪里？
- 谁提供？
- 数据格式是什么？
- Required Fields 是什么？
- Optional Fields 是什么？
- 是否可能缺失？
- 是否可能重复？
- 数据是否可信？
- 是否需要清洗？
- 是否需要验证？
- 是否保存 Raw Data？
- 是否需要历史数据？
- 数据量有多大？
- 是否需要 API Authentication？
- 是否包含敏感数据？

## Input Table

| Input | Type | Source | Format | Required | Notes |
|---|---|---|---|---|---|
| | | | | | |

---

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