# Hot Skills Research

Date: 2026-07-15

Scope:

- ClawHub public updated, download-ranked, and star-ranked API surfaces
- GitHub repository search, metadata, commits since the previous run, and primary source files
- Incremental comparison against the 2026-07-14 note

This note records reusable mechanisms, not popularity claims by themselves.

---

## Sources Checked

- ClawHub `/api/v1/skills` responses sorted by update time, downloads, and stars
- GitHub repository metadata, commit history, diffs, tests, and skill/docs files for:
  - `NVIDIA/SkillSpector`
  - `Agents365-ai/drawio-skill`
  - `google/skills`
  - `microsoft/SkillOpt`

Visible momentum on 2026-07-15:

- `NVIDIA/SkillSpector`: 13,176 stars and 1,067 forks in the current GitHub API snapshot; its 2026-07-14 OSS release bundled fixes for recursive report completeness, documentation false positives, provider isolation, SARIF metadata, and multiple security analyzers.
- `Agents365-ai/drawio-skill`: 5,778 stars and 463 forks; the 2026-07-14 update added six workflow scripts and then fixed distribution-version drift with a regression test and fail-closed sync workflow.
- `google/skills`: 14,797 stars and 1,136 forks; four commits after the prior run added two multi-agent data workflows and updated cloud skills. It was inspected as a momentum candidate, but no additional pattern was promoted without deeper evidence beyond the new content volume.
- ClawHub's updated surface showed extreme version churn in entries such as `canonry` (390 versions, 6,266 cumulative downloads), `travel-planner-notion-ai-obsidian-kontour-integration` (103 versions, 3,552 downloads), and several career/insurance skills above 120 versions. These remain candidate signals only: cumulative versions and downloads do not establish day-over-day adoption velocity.
- ClawHub's download-ranked surface remained led by mature utilities such as `self-improving-agent`, `skill-vetter`, and `self-improving`. Their counters were used as adoption context, not evidence of today's growth.

---

## Standout Skills And Mechanisms

### `NVIDIA/SkillSpector`: recursive scan reports preserve verdict coverage

The current scanner distinguishes static-only from LLM-backed analysis and reports whether the requested semantic pass actually ran. Its recursive JSON fix preserves the full per-skill report payload—including components, issues, scan scope, and `analysis_completeness`—instead of collapsing each child to a score and finding count. Tests cover valid full payloads, malformed or non-object report bodies, and per-skill errors.

Reusable lesson:

A verdict is not portable when its coverage disappears during aggregation. Every security, quality, or compliance conclusion should carry the evidence channels used, components examined, completeness, and degraded-mode status through both single-item and batch outputs.

Pattern extracted:

- `PAT-073 Coverage-Bearing Verdict`

### `NVIDIA/SkillSpector`: documentation suppression proves negative space

The static runner now suppresses a narrow allowlist of lexical rules only when the match is in prose or a comment and lacks execution signals. It explicitly excludes `SKILL.md` from this suppression, keeps executable twins detectable, and tests both safe documentation and dangerous negative-space cases such as environment reads, subprocess calls, YAML run steps, and code hidden in markdown.

Reusable lesson:

False-positive suppression should be a proof obligation, not a broad file-type exemption. A suppressor must name the rules it governs, prove the non-executable context, preserve protected control files, and test near-identical executable counterexamples.

Pattern extracted:

- `PAT-074 Negative-Space Suppression Gate`

### `Agents365-ai/drawio-skill`: distribution metadata parity fails closed

The repository publishes the same skill through multiple distribution surfaces. A recent fix corrected a stale distributed version, changed the sync workflow from warnings to errors when the source version or marketplace entry cannot be parsed, expanded CI path triggers to include the skill and sync workflow, and added a regression test asserting that top-level and embedded metadata versions match.

Reusable lesson:

Replicated skill metadata is part of the routing and installation contract. When one canonical version is copied into registries, plugin manifests, or host-specific adapters, synchronization must be derived from the canonical source, validated across every replica, and fail closed when parsing or target lookup breaks.

Pattern extracted:

- `PAT-075 Replicated Metadata Parity Gate`

---

## Local Review Refinements

- Treat every verdict as a tuple of conclusion plus coverage. Batch aggregation must not strip scan mode, evidence scope, completeness, or child errors.
- Review fallback outputs for claim strength: static-only or partial scans may still report findings, but must not masquerade as full clean scans.
- Require suppression logic to prove non-executability and to enumerate the exact rules it may suppress. Broad `docs/` or extension exemptions are too permissive.
- Add negative-space tests around every suppression gate: the same phrase in prose, comments, executable code, structured run steps, and protected control files.
- When skill metadata is replicated across hosts or catalogs, designate one canonical field, derive replicas mechanically, and make parse/lookup failures block release.
- Continue treating ClawHub cumulative counters as candidate-selection signals until prior snapshots support an actual velocity claim.
