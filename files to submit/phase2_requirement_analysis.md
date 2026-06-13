# 🟡 Phase 2 — Requirement Analysis
## Status: ✅ DONE

> **Test Designer responsibility.** This document summarizes the behavior analysis using AI assistance, cross-referenced with the initial feature selection.

---

## AI Prompt (Phase 2, Step 2.2)
**Used Prompt:**
```
Feature: User Login
Description: A registered user enters username and password to access the
system dashboard. The system validates credentials and redirects on success,
shows an error on failure, and locks the account after 5 failed attempts.
Constraints:
- Login must complete within 3 seconds
- Account locks after 5 consecutive failed attempts
- Session expires after 30 minutes of inactivity
- Passwords are case-sensitive

Generate a list of testable behaviors, including:
- Happy path scenarios
- Boundary conditions
- Failure/negative scenarios
- Real-time / timing-sensitive scenarios (session timeout)
```

---

## AI Generated Behaviors (Review & Red-Team)
The AI suggested the following behaviors, which were then reviewed by the team:

1. **Successful Login:** Dashboard loads with correct user profile.
2. **Invalid Password:** Error "Invalid username or password" shown.
3. **Invalid Username:** Error "Invalid username or password" shown (security practice).
4. **Empty Fields:** Prompting the user to fill in required fields.
5. **Account Locking:** System locks account on 5th failure.
6. **Session Timeout:** Automatic logout after 30m idle.
7. **Performance Check:** Page redirect occurs within the 3s window.
8. **Case Sensitivity:** 'Password123' vs 'password123'.

---

## Final Confirmed Behavior List
After red-teaming and comparing with `phase1_feature_selected.md`, the following behaviors are confirmed for test case generation:

| # | Behavior | Type | Source |
|---|---|---|---|
| B-01 | Valid credentials → dashboard loads ≤ 3s | Happy Path | Phase 1 & AI |
| B-02 | Invalid password → error message, no login | Negative | Phase 1 & AI |
| B-03 | Empty username/password → validation error | Boundary | Phase 1 & AI |
| B-04 | 5 failed attempts → account locked | Limit/Negative | Phase 1 & AI |
| B-05 | 30 minutes inactivity → automatic logout | Real-Time | Phase 1 & AI |
| B-06 | Case sensitivity check for password | Functional | AI |

---

## Quality Gate Checklist ✅
- [x] At least 5 confirmed testable behaviors
- [x] Includes happy path, negative, boundary, and real-time
- [x] Reviewed and red-teamed against project constraints

---

## Next Phase: Phase 3 — Test Case Writing
**Owner:** Test Designer
**Action:** Use these behaviors to generate full test cases in Phase 3.
