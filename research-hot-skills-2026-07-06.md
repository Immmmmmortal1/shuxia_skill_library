# Hot Skills Research

Date: 2026-07-06

Scope:

- ClawHub public skills page and `/api/v1/skills` active-update feed
- OpenClaw skills documentation for loading, gating, environment injection, and sandbox caveats
- GitHub topic pages for `agentic-skills`
- GitHub API metadata for current high-momentum skill repositories
- Raw repository artifacts for selected GitHub skill libraries
- Re-check against 2026-07-05 notes to avoid repeating machine-readable manifest and typed mandatory artifact observations

This note records reusable mechanisms, not popularity claims by themselves.

---

## Sources Checked

ClawHub and OpenClaw:

- `https://clawhub.ai/skills`
- `https://hub.openclaw.ai/skills?topic=ai`
- `https://clawhub.ai/api/v1/skills`
- `https://docs.openclaw.ai/tools/skills`
- Selected ClawHub API detail endpoints for `alibabacloud-waf-checkresponse-intercept-query`, `totalreclaw`, `openclaw-master-skills`, and `gingiris-opensource`

GitHub and raw skill sources:

- `https://github.com/topics/agentic-skills`
- GitHub API metadata for:
  - `sickn33/antigravity-awesome-skills`
  - `VoltAgent/awesome-openclaw-skills`
  - `phuryn/pm-skills`
  - `MicrosoftDocs/Agent-Skills`
  - `sudokar/openspec-plus`
  - `frankxai/claude-skills-library`
  - `github/awesome-copilot`
- `https://raw.githubusercontent.com/MicrosoftDocs/Agent-Skills/main/README.md`
- `https://raw.githubusercontent.com/MicrosoftDocs/Agent-Skills/main/skills/azure-functions/SKILL.md`
- `https://raw.githubusercontent.com/sudokar/openspec-plus/main/README.md`
- `https://raw.githubusercontent.com/sudokar/openspec-plus/main/skills/openspec-plus-proposal/SKILL.md`
- `https://raw.githubusercontent.com/sudokar/openspec-plus/main/skills/openspec-plus-apply/SKILL.md`
- `https://raw.githubusercontent.com/phuryn/pm-skills/main/README.md`
- `https://raw.githubusercontent.com/phuryn/pm-skills/main/pm-product-discovery/skills/identify-assumptions-new/SKILL.md`
- `https://raw.githubusercontent.com/phuryn/pm-skills/main/pm-product-discovery/skills/prioritize-assumptions/SKILL.md`
- `https://raw.githubusercontent.com/github/awesome-copilot/main/README.md`
- `https://raw.githubusercontent.com/github/awesome-copilot/main/.schemas/collection.schema.json`
- `https://github.blog/changelog/2026-04-16-manage-agent-skills-with-github-cli/`

Visible momentum on 2026-07-06:

- ClawHub's active-update feed showed newly or recently updated skills with current version churn:
  - `alibabacloud-waf-checkresponse-intercept-query`: 464 downloads, 15 installs, 4 versions, latest update 2026-07-06.
  - `totalreclaw`: 2,499 downloads, 89 installs, 103 versions, latest RC update 2026-07-06.
  - `gh-data`: 374 downloads, 4 installs, 40 versions, latest update 2026-07-06.
  - `kimi-websearch`: new Kimi WebSearch skill with async polling behavior, created and updated 2026-07-06.
  - `openclaw-master-skills`: 4,715 downloads, 166 installs, 14 versions, weekly `+100 skills` update to 2,209 total skills.
- GitHub API confirmed active update signals:
  - `sickn33/antigravity-awesome-skills`: 42,399 stars, pushed 2026-07-05, updated 2026-07-06.
  - `VoltAgent/awesome-openclaw-skills`: 50,955 stars, updated 2026-07-06.
  - `phuryn/pm-skills`: 22,638 stars, pushed 2026-07-03, updated 2026-07-06.
  - `MicrosoftDocs/Agent-Skills`: 630 stars, pushed 2026-07-05, updated 2026-07-05/06.
  - `sudokar/openspec-plus`: 62 stars, pushed and updated 2026-07-05.
  - `github/awesome-copilot`: 36,199 stars, pushed 2026-07-05, updated 2026-07-06.

---

## Standout Skills And Mechanisms

### ClawHub: `alibabacloud-waf-checkresponse-intercept-query`

Why it stood out:

- The latest changelog tightened runtime traceability: each CLI call must carry a unique session id in the User-Agent.
- The previous update also required Aliyun CLI AI-Mode to be enabled at workflow entry and disabled on every exit.
- The skill's domain is operational diagnosis, so traceability and mode cleanup are not polish; they are correctness and blast-radius controls.

Reusable lesson:

Tool-facing skills should treat every external command as a scoped session. If a skill enables a global or semi-global tool mode, it must define entry, exit, error-exit, and trace identifiers. This is stronger than simply saying "use the CLI carefully."

Pattern extracted:

- `PAT-040 Scoped External Tool Session`

### ClawHub: `kimi-websearch`

Why it stood out:

- The skill moved to an async submit-and-poll model.
- Its changelog names progress feedback, fixed poll intervals, timeout handling, API-key errors, submission failure, and task failure.
- This is a useful contrast with simple "call a search API" skills: the main design work is not the request, but the pending/error contract.

Reusable lesson:

Skills that wrap async services need a deterministic wait contract: submit, poll cadence, progress surface, terminal states, timeout, and structured output. Without that, agents either block indefinitely or hallucinate completion.

Pattern extracted:

- `PAT-041 Async Operation Wait Contract`

### ClawHub: `totalreclaw`

Why it stood out:

- The current ClawHub entry is an RC build and explicitly says it is not recommended for production.
- The skill is a memory provider, so persistent state and privacy are core behavior, not peripheral setup.
- Its metadata declares OS compatibility across macOS, Linux, and Windows.

Reusable lesson:

Memory and persistent-state skills need lifecycle maturity labels. A release-candidate memory provider may be fine for evaluation, but production use should require an explicit maturity gate and rollback/export story.

Pattern reinforced:

- `PAT-034 Typed Shared-State Contract`
- `PAT-010 Deterministic Gate`

### ClawHub: `openclaw-master-skills`

Why it stood out:

- It packages a very large skill collection and reports weekly growth to 2,209 skills.
- The useful signal is not the raw count; it is the pressure such packages put on routing, provenance, and manifest quality.

Reusable lesson:

Large aggregate skill packs should not be treated as one installable blob unless they expose category, source, update, risk, and selection metadata. Otherwise they amplify routing collisions and supply-chain uncertainty.

Pattern reinforced:

- `PAT-038 Machine-Readable Discovery Manifest`
- `PAT-031 Context Load Budget`

### GitHub: `MicrosoftDocs/Agent-Skills`

Why it stood out:

- The README frames skills as pre-compiled decisions, procedures, best practices, and constraints from Microsoft Learn rather than raw RAG snippets.
- The repository ships native plugin manifests for multiple hosts.
- Individual generated skills such as `azure-functions` include a category index, official documentation links, generated-at metadata, network/tool requirements, and cross-skill exclusions in the description.

Reusable lesson:

Documentation-derived skills work best when they are compiled into a local routing/index layer, then selectively fetch canonical docs for volatile details. The skill should say what it can decide locally, what it must fetch, and when its generated snapshot is stale.

Pattern extracted:

- `PAT-042 Precompiled Doc Skill With Freshness Gate`

### GitHub: `sudokar/openspec-plus`

Why it stood out:

- It defines phase-owned skills: proposal, spec, design, tasks, apply, and TDD.
- The `proposal` skill explicitly forbids source-code reading because the phase owns intent, not implementation grounding.
- The `apply` skill takes over only vanilla step 6, refuses to modify spec/design from implementation, and gates progress through spec-compliance review before code-quality review.
- It uses update checks, mode questions, dependency analysis, per-slice gates, and strict stop conditions.

Reusable lesson:

Strong workflow skill sets allocate ownership by phase and forbid tempting cross-phase shortcuts. A proposal skill should not quietly become a design skill; an implementation skill should escalate artifact gaps instead of editing upstream artifacts.

Pattern extracted:

- `PAT-043 Phase Ownership Boundary`

### GitHub: `phuryn/pm-skills`

Why it stood out:

- It separates skills, commands, and plugins: skills hold frameworks, commands chain workflows, and plugins package PM domains.
- Product discovery skills use explicit risk categories, perspective switching, and scoring matrices.
- The README documents a cross-platform semantic mismatch: Claude slash commands install, but Codex does not expose them as slash commands, so workflows must be invoked by natural language or converted.

Reusable lesson:

Cross-agent compatibility is not just "files can be copied." The same repository may have different command semantics by host. A portable skill library should state what survives migration unchanged, what degrades, and what adapter/conversion path is needed.

Pattern reinforced:

- `PAT-038 Machine-Readable Discovery Manifest`
- `PAT-043 Phase Ownership Boundary`

### GitHub: `github/awesome-copilot`

Why it stood out:

- The repository spans agents, instructions, skills, hooks, workflows, plugins, tools, and learning materials.
- It exposes `llms.txt` for machine-readable listings.
- Its collection schema caps collection size, restricts item paths/kinds, and forces typed manifest entries.

Reusable lesson:

Mixed artifact libraries need typed collection manifests, not one global list. A collection should declare item kind and path constraints so agents can route to a skill, instruction, hook, workflow, or agent without semantic collapse.

Pattern reinforced:

- `PAT-038 Machine-Readable Discovery Manifest`

---

## Pattern Refinements For Local Reviews

Add these checks when reviewing or writing Shuxia skills:

1. If the skill enables an external tool mode, does it declare entry, cleanup, failure cleanup, and trace identifiers?
2. If the skill wraps an async API, does it define submit/poll/timeout/failure/success states instead of waiting vaguely?
3. If the skill controls persistent memory, does it state maturity, production-readiness, export, rollback, and privacy boundaries?
4. If the skill is documentation-derived, does it separate local stable guidance from fetched volatile documentation?
5. Does generated documentation guidance have a freshness gate such as `generated_at` or a repository version check?
6. Does each phase-owned skill forbid crossing into neighboring phases, and does it escalate gaps rather than silently editing upstream artifacts?
7. For cross-platform repositories, does the documentation say which semantics survive on each host and which features need adapters?
8. For mixed libraries, are artifacts typed by kind before routing: skill, instruction, hook, workflow, agent, command, plugin?

---

## Local Updates

- Updated `skill-patterns.md`:
  - added `PAT-040 Scoped External Tool Session`
  - added `PAT-041 Async Operation Wait Contract`
  - added `PAT-042 Precompiled Doc Skill With Freshness Gate`
  - added `PAT-043 Phase Ownership Boundary`
- Added this dated research note because today's signals produced reusable mechanisms around runtime session boundaries, async completion contracts, doc-skill freshness, and phase ownership.

---
