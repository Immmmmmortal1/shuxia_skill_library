# Hot Skills Research

Date: 2026-07-05

Scope:

- ClawHub search result pages and selected ClawHub skill detail pages
- GitHub topic page for `agent-skills`
- GitHub API metadata for high-momentum skill repositories
- Raw repository artifacts for selected skill libraries and individual skills
- Re-check against 2026-07-04 notes to avoid repeating protected-span, evidence-ledger, and fragile-script-gate observations

This note records reusable mechanisms, not popularity claims by themselves.

---

## Sources Checked

ClawHub and OpenClaw:

- `https://clawhub.ai/tengj/skills/openclaw-hot-skills`
- `https://clawhub.ai/plgonzalezrx8/skills/agent-builder`
- `https://clawhub.ai/nextfrontierbuilds/skills/elite-longterm-memory`
- `https://clawhub.ai/atyachin/skills/lead-generation`
- `https://clawhub.ai/udiedrichsen/skills/stock-analysis`
- `https://hub.openclaw.ai/skills?topic=ai`
- `https://unit42.paloaltonetworks.com/openclaw-ai-supply-chain-risk/`

GitHub and raw skill sources:

- `https://github.com/topics/agent-skills`
- GitHub API metadata for:
  - `sickn33/antigravity-awesome-skills`
  - `wshobson/agents`
  - `github/awesome-copilot`
  - `K-Dense-AI/scientific-agent-skills`
  - `VoltAgent/awesome-agent-skills`
  - `alirezarezvani/claude-skills`
  - `mattpocock/skills`
- `https://raw.githubusercontent.com/sickn33/antigravity-awesome-skills/main/skills_index.json`
- `https://raw.githubusercontent.com/sickn33/antigravity-awesome-skills/main/schemas/skills-index.v1.schema.json`
- `https://raw.githubusercontent.com/sickn33/antigravity-awesome-skills/main/schemas/skill-score.v1.schema.json`
- `https://raw.githubusercontent.com/mattpocock/skills/main/skills/engineering/tdd/SKILL.md`
- `https://raw.githubusercontent.com/mattpocock/skills/main/skills/engineering/implement/SKILL.md`
- `https://raw.githubusercontent.com/K-Dense-AI/scientific-agent-skills/main/skills/literature-review/SKILL.md`

Visible momentum on 2026-07-05:

- GitHub `agent-skills` topic showed several large repositories updated on July 4, including `sickn33/antigravity-awesome-skills`, `github/awesome-copilot`, and `K-Dense-AI/scientific-agent-skills`.
- GitHub API confirmed active update/star signals:
  - `sickn33/antigravity-awesome-skills`: 42,352 stars, pushed 2026-07-04, updated 2026-07-05.
  - `wshobson/agents`: 37,521 stars, updated 2026-07-05.
  - `github/awesome-copilot`: 36,172 stars, pushed 2026-07-04, updated 2026-07-05.
  - `K-Dense-AI/scientific-agent-skills`: 30,149 stars, pushed 2026-07-04, updated 2026-07-05.
  - `VoltAgent/awesome-agent-skills`: 27,321 stars, updated 2026-07-05.
  - `alirezarezvani/claude-skills`: 20,169 stars, pushed 2026-07-03, updated 2026-07-05.
  - `mattpocock/skills`: 156,580 stars, pushed 2026-07-03, updated 2026-07-05.
- ClawHub surfaced recent specialty skills around skill discovery, agent workspace generation, long-term memory, lead generation, and finance analysis. The strongest reusable signal came from the design of the skills, not from the raw popularity numbers.
- Unit 42's June 23 ClawHub research remains important current context: five malicious skills passed available screening at the time, including infostealers, scanner-evasion via file padding, affiliate injection, and agentic front-running. This raises the bar for provenance, network disclosure, and line-by-line audit before recommending installs.

---

## Standout Skills And Mechanisms

### ClawHub: `openclaw-hot-skills`

Why it stood out:

- It turns skill discovery into a workflow with explicit ranking modes: `trending`, `installsAllTime`, `installs`, `downloads`, and topic search.
- It defines fallback behavior when a ranking mode is rate-limited or unavailable.
- It requires deduplication across ranking/search modes and asks the agent to report install status only when verified by local state.
- It has a compact output contract: name, slug, purpose, heat signals, link, install status, and reason to care.

Reusable lesson:

Discovery skills should not simply dump marketplace search results. The durable mechanism is a ranking protocol with declared fallback sources, deduplication, local-state verification, and a stable output contract.

Pattern reinforced:

- `PAT-007 Output Contract`
- `PAT-009 Trigger Discoverability`
- `PAT-010 Deterministic Gate`

### ClawHub: `agent-builder`

Why it stood out:

- It binds an OpenClaw agent to concrete workspace files: `SOUL.md`, `IDENTITY.md`, `AGENTS.md`, `USER.md`, `HEARTBEAT.md`, optional memory files, and dated memory notes.
- It asks for tight clarifying questions before writing an agent, which protects identity boundary and autonomy scope.
- It separates canonical references and templates from the primary workflow.

Reusable lesson:

For agent-construction skills, identity is not one prompt. The output contract should enumerate files by responsibility so persona, operating rules, user preferences, heartbeat behavior, and memory have separate owners.

Pattern reinforced:

- `PAT-001 Role Lock`
- `PAT-002 Scope Split`
- `PAT-012 Output As Artifact`
- `PAT-034 Typed Shared-State Contract`

### GitHub: `sickn33/antigravity-awesome-skills`

Why it stood out:

- The library exposes `skills_index.json` with 1,898 skill entries, rather than depending only on a README list.
- `schemas/skills-index.v1.schema.json` requires path, category, name, description, risk, source, and date fields.
- `schemas/skill-score.v1.schema.json` separates metadata, documentation, and security scores, while declaring that scores are informational and do not automatically block usage.
- The repository has cross-agent/package surface area: plugins, schemas, scripts, skill index, and docs.

Reusable lesson:

Large skill libraries need machine-readable discovery and risk metadata before the model reads individual skill bodies. This improves routing, installer behavior, auditability, and cross-agent semantic stability.

Pattern extracted:

- `PAT-038 Machine-Readable Discovery Manifest`

### GitHub: `mattpocock/skills`

Why it stood out:

- `implement` is intentionally thin and delegates to `/tdd` and `/code-review`, which keeps implementation from becoming a universal mega-skill.
- `tdd` requires tests at pre-agreed public seams, not against internals.
- It explicitly names test anti-patterns: implementation-coupled tests, tautological assertions, and horizontal slicing.
- It asks agents to consult `CONTEXT.md` and ADRs so test vocabulary matches the domain.

Reusable lesson:

High-signal engineering skills often win by being small routers into stricter sub-skills. The strongest boundary is the pre-agreed seam gate: it makes validation meaningful before code is written.

Pattern reinforced:

- `PAT-005 Evidence Before Output`
- `PAT-010 Deterministic Gate`
- `PAT-013 Safe Decomposition`

### GitHub: `K-Dense-AI/scientific-agent-skills` `literature-review`

Why it stood out:

- It has a serious multi-phase workflow: research question, search strategy, multi-database search, deduplication, screening, full-text review, quality assessment, synthesis, and citation verification.
- It records search parameters and selection counts, giving the review an audit trail.
- Its unconditional requirement that every literature review include AI-generated figures is a useful design caution: a hard gate may be valid for some subtypes, but not every subtype.

Reusable lesson:

Mandatory artifacts should be typed by task subtype. For example, PRISMA-style artifacts fit systematic reviews, but short scoping memos may need a search ledger and verified citations instead of generated diagrams.

Pattern extracted:

- `PAT-039 Typed Mandatory Artifact Gate`

### ClawHub Security Context: Unit 42 OpenClaw Supply-Chain Research

Why it stood out:

- Unit 42 documented malicious ClawHub skills that passed available scanning at the time.
- Threat patterns included paste-site prerequisite lures, file padding to evade scanners, dynamic affiliate injection, and coordinated financial manipulation through agentic execution.
- The strongest design implication is not merely “scan packages”; it is “document declared network behavior and compare it with actual outbound behavior.”

Reusable lesson:

Any skill that fetches remote data, asks for prerequisites, or influences money decisions needs a declared network/authority contract. Marketplace badges are weak evidence unless the skill body, package files, and runtime behavior agree.

Pattern reinforced:

- `PAT-032 Portable Provenance Frontmatter`
- `PAT-037 Fragile Operation Script Gate`
- `PAT-038 Machine-Readable Discovery Manifest`

---

## Pattern Refinements For Local Reviews

Add these checks when reviewing or writing Shuxia skills:

1. For discovery or marketplace skills, is the ranking protocol explicit, including fallback sort modes and deduplication?
2. Does the skill distinguish verified local install state from inferred or marketplace state?
3. For agent-builder skills, are identity, operating rules, heartbeat/autonomy, user preferences, and memory stored in separate artifacts?
4. For large libraries, is there a machine-readable index that can be validated before loading many skill bodies?
5. Does risk/quality scoring explain whether it blocks usage or only informs review?
6. For test or validation skills, are seams agreed before tests are written?
7. Are mandatory artifacts tied to task subtype, or does the skill force the same output for every invocation?
8. If a skill fetches remote data or controls money-related advice, are allowed network endpoints and authority boundaries declared?

---

## Local Updates

- Updated `skill-patterns.md`:
  - added `PAT-038 Machine-Readable Discovery Manifest`
  - added `PAT-039 Typed Mandatory Artifact Gate`
- Added this dated research note because today's signals produced two reusable mechanisms around machine-readable discovery and subtype-bound mandatory artifacts.

---
