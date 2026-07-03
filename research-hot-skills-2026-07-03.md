# Hot Skills Research

Date: 2026-07-03

Scope:

- ClawHub front page and selected high-heat skill pages
- GitHub topic pages, repository READMEs, issue/discussion surfaces, and GitHub changelog evidence
- Re-check of fast-moving skill ecosystem signals since 2026-07-02

This note only records mechanisms that add something useful beyond yesterday's self-improvement, vetting, and context-budget patterns.

---

## Sources Checked

ClawHub:

- `https://clawhub.ai/`
- `https://clawhub.ai/oswalpalash/skills/ontology`
- Front-page high-heat entries including `self-improving agent`, `Skill Vetter`, `Self-Improving + Proactive Agent`, `Github`, `ontology`, `SkillScan`, `Agent Browser`, and `Auto-Updater Skill`

GitHub and related primary sources:

- `https://github.com/topics/agent-skills`
- `https://github.com/anthropics/skills`
- `https://github.com/anthropics/skills/blob/main/skills/skill-creator/SKILL.md`
- `https://github.com/github/awesome-copilot`
- `https://github.com/github/awesome-copilot/blob/main/skills/github-copilot-starter/SKILL.md`
- `https://github.com/hqhq1025/skill-optimizer`
- `https://github.com/K-Dense-AI/scientific-agent-skills`
- `https://github.blog/changelog/2026-04-16-manage-agent-skills-with-github-cli/`

Visible momentum on 2026-07-03:

- ClawHub front page still shows self-improvement, vetting, GitHub gateway, ontology, SkillScan, browser automation, and auto-updater skills in the high-popularity list.
- `obra/superpowers` remained the largest visible GitHub skill framework signal, with GitHub API showing 244k+ stars, updated 2026-07-03, pushed 2026-07-02.
- GitHub topic pages showed current skill-adjacent repositories with strong visible counts and recent updates, including `anthropics/skills` around 158k stars, `github/awesome-copilot` around 36k stars, `K-Dense-AI/scientific-agent-skills` around 30k stars, and `VoltAgent/awesome-agent-skills` around 27k stars.
- GitHub's `gh skill` changelog is important ecosystem evidence because skills are now being treated like installable packages with provenance, pinning, update checks, and publishing validation.

---

## Standout Skills And Mechanisms

### GitHub CLI `gh skill`

Why it stood out:

- It treats a skill as an installable package with supply-chain metadata, not just a copied markdown folder.
- Install supports tag or commit pinning.
- Installed skills record repository provenance and source tree identity in frontmatter so the metadata travels with the skill.
- Update checks compare content identity instead of trusting a version string alone.
- Publishing validation checks the skill spec and encourages release immutability and repository security controls.

Reusable lesson:

Provenance should be portable with the skill artifact. A local skill review should ask whether the skill can still be audited after it is copied between Claude Code, Codex, Cursor, Gemini, or a project-local directory.

Pattern extracted:

- `PAT-032 Portable Provenance Frontmatter`

### GitHub: `hqhq1025/skill-optimizer`

Why it stood out:

- It split the lifecycle into three named skills instead of one broad optimizer:
  - `skill-miner` discovers repeated workflows from real agent history.
  - `skill-personalizer` adapts a skill inward to one user's tools, phrasing, directories, and verification habits.
  - `skill-generalizer` removes private context and prepares a portable public artifact.
- The split matches different evidence requirements: history evidence for mining, local evidence for personalization, and privacy/portability checks for publication.

Reusable lesson:

Skill quality work has direction. "Optimize this skill for me" and "make this publishable" are opposite transformations and should not share one unchecked default path.

Pattern extracted:

- `PAT-033 Evidence-Backed Skill Lifecycle Split`

### ClawHub: `ontology`

Why it stood out:

- It turns shared memory into a typed graph with entity types, relation constraints, append-only storage, and validation before mutation.
- It uses `Credential.secret_ref` rather than storing secrets directly.
- It asks skills that use the ontology to declare read/write types plus preconditions and postconditions.
- It models planning as graph transformations and rolls back on constraint violations.

Reusable lesson:

Persistent state becomes more trustworthy when it is an interface, not a note pile. Cross-skill shared state should have contracts similar to API contracts: types, allowed writes, preconditions, postconditions, and validation gates.

Pattern extracted:

- `PAT-034 Typed Shared-State Contract`

### GitHub: `anthropics/skills` `skill-creator`

Why it stood out:

- It frames skill creation as an iterative eval loop: draft, create test prompts, run skill-enabled trials, review qualitative and quantitative results, rewrite, repeat, then expand the test set.
- Recent issues around eval matching and trigger accuracy reinforce that skill quality is partly a measurement problem, not only an instruction-writing problem.

Reusable lesson:

For skills that claim to improve triggering or behavior, the output contract should include test prompts, eval artifacts, or a documented measurement plan. Existing local patterns already cover this through `Validation Companion`, `Red-Capable Feedback Gate`, and `Context Load Budget`, so no new pattern was added today.

### GitHub: `awesome-copilot`

Why it stood out:

- The repository collects instructions, agents, skills, hooks, workflows, and plugins rather than treating all agent customization as one object type.
- Its `github-copilot-starter` skill requires project facts before generating repository-wide Copilot configuration, then emits a concrete file set.
- Discussions around sharing code between skills show the scaling pressure: duplicated small utilities, packages, bundling, and registry experiments.

Reusable lesson:

Large skill libraries need object-type boundaries and shared-utility policy. A "skill" collection eventually needs rules for when to keep helper code vendored for portability versus extracting shared packages for maintenance.

No new pattern was added because this is an extension of `Invocation Class Split`, `Scope Split`, and `Context Load Budget`.

---

## Pattern Refinements For Local Reviews

Add these checks when reviewing or writing Shuxia skills:

1. Does the skill carry enough provenance to audit where it came from after it is copied?
2. If a skill is installed from a marketplace or GitHub repo, is the source pinned or at least content-addressed?
3. Is the task mining, personalizing, or publishing a skill? If yes, does the workflow keep those directions separate?
4. If the skill writes shared memory, does it declare typed reads/writes, preconditions, postconditions, and secret indirection?
5. If the skill claims to improve triggers or behavior, what eval prompt set or measurement artifact proves the change?
6. If helper code is shared across skills, is portability or maintainability the dominant constraint?

---

## Local Updates

- Updated `skill-patterns.md`:
  - fixed duplicate pattern IDs introduced by earlier incremental additions
  - added `PAT-032 Portable Provenance Frontmatter`
  - added `PAT-033 Evidence-Backed Skill Lifecycle Split`
  - added `PAT-034 Typed Shared-State Contract`
- Added this dated research note because today's findings add three transferable mechanisms around provenance, lifecycle direction, and shared-state contracts.

---
