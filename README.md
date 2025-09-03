# Drizzle monorepo

This repository contains the Payload + Next.js app in `ltc-backend`.

## Quickstart

Prerequisites:
- Node.js 20.x (or >= 20.9.0)
- pnpm 10.x

### Development

```bash
cd ltc-backend
cp .env.example .env
# Edit .env and set your PostgreSQL connection string, e.g.
# DATABASE_URI=postgresql://postgres:...@...:5432/postgres

pnpm install
pnpm dev
```

The app will start at http://localhost:3000.

### Tests

```bash
cd ltc-backend
pnpm test:int
```

### Lint & Typecheck

```bash
cd ltc-backend
pnpm lint
pnpm exec tsc -p tsconfig.json --noEmit
```

## CI

- GitHub Actions workflow: `.github/workflows/ci.yml`
- Jobs required to pass on `main`: `build`, `test`

## Contributing

- Open PRs against `main`
- Fill out the PR template: `.github/pull_request_template.md`
- Ensure CI is passing before requesting review

