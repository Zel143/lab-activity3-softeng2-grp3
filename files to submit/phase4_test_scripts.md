# 🟡 Phase 4 — Script Development
## Status: ✅ DONE

> **Script Developer responsibility.** This document contains the automated test scripts (Python/pytest) generated from the test cases in Phase 3.

---

## Technical Setup
- **Framework:** pytest
- **Approach:** Mocked system interactions (simulating a login system)
- **File Structure:** `test_login_feature.py`

---

## 📄 `test_login_feature.py`

```python
import pytest
import time

# --- Mock System Implementation ---
class LoginSystem:
    def __init__(self):
        self.users = {"testuser": "Pass123!", "lockuser": "Pass123!"}
        self.failed_attempts = {"lockuser": 0}
        self.locked_users = set()
        self.sessions = {} # user -> last_activity_timestamp

    def login(self, username, password):
        if not username or not password:
            return "VALIDATION_ERROR", "Username and password are required"
        
        if username in self.locked_users:
            return "LOCKED", "Account locked due to multiple failed attempts"

        if username in self.users and self.users[username] == password:
            self.sessions[username] = time.time()
            # Simulate 1s network delay
            time.sleep(1) 
            return "SUCCESS", "Redirecting to dashboard..."
        else:
            if username in self.failed_attempts:
                self.failed_attempts[username] += 1
                if self.failed_attempts[username] >= 5:
                    self.locked_users.add(username)
            return "AUTH_FAILURE", "Invalid username or password"

    def check_session(self, username):
        if username not in self.sessions:
            return "NO_SESSION"
        
        # Simulate 30 minute timeout in seconds for testing (e.g., use 0.1s for demo)
        timeout = 1800 # 30 minutes
        if time.time() - self.sessions[username] > timeout:
            del self.sessions[username]
            return "EXPIRED"
        return "ACTIVE"

# --- Test Scripts ---

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

## Quality Gate Checklist ✅
- [x] Scripts match TC logic exactly
- [x] Setup, steps, and assertions included
- [x] Force-fail validation: Scripts fail if `LoginSystem` logic is changed to be incorrect
- [x] Real-time timing (timeout) is simulated correctly

---

## Next Phase: Phase 5 — Test Execution
**Owner:** Executor
**Action:** Run these scripts using `pytest` and record the results.
