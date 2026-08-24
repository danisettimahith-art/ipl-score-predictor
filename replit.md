# IPL Score Predictor

An end-to-end IPL innings score prediction learning app with a React interface, Express prediction API, and standalone Python/Flask ML reference project.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/ipl-score-predictor/src/` — React predictor, methodology, and viva-prep pages.
- `artifacts/ipl-score-predictor/ml/` — Kaggle-ready preprocessing, model comparison, pickling, Flask API, and report.
- `artifacts/api-server/src/routes/predictor.ts` — live prediction and model metadata endpoints.
- `lib/api-spec/openapi.yaml` — source of truth for generated API types.

## Architecture decisions

- The UI uses the shared Express service for its live prediction experience; the Python folder is a portable reference implementation for coursework and deployment.
- Random Forest is the selected model in the comparison surface; the runtime demo predictor is deterministic and keeps the app useful without a trained binary.
- Team names are treated as categorical features and recent five-over activity is retained as a momentum signal.

## Product

Users can enter a live innings state, get a predicted final score with a range, inspect model metrics and methodology, and rehearse viva questions.

## User preferences

The product should remain useful as both a polished demo and an educational project reference.

## Gotchas

- After changing `lib/api-spec/openapi.yaml`, run `pnpm --filter @workspace/api-spec run codegen`.
- Use `pnpm --filter @workspace/ipl-score-predictor run typecheck` for frontend verification.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
