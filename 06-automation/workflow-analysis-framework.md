# Workflow Analysis Framework

## Purpose

This document provides a reusable framework for analyzing and designing AI / Automation workflows.

It is not tied to one specific project.

The framework can be applied to different business scenarios to answer:

> What business problem are we solving, how should the workflow operate, where should AI / automation / humans participate, and how can the system be implemented, evaluated and improved?

Core analysis sequence:

Business Problem
↓
Trigger
↓
Input
↓
Process
↓
Decision
↓
Action
↓
Output
↓
Technology Mapping
↓
Implementation
↓
Evaluation
↓
Iteration

Supporting cross-workflow concerns:

Data Contract
Human-in-the-loop
State & History
Error Handling
Idempotency
Traceability
Observability
Security
Cost
Maintainability
Scalability

---

# 1. Core Principle

The purpose of Workflow Analysis is not to automate every step.

The goal is to identify:

1. What problem actually exists?
2. Which parts should be automated?
3. Which parts require AI?
4. Which parts should remain deterministic?
5. Which decisions should remain human-controlled?
6. What data must flow between steps?
7. How should failures and uncertainty be handled?
8. What outputs create real business value?
9. How can the workflow be tested and improved?

A useful principle:

> Rule handles certainty.  
> AI handles semantic uncertainty.  
> Human handles high-value judgment.

Technology should follow business requirements.

Do not start with:

“What tool should I use?”

Start with:

“What problem and workflow am I designing?”

---

# 2. Business Problem Analysis

Before designing the workflow, define the business problem.

Recommended structure:

Business Problem
├── Current Workflow (As-Is)
├── Stakeholders / Users
├── Pain Points
├── Root Causes
├── Automation Opportunity
├── Automation Boundary
├── Product Goal
├── MVP Scope
└── Success Metrics

---

## 2.1 Current Workflow (As-Is)

Document how the work is currently performed.

Example:

User Request
↓
Manual Search
↓
Manual Collection
↓
Manual Analysis
↓
Human Decision
↓
Manual Output

Do not design the future system yet.

First understand the current system.

Questions:

- Who performs each step?
- What information is required?
- Which tools are currently used?
- Where are handoffs happening?
- Where does waiting occur?
- Where is information duplicated?
- Where does human judgment occur?

---

## 2.2 Stakeholders / Users

Identify:

- Primary User
- Secondary User
- Decision Maker
- Data Provider
- System Administrator
- External System / Platform

For each stakeholder, ask:

- What are they trying to achieve?
- What decisions do they make?
- What information do they need?
- What work should the system remove?
- What work should remain under their control?

---

## 2.3 Pain Points

Pain Points describe where the current workflow creates friction.

Common categories:

- Time Cost
- Repetitive Work
- Manual Search
- Manual Data Entry
- Information Overload
- Inconsistent Judgment
- Delayed Follow-up
- Data Fragmentation
- Poor Traceability
- High Maintenance Cost
- Platform / API Instability
- Human Attention Bottleneck

---

## 2.4 Root Cause

Do not stop at the visible symptom.

Example:

Pain Point:
Manual review takes too long.

Possible Root Causes:

- Too much irrelevant information
- No automatic filtering
- No prioritization
- No structured summary
- No persistent research history

Root Cause Analysis helps avoid automating the wrong problem.

---

## 2.5 Automation Opportunity

For every workflow step, ask:

Can this be:

- Removed?
- Automated?
- AI-assisted?
- Rule-based?
- Batched?
- Scheduled?
- Triggered by an event?
- Simplified?
- Deferred until needed?

---

## 2.6 Automation Boundary

Not every task should be automated.

A useful classification:

### Rule / System

Best for:

- deterministic logic
- validation
- scheduling
- filtering
- counting
- state checks
- threshold checks
- deduplication

### AI

Best for:

- semantic understanding
- classification
- summarization
- extraction
- similarity
- clustering
- contextual relevance
- generation

### Human

Best for:

- professional judgment
- business value judgment
- high-risk approval
- strategic prioritization
- final acceptance

---

## 2.7 Product Goal

Translate the Business Problem into a clear Product Goal.

Example structure:

> Reduce [manual work / delay / inconsistency] by creating a system that automatically performs [specific workflow], while preserving human control over [important decisions].

---

## 2.8 MVP Scope

Define:

### In Scope

What must exist for the first usable version?

### Out of Scope

What will intentionally not be built yet?

Important principle:

> MVP should prove the core value loop, not contain every possible feature.

---

## 2.9 Success Metrics

Success Metrics should connect to the original Business Problem.

Possible dimensions:

### Efficiency

- Time Saved
- Manual Steps Reduced
- Processing Time

### Quality

- Relevant Result Rate
- Approval Rate
- Error Rate
- AI Output Quality

### Business Value

- Useful Outputs Generated
- Conversion to Downstream Action
- User Adoption

### Reliability

- Workflow Success Rate
- Failure Recovery Rate
- Delivery Success Rate

Avoid vanity metrics that do not measure whether the workflow solves the original problem.

---

# 3. Trigger Analysis

Trigger answers:

> What causes the workflow to start?

Common Trigger Types:

### Schedule Trigger

Examples:

- Daily
- Weekly
- Monthly
- Every N hours

### Event Trigger

Examples:

- New Data
- New File
- Form Submission
- Webhook
- Human Decision

### Data Condition Trigger

Examples:

- Status changed
- Threshold reached
- Due date reached
- New eligible record exists

### Manual Trigger

Examples:

- User clicks Run
- Admin initiates reprocessing
- Manual test

---

## 3.1 Trigger Questions

For each workflow ask:

- What starts it?
- Is the trigger deterministic?
- Can it happen twice?
- Can it arrive late?
- Can it arrive out of order?
- Does it require current state?
- Does it create a new workflow run?
- Should duplicate triggers be ignored?

---

## 3.2 Trigger vs Schedule

Do not assume every workflow should be scheduled.

Example:

Daily Collection
→ Schedule

Human Approval Handler
→ Event / Webhook

Future Tracking
→ Due-state + Scheduled Check

The trigger should match the business event.

---

# 4. Input Analysis

Input answers:

> What information does the workflow require before processing can begin?

Input Analysis should include:

Input
├── Source
├── Field
├── Meaning
├── Data Type
├── Required / Optional
├── Nullable
├── Normalization
├── Validation
├── Freshness
├── History Requirement
└── Downstream Usage

---

## 4.1 Input Source

Possible sources:

- API
- Database
- User Input
- File
- Spreadsheet
- Previous Workflow
- AI Output
- Webhook
- External Platform

---

## 4.2 Data Type

Examples:

- String
- Integer
- Float
- Boolean
- Datetime
- Array
- Object
- Enum

Correct Data Types improve:

- validation
- storage
- comparison
- downstream processing

---

## 4.3 Required vs Optional

### Required

Workflow cannot correctly continue without it.

### Optional

Useful but not necessary.

Do not make every field Required.

Overly strict requirements create unnecessary workflow failures.

---

## 4.4 Empty vs Null

These should not automatically mean the same thing.

Example:

Empty String:
""

Null:
null

Empty Array:
[]

Possible meanings differ.

Define them explicitly in the Data Contract.

---

## 4.5 Normalization

Normalization converts raw data into a consistent internal format.

Examples:

Raw:
"  AI Automation "

Normalized:
"AI Automation"

Other examples:

- Datetime → common timezone
- Number String → Integer
- Platform-specific ID → String
- Missing optional field → null
- Hashtag String → Array

Recommended sequence:

Raw Input
↓
Normalization
↓
Validation
↓
Processing

---

## 4.6 Validation

Validation checks whether normalized data is usable.

Examples:

- Required field exists
- ID format valid
- Datetime parseable
- Array structure valid
- Enum value allowed
- Numeric field non-negative

Validation should produce explicit outcomes.

Avoid silent data corruption.

---

# 5. Data Contract

Data Contract defines how shared data objects are understood across workflows.

Purpose:

> Ensure upstream Output can reliably become downstream Input.

A Data Contract may define:

| Field | Meaning | Type | Required | Nullable | Source | Validation | History |
|---|---|---|---|---|---|---|---|

Questions:

- Does every workflow use the same field meaning?
- Is the same ID represented consistently?
- Are timestamps using the same timezone?
- Does null mean the same thing?
- Can downstream workflows distinguish missing data from valid empty results?
- Is historical information required?

---

## 5.1 Shared Data Objects

Identify objects used across multiple workflows.

Examples:

- User
- Keyword
- Post
- Search Hit
- Observation
- Analysis
- Review Item
- Decision
- Request
- Research Subject
- Case
- Candidate
- Output

These objects become candidates for the future Data Model.

---

## 5.2 Entity vs Relationship

Do not confuse an object with the relationship that discovered or connects it.

Example:

Keyword A
↓
Post 001

Keyword B
↓
Post 001

Post 001 should normally remain one entity.

But both relationships may need to be preserved.

Principle:

> Deduplicate the entity; preserve meaningful relationships.

---

## 5.3 State Data vs Event Data

### State Data

Represents current condition.

Example:

Current Status = Active

### Event Data

Represents something that happened.

Example:

Approval Event at 2026-01-01

Many systems require both.

Current State answers:

> What is true now?

Event History answers:

> How did we get here?

---

# 6. Process Analysis

Process answers:

> What happens after valid Input enters the workflow?

Recommended framework:

Process
├── Boundary
├── Sequence
├── Batch / Loop
├── Transformation
├── Persistence
├── State Change
├── External Call
├── Human Interaction
├── Error Path
├── Retry
├── Idempotency
└── Completion

---

## 6.1 Process Boundary

Define:

Start:
What event / state begins the workflow?

End:
What means the workflow has completed?

Avoid workflows with unclear boundaries.

---

## 6.2 Sequence

Document the logical order.

Example:

Load Input
↓
Normalize
↓
Validate
↓
Process
↓
Persist
↓
Produce Output

Do not jump directly to tool-specific nodes.

---

## 6.3 Batch and Loop

Ask:

- One object or many?
- One request or multiple?
- Sequential or parallel?
- Is there a maximum batch size?
- Can one item fail without failing the whole batch?

---

## 6.4 Transformation

Identify how data changes.

Example:

Raw Content
↓
Normalized Content
↓
Structured AI Output
↓
Business Object

---

## 6.5 Persistence

Important business data should not exist only inside temporary workflow memory.

Recommended:

Process
↓
Persist
↓
Downstream Processing

Principle:

> Persist important state before relying on downstream execution.

---

## 6.6 Progressive Enrichment

Do not collect or process expensive data before it is needed.

Example:

Basic Data
↓
Candidate Selection
↓
Human / System Qualification
↓
Deep Data Collection
↓
Expensive Analysis

Principle:

> Spend expensive processing only when business value justifies it.

---

# 7. Decision Analysis

Decision answers:

> Why does the workflow choose one path instead of another?

Three common layers:

Rule-based Decision
AI-assisted Decision
Human Decision

---

## 7.1 Rule-based Decision

Use when:

- logic is deterministic
- conditions are explicit
- ambiguity is low

Examples:

- Required field exists?
- Due date reached?
- Duplicate exists?
- Threshold reached?
- Schema valid?

---

## 7.2 AI-assisted Decision

Use when:

- meaning must be interpreted
- similarity matters
- classification is contextual
- rules would become brittle

Examples:

- semantic relevance
- topic classification
- clustering
- similarity
- contextual matching

---

## 7.3 Human Decision

Use when:

- professional judgment matters
- business strategy matters
- risk is high
- final approval should remain human-controlled

---

## 7.4 Signal vs Decision

A Signal is evidence.

A Decision determines workflow behavior.

Example:

High Engagement
=
Signal

Worth Further Research
=
Decision

Do not automatically convert every signal into a business decision.

---

## 7.5 Eligibility vs Selection

Eligibility:

> Is the object allowed to enter the next workflow?

Selection:

> Should it actually enter?

Example:

Eligible for Deep Analysis
≠
Automatically Deep Analyze

This distinction prevents hidden business logic.

---

## 7.6 Recommendation vs Authority

A system or AI may recommend:

Promote
Reduce
Approve
Reject
Retire

But ask:

> Does the recommendation itself have authority to change production state?

For high-value decisions:

Recommendation
↓
Human Review
↓
Approved State Change

---

## 7.7 Re-evaluation

Decisions may change when new evidence appears.

Example:

Initial Decision:
No Deep Analysis

Later:
New Evidence

Then:
Re-evaluate

Principle:

> A previous decision should not automatically become a permanent decision when the underlying evidence can change.

---

## 7.8 Decision History

Store important decisions as events.

Possible fields:

- Decision Type
- Decision Value
- Decision Maker
- Decision Time
- Evidence Reference
- Previous Decision
- Reason / Note

Do not overwrite meaningful decision history.

---

# 8. Human-in-the-loop Design

Human-in-the-loop should be designed intentionally.

Do not simply insert:

“Human checks here.”

Define:

- What does the human see?
- What information supports the decision?
- What choices are available?
- Is approval mandatory?
- What happens if no decision is made?
- Can the decision later change?
- How is the decision recorded?
- What downstream action does it trigger?

---

## 8.1 Asynchronous Human Review

Avoid keeping a workflow alive while waiting hours or days for human input.

Better pattern:

Workflow
↓
Persist Review Item
↓
Deliver to Human
↓
Workflow Completes

Later:

Human Decision Event
↓
Persist Decision
↓
Evaluate State
↓
Trigger Downstream Workflow

---

## 8.2 Pending ≠ Reject

No response should not automatically mean rejection.

Possible states:

Pending
Approved
Rejected

This distinction is important for Human-in-the-loop systems.

---

# 9. Action Analysis

Action answers:

> Once a decision is made, what should the system actually do?

Common Action Types:

### CREATE

Create a new business object.

### UPDATE

Update current state.

### APPEND

Add historical evidence or event.

### LINK

Create relationship between objects.

### DELIVER

Send information to a human or external system.

### TRIGGER

Start another workflow.

---

## 9.1 Decision → Action Mapping

For every important Decision, define its Action.

Example:

Decision:
Track = Yes

Action:
Create Tracking Request

Example:

Decision:
Approve Candidate

Action:
Update State
+
Trigger Downstream Processing

This prevents decisions from existing without operational consequences.

---

# 10. Output Analysis

Output answers:

> What does the workflow produce?

Output should be analyzed from multiple perspectives.

---

## 10.1 Business Output

Useful result for the business.

Examples:

- Candidate List
- Research Result
- Recommendation
- Approved Asset
- Report

---

## 10.2 Data Output

Reusable structured data for downstream workflows.

Examples:

- Structured Object
- Observation
- Relationship
- Decision
- Analysis Result

---

## 10.3 Human-facing Output

What the user actually sees.

Examples:

- Dashboard
- Review Card
- Daily Report
- Weekly Package
- Approval Request

---

## 10.4 Operational Output

Information required to operate the system.

Examples:

- Workflow Status
- Error
- Retry Result
- Delivery Status
- API Failure
- AI Validation Failure

---

## 10.5 Output Contract

For every important output define:

- Output Name
- Producer
- Consumer
- Schema
- Required Fields
- Optional Fields
- Empty Result Meaning
- Failure Meaning

---

## 10.6 Valid Empty Result

A workflow can successfully produce:

No Result

Examples:

- No matching record
- No eligible item
- No useful candidate
- No relevant case

This may be:

Valid Business Outcome

not:

Technical Failure

---

# 11. Error Handling

A real workflow must define more than the Happy Path.

Useful error categories:

### Technical Error

Examples:

- API Timeout
- Authentication Failure
- Database Failure

### Data Error

Examples:

- Missing Required Field
- Invalid Datetime
- Invalid JSON
- Schema Mismatch

### Business Condition

Examples:

- No Eligible Item
- No Relevant Result
- Resource Unavailable

These categories should not be handled identically.

---

## 11.1 Retry

Retry is appropriate for some temporary failures.

Examples:

- Timeout
- Rate Limit
- Temporary Network Error

Retry is usually inappropriate for:

- Invalid Input
- Permanent Missing Resource
- Broken Business Rule

Define:

- Retry Limit
- Retry Delay
- Final Failure State
- Alert Condition

---

## 11.2 Partial Success

Batch workflows may produce:

Success
Partial Success
Failure

Example:

10 items processed:

8 Success
2 Failed

The workflow should preserve successful results and record failed items.

---

# 12. Idempotency

Ask:

> If the same event is processed twice, will business data remain correct?

Duplicate execution can happen because of:

- Retry
- Duplicate Webhook
- Timeout
- Manual Rerun
- Scheduler Overlap

Potential problems:

- Duplicate Entity
- Duplicate Decision
- Duplicate Request
- Duplicate Output

Design idempotency around business identifiers and state.

---

# 13. State Management

Long-running or multi-workflow systems need explicit State.

Examples:

- Pending Review
- Approved
- Rejected
- Tracking Scheduled
- Tracking Complete
- Analysis Requested
- Analysis Complete

Do not rely on:

“Which workflow node ran last?”

as the only representation of business state.

---

# 14. Traceability

Important outputs should be traceable back to their evidence.

Example:

Final Candidate
↓
Analysis
↓
Source Object
↓
Collection Event
↓
Original Input

If additional evidence is used:

Final Candidate
↓
Evidence Links
├── Comment
├── Observation
├── Case
└── Human Decision

Traceability supports:

- Debugging
- Evaluation
- Human Review
- Auditability
- Future Productization

---

# 15. AI Workflow Design

When AI participates, define:

Input
↓
Prompt / Instruction
↓
Model
↓
Structured Output
↓
Validation
↓
Business Use

Do not treat:

“Send it to AI”

as a complete workflow step.

---

## 15.1 Structured Output

Prefer structured output when AI results feed downstream automation.

Example:

{
  "topic": "...",
  "summary": "...",
  "relevance": "...",
  "evidence": []
}

Benefits:

- validation
- database storage
- branching
- evaluation
- retry
- debugging

---

## 15.2 AI Provenance

Where useful, preserve:

- Model
- Prompt Version
- Input Reference
- Output
- Generated At
- Validation Result

This helps future evaluation and debugging.

---

## 15.3 AI Failure Handling

AI failure should not automatically destroy valid upstream data.

Pattern:

Valid Business Object
↓
AI Failure
↓
Preserve Object
↓
Record Failure
↓
Retry / Manual Review / Continue with Reduced Output

---

# 16. Technology Mapping

Only after Business Workflow is sufficiently understood should technology be selected.

Map requirements to capabilities.

Example:

| Requirement | Capability |
|---|---|
| Scheduled execution | Scheduler |
| External data | API / HTTP |
| Structured storage | Database |
| Semantic understanding | LLM |
| Human approval | UI / Messaging / Webhook |
| Event continuation | Webhook / Queue / Workflow Engine |

Then select actual tools.

Principle:

> Requirement → Capability → Technology

not:

> Technology → Find something to use it for

---

# 17. Technical Foundations

Common technical concepts required for AI Automation:

### API

How systems communicate.

### HTTP

Request / response communication.

### JSON

Structured data exchange.

### Webhook

Event-driven communication.

### Database

Persistent system state.

### SQL

Query and manage relational data.

### Python

Useful for:

- data processing
- API testing
- migration
- evaluation
- custom logic

Learn them through actual implementation whenever possible.

---

# 18. Workflow Architecture

Avoid one giant workflow when the system contains:

- long waits
- human approval
- retries
- independent schedules
- multiple downstream branches

Prefer:

Independent Workflows
+
Persistent State
+
Events
+
Shared Data Contracts

Example:

Collection Workflow
↓
Database

Analysis Workflow
↓
Database

Human Decision
↓
Event

Downstream Workflow
↓
Database

---

# 19. System of Record

Define:

> Where does authoritative business data live?

Do not accidentally make:

Messaging Tool
Spreadsheet View
Temporary Workflow Memory

the system of record unless intentionally designed that way.

A persistent database often becomes the System of Record for complex automation.

---

# 20. User Interaction Layer

Separate:

System Memory

from:

Human Workspace

Human Workspace may provide:

- Review
- Approval
- Reporting
- Search
- Visibility

But authoritative state may live elsewhere.

This separation improves maintainability and traceability.

---

# 21. Cloud / Unattended Execution

For automation expected to run without the user's computer:

require:

- Cloud-accessible Workflow Runtime
- Persistent Database
- External API Access
- Scheduler
- Secret Management
- Failure Handling

Requirement:

Local Computer OFF
↓
Automation Still Runs

This should be treated as a product / architecture requirement, not an afterthought.

---

# 22. Security

Before production use, review:

- API Key Storage
- Authentication
- Authorization
- Sensitive Data
- Personal Information
- Logging
- Data Retention
- External Data Transfer
- Least Privilege

Never hard-code secrets in:

- source code
- public repository
- screenshots
- documentation

---

# 23. Observability

Automation should be observable.

Useful information:

- Run ID
- Start Time
- End Time
- Status
- Items Processed
- Success Count
- Failure Count
- Error Type
- Retry Count
- External API Status
- AI Validation Status
- Delivery Status

Goal:

> When something goes wrong, can we understand what happened?

---

# 24. Cost

AI Automation can create costs through:

- API Requests
- LLM Tokens
- Database
- Cloud Runtime
- Third-party Services

Use:

Progressive Enrichment

to avoid expensive processing on low-value data.

Measure cost where relevant.

---

# 25. Evaluation

A workflow is not finished when it runs successfully.

Evaluation asks:

> Does it actually produce useful and reliable outcomes?

---

## 25.1 Workflow Evaluation

Measure:

- Workflow Success Rate
- Partial Failure Rate
- Retry Rate
- Processing Time
- Delivery Success

---

## 25.2 AI Evaluation

Possible dimensions:

- Relevance
- Classification Accuracy
- Extraction Quality
- Structured Output Validity
- Hallucination
- Consistency
- Human Approval Rate

---

## 25.3 Business Evaluation

Measure against original Success Metrics.

Examples:

- Manual Time Reduced
- Useful Result Rate
- Human Review Efficiency
- Downstream Conversion
- Business Asset Created

---

# 26. Feedback Loop

A mature workflow should learn from outcomes.

Generic structure:

Input
↓
Processing
↓
Human / Business Outcome
↓
Performance Evidence
↓
Evaluation
↓
Adjustment
↓
Future Input / Rules / Prompt / Configuration

Feedback can improve:

- Search Strategy
- Rules
- Prompt
- AI Classification
- Thresholds
- User Experience
- Workflow Configuration

---

# 27. Product Design Integration

Workflow Analysis can directly support Product Management.

Recommended Product Portfolio outputs:

1. Business Problem
2. Stakeholders
3. As-Is Workflow
4. Pain Points
5. Product Goal
6. MVP Scope
7. Success Metrics
8. User Stories
9. Acceptance Criteria
10. Workflow Diagram
11. PRD
12. Prototype if needed
13. System Architecture
14. Technology Mapping
15. Implementation
16. Test Cases
17. Evaluation
18. Iteration Log
19. Final Case Study

---

# 28. User Story

Recommended format:

> As a [user], I want [capability], so that [business value].

Example:

> As a reviewer, I want to see summarized candidate items so that I can make decisions without manually reading every raw source.

User Stories should describe user value, not implementation details.

---

# 29. Acceptance Criteria

Acceptance Criteria define:

> What must be true for the requirement to be considered successfully implemented?

Good Acceptance Criteria should be:

- Observable
- Testable
- Specific
- Business-relevant

Example:

Given valid input,
when the workflow completes,
then the normalized record is persisted and can be retrieved using its business identifier.

---

# 30. Prototype

Prototype is useful when:

- Human Interaction is important
- Review flow needs validation
- User Interface affects decision quality
- Product behavior is unclear

Not every backend automation requires a complex prototype.

Prototype should serve a real validation purpose.

---

# 31. Implementation Strategy

Prefer Vertical Slices.

Instead of:

Build every database table
↓
Build every API
↓
Build every AI feature
↓
Finally test end-to-end

Prefer:

Small Business Value Loop
↓
Real Input
↓
Real Processing
↓
Real Persistence
↓
Real Output
↓
Test
↓
Expand

This reduces implementation risk.

---

# 32. Build-phase Learning

For project-driven learning:

Do not:

Learn every tool first
↓
Then search for a use case

Prefer:

Project Requirement
↓
Technical Problem
↓
Learn Required Concept
↓
Implement
↓
Test
↓
Debug
↓
Document

Examples:

Need external data
→ Learn API + HTTP + JSON

Need persistent state
→ Learn Database + SQL

Need human response
→ Learn Webhook

Need semantic processing
→ Learn LLM + Structured Output

Need retrieval
→ Learn Search / RAG when the real retrieval problem appears

---

# 33. Technology Boundary

Do not introduce technology simply because it is popular.

Examples:

Agent
RAG
Vector Database
Fine-tuning
Multi-Agent
Frameworks

should only be introduced when the workflow has a real requirement.

Questions:

- What problem does this technology solve?
- Can simpler deterministic logic solve it?
- Does it improve measurable value?
- What complexity does it add?

---

# 34. Design Review Checklist

Before implementation, review:

## Business

- Is the problem clearly defined?
- Is the user clear?
- Is the MVP scope controlled?
- Are Success Metrics meaningful?

## Trigger

- Does every workflow have a clear start condition?

## Input

- Are required inputs defined?
- Are normalization and validation clear?

## Data Contract

- Can workflows exchange data consistently?

## Process

- Is the Happy Path clear?
- Are batch and partial-success cases handled?

## Decision

- Is each decision owned by Rule, AI or Human?

## Action

- Does every important decision create a defined action?

## Output

- Are business, data, human and operational outputs defined?

## State

- Can the system resume after delays and human decisions?

## Error

- Are technical errors distinguished from valid empty results?

## Idempotency

- Can retries happen safely?

## Traceability

- Can important outputs be traced back to source evidence?

## AI

- Are outputs structured and validated?

## Technology

- Does each technology solve a real requirement?

## Security

- Are credentials and sensitive data protected?

## Cloud

- Can the workflow run without the user's local computer if required?

## Evaluation

- Do we know how success will be measured?

---

# 35. Final Framework

The complete reusable framework:

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
↓
Action
↓
Output
↓
Technology Mapping
↓
Implementation
↓
Evaluation
↓
Iteration

Across every stage continuously consider:

Human-in-the-loop
State
History
Error Handling
Retry
Partial Success
Idempotency
Traceability
Security
Observability
Cost
Maintainability
Scalability

---

# Core Mindset

The goal of AI Automation is not:

> Use as much AI as possible.

The goal is:

> Design a reliable business system in which deterministic automation, AI capabilities and human judgment each perform the work they are best suited for.

And the preferred learning path is:

Real Business Problem
↓
Workflow Design
↓
Product Requirement
↓
Technology Selection
↓
Implementation
↓
Testing
↓
Evaluation
↓
Iteration

> Project-driven Learning.