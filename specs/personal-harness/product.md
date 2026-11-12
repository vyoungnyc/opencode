# Product and Scope

Status: Draft.
Parent: [Living RFC/PRD](./README.md).

## Problem

The user wants a personal coding environment that can use multiple LLMs and harnesses together without manually managing every terminal, worker launch, or handoff. Previous Pi customization provided useful flexibility, but lacked the contextual command-permission behavior the user valued in Claude Code.

## Goals

- Customize an OpenCode fork while retaining access to upstream improvements.
- Choose different LLMs for different work rather than coupling the environment to one model.
- Run multiple harness sessions in visible panes and launch additional workers when needed.
- Let workers exchange tasks, questions, and results without manual copy-and-paste.
- Review commands in task context before execution and request informed human approval when risk is detected.
- Refine the product and technical design incrementally through this modular RFC/PRD.

## Terminology

- **Model:** an LLM selected through a provider or local inference endpoint.
- **Harness:** the runtime that owns a model's tool loop, context, permissions, and session behavior. OpenCode, Pi, Claude Code, and Codex are examples, not a committed support list.
- **Session:** one conversation and its execution state within a harness.
- **Coordinator:** the role that assigns work and receives worker reports. Whether this is a dedicated agent remains open.
- **Worker:** a session executing delegated work. It need not have a dedicated operating-system process or pane.
- **Pane backend:** the terminal surface and controls used to show or attach to sessions. Pane visibility does not itself provide orchestration or security isolation.
- **Orchestration:** task assignment, dependencies, communication, lifecycle, and result collection across sessions.
- **Permission gate:** harness-enforced interception before an action executes; a safety model supplies a judgment but does not execute the action.

## Illustrative Workflow

This scenario explains the desired experience. It is not the selected first benchmark or an approved architecture.

1. The user gives a coding task and any scope restrictions.
2. The coordinator determines whether additional workers are useful.
3. Workers launch as needed with explicit task context and selected models or harnesses.
4. The user can inspect active work through panes and intervene when necessary.
5. Workers ask questions and return results through the orchestration layer.
6. A proposed command is reviewed before execution. Potentially dangerous work pauses for an explanation and approval.
7. Results return to the owner of the task for verification and integration.

## Scope Boundaries

Confirmed boundaries:

- This is a personal harness initiative, with its repository under `vyoungnyc`.
- Command classification is part of the product, but deep permission-system design must not distract from foundation decisions.
- This document set is a living specification, not evidence that a feature exists.

Proposed boundaries, not yet agreed:

- Prefer existing OpenCode capabilities and a small fork delta over rebuilding the engine.
- Reuse a pane/orchestration runtime rather than writing another terminal emulator.
- Do not assume commercial hosting, team administration, or unrestricted autonomous merging is needed.
- Do not assume every supported harness needs a custom tool loop or permission implementation.

Supported providers, native harnesses, operating environments, and the first usable milestone are open in [decisions.md](./decisions.md).
