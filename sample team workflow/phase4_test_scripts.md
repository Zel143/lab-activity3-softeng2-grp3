# 🟠 Phase 4 — Test Scripts
## Feature: User Login

> **Owner:** Script Developer
> **Status:** ✅ COMPLETE
> This file contains the executable test scripts based on the test cases in Phase 3.

---

### Test Script ID: TS-01 (Valid Login)
**Feature:** User Login  
**Environment:** Web Browser (Staging/Production)

**Steps:**  
1. Navigate to `https://app.example.com/login`
2. Locate the "Email" field and enter `user@test.com`
3. Locate the "Password" field and enter `123456`
4. Click the "Login" button
5. Observe the URL and page content

**Expected Output:**  
The URL changes to `https://app.example.com/dashboard` and the text "Welcome, User" is visible within 3.0 seconds.

---

### Test Script ID: TS-02 (Invalid Password)
**Feature:** User Login  
**Environment:** Web Browser (Staging/Production)

**Steps:**  
1. Navigate to `https://app.example.com/login`
2. Enter `user@test.com` in the Email field
3. Enter `wrongpassword` in the Password field
4. Click the "Login" button
5. Check for error messages

**Expected Output:**  
The message "Invalid credentials" appears in red text. The user remains on the login page.

---

### Test Script ID: TS-03 (Empty Username)
**Feature:** User Login  
**Environment:** Web Browser (Staging/Production)

**Steps:**  
1. Navigate to `https://app.example.com/login`
2. Leave the Email field empty
3. Enter `123456` in the Password field
4. Click the "Login" button

**Expected Output:**  
A validation tooltip or message stating "Username is required" appears. No network request is sent to the server.

---

### Test Script ID: TS-04 (Account Lockout)
**Feature:** User Login  
**Environment:** Web Browser (Staging/Production)

**Steps:**  
1. Navigate to login page.
2. Enter `user@test.com` and an incorrect password. Click Login. (Repeat 5 times)
3. On the 5th attempt, observe the message.

**Expected Output:**  
The system displays: "Your account has been locked for 30 minutes due to security reasons."

---

### Test Script ID: TS-05 (Session Timeout - Real-Time)
**Feature:** User Login  
**Environment:** Web Browser (Staging/Production)

**Steps:**  
1. Log in successfully with valid credentials.
2. Confirm arrival at the Dashboard.
3. Stop all keyboard and mouse activity for exactly 30 minutes.
4. Attempt to click a link on the dashboard after the timer expires.

**Expected Output:**  
The page automatically redirects to the Login screen. A message "Session expired. Please log in again." is shown.

---

## ✅ Quality Gate Check
- [x] Scripts match Test Case logic
- [x] Preconditions are implied/included
- [x] Assertions/Expected outputs are specific
- [x] Follows teammate's required template format

---

*Phase 4 complete | 2026-06-13 | Script Developer*
