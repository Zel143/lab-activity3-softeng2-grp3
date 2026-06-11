# Project Context — Lab Activity 3
## Software Engineering | Real-Time Systems & Testing

---

## Project Identity

| Field | Value |
|---|---|
| **Lab Title** | Lab Activity 3: Creating Test Cases and Test Scripts |
| **Subject** | Software Engineering |
| **Topic** | Real-Time Software Engineering (Chapter 21) |
| **Deliverables** | Test cases, test scripts, executed results |
| **Primary Reference** | Ch 21 - Real-time software engineering (Sommerville) |
| **Tools** | Enhanced Test Template (xlsx), AI assistant, test automation framework |
| **Date** | 2026-06-12 |

---

## Learning Objectives

1. **Identify system requirements** — Extract testable behaviors from specifications.
2. **Create test cases** — Structure requirements into formal test cases with clear pass/fail criteria.
3. **Develop test scripts** — Convert test cases into executable, automated (or manual) scripts.
4. **Execute and evaluate** — Run scripts, record results, and interpret outcomes.

---

## Procedure Summary

| Step | Activity | Output |
|---|---|---|
| 1 | Select a project feature (e.g., login, registration) | Feature selected |
| 2 | Write at least 5 test cases | Completed test case table |
| 3 | Convert test cases to test scripts | Executable test scripts |
| 4 | Execute test scripts and record results | Filled Enhanced Test Template |

---

## Real-Time Software Engineering Context (Ch. 21)

### What is Real-Time Software?
Software that must respond to events within defined time constraints.
- **Hard real-time:** Missing deadline = system failure (e.g., airbag controller)
- **Soft real-time:** Missing deadline = degraded performance (e.g., video streaming)

### Key Concepts Relevant to Testing
| Concept | Testing Implication |
|---|---|
| **Process scheduling** | Test that high-priority processes preempt lower-priority ones correctly |
| **Interrupt handling** | Test interrupt response time under varying load |
| **Timing constraints** | Validate deadline adherence with profiling tools |
| **State machines** | Test all state transitions including invalid/unexpected transitions |
| **Concurrency** | Test for race conditions, deadlocks, and shared resource access |
| **Watchdog timers** | Test system recovery when watchdog fires |
| **Sensor-actuator loops** | Test control loop response under boundary sensor values |

---

## File Map

```
g:\Lab Acitivity 3\
├── context\
│   ├── karpathy_rules.md          ← AI coding principles & discipline
│   ├── ai_workflow_logs.md        ← Session audit trail
│   ├── ai_workflow.md             ← Phase-by-phase AI-assisted workflow
│   └── project_context.md         ← THIS FILE — project overview
├── Enhanced_Test_Template(1).xlsx  ← Test case + result recording sheet
├── Lab_Testing_Exercise.docx       ← Lab instructions
├── Ch 21 - Real-time software engineering - Tagged.pdf  ← Course reference
└── sample team workflow\           ← (Available for team reference)
```

---

## Test Feature Options (choose one for the lab)

| # | Feature | Complexity | Real-Time Aspect |
|---|---|---|---|
| 1 | User Login | Low | None |
| 2 | User Registration | Low | None |
| 3 | Sensor Data Polling | High | Timing-critical |
| 4 | Event-Driven Notification | Medium | Interrupt-based |
| 5 | Session Timeout | Medium | Timing-based |
| 6 | Concurrent Data Access | High | Concurrency/race |

---

## AI Assistance Boundaries

| Allowed | Not Allowed (human-only) |
|---|---|
| Generating test case drafts | Final sign-off on safety-critical tests |
| Suggesting test coverage gaps | Validating real-time timing constraints |
| Converting test cases to scripts | Approving security-sensitive test results |
| Summarizing test results | Root-cause analysis of real-time failures |

---

## Quality Standards

- **Minimum:** 5 test cases per feature
- **Required coverage:** happy path + negative + boundary
- **Scripts:** must be runnable and self-contained
- **Results:** recorded in Enhanced Test Template with pass/fail status
- **Review:** all AI-generated content reviewed by human before submission

---

## Relevant Principles (from Karpathy Rules)

> *"Test the tests."* — Force failures intentionally to validate your test logic.
> *"Version everything."* — Every test case and script is under version control.
> *"AI is a pair programmer, not an oracle."* — Review all AI output critically.

---

## Team / Author

| Field | Value |
|---|---|
| **Author** | [Your Name] |
| **Section** | [Your Section] |
| **Instructor** | [Instructor Name] |
| **Institution** | [Your Institution] |
| **Submission Date** | [Due Date] |

---

*Project Context v1.0 | Generated: 2026-06-12 | Lab Activity 3*
