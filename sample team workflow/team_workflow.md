# 🧪 Sample Team Workflow
## Lab Activity 3 — Software Testing Exercise
### Real-Time Software Engineering (Chapter 21)

> **How to use this file:**
> This is the team's operational playbook. Work through each phase together.
> Reference the `context/` files at every phase gate before moving forward.
> Update the **Team Status Board** as you complete each step.

---

## 👥 Team Roles

| Role | Responsibility | Owner |
|---|---|---|
| **Test Lead** | Owns test strategy, final review gate | [Name] |
| **Test Designer** | Writes test cases using AI workflow | [Name] |
| **Script Developer** | Converts test cases to runnable scripts | [Name] |
| **Executor** | Runs scripts, records results in xlsx template | [Name] |
| **Reviewer** | Red-teams AI output, validates results | [Name] |

> ℹ️ In small teams, one person can hold multiple roles. Assign before starting Phase 1.

---

## 📋 Team Status Board

| Phase | Status | Owner | Notes |
|---|---|---|---|
| 0 — Setup | ✅ | All | Context files ready in `context/` |
| 1 — Feature Selection | ✅ | Test Lead | **User Login** selected → see `phase1_feature_selected.md` |
| 2 — Requirement Analysis | ✅ | Test Designer | Completed in `phase2_requirement_analysis.md` |
| 3 — Test Case Writing | ✅ | Test Designer | Completed in `phase3_test_cases.csv` |
| 4 — Script Development | ✅ | Script Developer | Completed in `phase4_test_scripts.md` |
| 5 — Execution | ✅ | Executor | Completed in `phase5_test_execution.md` |
| 6 — Review & Report | ✅ | Reviewer + Lead | Summary generated in `phase6_summary_report.md` |

**Status Legend:** ⏳ Not Started | 🔄 In Progress | ✅ Done | ❌ Blocked

---

## Phase 0 — Team Setup (Do This First, Together)

**Time estimate:** 15 minutes

### Checklist
- [ ] All team members read [`context/project_context.md`](../context/project_context.md)
- [ ] All team members read [`context/karpathy_rules.md`](../context/karpathy_rules.md)
- [ ] Test Lead walks through [`context/ai_workflow.md`](../context/ai_workflow.md)
- [ ] Team agrees on AI tool to use (Claude, Copilot, ChatGPT, etc.)
- [ ] Team agrees on test script format (manual checklist / Selenium / Postman / plain Python)
- [ ] Roles assigned (fill table above)

### Gate ✅
> All members have read the context files and roles are assigned before proceeding.

---

## Phase 1 — Feature Selection

**Owner:** Test Lead
**Time estimate:** 10 minutes

### Step 1.1 — Pick a Feature
Choose **one** feature from this list (or propose your own):

| # | Feature | Real-Time Element | Difficulty |
|---|---|---|---|
| A | **User Login** | Session timeout (soft RT) | 🟢 Easy |
| B | **User Registration** | Email validation response time | 🟢 Easy |
| C | **Sensor Data Polling** | Periodic sampling deadline | 🔴 Hard |
| D | **Event Notification Push** | Interrupt-driven response | 🟡 Medium |
| E | **Session Auto-Logout** | Timer-based state change | 🟡 Medium |
| F | **Concurrent Cart Update** | Shared resource / race condition | 🔴 Hard |

> **Team Decision — Selected Feature:**
> ```
> Feature: ___________________________________
> Reason:  ___________________________________
> ```

### Step 1.2 — Write the Feature Description
Fill this in as a team:

```
Feature Name:
System/App:
Brief Description:
User Role(s) Involved:
Key Inputs:
Key Outputs:
Known Constraints (timing, security, load):
Real-Time Concern (if any):
```

### Gate ✅
> Feature selected and described before proceeding to Phase 2.

---

## Phase 2 — Requirement Analysis (AI-Assisted)

**Owner:** Test Designer
**Reference:** [`context/ai_workflow.md`](../context/ai_workflow.md) → Phase 1

### Step 2.1 — Manual Analysis First
Before touching AI:
- [ ] List at least 3 happy path scenarios (write on whiteboard/doc)
- [ ] List at least 2 failure/error scenarios
- [ ] List at least 1 boundary condition
- [ ] List at least 1 timing or concurrency concern (if applicable)

### Step 2.2 — AI Prompt (Phase 1 Template)
Use this prompt:

```
Feature: [SELECTED FEATURE NAME]
Description: [YOUR FEATURE DESCRIPTION FROM PHASE 1]
Constraints: [PASTE CONSTRAINTS FROM PHASE 1]

Generate a list of testable behaviors, including:
- Happy path scenarios
- Boundary conditions
- Failure/negative scenarios
- Real-time / timing-sensitive scenarios (if applicable)
```

### Step 2.3 — Red-Team the AI Output
- [ ] Reviewer compares AI list vs. team's manual list
- [ ] Identify what AI missed
- [ ] Add missing behaviors to the final list

### Output — Confirmed Behavior List:
```
1.
2.
3.
4.
5.
6. (add more as needed)
```

### Gate ✅
> At least 5 confirmed testable behaviors before proceeding.

---

## Phase 3 — Test Case Writing (AI-Assisted)

**Owner:** Test Designer
**Reference:** [`context/ai_workflow.md`](../context/ai_workflow.md) → Phase 2
**Template:** [`Enhanced_Test_Template(1).xlsx`](../Enhanced_Test_Template(1).xlsx)

### Step 3.1 — Generate Test Cases
For each behavior from Phase 2, use this AI prompt:

```
Behavior to test: [BEHAVIOR FROM LIST]
System: [SYSTEM NAME / FEATURE]

Generate a test case in this format:
- Test Case ID: TC-00X
- Feature:
- Description:
- Preconditions:
- Test Steps: (numbered)
- Expected Result:
- Pass/Fail Criteria:
```

### Step 3.2 — Record in Excel Template
Open `Enhanced_Test_Template(1).xlsx` and fill in each test case.

### Step 3.3 — Quality Check
- [ ] Minimum **5 test cases** total
- [ ] At least **1 negative/failure** test case (what happens when it breaks?)
- [ ] At least **1 boundary condition** test (edge of valid range)
- [ ] All expected results are **specific and measurable** (not "it works")
- [ ] Reviewer signs off on each test case

### Sample Test Case (Login Feature):

| Field | Value |
|---|---|
| **Test Case ID** | TC-001 |
| **Feature** | User Login |
| **Description** | Valid credentials → successful login |
| **Preconditions** | User account exists; system is running |
| **Test Steps** | 1. Navigate to login page. 2. Enter valid username. 3. Enter valid password. 4. Click "Login". |
| **Expected Result** | User is redirected to dashboard within 2 seconds |
| **Pass/Fail Criteria** | PASS if dashboard loads ≤ 2s with user's name displayed; FAIL otherwise |

### Gate ✅
> All 5+ test cases reviewed and entered in template before proceeding.

---

## Phase 4 — Test Script Development (AI-Assisted)

**Owner:** Script Developer
**Reference:** [`context/ai_workflow.md`](../context/ai_workflow.md) → Phase 3

### Step 4.1 — Choose Script Format

| Option | When to Use |
|---|---|
| **Manual checklist** | No automation tools available |
| **Python (unittest/pytest)** | Backend / API testing |
| **Selenium (Python/JS)** | Browser UI testing |
| **Postman collection** | REST API testing |
| **Bash / PowerShell script** | CLI or system-level testing |

> **Team Decision — Script Format:**
> ```
> Format: ___________________
> ```

### Step 4.2 — Generate Scripts with AI
For each test case, use this prompt:

```
Test Case ID: TC-00X
Tool/Framework: [CHOSEN TOOL]
Language: [LANGUAGE]

Convert this test case into a runnable test script.
Include: setup, steps, assertions, teardown.

Test Case:
[PASTE FULL TEST CASE HERE]
```

### Step 4.3 — Force-Fail Validation (Karpathy Rule)
Before marking script as done:
- [ ] Run script against a **broken** system / wrong input → it **must FAIL** ❌
- [ ] Fix the system → run again → it **must PASS** ✅
- [ ] If it passes on broken input → the script is wrong. Fix it.

### Gate ✅
> All scripts run successfully and pass the force-fail validation check.

---

## Phase 5 — Test Execution

**Owner:** Executor
**Reference:** [`Enhanced_Test_Template(1).xlsx`](../Enhanced_Test_Template(1).xlsx)

### Step 5.1 — Environment Check
- [ ] System under test is deployed/running
- [ ] Test data is prepared (accounts, sample inputs, etc.)
- [ ] All scripts are accessible and runnable

### Step 5.2 — Execute Each Script
For each test case:
1. Run the script / follow the manual steps
2. Record **actual result**
3. Assign status: `PASS` / `FAIL` / `BLOCK` / `SKIP`
4. For FAIL: capture screenshot or error log

### Step 5.3 — Log Results in Excel Template
Fill in the results columns in `Enhanced_Test_Template(1).xlsx`:
- Actual Result
- Status
- Notes / Defect ID (if failed)

### Gate ✅
> All test cases executed and results recorded in the template.

---

## Phase 6 — Review & Report

**Owner:** Reviewer + Test Lead
**Reference:** [`context/ai_workflow.md`](../context/ai_workflow.md) → Phase 5
**Reference:** [`context/ai_workflow_logs.md`](../context/ai_workflow_logs.md)

### Step 6.1 — Generate Summary with AI
Use this prompt:

```
Here are our test results:
- Total cases: X
- Passed: X
- Failed: X
- Blocked: X

Features tested: [LIST]
Key failures observed: [DESCRIBE]

Generate a brief test summary including:
- Summary table
- Key findings
- Root causes for failures (if known)
- Recommended next steps
```

### Step 6.2 — Human Review of AI Summary
- [ ] Reviewer compares AI summary to actual raw results in template
- [ ] Correct any inaccuracies
- [ ] Add team observations AI missed

### Step 6.3 — Log the AI Session
Update [`context/ai_workflow_logs.md`](../context/ai_workflow_logs.md) with:
- Session ID (next in sequence)
- Date
- Model used
- Task completed
- Red-team notes

### Step 6.4 — Final Deliverables Checklist
- [ ] `Enhanced_Test_Template(1).xlsx` — completed with all results
- [ ] Test scripts saved in project folder
- [ ] `context/ai_workflow_logs.md` — updated
- [ ] Summary report written / attached
- [ ] All files committed / submitted

### Gate ✅
> All deliverables complete. Test Lead does final sign-off.

---

## ⚠️ Common Team Pitfalls

| Pitfall | Prevention |
|---|---|
| Accepting AI test cases without review | Always red-team AI output (Karpathy Rule #1) |
| Writing tests that only test happy paths | Require 1 negative + 1 boundary per feature |
| Scripts that pass on broken input | Force-fail validation (Phase 4, Step 4.3) |
| Not logging which AI was used | Update `ai_workflow_logs.md` every session |
| Last-minute scripting rush | Scripts must pass force-fail BEFORE execution phase |
| Real-time assumptions without measurement | Timing = profiler only, not visual inspection |

---

## 📎 Quick Reference Links

| Resource | Path |
|---|---|
| Project Context | [`context/project_context.md`](../context/project_context.md) |
| Karpathy Rules | [`context/karpathy_rules.md`](../context/karpathy_rules.md) |
| AI Workflow | [`context/ai_workflow.md`](../context/ai_workflow.md) |
| AI Session Logs | [`context/ai_workflow_logs.md`](../context/ai_workflow_logs.md) |
| Test Template | [`Enhanced_Test_Template(1).xlsx`](../Enhanced_Test_Template(1).xlsx) |
| Lab Instructions | [`Lab_Testing_Exercise.docx`](../Lab_Testing_Exercise.docx) |
| Course Reference | [`Ch 21 - Real-time software engineering - Tagged.pdf`](../Ch%2021%20-%20Real-time%20software%20engineering%20-%20Tagged.pdf) |

---

*Team Workflow v1.0 | Lab Activity 3 | 2026-06-12*
*Start with Phase 0. Don't skip the gates. Ship good tests.*
