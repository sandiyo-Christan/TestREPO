# AWS Security Agent — Benchmark Data Capture Guide
## What to capture in your Excel workbook (single source of truth)

---

## YOUR OBJECTIVE (keep this visible)
> Produce a benchmark & whitepaper that proves:
> 1. **Coverage** — what it finds, what it misses (detection rate per language, per vuln category)
> 2. **Differentiation from Manual Pentesting** — unique strengths, blind spots, hybrid model
> 3. **Efficiency** — time, cost, quality per language, per capability
> 4. **Accuracy** — false positive rate, precision, recall, F1 — is the signal trustworthy?
> 5. **Actionability** — are findings developer-ready? (PoC quality, fix suggestions, remediation guidance)
> 6. **Contextual Intelligence** — attack chain detection that siloed tools miss (AWS SA's key differentiator)
> 7. **Adoption Friction** — setup time, integration effort, learning curve, developer workflow fit
>
> *Objectives 1-3: "Is it good?" | Objective 4: "Can I trust it?" | Objective 5: "Can my team use it?" | Objective 6: "What can it do that nothing else can?" | Objective 7: "How hard is it to adopt?"*

---

## EXCEL STRUCTURE: 8 Sheets

---

### SHEET 1: COMPETITIVE FEATURE MATRIX (Desk Research — No Execution)

**Purpose:** Map every tool's capabilities so you know what to test AWS Security Agent against.

**Tools to cover:** AWS Security Agent, Snyk, Checkmarx (CxOne), SonarQube/SonarCloud, Veracode, Semgrep, GitHub Advanced Security (CodeQL), Burp Suite Pro, OWASP ZAP, Wiz, Prisma Cloud

**Rows = Tools (one row per tool), Columns = these data points:**

| # | Column | What to capture | Where to find it |
|---|--------|----------------|-----------------|
| 1 | Tool Name | — | — |
| 2 | Vendor | — | — |
| 3 | Product Category | SAST / SCA / DAST / Pentest / IaC / Container / Design Review / Secret Detection / API Security — mark all that apply | Product homepage |
| 4 | SAST Supported | Yes/No | Docs |
| 5 | SAST — Languages Supported (list all) | e.g., "Python, Java, JS, TS, Go, C#, Ruby, PHP, Kotlin, Rust, Swift, Scala, C/C++" | Docs — language support page |
| 6 | SAST — Total Language Count | Number | Count from above |
| 7 | SAST — Framework-Aware Rules | Yes/No + which frameworks (e.g., "Django, Flask, Spring Boot, Express") | Docs |
| 8 | SAST — Custom Rule Support | Yes/No + format (YAML/QL/Proprietary) | Docs |
| 9 | SAST — Auto-Fix Suggestions | Yes/No | Docs |
| 10 | SAST — PR/MR Integration | Yes/No | Docs |
| 11 | SCA Supported | Yes/No | Docs |
| 12 | SCA — Package Ecosystems | npm, PyPI, Maven, Go Modules, NuGet, RubyGems, Cargo, pub, Composer — list all | Docs |
| 13 | SCA — Transitive Dependency Detection | Direct Only / Full Tree | Docs |
| 14 | SCA — Reachability Analysis | Yes/No (does it check if the vulnerable function is actually called?) | Docs |
| 15 | SCA — Vulnerability DB | NVD Only / Proprietary / Both | Docs |
| 16 | SCA — License Detection | Yes/No | Docs |
| 17 | SCA — Auto-Upgrade PRs | Yes/No | Docs |
| 18 | DAST Supported | Yes/No | Docs |
| 19 | DAST — Authenticated Scanning | Yes/No | Docs |
| 20 | DAST — API Scanning (REST/GraphQL/gRPC) | Mark which | Docs |
| 21 | DAST — SPA/JS Rendering | Yes/No | Docs |
| 22 | DAST — Custom Auth Flows | Yes/No | Docs |
| 23 | Pentest Supported | Yes/No (automated pentest, not DAST) | Docs |
| 24 | Pentest — Attack Chain Detection | Yes/No | Docs |
| 25 | Pentest — Business Logic Testing | Yes/No | Docs |
| 26 | Pentest — Risk Categories Covered | Count + list | Docs |
| 27 | Pentest — OWASP Top 10 Coverage | % or list of which categories | Docs |
| 28 | Pentest — OWASP API Top 10 Coverage | % or list | Docs |
| 29 | Pentest — Evidence/PoC Generation | Yes/No | Docs |
| 30 | IaC Scanning Supported | Yes/No | Docs |
| 31 | IaC — Platforms (Terraform/CFN/CDK/Pulumi/K8s/Dockerfile/Helm) | Mark which | Docs |
| 32 | Container Security Supported | Yes/No | Docs |
| 33 | Container — Image Scanning | Yes/No | Docs |
| 34 | Container — Runtime Protection | Yes/No | Docs |
| 35 | Container — SBOM Generation | Yes/No | Docs |
| 36 | Design Review Supported | Yes/No | Docs |
| 37 | Design Review — Architecture Diagram Ingestion | Yes/No | Docs |
| 38 | Design Review — Threat Modeling | Yes/No | Docs |
| 39 | Design Review — Pre-Code Security Feedback | Yes/No | Docs |
| 40 | Secret Detection Supported | Yes/No | Docs |
| 41 | Secret Detection — Git History Scanning | Yes/No | Docs |
| 42 | API Security — Schema Validation | Yes/No | Docs |
| 43 | API Security — BOLA/IDOR Detection | Yes/No | Docs |
| 44 | Deployment Model | SaaS / Self-Hosted / Hybrid / Agent-Based | Docs |
| 45 | CI/CD Integrations | GitHub Actions, GitLab CI, Jenkins, CodePipeline, etc. — list all | Docs |
| 46 | IDE Integrations | VSCode, IntelliJ, etc. | Docs |
| 47 | Pricing Model | Per Dev / Per Scan / Per Project / Consumption | Pricing page |
| 48 | Free Tier Available | Yes/No + limits | Pricing page |
| 49 | Enterprise Price (approx $/yr) | Approximate | Pricing page / sales quotes |
| 50 | Compliance Certs | SOC2, FedRAMP, ISO27001, etc. | Docs |
| 51 | Documentation URL | Link | — |

---

### SHEET 2: SAST LANGUAGE DEPTH (Per Tool, Per Language)

**Purpose:** Your manager's core ask — how deep is each tool for each language?

**Structure:** Rows = Language + Framework combos. Columns = one group per tool.

**Languages to test (tiered by market usage):**

**Tier 1 — Must test (highest adoption, diverse paradigms):**
- Python (Django, Flask, FastAPI)
- JavaScript/TypeScript (Express, NestJS, React*, Angular*, Vue*, Next.js)
- Java (Spring Boot, Jakarta EE)
- Go (Gin, Echo)
- C# / .NET (ASP.NET Core)

**Tier 2 — Should test (significant usage, different attack surfaces):**
- Kotlin (Spring Kotlin, Ktor, Android)
- Ruby (Rails)
- PHP (Laravel, WordPress)
- Rust (Actix Web, Rocket)

**Tier 3 — If time permits (mobile/niche):**
- Swift (iOS)
- Dart/Flutter
- React Native
- Scala

*React/Angular/Vue = frontend frameworks — test via DAST on running apps, not SAST on JSX/templates*

**Columns per tool (repeat this block for AWS SA, Snyk, Checkmarx, SonarQube, Semgrep, CodeQL):**

| # | Column | What to capture |
|---|--------|----------------|
| 1 | Language | e.g., Python |
| 2 | Framework | e.g., Django |
| 3 | Tool Name | e.g., AWS Security Agent |
| 4 | Language Supported | Yes/No |
| 5 | Framework-Specific Rules | Yes/No |
| 6 | Rule Count (if available) | Number — how many SAST rules for this language |
| 7 | Vuln Categories Covered | List CWEs: SQLi, XSS, SSRF, Command Injection, Path Traversal, etc. |
| 8 | Auto-Fix Available for This Language | Yes/No |
| 9 | Source | Documentation URL or page reference |

---

### SHEET 3: VULNERABILITY COVERAGE MATRIX (What vulns can each tool catch, per language?)

**Purpose:** The precision matrix — for each vulnerability type, which tool catches it in which language?

**Rows = Vulnerability types (34 key types below). Columns = Language × Tool combos.**

**Vulnerability types to track:**

| # | Vulnerability | CWE | OWASP 2021 |
|---|--------------|-----|------------|
| 1 | SQL Injection | CWE-89 | A03 |
| 2 | NoSQL Injection | CWE-943 | A03 |
| 3 | Command Injection (OS) | CWE-78 | A03 |
| 4 | LDAP Injection | CWE-90 | A03 |
| 5 | XSS — Reflected | CWE-79 | A03 |
| 6 | XSS — Stored | CWE-79 | A03 |
| 7 | XSS — DOM Based | CWE-79 | A03 |
| 8 | SSRF | CWE-918 | A10 |
| 9 | Path Traversal | CWE-22 | A01 |
| 10 | Broken Authentication | CWE-287 | A07 |
| 11 | Broken Session Management | CWE-384 | A07 |
| 12 | Hardcoded Credentials | CWE-798 | A07 |
| 13 | Insecure Deserialization | CWE-502 | A08 |
| 14 | XXE | CWE-611 | A05 |
| 15 | CSRF | CWE-352 | A01 |
| 16 | IDOR | CWE-639 | A01 |
| 17 | Missing Access Control | CWE-862 | A01 |
| 18 | Privilege Escalation | CWE-269 | A01 |
| 19 | Sensitive Data Exposure | CWE-200 | A02 |
| 20 | Weak Cryptography | CWE-327 | A02 |
| 21 | Insecure TLS Config | CWE-295 | A02 |
| 22 | Security Misconfiguration | CWE-16 | A05 |
| 23 | Missing Security Headers | CWE-693 | A05 |
| 24 | Open Redirect | CWE-601 | A01 |
| 25 | Race Condition | CWE-362 | A04 |
| 26 | Integer Overflow | CWE-190 | A03 |
| 27 | Buffer Overflow | CWE-120 | A03 |
| 28 | Mass Assignment | CWE-915 | A04 |
| 29 | Regex DoS (ReDoS) | CWE-1333 | A03 |
| 30 | Template Injection (SSTI) | CWE-1336 | A03 |
| 31 | Prototype Pollution | CWE-1321 | A03 |
| 32 | Logging/Monitoring Gaps | CWE-778 | A09 |
| 33 | Insecure File Upload | CWE-434 | A04 |
| 34 | HTTP Request Smuggling | CWE-444 | A05 |

**For each cell (Vuln × Language × Tool), mark:** Detected / Not Detected / Not Applicable / Not Tested

---

### SHEET 4: TEST APP REGISTRY & LANGUAGE MAPPING

**Purpose:** Which test app you'll use for which language, and what's seeded in it.

**Columns:**

| # | Column | What to capture |
|---|--------|----------------|
| 1 | Test App Name | e.g., OWASP Juice Shop |
| 2 | Type | Intentionally Vulnerable / Real App (with permission) |
| 3 | Primary Language | e.g., JavaScript/TypeScript |
| 4 | Framework | e.g., Express.js + Angular |
| 5 | Database | e.g., SQLite |
| 6 | API Type | REST / GraphQL / gRPC / WebSocket |
| 7 | Auth Mechanism | JWT / Session / OAuth |
| 8 | Known Vuln Count | Number of seeded/known vulnerabilities |
| 9 | OWASP Categories Covered | Which of A01-A10 are present |
| 10 | Architecture Docs Available | Yes/No |
| 11 | API Spec Available (OpenAPI/Swagger) | Yes/No |
| 12 | Used For (SAST/DAST/Pentest/SCA/All) | Which test phases |
| 13 | Git Repo URL | Link |
| 14 | Deployment Status | Not Started / In Progress / Ready |
| 15 | Notes | Gaps, setup issues, etc. |

**Recommended test apps:**
- **Python:** Pygoat (Django), crAPI (Flask + microservice)
- **JavaScript/Node:** Juice Shop (Express), NodeGoat (Express)
- **Java:** WebGoat (Spring Boot)
- **Go:** crAPI (Go microservice)
- **PHP:** DVWA (custom PHP)
- **Ruby:** RailsGoat (Rails)
- **IaC:** Terragoat (Terraform), Kubernetes Goat
- **C#/.NET, Kotlin, Rust:** You'll need to build or find custom seed apps (this is a gap — document it)

---

### SHEET 5: EXECUTION RESULTS (The core data — one row per finding)

**Purpose:** Every single finding from every tool goes here. This is your raw data.

**Columns:**

| # | Column | What to capture |
|---|--------|----------------|
| 1 | Test Run ID | Unique identifier (e.g., "AWS-SA-SAST-Python-001") |
| 2 | Tool | AWS Security Agent / Snyk / Semgrep / ZAP / Burp / Manual |
| 3 | Capability Tested | SAST / SCA / DAST / Pentest / Design Review / IaC |
| 4 | Test App | e.g., Juice Shop |
| 5 | Language | e.g., JavaScript |
| 6 | Framework | e.g., Express.js |
| 7 | Scan Start Time | Timestamp |
| 8 | Scan End Time | Timestamp |
| 9 | Duration (mins) | Calculated |
| 10 | Finding ID | Tool's own ID |
| 11 | Finding Title | e.g., "SQL Injection in search endpoint" |
| 12 | Finding Description | Full description |
| 13 | CWE ID | e.g., CWE-89 |
| 14 | OWASP Category | e.g., A03 Injection |
| 15 | Severity | Critical / High / Medium / Low / Info |
| 16 | CVSS Score | 0.0 — 10.0 |
| 17 | Affected File/URL | File path (SAST) or endpoint URL (DAST/Pentest) |
| 18 | Line Number | For SAST findings |
| 19 | Evidence/PoC Provided | Yes / No |
| 20 | PoC Quality | Full Exploit / Partial / Screenshot Only / None |
| 21 | Fix Suggestion Provided | Yes / No |
| 22 | Fix Quality | Correct / Partial / Wrong / N/A |
| 23 | True Positive | Yes / No (verified manually) |
| 24 | False Positive | Yes / No |
| 25 | False Positive Reason | If FP — why? |
| 26 | Matched to Known/Seeded Vuln | Seeded Vuln ID or "New Discovery" |
| 27 | Attack Chain Part | Yes / No |
| 28 | Attack Chain ID | If part of a chain, which one |
| 29 | Also Found By (other tools) | List tool names |
| 30 | Unique to This Tool | Yes / No |
| 31 | Time to Find (mins from scan start) | For coverage-over-time curve |
| 32 | Notes | — |

---

### SHEET 6: SUMMARY METRICS (Calculated from Sheet 5)

**Purpose:** The aggregated numbers that go into your paper charts and tables.

**Section A — Per Tool, Per Language:**

| # | Metric | Formula |
|---|--------|---------|
| 1 | Total Findings | Count from Sheet 5 |
| 2 | True Positives (TP) | Count where True Positive = Yes |
| 3 | False Positives (FP) | Count where False Positive = Yes |
| 4 | False Negatives (FN) | Known vulns NOT found by this tool |
| 5 | Precision (%) | TP / (TP + FP) × 100 |
| 6 | Recall / Detection Rate (%) | TP / (TP + FN) × 100 |
| 7 | F1 Score | 2 × (Precision × Recall) / (Precision + Recall) |
| 8 | Scan Duration (mins) | From Sheet 5 |
| 9 | Time to First Finding (mins) | Earliest finding timestamp |
| 10 | OWASP A01-A10 Coverage | % of each category's known vulns detected |
| 11 | Critical/High Detection Rate (%) | Critical+High TP / Total Critical+High known |
| 12 | Unique Findings Count | Findings only this tool found |
| 13 | Attack Chains Detected | Count |

**Section B — Cost Metrics (Per Tool):**

| # | Metric | What to capture |
|---|--------|----------------|
| 1 | Tool License Cost ($/yr) | From pricing research |
| 2 | AWS Compute Cost for This Test ($) | From AWS billing |
| 3 | Human Hours (setup + triage + review) | Time-tracked |
| 4 | Human Cost ($) | Hours × rate |
| 5 | Total Cost ($) | License + Compute + Human |
| 6 | Cost Per Finding ($) | Total Cost / Total TP |
| 7 | Cost Per Critical Finding ($) | Total Cost / Critical TP |
| 8 | ROI vs Manual Pentest (%) | (Manual Cost - Tool Cost) / Manual Cost × 100 |

**Section C — Coverage Over Time (for the curve chart):**

| # | Metric | What to capture |
|---|--------|----------------|
| 1 | Tool Name | — |
| 2 | Time Elapsed (mins) | 5, 10, 15, 30, 60, 120, 240, 480, Final |
| 3 | Cumulative Findings at This Time | Count |
| 4 | Cumulative Critical+High at This Time | Count |

*This gives you the coverage-vs-time curve — X axis = time, Y axis = findings, one line per tool.*

---

### SHEET 7: MANUAL PENTEST BASELINE

**Purpose:** The human ground truth to compare everything against.

**Columns:**

| # | Column | What to capture |
|---|--------|----------------|
| 1 | Pentester Name/Team | — |
| 2 | Experience Level | Junior / Mid / Senior / Expert |
| 3 | Test App | — |
| 4 | Engagement Start Date | — |
| 5 | Engagement End Date | — |
| 6 | Total Hours Spent | — |
| 7 | Recon Hours | — |
| 8 | Active Testing Hours | — |
| 9 | Report Writing Hours | — |
| 10 | Hourly Rate ($) | — |
| 11 | Total Cost ($) | — |
| 12-32 | Same finding columns as Sheet 5 | (Finding ID through Notes) |
| 33 | Why Automation Missed This (if unique to manual) | Business logic / Social engineering context / Novel technique / Chained manual steps / Other |
| 34 | Could Automation Ever Catch This | Yes / Possibly / No |

---

### SHEET 8: FINAL COMPARISON MATRIX (The "money slide")

**Purpose:** The single table your manager and paper readers will look at first.

**Rows = Metrics. Columns = Tools + Manual.**

| Metric | AWS Security Agent | Snyk | Semgrep | SonarQube | Burp/ZAP | Manual Pentest | Winner |
|--------|-------------------|------|---------|-----------|----------|---------------|--------|
| **OBJ 1: COVERAGE** | | | | | | | |
| Total True Positives | | | | | | | |
| Detection Rate (%) | | | | | | | |
| Critical/High Detection (%) | | | | | | | |
| OWASP Top 10 Coverage (%) | | | | | | | |
| Languages Fully Supported | | | | | | | |
| Best Language (highest detection) | | | | | | | |
| Worst Language (lowest detection) | | | | | | | |
| Business Logic Vulns Found | | | | | | | |
| **OBJ 2: DIFFERENTIATION FROM MANUAL** | | | | | | | |
| Findings Manual Found, Tool Missed | | | | | | | |
| Findings Tool Found, Manual Missed | | | | | | | |
| Overlap (%) — found by both | | | | | | | |
| Categories Only Manual Catches | | | | | | | |
| Categories Only Tool Catches | | | | | | | |
| **OBJ 3: EFFICIENCY** | | | | | | | |
| Setup Time | | | | | | | |
| Time to First Finding | | | | | | | |
| Time to Full Report | | | | | | | |
| Total Cost ($) | | | | | | | |
| Cost Per Finding ($) | | | | | | | |
| Cost Per Critical Finding ($) | | | | | | | |
| ROI vs Manual (%) | | | | | | | |
| **OBJ 4: ACCURACY (TRUST)** | | | | | | | |
| Precision (%) | | | | | | | |
| Recall (%) | | | | | | | |
| F1 Score | | | | | | | |
| False Positive Rate (%) | | | | | | | |
| False Positive Count | | | | | | | |
| Signal-to-Noise Ratio (TP:FP) | | | | | | | |
| **OBJ 5: ACTIONABILITY** | | | | | | | |
| PoC/Evidence Quality (1-5) | | | | | | | |
| Fix Suggestion Provided (%) | | | | | | | |
| Fix Suggestion Accuracy (%) | | | | | | | |
| Remediation Guidance Completeness (1-5) | | | | | | | |
| Developer Can Act Without Security Team (%) | | | | | | | |
| **OBJ 6: CONTEXTUAL INTELLIGENCE** | | | | | | | |
| Attack Chains Detected | | | | | | | |
| Multi-Step Chains (3+ steps) | | | | | | | |
| Chain Severity Uplift (avg individual vs chain CVSS) | | | | | | | |
| Findings Missed by Siloed Tools but Caught via Context | | | | | | | |
| Design-to-Code Traceability (findings linked to architecture) | | | | | | | |
| **OBJ 7: ADOPTION FRICTION** | | | | | | | |
| Time from Zero to First Scan (mins) | | | | | | | |
| CI/CD Integration Time (mins) | | | | | | | |
| Documentation Quality (1-5) | | | | | | | |
| Learning Curve (1-5, 1=easy) | | | | | | | |
| Config Complexity (lines of config / steps required) | | | | | | | |
| Developer Workflow Disruption (1-5, 1=minimal) | | | | | | | |

---

## EXECUTION ORDER

```
WEEK 1-2 ──→ Fill Sheet 1 (Feature Matrix) + Sheet 2 (Language Depth)
              Pure desk research from docs. No tools running yet.

WEEK 2-3 ──→ Fill Sheet 3 (Vuln Coverage Matrix) from documentation
              Fill Sheet 4 (Test App Registry) — decide apps, start deploying

WEEK 4-6 ──→ Run AWS Security Agent on all test apps
              Fill Sheet 5 (Execution Results) — one row per finding
              Log timestamps for Sheet 6C (Coverage Over Time)

WEEK 6-7 ──→ Run competitor tools (Snyk, Semgrep, ZAP/Burp)
              Same Sheet 5 — append rows with different tool names

WEEK 7-9 ──→ Run manual pentest baseline
              Fill Sheet 7

WEEK 9-10 ──→ Calculate Sheet 6 (Summary Metrics)
               Build Sheet 8 (Final Comparison)

WEEK 10-11 ──→ Write the paper using Sheet 8 as your core data
```

---

## KEY PRINCIPLE

Every cell in Sheet 8 (Final Comparison) must be traceable back to raw data in Sheet 5 (Execution Results). If you can't trace it, it's opinion, not benchmark data. That traceability is what separates a research paper from a marketing brochure.
