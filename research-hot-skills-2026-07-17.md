# Hot Skills Research

Date: 2026-07-17

Scope:

- ClawHub public updated, download-ranked, and star-ranked API surfaces
- GitHub repository search, metadata, commits, diffs, tests, and primary skill/docs files since the previous run
- Incremental comparison against the 2026-07-15 note

This note records reusable mechanisms, not popularity claims by themselves.

---

## Sources Checked

- ClawHub `/api/v1/skills` responses sorted by update time, downloads, and stars
- GitHub primary repository and commit evidence for:
  - [`sylvanus4/automl-train-skill`](https://github.com/sylvanus4/automl-train-skill)
  - [`initializ/forge`](https://github.com/initializ/forge)
  - [`microsoft/SkillOpt`](https://github.com/microsoft/SkillOpt)
  - [`agent-sh/agnix`](https://github.com/agent-sh/agnix)

Visible momentum on 2026-07-17:

- `automl-train-skill` was created on 2026-07-16 and shipped six substantive commits in its first day, including deterministic gates, a failure taxonomy, a zero-GPU end-to-end runner, three backend proofs, and CI. Its two GitHub stars are a weak adoption signal, so it is treated as a fresh mechanism candidate rather than a popularity leader.
- `initializ/forge` had 25 stars and 7 forks in the current GitHub API snapshot and landed a dense series of approval and MCP OAuth commits after the previous run, including per-tool approver allowlists and fail-closed identity resolution.
- `microsoft/SkillOpt` had 12,951 stars and 1,201 forks. A 2026-07-16 fix isolated Codex token tracking and added a regression test against shared-state double counting. This reinforced existing state-isolation lessons but did not warrant a separate new pattern today.
- `agent-sh/agnix` had 348 stars and 29 forks and published versions 0.38.0 through 0.40.0 within the observed window, adding rules for newly changed agent configuration and permissions. It was retained as a fast-update validation-tool signal, but no novel pattern was promoted from release cadence alone.
- ClawHub's updated surface was dominated by fresh or mechanically synchronized entries and metadata-link churn. The download/star surfaces remained led by mature skills such as `self-improving-agent`, `skill-vetter`, and `self-improving`. Cumulative counters were used only for candidate selection because no prior same-surface snapshot was available to prove daily velocity.

---

## Standout Skills And Mechanisms

### `automl-train-skill`: repeated systemic failures stop the budget loop

The skill separates trial-local model failures from systemic data, credential, infrastructure, and schema failures. A deterministic classifier labels failures, and a policy script stops the sweep when consecutive failures share the same systemic cause. The final report preserves the stop reason and supports the honest result that nothing was promoted.

Reusable lesson:

Retry loops should not treat every failure as independent. A skill that spends money, compute, API quota, or user attention needs a code-owned taxonomy that distinguishes retryable local variance from shared causes, then terminates on repeated systemic evidence with an auditable fallback output.

Pattern extracted:

- `PAT-076 Systemic-Failure Budget Circuit Breaker`

### `automl-train-skill`: portability is demonstrated across semantic axes

The repository does not merely claim to be backend-agnostic. Its smoke suite runs the same contract against two different algorithms and a non-Python shell trainer, and exercises both minimize and maximize objective directions. The backend seam is reduced to two explicit adapters: submit a flat environment and scrape a numeric metric.

Reusable lesson:

Cross-platform or backend-neutral claims need a proof matrix. Tests should vary the implementation family, language or host boundary, and semantic polarity—not just run the same happy path through several names.

Pattern extracted:

- `PAT-077 Portability Claim Proof Matrix`

### `initializ/forge`: approval identity is resolved once and enforced centrally

Forge's approval update distinguishes delivery-channel membership from actual authority. Per-tool and default approver email allowlists are normalized, the channel adapter resolves a clicker to the portable identity, and the shared runtime enforces the allowlist even for direct API decisions. Missing or unresolved identity returns `403` and leaves the deferred action pending.

Reusable lesson:

Presentation-layer identity is not an authorization principal. Approval skills should name a cross-channel semantic identity, resolve platform actors to it, enforce authorization in the shared decision boundary, and keep the action pending when identity cannot be proven.

Pattern extracted:

- `PAT-078 Portable Approval Principal Gate`

---

## Local Review Refinements

- Review autonomous loops for a failure taxonomy and a systemic-cause stop policy, not merely a retry count.
- Require budget-consuming skills to return a structured stopped/no-promotion outcome with cause, consumed budget, and safe recovery action.
- Treat portability as a testable claim: require representative hosts or backends, different semantic directions, and at least one language or protocol boundary when applicable.
- Keep adapter seams narrow and explicit so parity tests exercise the shared contract rather than backend-specific internals.
- Separate notification reachability from approval authority. Resolve platform actors to a stable principal and enforce authorization at the shared decision boundary.
- Fail closed on unresolved approver identity while preserving the pending state; never convert identity lookup failure into implicit approval or rejection.
- Continue treating ClawHub cumulative counters and rapid version churn as nomination signals, not day-over-day growth claims.
