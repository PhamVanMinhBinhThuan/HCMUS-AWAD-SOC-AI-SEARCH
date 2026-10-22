# SOC AI Search: Trustworthy Natural-Language Queries for SOC Triage

**CSC13114 | PA#1 - Project Proposal & Planning**

**Group:** Phạm Văn Minh (23127228) - Trần Anh Khoa (23127395)

**Repository:** https://github.com/PhamVanMinhBinhThuan/HCMUS-AWAD-SOC-AI-SEARCH

## 1. Problem and Users

Mai, a *fictional Tier-1 SOC analyst* on an overnight shift, investigates repeated VPN login failures. She currently copies and edits Elasticsearch Query DSL, risking incorrect fields, filters or time windows. Our console accepts English/Vietnamese questions and shows exactly what it will search.

## 2. One Core LLM Feature and the Cost of Being Wrong

The core feature is **natural-language question -> validated SearchPlan -> Elasticsearch results**. For “Show failed logins in the last 24 hours”, the LLM proposes a constrained plan; Spring Boot validates and deterministically compiles it, then shows **Query Breakdown** before execution. The LLM never submits DSL; ambiguous high-impact conditions require confirmation.

A valid plan may silently use `now-1h` instead of `now-24h`. In a planned fixture with 60 relevant events, this omits 40 (66.7% recall loss), potentially falsely reassuring Mai and delaying escalation. She can rerun it, but cannot recover the delay.

We will test 120 bilingual questions against reference plans and results. Targets: **90% critical-filter exact match**, **95% event recall**, **zero disallowed executions**, and clarification for ambiguous high-impact requests.

## 3. Scope for This Semester

**In:** Bilingual React console; validated SearchPlan-to-Elasticsearch execution; 10,000 synthetic events; fixed analyst/viewer login; Query Breakdown correction/clarification; search, count, top-N and time-series queries; reproducible evaluation.

**Out:** Real data, live SIEM integration, automated response, fine-tuning, autonomous investigations, dashboards, summaries, suggestions, exports and role administration.

## 4. Six Checkpoints: Work, Owner and Date

| Checkpoint | Date | Owner and deliverable |
|:--|:--|:--|
| **CP1 Foundations** | **2026-10-26** | Minh: repo, Docker/CI, schema; Khoa: data and 20 checked questions |
| **CP2 Core path** | **2026-11-09** | Minh: validator, compiler, Gemini/mock; Khoa: console and Query Breakdown |
| **CP3 Data/oracle** | **2026-11-23** | Khoa: 120 questions; Minh: oracle, login, query log; both: review |
| **CP4 Evaluation** | **2026-12-07** | Khoa: scoring/baseline; Minh: confirmation gate |
| **CP5 Validation** | **2026-12-21** | Khoa: correction UI/evaluation; Minh: regression/correction tests |
| **CP6 Delivery** | **2027-01-04** | Minh: deployment/demo; Khoa: cost report/final comparison |

Minh = Phạm Văn Minh; Khoa = Trần Anh Khoa. Dependencies are sequential; both review the labels.

## 5. Two Project-Ending Risks and Immediate Mitigations

1. **Wrong but valid queries** could hide threats. This week: test 20 authored questions with Gemini, log mismatches and require confirmation for ambiguous high-impact requests.
2. **Unreliable ground truth** could invalidate evaluation. This week: freeze the generator, check 20 reference queries and run an LLM-independent oracle.

## 6. Technology Choices and Budget

| Choice | Why this project needs it |
|:--|:--|
| **React/TypeScript** | Bilingual console and editable Query Breakdown. |
| **Java 21/Spring Boot** | Plan validation, authorization and deterministic DSL. |
| **Elasticsearch/PostgreSQL/Keycloak** | Log search, audit history and fixed-role access. |
| **Docker Compose/GitHub Actions** | Reproducible stack and evaluation. |
| **Gemini 3.1 Flash-Lite** | Affordable structured plans; deterministic CI mock. |

**LLM cost:** [Google pricing](https://ai.google.dev/gemini-api/docs/pricing) gives an estimated **USD 0.00075/request**, or **USD 1.50 per 2,000 calls**; we will log usage and cap the initial budget at **USD 10**.
