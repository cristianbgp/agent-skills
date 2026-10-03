# Local development preferences

## Bun

Use Bun commands and package management by default. Respect the repository's existing dependency and lockfile structure.

## Portless

- Prefer stable named local URLs instead of manually coordinating ports.
- Use Portless's native commands and configuration.
- Avoid custom launchers that duplicate built-in behavior.
- Keep frontend URLs, API URLs, trusted origins, and authentication configuration consistent.
- Keep local URL configuration separate from secrets and production configuration.
- Resolve certificate and privileged-port prompts in an interactive terminal before starting mprocs.
- On a supported platform, a startup service can avoid repeated proxy startup prompts. Explain the system change and obtain authorization before installing it.
- Document a straightforward way to run without Portless.

## mprocs

- Use mprocs when several development processes need to run together.
- Keep one configuration when possible.
- Give each process a clear name and preserve readable logs.
- Keep individual applications runnable independently.
- Do not make mprocs mandatory for a single-process project.

## Keep it simple

Prefer a small package-script setup and native configuration. Create helper scripts only when they handle a demonstrated requirement that the tools do not already cover.
