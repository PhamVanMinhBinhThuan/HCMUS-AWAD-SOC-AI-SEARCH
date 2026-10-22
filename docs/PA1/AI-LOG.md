# AI-LOG.md — PA#1 Proposal and Planning
## CSC13114 · 23KTPM1 · Phạm Văn Minh (23127228) · Trần Anh Khoa (23127395)

---

## 2026-10-22 — Initial proposal drafting and structuring

**Tool:** Antigravity (Google DeepMind AI coding assistant) in VS Code  
**Session goal:** Draft the full PA#1 proposal following the rubric for all six criteria, and produce a coherent two-page document.

**Context given to AI:**
- The PA#1 rubric (six criteria: Problem and users, LLM feature + cost, Scope, Plan and ownership, Risks, Technology choices).
- The project idea: a natural-language search console for SOC analysts backed by an LLM-to-SearchPlan pipeline.
- Team members: Phạm Văn Minh (23127228) and Trần Anh Khoa (23127395).

**AI proposed and I confirmed the following decisions:**

- **§1 Problem and users:** AI suggested using a named fictional persona (Mai, Tier-1 SOC analyst) instead of a generic category ("SOC staff") to satisfy the rubric's highest band. The overnight-shift VPN-failure triage scenario and the manual DSL editing workaround were proposed by AI; the student confirmed this accurately reflected a real SOC workflow.
- **§2 LLM feature:** AI proposed the NL-to-SearchPlan architecture (LLM outputs constrained JSON; Spring Boot validates and compiles deterministically; LLM never touches raw DSL). The `now-1h` vs `now-24h` silent error example, the 40/60 missed-event synthetic test fixture, and the 120-question bilingual benchmark design were all AI-proposed and student-approved.
- **§3 Scope:** AI drafted the in-scope and out-of-scope lists. Students confirmed the boundary (one reliable LLM search feature; not a full SOC platform).
- **§4 Plan:** AI generated six dated checkpoints (CP1 2026-10-26 through CP6 2027-01-04) with per-task owner assignments. Students reviewed the dates against the course calendar and confirmed the split (Minh: backend/LLM path; Khoa: data/evaluation/UI). AI flagged sequential dependencies between checkpoints.
- **§5 Risks:** AI proposed two project-specific risks (semantically wrong but valid plans; untrustworthy evaluation oracle) with start-this-week mitigations and objective warning signals. Generic risks ("time pressure") were explicitly rejected.
- **§6 Technology:** AI produced the technology table and calculated the per-request and 2,000-call LLM cost estimates using the official Google pricing page. The USD 10 API spending cap was a student decision.

**Student decisions (not AI):**
- Chose Elasticsearch (not a different search backend) because the team has prior familiarity.
- Chose Keycloak for authentication (off-the-shelf; not hand-written auth).
- Decided the project scope covers exactly two fixed roles (analyst / viewer), not a full RBAC system.
- Approved the `now-1h` vs `now-24h` error as the canonical cost-of-error example over other alternatives AI mentioned.
- Set the 120-question corpus size and the ≥90% / ≥95% semester targets.

**Changed / rejected by student:**
- AI initially drafted a broader scope including "follow-up suggestion" features; student removed these to keep focus on the one LLM search feature.
- AI suggested adding a Fine-tuning section under Technology; student rejected (out of scope for this semester, explicitly listed in §3 Out).

**Verification:** The final `PA1_SOC_AI_Search_Proposal.md` is 58 lines and fits within the two-page limit when rendered.  
**SELF_ASSESSMENT_REPORT.md** was drafted by AI and reviewed and adjusted by student; final claimed total: **92/100**.

---

## 2026-10-22 — Codex (VS Code) assistance: refinement pass

**Tool:** Codex in VS Code  
**Session goal:** Refine language, tighten phrasing, and cross-check internal consistency of the proposal document.

**AI proposed:**
- Tightened the Query Breakdown description in §2 to be more precise about what the analyst sees.
- Flagged that the §4 table header was inconsistent with the rubric's "Work, Owner and Date" format; corrected.
- Suggested adding the note about sequential checkpoint dependencies (the italicized footnote in §4).

**Student confirmed:** All changes were reviewed before accepting; no new business decisions were introduced.

**Changed:** Minor wording improvements; footnote added to §4 checkpoint table.  
**Not changed:** Core architecture, cost numbers, scope boundaries, and checkpoint dates remained as decided in the Antigravity session.

---

## Summary of AI use across this assignment

| Session | Tool | Role of AI | Role of Student |
|:--|:--|:--|:--|
| Proposal drafting | Antigravity | Drafted all six sections following rubric structure | Confirmed/rejected each element; made all scope/tech/date decisions |
| Refinement pass | Codex (VS Code) | Tightened language; caught one formatting inconsistency | Reviewed all edits before accepting |
| Self-assessment | Antigravity | Drafted evidence column and calibration note | Adjusted total from 100 to 92; owns all claims |

**Student owns and can explain:** the project concept (NL-to-SearchPlan for SOC triage), the architecture choices (SearchPlan JSON isolation, Spring Boot validation layer, Elasticsearch oracle), the checkpoint dates and owner assignments, and all scope decisions in §3.
