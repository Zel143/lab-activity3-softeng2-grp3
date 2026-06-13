# 🔵 Phase 2 — Requirement Analysis
## Feature: User Login

> **Owner:** Test Designer
> **Status:** ✅ COMPLETE
> This phase identifies all testable behaviors for the "User Login" feature, including real-time and edge cases.

---

## 📖 Feature Context

**Description:** A registered user enters username and password to access the system dashboard. The system validates credentials and redirects on success, shows an error on failure, and locks the account after 5 failed attempts.
**Constraints:**
- Login must complete within 3 seconds
- Account locks after 5 consecutive failed attempts
- Session expires after 30 minutes of inactivity
- Passwords are case-sensitive

---

## 🧪 List of Testable Behaviors

Following Phase 2 Step 2.2 (AI-Assisted Analysis), the following behaviors have been identified and reviewed:

### 1. Happy Path Scenarios
| ID | Behavior | Expected Outcome | Priority |
|---|---|---|---|
| B-01 | Valid username + valid password | Login succeeds; redirect to dashboard ≤ 3 seconds. | 🔴 High |
| B-02 | "Remember Me" checked during valid login | User remains logged in after browser restart (session persistence). | 🟡 Medium |

### 2. Boundary Condition Scenarios
| ID | Behavior | Expected Outcome | Priority |
|---|---|---|---|
| B-03 | Username at maximum character limit | System accepts input and processes login normally. | 🟡 Medium |
| B-04 | Password at minimum required length | System accepts input and processes login normally. | 🟡 Medium |
| B-05 | Login attempt exactly at 5th failure | Account locks immediately; lock message displayed. | 🔴 High |

### 3. Failure / Negative Scenarios
| ID | Behavior | Expected Outcome | Priority |
|---|---|---|---|
| B-06 | Invalid username + valid password | "Invalid credentials" error; no access granted. | 🔴 High |
| B-07 | Valid username + incorrect password | "Invalid credentials" error; attempt count increments. | 🔴 High |
| B-08 | Empty username field + submit | "Username is required" validation error; no request sent. | 🔴 High |
| B-09 | Empty password field + submit | "Password is required" validation error; no request sent. | 🔴 High |
| B-10 | SQL Injection attempt in fields | System sanitizes input; login fails; no database error. | 🟡 Medium |

### 4. Real-Time / Timing-Sensitive Scenarios
| ID | Behavior | Expected Outcome | Priority |
|---|---|---|---|
| B-11 | **Session Inactivity (Soft RT)** | After exactly 30 mins of no activity, user is logged out. | 🔴 High |
| B-12 | **Login Performance** | System must respond (success/fail) within 3.0s deadline. | 🔴 High |
| B-13 | Simultaneous logins (same account) | System handles concurrency based on policy (allow/deny). | 🟡 Medium |

---

## ✅ Quality Gate Check
- [x] At least 5 behaviors identified (13 total)
- [x] Includes Happy Path (B-01, B-02)
- [x] Includes Negative Scenarios (B-06, B-07, B-10)
- [x] Includes Boundary Conditions (B-03, B-04, B-05, B-08, B-09)
- [x] Includes Real-Time timing behaviors (B-11, B-12)

---

## 🚀 Next Step
Move to **Phase 3 — Test Case Writing** using this behavior list as the primary input.

*Phase 2 complete | 2026-06-13 | Test Designer*
