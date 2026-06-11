# 🟢 Phase 1 — Feature Selection
## Status: ✅ DONE — Team can proceed to Phase 2

> **Test Lead responsibility.** This document is pre-filled to unblock the team.
> Next step: Test Designer opens Phase 2 and starts the behavior analysis.

---

## ✅ Selected Feature: User Login

### Why This Feature?
- Covers all required test types: happy path, negative, boundary, timing
- Realistic system feature every team member can understand
- No special hardware or environment needed
- Maps well to real-time concept: **session timeout** (soft real-time behavior)
- Low setup friction → team starts fast

---

## Feature Description (Filled)

```
Feature Name:       User Login
System/App:         Web Application (or any login-capable system)
Brief Description:  A registered user enters their credentials (username + password)
                    and gains access to the system dashboard.

User Role(s):       - Registered User (valid account)
                    - Unregistered/Guest (no account)
                    - Admin (for locked account scenarios)

Key Inputs:
  - Username / Email address
  - Password
  - "Remember Me" toggle (optional)
  - Login button

Key Outputs:
  - Successful: redirect to dashboard, session created
  - Failed: error message displayed, attempt logged
  - Locked: account lock message after N failed attempts

Known Constraints:
  - Login must complete within 3 seconds (performance requirement)
  - Account locks after 5 consecutive failed attempts
  - Session expires after 30 minutes of inactivity
  - Passwords are case-sensitive

Real-Time Concern:
  - Session timeout is a soft real-time behavior:
    after exactly 30 minutes of inactivity, the user must
    be logged out automatically. This must be tested explicitly.
```

---

## Behavior List (Hand-off to Test Designer)

The following behaviors are confirmed for Phase 2 analysis and test case writing:

| # | Behavior | Type | Priority |
|---|---|---|---|
| B-01 | Valid username + valid password → login succeeds, dashboard loads ≤ 3s | Happy Path | 🔴 High |
| B-02 | Valid username + wrong password → error message shown, no login | Negative | 🔴 High |
| B-03 | Wrong username + any password → error message shown, no login | Negative | 🔴 High |
| B-04 | Empty username field + submit → validation error, form not submitted | Boundary | 🟡 Medium |
| B-05 | Empty password field + submit → validation error, form not submitted | Boundary | 🟡 Medium |
| B-06 | 5 consecutive failed logins → account is locked, lock message shown | Negative/Limit | 🔴 High |
| B-07 | Session inactive for 30 minutes → user auto-logged out *(real-time)* | Timing/RT | 🔴 High |
| B-08 | SQL injection string in username field → system rejects safely, no crash | Security/Negative | 🟡 Medium |

> **Test Designer:** Use behaviors B-01 through B-05 for the minimum 5 test cases.
> B-06 and B-07 are stretch goals — highly recommended for full marks.
> B-08 is a bonus red-team scenario.

---

## Team Status Update

| Field | Value |
|---|---|
| **Phase 1 Status** | ✅ COMPLETE |
| **Completed by** | Test Lead |
| **Date** | 2026-06-12 |
| **Next Phase** | Phase 2 — Requirement Analysis |
| **Next Owner** | Test Designer |
| **Immediate Action** | Open `team_workflow.md` → Phase 2, use behavior list above |

---

## 📌 Test Designer — Your Next Move

1. Open [`team_workflow.md`](./team_workflow.md) → **Phase 2**
2. The behavior list above is your **confirmed input** — skip Step 2.1 manual brainstorm (already done)
3. Go directly to **Step 2.2** — use the AI prompt with this feature description
4. Red-team the AI output against the behavior list above
5. Once behavior list is finalized, move to **Phase 3 — Test Case Writing**

**AI Prompt ready to paste:**
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

*Phase 1 complete. The team is unblocked. Test Designer: go.*
