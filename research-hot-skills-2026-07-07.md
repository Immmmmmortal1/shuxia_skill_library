# Hot Skills Research

Date: 2026-07-07

Scope:

- ClawSkills / ClawHub public discovery pages
- Skills.sh all-time, trending, and hot leaderboards
- GitHub API metadata for newly created or recently active skill repositories
- Raw repository artifacts for selected high-momentum skill libraries
- Re-check against 2026-07-06 notes to avoid repeating async wait, phase ownership, and manifest observations

This note records reusable mechanisms, not popularity claims by themselves.

---

## Sources Checked

ClawHub and public skill indexes:

- `https://clawskills.sh/`
- `https://clawskills.sh/skills/clawd-maf-cad-agent`
- `https://clawskills.sh/skills/varsmallrookie-bluente-translate`
- `https://clawhub.ai/skills`
- `https://hub.openclaw.ai/skills?topic=ai`
- `https://www.skills.sh/`
- `https://www.skills.sh/trending`
- `https://www.skills.sh/hot`

GitHub and raw skill sources:

- GitHub API metadata for:
  - `VoltAgent/awesome-openclaw-skills`
  - `travisvn/awesome-claude-skills`
  - `Orchestra-Research/AI-Research-SKILLs`
  - newly created high-star repositories matching `claude skills created:>2026-06-01`
- Local shallow clones for:
  - `JimLiu/baoyu-design`
  - `amElnagdy/guard-skills`
  - `Kulaxyz/self-learning-skills`
  - `anthropics/launch-your-agent`
  - `mrtooher/fable-mode`
  - `u7079256/paperjury`

Visible momentum on 2026-07-07:

- `VoltAgent/awesome-openclaw-skills`: 50,986 stars, 4,938 forks, updated 2026-07-07, still acting as a high-traffic index over OpenClaw skill discovery.
- `travisvn/awesome-claude-skills`: 13,990 stars, 1,645 forks, updated 2026-07-07.
- `Orchestra-Research/AI-Research-SKILLs`: 10,436 stars, 778 forks, updated 2026-07-06.
- GitHub search for recently created skill repositories surfaced several fast-rising June/July projects:
  - `JimLiu/baoyu-design`: 2,443 stars, created 2026-06-07, pushed 2026-07-02.
  - `amElnagdy/guard-skills`: 968 stars, created 2026-06-06, pushed 2026-07-04.
  - `Kulaxyz/self-learning-skills`: 843 stars, created 2026-06-28, pushed 2026-07-01.
  - `anthropics/launch-your-agent`: 733 stars, created 2026-06-16, pushed 2026-07-02.
  - `mrtooher/fable-mode`: 618 stars, created 2026-06-13, pushed 2026-07-05.
  - `u7079256/paperjury`: 608 stars, created 2026-06-02, pushed 2026-06-30.
- ClawSkills currently exposes a filtered OpenClaw subset and makes risk visible:
  - `cad-agent`: 2.5k downloads, OpenClaw status `Suspicious`, Docker requirement, CAD render/export loop.
  - `bluente-translate`: 159 downloads, OpenClaw status `Benign`, file upload/status-poll/download translation loop.
- Skills.sh trending and hot pages show short-window skill demand around `find-skills`, `just-scrape`, `grill-me`, `grill-with-docs`, Lark document skills, UI taste skills, `agent-browser`, `frontend-design`, `caveman`, and several `mattpocock/skills` / `obra/superpowers` execution-discipline skills.

---

## Standout Skills And Mechanisms

### ClawSkills: `cad-agent`

Why it stood out:

- It is small by star count but already has 2.5k downloads and exposes a clear capability uplift: text-only agents can generate CAD code, render it, inspect a PNG, modify the model, and export STL/STEP.
- The public index labels it `Suspicious` while VirusTotal is benign. The useful signal is the presence of a risk label next to install instructions, not the final risk judgment by itself.
- Its workflow is built around a visual feedback loop rather than a one-shot code generator.

Reusable lesson:

Tool-heavy skills need a visible trust and feedback boundary. If a skill requires Docker, runs code in a rendering server, or emits physical-world artifacts such as printable models, the skill should expose security status and make visual inspection part of completion.

Pattern extracted:

- `PAT-044 Registry Risk Signal`
- `PAT-045 Visual Feedback Loop`

### ClawSkills: `bluente-translate`

Why it stood out:

- It translates PDF/DOCX/PPTX while preserving formatting and batches folders through upload, status polling, and download.
- Its example workflow makes API key, source path, target language, file discovery, polling, and saved outputs explicit.
- Compared with the 2026-07-06 async web-search note, this is a document-pipeline version of the same wait contract.

Reusable lesson:

Document-processing skills should treat "format preserved" as a verifiable pipeline claim, not marketing copy. The skill should name the intake formats, polling lifecycle, output paths, and degraded/failure behavior when a format cannot be preserved.

Pattern reinforced:

- `PAT-041 Async Operation Wait Contract`
- `PAT-012 Output As Artifact`

### Skills.sh: `grill-me`, `grill-with-docs`, and high-trending interview skills

Why they stood out:

- Short-window installs favored skills that slow the agent down before execution: `grill-me`, `grill-with-docs`, and related questioning/planning skills appeared near the top of trending lists.
- The reusable idea is not "ask more questions." It is to turn missing decisions into a bounded, purpose-built interrogation phase with a stop condition.

Reusable lesson:

A high-value confirmation skill should have a limited jurisdiction, one question cluster at a time, and a hard transition back to execution after enough decisions are resolved. Otherwise it becomes ceremonial friction.

Pattern reinforced:

- `PAT-016 Streaming Confirmation Gate`
- `PAT-010 Deterministic Gate`

### GitHub: `JimLiu/baoyu-design`

Why it stood out:

- A broad design skill is kept governable by an orchestrator entry file, harness-specific references, and many built-in sub-skills for deck, wireframe, design system, import/export, Figma, PPTX, and video.
- It requires a design methodology file first, then a runtime/harness reference, then only the relevant built-in skill.
- Its deck flow has unusually concrete artifact contracts: fixed 1920 x 1080 stage, `deck-stage` component, static editable markup, typed animation attributes, wrapper-fill CSS rule, and export-compatible sequencing.
- It also includes a read-only design-system checker subagent whose only job is to run a validation script and report stdout.

Reusable lesson:

Broad creative skills should not rely on one huge instruction body. They need a hub-and-spoke scope split, stable starter components, and read-only validators for fragile artifact quality. The strongest part is not the design taste; it is the way visual work is turned into editable, exportable, and checkable artifacts.

Pattern extracted:

- `PAT-046 Capability Hub With Built-In Subskills`
- `PAT-047 Read-Only Validator Role`

### GitHub: `amElnagdy/guard-skills`

Why it stood out:

- It splits quality review into domain guards: clean code, docs, tests, WordPress, WooCommerce.
- `clean-code-guard` says it should self-invoke after non-trivial production code changes, but excludes conceptual questions, CI, git workflow, prose, data analysis, and test-code review.
- `docs-guard` treats documentation as checkable claims about the codebase and requires symbols, flags, endpoints, config keys, and samples to be verified against source.
- Both skills distinguish guard-pass, live, and review modes.

Reusable lesson:

Quality gates become stronger when split by claim type. Code quality, documentation accuracy, and test quality have different evidence surfaces, so one generic "review" skill should not own them all.

Pattern extracted:

- `PAT-048 Claim-Type Guard Split`

### GitHub: `Kulaxyz/self-learning-skills`

Why it stood out:

- The skill does not harvest every lesson. It requires three promotion conditions before writing a reusable skill: a passing check, a named failure pattern, and at least one ruled-out dead end.
- It separates skill, memory, and skip decisions, defaulting to memory for one-line facts and skipping one-off observations.
- It explicitly forbids secrets in harvested skills and requires dedupe before creating another skill.

Reusable lesson:

Persistent learning needs a promotion gate. Without proof, failure naming, and dead-end capture, "self-learning" turns transient guesses into permanent routing noise.

Pattern extracted:

- `PAT-049 Promotion Rule For Persistent Learning`

### GitHub: `anthropics/launch-your-agent`

Why it stood out:

- It turns a founder-facing workflow into four phases: interview, stage/launch, grade/iterate, run without the user.
- It writes a durable `my-agent/` folder with build-sheet, payloads, `.env`, launch script, evals, overview page, next directions, and IDs.
- It treats the overview HTML as a live schema: planned -> launched -> iterated state, real API fields, Console links, run log, and version rail.
- Credential handling is deliberately staged: warn early, stage keyless artifacts first, accept credentials only through shell/env/file, never chat.

Reusable lesson:

External-platform skills should produce a local control plane. The user needs resumable files, current IDs, evals, and a visual status artifact that maps to real API objects. A chat transcript is not enough state for deployment-grade work.

Pattern extracted:

- `PAT-050 Local Control Plane Artifact`

### GitHub: `mrtooher/fable-mode`

Why it stood out:

- It distinguishes execution discipline from model capability and says the checklist cannot raise a model's reasoning ceiling.
- It uses model-tier calibration: frontier models get lightweight checks, Sonnet runs the full loop, Haiku gets stricter verification and escalation.
- It defines a replan budget and requires each stage to produce a verifiable artifact or merge with a later stage.

Reusable lesson:

Strong process skills should calibrate ceremony to task and model. The same staged loop is overkill for trivial work and insufficient for work beyond the model's synthesis ability; the skill needs both a trigger threshold and an escalation boundary.

Pattern extracted:

- `PAT-051 Calibrated Process Intensity`

### GitHub: `u7079256/paperjury`

Why it stood out:

- It separates direct edit, review, and unattended auto modes.
- It resolves manuscript, venue family, ledger, author, reviewer personas, and style profile at runtime instead of baking paper-specific paths into the skill.
- Review mode keeps durable issue state in `LEDGER.json`, routes issues through deterministic and workflow stages, and requires author sign-off before manuscript edits.
- Hard rules include reviewer isolation, close criteria for valid-fixable issues, no leakage of revision logs into reviewed text, logged overrides, and no hardcoded paths.

Reusable lesson:

High-stakes document skills need a triad: runtime input resolution, durable issue ledger, and human authorization boundary. The skill should track review state and edit permissions separately so "finding a flaw" does not silently become "rewriting the source."

Pattern extracted:

- `PAT-052 Human-Signed Edit Boundary`

---

## Pattern Refinements For Local Reviews

Add these checks when reviewing or writing Shuxia skills:

1. If a registry or index exposes security/risk status, does the skill preserve that signal before installation or execution?
2. If a skill uses generated visual output as evidence, does it require an inspectable render before export or completion?
3. If a skill is broad, does it route through sub-skills and starter components instead of loading all domain detail at once?
4. If validation is delegated, is the validator explicitly read-only and prevented from "fixing" the artifact it judges?
5. If the skill reviews quality, does it split by claim type: code behavior, docs truth, tests, domain security, or deployment?
6. If the skill writes persistent memory or new skills, does it require a passing check, named failure pattern, and ruled-out dead end?
7. If the skill launches or configures an external platform, does it create a local control plane with payloads, IDs, scripts, evals, and a status artifact?
8. If the skill imposes a heavy process, does it define when the ceremony is worth it, when to run a lighter version, and when to escalate?
9. If the skill edits user-owned or high-stakes content, does it separate issue discovery from authorized mutation?

---

## Local Updates

- Added this research note: `research-hot-skills-2026-07-07.md`.
- Added `PAT-044` through `PAT-052` to `skill-patterns.md`.
- Updated `CHANGELOG.md` for the 2026-07-07 daily mining update.

