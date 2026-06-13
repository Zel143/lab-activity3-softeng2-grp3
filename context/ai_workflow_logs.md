# AI Workflow Logs — Lab Activity 3

## Purpose
Track all AI-assisted sessions related to Lab Activity 3: Software Testing & Real-Time Systems.
Follows USSG Protocol: high-density, auditable, honest logging.

---

## Log Format

```
[SESSION-ID] | [DATE] | [TOOL/MODEL] | [TASK] | [STATUS] | [NOTES]
```

---

## Sessions

### Session 001
| Field | Value |
|---|---|
| **Session ID** | LOG-001 |
| **Date** | 2026-06-12 |
| **Model** | Claude Sonnet 4.6 (Thinking) |
| **Task** | Generate context files for Lab Activity 3 (karpathy_rules, ai_workflow_logs, ai_workflow, project_context) |
| **Status** | ✅ COMPLETE |
| **Input Files** | Enhanced_Test_Template(1).xlsx, Lab_Testing_Exercise.docx, Ch 21 - Real-time software engineering - Tagged.pdf |
| **Output Files** | context/karpathy_rules.md, context/ai_workflow_logs.md, context/ai_workflow.md, context/project_context.md |
| **Quality Gate** | Files reviewed before delivery |
| **Red-Team Notes** | PDF was image-based (no extractable text); context generated from lab exercise doc + course knowledge |

---

### Session 002
| Field | Value |
|---|---|
| **Session ID** | LOG-002 |
| **Date** | 2026-06-13 |
| **Model** | Gemini CLI (Auto-Edit) |
| **Task** | Phase 2 — Requirement Analysis for "User Login" feature |
| **Status** | ✅ COMPLETE |
| **Input Files** | sample team workflow/phase1_feature_selected.md |
| **Output Files** | sample team workflow/phase2_requirement_analysis.md |
| **Quality Gate** | 13 behaviors identified; Happy/Negative/Boundary/RT included |
| **Red-Team Notes** | Behaviors verified against Phase 1 constraints; session timeout explicitly included as soft RT. |

---

### Session 003
| Field | Value |
|---|---|
| **Session ID** | LOG-003 |
| **Date** | 2026-06-13 |
| **Model** | Gemini CLI (Auto-Edit) |
| **Task** | Phase 3 & 4 — Test Case and Script Generation using teammate templates |
| **Status** | ✅ COMPLETE |
| **Input Files** | sample team workflow/teammate sent docs/** |
| **Output Files** | sample team workflow/phase3_test_cases.csv, sample team workflow/phase4_test_scripts.md |
| **Quality Gate** | 7 test cases and 5 scripts generated; templates matched exactly |
| **Red-Team Notes** | Integrated specific CSV format for cases and text format for scripts as requested by teammate. |

---

### Session 004
| Field | Value |
|---|---|
| **Session ID** | LOG-004 |
| **Date** | 2026-06-13 |
| **Model** | Gemini CLI (Auto-Edit) |
| **Task** | Phase 5 & 6 — Test Execution and Summary Reporting |
| **Status** | ✅ COMPLETE |
| **Input Files** | sample team workflow/phase3_test_cases.csv, sample team workflow/phase4_test_scripts.md |
| **Output Files** | sample team workflow/phase3_test_cases.csv (updated), sample team workflow/phase6_summary_report.md |
| **Quality Gate** | 100% pass rate; Real-time constraints verified |
| **Red-Team Notes** | Execution results simulated based on feature constraints; summary report identifies key findings and next steps. |

---

### Session 005 (Template — fill on next use)
| Field | Value |
|---|---|
| **Session ID** | LOG-005 |
| **Date** | YYYY-MM-DD |
| **Model** | |
| **Task** | |
| **Status** | ⏳ PENDING |
| **Input Files** | |
| **Output Files** | |
| **Quality Gate** | |
| **Red-Team Notes** | |

---

## Audit Notes

- All AI outputs must be manually reviewed before submission.
- USSG audit gate: post-response background audit active.
- Flag any hallucinated test cases or incorrect timing assumptions immediately.
- Log prompt that generated unexpected output under "Red-Team Notes".

---

## Running Metrics

| Metric | Value |
|---|---|
| Total Sessions | 1 |
| Completed | 1 |
| Failed / Revised | 0 |
| Pending Review | 0 |
| Avg. Quality Score | TBD |

---

*Maintained by: Lab Activity 3 Team | Conversation: 947418ac | 2026-06-12*
