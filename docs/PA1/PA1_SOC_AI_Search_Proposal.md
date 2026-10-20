# SOC AI Search: Trustworthy Natural-Language Queries for SOC Triage

**CSC13114 | PA#1 - Project Proposal & Planning**

**Group Submission:** Phạm Văn Minh (23127228) - Trần Anh Khoa (23127395)

**Repository:** https://github.com/PhamVanMinhBinhThuan/HCMUS-AWAD-SOC-AI-SEARCH

## 1. Problem and Users

**Named representative user and situation:** Mai, a *fictional Tier-1 SOC analyst*, is on the overnight monitoring shift when repeated VPN login failures require triage. **One-sentence problem:** To identify suspicious accounts and source IPs, Mai must manually write or adapt Elasticsearch Query DSL, risking incorrect field names, time windows or filters before she can investigate. **Current workaround:** copy an older DSL query, edit the conditions, run it and manually check whether its results match the intended question. **Product:** a focused SOC search console that accepts English/Vietnamese investigative questions and shows precisely what it will search.

## 2. One Core LLM Feature - and the Cost of Being Wrong

**Natural-language question -> validated SearchPlan -> Elasticsearch results.** For "Show failed logins in the last 24 hours", the LLM proposes a constrained JSON `SearchPlan` with `mode=search`, `event_type=[failed_login]`, and `timestamp=[now-24h, now]`. The LLM **never submits executable DSL**. Spring Boot strictly parses and validates the SearchPlan (schema, allowlisted fields, time/size limits), compiles the Elasticsearch DSL deterministically, and executes it. **Query Breakdown** displays the interpreted filters so the analyst can verify or correct them; an ambiguous high-impact condition will require clarification/confirmation.

**Concrete failure cost:** A plan can pass every schema check yet silently select `now-1h` instead of `now-24h`. Consider a **planned synthetic test fixture** with 60 relevant failed-login events, 40 of which occurred between 1 and 24 hours ago. The wrong plan omits **40/60 events (66.7% recall loss)** and may falsely reassure Mai during triage. She can correct and rerun the query (at least one extra investigation step and API call), **but cannot recover the response delay**. The 60/40 counts illustrate a *test case to construct*, not observed production results. The cost to the analyst is missed evidence and additional investigation time; downstream responders may receive a late escalation.

**How we will know:** Create **120 labeled questions** (60 English, 60 Vietnamese, including 20 ambiguous/adversarial cases) with reference SearchPlans and deterministic expected event IDs/counts. Report (i) exact match of critical fields/time ranges, (ii) event-level recall and missed-event count, (iii) disallowed-plan execution count, (iv) median correction time, and (v) latency and billed tokens. **Semester targets, not current results:** >=90% critical-filter exact match for unambiguous requests, >=95% event recall on the held-out cases, **0 disallowed queries executed**, and explicit clarification instead of silent execution for ambiguous high-impact requests.

## 3. Scope for This Semester

**In:** (1) Build the end-to-end search path: React console with Query Breakdown, Spring Boot SearchPlan validator and deterministic DSL compiler, Elasticsearch loaded with roughly 10,000 seeded **synthetic** events, and login with fixed analyst/viewer roles; (2) support basic bilingual event search plus `count`, `top_n` and time-series aggregation; (3) build the labeled test corpus, oracle queries and reproducible evaluation runner; (4) add semantic-error review/clarification and regression tests; (5) demonstrate results, corrections, model latency and API expense.

**Out:** Real enterprise SOC data; live SIEM integrations; automated incident blocking/response; fine-tuning; autonomous multi-turn investigations; dashboards, AI summaries, follow-up suggestions, CSV exports; role administration beyond the two fixed roles. This is **one reliable LLM search feature**, not a full SOC platform.

## 4. Six Checkpoints: Work, Owner and Date

| Checkpoint | Date | Work - owner |
|:--|:--|:--|
| **CP1 - Foundations** | **2026-10-26** | Proposal - Khoa; repository, Docker Compose stack and CI (lint + tests) - Minh; SearchPlan JSON schema and field allowlist - Minh; seeded synthetic event generator and 20 hand-checked questions with reference DSL/expected event IDs - Khoa |
| **CP2 - Core search path** | **2026-11-09** | SearchPlan validator and deterministic DSL compiler (search, `count`, `top_n`, time-series) with unit tests - Minh; Gemini call producing SearchPlans, plus deterministic mock for CI - Minh; React console: question input, results, Query Breakdown - Khoa |
| **CP3 - Data & oracle** | **2026-11-23** | 120 labeled questions with reference SearchPlans, dev/held-out split - Khoa; LLM-independent oracle runner (expected IDs/counts) - Minh; Keycloak login and PostgreSQL query log (plan, tokens, latency) - Minh; cross-review of each other's labels/oracle - Minh, Khoa |
| **CP4 - Evaluation** | **2026-12-07** | CI scoring runner (exact match, recall, disallowed count, latency, tokens) - Khoa; baseline run and failure analysis - Khoa; ambiguity detection and confirmation gate in validator - Minh |
| **CP5 - Mitigation & validation** | **2026-12-21** | Confirmation/correction UI in Query Breakdown - Khoa; regression tests from baseline failures - Minh; held-out evaluation and failure-case write-up - Khoa; correction-time test with 3-5 users - Minh |
| **CP6 - Delivery** | **2027-01-04** | Reproducible deployment and demo - Minh; token/cost report against budget - Khoa; final report: baseline vs. mitigated comparison, limitations, what changed and why - Khoa |

*Minh = Phạm Văn Minh, Khoa = Trần Anh Khoa. Dependencies are sequential (search path -> oracle -> baseline -> mitigation -> held-out evaluation); labels are written and verified by different members.*

## 5. Two Project-Ending Risks and Immediate Mitigations

1. **Semantically wrong but valid queries** could hide threats despite successful validation, making the tool unsafe for triage. **Start this week:** write 20 representative questions with manually authored reference DSL, run them through Gemini with a draft prompt and schema in a standalone script, and log field/time mismatches; the product then surfaces Query Breakdown and blocks automatic execution of ambiguous high-impact requests until confirmed. **Warning signal:** critical-filter exact-match below 90% in pilot tests.
2. **Untrustworthy evaluation ground truth** could make a polished demo impossible to assess: synthetic events, labels and expected results might disagree. **Start this week:** write the seeded event generator and freeze its output, hand-verify 20 reference queries and expected event IDs, keep development/held-out questions separate, and run the oracle independently of LLM output. **Warning signal:** reference queries produce inconsistent counts across repeat runs.

## 6. Technology Choices and Budget

| Choice | Why this project needs it |
|:--|:--|
| **React + TypeScript** | Console that shows the SearchPlan interpretation (Query Breakdown) and lets analysts correct it. |
| **Java 21 / Spring Boot** | Enforce schema/business validation, authorization and deterministic DSL compilation. |
| **Elasticsearch** | Execute time-bounded log filters and count/top-N/time-series queries; provide oracle event IDs. |
| **PostgreSQL** | Retain query history, corrections and reproducible audit evidence. |
| **Keycloak** | Off-the-shelf login and fixed analyst/viewer roles instead of hand-written auth; prevents unauthorized log access. |
| **Gemini 3.1 Flash-Lite API (proposed)** | Affordable structured JSON generation for the bilingual SearchPlan task; use a deterministic mock during CI. |
| **Docker Compose + GitHub Actions** | Recreate the stack and automatically rerun evaluation/regression checks. |

**LLM cost (official [Google pricing](https://ai.google.dev/gemini-api/docs/pricing), standard paid tier):** USD **0.25 / 1M input tokens** and **1.50 / 1M billed output tokens**. At an *assumed* 1,200 input + 300 output tokens per request: **USD 0.00075/request**, or **USD 1.50 for 2,000 calls** (excluding retries, infrastructure and pricing changes). Log actual tokens; set an initial **USD 10 API spending cap**. This is a budget estimate, not a measured deployment bill.
