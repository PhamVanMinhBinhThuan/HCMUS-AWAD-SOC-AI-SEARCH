# PA#1 - SELF_ASSESSMENT_REPORT

**Course:** CSC13114 - Proposal and Planning  
**Students:** Phạm Văn Minh (23127228) - Trần Anh Khoa (23127395) | **Submission:** Group  
**Project:** SOC AI Search: Trustworthy Natural-Language Queries for SOC Triage  
**Evidence file:** [PA1_SOC_AI_Search_Proposal.md](PA1_SOC_AI_Search_Proposal.md)  
**Repository:** https://github.com/PhamVanMinhBinhThuan/HCMUS-AWAD-SOC-AI-SEARCH

**Self-assessed total: 92/100.** Each claim below refers to **proposal quality**, not completion of proposed experiments. The instructor determines the actual mark.

| Rubric criterion | Maximum | Claimed | Specific evidence for the claim |
|:--|--:|--:|:--|
| **1. Problem and users** | 20 | **17** | Proposal **§1**: named fictional persona *Mai*, Tier-1 SOC analyst on an overnight VPN incident; precisely stated manual-DSL problem and existing workaround. Deduct 3: persona is fictional (not an interviewed real user), so the authenticity of the problem statement is unverified; the workaround is plausible but not confirmed with a practitioner. |
| **2. LLM feature and cost of error** | 25 | **22** | Proposal **§2**: one NL-to-SearchPlan feature, explicit execution boundary, semantically wrong but valid `now-1h` example, **40/60 missed synthetic events** as a *future test fixture*, named affected analyst, reversibility and lost time; **120-case benchmark**, evaluation measures and semester targets. Deduct 3: cost figures (40/60 events, correction time) are planned synthetic fixtures not yet constructed; the consequence for the analyst is clearly named, but the "cannot recover the response delay" claim remains unquantified. |
| **3. Scope in and out** | 15 | **15** | Proposal **§3**: explicit in/out lists; every in-scope item maps to a §4 task (search path CP1–CP3, corpus/oracle CP3, evaluation CP4, mitigation CP4–CP5, demo CP6). Consistent with plan. |
| **4. Plan and ownership** | 20 | **18** | Proposal **§4**: **six** dated checkpoints from foundations (2026-10-26) to delivery (2027-01-04), each split into tasks with one named owner per task (Minh: backend/LLM path, Khoa: data/evaluation/UI); sequential dependencies noted. Deduct 2: dates have not been cross-checked against mid-term or other course deadlines; CP1 (2026-10-26) is 4 days away, leaving very little buffer if the proposal is still being refined. |
| **5. Risks** | 10 | **10** | Proposal **§5**: two failure-causing *project-specific* risks (undetected semantic errors; invalid evaluation oracle), immediate mitigations actionable this week, and objective warning signals (exact-match below 90%; inconsistent oracle counts). |
| **6. Technology choices** | 10 | **10** | Proposal **§6**: every technology tied to this workflow; **Gemini 3.1 Flash-Lite** (`gemini-3.1-flash-lite`) is a real available API model (confirmed at `ai.google.dev`), pricing of $0.25/1M input and $1.50/1M output matches the proposal; per-request and 2,000-call cost estimates computed and a USD 10 cap set. |
| **TOTAL** | **100** | **92** | 17 + 22 + 15 + 18 + 10 + 10 = **92** |

## What we did not manage / remaining uncertainties

- **Planned, not measured:** The search path, 120-question benchmark, 60/40-error fixture and semantic-safety improvements are semester *deliverables*, not completed work. No performance measurements are fabricated.
- **Persona validation:** *Mai* is a fictional but representative persona; no real SOC analyst was interviewed for this proposal.
- **Model confirmed:** "Gemini 3.1 Flash-Lite" (`gemini-3.1-flash-lite`) exists and matches the pricing in the proposal; deduction removed from §6.
- **Variable LLM bill:** The listed rate is sourced from Google's pricing page; actual request tokens, retries and final cost are estimates to be measured.
- **AI use:** Antigravity and Codex (VS Code) were used to draft and refine all six proposal sections. All architecture, scope, date, and technology decisions were reviewed and confirmed by the students. See `AI-LOG.md` for a full session-by-session record.

**Calibration note:** The 92-point claim means each rubric criterion is directly addressed in the *proposal*, with honest deductions for items not yet verified or not yet constructed. It is not a representation that the instructor has awarded 92 or that the semester implementation has been completed.
