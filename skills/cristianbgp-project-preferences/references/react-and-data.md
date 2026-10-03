# React and server data preferences

Use this reference for React components and API consumption. Apply the parts that match the project; it does not require SSR, React Server Components, or React Router framework mode.

## Components and state

- Calculate values derived from props or state during rendering instead of synchronizing a second copy with an effect.
- Keep user-triggered work in event handlers or mutation callbacks. Use effects to synchronize with external systems, and clean up subscriptions and timers.
- Keep state near its consumers. Use composition before introducing a global store or a generic component with many interacting mode flags.
- Use explicit variants or composable parts when they clarify different workflows. Ordinary booleans such as disabled or open do not need a new abstraction.
- Add memoization for measured expensive work or a demonstrated identity requirement. Do not wrap trivial expressions by default.
- Place error boundaries where failures should be isolated, with useful recovery behavior. Handle request and event-handler errors through their own error paths.

## API contracts and query ownership

- Consume the OpenAPI-generated Orval client instead of hand-maintaining duplicate endpoint types and request functions.
- Configure shared transport concerns through supported generation options or the project's existing transport integration. Do not edit generated files or add a wrapper that only forwards arguments.
- Use TanStack Query as the owner of server-data caching and mutation state. Include inputs that change the result in query keys, and keep cached data scoped to the relevant user or tenant.
- Reuse generated query keys and hooks when provided. Invalidate or update affected queries after mutations; do not refetch unrelated data by default.
- Clear or separate private cached data when authentication or account context changes.
- Set freshness, polling, and retry behavior according to the data and failure type. Avoid a universal interval or retrying failed mutations without considering duplicate effects.
- React Router loaders may prepare navigation by using the same query definitions and cache. Do not create a competing cache or require all fetching to live in loaders.

## Async behavior and failures

- Run independent reads concurrently when it helps; keep dependent operations and ordered writes in the required sequence. Respect concurrency limits and transaction boundaries.
- Distinguish network failures, HTTP errors, validation errors, and cancellation. Present a useful recovery action without exposing server internals.
- If cancellation is needed, pass TanStack Query's AbortSignal through the actual transport. Unmounting alone does not guarantee that the network request is aborted.
- Avoid stale results replacing newer input-driven results. Keep query keys aligned with input and use the transport's cancellation support when appropriate.
- Use query or mutation status for network feedback. A React transition can prioritize rendering but does not replace caching, request cancellation, or mutation tracking.
- Use optimistic updates only when their rollback and reconciliation behavior is clear. For operations where correctness depends on server confirmation, reflect that confirmation in the UI.

## Performance and validation

- Load heavy optional features when they are needed, using the framework and bundler's supported mechanisms. Prefer public package exports; do not reach into private distribution paths merely to shorten imports.
- Optimize rendering, bundles, and lookups in response to evidence. Avoid changing readable code for speculative microoptimizations.
- Validate untrusted input at the relevant boundary with Zod or an equivalent existing validator. A generated TypeScript type or an assertion does not perform runtime validation.
- Keep secrets out of client bundles. Check authentication integration, cookie behavior, and trusted origins against the actual frontend/API URLs.
- For Better Auth, consult current official documentation when implementing integration details. Review generated schema changes when adapters or plugins change; preserve the project's migration workflow.
