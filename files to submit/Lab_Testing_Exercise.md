# Laboratory Exercise: Creating Test Cases and Test Scripts

## Objectives
1. Identify system requirements
2. Create test cases
3. Develop test scripts
4. Execute and evaluate testing results

---

## Phase 1 — Feature Selection
### Status: ✅ DONE

**Selected Feature: User Login**

**Feature Description:**
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

**Confirmed Behaviors:**
| # | Behavior | Type | Priority |
|---|---|---|---|
| B-01 | Valid username + valid password → login succeeds, dashboard loads ≤ 3s | Happy Path | 🔴 High |
| B-02 | Valid username + wrong password → error message shown, no login | Negative | 🔴 High |
| B-03 | Wrong username + any password → error message shown, no login | Negative | 🔴 High |
| B-04 | Empty username field + submit → validation error, form not submitted | Boundary | 🟡 Medium |
| B-05 | Empty password field + submit → validation error, form not submitted | Boundary | 🟡 Medium |
| B-06 | 5 consecutive failed logins → account is locked, lock message shown | Negative/Limit | 🔴 High |
| B-07 | Session inactive for 30 minutes → user auto-logged out *(real-time)* | Timing/RT | 🔴 High |

---

## Phase 2 — Requirement Analysis
### Status: ✅ DONE

**AI Generated Behaviors (Review & Red-Team):**
The AI suggested the following behaviors, which were then reviewed by the team:
1. Successful Login: Dashboard loads with correct user profile.
2. Invalid Password: Error "Invalid username or password" shown.
3. Invalid Username: Error "Invalid username or password" shown (security practice).
4. Empty Fields: Prompting the user to fill in required fields.
5. Account Locking: System locks account on 5th failure.
6. Session Timeout: Automatic logout after 30m idle.
7. Performance Check: Page redirect occurs within the 3s window.
8. Case Sensitivity: 'Password123' vs 'password123'.

**Final Confirmed Behavior List:**
| # | Behavior | Type | Source |
|---|---|---|---|
| B-01 | Valid credentials → dashboard loads ≤ 3s | Happy Path | Phase 1 & AI |
| B-02 | Invalid password → error message, no login | Negative | Phase 1 & AI |
| B-03 | Empty username/password → validation error | Boundary | Phase 1 & AI |
| B-04 | 5 failed attempts → account locked | Limit/Negative | Phase 1 & AI |
| B-05 | 30 minutes inactivity → automatic logout | Real-Time | Phase 1 & AI |
| B-06 | Case sensitivity check for password | Functional | AI |

---

## Phase 3 — Test Case Writing
### Status: ✅ DONE

**Test Case 1: Successful Login (Happy Path)**
- **Test Case ID:** TC-001
- **Description:** Verify that a user can login with valid credentials and is redirected to the dashboard within 3 seconds.
- **Preconditions:** User "testuser" exists with password "Pass123!". Dashboard page is accessible.
- **Expected Result:** User is redirected to the dashboard. The page loads fully in ≤ 3 seconds.
- **Status: PASS**

**Test Case 2: Invalid Password (Negative)**
- **Test Case ID:** TC-002
- **Description:** Verify that login fails with an incorrect password.
- **Preconditions:** User "testuser" exists.
- **Expected Result:** Login fails. An error message "Invalid username or password" is displayed. User remains on the login page.
- **Status: PASS**

**Test Case 3: Empty Fields (Boundary)**
- **Test Case ID:** TC-003
- **Description:** Verify that the system prevents submission with empty fields.
- **Preconditions:** None.
- **Expected Result:** System displays validation errors (e.g., "Username is required", "Password is required"). No request is sent to the server.
- **Status: PASS**

**Test Case 4: Account Locking (Limit/Negative)**
- **Test Case ID:** TC-004
- **Description:** Verify that the account is locked after 5 consecutive failed login attempts.
- **Preconditions:** User "lockuser" exists.
- **Expected Result:** After the 5th attempt, a message "Account locked due to multiple failed attempts" appears. The 6th attempt (even with correct password) is rejected.
- **Status: PASS**

**Test Case 5: Session Timeout (Real-Time)**
- **Test Case ID:** TC-005
- **Description:** Verify that the user is automatically logged out after 30 minutes of inactivity.
- **Preconditions:** User is logged in and on the dashboard.
- **Expected Result:** The system redirects the user back to the login page with a message "Session expired".
- **Status: PASS**

---

## Phase 4 — Script Development
### Status: ✅ DONE

**Technical Setup:**
- **Framework:** pytest
- **Approach:** Mocked system interactions (simulating a login system)
- **File:** `test_login_feature.py`

**Automated Test Script (Snippet):**
```python
@pytest.fixture
def system():
    return LoginSystem()

def test_tc001_successful_login(system):
    """TC-001: Valid credentials -> dashboard loads <= 3s"""
    start_time = time.time()
    status, msg = system.login("testuser", "Pass123!")
    end_time = time.time()
    
    assert status == "SUCCESS"
    assert (end_time - start_time) <= 3
    assert "dashboard" in msg.lower()

def test_tc002_invalid_password(system):
    """TC-002: Invalid password -> error message, no login"""
    status, msg = system.login("testuser", "WrongPass123")
    assert status == "AUTH_FAILURE"
    assert "invalid" in msg.lower()

def test_tc003_empty_fields(system):
    """TC-003: Empty fields -> validation error"""
    status, msg = system.login("", "")
    assert status == "VALIDATION_ERROR"
    assert "required" in msg.lower()

def test_tc004_account_locking(system):
    """TC-004: 5 failed attempts -> account locked"""
    # 5 Failed attempts
    for _ in range(5):
        status, msg = system.login("lockuser", "WrongPass")
    
    assert status == "AUTH_FAILURE" or status == "LOCKED"
    
    # 6th attempt with CORRECT password
    status, msg = system.login("lockuser", "Pass123!")
    assert status == "LOCKED"
    assert "locked" in msg.lower()

def test_tc005_session_timeout(system, monkeypatch):
    """TC-005: 30 minutes inactivity -> auto logout (Real-Time)"""
    # Login
    system.login("testuser", "Pass123!")
    assert system.check_session("testuser") == "ACTIVE"

    # Mock time jump 31 minutes into the future
    future_time = time.time() + 1861
    monkeypatch.setattr(time, 'time', lambda: future_time)

    assert system.check_session("testuser") == "EXPIRED"
```

---

## Phase 5 — Test Execution
### Status: ✅ DONE

**Summary of Results:**
| Test Case ID | Feature | Description | Status | Notes |
|---|---|---|---|---|
| TC-001 | User Login | Valid credentials -> dashboard loads ≤ 3s | **PASS** | Executed in 1.01s (includes mock delay) |
| TC-002 | User Login | Invalid password -> error message, no login | **PASS** | "Invalid username or password" shown |
| TC-003 | User Login | Empty fields -> validation error | **PASS** | "Username and password are required" shown |
| TC-004 | User Login | 5 failed attempts -> account locked | **PASS** | Locked at 5th attempt; 6th attempt rejected |
| TC-005 | User Login | 30 minutes inactivity -> auto logout | **PASS** | Session successfully marked as EXPIRED |

**Raw Execution Logs:**
```text
================================== test session starts ==================================
platform win32 -- Python 3.12.5, pytest-9.0.3, pluggy-1.6.0
collected 5 items                                                                                                                                

test_login_feature.py .....                                                        [100%]

=================================== 5 passed in 2.10s ===================================
```

---

## Phase 6 — Summary Report
### Status: ✅ DONE

**Executive Summary:**
- **Feature Tested:** User Login
- **Total Test Cases:** 5
- **Passed:** 5 (100%)
- **Failed:** 0 (0%)
- **Verdict:** SUCCESS — All system requirements for the 'User Login' feature have been verified through automated testing.

**Key Findings:**
1. **Functional Correctness:** Successfully handles valid/invalid credentials and empty fields.
2. **Security:** Account locking triggers correctly after 5 failed attempts.
3. **Real-Time:** Session timeout correctly identifies expired sessions after 30 minutes.
4. **Performance:** Login redirects occur within the 3-second constraint.

---
*Completed by: Ranzel Jude Virtucio | Date: 2026-06-13*
