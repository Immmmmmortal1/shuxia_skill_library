# Hot Skills Research

Date: 2026-07-20

Scope:

- ClawHub public updated, download-ranked, and star-ranked API surfaces
- GitHub repository search, metadata, commits, diffs, tests, and primary documentation since the previous run
- Incremental comparison against the 2026-07-17 note

This note records reusable mechanisms, not popularity claims by themselves.

---

## Sources Checked

- ClawHub `/api/v1/skills` responses sorted by update time, downloads, and stars
- GitHub primary repository and commit evidence for:
  - [`SlanchaAI/ingot`](https://github.com/SlanchaAI/ingot)
  - [`RudrenduPaul/evolveguard`](https://github.com/RudrenduPaul/evolveguard)
  - [`initializ/forge`](https://github.com/initializ/forge)
  - [`SVGreg/skill-guard`](https://github.com/SVGreg/skill-guard)
  - [`TerminalSkills/skills`](https://github.com/TerminalSkills/skills)

Visible momentum on 2026-07-20:

- `ingot` shipped a dense 2026-07-19 series covering deterministic acceptance criteria, graded promotion gates, cross-model compatibility sweeps, evidence-rich two-step human promotion, and broader tests. Its one GitHub star is weak adoption evidence, so it is treated as a fast-moving mechanism candidate rather than a popularity leader.
- `evolveguard` was created on 2026-07-15, published matching npm and PyPI CLIs, and added a deterministic capability-surface regression pipeline with tests in its first days. Its one star is also weak adoption evidence.
- `forge` rose from 25 to 26 stars in the current snapshots and added durable delegated-consent artifacts plus Slack delivery after the previous run. The one-star change is directional but too small to establish a robust growth rate by itself.
- `skill-guard` was created on 2026-07-17 and released a signing, attestation, trust-roster, and bundle-integrity toolchain by 2026-07-19. This reinforces existing publisher-side integrity guidance rather than creating a distinct pattern today.
- `TerminalSkills/skills` had 114 stars and 12 forks and added a Claude Code plugin/marketplace surface. The release is a useful distribution signal, but its mechanism overlaps existing replicated-metadata and publisher-integrity patterns.
- ClawHub's updated surface was again dominated by fresh or mechanically revised entries, including repeated suites and low-install uploads. Mature skills still led cumulative downloads and stars. Those counters and update timestamps were used for nomination only because they do not prove day-over-day velocity.

---

## Standout Skills And Mechanisms

### `ingot`: invariants participate in search and remain sovereign at promotion

Per-skill forbidden-output criteria are evaluated deterministically. Violations are fed into the optimizer's inner-loop score so search receives actionable pressure, then recomputed on held-out answers at the promotion boundary. Pervasive violations block promotion; minority violations remain visible warnings for human review. A better mean judge score cannot override a blocking invariant.

Reusable lesson:

For self-rewriting or optimizing skills, a hard rule used only at the final gate wastes search budget, while a rule used only as training feedback can be reward-hacked or forgotten. Encode the same invariant in both places, keep the final check deterministic and independent, and define explicit block/warn semantics from evidence prevalence.

Pattern extracted:

- `PAT-079 Invariant Feedback And Promotion Sovereignty`

### `evolveguard`: narrow fixtures are backed by a whole-surface drift check

Each fixture may project the skill's capability surface down to the tools and scopes relevant to one prompt. The final diff separately compares the complete declared-and-inferred capability surface, so a newly added network or filesystem capability cannot disappear merely because no fixture selected it. Duplicate findings are filtered when the local and global checks catch the same change.

Reusable lesson:

Selective scenarios make validation understandable, but selection creates blind spots. Pair focused contract projections with a completeness backstop over the whole safety-relevant surface, then deduplicate findings without weakening either verdict.

Pattern extracted:

- `PAT-080 Focused Projection With Whole-Surface Backstop`

### `forge`: durable recovery path precedes best-effort notification

Forge now publishes the delegated-consent URL on the parked task's A2A `auth-required` artifact before attempting Slack delivery. Slack is an additive push channel: a missing user, missing scope, or delivery failure is logged but does not remove the durable link or prevent the callback from resuming the parked call.

Reusable lesson:

Human-interaction workflows should not make an ephemeral delivery channel the sole holder of recovery state. Persist the action, subject, expiry, and continuation reference on the canonical workflow object first; then fan out notifications as replaceable hints.

Pattern extracted:

- `PAT-081 Durable Recovery Anchor Before Notification Fan-Out`

The same Forge change added a cancel-clicker guard, but identity lookup failure can still allow cancellation in its current DM-only threat model. That exception was not promoted into a reusable authorization pattern; `PAT-078 Portable Approval Principal Gate` remains the stronger fail-closed rule for authority decisions.

---

## Local Review Refinements

- Review self-optimizing skills for invariant placement at both candidate-search time and final promotion time.
- Keep deterministic promotion gates sovereign over aggregate LLM-judge improvements; preserve blocked candidates for diagnosis without permitting activation.
- If violation prevalence controls block versus warning, declare the denominator, threshold boundary, minimum sample count, and zero-sample behavior.
- Pair fixture-scoped or scenario-scoped checks with a whole-surface backstop for capabilities, permissions, side effects, and other safety-relevant dimensions.
- Deduplicate overlapping local/global findings only after both checks have run; never use deduplication to erase coverage metadata.
- Persist recovery-critical human-interaction state on the canonical task before attempting email, chat, push, or webhook delivery.
- Treat notification adapters as replaceable fan-out channels, not as the source of truth for pending actions or continuation state.
- Continue treating ClawHub cumulative counters, repeated suite updates, and fresh zero-install uploads as nomination signals rather than proof of fast adoption.
