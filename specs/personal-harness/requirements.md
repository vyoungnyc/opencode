# Requirements

Status: Draft baseline extracted from the user's requests.
Parent: [Living RFC/PRD](./README.md).

The outcomes below reflect requested capabilities. Acceptance criteria are working interpretations for refinement, not an approved release scope. None of these capabilities is claimed implemented unless stated explicitly.

## Requested Capabilities

### R-001 — Personal OpenCode fork

Maintain the project in the user's GitHub account, based on `anomalyco/opencode`.

Acceptance: the repository identifies its upstream and preserves upstream history and license notices. Initial fork creation is complete; no custom runtime has shipped.

### R-002 — Multiple LLMs

Allow work to use different LLMs rather than one fixed model.

Acceptance: two sessions can select different configured models, and their effective model choices are inspectable. Providers and routing automation remain open.

### R-003 — Multiple harness sessions

Run multiple harness sessions concurrently.

Acceptance: at least two sessions can work independently. Whether they must use distinct native harness products, or may initially be OpenCode sessions with different models, is Q-02 in [decisions.md](./decisions.md#foundation-questions).

### R-004 — On-demand workers

Start workers when work requires them rather than requiring every worker to be launched manually in advance.

Acceptance: a task can cause a worker to start, receive its assignment, and report completion or failure. Launch policy and concurrency limits remain open.

### R-005 — Visible terminal work

Provide panes or an equivalent inspectable terminal experience for active harnesses.

Acceptance: the user can identify and inspect active sessions and intervene. Whether actual tmux compatibility is required is Q-03 in [decisions.md](./decisions.md#foundation-questions).

### R-006 — Inter-harness communication

Allow harness sessions to exchange tasks, questions, and results.

Acceptance: a worker can ask a question, receive an answer, and return an attributed result without the user copying text between terminals. Direct peer messaging versus coordinator-mediated communication remains open.

### R-007 — Contextual command review

Before a proposed shell command executes, consult a separate safety model about its risk and authorization in the context of the user's task.

Acceptance: execution waits for review; the review includes the command and task context. The classifier can use a local or hosted model. Model choice and latency targets remain open. This requirement concerns shell invocations, not a claim that every subprocess inside a script is independently classified.

### R-008 — Informed approval for risky commands

When review identifies potential danger, pause before execution and ask the user whether the action may proceed, explaining the risks.

Acceptance: the prompt identifies the action and target, describes the risk, and offers approval or rejection. Rejected actions do not execute. Approval scope, unavailable-classifier behavior, and unattended operation need explicit policy decisions.

### R-009 — Living, selective-context specification

Maintain one main RFC/PRD entry point with separately loadable sections that can be refined over time.

Acceptance: the main file links every section, each topic has one canonical owner, and a focused task does not require reading the whole specification. This document set provides the initial structure.

## Proposed Quality Constraints

These are recommendations, not additional user-approved scope:

- **N-001 — Minimal divergence:** use native capabilities and supported extension points before changing core behavior.
- **N-002 — Durable identity:** distinguish task, session, worker attempt, execution host, and pane identity.
- **N-003 — Safe concurrency:** isolate concurrent file editors and define who integrates results.
- **N-004 — Bounded operation:** set explicit concurrency, spending, and runtime limits.
- **N-005 — Enforced permissions:** hard restrictions and human approvals must not depend solely on a model's judgment or willingness to comply.
- **N-006 — Fail-closed review:** an unavailable gate, invalid classifier response, or missing human approval must not silently authorize a command.
- **N-007 — Observable behavior:** expose lifecycle, model selection, outcomes, and approval decisions without retaining secrets.
- **N-008 — Provenance:** distinguish human instructions and approvals from agent messages and untrusted external content.
- **N-009 — Compatibility:** pin and verify the chosen engine, plugins, harness adapters, and pane backend together.

## Product Verification

The eventual acceptance scenario should cover one real user task with different model selections, an on-demand worker, an attributed question/result exchange, and an inspectable pane. A harmless permission probe must demonstrate that a risky command cannot execute before approval and does not execute after rejection.

The task, completion criteria, performance thresholds, recovery expectations, and release gates are not selected yet. This is an acceptance outline, not a test implementation or a promise that the current checkout passes it.
