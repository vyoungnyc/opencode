# Architecture RFC

Status: Proposed; no architecture option is approved.
Parent: [Living RFC/PRD](./README.md).

## Working Recommendation

Use the existing OpenCode fork as the engine baseline. Keep model routing, orchestration, pane presentation, and contextual permissions separate so that one can change without replacing the others. Prefer native functionality and supported extensions; make core changes only when an enforced requirement cannot be met otherwise.

This recommendation is not a commitment to a custom supervisor, database, pane backend, or plugin-only implementation.

## Responsibility Boundaries

| Concern | Responsibility | Open choice |
| --- | --- | --- |
| OpenCode engine | Sessions, model calls, tools, context, native subagents | Release baseline and permitted fork changes |
| Model selection | Explicit roles, effective model visibility, optional routing | Providers, models, fallback and escalation policy |
| Orchestration | Assignments, worker attempts, dependencies, communication, lifecycle | Reuse Orca or another runtime; build only missing behavior |
| Pane backend | Present terminals, attach to sessions, route human input | Orca, Herdr, tmux, or another backend |
| Harness adapters | Launch, prompt, observe, interrupt, resume, and collect results | OpenCode only initially, or multiple native harnesses |
| Permission gate | Intercept actions, evaluate risk and authorization, obtain approval | Enforcement boundary and classifier provider |
| State and artifacts | Keep task results and recovery evidence addressable | Reuse existing storage versus add a cross-harness store |

A pane is a view or process attachment, not the authoritative record of a task. A separate session is not filesystem isolation. A worktree is not a security sandbox.

## Integration Options

### A — OpenCode-centered runtime

Use native sessions, agents, background subagents, and worktrees. Add custom routing or communication through supported interfaces where needed. Attach pane clients for inspection.

Benefit: fewer independent runtimes and less integration work.
Tradeoff: does not automatically provide native Claude Code, Codex, or Pi execution.

### B — External orchestration runtime

Use Orca ADE or another supervisor for task dispatch, worker lifecycle, and communication. Run the OpenCode fork as a supported or custom harness alongside other runtimes.

Benefit: can reuse existing multi-harness orchestration.
Tradeoff: adapter compatibility, permission handling, and ownership must be verified; an arbitrary terminal launch does not imply supervised-worker support.

### C — Terminal-first runtime plus coordination

Use Herdr or tmux for panes and persistence, adding or integrating task coordination only where absent.

Benefit: terminal-first control and visible native harnesses.
Tradeoff: pane prompting alone does not provide durable task delivery or completion tracking.

## Existing OpenCode Boundaries

Current V2 offers a network client (`@opencode/client`), an embedded host (`@opencode/sdk`), and server/TUI plugins (`@opencode/plugin`). These are distinct integration choices, not interchangeable package names. See [research.md](./research.md#opencode-version-baseline).

The repository separates [Core](../../packages/core/), [Protocol](../../packages/protocol/), [Server](../../packages/server/), [Client](../../packages/client/), [SDK](../../packages/sdk/), and [Plugin](../../packages/plugin/). These are context pointers, not proposed edit targets. Exact implementation work needs its own scoped inspection and package instructions.

## Permission Boundary — Detail Deferred

The gate must sit before execution, not merely advise the coding model. The coding model proposes the command; a separate classifier reviews it; the harness enforces the resulting policy and approval requirement.

OpenCode's permission evaluation hook is a candidate extension point. It is not yet proof of mandatory coverage: asynchronous plugin loading, later command mutation, alternate execution paths, and other native harnesses require investigation before claiming that every command is gated.

A classifier cannot enforce operating-system isolation. Whether containers or VMs are needed is an open product/security decision. No classifier model, prompt, scoring scheme, or two-stage pipeline is selected.

## Contracts to Resolve Before Implementation

- Which layer owns worker launch, termination, and recovery?
- What identifies a task, a worker attempt, a session, and a pane?
- What constitutes completion, a blocked task, cancellation, and an unknown outcome?
- How are human approvals distinguished from agent messages and bound to one action?
- How does communication recover after a disconnected event stream or process restart?
- Which runtime state belongs to existing OpenCode storage, and which state is genuinely cross-harness?

The user-facing choices are tracked in [decisions.md](./decisions.md); do not treat these questions as permission to build every possible mechanism.
