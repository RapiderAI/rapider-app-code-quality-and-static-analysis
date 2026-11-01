<!-- Rapider Official App SOW & Specification | App #107: Code Quality & Static Analysis (code-quality-and-static-analysis) | Domain: DEV -->

# #107 Code Quality & Static Analysis (`code-quality-and-static-analysis`) — Scope of Work (SOW)

- **App Number & Name:** `#107 Code Quality & Static Analysis`
- **Proposed App Key:** `code-quality-and-static-analysis`
- **Domain / Suite & Model Prefix:** `DEV` (`Dev*`) — Category `11. Software Development & DevOps`
- **Representative Benchmark (`P1`):** `SonarCloud` (`SonarQube Cloud`)
- **Combined Feature Catalog:** [../combined-features/107-code-quality-and-static-analysis-features.md](../combined-features/107-code-quality-and-static-analysis-features.md)

---

## 1. Executive Outcome & Target Audience

**Code Quality & Static Analysis (`code-quality-and-static-analysis`)** serves as the automated "Clean as You Code" and AI Code Assurance control plane for engineering, AppSec, and platform teams across the Rapider `DEV` suite. As teams merge increasing volumes of human- and AI-authored pull requests, `#107` continuously inspects every commit and branch for SAST security taint vulnerabilities, hardcoded secrets, reliability bugs, maintainability code smells, code duplication, cognitive complexity, and New-Code unit test coverage—enforcing deterministic PR Quality Gates before technical debt or security flaws ever reach production.

- **SME & Startup Fast-Path:** An engineering team registers a `DevAnalyzedRepo` in `repo-drawer`, attaches the Built-in `Clean as You Code` Quality Gate (`0` new criticals, `>= 80%` new coverage, `<= 3%` new duplication), and uploads SARIF + LCOV reports from CI—getting instant PR pass/fail checks, redacted secret leak alerts, and 1-click `ApmIssue` bug creation with zero custom rule authoring.
- **Enterprise Progressive Disclosure:** Multi-squad and regulated enterprises unlock language-specific `DevRuleProfile` governance, custom declarative `DevStaticRule` AST patterns, dedicated `DevSecurityHotspot` human security review queues, OWASP Top 10 / CWE Top 25 / SOC2 compliance matrices, and time-bounded 4-eyes `DevFindingExemption` waivers routed via shared Rapider Home `WorkItem`s.
- **Measurable Business & Engineering Outcomes:**
  1. Block **95%+ of newly introduced SAST vulnerabilities and hardcoded secrets** at the Pull Request stage before merge (`0` production remediation cost vs. 10x–30x post-release cost).
  2. Sustain **80%+ unit test line coverage on all newly modified code** without freezing teams over legacy historical debt ("Clean as You Code" delta focus).
  3. Reduce AppSec & PR review bottlenecks by **50%** via taint-flow visualization, Security Hotspot triage, and grounded AI CodeFix patch proposals.
- **Top 6 Global Benchmarks Synthesized (`P1`–`P6`):** `SonarCloud / SonarQube Cloud` (`P1` — Representative Product), `Snyk Code` (`P2`), `Semgrep Code & Secrets` (`P3`), `Codacy` (`P4`), `Microsoft / GitHub Advanced Security (CodeQL)` (`P5`), and `SAP ABAP Test Cockpit (ATC) & Cloud ALM` (`P6`).

---

## 2. In-Scope, Out-of-Scope & Suite Ownership Boundaries

### In-Scope
- Registering `DevAnalyzedRepo` projects, New-Code baselines, `DevRuleProfile` rule sets, custom `DevStaticRule` patterns, and scoped CI scanner tokens (`CQS-001`, `CQS-005`, `CQS-023`).
- Ingesting SARIF v2.1.0 static scans (SAST, reliability bugs, smells, SCA, IaC misconfigurations) and LCOV/JaCoCo/Cobertura line & branch coverage deltas (`Decimal128`), computing duplication % and `A`–`E` ratings (`CQS-002`–`CQS-004`, `CQS-015`, `CQS-021`, `CQS-022`).
- Detecting source-to-sink taint vulnerabilities, redacted `SECRET_LEAK` credentials (with mandatory rotation escalations), and `DevSecurityHotspot` review items mapped to OWASP/CWE (`CQS-006`–`CQS-010`, `CQS-020`).
- Evaluating `DevCodeQualityGate` PR/branch conditions, PR decoration summaries, time-bounded 4-eyes `DevFindingExemption` waivers via Home `WorkItem`s, `ApmIssue` backlog promotion, and grounded AI CodeFix diffs (`CQS-011`–`CQS-014`, `CQS-016`–`CQS-019`, `CQS-024`–`CQS-028`).

### Out-of-Scope
- Live browser/mobile E2E test execution, Percy visual screenshot diffing, and runtime DOM accessibility scanning (owned by `#106 Automated Software Testing`).
- Production runtime unhandled crash ingestion and live user session replay (owned by `#104 Application Error Tracking`).
- Hosting Git repositories or running general-purpose CI/CD container build runners (owned by `#099` / `#100` Source Control & CI/CD).
- Executing live cloud Terraform `plan`/`apply` state mutations (owned by `#110 Infrastructure as Code Management`; `#107` performs static HCL/YAML linting only).

### Cross-Suite Ownership & Integration Contract

| Domain / App | Owns (Canonical System of Record) | Integration Contract with `#107` (`code-quality-and-static-analysis`) |
| :--- | :--- | :--- |
| **`#107` (`code-quality-and-static-analysis`)** | `DevAnalyzedRepo`, `DevCodeAnalysisRun`, `DevCodeFinding`, `DevSecurityHotspot`, `DevCodeQualityGate`, `DevRuleProfile`, `DevStaticRule`, `DevFindingExemption` | Evaluates static quality/security gates and publishes `dev.code_quality.gate_evaluated.v1` and `dev.code_quality.secret_detected.v1`. |
| **`APM` (`planning` / `apm`)** | `ApmProject`, `ApmEpic`, `ApmIssue` | `#107` links `DevCodeFinding.linkedApmIssueId` to canonical `ApmIssue` for vulnerability remediation, secret rotation, and debt refactoring. |
| **`#104` & `#106` (`DEV` Quality Peers)** | `DevErrorIssue` (`#104`), `DevTestRun` (`#106`) | `#107` correlates high-complexity/low-coverage files with `#104` crash frequency and `#106` dynamic E2E failure hotspots (`CQS-019`). |
| **`#110` (`infrastructure-as-code-management`)** | `DevIacWorkspace`, `DevIacModule` | Static HCL/Terraform misconfiguration findings in `#107` link directly to registered `#110` modules prior to `plan`/`apply`. |
| **Platform Core Services** | Identity/RBAC, Secret Manager, Files/Drive, Notebooks, Home `WorkItem`s, `projectChannelMessage` | Raw SARIF/LCOV artifacts store in Platform Files; `CRITICAL` waivers and `SECRET_LEAK` alerts emit Home `WorkItem`s; AI CodeFix runs on `projectChannelMessage`. |

---

## 3. Primary Web Pages & Sidebar Navigation Architecture (12 Pages)

Every visible sidebar section strictly enforces the **Minimum 3 Items Rule** (`Portfolio & Findings` = 3 items, `Security & Debt` = 3 items, `Quality Governance` = 3 items; detail and drawer routes set `displayOnMenu: false`).

| # | Route | Page Title | Sidebar Section | Menu Visible | Key Components & UX Standards |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `dashboard` | Code Health & Assurance Overview | `Portfolio & Findings` | `true` (Order 1) | KPI cards (`countSWR`/`findSWR`) for Portfolio Gate Pass %, Open Critical Vulnerabilities, Unreviewed Hotspots, Avg New-Code Coverage %, and AI Code Assurance status. |
| 2 | `repositories` | Analyzed Repositories | `Portfolio & Findings` | `true` (Order 2) | `DevAnalyzedRepo` catalog displaying `A`–`E` Security/Reliability/Maintainability badges, New Coverage %, Duplication %, Gate status, and clickable repo name (`repo-detail`). |
| 3 | `findings` | Static Findings & SAST Explorer | `Portfolio & Findings` | `true` (Order 3) | Dual Table + `<rapider-kanban>` Triage Board (`OPEN`, `CONFIRMED`, `ACCEPTED_WAIVER`, `FALSE_POSITIVE`, `FIXED`); `#activeFilterTagsBar` with `Clear all`; New-Code toggle; clickable finding title (`finding-detail`). |
| 4 | `security-hotspots` | Security Hotspots & Secrets | `Security & Debt` | `true` (Order 4) | Dedicated AppSec queue (`TO_REVIEW`, `SAFE`, `FIXED`, `ACKNOWLEDGED_RISK`) + high-priority redacted `SECRET_LEAK` rotation tracker with CWE/OWASP pills. |
| 5 | `scans` | PR & Branch Analysis Runs | `Security & Debt` | `true` (Order 5) | Chronological `DevCodeAnalysisRun` log showing PR/branch ref, commit SHA, `PASSED`/`FAILED` gate badge, New-Code metric deltas, and AI-authored commit flag. |
| 6 | `compliance-debt` | OWASP Posture & Debt Analytics | `Security & Debt` | `true` (Order 6) | OWASP Top 10 & CWE Top 25 compliance matrix, high-complexity/low-coverage risk quadrant (with `#104` crash overlay), and Save-to-Notebook export. |
| 7 | `quality-gates` | Clean-Code Quality Gates | `Quality Governance` | `true` (Order 7) | `DevCodeQualityGate` manager configuring `Decimal128` New-Code coverage, duplication, rating, and hotspot conditions with `Edit` (icon + text) and `Delete` (icon-only). |
| 8 | `rule-profiles` | Rule Profiles & Custom Rules | `Quality Governance` | `true` (Order 8) | Language `DevRuleProfile` catalog and custom AST/pattern `DevStaticRule` builder with positive/negative test snippet validator. |
| 9 | `exemptions` | Waivers & Risk Exemptions | `Quality Governance` | `true` (Order 9) | 4-eyes `DevFindingExemption` queue (`PENDING_APPROVAL`, `ACTIVE_WAIVER`, `EXPIRED`, `REJECTED`) synced with Rapider Home `WorkItem`s and TTL expiry countdowns. |
| 10 | `finding-detail` | Finding Triage & Taint Flow | *(Hidden)* | `false` | Annotated source snippet (escaped), multi-file source-to-sink taint step trace, CWE rule remediation guide, `ApmIssue` linker, waiver requester, and AI CodeFix (`projectChannelMessage`). |
| 11 | `repo-detail` | Repository Quality Scorecard | *(Hidden)* | `false` | Per-repo New Code vs. Overall Code split panel, uncovered file tree, clone block browser, branch/PR history, and embeddable SVG badge generator. |
| 12 | `repo-drawer` | Onboard / Edit Repository | *(Hidden)* | `false` | Sliding form drawer for `DevAnalyzedRepo` onboarding, New-Code baseline horizon, Gate & Rule Profile bindings; enforces `try/catch/finally`, SWR invalidation, and auto-close. |

**Mandatory Rapider UI Compliance across all 12 Pages:**
- Initial data queries exclusively call `window.rapiderApi.findSWR` and `countSWR` with zero redundant `isDeleted` filter clauses; local arrays filter `item.isDeleted !== true` and update optimistically on triage/waiver/edit/delete.
- Tables never render a standalone "View" button in `Actions`; primary identifiers (`repoName`, `findingKey`, `gateName`, `exemptionTitle`) navigate to detail views; `Edit` renders icon + text and `Delete` renders icon-only with `aria-label="Delete"`.
- Primary and danger confirmation buttons enforce `#ffffff !important` text contrast; native `alert`/`confirm`/`prompt` dialogs are strictly banned.

---

## 4. Canonical Data Models (`Dev*` — 8 Models)

All models omit `projectId`, use backend-generated UUIDs (`00000000-xxxx-xxxx-xxxx-xxxxxxxxxxxx` in deterministic fixtures), enforce optimistic `version` checks, and store exact ratios/thresholds as `Decimal128`.

| Model Name | Key Fields & Types | Relationships & External Refs | Invariants & Lifecycle |
| :--- | :--- | :--- | :--- |
| **`DevAnalyzedRepo`** | `id` (UUID), `name` (String), `slug` (String), `gitRepoRef` (String), `defaultBranch` (String), `newCodeHorizonType` (`PREVIOUS_VERSION` \| `DAYS_WINDOW` \| `BASE_BRANCH`), `newCodeHorizonValue` (String), `qualityGateId` (UUID), `ruleProfileIds` (UUID[]), `securityRating` (`A`..`E`), `reliabilityRating` (`A`..`E`), `maintainabilityRating` (`A`..`E`), `overallCoveragePercent` (`Decimal128`), `duplicationPercent` (`Decimal128`), `debtMinutes` (Long), `lastGateStatus` (`PASSED` \| `FAILED` \| `NONE`), `version` (Integer) | Refs `DevCodeQualityGate`, `DevRuleProfile[]`, optional `linkedApmProjectId` (`ApmProject`) | `slug` unique per workspace; scanner token stored hashed; ratings deterministically derived from open non-waived findings (`A` = 0 bugs/vulns). |
| **`DevCodeAnalysisRun`** | `id` (UUID), `runKey` (String), `repoId` (UUID), `scanTargetType` (`MAIN_BRANCH` \| `BRANCH` \| `PULL_REQUEST`), `branchName` (String), `pullRequestNumber` (String?), `commitSha` (String), `isAiAssistedCommit` (Boolean), `newLinesCount` (Integer), `newCoveragePercent` (`Decimal128`), `newDuplicationPercent` (`Decimal128`), `newBlockerCriticalCount` (Integer), `hotspotsReviewedPercent` (`Decimal128`), `gateStatus` (`PASSED` \| `FAILED`), `sarifFileId` (UUID?), `lcovFileId` (UUID?), `analyzedAt` (DateTime), `version` (Integer) | Belongs to `DevAnalyzedRepo`; `sarifFileId`/`lcovFileId` ref Platform Files/Drive | **Immutable scan snapshot** once `gateStatus` is computed; duplicate `(repoId, commitSha, scanTargetType)` with same `idempotencyKey` returns existing run. |
| **`DevCodeFinding`** | `id` (UUID), `findingKey` (String), `repoId` (UUID), `firstSeenRunId` (UUID), `lastSeenRunId` (UUID), `ruleId` (UUID), `softwareQuality` (`SECURITY` \| `RELIABILITY` \| `MAINTAINABILITY`), `category` (`SAST_VULNERABILITY` \| `SECRET_LEAK` \| `BUG` \| `CODE_SMELL` \| `SCA_DEPENDENCY` \| `IAC_MISCONFIG`), `severity` (`BLOCKER` \| `CRITICAL` \| `MAJOR` \| `MINOR` \| `INFO`), `cweIds` (String[]), `owaspTags` (String[]), `filePath` (String), `startLine` (Integer), `endLine` (Integer), `astFingerprint` (String), `redactedSnippet` (String), `taintFlowSteps` (JSON[]), `effortMinutes` (Integer), `isOnNewCode` (Boolean), `status` (`OPEN` \| `CONFIRMED` \| `ACCEPTED_WAIVER` \| `FALSE_POSITIVE` \| `FIXED`), `version` (Integer) | Belongs to `DevAnalyzedRepo` & `DevStaticRule`; optional `linkedApmIssueId` (`ApmIssue`), `activeExemptionId` (`DevFindingExemption`), `threadChannelId` (`projectChannelMessage`) | For `category = SECRET_LEAK`, `redactedSnippet` MUST mask middle/secret characters prior to persistence; `BLOCKER`/`CRITICAL` security findings cannot transition to `ACCEPTED_WAIVER` or `FALSE_POSITIVE` without an `ACTIVE_WAIVER` `DevFindingExemption`. |
| **`DevSecurityHotspot`** | `id` (UUID), `repoId` (UUID), `ruleCode` (String), `riskProbability` (`HIGH` \| `MEDIUM` \| `LOW`), `owaspCategory` (String), `filePath` (String), `lineNumber` (Integer), `codeExcerpt` (String), `reviewStatus` (`TO_REVIEW` \| `SAFE` \| `FIXED` \| `ACKNOWLEDGED_RISK`), `reviewerUserId` (UUID?), `reviewComment` (String?), `reviewedAt` (DateTime?), `version` (Integer) | Belongs to `DevAnalyzedRepo`; `reviewerUserId` refs Platform Identity | Requires explicit `reviewComment` when marking `SAFE` or `ACKNOWLEDGED_RISK`; `hotspotsReviewedPercent` on `DevCodeAnalysisRun` reflects `(reviewed / total) * 100` in `Decimal128`. |
| **`DevCodeQualityGate`** | `id` (UUID), `name` (String), `isBuiltInCleanCode` (Boolean), `minNewCoveragePercent` (`Decimal128`), `maxNewDuplicationPercent` (`Decimal128`), `maxNewBlockerCriticalCount` (Integer), `minHotspotsReviewedPercent` (`Decimal128`), `enforceAiCodeAssurance` (Boolean), `version` (Integer) | Referenced by `DevAnalyzedRepo` | Cannot delete a gate referenced by `>= 1` active `DevAnalyzedRepo`; `Decimal128` percentages validated within `[0.0000, 100.0000]`. |
| **`DevRuleProfile`** | `id` (UUID), `name` (String), `language` (`TYPESCRIPT` \| `PYTHON` \| `JAVA` \| `CSHARP` \| `GO` \| `HCL_TERRAFORM` \| `SQL` \| `HTML_CSS`), `activeRuleIds` (UUID[]), `severityOverrides` (JSON), `isDefault` (Boolean), `version` (Integer) | Referenced by `DevAnalyzedRepo`; contains `DevStaticRule` refs | Unique `(name, language)` per workspace. |
| **`DevStaticRule`** | `id` (UUID), `ruleCode` (String, e.g., `S3649` or `CUSTOM-NO-ALERT`), `title` (String), `language` (String), `softwareQuality` (`SECURITY` \| `RELIABILITY` \| `MAINTAINABILITY`), `defaultSeverity` (String), `patternSpec` (String?), `cweIds` (String[]), `remediationMarkdown` (String), `isCustom` (Boolean), `isActive` (Boolean), `version` (Integer) | Referenced by `DevRuleProfile` and `DevCodeFinding` | Custom rules require `>= 1` passing positive & negative validation test case before `isActive = true`. |
| **`DevFindingExemption`** | `id` (UUID), `title` (String), `findingId` (UUID), `exemptionType` (`ACCEPTED_RISK` \| `FALSE_POSITIVE`), `requestedByUserId` (UUID), `justification` (String), `expiresAt` (DateTime?), `status` (`PENDING_APPROVAL` \| `ACTIVE_WAIVER` \| `EXPIRED` \| `REJECTED`), `approvedByUserId` (UUID?), `homeWorkItemId` (UUID?), `version` (Integer) | Belongs to `DevCodeFinding`; `homeWorkItemId` refs Platform Home `WorkItem` | 4-eyes enforcement (`requestedByUserId != approvedByUserId`); `ACCEPTED_RISK` requires a bounded `expiresAt` (`<= 180` days); expiry automatically reverts `DevCodeFinding.status -> OPEN`. |

---

## 5. Core End-to-End User Journeys

1. **SME PR Scan -> Quality Gate Block -> AI CodeFix -> Clean Re-Scan:**
   - Developer opens PR `#88` adding an SQL query helper without unit tests (`New Coverage = 54.00% < 80.00%`, plus 1 `CRITICAL` SQL-injection taint finding `S3649`).
   - CI calls `ingestAnalysisRun`, marking `DevCodeAnalysisRun.gateStatus = FAILED`. Developer clicks from `#/scans` into `#/finding-detail`, views the 4-step HTTP-to-SQL taint trace, clicks **Generate AI CodeFix**, reviews the parameterized query diff posted on `projectChannelMessage`, commits the fix + unit tests, and the next CI scan passes (`PASSED`, `New Coverage = 91.50%`).
2. **Hardcoded Secret Leak Detection & Immediate Rotation Escalation:**
   - A branch scan detects an accidentally committed Stripe/API key (`SECRET_LEAK`). `ingestAnalysisRun` redacts the snippet (`sk_live_****9a2f`) before DB write, fails the PR Quality Gate, emits `dev.code_quality.secret_detected.v1`, and creates an urgent Rapider Home `WorkItem` + linked `ApmIssue` instructing key revocation even if the line is later deleted.
3. **Time-Bounded 4-Eyes Risk Waiver via Home `WorkItem`:**
   - An engineer flags a `CRITICAL` legacy third-party crypto rule in an isolated test harness as `ACCEPTED_RISK` (60-day TTL) via `#/finding-detail`.
   - `requestFindingExemption` creates `DevFindingExemption` (`PENDING_APPROVAL`) and routes a Home `WorkItem` to the AppSec Lead. AppSec Lead inspects the code context on `#/exemptions`, approves the 60-day waiver (`ACTIVE_WAIVER`), unblocking the release while scheduling automatic re-open on `expiresAt`.
4. **Custom Rapider Architecture Rule Authoring:**
   - Platform Lead opens `#/rule-profiles`, creates custom rule `CUSTOM-NO-NATIVE-DIALOG` banning `window.alert(` / `window.confirm(`, validates positive/negative JS snippets, activates it in the `Frontend UI Standard` profile, and enforces it across all microapp repositories.
5. **Multi-Facet Filtering, Click-Through & Back Restoration:**
   - On `#/findings`, user toggles `New Code Only: true`, selects `Quality: SECURITY` + `Severity: CRITICAL`, and searches `"sql"`. `#activeFilterTagsBar` renders dismissible chips and `Clear all`.
   - Clicking `S3649: SQL Injection in orderRepo.ts` transitions cleanly to `#/finding-detail?id=...`; clicking `#btnGoBack` restores `#/findings` with all filter chips intact.

---

## 6. Consolidated Feature Priorities & Work Packages

### `P0` Foundation (MVP Release-Ready Core)
- **WP-P0-1: Repository Onboarding, SARIF/LCOV Ingestion & Ratings (`CQS-001`–`CQS-004`, `CQS-015`):** `DevAnalyzedRepo`, `DevCodeAnalysisRun` schemas, `Decimal128` coverage/duplication parsers, `A`–`E` SQALE calculators, `#/dashboard`, `#/repositories`, `repo-drawer`, `#/repo-detail`, `#/scans`.
- **WP-P0-2: SAST Taint Findings, Redacted Secrets & Security Hotspots (`CQS-006`–`CQS-008`, `CQS-017`):** `DevCodeFinding` & `DevSecurityHotspot` engines, mandatory secret redaction, `<rapider-kanban>` triage boards, `#activeFilterTagsBar`, `#/findings`, `#/finding-detail`, `#/security-hotspots`.
- **WP-P0-3: "Clean as You Code" Gates, PR Decoration & 4-Eyes Exemptions (`CQS-011`–`CQS-014`, `CQS-016`):** `DevCodeQualityGate` (`#/quality-gates`), auto-closure on AST fix, `DevFindingExemption` + Home `WorkItem` (`#/exemptions`), PR status payloads, and `ApmIssue` promotion.

### `P1` Enterprise AppSec & Cross-Suite Intelligence
- **WP-P1-1: Custom Rule Profiles, OWASP Compliance & AI Code Assurance (`CQS-005`, `CQS-009`, `CQS-010`):** `DevRuleProfile` & `DevStaticRule` editors (`#/rule-profiles`), OWASP/CWE posture matrices (`#/compliance-debt`), and strict AI-assisted PR gates.
- **WP-P1-2: Secret Incident Playbooks, SCA/IaC & Crash/Test Correlation (`CQS-018`–`CQS-022`):** `SECRET_LEAK` Home `WorkItem` rotation alerts, SARIF SCA/IaC ingestion (cross-linked to `#110`), and `#104` crash + `#106` test failure risk quadrant.

### `P2` Adjacent Capabilities & Grounded AI CodeFix
- **WP-P2-1: Architecture Import Boundaries, SVG Badges & MCP Feed (`CQS-023`–`CQS-025`):** Forbidden-import rules, workspace-scoped SVG quality badges, and IDE/MCP rule feed.
- **WP-P2-2: Grounded AI CodeFix, Sanitizer Triage & Rule Builder (`CQS-026`–`CQS-028`):** Context-aware diff proposals, hotspot sanitizer analysis, and plain-English-to-`DevStaticRule` drafts on `projectChannelMessage`.

---

## 7. Roles, Permissions & Field-Level Governance

| Role | Permitted Actions | Restricted / Field-Level Boundaries |
| :--- | :--- | :--- |
| **Developer** | View `DevAnalyzedRepo` metrics, `DevCodeFinding` taint traces, and uncovered lines; transition non-critical code smells (`CONFIRMED`); create linked `ApmIssue` tasks; submit `DevFindingExemption` requests; generate AI CodeFix diffs. | Cannot directly mark `BLOCKER`/`CRITICAL` security findings or `SECRET_LEAK` items as `FALSE_POSITIVE`/`ACCEPTED_WAIVER`; cannot edit `DevCodeQualityGate` thresholds. |
| **AppSec / Security Reviewer** | Review `DevSecurityHotspot` items (`SAFE`, `FIXED`, `ACKNOWLEDGED_RISK`); approve/reject 4-eyes `DevFindingExemption` waivers (`Home WorkItem`); author security `DevStaticRule` rules; audit OWASP/SOC2 posture. | Cannot self-approve own `DevFindingExemption` request; cannot unmask redacted secret values (never stored in plaintext). |
| **Engineering / Platform Lead** | Onboard/edit `DevAnalyzedRepo`, configure `DevCodeQualityGate` thresholds and `DevRuleProfile` assignments, manage scanner tokens, and export portfolio debt reports. | Cannot delete or alter sealed `DevCodeAnalysisRun` records or historical exemption audit trails. |
| **Read-Only Auditor** | Inspect `DevCodeQualityGate` configurations, `DevCodeAnalysisRun` pass/fail histories, OWASP compliance matrices, and `DevFindingExemption` approval chains. | Zero mutation access; source snippets restricted if repository source-visibility mask is enabled. |
| **CI Scanner Identity** | Write-only `ingestAnalysisRun` scoped strictly to its single `DevAnalyzedRepo` token. | Zero read/mutation access to waivers, gates, or other repositories. |

---

## 8. Technical APIs, Guarded Commands, Events & `requiredWorkflows`

### Guarded Domain Commands
All mutating commands validate RBAC, `idempotencyKey`, `correlationId`, and `expectedVersion`:
- `ingestAnalysisRun(repoToken, metadata, sarifFileId, lcovFileId?, idempotencyKey)` -> Scrubs secret snippets, matches AST fingerprints against existing `DevCodeFinding` rows (auto-closing fixed issues), computes `Decimal128` New-Code coverage/duplication, evaluates `DevCodeQualityGate`, and seals `DevCodeAnalysisRun`.
- `reviewSecurityHotspot(hotspotId, decision, reviewComment, expectedVersion, idempotencyKey)` -> Validates mandatory comment, updates `DevSecurityHotspot`, and recalculates `hotspotsReviewedPercent`.
- `requestFindingExemption(findingId, exemptionType, justification, expiresAt?, idempotencyKey)` -> Creates `DevFindingExemption` (`PENDING_APPROVAL`) and emits shared Home `WorkItem`.
- `decideFindingExemption(exemptionId, decision, reviewComment, expectedVersion, idempotencyKey)` -> Enforces `requestedByUserId != actorUserId` and bounded `expiresAt`, transitioning `DevCodeFinding` to `ACCEPTED_WAIVER` or `FALSE_POSITIVE`.
- `requestAiCodeFix(findingId, channelId, idempotencyKey)` -> Generates syntax-checked remediation diff on `projectChannelMessage`.

### Kafka Domain Events (Published & Consumed)
- **Published:** `dev.code_quality.run_completed.v1`, `dev.code_quality.gate_failed.v1`, `dev.code_quality.gate_passed.v1`, `dev.code_quality.secret_detected.v1`, `dev.code_quality.exemption_expired.v1`.
- **Consumed:** `apm.issue.status_changed.v1` (updates remediation tracking badge on `DevCodeFinding`), `dev.git.pr_opened.v1` (initializes pending PR quality gate check).

### `requiredWorkflows` in `app.manifest.json`
1. `dev-code-sarif-and-coverage-ingest-wf` (Parses SARIF v2.1.0 & LCOV bundles from Platform Files, redacts secrets, deduplicates AST hashes, and evaluates `DevCodeQualityGate`).
2. `dev-code-secret-leak-escalation-wf` (Immediately creates high-priority Home `WorkItem`s and security notifications upon any `SECRET_LEAK` detection).
3. `dev-code-exemption-expiry-watcher-wf` (Scheduled sweep transitioning expired `DevFindingExemption` waivers to `EXPIRED`, reopening `DevCodeFinding` to `OPEN`, and notifying owners).
4. `dev-code-ai-codefix-wf` (Grounded AI remediation diff & custom rule assistant on `projectChannelMessage`—strictly read-only against repositories, requiring human developer PR review).

---

## 9. Security, Privacy, Compliance & Non-Functional Requirements

- **Zero Secondary Secret Leakage (STRICT):** Whenever `CQS-007` detects a hardcoded token, password, or connection URI in scanned source code, the ingestion pipeline cryptographically hashes the token for deduplication and masks the middle characters (`sk_live_****9a2f`) *before* writing `DevCodeFinding` to the database, logs, or AI context—ensuring `#107` never stores plaintext leaked credentials (\$0 breach amplification risk).
- **XSS & Untrusted Code Snippet Sanitization:** Scanned source excerpts (`redactedSnippet`, `codeExcerpt`) frequently contain literal `<script>` payloads from XSS test fixtures or vulnerable templates; all code views render strictly inside escaped `<pre><code>` blocks (`escapeHtml()`).
- **SOC2 / ISO-27001 Auditability:** Every Quality Gate modification, Rule Profile change, Security Hotspot decision, and 4-eyes `DevFindingExemption` approval is immutably logged with actor, timestamp, and justification.
- **Accessibility & Responsive Parity:** WCAG 2.2 AA compliant across `390px`, `768px`, and `1440px` (`light`/`dark` themes); color-blind-safe `A`–`E` letter + shape badges (never color alone); `findSWR` cached views `< 150ms` p95.

---

## 10. Deterministic Acceptance Criteria

1. **Zero `projectId` & Platform UUIDs:** All 8 `Dev*` schemas contain zero `projectId` fields, generate backend UUIDs on creation, and use `00000000-xxxx-xxxx-xxxx-xxxxxxxxxxxx` in deterministic fixtures.
2. **Exact `Decimal128` "Clean as You Code" Gate Evaluation:** A PR scan with `newCoveragePercent = 79.9900%` against `minNewCoveragePercent = 80.0000%` deterministically evaluates `gateStatus = FAILED` without float rounding error; `80.0000%` with `0` new criticals evaluates `PASSED`.
3. **Pre-Persistence Secret Redaction & Escalation:** Ingesting a SARIF `SECRET_LEAK` finding masks the raw token in `DevCodeFinding.redactedSnippet`, fails the gate, and emits a Rapider Home `WorkItem`.
4. **AST Auto-Closure on Fix:** Ingesting a subsequent scan on the same branch where the offending AST fingerprint is absent automatically transitions `DevCodeFinding.status` from `OPEN` to `FIXED`.
5. **4-Eyes Waiver Lock & Automatic TTL Expiry:** Direct developer attempts to mark a `CRITICAL` `SAST_VULNERABILITY` as `FALSE_POSITIVE` fail with `403 EXEMPTION_APPROVAL_REQUIRED`; self-approval of `DevFindingExemption` fails; once `expiresAt` passes, the expiry workflow transitions `status -> EXPIRED` and reopens the finding.
6. **Bi-Directional `ApmIssue` Promotion:** Clicking **Create Remediation Issue** on `#/finding-detail` links a canonical `ApmIssue` without duplicating sprint task models.
7. **Sidebar Minimum 3 Items Rule:** All 3 visible sidebar sections (`Portfolio & Findings`, `Security & Debt`, `Quality Governance`) each contain 3 visible items (`displayOnMenu: true`), while `finding-detail`, `repo-detail`, and `repo-drawer` set `displayOnMenu: false`.
8. **SWR Clean Query & Optimistic Updates:** All pages load via `findSWR`/`countSWR` with zero `isDeleted` filter clauses; reviewing a hotspot, editing a gate, or deleting a custom draft rule updates local arrays and `<rapider-kanban>` optimistically, clears SWR cache, and rolls back on error.
9. **Table Actions, Contrast & Dialog Ban:** Zero tables render a "View" button in `Actions`; primary identifiers navigate to detail routes; `Edit` renders icon + text; `Delete` renders icon-only with `aria-label="Delete"`; primary/danger buttons enforce `#ffffff` text; zero `alert`/`confirm`/`prompt` calls exist.
10. **Active Filter Tags & Clear All:** Toggling `New Code Only` or filtering by severity/quality on `#/findings` renders `#activeFilterTagsBar` with HTML-escaped dismissible chips and `Clear all`, updating Table and `<rapider-kanban>` synchronously.
11. **Drawer Auto-Close & `finally` Reset:** Saving or cancelling `repo-drawer` closes the drawer, broadcasts `RECORD_CREATED`/`RECORD_UPDATED`, and resets Save button state inside `finally`.
12. **Click-Through Navigation & Back State Restoration:** Clicking a finding link on `#/findings` navigates to `#/finding-detail?id=...` without `<base href>` 404 diversion, renders taint steps, and `#btnGoBack` restores `#/findings` with active filters preserved.
13. **Grounded AI CodeFix Boundary:** Requesting AI CodeFix posts a syntax-escaped patch diff onto `projectChannelMessage` citing CWE rules and never pushes commits automatically.
14. **Theme & Viewport Compliance:** Automated light/dark `validate_theme` checks and `390px`/`768px`/`1440px` layout assertions pass cleanly.
