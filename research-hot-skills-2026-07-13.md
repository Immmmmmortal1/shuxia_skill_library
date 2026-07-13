# Hot Skills Research

Date: 2026-07-13

Scope:

- ClawHub public registry surface and current security/audit metadata
- GitHub API repository metadata, recent activity, trees, and primary `SKILL.md` files
- Incremental comparison against the 2026-07-10 note

This note records reusable mechanisms, not popularity claims by themselves.

---

## Sources Checked

- ClawHub public home/registry surface, including search, publisher, audit, install, version-history, and trust-signal affordances
- GitHub topic searches for `agent-skills` and `codex-skills`, sorted by recent updates
- GitHub repository metadata and source files for:
  - `dpearson2699/swift-ios-skills`
  - `openclaw/agent-skills`
  - `microsoft/GitHub-Copilot-for-Azure`

Visible momentum on 2026-07-13:

- `dpearson2699/swift-ios-skills`: 869 stars, 43 forks, updated and pushed on 2026-07-13; its catalog contains many narrowly routed Apple-framework skills.
- `openclaw/agent-skills`: 882 stars, 55 forks, pushed 2026-07-12; its `behavior-validator` provides a concrete black-box validation contract.
- `microsoft/GitHub-Copilot-for-Azure`: 232 stars, 186 forks, pushed 2026-07-13; its repository contains both product skills and skills for authoring, reviewing, evaluating, and analyzing skill test runs.
- ClawHub's current public surface exposes audit, publisher, version-history, download/install, and trust-signal concepts. These reinforce the prior supply-chain patterns but did not justify another duplicate trust pattern today.

---

## Standout Skills And Mechanisms

### `openclaw/agent-skills`: `behavior-validator`

The validator is explicitly source-blind. It accepts a prewritten behavior contract, restricts evidence to observable surfaces, treats source access as contamination, uses anti-cheat probes, and reports every contract clause as pass, fail, blocked, or out of scope. It also recommends an isolated temporary workspace and redacted evidence capture.

Reusable lesson:

Independent validation needs an evidence-channel boundary, not merely a different reviewer prompt. If an evaluator can see implementation details, it can accidentally validate intent instead of behavior. A strong black-box skill declares allowed evidence, contamination conditions, isolation, anti-cheat probes, and a complete clause-status contract.

Pattern extracted:

- `PAT-068 Evidence-Channel Isolation`

### `dpearson2699/swift-ios-skills`: `activitykit`

The skill routes ordinary widgets to `widgetkit` and generic APNs setup to `push-notifications`, but it keeps Live Activity payload shape, `content-state`, and ActivityKit-specific APNs invariants in scope. Its frontmatter contains concrete user scenarios and API names, while the body states the neighboring-skill boundary without surrendering the local semantic contract.

Reusable lesson:

Scope splitting should not break semantic ownership. A domain skill may route generic infrastructure elsewhere while retaining the data invariants that determine whether its own artifact works. This prevents cross-skill handoffs from creating a gap where neither skill owns the end-to-end contract.

Pattern extracted:

- `PAT-069 Semantic-Core Retention Across Handoffs`

### `microsoft/GitHub-Copilot-for-Azure`: `analyze-test-run`

The skill uses trigger-rich frontmatter, fixed repository/tool parameters, artifact-first parsing, an explicit job-log fallback, formula-defined metrics, duplicate-issue search before mutation, and exclusions for failures that must not create issues.

Reusable lesson:

This reinforces existing patterns rather than adding a new one: operational analysis skills should define deterministic inputs, source priority, fallback evidence, metric formulas, and a deduplication gate before side effects. The notable design quality is how fallback reduces confidence without silently changing the output claim.

---

## Local Review Refinements

- When reviewing a validator, ask whether its evidence channels are independent from the implementation under test. Separate personas are insufficient if both can read the same source and rationale.
- When splitting a broad domain into neighboring skills, identify the semantic core for each skill. Route generic setup away, but keep the invariants required to make the local artifact correct.
- Treat fallback as an evidence downgrade: record which primary artifact was unavailable, which substitute was used, and which conclusions are therefore best-effort.
- Keep registry popularity separate from trust. ClawHub audit and publisher surfaces are useful evidence fields, not substitutes for source inspection or pinned identity.
