# Assistant Assessment Platform

An hour-long, job-realistic pre-hire test for executive and administrative assistants, with scored employer reports and red flags for interviews. Built for Ashlee (GSD Queen, which places assistants with business owners). Working name: GSD Queen Assessments.

> Everything general lives in `~/.claude/CLAUDE.md` and applies here. This file
> holds only what is true of this project and nothing else.

## Rules that can never be broken

- **The prototype is the spec.** `Assistant Assessment Platform_ Clickable Prototype.html` holds the screens, the full assessment content (items, answer keys, explanations, red flags) and the **Developer notes** panel listing what must be built. `docs/requirements.md` is extracted from it — when they disagree, ask.
- **Answer keys and scoring never reach the browser.** Scoring and section timers run on the server (the prototype does both in the browser; that must not carry over).
- **The candidate never sees red flags, ratings or timing.** Their report has scores and explanations only; showing correct answers is a per-employer setting.
- **Assessments are versioned.** A report must always render against the exact questions that candidate saw — never edit a published version in place.
- **Each employer sees only its own candidates** (from Phase 2; design for it from the start).

## Where the repo misleads you

- The prototype HTML is **not the app's codebase** — it's a single front-end-only file with sample data. Don't extend it or build on its code; extract content and behavior from it.
- `tsconfig.json` (`{}`) is a placeholder written by the code-graph indexer. It does not mean the stack is TypeScript — the stack is undecided.

## Stack and commands

Not chosen yet. Decide with `/gsd-t-architect` (see Open Questions in `docs/requirements.md`: lean Phase 1 vs. full app). Fill this section in once decided.

| | |
|---|---|
| Build | — |
| Test | — |
| Expected branch | `main` |

## Where things are written down

| | |
|---|---|
| Requirements (from the prototype) | `docs/requirements.md` |
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
