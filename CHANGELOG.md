# Changelog

All notable changes to `shuxia-skill-library` will be documented in this file.

This project follows a simple changelog style focused on meaningful repository evolution.

---

## 2026-07-01

### Added

- Initial open-source release of `shuxia-skill-library`
- Main review skill: `SKILL.md`
- Reusable pattern library: `skill-patterns.md`
- Hot skill research note based on ClawHub and GitHub
- Bilingual open-source homepage `README.md`
- `MIT` license
- Contributor guide `CONTRIBUTING.md`
- Practical examples directory
- `review-huashu-design.md` example
- `rewrite-template.md` template
- `scorecard.md` for structured skill evaluation

### Purpose

- Turn the repository into a reusable system for studying, reviewing, and improving agent skills
- Help people build skills with stronger boundaries, constraints, outputs, and fallback behavior

## 2026-07-02

### Added

- Added `PAT-014 Mode Split For Asset Pipelines` to capture a reusable boundary pattern for image and template workflows that must separate `reference-only` URL retrieval from `replaceable` local-template composition
- Added `PAT-016 Streaming Confirmation Gate` to require one-by-one decision confirmation before drafting or revising a skill

### Changed

- Updated `SKILL.md` so skill creation and revision now use a superpower-style `Streaming Confirmation Mode`: ask one scoped question at a time, summarize confirmed decisions, and wait for final approval before writing

## 2026-07-03

### Added

- Added `research-hot-skills-2026-07-03.md` with current ClawHub and GitHub skill ecosystem findings
- Added `PAT-032 Portable Provenance Frontmatter` for source/ref/tree identity that travels with installed skills
- Added `PAT-033 Evidence-Backed Skill Lifecycle Split` for separating mining, personalization, and publication workflows
- Added `PAT-034 Typed Shared-State Contract` for memory graphs and cross-skill state handoffs

### Changed

- Fixed duplicate pattern IDs in `skill-patterns.md` and updated 2026-07-02 research references to the corrected IDs

## 2026-07-06

### Added

- Added `research-hot-skills-2026-07-06.md` with current ClawHub active-update and GitHub skill-library findings
- Added `PAT-040 Scoped External Tool Session`
- Added `PAT-041 Async Operation Wait Contract`
- Added `PAT-042 Precompiled Doc Skill With Freshness Gate`
- Added `PAT-043 Phase Ownership Boundary`

## 2026-07-07

### Added

- Added `research-hot-skills-2026-07-07.md` with current ClawSkills, Skills.sh, and GitHub high-momentum skill findings
- Added `PAT-044 Registry Risk Signal`
- Added `PAT-045 Visual Feedback Loop`
- Added `PAT-046 Capability Hub With Built-In Subskills`
- Added `PAT-047 Read-Only Validator Role`
- Added `PAT-048 Claim-Type Guard Split`
- Added `PAT-049 Promotion Rule For Persistent Learning`
- Added `PAT-050 Local Control Plane Artifact`
- Added `PAT-051 Calibrated Process Intensity`
- Added `PAT-052 Human-Signed Edit Boundary`
