# Legal Content Automation - Workflow Analysis

## 0. Business Problem

### Current Workflow (As-Is)

Step 1: 律师根据自身业务方向确定案件类目。

Step 2: 将案件类目进一步拆分为不同分组。

Step 3: 针对每个分组，使用 AI 扩展和生成相关10个法律关键词。

Step 4: 律师使用关键词在社交媒体平台进行搜索，目前主要为小红书。

Step 5: 浏览搜索结果，根据帖子互动量进行初步筛选。
当前筛选标准：
互动量 = 点赞量 + 收藏量 + 评论数
互动量 > 500 的帖子进入重点关注范围。

Step 6: 对筛选出的帖子进行内容分析和记录，重点关注：
- 帖子文案内容
- 帖子讨论的核心话题
- 评论区主要讨论的话题
- 当前互动数据

Step 7: 对值得关注的帖子进行持续追踪，在约 7 天后再次观察互动数据变化，用于判断内容及相关话题是否仍在获得流量。

Step 8: 将社交媒体热门话题与律师自身案例库进行匹配，寻找同类型或相关案例，最终由律师决定是否将其作为脚本选题。

### Pain Points
#### Pain Point 1 — Keyword Quality & Validation

**发生步骤：** Step 3

**具体问题：**
AI 根据法律案件分类生成的关键词，不一定符合社交媒体用户的真实表达习惯。
目前缺少基于平台真实数据验证关键词有效性的机制，无法判断生成的关键词是否存在足够的实际讨论和内容。

**造成后果：**
- 搜索结果与目标法律话题相关度不足
- 可能遗漏用户真实使用的高频表达
- 无效关键词增加后续采集和分析成本
- 上游关键词质量问题会进一步影响后续热点识别准确度


#### Pain Point 2 — Manual Collection & Poor Scalability

**发生步骤：** Step 4–5

**具体问题：**
目前需要人工逐个关键词在社交媒体平台搜索并筛选帖子。
随着关键词数量、搜索频率和社交平台数量增加，相同操作需要不断重复。

**造成后果：**
- 数据采集耗时高
- 难以扩大关键词覆盖范围
- 难以扩展到多个社交媒体平台
- 数据采集频率受到人工时间限制
- 可能遗漏潜在热门内容

#### Pain Point 3 — Manual Analysis & Inconsistent Standards

**发生步骤：** Step 6

**具体问题：**
筛选后的帖子需要人工阅读、整理文案、识别核心话题并分析评论讨论内容。
目前缺少统一、结构化的分析标准，律师本人在不同时间的判断可能存在波动，不同人员之间也可能产生判断差异。

**造成后果：**
- 内容分析耗时高
- 不同帖子之间难以保持统一分析标准
- 助理参与后可能进一步增加判断差异
- 数据质量不稳定
- 后续热点分析容易受到前期数据质量影响

#### Pain Point 4 — Manual Tracking & Missing Historical Trend Data

**发生步骤：** Step 7

**具体问题：**
需要人工保存并重新输入帖子 ID，定期查询互动数据并手动记录变化。
当需要追踪的帖子数量增加时，人工持续追踪非常困难，同时缺乏连续、结构化的历史互动数据。

**造成后果：**
- 重复操作耗时
- 容易漏掉需要追踪的帖子
- 历史数据记录不完整
- 难以准确计算互动增长速度
- 难以判断话题热度处于增长、稳定还是下降阶段

#### Pain Point 5 — Inefficient Case Matching

**发生步骤：** Step 8

**具体问题：**
律师案例库数量不断增加，目前主要依靠人工记忆和关键词查找相关案例。
社交媒体热门话题与案例库中的案件描述可能使用不同表达，单纯依赖关键词搜索容易遗漏语义相关案例。

**造成后果：**
- 人工查找案例耗时
- 案例库越大，查找效率越低
- 可能遗漏高度相关但表达方式不同的案例
- 热点与律师真实办案经验之间无法高效建立关联

#### Pain Point 6 — Static Keyword Library & Lack of Feedback Loop

**发生步骤：** Step 3–7

**具体问题：**
当前关键词主要由案件类目和 AI 扩展产生，关键词库建立后缺少基于真实社交媒体数据持续校准和更新的机制。

在帖子采集和分析过程中产生的大量真实用户表达、长尾词和新兴话题，目前无法有效反哺关键词库。

**造成后果：**
- 关键词库可能随着时间逐渐失效或过时
- 难以及时发现用户正在使用的新表达和长尾词
- 无法利用真实平台数据持续提高搜索关键词质量
- 搜索覆盖范围和热点发现能力可能随时间下降
- 无法将高价值长尾词进一步用于内容标签和发布表达

### Additional Requirement — Keyword Feedback Loop

The keyword system should not be static.

Social media data collected by the workflow should continuously feed back into the keyword system.

The system should support two additional capabilities:

#### 1. Long-tail Keyword Discovery

Analyze real social media content, including post titles, post content, comments and tags, to identify expressions and long-tail keywords actually used by users.

Potential uses:

- Recommend relevant tags for legal content publishing
- Improve title/topic wording
- Discover new search keywords
- Identify emerging user language and discussion patterns

#### 2. Keyword Calibration

Evaluate existing search keywords based on real platform performance.

Possible signals include:

- Number of relevant posts
- Number of high-engagement posts
- Average engagement
- Business relevance
- Recent growth trend
- Long-tail keyword occurrence

Keyword lifecycle:

Candidate → Testing → Active → Observe → Retired

The goal is to create a continuously updated keyword library based on real social media data rather than relying only on AI-generated keywords.

### Automation Goal

#### A. Fully Automated

系统应尽可能自动完成规则明确、重复性高、适合标准化执行的工作，包括：

- 根据关键词自动搜索和采集社交媒体帖子数据
- 根据统一规则计算帖子互动量并进行初步筛选
- 对筛选后的帖子进行结构化整理
- 分析帖子正文及评论内容，提取核心讨论信息
- 定期重新获取重点帖子的互动数据
- 保存历史互动数据并计算增长变化
- 根据真实社媒数据持续记录关键词表现
- 从真实社媒内容中发现潜在长尾词

对于 AI 分析结果异常、置信度较低或无法完成的情况，应进入人工复核流程。

#### B. AI-assisted

对于需要语义理解、相关性判断或推荐的工作，由 AI 完成第一轮分析，并保留律师审核和调整能力，包括：

- 根据案件类目和分组生成初始搜索关键词
- 根据真实平台数据辅助判断和校准关键词有效性
- 推荐新增、保留、观察或淘汰的关键词
- 从真实用户表达中推荐适合内容发布的长尾关键词和标签
- 辅助识别社交媒体热点话题与律师案例库之间的相关性
- 推荐可能相关的真实案例
- 结合热点、用户讨论和案例信息生成候选脚本选题及推荐理由

#### C. Human-controlled

以下关键业务决策由律师本人控制：

- 确定主要业务领域、案件类目和内容方向
- 审核关键词库的重要调整
- 判断 AI 推荐案例是否真正适合用于内容创作
- 对候选选题进行专业判断
- 决定最终采用哪些脚本选题
- 对最终对外发布的法律观点和内容负责

#### Automation Boundary

The goal of this system is not to replace the lawyer's professional judgment.

The system should automate repetitive data collection, organization, tracking and first-level analysis, while using AI to assist with semantic analysis, matching and recommendation.

Final professional and content decisions remain human-controlled.

Expected workflow:

Business Direction
↓
Keyword Generation & Validation
↓
Automated Social Media Collection
↓
Post Filtering & Analysis
↓
Topic & Trend Discovery
↓
Keyword Feedback Loop
↓
Case Library Matching
↓
Candidate Topic Recommendation
↓
Lawyer Review & Final Selection
### Success Metrics

> Success Metrics are used to evaluate whether the automation actually improves the business process rather than simply whether the workflow runs successfully.

#### 1. Time Saved

**Measure:**
律师每周用于社媒搜索、帖子筛选、内容整理、数据追踪、案例匹配和选题准备的人工时间。

**Baseline:**
TBD — 在自动化系统正式运行前记录当前人工流程耗时。

**Target:**
显著减少重复性人工操作时间，使律师主要将时间投入最终选题判断和内容创作。

---

#### 2. Manual Work Reduction

**Measure:**
原人工 Workflow 中需要律师或助理手动完成的重复操作数量及占比。

重点观察：

- 手工搜索关键词
- 手工筛选帖子
- 手工记录帖子数据
- 手工整理文案和评论
- 手工重新查询帖子互动数据
- 手工计算互动变化
- 手工查找相关案例

**Baseline:**
TBD

**Target:**
重复性、规则明确的工作尽可能自动化，人工主要保留审核、专业判断和最终选题。

---

#### 3. Content Coverage

**Measure:**

- 每周期覆盖的关键词数量
- 每周期采集的相关帖子数量
- 可持续追踪的帖子数量
- 覆盖的社交媒体平台数量
- 数据采集频率

**Baseline:**
当前主要依赖人工搜索，主要覆盖小红书。

**Target:**
在不显著增加人工工作量的情况下，提高关键词、帖子和平台的数据覆盖能力。

---

#### 4. Keyword Effectiveness

**Measure:**

- 每个关键词获得的相关帖子数量
- 高互动帖子数量
- 关键词对应内容的业务相关度
- 关键词近期表现变化
- 新增长尾关键词数量
- 无效或过时关键词识别数量

**Goal:**
建立基于真实社交媒体数据的关键词评估机制，而不是仅依赖 AI 生成关键词。

关键词库应能够持续完成：

Candidate
↓
Testing
↓
Active
↓
Observe
↓
Retired

并通过真实数据不断校准。

---

#### 5. Analysis Consistency

**Measure:**
系统对帖子内容、核心话题、评论讨论点等信息进行结构化分析时的一致性和准确性。

**Evaluation Method:**
定期由律师人工抽样检查 AI 分析结果，并记录：

- Topic Classification Accuracy
- Business Relevance Accuracy
- Key Discussion Point Accuracy
- Invalid / Low-quality Analysis Rate

**Baseline:**
当前依赖人工判断，不同时间或不同人员之间可能存在判断差异。

**Target:**
建立统一的第一轮分析标准，提高数据整理和内容判断的一致性。

---

#### 6. Trend Detection Quality

**Measure:**

- 是否能够持续保存重点帖子的历史互动数据
- 是否能够准确计算互动增长
- 是否能够识别 Growing / Stable / Declining 等趋势
- 是否能够发现值得持续关注的话题

**Baseline:**
当前依赖人工在约 7 天后重新查询和记录数据。

**Target:**
形成连续、可追踪的历史数据，为热点趋势判断提供数据依据。

---

#### 7. Case Matching Quality

**Measure:**

AI 推荐的相关案例中，经律师确认确实与热点话题具有业务或内容关联的比例。

Example:

AI Recommended Cases
↓
Lawyer Review
↓
Relevant / Not Relevant

**Baseline:**
当前主要依赖律师人工记忆和搜索案例库。

**Target:**
减少人工查找案例的时间，同时提高对潜在相关案例的发现能力。

---

#### 8. Topic Recommendation Quality

**Measure:**

系统生成的候选选题中，最终被律师认可或采用的比例。

Example:

20 Candidate Topics Generated
↓
8 Accepted by Lawyer

Recommendation Adoption Rate = 8 / 20 = 40%

**Baseline:**
TBD

**Target:**
候选选题不仅具有社交媒体热度，还应同时满足：

- 与律师业务相关
- 有真实用户讨论基础
- 有数据支持
- 可以与真实案例或专业经验结合
- 具有内容创作价值

---

### MVP Success Criteria

第一版系统（MVP）优先验证：

1. 是否能够明显减少人工搜索、整理和追踪时间
2. 是否能够稳定采集并保存有效社媒数据
3. 是否能够形成统一的帖子和话题分析结果
4. 是否能够持续追踪互动数据并识别增长趋势
5. 是否能够根据真实数据改善关键词库
6. 是否能够辅助律师找到相关案例
7. 是否能够输出具有实际使用价值的候选选题

具体数值目标将在系统获得真实运行数据后，根据 Baseline 进一步确定。

---

### Future Metrics

以下指标暂不作为第一版 MVP 的核心 Success Metrics：

Content Recommendation
↓
Lawyer Adoption
↓
Content Published
↓
Actual Views / Likes / Comments / Saves
↓
Feedback to Topic Recommendation System

未来可以进一步研究：

- 推荐选题实际发布后的内容表现
- 高表现内容与原始 Topic Heat Score 的相关性
- 哪些类型的选题更容易被律师采用
- 发布结果是否可以反向优化选题评分机制

该 Feedback Loop 暂列为 Future Improvement，避免扩大第一版 MVP Scope。
## 1. Trigger

The Legal Content Automation System contains multiple workflows with different trigger mechanisms.

The MVP primarily uses scheduled batch processing combined with human approval and workflow dependencies.

Trigger analysis should distinguish between:

**Trigger → Upstream Dependency → Precondition → Execution Rule → Execution**

---

### Trigger A — Social Media Content Collection

**Workflow:**

Search Keywords → Collect New Social Media Posts

**Trigger Type:**

Schedule Trigger

**Trigger Condition:**

Monday to Saturday at 10:00.

**Upstream Dependency:**

Official Seed Keyword Library.

**Precondition:**

At least one valid Active seed keyword must be available for the current collection cycle.

If no valid seed keyword is available, the collection workflow should be skipped and the reason recorded.

**Execution Rules:**

- Rotate official seed keywords based on predefined legal topics.
- Process a maximum of 4 official seed keywords per collection cycle.
- Only use keywords currently eligible for collection.
- Collect new social media posts associated with the selected keywords.
- Avoid duplicate collection of previously stored posts where possible.

**Execution Mode:**

Scheduled Batch Processing.

**Purpose:**

Continuously collect real social media content related to the lawyer's business areas and build the data foundation for subsequent analysis.

**Important Distinction:**

```text
Monday–Saturday 10:00
→ Trigger

Official Seed Keyword Library
→ Upstream Dependency

At least one valid keyword exists
→ Precondition

Maximum 4 seed keywords per run
→ Execution Rule
```

---

### Trigger B — Priority Post Tracking

**Workflow:**

Re-fetch engagement data for priority posts.

**Trigger Type:**

Schedule Trigger

**Trigger Condition:**

Every Sunday at 10:00.

**Upstream Dependency:**

Priority Post Pool created from previously collected social media posts.

**Precondition:**

The Priority Post Pool must contain posts requiring follow-up tracking.

If no eligible posts exist, the scheduled tracking workflow should be skipped and the reason recorded.

**Eligibility Rule:**

Posts with initial engagement greater than 500 enter the Priority Post Pool.

Current engagement calculation:

```text
Engagement = Likes + Saves + Comments
```

Current threshold:

```text
Engagement > 500
→ Priority Post
```

**Execution Rules:**

- Re-fetch the latest engagement data for eligible priority posts.
- Store the new engagement data without overwriting historical observations.
- Preserve the Post ID so different observation periods can be compared.
- Avoid duplicate tracking records for the same observation period.

**Execution Mode:**

Weekly Batch Processing.

**Purpose:**

Create historical engagement data that can later be used to evaluate post and topic growth trends.

**Important Distinction:**

`Engagement > 500` is not the Trigger.

It is an eligibility / decision rule that determines whether a post enters the Priority Post Pool.

```text
Post Collection
↓
Calculate Engagement
↓
Engagement > 500?
↓
YES
↓
Priority Post Pool
↓
Wait
↓
Sunday 10:00
↓
Priority Post Tracking
```

---

### Trigger C — AI Content & Comment Analysis

**Workflow:**

Perform deeper AI analysis on selected posts and their discussion content.

**Trigger Type:**

Manual Trigger / Human Approval.

**Trigger Condition:**

Candidate posts are presented to the lawyer.

The lawyer confirms that a post is worth further analysis.

**Upstream Dependencies:**

- Social Media Content Collection
- Candidate Post Data
- Initial engagement screening results

**Precondition:**

The candidate post must:

- contain sufficient valid content for analysis;
- have been reviewed and approved by the lawyer;
- not already have a valid completed analysis for the same analysis version.

**Execution Rules:**

After lawyer approval, the system analyzes relevant information such as:

- Post Content
- Core Topic
- User Problem
- Legal Issue
- Key Discussion Points
- Comment Discussion
- User Expressions

The exact structured fields will be defined later during Input and Process Analysis.

**Execution Mode:**

Human-in-the-loop / Event-driven Analysis.

**Purpose:**

Use lawyer approval as a quality gate before spending additional AI processing resources on deeper content analysis.

**Workflow:**

```text
Candidate Post
↓
Lawyer Review
↓
Approved?
├── No → Stop / Ignore
└── Yes
      ↓
AI Content & Comment Analysis
      ↓
Analyzed Post & Comment Library
```

---

### Trigger D — Long-tail Keyword Discovery

**Workflow:**

Discover long-tail expressions from previously analyzed social media content.

**Trigger Type:**

Schedule Trigger.

**Trigger Condition:**

Every Sunday at 10:30.

**Upstream Dependency:**

Task C — AI Content & Comment Analysis.

The workflow depends on the Analyzed Post & Comment Library produced from previously approved and analyzed posts.

**Precondition:**

The Analyzed Post & Comment Library must contain valid analyzed content from the current analysis period.

If no valid analyzed content exists, the scheduled workflow should be skipped and the reason recorded.

**Execution Rules:**

Analyze real user language appearing in:

- Post titles
- Post content
- Comments
- Existing tags
- Repeated user expressions
- Emerging topic expressions

Potential long-tail keywords should be recorded as candidates rather than automatically becoming official seed keywords.

**Execution Mode:**

Weekly Batch Processing.

**Purpose:**

- Discover real user expressions
- Identify potential long-tail keywords
- Recommend expressions suitable for social media tags
- Discover candidate search keywords
- Provide data for future keyword calibration

**Dependency Flow:**

```text
Lawyer Approved Posts
↓
AI Content & Comment Analysis
↓
Analyzed Post & Comment Library
↓
Accumulate During the Week
↓
Sunday 10:30
↓
Long-tail Keyword Discovery
↓
Long-tail Keyword Candidates
```

---

### Trigger E — Seed Keyword Calibration

**Workflow:**

Evaluate and calibrate official seed keyword performance.

**Trigger Type:**

Schedule Trigger.

**Trigger Condition:**

10:00 on the last day of each month.

**Upstream Dependencies:**

- Official Seed Keyword Library
- Historical keyword performance data
- Collected social media post data
- Analyzed post and comment data
- Long-tail keyword discovery results

**Precondition:**

Sufficient valid historical data must exist to evaluate keyword performance.

If insufficient data exists for a keyword, the system should avoid making a strong retirement decision.

The keyword may remain in:

- Candidate
- Testing
- Active
- Observe

until sufficient evidence becomes available.

**Execution Rules:**

Evaluate keyword performance using real social media data.

The exact scoring criteria and thresholds will be defined later during Decision Analysis.

Possible keyword lifecycle:

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

The system should recommend keyword status changes.

Important keyword changes should remain subject to lawyer review during the MVP stage.

**Execution Mode:**

Monthly Batch Processing.

**Purpose:**

Prevent the keyword library from becoming static or outdated.

Use real social media performance to continuously improve the quality of search keywords.

**Keyword Feedback Flow:**

```text
Seed Keyword Library
↓
Social Media Collection
↓
Post Performance Data
↓
Content & Comment Analysis
↓
Long-tail Keyword Discovery
↓
Historical Keyword Performance
↓
Last Day of Month 10:00
↓
Keyword Calibration
↓
Keyword Update Recommendation
↓
Lawyer Review
↓
Updated Keyword Library
↓
Next Collection Cycle
```

**Design Principle:**

Keyword calibration should be based on real social media performance rather than relying only on AI-generated keywords.

---

### Trigger F — Case Library Matching

**Workflow:**

Match lawyer-approved topics with potentially relevant cases from the lawyer's case library.

**Trigger Type:**

Schedule Trigger.

**Trigger Condition:**

Every Sunday at 10:30.

**Upstream Dependencies:**

- AI Content & Comment Analysis
- Topic Analysis Results
- Lawyer Approval
- Approved Topic Pool
- Lawyer Case Library

**Precondition:**

The Approved Topic Pool must contain at least one topic approved by the lawyer during the current analysis period.

The Case Library must also be available for retrieval.

If no approved topics exist, Case Library Matching should be skipped.

**Execution Rules:**

Only topics explicitly approved by the lawyer should enter weekly Case Library Matching.

Lawyer approval does not immediately start Case Library Matching.

Instead, approval changes the Topic's data state.

```text
Topic
↓
Lawyer Review
↓
Approved
↓
Topic Status = Approved
↓
Approved Topic Pool
↓
Wait for Weekly Batch
↓
Sunday 10:30
↓
Case Library Matching
```

Therefore:

```text
Lawyer Approval
→ Human Decision / Data State Change

Sunday 10:30
→ Schedule Trigger

Approved Topic Pool is not empty
→ Precondition
```

**Execution Mode:**

Weekly Batch Processing.

**Purpose:**

Identify potentially relevant cases for lawyer-approved social media topics so that content recommendations can combine:

- Real social media discussion
- Trending topics
- User problems
- Legal issues
- Lawyer's real case experience

**Important Note:**

The detailed Case Library Matching method is intentionally not defined at the Trigger stage.

Possible approaches such as:

- Keyword Search
- Metadata Filtering
- Semantic Search
- Embeddings
- RAG

will be evaluated later during Process, Decision and Technology Mapping.

---

### Trigger G — Candidate Script Topic Generation

**Workflow:**

Generate candidate script topics by combining approved social media topics with relevant case information.

**Trigger Type:**

Event Trigger / Workflow Completion Trigger.

**Trigger Condition:**

The weekly Case Library Matching workflow has successfully completed.

**Upstream Dependencies:**

- Approved Topic Pool
- Topic Analysis Results
- Topic Trend Data
- Case Library Matching Results

**Precondition:**

At least one valid approved topic must exist.

Required upstream analysis must be available before candidate topic generation begins.

Case matching results should either:

- contain relevant case candidates; or
- explicitly indicate that no relevant case was found.

Whether a topic without a matching case can still become a candidate script topic will be defined later during Decision Analysis.

**Execution Rules:**

Generate candidate script topics using available information such as:

- Approved Topic
- Social Media Discussion
- User Problem
- Legal Issue
- Trend / Engagement Information
- Relevant Case Candidates
- Lawyer Business Direction

The system generates recommendations rather than making the final content decision.

**Execution Mode:**

Weekly Batch Processing / Workflow Dependency.

**Dependency Flow:**

```text
Approved Topic Pool
↓
Sunday 10:30
↓
Case Library Matching
↓
Case Matching Completed
↓
Candidate Script Topic Generation
↓
Candidate Topic List
↓
Lawyer Final Review
↓
Final Selected Topics
```

**Human-in-the-loop:**

The system generates candidate script topics and supporting information.

The lawyer retains final control over:

- Case relevance
- Professional judgment
- Content direction
- Final topic selection

---

### Trigger Summary

| Workflow | Trigger Type | Trigger | Upstream Dependency | Execution Mode |
|---|---|---|---|---|
| A. Social Media Content Collection | Schedule | Monday–Saturday 10:00 | Seed Keyword Library | Scheduled Batch |
| B. Priority Post Tracking | Schedule | Sunday 10:00 | Priority Post Pool | Weekly Batch |
| C. AI Content & Comment Analysis | Manual / Human Approval | Lawyer approves candidate post | Candidate Post Pool | Human-in-the-loop |
| D. Long-tail Keyword Discovery | Schedule | Sunday 10:30 | Analyzed Post & Comment Library | Weekly Batch |
| E. Seed Keyword Calibration | Schedule | Last day of month 10:00 | Historical Keyword & Content Data | Monthly Batch |
| F. Case Library Matching | Schedule | Sunday 10:30 | Approved Topic Pool + Case Library | Weekly Batch |
| G. Candidate Script Topic Generation | Workflow Completion | Case Matching completed | Topic + Case Matching Results | Weekly Batch |

---

### Trigger Dependency Overview

```text
Official Seed Keyword Library
        ↓
[Schedule: Mon–Sat 10:00]
        ↓
A. Social Media Content Collection
        ↓
Engagement Screening
        ↓
Candidate Posts
        ├─────────────────────────────┐
        ↓                             │
Lawyer Review                        │
        ↓                             │
Approved Posts                       │
        ↓                             │
C. AI Content & Comment Analysis     │
        ↓                             │
Analyzed Post & Comment Library      │
        │                             │
        │                    Engagement > 500
        │                             ↓
        │                    Priority Post Pool
        │                             ↓
        │                    [Sunday 10:00]
        │                             ↓
        │                    B. Post Tracking
        │
        ├─────────────────────────────┐
        ↓                             ↓
[Sunday 10:30]                Topic Analysis
        ↓                             ↓
D. Long-tail Discovery        Lawyer Approval
        ↓                             ↓
Long-tail Candidates          Approved Topic Pool
        │                             ↓
        │                     [Sunday 10:30]
        │                             ↓
        │                     F. Case Matching
        │                             ↓
        │                     Matching Completed
        │                             ↓
        │                     G. Candidate Topics
        │                             ↓
        │                     Lawyer Final Review
        │
        ↓
Historical Keyword Data
        ↓
[Last Day of Month 10:00]
        ↓
E. Keyword Calibration
        ↓
Keyword Update Recommendation
        ↓
Lawyer Review
        ↓
Updated Seed Keyword Library
        ↓
Next Collection Cycle
```

---

### Trigger Design Principles Learned

This project distinguishes five different concepts:

#### 1. Trigger

What actually starts the workflow?

Example:

```text
Sunday 10:00
```

#### 2. Upstream Dependency

What previous workflow or data does the current workflow depend on?

Example:

```text
Analyzed Post & Comment Library
```

#### 3. Precondition

What must already be true before the workflow can proceed?

Example:

```text
Approved Topic Pool is not empty
```

#### 4. Execution Rule

What business rules control how the workflow runs?

Example:

```text
Maximum 4 seed keywords per collection cycle
```

#### 5. Decision

What condition determines the next action while the workflow is running?

Example:

```text
Engagement > 500?
↓
YES → Priority Post Pool
NO → Normal Post
```

---

### Key Learning

A workflow may depend on another workflow without being directly triggered by that workflow.

Example:

```text
Task C
↓
Produces analyzed data
↓
Analyzed Post Library
↓
Wait
↓
Sunday 10:30
↓
Task D
```

Task D depends on Task C, but its actual Trigger remains the Sunday 10:30 Schedule Trigger.

Therefore:

> **Dependency determines what the workflow needs.  
> Trigger determines when the workflow starts.**

This distinction is important when designing batch-processing automation systems.
## 2. Input

This section defines the business data and configuration required by the Legal Content Automation workflows.

The purpose of this section is to define:

- what data each workflow needs;
- where the data comes from;
- which fields are required;
- how raw platform data should be normalized and validated;
- how incomplete or invalid data should be handled;
- which historical observations and relationships should be preserved.

Detailed technical implementation will be defined later during Technology Mapping.

---

### 2.1 Input Architecture

The current system contains several major input sources:

```text
Official Seed Keyword Library
        +
Platform Configuration
        +
Search Configuration
        ↓
Social Media Content Collection
        ↓
Candidate Post Data
        ↓
Lawyer Review
        ↓
Approved Post Data
        ↓
Content & Comment Enrichment
        ↓
AI Analysis
```

Historical data is also required for later workflows:

```text
Search Hit History
→ Keyword Performance / Calibration

Engagement History
→ Post Trend Detection

Analyzed Post & Comment Library
→ Long-tail Keyword Discovery

Approved Topic Pool
→ Case Library Matching

Case Library
→ Candidate Topic Generation
```

---

## 2.2 Task A — Social Media Content Collection Inputs

Task A collects social media posts based on official seed keywords.

### Input 1 — Official Seed Keyword

**Source:**

Official Seed Keyword Library.

**Required:**

Yes.

**Current Requirement:**

The keyword must:

- exist in the Keyword Library;
- not be empty;
- not have `Retired` status;
- currently be eligible for search.

Example:

```text
Keyword:
调岗降薪

Status:
Active
```

Workflow:

```text
Seed Keyword Library
↓
Read Keyword
↓
Check Status
↓
Eligible?
├── Yes → Continue Collection
└── No  → Skip Keyword
```

---

### Input 2 — Target Platform

**Source:**

Platform Configuration.

**Required:**

Yes.

**Current MVP Platform:**

```text
Xiaohongshu
```

Future versions may support additional platforms.

The platform must:

- exist in the supported platform configuration;
- currently be Active;
- have a usable data acquisition channel.

Possible acquisition methods may include:

```text
Official API
Third-party API
Web Collection / Scraping
Other Connector
```

The exact acquisition technology is intentionally not defined at the Input stage.

The business requirement is:

> The system must be able to acquire the required data from the selected platform.

---

### Input 3 — Post Time Range

**Source:**

Search Configuration.

**Required:**

Yes.

**Current MVP Value:**

```text
Last 7 Days
```

The collection workflow should ultimately retain posts published within the configured time range.

If the selected acquisition method cannot directly filter by publication time:

```text
Collect Search Results
↓
Read Published At
↓
Normalize Datetime
↓
Secondary Time Filtering
```

The business requirement applies to the final eligible dataset rather than requiring the external platform or API to support native time filtering.

---

### Input 4 — Collection Limit

**Source:**

Search Configuration.

**Required:**

Yes.

**Current MVP Value:**

```text
Maximum 5 Candidate Posts
per Seed Keyword
per Collection Run
```

Rules:

- The value must be a positive integer.
- Fewer than 5 results are acceptable if insufficient eligible posts exist.
- Duplicate posts do not count as additional unique Candidate Posts.

---

### Input 5 — Candidate Selection Strategy

**Source:**

Search Configuration / Business Rules.

**Required:**

Yes.

Current priority:

```text
High Relevance
+
High Engagement
```

Among posts within the configured time range, the system should prioritize posts that:

1. are relevant to the Seed Keyword / target legal topic; and
2. demonstrate stronger engagement.

The system retains a maximum of 5 Candidate Posts for each Seed Keyword during each collection cycle.

The exact relevance calculation and ranking logic will be defined later during Process and Decision Analysis.

---

## 2.3 Candidate Post Data

Task A should collect enough information to support:

- initial screening;
- lawyer review;
- engagement calculation;
- future tracking;
- later AI analysis.

Current Candidate Post structure:

```text
Candidate Post
│
├── Identity
│   ├── Post ID
│   ├── Post URL
│   └── Platform
│
├── Content
│   ├── Title
│   ├── Post Content
│   ├── Author
│   └── Tags / Hashtags
│
├── Time
│   └── Published At
│
├── Raw Engagement
│   ├── Likes
│   ├── Saves
│   └── Comments Count
│
└── Derived Data
    └── Engagement
```

Search relationships and historical observations are stored separately rather than duplicated inside the Post object.

---

## 2.4 Candidate Post Input Specification

| Field | Source | Data Type | Requirement | Main Validation / Handling |
|---|---|---|---|---|
| Post ID | Platform | String | Required / Non-null | Valid format; corresponding post should be identifiable |
| Post URL | Platform | String | Required / Non-null | Valid URL; consistent with Platform |
| Platform | System / Platform | Enum | Required / Non-null | Must belong to supported platforms |
| Title | Platform | String | Required / Non-null | Trim whitespace; must not be empty after normalization |
| Post Content | Platform | String | Required | Complete → Valid; partial → Incomplete |
| Author | Platform | String | Optional | Missing author does not block Task A |
| Tags / Hashtags | Platform | Array<String> | Required / Empty Allowed | Field must exist; `[]` is valid |
| Published At | Platform | Datetime | Required / Non-null | Parseable; normalized; not future; within configured collection range |
| Likes | Platform | Integer | Required / Non-null | Normalize first; value >= 0 |
| Saves | Platform | Integer | Required / Non-null | Normalize first; value >= 0 |
| Comments Count | Platform | Integer | Required / Non-null | Normalize first; value >= 0 |
| Engagement | System Calculated | Integer | Derived | Likes + Saves + Comments Count |

---

## 2.5 Engagement

Current engagement formula:

```text
Engagement
=
Likes
+
Saves
+
Comments Count
```

`Likes`, `Saves`, and `Comments Count` are Raw Data.

`Engagement` is Derived Data.

Therefore:

```text
Raw Engagement Data
├── Likes
├── Saves
└── Comments Count

        ↓ Calculate

Derived Data
└── Engagement
```

The raw metrics should be preserved rather than storing only the final Engagement value.

---

## 2.6 Top 5 Candidate vs Priority Post

Two different business rules must remain separate.

### Candidate Selection

```text
Relevant Search Results
↓
Relevance + Engagement Evaluation
↓
Ranking
↓
Top 5
↓
Candidate Post Pool
```

`Top 5` determines which posts become Candidate Posts for lawyer review.

### Priority Post Eligibility

Current rule:

```text
Engagement > 500
→ Priority Post
```

Therefore:

```text
Candidate Post
↓
Calculate Engagement
↓
Engagement > 500?
├── Yes → Priority Post Pool
└── No  → Normal Candidate
```

A post does not need Engagement > 500 to become a Candidate Post.

`Top 5` and `Engagement > 500` serve different business purposes.

---

## 2.7 Tags / Hashtags

Tags / Hashtags are required because they support later workflows including:

- Long-tail Keyword Discovery
- Keyword Calibration
- Weekly Topic Analysis
- Publishing Tag Recommendation

Current specification:

```text
Data Type:
Array<String>

Requirement:
Required Field / Empty Allowed
```

Example:

```text
["劳动仲裁", "调岗降薪", "职场维权"]
```

Raw values should be normalized where possible.

Example:

```text
["#劳动仲裁", " 调岗降薪 ", "劳动仲裁"]

↓ Normalize

["劳动仲裁", "调岗降薪"]
```

Normalization may include:

- Remove `#`
- Trim whitespace
- Remove duplicate values

Important distinction:

```text
tags = []
→ Valid Empty

tags = null
→ Potential Missing Data
```

---

## 2.8 Post Content Data Quality

Post Content is required for later analysis, but incomplete content should not automatically cause the Post record to be discarded.

Possible states:

```text
Complete Content
→ Valid

Partial Content
→ Incomplete

Content expected but not obtained
→ Missing

Post deleted / inaccessible
→ Unavailable
```

Principle:

> Incomplete content does not automatically mean the post has no business value.

If partial content is still sufficient for initial screening, the Candidate Post may remain in the system and be enriched later.

---

## 2.9 Progressive Data Enrichment

The MVP uses Progressive Data Enrichment.

Task A does not need to collect all expensive or deep data immediately.

Current flow:

```text
Search Results
↓
Collect Basic Post Data
↓
Candidate Post Pool
↓
Lawyer Review
↓
Approved?
├── No → No Deep Enrichment
└── Yes
      ↓
Collect Additional Data
      ↓
Comment Content
      ↓
Task C — AI Content & Comment Analysis
```

Task A still collects:

```text
Comments Count
```

because it is required for Engagement calculation.

However:

```text
Comment Content
```

is collected later for posts approved for deeper analysis.

Purpose:

- reduce unnecessary data acquisition;
- reduce API / collection cost;
- reduce AI token usage;
- reduce storage and processing cost;
- focus deep analysis on higher-value posts.

---

## 2.10 Data Normalization

Raw social media data may use inconsistent formats.

The system should normalize raw data before validation.

General flow:

```text
Raw Platform Data
↓
Normalization
↓
Validation
↓
Eligible Data
```

Examples:

### Engagement Number

```text
"1.2万"
↓
12000
```

### Relative Time

```text
"昨天 18:30"
↓
Concrete Datetime
```

### Tags

```text
"#劳动仲裁,#调岗降薪"

↓ Normalize

["劳动仲裁", "调岗降薪"]
```

---

## 2.11 Datetime & Timezone

Two different time concepts must be distinguished.

### Published At

When the author published the post.

```text
Source:
Platform
```

### Collected At / Observed At

When the system collected a particular observation.

```text
Source:
System Generated
```

These timestamps serve different purposes.

Example:

```text
Published At:
2026-08-20 15:30 +08:00

Observed At:
2026-08-22 10:00 +08:00
```

Datetime data should use a clear and consistent timezone.

If source platforms use different timezone formats, the system should normalize them into the system's chosen standard.

---

## 2.12 Duplicate Post Handling

The same Post may appear under multiple Seed Keywords.

Example:

```text
Keyword A
↓
Post 001

Keyword B
↓
Post 001
```

The system should not create two separate Post objects.

Instead:

```text
Post 001
→ One Unique Post

Keyword A → Post 001
Keyword B → Post 001
→ Preserve Both Relationships
```

Therefore:

> Deduplication should remove duplicate Business Objects without deleting valuable search relationships.

---

## 2.13 Search Hit History

The system should preserve historical relationships between Seed Keywords and Posts.

Current logical structure:

```text
Search Hit
├── Post ID
├── Source Keyword
├── Search At
└── Search Rank
```

Purpose:

- record which keyword discovered which post;
- preserve multiple keyword-to-post relationships;
- support future Keyword Performance analysis;
- support Keyword Calibration;
- observe changes in search performance over time.

Example:

```text
Post 001

Search Hit 1
├── Keyword: 调岗降薪
├── Search At: Week 1
└── Search Rank: 1

Search Hit 2
├── Keyword: 恶意调岗
├── Search At: Week 2
└── Search Rank: 3
```

Search Rank should be treated as an observation signal rather than direct proof of post quality.

The exact use of Search Rank in Keyword Performance scoring will be defined later.

---

## 2.14 Engagement History

Engagement values change over time.

Therefore, new engagement observations should not overwrite previous observations.

Current logical structure:

```text
Engagement Observation
├── Post ID
├── Observed At
├── Likes
├── Saves
├── Comments Count
└── Engagement
```

Example:

```text
Post 001

2026-08-22
├── Likes: 200
├── Saves: 100
├── Comments: 150
└── Engagement: 450

2026-08-29
├── Likes: 700
├── Saves: 350
├── Comments: 400
└── Engagement: 1450
```

This allows later calculation of:

```text
Growth
Growth Rate
Trend
Growing / Stable / Declining
```

Task A creates the initial observation.

Task B adds later observations.

---

## 2.15 Search Hit History vs Engagement History

The system currently requires two different types of history.

### Search Hit History

Answers:

> Which keyword discovered which post, when, and at what search position?

```text
Keyword
↓
Search At
↓
Post
↓
Search Rank
```

Main use:

```text
Keyword Performance
Keyword Calibration
```

### Engagement History

Answers:

> How did the post's engagement change over time?

```text
Post
↓
Observed At
↓
Engagement Metrics
↓
Trend
```

Main use:

```text
Priority Post Tracking
Trend Detection
Topic Trend Analysis
```

The two histories should not be treated as the same dataset.

---

## 2.16 Missing / Invalid Data Handling

Data problems should be handled according to their cause.

Current general logic:

```text
Data Problem
↓
Determine Reason
↓
├── Source genuinely has no value
│   → Valid Empty
│
├── Temporary acquisition failure
│   → Retry
│
├── Raw format inconsistent
│   → Normalize
│
├── Current acquisition method cannot obtain full data
│   → Alternative Method / Mark Incomplete
│
├── Partial content
│   → Keep + Mark Incomplete
│
└── Post unavailable
    → Mark Unavailable
```

Retry should be bounded rather than infinite.

Failure reasons should be recorded where practical to support later system debugging and monitoring.

---

## 2.17 Task A Input Summary

Current Task A input flow:

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
        ↓
Social Media Search
        ↓
Raw Post Data
        ↓
Normalization
        ↓
Validation
        ↓
Deduplication
        ↓
Eligible Search Results
        ↓
Relevance + Engagement Evaluation
        ↓
Top 5 Candidate Posts
        ↓
Candidate Post Pool
```

At the same time:

```text
Keyword ↔ Post
↓
Search Hit History
```

and:

```text
Post
+
Observed At
+
Engagement Metrics
↓
Initial Engagement Observation
```

These datasets provide the foundation for later:

```text
Lawyer Review
↓
Deep Content & Comment Analysis
↓
Priority Post Tracking
↓
Long-tail Keyword Discovery
↓
Keyword Calibration
↓
Case Library Matching
↓
Candidate Topic Generation
```

---

## 2.18 Inputs for Downstream Workflows

Task A has completed detailed Input Analysis for the current MVP scope.

Tasks B–G have currently identified only their main Input / Dependency. Their detailed Input Analysis still needs to be completed.

| Workflow | Main Input / Dependency | Input Analysis Status |
|---|---|---|
| A. Social Media Content Collection | Seed Keyword Library + Platform Configuration + Search Configuration | Completed for Current MVP |
| B. Priority Post Tracking | Priority Post Pool + Post Identity + Previous Engagement History | To Be Completed |
| C. AI Content & Comment Analysis | Lawyer-approved Candidate Post + Enriched Comment Content | To Be Completed |
| D. Long-tail Keyword Discovery | Analyzed Post & Comment Library | To Be Completed |
| E. Seed Keyword Calibration | Keyword Library + Search Hit History + Historical Performance Data + Long-tail Candidates | To Be Completed |
| F. Case Library Matching | Approved Topic Pool + Case Library | To Be Completed |
| G. Candidate Script Topic Generation | Approved Topics + Topic Analysis + Trend Data + Case Matching Results | To Be Completed |

The project will complete detailed Input Analysis for Tasks B–G before moving into Process Analysis.

During the analysis of Tasks B–G, new downstream Input requirements may reveal missing upstream data requirements.

If this happens, the relevant upstream workflow should be updated.

Example:

Downstream Input Requirement
↓
Check Upstream Data
↓
Missing Required Data?
├── No → Continue
└── Yes → Update Upstream Data Requirement

Therefore, an Input marked as "Completed" means:

> Completed for the current MVP analysis stage, not permanently finalized.

## 2.19 Current Input Design Decisions

The MVP currently follows these principles:

```text
1. Collect minimum necessary data first.

2. Deep-enrich only higher-value / lawyer-approved posts.

3. Preserve Raw Engagement Data.

4. Calculate Engagement as Derived Data.

5. Do not overwrite historical engagement observations.

6. Deduplicate Posts without losing Keyword ↔ Post relationships.

7. Preserve Search Hit History for future Keyword Calibration.

8. Preserve Engagement History for Trend Detection.

9. Distinguish Empty, Missing, Incomplete and Unavailable data.

10. Normalize external platform data before Validation.

11. Use explicit Datetime and Timezone handling.

12. Defer detailed technical implementation until Technology Mapping.
```

---

## 2.20 Input Analysis Status

Current project status:

```text
Task A — Social Media Content Collection
Input Analysis: Completed for Current MVP

Task B — Priority Post Tracking
Input Analysis: To Be Completed

Task C — AI Content & Comment Analysis
Input Analysis: To Be Completed

Task D — Long-tail Keyword Discovery
Input Analysis: To Be Completed

Task E — Seed Keyword Calibration
Input Analysis: To Be Completed

Task F — Case Library Matching
Input Analysis: To Be Completed

Task G — Candidate Script Topic Generation
Input Analysis: To Be Completed