# PA#1 - SELF_ASSESSMENT_REPORT

**Course:** CSC13114 - Proposal and Planning  
**Students:** Phạm Văn Minh (23127228) - Trần Anh Khoa (23127395) | **Submission:** Group  
**Project:** SOC AI Search: Trustworthy Natural-Language Queries for SOC Triage  
**Evidence file:** [PA1_SOC_AI_Search_Proposal.md](PA1_SOC_AI_Search_Proposal.md)  
**Repository:** https://github.com/PhamVanMinhBinhThuan/HCMUS-AWAD-SOC-AI-SEARCH

**Self-assessed target: 100/100.** Each claim below refers to **proposal quality/planned work**, not completion of proposed experiments. The instructor determines the actual mark.

| Rubric criterion | Maximum | Claimed | Specific evidence for the claim |
|:--|--:|--:|:--|
| **1. Problem and users** | 20 | **20** | Proposal **§1**: named fictional persona *Mai*, Tier-1 SOC analyst on an overnight VPN incident; precisely stated manual-DSL problem and existing workaround. |
| **2. LLM feature and cost of error** | 25 | **25** | Proposal **§2**: one NL-to-SearchPlan feature, explicit execution boundary, semantically wrong but valid `now-1h` example, **40/60 missed synthetic events** as a *future test fixture*, named affected analyst, reversibility and lost time; **120-case benchmark**, evaluation measures and targets. |
| **3. Scope in and out** | 15 | **15** | Proposal **§3**: explicit in/out lists; every in-scope item maps to a §4 task (search path CP1-CP3, corpus/oracle CP3, evaluation CP4, mitigation CP4-CP5, demo CP6). |
| **4. Plan and ownership** | 20 | **20** | Proposal **§4**: **six** dated checkpoints from foundations to delivery, each split into tasks with one named owner per task (Minh: backend/LLM path, Khoa: data/evaluation/UI); sequential dependencies; labels written and verified by different members. |
| **5. Risks** | 10 | **10** | Proposal **§5**: two failure-causing *project-specific* risks (undetected semantic errors; invalid evaluation oracle), immediate mitigations and objective warning signals. |
| **6. Technology choices** | 10 | **10** | Proposal **§6**: every technology tied to this workflow; **Gemini 3.1 Flash-Lite** named with official pricing URL, explicit token assumptions, per-call/2,000-call estimates and a USD 10 API budget cap. |
| **TOTAL** | **100** | **100** | **20 + 25 + 15 + 20 + 10 + 10 = 100**. |

## What we did not manage / remaining uncertainties

- **Planned, not measured:** The search path, 120-question benchmark, 60/40-error fixture and semantic-safety improvements are semester *deliverables*, not completed work or test outcomes. There are no fabricated performance measurements in the proposal.
- **Variable LLM bill:** The listed rate is sourced from Google's pricing page, while request tokens, retries and final cost are estimates to be measured later.

**Calibration note:** The 100-point claim means each rubric criterion is directly addressed in the *proposal*. It is not a representation that the instructor has awarded 100 or that the semester implementation has already been completed.
