---
name: shuxia-skill-library
description: >-
  Use when creating, reviewing, or refining an agent skill and the goal is to
  make the skill more obedient, better bounded, and harder to misuse. Especially
  useful when extracting reusable ideas from strong external skills, turning
  them into boundary rules, constraint patterns, review checklists, and concrete
  revisions for local skills. When the target skill ships scripts or gate
  tools, review those executables too — not only SKILL.md prose.
metadata:
  version: 0.1.6
---

# Shuxia Skill Library

## Overview

This skill is a `skill-for-skills`.

Use it to study why a strong skill behaves well, extract its reusable boundary design, and apply those lessons to improve local skills. The focus is not content quality alone, but whether a skill is:

- clearly bounded
- operationally constrained
- hard to hijack
- easy to trigger correctly
- easy to discover and route correctly at scale
- consistent in output

This skill also acts as a normalization reviewer for new or existing skills in the local library.

When the task is to `create` or `revise` a skill, this skill must behave like a `streaming confirmation writer`:

- ask one scoped confirmation at a time
- wait for the user's answer before asking the next one
- summarize the confirmed decisions before writing
- do not draft or edit the target skill until confirmations are complete

## When to Use

Use when:

- creating a new skill and you want stricter boundaries
- reviewing an existing skill that feels too loose, too generic, or too easy to misuse
- studying an external skill and wanting to absorb its good ideas
- extracting reusable patterns for `scope`, `fallback`, `output contract`, or `anti-slop` behavior
- building a local skill library that should get stronger over time
- rewriting a skill where the desired scope, defaults, or boundaries are still ambiguous and must be confirmed step by step before writing

Do not use when:

- the task is only to explain what a skill says
- the task is only to copy a skill verbatim
- the problem should be solved by code enforcement or tooling instead of documentation
- the user already provided a final approved spec and explicitly asked to skip confirmation

## Adjacent Skills

- `memhub-skill-creator`: use when the primary goal is to create, package, validate, or publish a MemHub-ready skill rather than review or refine skill boundaries
- `self-improvement`: use when the primary goal is to record mistakes, corrections, workflow lessons, or long-term improvement items rather than actively redesign a skill

## Core Principle

A strong skill does not become obedient by sounding strict.

It becomes obedient by turning judgment into structure:

- define what it **is**
- define what it **is not**
- define when it must **stop**, **fallback**, or **ask**
- define what evidence must come **before** generation
- define what output shape is **required**

When a skill stops getting selected reliably as the library grows, treat that as a `routing system` problem first, not a `prompt polish` problem first.

At scale, skill selection behaves like retrieval:

- `name` and `description` act like title and abstract
- trigger conditions act like recall features
- `do not use` rules act like negative constraints
- skill families and folders act like search-space reduction

If a rule is important, it should appear in the workflow, not only in prose.

When the task is skill creation or revision, a strong skill-for-skills must also turn `unclear intent` into a confirmation sequence before any writing begins.

## Review Lens

Always review a target skill across these dimensions:

1. `Identity Boundary`
   - Does the skill clearly say what role it plays?
   - Example: “HTML-native designer, not production frontend engineer.”

2. `Task Boundary`
   - Does it list valid use cases and invalid use cases?
   - Can a caller tell when to route elsewhere?

3. `Execution Boundary`
   - Are the constraints encoded in order?
   - Example: search first, verify assets second, produce output last.

4. `Fallback Boundary`
   - When context is insufficient, does the skill degrade safely?
   - Example: switch to exploration mode instead of hallucinated hi-fi output.

5. `Output Boundary`
   - Does it force a response shape, artifact shape, or evidence format?
   - For image or media-generation skills, does it force exact canvas size and output dimensions?

6. `Anti-Slop Boundary`
   - Does it explicitly block common generic behavior?
   - Example: ban default gradients, fake brand assets, or vague summaries.

7. `Transferability`
   - Is the good idea reusable in other skills, or is it too domain-specific?

8. `Artifact Quality Boundary`
   - For generated files, does the skill define technical validity checks beyond prose quality?
   - For image assets, does it reject wrong canvas size, thumbnail templates, and invalid output dimensions?
   - For gate / DONE artifacts: can an Agent forge the success file by flags alone (honor-system script)?

9. `Routing Discoverability Boundary`
   - Can the skill be found reliably from its `name`, `description`, and trigger wording?
   - Does it describe when to use it, not only what it does?
   - When many neighboring skills exist, is its boundary distinctive enough to reduce collisions?

10. `Executable Gate Boundary`
    - If the skill directory (or referenced templates) ships `scripts/` / gate tools, were those files reviewed?
    - Do SUCCESS/DONE writers require evidence the agent cannot invent in one flag (`--ok true`)?
    - Is a prose ban mirrored by a hard fail in the script, or only by documentation?

## Workflow

### Step 1 — Classify the target skill

Identify:

- what the skill claims to do
- what medium it operates in
- what failure mode it is trying to prevent
- whether it is a `technique`, `workflow`, `reviewer`, `orchestrator`, or `domain skill`
- whether it produces a concrete artifact that needs technical validation such as exact image size
- whether it ships or references **executable gates** (`scripts/`, verify tools, confirm writers, templates under `assets/`)

If executable gates exist, the review **must** open those files in Step 8. Reviewing `SKILL.md` alone is incomplete and must not be scored as a full PASS.

### Step 2 — Decide whether a confirmation gate is required

If the task is `create` or `revise` and any of the following are unclear, you must switch into `Streaming Confirmation Mode`:

- the skill's primary job
- the default execution path
- what the skill must refuse
- whether the skill should ask, fallback, or stop when context is missing
- what artifact the skill should output

If these are already explicit and approved by the user, you may skip the confirmation gate and continue.

### Step 3 — Run Streaming Confirmation Mode

Ask one question at a time. Never dump a full questionnaire at once.

The question sequence should usually confirm:

1. `Primary job`
   - What is the skill mainly for?
2. `Default path`
   - What should it do by default when the user request is brief?
3. `Hard boundary`
   - What must it never do on its own?
4. `Fallback`
   - If required context is missing, should it stop, ask, or switch mode?
5. `Output`
   - What concrete artifact or answer shape must it return?

Rules for this mode:

- ask only one confirmation at a time
- keep each question short and decision-focused
- after each answer, restate the confirmed decision in one sentence
- do not write or rewrite the target skill yet
- if the user changes an earlier decision, update the confirmed state before continuing

### Step 4 — Present a confirmation summary and get final approval

Before writing the skill, output a compact summary:

- `Confirmed Primary Job`
- `Confirmed Default Path`
- `Confirmed Hard Boundary`
- `Confirmed Fallback`
- `Confirmed Output`

Then ask for one final go-ahead.

Do not draft, revise, or patch the target skill until the user confirms this summary.

### Step 5 — Extract boundary mechanisms, not just nice wording

Look for mechanisms such as:

- explicit “use / do not use” lists
- ordered steps
- required evidence sources
- mandatory checkpoints
- canvas or artifact contracts
- fallback modes
- negative lists
- output contracts
- role framing

If a strength is only stylistic, do not over-credit it.
Prefer mechanism over tone.

### Step 6 — Check routing and discoverability before rewriting internals

If the complaint is low hit rate, wrong-skill selection, or missing skill activation, inspect these before changing the skill body:

- `name`
- frontmatter `description`
- trigger scenarios in `Use when`
- negative boundaries in `Do not use when`
- whether neighboring skills sound too similar
- whether the library needs hierarchy instead of a flat list

Hard rules:

- do not only polish the skill body while skipping `name / description / trigger conditions`
- when many skills compete, do not frame the issue as prompt quality alone; analyze it as retrieval, ranking, and constraint design

If evidence is missing, do the smallest safe diagnosis first. Then stop and ask for at least:

- target skill `name`
- target skill `description`
- several adjacent or competing skill samples

### Step 7 — Convert observations into reusable patterns

For every strong idea, rewrite it as:

- `Pattern name`
- `Why it works`
- `Where to reuse`
- `How to encode it in a skill`

Store distilled ideas in [skill-patterns.md](skill-patterns.md).

### Step 8 — Audit the local target skill

When reviewing a local skill, report:

- boundary gaps
- ambiguity points
- loopholes that invite misuse
- rules that exist only in prose but not in flow
- missing fallback behavior
- missing output contract
- missing canvas or artifact validation for generated files
- weak trigger wording that hurts discoverability
- flat taxonomy or overlapping neighbors that hurt routing precision

**Executable-gate sub-audit** (mandatory when `scripts/`, verify/confirm tools, or gate templates exist):

1. List gate scripts and what DONE file each writes
2. Check whether SUCCESS can be produced by agent-supplied booleans alone
3. Check whether required evidence is a real artifact (file hash, API match, non-empty screenshot) vs a free-text claim
4. Severity rule:
   - prose forbids X but script still allows X → prefer **ERROR** (execution loophole), not only “missing Fallback section”
   - missing `Do not use when` while gates are solid → usually **WARNING** (routing), do not outrank forgeable DONE
5. Prefer repairs that harden the script **and** the skill workflow, not documentation-only bans

### Step 9 — Rewrite toward obedience

Prefer these repairs:

- replace vague authority language with explicit routing rules
- rewrite `name` and `description` around trigger scenarios, not just capability labels
- move critical constraints into ordered workflow
- add “do not use when” lists
- add `when not to use` examples when collisions are common
- add fallback modes for missing context
- add output contract sections
- add canvas or artifact contracts when outputs have required technical dimensions
- add anti-pattern or anti-slop sections
- add confirmation gates when the skill is prone to drifting before user intent is locked
- split broad skill families into hierarchy when a flat library causes collisions
- recommend `recall then rerank` routing when the library is too large for full-list selection
- for gate skills: require evidence artifacts in scripts; align Claim vocabulary with DONE; sync templates when scripts change

## Output Contract

When this skill is used for analysis, produce:

- `Skill Type`
- `Primary Boundary`
- `Boundary Mechanisms`
- `What Makes It Obedient`
- `Reusable Patterns`
- `Local Improvements`

When this skill is used to review a local skill, produce:

- `PASS`, `WARNING`, or `ERROR`
- each finding tied to one of the review dimensions
- a concrete rewrite suggestion, not only criticism
- default to a `module-first review`, not a loose issue dump

When this skill is used to review a local skill, the default output format should be:

- `PASS`, `WARNING`, or `ERROR`
- `Current Sections`
- `How Existing Sections Should Change`
- `Missing Sections To Add`
- `Why Each Change Matters`

Rules for this review format:

- start from the target skill's current structure instead of abstract theory
- explain each change in the vocabulary of the target skill's existing sections
- if a section is good, say it should be kept and why
- if a section is weak, say whether it should be tightened, split, or rewritten
- if a section is missing, say where it should be inserted and what job it serves
- do not begin with a generic taxonomy unless the user explicitly asks for one
- findings may still reference review dimensions, but they should be embedded inside the section-based review
- when executable gates exist, include a short `Executable Gate Audit` subsection (scripts reviewed, forge risk, suggested script+prose fix)

When this skill is used to create or revise a skill, the revised skill must include:

- frontmatter with a trigger-focused description
- explicit use / do-not-use scope
- workflow with ordered constraints
- fallback behavior if context is insufficient
- output contract

When the target problem is skill hit rate or routing quality, the rewrite plan must also include:

- `name` and `description` changes that improve retrieval
- trigger-scene wording, not only functional wording
- negative boundary wording for nearby collisions
- hierarchy or family split suggestions when the library is too flat
- retrieval or rerank suggestions when scale makes direct routing unstable

Before the revised skill is written, this skill must produce:

- `Open Decisions`
- `Current Confirmation Question`

Before the revised skill is patched, this skill must produce:

- `Confirmation Summary`
- `Final Approval Check`

## Seed Patterns

The following ideas are already accepted into this library and should be reused when applicable:

- `Role Lock`
  - Declare what the skill is and what it is not.

- `Scope Split`
  - Explicitly separate valid scenarios from invalid scenarios.

- `Constraint In Workflow`
  - Important rules must appear in execution order, not only in principles.

- `Fallback Instead Of Hallucination`
  - When context is weak, switch mode rather than fabricate high-confidence output.

- `Negative List`
  - Ban the most common low-quality defaults explicitly.

- `Evidence Before Output`
  - Require retrieval, assets, or source-of-truth before synthesis.

- `Output Contract`
  - Force the structure of the final answer or artifact.

- `Pattern Harvesting`
  - Strong external skills should be mined for reusable mechanisms, not copied blindly.

- `Confirmation Gate`
  - When creation intent is ambiguous, ask one scoped question at a time and do not write before approval.

- `Canvas Contract`
  - For image-generation skills, exact canvas size and output dimensions must be declared and validated.

- `Trigger Discoverability`
  - Names and descriptions should optimize for retrieval by describing when to use the skill.

- `Hierarchy Before Scale`
  - When many skills compete, route through category layers before final skill selection.

- `Negative Routing Boundary`
  - State not just what the skill does, but which adjacent requests it must not absorb.

- `Recall Then Rerank`
  - At larger scale, retrieve a small candidate set first, then let the model decide among them.

- `Executable Gate Review`
  - When a skill ships scripts that write DONE/SUCCESS artifacts, review those scripts for honor-system bypasses; forgeable DONE is an ERROR-class finding.

- `Evidence-Backed Confirm`
  - Confirm/record scripts must require a real evidence file (or cryptographic/API match), not only `--listed true` flags.

`huashu-design` is a reference example for:

- strong role lock
- scope split
- brand asset protocol
- fallback via design-direction mode
- anti-slop negative lists

`play-store-screenshots` is a reference example for:

- incident-locked negative list (Fastlane SUCCESS ≠ done)
- API SHA evidence before claim
- confirm script requiring `--evidence` file (raises forge bar; still not OCR)
- Claim vocabulary aligned with DONE (no vague「上传成功」)

## Common Mistakes

- Confusing strict tone with real constraint
- Praising wording while missing execution loopholes
- Copying domain-specific rules into unrelated skills
- Writing principles without fallback behavior
- Letting descriptions summarize workflow instead of trigger conditions
- Treating hit-rate problems as body-prompt problems while skipping routing fields
- Keeping dozens of near-duplicate skills in one flat list without hierarchy
- Omitting `when not to use` guidance for skills with nearby overlaps
- Starting to draft the skill before the user has confirmed the core decisions
- Asking five clarification questions at once and then guessing from partial answers
- Reviewing an image-generation skill without checking exact canvas size and output dimension enforcement
- Reviewing only `SKILL.md` when the skill ships `scripts/` or gate templates that write DONE artifacts
- Ranking missing `Do not use when` above forgeable honor-system confirm/SUCCESS writers
- Treating documentation-only bans as fixed when the companion script still accepts `--ok true`

## Real-World Goal

The local skill library should improve over time.

Each good external skill should leave behind reusable boundary patterns so future local skills become more precise, more obedient, and easier to trust.

## Version

Current version: 0.1.6

## Version History

- 0.1.6 - Add Executable Gate Boundary: reviews must audit shipped scripts/templates; forgeable DONE is ERROR-class; prefer evidence-backed confirm over prose-only bans; harvest pattern from play-store-screenshots.
- 0.1.5 - Add adjacent-skill routing split against MemHub skill publishing and self-improvement logging so the skill routes more clearly as a review/refine skill-for-skills.
- 0.1.4 - Fix skill-review output to default to a section-based module review: current sections, how to change them, what to add, and why each change matters.
- 0.1.3 - Add routing discoverability review, scale-aware skill hit-rate analysis, and rewrite rules for names, descriptions, hierarchy, and recall-then-rerank routing.
- 0.1.2 - Add artifact quality review, including mandatory canvas contract checks for image-generation skills.
- 0.1.1 - Add `Streaming Confirmation Mode` so skill creation and revision must ask scoped questions one by one, summarize confirmed decisions, and wait for final approval before writing.
- 0.1.0 - Initial local release as a skill-for-skills reviewer and pattern harvester.
