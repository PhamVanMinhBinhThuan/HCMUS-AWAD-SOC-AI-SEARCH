# PA#1 - SELF_ASSESSMENT_REPORT

**Course:** CSC13114 - Proposal and Planning  
**Student:** Phạm Văn Minh (23127228) - Trần Anh Khoa (23127395) | **Submission:** Group  
**Project:** SOC AI Search: Trustworthy Natural-Language Queries for SOC Triage  
**Evidence file:** [PA1_SOC_AI_Search_Proposal.md](PA1_SOC_AI_Search_Proposal.md)  
**Baseline source:** https://github.com/PhamVanMinhBinhThuan/soc-ai-search

**Self-assessed target: 100/100.** Each claim below refers to **proposal quality/planned work**, not completion of proposed experiments. The instructor determines the actual mark.

| Rubric criterion | Maximum | Claimed | Specific evidence for the claim |
|:--|--:|--:|:--|
| **1. Problem and users** | 20 | **20** | Proposal **§1**: named fictional persona *Mai*, Tier-1 SOC analyst on an overnight VPN incident; precisely stated manual-DSL problem and existing workaround. |
| **2. LLM feature and cost of error** | 25 | **25** | Proposal **§2**: one NL-to-SearchPlan feature, explicit execution boundary, semantically wrong but valid `now-1h` example, **40/60 missed synthetic events** as a *future test fixture*, named affected analyst, reversibility and lost time; **120-case benchmark**, evaluation measures and targets. |
| **3. Scope in and out** | 15 | **15** | Proposal **§3**: explicit paired in/out lists, narrowed semester contribution, baseline-vs-new-work distinction aligned to the six-step plan. |
| **4. Plan and ownership** | 20 | **20** | Proposal **§4**: **six** individually dated checkpoints; one named accountable owner on every row; dependency ordering and verifiable deliverables. Dates are internal targets pending official calendar verification. |
| **5. Risks** | 10 | **10** | Proposal **§5**: two failure-causing *project-specific* risks (undetected semantic errors; invalid evaluation oracle), immediate mitigations and objective warning signals. |
| **6. Technology choices** | 10 | **10** | Proposal **§6**: every technology tied to this workflow; **Gemini 3.1 Flash-Lite** named with official pricing URL, explicit token assumptions, per-call/2,000-call estimates and a USD 10 API budget cap. |
| **TOTAL** | **100** | **100** | **20 + 25 + 15 + 20 + 10 + 10 = 100**. |

## What I did not manage / remaining uncertainties

- **Official dates unavailable:** The supplied rubric does not include the course's six milestone dates. The dated plan is actionable but must be reconciled with the instructor's calendar; full marks for calendar compatibility cannot be guaranteed until then.
- **Planned, not measured:** The 120-question benchmark, 60/40-error fixture and proposed semantic-safety improvements are semester *deliverables*, not already completed test outcomes. There are no fabricated performance measurements in the proposal.
- **Prior-work and permission check:** The existing SOC AI Search code predates CSC13114. Its reuse must satisfy course academic-integrity rules and any applicable intellectual-property limitations from the original internship project.
- **Variable LLM bill:** The listed rate is sourced from Google's pricing page, while request tokens, retries and final cost are estimates to be measured later.

**Calibration note:** The 100-point claim means each rubric criterion is directly addressed in the *proposal*. It is not a representation that the instructor has awarded 100 or that the semester implementation has already been completed.
