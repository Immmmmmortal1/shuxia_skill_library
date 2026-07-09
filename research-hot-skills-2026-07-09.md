# Hot Skills Research

Date: 2026-07-09

Scope:

- ClawHub active-update feed and selected skill details
- GitHub API metadata for fast-moving skill repositories
- Raw GitHub/API contents for selected high-signal skills
- Re-check against 2026-07-08 notes to avoid repeating paid-operation gates, live catalog gates, and lifecycle fallback patterns

This note records reusable mechanisms, not popularity claims by themselves.

---

## Sources Checked

ClawHub:

- `https://clawhub.ai/api/v1/skills?sort=updated&limit=20`
- `https://clawhub.ai/api/v1/skills/dlazy-image-storyboard`
- `https://clawhub.ai/api/v1/skills/siluzan-tso`
- `https://clawhub.ai/api/v1/skills/dlazy-kling-audio-clone`

GitHub and raw repository sources:

- GitHub API metadata for:
  - `NVIDIA/skills`
  - `K-Dense-AI/scientific-agent-skills`
  - `anthropics/skills`
  - `VoltAgent/awesome-agent-skills`
  - `VoltAgent/awesome-openclaw-skills`
- Raw or API-decoded skill contents for:
  - `NVIDIA/skills` `skill-card-generator`
  - `NVIDIA/skills` `dicom-series-preflight`
  - `NVIDIA/skills` `nemo-rl-session-memory`
  - `K-Dense-AI/scientific-agent-skills` `scanpy`
- Repository README evidence for:
  - `NVIDIA/skills`
  - `K-Dense-AI/scientific-agent-skills`
  - `anthropics/skills`
  - `VoltAgent/awesome-agent-skills`
  - `VoltAgent/awesome-openclaw-skills`

Visible momentum on 2026-07-09:

- ClawHub active-update feed showed same-day updates across the Dlazy media-generation family. Standouts included `dlazy-image-storyboard` with 1,955 downloads, 68 installs, and 14 versions; `dlazy-kling-v3` with 1,887 downloads, 65 installs, and 14 versions; and `dlazy-kling-audio-clone` with 1,872 downloads, 64 installs, and 14 versions.
- `siluzan-tso` was updated the same day to version `1.1.36`, with 1,388 downloads, 41 installs, and 26 versions. Its changelog added a dedicated user communication guide and refined routing/operation instructions.
- `NVIDIA/skills`: 2,319 stars, 268 forks, pushed 2026-07-08, updated 2026-07-09. The README positions the repo as official NVIDIA-verified skills, mirrored daily from product repos.
- `K-Dense-AI/scientific-agent-skills`: 30,494 stars, 3,071 forks, pushed 2026-07-08, updated 2026-07-09.
- `anthropics/skills`: 159,496 stars, 18,833 forks, updated 2026-07-09.
- `VoltAgent/awesome-openclaw-skills`: 51,038 stars, 4,937 forks, updated 2026-07-09; README states it filters 5,400+ OpenClaw skills from the official registry.
- `VoltAgent/awesome-agent-skills`: 27,633 stars, 2,956 forks, updated 2026-07-09; README lists 1,000+ cross-agent skills and warns that listed projects are not security-audited.

---

## Standout Skills And Mechanisms

### ClawHub: `dlazy-image-storyboard`

Why it stood out:

- The skill makes "plan first, render later" a mandatory state machine rather than a style preference.
- Step 0 requires a task plan with requirements, character design, script gate, image generation, and final assembly.
- Only one task may be `in_progress` at a time, and rollback/rework must return the workflow to the relevant state.
- The character master sheet is a deterministic drift-control gate: visual identity is approved before script generation.
- Images are generated only after script approval, and generation is single-command, synchronous, and one asset at a time.
- It explicitly bans saving prompts to ad hoc files, asking the user to use third-party generation platforms, background commands, chained commands, and bulk generation.

Reusable lesson:

Creative generation skills need staged creative locks. The useful boundary is not "ask for approval sometimes"; it is to split creative work into spec lock, identity lock, script lock, and asset-by-asset execution, with rollback returning to the correct state.

Pattern extracted:

- `PAT-058 Staged Creative Locks`

### ClawHub: `siluzan-tso`

Why it stood out:

- The description functions as a routing firewall. High-risk ambiguous words such as report, diagnosis, analysis, monitoring, website, industry, and keyword planning are mapped to named workflows with explicit precedence.
- It repeatedly forbids near-miss routes: website diagnosis cannot drift into market analysis or account diagnosis; industry reports cannot be replaced by pure web search; keyword planning cannot fabricate search volume.
- It requires the agent to read a central conventions document first, then the intent-routing document when ambiguity appears, then the one selected workflow's required documents.
- It separates user-facing communication constraints from CLI mechanics: final answers should be conclusion-first and should not mechanically paste commands or workflow IDs.

Reusable lesson:

When a skill controls a large operational surface, the description must carry routing precedence, not just a list of supported commands. Negative route constraints are as important as positive triggers because they prevent the agent from turning broad words like "report" into the wrong workflow.

Pattern extracted:

- `PAT-059 Routing Precedence Firewall`

### GitHub: `NVIDIA/skills` `skill-card-generator`

Why it stood out:

- It is scoped narrowly: generate or refresh a governance card for an existing skill directory, not explain skills, create skills, publish cards, or replace legal/safety review.
- It declares read, write, and shell permissions in frontmatter and repeats the permission boundary in workflow steps.
- It requires structured discovery before reading arbitrary excerpts, then builds a JSON context and renders a deterministic markdown card.
- Credential classification is constrained to a two-field schema and controlled vocabulary. The skill explicitly forbids raw credential values, assignments, and environment variable names.
- It uses marker cleanup and template-fragment checks as deterministic completion gates before submission.

Reusable lesson:

Governance skills should make trust work auditable. The pattern is source signals -> structured context -> deterministic rendering -> unresolved-marker validation -> human owner review, with permissions constrained throughout.

Pattern extracted:

- `PAT-060 Governance Card Pipeline`

### GitHub: `NVIDIA/skills` `dicom-series-preflight`

Why it stood out:

- The skill is explicit that it performs header-only preflight and is not de-identification, clinical clearance, autonomous diagnosis, or production ingestion.
- It tells the agent to use the documented wrapper rather than handwrite an implementation.
- It names manifest I/O, expected JSON output, verifier pairing, engineering invariant gates, and evidence pack retention on validation failure.
- Limitations are operationally specific: no pixel decoding, no burnt-in PHI detection, compressed transfer syntax warned not decoded, single-directory scan.

Reusable lesson:

Medical, regulated, or safety-adjacent skills should encode non-capabilities as first-class boundaries. A preflight skill is safer when it proves a narrow engineering invariant and refuses to imply clinical or compliance authority.

Pattern extracted:

- `PAT-061 Non-Authority Boundary`

### GitHub: `NVIDIA/skills` `nemo-rl-session-memory`

Why it stood out:

- It defines durable working-session memory as a local repo artifact, not model memory.
- It has a clear use/not-use boundary: long-running work, handoffs, disconnects, branch switches, and nontrivial edits; not simple questions, one-off commands, linting, or code review.
- It specifies file contracts for `session_state.md`, `timeline.md`, `files.md`, and `handoff.md`, plus a checkpoint rhythm.
- It warns that session notes are not source of truth and must be verified against git state, files, and command output.

Reusable lesson:

Persistent state should be compact, inspectable, and explicitly demoted from authority. Memory artifacts help resumption, but the workflow must verify them before acting.

Pattern reinforced:

- `PAT-017 Persistent State`

### GitHub: `K-Dense-AI/scientific-agent-skills` `scanpy`

Why it stood out:

- The skill routes neighboring domains: use `anndata` for structure/I/O, `scvi-tools` for probabilistic models, and `rapids-singlecell` for GPU-accelerated operations.
- It prefers bundled scripts over ad hoc code for common analysis stages, because scripts preserve defaults, file chaining, progress logging, and raw-count handling.
- It includes current runtime/version constraints and warns that R-native single-cell objects must be converted with R tooling before Scanpy use.
- The repository README adds installation provenance and reproducibility guidance through `npx skills add`, `gh skill install`, agent targeting, and pinning by release tag or commit SHA.

Reusable lesson:

Domain-library skills should split "standard path" from "customization path." The default path should run maintained scripts with stable file contracts; customization is allowed only when the requested analysis is outside script coverage.

Pattern extracted:

- `PAT-062 Script-First Domain Workflow`

---

## Pattern Refinements For Local Reviews

- For marketplace and catalog skills, add a provenance check: what source installed the skill, can it be pinned, and does the installer record enough metadata to later audit or update it?
- For large operational skills, inspect trigger precedence before internal prose. If several workflows share words like "report" or "diagnosis", the skill needs a precedence firewall.
- For creative media skills, require stage-specific confirmation gates. One generic "confirm before generation" rule is weaker than separate spec, identity, script, and asset gates.
- For regulated domains, prefer narrow wrappers with verifier evidence over broad diagnostic authority. A skill should name what it cannot certify.
- For persistent state, require both artifact schema and verification rhythm. Resumability without source-of-truth demotion can turn stale notes into false authority.
