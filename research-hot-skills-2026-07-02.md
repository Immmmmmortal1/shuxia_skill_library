# Hot Skills Research

Date: 2026-07-02

Scope:

- ClawHub front page and individual skill pages for current high-heat skills
- GitHub repository metadata and raw `SKILL.md` / README evidence for fast-rising skill repositories
- GitHub search for recently created skill repositories with visible star/update momentum

This note focuses on reusable skill-design mechanisms, not hype or install recommendations.

---

## Sources Checked

ClawHub:

- `https://clawhub.ai/`
- `https://clawhub.ai/pskoett/skills/self-improving-agent`
- `https://clawhub.ai/spclaudehome/skills/skill-vetter`
- `https://clawhub.ai/ivangdavila/skills/self-improving`
- `https://clawhub.ai/steipete/skills/github`

GitHub:

- `mattpocock/skills`
- `alirezarezvani/claude-skills`
- `VoltAgent/awesome-agent-skills`
- recent-created search samples including `anthropics/launch-your-agent`, `hyuce/master-brain`, `kainulla/skillfire`, `Teycir/SkillsGuard`, and `KnoxOps/agent-runbook`

Visible momentum on 2026-07-02:

- `mattpocock/skills`: 153k+ stars, pushed 2026-07-01.
- `VoltAgent/awesome-agent-skills`: 27k+ stars, updated 2026-07-02, 1497+ listed skills.
- `alirezarezvani/claude-skills`: 19k+ stars by GitHub API despite README badge text lagging behind, pushed 2026-07-01.
- ClawHub front page highlighted `self-improving agent`, `Skill Vetter`, `Self-Improving + Proactive Agent`, and `Github`, with ClawHub pages showing star counts, update age, version, and security audit state.

---

## Standout Skills And Mechanisms

### ClawHub: `Skill Vetter`

Why it stood out:

- It is not a capability skill; it is a safety gate for installing other skills.
- Its workflow orders source review, all-file code review, permission scope, risk classification, and verdict.
- It uses an explicit reject list for unknown network calls, credential access, obfuscation, broad file reads, and elevated permissions.

Reusable lesson:

Public skill marketplaces need a local supply-chain protocol. Registry heat, star count, and audit badges should be treated as evidence inputs, not as permission to install.

Pattern extracted:

- `PAT-025 Skill Supply-Chain Trust Ladder`

### ClawHub: `Self-Improving + Proactive Agent`

Why it stood out:

- It makes persistent memory bounded through temperature tiers instead of one growing memory file.
- HOT memory is small and always loaded; WARM project/domain memory is loaded on demand; COLD archive keeps decayed patterns out of the active path.
- It requires repeated signals before promotion, and it explicitly ignores one-time instructions.

Reusable lesson:

Persistent state needs load policy. Memory quality is not only about writing facts; it is about when facts are allowed into the always-loaded layer.

Pattern extracted:

- `PAT-026 Memory Temperature Tiers`

### GitHub: `mattpocock/skills`

Why it stood out:

- The README draws a hard line between user-invoked skills and model-invoked skills.
- User-invoked skills orchestrate; model-invoked skills carry reusable discipline such as debugging, TDD, domain modeling, and codebase design.
- `diagnosing-bugs` blocks progress until there is a tight, red-capable feedback loop already run once.
- `writing-great-skills` treats descriptions, references, and stale prose as context-load costs.

Reusable lessons:

- Invocation is a boundary, not a packaging detail.
- Debugging skills need an observable gate before hypothesis work.
- Skill text should be pruned by whether it changes invocation or execution behavior.

Patterns extracted:

- `PAT-023 Invocation Class Split`
- `PAT-024 Red-Capable Feedback Gate`
- `PAT-027 Context Load Budget`

### GitHub: `master-brain`

Why it stood out:

- It turns reasoning into a fixed stage loop: Observation, Hypothesis, Evidence, Conclusion, Verification.
- It requires per-claim confidence and source-quality notes before conclusions.
- If verification fails, the loop returns to Observation instead of patching the conclusion.

Reusable lesson:

Evidence-before-output becomes stronger when each reasoning stage has its own marker and cannot be merged with adjacent stages.

No new pattern added today because the existing `Evidence Before Output`, `Constraint In Workflow`, and `Deterministic Gate` patterns already cover most of this mechanism.

### GitHub: fast-rising safety and meta-skill repos

Recent-created search surfaced `skillfire`, `SkillsGuard`, and `agent-runbook` style projects. The useful signal is not their current size; it is the cluster:

- skills need collision/routing tests
- skills need static security scanners
- skills need compiled runbooks with checkpoints

Reusable lesson:

The skill ecosystem is moving from "write better markdown" toward governance: routing validation, permission review, static scanning, and checkpoint compilation.

---

## Pattern Refinements For Local Reviews

Add these checks when reviewing or writing a Shuxia skill:

1. Does the skill specify whether it is user-invoked, model-invoked, or a router?
2. If it performs diagnosis, review, or validation, what is the earliest observable red/green gate?
3. If it installs, runs, or imports third-party skills/scripts, what is the source and permission review protocol?
4. If it writes memory, what keeps one-off context out of the always-loaded tier?
5. Does every always-visible line change invocation or execution behavior?

These checks are worth adding to reviews before increasing skill length. The high-quality repos are moving toward smaller active surfaces with stronger gates, not bigger prompt bodies.

---

## Local Updates

- Updated `skill-patterns.md`:
  - renumbered duplicate PAT entries so pattern IDs are stable
  - added `PAT-023 Invocation Class Split`
  - added `PAT-024 Red-Capable Feedback Gate`
  - added `PAT-025 Skill Supply-Chain Trust Ladder`
  - added `PAT-026 Memory Temperature Tiers`
  - added `PAT-027 Context Load Budget`
- Added this dated research note because today's findings add multiple reusable mechanisms beyond the 2026-07-01 market scan.

---
