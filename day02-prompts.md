# day02-prompts.md

## Prompt #1 المثال الأول: مراجعة كود برمجي (Code Review)

Original:
❌ الأمر البسيط (القديم):
"راجع هذا الكود: def get_user(user_id): query = "SELECT * FROM users WHERE id = " + user_id result = db.execute(query) return result[0]"
What is missing:
المشكلة: لم نحدد دور المراجع، السياق، القيود، أو شكل الإجابة المطلوب.

Original output (summary)

هذا الكود يعاني من مشكلتين رئيسيتين: واحدة أمنية خطيرة، وأخرى منطقية قد تسبب توقف الكود (Crash).
1. الثغرة الأمنية (SQL Injection)
المشكلة: دمج المتغير user_id مباشرة في نص الاستعلام عبر concatenation (+) يجعل التطبيق عرضة لثغرات حقن SQL (SQL Injection). إذا قام المستخدم بتمرير نص خبيث مثل '1 OR 1=1'، سيمكنه التلاعب بشرط الاستعلام وقراءة جميع بيانات الجدول أو تعديلها.
الحل: استخدام الاستعلامات المجهزة المعتمدة على المعلمات (Parameterized Queries / Prepared Statements) ليفصل المحرك بين كود SQL والبيانات الممررة.

2. خطأ وقت التشغيل (IndexError / Unhandled Exception)
المشكلة: عند تنفيذ الاستعلام عبر db.execute(query)، إذا لم يوجد مستخدم بالمعرف user_id الممرر، ستكون النتيجة مصفوفة فارغة []. الوصول إلى العنصر الأول result[0] مباشرة سيتسبب في إلقاء خطأ من نوع IndexError وتوقف البرنامج.
الحل: التحقق أولاً من وجود عناصر داخل result قبل محاولة الوصول إلى العنصر الأول.
The complete version:
 أنت مهندس برمجيات متخصص في أمان البيانات (Security).   راجع الدالة البرمجية واكتشف الأخطاء والثغرات الأمنية.
الدالة تعمل في نظام حقيقي، ورمز المستخدم user_id يأتي مباشرة من رابط الموقع.
ركز فقط على الأمان وصحة التنفيذ والتعامل مع الأخطاء (تجاهل أسماء المتغيرات والشكل).
 قائمة رقمية لكل مشكلة: [مستوى الخطورة: عالي/متوسط/منخفض] المشكلة ← سبب أهميتها ← الحل المباشر.
أريد حلولاً جاهزة للنسخ واللصق فوراً داخل المشروع.
Rewritten output (summary)

[مستوى الخطورة: عالي جداً] ثغرة حقن استعلامات إس كيو إل (SQL Injection)
سبب الأهمية: بما أن المتغير user_id يأتي مباشرة من رابط الموقع (URL Parameter) ويُدمج نصياً مع الاستعلام، يمكن لأي مهاجم الملاحة في الرابط وتمرير نصوص خبيثة مثل 1 OR 1=1 للوصول لقاعدة البيانات كاملة، أو استخدام تقنيات متقدمة لتعديل وحذف البيانات والتجاوز التام لنظام الصلاحيات.
الحل المباشر: تمرير القيم عبر الاستعلامات المعلمية (Parameterized Queries) ليصل القيمة لمحرّك قاعدة البيانات كبيانات مقيدة وليست كجزء من أصل أمر SQL.
[مستوى الخطورة: متوسط] عدم معالجة الحالات الحدية واستثناء النتيجة الفارغة (IndexError)
سبب الأهمية: عند طلب مستخدم غير موجود بالمعرف الممرر في الرابط، تُرجع قاعدة البيانات مصفوفة فارغة []. محاولة الوصول المباشر للعنصر الأول result[0] تؤدي لانهيار التطبيق فوراً بخطأ IndexError وإرجاع استجابة Server Error (500) للمستخدم.
الحل المباشر: التحقق من وجود نتائج أولاً وإرجاع None أو كائن فارغ في حال عدم العثور على المستخدم.
[مستوى الخطورة: متوس] غياب التحقق من نوع ومدخلات المستخدم (Typecasting / Input Validation)
سبب الأهمية: استقبال المدخل المباشر من الرابط كنص دون التأكد من طبيعته (كأن يتوقع النظام رقم صحيح Integer) قد يتسبب في أخطاء غير متوقعة أو ثغرات تتبع منطق العمل (Type Confusion / Logic Flaws).
الحل المباشر: تحويل القيمة صراحة إلى رقم صحيح int(user_id) والتعامل مع الخطأ في حال كانت القيمة غير قابلة للتحويل.
The difference:
مستوى الأمان: الاستجابة الأولى عالجت الثغرة الأساسية فقط، بينما الثانية أضافت خطوة أمان إضافية وهي التأكد من أن رمز المستخدم هو رقم صحيح فعلاً (int(user_id)) لتفادي المدخلات الخاطئة من الرابط.
الالتزام بالشروط: الأولى كانت إجابة عامة، بينما الثانية التزمت بالدور (مهندس أمان) وبصيغة محددة (مستوى الخطورة ← السبب ← الحل).
جاهزية الكود: كود الاستجابة الثانية أكثر حماية وأجهز للنسخ واللصق فوراً في نظام حقيقي.



## Prompt #2 المثال الثاني: كتابة توثيق لمشروع (Project Documentation)

Original:
❌ الأمر البسيط (القديم):
"اكتب توثيقاً للمشروع"
What is missing:
المشكلة: الذكاء الاصطناعي لا يعرف ما هو المشروع، لمن يكتب، وما هي تفاصيله
Original output (summary):
يبدو أنك لم ترفق كود المشروع أو تفاصيله!
يرجى تزويدي بالكود، أو إعطائي نبذة عن المشروع (مثل: اسم المشروع، التقنيات المستخدمة، الوظائف الرئيسية، والهدف منه)، وسأقوم بكتابة توثيق متكامل وشامل (Documentation / Readme) فوراً.

The complete version:
 أنت كاتب تقني تشرح الأشياء المعقدة للمبتدئين.
اكتب ملف README.md للمشروع.
 المشروع اسمه csv2json وهو أداة تحول ملفات CSV إلى JSON، ويستخدمه فريق بيانات صغير.
افترض أن القارئ لا يفهم في البرمجة إطلاقاً، اشرح ماهية "موجه الأوامر Terminal" ببساطة، ولا تتجاوز 400 كلمة.
ملف README يحتوي على الأقسام: ما هذا؟ / التثبيت / طريقة الاستخدام / مثال.
 يستطيع أي شخص غير تقني اتباع الخطوات وتطبيقها بدون مساعدة.

Rewritten output (summary):
# csv2json

## ما هذا؟
هل لديك جدول بيانات مثل **Excel** وتحتاج إلى تحويله إلى صيغة يفهمها المبرمجون والمواقع الإلكترونية تُسمى **JSON**؟ 
هذه الأداة البسيطة تُنجز لك هذه المهمة بنقرة زر واحدة! كل ما عليك فعله هو إعطاؤها ملف CSV (جدول)، وستقوم هي بتحويله فوراً إلى ملف JSON جاهز للاستخدام
## ما هو "موجه الأوامر" (Terminal)؟
تخيل أن كمبيوترك منزل. استخدام الفأرة والنقر على الأيقونات يشبه فتح الأبواب بيديك. أما **موجه الأوامر (Terminal)**، فهو مثل شاشة سحرية تكتب فيها اسم الغرفة التي تريد فتحها فتفتح فوراً!
هو نافذة سوداء أو بيضاء صغيرة، تكتب فيها أوامر نصية بسيطة ليتنفذ ما تريد بسرعة وبدون الحاجة لفتح برامج ثقيلة.
* **على ويندوز:** ابحث في القائمة عن `Command Prompt` أو `cmd`.
* **على ماك (Mac):** ابحث في التطبيقات عن `Terminal`.
## التثبيت
قبل أن تبدأ، تأكد من تثبيت لغة **Python** على جهازك (إذا لم تكن مثبتة، حملها من موقع [python.org](https://www.python.org)).
1. افتح نافذة **Terminal** على جهازك.
2. انسخ الأمر التالي والصقه داخل النافذة، ثم اضغط زر **Enter**:
3. ```bash
pip install csv2json

The difference:
الاستجابة الأولى: كانت مجرد سؤال بطلب فيه تفاصيل مشروعك عشان أقدر أساعدك.
الاستجابة الثانية: هي التوثيق الفعلي جاهز للنسخ (ملف README بسيط ومختصر، مشروح فيه الموجه البرمجي خطوة بخطوة وبأقل من 400 كلمة وبحجم خفيف جداً).




## Prompt #3
(The hypothetical system used for the experiment: a simple web authentication system — Signup / Login / Password Reset, an internal tool for ~50 employees, not public-facing.)

Original:
make a test plan for the whole system

What is missing:
Role — There is no specification of the test plan author’s role (QA Lead? What level of experience?).
Context — There is no description of the “system” itself: What are its features? Who is it for? How many users does it have?
Constraints — There is no clear scope (functional testing only? Or should performance/load testing also be included?).
Format — There is no specified structure (table? List? Separate sections for each feature?).
Examples/Criteria— There is no definition of what qualifies as a **“High priority”** test case.
Success Criteria — There is no definition of what it means for the test plan to be **“ready for execution.”**
(The Task/Goal is implicitly present: “make a test plan.”)

The complete version:
Role: You are a QA lead planning test coverage for a web application.
Task: Create a test plan for the system described below.
Context: The system is a simple web login system with three features: Signup (email + password), Login (email + password, with "remember me" option), and Password Reset (via email link). It's a small internal tool, not public-facing, used by ~50 employees.
Constraints: Cover functional and security testing only — skip performance/load testing since traffic is very low. Assume manual testing (no test automation framework set up yet).
Format: A table per feature with columns: Test Case | Steps | Expected Result | Priority (High/Medium/Low).
Examples: A "High" priority test case is one where failure would let an unauthorized user access an account, or block a legitimate user entirely.
Success criteria: A QA tester with no prior context should be able to execute the plan directly without needing to ask me clarifying questions.

Original output (summary):
The response was provided as a very generic test plan consisting of five sections: **Objective, Scope, Test Cases, Test Environment, and Exit Criteria**.
The **“Test Cases”** section was particularly speculative: it mentioned **“verify user login works”** as a general example even though the model did not actually know whether the system included a login feature—it was simply assuming a common feature.
The **“Scope”** section listed four types of testing (**functional, integration, performance, and security**) without providing any implementation details for how each type should be performed.

Rewritten output (summary):
The response was delivered as a structured test plan with a separate table for each of the three actual features (**Signup, Login, and Password Reset**):
* Each table contained **4–5 test cases** with the columns **Test Case / Steps / Expected Result / Priority**.
* It included specific, practical security scenarios: an **SQL injection attempt** in the email field, prevention of **user enumeration** (showing a generic error message instead of revealing whether an email exists), and **account lockout** after repeated failed login attempts.
* It explicitly excluded **performance/load testing** at the end and explained why (**low internal traffic**), following the specified **Constraints**.
Available next action: Create a downloadable DOCX file here in this chat containing the plan and action items above

The difference:
1. Specific Test Cases Instead of General Guesswork: The original generally assumed a “login” feature without any real system details. The completed version, thanks to the Context (the details of the three actual features), covered each feature with precise test cases based on specific, realistic behavior.
2.Real Security Depth Instead of an Empty Label: The original only listed “Security testing” as an item in the Scope without providing any details. The completed version, based on the Examples/Criteria that defined what qualifies as **High priority**, produced actual security test cases that were directly executable.
3.Immediate Execution Readiness: The original provided a general list of points that required the QA tester to write the steps themselves. The completed version, because of the specified Format and Success Criteria, was delivered as tables containing ready-to-execute steps, expected results, and priorities, without requiring additional questions.






## Prompt #4

(The hypothetical QA scenario: Testing and documenting the API endpoint `GET /api/v1/orders` used in an e-commerce platform control panel to verify search filters, pagination, and boundary conditions.)

Original: write API documentation and test cases for this endpoint: GET /api/v1/orders that filters orders by status (pending, shipped, delivered) and date range.

What is missing: 
- Context & Audience — It doesn't specify the business domain, who will use the document (QA team for test execution vs. frontend developers for integration), or the expected database volume.
- Constraints & Edge Cases — It lacks explicit requirements to cover boundary conditions, invalid query parameters, pagination rules, and standard error responses (400/401).
(Note: The Role, Task, Inputs, and basic Output Format are implicitly present in the prompt.)

The complete version: 
Role: You are a Lead Software QA Automation Engineer.
Task: Write complete API documentation and a structured manual test suite for the endpoint described below.
Context: This endpoint is used in an e-commerce admin dashboard where customer support agents search and filter through thousands of daily orders.
Inputs: Endpoint `GET /api/v1/orders` with query parameters: `status` (enum: pending, shipped, delivered), `start_date` (YYYY-MM-DD), `end_date` (YYYY-MM-DD), `page` (integer, default: 1), and `limit` (integer, default: 20).
Constraints: Include both happy paths and boundary/negative test scenarios (e.g., invalid date format, end_date before start_date, unsupported status value, page out of bounds). Cover 200 OK, 400 Bad Request, and 401 Unauthorized responses.
Format: Structured Markdown containing: 
1. Endpoint Specification & JSON Response Payload
2. Test Cases Table with columns: Test Case ID | Scenario | Input Parameters | Expected Status Code | Expected Result
Success Criteria: A QA tester should be able to execute these test cases directly against the Staging environment without needing to ask backend developers for parameter boundaries or error response formats.

Original output (summary):
The model provided a basic overview of the endpoint and listed 3 generic test cases:
- It showed a standard `200 OK` response with a basic array of order objects.
- It listed simple test steps: "Test pending status", "Test shipped status", and "Test date filter".
- It omitted negative scenarios, invalid parameter formats, boundary checks for date ranges, and pagination limits.
- It provided no explicit HTTP status code checks or structured test execution table.

Rewritten output (summary):
The model delivered a comprehensive QA testing and documentation artifact:
- **Endpoint Spec:** Documented parameters, types, defaults, and realistic `200 OK` JSON response (including `data` array and `pagination` metadata like `total_records` and `total_pages`).
- **Complete Error Schemas:** Detailed JSON outputs for `400 Bad Request` when `end_date` is earlier than `start_date` or when `status` receives an invalid string.
- **Structured QA Test Suite Table:** Provided 7 distinct test cases covering:
  - Valid status & date filtering (200 OK)
  - Default pagination verification (200 OK)
  - Boundary Date Check: `end_date < start_date` (400 Bad Request)
  - Invalid Enum Value: `status=cancelled_test` (400 Bad Request)
  - Date Format Validation: `start_date=27-09-2026` instead of `YYYY-MM-DD` (400 Bad Request)
  - Unauthorized Access: Missing Bearer Token (401 Unauthorized)

The difference:
1. **QA Test Coverage Depth:** Adding the missing Constraints forced the model to generate critical negative and boundary test cases (invalid date formats, enum validation, token authorization) instead of only 3 "happy path" checks.
2. **Actionable Test Execution:** Specifying the missing Context and Success Criteria transformed vague bullet points into a structured Test Suite table that QA engineers can directly copy into test management tools (like Jira or TestRail).
3. **API Contract Verification:** Providing clear pagination metadata and exact error JSON schemas gives QA testers exact expectations for backend response assertions.





## Prompt #5

(The hypothetical QA scenario: Writing an automation script to detect broken internal anchors and external reference links across API and system documentation files.)

Original: write a script to find broken links in our technical documentation repository

What is missing: 
- Context & Tooling — It doesn't specify the repository structure (e.g., local Markdown files in `/docs` vs. a published static site) or the preferred programming language.
- Execution Constraints — It lacks parameters for request timeouts, handling external vs. internal relative paths, and CI/CD status code behaviors.
(Note: The Role, Task, and general Goal are implicitly present in the prompt.)

The complete version: 
Role: You are a QA Automation Engineer specializing in documentation testing and tooling.
Task: Write a Python script to scan Markdown documentation files in a repository and report broken internal relative links and external HTTP links.
Context: Our team maintains system documentation in a local `/docs` directory. We need an automated pre-commit script to prevent dead links from entering the `main` branch.
Inputs: Root directory path containing `.md` files.
Constraints: Set a 5-second HTTP timeout for external link checks to avoid hanging. Filter out duplicate URL checks. Include error handling for network timeouts.
Format: Executable Python script (`check_docs_links.py`) with clean functions that prints a terminal report and exits with status code 1 if broken links exist, or 0 if all links are valid.
Success Criteria: A QA engineer can run `python check_docs_links.py ./docs` in the terminal or inside GitHub Actions to automatically fail the build when broken links are detected.

Original output (summary):
The model provided a basic web-scraping script using Python's `requests` and `beautifulsoup4`:
- It assumed the documentation was hosted on a live web server (URL) rather than local Markdown files.
- It did not handle local relative file paths (e.g., `[Setup Guide](../setup/readme.md)`).
- It lacked request timeouts, causing the execution to hang indefinitely on unreachable URLs.
- It printed findings to stdout but returned a `0` exit code regardless of errors, making it unusable for CI/CD pipeline enforcement.

Rewritten output (summary):
The model delivered an automation script tailored to repository-level QA checks:
- **Local & Remote Scanning:** Parsed `.md` files using regular expressions to validate both relative file paths on disk and absolute HTTP links.
- **Robust Execution:** Added `timeout=5` for external requests and caught `requests.exceptions.RequestException` gracefully.
- **CI/CD Readiness:** Implemented `sys.exit(1)` when broken links were identified and `sys.exit(0)` on success, accompanied by a clean summary table (File Path -> Broken Link -> Error Reason).

The difference:
1. **Automation & Pipeline Integration:** Specifying the missing Execution Constraints forced the script to return proper exit codes (`sys.exit(1)`), allowing QA to integrate it directly into GitHub Actions or Git hooks.
2. **Context-Aware Link Parsing:** Providing the missing Context (local Markdown files vs. live URLs) ensured the script validated relative repository file paths alongside HTTP web links.
3. **Reliability:** The inclusion of timeouts and exception handling prevented test run freezes during automated builds.





## Prompt #6

**Original:** improve this documentation

(The hypothetical QA scenario: Reviewing and editing a buggy setup guide for an automated testing framework to make it actionable for new QA team members.)

Original: improve this documentation snippet: To run the E2E test suite, you should try cloning the repository, then probably execute npm install to get dependencies, and if everything looks fine, run npm test to execute the suite.

What is missing: 
- Context & Target Audience — It doesn't specify who is using the guide (e.g., junior QA engineers onboarding to the project) or the project's quality standards.
- Formatting & Tone Constraints — It lacks rules to eliminate passive voice, remove hesitant language ("probably", "try"), and format steps into actionable commands.
(Note: The Role, Task, and Input snippet are provided in the prompt.)

The complete version: 
Role: You are a Senior Technical QA Editor specializing in Developer Experience (DX) and Onboarding Guides.
Task: Rewrite the provided setup documentation snippet to improve technical clarity, active tone, and execution efficiency.
Context: This documentation is part of the QA team's onboarding wiki for new test automation engineers setting up their local test environment.
Inputs: The provided informal setup text.
Constraints: Convert all sentences to active imperative voice, eliminate passive/hesitant language, use numbered execution steps with code blocks, and keep total length under 50 words.
Format: A 2-column comparison table (`Original` vs. `Improved`) followed by a copy-pasteable Markdown block.
Success Criteria: A newly joined QA engineer can follow the setup commands sequentially without encountering ambiguous instructions.

Original output (summary):
The model generated general advice on technical writing rather than providing a direct rewrite:
- It listed bullet points like "Use clear headings", "Avoid passive voice", and "Keep code snippets updated".
- It offered a slightly edited paragraph that still kept informal phrasing ("First clone the repo, then you can run npm install...").
- It did not format the instructions into distinct code blocks or actionable steps.

Rewritten output (summary):
The model provided a direct, production-ready documentation update:
- **Comparison Table:** Highlighted specific flaws (hesitant tone like "probably", lack of clear commands) versus the active improvements.
- **Actionable Markdown Snippet:** Delivered concise, numbered instructions:
  1. Clone the repository: `git clone <repo-url>`
  2. Install dependencies: `npm install`
  3. Execute E2E test suite: `npm test`

The difference:
1. **Immediate Usability:** Adding Tone and Formatting Constraints produced a clean Markdown block ready for immediate inclusion in the team wiki, rather than general writing advice.
2. **Reduced Onboarding Friction:** Removing hesitant language ("try", "probably") and presenting explicit terminal commands eliminated ambiguity for junior testers.
3. **Clarity of Improvements:** The comparison table provided rationale for each edit, making review and approval faster for the team lead.



## Prompt #7

(The hypothetical QA scenario: Debugging a failing Playwright/Selenium UI test run in the CI/CD build pipeline.)

Original: why is the CI test step failing with this log: Error: locator.click: Target page, context or browser has been closed

What is missing: 
- Context & Environment — It doesn't specify the test runner framework (e.g., Playwright Node.js vs. Python), CI environment (GitHub Actions), or recent app changes.
- Output Format — It doesn't request a structured root cause analysis or specific remediation code for the flaky test scenario.
(Note: The Role, Task, and Error Input are present in the prompt.)

The complete version: 
Role: You are a Test Automation Lead debugging flaky CI pipeline test failures.
Task: Analyze the provided Playwright CI log, determine the root cause of the failure, and provide a corrected test code pattern.
Context: This Playwright WebKit test runs inside GitHub Actions on headless Linux. The failure occurs intermittently during the user checkout automation flow when submitting payment.
Inputs: `Error: locator.click: Target page, context or browser has been closed` at `checkout.spec.js:42`.
Constraints: Focus strictly on the exact race condition or timeout cause. Do not explain general CI/CD concepts.
Format: Structured response with sections: 1. Root Cause Analysis, 2. Flakiness Trigger, 3. Corrected Code Snippet with proper wait assertions.
Success Criteria: The suggested code fix should directly eliminate the race condition causing browser context closure during CI execution.

Original output (summary):
The model listed 5 generic reasons why browser automation tests fail in CI:
- Mentioned general possibilities like "Out of memory", "Element not found", "Browser crashed", or "Invalid selector".
- Suggested general debugging advice like "Increase timeout" or "Check video recordings".
- Provided no specific code fixes or analysis of the actual Playwright execution flow.

Rewritten output (summary):
The model provided a targeted QA debugging report:
- **Root Cause Analysis:** Identified that an unhandled navigation or pop-up redirect during form submission was closing the page context before `click()` completed execution.
- **Flakiness Trigger:** Explained that headless execution in GitHub Actions runs faster/slower than local GUI runs, causing a race condition where the page navigates away while the locator is still attempting interaction.
- **Code Fix:** Provided an explicit Playwright assertion fix using `Promise.all([ page.waitForNavigation(), button.click() ])` or `await page.waitForLoadState('networkidle')` prior to interaction.

The difference:
1. **Targeted Diagnosis vs. Guesswork:** Providing the missing Environment Context allowed the model to pin down the exact race condition instead of listing general CI failures.
2. **Actionable Fix:** Requesting a specific Output Format yielded copy-pasteable test automation code rather than generic troubleshooting suggestions.
3. **Time Saved:** The QA engineer received an immediate solution to fix the flaky test without searching through generic documentation.


## Prompt #8

(The hypothetical QA scenario: Querying GitHub CLI for open PRs that are awaiting QA review and approval.)

Original: gh pr list --state open --label "needs-qa" (write a prompt to instruct the AI to generate a complete GitHub CLI query for QA PRs)

What is missing: 
- Role — There is no specification of who the AI should act as (e.g., DevOps/QA Productivity Engineer vs. standard developer).
- Examples / Evaluation Criteria — There is no definition or examples of what differentiates a "ready for QA review" PR from an unready one (e.g., Draft status, lacking required labels, or already having approvals).
(Note: The Task, Context, Inputs, Format, and Constraints are already explicitly provided in the prompt.)

The complete version: 
Role: You are a Lead QA Operations Engineer optimizing release workflows.
Task: Write a single GitHub CLI (`gh`) command to retrieve open Pull Requests that require QA verification.
Context: Our engineering team uses GitHub Pull Requests. QA engineers need a terminal one-liner to check open PRs requiring test verification during daily standups.
Inputs: Repository flags and GitHub CLI syntax.
Constraints: Exclude Draft PRs and PRs that already have approving reviews. Filter strictly by label `needs-qa`. Include fields: PR Number, Title, Author, and Created Date.
Format: A single-line executable `gh` command followed by a brief parameter breakdown.
Examples / Criteria: A valid target PR is one that is marked "Ready for Review" (not Draft) and labeled `needs-qa`. An invalid PR example is a Draft PR or one labeled `work-in-progress`.
Success Criteria: Executing the command in the terminal returns a clean list of actionable PRs requiring QA testing.

Original output (summary):
The model provided a basic command: `gh pr list --state open --label "needs-qa"`.
- It did not exclude Draft PRs, resulting in incomplete/unready work being fetched.
- It did not format the output fields, returning raw unformatted list output.
- It lacked specific criteria filtering out PRs that were already approved by peers.

Rewritten output (summary):
The model delivered an advanced, criteria-filtered GitHub CLI query:
```bash      gh pr list --state open --draft=false --label "needs-qa" --search "review:required" --json number,title,author,createdAt --template '{{range .}}#{{.number}} - {{.title}} (By @{{.author.login}})\n{{end}}       It included a clear explanation of how --draft=false and criteria-based search terms ensure only truly actionable PRs are returned.                                                                                                                                                                                                                                                                                                 The difference:                                                                                                                                                       Persona & Depth: Adding the explicit Role (QA Operations Engineer) forced the model to adopt a release-management mindset rather than offering a simplistic beginner command.                                                                                                                                                    Criteria Filtering: Specifying clear Examples/Criteria prevented the inclusion of Draft PRs and work-in-progress code, ensuring only PRs truly ready for testing appear in the output.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        ## Prompt #9                                                                                                                                                    (The hypothetical QA scenario: Summarizing a pull request for QA impact analysis and test planning.)                                                                                                                                                                                                                              Original: As a Lead QA Engineer, create a structured QA Test Strategy summary in Markdown (sections: Summary, Scenarios, Risks) for this pull request adding a discount coupon feature so I can write test cases in Jira under 150 words.                                                                                                                                                                                                                                                         What is missing:                                                                                                                                                  - Inputs — The actual code diff, modified files, schema changes, or PR details are completely missing (the model is expected to summarize something that hasn't been provided).                                                                                                                                               - Constraints — There are no explicit boundaries on what types of risks to focus on (e.g., database schema migrations, API backward compatibility, performance impact).                                                                                                                                                      (Note: The Role, Task, Context, Format, and Success Criteria are explicitly present in the prompt.)                                                                                                                                                                                                                                                                                                                                                                                                    The complete version:                                                                                                                                                 Role: You are a Lead Software QA Engineer performing test impact analysis on incoming code changes.Task: Summarize the provided PR code changes into a QA Test Strategy summary.Context: This PR updates the e-commerce checkout service to support promotional discount codes. QA needs to evaluate risk areas and write regression test cases.Inputs:    text PR Changes Summary:- Added validate_coupon() in coupon_service.py- Updated Order.calculate_total() to apply percentage and fixed-amount discounts- Added coupon_code column to orders table schema- Modified POST /api/v1/checkout to accept optional coupon_code fieldConstraints: Focus strictly on high-risk backend regression areas (e.g., database schema compatibility and order total calculation errors). Exclude frontend UI testing scope. Keep under 150 words.Format: Markdown document with sections: ## Feature Summary, ## Critical Test Scenarios, ## Regression Risk Areas, and ## Recommended Test Data.Success Criteria: A QA engineer can write targeted test cases for the feature and identify affected regression modules solely by reading this summary.                                                                                                                                                                                                                                                                                                                                          Original output (summary):                                                                                                                                          Because no code inputs were provided, the model generated a purely hypothetical summary about testing discount coupons in general:                                 It listed generic UI test scenarios ("Click coupon button", "Enter promo code").                                                                                It guessed generic features that might not exist in the backend PR.                                                                                              It missed specific backend risks like database column nullability or mathematical calculation bugs.                                                                                                                                                                                                                                    Rewritten output (summary):                                                                                                                                     The model delivered a precise, code-aware QA Impact Analysis based on the provided inputs:                                                                         Feature Summary: Highlighted backend updates to checkout API, calculation service, and database schema                                                             Critical Test Scenarios: Focused on backend logic: percentage vs. fixed-amount discount calculations and null/empty string handling.                               Regression Risk Areas: Explicitly flagged Order.calculate_total() as a critical regression point affecting all standard non-discount checkouts.                    Constraints Applied: Excluded UI scope completely, keeping the output under the 150-word limit.                                                                                                                                                                                                                                    The difference:                                                                                                                                                   Concrete vs. Speculative Analysis: Providing the missing Inputs allowed the model to analyze real code diffs (file names, methods, schema changes) instead of hallucinating generic feature ideas.Boundary Precision: Adding specific Constraints directed the focus exclusively to backend data/API risks rather than wasting space on frontend UI checks.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              ## Prompt #10                                                                                                                                                  (The hypothetical QA scenario: Onboarding junior test automation engineers on how to conduct peer code reviews for automation scripts.)                                                                                                                                                                                         Original: You are a QA Automation Manager onboarding junior test automation engineers. Explain how to perform effective code reviews on test automation scripts (Selenium/Playwright) in our team, focusing on avoiding hardcoded data, handling explicit waits, and ensuring test independence in under 250 words.                                                                                                                                                                                      What is missing:                                                                                                                                               - Format — There is no layout or structural specification (e.g., plain paragraphs vs. structured Markdown checklist vs. bulleted rules).- Success Criteria — There is no clear definition of what constitutes a successful, actionable explanation (e.g., providing copy-pasteable review comment templates or actionable verification steps).                                                                                                                                         (Note: The Role, Task, Context, Inputs, and Constraints are explicitly provided in the prompt.)                                                                                                                                                                                                                                       The complete version:                                                                                                                                              -Role: You are a QA Automation Manager onboarding junior test automation engineers.                                                                                -Task: Explain how to perform effective code reviews on test automation scripts (Selenium/Playwright).                                                             - Context: Our QA team maintains a shared test automation repository. Junior engineers are learning to review peer test scripts for maintainability, flakiness, and hardcoded data.                                                                                                                                                -Inputs: Common test automation anti-patterns (flaky waits, hardcoded test data).                                                                                  -Constraints: Keep tone encouraging and practical. Avoid academic language. Limit total response to under 250 words.                                               -Format: Structured Markdown guide: Why QA Code Reviews Matter` -> `Automation Review Checklist (4 Items)` -> `Constructive Review Comment Examples
-Success Criteria: The guide must include a practical, copy-pasteable checklist and real example comments that a junior tester can directly reference during their first PR review.

Original output (summary):
The model produced a well-written but unstructured essay in plain paragraphs:
- It explained the concepts of waits and hardcoded data clearly in prose.
- It lacked visual hierarchy, making it hard to use as a quick reference tool during an actual code review.
- It contained no practical comment templates or clear success indicators for the reader.

Rewritten output (summary):
The model delivered a highly structured, actionable Onboarding Reference Guide:
- **Why It Matters:** Brief 2-sentence intro on preventing flaky builds in CI.
- **Checklist Format:** 4 clear, bolded checklist items (No Hardcoded Data, Explicit Waits Only, Test Independence, Assertion Quality).
- **Constructive Comment Examples:** Included explicit quotes/templates junior testers can copy into GitHub PR comments (e.g., *"Consider using `waitForSelector` here instead of fixed sleep to prevent CI flakiness"*).
- **Fulfilling Success Criteria:** Provided an immediate reference card ready for daily team use.

The difference:
1. **Readability & Usability:** Defining the missing Format converted a block of narrative text into a structured checklist card ideal for quick scanning during PR reviews.
2. **Actionable Delivery:** Specifying Success Criteria forced the model to include concrete comment templates, bridging the gap between theory and real-world execution.



