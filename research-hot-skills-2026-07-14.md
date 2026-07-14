# Hot Skills Research

Date: 2026-07-14

Scope:

- ClawHub public `top`, `updated`, and download-ranked API surfaces
- GitHub repository search, repository metadata, commits since the previous run, and primary skill/docs files
- Incremental comparison against the 2026-07-13 note

This note records reusable mechanisms, not popularity claims by themselves.

---

## Sources Checked

- ClawHub public catalog and `/api/v1/skills` responses for top, recently updated, and download-ranked skills
- GitHub repository search for recently pushed `agent-skills` and `codex-skills` repositories
- GitHub commits and source files for:
  - `mvanhorn/last30days-skill`
  - `OthmanAdi/planning-with-files`
  - `openai/skills`
  - `anthropics/skills`

Visible momentum on 2026-07-14:

- `mvanhorn/last30days-skill`: 51,982 stars and 4,515 forks in the current GitHub API snapshot; pushed on 2026-07-13 with release `v3.14.0` and a substantial discovery-pipeline rebuild.
- `OthmanAdi/planning-with-files`: 25,290 stars and 2,134 forks; release `v3.5.0` on 2026-07-13 added Codex Windows hook work, plan-lifecycle documentation, namespace corrections, and close-marker fixes.
- ClawHub's updated list showed rapid version churn in operational skills such as `investoday-finance-data` (65 versions, 3,184 cumulative downloads), `solo-mission` (21 versions, 1,296 downloads), and `ekyc-suite` (12 versions, 1,002 downloads). These are candidate signals, not proof of day-over-day growth because no prior counter snapshot was available.
- ClawHub's top and download-ranked surfaces remained dominated by mature utilities and self-improvement skills. Their cumulative counters were treated as adoption context, not velocity.

---

## Standout Skills And Mechanisms

### `mvanhorn/last30days-skill`: `last30days` discovery mode

The 3.14.0 release splits discovery into cheap nomination and expensive enrichment. It preserves nomination order when enrichment fails, applies a wall-clock budget, and then requires an absolute evidence floor: either independent cross-source confirmation or a genuinely strong single-source spike. If nothing clears the floor, `nothing-solid` is a first-class output with the closest weak signal; the skill explicitly forbids retrying or fabricating topics around that result.

Reusable lesson:

Ranking is not validation. A top-N list always produces winners even when every candidate is weak. High-integrity discovery skills need an absolute acceptance floor and a valid empty-state contract after ranking.

Pattern extracted:

- `PAT-070 Absolute Confidence Floor With Honest Empty State`

### `OthmanAdi/planning-with-files`: active-plan recovery and closure

The skill persists plan, findings, and progress files across context loss. Its recovery order is explicit: environment-selected plan, active-plan pointer, newest scoped plan, then legacy root files. Recent fixes show why terminality must be stored separately from progress counts: a closed plan now carries a close marker that suppresses both follow-up nags and loop ticks. Selection also uses the plan file's modification time rather than the directory's modification time.

Reusable lesson:

Persistent state is unsafe if selection and termination are implicit. A skill must define which state wins, what timestamp represents freshness, what terminal marker ends automation, and how stale siblings are excluded.

Pattern extracted:

- `PAT-071 Persistent-State Selection And Terminality Contract`

### `OthmanAdi/planning-with-files`: cross-platform parity set

The release describes a 17-file parity set across agent hosts, fixes command namespaces that existed only on some language variants, adds a missing Traditional Chinese command, and keeps some adapters explicitly behind by design. Windows hook changes focus on parseable active-plan pointers and protocol-safe output while preserving the same plan semantics.

Reusable lesson:

Cross-platform support should preserve one semantic contract through explicit adapters and a parity manifest. Platform-specific syntax can differ, but routing names, state precedence, terminal states, and output meaning must remain testable invariants; intentional lag should be declared rather than hidden.

Pattern extracted:

- `PAT-072 Cross-Platform Semantic Parity Manifest`

---

## Local Review Refinements

- For ranked discovery or recommendation skills, ask what absolute condition allows the top result to ship. Relative rank alone is not evidence quality.
- Require a named, user-visible empty outcome when no candidate clears the floor. Do not reward retry loops that manufacture an answer.
- For persistent workflows, review state selection and state termination separately. Completion percentage is not a substitute for a terminal marker.
- Define freshness against the file or record that actually changes, not its container's metadata.
- For multi-host skills, keep a parity manifest of semantic invariants and adapter coverage. Mark intentionally lagging platforms explicitly.
- Treat ClawHub update/download counters as candidate-selection signals unless a prior snapshot supports an actual velocity claim.
