# 🟡 Phase 5 — Test Execution
## Status: ✅ DONE

> **Executor responsibility.** This document records the results of the automated test execution.

---

## Execution Environment
- **Date:** 2026-06-13
- **System:** Mock Login System (Python-based)
- **Framework:** pytest 9.0.3

---

## 📊 Summary of Results

| Test Case ID | Feature | Description | Status | Notes |
|---|---|---|---|---|
| TC-001 | User Login | Valid credentials -> dashboard loads ≤ 3s | **PASS** | Executed in 1.01s (includes mock delay) |
| TC-002 | User Login | Invalid password -> error message, no login | **PASS** | "Invalid username or password" shown |
| TC-003 | User Login | Empty fields -> validation error | **PASS** | "Username and password are required" shown |
| TC-004 | User Login | 5 failed attempts -> account locked | **PASS** | Locked at 5th attempt; 6th attempt rejected |
| TC-005 | User Login | 30 minutes inactivity -> auto logout | **PASS** | Session successfully marked as EXPIRED |

---

## 🧪 Raw Execution Logs (CLI Snippet)
```text
================================== test session starts ==================================
platform win32 -- Python 3.12.5, pytest-9.0.3, pluggy-1.6.0
rootdir: G:\Lab Acitivity 3
collected 5 items                                                                                                                                

test_login_feature.py .....                                                        [100%]

=================================== 5 passed in 2.10s ===================================
```

---

## Quality Gate Checklist ✅
- [x] All 5 test cases executed
- [x] Results recorded with status (PASS/FAIL)
- [x] Evidence captured (CLI logs)
- [x] No regressions or unexpected failures

---

## Next Phase: Phase 6 — Review & Report
**Owner:** Reviewer + Test Lead
**Action:** Generate a final summary report and close the session.
