# agent-skills

Personal engineering preferences and focused development workflows by **cristianbgp**, packaged as portable Agent Skills.

Public GitHub repository: `cristianbgp/agent-skills`. Licensed under [MIT](LICENSE).

## Context and decisions

This collection started from [Mi stack actual](https://cristianbgp.com/articles/mi-stack-actual/) and experience building Runa. It captures reusable preferences, not Runa's architecture or brand.

The agreed updates to the article's baseline are:

- Prefer Tailwind CSS + shadcn/ui built on **Base UI**, using Radix when the required Base UI option is unavailable or unsuitable. Preserve existing projects' component foundations.
- Prefer **OpenAPI + Orval**, including in monorepos. Hono RPC remains an alternative with a concrete justification.
- Include **Bun, Portless, and mprocs** for simple local development. Prefer native configuration over custom launchers; mprocs is optional for a single process.
- Define UI tools and quality criteria, **not a fixed aesthetic**. Each product determines its colors, typography, density, and visual direction.
- Keep project preferences in **one skill** with selectively loaded references. Separate skills cover independently useful workflows rather than duplicating these defaults.
- Use the username **cristianbgp** throughout.

The remaining baseline includes TypeScript, React/Vite/React Router, TanStack Query, Hono/Zod, PostgreSQL/Drizzle, Better Auth, Vitest, Cloudflare Pages, and Railway. These are conditional defaults: do not install every piece, force a monorepo, or migrate an existing project automatically.

## Structure

```text
README.md
LICENSE
skills/
├── cristianbgp-project-preferences/
│   ├── SKILL.md
│   └── references/
│       ├── web-ui.md
│       ├── react-and-data.md
│       ├── testing.md
│       └── local-development.md
└── web-animation-performance/
    └── SKILL.md
```

`SKILL.md` contains the instructions and links to the references. No `agents/openai.yaml` is included: this package does not need Codex-specific display metadata. No runtime code, package.json, build, or npm publishing is required.

References are loaded by task: `web-ui.md` for UI, mobile browser behavior, and motion; `react-and-data.md` for React and API consumption; `testing.md` for verification strategy; and `local-development.md` for local tooling. All preference instructions are included in this package.

## Skills

- [cristianbgp-project-preferences](skills/cristianbgp-project-preferences/SKILL.md): preferred stack and engineering criteria, with references selected by task.
- [web-animation-performance](skills/web-animation-performance/SKILL.md): design new web animations and diagnose existing performance problems through rendering evidence. Framework-independent and self-contained; no animation library is required.

The animation skill is an independent, optional package for selected projects. Project preferences do not load it or require its installation. Installing or updating `cristianbgp-project-preferences` does not select the animation skill.

## Publishing changes

Review and validate changes here before committing and pushing them to GitHub. Remote installations read the published repository, not unpublished files in this checkout.

Before publishing, check local skill discovery without installing:

```bash
bunx skills add . --list
```

After pushing, verify discovery from GitHub:

```bash
bunx skills add cristianbgp/agent-skills --list
```

## Install

Install each skill by name to select only the workflow you want. New skills and changes become available through these commands after they have been pushed.

### Project preferences

Choose your agent interactively:

```bash
bunx skills add cristianbgp/agent-skills --skill cristianbgp-project-preferences
```

For a global Codex installation:

```bash
bunx skills add cristianbgp/agent-skills --skill cristianbgp-project-preferences --agent codex --global
```

The CLI supports other agents; their discovery and activation behavior can differ. See the [skills CLI documentation](https://github.com/vercel-labs/skills#readme).

### Optional animation skill: project installation

Run this command from the project where you want animation assistance available. Omit `--global` to keep the installation scoped to that project:

```bash
bunx skills add cristianbgp/agent-skills --skill web-animation-performance --agent codex
```

Invoke it explicitly in Codex with `$web-animation-performance` when requesting animation work. Installation scope and automatic activation are separate: an agent may also select an installed skill based on its description. This portable package does not configure an agent-specific explicit-only policy.

## Use

Project preferences:

> Use cristianbgp-project-preferences to propose the smallest suitable stack for this project. Explain any departures from my preferences before implementing.

Animation design:

> Use web-animation-performance to implement an interruptible panel transition using this project's existing tools. Preserve document flow and support reduced motion.

Animation diagnosis:

> Use web-animation-performance to investigate why this drawer stutters with a long list. Separate suspected causes from measured evidence and verify any fix under comparable conditions.

In Codex, explicitly invoke the corresponding skill with `$cristianbgp-project-preferences` or `$web-animation-performance`. Each skill works independently.

## Maintain and update

Treat this repository as the source of truth. Edit the skill here, review the changes, and commit/push when desired. Then update the installed copy:

```bash
bunx skills update cristianbgp-project-preferences --global
```

For the animation skill, run the following from a project where it is installed:

```bash
bunx skills update web-animation-performance --project
```

Neither targeted update command selects the other skill. Keep edits in this repository; installed copies are managed by the CLI. When moving a manually copied installation to CLI management, back it up outside skill discovery directories and reconcile local changes first.

Validate changes with representative scenarios: a simple static site should not acquire an API/database; an existing Radix app should not be migrated automatically; an offline-first mobile app should not inherit the entire web stack. Format validation alone does not establish good agent behavior.

For animation, check both a new interaction and an existing performance problem. Include a case without browser access to verify that the agent reports uncertainty rather than inventing measurements. The animation skill has passed format and CLI discovery checks; behavioral evaluation on a real project is pending.

No repository, commit, push, or production changes are authorized by the skill itself.

## License

[MIT](LICENSE) © 2026 cristianbgp.
