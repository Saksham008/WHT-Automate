# Architecture & Component Overview

## 🏗️ Project Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                  SELENIUM AUTOMATION SUITE                      │
│              PWC Withholding Tax - Login Automation             │
└─────────────────────────────────────────────────────────────────┘

┌──────────────────────────┐
│     TEST EXECUTION       │
├──────────────────────────┤
│  TestNG Test Runner      │
│  ├─ Priority-based       │
│  ├─ Parallel (2 threads) │
│  └─ Data-driven          │
└────────────┬─────────────┘
             │
    ┌────────┴────────────┐
    ▼                     ▼
┌─────────────┐      ┌──────────────────┐
│  Test Class │      │  Test Listeners  │
│  (Login)    │◄─────┤  ProjectListener │
│             │      └──────────────────┘
└─────────────┘            │
    │                      ├─► Extent Reports Manager
    │                      ├─► Screenshot Manager
    │                      └─► Logging Events
    ▼
┌─────────────────────────────────────┐
│   Page Object Model (POM)           │
├─────────────────────────────────────┤
│  LoginPage                          │
│  ├─ login()                         │
│  ├─ isWhtHeadingVisible()           │
│  ├─ isErrorMessageVisible()         │
│  ├─ isDashboardTextVisible()        │
│  └─ navigateToAdminPage()           │
│                                     │
│  EntityPage                         │
│  └─ isEntityTextVisible()           │
└────────────┬────────────────────────┘
             │
    ┌────────┴─────────────┐
    ▼                      ▼
┌─────────────────┐  ┌──────────────────┐
│  Selenium WebDriver      │  Utilities   │
│  ├─ Chrome Driver        │  ├─ JsonReader
│  ├─ WebElements  ◄───────┼─ PropertyReader
│  └─ Wait Logic           │  ├─ ExtentReportManager
└─────────────────┘        │  ├─ ScreenshotManager
                           │  └─ DriverFactory
                           └──────────────────┘
    ▼                      ▼
┌─────────────┐  ┌────────────────────────┐
│   Browser   │  │  Output / Reporting    │
│   Chrome    │  ├─ HTML Reports
│             │  ├─ Screenshots
└─────────────┘  └─ Logs & Artifacts
```

---

## 📊 Test Execution Flow

```
START
 │
 ├─► Setup: BaseTest.setup()
 │   ├─ Initialize WebDriver
 │   ├─ Navigate to URL
 │   └─ Set Implicit Waits
 │
 ├─► Priority 1: verifyEmptyLogin
 │   ├─ Listener.onTestStart()
 │   ├─ Test execution
 │   ├─ Listener.onTestSuccess/Failure()
 │   │  ├─ Take Screenshot
 │   │  ├─ Attach to Report
 │   │  └─ Log Result
 │   └─ Teardown
 │
 ├─► Priority 2: verifyInvalidLogin (Data Set 1)
 │   └─ [Same flow as above]
 │
 ├─► Priority 2: verifyInvalidLogin (Data Set 2)
 │   └─ [Same flow as above]
 │
 ├─► Priority 3: verifyInvalidUsername
 │   └─ [Same flow as above]
 │
 ├─► Priority 4: verifyInvalidPassword
 │   └─ [Same flow as above]
 │
 ├─► Priority 5: verifyValidLoginAndNavigateToAdmin
 │   └─ [Same flow as above]
 │
 ├─► Listener.onFinish()
 │   ├─ Generate HTML Report
 │   ├─ Print Summary
 │   └─ Flush Reports
 │
 └─► END
```

---

## 📈 Data Flow Diagram

```
┌─────────────────────────────────────────────────────────┐
│                   EXECUTION CYCLE                       │
└─────────────────────────────────────────────────────────┘

TEST DATA (JSON)
├─ validlogin.json
│  └─ username: itadmin_wht_qa
│     password: itadmin@123
│
└─ invalidlogin.json
   ├─ invalid_user / invalid_pass
   └─ invalid_user2 / invalid_pass2

        ▼
┌─────────────────────────────────────────────────────────┐
│              TEST EXECUTION ENGINE                      │
│  (TestNG with Data Providers)                           │
└─────────────────────────────────────────────────────────┘

        ▼
┌─────────────────────────────────────────────────────────┐
│           LOGIN PAGE TEST LOGIC                         │
│  1. Enter Username ─────┐                               │
│  2. Enter Password ─────┼─► Send Keys to WebElements    │
│  3. Click Login Button ─┘                               │
│  4. Wait for Response                                   │
│  5. Verify Result                                       │
└─────────────────────────────────────────────────────────┘

        ▼
┌─────────────────────────────────────────────────────────┐
│        ASSERTION & LOGGING                              │
│  ├─ Check: Dashboard Visible / Error Message            │
│  ├─ Log: Result with Timestamp                          │
│  └─ Capture: Screenshot                                │
└─────────────────────────────────────────────────────────┘

        ▼
┌─────────────────────────────────────────────────────────┐
│        LISTENER EVENTS                                  │
│  ├─ onTestSuccess/Failure                              │
│  ├─ Attach Screenshot to Report                        │
│  └─ Update Report Status                               │
└─────────────────────────────────────────────────────────┘

        ▼
┌─────────────────────────────────────────────────────────┐
│        OUTPUT GENERATION                                │
│  ├─ HTML Report (Extent)                               │
│  ├─ Screenshots (PNG)                                  │
│  └─ Console Logs (SLF4J)                               │
└─────────────────────────────────────────────────────────┘
```

---

## 🔗 Component Interactions

```
┌────────────────────────────────────────────────────────────┐
│                   LOGIN.JAVA (TEST)                        │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ @Test(priority = N)                                │  │
│  │ public void testMethod(String user, String pass) { │  │
│  │   LoginPage loginPage = new LoginPage(driver);      │  │
│  │   loginPage.login(user, pass);     ──────────┐     │  │
│  │   loginPage.verify...();                     │     │  │
│  │ }                                             │     │  │
│  └──────────────────────────────────────────┬───┘     │  │
│                                             │         │  │
│                                    ┌────────▼──────┐  │  │
│                                    │ loginPage()   │  │  │
│                                    └────────┬──────┘  │  │
└────────────────────────────────────────────┼──────────┘  │
                                             │
                    ┌────────────────────────┴───────────┐
                    ▼                                     ▼
        ┌──────────────────────────┐      ┌──────────────────────┐
        │    LOGINPAGE.JAVA        │      │   ENTITYPAGE.JAVA    │
        │ (Page Object Model)      │      │ (Page Object Model)  │
        │                          │      │                      │
        │ - usernameInput          │      │ - entityText         │
        │ - passwordInput          │      │                      │
        │ - loginButton            │      │ Methods:             │
        │ - errorMessage           │      │ - isEntityText...()  │
        │ - dashboardText          │      │                      │
        │ - burgerMenuButton       │      │ Logging:             │
        │ - adminButton            │      │ - Element checks     │
        │                          │      │ - Visibility status  │
        │ Methods:                 │      │                      │
        │ - login()  ───────┐      │      │                      │
        │ - verify...()     │      │      │                      │
        │ - navigate...() ──┼──┐   │      │                      │
        │                  │  │   │      │                      │
        │ Logging:         │  │   │      │                      │
        │ - Method entry   │  │   │      │                      │
        │ - Element actions│  │   │      │                      │
        │ - Wait status    │  │   │      │                      │
        │ - Error capture  │  │   │      │                      │
        └──────────────────────────┘      └──────────────────────┘
                 │                                    │
                 ├────────────────┬───────────────────┤
                 ▼                ▼                   ▼
        ┌──────────────────────────────────────────────────┐
        │        PROJECTLISTENER.JAVA                      │
        │  (Test Listener - ITestListener)                │
        │                                                  │
        │  Events:                                         │
        │  ├─ onStart()                                   │
        │  │  └─► ExtentReportManager.initReports()      │
        │  ├─ onTestStart(result)                        │
        │  │  └─► ExtentReportManager.createTest()       │
        │  ├─ onTestSuccess(result)                      │
        │  │  ├─► ExtentTest.pass()                      │
        │  │  ├─► ScreenshotManager.getBase64()          │
        │  │  └─► extentTest.addScreenCaptureFromBase64()
        │  ├─ onTestFailure(result)                      │
        │  │  ├─► ExtentTest.fail()                      │
        │  │  ├─► ScreenshotManager.getBase64()          │
        │  │  └─► extentTest.addScreenCaptureFromBase64()
        │  └─ onFinish()                                 │
        │     └─► ExtentReportManager.flushReports()     │
        └──────────────────────────────────────────────────┘
                 │
         ┌───────┴──────────┬─────────────┐
         ▼                  ▼              ▼
    ┌─────────────┐  ┌────────────┐  ┌────────────┐
    │  EXTENT     │  │ SCREENSHOT │  │   LOGS     │
    │  REPORTS    │  │  MANAGER   │  │  (SLF4J)   │
    │             │  │            │  │            │
    │  - HTML     │  │ - Base64   │  │ - INFO     │
    │  - Embed    │  │ - PNG Save │  │ - DEBUG    │
    │   Screen    │  │ - Timestamp│  │ - ERROR    │
    │  - Stats    │  │            │  │            │
    └─────────────┘  └────────────┘  └────────────┘
         │                │                │
         └────────────────┴────────────────┘
                  ▼
        ┌──────────────────────────────────┐
        │    OUTPUT / ARTIFACTS            │
        ├──────────────────────────────────┤
        │ ✅ test-output/                  │
        │    ├─ ExtentReports/             │
        │    │  └─ Report_[timestamp].html │
        │    │     (With embedded images)  │
        │    └─ Screenshots/               │
        │       └─ [test]_[timestamp].png  │
        │ ✅ Console Logs                  │
        └──────────────────────────────────┘
```

---

## 🔄 Request-Response Cycle

```
CLIENT (Test Code)              BROWSER (Chrome)           APPLICATION (Server)
         │                             │                           │
         ├─ Enter Username ───────────►│                           │
         │                             ├─ Send Form Data ─────────►│
         │                             │                           │
         │                             │◄─ Response (Login Failed) ◄┤
         │◄──────────────────────────────┤                         │
         │ Error Message Displayed       │                         │
         │                             │                           │
         └─ Verify Error ◄─────────────┴───────────────────────────┘
                │
                ▼
         ┌──────────────────┐
         │ Take Screenshot  │
         │ Log Status: FAIL │
         │ Attach to Report │
         └──────────────────┘
```

---

## 🎯 Logging Flow

```
┌─────────────────────────────────────────┐
│          TEST START EVENT               │
│  └─► ProjectListener.onTestStart()      │
│      └─► Log: "Test Started: ..."       │
│          ExtentReportManager.createTest()│
└─────────────────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────────┐
│       TEST EXECUTION                    │
│  ├─► Login.verifyInvalidLogin()         │
│  │   └─► Logger.info("Starting test...")│
│  │                                     │
│  ├─► LoginPage.login()                  │
│  │   ├─► Logger.debug("Entering...")   │
│  │   ├─► Logger.debug("Clicking...")   │
│  │   └─► Logger.info("Login attempted")│
│  │                                     │
│  └─► LoginPage.isErrorMessageVisible() │
│      ├─► Logger.debug("Checking...")  │
│      └─► Logger.info("Error visible")  │
└─────────────────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────────┐
│       TEST RESULT EVENT                 │
│  ├─► onTestSuccess/Failure()            │
│  ├─► Logger: "✅ Test PASSED"           │
│  ├─► Screenshot captured                │
│  └─► Extent Report updated              │
└─────────────────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────────┐
│     ALL TESTS COMPLETED                 │
│  └─► ProjectListener.onFinish()         │
│      ├─► Log Summary Statistics         │
│      ├─► ExtentReports.flush()          │
│      └─► HTML Report Generated          │
└─────────────────────────────────────────┘
```

---

## 📦 Dependency Tree

```
selenium_automation_suite
├── org.seleniumhq.selenium:selenium-java:4.40.0
│   ├── org.openqa.selenium.chrome:ChromeDriver
│   ├── org.openqa.selenium:WebDriver
│   └── org.openqa.selenium.support:PageFactory
│
├── org.testng:testng:7.12.0
│   ├── ITestListener
│   ├── @Test annotation
│   ├── @DataProvider
│   └── SoftAssert
│
├── org.slf4j:slf4j-api:2.0.17
│   └── Logger interface
│
├── ch.qos.logback:logback-classic:1.5.27
│   └── SLF4J implementation
│
├── com.fasterxml.jackson.core:jackson-databind:2.21.0
│   └── JSON parsing
│
└── com.aventstack:extentreports:5.1.1
    ├── ExtentReports
    ├── ExtentTest
    ├── ExtentSparkReporter
    └── Screenshot embedding

```

---

## ✅ Summary

This architecture provides:
- ✅ **Separation of Concerns** - Tests, Pages, Listeners separated
- ✅ **Testability** - Easy to add/modify tests
- ✅ **Maintainability** - Clean Page Object Model
- ✅ **Visibility** - Comprehensive logging
- ✅ **Evidence** - Automatic screenshots
- ✅ **Reporting** - Professional HTML reports
- ✅ **Scalability** - Thread-safe implementation
- ✅ **Reliability** - Error handling throughout

