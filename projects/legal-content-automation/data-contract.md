# Data Contract — Legal Content Automation

**Project:** Legal Content Automation  
**Document Type:** Logical Data Contract  
**Stage:** Pre-Implementation Design  
**Status:** Approved for Architecture Design

---

# 1. Purpose

本文件定义 Legal Content Automation MVP 中跨 Workflow 使用的核心业务对象、字段、状态、关系、数据质量规则和 Input / Output Contract。

Data Contract 的目标是保证：

```text
Task A
Task B
Task C
Task D
Task E
Task F
Task G
Feishu Human Review
Database
AI Processing
```

对同一业务对象具有一致理解。

本文件属于：

```text
Logical Data Contract
```

而不是：

```text
Physical Database Schema
```

因此当前定义：

- Object
- Field
- Data Type
- Required / Optional
- State
- Relationship
- Validation Rule
- Cross-workflow Contract

暂不规定：

- PostgreSQL Table DDL
- Index
- Foreign Key Implementation
- JSONB / Relational Storage Choice
- Vector Schema
- API Endpoint Schema
- n8n Node Configuration

这些在 Architecture / Implementation 阶段确定。

---

# 2. Core Data Principles

## 2.1 Normalize Before Validate

所有外部数据：

```text
Raw Data
↓
Normalization
↓
Validation
↓
Persistence
↓
Business Logic
```

不得直接将 Platform-specific Raw Data 作为下游标准业务对象。

---

## 2.2 Null ≠ Empty String

统一原则：

```text
null
=
value unavailable / not provided / not applicable
```

```text
""
=
a real string value that happens to be empty
```

原则上：

> 不使用 Empty String 代替 Missing Value。

---

## 2.3 Missing ≠ Zero

例如：

```text
comment_count = null
```

表示：

> 无法获取评论数。

而：

```text
comment_count = 0
```

表示：

> 已确认评论数为 0。

两者不得混淆。

---

## 2.4 Timestamp Standard

所有系统内部 Datetime：

```text
ISO 8601
+
Timezone-aware
```

必须区分：

```text
published_at
collected_at
observed_at
generated_at
decided_at
created_at
updated_at
```

不得使用一个：

```text
time
```

字段表达不同业务时间。

---

## 2.5 Preserve Raw Source

Normalization 后仍应保留必要的：

```text
raw_payload
or
raw_source_reference
```

用于：

- Debugging
- API Field Change Investigation
- Data Recovery
- Future Reprocessing

是否完整长期保存 Raw Payload：

Architecture 阶段结合 Storage Cost 决定。

---

# 3. Core Object Model

MVP 核心对象：

```text
Keyword
SearchHit
Post
BasicAnalysis
EngagementObservation
LawyerDecision
TrackingState
DeepAnalysisRequest
SelectedComment
ResearchSubject
LongTailCandidate
CaseRecord
CaseMatch
CandidateTopic
TopicFeedback
KeywordHistory
WorkflowRun
DeliveryRecord
```

---

# 4. Core Relationship Overview

```text
Keyword
  │
  └──< SearchHit >── Post
                      │
                      ├── BasicAnalysis
                      │
                      ├──< EngagementObservation
                      │
                      ├──< LawyerDecision
                      │
                      ├── TrackingState
                      │
                      └──< DeepAnalysisRequest
                                │
                                ├──< SelectedComment
                                │
                                └── ResearchSubject
                                       │
                                       ├──< LongTailCandidate
                                       │
                                       ├──< CaseMatch >── CaseRecord
                                       │
                                       └──< CandidateTopic
                                                │
                                                ├──< LawyerDecision
                                                └── TopicFeedback

Keyword
  │
  └──< KeywordHistory

Workflow
  │
  └──< WorkflowRun

Feishu Delivery
  │
  └── DeliveryRecord
```

---

# 5. Object — Keyword

## Purpose

表示系统当前或历史使用过的搜索关键词。

Keyword 不等于 LongTailCandidate。

```text
LongTailCandidate
↓
Lawyer Approval
↓
Keyword
```

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| keyword_id | string | Yes | Internal unique identifier |
| keyword_text | string | Yes | Normalized search keyword |
| keyword_type | enum | Yes | seed / long_tail |
| lifecycle_status | enum | Yes | active / observe / reduced / retired |
| platform_scope | array[string] | Yes | Eligible platforms |
| created_at | datetime | Yes | Creation time |
| updated_at | datetime | Yes | Latest update |
| source_long_tail_candidate_id | string/null | No | Source candidate if promoted from long-tail |
| config | object/null | No | Keyword-specific search configuration |

---

## Lifecycle

```text
Seed Keyword
↓
active
↓
reduced
↓
retired
```

Long-tail Keyword：

```text
LongTailCandidate
↓
Lawyer Approve
↓
observe
↓
active / reduced / retired
```

---

## Validation

```text
keyword_text
```

不得：

- null
- empty
- whitespace-only

Normalized duplicate keywords 应避免重复创建。

---

# 6. Object — SearchHit

## Purpose

记录：

> 某个 Keyword 在某次 Search 中发现了某个 Post。

因此：

```text
Post ≠ SearchHit
```

同一 Post 可以由多个 Keyword 找到。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| search_hit_id | string | Yes | Unique identifier |
| keyword_id | string | Yes | Source Keyword |
| post_id | string | Yes | Matched Post |
| platform | string | Yes | Source platform |
| workflow_run_id | string | Yes | Search workflow run |
| rank | integer/null | No | Result rank if available |
| search_query | string | Yes | Actual query used |
| collected_at | datetime | Yes | Search collection time |
| raw_search_metadata | object/null | No | Platform/provider-specific metadata |

---

## Deduplication

Recommended logical uniqueness:

```text
workflow_run_id
+
keyword_id
+
post_id
```

重复 Retry 不得重复创建相同 SearchHit。

---

# 7. Object — Post

## Purpose

表示一个唯一的 Social Content Post。

---

## Identity

Logical identity：

```text
platform
+
platform_post_id
```

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| post_id | string | Yes | Internal unique ID |
| platform | string | Yes | xiaohongshu etc. |
| platform_post_id | string | Yes | Platform source ID |
| title | string/null | No | Post title |
| body_text | string/null | No | Available post text |
| author_id | string/null | No | Platform author ID |
| author_name | string/null | No | Display name |
| source_url | string | Yes | Original source URL |
| published_at | datetime/null | No | Original publish time |
| first_collected_at | datetime | Yes | First collection |
| last_collected_at | datetime | Yes | Latest collection |
| tags | array[string] | Yes | Normalized tags; empty array allowed |
| media_type | enum/null | No | text / image / video / mixed / unknown |
| raw_payload | object/null | No | Raw provider data or relevant snapshot |
| created_at | datetime | Yes | Internal creation time |
| updated_at | datetime | Yes | Internal update time |

---

## Validation

Required identity:

```text
platform
platform_post_id
source_url
```

如果：

```text
title = unavailable
```

允许：

```text
title = null
```

不能人为生成一个 Source Title 作为原始数据。

AI 生成标题如未来需要，应存储在 AI Object 中。

---

# 8. Object — BasicAnalysis

## Purpose

保存 Task A 对 Post 的基础 AI 分析。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| basic_analysis_id | string | Yes | Unique ID |
| post_id | string | Yes | Source Post |
| topic_category | string | Yes | AI-generated category |
| summary | string | Yes | Short summary |
| relevance | enum | Yes | relevant / uncertain / irrelevant |
| relevance_reason | string/null | No | AI explanation |
| model | string | Yes | Model identifier |
| prompt_version | string | Yes | Prompt version |
| generated_at | datetime | Yes | Generation time |
| validation_status | enum | Yes | valid / invalid |
| raw_ai_output | object/null | No | Optional raw structured output |

---

## Rule

```text
topic_category
```

由 AI 生成。

律师不需要人工完成 Category Classification。

---

## Downstream Rule

只有：

```text
validation_status = valid
```

才能作为 Candidate Gate 的正式输入。

---

# 9. Engagement Metrics

MVP Engagement：

```text
likes
+
comments
+
saves
```

定义：

```text
total_engagement =
likes + comments + saves
```

仅在三项数据均可靠可用时直接计算。

如果 Provider 存在 Missing Value：

不得默认将 Missing 转换为 0。

---

# 10. Object — EngagementObservation

## Purpose

保存某个 Post 在特定时间点的互动数据快照。

不得直接覆盖旧 Engagement。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| observation_id | string | Yes | Unique ID |
| post_id | string | Yes | Source Post |
| observation_type | enum | Yes | collection / tracking |
| likes | integer/null | No | Like count |
| comments | integer/null | No | Comment count |
| saves | integer/null | No | Save count |
| total_engagement | integer/null | No | Derived total |
| observed_at | datetime | Yes | Observation time |
| provider | string | Yes | Data provider |
| workflow_run_id | string | Yes | Producing workflow |
| raw_metrics | object/null | No | Raw provider values |

---

## Validation

Counts：

```text
integer >= 0
or
null
```

不得为：

```text
negative
string numeric
```

Normalization 必须先完成类型转换。

---

# 11. Object — LawyerDecision

## Purpose

统一保存 Human-in-the-loop Decision History。

核心原则：

```text
Decision ≠ Current State
```

Decision 是事件。

Current State 可以从历史 Decision 和业务对象推导。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| decision_id | string | Yes | Unique ID |
| target_type | enum | Yes | post / candidate_topic / keyword / long_tail_candidate |
| target_id | string | Yes | Target object |
| decision_type | enum | Yes | Decision category |
| decision_value | string/boolean | Yes | Actual decision |
| decision_stage | string | Yes | daily / tracking / weekly / monthly |
| decided_by | string | Yes | User identifier |
| decided_at | datetime | Yes | Decision time |
| source_channel | enum | Yes | feishu / backend / other |
| source_event_id | string/null | No | Idempotency source |
| note | string/null | No | Optional note |
| supersedes_decision_id | string/null | No | Optional logical link to previous decision |

---

## Decision Types

MVP 至少支持：

```text
keep
track
deep_analysis
comment_analysis
topic_approval
keyword_lifecycle
long_tail_promotion
```

---

## History Rule

例如：

```text
Decision 01

decision_type = deep_analysis
decision_value = false
decision_stage = daily
```

Tracking 后：

```text
Decision 02

decision_type = deep_analysis
decision_value = true
decision_stage = tracking
supersedes_decision_id = Decision 01
```

不得修改 Decision 01。

---

## Pending Rule

```text
No LawyerDecision
```

可以代表：

```text
Pending
```

不得人为创建：

```text
decision_value = false
```

表示用户没操作。

---

# 12. Object — TrackingState

## Purpose

表示某个 Post 当前是否处于 Tracking Lifecycle 中。

TrackingState 是 Current Business State。

EngagementObservation 是 Evidence History。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| tracking_state_id | string | Yes | Unique ID |
| post_id | string | Yes | Tracked Post |
| status | enum | Yes | scheduled / waiting / due / completed / cancelled / failed |
| approved_decision_id | string | Yes | Lawyer Track approval |
| initial_observation_id | string | Yes | Day 0 observation |
| followup_observation_id | string/null | No | Follow-up observation |
| tracking_started_at | datetime | Yes | Start |
| next_check_at | datetime | Yes | Eligibility time |
| completed_at | datetime/null | No | Completion |
| absolute_growth | integer/null | No | Calculated growth |
| growth_rate | number/null | No | Percentage / ratio according to implementation convention |
| created_at | datetime | Yes | Creation |
| updated_at | datetime | Yes | Update |

---

## Rule

Tracking Eligibility：

```text
Keep = Yes
+
Track = Yes
```

---

## Observation Window

Business logic：

```text
next_check_at
=
tracking_started_at
+
tracking_window
```

MVP 默认目标：

```text
approximately 7 days
```

具体 Scheduler 实现不得成为 Data Contract 的业务语义。

---

# 13. Growth Calculation

如果：

```text
initial_total_engagement
followup_total_engagement
```

均存在：

```text
absolute_growth =
followup - initial
```

如果：

```text
initial > 0
```

则：

```text
growth_rate =
(followup - initial) / initial
```

如果：

```text
initial = 0
```

不得直接除零。

此时：

```text
growth_rate = null
```

并保留 Absolute Growth。

---

# 14. Object — DeepAnalysisRequest

## Purpose

表示律师批准的一次 Deep Analysis 请求及其处理状态。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| deep_analysis_request_id | string | Yes | Unique ID |
| post_id | string | Yes | Source Post |
| approval_decision_id | string | Yes | Lawyer approval |
| comment_analysis_required | boolean | Yes | Whether comment analysis was approved |
| comment_decision_id | string/null | No | Related comment-analysis decision |
| status | enum | Yes | pending / processing / completed / failed |
| requested_at | datetime | Yes | Request time |
| started_at | datetime/null | No | Processing start |
| completed_at | datetime/null | No | Completion |
| workflow_run_id | string/null | No | Processing workflow |
| error_code | string/null | No | Failure classification |
| error_message | string/null | No | Failure detail |

---

## Idempotency

同一个有效：

```text
Deep Analysis Approval Decision
```

不得创建多个 Active DeepAnalysisRequest。

---

# 15. Object — SelectedComment

## Purpose

保存被选择进入 Deep Analysis 的评论及选择依据。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| selected_comment_id | string | Yes | Internal ID |
| deep_analysis_request_id | string | Yes | Parent request |
| platform_comment_id | string/null | No | Source ID if available |
| post_id | string | Yes | Source Post |
| comment_text | string | Yes | Raw / normalized comment |
| like_count | integer/null | No | Comment likes |
| published_at | datetime/null | No | Comment publish time |
| source_url | string/null | No | Direct source if available |
| selection_reason | enum | Yes | high_like_relevant / latest_fallback |
| relevance | string/null | No | AI/rule relevance metadata |
| selected_at | datetime | Yes | Selection time |

---

## Selection Rule

Preferred：

```text
High-like
+
Strong Relevance
↓
Top 10
```

Fallback：

```text
Latest Comments
```

直到：

```text
up to 10
```

如果实际可获得评论不足 10 条：

允许少于 10。

---

# 16. Object — ResearchSubject

## Purpose

ResearchSubject 是 Task C 的核心 Structured Research Object。

它不是：

```text
Post Summary
```

也不是：

```text
Candidate Topic
```

而是：

> 对一个值得进一步利用的用户问题 / 法律内容研究对象进行结构化表达。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| research_subject_id | string | Yes | Unique ID |
| deep_analysis_request_id | string | Yes | Source request |
| post_id | string | Yes | Primary source Post |
| core_topic | string | Yes | Core research topic |
| user_problem | string | Yes | User problem statement |
| legal_business_issues | array[string] | Yes | Issues worth further research |
| user_expressions | array[object] | Yes | User language + source reference |
| content_opportunities | array[string] | Yes | Potential content/research directions |
| post_evidence | array[object] | Yes | Evidence from original Post |
| comment_findings | array[object] | No | Findings from selected comments |
| comment_evidence | array[object] | No | Comment source references |
| model | string | Yes | Model |
| prompt_version | string | Yes | Prompt version |
| generated_at | datetime | Yes | Generation time |
| validation_status | enum | Yes | valid / invalid |

---

# 17. ResearchSubject — user_expressions

建议 Logical Structure：

```json
{
  "expression": "公司就是想逼我自己走",
  "source_type": "post",
  "source_id": "..."
}
```

或：

```json
{
  "expression": "调岗不同意算旷工吗",
  "source_type": "comment",
  "source_id": "..."
}
```

目的：

> User Expression 必须尽可能保留来源，而不是生成无法验证的“用户语言”。

---

# 18. ResearchSubject — post_evidence

建议结构：

```json
{
  "evidence_type": "statement",
  "content": "...",
  "source_post_id": "...",
  "source_location": null
}
```

MVP 不要求实现复杂 Citation Engine。

但至少应能够：

```text
ResearchSubject
↓
Source Post
```

---

# 19. ResearchSubject — comment_findings

只有：

```text
comment_analysis_required = true
```

且存在有效 Selected Comments 时才产生。

示例逻辑：

```json
{
  "finding": "评论区大量用户进一步询问调岗后旷工风险",
  "supporting_comment_ids": ["...", "..."]
}
```

---

# 20. ResearchSubject Validation

Required：

```text
core_topic
user_problem
legal_business_issues
user_expressions
content_opportunities
post_evidence
```

Array 可以：

```text
[]
```

仅当业务上允许 Valid Empty。

但 Required Array 字段本身不得：

```text
null
```

Structured Output Validation Failure：

不得进入正式 Downstream Research Workflow。

---

# 21. Object — LongTailCandidate

## Purpose

表示 AI 从真实用户表达中发现的潜在 Search Keyword。

LongTailCandidate：

```text
≠ Keyword
```

它只是：

```text
Search Hypothesis
```

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| long_tail_candidate_id | string | Yes | Unique ID |
| normalized_keyword | string | Yes | Normalized candidate |
| raw_expressions | array[string] | Yes | Supporting real expressions |
| source_research_subject_ids | array[string] | Yes | Source research |
| source_post_ids | array[string] | Yes | Source posts |
| occurrence_count | integer | Yes | Number of observed expressions |
| source_count | integer | Yes | Distinct source count |
| related_topics | array[string] | Yes | Related topics |
| status | enum | Yes | accumulating / ready_for_review / approved / rejected / promoted |
| first_observed_at | datetime | Yes | First evidence |
| last_observed_at | datetime | Yes | Latest evidence |
| model | string/null | No | AI model if AI normalization used |
| prompt_version | string/null | No | Prompt version |
| created_at | datetime | Yes | Creation |
| updated_at | datetime | Yes | Update |

---

## Promotion Rule

```text
LongTailCandidate
↓
Monthly Review
↓
Lawyer Approve
↓
Keyword
keyword_type = long_tail
lifecycle_status = observe
```

不得：

```text
LongTailCandidate
↓
Auto Active Keyword
```

---

# 22. Object — CaseRecord

## Purpose

表示线上案例库中的标准案例对象。

当前物理来源：

```text
Unified Excel Case Library
```

未来 Architecture 决定如何同步 / 迁移。

---

## Minimum Logical Fields

由于当前 Case Excel 的最终 Schema 需要在 Architecture 阶段结合实际文件再次 Review，本 Data Contract 暂定义最小公共字段：

| Field | Type | Required | Description |
|---|---|---:|---|
| case_id | string | Yes | Stable case identifier |
| case_title | string/null | No | Case title |
| case_number | string/null | No | Court case number |
| court | string/null | No | Court |
| decision_date | datetime/null | No | Decision date |
| case_type | string/null | No | Case classification |
| issues | array[string] | Yes | Structured issues |
| facts_summary | string/null | No | Structured facts |
| decision_summary | string/null | No | Result summary |
| source_reference | string/null | No | Original judgment / source |
| source_updated_at | datetime/null | No | Source library update time |

---

## Important

本节不得被理解为：

> 替换现有 Excel Schema。

Architecture 阶段必须：

```text
Open Existing Case Library
↓
Review Actual Columns
↓
Map Existing Schema
↓
Decide Online CaseRecord Schema
```

不得凭当前 Logical Contract 删除现有案例库字段。

---

# 23. Object — CaseMatch

## Purpose

保存：

```text
ResearchSubject
↔
CaseRecord
```

之间的匹配结果。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| case_match_id | string | Yes | Unique ID |
| research_subject_id | string | Yes | Research subject |
| case_id | string | Yes | Matched case |
| match_reason | string | Yes | Why relevant |
| match_method | string | Yes | Retrieval/matching method |
| relevance_metadata | object/null | No | Optional score/rank/evidence |
| generated_at | datetime | Yes | Match time |
| model | string/null | No | If LLM used |
| prompt_version | string/null | No | If LLM used |

---

## Valid Empty

```text
No Relevant Case
```

不创建虚假 CaseMatch。

业务流程继续。

---

# 24. Object — CandidateTopic

## Purpose

表示 Task G 生成、等待律师 Weekly Review 的 Evidence-backed Topic。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| candidate_topic_id | string | Yes | Unique ID |
| research_subject_id | string | Yes | Required core evidence |
| topic | string | Yes | Candidate topic/title |
| suggested_angle | string | Yes | Recommended content angle |
| recommendation_rationale | string | Yes | Why recommended |
| supporting_tracking_ids | array[string] | Yes | Optional evidence refs; [] allowed |
| supporting_long_tail_ids | array[string] | Yes | Optional evidence refs; [] allowed |
| supporting_case_match_ids | array[string] | Yes | Optional evidence refs; [] allowed |
| supporting_comment_ids | array[string] | Yes | Optional evidence refs; [] allowed |
| status | enum | Yes | pending_review / approved / rejected |
| model | string | Yes | Model |
| prompt_version | string | Yes | Prompt version |
| generated_at | datetime | Yes | Generation time |
| validation_status | enum | Yes | valid / invalid |

---

## Required Evidence

必须：

```text
research_subject_id
```

Optional Evidence：

```text
Tracking
Long-tail
CaseMatch
Comment
```

因此 Optional Evidence Array：

```text
[]
```

是合法状态。

---

# 25. Object — TopicFeedback

## Purpose

保存律师对 CandidateTopic 的 Optional 价值评分。

Topic Approval 本身由：

```text
LawyerDecision
```

保存。

TopicFeedback 只负责附加 Feedback。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| topic_feedback_id | string | Yes | Unique ID |
| candidate_topic_id | string | Yes | Topic |
| rating | integer | Yes | 1–5 |
| feedback_text | string/null | No | Optional future feedback |
| provided_by | string | Yes | User |
| provided_at | datetime | Yes | Time |

---

## Validation

```text
rating ∈ {1,2,3,4,5}
```

Rating：

```text
Optional
```

不存在 TopicFeedback：

不得阻塞 Topic Approval。

---

# 26. Object — KeywordHistory

## Purpose

保存 Keyword Lifecycle 的状态变化。

不能只保存：

```text
keyword.lifecycle_status
```

而丢失历史。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| keyword_history_id | string | Yes | Unique ID |
| keyword_id | string | Yes | Keyword |
| from_status | enum/null | No | Previous status |
| to_status | enum | Yes | New status |
| change_reason | string/null | No | Human/system rationale |
| recommendation_snapshot | object/null | No | Monthly evidence / recommendation |
| decision_id | string/null | No | Lawyer decision |
| changed_at | datetime | Yes | Change time |

---

# 27. Keyword Performance

Keyword Performance 是：

```text
Derived Analytics
```

不一定需要独立永久业务对象。

可以通过：

```text
Keyword
SearchHit
BasicAnalysis
LawyerDecision
DeepAnalysisRequest
CandidateTopic
```

聚合得到。

MVP 至少需要计算：

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

---

# 28. Object — WorkflowRun

## Purpose

提供系统 Observability。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| workflow_run_id | string | Yes | Unique ID |
| workflow_name | string | Yes | Logical workflow |
| trigger_type | enum | Yes | schedule / human / state / retry |
| started_at | datetime | Yes | Start |
| finished_at | datetime/null | No | Finish |
| status | enum | Yes | running / success / partial_success / failed |
| items_processed | integer | Yes | Processed count |
| success_count | integer | Yes | Success |
| failure_count | integer | Yes | Failure |
| error_summary | string/null | No | Summary |
| retry_of_run_id | string/null | No | Previous failed/partial run |
| metadata | object/null | No | Additional run metadata |

---

## Validation

Counts：

```text
integer >= 0
```

Completion should satisfy where applicable:

```text
success_count + failure_count
<=
items_processed
```

具体是否允许 Skipped Item：

Architecture 阶段决定是否新增：

```text
skipped_count
```

---

# 29. Object — DeliveryRecord

## Purpose

记录 Daily / Tracking / Weekly / Monthly Feishu Delivery。

Feishu Message 本身不是 Business Data。

DeliveryRecord 用于判断：

> Business Output 是否成功送达 Human Interaction Layer。

---

## Fields

| Field | Type | Required | Description |
|---|---|---:|---|
| delivery_id | string | Yes | Unique ID |
| delivery_type | enum | Yes | daily / tracking / weekly / monthly |
| workflow_run_id | string | Yes | Producing workflow |
| channel | enum | Yes | feishu |
| recipient_id | string | Yes | Logical recipient |
| external_message_id | string/null | No | Feishu message/card ID |
| status | enum | Yes | pending / sent / failed |
| sent_at | datetime/null | No | Delivery time |
| error_message | string/null | No | Failure |
| idempotency_key | string | Yes | Duplicate-delivery protection |

---

# 30. Feishu Interaction Contract

Feishu：

```text
Human Interaction Layer
```

Database：

```text
System of Record
```

Human Action Flow：

```text
Feishu Action
↓
Incoming Event
↓
Authentication / Validation
↓
Idempotency Check
↓
Create LawyerDecision
↓
Update Derived Business State
↓
Trigger Eligible Downstream Workflow
```

---

# 31. Feishu Event Minimum Contract

Incoming Human Event 至少需要解析：

```text
source_event_id
actor_id
target_type
target_id
action_type
action_value
occurred_at
```

如果：

```text
source_event_id
```

已成功处理：

```text
do not create duplicate business side effect
```

---

# 32. Current State vs Event History

Data Model 必须区分：

```text
Event History
```

和：

```text
Current State
```

例如：

### Event

```text
LawyerDecision:
Deep Analysis = No
```

之后：

```text
LawyerDecision:
Deep Analysis = Yes
```

### Current State

可以推导：

```text
deep_analysis_approved = true
```

但不得删除第一次 Decision。

同理：

```text
KeywordHistory
EngagementObservation
```

均遵守该原则。

---

# 33. Candidate State

Candidate 不一定需要成为独立 Object。

MVP 可以通过：

```text
BasicAnalysis
+
Candidate Gate
+
Review State
```

推导。

如果 Architecture 阶段发现：

```text
Daily Candidate Queue
```

需要复杂生命周期管理，再考虑新增：

```text
CandidateRecord
```

当前 Logical Contract 不提前增加冗余对象。

---

# 34. Priority Pool State

Priority Pool 也可以作为：

```text
Derived Business State
```

核心规则：

```text
Latest Effective Keep Decision = Yes
↓
Priority Pool
```

不要求第一版建立独立：

```text
PriorityPool table
```

Architecture 决定物理实现。

---

# 35. Cross-workflow Contract — Task A

## Input

```text
Keyword
Search Configuration
Platform
Time Window
```

## Output

```text
SearchHit
Post
EngagementObservation
BasicAnalysis
WorkflowRun
```

## Human-facing Output

```text
Daily Feishu Review
```

---

# 36. Cross-workflow Contract — Daily Human Review

## Input

```text
Post
BasicAnalysis
Current EngagementObservation
SearchHit Evidence
```

## Output

```text
LawyerDecision:
keep
track
deep_analysis
comment_analysis
```

Depending on decision:

```text
TrackingState
DeepAnalysisRequest
```

may become eligible.

---

# 37. Cross-workflow Contract — Task B

## Input

```text
TrackingState
Post
Initial EngagementObservation
```

## Output

```text
Follow-up EngagementObservation
Updated TrackingState
Tracking Evidence
```

Optional Human Output:

```text
New Deep Analysis LawyerDecision
```

---

# 38. Cross-workflow Contract — Task C

## Input

Required:

```text
DeepAnalysisRequest
Post
BasicAnalysis
Relevant Search Evidence
```

Optional:

```text
SelectedComment[]
Tracking Evidence
```

## Output

```text
ResearchSubject
```

---

# 39. Cross-workflow Contract — Task D

## Input

```text
ResearchSubject
```

especially:

```text
user_expressions
post_evidence
comment_evidence
```

## Output

```text
LongTailCandidate
```

---

# 40. Cross-workflow Contract — Task E

## Input

```text
Keyword
SearchHit
BasicAnalysis
LawyerDecision
DeepAnalysisRequest
CandidateTopic
LongTailCandidate
KeywordHistory
```

## Derived Evidence

```text
Keyword Performance
```

## Output

```text
System Recommendation
+
LawyerDecision
+
KeywordHistory
+
Optional New Trial Keyword
```

---

# 41. Cross-workflow Contract — Task F

## Input

```text
ResearchSubject
CaseRecord
```

## Output

```text
CaseMatch[]
```

Valid Output can be:

```text
[]
```

meaning:

```text
No Relevant Case
```

---

# 42. Cross-workflow Contract — Task G

## Input

Required:

```text
ResearchSubject
```

Optional:

```text
Tracking Evidence
LongTailCandidate
CaseMatch
SelectedComment
```

## Output

```text
CandidateTopic[]
```

Valid Output can be:

```text
[]
```

if no useful Candidate Topic is generated.

---

# 43. Weekly Review Contract

## Input

```text
ResearchSubject[]
CandidateTopic[]
LongTailCandidate[]
CaseMatch[]
Tracking Evidence[]
```

## Human Output

```text
LawyerDecision:
topic_approval
```

Optional:

```text
TopicFeedback
```

---

# 44. Monthly Review Contract

## Input

```text
Keyword Performance
LongTailCandidate
KeywordHistory
```

## Human Output

```text
LawyerDecision:
keyword_lifecycle
long_tail_promotion
```

## State Output

```text
KeywordHistory
Keyword.lifecycle_status
New Trial Keyword where approved
```

---

# 45. Valid Empty Rules

The following are valid:

```text
tags = []

legal_business_issues = []

user_expressions = []

content_opportunities = []

comment_findings = []

comment_evidence = []

supporting_tracking_ids = []

supporting_long_tail_ids = []

supporting_case_match_ids = []

supporting_comment_ids = []

CaseMatch[] = []

CandidateTopic[] = []
```

But:

> Valid Empty must only be used where the business meaning supports “none found”.

Required Scalar Field：

不得通过 Empty String 模拟 Valid Empty。

---

# 46. Error State Rules

至少区分：

```text
technical_error
data_validation_error
ai_validation_error
valid_empty
pending_human
```

这些状态不能混用。

例如：

```text
No Case Match
```

不是：

```text
case_matching_failed
```

---

# 47. AI Structured Output Contract

所有需要供 Downstream Workflow 消费的 AI Output：

```text
BasicAnalysis
ResearchSubject
LongTailCandidate normalization where AI-assisted
CaseMatch where AI-assisted
CandidateTopic
```

必须：

```text
Structured Output
↓
Schema Validation
↓
Valid
↓
Persist
```

如果：

```text
Invalid
```

则：

```text
Retry / Error Handling
```

不得把 malformed output 当正式业务对象。

---

# 48. AI Provenance Contract

核心 AI Object 原则上保存：

```text
model
prompt_version
generated_at
validation_status
```

目的：

```text
Evaluation
Prompt Comparison
Debugging
Reprocessing
```

---

# 49. Idempotency Contract

必须考虑 Idempotency 的主要场景：

```text
Scheduled Retry

TikHub Re-fetch

Feishu Duplicate Event

Deep Analysis Retry

Tracking Retry

Delivery Retry
```

Logical Idempotency Keys 至少需要覆盖：

### Post

```text
platform + platform_post_id
```

### SearchHit

```text
workflow_run_id + keyword_id + post_id
```

### Human Event

```text
source_event_id
```

### Delivery

```text
idempotency_key
```

### Deep Analysis

```text
approval_decision_id
```

具体 Database Constraint：

Architecture 阶段实现。

---

# 50. Data Retention Principle

MVP 核心研究数据默认：

```text
Preserve
```

尤其：

- SearchHit
- Post
- EngagementObservation
- LawyerDecision
- ResearchSubject
- LongTailCandidate
- CandidateTopic
- KeywordHistory

因为这些数据未来用于：

```text
Evaluation
Search Calibration
Prompt Improvement
Workflow Analysis
Portfolio Metrics
```

具体 Retention Period：

MVP 暂不设置自动删除策略。

---

# 51. Source Traceability

至少支持：

```text
CandidateTopic
↓
ResearchSubject
↓
Post
↓
source_url
```

如果 Topic 使用：

```text
CaseMatch
```

则支持：

```text
CandidateTopic
↓
CaseMatch
↓
CaseRecord
↓
source_reference where available
```

如果使用：

```text
Comment Evidence
```

则支持：

```text
ResearchSubject
↓
SelectedComment
↓
Source Post
```

---

# 52. Data Quality Rules

## String

Required String：

```text
trim
↓
must not be empty
```

---

## Integer

Count Fields：

```text
integer
>= 0
```

---

## Datetime

必须 Normalize 为：

```text
Timezone-aware ISO 8601
```

---

## Array

不存在数据时：

```text
[]
```

如果字段语义为集合。

不要：

```text
null
```

与：

```text
[]
```

混用。

---

## Enum

未知值：

不得直接写入正式 Enum。

应：

```text
Map
or
Validation Error
```

---

# 53. Data Contract and Physical Schema Boundary

当前：

```text
Logical Data Model
```

未来可能映射：

```text
PostgreSQL Tables
JSONB
Object Storage
Vector Index
Feishu Records
```

但：

> 一个 Logical Object 不一定等于一张 Database Table。

例如：

```text
Keyword Performance
Priority Pool
Candidate State
```

都可能通过 Query / View / Derived State 实现。

---

# 54. Case Library Migration Boundary

现有 Case Excel 是真实业务资产。

Architecture 阶段必须执行：

```text
Inspect Existing Excel
↓
Document Current Schema
↓
Identify Stable Case ID
↓
Map Fields
↓
Choose Online Storage
↓
Design Sync Strategy
```

需要解决：

```text
Local Excel continues updating?
or
Cloud becomes primary?
or
One-way sync?
or
Two-way sync?
```

在没有检查实际 Excel 前：

不得假设最终 CaseRecord Physical Schema。

---

# 55. Feishu Boundary

Feishu 可以保存：

```text
Display State
Interaction State
Message Metadata
```

但以下核心数据不能只存在 Feishu：

```text
LawyerDecision
Tracking Evidence
ResearchSubject
CandidateTopic
KeywordHistory
```

必须进入 Backend Persistent Storage。

---

# 56. Evaluation Data Readiness

当前 Data Contract 应能够支持未来计算：

```text
Lawyer Keep Rate

Candidate Rate

Deep Analysis Rate

Tracking Re-evaluation Rate

Topic Approval Rate

Approved Topics per Week

Keyword → Approved Topic Conversion

Long-tail Trial Performance

Workflow Success Rate

AI Structured Output Failure Rate
```

以及：

```text
Prompt Version
↓
Human Feedback
```

之间的比较。

---

# 57. Manual Research Time

Manual Research Time 属于：

```text
Business Metric
```

当前不强制建立复杂 Tracking Object。

MVP Baseline 阶段可以通过：

```text
Manual Recording
```

获得：

```text
Before MVP
After MVP
```

数据。

如果未来需要自动化，再扩展 UserActivity / ReviewSession Object。

---

# 58. MVP Object Status Summary

```text
Keyword                  Defined
SearchHit                Defined
Post                     Defined
BasicAnalysis            Defined
EngagementObservation    Defined
LawyerDecision           Defined
TrackingState            Defined
DeepAnalysisRequest      Defined
SelectedComment          Defined
ResearchSubject          Defined
LongTailCandidate        Defined
CaseRecord               Logical Minimum Defined
CaseMatch                Defined
CandidateTopic           Defined
TopicFeedback            Defined
KeywordHistory           Defined
WorkflowRun              Defined
DeliveryRecord           Defined
```

---

# 59. Cross-workflow Contract Status

```text
Task A Input / Output             Defined

Daily Human Review Contract      Defined

Task B Input / Output             Defined

Task C Input / Output             Defined

Task D Input / Output             Defined

Task E Input / Output             Defined

Task F Input / Output             Defined

Task G Input / Output             Defined

Weekly Review Contract           Defined

Monthly Review Contract          Defined

Feishu Event Contract            Defined

AI Output Contract               Defined

Idempotency Contract             Defined

Traceability Contract            Defined
```

---

# 60. Open Architecture Questions

以下问题不属于 Data Contract 未完成，而是有意留给下一阶段：

```text
Which database?

n8n Cloud or self-hosted?

Which cloud provider?

Which LLM?

How should Feishu interactive cards be implemented?

How should webhook security work?

How should retries be implemented?

How should the existing Excel case library be synchronized?

Does case retrieval need full-text search?

Does it need embeddings?

Does it need hybrid retrieval?

Does it actually need RAG?

Which workflow logic belongs in n8n?

Which logic belongs in Python?

How should prompt versions be managed?

How should raw TikHub payloads be retained?
```

这些将在：

```text
System Architecture
+
Technology Mapping
```

阶段回答。

---

# 61. Final Data Principles

The system should preserve:

```text
Source
Evidence
Decision
History
Provenance
```

而不是只保存最终结果。

核心区别：

```text
Post
≠
SearchHit

Decision
≠
Current State

Observation
≠
Tracking State

ResearchSubject
≠
CandidateTopic

LongTailCandidate
≠
Keyword

CaseRecord
≠
CaseMatch

Feishu Message
≠
Business Data

Valid Empty
≠
Error

Pending
≠
Reject
```

最终数据流：

```text
Raw Source
↓
Normalize
↓
Validate
↓
Persist
↓
Analyze
↓
Human Decision
↓
Preserve History
↓
Generate Research Evidence
↓
Generate Candidate Output
↓
Human Feedback
↓
Use Real Outcomes to Improve Future Search
```

---

# 62. Data Contract Status

```text
Workflow Analysis
✓

Cross-workflow Input Review
✓

Logical Object Review
✓

Decision History Review
✓

Tracking Data Review
✓

ResearchSubject Review
✓

Long-tail Lifecycle Review
✓

Case Integration Boundary
✓

Topic Feedback Review
✓

AI Provenance Review
✓

Idempotency Review
✓

Error / Empty / Pending Review
✓

Evaluation Readiness Review
✓

PRD Cross-check
✓
```

**Status: Ready for System Architecture Design**