# Local development preferences

## Bun

Use Bun commands and package management by default. Respect the repository's existing dependency and lockfile structure.

## Portless

- Prefer stable named local URLs instead of manually coordinating ports.
- Use Portless's native commands and configuration.
- Avoid custom launchers that duplicate built-in behavior.
- Keep frontend URLs, API URLs, trusted origins, and authentication configuration consistent.
- Keep local URL configuration separate from secrets and production configuration.
- Resolve certificate and privileged-port prompts in an interactive terminal before starting crew or another process coordinator.
- On a supported platform, a startup service can avoid repeated proxy startup prompts. Explain the system change and obtain authorization before installing it.
- Document a straightforward way to run without Portless.

## crew

- Prefer crew (`@cristianbgp/crew`) for new setups that coordinate several development services, within one repository or across local repositories.
- Keep a small native `crew.toml` using existing service commands and paths relative to that file. Reuse Portless commands directly when applicable.
- Give each process a clear name and preserve readable logs.
- Keep individual applications runnable independently.
- Add startup dependencies and readiness checks only where startup actually depends on another service being available.
- Let each service load its own environment from its working directory; do not inject the launch project's dotenv files into every service. Already exported variables remain inherited.
- Keep working mprocs or other process setups in existing projects unless a migration is requested.
- Do not require crew for a single-process project. A package script may be sufficient.

## Keep it simple

Prefer a small package-script setup and native configuration. Create helper scripts only when they handle a demonstrated requirement that the tools do not already cover.
