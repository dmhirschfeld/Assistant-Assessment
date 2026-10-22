# Assistant Assessment Platform

An hour-long, job-realistic pre-hire test for executive and administrative assistants, with scored employer reports and red flags for interviews. Built for Ashlee (GSD Queen, which places assistants with business owners). Working name: GSD Queen Assessments.

> Everything general lives in `~/.claude/CLAUDE.md` and applies here. This file
> holds only what is true of this project and nothing else.

## Rules that can never be broken

- **The prototype is the spec.** `Assistant Assessment Platform_ Clickable Prototype.html` holds the screens, the full assessment content (items, answer keys, explanations, red flags) and the **Developer notes** panel listing what must be built. `docs/requirements.md` is extracted from it — when they disagree, ask.
- **Answer keys and scoring never reach the browser.** Scoring and section timers run on the server (the prototype does both in the browser; that must not carry over).
- **The candidate never sees red flags, ratings or timing.** Their report has scores and explanations only; showing correct answers is a per-employer setting.
- **Assessments are versioned.** A report must always render against the exact questions that candidate saw — never edit a published version in place.
- **This is a multi-tenant SaaS product from day one.** GSD Queen is the first tenant, not a separate internal tool. Each employer sees only its own candidates; tenant isolation is P1.

## Where the repo misleads you

- The prototype HTML is **not the app's codebase** — it's a single front-end-only file with sample data. Don't extend it or build on its code; extract content and behavior from it.
- `tsconfig.json` (`{}`) is a placeholder written by the code-graph indexer, not a real TypeScript config — replace it when the first package is scaffolded.

## Stack and commands

Planned (not built yet): TypeScript throughout — React + Vite web app (`web-app/`), Fastify API (`server/`), shared constants (`shared/`), Postgres on Neon with row-level security, hosted on Vercel, email via Resend, Vitest + Playwright. Design: `.gsd-t/pseudocode/PseudoCode-Foundation.md`.

| | |
|---|---|
| Build | — |
| Test | — |
| Expected branch | `main` |

## Where things are written down

| | |
|---|---|
| Requirements (from the prototype) | `docs/requirements.md` |
| Foundation design | `.gsd-t/pseudocode/PseudoCode-Foundation.md` |
| State and decisions | `.gsd-t/progress.md` |
| Interfaces between parts | `.gsd-t/contracts/` |
| How to reach environments | `docs/infrastructure.md` |

<!--
  Written 2026-10-22 from the clickable prototype (no code existed yet).

  Nothing above should carry a number that changes on its own — no version, no
  line count, no "currently in progress". Those belong in progress.md, and a
  file that repeats them is wrong within a week.

  Regenerate with /gsd-t-init-scan-setup.
-->


# Destructive Action Guard (MANDATORY)

**NEVER perform destructive or structural changes without explicit user approval.** This applies at ALL autonomy levels.

Before any of these actions, STOP and ask the user:
- DROP TABLE, DROP COLUMN, DROP INDEX, TRUNCATE, DELETE without WHERE
- Renaming or removing database tables or columns
- Schema migrations that lose data or break existing queries
- Replacing an existing architecture pattern (e.g., normalized → denormalized)
- Removing or replacing existing files/modules that contain working functionality
- Changing ORM models in ways that conflict with the existing database schema
- Removing API endpoints or changing response shapes that existing clients depend on
- Any change that would require other parts of the system to be rewritten

**Rule: "Adapt new code to existing structures, not the other way around."**
