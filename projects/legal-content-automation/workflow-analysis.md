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