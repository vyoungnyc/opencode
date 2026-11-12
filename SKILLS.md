# Repository Skills Index

This file is a navigation index, not a runtime skill manifest. Canonical skill definitions live under `.opencode/skills/`. OpenCode discovers those definitions; this index does not install integrations or configure another harness's skill discovery.

## Load Only What Applies

1. Follow the root [AGENTS.md](./AGENTS.md) and any applicable package instructions.
2. Choose a skill by the task, not merely because the skill exists.
3. Read the selected `SKILL.md` before performing the matching work, then follow only the references that work needs.
4. Do not preload all skills or copy their full bodies into repository instructions.
5. In a harness without native discovery for `.opencode/skills/`, read the linked file directly as task guidance; do not assume a native skill command exists.

## Existing Skills

| Skill | Load when |
| --- | --- |
| [opencode-dev](./.opencode/skills/opencode-dev/SKILL.md) | Interactively running, debugging, or verifying this repository's CLI/TUI or server |
| [effect](./.opencode/skills/effect/SKILL.md) | Working with Effect v4 services, schemas, workflows, or their APIs |
| [unit-tests](./.opencode/skills/unit-tests/SKILL.md) | Writing, reviewing, fixing, or speeding up Bun unit tests, including CLI subprocess and service tests |
| [tui-tests](./.opencode/skills/tui-tests/SKILL.md) | Working on OpenTUI renderer tests in `packages/tui` or `packages/cli` |
| [component-tests](./.opencode/skills/component-tests/SKILL.md) | Working on Playwright component tests, fixtures, or the stories they mount |
| [app-e2e-tests](./.opencode/skills/app-e2e-tests/SKILL.md) | Working on Playwright end-to-end tests in `packages/app/e2e` |
| [rtl-aware-development](./.opencode/skills/rtl-aware-development/SKILL.md) | Implementing or reviewing RTL/LTR behavior in the web or desktop interface |
| [sample-skill](./.opencode/skills/sample-skill/SKILL.md) | Explicitly demonstrating a skill or creating a skill template; not routine coding |

Skill files own their detailed procedures and prerequisites. This index does not replace them or prescribe test commands independently of package guidance.

## Personal Harness Discovery

For product and RFC refinement, start with [the living RFC/PRD](./specs/personal-harness/README.md), then load only the section being refined. Product requirements and unresolved decisions belong there, not in skill definitions.

Do not create a new skill for every planned capability. Add one when a repeatable workflow has concrete steps worth reusing. Keep each definition in one canonical location, use a clear task-specific description, and update this index when adding, removing, or renaming a repository skill. Do not copy machine-local or externally installed skills into the repository by default.
