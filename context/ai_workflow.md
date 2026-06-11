# AI Workflow — Lab Activity 3
## Software Testing Exercise with AI Assistance

> Applies Vibe-Coding + Red-Teaming standards.
> Structured for real-time software engineering context (Ch. 21).

---

## Overview

This workflow governs how AI tools are used throughout Lab Activity 3:
- Test case identification
- Test script development
- Test execution and result evaluation
- Documentation and reporting

---

## Phase 1 — Requirement Analysis

**Goal:** Understand the system feature to test.

### Steps:
1. Read the feature specification carefully (manual step — no AI yet).
2. Identify: inputs, outputs, constraints, edge cases.
3. Ask AI: *"Given this feature description, what are the critical behaviors to test?"*
4. **Red-Team:** Challenge AI's list — what did it miss? What's a timing-sensitive edge case?

### AI Prompt Template (Phase 1):
```
Feature: [NAME]
Description: [DESCRIPTION]
Constraints: [ANY TIMING, SAFETY, OR PERFORMANCE CONSTRAINTS]

Generate a list of testable behaviors, including:
- Happy path scenarios
- Boundary conditions
- Failure/negative scenarios
- Real-time / timing-sensitive scenarios (if applicable)
```

---

## Phase 2 — Test Case Generation

**Goal:** Convert behaviors into structured test cases.

### Steps:
1. Use the Enhanced Test Template as the output format.
2. Prompt AI with one behavior at a time (Karpathy Rule #4 — small context).
3. Review each test case for:
   - Correct preconditions
   - Realistic inputs
   - Verifiable expected outcomes
   - Clear pass/fail criteria

### AI Prompt Template (Phase 2):
```
Behavior to test: [BEHAVIOR]
System: [SYSTEM NAME / FEATURE]

Generate a test case in this format:
- Test Case ID: TC-XXX
- Feature: 
- Description:
- Preconditions:
- Test Steps: (numbered)
- Expected Result:
- Pass/Fail Criteria:
```

### Quality Gate ✅
- [ ] At least 5 test cases per feature
- [ ] At least 1 negative/failure test case
- [ ] At least 1 boundary condition test
- [ ] All expected results are specific and measurable

---

## Phase 3 — Test Script Development

**Goal:** Convert test cases into executable test scripts.

### Steps:
1. Select the automation target (manual, Selenium, Postman, etc.).
2. Prompt AI: *"Convert this test case into a [TOOL] script."*
3. Review generated script:
   - Does it match the test case logic exactly?
   - Are setup/teardown steps included?
   - Are assertions specific?

### AI Prompt Template (Phase 3):
```
Test Case ID: TC-XXX
Tool/Framework: [TOOL NAME]
Language: [PYTHON / JAVASCRIPT / etc.]

Convert this test case into a runnable test script.
Include: setup, steps, assertions, teardown.
Test Case:
[PASTE TEST CASE HERE]
```

### Quality Gate ✅
- [ ] Script runs without syntax errors
- [ ] Script fails when expected behavior is violated (force-fail test)
- [ ] Script passes on correct implementation
- [ ] Script is version-controlled

---

## Phase 4 — Test Execution & Evaluation

**Goal:** Execute scripts, record results, analyze failures.

### Steps:
1. Run scripts in the designated test environment.
2. Record results in the Enhanced Test Template (xlsx).
3. For failures: root-cause analysis before asking AI.
4. Ask AI: *"This test failed with [ERROR]. Given [CONTEXT], what are likely causes?"*
5. **Red-Team:** Verify AI's diagnosis against actual system behavior.

### Result Status Codes:
| Code | Meaning |
|---|---|
| PASS | Behavior confirmed correct |
| FAIL | Behavior does not match expected |
| BLOCK | Cannot execute — dependency/environment issue |
| SKIP | Out of scope for this session |
| DEFER | Timing/resource constraint — retry later |

---

## Phase 5 — Review & Documentation

**Goal:** Finalize, document, and version all outputs.

### Steps:
1. Summarize test results in a brief report.
2. Update `ai_workflow_logs.md` with session details.
3. Commit all test cases, scripts, and results to version control.
4. Ask AI to generate a test summary table.
5. Human review: validate AI-generated summary against raw results.

### AI Prompt Template (Phase 5):
```
Here are my test results: [TABLE OR LIST]
Generate a brief test summary including:
- Total cases: X
- Passed: X
- Failed: X
- Blocked: X
- Key findings: [LIST]
- Recommended next steps: [LIST]
```

---

## Real-Time Systems Special Rules (Ch. 21)

> These rules apply when testing real-time or embedded software features.

1. **Timing is a first-class requirement.** Test deadline adherence explicitly.
2. **Interrupt-driven behavior** must be tested under load, not just in isolation.
3. **Watchdog and recovery paths** are critical — test failure recovery, not just normal operation.
4. **Concurrency bugs** don't always reproduce — use stress testing and logging.
5. **AI cannot verify timing constraints** — only run-time measurement tools can. Use profilers and oscilloscopes (or simulators) for final validation.

---

*Workflow version: 1.0 | Lab Activity 3 | 2026-06-12*
