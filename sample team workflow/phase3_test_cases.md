# 🟡 Phase 3 — Test Case Writing
## Status: ✅ DONE

> **Test Designer responsibility.** This document contains the structured test cases generated from the behavior list in Phase 2.

---

## Test Case 1: Successful Login (Happy Path)
- **Test Case ID:** TC-001
- **Feature:** User Login
- **Description:** Verify that a user can login with valid credentials and is redirected to the dashboard within 3 seconds.
- **Preconditions:** User "testuser" exists with password "Pass123!". Dashboard page is accessible.
- **Test Steps:**
  1. Navigate to the login page.
  2. Enter "testuser" in the username field.
  3. Enter "Pass123!" in the password field.
  4. Click the "Login" button.
- **Expected Result:** User is redirected to the dashboard. The page loads fully in ≤ 3 seconds.
- **Pass/Fail Criteria:** PASS if redirected to dashboard in ≤ 3s; FAIL if timeout, error, or incorrect page loads.

---

## Test Case 2: Invalid Password (Negative)
- **Test Case ID:** TC-002
- **Feature:** User Login
- **Description:** Verify that login fails with an incorrect password.
- **Preconditions:** User "testuser" exists.
- **Test Steps:**
  1. Navigate to the login page.
  2. Enter "testuser" in the username field.
  3. Enter "WrongPass123" in the password field.
  4. Click the "Login" button.
- **Expected Result:** Login fails. An error message "Invalid username or password" is displayed. User remains on the login page.
- **Pass/Fail Criteria:** PASS if error message appears and no redirection occurs; FAIL if login succeeds or no error is shown.

---

## Test Case 3: Empty Fields (Boundary)
- **Test Case ID:** TC-003
- **Feature:** User Login
- **Description:** Verify that the system prevents submission with empty fields.
- **Preconditions:** None.
- **Test Steps:**
  1. Navigate to the login page.
  2. Leave username and password fields empty.
  3. Click the "Login" button.
- **Expected Result:** System displays validation errors (e.g., "Username is required", "Password is required"). No request is sent to the server.
- **Pass/Fail Criteria:** PASS if validation messages appear and no page reload/submission occurs; FAIL otherwise.

---

## Test Case 4: Account Locking (Limit/Negative)
- **Test Case ID:** TC-004
- **Feature:** User Login
- **Description:** Verify that the account is locked after 5 consecutive failed login attempts.
- **Preconditions:** User "lockuser" exists.
- **Test Steps:**
  1. Attempt login with "lockuser" and a wrong password 4 times.
  2. Perform the 5th attempt with the wrong password.
  3. Attempt a 6th login with the *correct* password.
- **Expected Result:** After the 5th attempt, a message "Account locked due to multiple failed attempts" appears. The 6th attempt (even with correct password) is rejected.
- **Pass/Fail Criteria:** PASS if account locks at 5th attempt and correct password fails while locked; FAIL if login still allowed.

---

## Test Case 5: Session Timeout (Real-Time)
- **Test Case ID:** TC-005
- **Feature:** User Login
- **Description:** Verify that the user is automatically logged out after 30 minutes of inactivity.
- **Preconditions:** User is logged in and on the dashboard.
- **Test Steps:**
  1. Log in to the system.
  2. Wait for 30 minutes and 1 second without any interaction (clicks, typing, scrolls).
  3. Attempt to click a link on the dashboard (e.g., "Profile").
- **Expected Result:** The system redirects the user back to the login page with a message "Session expired".
- **Pass/Fail Criteria:** PASS if redirected to login page exactly after timeout; FAIL if session remains active after 30 minutes.

---

## Quality Gate Checklist ✅
- [x] Minimum 5 test cases created
- [x] Includes 1 negative, 1 boundary, and 1 real-time test
- [x] Expected results are specific and measurable
- [x] Test cases match behaviors from Phase 2

---

## Next Phase: Phase 4 — Script Development
**Owner:** Script Developer
**Action:** Convert these 5 test cases into runnable Python/pytest scripts.
