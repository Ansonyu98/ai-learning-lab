# Legal Content Automation - Workflow Analysis

## 0. Business Problem

### Current Workflow (As-Is)

Step 1: 律师根据自身业务方向确定案件类目。

Step 2: 将案件类目进一步拆分为不同分组。

Step 3: 针对每个分组，使用 AI 扩展和生成相关10个法律关键词。

Step 4: 律师使用关键词在社交媒体平台进行搜索，目前主要为小红书。

Step 5: 浏览搜索结果，根据帖子互动量进行初步筛选。

当前筛选标准：

```text
互动量
=
点赞量
+
收藏量
+
评论数
```

互动量 > 500 的帖子进入重点关注范围。

Step 6: 对筛选出的帖子进行内容分析和记录，重点关注：

- 帖子文案内容
- 帖子讨论的核心话题
- 评论区主要讨论的话题
- 当前互动数据

Step 7: 对值得关注的帖子进行持续追踪，在约 7 天后再次观察互动数据变化，用于判断内容及相关话题是否仍在获得流量。

Step 8: 将社交媒体热门话题与律师自身案例库进行匹配，寻找同类型或相关案例，最终由律师决定是否将其作为脚本选题。

---

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

---

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

---

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

---

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

---

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

---

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

---

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
- Lawyer Keep / Reject feedback

Keyword lifecycle:

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

The goal is to create a continuously updated keyword library based on real social media data rather than relying only on AI-generated keywords.

---

### Additional Requirement — Feishu Interaction & Delivery Layer

Feishu is not only used for daily notifications.

In the target system, Feishu should serve as the primary Human-in-the-loop interaction and result delivery layer for the lawyer.

The system should use Feishu to support different stages of the workflow, including:

- Daily collection result delivery
- Daily Candidate Post review
- Weekly analysis result delivery
- Trend analysis result delivery
- Long-tail keyword result delivery
- Candidate topic recommendation
- Lawyer review and approval actions
- Other Human-in-the-loop decisions required by the workflow

The lawyer should not need to enter the automation backend for normal business review and decision-making.

Conceptually:

```text
Automation / AI System
        ↓
      Feishu
        ↕
      Lawyer
        ↓
Human Decision
        ↓
Automation Continues
```

The exact Feishu implementation method, such as message cards, forms, tables, multi-dimensional tables or other interfaces, will be determined later during Product Design and Technology Mapping.

---

### Additional Requirement — Always-on Execution

The production MVP should operate independently of the lawyer's local computer.

Scheduled workflows must continue running when:

- the lawyer's personal computer is turned off;
- local development tools are not open;
- the lawyer is not actively operating the system.

Therefore, the production system requires an always-on execution environment.

Conceptually:

```text
Local Computer Offline
        ↓
Scheduled Workflow
        ↓
Still Executes Normally
```

The exact hosting or deployment technology is intentionally deferred until Technology Mapping.

Possible technical approaches should be evaluated later based on:

- Cost
- Reliability
- Maintenance effort
- Automation platform requirements
- Python requirements
- Database requirements
- API connectivity
- Deployment complexity

This is currently a system requirement, not a technology decision.

---

### Automation Goal

#### A. Fully Automated

系统应尽可能自动完成规则明确、重复性高、适合标准化执行的工作，包括：

- 根据关键词自动搜索和采集社交媒体帖子数据
- 对采集数据进行标准化、验证、去重和保存
- 计算并保存帖子互动数据
- 对每日 Candidate Posts 进行基础 AI 分析
- 由 AI 自动完成 Topic Classification
- 由 AI 自动生成供律师快速理解帖子内容的 Short Summary
- 将每日采集和基础分析结果通过 Feishu 推送给律师
- 定期重新获取 Priority Posts 的互动数据
- 保存历史互动数据并支持后续趋势分析
- 根据已确认和已分析的数据执行周期性分析
- 从真实社媒数据中发现潜在长尾词
- 将 Weekly Analysis、Long-tail Results 和 Candidate Topics 等结果通过 Feishu 交付

对于系统异常、数据无法获取、AI 无法形成可靠结果或其他异常情况，应进入相应的 Error Handling 或 Human Review 流程。

---

#### B. AI-assisted

对于需要更深层语义理解、匹配或推荐的工作，由 AI 完成第一轮处理，并保留律师最终业务或专业判断，包括：

- 根据案件类目和分组生成初始搜索关键词
- 对律师选择进行深入分析的帖子执行 Deep Post Analysis
- 根据 Deep Analysis 的业务需要，对评论数据执行结构化分析
- 提取真实用户问题、讨论重点和用户表达
- 根据真实平台数据辅助判断和校准关键词有效性
- 推荐新增、保留、观察或淘汰的关键词
- 从真实用户表达中推荐长尾关键词和标签
- 辅助识别社交媒体话题与律师案例库之间的相关性
- 推荐可能相关的真实案例
- 结合话题、用户讨论、趋势数据和案例信息生成候选脚本选题及推荐理由

Daily Topic Classification 和 Short Summary 属于系统自动执行的 Basic Analysis，不要求律师逐条确认分类。

---

#### C. Human-controlled

律师主要保留具有业务价值判断、专业判断和最终内容决策性质的工作，包括：

- 确定主要业务领域、案件类目和内容方向
- 判断每日 Candidate Post 是否值得保留
- 决定哪些帖子进入 Priority Post Pool
- 判断哪些 Priority Posts 值得进行 Deep Analysis
- 审核关键词库的重要调整
- 判断 AI 推荐案例是否真正适合用于内容创作
- 对候选选题进行专业判断
- 决定最终采用哪些脚本选题
- 对最终对外发布的法律观点和内容负责

Topic Classification 和日常帖子基础归类原则上由 AI 完成，不要求律师逐条进行人工分类。

---

#### Automation Boundary

The goal of this system is not to replace the lawyer's professional judgment.

The system should automate repetitive data collection, organization, basic analysis, tracking and periodic research work.

AI should be responsible for first-level understanding, classification, summarization, deeper semantic analysis, matching and recommendation where appropriate.

The lawyer should primarily act as a business-value and professional-quality gate.

Feishu should serve as the primary Human-in-the-loop interaction and result delivery layer.

The target production system should operate in an always-on environment and should not depend on the lawyer's local computer remaining online.

Expected workflow:

```text
Business Direction
↓
Keyword Generation & Validation
↓
Automated Social Media Collection
↓
Candidate Posts
↓
AI Basic Analysis
├── Topic Classification
└── Short Summary
↓
Feishu Daily Review
↓
Lawyer Value Decision
├── Reject
└── Keep
      ↓
Priority Post Pool
      ├── Priority Post Tracking
      │
      └── Deep Analysis Selection
              ↓
        Deep Post / Comment Analysis
              ↓
        Periodic Research Analysis
              ↓
        Long-tail Keyword Discovery
              ↓
        Keyword Feedback Loop
              ↓
        Case Library Matching
              ↓
        Candidate Topic Recommendation
              ↓
             Feishu
              ↓
        Lawyer Final Selection
```

---

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
- 不同关键词产生 Candidate Posts 的数量
- 不同关键词产生律师 Keep / Reject 结果的比例

**Goal:**

建立基于真实社交媒体数据的关键词评估机制，而不是仅依赖 AI 生成关键词。

关键词库应能够持续完成：

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

```text
AI Recommended Cases
↓
Lawyer Review
↓
Relevant / Not Relevant
```

**Baseline:**

当前主要依赖律师人工记忆和搜索案例库。

**Target:**

减少人工查找案例的时间，同时提高对潜在相关案例的发现能力。

---

#### 8. Topic Recommendation Quality

**Measure:**

系统生成的候选选题中，最终被律师认可或采用的比例。

Example:

```text
20 Candidate Topics Generated
↓
8 Accepted by Lawyer

Recommendation Adoption Rate
=
8 / 20
=
40%
```

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

#### 9. Research Retention Rate — Potential Metric

**Measure:**

每日系统产生的 Candidate Posts 中，最终被律师判断为值得保留并进入 Priority Post Pool 的比例。

Example:

```text
20 Candidate Posts
↓
Lawyer Review
↓
8 Kept as Priority Posts

Research Retention Rate
=
8 / 20
=
40%
```

该指标可以用于评估：

- 搜索关键词质量
- Candidate Selection Quality
- 每日采集结果的业务相关性
- 上游数据采集是否持续产生有价值的数据

**Baseline:**

TBD

**Target:**

TBD

该指标当前作为 Potential Metric 保留。

在获得真实运行数据前，不人为设定目标值。

---

### MVP Success Criteria

第一版系统（MVP）优先验证：

1. 是否能够明显减少人工搜索、整理和追踪时间
2. 是否能够稳定采集并保存有效社媒数据
3. 是否能够形成统一的帖子和话题基础分析结果
4. 是否能够通过 Feishu 支持律师完成日常数据审核
5. 是否能够持续追踪 Priority Posts 的互动数据
6. 是否能够根据真实数据改善关键词库
7. 是否能够辅助律师找到相关案例
8. 是否能够输出具有实际使用价值的候选选题
9. 是否能够在不依赖律师本地电脑在线的情况下持续运行

具体数值目标将在系统获得真实运行数据后，根据 Baseline 进一步确定。

---

### Future Metrics

以下指标暂不作为第一版 MVP 的核心 Success Metrics：

```text
Content Recommendation
↓
Lawyer Adoption
↓
Content Published
↓
Actual Views / Likes / Comments / Saves
↓
Feedback to Topic Recommendation System
```

未来可以进一步研究：

- 推荐选题实际发布后的内容表现
- 高表现内容与原始 Topic Heat Score 的相关性
- 哪些类型的选题更容易被律师采用
- 发布结果是否可以反向优化选题评分机制

该 Feedback Loop 暂列为 Future Improvement，避免扩大第一版 MVP Scope.

---

# 1. Trigger

The Legal Content Automation System contains multiple workflows with different trigger mechanisms.

The MVP primarily uses scheduled batch processing combined with human review and workflow dependencies.

Trigger analysis should distinguish between:

```text
Trigger
↓
Upstream Dependency
↓
Precondition
↓
Execution Rule
↓
Execution
```

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
- Avoid duplicate creation of previously stored Post objects where possible.
- Preserve valid Keyword ↔ Post search relationships.

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

### Trigger A2 — Daily Basic Analysis & Lawyer Review

**Workflow:**

Candidate Posts → AI Basic Analysis → Feishu Daily Review → Lawyer Value Decision

**Trigger Type:**

Workflow Completion + Human-in-the-loop.

**Trigger Condition:**

Task A completes the current daily collection cycle and produces valid Candidate Posts.

**Upstream Dependencies:**

- Task A — Social Media Content Collection
- Candidate Post Pool
- Initial Engagement Observation

**Precondition:**

At least one valid Candidate Post must exist for the current collection cycle.

If no valid Candidate Post exists, the daily review workflow may be skipped and the reason recorded.

**Execution Rules:**

For each Candidate Post, the system should automatically generate basic information that helps the lawyer quickly understand the collected data.

Current MVP Basic Analysis includes:

- Topic Classification
- Short Summary
- Current Engagement Data
- Source Post Information

The system should deliver the daily results to the lawyer through Feishu.

The lawyer does not need to manually classify the topic.

The lawyer's main decision is:

```text
Worth Keeping?
├── No → Reject / Archive
└── Yes → Priority Post Pool
```

Initial Engagement and other quantitative signals may support the lawyer's review but do not independently determine Priority status.

**Execution Mode:**

Automated Analysis + Feishu Human Review.

**Purpose:**

Reduce the lawyer's daily information-processing workload while preserving human control over which collected data has enough business value to remain in the research system.

**Important Distinction:**

```text
AI
→ What is this post mainly about?

Lawyer
→ Is this post worth keeping for future research?
```

These are different decisions.

Topic Classification belongs to AI.

Research-value judgment belongs to the lawyer.

---

### Trigger B — Priority Post Tracking

**Workflow:**

Re-fetch engagement data for lawyer-confirmed Priority Posts.

**Trigger Type:**

Schedule Trigger

**Trigger Condition:**

Every Sunday at 10:00.

**Upstream Dependency:**

Priority Post Pool created through Task A2 lawyer review.

**Precondition:**

The Priority Post Pool must contain posts that:

- have been confirmed by the lawyer as worth keeping;
- remain eligible for follow-up tracking;
- have reached the minimum tracking interval from Initial Observed At.

Current MVP minimum tracking interval:

```text
7 days from Initial Observed At
```

If no eligible posts exist, the scheduled tracking workflow should be skipped and the reason recorded.

**Priority Eligibility Rule:**

Priority status is determined by lawyer value judgment.

```text
Candidate Post
↓
AI Basic Analysis
↓
Feishu Review
↓
Lawyer: Worth Keeping?
├── No → Not Priority
└── Yes → Priority Post Pool
```

Current engagement calculation remains:

```text
Engagement
=
Likes
+
Saves
+
Comments Count
```

`Engagement > 500` remains an important high-engagement signal that can support screening and lawyer review.

However:

```text
Engagement > 500
≠ Automatically Priority
```

The engagement threshold is a quantitative signal, not the final business-value decision.

**Execution Rules:**

- Re-fetch the latest engagement data for eligible Priority Posts.
- Store new engagement data without overwriting historical observations.
- Preserve Post ID across observation periods.
- Preserve Initial Observed At as the baseline for the tracking interval.
- Avoid duplicate tracking observations for the same tracking run / observation period.
- For the current MVP, perform Initial Observation + one follow-up observation.
- After a valid follow-up observation, the current MVP tracking cycle may be considered completed.
- Deleted, private or temporarily unavailable posts should preserve historical data and record the appropriate availability state.

**Execution Mode:**

Weekly Batch Processing.

**Purpose:**

Create historical engagement data that can later be used to evaluate whether lawyer-confirmed Priority Posts and their related topics continue to gain attention.

**Important Distinction:**

```text
Lawyer Keep Decision
→ Priority Eligibility

7-day Interval
→ Tracking Eligibility

Sunday 10:00
→ Tracking Trigger
```

These three concepts must not be mixed together.

---

### Trigger C — Deep AI Content & Comment Analysis

**Workflow:**

Perform deeper AI analysis on selected Priority Posts and, when required by the Deep Analysis workflow, selected comment data.

**Trigger Type:**

Human Decision / Event-driven Trigger.

**Trigger Condition:**

A lawyer-confirmed Priority Post is marked as requiring Deep Analysis.

Conceptually:

```text
Priority Post
↓
Lawyer: Deep Analysis Required?
├── No → Remain in Research / Tracking Pool
└── Yes → Task C
```

**Upstream Dependencies:**

- Priority Post Pool
- Candidate Post Data
- AI Basic Analysis Result
- Lawyer Keep Decision
- Deep Analysis Request

**Precondition:**

The post must:

- already belong to the Priority Post Pool;
- have a valid Deep Analysis request;
- contain sufficient valid content for the requested analysis;
- not already have a valid completed analysis for the same valid input state under the current MVP.

**Execution Rules:**

Task C is a deeper research workflow and is not required to run for every daily Candidate Post.

Deep Analysis may include:

- Core Topic
- User Problem
- Legal Issue
- Key Discussion Points
- User Expressions
- Other structured research fields defined later

Comment Analysis is conditional and exists to support downstream research such as topic discovery and long-tail keyword discovery.

When Comment Analysis is required by the Deep Analysis workflow:

```text
Deep Analysis
↓
Need Comment-level Research Data?
├── No
│   → Post Analysis only
└── Yes
      ↓
Comment Data Enrichment
      ↓
Comment Selection
      ↓
Comment Analysis
```

Current confirmed Comment Selection rule:

1. Prioritize valid comments with both high engagement and strong relevance to the post.
2. If fewer than 10 such comments are available, retain those comments and supplement the set with the latest valid comments.
3. Analyze a maximum of 10 selected comments.
4. If fewer than 10 valid comments exist in the available pool, analyze the available valid comments rather than requiring exactly 10.

The exact definitions of:

- High Engagement
- Relevance
- Comment Sufficiency
- Comment Retrieval Limit

will be determined later during Decision Analysis and Technology Mapping.

**Execution Mode:**

Human-in-the-loop / Event-driven Deep Analysis.

**Purpose:**

Use lawyer-selected high-value research data for deeper structured analysis that can support:

- Long-tail Keyword Discovery
- User-language discovery
- Topic research
- Case Matching
- Candidate Topic Generation

Task C is not the daily basic-analysis workflow.

Daily Basic Analysis belongs to Task A2.

---

### Trigger D — Long-tail Keyword Discovery

**Workflow:**

Discover long-tail expressions from previously deep-analyzed social media content.

**Trigger Type:**

Schedule Trigger.

**Trigger Condition:**

Every Sunday at 10:30.

**Upstream Dependency:**

Task C — Deep AI Content & Comment Analysis.

The workflow depends on valid Deep Analyzed Research Data accumulated from Priority Posts selected for deeper analysis.

Daily Basic Analysis results alone do not automatically qualify as Deep Analyzed Research Data.

**Precondition:**

The Deep Analyzed Research Data must contain valid analyzed records from the current analysis period.

If no valid deep-analyzed content exists, the scheduled workflow should be skipped and the reason recorded.

**Execution Rules:**

Analyze real user language appearing in:

- Post titles
- Post content
- Comments where available and relevant
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
Priority Post Pool
↓
Deep Analysis Selection
↓
Task C — Deep AI Analysis
↓
Deep Analyzed Research Data
↓
Accumulate During the Analysis Period
↓
Sunday 10:30
↓
Long-tail Keyword Discovery
↓
Long-tail Keyword Candidates
↓
Feishu Weekly Result Delivery
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
- Search Hit History
- Engagement History
- Deep Analyzed Research Data
- Long-tail keyword discovery results
- Lawyer Keep / Reject feedback

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

Use real social media performance and lawyer feedback to continuously improve the quality of search keywords.

**Keyword Feedback Flow:**

```text
Seed Keyword Library
↓
Social Media Collection
↓
Search Hit History
+
Engagement History
+
Lawyer Keep / Reject Feedback
↓
Deep Analysis
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

Keyword calibration should be based on real social media performance and business-value feedback rather than relying only on AI-generated keywords.

---

### Trigger F — Case Library Matching

**Workflow:**

Match lawyer-approved topics with potentially relevant cases from the lawyer's case library.

**Trigger Type:**

Schedule Trigger.

**Trigger Condition:**

Every Sunday at 10:30.

**Upstream Dependencies:**

- Deep Analyzed Research Data
- Topic Analysis Results
- Lawyer Approval
- Approved Topic Pool
- Lawyer Case Library

**Precondition:**

The Approved Topic Pool must contain at least one topic approved by the lawyer during the current analysis period.

The Case Library must also be available for retrieval.

If no approved topics exist, Case Library Matching should be skipped.

**Execution Rules:**

Only topics explicitly approved by the lawyer should enter weekly Case Library Matching under the current architecture.

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

The Approved Topic architecture will be re-validated during Task F Input Analysis.

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

The Candidate Topic results should be delivered through Feishu for lawyer review.

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
Feishu
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
| A2. Daily Basic Analysis & Lawyer Review | Workflow Completion + Human Review | Task A produces Candidate Posts | Candidate Post Pool | Automated Analysis + Feishu Human Review |
| B. Priority Post Tracking | Schedule | Sunday 10:00 | Lawyer-confirmed Priority Post Pool | Weekly Batch |
| C. Deep AI Content & Comment Analysis | Human Decision / Event | Priority Post marked Deep Analysis Required | Priority Post Pool | Human-in-the-loop / Event-driven |
| D. Long-tail Keyword Discovery | Schedule | Sunday 10:30 | Deep Analyzed Research Data | Weekly Batch |
| E. Seed Keyword Calibration | Schedule | Last day of month 10:00 | Historical Keyword & Content Data | Monthly Batch |
| F. Case Library Matching | Schedule | Sunday 10:30 | Approved Topic Pool + Case Library | Weekly Batch |
| G. Candidate Script Topic Generation | Workflow Completion | Case Matching completed | Topic + Case Matching Results | Weekly Batch |

**System-level Execution Requirement:**

All scheduled production workflows must run in an always-on environment independent of the lawyer's local computer.

**Human Interaction Requirement:**

Feishu serves as the primary interaction and result-delivery layer for daily review, weekly analysis and candidate topic workflows.

---

### Trigger Dependency Overview

```text
Official Seed Keyword Library
        ↓
[Mon–Sat 10:00]
        ↓
A. Social Media Content Collection
        ↓
Candidate Posts
        ↓
A2. AI Daily Basic Analysis
├── Topic Classification
└── Short Summary
        ↓
Feishu Daily Review
        ↓
Lawyer: Worth Keeping?
        │
        ├── No → Reject / Archive
        │
        └── Yes
              ↓
        Priority Post Pool
              │
              ├──────────────────────────────┐
              │                              │
              ↓                              ↓
       [Eligible after                Lawyer:
        minimum interval]             Deep Analysis Required?
              │                              │
       [Sunday 10:00]                 ├── No → Keep / Track
              ↓                       │
       B. Priority Post Tracking      └── Yes
              ↓                              ↓
       Engagement History             C. Deep AI Analysis
                                             │
                                  ┌──────────┴──────────┐
                                  ↓                     ↓
                           Post Deep Analysis     Comment Analysis
                                                  when required
                                  └──────────┬──────────┘
                                             ↓
                                  Deep Analyzed Research Data
                                             │
                    ┌────────────────────────┼──────────────────────┐
                    ↓                        ↓                      ↓
             [Sunday 10:30]           Topic Research         Trend / Research Data
                    ↓
          D. Long-tail Discovery
                    ↓
          Long-tail Candidates
                    │
                    ↓
           Keyword Performance Data
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


Deep Analyzed Research Data
        ↓
Topic Analysis
        ↓
Approved Topic Architecture
[To Be Re-validated during Task F Input Analysis]
        ↓
F. Case Library Matching
        ↓
Matching Results
        ↓
G. Candidate Topic Generation
        ↓
Feishu Candidate Topic Delivery
        ↓
Lawyer Final Review
        ↓
Final Selected Topics
```

**Feishu Interaction Layer:**

```text
Daily Collection Review
+
Weekly Analysis Delivery
+
Long-tail / Research Results
+
Candidate Topic Delivery
+
Human Review / Approval
```

**Execution Environment:**

```text
Always-on Production Environment
        ↓
Scheduled / Event-driven Automation
        ↓
Runs independently of local computer
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
Deep Analyzed Research Data
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
Lawyer: Worth Keeping?
↓
YES → Priority Post Pool
NO → Reject / Archive
```

A quantitative signal may support a Decision without becoming the Decision itself.

Example:

```text
Engagement > 500
→ High-engagement Signal

Engagement > 500
≠ Automatic Priority Decision
```

Core principle:

```text
Signal
≠
Decision
```

---

### Key Learning

A workflow may depend on another workflow without being directly triggered by that workflow.

Example:

```text
Task C
↓
Produces Deep Analyzed Research Data
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

---

# 2. Input

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
Task A — Social Media Content Collection
        ↓
Candidate Post Data
        ↓
Task A2 — AI Basic Analysis
├── Topic Classification
└── Short Summary
        ↓
Feishu Daily Review
        ↓
Lawyer Keep / Reject Decision
        ↓
Priority Post Pool
        │
        ├── Task B — Tracking
        │
        └── Deep Analysis Selection
                  ↓
          Deep Data Enrichment
                  ↓
          Task C — Deep AI Analysis
```

Historical and feedback data is also required for later workflows:

```text
Search Hit History
→ Keyword Performance / Calibration

Engagement History
→ Post Trend Detection

Lawyer Keep / Reject Feedback
→ Collection Quality / Keyword Calibration

Deep Analyzed Research Data
→ Long-tail Keyword Discovery
→ Topic Research

Approved Topic Pool
→ Case Library Matching
[Architecture to be re-validated]

Case Library
→ Candidate Topic Generation
```

The system uses Progressive Data Enrichment rather than acquiring all deep data for all Candidate Posts.

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
- AI Basic Analysis;
- lawyer review;
- engagement calculation;
- future tracking;
- later Deep Analysis.

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
        ↓
Calculate
        ↓
Derived Data
└── Engagement
```

The raw metrics should be preserved rather than storing only the final Engagement value.

---

## 2.6 Top 5 Candidate Posts vs High-engagement Signal vs Priority Posts

These are different concepts.

### Candidate Post

Task A selects a maximum of 5 Candidate Posts per seed keyword per collection run based on the current Candidate Selection Strategy.

Current strategy considers:

- Business relevance
- Engagement

Candidate selection determines:

> Which collected posts are worth presenting for daily review?

---

### High-engagement Signal

Current engagement calculation:

```text
Engagement
=
Likes
+
Saves
+
Comments Count
```

Current reference threshold:

```text
Engagement > 500
```

This threshold identifies a high-engagement signal.

However:

```text
Engagement > 500
≠ Priority Post
```

A high-engagement post may still be irrelevant to the lawyer's content research needs.

---

### Priority Post

A Candidate Post becomes a Priority Post only after lawyer review.

```text
Candidate Post
↓
AI Basic Analysis
↓
Feishu Daily Review
↓
Lawyer: Worth Keeping?
├── No → Reject / Archive
└── Yes → Priority Post Pool
```

Therefore:

```text
Candidate Selection
≠
High-engagement Signal
≠
Priority Decision
```

They serve different purposes:

```text
Candidate Selection
→ Controls what enters daily review

High-engagement Signal
→ Provides quantitative evidence for review

Lawyer Keep Decision
→ Controls what enters Priority Post Pool
```

Priority Posts may later be used for:

- 7-day Engagement Tracking
- Historical Research Data
- Deep Analysis Selection
- Downstream Topic and Keyword Research

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

If partial content is still sufficient for Daily Basic Analysis or lawyer review, the Candidate Post may remain in the system and be enriched later.

Deep Analysis may require a higher completeness standard than Daily Basic Analysis.

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
AI Basic Analysis
├── Topic Classification
└── Short Summary
↓
Feishu Daily Review
↓
Lawyer: Worth Keeping?
├── No
│   → Reject / Archive
│   → No Deep Enrichment
└── Yes
      ↓
Priority Post Pool
      │
      ├── Tracking
      │
      └── Lawyer: Deep Analysis Required?
              ├── No
              │   → Keep / Track
              └── Yes
                    ↓
              Deep Data Enrichment
                    ↓
              Task C — Deep AI Analysis
                    ↓
              Comment Data
              when required by Deep Analysis
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

is not required for every Candidate Post.

It is acquired later when downstream Deep Analysis requires it.

Purpose:

- reduce unnecessary data acquisition;
- reduce API / collection cost;
- reduce AI token usage;
- reduce storage and processing cost;
- focus deep analysis on higher-value posts.

Core principle:

> Collect minimum necessary data first.  
> Enrich deeper only when downstream business value requires it.

---

## 2.10 Data Normalization

Raw social media data may use inconsistent formats.

The system should normalize raw data before validation when validation depends on normalized values.

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

Important distinction:

```text
Not Required
≠
Missing
```

A field that is not required for the current workflow stage should not be treated as missing data.

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

Task A does not make the final Priority decision.

Its downstream flow is:

```text
Candidate Post Pool
↓
Task A2 — AI Basic Analysis
├── Topic Classification
└── Short Summary
↓
Feishu Daily Review
↓
Lawyer: Worth Keeping?
├── No → Reject / Archive
└── Yes
      ↓
Priority Post Pool
      ├── Task B — Priority Post Tracking
      └── Deep Analysis Selection
              ↓
          Task C
```

`Engagement > 500` remains a high-engagement signal but does not independently place a post into the Priority Post Pool.

---

## 2.18 Inputs for Downstream Workflows

Task A has completed detailed Input Analysis for the current MVP scope.

The clarified Daily Review architecture introduces Task A2 between Collection and Priority Post creation.

Current downstream dependencies are:

| Workflow | Main Input / Dependency | Input Analysis Status |
|---|---|---|
| A. Social Media Content Collection | Seed Keyword Library + Platform Configuration + Search Configuration | Completed for Current MVP |
| A2. Daily Basic Analysis & Lawyer Review | Candidate Post Pool + Initial Engagement Observation + Basic Analysis Configuration + Feishu Review Context | Completed for Current MVP |
| B. Priority Post Tracking | Lawyer-confirmed Priority Post Pool + Post Identity + Previous Engagement History + Tracking Configuration | Completed for Current MVP |
| C. Deep AI Content & Comment Analysis | Priority Post + Deep Analysis Request + Post Content + Conditional Comment Data | In Progress |
| D. Long-tail Keyword Discovery | Deep Analyzed Research Data | To Be Completed |
| E. Seed Keyword Calibration | Keyword Library + Search Hit History + Historical Performance Data + Long-tail Candidates + Lawyer Keep / Reject Feedback | To Be Completed |
| F. Case Library Matching | Approved Topic Pool + Case Library | To Be Re-validated |
| G. Candidate Script Topic Generation | Topic Analysis + Trend Data + Case Matching Results | To Be Completed |

The project will complete detailed Input Analysis across the remaining workflows before moving into Process Analysis.

During downstream analysis, new Input requirements may reveal missing upstream requirements.

```text
Downstream Requirement
↓
Check Upstream Data
↓
Missing?
├── No → Continue
└── Yes → Revise Upstream Requirement
```

This has already occurred in the current project:

```text
Deep Analysis Requirement
↓
Clarified Daily Review Requirement
↓
Discovered Need for AI Basic Analysis
+
Feishu Human Review
↓
Revised Priority Post Entry Logic
↓
Updated Workflow Architecture
```

Therefore:

> Completed means completed for the current MVP analysis stage, not permanently finalized.

---

## 2.19 Current Input Design Decisions

The MVP currently follows these principles:

```text
1. Collect minimum necessary data first.

2. Use AI Basic Analysis to help the lawyer understand daily Candidate Posts.

3. AI performs Topic Classification and Short Summary generation.

4. Lawyer performs business-value judgment rather than routine topic classification.

5. A Candidate becomes Priority only after lawyer Keep decision.

6. Engagement > 500 is a signal, not an automatic Priority decision.

7. Deep-enrich only Priority Posts selected for Deep Analysis.

8. Comment Data is Conditional Required only when the Deep Analysis workflow requires Comment Analysis.

9. Not Required is different from Missing.

10. Preserve Raw Engagement Data.

11. Calculate Engagement as Derived Data.

12. Do not overwrite historical engagement observations.

13. Deduplicate Posts without losing Keyword ↔ Post relationships.

14. Preserve Search Hit History for future Keyword Calibration.

15. Preserve Engagement History for Trend Detection.

16. Preserve lawyer Keep / Reject decisions as future feedback data.

17. Distinguish Empty, Missing, Incomplete, Unavailable and Not Required.

18. Normalize external platform data before Validation when required.

19. Use explicit Datetime and Timezone handling.

20. Use Feishu as the primary Human-in-the-loop interaction and result delivery layer.

21. Production workflows must eventually run in an always-on environment independent of the local computer.

22. Defer detailed technical implementation until Technology Mapping.
```

---

## 2.20 Input Analysis Status

```text
Task A — Social Media Content Collection
Input Analysis:
Completed for current MVP scope

Task A2 — Daily Basic Analysis & Lawyer Review
Input Analysis:
Completed for current MVP scope

Task B — Priority Post Tracking
Input Analysis:
Completed for current MVP scope

Task C — Deep AI Content & Comment Analysis
Input Analysis:
In Progress

Tasks D–G
Detailed Input Analysis:
To Be Completed
```

Current analysis sequence:

```text
Complete Task C Input
↓
Task D Input
↓
Task E Input
↓
Task F Input
↓
Task G Input
↓
Cross-workflow Input Review
↓
Complete Day 03
↓
Begin Process Analysis
```

---

## 2.21 Task A2 — Daily Basic Analysis & Lawyer Review: Detailed Input Analysis

### 2.21.1 Task Purpose

Task A2 converts daily Candidate Posts into reviewable research items.

Its purpose is not to perform full Deep Analysis.

Instead, it should help the lawyer quickly understand:

```text
What was collected today?
+
What is this post mainly about?
+
Is it worth keeping?
```

Current flow:

```text
Candidate Post
↓
AI Basic Analysis
├── Topic Classification
└── Short Summary
↓
Feishu Daily Review
↓
Lawyer Keep / Reject
```

---

### 2.21.2 Candidate Post Input

**Source:**

Task A Candidate Post Pool.

**Requirement:**

Required.

Task A2 requires the Candidate Post identity, content and current engagement data created during Task A.

Required conceptual inputs include:

```text
Post ID
Post URL
Platform
Title
Post Content
Tags / Hashtags
Published At
Likes
Saves
Comments Count
Engagement
```

Author remains Optional unless a future business requirement makes it necessary.

---

### 2.21.3 Basic Analysis Configuration

Task A2 requires configuration defining the minimum Daily Basic Analysis output.

Current MVP requires:

```text
Topic Classification
Short Summary
```

The exact prompt, LLM, model parameters and structured output implementation are intentionally deferred until Technology Mapping and Implementation.

The business requirement is:

> AI should produce enough information for the lawyer to understand the post without manually reading every collected item in full.

---

### 2.21.4 Topic Classification

Topic Classification is generated by AI.

It should answer:

> What is this post mainly about from the content-research perspective?

Topic Classification is not a lawyer input.

The lawyer is not expected to manually categorize every Candidate Post during the daily workflow.

The exact topic taxonomy will be refined later if required.

---

### 2.21.5 Short Summary

Short Summary is generated by AI.

It should provide a concise explanation of:

- what happened;
- what problem the user is discussing;
- what the post is mainly concerned with.

The exact summary format and length belong to later Output / Product Design.

---

### 2.21.6 Current Engagement Context

Daily review should receive current engagement information.

Required data:

```text
Likes
Saves
Comments Count
Engagement
```

This data already exists from Task A and should be reused rather than recollected solely for Task A2.

Engagement is a supporting signal for lawyer review.

It is not the final Priority Decision.

---

### 2.21.7 Feishu Review Context

Task A2 requires a destination / review context that allows the system to deliver reviewable Candidate Posts through Feishu.

At the business-analysis stage, the requirement is only:

```text
System Result
↓
Feishu
↓
Lawyer Review
```

The exact implementation may later use:

- message cards;
- tables;
- multi-dimensional tables;
- forms;
- other Feishu interfaces.

No implementation method is selected at the Input stage.

---

### 2.21.8 Lawyer Review Decision

Task A2 requires a human decision for each reviewed Candidate Post:

```text
Worth Keeping?
```

Conceptual result:

```text
Keep
Reject
```

The decision should be associated with:

```text
Post ID
Review Result
Reviewed At
```

The exact storage implementation will be determined later.

The system should preserve the decision as feedback data rather than treating it only as a temporary interaction event.

---

### 2.21.9 Priority Post Creation

A Candidate Post enters the Priority Post Pool only when:

```text
Lawyer Review Result = Keep
```

Therefore:

```text
Engagement > 500
→ Supporting Signal

Lawyer Keep
→ Priority State Change
```

This distinction should remain explicit throughout downstream workflows.

---

### 2.21.10 Review Feedback as Historical Data

Lawyer Keep / Reject decisions may later support:

- Research Retention Rate
- Candidate Selection Quality evaluation
- Keyword Calibration
- Collection Quality improvement
- Future AI evaluation

Therefore, the review result should be treated as reusable business feedback.

---

### 2.21.11 Data Quality

AI Basic Analysis may fail or produce insufficient output.

Conceptual quality states may include:

```text
Valid
Incomplete
Invalid
Unavailable
```

Examples:

```text
Post Content incomplete
→ Basic Analysis may still be possible
→ Mark quality appropriately

AI returns unusable structure
→ Invalid Analysis Output

Source post unavailable before analysis
→ Unavailable
```

Exact retry and fallback logic belongs to Process / Error Handling.

---

### 2.21.12 Task A2 Input Summary

```text
Candidate Post Data
+
Initial Engagement Observation
+
Basic Analysis Configuration
+
Feishu Review Context
↓
AI Basic Analysis
↓
Feishu Delivery
↓
Lawyer Keep / Reject
↓
Priority Post Pool
```

Task A2 is complete for the current MVP Input Analysis scope.

---

## 2.22 Task B — Priority Post Tracking: Detailed Input Analysis

### 2.22.1 Task Purpose

Task B tracks lawyer-confirmed Priority Posts after the initial observation in order to determine how their engagement changes over time.

MVP tracking scope:

- Priority status is created through lawyer Keep decision.
- Engagement > 500 does not independently determine Priority status.
- Each eligible Priority Post requires one follow-up tracking cycle after the minimum 7-day interval.
- Long-term continuous tracking is outside the current MVP scope.

Core comparison:

```text
Initial Engagement
vs.
Follow-up Engagement
```

Business purpose:

> Determine how the post's total engagement changed after the initial observation and provide historical data for later trend analysis.

---

### 2.22.2 Tracking Target

**Source:**

Priority Post Pool.

**Requirement:**

Required.

A post becomes a Priority Post when:

```text
Candidate Post
↓
AI Basic Analysis
↓
Feishu Review
↓
Lawyer Keep
↓
Priority Post Pool
```

Task B therefore consumes Priority status created by Task A2.

Each Tracking Target requires:

- Post ID
- Post URL
- Platform
- Initial Observed At
- Initial Engagement Observation
- Tracking Status

The Post ID remains the primary identity used to associate the same post with multiple observations over time.

---

### 2.22.3 Post Identity

Task B reuses Post Identity created during Task A.

Required identity fields:

```text
Post ID
Post URL
Platform
```

Purpose:

- identify the same post across tracking cycles;
- locate the original post for follow-up data acquisition;
- associate new observations with existing historical records.

Task B must not create a new Post entity when tracking an existing Priority Post.

---

### 2.22.4 Initial Engagement Observation

Task B requires the Initial Engagement Observation created during Task A.

Required historical fields:

```text
Post ID
Observed At
Likes
Saves
Comments Count
Engagement
```

Where:

```text
Engagement
=
Likes
+
Saves
+
Comments Count
```

The Initial Observation must remain unchanged.

Follow-up tracking must append a new observation rather than overwrite the Initial Observation.

Example:

```text
Post 001

Initial Observation
├── Observed At
├── Likes
├── Saves
├── Comments Count
└── Engagement

Follow-up Observation
├── Observed At
├── Likes
├── Saves
├── Comments Count
└── Engagement
```

This forms the Engagement History for the post.

---

### 2.22.5 Tracking Interval

**Tracking Interval:**

```text
7 days minimum
```

A Priority Post becomes eligible for follow-up tracking only after at least 7 days have passed since its Initial Observed At.

Conceptually:

```text
Initial Observed At
+
7 Days
↓
Follow-up Eligible
```

Task B itself is triggered by the Sunday 10:00 schedule.

Therefore:

```text
7 Days
=
Minimum Tracking Interval

Sunday 10:00
=
Execution Schedule
```

A post does not have to be tracked exactly on Day 7.

If the 7-day interval has not been reached when the Sunday batch starts:

```text
Not Eligible
↓
Skip for current tracking batch
```

The post remains available for the next eligible tracking batch.

If no Priority Posts are eligible during a scheduled Task B run:

```text
No Eligible Tracking Targets
↓
Skip Tracking
```

---

### 2.22.6 Tracking Status / State

Task B requires the system to know whether a Priority Post still requires follow-up tracking.

Tracking Status represents the current tracking lifecycle state of the post.

Conceptual states may include:

```text
Waiting
Due
Active
Completed
Unavailable
```

Exact implementation values may be refined later.

The important business requirement is:

> The system must distinguish between posts waiting for follow-up, posts currently eligible for tracking, posts whose MVP follow-up has been completed, and posts that are no longer available.

For the current MVP:

```text
Priority Post
↓
Initial Observation Exists
↓
Wait Minimum 7 Days
↓
Follow-up Eligible
↓
Follow-up Tracking
↓
Successful Follow-up Observation
↓
MVP Tracking Completed
```

Future continuous or conditional tracking is outside the current MVP scope.

---

### 2.22.7 Tracking Run Context

Task B requires execution context so that the system can distinguish:

- which weekly tracking run produced an observation;
- whether the same post has already been processed during the same tracking period;
- an intentional new historical observation from an accidental duplicate caused by workflow retry.

Required conceptual fields:

```text
Tracking Run ID
Run Time
```

`Tracking Run ID` identifies the weekly tracking execution.

`Run Time` records when the tracking batch started.

These are different from:

```text
Observed At
```

`Observed At` records when the engagement data for the individual post was actually observed.

Conceptually:

```text
Tracking Run
└── Post
    └── Observation
```

---

### 2.22.8 Observation Period and Duplicate Prevention

Task B must not create duplicate Follow-up Observations for the same post within the same tracking run.

Conceptually:

```text
Post ID
+
Tracking Run ID
```

identifies whether the post has already been successfully processed during that tracking run.

Example:

```text
Sunday 10:00
↓
Post 001
↓
Follow-up Observation Created
↓
Workflow accidentally retries at 10:05
↓
Same Post ID + Same Tracking Run ID
↓
Do Not Create Duplicate Follow-up Observation
```

A retry within the same tracking run must not be interpreted as a new historical observation period.

---

### 2.22.9 Follow-up Engagement Observation

When follow-up acquisition succeeds, Task B creates a new Engagement Observation.

Required fields:

```text
Post ID
Observed At
Likes
Saves
Comments Count
Engagement
Tracking Run ID
```

The new observation is appended to Engagement History.

Example:

```text
Post 001

Initial Observation
Engagement = 800

Follow-up Observation
Engagement = 1600
```

Task B preserves both observations.

It must not perform:

```text
800
↓ overwrite
1600
```

Historical observations are immutable records of what was observed at a specific point in time.

---

### 2.22.10 Current State vs Historical Observation

Task B distinguishes between:

**Current State**

The latest known state of the post.

and:

**Historical Observation**

A snapshot of engagement metrics observed at a specific time.

Example:

```text
Post 001
│
├── Observation 1
│   └── Engagement = 800
│
└── Observation 2
    └── Engagement = 1600
```

The Post remains the same business object.

The observations represent different points in time.

Historical observations must not be deleted or overwritten when the current state changes.

---

### 2.22.11 Availability Status

Follow-up acquisition may fail because the post is no longer accessible.

Task B must distinguish between temporary acquisition failure and post availability changes.

Conceptual availability information:

```text
Availability Status
Unavailable Reason
```

Possible reasons may include:

```text
Deleted
Private
Temporarily Unavailable
Acquisition Failure
```

Exact implementation values may be refined later.

---

### 2.22.12 Deleted Posts

If a post is confirmed as deleted:

```text
Post
↓
Deleted
↓
Preserve Existing Engagement History
↓
Do Not Create False Observation
↓
End MVP Tracking
```

Historical observations must remain available for later analysis.

Deleting or losing access to the current post must not delete its historical records.

---

### 2.22.13 Private or Temporarily Unavailable Posts

If the post becomes private or temporarily inaccessible:

```text
Tracking Attempt
↓
Unable to Retrieve Current Engagement
↓
Record Availability / Failure Reason
↓
Do Not Create False Engagement Observation
```

The system must not convert unavailable engagement metrics into zero.

For example:

```text
Missing Likes ≠ 0 Likes
Missing Saves ≠ 0 Saves
Missing Comments ≠ 0 Comments
```

Whether temporarily unavailable posts should be retried in a later tracking cycle may be refined during Process / Decision Analysis.

---

### 2.22.14 Data Quality Status

Task B must distinguish the quality of acquired follow-up data.

Conceptual Data Quality states:

```text
Valid
Incomplete
Missing
Invalid
Unavailable
```

Data Quality Status answers:

> What is the quality of the data obtained during this observation?

This is different from Tracking Status, which answers:

> What stage of the tracking lifecycle is this post currently in?

The two must not be combined into one generic `Status` field.

---

### 2.22.15 Incomplete Engagement Data

If only part of the engagement data can be acquired, the missing value must not automatically be converted to zero.

Example:

```text
Likes = 1000
Saves = Missing
Comments Count = 300
```

must not automatically become:

```text
Engagement = 1300
```

because:

```text
Missing ≠ 0
```

The observation should be treated as incomplete.

Whether Engagement may be calculated from incomplete component data will be determined during Process / Decision Analysis.

---

### 2.22.16 Temporary Acquisition Failure

Temporary acquisition failures may include:

- timeout;
- temporary platform failure;
- temporary acquisition-channel failure;
- other recoverable access errors.

Conceptual handling:

```text
Temporary Failure
↓
Bounded Retry
↓
Still Failed
↓
Record Failure Reason
↓
No Valid Follow-up Observation
```

Retry rules and retry limits belong to later Process / Error Handling design.

Task B Input Analysis only establishes that temporary acquisition failure must be distinguishable from:

```text
Deleted
Private
Valid Empty
Incomplete Data
```

---

### 2.22.17 Tracking Attempt vs Engagement Observation

A Tracking Attempt and an Engagement Observation are different records.

A Tracking Attempt represents:

> The system attempted to track this post during this tracking run.

Conceptual fields:

```text
Post ID
Tracking Run ID
Attempted At
Result
Failure Reason
```

An Engagement Observation represents:

> Valid or usable engagement data was observed at a specific point in time.

Relationship:

```text
Tracking Attempt
↓
Successful Acquisition
↓
Engagement Observation
```

If acquisition fails:

```text
Tracking Attempt
↓
Failure Reason
↓
No False Engagement Observation
```

This distinction allows the system to know whether missing historical data means:

- tracking was never attempted; or
- tracking was attempted but failed.

---

### 2.22.18 MVP Tracking Completion

For the current MVP, Task B requires one follow-up tracking cycle after the minimum 7-day interval.

Conceptually:

```text
Candidate Post
↓
AI Basic Analysis
↓
Feishu Review
↓
Lawyer Keep
↓
Priority Post Pool
↓
Initial Observation
↓
Wait Minimum 7 Days
↓
Eligible for Follow-up
↓
Sunday Tracking Batch
↓
Follow-up Observation
↓
Compare Initial vs Follow-up Engagement
↓
MVP Tracking Completed
```

The business objective is to support later determination of:

> How the post's total engagement changed after the initial observation.

The exact definition of whether the growth is significant, stable or declining belongs to later Decision Analysis.

---

### 2.22.19 Current MVP Scope Boundary

Included in the current MVP:

- Lawyer Keep decision determines entry into Priority Post Pool.
- Engagement > 500 remains a supporting signal only.
- Minimum Tracking Interval = 7 days.
- Task B executes through the Sunday 10:00 scheduled batch.
- One follow-up tracking cycle is required.
- Initial and Follow-up Engagement Observations are both preserved.
- Historical observations are never overwritten.
- Duplicate observations within the same tracking run must be prevented.
- Deleted posts preserve historical records and end MVP tracking.
- Private or temporarily unavailable posts do not generate false observations.
- Missing engagement values must not be treated as zero.
- Tracking Attempt and Engagement Observation are treated as different concepts.

Not included in the current MVP:

- Long-term weekly tracking after the first follow-up observation.
- Conditional continued tracking based on growth performance.
- Advanced trend modeling.
- Exact technical implementation of Tracking Run ID.
- Final retry mechanism and retry limits.
- Automatic changes to Priority status based solely on later engagement thresholds.

---

### 2.22.20 Task B Input Design Principles

1. **Priority Is a Business Decision**
   - Priority comes from lawyer Keep decision.
   - Engagement thresholds are supporting signals.

2. **Same Post, Multiple Observations**
   - Post identity remains stable.
   - Engagement data is stored as time-based observations.

3. **Historical Observation Must Not Be Overwritten**
   - Current values do not replace historical values.

4. **7 Days Is the Minimum Tracking Interval**
   - Actual execution remains controlled by the Sunday schedule.

5. **Missing Is Not Zero**
   - Failed or incomplete acquisition must not create false engagement decline.

6. **Availability and Data Quality Are Different Dimensions**
   - A post's accessibility and the quality of acquired data must be represented separately.

7. **Tracking Status and Data Quality Status Are Different**
   - Lifecycle state must not be mixed with observation quality.

8. **Tracking Attempt Is Not the Same as Observation**
   - Failed execution must remain visible without generating false engagement data.

9. **Preserve History Even When the Source Disappears**
   - Deleted or inaccessible posts do not erase previously collected observations.

10. **Prevent Duplicate Observation Within the Same Tracking Run**
    - Workflow retry must not create false historical snapshots.

11. **MVP Scope Must Remain Controlled**
    - Long-term and advanced trend logic is deferred until later versions.