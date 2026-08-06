# 🤖 AI in QA Testing

There are two main ways to use AI in software testing:

## 1. AI Testing Platforms

Use AI-powered platforms that automatically create and execute tests.

### Examples

- Autify AI
- Testim
- Momentic
- CoTester
- Aximo

---

## 2. AI Agents + Playwright
https://playwright.dev/docs/intro
Use AI coding assistants such as:

- Cursor
- GitHub Copilot
- Claude Code

These AI agents generate and maintain **Playwright** tests for your project.

---

# 🎭 What is Playwright?

**Playwright** is an automation framework that controls a web browser exactly like a real user.

Instead of manually opening a website and interacting with it, Playwright performs those actions automatically.

---

# 🚀 What Can Playwright Do?

Playwright can automate almost everything a user does in the browser.

- 🌐 Open websites
- 🖱️ Click buttons
- ⌨️ Fill forms
- 🔐 Login with email and password
- 📋 Select dropdown options
- 📤 Upload files
- 🛒 Add products to cart
- 💳 Complete checkout
- ✅ Verify expected results

---

# 🎯 What Is Playwright Used For?

## 1. End-to-End (E2E) Testing

Tests the complete user journey from start to finish.

```text
Login
   │
   ▼
Browse Products
   │
   ▼
Add to Cart
   │
   ▼
Checkout
   │
   ▼
Order Created Successfully
```

---

## 2. UI Testing

Verify that the user interface behaves correctly.

Examples:

- ✅ Is the button visible?
- ✅ Is the image displayed?
- ✅ Is the text correct?
- ✅ Is the price correct?
- ✅ Are the products displayed in the correct order?
- ✅ Are validation messages shown correctly?

---

# 📸 Screenshots

Playwright can automatically capture screenshots.

Example:

```text
❌ Login Failed

📸 Screenshot Saved
```

Screenshots make it easier to identify the cause of failures.

---

# 🎥 Video Recording

Playwright can record a complete video of every test execution.

This allows you to watch exactly what happened before the test failed.

---

# 🔍 Trace Viewer

One of Playwright's most powerful features.

It records every action performed during the test.

Example:

```text
Open Website
      │
      ▼
Click Login
      │
      ▼
Enter Email
      │
      ▼
Enter Password
      │
      ▼
Click Login
      │
      ▼
Wait for Response
      │
      ▼
Error Appeared
```

With Trace Viewer you can inspect:

- Every click
- Every locator used
- Every network request and response
- Console logs
- Timing information
- DOM snapshots
- Screenshots during execution

---

# ⭐ Why Playwright?

- ⚡ Fast execution
- 🌍 Cross-browser support (Chromium, Firefox, WebKit)
- 📱 Mobile device emulation
- 📸 Automatic screenshots
- 🎥 Video recording
- 🔍 Powerful Trace Viewer
- 🤖 Excellent integration with AI tools like Cursor, GitHub Copilot, and Claude Code

---

# How install and using in Cursor
A- Playwright Testing Platforms:
   1- Installation:
    - open cmd in your project
    - Enter npm init playwright@latest
    - choose TypeScript

   2- Run it commands:
      - npx playwright test: This command run all your test
      - npx playwright test --headed: This gives you the ability to visually see how Playwright interacts with the website.
      - npx playwright test landing-page.spec.ts: Run specific tests.
      - npx playwright test --ui: Debug tests in UI mode.
      - npx playwright test --debug: Debug tests with the Playwright Inspector.
      - npx playwright show-report: Test reports
      
B- AI Agents + Playwright MCP
   1- Configuration: 
      - Go to Cursor Settings → MCP → Add new MCP Server
      ```text
      "playwright": {
        "command": "npx",
        "args": [
          "@playwright/mcp@latest"
        ]
      }
      ```

   2- Using: By give cursor scenario and using defended rules. 

---

# 💡 Summary

There are two popular approaches to AI-powered testing:

| Approach | Description |
|----------|-------------|
| AI Testing Platforms | AI creates and maintains tests through a visual interface (Autify, Testim, Momentic, etc.) |
| AI Agents + Playwright | AI generates Playwright code that developers can customize, review, and version-control using tools like Cursor.
