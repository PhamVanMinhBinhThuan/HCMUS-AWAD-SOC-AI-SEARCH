# SOC AI Search: Trustworthy Natural-Language Queries for SOC Triage

**CSC13114 | PA#1 - Project Proposal & Planning**

**Group:** Phạm Văn Minh (23127228) - Trần Anh Khoa (23127395)

**Repository:** https://github.com/PhamVanMinhBinhThuan/HCMUS-AWAD-SOC-AI-SEARCH

## 1. Problem and Users

Mai, a *fictional Tier-1 SOC analyst* on an overnight shift, must investigate repeated VPN login failures. To identify suspicious accounts and source IPs, she currently copies and edits Elasticsearch Query DSL, risking incorrect fields, filters or time windows. Our focused console accepts English/Vietnamese questions and shows exactly what it will search.

## 2. One Core LLM Feature and the Cost of Being Wrong

The core feature is **natural-language question -> validated SearchPlan -> Elasticsearch results**. For “Show failed logins in the last 24 hours”, the LLM proposes a constrained plan; Spring Boot validates it, compiles the query deterministically and displays the interpretation in **Query Breakdown** before execution. The LLM never submits executable DSL. Ambiguous high-impact conditions require confirmation.

A plan may pass schema checks but silently use `now-1h` instead of `now-24h`. In a planned synthetic fixture with 60 relevant events, this would omit 40 (66.7% recall loss), potentially falsely reassuring Mai and delaying escalation. She can correct and rerun the query, but cannot recover the delay.

We will test 120 bilingual questions, including ambiguous cases, against reference plans and expected event results. Targets are at least **90% critical-filter exact match**, **95% event recall**, **zero disallowed executions**, and clarification instead of silent execution for ambiguous high-impact requests.

## 3. Scope for This Semester

**In:** A bilingual React console; validated SearchPlan-to-Elasticsearch execution; roughly 10,000 synthetic events; fixed analyst/viewer login; Query Breakdown with correction and clarification; search, count, top-N and time-series queries; and a reproducible evaluation suite.

**Out:** Real enterprise data, live SIEM integration, automated response, fine-tuning, autonomous investigations, dashboards, AI summaries, suggestions, exports and role administration. This is one reliable LLM search feature, not a full SOC platform.

## 4. Six Checkpoints: Work, Owner and Date

| Checkpoint | Date | Owner and deliverable |
|:--|:--|:--|
| **CP1 - Foundations** | **2026-10-26** | Minh: repository, Docker/CI and SearchPlan schema; Khoa: synthetic data and 20 checked questions |
| **CP2 - Core path** | **2026-11-09** | Minh: validator, compiler and Gemini/mock integration; Khoa: React console and Query Breakdown |
| **CP3 - Data and oracle** | **2026-11-23** | Khoa: 120 labelled questions; Minh: oracle, login and query log; both: cross-review |
| **CP4 - Evaluation** | **2026-12-07** | Khoa: scoring runner and baseline; Minh: ambiguity confirmation gate |
| **CP5 - Validation** | **2026-12-21** | Khoa: correction UI and held-out evaluation; Minh: regression and correction-time tests |
| **CP6 - Delivery** | **2027-01-04** | Minh: deployment/demo; Khoa: cost report and final comparison |

Minh = Phạm Văn Minh; Khoa = Trần Anh Khoa. Dependencies are sequential, and each member reviews the other's labels.

## 5. Two Project-Ending Risks and Immediate Mitigations

1. **Semantically wrong but valid queries** could hide threats. This week, we will test 20 manually authored questions with Gemini, log field/time mismatches, and require confirmation for ambiguous high-impact requests.
2. **Unreliable ground truth** could invalidate evaluation. This week, we will freeze the synthetic generator, hand-check 20 reference queries and run an LLM-independent oracle.

## 6. Technology Choices and Budget

| Choice | Why this project needs it |
|:--|:--|
| **React + TypeScript** | Builds the bilingual console and editable Query Breakdown. |
| **Java 21 / Spring Boot** | Validates plans, handles authorization and compiles deterministic DSL. |
| **Elasticsearch, PostgreSQL, Keycloak** | Provide log search, audit history and fixed analyst/viewer access. |
| **Docker Compose + GitHub Actions** | Reproduce the stack and run tests/evaluation consistently. |
| **Gemini 3.1 Flash-Lite API** | Generates affordable structured plans; a deterministic mock is used in CI. |

**LLM cost:** Based on the [official Google pricing](https://ai.google.dev/gemini-api/docs/pricing), an assumed 1,200 input + 300 output tokens costs about **USD 0.00075/request**, or **USD 1.50 per 2,000 calls**. We will log actual usage and set an initial **USD 10 API cap**.
