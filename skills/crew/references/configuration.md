# Workspace configuration

## Minimal example

Adapt commands and paths to the actual project. Neither service depends on the other merely because both run in the same workspace.

```toml
name = "product"

[services.web]
cwd = "./apps/web"
command = "bun run dev"

[services.api]
cwd = "./apps/api"
command = "bun run dev"
```

Required service fields are `cwd` and `command`. Paths resolve from the configuration file. `repo` is an optional sidebar group, defaulting to the workspace name; it does not clone, checkout, or otherwise operate on Git repositories. `autostart` defaults to true. A sibling repository may use a relative path such as `../worker`, but do not assume a user's local layout in a reusable example.

## Startup dependencies

Add only the dependency and check the project needs. For example, a worker may need the API's existing health endpoint:

```toml
name = "product"

[services.api]
cwd = "./apps/api"
command = "bun run dev"
ready = { http = "http://127.0.0.1:3000/health", timeout_ms = 30000 }

[services.worker]
cwd = "./apps/worker"
command = "bun run dev"
depends_on = ["api"]
autostart = false
```

Use the actual endpoint and port, not the example's values by assumption. A readiness table selects exactly one of:

- `port`: TCP port; optional `host` defaults to `127.0.0.1`.
- `http`: HTTP(S) URL without embedded credentials; a 2xx response passes. Redirects are not followed.
- `log`: literal, case-sensitive output from the current run, not a regular expression or a previous run's retained history.

`timeout_ms` defaults to 30,000 and accepts 1–300,000. Readiness runs at startup, not continuously. A timeout leaves output and the process available but blocks dependent starts. Without a check, running does not establish application-level availability.

Dependencies reference service IDs and must not form cycles. Starting a service can start dependencies whose own autostart is false. Group start may reach dependencies outside the group; group stop does not stop dependents outside the group. Do not use visual groups as lifecycle isolation boundaries.

## Environment and Portless

Commands run in a shell with `-c`, the service's working directory, and inherited exported variables. Login profiles are not loaded. crew does not read the launch directory's dotenv files into all services; each framework/runtime loads its own environment files according to its rules.

An explicit service loader is allowed, for example `command = "bun --env-file=.env.staging run dev"`. Its environment-file path is relative to that service's directory. Keep secrets out of shared TOML and remember exported variables can override service files.

Reuse existing Portless commands and URLs directly. Complete required certificate/proxy setup interactively before starting the workspace. Verify the actual URL used for readiness; a reachable proxy is not necessarily a ready application.

Prefer the installed executable. When deliberately running crew from its source checkout, prevent the outer Bun invocation from loading dotenv: use `bun run --no-env-file dev`, or the verified public entry `bun --no-env-file src/entry.ts dev`. These are source-development commands, not commands for a consumer project.

## Launch and lifecycle

Run `crew` from the directory containing the file, or `crew --config path/to/crew.toml` from elsewhere. A project script such as `"dev:all": "crew"` keeps the invocation local to project tooling.

Each invocation owns its workspace and processes. Quit through Ctrl+Q or the UI; Ctrl+C normally interrupts the focused service, or copies its selection. Quit allows graceful shutdown before forcing remaining owned process groups to exit. Deliberately detached processes and forcibly killing crew itself are outside ordinary cleanup guarantees.
