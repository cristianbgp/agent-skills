---
name: cristianbgp-project-preferences
description: Apply cristianbgp's preferred stack and engineering criteria when starting a project, choosing architecture, or implementing web UI and local development tooling. Respect existing project conventions; do not initiate migrations unless requested.
---

# cristianbgp's project preferences

Use these preferences as defaults, not as a mandatory template. Choose the smallest setup that serves the product.

Explicit project requirements take precedence. In existing projects, preserve established conventions unless a change is requested or necessary. Explain meaningful departures from these defaults.

## Language and tooling

- Prefer TypeScript.
- Use Bun for dependency management and scripts, and as the API runtime when compatible with the deployment target.
- Do not replace working tools merely to make every project identical.
- Do not pin new projects to versions used by an older project. Check current compatibility before selecting versions.

## Web applications

- Default to React, Vite, and React Router.
- Consider Astro for public websites and content-oriented surfaces when its rendering model benefits the product.
- Use TanStack Query for server state: fetching, caching, invalidation, and mutations.
- Keep UI state local when possible. Introduce Zustand only for genuinely shared client-side state.
- Do not copy server data into a global store without a concrete reason.

For UI work, read [web-ui.md](references/web-ui.md).

For React components, API consumption, or server-state handling, read [react-and-data.md](references/react-and-data.md).

## APIs and contracts

- Prefer Hono.
- Use Zod at trust boundaries: HTTP input, configuration, and external responses that need runtime validation.
- Default to OpenAPI + Orval for frontend API clients.
- Keep the OpenAPI contract connected to route definitions and validation; avoid separately maintained versions of the same contract.
- Generate clients and types instead of manually duplicating them.
- Do not edit generated client files directly.
- Hono RPC is an alternative when its simplicity clearly benefits the project, not the automatic choice merely because it is a monorepo.
- Keep business logic testable independently of HTTP handlers and UI.

## Persistence and authentication

- When server-side persistence is needed, prefer PostgreSQL, Drizzle ORM, Drizzle Kit, and postgres.js.
- When authentication is needed, prefer Better Auth.
- Do not add a database or authentication before the product requires it.
- Review generated migrations. For existing data, consider compatibility, backups, and validation before applying changes.
- A successful local migration is useful evidence, not a guarantee that production is safe.

## Repository structure

- Use a single application or a monorepo according to the product's needs.
- Do not create shared packages, workers, or separate services by default.
- Introduce shared code when there is meaningful reuse or a clear boundary, not just to hold types already available from an API contract.
- Avoid custom wrappers when the chosen tools already support the workflow.

For development setup, read [local-development.md](references/local-development.md).

## Testing

- Prefer Vitest.
- For React behavior, prefer Testing Library with an appropriate DOM environment such as jsdom.
- Test observable behavior rather than source-code strings or implementation details.
- Test business rules independently, and cover endpoints and service integration where useful.
- When correctness depends on SQL behavior, use database-backed tests. Consider PGlite when representative; use real PostgreSQL when features or behavior require it.
- Preserve Bun's test runner in projects where it already works well.
- Match verification to the risk of the change.

When choosing or writing tests, read [testing.md](references/testing.md).

## Deployment

- Default to Cloudflare Pages for compatible frontends and Railway for APIs and managed PostgreSQL.
- Verify runtime and framework compatibility before committing to a host.
- Prefer Railway's native build tooling when sufficient; add a Dockerfile only when it solves a concrete need.
- Consider Cloudflare Workers for suitable APIs, especially those that benefit from Cloudflare services.
- Keep costs and operational complexity proportional to actual usage.
- Allow frontend and API to deploy independently while preserving contract compatibility.

## Other project types

Do not force the web stack onto every product.

For an offline-first mobile application, consider Expo, React Native, and SQLite. Add backend services only when needed. Do not automatically carry web UI libraries into native applications.

## Applying these preferences

When starting a project:

- Identify its surfaces, persistence needs, authentication needs, and deployment constraints.
- Propose the minimal applicable subset of this stack.
- Explain important trade-offs or exceptions.
- Add dependencies for an actual feature or requirement, not for hypothetical future use.

These preferences do not authorize deployments, production migrations, system-wide installations, commits, or pushes.
