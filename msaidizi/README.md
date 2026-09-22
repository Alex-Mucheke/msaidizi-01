# Msaidizi

> **Find trusted help. Get things done.**

Msaidizi is a **service marketplace** connecting people who need services with trusted, verified service providers. It is not an e-commerce storefront — the core transaction is a service request, quote, and booking between a customer and a provider, not a product purchase.

---

## Project Vision

Msaidizi aims to make it simple and safe to find and hire trusted local service providers — and equally simple for providers to find work, manage bookings, and grow a professional reputation on the platform.

## Core Users

- **Customers** — discover services and providers, request quotes, book providers, communicate, track bookings, and leave reviews.
- **Service Providers** — build a verified profile, list services and pricing, manage availability, receive and respond to requests, communicate with customers, manage bookings, and track earnings.
- **Administrators** — manage users and providers, verification, service categories, bookings, disputes, reviews, and overall platform health.

## Planned Technology Stack

| Layer | Technology |
|---|---|
| Frontend | Next.js, TypeScript, React, Tailwind CSS |
| Backend | NestJS, TypeScript, REST API |
| Database | PostgreSQL, Prisma ORM |
| Auth | JWT, secure password hashing, role-based access control |
| Version control | Git, GitHub |

**Future integrations (PLANNED, NOT IMPLEMENTED YET):** maps/location services, email, SMS, push notifications, a payment provider, file/image storage, WebSockets for real-time messaging.

## Architecture

```
Frontend  →  REST API  →  NestJS Backend  →  Prisma  →  PostgreSQL
```

The frontend never talks to PostgreSQL directly — all data access goes through the backend's REST API. Authorization is enforced on the backend; the frontend must not be relied on as a security boundary.

## Repository Structure

```
msaidizi/
├── frontend/     Next.js + TypeScript + Tailwind CSS application
├── backend/      NestJS + TypeScript REST API
├── docs/         Product, design, and engineering documentation
├── database/     Database assets outside the backend's Prisma setup (SQL, ERDs, seed data)
├── .gitignore
└── README.md
```

See `docs/` for the full documentation set, including `docs/14-project-roadmap.md` for the phased plan.

## Development Philosophy

Msaidizi is built incrementally, following:

**RESEARCH → PLAN → DESIGN → IMPLEMENT → TEST → REVIEW → IMPROVE → DOCUMENT**

Every major feature is planned, designed, implemented, tested, and documented before moving on. Architectural decisions that affect the rest of the application are documented (decision, rationale, alternatives considered, trade-offs, future impact) rather than assumed.

## Current Development Stage

**PHASE 0 — Product Discovery / Foundation**

Status: architecture planning and project scaffolding.

What exists right now:
- ✅ Root project structure (`frontend/`, `backend/`, `docs/`, `database/`)
- ✅ Documentation skeleton (14 planning documents, purpose defined, content **NOT STARTED**)
- ✅ Frontend foundation: Next.js (App Router) + TypeScript + Tailwind CSS, builds and lints cleanly. Only a placeholder landing page exists.
- ✅ Backend foundation: NestJS + TypeScript, builds, lints, and tests cleanly. Only the default health-check module exists.
- ✅ Planned (empty) module/folder structure for both frontend and backend, documented with short READMEs

What is explicitly **NOT IMPLEMENTED YET**:
- ❌ Authentication / authorization
- ❌ Database schema (Prisma models)
- ❌ Any product pages, dashboards, or UI beyond a placeholder screen
- ❌ Any API endpoints beyond the default Nest health-check route
- ❌ Payments, maps, messaging, notifications, or any other feature logic
- ❌ Any fake/sample/seed data

Do not assume any of the above exists just because a folder for it does — the folders are reserved boundaries for future work, not implementations.

## Running Locally (PLANNED)

> These commands work today for the scaffolded foundations. There are no product features to exercise yet.

### Frontend

```bash
cd frontend
npm install
npm run dev
```

Runs the Next.js dev server (default: http://localhost:3000).

### Backend

```bash
cd backend
npm install --legacy-peer-deps
npm run start:dev
```

Runs the NestJS dev server (default: http://localhost:3000 unless `PORT` is set — see `backend/.env.example`).

> **Note:** `--legacy-peer-deps` is currently required for `npm install` in `backend/` due to a peer-dependency resolution issue between the NestJS CLI's Vitest tooling and npm's dependency resolver (`arborist`) in this environment. See `docs/14-project-roadmap.md` / engineering notes for details. Plain `npm install` may work fine in other environments; if it fails with `Cannot read properties of null (reading 'edgesOut')`, fall back to `--legacy-peer-deps`.

### Database (NOT IMPLEMENTED YET)

No PostgreSQL schema or Prisma configuration exists yet. This section will be filled in once `docs/09-database-design.md` is complete and `backend/prisma/schema.prisma` is created.

## Code Quality

- TypeScript strictness where practical; avoid unnecessary `any`
- Small, focused modules and components — no giant services or components
- Clear separation of concerns between frontend, backend, and database
- Environment variables for all secrets — never hardcoded credentials
- Input validation on all external input
- No unnecessary dependencies, no duplicated business logic

## Contributing / AI Development Notes

This project may be worked on by multiple AI development assistants over time. Anyone (human or AI) contributing should:

1. Preserve the existing folder structure, naming conventions, and architecture.
2. Not introduce a different architecture without first documenting the proposed change, rationale, affected files, risks, and getting approval.
3. Follow the RESEARCH → PLAN → DESIGN → IMPLEMENT → TEST → REVIEW → IMPROVE → DOCUMENT process for new features.
4. Update the relevant `docs/` file whenever a major decision is made.

---

**License:** Not yet decided.
