# 🤖 AI in QA Testing

There are two main ways to use AI in software testing:

## 1. AI Testing Platforms

Use AI-powered platforms that automatically create and execute tests.

### Examples

* Autify AI
* Testim
* Momentic
* CoTester
* Aximo

These platforms usually provide a higher-level testing experience where AI can help create, execute, maintain, and analyze tests through a visual interface.

---

# 2. AI Agents + Playwright

Another powerful approach is combining:

* AI Coding Agents
* Playwright
* Playwright MCP
* Playwright Test Agents

Examples of AI coding agents:

* Cursor
* GitHub Copilot
* Claude Code

The AI agent can understand testing requirements, interact with the browser, generate Playwright tests, execute them, analyze failures, and improve the tests.

---

# 🎭 What is Playwright?

**Playwright** is an automation framework that controls a web browser exactly like a real user.

Instead of manually opening a website and interacting with it, Playwright performs those actions automatically.

---

# 🚀 What Can Playwright Do?

Playwright can automate almost everything a user does in the browser.

* 🌐 Open websites
* 🖱️ Click buttons
* ⌨️ Fill forms
* 🔐 Login with email and password
* 📋 Select dropdown options
* 📤 Upload files
* 🛒 Add products to cart
* 💳 Complete checkout
* ✅ Verify expected results
* 📸 Take screenshots
* 🎥 Record videos
* 🔍 Capture traces
* 🌐 Inspect network requests
* 🧪 Execute automated tests

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

Playwright can verify that the user interface behaves correctly.

Examples:

* ✅ Is the button visible?
* ✅ Is the image displayed?
* ✅ Is the text correct?
* ✅ Is the price correct?
* ✅ Are products displayed in the correct order?
* ✅ Are validation messages shown correctly?
* ✅ Is the button disabled/enabled correctly?
* ✅ Does navigation work correctly?

---

# 📸 Screenshots

Playwright can automatically capture screenshots.

Screenshots make it easier to identify the visual state of the application when a test fails.

---

# 🎥 Video Recording

Playwright can record a complete video of a test execution.

This allows you to watch exactly what happened before the test failed.

---

# 🔍 Trace Viewer

One of Playwright's most powerful debugging features is **Trace Viewer**.

It records the actions performed during the test and provides detailed information about what happened.

With Trace Viewer you can inspect:

* Every action
* Every locator
* DOM snapshots
* Screenshots
* Network activity
* Console messages
* Timing information
* Test errors
* Before/after states

---

# ⭐ Why Playwright?

* ⚡ Fast execution
* 🌍 Cross-browser support
* 📱 Mobile device emulation
* 📸 Automatic screenshots
* 🎥 Video recording
* 🔍 Powerful Trace Viewer
* 🧪 Powerful assertions
* 🔄 Auto-waiting
* 🤖 Excellent integration with AI agents
* 🌐 Supports Chromium, Firefox, WebKit, and Edge

---

# 🧠 Playwright MCP

**Playwright MCP** is the bridge between an AI agent and the browser.

MCP stands for:

```text
Model Context Protocol
```

The important idea is:

```text
AI Agent
   │
   ▼
Playwright MCP
   │
   ▼
Browser
   │
   ▼
Website
```

Playwright MCP allows AI agents to interact with web pages through browser automation capabilities.

---

# 🤖 Playwright Test Agents

On top of **Playwright MCP**, Playwright provides **Playwright Test Agents**.

These agents provide a higher-level workflow for creating and maintaining Playwright tests.

There are three main agents:

```text
                Playwright Test Agents
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
       Planner        Generator       Healer
```

## 🎭 Planner

The **Planner** explores the application and creates a detailed Markdown test plan.

Its role is to determine:

* What should be tested
* Which scenarios should be covered
* Required test steps
* Expected results
* Edge cases
* Preconditions

The output is a Markdown specification that can later be used by the Generator.

---

## 🎭 Generator

The **Generator** takes the Markdown test plan and converts it into executable Playwright tests.

It can interact with the application to help determine appropriate locators, actions, and assertions while generating the tests.

---

## 🎭 Healer

The **Healer** is responsible for dealing with failing tests.

It can:

* Reproduce the failure
* Inspect the current application state
* Analyze the failure
* Identify potential causes
* Suggest or apply test fixes
* Re-run the test

The goal is to determine whether the problem is with the test or with the application itself.

---

## Playwright Test Agents

The Agents provide the **testing workflow**.

Think of them as the QA workflow layer.

```text
Planner
   ↓
Generator
   ↓
Healer
```
---

# 💻 Installing Playwright in Cursor

## A. Install Playwright

Open CMD/Terminal inside your project:

```bash
npm init playwright@latest
npm init playwright@latest
```

Choose:

```text
TypeScript
```

This creates the Playwright testing environment.

---

# ▶️ Running Playwright Tests

### Run all tests

```bash
npx playwright test
```

### Run tests with visible browser

```bash
npx playwright test --headed
```

This allows you to visually see Playwright interacting with the website.

### Run a specific test

```bash
npx playwright test landing-page.spec.ts
```

### UI Mode

```bash
npx playwright test --ui
```

Useful for interactively debugging tests.

### Debug Mode

```bash
npx playwright test --debug
```

Opens the Playwright Inspector for debugging.

### Show Test Report

```bash
npx playwright show-report
```

---

# 🔌 Installing Playwright MCP in Cursor

Playwright MCP can be configured from:

```text
Cursor
   ↓
Settings
   ↓
MCP
   ↓
Add new MCP Server
```

Configuration:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": [
        "@playwright/mcp@latest"
      ]
    }
  }
}
```

---

# 🤖 Installing Playwright Test Agents

Playwright provides an `init-agents` command for generating the Agent definitions.

For VS Code:

```bash
npx playwright init-agents --loop=vscode
```
---

# 🖥️ Playwright Agents in Cursor

If you are using Cursor, the configuration is conceptually similar to VS Code, but Cursor uses its own project configuration directory.

Instead of:

```text
.vscode/
```

Cursor uses:

```text
.cursor/
```

The general structure can look like:

```text
Project
│
├── .cursor/
│
├── specs/
│
├── tests/
│
├── playwright.config.ts   ← Defines the project base URL and Playwright configuration (await page.goto('https://example.com/login');)
│
└── package.json
```
---

# ⚙️ Enable Playwright Testing in Cursor

After configuring Playwright, open Cursor Settings and make sure the **Playwright Test** integration/extension is enabled.

Conceptually:

```text
Cursor Settings
      ↓
Extensions / Testing
      ↓
Playwright Test
      ↓
Enable
```

---

# 📝 Using the Planner in Cursor

When you want to create a test plan first, use the Planner instead of immediately generating `.spec.ts` files.

In Cursor, you can reference the planning instructions/agent from the chat using the appropriate agent command or configuration.

For example, the workflow is:

```text
Planner
   ↓
Markdown Test Plan
   ↓
Generator
   ↓
Playwright Test
```

The Markdown specification acts as the bridge between planning and test generation.

---

# 📄 Using the Generated Markdown Plan

After the Planner creates the Markdown specification, the Generator uses that specification as its source for generating the Playwright tests.

The workflow becomes:

```text
Test Requirement
      ↓
Planner
      ↓
.specification.md
      ↓
Generator
      ↓
.spec.ts
      ↓
Playwright
      ↓
Test Execution
```

---

# 🩹 Using Healer

When a generated Playwright test fails:

```text
Failing Test
     ↓
Healer
     ↓
Analyze Failure
     ↓
Inspect Application
     ↓
Fix Test
     ↓
Run Again
     ↓
Verify Result
```

The Healer should not simply hide failures. It should help distinguish between:

```text
Test Problem
```

and:

```text
Application Bug
```

This distinction is critical in professional QA.

---

# 🏆 The Big Picture

The complete AI-powered Playwright workflow is:

```text
🧠 Plan
   ↓
🎭 Explore
   ↓
📝 Generate Test Plan
   ↓
💻 Generate Test Code
   ↓
🧪 Execute Tests
   ↓
🔍 Analyze Failures
   ↓
🩹 Heal Tests
   ↓
🔁 Re-run
   ↓
✅ Verified Test Suite
```

---

# 💡 Summary

There are three useful levels to distinguish:

| Approach                                    | What it does                                                                   |
| ------------------------------------------- | ------------------------------------------------------------------------------ |
| **AI Testing Platforms**                    | High-level AI testing through platforms such as Autify, Testim, Momentic, etc. |
| **AI Agent + Playwright MCP**               | AI directly controls the browser through Playwright MCP                        |
| **AI Agent + Playwright Test Agents + MCP** | Full workflow: **Plan → Generate → Execute → Heal**                            |

The third approach provides a complete AI-assisted QA workflow while keeping the resulting tests as real **Playwright/TypeScript code** inside the project.

---

# 📚 References

* [Agents | Playwright](https://playwright.dev/docs/test-agents)
* [Playwright MCP + AI Agents — A Practical Setup Guide | ShapeMyInterview](https://www.shapemyinterview.com/resources/playwright-mcp-ai-agents-guide)
* [Introduction | Playwright](https://playwright.dev/mcp/introduction)
* [Installation | Playwright](https://playwright.dev/docs/intro)
