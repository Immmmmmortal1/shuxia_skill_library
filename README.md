# shuxia-skill-library

A reusable skill-review and skill-design library for people who want to build more obedient, better-bounded, and more trustworthy agent skills.

The goal of this repository is simple:

- help people create skills that are easier to trigger correctly
- help people define sharper boundaries
- help people encode constraints into workflow, not just prose
- help people design safer fallback behavior
- help people produce more stable output contracts

Instead of treating a skill as "just a prompt", this library treats a skill as a behavior contract.

## What is inside

- [`SKILL.md`](./SKILL.md)
  - the main review skill
  - used to analyze, normalize, and strengthen other skills

- [`skill-patterns.md`](./skill-patterns.md)
  - reusable patterns harvested from strong skills
  - includes patterns for scope, gating, fallback, validation, portability, and output contracts

- [`research-hot-skills-2026-07-01.md`](./research-hot-skills-2026-07-01.md)
  - a research note based on hot skills from ClawHub and GitHub
  - summarizes the common traits of popular, high-quality skills

## What this library cares about

This library mainly reviews whether a skill has:

1. clear identity
2. strong trigger discoverability
3. narrow and explicit scope
4. ordered constraints
5. deterministic gates
6. strong output contracts
7. safe fallback behavior
8. validation support
9. persistent state when needed
10. portable semantics across runtimes

## Why this exists

Many skills sound strict but are still easy to misuse.

The common failure modes are:

- unclear boundaries
- generic descriptions that do not trigger at the right time
- principles that never become workflow
- no fallback when context is weak
- no output structure
- no validation story

This repository exists to make those problems visible and fixable.

## How to use

Use this library when you want to:

- create a new skill
- review an existing skill
- study an excellent external skill
- extract reusable boundary patterns
- improve a local skill ecosystem over time

Typical prompts:

- `Use shuxia-skill-library to review this skill`
- `Use shuxia-skill-library to extract the best boundary ideas from this external skill`
- `Use shuxia-skill-library to rewrite this skill so it becomes more obedient`

## Inspiration

This library already absorbs ideas from skills and repositories that show strong discipline around:

- role framing
- scope split
- gating
- persistence
- artifact-oriented outputs
- validation
- anti-slop constraints

One early example included in the library is `huashu-design`, especially for:

- role lock
- scope split
- evidence before output
- fallback instead of hallucination
- anti-slop negative lists

## Vision

The long-term goal is to make it easier for anyone to build a skill they are genuinely satisfied with:

- clearer
- stricter
- more reusable
- easier to trust
- easier to maintain
