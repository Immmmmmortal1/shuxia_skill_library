# Hot Skills Research

Date: 2026-07-04

Scope:

- ClawHub front page and `/api/v1/skills` active-update feed
- Selected ClawHub skill detail payloads for newly created or recently updated skills
- GitHub repository pages and GitHub API metadata for current high-momentum skill repositories
- Re-check against 2026-07-02 and 2026-07-03 notes to avoid repeating provenance, lifecycle split, shared-state, and memory-tier patterns

This note records only mechanisms that add reusable skill-design value.

---

## Sources Checked

ClawHub:

- `https://clawhub.ai/`
- `https://clawhub.ai/api/v1/skills`
- `https://clawhub.ai/api/v1/skills/zero-cover-mode`
- `https://clawhub.ai/api/v1/skills/humanize-text-skill`

GitHub and raw skill sources:

- `https://github.com/addyosmani/web-quality-skills`
- `https://raw.githubusercontent.com/addyosmani/web-quality-skills/main/skills/web-quality-audit/SKILL.md`
- `https://github.com/hashicorp/agent-skills`
- `https://github.com/OthmanAdi/planning-with-files`
- `https://github.com/mgechev/skills-best-practices`
- `https://raw.githubusercontent.com/mgechev/skills-best-practices/main/skill/SKILL.md`
- `https://github.com/VoltAgent/awesome-openclaw-skills`
- `https://github.com/VoltAgent/awesome-agent-skills`
- `https://github.com/anthropics/skills`

Visible momentum on 2026-07-04:

- ClawHub front page has shifted its visible positioning toward registry governance: signed manifests, moderated releases, version history, ownership, docs, package integrity, install/scan/publish/verify, and trust signals.
- ClawHub `/api/v1/skills` showed multiple same-day updates and new skills. Notable active items included `sql-splitter` with 1,312 downloads and 36 versions, `humanize-text-skill` as a fresh release, and `zero-cover-mode` as a fresh rigorous bug-fix workflow.
- `OthmanAdi/planning-with-files` remained a large active planning skill signal: GitHub API showed 24,443 stars, 2,102 forks, updated 2026-07-04, and pushed 2026-07-03.
- `addyosmani/web-quality-skills` showed 2,452 stars, updated 2026-07-03, and uses a category/router split for performance, Core Web Vitals, accessibility, SEO, and best practices.
- `mgechev/skills-best-practices` showed 2,091 stars and a compact skill-creator that validates metadata, keeps `SKILL.md` lean, and moves fragile logic into scripts.
- `hashicorp/agent-skills` showed 697 stars and an organization-maintained product/plugin/skill hierarchy for Terraform and Packer skills.

---

## Standout Skills And Mechanisms

### ClawHub: `humanize-text-skill`

Why it stood out:

- It frames humanization as editing, not classification. The skill explicitly says AI-tone findings are signals, not proof.
- It runs protected-span detection before every mode so commands, paths, versions, errors, quotes, and anchored facts do not drift.
- It has three modes with different output expectations: detect-only, rewrite, and edit-in-place.
- It uses scene packs and voice profiles, but blocks copying facts or opinions from a sample voice.

Reusable lesson:

Any style-changing skill needs a factual stability layer before the style layer. This applies beyond writing: migration notes, release notes, bug reports, PR summaries, compliance text, and generated documentation all need protected anchors before prose cleanup.

Pattern extracted:

- `PAT-035 Protected Span Fence`

### ClawHub: `zero-cover-mode`

Why it stood out:

- It treats a bug fix as a durable evidence object, not just a patch.
- It creates a per-bug directory with root cause, test result, regression output, evidence attachments, and optional revert logs.
- It appends structured closure events to `FIX_CLOSURE_LOG.ndjson` and uses central state only through atomic read-modify-write flows.
- It forces a root-cause artifact before code changes, a real execution result before closure, and recurrence/refactor alerts from aggregate logs.
- It includes explicit fallback modes for projects without known test frameworks, VCS, or Python.

Reusable lesson:

For repair workflows, the output contract should include the evidence ledger, not only the code change. Persistent state is safer when local task folders hold rich evidence and the shared index stores only structured summaries.

Pattern extracted:

- `PAT-036 Per-Task Evidence Ledger`

### ClawHub: `sql-splitter`

Why it stood out:

- Its latest ClawHub changelog reports conversion-specific fixes around schema-prefix handling, bracket identifier replacement, statement semicolons, and type keyword ordering.
- The useful signal is the validation story: it reports all 312 procedure conversions passing after the transformation changes.
- This is a precision skill where a prose instruction cannot reliably cover all parser and regex edge cases.

Reusable lesson:

Skills that perform brittle mechanical transformations should expose a deterministic validation corpus. A version update should say what corpus passed, not only what wording changed.

Pattern extracted:

- `PAT-037 Fragile Operation Script Gate`

### GitHub: `mgechev/skills-best-practices`

Why it stood out:

- The `skill-creator` skill validates metadata with `scripts/validate-metadata.py` before drafting the rest of the skill.
- It moves fragile/repetitive operations into tiny CLI scripts and uses stdout/stderr as the correction channel.
- It treats `SKILL.md` as a lean router and moves bulky material into flat `references/`, `assets/`, or deterministic `scripts/`.

Reusable lesson:

Validation should happen at the earliest point where bad structure can still be cheap to correct. For skill authoring, metadata is not a finishing detail; it is the routing interface.

Pattern refined:

- Reinforces `PAT-037 Fragile Operation Script Gate`
- Reinforces `PAT-031 Context Load Budget`
- Reinforces `PAT-009 Trigger Discoverability`

### GitHub: `addyosmani/web-quality-skills`

Why it stood out:

- The repository splits broad web quality into narrower skills: audit, performance, Core Web Vitals, accessibility, SEO, and best practices.
- The audit skill has explicit severity levels and an output contract with Critical/High/Medium/Low findings, impacts, fixes, summary, and priority order.
- It includes a Lighthouse v13 compatibility note that separates stable advice from changing report names.

Reusable lesson:

Cross-platform semantic stability is not just directory compatibility. Skills should distinguish stable concepts from tool-version-specific labels, especially when their evidence source changes naming or report shape.

No new pattern was added because this extends `PAT-013 Safe Decomposition`, `PAT-007 Output Contract`, and `PAT-031 Context Load Budget`.

### GitHub: `hashicorp/agent-skills`

Why it stood out:

- It uses an organization/product/plugin/skill hierarchy instead of a flat skill pile.
- Individual skills can be installed directly, while plugins group product workflows.
- This structure carries product ownership and domain boundaries into the package layout.

Reusable lesson:

For large official libraries, hierarchy is part of the routing contract. Product and plugin layers reduce semantic collision before the model sees individual skill descriptions.

No new pattern was added because this extends `PAT-002 Scope Split`, `PAT-013 Safe Decomposition`, and `PAT-031 Context Load Budget`.

---

## Pattern Refinements For Local Reviews

Add these checks when reviewing or writing Shuxia skills:

1. If the skill rewrites user content, what spans are fenced before any stylistic edit?
2. Does the skill distinguish signal from verdict when classifying text, security, quality, or intent?
3. If the skill fixes bugs or performs long-running repair, where is the per-task evidence ledger stored?
4. Does shared workflow state use atomic append/update semantics instead of free-form overwrite?
5. If the skill performs brittle transformation, what script, corpus, or pass-count proves the transformation?
6. Are stable domain concepts separated from version-specific labels in the tool output the skill reads?
7. For large libraries, does folder hierarchy reduce routing collisions before descriptions compete?

---

## Local Updates

- Updated `skill-patterns.md`:
  - added `PAT-035 Protected Span Fence`
  - added `PAT-036 Per-Task Evidence Ledger`
  - added `PAT-037 Fragile Operation Script Gate`
- Added this dated research note because today's ClawHub active-update feed produced concrete new mechanisms around factual stability, task evidence ledgers, and deterministic transformation gates.

---
