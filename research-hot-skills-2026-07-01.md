# Hot Skills Research

Date: 2026-07-01

Scope:

- ClawHub hot skills sampled from `https://clawhub.ai/api/v1/skills?limit=100`
- GitHub hot skill repositories sampled from GitHub repository search for `SKILL.md` / agent skills

This note is not a literal “best 20 skills ever” ranking.
It is a practical sample of currently visible, high-heat skills and repositories used to extract reusable quality patterns.

---

## Sampled ClawHub Top 10

Sorted mainly by installs, then downloads.

1. `PPT Generator`
2. `The News`
3. `Bring`
4. `HuaHuaDailyMCP`
5. `DeepMiner Skills`
6. `Sentisense`
7. `Stock Terminal`
8. `Us Stocks Analysis`
9. `Outdoor Sports Event Risk Analysis Tool`
10. `Tencent VOD`

What stands out on ClawHub:

- top skills are usually narrow, concrete, and immediately useful
- the winning pattern is not “general intelligence”, but “one domain + one job to be done”
- many descriptions include a hard trigger, such as “must trigger whenever the request involves X”
- output is often artifact-like or action-like: report, command, booking result, block message, PPTX

---

## Sampled GitHub Top 10

Sorted by stars from GitHub repository search on 2026-07-01.

1. `OthmanAdi/planning-with-files`
2. `microsoft/SkillOpt`
3. `FrancyJGLisboa/agent-skill-creator`
4. `bergside/awesome-design-skills`
5. `skalesapp/skales`
6. `sno-ai/mda`
7. `dzcmemory-web/bazi-ziwei-skill`
8. `mxyhi/ok-skills`
9. `agent-sh/agnix`
10. `Narwhal-Lab/MagicSkills`

Other notable high-heat repositories:

- `awesome-gamedev-agent-skills`
- `ai-research-skills`
- `robotics-agent-skills`
- `alpaca-skills`
- `sports-skills`

What stands out on GitHub:

- heat clusters around infrastructure, not only domain prompts
- strong projects often solve one of these meta-problems:
  - persistence
  - validation
  - portability
  - routing
  - generation of other skills
- the most admired repositories are often not a single skill, but a skill system

---

## What Excellent Skills Repeatedly Have

### 1. Clear boundary of identity

Excellent skills say:

- what role they play
- what they are not
- what neighboring tasks belong elsewhere

This reduces accidental overreach.

### 2. Strong trigger discoverability

Excellent skills are easy to retrieve.

They include:

- trigger conditions
- symptoms
- realistic user phrasing
- domain vocabulary

Bad skills may be smart, but invisible.

### 3. Narrow job-to-be-done

Hot skills often win because they do one thing very clearly:

- generate a PPTX
- fetch news
- build a stock brief
- create a skill
- maintain a persistent plan
- lint skill configs

Specificity beats broadness.

### 4. Ordered constraints

The best skills do not merely contain principles.
They encode order:

- inspect first
- validate second
- synthesize third
- confirm before mutation

This is one of the strongest obedience signals.

### 5. Deterministic gates

Excellent skills insert explicit gates:

- completion gate
- confirm gate
- validation gate
- commit gate

This prevents silent drift and premature completion.

### 6. Output contract

Strong skills force a shape:

- report sections
- PASS/WARNING/ERROR
- exact file output
- editable artifact
- command format

Without an output contract, skills feel “advisory” instead of reliable.

### 7. Safe fallback

When information is missing, strong skills do not bluff.
They:

- switch modes
- ask once
- degrade to exploration
- refuse unsupported execution

Fallback behavior is one of the best indicators of maturity.

### 8. Validation or enforcement

The best ecosystems increasingly pair skill docs with:

- linting
- schema validation
- fixtures
- tests
- examples

The pattern is clear:
instruction without validation is respected less consistently.

### 9. Persistent state for long workflows

Long-running skill systems increasingly externalize memory:

- files
- plans
- progress markers
- reusable artifacts

This reduces context-loss failure and improves resumability.

### 10. Portability with invariant behavior

Cross-platform skill projects do well when they preserve core behavior across:

- Claude Code
- Codex
- Cursor
- OpenClaw
- Gemini CLI

The important part is not export itself, but stable semantics after export.

---

## What Weak Skills Usually Miss

- no `do not use when`
- no fallback rule
- no output contract
- no hard transition gate
- broad identity with vague responsibility
- nice prose but no workflow
- reusable sounding title with poor trigger coverage
- domain enthusiasm but no evidence requirements

---

## Practical Standard For Shuxia Skill Reviews

When reviewing a local skill, score it against these qualities:

1. `Identity`
2. `Trigger discoverability`
3. `Scope narrowness`
4. `Ordered constraints`
5. `Deterministic gates`
6. `Output contract`
7. `Fallback behavior`
8. `Validation story`
9. `Persistent state need`
10. `Portability of semantics`

A high-quality skill should be strong in at least:

- identity
- scope
- workflow
- output
- fallback

A top-tier skill ecosystem usually also adds:

- validation
- persistence
- composability

---

## Source Notes

ClawHub:

- `https://clawhub.ai/skills`
- `https://clawhub.ai/api/v1/skills?limit=100`

GitHub examples:

- `https://github.com/OthmanAdi/planning-with-files`
- `https://github.com/microsoft/SkillOpt`
- `https://github.com/FrancyJGLisboa/agent-skill-creator`
- `https://github.com/agent-sh/agnix`
- `https://github.com/gamedev-skills/awesome-gamedev-agent-skills`
- `https://github.com/WenyuChiou/ai-research-skills`
