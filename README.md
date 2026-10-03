# agent-skills

Personal engineering preferences by **cristianbgp**, packaged as portable Agent Skills.

Prepared for publication as the public GitHub repository `cristianbgp/agent-skills`, under the [MIT license](LICENSE).

## Context and decisions

This collection started from [Mi stack actual](https://cristianbgp.com/articles/mi-stack-actual/) and experience building Runa. It captures reusable preferences, not Runa's architecture or brand.

The agreed updates to the article's baseline are:

- Prefer Tailwind CSS + shadcn/ui built on **Base UI**, using Radix when the required Base UI option is unavailable or unsuitable. Preserve existing projects' component foundations.
- Prefer **OpenAPI + Orval**, including in monorepos. Hono RPC remains an alternative with a concrete justification.
- Include **Bun, Portless, and mprocs** for simple local development. Prefer native configuration over custom launchers; mprocs is optional for a single process.
- Define UI tools and quality criteria, **not a fixed aesthetic**. Each product determines its colors, typography, density, and visual direction.
- Keep these preferences in **one skill** with selectively loaded references. Split it only if actual usage establishes independently useful workflows.
- Use the username **cristianbgp** throughout.

The remaining baseline includes TypeScript, React/Vite/React Router, TanStack Query, Hono/Zod, PostgreSQL/Drizzle, Better Auth, Vitest, Cloudflare Pages, and Railway. These are conditional defaults: do not install every piece, force a monorepo, or migrate an existing project automatically.

## Structure

```text
README.md
LICENSE
skills/
└── cristianbgp-project-preferences/
    ├── SKILL.md
    └── references/
        ├── web-ui.md
        ├── react-and-data.md
        ├── testing.md
        └── local-development.md
```

`SKILL.md` contains the instructions and links to the references. No `agents/openai.yaml` is included: this package does not need Codex-specific display metadata. No runtime code, package.json, build, or npm publishing is required.

References are loaded by task: `web-ui.md` for UI, mobile browser behavior, and motion; `react-and-data.md` for React and API consumption; `testing.md` for verification strategy; and `local-development.md` for local tooling. All preference instructions are included in this package.

## Publication

The package is ready for a public repository at `cristianbgp/agent-skills`. To publish it, create an empty GitHub repository without generated files, commit the contents of this project, connect the remote, and push. Keep this repository's history independent of Runa.

Before publishing, check local skill discovery without installing:

```bash
bunx skills add . --list
```

After pushing, verify discovery from GitHub:

```bash
bunx skills add cristianbgp/agent-skills --list
```

## Install after publishing

The following remote commands assume `cristianbgp/agent-skills` has been created and pushed.

Choose your agent interactively:

```bash
bunx skills add cristianbgp/agent-skills --skill cristianbgp-project-preferences
```

For a global Codex installation:

```bash
bunx skills add cristianbgp/agent-skills --skill cristianbgp-project-preferences --agent codex --global
```

The CLI supports other agents; their discovery and activation behavior can differ. See the [skills CLI documentation](https://github.com/vercel-labs/skills#readme).

## Use

Example request:

> Use cristianbgp-project-preferences to propose the smallest suitable stack for this project. Explain any departures from my preferences before implementing.

In Codex, explicitly invoke it with `$cristianbgp-project-preferences`.

## Maintain and update

Treat this repository as the source of truth. Edit the skill here, review the changes, and commit/push when desired. Then update the installed copy:

```bash
bunx skills update cristianbgp-project-preferences --global
```

A manually copied skill is not necessarily tracked by the CLI. The original version was installed manually at `~/.codex/skills/cristianbgp-project-preferences` with optional Codex metadata. This portable package does not alter that installation. When switching to the repository-managed installation, back up any local edits and reconcile the existing copy to avoid duplicates.

Validate changes with representative scenarios: a simple static site should not acquire an API/database; an existing Radix app should not be migrated automatically; an offline-first mobile app should not inherit the entire web stack. Format validation alone does not establish good agent behavior.

No repository, commit, push, or production changes are authorized by the skill itself.

## License

[MIT](LICENSE) © 2026 cristianbgp.
