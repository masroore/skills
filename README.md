# Skills

A small collection of agent skills — reusable instruction sets that give coding agents specialized workflows.

Each skill lives in its own directory as a `SKILL.md` file with YAML frontmatter (`name`, `description`) followed by the instructions the agent follows when it activates that skill.

## Install

Install a skill with the Skills CLI:

```bash
npx skills add masroore/skills
npx skills add masroore/skills@implement-plan
npx skills add masroore/skills@implement-plan-worktree
npx skills add masroore/skills@designs
```

Add `-g` to install globally (user-level) and `-y` to skip confirmation prompts.

Run `npx skills update` to update everything you've installed, or `npx skills find` to browse the wider ecosystem.

## Skills

| Skill | What it does |
| --- | --- |
| [`designs`](./designs/SKILL.md) | Produces four new design options as real image renders of the actual app UI — using the app's own components, icons, fonts, and colors rather than an invented mockup. |
| [`implement-plan`](./implement-plan/SKILL.md) | Executes an implementation plan end-to-end: reads the plan, studies the existing codebase, implements every requirement and checklist item, runs the project's full verification tooling, and reports honestly. |
| [`implement-plan-worktree`](./implement-plan-worktree/SKILL.md) | Same protocol as `implement-plan`, but works in an isolated Git worktree on a feature branch with atomic commits, then syncs, rebases, merges to `master`, and cleans up. |

## Usage

Drop a skill directory into your agent's skills location so the agent can discover its `SKILL.md`, or point your agent at the file directly. Invoke a skill explicitly (for example `/implement-plan`) when your agent supports skill commands, or let the agent pick it up from the skill's `description` when the task matches.

`implement-plan` and `implement-plan-worktree` expect an attached plan file (e.g. `.plan/*.md`) and will ask which plan to implement if none is provided.

## License

MIT — see [LICENSE](./LICENSE).
