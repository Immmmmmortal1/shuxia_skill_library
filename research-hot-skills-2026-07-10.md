# Hot Skills Research

Date: 2026-07-10

Scope:

- GitHub topic and repository metadata for fast-rising agent skill libraries
- GitHub API repository, commit, release, tree, and decoded `SKILL.md` evidence
- ClawHub ecosystem and registry evidence from public ClawHub repository and recent security research
- Re-check against 2026-07-09 notes to avoid repeating staged creative locks, routing precedence, governance cards, non-authority boundaries, and script-first domain workflows

This note records reusable mechanisms, not popularity claims by themselves.

---

## Sources Checked

ClawHub and OpenClaw:

- `openclaw/clawhub` README and GitHub API metadata
- `VoltAgent/awesome-openclaw-skills` README and GitHub API metadata
- Unit 42 ClawHub supply-chain research, published 2026-06-23

GitHub topic and repository sources:

- GitHub topic page `codex-skills`, sorted by stars
- GitHub API metadata and recent commits for:
  - `addyosmani/agent-skills`
  - `tech-leads-club/agent-skills`
  - `supabase/agent-skills`
  - `sickn33/agentic-awesome-skills`
  - `Egonex-AI/Understand-Anything`
  - `Yuan1z0825/nature-skills`
  - `alirezarezvani/claude-skills`
  - `VoltAgent/awesome-agent-skills`
  - `VoltAgent/awesome-openclaw-skills`
- GitHub release metadata for:
  - `addyosmani/agent-skills`
  - `tech-leads-club/agent-skills`
  - `supabase/agent-skills`
- GitHub tree and decoded contents for:
  - `addyosmani/agent-skills` `test-driven-development`
  - `addyosmani/agent-skills` `source-driven-development`
  - `tech-leads-club/agent-skills` `skill-architect`
  - `tech-leads-club/agent-skills` `spec-driven-eval`
  - `supabase/agent-skills` `supabase-postgres-best-practices`

Visible momentum on 2026-07-10:

- `addyosmani/agent-skills`: 75,903 stars, 8,165 forks, pushed 2026-07-09 and updated 2026-07-10. Latest recent release was `0.6.3` on 2026-07-03. Recent commits refined scope notes and documentation policy.
- `sickn33/agentic-awesome-skills`: 42,734 stars, 6,793 forks, pushed 2026-07-09 and updated 2026-07-10. Recent commits included repository audit hardening.
- `tech-leads-club/agent-skills`: 4,853 stars, 439 forks, pushed 2026-07-07 and updated 2026-07-09. Releases were frequent: `skills-catalog-v0.15.1` on 2026-07-07 and `skills-catalog-v0.15.0` on 2026-07-04.
- `openclaw/clawhub`: 9,121 stars, 1,422 forks, pushed 2026-07-09 and updated 2026-07-10. The README frames ClawHub as a public skill registry with versioning, search, star/comment surfaces, moderation hooks, pinning, and package metadata.
- `VoltAgent/awesome-openclaw-skills`: 51,072 stars, 4,944 forks, updated 2026-07-10. README states it filters 5,400+ OpenClaw skills from the official registry and warns that listed skills are not security audited.
- GitHub `codex-skills` topic showed 703 public repositories. High-star, recently updated standouts included `Egonex-AI/Understand-Anything` at 72.3k stars, `sickn33/agentic-awesome-skills` at 42.7k, `VoltAgent/awesome-agent-skills` at 27.7k, and `Yuan1z0825/nature-skills` at 27.4k.

---

## Standout Skills And Mechanisms

### GitHub: `addyosmani/agent-skills`

Why it stood out:

- The repository applies a consistent anatomy across 24 lifecycle skills: overview, trigger conditions, process, rationalizations, red flags, and verification.
- The README makes "process, not prose" a design requirement: skills are workflows with steps, checkpoints, and exit criteria.
- `test-driven-development` encodes RED/GREEN/REFACTOR and a bug-fix "prove it" loop. A passing test is not enough unless a failing reproduction existed first.
- `source-driven-development` defines a source hierarchy, requires exact stack/version detection, bans non-authoritative primary sources, and forces conflict disclosure when official docs and project code disagree.
- The design adds an explicit anti-rationalization section: common agent excuses are named in advance and paired with counter-arguments.

Reusable lesson:

Strong engineering skills should defend against the agent's predictable shortcuts, not only describe the ideal workflow. The highest-leverage mechanism is to name common rationalizations, force a red-capable proof loop, and end with non-negotiable evidence.

Patterns extracted:

- `PAT-063 Anti-Rationalization Table`
- `PAT-065 Source Hierarchy With Conflict Disclosure`

### GitHub: `tech-leads-club/agent-skills`

Why it stood out:

- The README positions the catalog as a hardened library rather than an open marketplace: open-source-only skills, static analysis, content hashing, lockfiles, path isolation, symlink guards, audit trail, and pre-publish scanning.
- The catalog has 82 `SKILL.md` files and frequent releases, suggesting a maintained registry rather than a one-off prompt collection.
- `skill-architect` forces Discovery -> Architecture -> Craft -> Validate -> Deliver, with explicit exit criteria before moving phases.
- `spec-driven-eval` has `disable-model-invocation: true`, making evaluation explicitly user-invoked instead of auto-triggered.
- `spec-driven-eval` decomposes acceptance criteria into atomic binary checks, requires `file:line` evidence for every met check, records search-before-zero attempts, and scores implementation and tests separately.

Reusable lesson:

Evaluation skills need reproducibility mechanics. Binary checks with located evidence are stronger than broad grades, and sensitive evaluator skills should be explicit-invocation only to avoid accidental scoring or recursive workflow activation.

Patterns extracted:

- `PAT-064 Binary Evidence Scoring`
- `PAT-067 Publisher-Side Integrity Gates`

### GitHub: `supabase/agent-skills`

Why it stood out:

- The repo is narrower than general catalogs: two Supabase skills, with official Supabase ownership and release artifacts.
- `supabase-postgres-best-practices` prioritizes rule categories by impact: query performance, connection management, and security/RLS are critical before lower-impact monitoring or advanced features.
- The skill pushes detailed examples into referenced rule files, each with explanation, incorrect SQL, correct SQL, optional `EXPLAIN` or metrics, and Supabase-specific notes.
- The README describes `.well-known/agent-skills/` release artifacts and `dist/index.json`, turning discovery into a structured publication surface rather than a README-only convention.

Reusable lesson:

Domain best-practice skills should not be flat checklists. They should rank rules by impact, keep the entry skill compact, and put detailed examples into on-demand references that preserve incorrect/correct examples and metrics.

Pattern extracted:

- `PAT-066 Priority Rule Corpus With Progressive References`

### ClawHub / OpenClaw ecosystem

Why it stood out:

- `openclaw/clawhub` presents registry-level features that matter for skill design: versioning, changelogs, search, stars/comments, moderation, pinning local installs, and package trust/capability metadata.
- `VoltAgent/awesome-openclaw-skills` aggregates 5,400+ registry skills but explicitly warns that the collection does not audit or guarantee listed projects.
- Unit 42's 2026-06-23 research found that even after ClawHub added proactive screening, malicious skills persisted, including infostealers, scanner evasion through inflated file size, and agentic affiliate/front-running threats.

Reusable lesson:

Popularity and registry presence are weak trust signals. Skill libraries need both consumer-side vetting and publisher-side integrity gates. The publisher side should make provenance, content identity, scanning, and install pinning inspectable before a user or agent executes anything.

Pattern reinforced:

- `PAT-029 Skill Supply-Chain Trust Ladder`
- `PAT-067 Publisher-Side Integrity Gates`

---

## Pattern Refinements For Local Reviews

- Add an "agent excuse" pass to review checklists. If a skill routinely needs tests, docs, or verification, ask whether it names the excuses an agent will use to skip them.
- For evaluator skills, prefer binary evidence checks over subjective numeric rubrics. Partial credit should be derived from atomic checks, not judged directly.
- For source-backed implementation skills, require a source hierarchy and a conflict rule. The skill should say what to do when official docs, migration guides, and local code disagree.
- For domain rule corpora, inspect priority order. Critical safety/performance rules should not sit beside low-impact polish as equal checklist items.
- For public catalogs, distinguish consumer vetting from publisher hardening. A local review skill should ask for both.
