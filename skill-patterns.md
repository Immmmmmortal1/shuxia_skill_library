# Skill Patterns

This file stores reusable skill-design patterns harvested from strong external or local skills.

Use this file as a reference when reviewing or writing new skills.

---

## [PAT-001] Role Lock

**Definition**
State what the skill is, and what it is not.

**Why it works**
Prevents the skill from expanding into neighboring task types.

**How to encode**
- one-sentence identity in Overview
- explicit contrast in scope

**Example source**
- `huashu-design`: HTML-native designer, not production frontend engineer

---

## [PAT-002] Scope Split

**Definition**
Separate valid use cases from invalid ones.

**Why it works**
Makes routing clearer and reduces accidental invocation.

**How to encode**
- `Use when`
- `Do not use when`

---

## [PAT-003] Constraint In Workflow

**Definition**
Critical restrictions appear as ordered steps, not only principles.

**Why it works**
Agents follow steps more reliably than abstract rules.

**How to encode**
- put retrieval, validation, or checkpoint logic before generation

---

## [PAT-004] Fallback Instead Of Hallucination

**Definition**
When context is insufficient, switch to a safer mode.

**Why it works**
Prevents confident low-quality output.

**How to encode**
- “If X is missing, switch to Y mode”
- examples: exploration mode, direction mode, ask-once gate

**Example source**
- `huashu-design`: direction exploration instead of fake hi-fi output

---

## [PAT-005] Evidence Before Output

**Definition**
Require source-of-truth input before synthesis.

**Why it works**
Reduces hallucination and improves traceability.

**How to encode**
- mandate document lookup
- mandate brand asset gathering
- mandate code/context inspection

---

## [PAT-006] Negative List

**Definition**
Explicitly ban common low-quality defaults.

**Why it works**
Many agent failures come from safe generic priors, not from lack of ability.

**How to encode**
- anti-slop list
- common mistakes section

**Example source**
- `huashu-design`: bans generic gradient/icon/data defaults

---

## [PAT-007] Output Contract

**Definition**
Define the required structure of the result.

**Why it works**
Makes responses more consistent and reviewable.

**How to encode**
- fixed sections
- PASS/WARNING/ERROR format
- required evidence items

---

## [PAT-008] Pattern Harvesting

**Definition**
Extract reusable mechanisms from excellent external skills instead of cloning them whole.

**Why it works**
Builds a stronger local library without importing irrelevant domain assumptions.

**How to encode**
- record pattern name
- explain why it works
- note reuse targets

---

## [PAT-009] Trigger Discoverability

**Definition**
Descriptions should optimize for retrieval: concrete triggers, symptoms, and phrases a user would actually say.

**Why it works**
A strong skill that never gets loaded is still a weak system component.

**How to encode**
- trigger-focused frontmatter
- symptom-based `Use when`
- example phrases only when they improve recall

**Example source**
- `agent-skill-creator`: broad but explicit trigger phrase coverage

---

## [PAT-010] Deterministic Gate

**Definition**
Important transitions must be guarded by a clear gate before the agent proceeds.

**Why it works**
Prevents silent drift from “analysis” into “execution”, or from “draft” into “done”.

**How to encode**
- explicit confirm step
- completion gate
- validation gate
- commit gate

**Example source**
- `planning-with-files`: deterministic completion gate

---

## [PAT-011] Validation Companion

**Definition**
Excellent skill ecosystems pair instruction with validation or linting.

**Why it works**
Documentation alone is soft power; validation turns it into enforceable quality.

**How to encode**
- linter
- schema
- tests
- examples or fixtures

**Example source**
- `agnix`: validates SKILL.md, AGENTS.md, hooks, MCP configs

---

## [PAT-012] Output As Artifact

**Definition**
The skill should define not just answer structure, but the concrete artifact it must produce.

**Why it works**
Artifact-driven skills are easier to judge, verify, and reuse.

**How to encode**
- required file
- required plan
- required report
- required generated asset

**Example source**
- `planning-with-files`: persistent markdown plans
- `pptx-generator`: editable PPTX output

---

## [PAT-013] Safe Decomposition

**Definition**
Large or vague tasks should be transformed into smaller controlled subflows, not handled as one monolithic instruction.

**Why it works**
Reduces ambiguity and keeps the agent on rails.

**How to encode**
- classify first
- route second
- generate last
- use master router only when sub-skill boundaries are clear

---

## [PAT-014] Mode Split For Asset Pipelines

**Definition**
Separate `reference retrieval` from `replaceable template composition` when the evidence requirements are different.

**Why it works**
Many image workflows overpromise by treating raw public screenshots as if they were editable local templates. Splitting modes prevents fake geometry inference and keeps the agent honest about what is directly composable.

**How to encode**
- add two named modes with different entry conditions
- make URL-only mode reference-only
- make composition mode require local slot metadata or masks
- refuse replacement when metadata is missing

**Example source**
- `market-reference-pack-generator`: Google Play links are enough for inspiration, but direct screenshot replacement requires local `pack.json` slot metadata

---

## [PAT-015] Passthrough Default For Replacement Tasks

**Definition**
When the user asks to replace, overwrite, swap, or export assets, the default path should be a literal passthrough or direct replacement flow, not a redesigned composition flow.

**Why it works**
Users often mean “do the simple mechanical thing” when they say “替换截图”. If the skill defaults to templates, framing, or layout generation, it silently upgrades the task into design work and breaks trust.

**How to encode**
- classify `replace`, `overwrite`, `swap`, `覆盖`, `直接替换` into a deterministic passthrough mode
- require an explicit named template pack before any composition mode is allowed
- forbid decorative additions in passthrough mode
- add a separate output contract for passthrough results

**Example source**
- `market-reference-pack-generator`: screenshot replacement should default to direct export unless the user explicitly selects a local template pack

---

## [PAT-021] Trigger Discoverability

**Definition**
Skill `name` and `description` should be written for routing recall, not only human readability.

**Why it works**
As the library grows, the router often sees metadata before full skill content. If retrieval fields are vague, a strong skill still gets missed.

**How to encode**
- describe concrete user scenarios
- include phrases a caller would naturally use
- prefer `when to use` wording over abstract capability labels
- keep adjacent skills semantically distinguishable

**Example source**
- skill-routing discussion: `name + description` behave like title and abstract in retrieval

---

## [PAT-022] Hierarchy Before Scale

**Definition**
When many skills compete, organize them into families or routing layers before final selection.

**Why it works**
Flat lists force the model to compare too many near neighbors at once, which makes routing unstable.

**How to encode**
- add top-level categories
- define sub-skill families
- route broad domain first, then specific skill
- document the expected parent category for each skill

**Example source**
- skill-routing discussion: large libraries should narrow search space before detailed selection

---

## [PAT-023] Negative Routing Boundary

**Definition**
A skill should state not only what it handles, but what nearby requests it must not absorb.

**Why it works**
Collisions often happen between related skills, not unrelated ones. Negative boundaries reduce false positives.

**How to encode**
- add `Do not use when`
- add `when not to use` examples
- mention adjacent task types that should route elsewhere

**Example source**
- skill-routing discussion: negative examples reduce accidental activation

---

## [PAT-024] Recall Then Rerank

**Definition**
At larger scale, route by retrieving a small candidate set first, then ranking those candidates.

**Why it works**
Once the library is large enough, skill routing behaves like search. Two-stage selection is more stable than asking one model pass to choose from everything.

**How to encode**
- recall top-k by embeddings, keywords, or trigger phrases
- ask the model to choose only among recalled candidates
- log misses to improve metadata and reranking

**Example source**
- skill-routing discussion: skill routing becomes a retrieval problem at scale

---

## [PAT-016] Streaming Confirmation Gate

**Definition**
When a creation or revision task has unresolved product decisions, the skill must ask one confirmation question at a time and must not start writing until the user approves the confirmed summary.

**Why it works**
Many skill failures come from drafting too early. A streaming confirmation gate prevents silent assumption drift and turns vague intent into approved structure before edits begin.

**How to encode**
- detect unresolved decisions before writing
- ask one short question at a time
- restate each confirmed answer
- produce a confirmation summary
- require one final approval before patching the skill

**Example source**
- `shuxia-skill-library`: skill creation should behave like a superpower-style guided confirmation flow instead of a one-shot draft

---

## [PAT-017] Persistent State

**Definition**
Long-running workflows should store durable state outside model memory.

**Why it works**
Prevents context loss and makes multi-step work auditable.

**How to encode**
- files as memory
- explicit state files
- resumable progress markers

**Example source**
- `planning-with-files`

---

## [PAT-018] Canvas Contract For Generated Images

**Definition**
Image-generation or image-composition skills must declare exact output canvas sizes and enforce them in tooling before reporting success.

**Why it works**
Without a hard canvas contract, low-resolution thumbnails or reference images can be accidentally promoted into final templates. This creates technically invalid assets even when the visual composition appears to work.

**How to encode**
- add a `Canvas Contract` section to the skill
- require `pack.json` or equivalent metadata to declare `canvas.width` and `canvas.height`
- validate every template image against the declared canvas before composition
- validate every output image against the declared canvas before success
- reject thumbnail-sized templates instead of upscaling or silently generating small outputs

**Example source**
- `vvcat-ui-appstore-standard-market`: iOS must be `1284 x 2778`; Android must be `1242 x 2208`
- `market-reference-pack-generator`: Google Play default pack must generate `1242 x 2208` outputs and reject low-resolution templates

---

## [PAT-019] Cross-Platform, Same Semantics

**Definition**
A strong skill may be portable across agent runtimes, but its core semantics must remain stable.

**Why it works**
Portability is valuable only if the behavior contract survives migration.

**How to encode**
- separate platform wrapper from core logic
- keep invariants consistent across exports

**Example source**
- `agent-skill-creator`

---

## [PAT-020] Legal Blocked Exit

**Definition**
Separate “completed successfully” from “stopped safely because a required external condition is unavailable.”

**Why it works**
Without a legal blocked exit, agents either falsely claim completion or leave workflows in ambiguous pending states.

**How to encode**
- define a `Blocked Gate Result`
- require exact blocker source, attempted action, exact error, completed gates, and safe next action
- make validators accept `blocked-valid` as a safe stop, not as completion

**Example source**
- `dev-flow-ui`: real-device launch can be blocked by developer profile trust, while earlier UI gates still remain valid.

---

## [PAT-021] Evidence Packet Levels

**Definition**
Review evidence should be structured by review target instead of using one oversized packet for every call.

**Why it works**
Prevents summary-only reviews while avoiding unnecessary overhead for every small checkpoint.

**How to encode**
- Level A: source evidence and gates
- Level B: Level A plus implementation diff/build evidence
- Level C: Level B plus runtime screenshot/view hierarchy/action history

**Example source**
- `dev-flow-ui`: MCP review packets distinguish preflight/gates, implementation, and final runtime review.

---

## [PAT-022] Ownership Count Split

**Definition**
Element inventory should count app-owned UI separately from system UI, background context, and decorative assets.

**Why it works**
Prevents agents from treating keyboards, background screenshots, or decorative context as missing native controls.

**How to encode**
- app-owned visible element count
- system UI element count
- background/context element count
- decorative asset count
- native app-owned visible element count

**Example source**
- `dev-flow-ui`: separates modal sheet controls from iOS keyboard and background Mine/More context.

---

## [PAT-023] Failure-Mode-First

**Definition**
Start by naming the most common ways a skill is likely to go wrong, then write constraints against those failure modes.

**Why it works**
Many weak skills only describe desired behavior. Stronger skills also defend against predictable bad defaults.

**How to encode**
- add a common failure modes section
- add explicit negative constraints
- turn each repeated failure into a workflow or gating rule

**Example source**
- `andrej-karpathy-skills`: highlights guessing, hidden confusion, overengineering, and unrelated edits

---

## [PAT-024] Surgical Scope

**Definition**
Every change or action should be traceable to the user's goal, with no opportunistic expansion.

**Why it works**
Agents frequently drift by “improving nearby things.” This pattern keeps work tight and reviewable.

**How to encode**
- prohibit unrelated refactors
- require that changes map back to the request
- default to minimal, target-linked edits

**Example source**
- `andrej-karpathy-skills`: “surgical changes”

---

## [PAT-025] Success-Criteria-Driven Execution

**Definition**
Do not only tell the agent what to do. Define what counts as success.

**Why it works**
Success criteria reduce ambiguity and align execution toward verifiable outcomes instead of vague effort.

**How to encode**
- define completion conditions
- define validation expectations
- convert tasks into outcome checks where possible

**Example source**
- `andrej-karpathy-skills`: goal-driven execution

---

## [PAT-026] Assumption Exposure

**Definition**
When multiple interpretations or hidden assumptions exist, the agent must surface them instead of silently picking one.

**Why it works**
Silent assumptions are a major source of drift, misalignment, and expensive rework.

**How to encode**
- require clarification on critical ambiguity
- require explicit statement of assumptions
- ban silent branch selection when it materially affects output

**Example source**
- `andrej-karpathy-skills`: do not guess, expose confusion and inconsistency

---

## Huashu Design Notes

The following ideas are worth reusing from `huashu-design`:

- hard role framing
- precise applicable / non-applicable task split
- brand asset protocol as a pre-generation evidence gate
- safe fallback when context is weak
- anti-slop enforcement through explicit negative lists
- strong emphasis that important rules belong in flow, not just prose

---

## Andrej Karpathy Skills Notes

The following ideas are worth reusing from `andrej-karpathy-skills`:

- define repeated agent failure modes explicitly
- constrain changes to user-goal-traceable scope
- define success criteria, not just commands
- surface assumptions instead of silently guessing

What is more packaging than pattern:

- the “four principles” framing is very effective for communication
- but the deeper reusable value lies in the negative constraints and goal semantics

---

## Hot Skill Market Notes

From ClawHub and GitHub hot skills sampled on 2026-07-01, strong skills repeatedly show:

- strong discoverability
- hard gates around state transitions
- artifact-oriented outputs
- validation or lint support
- explicit decomposition and routing
- persistent state for long workflows
- stable semantics even when exported across agents

---

## [PAT-027] Invocation Class Split

**Definition**
Separate skills by who is allowed to invoke them: explicit user commands orchestrate, model-invoked skills carry reusable discipline.

**Why it works**
It reduces accidental workflow recursion while keeping repeatable sub-discipline available to the agent when the task naturally matches.

**How to encode**
- mark user-only skills with an explicit invocation boundary
- keep router/orchestrator skills user-invoked when possible
- allow model invocation only for narrow, reusable behaviors with strong trigger descriptions
- document which invocation class may call which other class

**Example source**
- `mattpocock/skills`: user-invoked skills orchestrate; model-invoked engineering skills such as debugging, TDD, domain modeling, and design hold reusable process.

---

## [PAT-028] Red-Capable Feedback Gate

**Definition**
Before diagnosing or fixing, require one runnable feedback loop that can fail on the exact target symptom.

**Why it works**
It blocks conclusion-first debugging and turns "I think this is fixed" into an observable pass/fail contract.

**How to encode**
- require the exact command or script path
- require that it has already been run at least once
- require red-capable, deterministic, fast, and agent-runnable properties
- if no loop can be built, stop with tried attempts and needed artifact/access

**Example source**
- `mattpocock/skills` `diagnosing-bugs`: Phase 1 cannot complete without a tight command that can go red on the user's bug.

---

## [PAT-029] Skill Supply-Chain Trust Ladder

**Definition**
Unknown skills must pass source, code, permission, and risk checks before installation or execution.

**Why it works**
Public skill registries are executable instruction supply chains. Popularity and a passing registry badge reduce uncertainty but do not replace local review.

**How to encode**
- source check before install
- mandatory all-file review for untrusted skills
- reject list for credential access, obfuscation, unknown network calls, broad file reads, and elevated permissions
- risk classes with clear actions: install, caution, human approval, or reject
- output a vetting report with files reviewed, permissions, red flags, risk level, and verdict

**Example source**
- ClawHub `Skill Vetter`: trust hierarchy plus red-flag and permission-scope gates.

---

## [PAT-030] Memory Temperature Tiers

**Definition**
Persistent agent memory should be tiered by load frequency and stability instead of kept in one ever-growing file.

**Why it works**
Hot memory stays small and always useful, while project/domain/archive tiers keep history available without bloating every run.

**How to encode**
- HOT: always-loaded, line-limited memory
- WARM: project or domain files loaded on demand
- COLD: archived or decayed patterns
- promotion requires repeated signal, not one-off task context
- expose memory stats and explicit forget/export operations

**Example source**
- ClawHub `Self-Improving + Proactive Agent`: hot `memory.md`, indexed warm project/domain files, cold archive, promotion after repeated patterns.

---

## [PAT-031] Context Load Budget

**Definition**
Treat every always-visible description and rule as a cost; keep only text that changes invocation or execution behavior.

**Why it works**
Skills degrade when trigger prose, reference material, and stale advice accumulate. Budgeting context forces precise triggers, progressive disclosure, and pruning.

**How to encode**
- put only trigger branches in model-facing descriptions
- move branch-specific reference behind context pointers
- delete no-op lines that do not change behavior
- split by invocation or sequence only when the split earns its load cost
- keep one source of truth per behavioral rule

**Example source**
- `mattpocock/skills` `writing-great-skills`: context load, information hierarchy, no-op pruning, and progressive disclosure.

---

## [PAT-032] Portable Provenance Frontmatter

**Definition**
Installed skills should carry source, ref, and content identity metadata inside the skill package itself.

**Why it works**
Agent skills are copied between hosts, projects, and user directories. If provenance only lives in an installer cache, the safety context disappears when the skill is moved. Portable provenance lets update checks, audits, and pinning survive relocation.

**How to encode**
- add repository, ref/tag/commit, and source directory metadata to skill frontmatter
- record a content hash or git tree SHA for the installed skill directory
- support pinned installs that require explicit upgrade
- make update flows compare content identity, not only version text

**Example source**
- GitHub CLI `gh skill`: install/update stores repository provenance and tree SHA in skill frontmatter, supports tag/commit pinning, and compares installed content to upstream changes.

---

## [PAT-033] Evidence-Backed Skill Lifecycle Split

**Definition**
Separate mining repeated workflows, personalizing local skills, and generalizing public skills into different modes or skills.

**Why it works**
The evidence needed to discover a skill is not the same as the evidence needed to adapt it to one user or publish it safely. Splitting the lifecycle prevents private shortcuts from leaking into public artifacts and keeps local optimization grounded in real usage.

**How to encode**
- define separate `mine`, `personalize`, and `generalize` modes
- require session/history evidence before proposing a new skill
- preserve local defaults only in personalization mode
- require privacy stripping, portable examples, install claims, and README checks before publishing

**Example source**
- `hqhq1025/skill-optimizer`: splits `skill-miner`, `skill-personalizer`, and `skill-generalizer` with evidence-backed mining, inward fit, and outward publication boundaries.

---

## [PAT-034] Typed Shared-State Contract

**Definition**
When skills share memory or workflow state, declare the typed entities, read/write permissions, preconditions, and postconditions for each participating skill.

**Why it works**
Shared state becomes unreliable when every skill writes free-form notes. A typed contract turns memory into a validated interface: cross-skill handoffs can be checked before mutation, secrets can be represented by references, and failed constraints can block unsafe writes.

**How to encode**
- define entity and relation types with required fields and enum constraints
- force append/merge rather than overwrite for durable graph state
- declare per-skill reads, writes, preconditions, and postconditions
- validate constraints before committing mutations
- use `secret_ref` style indirection instead of storing credentials directly

**Example source**
- ClawHub `ontology`: typed graph memory with append-only storage, schema validation, relation constraints, and a per-skill ontology contract.

---

## [PAT-035] Protected Span Fence

**Definition**
Before rewriting or transforming user content, identify spans that must not drift: versions, commands, paths, errors, quoted text, numbers, dates, identifiers, citations, and other anchored facts.

**Why it works**
Many useful agent transformations are stylistic or structural, but trust breaks when facts shift. A protected-span fence lets the agent improve the surrounding artifact while keeping factual anchors stable.

**How to encode**
- run protected-span detection before any rewrite
- state which span classes are protected
- prefer the smallest edit that solves the stated problem
- forbid inventing facts, sources, or attitude to make the output smoother
- add a final residue pass that checks protected spans did not change

**Example source**
- ClawHub `humanize-text-skill`: every mode fences protected spans before detecting or rewriting AI-shaped prose.

---

## [PAT-036] Per-Task Evidence Ledger

**Definition**
Long-running repair or quality workflows should create an isolated evidence ledger for each task, plus a structured append-only index for aggregate review.

**Why it works**
Agent work becomes auditable when root cause, tests, regression logs, screenshots, and closure data live with the task instead of being scattered through chat. A central append-only index then supports recurrence detection without overwriting per-task evidence.

**How to encode**
- create a deterministic task id before edits
- isolate evidence under `tasks/{task_id}/` or `bugs/{bug_id}/`
- require root-cause and test-result artifacts before closure
- append structured closure records to an ndjson log
- use atomic writes for shared state and logs
- trigger recurrence or refactor alerts from the structured index

**Example source**
- ClawHub `zero-cover-mode`: per-bug directories, root-cause files, regression logs, ndjson closure records, session registration, atomic writes, and recurrence alerts.

---

## [PAT-037] Fragile Operation Script Gate

**Definition**
When a skill depends on brittle parsing, conversion, validation, or metadata normalization, move the fragile step into a tiny script and require the agent to run the script or validation corpus before claiming success.

**Why it works**
Some tasks are precision operations where natural-language compliance is too weak. Scripts provide deterministic stdout/stderr gates, and conversion corpora expose edge cases that prompt rules miss.

**How to encode**
- identify regex-heavy, parser-heavy, or repetitive boilerplate steps
- ship a single-purpose script under `scripts/` or `lib/`
- require validation before proceeding or before final output
- publish corpus/pass-count evidence when the skill is updated
- make failure self-correcting: read stderr, fix inputs or metadata, rerun

**Example sources**
- ClawHub `sql-splitter`: changelog reports all 312 procedure conversions passing after regex and DDL/DML conversion fixes.
- `mgechev/skills-best-practices` `skill-creator`: validates metadata with a script before drafting the rest of the skill.

---

## [PAT-038] Machine-Readable Discovery Manifest

**Definition**
Large skill libraries should expose a typed discovery manifest and, when possible, a separate quality/risk score schema instead of relying on README prose alone.

**Why it works**
Once a library grows past a small curated set, human-readable lists stop being a reliable routing interface. A manifest lets installers, search tools, review bots, and cross-agent adapters reason about path, category, description, risk, source, date added, and target platforms without scraping free-form markdown.

**How to encode**
- publish an index file with stable ids, paths, categories, descriptions, source, date, and risk fields
- validate the index with JSON Schema or an equivalent typed contract
- keep quality/risk scores informational unless the blocking policy is explicitly documented
- separate discovery metadata from the skill body so routing can happen before context loading
- include compatibility or plugin target metadata for cross-agent installs

**Example source**
- `sickn33/antigravity-awesome-skills`: `skills_index.json` covers 1,898 skills, and `schemas/skills-index.v1.schema.json` plus `schemas/skill-score.v1.schema.json` make discovery and scoring machine-checkable.

---

## [PAT-039] Typed Mandatory Artifact Gate

**Definition**
If a skill requires a mandatory artifact before completion, bind that requirement to the task type and acceptance criteria, not to every invocation of the skill.

**Why it works**
Mandatory artifacts are useful when they prove the work is complete, but they become slop when applied universally. A literature review may need a PRISMA diagram for a systematic review, while a short scoping memo may only need verified citations and a search ledger. Typed gates preserve rigor without forcing decorative or irrelevant output.

**How to encode**
- classify task subtype before applying artifact requirements
- state which subtypes require which artifacts
- define a fallback when the artifact tool or evidence is unavailable
- let the output contract explain why an artifact was included or intentionally omitted
- avoid upgrading optional enhancements into global completion blockers

**Example source**
- `K-Dense-AI/scientific-agent-skills` `literature-review`: strong multi-phase search, screening, quality assessment, and citation verification workflow, but its unconditional figure requirement shows why mandatory artifact gates should be subtype-bound.

---

## [PAT-040] Scoped External Tool Session

**Definition**
When a skill enables or drives an external tool mode, every run must have an explicit session boundary: prerequisite check, mode entry, per-call trace identifier, normal cleanup, and failure cleanup.

**Why it works**
External CLIs often mutate state outside the agent transcript. Session boundaries prevent leaked modes, make logs attributable, and reduce blast radius when a command fails halfway through a workflow.

**How to encode**
- check tool version and required plugins before the first call
- generate a session id once per skill run
- attach the session id or User-Agent to every external call when supported
- define cleanup in every exit path, including errors and user cancellation
- state which tool modes are temporary and must not remain enabled after the skill finishes

**Example source**
- ClawHub `alibabacloud-waf-checkresponse-intercept-query`: requires Aliyun CLI AI-Mode at workflow entry/exit and unique session-id User-Agent handling for traceability.

---

## [PAT-041] Async Operation Wait Contract

**Definition**
Skills that wrap asynchronous services should define a deterministic completion contract: submit, poll cadence, progress reporting, timeout, terminal success, terminal failure, and structured output.

**Why it works**
Async APIs fail badly under vague instructions. Agents either block indefinitely, report too early, or lose error context. A wait contract makes pending state observable and completion auditable.

**How to encode**
- separate submit and poll steps
- specify poll interval and maximum wait
- surface concise progress while waiting
- enumerate terminal states and error classes
- require raw task id, status, and result payload in the final evidence when available
- define fallback behavior for timeout or API-key failure

**Example source**
- ClawHub `kimi-websearch`: async search submission, 5-second polling, progress feedback, timeout, API-key error, submission failure, task failure, and structured JSON output.

---

## [PAT-042] Precompiled Doc Skill With Freshness Gate

**Definition**
Documentation-derived skills should precompile stable decisions, categories, and routing indexes locally, then fetch canonical docs only for volatile details or user-specific implementation questions.

**Why it works**
Raw RAG forces the agent to reinterpret large docs every run. A precompiled skill gives the agent a stable decision surface while a freshness gate prevents stale generated guidance from pretending to be current.

**How to encode**
- include a category index or task map in `SKILL.md`
- distinguish local quick-reference guidance from remote authoritative documentation
- declare required fetch tools and fallback fetch path
- add `generated_at`, source version, or equivalent freshness metadata
- require an update suggestion or remote lookup when the local snapshot is stale
- include cross-skill exclusions in the description to avoid neighboring-service collisions

**Example source**
- `MicrosoftDocs/Agent-Skills` `azure-functions`: generated Azure skill with category index, official Learn links, network/tool requirement, generated-at metadata, and neighboring-service exclusions.

---

## [PAT-043] Phase Ownership Boundary

**Definition**
In a multi-phase workflow, each phase skill should own one phase's artifact and explicitly refuse neighboring phase work, even when that shortcut feels convenient.

**Why it works**
Workflow drift usually starts when a proposal skill designs, a design skill implements, or an implementation skill silently edits upstream specs. Phase ownership keeps artifacts reviewable and makes gaps visible at the right level.

**How to encode**
- name the phase and artifact the skill owns
- list upstream inputs and downstream outputs
- forbid source types that belong to neighboring phases
- define escalation when a gap is discovered outside the current phase
- gate phase completion with the phase's own acceptance checks
- avoid editing upstream artifacts from downstream implementation skills

**Example source**
- `sudokar/openspec-plus`: proposal forbids source-code reading and implementation detail; apply takes over only implementation loop, reviews spec compliance before code quality, and escalates spec/design gaps instead of editing them.

---

## [PAT-044] Registry Risk Signal

**Definition**
When a skill is discovered through a registry or public index, preserve visible risk, audit, provenance, and requirement signals before installation or execution.

**Why it works**
Skill popularity is not a trust signal. Public registries may expose security status, suspicious labels, install commands, external runtime requirements, and audit links. Carrying those signals into the agent workflow prevents a high-download skill from being treated as automatically safe.

**How to encode**
- read registry risk/audit fields before recommending installation
- show security status and runtime requirements near the install step
- require extra confirmation for suspicious, unaudited, or code-executing skills
- distinguish registry metadata from the skill author's own claims
- keep provenance links in the research or install summary

**Example source**
- ClawSkills `cad-agent`: visible OpenClaw `Suspicious` status appears next to install commands, Docker requirement, and VirusTotal status.

---

## [PAT-045] Visual Feedback Loop

**Definition**
For skills that generate spatial, visual, or physical-world artifacts, make an inspectable render part of the work loop before export or completion.

**Why it works**
Code may compile while the artifact is visually wrong. Visual domains such as CAD, UI, animation, charts, slides, and image generation need a feedback artifact that the agent can inspect and revise against before declaring success.

**How to encode**
- generate a render, screenshot, preview, or multi-view image before final export
- inspect the render against the requested geometry, layout, or composition
- iterate from observed render defects, not only code errors
- export final artifacts only after the visual check passes
- keep the render path in final evidence when useful

**Example source**
- ClawSkills `cad-agent`: model creation and modification are followed by PNG render inspection before STL/STEP export.

---

## [PAT-046] Capability Hub With Built-In Subskills

**Definition**
A broad domain skill should act as a routing hub that loads only the relevant methodology, harness reference, and sub-skill for the current task.

**Why it works**
Broad skills become unusable when every mode, edge case, and platform instruction loads at once. A hub-and-spoke design keeps trigger recall broad while execution remains narrow, ordered, and token-efficient.

**How to encode**
- keep the top-level skill as an orchestrator, not the whole handbook
- load core methodology first
- detect the runtime or harness and load its reference once
- load exactly the sub-skill or built-in guide matching the task type
- move deep mode detail into `built-in-skills/`, `references/`, `agents/`, or `starter-components/`

**Example source**
- `JimLiu/baoyu-design`: top-level design skill routes to harness references, design methodology, and task-specific built-in skills for decks, prototypes, design systems, import/export, and media.

---

## [PAT-047] Read-Only Validator Role

**Definition**
Validation subagents or validation modes should be explicitly read-only unless the caller has invoked a separate fixing step.

**Why it works**
Validators are more trustworthy when they cannot mutate the artifact they judge. Separating "report" from "repair" prevents validation from hiding failures by quietly editing files, and makes the main agent own the actual fix.

**How to encode**
- state that the validator must not create, edit, delete, compile, or serve files
- allow only inspection commands and validation scripts
- require stdout or structured report to be relayed without summarizing away details
- return a small health verdict after the raw validation report
- make repair a separate explicit workflow owned by the main agent

**Example source**
- `JimLiu/baoyu-design` `design-system-checker`: read-only validator that runs the checker script, relays stdout, and reports a clean/issues verdict without modifying files.

---

## [PAT-048] Claim-Type Guard Split

**Definition**
Split review skills by the kind of claim being checked: production code behavior, documentation truth, tests, security, domain compliance, or generated artifact quality.

**Why it works**
Different claims need different evidence. Documentation accuracy is checked against source symbols and CLI help; production code quality is checked against diffs, contracts, error handling, and maintainability; tests need failure-mode coverage. A generic review skill tends to blur these surfaces and either overreach or miss domain-specific failures.

**How to encode**
- define one guard per claim type or domain
- put exclusions in the frontmatter description to prevent cross-guard collisions
- provide separate guard-pass, live, and review modes when useful
- require the evidence source appropriate to the claim type
- keep shared principles in references, but keep trigger surfaces distinct

**Example source**
- `amElnagdy/guard-skills`: separates `clean-code-guard`, `docs-guard`, `test-guard`, `wp-guard`, and `woo-guard`, with claim-specific rules and exclusions.

---

## [PAT-049] Promotion Rule For Persistent Learning

**Definition**
Do not turn a session observation into a durable skill or memory unless it passes a promotion rule: verified check, named failure pattern, and ruled-out dead end.

**Why it works**
Self-learning systems fail when they persist confident guesses. Promotion criteria keep the skill library from accumulating one-off notes, unverified folklore, or duplicated workflows that later trigger in the wrong context.

**How to encode**
- require a passing test, successful command, reproduced fix, or other concrete check
- name the failure pattern the new knowledge avoids
- record at least one dead end that was tried and eliminated
- route one-line facts to memory, multi-step reusable workflows to skills, and one-off discoveries to skip
- dedupe against existing skills and memory before writing
- prohibit secret values; store only where to find them

**Example source**
- `Kulaxyz/self-learning-skills`: requires a passing check, named failure pattern, and ruled-out dead end before harvesting a new skill.

---

## [PAT-050] Local Control Plane Artifact

**Definition**
External-platform skills should create a local, resumable control plane containing payloads, IDs, scripts, evals, status, and next directions.

**Why it works**
When a skill launches, configures, or deploys something outside the chat, the transcript is not enough operational state. A local control plane makes the work resumable, reviewable, shareable, and auditable after the session ends.

**How to encode**
- create one deterministic working folder
- write source-of-truth config plus projected API payloads
- save external object IDs as soon as they are created
- include resumable launch or update scripts
- include eval cases or verification artifacts
- maintain a status artifact such as an overview page, dashboard, or run report
- keep credentials out of chat and in a gitignored/env/vault location

**Example source**
- `anthropics/launch-your-agent`: writes `my-agent/` with build sheet, payloads, scripts, evals, `.env`, IDs, overview page, and next-direction plan for a Managed Agent launch.

---

## [PAT-051] Calibrated Process Intensity

**Definition**
Heavy execution loops should define when to run fully, when to run lightly, and when to escalate instead of adding more process.

**Why it works**
The same checklist can be overkill for simple work and insufficient for work beyond the current model or context. Calibrating intensity prevents ceremony from replacing judgment, while still enforcing verification where the model is likely to skip it.

**How to encode**
- name objective trigger thresholds such as multi-file, multi-source, or multi-session work
- define when not to use the loop
- vary verification strictness by model/runtime capability when known
- cap replans or repeated loops
- require every stage to produce a verifiable artifact or merge it into another stage
- escalate when synthesis or requirements ambiguity exceeds what checks can compensate for

**Example source**
- `mrtooher/fable-mode`: calibrates the staged loop by model tier, caps replans, and requires failable checks while admitting that process cannot raise the model's reasoning ceiling.

---

## [PAT-052] Human-Signed Edit Boundary

**Definition**
For high-stakes or user-owned content, separate issue discovery from content mutation and require explicit authorization before applying edits.

**Why it works**
Review findings, rewrite suggestions, and applied changes have different authority levels. Human sign-off prevents an agent from silently converting a critique into source mutation, especially for papers, legal documents, customer-facing materials, and production policies.

**How to encode**
- resolve the working artifact and owner at runtime
- discover or review issues into a durable ledger first
- assign each actionable issue a close criterion
- show patches or proposed edits before applying them
- require explicit author approval, or an up-front bounded policy for unattended mode
- keep revision logs, self-checks, and back-translations outside the edited artifact
- log overrides and unresolved disagreements

**Example source**
- `u7079256/paperjury`: review and auto modes use a durable ledger, close criteria, reviewer isolation, and author sign-off before manuscript edits are applied.

---

## [PAT-053] Recommendation Gate Before Install

**Definition**
Discovery skills should verify fit, trust, and repository health before recommending or installing a found skill.

**Why it works**
Search results optimize recall, not safety or usefulness. A skill that happens to match a keyword may be abandoned, untrusted, low-quality, or a poor fit for the user's actual task.

**How to encode**
- understand the user's domain and task before searching
- check a live leaderboard or registry when one exists
- search only after common high-quality sources are considered
- require objective trust signals such as install count, source reputation, repository stars, recency, or registry status
- present install command, source, and reason to care separately
- when no match exists, say so and offer direct help or skill creation instead of fabricating a recommendation

**Example source**
- `vercel-labs/skills` `find-skills`: checks leaderboard, searches with `npx skills find`, verifies install count/source reputation/GitHub stars, then offers installation.

---

## [PAT-054] Paid Operation Confirmation Gate

**Definition**
Skills that can spend money, consume credits, or trigger billable API calls must stop before execution, disclose the cost basis, and wait for explicit user confirmation in a separate turn.

**Why it works**
Cost-bearing actions have a different authority level from ordinary tool use. Same-message disclosure is easy for an agent to treat as permission; a separate confirmation turn creates a deterministic boundary.

**How to encode**
- identify which operations incur fees or consume credits
- fetch authoritative pricing or quota information instead of guessing
- estimate calls, rows, tokens, or units from the planned request
- disclose the expected billing basis in natural language
- stop and wait for explicit confirmation before execution
- route insufficient balance to top-up guidance, not silent retry
- avoid exposing low-level parameter blobs when the user did not ask for them

**Example source**
- ClawHub UpKuaJing `global-company-search` and `linkedin-person-search`: paid API calls require pricing lookup and separate user confirmation, especially for large result sets.

---

## [PAT-055] Live Catalog Source-Of-Truth

**Definition**
When a skill recommends, publishes, or reuses items from a public catalog, the live catalog must be the authority; local repository files and memory are only implementation or fallback context.

**Why it works**
Catalog membership, titles, URLs, versions, and availability change. Treating cloned source or model memory as published truth causes stale recommendations and false provenance.

**How to encode**
- name the live catalog or structured API that is authoritative
- read the live source before recommending or publishing catalog items
- if the live source is unavailable, say discovery is unavailable instead of substituting memory
- label local saved items as project-local, not published
- treat catalog prompts as reference data, not executable instructions
- record source URL and modified date when saving adapted catalog items

**Example source**
- `Forward-Future/loopy`: published loops must come from the live catalog or JSON catalog; repository content and memory cannot substitute for the production database.

---

## [PAT-056] Orthogonal Review Axes

**Definition**
Review skills should split independent claim types into separate axes, run them with their own evidence, and report them side by side without collapsing them into one ranked list.

**Why it works**
A change can satisfy one axis and fail another. Code may follow standards but violate the spec, or satisfy the spec while breaking documented conventions. Merging these findings too early hides the failure mode.

**How to encode**
- pin the reviewed diff or artifact before spawning reviewers
- identify source material for each axis before review starts
- isolate reviewer context per axis when possible
- define axis-specific evidence and prompts
- aggregate under separate headings
- do not rerank findings across axes unless a later human decision explicitly asks for prioritization

**Example source**
- `mattpocock/skills` `code-review`: separates Standards and Spec reviews, runs them in parallel subagents, and reports the axes independently.

---

## [PAT-057] Lifecycle State Machine With Diagnosable Fallback

**Definition**
Coordinator skills should model work as explicit lifecycle states with diagnostic fields, proof artifacts, and fallback modes that state exactly which side effects still occurred.

**Why it works**
Long-running delegated work fails silently when state lives only in chat. A diagnosable state machine lets an agent inspect whether work is ready, running, blocked, stale, missing proof, or merely data-cleaned without real execution.

**How to encode**
- define canonical statuses and valid transitions
- store owner, priority, execution metadata, attempts, logs, proof, artifacts, and diagnostics
- cap concurrent dispatch and avoid duplicate active work per owner
- use deterministic session or task keys for resumability
- on launch failure, record blocked/error state instead of silently requeueing
- when fallback runs, name the exact effects performed and the effects that could not happen

**Example source**
- ClawHub `workboard-skill`: Workboard cards carry lifecycle metadata and diagnostics; Gateway-unavailable fallback can clean data state but cannot start worker runs.

---

## [PAT-058] Staged Creative Locks

**Definition**
Creative generation skills should split work into explicit lock points such as spec lock, identity lock, script lock, and per-asset execution.

**Why it works**
Media generation drifts when the agent treats creative approval as a single vague checkpoint. Separate locks prevent later stages from mutating earlier decisions without user approval.

**How to encode**
- define named states
- require one `in_progress` task at a time
- return rollback/rework to the matching prior state
- wait for confirmation before moving from spec to identity, identity to script, and script to generation
- generate one asset at a time when outputs are expensive or hard to reverse

**Example source**
- ClawHub `dlazy-image-storyboard`: strict "plan first, render later" workflow with character and script gates

---

## [PAT-059] Routing Precedence Firewall

**Definition**
Large operational skills should define an ordered routing precedence table that maps ambiguous user phrases to one workflow and explicitly forbids near-miss workflows.

**Why it works**
Broad trigger words like "report", "diagnosis", "analysis", "monitoring", or "keywords" can match several workflows. Precedence prevents the agent from choosing the most familiar or easiest route.

**How to encode**
- put highest-priority disambiguation in the frontmatter description and workflow
- name the exact workflow selected by each ambiguous phrase
- add negative route clauses such as "website diagnosis is not market analysis"
- require reading the routing document before execution when the object is unclear

**Example source**
- ClawHub `siluzan-tso`: website diagnosis, market analysis, keyword planning, and account reports are separated by explicit precedence

---

## [PAT-060] Governance Card Pipeline

**Definition**
Governance documentation should be generated from source signals through a structured context object, deterministic rendering, marker cleanup, and validation.

**Why it works**
Safety and trust reviews are weak when the agent freewrites. A pipeline makes evidence, missing fields, and human-review obligations visible.

**How to encode**
- declare read/write/shell permission boundaries
- discover source signals before reading arbitrary files
- build a schema-validated context JSON
- render from a fixed template
- fail if review markers or template fragments remain
- state that human owner/legal/safety review is still required

**Example source**
- `NVIDIA/skills` `skill-card-generator`

---

## [PAT-061] Non-Authority Boundary

**Definition**
Safety-adjacent skills should state what they cannot certify as clearly as what they can check.

**Why it works**
Agents often overstate the meaning of a narrow technical check. A non-authority boundary prevents a preflight, lint, or diagnostic step from being treated as clinical, legal, regulatory, or production clearance.

**How to encode**
- name the exact input/output contract
- forbid replacing vetted upstream tools with handwritten logic
- list non-capabilities in operational terms
- require verifier evidence before treating output as proof
- preserve failed evidence packs for review

**Example source**
- `NVIDIA/skills` `dicom-series-preflight`: header-only DICOM preflight, not de-identification or clinical clearance

---

## [PAT-062] Script-First Domain Workflow

**Definition**
Domain-library skills should default to maintained scripts for common workflows and only drop to custom code when the requested path is outside script coverage.

**Why it works**
Bundled scripts carry stable defaults, file contracts, logging, and validation behavior. Ad hoc code silently loses those guarantees.

**How to encode**
- include a script toolkit table with purpose, inputs, outputs, and typical calls
- make scripts chain through stable artifact formats
- state when custom code is allowed
- route neighboring domains to neighboring skills instead of expanding scope
- pin runtime and package constraints

**Example source**
- `K-Dense-AI/scientific-agent-skills` `scanpy`

---

## [PAT-063] Anti-Rationalization Table

**Definition**
Skills should name the excuses an agent is likely to use to skip required work, then pair each excuse with a concrete counter-rule.

**Why it works**
Agents often fail by rationalizing shortcuts: tests can come later, docs are probably known, the change is too small to verify, or a result "looks right." Naming those shortcuts in advance turns vague discipline into an enforceable guardrail.

**How to encode**
- add a `Rationalizations` or `Common Excuses` section
- list concrete shortcut phrases the agent might use
- pair each phrase with the required action
- connect the counter-rule to a workflow gate or verification step
- keep the table specific to the skill's failure modes instead of generic scolding

**Example source**
- `addyosmani/agent-skills`: every skill anatomy includes rationalizations and verification; `test-driven-development` blocks bug fixes that lack a failing reproduction first.

---

## [PAT-064] Binary Evidence Scoring

**Definition**
Evaluation skills should decompose requirements into atomic binary checks and derive scores from located evidence, not subjective sliders.

**Why it works**
Broad grades invite evaluator drift. Binary checks make disagreement easier to inspect, and `file:line` evidence keeps scores auditable.

**How to encode**
- split each acceptance criterion into MET/UNMET checks
- require `file:line` or equivalent evidence for every MET check
- record the search performed before marking a check UNMET
- score implementation and tests separately when they can fail independently
- derive partial credit from the fraction of checks met

**Example source**
- `tech-leads-club/agent-skills` `spec-driven-eval`: checklist-based scoring with evidence-or-zero and search-before-zero rules.

---

## [PAT-065] Source Hierarchy With Conflict Disclosure

**Definition**
Source-backed implementation skills should define an authority order for sources and require explicit disclosure when authoritative sources conflict with local project practice.

**Why it works**
Current correctness depends on version, framework, and project context. Without a hierarchy, agents cite convenient sources; without conflict disclosure, they silently pick between "modern docs" and "existing codebase" without consent.

**How to encode**
- detect exact stack and versions before fetching references
- rank sources such as official docs, official changelogs, web standards, and compatibility tables
- ban tutorials, forum posts, and model memory as primary authority
- fetch the relevant page, not a generic homepage
- when docs and project code disagree, state the conflict and ask or justify the selected path
- cite the source for framework-specific decisions

**Example source**
- `addyosmani/agent-skills` `source-driven-development`

---

## [PAT-066] Priority Rule Corpus With Progressive References

**Definition**
Domain best-practice skills should rank rule families by impact and load detailed rule examples only when the task needs them.

**Why it works**
Flat checklists make critical correctness rules compete with low-impact polish. Priority ordering guides attention, while referenced rule files preserve detailed incorrect/correct examples without bloating every invocation.

**How to encode**
- define rule categories with priority and impact labels
- put critical categories before high, medium, and low-impact advice
- keep the entry `SKILL.md` compact
- move detailed explanations, wrong/right examples, metrics, and domain notes into `references/`
- use stable rule prefixes or IDs so findings can cite the relevant rule family

**Example source**
- `supabase/agent-skills` `supabase-postgres-best-practices`: eight priority categories and referenced rule files with SQL examples and metrics.

---

## [PAT-067] Publisher-Side Integrity Gates

**Definition**
Skill catalogs should harden publication and installation with content identity, static scanning, path isolation, lockfiles, audit trails, and pinned installs.

**Why it works**
Consumer-side vetting is necessary but late. Publisher-side gates reduce risk before discovery and make later audits possible when a skill is copied, updated, or pinned.

**How to encode**
- require source-only packages or clearly declared binary boundaries
- scan skills before publication
- record content hashes or lockfile identity
- guard path traversal and symlink behavior in installers
- keep an audit trail of installed source, version, and content identity
- support pinning so updates cannot silently overwrite a known-good local copy

**Example source**
- `tech-leads-club/agent-skills`: static analysis, content hashing, lockfiles, path isolation, symlink guards, audit trail, and Snyk Agent Scan before publishing.
- `openclaw/clawhub`: registry supports versioning, changelogs, moderation, trust/capability metadata, and pinned local installs.

---

## [PAT-068] Evidence-Channel Isolation

**Definition**
Independent validators should restrict themselves to declared observable evidence channels and treat implementation access as contamination.

**Why it works**
A reviewer who can see source, diffs, tests, and implementation rationale may validate intended behavior instead of actual behavior. Channel isolation preserves independence and makes pass claims reproducible from a user's or operator's perspective.

**How to encode**
- require a behavior contract before testing
- list allowed surfaces such as UI, CLI, API, generated artifacts, public logs, screenshots, and accessibility trees
- list forbidden evidence such as source, diffs, private tests, git history, and implementation notes
- define a contamination status such as `blocked_source_required`
- use an isolated workspace with only the contract, fixtures, and redacted captures
- run anti-cheat probes that vary data, retry, refresh, and verify persistence or real side effects
- assign every contract clause pass, fail, blocked, or out of scope

**Example source**
- `openclaw/agent-skills` `behavior-validator`

---

## [PAT-069] Semantic-Core Retention Across Handoffs

**Definition**
When a skill routes neighboring infrastructure or presentation work elsewhere, it should retain ownership of the data and behavior invariants that make its own domain artifact correct.

**Why it works**
Clean scope splits can create ownership gaps. If one skill owns generic transport and another owns the domain feature, neither may preserve the exact payload, lifecycle, or compatibility contract across the boundary.

**How to encode**
- name neighboring skills and the work routed to each
- define the local semantic core that must stay in scope
- preserve payload shapes, lifecycle invariants, version floors, and compatibility rules in the domain skill
- require handoff outputs to carry those invariants explicitly
- test the seam between skills, not only each skill in isolation
- keep trigger descriptions concrete enough to distinguish generic infrastructure from domain-specific contracts

**Example source**
- `dpearson2699/swift-ios-skills` `activitykit`: routes ordinary widgets and generic APNs setup away while retaining Live Activity payload and `content-state` invariants.

---

## [PAT-070] Absolute Confidence Floor With Honest Empty State

**Definition**
Ranked discovery and recommendation skills should apply an absolute evidence threshold after relative ranking and treat “nothing qualified” as a valid final outcome.

**Why it works**
A ranking algorithm always produces a first place, even when every candidate is noise. An absolute floor prevents polished weak signals from becoming false trends, recommendations, or conclusions.

**How to encode**
- separate cheap candidate nomination from deeper evidence enrichment
- define measurable acceptance paths such as independent cross-source confirmation or an exceptional single-source spike
- apply the floor after enrichment, not only to seed rank
- preserve a named weak signal for diagnosis without promoting it to a result
- define a first-class empty outcome and forbid retrying, padding, or fabricating around it
- make shallow mode explicit and keep the same minimum floor

**Example source**
- `mvanhorn/last30days-skill` `last30days` v3.14.0 discovery mode: nominate, enrich, floor, then emit `nothing-solid` when no topic qualifies.

---

## [PAT-071] Persistent-State Selection And Terminality Contract

**Definition**
Persistent workflow skills should define deterministic state-selection precedence, the freshness signal used for fallback selection, and an explicit terminal marker that stops all automation.

**Why it works**
Multiple saved states create ambiguity after context loss. Progress counts alone cannot distinguish a completed-but-retained state from an active one, and container timestamps can select stale siblings.

**How to encode**
- order state resolution, for example explicit environment id, active pointer, newest scoped state, then legacy fallback
- validate state identifiers before resolving paths
- measure freshness on the mutable state artifact, not merely its directory
- store terminality separately from progress percentage
- make every nag, loop, resume hook, and recovery path stop on the terminal marker
- test stale-sibling, closed-state, missing-pointer, and cross-session recovery cases

**Example source**
- `OthmanAdi/planning-with-files` v3.5.0: active-plan precedence, file-mtime recovery, and close-marker-aware follow-up and loop termination.

---

## [PAT-072] Cross-Platform Semantic Parity Manifest

**Definition**
Skills that ship across agent hosts, operating systems, or language adapters should maintain a manifest of shared semantic invariants and adapter coverage, including intentional lag.

**Why it works**
Copying similar files creates the appearance of portability while routing names, state recovery, terminal behavior, or output protocols silently diverge. A parity manifest makes semantic drift reviewable without forcing identical syntax.

**How to encode**
- declare one canonical semantic contract for routing, state, side effects, and output meaning
- list every host, OS, and language adapter covered by the release
- test adapter-specific syntax against the shared invariant set
- keep protocol output parseable and platform-safe
- record missing adapters and intentionally lagging variants explicitly
- require namespace and command-name parity checks before release

**Example source**
- `OthmanAdi/planning-with-files` v3.5.0: a documented 17-file parity set, Windows protocol fixes, language-command namespace correction, and explicitly lagging adapters.
