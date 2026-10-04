# AI SOFTWARE FACTORY — FULL REQUIREMENTS V0.7

**Status:** Requirements Baseline Candidate  
**Purpose:** Comprehensive system requirements for formal BA, Architecture, Security and Operational review.

This document contains the complete V0.6 requirements baseline followed by the authoritative V0.7 platform-governance update. Where V0.7 explicitly conflicts with an older rule, V0.7 takes precedence.

# AI SOFTWARE FACTORY — FULL REQUIREMENTS V0.6

**Document status:** Full V0.6 requirements package.

This document contains the complete V0.5 requirements baseline plus the authoritative V0.6 lifecycle update. Where V0.6 explicitly conflicts with an older lifecycle rule, V0.6 takes precedence.

# AI SOFTWARE FACTORY — FULL REQUIREMENTS V0.5

**Document status:** Full V0.5 requirements package.

This document contains the complete V0.4 baseline plus the authoritative V0.5 architecture update. If an older V0.4 statement conflicts with an explicit V0.5 rule, the V0.5 rule takes precedence.

# AI Software Factory — System Requirements Specification

**Document:** AI-SOFTWARE-FACTORY-REQUIREMENTS-V0.2.md  
**Version:** 0.2  
**Status:** Requirements Baseline  
**Language:** Vietnamese

---

# 1. Mục tiêu

Xây dựng một **AI Software Factory** có khả năng nhận một ý tưởng phần mềm từ người dùng và tổ chức, thực hiện, kiểm tra, phát hành và triển khai một dự án phần mềm theo quy trình giống một đội ngũ phát triển phần mềm thực tế.

Hệ thống không chỉ là một nhóm Multi-Agent gọi LLM.

Hệ thống phải có:

- Requirement management.
- Business analysis.
- UI/UX design.
- System architecture.
- Detailed design.
- Architecture review.
- Task planning.
- Dependency management.
- Task scheduling.
- Batch execution.
- Developer lifecycle.
- Task state tracking.
- Project monitoring.
- Context management.
- Integration.
- QA.
- Code review.
- Security review.
- Regression testing.
- Release.
- Deployment.
- Knowledge management.
- Architecture Decision Records (ADR).
- Token/cost monitoring.
- Human-in-the-loop.

Mục tiêu cuối cùng:

> **Biến một ý tưởng của con người thành một sản phẩm phần mềm có thể build, test, review và deploy thông qua một hệ thống AI Software Company có kiểm soát.**

---

# 2. Nguyên tắc cốt lõi

## 2.1 Agent không được đoán khi requirement chưa rõ

Nếu thông tin chưa đủ để đưa ra quyết định đúng, Agent phải:

```text
Detect ambiguity
      ↓
Create question
      ↓
WAITING_FOR_PO
      ↓
PO answers
      ↓
Continue
```

Không được tự suy đoán những quyết định ảnh hưởng tới nghiệp vụ hoặc kiến trúc.

## 2.2 Markdown-driven

Các artifact chính của project phải ưu tiên Markdown.

Markdown:

- Con người đọc được.
- Agent đọc được.
- Git diff dễ theo dõi.
- Có version history.
- Có thể chỉnh sửa thủ công.
- Dễ đưa vào context của LLM.
- Có thể làm knowledge base của project.

JSON chỉ được dùng khi cần dữ liệu machine-readable cho runtime, API, indexing hoặc state transport.

## 2.3 Git là source of truth cho code

Source code, test, migration và configuration phải được quản lý bằng Git.

## 2.4 Markdown là source of truth cho project knowledge

Markdown là source of truth cho:

- Requirement.
- Business analysis.
- UI/UX.
- Architecture.
- Detailed design.
- Tasks.
- Plans.
- State.
- Summary.
- Questions.
- Review.
- QA.
- Security.
- ADR.

Database có thể dùng làm index, runtime state, orchestration state và metrics nhưng không thay thế artifact Markdown chính.

## 2.5 Task Manager là nguồn điều phối

Agent không tự ý chạy task nếu task chưa READY.

Task Manager quyết định:

- Task nào READY.
- Task nào BLOCKED.
- Task nào được assign.
- Task nào được batch.
- Task nào được unlock.

## 2.6 Context tối thiểu nhưng đủ

Không gửi toàn bộ project vào mỗi LLM call.

Context Manager phải chọn:

- Requirement liên quan.
- Design liên quan.
- Dependency summaries.
- Relevant source code.
- Relevant tests.
- Relevant decisions.

Mục tiêu:

- Giảm token.
- Giảm chi phí.
- Giảm latency.
- Giảm hallucination.

---

# 3. Quy trình end-to-end

Quy trình chuẩn:

```text
USER IDEA
    |
    v
REQUIREMENT
    |
    v
REQUIREMENT VALIDATION
    |
    v
PO APPROVAL
    |
    v
BUSINESS ANALYSIS
    |
    v
UI/UX DESIGN
    |
    v
SYSTEM DESIGN
    |
    v
DETAILED DESIGN
    |
    v
ARCHITECTURE REVIEW
    |
    v
TASK PLANNING
    |
    v
TASK ESTIMATION
    |
    v
DEPENDENCY GRAPH
    |
    v
TASK SCHEDULING
    |
    v
BATCH PLANNING
    |
    v
DEVELOPER EXECUTION
    |
    v
TASK STATE + SUMMARY
    |
    v
CODE REVIEW
    |
    v
INTEGRATION
    |
    v
INTEGRATION TEST
    |
    v
QA
    |
    +-------- FAIL --------+
    |                      |
    |                      v
    |                  DEVELOPER
    |                      |
    |                      v
    |                 REGRESSION
    |                      |
    +----------------------+
    |
    v
SECURITY REVIEW
    |
    v
RELEASE
    |
    v
DEPLOY
    |
    v
HEALTH CHECK
    |
    v
POST-DEPLOY MONITORING
    |
    v
PROJECT COMPLETE
```

---

# 4. Giai đoạn 1 — User Idea

User cung cấp ý tưởng ban đầu.

Ví dụ:

> Tôi muốn xây dựng hệ thống quản lý phòng khám.

Input có thể rất ngắn. User không cần biết cách viết Software Requirement.

---

# 5. Giai đoạn 2 — Requirement Agent

Requirement Agent chuyển ý tưởng thành:

```text
requirements/requirement.md
```

Nội dung:

- Problem statement.
- Product goal.
- Target users.
- Scope.
- Main features.
- Actors.
- Initial business requirements.
- Initial acceptance criteria.
- Constraints.
- Assumptions.
- Open questions.

Requirement Agent không được tự tạo business rule chưa có cơ sở.

---

# 6. Giai đoạn 3 — Requirement Validation

Requirement Validator kiểm tra:

- Thiếu actor.
- Thiếu chức năng.
- Mâu thuẫn requirement.
- Requirement chưa rõ.
- Thiếu acceptance criteria.
- Scope bất hợp lý.
- Assumption chưa được xác nhận.
- Requirement trùng lặp.

Nếu không đạt:

```text
Requirement Validation
       |
       v
Questions
       |
       v
PO
       |
       v
Requirement Update
       |
       v
Validation Again
```

Nếu đạt:

```text
VALID
  |
  v
PO APPROVAL
```

---

# 7. Giai đoạn 4 — PO Approval

PO có thể:

- Approve.
- Request changes.
- Reject.
- Ask for clarification.

Không được chuyển sang BA nếu requirement chưa được approve.

---

# 8. Giai đoạn 5 — Business Analysis

BA Agent đọc requirement đã approved.

Tạo:

```text
analysis/business-analysis.md
```

Có thể tạo thêm:

```text
analysis/use-cases.md
analysis/business-rules.md
analysis/workflows.md
```

BA xác định:

- Actors.
- Use cases.
- Business rules.
- Workflow.
- Exceptions.
- Validation.
- Acceptance criteria.
- Business dependencies.

Nếu phát hiện requirement chưa rõ, BA phải hỏi PO.

---

# 9. Giai đoạn 6 — UI/UX Design

UI/UX Agent đọc:

- Requirement.
- Business analysis.
- Use cases.

Tạo:

```text
design/ui-ux-design.md
```

Có thể bao gồm:

- User flow.
- Screen list.
- Navigation.
- Form.
- Validation.
- Empty state.
- Loading state.
- Error state.
- Permission state.
- Responsive behavior.

---

# 10. Giai đoạn 7 — System Design

System Design Agent tạo:

```text
design/system-design.md
```

Bao gồm:

- Architecture.
- Components.
- Services.
- Communication.
- External systems.
- Authentication.
- Authorization.
- Data flow.
- Deployment architecture.
- Technology decisions.

---

# 11. Giai đoạn 8 — Detailed Design

Detailed Design Agent tạo:

```text
design/detailed-design.md
```

Có thể bao gồm:

- Domain model.
- Database design.
- API design.
- Class design.
- Sequence diagrams.
- Validation.
- Error handling.
- Transaction boundary.
- Event design.
- Cache strategy.
- Security details.

Có thể tách:

```text
design/database-design.md
design/api-design.md
design/domain-design.md
design/security-design.md
```

---

# 12. Giai đoạn 9 — Architecture Review

Architecture Review Agent kiểm tra:

- Requirement compliance.
- Architecture consistency.
- Scalability.
- Security.
- Maintainability.
- Dependency.
- Technology choices.
- Data consistency.
- Failure handling.
- Deployment feasibility.

Output:

```text
reviews/architecture-review.md
```

Nếu fail:

```text
Architecture Review
       |
       v
System Design / Detailed Design
       |
       v
Architecture Review Again
```

Chỉ khi PASS mới được tạo task chính thức.

---

# 13. Giai đoạn 10 — Task Planning

Task Planner đọc toàn bộ design đã approved và phân rã thành task.

Task không mô tả implementation chi tiết.

Task mô tả:

- Cần làm gì.
- Tại sao.
- Acceptance criteria.
- Dependency.
- Output mong đợi.
- Capability cần thiết.

Ví dụ:

```markdown
# TASK-003 — Create Login API

## Objective

Implement login API.

## Type

Backend

## Priority

HIGH

## Dependencies

- TASK-001
- TASK-002

## Independent

No

## Parallelizable

No

## Acceptance Criteria

- Valid credentials return JWT.
- Invalid credentials return HTTP 401.
- JWT contains user identity and roles.

## Required Capability

Backend Developer
```

---

# 14. Giai đoạn 11 — Task Estimation

Mỗi task nên có estimation:

```text
Estimated effort: 4h
Complexity: MEDIUM
Risk: LOW
```

Estimation là thông tin phục vụ scheduling, không phải cam kết thời gian tuyệt đối.

Mục đích:

- Scheduling.
- Capacity planning.
- Batch planning.
- Progress monitoring.
- Detect abnormal tasks.

---

# 15. Giai đoạn 12 — Dependency Graph

Task Planner tạo DAG.

Ví dụ:

```text
TASK-001 ─────┐
              ├──> TASK-003 ───> TASK-005
TASK-002 ─────┘

TASK-004 ───────────────────────> TASK-005
```

Task Manager phải biết:

```text
TASK-001 → blocks TASK-003
TASK-002 → blocks TASK-003
TASK-003 → blocks TASK-005
TASK-004 → blocks TASK-005
```

---

# 16. Giai đoạn 13 — Task Scheduling

Task Manager tìm task READY và quyết định:

- Agent nào nhận.
- Có thể chạy parallel không.
- Có thể batch không.
- Priority.
- Agent capacity.
- Dependency.
- Risk.

Task Manager không viết code.

---

# 17. Giai đoạn 14 — Batch Planning

Task độc lập có thể được gom thành batch.

Ví dụ:

```text
BATCH-001

TASK-101 User Entity
TASK-102 Role Entity
TASK-103 User Repository
TASK-104 Role Repository
```

Nếu phù hợp, một Developer Agent có thể xử lý nhiều task trong một LLM execution context.

Mục tiêu:

```text
Less LLM calls
Less repeated context
Less input tokens
Less output overhead
Lower latency
Lower cost
```

Không batch task nếu dependency hoặc coupling khiến batch làm sai kết quả.

---

# 18. Giai đoạn 15 — Developer Lifecycle

Developer Agent phải thực hiện:

```text
TASK READY
    |
    v
READ DOCUMENTS
    |
    v
UNDERSTAND
    |
    +---- UNCLEAR ----> ASK PO / BA
    |                       |
    |                       v
    |                 WAITING_FOR_PO
    |                       |
    |                       v
    |                 RECEIVE ANSWER
    |                       |
    +-----------------------+
    |
    v
IMPLEMENTATION PLAN
    |
    v
CODE
    |
    v
TEST
    |
    v
UPDATE STATE
    |
    v
CREATE SUMMARY
    |
    v
TASK COMPLETED
```

---

# 19. Developer đọc context

Developer phải đọc những tài liệu cần thiết:

```text
requirement
business analysis
UI/UX
system design
detailed design
task
dependency summaries
relevant ADR
relevant source code
relevant tests
```

Context Manager quyết định chính xác phần nào cần đưa vào prompt.

---

# 20. Developer hỏi PO/BA

Nếu không rõ:

```text
tasks/TASK-xxx/questions.md
```

Ví dụ:

```markdown
# TASK-003 Question

## Question

Login dùng username, email hay cả hai?

## Reason

Quyết định ảnh hưởng đến:

- API.
- Database query.
- Validation.
- UI.

## Status

WAITING_FOR_PO
```

Không được tự suy đoán quyết định nghiệp vụ quan trọng.

---

# 21. Developer Implementation Plan

Sau khi hiểu task:

```text
tasks/TASK-xxx/implementation-plan.md
```

Developer phải xác định:

- Approach.
- Files to create.
- Files to modify.
- Components.
- API changes.
- Database changes.
- Tests.
- Risks.
- Technical decisions.

Implementation plan có thể được cập nhật nếu phát sinh thay đổi lớn.

---

# 22. Developer Coding

Developer thực hiện code.

Trong quá trình code phải:

- Đọc code hiện tại.
- Tôn trọng architecture.
- Tôn trọng ADR.
- Tạo/sửa source code.
- Tạo/sửa tests.
- Chạy test.
- Sửa lỗi.
- Cập nhật state.

---

# 23. Task State

Mỗi task có:

```text
tasks/TASK-xxx/state.md
```

Ví dụ:

```markdown
# TASK-003 State

## Status

IN_PROGRESS

## Agent

backend-developer

## Progress

70%

## Current Step

Implementing AuthService.

## Completed

- [x] AuthController
- [x] Login DTO
- [x] Password validation

## Remaining

- [ ] JWT generation
- [ ] Unit tests

## Files Changed

- AuthController.kt
- LoginRequest.kt

## Tests

NOT_RUN

## Blockers

None

## Last Update

2026-10-01 16:40
```

---

# 24. Event-driven Task State

Agent phát sinh event:

```text
TASK_STARTED
FILE_CREATED
FILE_MODIFIED
TEST_STARTED
TEST_FAILED
TEST_PASSED
QUESTION_CREATED
BLOCKED
IMPLEMENTATION_COMPLETED
TASK_COMPLETED
```

State Manager xử lý event:

```text
Agent
  |
  v
Event
  |
  v
State Manager
  |
  +-- state.md
  +-- log.md
  +-- Task Graph
  +-- Project Monitor
```

---

# 25. Task Summary

Sau khi implementation hoàn thành:

```text
tasks/TASK-xxx/summary.md
```

Summary phải giúp Agent khác tiếp tục công việc mà không cần đọc toàn bộ lịch sử.

Bao gồm:

- Objective.
- Implementation.
- Files created.
- Files modified.
- APIs.
- Database changes.
- Tests.
- Important decisions.
- Known limitations.
- Notes for other agents.
- Dependencies unlocked.

Summary là **living artifact**.

---

# 26. Task Summary có thể được Agent khác cập nhật

Ví dụ:

```text
Backend Agent
     |
     v
summary.md
     |
     v
QA Agent
     |
     v
summary.md update
     |
     v
Security Agent
     |
     v
summary.md update
```

Mọi thay đổi quan trọng phải có Change History.

Nếu nhiều Agent cùng sửa artifact phải sử dụng version/lock/merge mechanism.

---

# 27. Task Completion

Task chỉ DONE khi:

- Implementation hoàn tất.
- Test phù hợp đã chạy.
- State được cập nhật.
- Summary được tạo.
- Không còn blocker.
- Acceptance criteria đạt.

Task Manager sau đó kiểm tra dependency.

Nếu task DONE:

```text
BLOCKED dependent task
        |
        v
Recalculate dependencies
        |
        v
READY nếu đủ dependency
```

---

# 28. Code Review

Code Review Agent kiểm tra:

- Requirement.
- Architecture.
- Code quality.
- Maintainability.
- Error handling.
- Test.
- Security.
- Unnecessary changes.

Nếu fail:

```text
REVIEW_FAILED
      |
      v
Developer
      |
      v
Review Again
```

---

# 29. Integration

Đây là bước bắt buộc sau khi các task song song hoàn thành.

Ví dụ:

```text
Backend DONE
Frontend DONE
Database DONE
       |
       v
Integration
```

Integration kiểm tra:

- API ↔ Frontend.
- Service ↔ Database.
- Service ↔ Service.
- Authentication.
- Authorization.
- Event/message.
- Configuration.

---

# 30. Integration Test

Sau integration:

```text
Integration
    |
    v
Integration Test
```

Nếu fail:

```text
Integration Test
       |
       v
Identify responsible task
       |
       v
Create / reopen bug task
       |
       v
Developer
```

---

# 31. QA

QA Agent kiểm tra:

- Functional test.
- API test.
- UI test.
- Integration test.
- Negative test.
- Boundary test.
- Regression test.

---

# 32. Bug Lifecycle

Khi QA phát hiện bug:

```text
BUG FOUND
   |
   v
Bug Analysis
   |
   v
Task Manager
   |
   v
Assign Developer
   |
   v
Developer Fix
   |
   v
Targeted Test
   |
   v
Regression Test
   |
   v
QA
```

---

# 33. Regression Testing

Mọi thay đổi có khả năng ảnh hưởng chức năng khác phải trigger regression test phù hợp.

Ví dụ:

```text
AuthService changed
      |
      +-- Login test
      +-- Refresh token test
      +-- Permission test
      +-- User session test
```

Không chỉ test đúng bug vừa sửa.

---

# 34. Security Review

Security Agent kiểm tra:

- Authentication.
- Authorization.
- Input validation.
- Injection.
- Secrets.
- Sensitive data exposure.
- API security.
- Dependencies.
- Configuration.
- Access control.

Output:

```text
security/security-report.md
```

---

# 35. Release Preparation

Trước release:

```text
Development PASS
Code Review PASS
Integration PASS
QA PASS
Security PASS
```

Release Agent kiểm tra:

- Version.
- Changelog.
- Migration.
- Configuration.
- Environment.
- Build.
- Artifact.
- Rollback strategy.

---

# 36. Deployment

Deploy Agent:

```text
Build
  |
  v
Package
  |
  v
Deploy
  |
  v
Health Check
  |
  v
Smoke Test
```

Nếu deploy fail:

```text
Deployment Failed
      |
      v
Rollback / Fix
```

---

# 37. Post-deployment Monitoring

Sau deploy:

- Health check.
- Error rate.
- Service availability.
- Logs.
- Basic performance.
- Critical business flow.

Project chỉ hoàn thành khi deployment và health check đạt yêu cầu.

---

# 38. Architecture Decision Records

Project phải có:

```text
decisions/
```

Ví dụ:

```text
ADR-001-database.md
ADR-002-authentication.md
ADR-003-message-broker.md
ADR-004-cache.md
```

ADR lưu:

- Context.
- Problem.
- Options.
- Decision.
- Consequences.
- Date.
- Related tasks.

Mục tiêu:

> Agent tương lai không đưa ra quyết định mâu thuẫn với các quyết định đã được chấp nhận.

---

# 39. Project Monitor

Project Monitor phải theo dõi:

```text
TOTAL TASKS
READY
IN_PROGRESS
WAITING_FOR_PO
BLOCKED
TESTING
REVIEW
DONE
FAILED
```

Ví dụ:

```text
Project Progress: 63%

READY          12
IN_PROGRESS     5
WAITING_PO      1
BLOCKED         3
TESTING         4
REVIEW          2
DONE           87
FAILED          1
```

Monitor phải phát hiện:

- Agent stuck.
- Task không có update.
- Dependency bị block.
- Task vượt estimation.
- Agent quá tải.
- Agent idle.
- Task có thể batch.
- Task mới được unlock.

---

# 40. Task Manager và Project Monitor

Hai thành phần không giống nhau.

## Task Manager

Quyết định và điều phối:

> Task nào chạy, chạy khi nào, giao cho ai.

## Project Monitor

Quan sát và phân tích:

> Project đang khỏe hay có vấn đề gì.

Ví dụ:

```text
Task Manager
    |
    +--> Assign TASK-101

Project Monitor
    |
    +--> Detect TASK-101 stuck 40 minutes
    |
    +--> Alert Task Manager
```

---

# 41. Context Manager

Flow:

```text
TASK
 |
 v
Dependency Resolver
 |
 v
Relevant Artifacts
 |
 v
Relevant Summaries
 |
 v
Relevant ADR
 |
 v
Relevant Source Code
 |
 v
Relevant Tests
 |
 v
Prompt Builder
 |
 v
LLM
```

Context Manager phải tránh đưa những dữ liệu không liên quan vào prompt.

---

# 42. Agent Registry

Registry quản lý:

- Agent ID.
- Capability.
- Model.
- Provider.
- Availability.
- Current workload.
- Supported task types.
- Permissions.

Ví dụ:

```text
backend-developer
frontend-developer
database-developer
qa-agent
security-agent
review-agent
devops-agent
```

---

# 43. LLM Abstraction

Không hard-code một model.

```text
Agent
  |
  v
LLM Abstraction
  |
  +-- OpenAI
  +-- Anthropic
  +-- Local LLM
  +-- Other provider
```

Mỗi Agent có thể sử dụng model khác nhau.

---

# 44. Token và Cost Management

Hệ thống phải ghi:

- Provider.
- Model.
- Agent.
- Task.
- Batch.
- Input tokens.
- Output tokens.
- Total tokens.
- Execution time.
- Estimated cost.

Ví dụ:

```text
TASK-101
Agent: backend-developer
Model: ...
Input: 8,200
Output: 4,100
Total: 12,300
Cost: ...
Execution: 84 sec
```

Mục tiêu:

- So sánh single-task với batch.
- Đo hiệu quả Context Manager.
- Tối ưu cost.
- Phát hiện Agent sử dụng token bất thường.

---

# 45. Error Classification

Hệ thống phải phân loại:

```text
LLM_ERROR
TOOL_ERROR
BUILD_ERROR
TEST_FAILURE
REQUIREMENT_AMBIGUITY
DEPENDENCY_BLOCKED
AGENT_TIMEOUT
AGENT_STUCK
GIT_CONFLICT
INTEGRATION_FAILURE
DEPLOYMENT_FAILURE
SECURITY_FAILURE
```

Mỗi loại có workflow xử lý riêng.

---

# 46. Human-in-the-loop

Con người có thể can thiệp tại:

```text
Requirement Approval
Architecture Approval
Business Question
High Risk Technical Decision
Security Finding
Release Approval
Deployment Approval
```

Vai trò có thể gồm:

```text
PO
BA
Architect
Developer
Reviewer
Admin
```

---

# 47. Permission và File Ownership

Hệ thống cần kiểm soát Agent nào được sửa artifact nào.

Ví dụ:

```text
Requirement Agent
    -> requirement.md

BA
    -> business-analysis.md

Architect
    -> system-design.md

Developer
    -> implementation-plan.md
    -> source code
    -> task state
    -> task summary

QA
    -> QA report
    -> test artifacts

Security
    -> security report
```

Summary có thể được Agent khác cập nhật nếu có quyền.

---

# 48. Concurrent File Editing

Nếu nhiều Agent có thể sửa cùng một artifact phải có cơ chế:

- Lock.
- Version.
- Optimistic concurrency.
- Merge.
- Conflict resolution.

Không được để Agent ghi đè mất thay đổi của Agent khác.

---

# 49. Project Artifact Structure

```text
/project
│
├── requirements/
│   └── requirement.md
│
├── analysis/
│   ├── business-analysis.md
│   ├── use-cases.md
│   ├── business-rules.md
│   └── workflows.md
│
├── design/
│   ├── ui-ux-design.md
│   ├── system-design.md
│   ├── detailed-design.md
│   ├── database-design.md
│   ├── api-design.md
│   └── security-design.md
│
├── decisions/
│   ├── ADR-001-database.md
│   ├── ADR-002-authentication.md
│   └── ...
│
├── tasks/
│   ├── task-plan.md
│   ├── task-dependencies.md
│   │
│   ├── TASK-001/
│   │   ├── task.md
│   │   ├── implementation-plan.md
│   │   ├── state.md
│   │   ├── summary.md
│   │   ├── questions.md
│   │   └── log.md
│   │
│   └── TASK-002/
│       └── ...
│
├── reviews/
│   ├── architecture-review.md
│   └── code-review.md
│
├── qa/
│   ├── qa-plan.md
│   └── qa-report.md
│
├── security/
│   └── security-report.md
│
├── release/
│   ├── release-plan.md
│   └── changelog.md
│
└── source/
```

---

# 50. Task State Machine

Task state đề xuất:

```text
DRAFT
  |
  v
READY
  |
  v
IN_PROGRESS
  |
  +----> WAITING_FOR_PO
  |             |
  |             v
  |         IN_PROGRESS
  |
  +----> BLOCKED
  |          |
  |          v
  |         READY
  |
  v
IMPLEMENTATION_DONE
  |
  v
REVIEW
  |
  +---- FAIL ---> IN_PROGRESS
  |
  v
TESTING
  |
  +---- FAIL ---> IN_PROGRESS
  |
  v
DONE
```

Các trạng thái có thể mở rộng trong implementation.

---

# 51. Project State

Ngoài task state, project phải có:

```text
project-state.md
```

Theo dõi:

- Current phase.
- Current milestone.
- Overall progress.
- Active agents.
- Blocked tasks.
- Open questions.
- Critical risks.
- Latest decisions.
- Latest deployment.
- Overall token/cost.

---

# 52. LangGraph

LangGraph là orchestration engine chính.

LangGraph chịu trách nhiệm:

- Workflow.
- State transition.
- Conditional routing.
- Parallel execution.
- Retry.
- Human-in-the-loop.
- Checkpoint.
- Resume.
- Agent execution.

LangGraph không phải nơi duy nhất chứa project knowledge.

---

# 53. Kiến trúc logic

```text
                    USER
                     |
                     v
              PROJECT MANAGER
                     |
        +------------+-------------+
        |            |             |
        v            v             v
   Requirement    Design       Task Manager
     Engine       Engine            |
        |            |              |
        +------------+--------------+
                     |
                     v
                LangGraph
                     |
          +----------+----------+
          |          |          |
          v          v          v
       Agents     Context     State
                  Manager     Manager
          |          |          |
          +----------+----------+
                     |
          +----------+----------+
          |                     |
          v                     v
      Markdown                 Git
      Artifacts             Repository
          |
          v
       Database
       / Index
```

---

# 54. Các engine chính

1. Requirement Engine.
2. Requirement Validation Engine.
3. Analysis Engine.
4. UI/UX Engine.
5. Design Engine.
6. Architecture Review Engine.
7. Task Planning Engine.
8. Task Management Engine.
9. Scheduling / Batch Engine.
10. Agent Execution Engine.
11. Context Management Engine.
12. State Management Engine.
13. Integration Engine.
14. QA Engine.
15. Security Engine.
16. Release Engine.
17. Deployment Engine.
18. Knowledge / Decision Engine.
19. Project Monitoring Engine.
20. Token / Cost Engine.

---

# 55. Non-functional Requirements

## Maintainability

Agent phải có responsibility rõ ràng.

## Observability

Có thể biết:

- Agent đang làm gì.
- Task nào đang chạy.
- Task nào block.
- Lỗi ở đâu.
- Model nào được gọi.
- Token bao nhiêu.

## Recoverability

Có thể resume sau khi process bị dừng.

## Idempotency

Retry không được tạo duplicate artifact hoặc operation nguy hiểm.

## Auditability

Các thay đổi quan trọng phải có lịch sử.

## Security

Agent chỉ được truy cập resource cần thiết.

## Scalability

Có thể chạy nhiều Agent và nhiều project.

---

# 56. Acceptance Criteria tổng thể

MVP được xem là đạt khi có thể:

1. Nhận một ý tưởng.
2. Tạo requirement Markdown.
3. Validate requirement.
4. Cho PO approve.
5. BA tạo business analysis.
6. UI/UX tạo design.
7. System Designer tạo architecture.
8. Detailed Designer tạo detailed design.
9. Architecture Review.
10. Task Planner tạo task.
11. Task có dependency.
12. Task có estimation.
13. Task Manager tìm task READY.
14. Task độc lập được nhận diện.
15. Task độc lập có thể được batch.
16. Developer đọc context.
17. Developer hỏi PO/BA nếu chưa rõ.
18. Developer tạo implementation plan.
19. Developer code.
20. Developer test.
21. Task state được cập nhật.
22. Task summary được tạo.
23. Agent khác đọc được summary.
24. Dependency được unlock tự động.
25. Code Review.
26. Integration.
27. Integration Test.
28. QA.
29. Bug được quay lại Developer.
30. Regression Test.
31. Security Review.
32. Release.
33. Deploy.
34. Health Check.
35. Post-deployment monitoring.
36. Project Monitor.
37. Token/cost tracking.
38. Có thể resume workflow.

---

# 57. MVP Roadmap

## Phase 1 — Foundation

- Python.
- LangGraph.
- Project structure.
- Markdown artifact manager.
- Git integration.
- LLM abstraction.
- Agent registry.
- Basic state manager.

## Phase 2 — Requirement & Design

- Requirement Agent.
- Requirement Validator.
- PO approval.
- BA Agent.
- UI/UX Agent.
- System Design Agent.
- Detailed Design Agent.
- Architecture Review Agent.

## Phase 3 — Task Engine

- Task Planner.
- Task definition.
- Dependency graph.
- Estimation.
- Task Manager.
- Task State.
- Task Log.
- Batch execution.

## Phase 4 — Developer

- Context Manager.
- Developer Agent.
- Question workflow.
- Implementation plan.
- Coding.
- Testing.
- Summary.
- Git operations.

## Phase 5 — Quality

- Code Review Agent.
- Integration Agent.
- QA Agent.
- Bug lifecycle.
- Regression testing.
- Security Agent.

## Phase 6 — Management

- Project Monitor.
- Dashboard.
- Agent monitoring.
- Task monitoring.
- Token monitoring.
- Cost monitoring.
- Risk monitoring.

## Phase 7 — Release

- Release Agent.
- DevOps Agent.
- Docker.
- CI/CD.
- Deployment.
- Health check.
- Rollback.

---

# 58. Các vấn đề TBD

Các vấn đề sau chưa được chốt:

- Database cụ thể.
- Dashboard framework.
- Git provider.
- CI/CD provider.
- LLM provider cho từng Agent.
- Local LLM.
- Sandbox cho Coding Agent.
- Permission model chi tiết.
- File locking implementation.
- Git branching strategy.
- Merge strategy.
- Rollback strategy.
- Deployment environment.
- Production approval policy.
- Exact task estimation algorithm.
- Agent capacity algorithm.
- Batch optimization algorithm.

---

# 59. Nguyên tắc thiết kế cuối cùng

> **Idea → Requirement → Validation → Approval → Analysis → UI/UX → Architecture → Detailed Design → Review → Task Graph → Scheduling → Batch → Development → State → Summary → Review → Integration → QA → Regression → Security → Release → Deploy → Health Check → Monitor.**

Trong giai đoạn Development:

> **Developer phải đọc tài liệu trước.**

> **Không rõ thì hỏi PO/BA.**

> **Hiểu rồi mới lập implementation plan.**

> **Plan xong mới code.**

> **Code phải đi cùng test.**

> **Mọi thay đổi quan trọng phải cập nhật task state.**

> **Hoàn thành task phải tạo summary.**

> **Summary phải đủ để Agent khác tiếp tục công việc.**

> **Task độc lập được batch khi phù hợp để tiết kiệm token và thời gian.**

> **Task phụ thuộc chỉ được mở khi dependency hoàn thành.**

> **Mọi quyết định kiến trúc quan trọng phải được lưu thành ADR.**

> **QA failure phải quay lại Developer và sau đó phải có regression test.**

> **Không deploy khi chưa vượt qua các gate bắt buộc.**

---

# 60. Tầm nhìn

AI Software Factory không nên được xây như:

```text
LLM
 + Agent 1
 + Agent 2
 + Agent 3
```

Mà phải được xây như:

```text
                  AI SOFTWARE COMPANY
                         |
        +----------------+----------------+
        |                |                |
   MANAGEMENT         DESIGN          ENGINEERING
        |                |                |
   Project Manager    Architect       Developers
   Task Manager      UI/UX           QA
   Monitor           BA              Security
                                     DevOps
        |                |                |
        +----------------+----------------+
                         |
                  KNOWLEDGE SYSTEM
                         |
        +----------------+----------------+
        |                |                |
     Markdown           Git           Database
        |
        v
     LangGraph
        |
        v
      LLMs
```

Mục tiêu là tạo ra một **AI Software Company có quy trình, trạng thái, kiến thức, trách nhiệm và khả năng tự điều phối**, thay vì chỉ tạo ra một Multi-Agent chatbot.

# V0.3 Architecture Addendum — Agent Worker, Role, Capability & Model Routing

## 1. Version
- Document: AI Software Factory Requirements
- Version: V0.3
- Status: Architecture baseline
- Date: 2026-10-01

## 2. Core Architectural Change

V0.3 formally separates four concepts:

**Agent Worker != Agent Role != Capability != Model**

- **Agent Worker**: a runtime worker capable of invoking one or more models and executing work.
- **Agent Role**: the business/engineering responsibility assigned for a particular execution.
- **Capability**: a normalized skill required by a task.
- **Model**: the underlying LLM provider/model used by a Worker.

A Worker can perform multiple Roles. A Role can be fulfilled by multiple Workers. A Task requests Capabilities rather than naming a model directly.

Therefore the Factory MUST NOT hard-code rules such as:
- Claude = Architect
- Gemini = Developer
- GPT = Project Manager

Those are deployment/configuration choices, not workflow rules.

## 3. Target Worker Model

The initial deployment may use a small number of Workers, for example:

### Strategic Worker
Possible models: Claude or another high-reasoning model.

Possible roles:
- Requirement Analyst
- BA
- System Architect
- Detailed Designer
- Architecture Reviewer
- ADR/Decision Analyst

### Engineering Worker
Possible models: Gemini, GPT, Claude, or another coding-capable model.

Possible roles:
- Backend Developer
- Frontend Developer
- Database Developer
- Integration Developer
- Test Developer
- QA Engineer
- Code Reviewer

### Management Worker
Possible models: GPT, Claude, Gemini, or another reasoning model.

Possible roles:
- Project Manager
- Task Planner
- Task Dispatcher
- Project Monitor
- Progress Analyst
- Documentation Coordinator

### Local Worker
Possible local models:
- Qwen Coder
- DeepSeek Coder
- GLM
- Other approved local coding models

Possible roles:
- Simple implementation
- Refactoring
- Documentation
- Formatting
- Low-risk bug fixes
- Repetitive test generation

Specialist Workers such as Security or DevOps may be introduced when required. They do not need to be permanently active.

## 4. Agent Registry

The Agent Registry defines available Workers.

Example:

```yaml
workers:
  - id: strategic-worker
    provider: anthropic
    model: claude
    enabled: true

  - id: engineering-worker
    provider: google
    model: gemini
    enabled: true

  - id: management-worker
    provider: openai
    model: gpt
    enabled: true

  - id: local-coding-worker
    provider: ollama
    model: qwen-coder
    enabled: true
```

The Registry MUST support:
- enable/disable
- model/provider configuration
- capabilities
- supported roles
- context limits
- cost information
- latency information
- reliability/health status
- permissions
- concurrency limits
- fallback workers

## 5. Capability Registry

Capabilities are the routing contract between Tasks and Workers.

Examples:

```yaml
capabilities:
  system_architecture:
    required_quality: high
  backend_development:
    required_quality: medium
  frontend_development:
    required_quality: medium
  automated_testing:
    required_quality: medium
  security_review:
    required_quality: high
  project_planning:
    required_quality: high
```

A Task SHOULD declare:

```markdown
## Required Capabilities
- backend_development
- automated_testing
```

The Task SHOULD NOT declare:

```markdown
## Model
Gemini
```

unless a human explicitly requires a model/provider.

## 6. Model Router

The Model Router selects a suitable Worker for a Task.

Routing inputs include:
- required capability
- role
- task complexity
- context size
- required quality
- token budget
- cost budget
- latency target
- security classification
- data residency/privacy rules
- Worker availability
- current Worker load
- model health
- historical success rate
- fallback policy

Conceptually:

```text
Task
  ↓
Required Capability
  ↓
Candidate Workers
  ↓
Permission / Security Filter
  ↓
Capability Match
  ↓
Quality / Context Filter
  ↓
Cost / Token / Latency Evaluation
  ↓
Load / Availability Check
  ↓
Primary Worker
  ↓
Fallback Worker if required
```

The Router MUST be configurable and MUST NOT embed provider-specific workflow logic.

## 7. Dynamic Role Assignment

At execution time:

```text
TASK-023
Capability = backend_development
Role = Backend Developer
        ↓
Model Router
        ↓
Engineering Worker
        ↓
Gemini
        ↓
Developer Role Prompt
        ↓
Relevant Context
        ↓
Implementation
```

The same Worker can later execute:

```text
Role = QA Engineer
```

or:

```text
Role = Code Reviewer
```

without creating a new permanent Agent.

## 8. Role Prompting

Role behavior MUST be supplied separately from the Worker.

Execution context:

```text
Worker
+
Role Definition
+
Task Definition
+
Relevant Markdown Artifacts
+
Relevant Source Code
+
ADR / Decisions
+
Permissions
+
Acceptance Criteria
```

This allows one Worker to safely perform multiple responsibilities while preserving role-specific behavior.

## 9. Task Routing Example

```text
TASK-001
Required Capability:
  system_architecture

        ↓

Router

        ↓

Strategic Worker
Role:
  System Architect

        ↓

Architecture Output
```

Another task:

```text
TASK-010
Required Capability:
  backend_development

        ↓

Router

        ↓

Engineering Worker
Role:
  Backend Developer

        ↓

Implementation
```

Another task:

```text
TASK-011
Required Capability:
  automated_testing

        ↓

Router

        ↓

Engineering Worker
Role:
  QA/Test Engineer

        ↓

Tests
```

The same Engineering Worker may execute all three developer/test roles across different tasks.

## 10. Dynamic Developer Workers

Developer execution is dynamic.

The Factory MUST NOT require one permanent Agent per task.

If 20 independent tasks are available, the Scheduler may create a batch such as:

```text
Batch-001
  ├── Engineering Worker Instance A → TASK-001
  ├── Engineering Worker Instance B → TASK-004
  ├── Engineering Worker Instance C → TASK-007
  └── Engineering Worker Instance D → TASK-009
```

The number of runtime instances depends on:
- available API capacity
- token budget
- task independence
- context requirements
- concurrency limits
- expected execution time
- project priority

## 11. Batch Execution and Token Optimization

Independent tasks SHOULD be grouped into batches where safe.

The Context Manager SHOULD reuse shared project context when possible.

The system SHOULD avoid repeatedly sending:
- the entire project
- unrelated requirements
- unrelated source code
- unrelated task history

Instead, the Context Manager selects:

```text
Requirement
+
Relevant Design
+
Relevant ADR
+
Dependency Summaries
+
Task
+
Relevant Source
+
Relevant Tests
```

## 12. Worker Fallback

If the primary Worker fails:

```text
Primary Worker
      ↓
Failure Classification
      ↓
Retry if transient
      ↓
Fallback Worker
      ↓
Resume Task
```

Examples:
- provider timeout
- rate limit
- unavailable model
- context overflow
- temporary API failure

The system MUST distinguish infrastructure failures from task failures.

## 13. Human Model Override

A human may explicitly require a provider/model for:
- sensitive architecture decisions
- regulated environments
- security work
- customer-specific constraints
- reproducibility
- debugging

Otherwise, routing remains capability-based.

## 14. Model Independence

Changing a model MUST NOT require changing:
- task definitions
- dependency DAG
- task state machine
- project workflow
- Markdown artifact structure
- LangGraph workflow definitions

Only Worker/Registry/Router configuration should normally change.

This is a core architectural requirement.

## 15. Updated Logical Architecture

```text
                         USER
                           │
                           ▼
                    ┌─────────────┐
                    │ LangGraph   │
                    │Orchestrator │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │Task Manager  │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │Model Router │
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
        Strategic      Engineering   Management
         Worker          Worker        Worker
              │            │            │
              └────────────┼────────────┘
                           │
                    ┌──────▼──────┐
                    │ Context Mgr │
                    └──────┬──────┘
                           │
              ┌────────────▼────────────┐
              │ Markdown + Git + DB    │
              │ Knowledge / State      │
              └────────────────────────┘
```

## 16. Responsibility Boundaries

### LangGraph
Responsible for:
- workflow orchestration
- branching
- loops
- retries
- human-in-the-loop
- state transitions

### Task Manager
Responsible for:
- task lifecycle
- dependency handling
- readiness
- dispatch

### Model Router
Responsible for:
- Worker selection
- model selection
- fallback
- routing policy

### Context Manager
Responsible for:
- context selection
- context minimization
- token optimization

### State Manager
Responsible for:
- task state
- event processing
- progress tracking
- consistency

### Agent Worker
Responsible for:
- executing assigned Role
- reading required context
- producing artifacts/code
- testing
- updating task state
- updating summary

## 17. Developer Role Lifecycle

```text
TASK READY
    ↓
READ CONTEXT
    ↓
UNDERSTAND
    ↓
UNCLEAR?
 ┌──┴──┐
YES    NO
 │      │
ASK PO  CREATE IMPLEMENTATION PLAN
 │      │
WAIT    ↓
 │     CODE
 └──→ TEST
        ↓
 UPDATE TASK STATE
        ↓
 UPDATE TASK SUMMARY
        ↓
 CODE REVIEW
        ↓
 INTEGRATION
```

Every coding action SHOULD produce task-state events such as:

```text
TASK_STARTED
FILE_CREATED
FILE_MODIFIED
TEST_STARTED
TEST_FAILED
TEST_PASSED
QUESTION_CREATED
BLOCKED
IMPLEMENTATION_COMPLETED
TASK_COMPLETED
```

## 18. Existing Factory Workflow — Preserved

```text
USER IDEA
 ↓
REQUIREMENT
 ↓
REQUIREMENT VALIDATION
 ↓
PO APPROVAL
 ↓
BUSINESS ANALYSIS
 ↓
UI/UX DESIGN
 ↓
SYSTEM DESIGN
 ↓
DETAILED DESIGN
 ↓
ARCHITECTURE REVIEW
 ↓
TASK PLANNING
 ↓
TASK ESTIMATION
 ↓
DEPENDENCY GRAPH
 ↓
TASK SCHEDULING
 ↓
BATCH PLANNING
 ↓
DEVELOPER EXECUTION
 ↓
TASK STATE + SUMMARY
 ↓
CODE REVIEW
 ↓
INTEGRATION
 ↓
INTEGRATION TEST
 ↓
QA
 ↓
BUG / FIX / REGRESSION
 ↓
SECURITY REVIEW
 ↓
RELEASE
 ↓
DEPLOY
 ↓
HEALTH CHECK
 ↓
POST-DEPLOY MONITORING
 ↓
PROJECT COMPLETE
```

## 19. Project Artifact Structure

```text
/project
├── requirements/
│   └── requirement.md
├── analysis/
│   ├── business-analysis.md
│   ├── use-cases.md
│   ├── business-rules.md
│   └── workflows.md
├── design/
│   ├── ui-ux-design.md
│   ├── system-design.md
│   ├── detailed-design.md
│   ├── database-design.md
│   ├── api-design.md
│   └── security-design.md
├── decisions/
│   ├── ADR-001-database.md
│   ├── ADR-002-authentication.md
│   └── ...
├── agents/
│   ├── agent-registry.md
│   ├── capability-registry.md
│   ├── routing-policy.md
│   └── role-definitions/
│       ├── ba.md
│       ├── architect.md
│       ├── developer.md
│       ├── qa.md
│       └── ...
├── tasks/
│   ├── task-plan.md
│   ├── task-dependencies.md
│   ├── TASK-001/
│   │   ├── task.md
│   │   ├── implementation-plan.md
│   │   ├── state.md
│   │   ├── summary.md
│   │   ├── questions.md
│   │   └── log.md
│   └── ...
├── reviews/
├── qa/
├── security/
├── release/
└── source/
```

## 20. Non-Functional Requirements Added in V0.3

### NFR-AGENT-01
The system MUST support multiple Roles per Worker.

### NFR-AGENT-02
The system MUST support multiple Workers for the same Capability.

### NFR-AGENT-03
Task definitions MUST be model-independent by default.

### NFR-AGENT-04
Workers MUST be replaceable without changing the business workflow.

### NFR-AGENT-05
Routing decisions MUST be observable and auditable.

### NFR-AGENT-06
The Router MUST support fallback Workers.

### NFR-AGENT-07
The Router MUST consider token/cost constraints.

### NFR-AGENT-08
The system MUST support dynamic Worker instances for parallel task execution.

### NFR-AGENT-09
Role instructions MUST be isolated from model/provider configuration.

### NFR-AGENT-10
Security and permission checks MUST happen before a Worker receives protected context.

## 21. Acceptance Criteria

V0.3 architecture is considered implemented when:

1. A task can declare a Capability without naming a model.
2. The Router can select a Worker based on Capability.
3. One Worker can execute multiple Roles.
4. Multiple Workers can provide the same Capability.
5. A Worker can be replaced through configuration.
6. A failed Worker can fall back to another Worker.
7. Independent tasks can run concurrently.
8. Task state and summary remain Markdown artifacts.
9. Routing decisions are recorded.
10. The workflow remains unchanged when the underlying model changes.

## 22. Architectural Principle

The Factory is NOT:

```text
LLM 1 = Agent 1
LLM 2 = Agent 2
LLM 3 = Agent 3
```

The Factory IS:

```text
Workflow
    +
Roles
    +
Capabilities
    +
Workers
    +
Models
    +
Router
    +
Context
    +
State
    +
Knowledge
```

This separation is a fundamental architectural principle of AI Software Factory V0.3.

## 23. Future Evolution

The architecture should allow:

```text
Claude
Gemini
GPT
DeepSeek
GLM
Qwen
Local Models
Future Models
```

to be added or removed without redesigning the Factory workflow.

The long-term objective is a **model-agnostic AI Software Company** where business responsibilities remain stable while execution models can evolve independently.

# AI SOFTWARE FACTORY REQUIREMENTS — V0.4

## 1. Version

- Document: AI Software Factory Requirements
- Version: V0.4
- Status: Architecture baseline
- Date: 2026-10-01
- Supersedes: V0.3

---

# 2. V0.4 Architectural Objective

V0.4 extends V0.3 by introducing a **Methodology Layer**.

The AI Software Factory Core MUST be independent from any specific software-development methodology.

The same Factory MUST be able to execute projects using:

- Agile
- Scrum
- Kanban
- Waterfall
- Hybrid
- Future/custom methodologies

The methodology controls **how work is organized, planned, scheduled, approved, reviewed, and measured**.

It MUST NOT redefine the underlying Agent Worker, Agent Role, Capability, Model Router, Context Manager, State Manager, Knowledge System, or core execution engine.

Core principle:

> **Methodology is a project-level policy/profile, not the Factory itself.**

---

# 3. Core Architecture

The Factory is divided into layers:

```text
┌──────────────────────────────────────────────┐
│                    USER                      │
└───────────────────────┬──────────────────────┘
                        │
                        ▼
┌──────────────────────────────────────────────┐
│              PROJECT CONFIGURATION           │
│                                              │
│ Methodology / Quality / Security / Policies  │
└───────────────────────┬──────────────────────┘
                        │
                        ▼
┌──────────────────────────────────────────────┐
│             METHODOLOGY ENGINE               │
│                                              │
│ Scrum / Agile / Kanban / Waterfall / Hybrid │
└───────────────────────┬──────────────────────┘
                        │
                        ▼
┌──────────────────────────────────────────────┐
│               CORE WORKFLOW                  │
│                  LangGraph                   │
└───────────────────────┬──────────────────────┘
                        │
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
      Task Manager  Project Monitor  State Manager
          │
          ▼
      Model Router
          │
   ┌──────┼──────┐
   ▼      ▼      ▼
Claude  Gemini   GPT
Worker  Worker  Worker
          │
          ▼
    Context Manager
          │
          ▼
 Markdown + Git + DB + Artifacts
```

---

# 4. Separation of Responsibilities

## 4.1 Factory Core

The Core is methodology-independent.

It provides:

- Requirement processing
- Analysis
- Design
- Task management
- Dependency management
- Scheduling primitives
- Agent routing
- Context management
- State management
- Code execution
- Testing
- QA
- Security
- Release
- Deployment
- Monitoring
- Knowledge management

## 4.2 Methodology Layer

The Methodology Layer determines:

- Work unit structure
- Planning cadence
- Approval gates
- Prioritization rules
- Scheduling policy
- Review cadence
- Completion rules
- Metrics
- ceremonies/events
- backlog behavior
- change-control behavior

---

# 5. Methodology Profile

Each project MUST have a methodology profile.

Example:

```yaml
project:
  name: ACMS
  methodology:
    type: scrum
    version: "1.0"
```

Alternative:

```yaml
project:
  name: Customer Portal
  methodology:
    type: waterfall
```

Hybrid:

```yaml
project:
  name: Enterprise Platform
  methodology:
    type: hybrid
    profiles:
      development: scrum
      infrastructure: waterfall
      maintenance: kanban
```

---

# 6. Methodology Engine

The Methodology Engine interprets the selected profile and generates project policies.

Responsibilities:

1. Load methodology profile.
2. Validate project configuration.
3. Configure workflow rules.
4. Configure planning behavior.
5. Configure task states where methodology-specific states are required.
6. Configure approval gates.
7. Configure planning/review cadence.
8. Configure metrics.
9. Expose methodology events to LangGraph.
10. Keep methodology-specific logic outside Core Agents.

---

# 7. Common Work Model

Regardless of methodology, the Factory uses a common internal work model.

```text
Project
  ↓
Requirement
  ↓
Feature / Epic
  ↓
User Story / Use Case
  ↓
Work Item
  ↓
Task
  ↓
Execution
  ↓
Validation
  ↓
Done
```

A methodology may rename or reorganize these objects, but the Core SHOULD preserve a normalized internal representation.

---

# 8. Common Task Model

Every executable Task can contain:

```markdown
# TASK-003

## Objective
Implement login API.

## Work Type
Backend

## Required Capabilities
- backend_development
- automated_testing

## Priority
HIGH

## Dependencies
- TASK-001
- TASK-002

## Independent
No

## Parallelizable
No

## Acceptance Criteria
- Valid credentials return JWT.
- Invalid credentials return HTTP 401.
- JWT contains user identity and roles.

## Methodology Context
Sprint: SPRINT-01
Story: US-003
```

The methodology context is additional metadata; it does not replace the Core Task Definition.

---

# 9. Scrum Profile

## 9.1 Scrum Objects

The Scrum profile supports:

- Product
- Product Goal
- Product Backlog
- Epic
- Feature
- User Story
- Sprint
- Sprint Goal
- Sprint Backlog
- Task
- Increment
- Definition of Done

## 9.2 Scrum Workflow

```text
Product Backlog
      ↓
Backlog Refinement
      ↓
Sprint Planning
      ↓
Sprint Backlog
      ↓
Task Dependency Analysis
      ↓
Batch Planning
      ↓
Development
      ↓
Code Review
      ↓
QA
      ↓
Integration
      ↓
Sprint Review
      ↓
Retrospective
      ↓
Next Sprint
```

## 9.3 Scrum AI Roles

Roles are mapped to existing Workers.

Examples:

- Product Owner → Management/Strategic Worker
- Scrum Master → Management Worker
- Business Analyst → Strategic Worker
- Architect → Strategic Worker
- Developer → Engineering Worker
- QA → Engineering/QA Worker
- Reviewer → Engineering Worker
- Project Monitor → Management Worker

These are Roles, not permanent Agent instances.

## 9.4 Scrum Events

The Methodology Engine may generate:

```text
SPRINT_STARTED
SPRINT_GOAL_SET
BACKLOG_REFINED
SPRINT_PLANNED
TASK_READY
TASK_STARTED
TASK_BLOCKED
TASK_DONE
SPRINT_REVIEW_STARTED
SPRINT_REVIEW_COMPLETED
RETROSPECTIVE_STARTED
RETROSPECTIVE_COMPLETED
SPRINT_COMPLETED
```

---

# 10. Kanban Profile

Kanban focuses on continuous flow.

Typical workflow:

```text
BACKLOG
   ↓
READY
   ↓
IN PROGRESS
   ↓
CODE REVIEW
   ↓
TESTING
   ↓
READY FOR RELEASE
   ↓
DONE
```

The Kanban profile supports:

- Work In Progress limits
- Pull-based scheduling
- Continuous delivery
- Priority queues
- Blocked work tracking
- Cycle time
- Lead time
- Throughput

Example:

```yaml
kanban:
  wip_limits:
    development: 4
    code_review: 2
    testing: 3
```

The Scheduler MUST respect WIP limits.

---

# 11. Waterfall Profile

Waterfall emphasizes sequential phases and formal gates.

Typical workflow:

```text
Requirement
     ↓
Requirement Approval
     ↓
Business Analysis
     ↓
System Design
     ↓
Detailed Design
     ↓
Design Approval
     ↓
Implementation
     ↓
Integration
     ↓
System Testing
     ↓
Security
     ↓
User Acceptance
     ↓
Release
     ↓
Deployment
```

## 11.1 Waterfall Gates

Example:

```text
GATE-01 Requirement Approval
GATE-02 Architecture Approval
GATE-03 Detailed Design Approval
GATE-04 Implementation Complete
GATE-05 System Test Approval
GATE-06 Release Approval
```

The Factory MUST NOT automatically cross a mandatory gate without its configured approval condition.

---

# 12. Agile Profile

Agile without Scrum uses continuous prioritization and iterative delivery.

Example:

```text
Backlog
  ↓
Priority
  ↓
Ready
  ↓
Development
  ↓
Review
  ↓
QA
  ↓
Done
  ↓
Next Work
```

No mandatory Sprint is required.

The Project Monitor focuses on:

- flow
- priority
- blockers
- delivery rate
- customer feedback
- change frequency

---

# 13. Hybrid Profile

Hybrid allows different methodologies for different workstreams.

Example:

```text
Project
│
├── Product Development
│      └── Scrum
│
├── Infrastructure
│      └── Waterfall
│
├── Support / Bug Fix
│      └── Kanban
│
└── Research
       └── Agile
```

The Factory MUST maintain a shared normalized Project model while allowing each Workstream to have its own Methodology Profile.

---

# 14. Methodology Adapter

To avoid hard-coding methodologies into Core logic, the system SHOULD use a Methodology Adapter interface.

Conceptually:

```text
MethodologyAdapter

    create_work_item()
    plan_work()
    start_iteration()
    complete_iteration()
    validate_transition()
    calculate_metrics()
    handle_change()
    get_next_action()
```

Implementations:

```text
ScrumAdapter
KanbanAdapter
WaterfallAdapter
AgileAdapter
HybridAdapter
```

Future:

```text
CustomMethodologyAdapter
```

---

# 15. Methodology State vs Core Task State

The system MUST distinguish:

### Core Task State

```text
DRAFT
READY
IN_PROGRESS
WAITING_FOR_PO
BLOCKED
IMPLEMENTATION_DONE
REVIEW
TESTING
DONE
```

### Methodology State

Example Scrum:

```text
PRODUCT_BACKLOG
SPRINT_BACKLOG
SPRINT_ACTIVE
SPRINT_REVIEW
SPRINT_DONE
```

Example Waterfall:

```text
REQUIREMENT_PHASE
DESIGN_PHASE
IMPLEMENTATION_PHASE
TEST_PHASE
RELEASE_PHASE
```

Methodology state MUST NOT destroy the Core Task State.

---

# 16. Change Management

Different methodologies handle change differently.

## Scrum / Agile

Changes can normally enter the backlog and be prioritized.

## Kanban

Changes can enter the flow according to priority and WIP rules.

## Waterfall

Changes after an approved gate may require:

```text
Change Request
      ↓
Impact Analysis
      ↓
Cost / Schedule Analysis
      ↓
Approval
      ↓
Baseline Update
      ↓
Task Replanning
```

The Methodology Engine owns this policy.

---

# 17. Project Configuration

Example:

```yaml
project:
  id: ACMS-001
  name: Access Control Management System

  methodology:
    type: scrum

  quality:
    code_review_required: true
    qa_required: true
    security_review_required: true

  release:
    approval_required: true

  execution:
    max_parallel_tasks: 5

  budget:
    max_tokens: 500000
```

---

# 18. Agent Architecture

V0.3's Worker/Role architecture remains unchanged.

```text
Agent Worker
    +
Role
    +
Capability
    +
Task
    +
Methodology Context
    +
Relevant Context
```

Example:

```text
Gemini Worker
Role = Backend Developer
Capability = backend_development
Methodology = Scrum
Sprint = SPRINT-04
Task = TASK-023
```

The model does not need to know the entire Scrum framework. It receives only the relevant execution context.

---

# 19. Methodology-Aware Routing

The Model Router MAY consider methodology context.

However, methodology MUST NOT directly select a model.

Correct:

```text
Methodology
     ↓
Task Policy
     ↓
Required Capability
     ↓
Model Router
     ↓
Worker
```

Incorrect:

```text
Scrum
 ↓
Gemini
```

---

# 20. Context Manager and Methodology

The Context Manager SHOULD provide only relevant methodology context.

For example, a developer executing a Scrum task may receive:

```text
Project Requirement
Relevant Design
ADR
User Story
Acceptance Criteria
Sprint Goal
Task
Dependencies
Relevant Source
```

A Waterfall developer may additionally receive:

```text
Approved Requirement Baseline
Approved Architecture
Approved Detailed Design
Change Request
Gate Status
```

---

# 21. Project Monitor

Project Monitor behavior is methodology-aware.

### Scrum

Monitor:

- Sprint progress
- Sprint goal
- blocked stories
- incomplete work
- velocity trends
- review readiness

### Kanban

Monitor:

- WIP
- blocked items
- cycle time
- throughput
- aging work

### Waterfall

Monitor:

- phase status
- gate status
- schedule variance
- dependency delays
- approval status
- change requests

### Hybrid

Monitor each Workstream according to its profile while providing one Project-level view.

---

# 22. Task Manager

Task Manager remains methodology-independent at its core.

It handles:

- readiness
- dependencies
- assignment
- state transitions
- scheduling requests
- blocked tasks
- retries
- completion

The Methodology Engine supplies additional policies.

Example:

```text
Task Manager:
"Is TASK-023 executable?"

        ↓

Methodology Engine:
"Yes, because Sprint is active."

        ↓

Dependency Engine:
"All dependencies are complete."

        ↓

Model Router:
"Engineering Worker is available."

        ↓

Execute
```

---

# 23. Release Management

Release behavior is methodology-aware.

Scrum/Agile:

```text
Increment
 ↓
QA
 ↓
Security
 ↓
Release
```

Waterfall:

```text
System Test Approval
 ↓
UAT
 ↓
Release Gate
 ↓
Deployment
```

Kanban:

```text
Ready for Release
 ↓
Automated Validation
 ↓
Continuous Deployment
```

The Release Engine remains common; the Methodology Profile determines its policy.

---

# 24. Unified Project Dashboard

The Factory SHOULD expose a common dashboard while adapting metrics to methodology.

Common:

- Project status
- Tasks
- Blockers
- Agents
- Token usage
- Cost
- Quality
- Security
- Releases

Scrum:

- Sprint progress
- Sprint goal
- backlog
- completed stories

Kanban:

- WIP
- throughput
- cycle time

Waterfall:

- phase progress
- gates
- schedule
- change requests

Hybrid:

- workstream-specific views
- unified project health

---

# 25. Methodology Selection at Project Creation

Project creation SHOULD provide:

```text
Create Project

Project Name: __________________

Methodology:
  [ Scrum ]
  [ Agile ]
  [ Kanban ]
  [ Waterfall ]
  [ Hybrid ]

Quality Level:
  [ Standard ]

Security Level:
  [ Standard ]

Deployment:
  [ Manual Approval ]
```

The selection creates the project's Methodology Profile.

---

# 26. Custom Methodology

The Factory SHOULD support custom methodology profiles.

Example:

```yaml
methodology:
  type: custom

  workflow:
    - requirements
    - architecture
    - implementation
    - qa
    - security
    - release

  approvals:
    architecture: human
    release: human

  wip:
    development: 4
```

This makes the Factory extensible beyond predefined methodologies.

---

# 27. Core Workflow

The overall Factory workflow remains:

```text
USER IDEA
 ↓
REQUIREMENT
 ↓
REQUIREMENT VALIDATION
 ↓
PO APPROVAL
 ↓
BUSINESS ANALYSIS
 ↓
UI/UX DESIGN
 ↓
SYSTEM DESIGN
 ↓
DETAILED DESIGN
 ↓
ARCHITECTURE REVIEW
 ↓
TASK PLANNING
 ↓
TASK ESTIMATION
 ↓
DEPENDENCY GRAPH
 ↓
METHODOLOGY POLICY
 ↓
TASK SCHEDULING
 ↓
BATCH PLANNING
 ↓
DEVELOPER EXECUTION
 ↓
TASK STATE + SUMMARY
 ↓
CODE REVIEW
 ↓
INTEGRATION
 ↓
INTEGRATION TEST
 ↓
QA
 ↓
BUG / FIX / REGRESSION
 ↓
SECURITY REVIEW
 ↓
RELEASE
 ↓
DEPLOY
 ↓
HEALTH CHECK
 ↓
POST-DEPLOY MONITORING
 ↓
PROJECT COMPLETE
```

The difference is that the **Methodology Engine controls how the work moves through the process**.

---

# 28. Complete Architecture

```text
                              USER
                               │
                               ▼
                     ┌───────────────────┐
                     │ PROJECT CREATION  │
                     └─────────┬─────────┘
                               │
                               ▼
                     ┌───────────────────┐
                     │ METHODOLOGY       │
                     │ PROFILE           │
                     └─────────┬─────────┘
                               │
          ┌────────────────────┼────────────────────┐
          ▼                    ▼                    ▼
       Scrum                Kanban              Waterfall
          │                    │                    │
          └────────────────────┼────────────────────┘
                               ▼
                     ┌───────────────────┐
                     │ METHODOLOGY       │
                     │ ENGINE            │
                     └─────────┬─────────┘
                               │
                               ▼
                     ┌───────────────────┐
                     │ LANGGRAPH CORE    │
                     └─────────┬─────────┘
                               │
               ┌───────────────┼───────────────┐
               ▼               ▼               ▼
         Task Manager     Project Monitor   State Manager
               │
               ▼
         Dependency Engine
               │
               ▼
          Batch Scheduler
               │
               ▼
          Model Router
               │
       ┌───────┼────────┐
       ▼       ▼        ▼
    Claude   Gemini     GPT
    Worker   Worker    Worker
       │       │        │
       └───────┼────────┘
               ▼
        Context Manager
               │
       ┌───────┼──────────┐
       ▼       ▼          ▼
     Git    Markdown      DB
       │       │          │
       └───────┼──────────┘
               ▼
       Knowledge / State
               │
               ▼
       QA / Security / Release
               │
               ▼
          Deployment
```

---

# 29. Non-Functional Requirements

### NFR-METHOD-01
The Factory Core MUST be independent of methodology.

### NFR-METHOD-02
A project MUST be able to select a methodology at creation.

### NFR-METHOD-03
The methodology MUST be changeable when project policy permits it.

### NFR-METHOD-04
The system MUST support Scrum, Agile, Kanban, Waterfall, and Hybrid.

### NFR-METHOD-05
Methodology-specific rules MUST be isolated in the Methodology Layer.

### NFR-METHOD-06
Core Task State MUST remain separate from Methodology State.

### NFR-METHOD-07
The Model Router MUST remain independent of methodology-specific provider choices.

### NFR-METHOD-08
The system MUST support custom methodology profiles.

### NFR-METHOD-09
Methodology transitions MUST be auditable.

### NFR-METHOD-10
Human approval gates MUST be configurable.

### NFR-METHOD-11
The system MUST preserve Git and Markdown as project knowledge/code sources of truth.

### NFR-METHOD-12
Methodology changes MUST NOT require rewriting Agent Workers.

---

# 30. Acceptance Criteria

V0.4 is considered architecturally complete when:

1. A project can be created with Scrum.
2. A project can be created with Kanban.
3. A project can be created with Waterfall.
4. A project can be created with Agile.
5. A project can be created with Hybrid.
6. The same Core Task Manager works across all methodologies.
7. The same Agent Workers can work across all methodologies.
8. Methodology changes do not require changing model routing.
9. Scrum can enforce Sprint rules.
10. Kanban can enforce WIP limits.
11. Waterfall can enforce phase gates.
12. Hybrid can assign different methodologies to different Workstreams.
13. Methodology state and Core Task state remain separate.
14. Methodology events are auditable.
15. Custom methodology profiles can be defined.
16. Agent routing remains capability-based.
17. Markdown artifacts remain readable by both humans and agents.
18. Git remains the source of truth for source code.
19. Project Monitor reports methodology-specific metrics.
20. Release policies can differ by methodology without changing the Release Engine.

---

# 31. Recommended Initial Implementation

The first implementation SHOULD NOT implement every methodology at once.

Recommended order:

### Phase 1
Core:

- Task model
- Agent Worker
- Role
- Capability
- Agent Registry
- Model Router
- Context Manager
- State Manager
- LangGraph
- Markdown/Git

### Phase 2
Scrum Profile:

- Product Backlog
- Sprint
- Sprint Goal
- Sprint Planning
- Sprint Review
- Retrospective

### Phase 3
Kanban Profile:

- Board
- WIP limits
- Continuous flow
- Cycle time

### Phase 4
Waterfall Profile:

- Phases
- Baselines
- Approval gates
- Change requests

### Phase 5
Hybrid:

- Workstream methodology
- Cross-workstream dependencies
- Unified dashboard

### Phase 6
Custom Methodology:

- Methodology DSL/profile
- Custom state transitions
- Custom gates
- Custom metrics

---

# 32. Final Architectural Principles

The AI Software Factory follows these principles:

1. **Core is methodology-agnostic.**
2. **Role is not Worker.**
3. **Worker is not Model.**
4. **Task requests Capability, not a model.**
5. **Model Router selects execution Workers.**
6. **Methodology controls project process, not model selection.**
7. **LangGraph orchestrates workflow.**
8. **Task Manager controls executable work.**
9. **Project Monitor observes and reports.**
10. **Context Manager minimizes context and token cost.**
11. **Markdown is the primary human/agent knowledge artifact.**
12. **Git is the source of truth for code.**
13. **Database stores runtime/index/orchestration state where appropriate.**
14. **Agents update Task State during execution.**
15. **Task Summary is a living handoff artifact.**
16. **Independent tasks should be batched for efficient execution.**
17. **Human approval is configurable at critical gates.**
18. **Security and permissions apply before protected context is provided.**
19. **Models can be replaced without redesigning the Factory.**
20. **Methodologies can be added without redesigning the Factory Core.**

---

# 33. V0.4 Vision

The final conceptual model is:

```text
                    AI SOFTWARE FACTORY
                           │
            ┌──────────────┴──────────────┐
            │                             │
      FACTORY CORE                  METHODOLOGY
            │                             │
      LangGraph                    Scrum / Agile
      Task Manager                 Kanban
      State Manager                Waterfall
      Context Manager              Hybrid
      Agent Router                 Custom
            │                             │
            └──────────────┬──────────────┘
                           │
                     PROJECT WORK
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
           Claude        Gemini         GPT
           Worker        Worker        Worker
              │            │            │
              └────────────┼────────────┘
                           ▼
                    Software Delivery
```

The Factory is therefore not a "Scrum Agent System", "Waterfall Agent System", or "Multi-Agent Coding System".

It is a **general AI Software Engineering Platform** capable of applying different project-management methodologies while preserving one common execution core.

---

# 34. Future V0.5 Candidates

Potential next architecture work:

- Detailed PostgreSQL schema
- LangGraph state model
- Agent Registry schema
- Capability Registry schema
- Model Router algorithm
- Methodology Profile schema
- Task/DAG schema
- Event model
- Context Manager architecture
- Git workspace/branch strategy
- Agent sandbox
- File locking/concurrency
- Permission model
- Human approval service
- Cost/token accounting
- Agent observability
- Web dashboard
- API design
- Queue/event bus
- Redis usage
- CI/CD integration
- Docker architecture
- Multi-project support
- Multi-tenant support


---

# V0.5 — PEAA + MCP CONTROL PLANE
## Authoritative architecture update

> All V0.4 requirements remain valid unless explicitly superseded below.

## 1. Primary change

V0.5 introduces the **Project Executive Advisor Agent (PEAA)**.

PEAA runs through an external AI client such as ChatGPT, Claude, Gemini, or another MCP-compatible client. It is the Owner-facing advisor and project executive. It is not required to run as an internal LangGraph Worker.

PEAA combines these reasoning responsibilities:

- Project Advisor
- Project Manager
- Task Manager
- Planner
- Dispatcher

The autonomous **Task Manager Agent is removed**.

The deterministic **Task Management Engine remains**.

Core principle:

> **LLM decides. Engine validates. Worker executes.**

## 2. Architecture

```text
                              OWNER
                                |
                                v
                   ChatGPT / Claude / Gemini
                                |
                          PEAA ROLE
                                |
                               MCP
                                |
                     +----------v----------+
                     | Factory MCP Gateway |
                     +----------+----------+
                                |
        +-----------------------+------------------------+
        |                       |                        |
        v                       v                        v
 Project Knowledge       Project Monitor        Task Management Engine
 / Context Services                                  |
                                              Dependency Engine
                                                     |
                                                State Engine
                                                     |
                                             Methodology Engine
                                                     |
                                             Permission Engine
                                                     |
                                                Model Router
                                                     |
                                  +------------------+------------------+
                                  v                  v                  v
                              Claude Worker      Gemini Worker      Local Worker
```

## 3. PEAA responsibilities

PEAA SHALL be able to:

- read all authorized project knowledge;
- report current project status, progress, phase, milestones and blockers;
- inspect Task definitions, dependencies, state, summaries and history;
- inspect Worker status and current execution;
- inspect relevant Git status/diffs, builds and tests;
- inspect QA, security, release and deployment status;
- advise the Owner about priority, architecture, risk, quality and delivery;
- create Tasks;
- edit Tasks;
- split Tasks;
- reprioritize Tasks;
- block/reopen Tasks where policy permits;
- assign or request assignment of Tasks;
- request execution and retry;
- coordinate parallel work;
- request small bug fixes and small changes;
- explain Engine rejection reasons;
- report delegated work results back to the Owner.

PEAA SHALL use current Factory state for project-status answers rather than relying only on conversational memory.

## 4. Task Manager Agent removal

The following V0.4 concept is superseded:

```text
Task Manager Agent = REMOVED
```

It is replaced by:

```text
PEAA                    = management reasoning and decisions
Task Management Engine  = deterministic validation/application
Project Monitor         = observation and metrics
Model Router            = Worker/model selection
Worker                  = execution
```

PEAA SHALL NOT bypass the Task Management Engine and call an internal Worker directly for managed project changes.

Required flow:

```text
PEAA
  |
MCP Gateway
  |
Task Management Engine
  |
State / Dependency / Methodology / Permission validation
  |
Model Router
  |
Worker + Role + Context + Permission
  |
Execution
```

## 5. Task Management Engine

The Task Management Engine remains an internal deterministic service.

It validates and applies operations such as:

```text
create_task
update_task
split_task
assign_task
unassign_task
change_priority
block_task
reopen_task
request_execution
retry_task
cancel_task
```

Validation may include:

- valid Task state;
- dependency completion;
- required Capability;
- Worker eligibility;
- concurrency conflicts;
- Methodology rules;
- permission scopes;
- approval requirements;
- protected resources;
- release/project state.

Example:

```text
PEAA requests: assign TASK-035

Engine result:
REJECTED

Reason:
DEPENDENCY_NOT_COMPLETED

Blocked by:
TASK-021
```

PEAA should explain the rejection and recommend a valid next action.

## 6. Project-wide knowledge access

PEAA may access, subject to permissions:

- requirements and validation;
- PO/Owner decisions;
- BA artifacts;
- use cases and workflows;
- UI/UX;
- system/detailed/database/API/security design;
- ADRs;
- Task plans and dependency DAG;
- task.md;
- implementation-plan.md;
- state.md;
- summary.md;
- questions.md;
- log.md;
- code-review results;
- Git status and relevant diffs;
- builds and tests;
- QA and security reports;
- release/deployment status;
- Worker activity;
- routing information;
- token/cost information;
- Methodology state;
- project history.

Project-wide access does NOT mean loading the whole project into every prompt.

```text
PEAA
 |
Project Knowledge Service
 |
 +-- Search
 +-- Structured Status
 +-- Summaries
 +-- Artifact Read
 +-- Task Graph Query
 +-- Git Query
 |
Context Builder
 |
Minimal relevant context
```

## 7. MCP Gateway

The Factory SHALL expose an MCP-compatible external management boundary.

Initial logical MCP capabilities:

```text
PROJECT
get_project_status
get_project_progress
get_current_phase
get_methodology_state
get_milestones
get_blockers
get_recent_activity
get_project_health

TASK
list_tasks
search_tasks
get_task
get_task_state
get_task_summary
get_task_dependencies
get_task_history
create_task
update_task
split_task
change_task_priority
block_task
reopen_task
assign_task
unassign_task
request_task_execution
retry_task
cancel_task

WORKER
list_workers
get_worker_status
get_worker_capabilities
get_running_tasks
get_worker_activity

DEVELOPMENT
get_git_status
get_task_diff
get_build_status
get_test_results
get_integration_status
request_bug_fix
request_small_change

KNOWLEDGE
search_project_knowledge
read_requirement
read_analysis
read_design
read_adr
read_task_artifact
get_decision_history

QUALITY
get_code_review_status
get_qa_status
get_security_status
get_regression_status

RELEASE / DEPLOYMENT
get_release_status
get_deployment_status
request_release
request_deployment
```

Exact MCP schemas remain a Technical Design TBD.

## 8. Permission model

Suggested permission scopes:

```text
project:read
knowledge:read

task:read
task:create
task:update
task:assign
task:execute
task:cancel

worker:read

code:read
change:request

qa:read
security:read

release:read
release:request
release:approve

deploy:read
deploy:request
deploy:execute

architecture:read
architecture:change_request
architecture:approve
```

Recommended default PEAA policy:

```text
Project-wide authorized read     ALLOW
Create/update Task               ALLOW
Assign/reprioritize Task         ALLOW
Request Task execution           ALLOW
Request small fix                ALLOW
Read source/diff/test            ALLOW

Architecture baseline approval   OWNER APPROVAL
Security exception               OWNER APPROVAL
Release approval                 OWNER APPROVAL
Production deployment            OWNER APPROVAL
Destructive project operation    DENY / OWNER-ONLY
Permission escalation            DENY / OWNER-ONLY
```

Policies SHALL be configurable per project.

## 9. Owner approval boundary

The Owner remains final authority.

PEAA SHALL clearly identify the exact item requiring approval and SHALL NOT interpret silence as approval.

Example:

```text
OWNER CONFIRMATION REQUIRED

Action:
Deploy RELEASE-2026.10.1 to Production

Validated:
- QA passed
- Security passed
- Regression passed

Awaiting:
Owner approval
```

## 10. PEAA task assignment

PEAA may reason using:

- priority;
- dependencies;
- Capability requirements;
- Worker availability and health;
- context requirements;
- cost;
- quality;
- latency;
- security;
- methodology;
- current project goals.

PEAA decides assignment intent.

The Model Router normally selects the concrete eligible Worker/model.

Example:

```text
TASK-021
Required Capability: backend_development

PEAA:
request execution

Task Management Engine:
validate

Model Router:
select Gemini Worker

Execution Role:
Backend Developer
```

The V0.4 principle remains:

> **Worker != Role != Capability != Model**

The same Worker may perform BA, Architect, Developer, Test, QA, or Review roles when its capabilities and policy allow it.

Multi-model deployment is optional, not mandatory.

## 11. Fast Fix

A small change SHALL still be traceable.

```text
Owner
 |
"Change timeout from 30s to 60s"
 |
PEAA impact check
 |
Lightweight Task
 |
Engine validation
 |
Model Router
 |
Developer Worker
 |
Relevant Test
 |
Git Diff / Review Policy
 |
state.md + summary.md
 |
PEAA reports result
```

Fast Fix SHALL preserve at minimum:

- Task identity;
- request origin;
- files changed;
- test evidence;
- Task state;
- Task summary;
- Git traceability;
- audit event.

Fast Fix SHALL NOT mean untracked direct source modification.

## 12. Task splitting and replanning

PEAA may split oversized Tasks.

Example:

```text
TASK-100 Implement Authentication
```

may become:

```text
TASK-101 User Model
TASK-102 Password Authentication
TASK-103 JWT Service
TASK-104 Login API
TASK-105 Authorization Middleware
TASK-106 Authentication Tests
```

Dependency and Task engines validate/persist the new graph.

Material scope or approved architecture changes may require Owner approval.

## 13. Project Monitor remains

Project Monitor is NOT replaced by PEAA.

It observes and calculates:

- Task state distribution;
- blockers/stuck Tasks;
- Worker utilization;
- throughput;
- cycle time;
- Sprint progress;
- Kanban WIP;
- Waterfall gates;
- milestones;
- test/build health;
- release readiness;
- token/cost usage;
- failure trends.

Separation:

```text
Project Monitor = observes/measures
PEAA            = reasons/advises/manages
Engines         = validate/enforce
Workers         = execute
```

## 14. Methodology integration

PEAA SHALL understand the active Methodology Context.

The Methodology Engine remains internal and deterministic/configuration-driven.

Scrum:
- inspect Sprint;
- manage READY Sprint Tasks;
- explain blockers;
- recommend scope changes.

Kanban:
- inspect WIP;
- select pullable work;
- respect WIP limits;
- identify bottlenecks.

Waterfall:
- inspect phase/gates;
- avoid prohibited downstream work;
- identify missing approvals.

Hybrid:
- respect methodology policy per workstream.

Methodology SHALL NOT directly select a model provider.

Core Task State and Methodology State remain separate.

## 15. Event-driven state and audit

PEAA actions may emit events:

```text
PEAA_TASK_CREATED
PEAA_TASK_UPDATED
PEAA_TASK_ASSIGNED
PEAA_PRIORITY_CHANGED
PEAA_EXECUTION_REQUESTED
```

Worker events remain, including:

```text
TASK_STARTED
FILE_CREATED
FILE_MODIFIED
TEST_STARTED
TEST_FAILED
TEST_PASSED
QUESTION_CREATED
BLOCKED
IMPLEMENTATION_COMPLETED
TASK_COMPLETED
```

State SHALL be validated/derived from accepted events, not from an LLM merely claiming DONE.

State-changing MCP requests SHOULD record:

```text
Timestamp
Project
Actor
External Client
PEAA Session/Request ID
Action
Target
Previous State
Requested State
Validation Result
Approval Reference
Execution Result
Related Task
Related Git Commit/Diff
```

## 16. Security

Project-wide PEAA access does not imply unrestricted secret access.

The MCP Gateway / Context Manager SHALL enforce relevant controls before returning protected context or executing actions, including:

- project membership;
- permission scopes;
- artifact classification;
- secret filtering;
- credential redaction;
- environment isolation;
- audit logging;
- protected branch policy;
- tenant isolation where applicable.

## 17. Updated responsibility matrix

| Component | Responsibility |
|---|---|
| Owner | Final authority / high-risk approval |
| PEAA | Advisor + PM + Task Manager + Planner + Dispatcher |
| MCP Gateway | External AI control boundary |
| Project Monitor | Project observation and metrics |
| Task Management Engine | Validate/apply Task operations |
| Dependency Engine | Enforce dependencies |
| State Engine | Enforce state transitions |
| Methodology Engine | Enforce process policy |
| Permission Engine | Authorize operations |
| Context Manager | Retrieve minimal relevant context |
| Model Router | Select eligible Worker/model |
| Worker | Execute a Role for a Task |
| Git | Source of truth for code |
| Markdown | Primary human/Agent project knowledge |
| Runtime DB | Runtime/index/orchestration state as required |

## 18. Updated runtime flow

```text
USER IDEA
 |
REQUIREMENT
 |
REQUIREMENT VALIDATION
 |
OWNER/PO APPROVAL
 |
BUSINESS ANALYSIS
 |
UI/UX
 |
SYSTEM DESIGN
 |
DETAILED DESIGN
 |
ARCHITECTURE REVIEW
 |
TASK PLANNING
 |
TASK ESTIMATION
 |
DEPENDENCY GRAPH
 |
METHODOLOGY POLICY
 |
READY TASKS
 |
PEAA requests assignment/execution
 |
TASK MANAGEMENT ENGINE VALIDATES
 |
MODEL ROUTER
 |
WORKER + ROLE + CONTEXT + PERMISSION
 |
IMPLEMENTATION
 |
TASK STATE + SUMMARY
 |
CODE REVIEW
 |
INTEGRATION
 |
INTEGRATION TEST
 |
QA
 |
BUG / FIX / REGRESSION
 |
SECURITY REVIEW
 |
RELEASE
 |
OWNER APPROVAL WHERE REQUIRED
 |
DEPLOY
 |
HEALTH CHECK
 |
POST-DEPLOY MONITORING
 |
PROJECT COMPLETE
```

## 19. Artifact additions

V0.5 adds/recommends:

```text
/project
├── agents/
│   ├── agent-registry.md
│   ├── capability-registry.md
│   ├── routing-policy.md
│   ├── peaa-policy.md
│   └── role-definitions/
├── methodology/
│   ├── profile.md
│   └── state.md
├── audit/
│   └── management-events.md
└── ...
```

Existing Task artifact structure remains:

```text
TASK-XXX/
├── task.md
├── implementation-plan.md
├── state.md
├── summary.md
├── questions.md
└── log.md
```

## 20. Updated logical engines/services

1. Requirement Engine
2. Requirement Validation Engine
3. Analysis Engine
4. UI/UX Engine
5. Design Engine
6. Architecture Review Engine
7. Task Planning Engine
8. Task Management Engine
9. Dependency Engine
10. Scheduling/Batch Engine
11. Agent Execution Engine
12. Context Management Engine
13. State Management Engine
14. Methodology Engine
15. Integration Engine
16. QA Engine
17. Security Engine
18. Release Engine
19. Deployment Engine
20. Knowledge/Decision Engine
21. Project Monitoring Engine
22. Token/Cost Engine
23. Permission/Policy Engine
24. MCP Gateway
25. Audit Service

PEAA is an external Agent role/control-plane participant rather than a required internal Engine.

## 21. V0.5 NFR additions

- **NFR-PEAA-01 External Client Independence:** Factory is not coupled to one PEAA provider.
- **NFR-PEAA-02 Project-Wide Visibility:** PEAA can query all authorized project domains.
- **NFR-PEAA-03 Least Context:** full visibility does not require full-project prompt injection.
- **NFR-PEAA-04 Engine Validation:** state-changing PEAA operations pass deterministic validation.
- **NFR-PEAA-05 No Worker Bypass:** PEAA cannot bypass project-control engines.
- **NFR-PEAA-06 Auditability:** state-changing PEAA operations are auditable.
- **NFR-PEAA-07 Approval Safety:** Owner-only actions require explicit approval.
- **NFR-PEAA-08 Provider Replaceability:** PEAA provider can change without workflow redesign.
- **NFR-PEAA-09 Fast Fix Traceability:** Fast Fix remains Task/test/state/Git traceable.
- **NFR-PEAA-10 Current-State Grounding:** project status comes from current Factory state.
- **NFR-PEAA-11 Failure Isolation:** PEAA disconnection cannot corrupt Factory state.
- **NFR-PEAA-12 Permission Enforcement:** MCP capabilities obey project security policy.

## 22. V0.5 acceptance criteria

- [ ] MCP-compatible external AI client can connect.
- [ ] PEAA can retrieve project status and blockers.
- [ ] PEAA can inspect Task state/summary/dependencies.
- [ ] PEAA can search authorized project knowledge.
- [ ] PEAA can create/update/reprioritize Tasks.
- [ ] PEAA can request assignment and execution.
- [ ] Invalid dependencies are rejected.
- [ ] Invalid state transitions are rejected.
- [ ] Unauthorized actions are rejected.
- [ ] Owner-only actions require explicit approval.
- [ ] PEAA cannot bypass Task Management Engine for managed changes.
- [ ] Router selects Workers by Capability.
- [ ] One Worker can perform multiple Roles when permitted.
- [ ] Multiple Workers can provide the same Capability.
- [ ] ChatGPT/Claude/Gemini can be swapped as PEAA without Factory workflow redesign.
- [ ] Fast Fix creates a traceable lightweight Task.
- [ ] Delegated work updates state.md and summary.md.
- [ ] State-changing MCP operations create audit records.
- [ ] Project Monitor remains separate from PEAA.
- [ ] Methodology rules remain Engine-enforced.
- [ ] Git remains source of truth for code.
- [ ] Markdown remains primary project knowledge.
- [ ] No autonomous Task Manager Agent is required.

## 23. Recommended V0.5 MVP order

### Phase 1 — Core State
Project, Task, state, events, dependency DAG, Markdown repository, Git integration.

### Phase 2 — Execution Core
Worker, Role, Capability Registry, Agent Registry, Model Router, Context Manager, execution lifecycle.

### Phase 3 — Task Management Engine
State/dependency validation, assignment, execution requests, retry, block/reopen, concurrency controls.

### Phase 4 — MCP Gateway + PEAA
Initial tools:

```text
get_project_status
get_blockers
list_tasks
get_task
get_task_state
get_task_summary
search_project_knowledge
create_task
update_task
assign_task
request_task_execution
get_test_results
get_git_status
```

### Phase 5 — Fast Fix
Owner -> PEAA -> lightweight Task -> validation -> Worker -> test -> Git -> summary.

### Phase 6 — Methodologies
Scrum -> Kanban -> Waterfall -> Hybrid -> Custom.

### Phase 7 — Quality and Delivery
Review -> Integration -> QA -> Security -> Release -> Deployment -> Monitoring.

### Phase 8 — Governance
Owner approvals, permission scopes, audit, cost policies, security boundaries, multi-project support.

## 24. First vertical slice

```text
Requirement Markdown
      |
Create Tasks
      |
PEAA asks project status through MCP
      |
PEAA selects READY Task
      |
PEAA requests assignment/execution
      |
Task Management Engine validates
      |
Model Router selects Worker
      |
Worker reads relevant context
      |
implementation-plan.md
      |
Code
      |
Test
      |
state.md + summary.md
      |
Git
      |
PEAA reads result through MCP
      |
Owner receives current status
```

## 25. Technical Design TBDs

Still unresolved and SHALL NOT be silently assumed:

- MCP transport/deployment topology;
- MCP authentication;
- exact MCP schemas;
- PEAA session identity;
- approval workflow/token;
- runtime database;
- queue/event bus;
- LangGraph state schema;
- event persistence;
- Git branch/worktree strategy;
- sandbox design;
- file locking/merge strategy;
- project search/vector implementation;
- summary generation;
- cost accounting;
- routing scoring;
- Worker health scoring;
- retry/fallback policy;
- secret management;
- multi-project isolation;
- multi-tenant architecture;
- dashboard;
- production infrastructure.

## 26. V0.5 core principles

1. Owner is final authority.
2. PEAA is the Owner-facing project executive and advisor.
3. PEAA replaces the autonomous Task Manager Agent.
4. Task Management Engine remains deterministic/internal.
5. **LLM decides; Engine validates; Worker executes.**
6. PEAA must not bypass Factory controls.
7. PEAA may access the complete authorized project while Context Manager retrieves only relevant context.
8. PEAA may create/edit/split/prioritize/assign/block/reopen/request execution according to policy.
9. High-risk actions require explicit Owner approval when configured.
10. Project Monitor observes; PEAA reasons/manages.
11. Worker != Role != Capability != Model.
12. Tasks request Capability, not hard-coded model.
13. Model Router selects eligible Workers/models.
14. One Worker may perform multiple Roles.
15. Multiple Workers may provide one Capability.
16. PEAA may run through ChatGPT, Claude, Gemini or future compatible clients.
17. MCP is the external AI control boundary.
18. Core remains methodology-agnostic.
19. Methodology controls process, not model selection.
20. Core Task State remains separate from Methodology State.
21. Markdown remains primary human/Agent project knowledge.
22. Git remains source of truth for code.
23. Agents continuously update Task state during execution.
24. Task Summary remains a living handoff artifact.
25. Independent Tasks may be batched/parallelized.
26. Fast Fix never means untracked modification.
27. Security/permissions are checked before protected context/actions.
28. State-changing management actions are auditable.
29. Models are replaceable without redesigning the Factory.
30. Methodologies are addable without redesigning Core.

## 27. V0.5 vision

The AI Software Factory is a model-agnostic, methodology-agnostic software engineering operating system.

The Owner manages the AI software organization conversationally through PEAA. PEAA understands project-wide state through MCP, advises the Owner, manages Tasks and requests work. Deterministic Engines protect workflow correctness. Model Router selects appropriate execution Workers. Workers perform specialized Roles. Markdown preserves shared project knowledge, Git preserves source-code truth, and state/events/tests/reviews/security/releases/deployments remain traceable.

```text
Owner: "Where are we?"
PEAA: reads current Factory state and explains it.

Owner: "Continue the important backend work."
PEAA: analyzes priority/dependencies and requests valid execution.
Factory: validates and routes work.
Workers: implement/test/review and update state.

Owner: "Fix this small issue."
PEAA: creates a traceable Fast Fix, delegates it through the Factory,
and reports the verified result.
```

---

# END OF V0.5 AUTHORITATIVE UPDATE


---

# V0.6 — FULL PRODUCT / PROJECT / RELEASE / MAINTENANCE LIFECYCLE
## Authoritative Lifecycle Architecture Update

> All V0.5 requirements remain valid unless explicitly superseded by this V0.6 section.
>
> V0.6 corrects an important lifecycle boundary: **delivery completion or project closure does not mean the software/product lifecycle is complete.**

---

## 1. V0.6 Executive Summary

V0.6 expands the AI Software Factory from a software-delivery system into a **full software/product lifecycle management system**.

The Factory SHALL support the lifecycle from:

```text
IDEA
  |
PRODUCT
  |
PROJECT / CHANGE INITIATIVE
  |
REQUIREMENT
  |
ANALYSIS / DESIGN
  |
IMPLEMENTATION
  |
QA / SECURITY / ACCEPTANCE
  |
RELEASE
  |
DEPLOYMENT
  |
PRODUCTION
  |
OPERATIONS & MAINTENANCE
  |
  +--> INCIDENT / BUG FIX
  +--> CORRECTIVE MAINTENANCE
  +--> ADAPTIVE MAINTENANCE
  +--> PERFECTIVE MAINTENANCE
  +--> PREVENTIVE MAINTENANCE
  +--> ENHANCEMENT / NEW FEATURE
  +--> UPGRADE / MIGRATION
  +--> OPTIMIZATION / TECHNICAL DEBT
  |
NEW RELEASE / NEW PROJECT WHEN NEEDED
  |
PRODUCTION
  |
  +-----------------------------+
  |                             |
  +---------- EVOLUTION LOOP ---+
  |
END-OF-LIFE DECISION
  |
DEPRECATION
  |
END OF SUPPORT
  |
DATA MIGRATION / ARCHIVE
  |
DECOMMISSION
  |
PRODUCT LIFECYCLE COMPLETE
```

A Project may be completed and closed while its Product remains active in Production.

---

# PART I — CORE DOMAIN MODEL

## 2. Product, Project, Release and Maintenance Are Different Concepts

### 2.1 Product

A **Product** is the long-lived software system or software offering being built, operated and evolved.

Examples:

```text
Product: Access Control System
Product: School Management Platform
Product: E-Commerce Platform
```

A Product may exist for many years and may contain multiple Projects and Releases.

### 2.2 Project

A **Project** is a finite delivery/change initiative with defined scope, objectives and lifecycle.

Examples:

```text
Project P001 — Initial MVP
Project P002 — Mobile Application
Project P003 — Authentication Architecture Migration
Project P004 — Version 3 Major Upgrade
```

A Product can have zero, one or many Projects over its lifetime.

### 2.3 Release

A **Release** is a versioned, deployable product increment.

Examples:

```text
v1.0.0
v1.0.1
v1.1.0
v2.0.0
```

A Release may originate from:

- a Project;
- a Maintenance Task or maintenance batch;
- an Enhancement;
- an Upgrade/Migration;
- an Incident/Bug Fix.

### 2.4 Maintenance

Maintenance is ongoing work performed after a Product enters operational use.

Maintenance does NOT automatically require reopening the original delivery Project.

### 2.5 Core Relationship

```text
PRODUCT
  |
  +-- Project P001 — Initial Development
  |       |
  |       +-- Release v1.0.0
  |       |
  |       +-- CLOSED
  |
  +-- Maintenance
  |       |
  |       +-- Bug Fix -> v1.0.1
  |       +-- Security Fix -> v1.0.2
  |
  +-- Project P002 — Major Upgrade
  |       |
  |       +-- Release v2.0.0
  |       |
  |       +-- CLOSED
  |
  +-- Maintenance / Evolution continues
```

Therefore:

> **Product lifetime > Project lifetime**

and:

> **Project Delivery Complete != Product Lifecycle Complete**

---

# PART II — PRODUCT LIFECYCLE

## 3. Product Lifecycle States

Reference Product states:

```text
CONCEPT
  |
ACTIVE_DEVELOPMENT
  |
PRODUCTION
  |
MAINTENANCE
  |
DEPRECATED
  |
END_OF_SUPPORT
  |
DECOMMISSIONING
  |
DECOMMISSIONED
```

A Product may move between `PRODUCTION` and `MAINTENANCE` operational modes repeatedly.

Exact state representation may be refined in Technical Design.

## 4. Product Lifecycle Completion

The following SHALL NOT mean Product completion:

- Project completed;
- Project closed;
- Release accepted;
- Release deployed;
- UAT accepted.

The Product lifecycle is considered complete only after an approved End-of-Life/Decommission process reaches:

```text
DECOMMISSIONED
```

---

# PART III — PROJECT LIFECYCLE

## 5. Project State Model

V0.6 defines the reference Project states:

```text
DRAFT
  |
PLANNING
  |
ACTIVE
  |
DELIVERY
  |
ACCEPTANCE
  |
COMPLETED
  |
CLOSED
```

Additional states/transitions:

```text
ACTIVE <------> ON_HOLD

CLOSED
  |
REOPENING
  |
ACTIVE

DRAFT / PLANNING / ACTIVE / ON_HOLD
  |
CANCELLED
```

A project MAY also be archived after closure according to retention policy.

## 6. Meaning of Project States

### DRAFT

Project exists but scope and execution baseline are not approved.

### PLANNING

Requirements, analysis, estimates, architecture, Task planning, methodology and execution plan are being prepared.

### ACTIVE

Approved project work is actively executing.

### ON_HOLD

Execution is intentionally paused.

Tasks SHALL NOT automatically continue unless policy explicitly permits specific maintenance/administrative operations.

### DELIVERY

The planned scope is substantially implemented and the Project is moving through final integration, QA, security, release preparation and delivery.

### ACCEPTANCE

The delivered scope is undergoing UAT/Owner/Customer acceptance.

### COMPLETED

The approved Project scope has been delivered and accepted.

`COMPLETED` does NOT yet mean administratively closed.

### CLOSED

Closure checks, handover, known-issue recording and required approvals have completed.

Normal Project execution is disabled unless the Project is reopened.

### REOPENING

The Factory is re-baselining a previously CLOSED Project before returning it to ACTIVE.

### CANCELLED

The Project was intentionally terminated before normal completion.

Cancellation SHALL preserve audit history and artifacts.

---

# PART IV — PROJECT CLOSURE

## 7. Close Project Capability

The Factory SHALL provide a controlled Project Closure workflow.

A Project SHALL NOT become CLOSED merely because all coding Tasks are DONE.

Reference flow:

```text
COMPLETED
   |
Request Project Closure
   |
PEAA Pre-Closure Review
   |
Closure Validation
   |
Closure Report
   |
OWNER APPROVAL
   |
CLOSED
```

## 8. Pre-Closure Checks

PEAA and the relevant Engines SHOULD evaluate at minimum:

```text
Scope delivered?
Acceptance/UAT completed?
All required Tasks DONE/CANCELLED?
Open blockers documented?
Open bugs documented?
Known limitations documented?
QA status recorded?
Security status recorded?
Release status recorded?
Production/deployment status known?
Documentation completed?
ADRs current?
Technical debt recorded?
Operational ownership defined?
Maintenance handover completed?
Monitoring/runbook available where required?
Rollback/recovery information recorded?
Outstanding approvals resolved?
```

Project policy determines which checks are mandatory.

## 9. Closure Report

The Factory SHALL generate or maintain a Project Closure Report.

Suggested content:

```text
Project
Product
Project Objective
Final Scope
Acceptance Result
Final Release(s)
Deployment Result
Completed Tasks
Cancelled Tasks
Open/Known Issues
Known Limitations
Technical Debt
Security Status
Operational Handover
Maintenance Handover
Important ADRs
Final Cost / Token Usage
Lessons / Retrospective
Follow-up Recommendations
Closure Approval
Closure Date
```

## 10. Close With Known Issues

Projects MAY support:

```text
CLOSE_WITH_KNOWN_ISSUES
```

only when project policy allows it.

Known issues SHALL be explicitly recorded.

High-risk unresolved items may require Owner approval.

PEAA SHALL identify the exact unresolved items before requesting closure approval.

## 11. Closed Project Behavior

When a Project is CLOSED:

- normal Task execution SHALL be disabled;
- historical artifacts remain readable according to permission;
- audit history remains preserved;
- Git history remains preserved;
- project summaries remain queryable;
- PEAA may inspect the Project;
- maintenance work for the Product may continue separately;
- reopening requires the Reopen Project workflow.

---

# PART V — REOPEN PROJECT

## 12. Reopen Project Capability

The Factory SHALL support reopening a CLOSED Project.

Reference flow:

```text
CLOSED
  |
REOPEN REQUEST
  |
PEAA analyzes reason
  |
Change Classification
  |
Re-Baseline / Impact Analysis
  |
OWNER APPROVAL where required
  |
REOPENING
  |
Refresh Project Context
  |
Create/Reopen Tasks
  |
ACTIVE
```

## 13. Re-Baseline Before Reopening

A Project may have been closed for months or years.

Before execution resumes, the Factory SHOULD reassess:

```text
Current source/Git baseline
Current production version
Current requirements
Architecture changes
ADRs since closure
Dependency versions
Framework versions
Database/schema state
Infrastructure state
External APIs
Security requirements
Known incidents/bugs
Open maintenance changes
Environment configuration
Tests and CI/CD
Worker/Capability availability
Methodology/project policy
```

Reopening SHALL NOT blindly reuse stale execution context.

## 14. Reopen vs Maintenance vs New Project

PEAA SHALL advise the Owner which path best matches the requested change.

### Prefer Maintenance Task when:

- change is small/localized;
- bug fix;
- patch;
- minor dependency update;
- low-risk optimization;
- operational correction;
- small security fix;
- no major scope/architecture change.

### Consider Reopening Existing Project when:

- unfinished work directly belongs to the original Project scope;
- acceptance discovered a material omission tied to that Project;
- closure occurred prematurely;
- Project-specific contractual/scope reasons require continuing the same initiative.

### Prefer New Project when:

- major new feature set;
- major architecture change;
- large migration;
- major version upgrade;
- substantial scope change;
- new application/channel/platform;
- work needs independent budget, schedule or governance.

PEAA SHALL present its reasoning, but the Owner may choose a different permitted path.

---

# PART VI — PROJECT CANCEL AND ARCHIVE

## 15. Cancel Project

The Factory SHALL support controlled Project cancellation.

Reference:

```text
DRAFT / PLANNING / ACTIVE / ON_HOLD
  |
CANCEL REQUEST
  |
Impact Review
  |
OWNER APPROVAL where required
  |
Stop/Safely Terminate Execution
  |
Record Partial Outputs
  |
Cancellation Report
  |
CANCELLED
```

Cancellation SHALL NOT delete project history.

## 16. Archive Project

Archive is a storage/visibility lifecycle operation, not equivalent to deletion.

An archived Project SHOULD:

- remain historically queryable;
- preserve artifacts and audit;
- be excluded from normal active dashboards by default;
- remain linked to Product and Releases;
- require explicit restoration/unarchive before management changes where policy requires.

Exact archival implementation is TBD.

---

# PART VII — RELEASE LIFECYCLE

## 17. Release Lifecycle

Reference Release lifecycle:

```text
PLANNED
  |
BUILDING
  |
VALIDATING
  |
READY_FOR_RELEASE
  |
APPROVED
  |
DEPLOYING
  |
DEPLOYED
  |
POST_DEPLOY_VERIFICATION
  |
ACCEPTED
```

Additional outcomes may include:

```text
REJECTED
ROLLED_BACK
SUPERSEDED
RETIRED
```

Exact state machine SHALL be finalized in Technical Design.

## 18. Release Does Not Close Product

After:

```text
RELEASE ACCEPTED
```

the Product enters or continues Production/Operations.

The Project that created the Release may proceed toward COMPLETED/CLOSED independently.

---

# PART VIII — OPERATIONS & MAINTENANCE

## 19. Operations Phase

After production deployment, the Factory SHALL support ongoing operational visibility.

Possible operational concerns include:

- service health;
- availability;
- errors;
- performance;
- logs;
- alerts;
- deployment status;
- infrastructure health;
- capacity;
- security signals;
- backup/restore status;
- external dependency health;
- cost.

Integration with external monitoring platforms is implementation-specific and may be added through tools/connectors.

## 20. Maintenance Categories

The Factory SHALL support at least the following maintenance classifications.

### 20.1 Corrective Maintenance

Fix defects found after delivery.

```text
Production Bug
  |
Triage
  |
Impact / Severity
  |
Maintenance Task
  |
Fix
  |
Test
  |
Regression
  |
Release Patch
  |
Production
```

### 20.2 Adaptive Maintenance

Adapt software to environmental changes.

Examples:

- operating system changes;
- database upgrades;
- external API changes;
- cloud/infrastructure changes;
- framework/runtime changes;
- regulatory/compatibility changes.

### 20.3 Perfective Maintenance

Improve existing software without primarily correcting a defect.

Examples:

- performance optimization;
- UX improvement;
- code quality;
- scalability;
- maintainability;
- cost optimization.

### 20.4 Preventive Maintenance

Reduce future failure/risk.

Examples:

- dependency updates;
- refactoring fragile code;
- improving test coverage;
- addressing technical debt;
- replacing deprecated APIs;
- strengthening monitoring.

---

# PART IX — INCIDENT AND BUG MANAGEMENT

## 21. Incident Lifecycle

Reference flow:

```text
Incident Detected
  |
Record Incident
  |
Severity / Impact Assessment
  |
Contain / Mitigate
  |
Root Cause Analysis
  |
Create Bug / Change Tasks
  |
Fix
  |
Test / Regression
  |
Release / Deploy
  |
Verify
  |
Incident Resolution
  |
Post-Incident Review when required
```

PEAA may assist the Owner by explaining impact, current mitigation and repair progress.

Critical production actions remain subject to permissions and approval policy.

## 22. Bug Lifecycle

A production Bug SHOULD be linked to:

- affected Product;
- affected Release/version;
- environment;
- severity;
- reproduction evidence;
- related Incident when applicable;
- fix Task(s);
- regression tests;
- fixing Release.

---

# PART X — ENHANCEMENT AND PRODUCT EVOLUTION

## 23. Enhancement / New Feature

New feature requests SHALL enter a change-classification process.

Reference:

```text
New Requirement
  |
PEAA Change Classification
  |
Impact Analysis
  |
Choose:
  +-- Maintenance/Enhancement Task
  +-- Reopen Project
  +-- Create New Project
  |
Requirement / BA as required
  |
Design Change as required
  |
Task Planning
  |
Implementation
  |
QA / Security
  |
Release
  |
Production
```

The Factory SHALL avoid forcing every small enhancement through the full initial-project lifecycle when a lighter approved workflow is appropriate.

---

# PART XI — UPGRADE AND MIGRATION

## 24. Upgrade/Migration Workflow

Major upgrades or migrations SHOULD use:

```text
Upgrade / Migration Request
  |
Impact Analysis
  |
Compatibility Analysis
  |
Risk Assessment
  |
Migration Strategy
  |
Rollback Strategy
  |
Project or Change Plan
  |
Implementation
  |
Compatibility Test
  |
Regression
  |
Migration
  |
Verification
  |
Release / Production
```

Examples:

- framework major version;
- database engine/version;
- cloud migration;
- monolith-to-services migration;
- authentication architecture migration;
- API version migration.

Large upgrades SHOULD normally become a new Project.

---

# PART XII — TECHNICAL DEBT AND OPTIMIZATION

## 25. Technical Debt

The Factory SHALL allow technical debt items to be recorded and prioritized.

A technical debt item SHOULD include:

```text
Description
Origin
Impact
Risk
Affected Components
Recommended Action
Estimated Effort
Priority
Related ADR/Task
Target Release/Project
```

PEAA may recommend creating preventive/perfective maintenance Tasks or a dedicated improvement Project.

---

# PART XIII — CHANGE CLASSIFICATION ENGINE / POLICY

## 26. Change Classification

V0.6 introduces a logical **Change Classification capability**.

It may initially be implemented through PEAA reasoning plus deterministic policy rather than as a separate autonomous Agent.

Inputs may include:

```text
Change description
Affected Product
Affected Release
Scope
Risk
Architecture impact
Database impact
Security impact
Compatibility impact
Estimated effort
Urgency
Dependencies
Operational impact
```

Possible classifications:

```text
INCIDENT
BUG
FAST_FIX
CORRECTIVE_MAINTENANCE
ADAPTIVE_MAINTENANCE
PERFECTIVE_MAINTENANCE
PREVENTIVE_MAINTENANCE
ENHANCEMENT
UPGRADE
MIGRATION
MAJOR_CHANGE
```

Output SHOULD recommend one of:

```text
Create Maintenance Task
Create Maintenance Batch
Reopen Existing Project
Create New Project
Reject / Need More Information
```

Engine/policy validation remains required for state-changing actions.

---

# PART XIV — PEAA RESPONSIBILITIES AFTER DELIVERY

## 27. PEAA Continues After Project Delivery

PEAA SHALL remain useful after a Project is accepted/closed.

Owner questions may include:

```text
How is Production doing?
What incidents are open?
What bugs are waiting?
Which dependencies need upgrades?
What technical debt is highest risk?
What maintenance should we prioritize?
Should this request be a maintenance Task or a new Project?
Should we reopen P001?
What changed since v1.0?
What Release contains this fix?
Is the Product ready for end-of-life?
```

PEAA SHALL use current Factory/Product state and available operational data.

## 28. PEAA Change Recommendation

Example:

```text
Owner:
"Login has a timeout bug."

PEAA:
Classification: Corrective Maintenance
Recommendation: Create Maintenance Task
Reason: localized defect, no architecture impact.
```

Example:

```text
Owner:
"Replace the complete authentication architecture."

PEAA:
Classification: Major Change / Migration
Recommendation: Create New Project
Reason:
- architecture baseline changes;
- multiple components affected;
- security review required;
- migration and rollback plan required.
```

---

# PART XV — UPDATED END-TO-END FACTORY LIFECYCLE

## 29. Authoritative V0.6 Lifecycle

Any older lifecycle ending directly in `PROJECT COMPLETE` after post-deployment monitoring is superseded by this model:

```text
IDEA
 |
PRODUCT CONCEPT
 |
PROJECT CREATION
 |
REQUIREMENT
 |
REQUIREMENT VALIDATION
 |
OWNER / PO APPROVAL
 |
BUSINESS ANALYSIS
 |
UI/UX
 |
SYSTEM DESIGN
 |
DETAILED DESIGN
 |
ARCHITECTURE REVIEW
 |
TASK PLANNING
 |
TASK ESTIMATION
 |
DEPENDENCY GRAPH
 |
METHODOLOGY POLICY
 |
PEAA MANAGEMENT / EXECUTION REQUESTS
 |
TASK MANAGEMENT ENGINE VALIDATION
 |
MODEL ROUTER
 |
WORKERS
 |
IMPLEMENTATION
 |
REVIEW / INTEGRATION
 |
TEST / QA / SECURITY
 |
ACCEPTANCE / UAT
 |
RELEASE
 |
DEPLOY
 |
POST-DEPLOY VERIFICATION
 |
RELEASE ACCEPTED
 |
PROJECT SCOPE COMPLETED
 |
PROJECT CLOSURE
 |
PROJECT CLOSED
 |
+---------------------------------------------------+
| PRODUCT CONTINUES                                 |
|                                                   |
| PRODUCTION / OPERATIONS                           |
|        |                                          |
|        +-- Incident                               |
|        +-- Bug / Corrective Maintenance           |
|        +-- Adaptive Maintenance                   |
|        +-- Perfective Maintenance                 |
|        +-- Preventive Maintenance                 |
|        +-- Enhancement                            |
|        +-- Upgrade / Migration                    |
|        +-- Technical Debt / Optimization          |
|                   |                               |
|                   v                               |
|       Maintenance Task / Reopen / New Project     |
|                   |                               |
|                   v                               |
|              NEW RELEASE                          |
|                   |                               |
|                   v                               |
|              PRODUCTION                           |
|                   |                               |
+-------------------+-------------------------------+
                    |
             END-OF-LIFE DECISION
                    |
                DEPRECATION
                    |
              END OF SUPPORT
                    |
          MIGRATION / DATA ARCHIVE
                    |
              DECOMMISSION
                    |
        PRODUCT LIFECYCLE COMPLETE
```

---

# PART XVI — PRODUCT / PROJECT / RELEASE TRACEABILITY

## 30. Traceability Requirements

The Factory SHALL preserve traceability among:

```text
Product
  |
Project
  |
Requirement
  |
Design / ADR
  |
Task
  |
Code Change / Commit
  |
Test
  |
Release
  |
Deployment
  |
Incident / Bug / Maintenance Change
```

A maintenance fix SHOULD be traceable back to the Product and affected Release even when no Project is reopened.

---

# PART XVII — ARTIFACT STRUCTURE ADDITIONS

## 31. Suggested V0.6 Artifact Structure

```text
/product
├── product.md
├── lifecycle.md
├── roadmap.md
├── releases/
│   ├── v1.0.0/
│   │   ├── release.md
│   │   ├── changelog.md
│   │   └── deployment.md
│   └── ...
├── operations/
│   ├── operational-status.md
│   ├── incidents/
│   └── runbooks/
├── maintenance/
│   ├── maintenance-backlog.md
│   ├── technical-debt.md
│   └── changes/
├── projects/
│   ├── P001/
│   │   ├── project.md
│   │   ├── closure-report.md
│   │   └── ...
│   └── P002/
└── eol/
    ├── eol-plan.md
    └── decommission-report.md
```

Existing project/task artifacts remain valid.

Logical storage layout may differ from physical Git repository layout and SHALL be finalized in Technical Design.

---

# PART XVIII — MCP CAPABILITY ADDITIONS

## 32. Product Lifecycle MCP Capabilities

V0.6 SHOULD add logical MCP operations such as:

```text
PRODUCT
get_product
get_product_status
get_product_roadmap
get_product_releases
get_product_maintenance_status

PROJECT LIFECYCLE
request_project_completion
get_project_closure_readiness
close_project
request_reopen_project
reopen_project
cancel_project
archive_project
unarchive_project

MAINTENANCE
list_maintenance_items
create_maintenance_task
classify_change
request_fast_fix
get_technical_debt

INCIDENT
list_incidents
get_incident
create_incident
request_incident_fix

RELEASE
list_releases
get_release
get_release_traceability

EOL
get_eol_readiness
request_product_deprecation
request_end_of_support
request_decommission
```

Exact schemas remain TBD.

---

# PART XIX — PERMISSIONS AND APPROVAL ADDITIONS

## 33. Suggested Additional Scopes

```text
product:read
product:update

project:close
project:reopen
project:cancel
project:archive

maintenance:read
maintenance:create
maintenance:execute

incident:read
incident:create
incident:manage

eol:read
eol:request
eol:approve
decommission:execute
```

Recommended defaults:

```text
Create Maintenance Task        PEAA ALLOW
Request Fast Fix               PEAA ALLOW
Recommend Reopen               PEAA ALLOW
Request Reopen                 PEAA ALLOW
Close Project                  OWNER APPROVAL
Cancel Active Project          OWNER APPROVAL
Major Upgrade Project          OWNER APPROVAL / project policy
Product Deprecation            OWNER APPROVAL
End of Support                 OWNER APPROVAL
Decommission Product           OWNER APPROVAL
Destructive Data Removal       OWNER-ONLY / explicit policy
```

---

# PART XX — NFR ADDITIONS

## 34. Lifecycle NFRs

### NFR-LC-01 — Lifecycle Continuity
The Factory SHALL manage software beyond initial delivery.

### NFR-LC-02 — Product/Project Separation
Closing a Project SHALL NOT implicitly close/decommission its Product.

### NFR-LC-03 — Historical Integrity
Close, cancel, archive and reopen operations SHALL preserve history and auditability.

### NFR-LC-04 — Reopen Re-Baseline
Reopened Projects SHALL refresh stale technical/project context before execution.

### NFR-LC-05 — Maintenance Traceability
Maintenance changes SHALL be traceable to Product, affected Release, Tasks, tests and fixing Release.

### NFR-LC-06 — Change-Proportional Process
The Factory SHOULD support lighter workflows for low-risk maintenance and stronger workflows for major changes.

### NFR-LC-07 — EOL Governance
Product deprecation, end-of-support and decommission SHALL be controlled and auditable.

### NFR-LC-08 — Operational Grounding
Where operational integrations exist, PEAA SHOULD use current operational data for production-status advice.

### NFR-LC-09 — Closed Project Protection
Normal execution SHALL not modify a CLOSED Project without an authorized reopen/change workflow.

### NFR-LC-10 — Release Independence
Maintenance Releases MAY be created without reopening the original development Project where policy allows.

---

# PART XXI — V0.6 ACCEPTANCE CRITERIA

## 35. Lifecycle Acceptance Criteria

- [ ] Product and Project are represented as separate lifecycle concepts.
- [ ] One Product can contain multiple Projects.
- [ ] One Product can contain multiple Releases.
- [ ] A Project can be CLOSED while Product remains in PRODUCTION/MAINTENANCE.
- [ ] Project supports DRAFT, PLANNING, ACTIVE, ON_HOLD, DELIVERY, ACCEPTANCE, COMPLETED, CLOSED, REOPENING and CANCELLED semantics.
- [ ] Project Closure performs configurable readiness checks.
- [ ] Project Closure produces a Closure Report.
- [ ] Required Owner approval is enforced for closure.
- [ ] CLOSED Projects reject normal execution.
- [ ] Reopen performs impact/re-baseline checks.
- [ ] Cancel preserves history.
- [ ] Archive does not mean delete.
- [ ] Corrective maintenance is supported.
- [ ] Adaptive maintenance is supported.
- [ ] Perfective maintenance is supported.
- [ ] Preventive maintenance is supported.
- [ ] Production incidents can create traceable repair Tasks.
- [ ] Enhancement requests can be classified.
- [ ] Upgrade/migration workflow is supported.
- [ ] Technical debt can be recorded and prioritized.
- [ ] PEAA can recommend Maintenance Task vs Reopen vs New Project.
- [ ] Maintenance fix can produce a new Release without reopening an old Project.
- [ ] Releases remain traceable to changes and tests.
- [ ] Product lifecycle continues after Project closure.
- [ ] EOL/Deprecation/End-of-Support/Decommission are represented.
- [ ] Only decommissioned/end-of-lifecycle Product is treated as lifecycle-complete.
- [ ] Lifecycle-changing actions are permission-controlled and auditable.

---

# PART XXII — UPDATED IMPLEMENTATION ROADMAP

## 36. Recommended Implementation Order

### Phase 1 — Existing V0.5 Core
Project, Task, State, Event, DAG, Markdown, Git.

### Phase 2 — Worker Execution
Worker/Role/Capability/Registry/Router/Context.

### Phase 3 — Task Management Engine
Validation, assignment, execution, retry, concurrency.

### Phase 4 — MCP + PEAA
Owner-facing management loop.

### Phase 5 — Product / Project / Release Domain
Implement separate domain models and traceability.

### Phase 6 — Project Lifecycle
Complete, Close, Reopen, Cancel, Archive and Closure Report.

### Phase 7 — Maintenance
Maintenance backlog, classification, Fast Fix, bug/incident flow.

### Phase 8 — Release & Operations
Release state, deployment traceability, operational status integration.

### Phase 9 — Methodologies
Scrum, Kanban, Waterfall, Hybrid, Custom.

### Phase 10 — Quality / Security / Governance
Review, QA, Security, permissions, audit, approvals.

### Phase 11 — Evolution
Enhancement, upgrade/migration, technical debt.

### Phase 12 — EOL
Deprecation, End of Support, migration/archive and Decommission.

---

# PART XXIII — V0.6 CORE PRINCIPLES

## 37. Authoritative Principles

1. **Product is long-lived; Project is finite.**
2. **Project completion does not mean Product completion.**
3. **Release acceptance does not mean Product completion.**
4. **A closed Project may belong to an active Product.**
5. **Maintenance may continue without reopening the original Project.**
6. **PEAA advises whether work should be Maintenance, Reopen, or New Project.**
7. **Reopened Projects must be re-baselined.**
8. **Closed Projects are protected from normal execution.**
9. **Cancel and Archive preserve history.**
10. **Maintenance is first-class Factory work.**
11. **Corrective, Adaptive, Perfective and Preventive Maintenance are supported.**
12. **Incidents and Bugs remain traceable through fixes and Releases.**
13. **Enhancements use process proportional to change impact.**
14. **Major upgrades/migrations normally use explicit Project governance.**
15. **Technical debt is managed as explicit project knowledge/work.**
16. **Product EOL requires explicit governance.**
17. **Decommission, not Project Closure, ends the Product lifecycle.**
18. **PEAA remains active and useful throughout Production/Maintenance.**
19. **LLM decides; Engine validates; Worker executes.**
20. **PEAA replaces the autonomous Task Manager Agent.**
21. **Task Management Engine remains deterministic.**
22. **Project Monitor observes; PEAA reasons and manages.**
23. **Worker != Role != Capability != Model.**
24. **MCP remains the external AI control boundary.**
25. **Core remains methodology-agnostic.**
26. **Git remains source of truth for source code.**
27. **Markdown remains primary human/Agent project knowledge.**
28. **Task State and Summary remain continuously maintained execution artifacts.**
29. **Lifecycle-changing operations are permission-controlled and auditable.**
30. **Models and methodologies remain replaceable/extensible without redesigning the Core.**

---

# PART XXIV — V0.6 VISION

## 38. Full Lifecycle Vision

The AI Software Factory SHALL behave as a long-running AI software organization, not merely an AI code-generation pipeline.

The Owner may create a Product, execute one or more Projects, release software, close completed Projects, continue operating and maintaining the Product, request fixes and enhancements, launch upgrade Projects, and eventually retire the Product.

PEAA remains the Owner-facing executive interface across the full lifecycle.

Example:

```text
Owner:
"Project P001 is accepted. Close it."

PEAA:
Checks closure readiness,
reports unresolved items,
requests Owner approval,
and closes P001 through the Engine.

Product:
Remains ACTIVE in Production.

Later...

Owner:
"Login has a small bug."

PEAA:
Classifies it as Corrective Maintenance,
creates a maintenance Task,
delegates the fix,
runs required validation,
and produces v1.0.1.

Later...

Owner:
"We need to replace the authentication architecture."

PEAA:
Classifies it as a major architectural migration,
recommends a new Project,
performs impact planning,
and manages the new delivery lifecycle.

Years later...

Owner:
"Retire this Product."

PEAA:
Runs EOL readiness,
migration/archive planning,
approval gates,
and controlled Decommission.
```

This is the intended end state:

> **AI Software Factory manages the complete life of software — from idea, through projects and releases, into operations, maintenance and evolution, until controlled end-of-life.**

---

# END OF V0.6 AUTHORITATIVE UPDATE


---

# V0.7 — REQUIREMENTS BASELINE CANDIDATE
## Enterprise Factory Administration, Multi-LLM, Resilience, Governance and Observability

> V0.7 preserves all confirmed V0.6 requirements unless explicitly superseded here.
>
> V0.7 is intended to be the **Requirements Baseline Candidate** for formal BA and Architecture review.
> Requirements in this section describe required behavior and governance. Specific products, databases,
> vaults, queues, cloud services, observability stacks and implementation frameworks remain Technical Design decisions unless explicitly mandated.

---

# PART I — V0.7 OBJECTIVES AND SCOPE

## 1. Objective

V0.7 closes the major platform-level gaps required for operating the AI Software Factory as a serious, long-lived software engineering platform.

The Factory SHALL include first-class capabilities for:

1. Multi-LLM Provider, Credential and Model Management.
2. Factory Administration and hierarchical configuration.
3. Secret and Credential Security.
4. Backup, Restore, Disaster Recovery and execution reconciliation.
5. Notification, Escalation and Owner Attention Management.
6. External Integration Adapter architecture.
7. Budget, Token and Cost Governance.
8. Factory Self-Observability and platform health.
9. Auditability and administrative governance.
10. Resilient execution across provider/platform failures.

These capabilities extend, but do not replace, the V0.6 Product/Project/Release/Maintenance lifecycle.

---

# PART II — CONSOLIDATED PLATFORM PRINCIPLES

## 2. Authoritative Principles

The following principles SHALL guide V0.7 and later designs:

```text
Product != Project != Release

Worker != Role != Capability != Model

Provider != Credential != Model != Worker

PEAA != Internal Worker

Project Monitor != Factory Monitor

Configuration != Secret

LLM decides.
Engine validates.
Worker executes.

Git is source of truth for source code.
Markdown is primary human/Agent-readable project knowledge.
Runtime DB/state stores operational orchestration data.
Secrets SHALL NOT be stored in project Markdown or source Git.

Core is methodology-agnostic.
Core is LLM-provider-agnostic.
Core is integration-vendor-agnostic.
```

---

# PART III — MULTI-LLM PROVIDER MANAGEMENT

## 3. Multi-Provider Requirement

The Factory SHALL support multiple LLM providers without redesigning Core orchestration.

Possible providers include, but are not limited to:

```text
OpenAI
Anthropic
Google
Azure-hosted models
AWS-hosted models
Self-hosted models
Local models
OpenAI-compatible endpoints
Future providers
```

No provider above is mandatory unless selected by deployment configuration.

## 4. Provider Domain Model

The logical relationship SHALL support:

```text
Provider
   |
   +-- Credential A
   +-- Credential B
   +-- Credential C
   |
   +-- Model A
   +-- Model B
   +-- Model C
```

Execution resolution SHALL conceptually support:

```text
Task
  |
Required Capability
  |
Model Router
  |
Provider + Credential + Model
  |
LLM Gateway
  |
Worker
  |
Role Prompt + Context + Permissions
  |
Execution
```

## 5. Provider Registry

The Factory SHALL maintain a Provider Registry.

A Provider SHOULD support metadata such as:

```text
Provider ID
Provider Type
Display Name
Endpoint / API Base
Enabled / Disabled
Health State
Supported Features
Default Timeout Policy
Default Retry Policy
Priority
Administrative Metadata
```

Endpoint support SHALL allow compatible private/self-hosted deployments where applicable.

## 6. Multiple Credentials per Provider

A Provider SHALL support multiple credentials/accounts/projects where the underlying provider permits it.

Example:

```text
Google
├── google-prod-a
├── google-prod-b
└── google-dev

OpenAI
├── openai-primary
└── openai-secondary
```

This enables:

- separate billing accounts;
- quota isolation;
- environment isolation;
- fallback;
- organizational separation;
- workload policies.

## 7. Credential Metadata

Credential records SHALL contain metadata and a secure secret reference, not plaintext secrets.

Logical fields may include:

```text
Credential ID
Provider ID
Display Name
Secret Reference
Environment
Enabled / Disabled
Health
Quota Metadata
Rate-Limit Metadata
Billing/Cost Context
Last Validation Time
Rotation Metadata
Created By
Created At
Updated At
```

## 8. Model Registry

The Factory SHALL maintain a Model Registry independent from Worker and Role definitions.

A model definition SHOULD be able to represent:

```text
Model ID
Provider
Provider Model Name
Enabled / Disabled
Capabilities
Context Limit metadata
Input/Output modalities
Tool support
Structured-output support
Quality profile
Latency profile
Cost profile
Routing tags
Safety/security policy
```

Exact provider/model metadata schemas are Technical Design decisions.

## 9. LLM Gateway / Adapter Layer

All provider-specific API behavior SHOULD be isolated behind a logical LLM Gateway/Adapter layer.

```text
Model Router
     |
LLM Gateway
     |
+----+------+-------+------+
|           |       |      |
OpenAI   Anthropic Google  Local
Adapter   Adapter   Adapter Adapter
```

Core workflow logic SHALL NOT depend directly on one provider SDK.

## 10. Provider Health

The Factory SHALL track provider/credential/model availability sufficiently for routing decisions.

Health may include:

```text
HEALTHY
DEGRADED
RATE_LIMITED
UNAVAILABLE
DISABLED
UNKNOWN
```

## 11. Quota and Rate-Limit Awareness

Where provider data permits, the Factory SHOULD track:

- quota;
- rate limits;
- throttling;
- retry-after signals;
- request failures;
- provider capacity constraints.

Router decisions MAY use these signals.

## 12. Provider Fallback

Routing policy SHALL support controlled fallback.

Example:

```text
Gemini selected
   |
429 / provider unavailable
   |
Retry policy
   |
Fallback policy
   |
GPT or Claude candidate
```

Fallback SHALL respect:

- capability requirements;
- project/provider allowlists;
- security/privacy policy;
- budget policy;
- context constraints;
- Owner restrictions.

Fallback SHALL NOT silently violate a project policy.

## 13. Provider Enable/Disable

Authorized administrators SHALL be able to disable:

```text
Provider
Credential
Model
```

Disabled resources SHALL not receive new work.

Running work behavior SHALL follow configured safe-stop/failure policy.

---

# PART IV — SECRET AND CREDENTIAL SECURITY

## 14. Secret Storage

Secrets SHALL NOT be stored in:

```text
project Markdown
task Markdown
prompt templates
Git source
logs
audit payload plaintext
error messages
```

Secrets SHALL be stored through an approved Secret Management mechanism.

Examples of implementation options may include a Vault, cloud secret service, encrypted local secret store or equivalent.

Specific technology is a Technical Design decision.

## 15. Secret References

Configuration SHALL reference secrets indirectly.

Example:

```text
credential_ref = secret://llm/openai/prod-01
```

The example URI is conceptual only.

## 16. Secret Access

Secret access SHALL follow least privilege.

Workers SHOULD receive only the credentials necessary for the specific execution path.

PEAA SHALL NOT need plaintext provider API keys for normal management operations.

## 17. Rotation and Revocation

The Factory SHALL support operational processes for:

```text
Credential validation
Credential rotation
Credential revocation
Credential disable
Credential replacement
Compromise response
```

## 18. Encryption

Sensitive credential data SHALL be protected in transit and at rest.

Specific cryptographic implementation belongs to Security/Technical Design.

## 19. Secret Audit

Security-relevant credential operations SHALL be auditable without exposing secret values.

Examples:

```text
CREDENTIAL_CREATED
CREDENTIAL_ROTATED
CREDENTIAL_DISABLED
CREDENTIAL_REVOKED
CREDENTIAL_VALIDATION_FAILED
```

---

# PART V — FACTORY ADMINISTRATION

## 20. Factory Administration Capability

The Factory SHALL provide an administrative capability for managing platform-level resources and policies.

Administrative domains include:

```text
Providers
Credentials
Models
Workers
Capabilities
Roles
Methodologies
Prompt Templates
Users / Identities
Permissions
Global Policies
Projects
Products
Integrations
Budgets
Notification Policies
Execution Policies
MCP Configuration
Audit Access
Backup / Recovery
```

A UI is desirable but exact UI implementation is not mandated by this requirement.

Administration MAY be exposed through API, web UI, CLI, MCP or controlled combinations.

## 21. Hierarchical Configuration

Configuration SHALL support hierarchical scope.

Reference hierarchy:

```text
Factory / Global
      |
Product
      |
Project
      |
Optional Workstream / Environment
```

## 22. Configuration Precedence

More specific configuration MAY override broader configuration only where policy allows.

Conceptual precedence:

```text
Mandatory Global Security Policy
        |
Global Defaults
        |
Product Policy
        |
Project Policy
        |
Task-specific allowed override
```

Mandatory security/governance controls SHALL NOT be bypassed by lower scopes.

## 23. Configuration Categories

Configuration SHOULD distinguish:

```text
Functional configuration
Routing policy
Budget policy
Security policy
Approval policy
Methodology policy
Notification policy
Integration configuration
Execution policy
Retention policy
```

## 24. Configuration Versioning

Material configuration changes SHOULD be versioned/audited.

The Factory SHOULD be able to identify which effective configuration governed an execution.

## 25. Environment Separation

The Factory SHOULD support environment-aware configuration such as:

```text
development
test
staging
production
```

Environment-specific secrets and policies SHALL remain appropriately isolated.

---

# PART VI — IDENTITY, AUTHORIZATION AND GOVERNANCE

## 26. Identity

The Factory SHALL identify actors sufficiently to attribute sensitive actions.

Actors may include:

```text
Owner
Administrator
Human Team Member
PEAA
Worker
System Service
Integration
```

## 27. Authorization

The Factory SHALL enforce permission checks for sensitive operations.

Permissions SHOULD be scope-aware.

Examples:

```text
factory:admin
provider:read
provider:manage
credential:manage
model:manage
worker:manage

product:read
product:update

project:read
project:update
project:close
project:reopen
project:cancel

task:read
task:create
task:update
task:assign
task:execute
task:cancel

release:request
release:approve

deploy:request
deploy:execute

budget:read
budget:manage

audit:read

backup:execute
restore:execute

eol:request
eol:approve
```

## 28. Least Privilege

Workers and integrations SHALL operate with the minimum practical permission set.

## 29. Approval Boundaries

High-risk actions SHALL support explicit approval gates.

Examples include:

- production deployment;
- architecture baseline approval;
- security exception;
- Project closure;
- Project cancellation;
- major budget override;
- Product EOL;
- destructive restore;
- destructive data operation;
- permission escalation.

Owner/policy determines final approval matrix.

---

# PART VII — BACKUP, RESTORE AND DISASTER RECOVERY

## 30. Backup Scope

The Factory SHALL define backup policies for critical platform state.

Potential protected assets include:

```text
Runtime database
Project metadata
Task state
Event/audit history
Configuration
Provider/model metadata
Integration configuration
Product/project/release metadata
Indexes that cannot be cheaply rebuilt
Operational knowledge
```

Git-managed source and Markdown MAY use Git as one recovery source but SHALL still be considered in overall disaster recovery planning.

Secrets require a secure backup/recovery policy appropriate to the selected Secret Manager.

## 31. Backup Policy

Backup policy SHOULD support:

```text
Frequency
Retention
Encryption
Storage location
Environment
Validation
Recovery priority
```

## 32. Restore

Authorized users SHALL be able to initiate controlled restore processes.

Restore SHALL protect against accidental state corruption and inappropriate overwrite.

## 33. Disaster Recovery

The Factory SHALL have a defined Disaster Recovery strategy.

Deployment-specific targets SHOULD define:

```text
RPO — Recovery Point Objective
RTO — Recovery Time Objective
```

Exact values are deployment/business requirements and SHALL be determined during Architecture/Operations planning.

## 34. Backup Validation

Backups SHOULD be periodically validated for restorability.

A backup that cannot be restored SHALL be treated as failed protection.

## 35. Execution Recovery

Factory restart or crash SHALL NOT cause task state to be guessed.

Reference recovery:

```text
Factory Restart
    |
Recovery/Reconciliation
    |
Read durable state
    |
Read event history
    |
Inspect Git/workspace
    |
Inspect execution lease/worker state
    |
Determine:
    +-- resume
    +-- retry
    +-- rollback
    +-- mark recovery-required
    +-- request human decision
```

## 36. In-Flight Task Reconciliation

Tasks interrupted during execution SHALL enter a deterministic recovery/reconciliation process.

Possible logical states include:

```text
RECOVERY_REQUIRED
RETRY_PENDING
RESUME_PENDING
FAILED_RECOVERABLE
FAILED_TERMINAL
```

Exact Task State integration SHALL be finalized in Detailed Design.

## 37. Idempotency

Operations that may be retried SHOULD be designed for idempotency or duplicate detection where practical.

This is especially important for:

- task dispatch;
- external integration calls;
- release operations;
- notifications;
- deployment requests.

---

# PART VIII — NOTIFICATION, ESCALATION AND OWNER ATTENTION

## 38. Notification Engine

The Factory SHALL support notifications for important events.

Potential events include:

```text
Task blocked
Task repeatedly failed
Worker unavailable
Provider unavailable
Question waiting for Owner/PO
Approval required
Architecture decision required
Security HIGH/CRITICAL finding
Budget threshold reached
Release ready
Deployment failed
Production incident
Project closure ready
Backup failure
Factory health degradation
```

## 39. Owner Inbox

The Factory SHALL provide a logical Owner Attention Inbox.

It SHALL aggregate items requiring human attention.

Example:

```text
OWNER ATTENTION

ADR-023
Architecture approval required

SEC-012
HIGH security finding

P002
Ready for Project closure approval

BUDGET
Project P004 reached 90%
```

## 40. Pending Questions

Questions from Workers/PEAA requiring human input SHALL remain durable and discoverable until answered, cancelled or superseded.

## 41. Escalation

Notification policy SHOULD support escalation based on:

```text
Severity
Age
Business impact
Security impact
Production impact
Deadline
Repeated failure
```

## 42. Notification Channels

The architecture SHALL allow pluggable channels.

Examples:

```text
In-app
PEAA/MCP
Email
Slack
Teams
Webhook
Future channels
```

No specific third-party channel is mandatory for MVP unless selected by project scope.

## 43. Notification Preferences

Authorized users SHOULD be able to configure notification routing and noise controls without suppressing mandatory critical alerts.

---

# PART IX — EXTERNAL INTEGRATION ARCHITECTURE

## 44. Integration Gateway

The Factory SHALL support an extensible Integration Gateway/Adapter architecture.

```text
Factory Core
    |
Integration Gateway
    |
+---+--------+----------+----------+---------+
|            |          |          |         |
Git        CI/CD     Issue      Monitoring  Communication
Adapter    Adapter    Tracker     Adapter     Adapter
```

## 45. Integration Categories

The architecture SHOULD permit integrations with:

```text
Git providers
CI/CD platforms
Issue trackers
Cloud providers
Container/artifact registries
Monitoring/observability systems
Security scanners
Communication platforms
Documentation systems
Deployment systems
```

## 46. Vendor Independence

Core workflow SHALL NOT require a specific Git/CI/issue/monitoring vendor unless a deployment explicitly selects one.

## 47. Integration Authentication

Integration credentials SHALL follow the same Secret Management and least-privilege requirements as LLM credentials.

## 48. Integration Health

The Factory SHOULD track integration health where it materially affects execution.

## 49. Integration Events

Important integration actions and failures SHOULD be auditable.

---

# PART X — BUDGET, TOKEN AND COST GOVERNANCE

## 50. Cost Accounting

The Factory SHALL track AI execution cost/token usage to the extent provider data permits.

Cost attribution SHOULD support:

```text
Factory
Product
Project
Task
Worker
Provider
Credential
Model
Role/Capability
Time period
```

## 51. Budget Hierarchy

Budget policy SHOULD support:

```text
Factory Budget
   |
Product Budget
   |
Project Budget
   |
Task / Workstream Budget
```

## 52. Budget Thresholds

Policies SHOULD support thresholds such as:

```text
50% informational
80% warning
90% escalation
100% block or Owner approval
```

Values are configurable; these are examples only.

## 53. Router Cost Awareness

Model Router MAY use cost as one routing factor alongside:

```text
Capability
Quality
Availability
Latency
Context fit
Security
Privacy
Quota
Health
Budget
```

Cost SHALL NOT override mandatory capability/security constraints.

## 54. Budget Approval

Policy MAY require Owner approval when execution would exceed a budget or high-cost threshold.

## 55. Cost Forecast

The Factory SHOULD support estimated remaining/projected AI execution cost when sufficient historical/planning data exists.

## 56. Cost Auditability

The Owner SHOULD be able to answer questions such as:

```text
How much has Project P003 cost?
Which model consumed the most tokens?
What did architecture analysis cost?
Why did today's cost increase?
How much budget remains?
```

---

# PART XI — FACTORY SELF-OBSERVABILITY

## 57. Project Monitor vs Factory Monitor

These are separate responsibilities.

```text
Project Monitor
= Is the project progressing correctly?

Factory Monitor
= Is the AI Software Factory platform itself healthy?
```

## 58. Factory Monitor

The Factory SHALL expose health and operational telemetry for critical platform components.

Potential monitored components:

```text
Task Management Engine
Dependency Engine
Methodology Engine
Permission Engine
MCP Gateway
Model Router
LLM Gateway
Context Manager
Provider connections
Workers
Queue/scheduler
Runtime database
Git integration
Workspace system
Integration Gateway
Notification system
Backup system
Audit system
```

## 59. Platform Metrics

Factory telemetry SHOULD include, where relevant:

```text
Running Tasks
Queued Tasks
Blocked Tasks
Failed Tasks
Retry rate
Worker utilization
Provider latency
Provider failures
Rate-limit events
Token consumption
Cost
Context retrieval latency
MCP latency/errors
Database health
Git failures
Integration failures
Notification failures
Backup status
```

## 60. Health States

Components SHOULD expose normalized health where appropriate:

```text
HEALTHY
DEGRADED
UNAVAILABLE
DISABLED
UNKNOWN
```

## 61. Factory Alerts

Factory Monitor SHALL be able to trigger notification/escalation for significant platform degradation.

## 62. PEAA Factory Visibility

PEAA SHOULD be able to answer:

```text
Why is execution slow?
Which provider is failing?
How many Tasks are queued?
Which Workers are overloaded?
Are backups healthy?
Is MCP healthy?
What caused the recent execution failures?
```

PEAA SHALL receive summarized/relevant telemetry rather than unrestricted raw logs by default.

---

# PART XII — EXECUTION RESILIENCE

## 63. Failure Classification

Execution failures SHOULD be classified, for example:

```text
TRANSIENT_PROVIDER_ERROR
RATE_LIMIT
TIMEOUT
AUTHENTICATION_ERROR
INVALID_REQUEST
CONTEXT_LIMIT
TOOL_ERROR
GIT_CONFLICT
TEST_FAILURE
SECURITY_POLICY_BLOCK
BUDGET_BLOCK
DEPENDENCY_BLOCK
PERMISSION_DENIED
WORKER_FAILURE
PLATFORM_FAILURE
```

Exact taxonomy may evolve.

## 64. Retry Policy

Retries SHALL be controlled by policy.

The Factory SHALL avoid uncontrolled infinite retry loops.

## 65. Circuit Breaking

Architecture SHOULD support temporarily avoiding unhealthy providers/integrations after repeated failures.

Exact algorithm belongs to Technical Design.

## 66. Execution Lease / Ownership

The Factory SHOULD prevent the same exclusive Task from being unintentionally executed by multiple Workers simultaneously.

Distributed locking/lease technology is a Technical Design decision.

## 67. Stuck Work Detection

Project/Factory monitoring SHOULD detect executions that appear stuck or exceed configured thresholds.

---

# PART XIII — AUDIT AND COMPLIANCE

## 68. Audit Log

Material management and execution events SHALL be auditable.

Audit SHOULD capture:

```text
Who/what acted
Action
Target
Timestamp
Result
Relevant policy/approval
Correlation/trace ID
Non-secret change metadata
```

## 69. Audit Events

Examples include:

```text
PROJECT_CREATED
PROJECT_CLOSED
PROJECT_REOPENED
PROJECT_CANCELLED

TASK_CREATED
TASK_ASSIGNED
TASK_EXECUTION_REQUESTED
TASK_COMPLETED

PROVIDER_ENABLED
PROVIDER_DISABLED
MODEL_ENABLED
MODEL_DISABLED

CREDENTIAL_CREATED
CREDENTIAL_ROTATED
CREDENTIAL_REVOKED

BUDGET_CHANGED
BUDGET_OVERRIDE_APPROVED

RELEASE_APPROVED
DEPLOYMENT_REQUESTED
DEPLOYMENT_EXECUTED

BACKUP_COMPLETED
BACKUP_FAILED
RESTORE_REQUESTED
RESTORE_COMPLETED

PERMISSION_CHANGED
POLICY_CHANGED
```

## 70. Correlation

A management request SHOULD be traceable across PEAA -> MCP -> Engine -> Router -> Worker -> tools/events where practical.

## 71. Retention

Audit, logs and project artifacts SHALL support configurable retention appropriate to deployment requirements.

---

# PART XIV — MCP MANAGEMENT CAPABILITIES

## 72. Additional MCP Capability Groups

V0.7 SHOULD expose logical MCP operations sufficient for PEAA to manage and inspect these domains subject to permission.

### Provider / Model

```text
list_providers
get_provider
get_provider_health
enable_provider
disable_provider

list_models
get_model
enable_model
disable_model

list_credentials_metadata
validate_credential
request_credential_rotation
```

Plaintext secret retrieval SHOULD NOT be exposed to PEAA.

### Factory

```text
get_factory_status
get_factory_health
get_factory_metrics
get_execution_queue
get_failed_executions
get_platform_alerts
```

### Budget

```text
get_budget
get_cost_summary
get_cost_breakdown
get_token_usage
get_budget_alerts
request_budget_change
```

### Attention

```text
get_owner_inbox
get_pending_approvals
get_pending_questions
acknowledge_notification
```

### Backup / Recovery

```text
get_backup_status
list_backups
request_backup
get_recovery_status
request_restore
```

High-risk restore SHALL require appropriate approval.

### Integration

```text
list_integrations
get_integration
get_integration_health
enable_integration
disable_integration
```

Exact MCP schemas and tool naming remain Detailed Design work.

---

# PART XV — CONFIGURATION AND ARTIFACT STRUCTURE

## 73. Suggested Platform Configuration Structure

Human-readable non-secret configuration MAY be represented conceptually as:

```text
/factory
├── configuration/
│   ├── factory-policy.md
│   ├── routing-policy.md
│   ├── budget-policy.md
│   ├── notification-policy.md
│   ├── retention-policy.md
│   └── security-policy.md
├── providers/
│   ├── provider-registry.md
│   └── model-registry.md
├── workers/
│   ├── worker-registry.md
│   ├── capability-registry.md
│   └── role-definitions/
├── methodologies/
├── integrations/
├── audit/
└── operations/
```

Secrets SHALL NOT appear in this structure.

The exact physical storage may use DB/config service/Git or combinations determined by Architecture.

## 74. Runtime State

Highly dynamic operational state SHOULD NOT rely solely on manually edited Markdown.

Examples:

```text
active execution leases
queue state
provider health
rate limits
runtime locks
notification delivery state
live telemetry
```

These require appropriate runtime persistence.

---

# PART XVI — DATA PROTECTION AND RETENTION

## 75. Sensitive Data Classification

Architecture SHALL identify classes of sensitive information including:

```text
Secrets
Source code
Customer/project data
Prompts/context
Model outputs
Logs
Audit data
Production telemetry
Personal information where applicable
```

## 76. Data Minimization

Context Manager and integrations SHOULD minimize unnecessary disclosure of project data to external models/providers.

## 77. Provider Data Policy

Routing policy SHOULD be able to restrict which providers/models may receive specific project classifications.

Example:

```text
Public project:
multiple providers allowed

Confidential project:
approved providers only

Restricted source:
local/private model only
```

Specific classification scheme is Security Design work.

## 78. Retention and Deletion

The Factory SHALL support configurable retention/deletion policies while preserving mandatory audit/legal requirements.

Destructive deletion SHALL require explicit authorization.

---

# PART XVII — NON-FUNCTIONAL REQUIREMENTS

## 79. NFR-MLLM-01 — Provider Independence

Adding/removing a supported LLM provider SHOULD NOT require redesigning workflow Core.

## 80. NFR-MLLM-02 — Secret Isolation

Provider secrets SHALL never be stored in project Markdown or source Git.

## 81. NFR-MLLM-03 — Controlled Fallback

Fallback SHALL preserve capability, security, privacy and budget policy.

## 82. NFR-ADM-01 — Configuration Governance

Effective configuration SHALL be attributable to scope and version where practical.

## 83. NFR-SEC-01 — Least Privilege

Workers, PEAA, integrations and human actors SHALL receive only authorized capabilities.

## 84. NFR-SEC-02 — Secret Protection

Secrets SHALL be protected in transit and at rest.

## 85. NFR-DR-01 — Recoverability

Critical Factory state SHALL be recoverable according to deployment RPO/RTO objectives.

## 86. NFR-DR-02 — Execution Reconciliation

Factory restart SHALL not arbitrarily mark in-flight work complete or ready without reconciliation.

## 87. NFR-NOTIFY-01 — Durable Attention

Mandatory approvals/questions SHALL remain discoverable until resolved.

## 88. NFR-INT-01 — Integration Independence

External integrations SHALL use adapters/interfaces that minimize vendor coupling.

## 89. NFR-COST-01 — Cost Attribution

AI usage SHOULD be attributable to project/task/provider/model where provider data permits.

## 90. NFR-OBS-01 — Platform Observability

Critical Factory components SHALL expose sufficient telemetry for health diagnosis.

## 91. NFR-AUD-01 — Auditability

Sensitive management operations SHALL produce durable non-secret audit records.

## 92. NFR-RES-01 — Bounded Retry

Automatic retries SHALL be bounded and policy-controlled.

## 93. NFR-RES-02 — Duplicate Protection

Critical retried operations SHOULD be idempotent or duplicate-detecting.

## 94. NFR-DATA-01 — Context Minimization

Only relevant/authorized context SHOULD be sent to external models.

---

# PART XVIII — ACCEPTANCE CRITERIA

## 95. Multi-LLM Acceptance

- [ ] Factory can register multiple LLM providers.
- [ ] Provider can contain multiple credentials.
- [ ] Credentials use secret references rather than plaintext project configuration.
- [ ] Factory can register multiple models per provider.
- [ ] Provider/model can be enabled or disabled.
- [ ] Router can select candidates across providers.
- [ ] Router can avoid unhealthy/disabled candidates.
- [ ] Controlled fallback is supported.
- [ ] Provider-specific behavior is isolated behind an adapter/gateway abstraction.
- [ ] Worker/Role/Capability remain independent from provider/model identity.

## 96. Administration Acceptance

- [ ] Global Factory configuration exists.
- [ ] Product/Project-specific configuration is supported.
- [ ] Mandatory global policies cannot be bypassed by lower scopes.
- [ ] Material policy/configuration changes are auditable.
- [ ] Administrative permissions are enforced.

## 97. Secret Security Acceptance

- [ ] API keys are not stored in Markdown/Git.
- [ ] Secret references are used.
- [ ] Credential rotation/revocation workflow exists.
- [ ] Secret values are not exposed in normal logs/audit.
- [ ] PEAA does not require plaintext keys for normal operations.

## 98. Recovery Acceptance

- [ ] Critical runtime state has a backup strategy.
- [ ] Restore process is defined.
- [ ] Backup validation is supported.
- [ ] RPO/RTO can be defined per deployment.
- [ ] Interrupted tasks are reconciled after restart.
- [ ] Factory does not guess task completion after crash.
- [ ] Recovery actions are auditable.

## 99. Notification Acceptance

- [ ] Owner Inbox exists logically.
- [ ] Pending approvals are discoverable.
- [ ] Pending questions are discoverable.
- [ ] Critical failures can trigger alerts.
- [ ] Escalation policy can consider severity/time.
- [ ] Notification channels are extensible.

## 100. Integration Acceptance

- [ ] Integration Adapter/Gateway abstraction exists.
- [ ] Git/CI/issue/monitoring integrations can be added without changing workflow Core.
- [ ] Integration credentials use Secret Management.
- [ ] Integration health can be surfaced where relevant.

## 101. Budget Acceptance

- [ ] Token/cost usage is captured where provider data permits.
- [ ] Cost can be attributed at least to Project, Task, Provider and Model.
- [ ] Budget thresholds are configurable.
- [ ] Thresholds can notify/escalate.
- [ ] Policy can require Owner approval before exceeding a hard budget.
- [ ] Router may consider cost but cannot bypass security/capability policy.

## 102. Factory Observability Acceptance

- [ ] Factory health is separate from Project progress.
- [ ] Core engines expose health.
- [ ] Provider/Worker health is visible.
- [ ] Queue/running/failed work is visible.
- [ ] Rate-limit/provider failures are visible.
- [ ] Backup status is visible.
- [ ] PEAA can retrieve summarized Factory health through MCP.

## 103. Audit Acceptance

- [ ] High-risk administrative actions are audited.
- [ ] Provider/credential lifecycle events are audited without secrets.
- [ ] Project close/reopen/cancel is audited.
- [ ] Budget overrides are audited.
- [ ] Backup/restore is audited.
- [ ] Correlation across management/execution flow is possible where practical.

---

# PART XIX — UPDATED LOGICAL ARCHITECTURE

## 104. V0.7 Logical Architecture

```text
                              OWNER
                                |
                                v
                              PEAA
                                |
                               MCP
                                |
                     +----------v-----------+
                     |      MCP GATEWAY     |
                     +----------+-----------+
                                |
        +-----------------------+------------------------+
        |                       |                        |
        v                       v                        v
 PRODUCT / PROJECT         MANAGEMENT CORE         FACTORY ADMIN
 LIFECYCLE                 Task Engine             Configuration
 Release                   Dependency Engine       Provider Registry
 Maintenance               Methodology Engine      Model Registry
 Operations                Permission Engine       Integration Registry
 EOL                       Change Classification   Budget Policy
        |                       |                   Notification Policy
        +-----------------------+------------------------+
                                |
                          MODEL ROUTER
                                |
                          LLM GATEWAY
                                |
               +----------------+----------------+
               |                |                |
               v                v                v
            Provider A       Provider B       Provider C
               |                |                |
          Credential(s)    Credential(s)    Credential(s)
               |                |                |
             Models           Models           Models
               +----------------+----------------+
                                |
                              WORKERS
                                |
              Role Prompt + Context + Permission
                                |
                       EXECUTION / TOOLS
                                |
                Git / Workspace / CI / Test
                                |
                         Release / Deploy

Cross-cutting platform services:

+ Secret Management
+ Audit
+ Notification / Owner Inbox
+ Budget / Cost Accounting
+ Backup / Restore / DR
+ Factory Monitor / Telemetry
+ Integration Gateway
+ Security / Authorization
```

---

# PART XX — OPERATIONAL SCENARIOS

## 105. Provider Failure Scenario

```text
TASK-125
Required Capability: backend_development
        |
Router selects Gemini
        |
Provider returns repeated rate limit
        |
Health = RATE_LIMITED
        |
Retry policy evaluated
        |
Fallback candidates evaluated
        |
GPT selected if allowed
        |
Execution continues
        |
Routing/failure event audited
```

## 106. Secret Rotation Scenario

```text
Administrator requests credential rotation
        |
Permission validation
        |
New secret stored securely
        |
Credential reference/version updated
        |
Connection validated
        |
Old credential revoked
        |
Audit event
```

No plaintext key is written to project artifacts.

## 107. Factory Crash Scenario

```text
Factory crashes while TASK-220 executes
        |
Factory restarts
        |
Recovery detects interrupted execution
        |
Durable state + events + Git/workspace reconciled
        |
TASK-220 = RECOVERY_REQUIRED
        |
Policy chooses resume/retry/human decision
        |
No false DONE state
```

## 108. Budget Scenario

```text
Project P004 budget = configured limit
        |
Usage reaches warning threshold
        |
Owner Inbox notification
        |
Router continues within policy
        |
Usage reaches hard threshold
        |
New expensive execution blocked
        |
Owner approval requested
```

## 109. Confidential Project Scenario

```text
Project classification = RESTRICTED
        |
Routing policy:
external public providers prohibited
        |
Router candidates filtered
        |
Private/local approved model selected
```

## 110. Factory Health Scenario

```text
Owner:
"Why is the Factory slow today?"

PEAA
  |
get_factory_health
  |
Factory Monitor
  |
Gemini: RATE_LIMITED
Queue: 38
Worker utilization: high
Git: HEALTHY
DB: HEALTHY
  |
PEAA:
explains cause and recommends permitted routing/capacity action.
```

---

# PART XXI — IMPLEMENTATION ROADMAP UPDATE

## 111. Recommended Delivery Order

### Phase 1 — Core Domain and State
Product, Project, Release, Task, Event, Git/Markdown conventions.

### Phase 2 — Task/Dependency/Execution Engines
Deterministic validation and execution lifecycle.

### Phase 3 — Worker/Role/Capability
Registry and execution abstraction.

### Phase 4 — Multi-LLM Platform
Provider Registry, Credential references, Model Registry, LLM Gateway, Router.

### Phase 5 — Secret and Permission Foundation
Secret Manager integration, RBAC/permission checks, audit.

### Phase 6 — MCP + PEAA
External executive management interface.

### Phase 7 — Context Manager
Selective knowledge/context retrieval.

### Phase 8 — Quality and Delivery
Review, integration, QA, Security, Release, Deploy.

### Phase 9 — Full Product Lifecycle
Operations, Maintenance, Change Classification, Upgrade/Migration, EOL.

### Phase 10 — Factory Administration
Hierarchical configuration and management interfaces.

### Phase 11 — Cost/Budget Governance
Accounting, thresholds, approval gates, reporting.

### Phase 12 — Notification and Owner Inbox
Approvals, questions, alerts, escalation.

### Phase 13 — Factory Observability
Platform telemetry, health, alerts and diagnosis.

### Phase 14 — Backup/Restore/DR
Backup policy, validation, reconciliation, recovery exercises.

### Phase 15 — Integration Ecosystem
Git/CI/CD/issue/monitoring/cloud/communication adapters as prioritized.

### Phase 16 — Methodology Profiles
Scrum, Kanban, Waterfall, Hybrid, Custom.

### Phase 17 — Hardening
Performance, concurrency, security hardening, failure injection, disaster recovery testing.

---

# PART XXII — REQUIREMENTS VS TECHNICAL DESIGN BOUNDARY

## 112. Requirements Baseline

V0.7 intentionally specifies WHAT the Factory must support.

Examples of requirements:

```text
Multiple LLM providers
Secure credential references
Controlled fallback
Project closure/reopen
Backup/restore
Owner Inbox
Cost governance
Factory health monitoring
Integration adapters
```

## 113. Technical Design Decisions

The following SHOULD NOT be frozen merely because they are mentioned as examples:

```text
Specific database
Specific queue
Specific Secret Manager
Specific cloud provider
Specific observability stack
Specific Git vendor
Specific CI/CD vendor
Specific UI framework
Specific vector database
Specific cache
Specific deployment topology
Specific locking algorithm
Specific event bus
```

Architecture/Technical Design SHALL select technologies based on approved NFRs and constraints.

---

# PART XXIII — FORMAL REVIEW GATES

## 114. Baseline Review

Before implementation begins at scale, V0.7 SHOULD pass:

```text
BA Review
  |
Ambiguity / Missing Requirement Review
  |
Owner Resolution
  |
Architecture Review
  |
Security Review
  |
Operational/DR Review
  |
Cost/Capacity Review
  |
Baseline Approval
```

## 115. Traceability

After BA formalization, major requirements SHOULD receive stable identifiers enabling:

```text
Requirement
  -> Use Case
  -> Architecture Component
  -> Design
  -> Task
  -> Test
  -> Acceptance Evidence
```

## 116. Change Control After Baseline

Once Owner approves the requirements baseline, material scope changes SHOULD enter Change Management rather than silently modifying baseline requirements.

---

# PART XXIV — V0.7 BASELINE ACCEPTANCE CHECKLIST

## 117. Baseline Candidate Checklist

### Core Architecture
- [ ] PEAA remains external through MCP.
- [ ] Task Manager Agent remains removed.
- [ ] Task Management Engine remains deterministic.
- [ ] LLM decides; Engine validates; Worker executes.
- [ ] Worker != Role != Capability != Model.
- [ ] Core remains methodology-agnostic.

### Lifecycle
- [ ] Product != Project != Release.
- [ ] Project close/reopen/cancel/archive exists.
- [ ] Operations and Maintenance exist after release.
- [ ] Corrective/Adaptive/Perfective/Preventive maintenance exist.
- [ ] Enhancement and Upgrade/Migration exist.
- [ ] EOL and Decommission exist.

### Multi-LLM
- [ ] Multiple providers.
- [ ] Multiple credentials per provider.
- [ ] Model Registry.
- [ ] LLM Gateway.
- [ ] Router health/quota/cost awareness.
- [ ] Controlled fallback.
- [ ] Provider/model enable-disable.

### Security
- [ ] Secrets outside Markdown/Git.
- [ ] Secret references.
- [ ] Rotation/revocation.
- [ ] Least privilege.
- [ ] Permission enforcement.
- [ ] Sensitive actions audited.
- [ ] Data/provider routing restrictions supported.

### Administration
- [ ] Global/Product/Project configuration.
- [ ] Policy precedence.
- [ ] Administrative management capabilities.
- [ ] Environment separation.

### Resilience
- [ ] Backup.
- [ ] Restore.
- [ ] DR.
- [ ] Configurable RPO/RTO.
- [ ] Backup validation.
- [ ] In-flight execution reconciliation.
- [ ] Bounded retry.
- [ ] Duplicate/idempotency protection.

### Human Attention
- [ ] Owner Inbox.
- [ ] Pending approvals.
- [ ] Pending questions.
- [ ] Notification policy.
- [ ] Escalation.
- [ ] Extensible channels.

### Integrations
- [ ] Integration Gateway/Adapters.
- [ ] Vendor-independent Core.
- [ ] Secure integration credentials.
- [ ] Integration health.

### Cost
- [ ] Token/cost accounting.
- [ ] Cost attribution.
- [ ] Budget hierarchy.
- [ ] Threshold alerts.
- [ ] Approval for hard limits.
- [ ] Router cost awareness.

### Observability
- [ ] Project Monitor.
- [ ] Factory Monitor.
- [ ] Provider/Worker/Engine health.
- [ ] Queue and execution metrics.
- [ ] Platform alerts.
- [ ] PEAA health visibility.

### Governance
- [ ] Audit log.
- [ ] Correlation/traceability.
- [ ] Retention policies.
- [ ] Formal baseline review.
- [ ] Requirement change control after approval.

---

# PART XXV — V0.7 FINAL VISION

## 118. Platform Vision

AI Software Factory is not merely a collection of coding Agents.

It is a governed software engineering platform capable of managing:

```text
Ideas
Requirements
Analysis
Architecture
Projects
Tasks
Workers
Multiple LLM providers
Credentials
Models
Source code
Testing
Security
Releases
Deployments
Production
Operations
Maintenance
Incidents
Enhancements
Upgrades
Costs
Approvals
Integrations
Platform health
Recovery
Audit
End-of-Life
```

The Owner interacts primarily with PEAA.

PEAA reasons and manages through MCP.

Deterministic Engines validate state and policy.

Model Router selects an allowed execution resource.

LLM Gateway isolates provider-specific behavior.

Workers execute scoped Roles using only required Context and Permissions.

The Factory records state, evidence, cost and audit information throughout the lifecycle.

The platform SHALL remain extensible so that providers, models, methodologies, integrations and implementation technologies can evolve without redesigning the fundamental Factory architecture.

> **V0.7 is the Requirements Baseline Candidate for formal BA and Architecture review.**

---

# END OF V0.7 AUTHORITATIVE UPDATE
