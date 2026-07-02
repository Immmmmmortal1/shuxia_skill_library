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

**Example source**
- `awesome-gamedev-agent-skills`: master router concept

---

## [PAT-014] Persistent State

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

## [PAT-015] Cross-Platform, Same Semantics

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

## [PAT-016] Legal Blocked Exit

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

## [PAT-017] Evidence Packet Levels

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

## [PAT-018] Ownership Count Split

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

## [PAT-019] Failure-Mode-First

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

## [PAT-020] Surgical Scope

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

## [PAT-021] Success-Criteria-Driven Execution

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

## [PAT-022] Assumption Exposure

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

## [PAT-023] Invocation Class Split

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

## [PAT-024] Red-Capable Feedback Gate

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

## [PAT-025] Skill Supply-Chain Trust Ladder

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

## [PAT-026] Memory Temperature Tiers

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

## [PAT-027] Context Load Budget

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
