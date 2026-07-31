---
name: review-prd
description: "Review a PRD, product requirement, feature specification, or change request through two complementary lenses: Senior Quality Engineer and end user. Use when the user asks to review/QA-check a PRD, find requirement gaps, assess testability or user experience, or generate sensible clarification questions for PM, PO, BA, design, or engineering. Produce evidence-linked, prioritized questions without inventing requirements. Do not use for code or pull-request review, or to create test cases from an already-approved specification."
---

# Review PRD — Senior QE & User Lens

Review whether a PRD gives a team enough unambiguous information to build, operate, verify, and measure a valuable feature. Think in three complementary lenses, then combine them in one concise review:

- **Business:** Is the intended outcome, success measure, allocation/priority rule, exception policy, and rollout decision clear?
- **Senior QE:** Can the behavior, data, integrations, non-functional needs, errors, and acceptance criteria be verified without guessing?
- **User:** Can each intended person understand, complete, recover from, and trust the journey—including on a small screen, slow network, or unusual but realistic situation?

The goal is not to rewrite the PRD or produce a generic checklist. Produce the smallest set of high-value questions that exposes decisions the team must make.

## Input and boundaries

Require the PRD text, file, or a readable link. Also use any supplied designs, user stories, APIs, analytics, policy/compliance constraints, or prior decisions as evidence. If the PRD is unavailable, ask for it rather than reviewing from memory.

Treat the PRD as the source of truth unless the user explicitly assigns precedence. Do not assume missing values, roles, messages, limits, states, or platform conventions. A plausible behavior is still a gap until a source confirms it.

If the user asks to focus on a section, persona, platform, or lens, review that scope only and omit the overall readiness conclusion unless requested.

## Workflow

### 1. Establish the product slice

Extract, with citations to PRD headings or quoted fragments:

- goal and measurable success outcome;
- target users, roles, permissions, and excluded users;
- trigger, main journey, alternate journeys, and end state;
- scope boundaries, dependencies, integrations, data, and stated constraints;
- acceptance criteria and unresolved decisions already present.

State a concise **review assumption** when a persona, platform, or product context is absent. Do not turn it into a requirement.

### 2. Inspect with the business lens

Identify the decision that makes the feature valuable, rather than reviewing implementation alone. Check only what is relevant:

| Area | Ask when the PRD does not make the business decision clear |
|---|---|
| Outcome | Target behavior or business outcome, baseline, KPI, and success threshold |
| Priority and allocation | Which users/products/campaigns win when capacity, budget, inventory, or attention is scarce |
| Exceptions | Urgent/manual override policy, who can change a decision, and the consequence of not acting |
| Trade-offs | What is intentionally optimized or sacrificed (for example, reach vs. timeliness, fairness vs. priority) |
| Rollout | Entry criteria, measurement, stop/rollback rule, and path from pilot to full release |

Do not invent business goals. If the PRD contains an operational mechanism without its intended business result, raise that as a decision to make.

### 3. Inspect with the Senior QE lens

Look for gaps that would cause ambiguous implementation, weak coverage, or production defects. Check only areas relevant to the PRD:

| Area | Ask when the PRD does not make it verifiable |
|---|---|
| Functional behavior | Happy path, state transitions, defaults, ordering, retries, cancellation, idempotency, and concurrent actions |
| Acceptance criteria | Observable trigger, test data/preconditions, measurable expected result, and negative/alternate outcome |
| Roles and authorization | Who can view/create/edit/delete/approve; ownership; access-denied behavior; audit expectations |
| Data and validation | Field type/format, requiredness, boundaries, duplicate handling, persistence, masking, retention, and migration |
| Errors and recovery | Validation, server/integration failures, timeouts, partial completion, user message, retry, and support path |
| Integrations | Contract owner, request/response, failure and timeout behavior, retries, versioning, and source of truth |
| Non-functional quality | Security/privacy, accessibility, performance/load, compatibility, observability, availability, localization, and compliance |
| Release and regression | Feature flags, rollout/rollback, migration, backward compatibility, analytics, monitoring, and impacted flows |

### 4. Inspect with the user lens

Walk the likely journey as each relevant user. Identify the point of confusion or loss of control, then turn it into a decision-seeking question. Consider:

- value and entry point: why use this, how find it, what happens if ineligible;
- clarity: labels, terminology, pricing/impact, confirmations, irreversible actions, and expectations;
- effort: required inputs, sensible defaults, progress, interruption/resume, and mobile constraints;
- control and recovery: edit/back/cancel/undo, clear errors, retry, support, and notification timing;
- trust and inclusion: consent, privacy, security signals, accessibility, language/locale, and vulnerable/low-connectivity users;
- completion: proof of success, resulting state, downstream effects, and what the user should do next.

Do not ask superficial design-preference questions (for example, color or button placement) unless the PRD states a user outcome that depends on them.

### 5. Form high-quality questions

For every finding, include the evidence, risk, owner, and a question that can be answered decisively. Prefer questions that distinguish meaningful alternatives:

- Weak: "Please clarify validation."
- Strong: "The PRD says the amount is required but gives no min/max or precision. Which values are accepted, and what result/message is expected for 0, a negative value, and a value above the limit?"

Classify each finding:

- **Blocking:** Different answers alter core behavior, expected result, compliance, data integrity, or test scope. Do not declare the PRD ready while one remains unresolved.
- **High:** Likely to create a material defect, harmful user outcome, or rework.
- **Medium:** Important edge case, usability, or operational decision; test/design can be parameterized temporarily.
- **Low:** Helpful refinement that does not change the safe core behavior.

Avoid duplicate questions. Combine related evidence into one answerable question, but keep separately owned decisions separate. Never present a question as a defect when the PRD explicitly answers it.

### 6. Synthesize readiness

Use judgment, not a numeric score:

- **READY:** Core user journey, business rules, expected outcomes, and significant risks are sufficiently defined for implementation and verification.
- **READY_WITH_CONDITIONS:** Core scope is usable, but the listed decisions must be resolved or explicitly parameterized before the affected work proceeds.
- **NOT_READY:** Missing or conflicting core behavior, acceptance criteria, ownership, or risk controls would force the team to guess.

## Required output

Write in the user's language and optimize for PM/PO/BA and operations readers. Start with a 2–4 sentence plain-language summary of the business value, the main decision, and the review conclusion. Explain any unavoidable technical term in ordinary language on first use. Combine business, user, and QE implications in the same decision; do not create separate review sections for each lens.

### 1. What is clear

List 3–6 concrete, evidence-backed strengths. Do not pad this section.

### 2. Quyết định cần chốt

Use this reader-friendly table by default. Phrase the decision in business language, state its user or operational consequence in `Nếu chưa chốt`, then put precise technical detail only in `Nguồn tham chiếu`. Use `Phải chốt trước test/release`, `Nên chốt`, or `Có thể bổ sung sau` rather than severity labels. Do not emit both this table and a second detailed question table.

| Mức độ cần chốt | Cần quyết định | Nếu chưa chốt | Nguồn tham chiếu |
|---|---|---|---|
| Phải chốt trước test/release | A concrete, answerable decision | Plain-language business or user impact | PRD §… / ticket comment / short evidence |

Order by urgency. Keep the table focused: normally 5–8 independent decisions. Combine related technical sub-questions under one business decision. Do not infer or assign an owner; include ownership only when the user explicitly asks for it.

### 3. Các tình huống cần chốt (optional)

Include this section **only** when it reveals a distinct journey, state transition, partial-failure behavior, or dependency that is not already clear from the questions table. Omit it for simple UI changes or when it merely restates the same questions.

Use plain language that a PM, PO, BA, or stakeholder can scan without QA terminology. For each important scenario, say what the PRD already defines and exactly what decision remains. Use `Đủ rõ`, `Cần làm rõ`, or `Chưa đề cập`.

| Tình huống | PRD đã nói gì | Cần chốt thêm | Mức độ rõ | Câu hỏi liên quan |
|---|---|---|---|---|
| Vào tính năng / thao tác thành công / dữ liệu trống / lỗi / gián đoạn | ... | ... | Đủ rõ / Cần làm rõ / Chưa đề cập | Q-01, Q-02 |

Omit irrelevant states. Add domain-specific situations such as approval, payment, delivery, or account recovery when relevant. Do not include implementation jargon such as "race condition" unless it is explained in the `Cần chốt thêm` column. Never repeat an item that adds no new decision beyond the questions table.

### 4. Readiness

- **Verdict:** READY / READY_WITH_CONDITIONS / NOT_READY
- **Reasoning:** Tie the conclusion to the decisions that must be made, not a count of findings.
- **Before implementation/testing:** List only `Phải chốt trước test/release` decisions in short action language.

## Guardrails

- Cite a PRD section, page, heading, or concise excerpt for every question. If no evidence can be located, label it `Context needed`, explain what source is missing, and do not infer an answer.
- Distinguish a missing requirement from a deliberate product trade-off. Ask who owns the decision instead of prescribing it.
- Do not convert assumptions into acceptance criteria, test cases, or implementation instructions.
- Flag contradictions explicitly with both conflicting sources and ask which source takes precedence.
- For sensitive domains (payments, health, identity, children, regulated data), elevate security, consent, auditability, retention, and failure/recovery questions when relevant.
