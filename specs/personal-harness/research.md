# Research and Evidence

Status: Discovery evidence, not implementation guarantees.
Parent: [Living RFC/PRD](./README.md).
Observed: 2026-11-12 through repository metadata, documentation, releases, and selected source inspection. No harness combination or classifier was runtime-tested.

Recheck the relevant versioned source before implementation. A release date, current branch, repository push timestamp, and supported engine range describe different things.

## OpenCode Version Baseline

- [OpenCode v2.2.7](https://github.com/anomalyco/opencode/releases/tag/v2.2.7) was published on 2026-11-10. The initial personal fork follows `dev`, not a pinned release tag.
- [V2 migration documentation](https://opencode.ai/docs/migrate-v1/) distinguishes supported legacy configuration from intentionally changed plugin and server contracts.
- [V1 plugin implementations do not run unchanged in V2](https://opencode.ai/docs/build/plugins/migrate-v1/).
- [Network client](https://opencode.ai/docs/build/client/): `@opencode/client`; event subscriptions are live-only, without replay or automatic reconnection.
- [Embedded SDK](https://opencode.ai/docs/build/sdk/): `@opencode/sdk`; hosts the server in the application without an HTTP listener.
- [Plugins](https://opencode.ai/docs/build/plugins/): `@opencode/plugin`; separate server, TUI, GUI, and RPC parts.
- [Native tools](https://opencode.ai/docs/tools/) already include background subagents and worktree operations. Do not assume older custom scaffolding is still needed.

## Actual Forks

### Shuvcode

[Repository](https://github.com/shuv1337/shuvcode) — GitHub ancestry verified as a fork of `anomalyco/opencode`; MIT.

Observed release: [v2.2.7-shuv.2](https://github.com/shuv1337/shuvcode/releases/tag/v2.2.7-shuv.2), 2026-11-12.

Useful reference for personal features, subagent visibility, provider customization, and deliberate upstream integration. Its [sync inventory](https://github.com/shuv1337/shuvcode/blob/integration-v2/docs/sync-2.2.6-shuv.2.md) separates retained features from historical work; an old merged branch does not prove that feature survived a rewrite. Not verified as a ready-made cross-harness supervisor.

### OC++

[Repository](https://github.com/devagrawal09/ocpp) — GitHub ancestry verified as an OpenCode fork; MIT. Latest inspected commit: 2026-10-21. The README states that release artifacts are not yet published.

Useful reference for cross-harness subagent drivers, structured results, durable execution, and explicit recovery of uncertain side effects. Its design substantially diverges from upstream. Automatic worktree isolation per worker was not established by the reviewed source.

## Clients and Extension Harnesses

### OpenChamber

[Repository](https://github.com/openchamber/openchamber) — independent OpenCode client/workspace, not an engine fork; MIT. Observed release: [v2.7.0](https://github.com/openchamber/openchamber/releases/tag/v2.7.0), 2026-11-08.

Useful reference for multi-model runs, optional worktrees, result fusion, and a narrow client integration boundary. Reviewed `main` [compatibility code](https://github.com/openchamber/openchamber/blob/main/packages/web/server/lib/opencode/compatibility.js) accepts OpenCode 2.x from 2.2.4; this is not proof that an older published binary has the same contract.

### Oh My OpenAgent

[Repository](https://github.com/code-yeongyu/oh-my-openagent) — canonical successor name for oh-my-opencode; not an OpenCode source fork. Observed release: [v5.1.69](https://github.com/code-yeongyu/oh-my-openagent/releases/tag/v5.1.69), 2026-11-11.

Useful routing, tmux lifecycle, and mailbox ideas. However, its [released V2 notice](https://github.com/code-yeongyu/oh-my-openagent/blob/v5.1.69/packages/omo-opencode/src/opencode-v2/startup-notice.ts) explicitly says the plugin loads while its agents, tools, and hooks are inactive. The project also has a standalone native direction. Its [Sustainable Use License](https://github.com/code-yeongyu/oh-my-openagent/blob/dev/LICENSE.md) is not MIT; examine reuse terms before copying code.

## Pane and Orchestration References

- **[Orca ADE](https://github.com/stablyai/orca):** independent runtime, not an OpenCode fork. Observed release [v1.4.257](https://github.com/stablyai/orca/releases/tag/v1.4.257), 2026-11-12. Its [orchestration contract](https://orca.dev/docs/cli/orchestration) includes Runs, tasks, Dispatch attempts, supervised workers, mailboxes, and decision gates. A Run does not itself schedule workers. Use installed-version skills for exact CLI behavior; website and release contracts can differ. [Agent settings](https://orca.dev/docs/agents/supported) prefill permission-bypass flags for supported launches, which conflicts with assuming safe permission defaults.
- **[Herdr](https://github.com/herdrdev/herdr):** independent terminal runtime; observed stable release [v0.9.5](https://github.com/herdrdev/herdr/releases/tag/v0.9.5), 2026-10-14. It replaces rather than requires tmux. Its [OpenCode integration](https://herdr.dev/tui/docs/integrations/#opencode) documents V2 testing against beta 19242, not current 2.2.7. The reviewed interface does not establish an Orca-equivalent durable task DAG/mailbox system. [Server restart restores layout and eligible conversations, not original processes](https://herdr.dev/tui/docs/session-state/).

The name Orca is ambiguous. `stablyai/orca` is Orca ADE; `fmfsaisai/orca` is a different tmux-script project. No pane backend is selected.

## Permission References — Detail Deferred

- [Claude Code permission modes](https://code.claude.com/docs/en/permission-modes) and [auto-mode configuration](https://code.claude.com/docs/en/auto-mode-config) describe contextual classification, policy precedence, and `classifyAllShell`. Default auto mode is not identical to the user's requested immediate approval prompt for risky commands.
- [Highflame analysis supplied by the user](https://www.highflame.com/blog/the-44kb-of-claude-codes-rulebook-you-cant-print/) reports observations of Claude Code 2.1.220. Consent provenance and cross-session permission laundering are relevant design risks; extracted prompts, sizes, and thresholds are not stable public contracts.
- [Anthropic's engineering report](https://www.anthropic.com/engineering/claude-code-auto-mode) describes two-stage classification and reports a 17% false-negative rate on 52 real overeager actions in that evaluation. This does not measure a future local classifier or establish current product performance.
- [OpenCode permission evaluation hooks](https://opencode.ai/docs/build/plugins/server/#permissions) can inspect context, call a model, and return `allow`, `ask`, or `deny`. Hook availability and complete execution-path coverage still need verification before using a plugin as mandatory enforcement.
- [Pi's permission-gate example](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/examples/extensions/permission-gate.ts) demonstrates pre-execution blocking and confirmation, but uses regex patterns rather than contextual model review.

## General Harness Lessons

[OpenAI's harness report](https://openai.com/index/harness-engineering/) emphasizes inspectable environments and executable feedback. [Cursor's coordination experiments](https://cursor.com/blog/self-driving-codebases) illustrate ownership and coordination failures. [Anthropic's long-running harness experiments](https://www.anthropic.com/engineering/harness-design-long-running-apps) show that scaffolding should be reevaluated as models improve. These are evidence for testing design assumptions, not universal architecture prescriptions.
