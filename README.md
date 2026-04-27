# chronos

A personal project for an all-in-one desktop utility — calendar and tasks first, more modules later. Vue 3 + Tauri client, NestJS + GraphQL + Postgres server, in a Rush monorepo.

## Status

Paused. Last active in 2023. The calendar/task module works (drag-to-update durations, repeating-task instances, keyboard navigation) and the Tauri shell runs, but several planned modules and the polish pass never landed.

I'm leaving this public because the architecture and the interaction code are still useful as a reference, and I might come back to it.

## Layout

- `apps/client` — Vue 3 frontend wrapped in Tauri (`src-tauri/`)
- `apps/server` — NestJS GraphQL API (`schema.gql`)
- `libs/types` — shared TypeScript types
- `common/` — Rush hooks, config, scripts
- `docker/` — Postgres dev container
- `rush.json` — Rush monorepo config (pnpm)

## Local dev

Convenience targets in `Makefile`:

```bash
make dev         # tauri-client + server in parallel
make tc          # tauri client only
make sv          # server only
make pg          # psql shell into the postgres container
```

## What I'd change if I picked it back up

- Replace Rush with a lighter monorepo tool (pnpm workspaces + turborepo) — Rush was overkill for a solo project and its install loop is the main reason I bounced off coming back.
- Lift the calendar interaction layer into a standalone library; the drag-to-update + repeating-instance logic is the most reusable piece and shouldn't live inside an app.
- Treat the GraphQL schema as the contract earlier — several FE/BE drift bugs would have been caught by codegen.
