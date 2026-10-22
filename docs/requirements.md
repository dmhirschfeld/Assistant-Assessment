# Requirements — Assistant-Assessment

## Last Updated: 2026-10-22

**Source:** `Assistant Assessment Platform_ Clickable Prototype.html` (repo root). The prototype is the spec: its screens show the product, and its **Developer notes** panel (toggle in the top bar) lists what must be built behind each screen. Where this doc and the prototype disagree, raise it — don't guess.

**Product:** an hour-long, job-realistic pre-hire test for executive and administrative assistants. Candidates work as an assistant to a busy owner ("Jane"): inbox, calendar, receipts, emails and judgment calls. Employers get a scored report with red flags to discuss in interviews. Working name: **GSD Queen Assessments**.

**Priority = phase:**

| Priority | Phase | Scope |
|---|---|---|
| P1 | Phase 1 — GSD Queen placements | Internal use, replacing the current off-the-shelf test. May start lean (e.g. Google Sheet + email notifications). |
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
| REQ-043 | Per-employer settings: spending limits in scenarios, which sections to include, cutoffs. | P2 | not started | — |
| REQ-044 | Randomize question and answer order. | P1 | not started | — |
| REQ-045 | Multiple versions of each item so answers can't be shared. | P2 | not started | — |
| **Accounts and billing** |||||
| REQ-050 | Employer accounts and logins; each organization sees only its own candidates (multi-tenant). | P2 | not started | — |
| REQ-051 | Roles: owner, recruiter, viewer. | P2 | not started | — |
| REQ-052 | Billing for paid plans. | P2 | not started | — |
| **Dental expansion** |||||
| REQ-060 | Front-office assessments: Insurance Verification, Treatment Coordinator, Office Manager — reuse existing item types. | P3 | not started | — |
| REQ-061 | Clinical-knowledge assessments: Dental Assistant (back office), Hygienist — need image-based items (instrument ID, charting). Online tests check knowledge, not hands-on skill. | P3 | not started | — |

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
| NFR-004 | Fairness: track pass rates by group to monitor adverse impact; keep job-analysis docs showing each section is job-related. | Report available per assessment | not started |
| NFR-005 | Employment attorney review before selling (Phase 2). | Sign-off recorded | not started |
| NFR-006 | Accessible UI (keyboard navigation, labels), works on desktop browsers. | WCAG 2.1 AA target | not started |

## Open Questions

| # | Question | Blocks |
|---|---|---|
| Q1 | Phase 1 stack: lean (Google Sheet + email) or a real app and database from the start? | Architecture |
| Q2 | Does the prototype's assessment content (items, answer keys, explanations) ship as-is for Phase 1? | REQ-040 |
| Q3 | Invite link expiry length (prototype suggests 7 days)? | REQ-012 |
| Q4 | Product name — "GSD Queen Assessments" is a working name. | Branding |

## Test Coverage

| Requirement | Test File | Test Name | Status |
|-------------|-----------|-----------|--------|
| — | — | No code yet | not written |
