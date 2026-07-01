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

## [PAT-016] Failure-Mode-First

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

## [PAT-017] Surgical Scope

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

## [PAT-018] Success-Criteria-Driven Execution

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

## [PAT-019] Assumption Exposure

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
