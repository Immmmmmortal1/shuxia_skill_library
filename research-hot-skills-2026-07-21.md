# Hot Skills Research

Date: 2026-07-21

Scope:

- ClawHub public updated, download-ranked, and star-ranked API surfaces
- GitHub repository metadata, commits, diffs, tests, and primary documentation since the previous run
- Incremental comparison against the 2026-07-20 note

This note records reusable mechanisms, not popularity claims by themselves.

---

## Sources Checked

- ClawHub `/api/v1/skills` responses sorted by update time, downloads, and stars
- GitHub primary repository and commit evidence for:
  - [`tsirou694-prog/flowprint`](https://github.com/tsirou694-prog/flowprint)
  - [`platypeeps/se-ai-command-pack`](https://github.com/platypeeps/se-ai-command-pack)
  - [`hangglider5/skill-crash-test-arcade`](https://github.com/hangglider5/skill-crash-test-arcade)
  - [`JasonColapietro/suede-creator-skills`](https://github.com/JasonColapietro/suede-creator-skills)

Visible momentum on 2026-07-21:

- `flowprint` was created on 2026-07-20 and shipped its first public release plus two merged quality and submission-readiness changes within roughly one day. The repository still had no stars in the current snapshot, so commit density is treated as a mechanism-discovery signal rather than adoption proof.
- `se-ai-command-pack` merged a new `se-help` discovery skill and its validation fixes on 2026-07-21 while continuing several same-day packaged-skill updates. Its current GitHub counters were also negligible, so the finding rests on implementation and test evidence, not popularity.
- `skill-crash-test-arcade` was created on 2026-07-20 and added a deterministic demo workflow on 2026-07-21. Its isolated public/private test design and claim calibration are strong, but they mainly reinforce `PAT-068 Evidence-Channel Isolation` and `PAT-080 Focused Projection With Whole-Surface Backstop` rather than justify another pattern.
- `suede-creator-skills` had 45 stars and 8 forks and continued a dense 2026-07-20–21 release series around packaging, public-policy checks, advisory gates, and validator coverage. The gate-severity changes are useful evidence for keeping declared policy aligned with actual enforcement, but the reusable mechanism overlaps existing deterministic-gate and replicated-metadata guidance.
- ClawHub's updated surface again mixed a few active skills with repeated low-install suites and fresh zero-install uploads. Mature skills still dominated cumulative downloads and stars. Without a saved prior counter snapshot, those counters nominate candidates but do not establish daily velocity.

---

## Standout Skills And Mechanisms

### `flowprint`: generated contracts retain field-level evidence lineage

Flowprint's compiler now emits six required execution sections, including inputs, missing-information behavior, output contract, checks, and permission boundaries. Statements in those sections carry the IDs of confirmed classification items. The generated manifest records the corresponding dependency edges, and the validator rejects missing sections, thin sections, omitted item IDs, absent dependency edges, or an output contract that contains no requirement text derived from a Core or Domain item.

Reusable lesson:

Template completeness is not enough for generated skills. A generator should preserve field-level lineage from approved source facts into executable sections, then validate both the rendered claim and its dependency edge. This makes unsupported specificity and silent omission diagnosable without pretending that structural validation proves real-world usefulness.

Pattern extracted:

- `PAT-082 Provenance-Bearing Generated Contract`

### `se-help`: catalog membership is reconciled with runtime discoverability

The pack generates its catalog from registry metadata and canonical skill frontmatter, then asks `se-help` to reconcile that packaged inventory with the current session's capability inventory. It uses distinct labels for available now, included but not discoverable now, intentionally not installed, planned but not shipped, and external or unknown. If a bundled skill is missing at runtime, the skill reports observed versions and routes to the native status/update path instead of guessing the cause or claiming availability.

Reusable lesson:

A generated catalog proves what a distribution contains, not what the current agent can invoke. Discovery skills should join static ownership metadata with live exposure state and preserve the disagreement as a first-class result. Recommendations and copy-ready triggers must be limited to capabilities actually exposed in the current session.

Pattern extracted:

- `PAT-083 Catalog-To-Runtime Availability Reconciliation`

---

## Local Review Refinements

- For generated skills, require every operational section to cite approved source-item identities rather than relying on plausible template prose.
- Validate both rendered inclusion and dependency-graph inclusion; either one alone can hide unsupported or silently dropped requirements.
- Keep structural-contract validation claims narrow: passing proves shape and lineage, not usefulness, correctness, or field performance.
- Treat package membership, installation receipt, host discovery, and current-session exposure as separate states.
- Require discovery and routing skills to label static/live disagreement explicitly and avoid recommending unavailable capabilities as immediately runnable.
- Generate catalogs from canonical frontmatter or registry metadata, but reconcile them against live capability inventory before producing a trigger or handoff.
- Continue treating ClawHub cumulative counters and update timestamps as nomination signals unless prior snapshots make the delta measurable.
