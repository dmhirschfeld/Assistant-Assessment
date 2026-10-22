# Architecture — Assistant-Assessment

## Last Updated: 2026-10-22

## System Overview
Multi-tenant SaaS: one Postgres database with every tenant-owned row tagged by company and enforced by row-level security. React web app + Fastify API (TypeScript), hosted on Vercel, database on Neon, email via Resend. Test content is stored as frozen, versioned documents; answer keys and scoring stay on the server; section deadlines are recorded and enforced by the server.

Full design and flows: `.gsd-t/pseudocode/PseudoCode-Foundation.md`.

## Components

### {Component Name}
- **Purpose**: {what it does}
- **Location**: `src/{path}/`
- **Dependencies**: {other components, external services}
- **Key Methods/Endpoints**: {list}

## Data Models

### {Model Name}
| Field | Type | Constraints | Notes |
|-------|------|-------------|-------|
| id | uuid | PK | auto-generated |

## API Structure

### {Endpoint Group}
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| GET | /api/{resource} | required | {description} |

## External Integrations

| Service | Purpose | Auth Method | Documentation |
|---------|---------|-------------|---------------|
| {service} | {what it does} | {API key / OAuth / etc.} | {link} |

## Design Decisions

| Date | Decision | Rationale | Alternatives Considered |
|------|----------|-----------|------------------------|
| 2026-10-22 | House stack: TypeScript, React + Vite, Fastify, Postgres on Neon, Vercel, Resend, Vitest + Playwright | Same as TimeTracking/binvoice — known patterns and deploy path | Next.js all-in-one |
| 2026-10-22 | Shared database, company column on every tenant row + row-level security | Simplest tenancy; database-enforced isolation | Database per company |
| 2026-10-22 | Platform library + per-company settings; only platform staff author | Keeps answer keys secret and one scoring path | Employer copies; employer authoring |
| 2026-10-22 | Candidates are per company, never linked | Privacy; simplest data ownership | Shared cross-company profile |
| 2026-10-22 | Agency clients: share links (P1), client-viewer logins (P2) | Client tag on invitations from day one supports both | Only one of the two |
| 2026-10-22 | Usage recorded per completed assessment | Any future pricing model can bill from it | Choose pricing first |
