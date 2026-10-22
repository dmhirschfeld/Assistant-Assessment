# Platform Foundation — Multi-Tenant Assessment SaaS

The groundwork every feature stands on: many employer companies on one system with their data walled off, a test library whose answer keys never leave the server, timers the server enforces, and reports built from saved answers. GSD Queen is the first company on it.

```text
Platform staff set up a new company (Phase 1 — self-service sign-up comes in Phase 2)
  Is it an agency that places assistants with client businesses:
    Yes: Turn on its client list (the businesses it places for)
    No:  Direct employer — no client list
  Invite the company owner by email — they set a password and sign in

Someone at the company signs in
  Every screen and every lookup is limited to their own company
  The database itself refuses rows from any other company (a second lock, not just the screens)
  What is their role:
    Owner:     Everything, including team and settings
    Recruiter: Invite candidates, read reports, record outcomes
    Viewer:    Read only
    Client viewer (Phase 2): Read only, and only candidates tagged to their one client business

Recruiter invites a candidate
  Enter first name, last name, email, which test, and optionally the client business
  Freeze the test version and the company's settings onto this invitation (so the report always matches what was taken)
  Make a single-use link with an expiry date
  Send the invitation email
  Did the email provider accept it:
    No:  Mark the invitation "email failed" on the dashboard and say so — never show it as sent
    Yes: Mark it "invited"

Candidate opens the link
  Is the link real, unused, unexpired and not cancelled:
    No:  Show which one ("expired", "already used", "cancelled") and how to ask for a new one
    Yes: Show the privacy and consent notice
      Do they accept:
        No:  Stop — nothing is recorded beyond the decline
        Yes: Confirm name and email — show the list of sections
          Is the screen a phone:
            Yes: Explain that a computer with a keyboard is required — stop
            No:  Continue

Candidate clicks Start inside a section
  Has this section already been started:
    Yes: Resume it — same deadline, saved answers restored (a refresh never resets the clock)
    No:  Record the start time and the deadline (section minutes, plus any approved extra time)
  Send the questions without the answer keys, in shuffled order
  As the candidate works, save each answer to the server
  Does a save arrive after the deadline:
    Yes: Refuse it — the section closes with what was saved in time
    No:  Keep it
  Candidate clicks Submit, or the deadline passes:
    Close the section — it can never be reopened by the candidate
    Score it on the server with the frozen version's keys
    Note any red flags (only possible in Morning Inbox, Judgment and Email)

Last section closes
  Add up the overall score, rating and typing speed
  Record one completed assessment against the company (the usage count any future price plan will bill from)
  Email the recruiter that results are ready
  Show the candidate their own report — scores and explanations only, never red flags, ratings, timing or correct answers

Recruiter opens a candidate's report
  Build it from the saved answers and the frozen test version
  The same report builder serves every view:
    Employer view:  everything, red flags first as interview talking points
    Candidate view: the employer view with red flags, ratings, timing and correct answers removed
    PDF download:   the employer view, printed
    Client link:    the employer view, read only, expires, can be revoked
  Record the hiring outcome — hired, not hired, still deciding
  Every view, outcome change and settings change goes in the audit log (who and when)
```

---

## What it does today

```text
A single clickable web page with sample data
  Employer screens show made-up candidates — nothing is saved or sent
  Candidate test runs entirely in the browser:
    Questions, answer keys, timers and scoring all live on the candidate's computer
  Reports are pre-written for three sample candidates
```

It was built to show the idea and settle the test content, not to run. Its content (items, keys, explanations, red flags, cutoffs) is the valuable part; its code is not carried forward.

## What changes

```text
Content moves out of the page into stored test versions on the server
Scoring moves from the browser to the server, one scorer per question type
Timers become deadlines the server records and enforces
Sample data becomes real companies, candidates and answers in a database
Every company's data is fenced off from every other company's
```

## The rules

- [RULE] Answer keys never reach the browser. The server sends questions with keys removed and scores on the server.
- [RULE] A section's deadline is set by the server when the candidate clicks Start, and any answer saved after it is refused.
- [RULE] Every tenant-owned row carries its company, and the database refuses cross-company reads (row-level security) — not only the app's filters.
- [RULE] A published test version is never edited. Changes create a new version. Each invitation freezes its version and the company's settings.
- [RULE] The candidate never sees red flags, ratings, timing or correct answers (library tests never reveal correct answers — Q9).
- [RULE] One report builder produces every view; the candidate view is the employer view with fields removed, never a second copy.
- [RULE] Candidates belong to one company. The same person at two companies is two unlinked records.
- [RULE] Employers configure library tests (sections, cutoffs); only platform staff author questions.
- [RULE] A failed invite or notification email is shown as failed — never reported as sent.
- [RULE] Usage is recorded once per completed assessment, per company.
- [RULE] Global: integer ids, plus a random public id on every table the app exposes; status and role values compared case-insensitively and kept in one shared list; no fallbacks.

## What I confirmed with you

- Stack: the house stack (same as TimeTracking and binvoice).
- Content: platform library plus per-company settings; companies don't author questions.
- Candidates: one record per company, never linked across companies.
- Agency clients: both — read-only links now, client logins in Phase 2.
- Not objected to (treated as fixed): prototype content is the Phase 1 content; usage counted per completed assessment; library tests never show correct answers.

## Why this shape

- **Objective:** let any number of companies run job-realistic assistant tests with trustworthy scores, starting with GSD Queen, without rebuilding the core when Phase 2 opens sales.
- **Conflict:** "Show correct answers" as a company setting (REQ-007) conflicts with a shared library's secret keys — resolved by never revealing keys on library tests. Per-company spending limits (REQ-043) conflict with fixed question text — see Traps.
- **Reuse:** the prototype's content and scoring rules (ported, not copied); the house stack's sign-in, email, database hosting, deploy and testing patterns from TimeTracking and binvoice.
- **Simplicity:** one database with a company column on every tenant row is the simplest tenancy; separate databases per company add operations work with no Phase 1 benefit. Test content as one stored document per version (not a table per question type) matches how it's authored and frozen. Timers as stored deadlines need no running clock on the server.
- **Duplication:** one report builder, one scorer per question type, one list of statuses and roles — no parallel versions.
- **Risk:** tenant leakage is the top risk, so isolation is enforced in the database, not only the app, and proven by tests that try cross-company reads. Candidate links are random, single-use and stored only as a fingerprint (hash). Client share links expire and can be revoked.
- **No fallback:** email failures, expired links and late answers all stop visibly; nothing degrades silently.
- **Verification:** scoring tests per question type built from the prototype's rules; cross-company isolation tests; end-to-end browser tests of invite → test → report, including refresh mid-section and a late save being refused.

## Traps found

- **Spending limit is baked into the questions.** Items like "a reorder costs about $180" and their keys ("under $500, within your authority") assume a fixed limit. A per-company limit needs questions written with a placeholder and keys computed from it. Phase 1 keeps the fixed limit; the setting waits for that rewrite.
- **Sample reports are a snapshot.** The prototype's three reports are pre-written outputs with no stored answers behind them — usable as layout reference, not as scoring test cases.
- **Typing benchmarks are a snapshot** of GSD Queen's placement data from another vendor's test (Criteria); unconfirmed whether that data exists and can be imported.
- **PDF on serverless hosting.** Printing a report to PDF needs a headless browser, which is heavy for Vercel functions — needs a short spike before committing.

## Open questions

- Q2/Q4/Q5 remain: content as-is for Phase 1, product name, pricing.
- Is the typing benchmark table real GSD Queen data, and can the current test's results be imported?
- AI-assisted cheating (SAAS-004): needs its own design pass — item design and detection signals.
- Google Sheets sync (REQ-024): proposed CSV export only in Phase 1.

## Where it lives

Planned layout (house stack — TypeScript throughout):

| Part | Location | Notes |
|---|---|---|
| Web app (employer + candidate screens) | `web-app/` | React + Vite |
| API server | `server/` | Fastify; `server/src/scoring/<itemType>.ts` one scorer per question type |
| Shared types and constant lists | `shared/` | statuses, roles, item types, rating bands |
| Database | Postgres on Neon | migrations in `server/migrations/`; row-level security policies keyed on `org_id` set per transaction |
| Test content | `content/assistant-v1.json` | extracted from the prototype, loaded as a published `assessment_version` |
| Email | Resend | invite, reminder, results-ready |
| Tests | `server/**/*.test.ts` (Vitest), `e2e/` (Playwright, headless) | |

Core tables (each with integer `id`; `public_id` UUID where exposed): `organizations` (kind: agency or employer), `users`, `memberships` (role, optional `client_id` for client viewers), `clients`, `assessments`, `assessment_versions` (frozen content document), `org_assessment_settings`, `candidates`, `invitations` (token hash, expiry, status, frozen version and settings, `client_id`), `attempts`, `section_attempts` (started, deadline, closed), `responses`, `section_scores`, `outcomes`, `share_links`, `usage_events`, `audit_log`.
