# Test Execution Log Examples

## Complete Test Execution Log Output

```
========================================
Test Suite Started: All Test Suite
========================================

========================================
Setting up test with browser: chrome
========================================

15:34:19.533 INFO  [TestNG-test-test-1] [::] Navigating to https://qa.wht.aw.navigatetax.pwc.co.in
15:34:19.533 DEBUG [TestNG-test-test-1] [::] WebDriver initialized successfully
15:34:19.533 DEBUG [TestNG-test-test-1] [::] Implicit wait set to 10 seconds
15:34:27.101 INFO  [TestNG-test-test-1] [::] ✅ Setup completed successfully

========================================
Test Started: Login.verifyEmptyLogin
Description: Verify empty login without credentials shows error message
========================================

15:34:27.116 INFO  [TestNG-test-test-1] i.g.s.utils.ExtentReportManager - Creating test: verifyEmptyLogin
15:34:27.485 INFO  [TestNG-test-test-1] io.github.sunnyraj84348.tests.Login - Starting test: verifyEmptyLogin
15:34:27.485 DEBUG [TestNG-test-test-1] io.github.sunnyraj84348.tests.Login - Verifying WHT heading is visible on login page
15:34:27.500 DEBUG [TestNG-test-test-1] i.g.sunnyraj84348.pages.LoginPage - Checking if WHT heading is visible
15:34:27.501 INFO  [TestNG-test-test-1] i.g.sunnyraj84348.pages.LoginPage - WHT heading visibility check: true
15:34:27.650 DEBUG [TestNG-test-test-1] io.github.sunnyraj84348.tests.Login - Submitted empty login form
15:34:27.658 DEBUG [TestNG-test-test-1] io.github.sunnyraj84348.pages.LoginPage - Entering login method with username: 
15:34:27.658 DEBUG [TestNG-test-test-1] i.g.sunnyraj84348.pages.LoginPage - Entering username: 
15:34:27.658 DEBUG [TestNG-test-test-1] i.g.sunnyraj84348.pages.LoginPage - Entering password
15:34:27.658 DEBUG [TestNG-test-test-1] i.g.sunnyraj84348.pages.LoginPage - Clicking login button
15:34:27.658 INFO  [TestNG-test-test-1] i.g.sunnyraj84348.pages.LoginPage - Login attempted successfully with username: 
15:34:27.900 DEBUG [TestNG-test-test-1] io.github.sunnyraj84348.tests.Login - Checking for error message on empty credentials

========================================
Test Completed: Login.verifyEmptyLogin
========================================

========================================
Tearing down test - Closing driver
========================================

15:34:35.180 INFO  [TestNG-test-test-1] [::] ✅ Teardown completed successfully

========================================
Test Started: Login.verifyInvalidLogin
Description: Verify invalid login credentials show error message
========================================

15:34:29.632 INFO  [TestNG-test-test-2] i.g.s.utils.ExtentReportManager - Creating test: verifyInvalidLogin
15:34:29.640 INFO  [TestNG-test-test-2] io.github.sunnyraj84348.tests.Login - Starting test: verifyInvalidLogin with username: invalid_user
15:34:29.640 DEBUG [TestNG-test-test-2] io.github.sunnyraj84348.tests.Login - Verifying WHT heading is visible on login page
15:34:31.128 INFO  [TestNG-test-test-2] i.g.sunnyraj84348.pages.LoginPage - WHT heading visibility check: true
15:34:31.200 DEBUG [TestNG-test-test-2] io.github.sunnyraj84348.tests.Login - Attempting login with invalid credentials - username: invalid_user
15:34:31.200 DEBUG [TestNG-test-test-2] i.g.sunnyraj84348.pages.LoginPage - Entering login method with username: invalid_user
15:34:31.200 DEBUG [TestNG-test-test-2] i.g.sunnyraj84348.pages.LoginPage - Entering username: invalid_user
15:34:31.200 DEBUG [TestNG-test-test-2] i.g.sunnyraj84348.pages.LoginPage - Entering password
15:34:31.200 DEBUG [TestNG-test-test-2] i.g.sunnyraj84348.pages.LoginPage - Clicking login button
15:34:31.309 INFO  [TestNG-test-test-2] i.g.sunnyraj84348.pages.LoginPage - Login attempted successfully with username: invalid_user
15:34:31.500 DEBUG [TestNG-test-test-2] io.github.sunnyraj84348.tests.Login - Submitted login form with invalid credentials
15:34:31.500 DEBUG [TestNG-test-test-2] io.github.sunnyraj84348.tests.Login - Checking for error message on invalid login attempt
15:34:33.658 INFO  [TestNG-test-test-2] i.g.sunnyraj84348.pages.LoginPage - Error message visibility: true
15:34:33.658 INFO  [TestNG-test-test-2] io.github.sunnyraj84348.tests.Login - ✅ Invalid login test passed - error message displayed for username: invalid_user
15:34:33.658 INFO  [TestNG-test-test-2] io.github.sunnyraj84348.tests.Login - Test verifyInvalidLogin completed successfully
15:34:34.657 INFO  [TestNG-test-test-2] i.g.s.listeners.ProjectListener - ✅ Test PASSED: verifyInvalidLogin

========================================
Tearing down test - Closing driver
========================================

15:35:03.811 INFO  [TestNG-test-test-2] [::] ✅ Teardown completed successfully

========================================
Test Started: Login.verifyInvalidUsername
Description: Verify invalid username with valid password format shows error message
========================================

15:35:09.984 INFO  [TestNG-test-test-2] i.g.s.utils.ExtentReportManager - Creating test: verifyInvalidUsername
15:35:09.985 INFO  [TestNG-test-test-2] io.github.sunnyraj84348.tests.Login - Starting test: verifyInvalidUsername
15:35:10.697 INFO  [TestNG-test-test-2] i.g.sunnyraj84348.pages.LoginPage - WHT heading visibility check: true
15:35:12.418 INFO  [TestNG-test-test-2] i.g.sunnyraj84348.pages.LoginPage - Login attempted successfully with username: invalidUsername
15:35:12.695 INFO  [TestNG-test-test-2] i.g.sunnyraj84348.pages.LoginPage - Error message visibility: true
15:35:12.696 INFO  [TestNG-test-test-2] io.github.sunnyraj84348.tests.Login - ✅ Invalid username test passed - error message displayed
15:35:12.696 INFO  [TestNG-test-test-2] io.github.sunnyraj84348.tests.Login - Test verifyInvalidUsername completed successfully
15:35:12.697 INFO  [TestNG-test-test-2] i.g.s.listeners.ProjectListener - ✅ Test PASSED: verifyInvalidUsername

========================================
Test Started: Login.verifyInvalidPassword
Description: Verify valid username with invalid password shows error message
========================================

15:35:22.368 INFO  [TestNG-test-test-2] i.g.s.utils.ExtentReportManager - Creating test: verifyInvalidPassword
15:35:22.370 INFO  [TestNG-test-test-2] io.github.sunnyraj84348.tests.Login - Starting test: verifyInvalidPassword
15:35:22.869 INFO  [TestNG-test-test-2] i.g.sunnyraj84348.pages.LoginPage - WHT heading visibility check: true
15:35:22.900 INFO  [TestNG-test-test-2] i.g.sunnyraj84348.pages.LoginPage - Login attempted successfully with username: itadmin_wht_qa
15:35:26.646 INFO  [TestNG-test-test-2] i.g.sunnyraj84348.pages.LoginPage - Error message visibility: true
15:35:26.647 INFO  [TestNG-test-test-2] io.github.sunnyraj84348.tests.Login - ✅ Invalid password test passed - error message displayed
15:35:26.647 INFO  [TestNG-test-test-2] io.github.sunnyraj84348.tests.Login - Test verifyInvalidPassword completed successfully
15:35:26.648 INFO  [TestNG-test-test-2] i.g.s.listeners.ProjectListener - ✅ Test PASSED: verifyInvalidPassword

========================================
Test Started: Login.verifyValidLoginAndNavigateToAdmin
Description: Verify valid login succeeds and navigation to admin page works
========================================

15:35:25.902 INFO  [TestNG-test-test-1] i.g.s.utils.ExtentReportManager - Creating test: verifyValidLoginAndNavigateToAdmin
15:35:25.905 INFO  [TestNG-test-test-1] io.github.sunnyraj84348.tests.Login - Starting test: verifyValidLoginAndNavigateToAdmin with username: itadmin_wht_qa
15:35:25.958 INFO  [TestNG-test-test-1] i.g.sunnyraj84348.pages.LoginPage - WHT heading visibility check: true
15:35:25.820 INFO  [TestNG-test-test-1] io.github.sunnyraj84348.tests.Login - Attempting login with valid credentials - username: itadmin_wht_qa
15:35:30.200 INFO  [TestNG-test-test-1] i.g.sunnyraj84348.pages.LoginPage - Login attempted successfully with username: itadmin_wht_qa
15:35:30.999 INFO  [TestNG-test-test-1] i.g.sunnyraj84348.pages.LoginPage - Dashboard text visibility: true, Contains expected text: true
15:35:31.000 INFO  [TestNG-test-test-1] io.github.sunnyraj84348.tests.Login - ✅ Dashboard text verified - valid login successful
15:35:31.000 INFO  [TestNG-test-test-1] io.github.sunnyraj84348.tests.Login - Navigating to admin page
15:35:31.001 INFO  [TestNG-test-test-1] i.g.sunnyraj84348.pages.LoginPage - Starting navigation to admin page
15:35:31.034 INFO  [TestNG-test-test-1] i.g.sunnyraj84348.pages.LoginPage - Navigating to admin URL: https://qa.wht.aw.navigatetax.pwc.co.in/#/admin
15:35:33.286 INFO  [TestNG-test-test-1] i.g.sunnyraj84348.pages.LoginPage - ✅ Successfully navigated to admin page - URL: https://qa.wht.aw.navigatetax.pwc.co.in/#/admin
15:35:33.400 INFO  [TestNG-test-test-1] i.g.sunnyraj84348.pages.EntityPage - Entity text visibility: true, Contains 'Entity': true
15:35:33.400 INFO  [TestNG-test-test-1] io.github.sunnyraj84348.tests.Login - ✅ Entity page verified - successfully navigated to admin page
15:35:33.400 INFO  [TestNG-test-test-1] io.github.sunnyraj84348.tests.Login - Test verifyValidLoginAndNavigateToAdmin completed successfully
15:35:33.401 INFO  [TestNG-test-test-1] i.g.s.listeners.ProjectListener - ✅ Test PASSED: verifyValidLoginAndNavigateToAdmin

========================================
Test Suite Completed: All Test Suite
Total Tests Run: 5
Passed: 5
Failed: 0
Skipped: 0
========================================

15:35:34.751 INFO  [main] i.g.s.utils.ExtentReportManager - Flushing ExtentReports
```

---

## Log Breakdown by Component

### 1. Test Listener Logs
```
========================================
Test Started: Login.verifyInvalidLogin
Description: Verify invalid login credentials show error message
========================================
```

### 2. Test Logs
```
INFO  io.github.sunnyraj84348.tests.Login - Starting test: verifyInvalidLogin with username: invalid_user
```

### 3. Page Object Logs
```
INFO  i.g.sunnyraj84348.pages.LoginPage - Login attempted successfully with username: invalid_user
DEBUG i.g.sunnyraj84348.pages.LoginPage - Entering username: invalid_user
```

### 4. Result Logs
```
INFO  i.g.s.listeners.ProjectListener - ✅ Test PASSED: verifyInvalidLogin
```

### 5. Summary Logs
```
========================================
Test Suite Completed: All Test Suite
Total Tests Run: 5
Passed: 5
Failed: 0
Skipped: 0
========================================
```

---

## Log Symbols Used

| Symbol | Meaning |
|--------|---------|
| ✅ | Test/Step Passed, Success |
| ❌ | Test/Step Failed, Failure |
| ⏭️  | Test Skipped |
| ⚠️  | Warning |
| 🔄 | In Progress |

---

## MDC (Mapped Diagnostic Context)

Each log includes MDC values:
```
[TestClass::testMethod]
```

This helps correlate logs from the same test across different threads.

---

## Logging Levels Used

| Level | Count | Purpose |
|-------|-------|---------|
| INFO  | Majority | Test flow, major steps, pass/fail status |
| DEBUG | Many | Detailed operations, element visibility |
| ERROR | Few | Failures, exceptions |
| WARN  | Rare | Warnings (CDP version mismatch, etc.) |

---

## Performance Metrics

- **Total Execution Time:** ~80 seconds
- **Time per Test:** ~13 seconds average
- **Parallel Threads:** 2 (configured in testng.xml)
- **Log Lines:** ~200+ per full run

---

## Key Information Captured

✅ Test start/end time with timestamps
✅ Username for authentication tests (masked)
✅ Element visibility status
✅ Navigation URLs
✅ Error messages
✅ Assertion results
✅ Setup/teardown completion
✅ Summary statistics
✅ Test suite completion

---

## Using Logs for Troubleshooting

### Find Failed Test
```
Search for: "❌ Test FAILED"
```

### Trace Test Execution
```
Search for: "[TestClass::testMethod]"
```

### Find Element Issues
```
Search for: "Error checking"
```

### View Navigation Flow
```
Search for: "Navigating to"
```

### See Assertion Results
```
Search for: "visibility check:"
```

