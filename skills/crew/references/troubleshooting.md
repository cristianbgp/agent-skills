# Troubleshooting a crew workspace

Start with the observed failure and the selected service's actual command, working directory, and current-run output. Change the smallest relevant configuration; do not reinstall tools or broaden timeouts as a first response.

| Symptom | Check first |
| --- | --- |
| Setup appears instead of saved services | Launch directory or explicit configuration path; crew does not search parents. |
| Interactive-terminal error | stdin and stdout must be terminals; help/version output does not exercise the workspace. |
| Command works in another terminal | Service cwd, exported environment, missing dependencies, and shell initialization; service shells do not load login profiles. |
| Unexpected variables from another project | Exported terminal values, direnv, or an outer runtime that loaded dotenv before launching crew. Inspect names and provenance without printing secrets. |
| Command not found after package installation | Optional native dependencies, host platform support, and the project's normal executable resolution. |
| Dependent never starts | Dependency ID/cycle, failed prerequisite, readiness type, exact endpoint/log text, and current process output. |
| HTTP readiness times out on a working browser URL | Browser redirects or authentication may hide a non-2xx response. Use an existing direct health endpoint that represents the required availability. |
| An autostart-disabled service launches | Another service may depend on it. |
| Log search misses earlier output | Search covers bounded retained output, not an unlimited log archive. |
| New command is saved but old behavior continues | Running command/directory changes require restart. |

## Navigation and logs

Use F1 for the installed version's shortcut guide, F2 for service search, Ctrl+K for commands, and F6 to move focus out of the service terminal. While terminal input is focused, typing, arrows, and Tab belong to that service.

Ctrl+F or F4 opens retained-output search. This is literal case-insensitive search per service, distinct from the live terminal screen. Matches include surrounding context; Context changes it, Reveal opens the retained output at the occurrence, and Matches returns to results.

Typing a query pauses the inspection snapshot while the service continues running. Refresh incorporates new output; Resume follows new matches. A paused inspector is not a paused process. Retention is bounded, so capture a fresh reproduction when the relevant output has expired.

Use Diagnostics to inspect command, cwd, process state, readiness, and output. Exported logs can contain anything printed by a service. Keep them local unless sharing is requested and the content has been checked. URLs detected from output are opened only by explicit action.

## Configuration conflicts

Preserve comments, unrelated services, and dependency/readiness settings during edits. If crew reports external file changes, reconcile the on-disk changes before saving. Keep editing retains unsaved form fields; Reload and discard replaces them with disk contents.

An adjacent `.lock` file is a persistent lock anchor, not proof that a workspace is running. Do not delete it or kill unrelated processes to resolve an assumed stale session. Reloading definitions can stop removed services, but does not automatically start newly added ones.

## Boundaries and evidence

Do not solve a consumer configuration issue by modifying crew's source or publishing a new package. If evidence suggests a crew bug, report the installed version, minimal configuration, expected/observed behavior, and reproduction; omit credentials and machine-specific private paths.

Do not run the tool's development suite to claim a consumer workspace works. Verify the actual service commands and interactive workflow when available, and state clearly when verification was limited to configuration review.
