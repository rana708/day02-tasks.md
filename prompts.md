## My Templates

1. Feature Test Case Generation (Web & Mobile UI/UX)

Purpose: Generate structured test cases for web and mobile features, including UI/UX, responsive layouts, and Arabic RTL alignment.

Prompt:

"Act as a Senior QA Tester. Generate a comprehensive set of test cases for the following feature:

Feature Description / Specs: [INSERT FEATURE OR USER STORY HERE, e.g., Mobile Login & OTP Verification / Shopping Cart Checkout] Platform: [Web Control Panel / Mobile App (iOS & Android)]

Output a Markdown table with columns: Test ID, Scenario, Type (Positive/Negative/Edge), Pre-conditions, Test Steps, Expected Result, Test Data Needed, and Priority. Ensure coverage for input validation, edge cases, cross-device responsiveness, and Arabic RTL layout alignment."





2. Standard Bug Report Formulation

Purpose: Transform messy notes, logs, or quick observations into a clear, developer-ready bug report.

Prompt:

"Act as a Lead QA Specialist. Convert my raw defect notes into a formal, highly detailed bug report:

Raw Defect Notes: [INSERT RAW NOTES, E.G., 'Button on Arabic mode bleeds out of screen on iPhone 13 or shift handover fails when clicking submit']

Generate a bug report with:

Defect Title: (Clear, concise summary)
Severity & Priority: (With brief justification)
Environment: (OS, Device/Browser, App Version)
Pre-conditions:
Steps to Reproduce: (Numbered, precise, deterministic steps)
Expected Result vs Actual Result:
Visual / Console Evidence Guidance: (What screenshots, network payload, or console logs developers need)"





3. Defect Retesting & Verification Charter

Purpose: Create a precise verification workflow for retesting fixed bugs and checking for regression around the fix.

Prompt:

"Act as a QA Engineer conducting bug retesting. I am verifying a resolved issue:

Original Bug: [INSERT ORIGINAL BUG TITLE & DESCRIPTION] Developer Fix Notes / PR: [INSERT DEVELOPER NOTES OR CODE FIX SUMMARY]

Provide:

Exact Retesting Steps to confirm the fix across target environments.
Boundary & Edge Conditions to try and break the fix.
A targeted Sanity / Smoke Regression Checklist for adjacent components that might be affected."




4. API Testing & Postman Payload Builder

Purpose: Generate JSON request payloads and Postman test scripts for testing REST APIs.

Prompt:

"Act as an API QA Tester. I am testing a RESTful API endpoint for [INSERT ENDPOINT PURPOSE, e.g., Profile Update / Order Processing].

Endpoint Docs / Schema: [INSERT ENDPOINT URL, METHOD & PARAMETERS]

Generate:

Test Payloads (JSON): Happy path, missing required fields, boundary limits, and invalid data types.
Postman JavaScript Test Snippets: Assertions for HTTP status codes (200/400/401/422), response execution time (< 500ms), and key field validation.
Auth/Authorization test cases: expired token, missing token, wrong role/permission, malformed header."





5. Task & Ticket Requirement Quality Audit

Purpose: Review task requirements (e.g., on Jira/ERP) before sprint execution to spot missing acceptance criteria or edge cases.

Prompt:

"Act as a QA Analyst reviewing a task ticket before testing.

Task Details: [INSERT ERP/JIRA TASK SPECIFICATIONS OR REQUIREMENTS]

Analyze the task for QA readiness:

Highlight ambiguous requirements, missing edge cases, or unstated assumptions.
Identify untestable acceptance criteria.
List clarification questions to ask the Developer or Product Owner before test execution.
If applicable, convert Acceptance Criteria into Given/When/Then (Gherkin) format."





6. Backend Code & Security Risk Assessor

Purpose: Audit backend logic (Laravel / Python / Node.js) for unhandled exceptions, SQL injection, or input validation flaws.

Prompt:

"Act as an Application Security & Backend QA Tester. Analyze the following backend code snippet:

[INSERT CODE HERE]

Tasks:

Identify security risks (e.g., raw SQL string vulnerabilities, unvalidated input execution).
Point out missing error handling or unexpected unhandled null values.
Provide specific QA test cases (positive, negative, and exploit payloads) to test this code."

⚠️ Note: Remove any secrets/API keys/customer data from the code before pasting it into any AI tool.



7. Localization, RTL, & Hydration UI Audit

Purpose: Catch RTL layout breakage, text overlap, and dynamic frontend hydration errors (e.g., Next.js / React console errors).

Prompt:

"Act as a Frontend QA Specialist focused on Arabic (RTL) localization and React/Next.js UI rendering.

UI Spec / Console Error / Code: [INSERT CONSOLE HYDRATION ERROR OR UI COMPONENT SPEC]

Provide:

Analysis of potential cause for layout breaking, text overlap, or hydration mismatches.
Checklist for verifying text alignment, icon mirroring, and font responsiveness in Arabic (RTL) vs English (LTR).
Specific cross-browser and cross-device testing steps."





8. Regression Testing Scope Checklist

Purpose: Build a targeted regression testing checklist based on sprint release notes or code changes.

Prompt:

"Act as a QA Lead preparing a release regression suite.

Release Notes / Code Changes: [INSERT CHANGELOG OR LIST OF MODIFIED FEATURES]

Generate a targeted Regression Testing Checklist:

High-risk primary workflows that MUST be verified.
Indirectly impacted modules/features that need sanity checks.
Suggested smoke test scenarios for staging/production deployment.
Add a Risk Level column (High/Medium/Low) next to each affected module to support prioritization under time constraints."




9. Exploratory Testing Charter (Time-boxed)

Purpose: Guide unstructured testing sessions to discover hidden edge cases in core app modules.

Prompt:

"Act as an Exploratory QA Specialist. Design a 30-minute Exploratory Testing Charter for:

Module / Feature: [INSERT MODULE, e.g., Multi-step Shift Handover / Course Filter & Search]

Provide:

Clear Objective & Persona.
Specific Heuristics & Angles to Probe (e.g., network disruption, rapid clicking, session timeouts, extreme input values).
Areas most likely to hide edge-case bugs."





10. Daily QA Execution Status Report

Purpose: Convert raw testing statistics into a clean, executive summary for project stakeholders.

Prompt:

"Act as a QA Specialist. Format the following daily testing progress into a professional summary report:

Execution Data:

Feature Tested: [INSERT FEATURE/MODULE NAME]
Total Test Cases Executed: [INSERT NUMBER]
Passed: [NUMBER] | Failed: [NUMBER] | Blocked: [NUMBER]
Critical/High Bugs Logged: [INSERT BUG TITLES/IDS]

Format a concise report suitable for Slack/Email/ERP comment including: Executive Summary, Current Blockers, Risk Level, and Next Actions."




11. Test Strategy for New Feature (from scratch)

Purpose: Build a test strategy before any code is written, based on risk analysis.

Prompt:

"Act as a QA Lead designing a test strategy for a new feature before development starts.

Feature Brief: [INSERT FEATURE DESCRIPTION, GOALS, USER FLOW] Tech Stack: [INSERT STACK, e.g., Next.js frontend / Laravel backend / Mobile app]

Provide:

Risk Assessment: Highest-risk areas (data integrity, security, performance, UX) and why.
Test Levels Needed: Unit / Integration / API / UI / Manual exploratory — and where automation adds most value.
Recommended Tools: Based on the stack given.
Entry/Exit Criteria: When testing can start and when the feature is "done" from a QA perspective.
Estimated Effort: Rough time/complexity estimate for QA coverage."
