---
name: crew
description: Configure and troubleshoot crew (@cristianbgp/crew) workspaces for running local frontends, APIs, workers, and other services together. Use when creating or editing crew.toml, coordinating startup, diagnosing environment or readiness issues, or inspecting service logs. Not for developing crew itself or publishing its packages.
---

# crew workspaces

Use crew to run a project's existing development commands in an interactive terminal workspace. This skill configures and diagnoses consumer projects; it does not require another skill, modify crew's source, or manage releases.

Read [configuration.md](references/configuration.md) when creating or editing a workspace. Read [troubleshooting.md](references/troubleshooting.md) for failures, unexpected environment values, log inspection, or configuration conflicts.

## Inspect before configuring

- Read existing package scripts, workspace configuration, directory layout, and developer instructions. Preserve the project's package manager and working commands.
- Identify the services that need to run together, their working directories, prerequisites, and any real startup ordering requirements. Keep each service runnable independently.
- Check `crew --version` and `crew --help` if installed. If compatibility matters, consult documentation for that version; do not assume a dated example defines current capabilities.
- Use an existing installation when available. If installation is needed and authorized, add `@cristianbgp/crew` with the project's package manager, preferably as a development dependency for a shared project workflow. Do not install globally or replace another coordinator merely to configure a file.
- The npm launcher uses optional platform packages; retain optional dependencies. Check current distribution support for the host rather than assuming every OS/libc is supported. Service commands still require their own dependencies and runtimes.

## Create or edit the workspace

1. Choose the location of `crew.toml`. Use paths relative to that file for shared configurations; use actual sibling paths only when the user's local layout requires them.
2. Reuse service scripts. Give services clear IDs and optional visual groups. Keep destructive setup, provisioning, and migrations out of automatic startup unless explicitly part of the requested workflow.
3. Add `depends_on` only for real startup dependencies and a readiness check when a live process is insufficient. Avoid imposing order on independent services.
4. Preserve existing comments and unrelated settings. If converting from mprocs was requested, preserve the old workflow until the replacement has been checked; do not silently migrate other projects.
5. Optionally expose a script such as `dev:all` running `crew`. Avoid naming a wrapper `dev` if services themselves run that script, which would recursively launch crew.
6. Explain how to launch from the chosen directory or use an explicit configuration path, how services load environment variables, and how to quit and clean up.

The default launch commands are `crew` and `crew dev`. They look for `crew.toml` in the current directory, not parent directories. `crew --config path/to/crew.toml` selects another file. A missing file opens interactive setup; do not describe this as an automatic configuration search.

## Verify without inventing CLI capabilities

- First check the TOML, service paths, commands, dependency references, and cycles. Syntax parsing alone does not validate crew's schema or prove services start.
- If runtime verification is authorized, run the individual commands as needed, then launch crew in a real interactive terminal or a suitable PTY. Startup may run services marked for autostart and their dependencies; inspect commands before launching.
- Verify relevant readiness, navigation, retained output, restart, and quit behavior. Stop the session you started and check owned services have exited when cleanup is part of the test.
- crew is a foreground workspace, not a daemon, detached-session manager, or provisioning tool. Do not invent `crew start`, `crew status`, JSON inspection, or a headless validation flag. Check the installed help before relying on additional commands.
- When only a noninteractive shell is available, complete static checks and give the interactive launch command. Report startup and terminal behavior as unverified rather than leaving a background session running or claiming success from help/version output.

## Report the result

List the files changed, service commands and directories, any dependency/readiness decisions, and how to launch and quit. State what was actually checked and what remains unverified. An exported diagnostic log may contain service secrets or personal data; inspect it before including it in a report.

For version-specific details, use the project's installed documentation or [crew's documentation](https://github.com/cristianbgp/crew). All core instructions needed for this workflow are included here and in the two local references.
