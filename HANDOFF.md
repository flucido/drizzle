# Project Handoff Guide

This document provides everything needed to continue development on the "drizzle" repository and its Payload + Next.js app located in ltc-backend.

Repository: https://github.com/flucido/drizzle


## Overview
- App: Payload CMS on Next.js (ltc-backend)
- Package manager: pnpm (pinned)
- Node: 20.x recommended (engines: ^18.20.2 || >=20.9.0)
- CI: GitHub Actions (build and test jobs)
- Branch protection: main requires PRs, 1 approving review, passing checks (build, test), conversation resolution enabled, enforce admins


## Local Development
Prerequisites
- Node 20.x
- pnpm 10.x

Setup
1) Clone and install:
   - git clone https://github.com/flucido/drizzle.git
   - cd drizzle/ltc-backend
   - pnpm install
2) Configure environment:
   - cp .env.example .env
   - Edit .env to set your PostgreSQL connection string and any other required values
     - Do NOT commit secrets; keep them in .env
3) Start dev server:
   - pnpm dev
   - App runs at http://localhost:3000

Notes
- packageManager is pinned in ltc-backend/package.json to pnpm@10.11.0 to ensure tooling consistency.
- The repository previously had multiple lockfiles; this has been cleaned so Next.js no longer warns.


## Repo Structure
- / (repo root)
  - README.md (quickstart and CI info)
  - .github/workflows/ci.yml (CI workflow)
  - .github/pull_request_template.md
  - ltc-backend/ (Payload + Next.js app)
    - package.json (scripts and engines)
    - pnpm-lock.yaml
    - .env.example
    - src/...


## Scripts (ltc-backend)
- pnpm dev: Run Next.js dev server
- pnpm build: Build Next.js app
- pnpm lint: Lint via eslint-config-next
- pnpm test:int: Run unit/integration tests via vitest
- pnpm test:e2e: Run Playwright E2E (browsers need to be installed in CI if used)
- pnpm payload: Run Payload CLI


## CI/CD
Workflow file: .github/workflows/ci.yml
Jobs
- build: pnpm install, lint, typecheck (tsc --noEmit), build
- test: pnpm install, unit tests (pnpm run test:int)
Node version: 20.x
Cache: pnpm

Branch Protection (main)
- Require pull requests (no direct pushes)
- Minimum 1 approving review
- Enforce admins: true
- Required status checks: build, test (must pass)
- Require conversation resolution: true


## Git Status
- Remote: origin → https://github.com/flucido/drizzle.git
- Default branch: main
- Latest additions committed and pushed:
  - CI workflow
  - PR template
  - README
  - Lockfile cleanup & packageManager pin
  - Initial Payload app commit


## Environment & Secrets
- Do not commit secrets. Use .env (already gitignored).
- Example vars:
  - DATABASE_URI=postgresql://postgres:{{PASSWORD}}@{{HOST}}:5432/postgres
- If you see a redacted secret (like ******) in any logs or commands, replace it locally with the actual value via environment variables.


## Known Warnings
- No email adapter provided: Payload will log emails to console by default. Configure an email adapter for production.


## Troubleshooting
- Port 3000 in use: change port or stop the conflicting process
- Multiple lockfiles warning: resolved by removing parent lockfile and pinning pnpm. If it reappears, ensure only pnpm-lock.yaml is present and tools use pnpm.
- Node version mismatch: use Node 20.x; see engines in package.json.


## Next Steps (Suggested)
- Add GitHub Actions badge to README
- Add CODEOWNERS and require code owner reviews
- Optionally add Playwright E2E job to CI (installs browsers, longer runtime)
- Configure email adapter for Payload (production readiness)
- Address Dependabot-reported vulnerabilities (see GitHub Security tab)


## Archon Workflow (Project Rule)
This project follows Archon task-driven development. Before writing code, ensure the Archon cycle is followed:
1) Check Current Task: Review task details and requirements in Archon
2) Research for Task: Consult project docs and examples
3) Implement the Task: Write code based on research
4) Update Task Status: Move task from "todo" → "doing" → "review" (not directly to complete)
5) Get Next Task: Check for next priority task
6) Repeat Cycle
Additional rules:
- Update all actions in Archon
- Maintain task descriptions and add implementation notes
- Do not make assumptions—check project documentation


## Command Cheat Sheet
From repo root:
- cd ltc-backend
- pnpm install
- pnpm dev
- pnpm lint
- pnpm exec tsc -p tsconfig.json --noEmit
- pnpm test:int
- pnpm build

Git:
- git checkout -b feature/your-change
- git add -A && git commit -m "feat: your change"
- git push -u origin feature/your-change
- Open a PR to main (required checks: build, test)


## Contact / Ownership
- GitHub user: flucido
- Repo: https://github.com/flucido/drizzle

If anything blocks you, check CI logs in GitHub Actions and local dev.log (ltc-backend/dev.log).
