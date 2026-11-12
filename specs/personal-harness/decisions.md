# Decisions and Questions

Status: Living decision register.
Parent: [Living RFC/PRD](./README.md).

Only explicit user direction belongs in Confirmed Decisions. Recommendations and unanswered questions do not authorize implementation choices. Future decisions should record date, choice, rationale, affected requirements, and any superseded decision.

## Confirmed Decisions

- **D-001 — Personal upstream fork** (2026-11-12): Start from a fork of `anomalyco/opencode` under `vyoungnyc`. Rationale: the user wants an owned foundation for personal customization. Initial fork creation is complete.
- **D-002 — Multi-LLM direction** (2026-11-12): Support a personal environment for multiple LLMs. Rationale: the user does not want to rely on one model. Exact providers and routing remain open.
- **D-003 — Visible, on-demand collaboration** (2026-11-12): Pursue panes, multiple harness sessions, on-demand startup, and communication between harnesses. Rationale: the user wants coordinated work rather than isolated manually managed terminals. Orca, Herdr, and tmux are references, not selected dependencies.
- **D-004 — Contextual command review** (2026-11-12): Include separate-model review before proposed commands execute, with human approval and risk explanation for potentially dangerous commands. Rationale: the user missed Claude Code's contextual permissions when customizing Pi. Local or fast hosted classification remains an option, not a selected model.
- **D-005 — Keep permission detail bounded** (2026-11-12): Retain permission classification as a requirement while deferring deep design. Rationale: the user explicitly asked not to become sidetracked from the overall harness.
- **D-006 — Modular living RFC/PRD** (2026-11-12): Maintain one main document with separately loadable section files and refine it incrementally. Rationale: focused context loading should avoid an oversized document.

## Foundation Questions

All questions below are **Open**. Answer a small related group when that decision becomes relevant; the user does not need to complete the entire register before further document refinement.

### Q-01 — First useful outcome

Which three real tasks should the harness handle, and what observable result makes the first one successful?

Recommendation: select one representative coding task before defining the first release scope. No benchmark is selected yet.

### Q-02 — Meaning of multiple harnesses

Must the first usable version run different native products such as OpenCode, Pi, Claude Code, and Codex, or can it start with multiple OpenCode sessions using different models?

Recommendation: keep the long-term cross-harness goal, but select the initial support list explicitly. Do not silently narrow R-003.

### Q-03 — Pane experience and tmux

Is the desired interface Orca's desktop environment, Herdr's terminal environment, or actual tmux? Is tmux compatibility mandatory, or are persistent panes and detach/reattach sufficient?

Recommendation: distinguish the required experience from the implementation. Evaluate Orca's existing orchestration before building equivalent machinery.

### Q-04 — Model access

Which provider accounts, subscriptions, API keys, and local inference endpoints must be supported? Should selection be manual, role-based, or automatically routed?

Recommendation: begin with explicit effective-model selection; choose automatic routing only against real tasks and account constraints.

### Q-05 — Execution location

Does the first version run only locally, or must it include SSH/remote workers? Which operating systems matter?

Recommendation: avoid distributed execution assumptions until a real workflow requires them.

### Q-06 — Launch and communication ownership

What launches workers: user request, coordinator judgment, queue, or schedule? May workers message each other directly, or should communication primarily pass through the coordinator?

Recommendation: establish one clear task owner. Permit structured question/result exchange without making every worker a scheduler.

### Q-07 — Resource and autonomy limits

What concurrency, spending, and runtime ceilings apply? Who can stop the entire run, and what happens to idle or failed workers?

Recommendation: explicit limits and user-visible cancellation; choose values after model access and task scope are known.

### Q-08 — Change isolation and integration

Does each editing worker need its own worktree? Which tasks need a container or VM? Who reviews, resolves conflicts, and merges results?

Recommendation: isolated worktrees for concurrent editors and human-controlled integration until the chosen workflow is proven. Worktrees do not protect host resources.

## Later Questions

These remain open but do not require deep design now:

- **Q-09 — Permission policy:** which actions always ask, which are forbidden, and how should approvals be scoped?
- **Q-10 — Classifier operations:** local-only or redacted hosted context; acceptable latency; unavailable-classifier and unattended behavior?
- **Q-11 — Coverage:** should contextual review cover direct file tools, MCP tools, browser actions, and delegated execution as well as shell commands?
- **Q-12 — Persistence:** which task state, memory, and artifacts survive restarts, and what must never be retained?
- **Q-13 — Recovery:** resume, retry, or escalate after process failure, interrupted delivery, or uncertain side effects?
- **Q-14 — Proof:** which real tasks, permission probes, and recovery scenarios establish readiness, and what performance targets matter?
- **Q-15 — Maintenance:** which upstream release baseline, synchronization cadence, fork divergence, and publishing approach are acceptable?

## Evidence and Scope Discipline

Research in [research.md](./research.md) informs these choices but does not decide them. A compatible-looking plugin or README is not a successful integration test. If a future answer changes a requirement, update [requirements.md](./requirements.md) and the affected architecture section rather than treating the decision register as a second specification.
