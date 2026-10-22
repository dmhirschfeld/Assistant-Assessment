# Requirements — Assistant-Assessment

## Last Updated: 2026-10-22

**Source:** `Assistant Assessment Platform_ Clickable Prototype.html` (repo root). The prototype is the spec: its screens show the product, and its **Developer notes** panel (toggle in the top bar) lists what must be built behind each screen. Where this doc and the prototype disagree, raise it — don't guess.

**Product:** an hour-long, job-realistic pre-hire test for executive and administrative assistants. Candidates work as an assistant to a busy owner ("Jane"): inbox, calendar, receipts, emails and judgment calls. Employers get a scored report with red flags to discuss in interviews. Working name: **GSD Queen Assessments**.

**Purpose: a SaaS product** (software sold by subscription, many employer companies on one shared system) for job-realistic pre-hire assessments. GSD Queen is the first customer, not a separate internal tool — so multi-tenancy (each company's data walled off), accounts and security are built into the foundation from P1, even where their screens ship later.

**Priority = phase:**

| Priority | Phase | Scope |
|---|---|---|
| P1 | Phase 1 — GSD Queen as first tenant | GSD Queen uses the SaaS platform to replace its current off-the-shelf test. Built on the multi-tenant foundation; self-service sign-up and billing can wait. |
| P2 | Phase 2 — Sell to employers | Other businesses get their own accounts, dashboards and billing. Accounts, billing and security matter most here. |
| P3 | Phase 3 — Dental roles | Role-specific assessments for dental front office and clinical-knowledge roles. |

## The Assessment (Executive & Administrative Assistant)

8 timed sections, 55 timed minutes, about an hour in total.

| # | Section | Measures | Time | Red flags possible |
|---|---|---|---|---|
| 1 | Morning Inbox | Prioritizing and judgment (drag-to-rank + choose an action per item) | 12 min | Yes |
| 2 | Scheduling | Calendar logic and attention to detail | 6 min | No |
| 3 | Judgment | Workplace judgment and discretion | 7 min | Yes |
| 4 | Budget Check | Accuracy and practical math (flag lines in a table) | 7 min | No |
| 5 | Email | Professional communication (best response) | 7 min | Yes |
| 6 | Math | Everyday office math (built-in calculator) | 6 min | No |
| 7 | English | Grammar, proofreading and reading | 7 min | No |
| 8 | Typing | Typing speed and accuracy | 3 min | No |

**Scoring rules (starting cutoffs — to be validated against GSD Queen's best placements):**

| Measure | Strong | Acceptable | Weak |
|---|---|---|---|
| Overall and per-section % | ≥ 80% | 65–79% | < 65% |
| Typing (adjusted WPM) | ≥ 40 | 35–39 | < 35 (below minimum) |

- **Adjusted WPM** = raw WPM minus uncorrected errors per minute; a "word" is 5 characters.
- Scenario spending authority: the assistant may spend up to **$500** without approval (per-employer setting later — REQ-043).
- GSD Queen's placement data: typing speed was the clearest predictor of hiring; hire rates peaked at 18% for 40–49 adjusted WPM.

## Functional Requirements

| ID | Requirement | Priority | Status | Tests |
|----|-------------|----------|--------|-------|
| **Candidate experience** |||||
| REQ-001 | Candidate signs in with first name, last name and email via their private invite link. | P1 | not started | — |
| REQ-002 | Candidate completes the 8 sections in order; can't go back to a finished section; short breaks allowed between sections. | P1 | not started | — |
| REQ-003 | Each section's timer starts only when the candidate clicks Start inside it; section auto-submits when time runs out. | P1 | not started | — |
| REQ-004 | Resume after an accidental refresh without restarting the current section's timer. | P1 | not started | — |
| REQ-005 | Support item types: drag-to-rank, single choice, best response, calendar placement, flag lines in a table, numeric entry with tolerance, click-to-mark proofreading, timed typing with adjusted WPM. | P1 | not started | — |
| REQ-006 | Built-in calculator in the Math section. | P1 | not started | — |
| REQ-007 | Candidate report: scores and explanations, **without** red flags, ratings or timing. Showing correct answers is a per-employer setting (showing them can leak the answer key). | P1 | not started | — |
| REQ-008 | Privacy and consent notice before starting; keyboard required for typing. | P1 | not started | — |
| REQ-009 | Accommodations such as extra time. | P2 | not started | — |
| **Employer: invitations** |||||
| REQ-010 | Invite a candidate: first name, last name, email, assessment, optional "Placing for" (client business). | P1 | not started | — |
| REQ-011 | Invite email contains a unique, tokenized, single-use link; one attempt per link. | P1 | not started | — |
| REQ-012 | Links expire after a set time (e.g. 7 days); invites can be resent or cancelled. | P1 | not started | — |
| **Employer: candidates dashboard** |||||
| REQ-020 | List candidates with status: Invited, In progress (with current section), Completed, Expired. | P1 | not started | — |
| REQ-021 | Summary stats: completed count, average score, in progress, waiting to start. | P1 | not started | — |
| REQ-022 | Filter by status; sort by most recent, highest score, most red flags; search by name or client. | P1 | not started | — |
| REQ-023 | "Placing for" tags each candidate to a client business. | P1 | not started | — |
| REQ-024 | Export to CSV; optional Google Sheets sync. | P1 | not started | — |
| **Employer: candidate report** |||||
| REQ-030 | Summary first: overall %, rating, typing WPM, red flag count, section table (score, rating, time used). | P1 | not started | — |
| REQ-031 | Red flag breakdown: situation, answer selected, why it may matter, stronger choice — framed as interview talking points. | P1 | not started | — |
| REQ-032 | Per-section detail: short intro on what it measures, then every answer with points and explanation. | P1 | not started | — |
| REQ-033 | Download report as PDF. | P1 | not started | — |
| REQ-034 | Share a read-only report link with the client. | P1 | not started | — |
| REQ-035 | Record hiring outcome (Hired / Not hired / Still deciding). | P1 | not started | — |
| REQ-036 | Later record 90-day retention and a performance rating; use outcomes to show which scores predict good hires and adjust cutoffs. | P2 | not started | — |
| REQ-037 | Email notifications (e.g. candidate completed). | P1 | not started | — |
| **Assessment library and authoring** |||||
| REQ-040 | Content model: Assessment → Sections → Items. Each item has type, content, answer key, point values, explanations and optional red flag text. | P1 | not started | — |
| REQ-041 | Version every assessment so old reports match the questions candidates actually saw. | P1 | not started | — |
| REQ-042 | Admin tool for GSD Queen to add/edit items and adjust timers and cutoffs without a developer. | P2 | not started | — |
| REQ-043 | Per-employer settings: spending limits in scenarios, which sections to include, cutoffs. | P1 (model) / P2 (screens) | not started | — |
| REQ-044 | Randomize question and answer order. | P1 | not started | — |
| REQ-045 | Multiple versions of each item so answers can't be shared. | P2 | not started | — |
| **Accounts and billing** |||||
| REQ-050 | Employer accounts and logins; each organization sees only its own candidates (multi-tenant). | P1 | not started | — |
| REQ-051 | Roles: owner, recruiter, viewer. | P1 (model) / P2 (screens) | not started | — |
| REQ-052 | Billing for paid plans. | P2 | not started | — |
| **Dental expansion** |||||
| REQ-060 | Front-office assessments: Insurance Verification, Treatment Coordinator, Office Manager — reuse existing item types. | P3 | not started | — |
| REQ-061 | Clinical-knowledge assessments: Dental Assistant (back office), Hygienist — need image-based items (instrument ID, charting). Online tests check knowledge, not hands-on skill. | P3 | not started | — |

## SaaS Platform Requirements

Gaps found against the SaaS purpose (2026-10-22). **Design-now** items shape the data model and must be settled in architecture even if built later.

| ID | Requirement | Why it matters | Priority | Status |
|----|-------------|----------------|----------|--------|
| **Design-now** |||||
| SAAS-001 | Business model: pricing unit (per assessment / subscription / per seat), what's metered, plan limits and what happens at the limit. | Decides what the system must count and enforce (assessments used, seats, plans). Retrofitting metering into a live system means touching every flow that consumes usage. | P1 (decide) | not started |
| SAAS-002 | Content ownership: platform library vs. employer-customized vs. employer-authored assessments, and how customized copies track new library versions. | The core of the data model. If employers can edit or author items, versioning, answer-key secrecy and scoring all become per-tenant — a different design than one shared library. | P1 (decide) | not started |
| SAAS-003 | Candidate identity: one record per employer vs. shared across employers; retakes, waiting period between attempts, duplicate detection. | Sharing a candidate across employers leaks one employer's results to another and raises privacy issues; per-employer records make retakes and duplicates harder to spot. Changing this later means migrating every response. | P1 (decide) | not started |
| SAAS-004 | Test integrity against AI help (e.g. pasting Judgment/Email items into ChatGPT): item design, detection signals, item variants. | The product only has value if scores reflect the candidate. Judgment and Email items are easy to paste into an AI tool; if employers stop trusting scores, they stop paying. | P1 | not started |
| SAAS-005 | Tenant types: staffing agency (places with clients) vs. direct employer; whether agency clients get logins or only shared links; one account managing several client companies. | GSD Queen is an agency placing assistants with clients; many buyers will be direct employers. Who logs in and who owns the data differs between the two — it sets the tenant and role model. | P1 (decide) | not started |
| **Accounts and platform admin** |||||
| SAAS-010 | Self-service employer sign-up, email verification, company account creation. | Without self-service sign-up every new customer needs manual setup — the product can't grow beyond what Ashlee can onboard by hand. | P2 | not started |
| SAAS-011 | Invite teammates; password reset; two-factor login; single sign-on for larger customers. | Customers have several hiring staff; logins hold candidate personal data, so password reset and two-factor are baseline security. Larger buyers require single sign-on to buy at all. | P2 (SSO P3) | not started |
| SAAS-012 | Account cancellation and full deletion of a company's data. | Customers will leave; their candidate data must be removable on request to meet privacy law and their own contracts. | P2 | not started |
| SAAS-013 | Platform admin console: manage tenants, view usage, suspend, refund, view-as-customer for support (logged). | Running a SaaS means answering "why can't I log in" or "refund this" without editing the database by hand. View-as-customer must be logged because it exposes their data. | P1 (basic) / P2 | not started |
| **Billing** |||||
| SAAS-020 | Payment provider, invoices, sales tax, failed-payment handling, upgrades/downgrades, plan-limit enforcement. | Billing is where revenue leaks: failed cards, unpaid usage over limits, tax owed in states. A payment provider handles most of it, but the app must react to its events. | P2 | not started |
| SAAS-021 | Free trial or demo assessment for prospects. | Buyers want to try a hiring test before committing; a trial or demo is the main sales tool for self-service SaaS. | P2 | not started |
| **Branding and candidate reach** |||||
| SAAS-030 | Employer logo and name on invite emails and the test; custom sender address. | Candidates trust (and open) an email from the company hiring them, not an unknown platform. Employers expect the test to feel like part of their hiring process. | P2 | not started |
| SAAS-031 | Public job-posting link (open invite), bulk invite from CSV. | Employers posting a job get many applicants; inviting one at a time doesn't scale for them. | P2 | not started |
| SAAS-032 | Reminders to candidates who haven't started; warning before a link expires. | Candidates who forget to start are lost hires and wasted invites; reminders raise completion rates at almost no cost. | P1 | not started |
| **Integrations** |||||
| SAAS-040 | Public API and webhooks (notify other software when a candidate finishes). | Employers want results flowing into their own systems automatically; an API is how larger customers and partners integrate. | P2 | not started |
| SAAS-041 | Applicant tracking system integrations; Zapier. | Most employers already manage hiring in an applicant tracking system; living inside it removes the biggest reason not to adopt. | P3 | not started |
| **Analytics and validity** |||||
| SAAS-050 | Compare candidates side by side; percentile rank against all candidates of an assessment. | Employers decide between candidates, not in isolation; percentile rank gives a score meaning ("better than 80% of candidates"). | P2 | not started |
| SAAS-051 | Outcome analytics: which scores predict hires, 90-day retention and performance (backs REQ-036). | Proof that scores predict good hires is the strongest selling point and lets cutoffs be tuned with real data. | P2 | not started |
| SAAS-052 | Item analysis: difficulty, how well each item separates strong and weak candidates; retire weak items; validate cutoffs. | Weak or too-easy items make scores meaningless; item analysis keeps the test accurate and defensible if a hiring decision is challenged. | P2 | not started |
| SAAS-053 | Optional demographic questions for adverse-impact monitoring, stored apart from scoring, visible only in aggregate (backs NFR-004). | A hiring test that screens out one group more than others creates legal risk for employers. Monitoring needs demographic data, which must never influence or be visible in individual scoring. | P2 | not started |
| **Candidate support** |||||
| SAAS-060 | Handle connection loss mid-section; employer can reset a section (logged); timer dispute process. | Timed tests fail in real life (Wi-Fi drops, browser crashes). Without a fair recovery path, good candidates get bad scores and employers get support tickets. | P1 | not started |
| SAAS-061 | Supported browsers defined; phones blocked with a clear message; time zones shown correctly. | Typing and drag-to-rank items don't work on phones; telling candidates up front avoids failed attempts. Wrong time zones make deadlines and timestamps confusing. | P1 | not started |
| SAAS-062 | Accommodations workflow: candidate requests, employer approves extra time (backs REQ-009). | Disability laws can require reasonable accommodations such as extra time; a defined workflow keeps it consistent and recorded. | P2 | not started |
| SAAS-063 | Other languages (e.g. Spanish). | Expands the market for roles where the job itself is in another language. | P3 | not started |
| **Legal** |||||
| SAAS-070 | Terms of service, privacy policy, data-processing agreement with employers. | No company will put candidate personal data into a platform without these contracts; they also limit Ashlee's liability. | P1 before first external customer | not started |
| SAAS-071 | Candidate data requests (access, deletion): who receives them and how they reach the employer. | Privacy laws give candidates rights over their data; the platform holds it on the employer's behalf, so requests need a defined path. | P2 | not started |
| SAAS-072 | Attorney check of state and city laws on automated hiring tools. | Some jurisdictions regulate tools that score job candidates (e.g. notice or audit rules); selling into them without checking is a legal exposure. | P2 | not started |
| **Go-to-market** |||||
| SAAS-080 | Public website and pricing page. | Prospects need somewhere to learn about and buy the product without a sales call. | P2 | not started |
| SAAS-081 | Import GSD Queen's existing placement data (source of the typing benchmarks). | GSD Queen's history is the evidence behind the cutoffs and the first data for outcome analytics. | P2 | not started |

## Technical Requirements

| ID | Requirement | Priority | Status |
|----|-------------|----------|--------|
| TECH-001 | Answer keys and scoring run on the server, never shipped to the browser. | P1 | not started |
| TECH-002 | Section timers enforced on the server, not only in the browser. | P1 | not started |
| TECH-003 | Database for invitations, responses, scores and hiring outcomes. | P1 | not started |
| TECH-004 | Disable pasting on typing and writing tasks; log tab switches. | P1 | not started |
| TECH-005 | Server-side PDF report generation. | P1 | not started |
| TECH-006 | Transactional email for invites and notifications. | P1 | not started |

## Non-Functional Requirements

| ID | Requirement | Metric | Status |
|----|-------------|--------|--------|
| NFR-001 | Candidate personal information stored securely. | Encrypted at rest and in transit | not started |
| NFR-002 | Data retention policy and delete-on-request for a candidate's data. | Deletion completes and is verifiable | not started |
| NFR-003 | Tenant isolation: no employer can read another's candidates. | Zero cross-tenant reads in tests | not started |
| NFR-007 | Availability. | Target TBD (e.g. 99.5% monthly) | not started |
| NFR-008 | Performance under load. | Target TBD: concurrent candidates mid-test, page response time | not started |
| NFR-009 | Backups and restore. | Daily backups; restore tested | not started |
| NFR-010 | Audit log: who viewed a report, changed an outcome, edited content or settings. | Every such action logged with user and time | not started |
| NFR-011 | Separate staging and production environments. | Exists before first paying customer | not started |
| NFR-012 | Security certification readiness (SOC 2) for larger customers. | Controls documented | not started |
| NFR-004 | Fairness: track pass rates by group to monitor adverse impact; keep job-analysis docs showing each section is job-related. | Report available per assessment | not started |
| NFR-005 | Employment attorney review before selling (Phase 2). | Sign-off recorded | not started |
| NFR-006 | Accessible UI (keyboard navigation, labels), works on desktop browsers. | WCAG 2.1 AA target | not started |

## Open Questions

| # | Question | Blocks |
|---|---|---|
| Q1 | ~~Lean Phase 1 vs. full app~~ — resolved: SaaS foundation from P1 (multi-tenant app + database). | — |
| Q2 | Does the prototype's assessment content (items, answer keys, explanations) ship as-is for Phase 1? | REQ-040 |
| Q3 | Invite link expiry length (prototype suggests 7 days)? | REQ-012 |
| Q4 | Product name — "GSD Queen Assessments" is a working name. | Branding |
| Q5 | Pricing model (SAAS-001). | Billing, metering |
| Q6 | Can employers author their own items, or only configure library assessments (SAAS-002)? | Content model |
| Q7 | Candidate record per employer or shared (SAAS-003)? | Data model, privacy |
| Q8 | Do agency clients log in, or only receive shared report links (SAAS-005)? | Roles, tenancy |
| Q9 | "Show correct answers" (REQ-007) vs. a shared library's secret key: may one employer reveal answers to a test other employers use? | REQ-007, SAAS-002 |

## Test Coverage

| Requirement | Test File | Test Name | Status |
|-------------|-----------|-----------|--------|
| — | — | No code yet | not written |
