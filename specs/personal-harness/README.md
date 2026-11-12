# Personal Harness — Living RFC/PRD

Status: Draft; discovery and refinement, not an approved implementation plan.
Owner: vyoungnyc
Created: 2026-11-12
Last updated: 2026-11-12

## Purpose

Build a personal, OpenCode-based harness for multiple LLMs, with visible terminal sessions, on-demand workers, and communication between harnesses. Include contextual command review that asks the user before potentially dangerous execution.

This file is the main document and navigation map. Each linked section owns its detailed content; this file does not duplicate those sections.

## Current State

- The public fork exists at [vyoungnyc/opencode](https://github.com/vyoungnyc/opencode), with [anomalyco/opencode](https://github.com/anomalyco/opencode) as upstream.
- Initial checkout: `dev`, commit `3d308eae2e68dc39dfc12aba9dd408f9ce1cc0a1`.
- Research covers actual forks, extension-based harnesses, Orca ADE, Herdr, and contextual permissions.
- No custom harness behavior has been implemented or runtime-verified.
- Runtime, pane backend, provider choices, and implementation scope remain open.
- The permission classifier is a required capability; its detailed design is intentionally deferred.

## Sections

| Section | Canonical file | Load when working on |
| --- | --- | --- |
| Product and scope | [product.md](./product.md) | Goals, boundaries, terminology, and user workflows |
| Requirements | [requirements.md](./requirements.md) | Expected behavior and draft acceptance criteria |
| Architecture RFC | [architecture.md](./architecture.md) | Component boundaries and implementation options |
| Decisions and questions | [decisions.md](./decisions.md) | Confirmed direction, unresolved choices, and recommendations |
| Research and evidence | [research.md](./research.md) | External examples, compatibility, and source freshness |

## Context Loading

1. Read this file first.
2. Load only the section relevant to the current task. Do not recursively read every link.
3. Load another section only for a specific referenced requirement, decision, or source.
4. For implementation, load the applicable repository and package instructions separately.
5. Follow links to upstream code or external documentation only when that detail is needed. Research summaries are not API contracts.

Examples: product refinement needs `product.md`; routing acceptance needs `requirements.md`; pane selection needs the relevant questions in `decisions.md` and evidence in `research.md`.

## Refinement Rules

- Confirmed user decisions, proposed designs, open questions, and observed implementation are different states. Keep those labels explicit.
- Keep each fact in one canonical section and link to it elsewhere.
- Preserve requirement and decision IDs. Record changed or superseded decisions rather than silently rewriting their history.
- Record a dated decision only after the user makes it. An assistant recommendation is not approval.
- When a decision changes scope, update the affected requirements and architecture in the same change.
- Update this file only when status, navigation, or the overall direction changes.
- Split a section when it develops independently useful topics. Do not maintain a second flattened copy or require loading all sections.
- Keep credentials, transcripts, runtime state, and private local configuration out of these documents.

The next refinement should resolve the foundation questions in [Decisions and questions](./decisions.md#foundation-questions). Permission internals remain deferred unless they change a foundation decision.
