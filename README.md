# shuxia-skill-library

> 让更多人都能轻松做出自己满意的 skill。  
> Help people build agent skills that are clearer, stricter, and easier to trust.

`shuxia-skill-library` 是一个面向 `agent skill` 的研究、审查与沉淀仓库。  
它不把 skill 当成“一个提示词”，而是把 skill 当成一种 **行为契约**。

这个仓库关注的不是“skill 会不会说”，而是：

- skill 的边界是否清楚
- skill 的约束是否真的写进了流程
- skill 在信息不足时会不会乱编
- skill 的输出是否稳定、可复核、可复用

`shuxia-skill-library` is a research and review library for agent skills.  
It treats a skill as a **behavior contract**, not just a prompt.

The focus is not whether a skill sounds smart, but whether it is:

- clearly bounded
- structurally constrained
- safe under uncertainty
- stable in output
- reusable across real workflows

---

## 快速开始 | Quick Start

如果你是第一次使用这个仓库，建议按这个顺序看：

1. 先读 [`README.md`](./README.md)
   - 了解仓库定位和目标

2. 再读 [`SKILL.md`](./SKILL.md)
   - 了解主 skill 怎么审 skill

3. 再看 [`scorecard.md`](./scorecard.md)
   - 学会怎么给 skill 打分

4. 再看 [`examples/review-huashu-design.md`](./examples/review-huashu-design.md)
   - 看一个优秀 skill 的正面案例

5. 再看 [`examples/review-weak-skill.md`](./examples/review-weak-skill.md)
   - 看一个典型弱 skill 为什么不听话

6. 最后看 [`skill-patterns.md`](./skill-patterns.md)
   - 把可复用模式沉淀下来

Suggested first path through the repository:

1. Read `README.md`
2. Read `SKILL.md`
3. Read `scorecard.md`
4. Read the strong example
5. Read the weak example
6. Then use `skill-patterns.md` as your reusable reference

---

## 为什么做这个仓库 | Why This Exists

很多 skill 看起来很严格，但实际并不“听话”。

常见问题包括：

- 边界不清，什么都想做
- description 很泛，导致触发不准
- 原则很多，但没有变成 workflow
- 信息不够时还在硬输出
- 没有 fallback
- 没有 output contract
- 没有验证或审查思路

这个仓库的目标，就是把这些问题显性化，并沉淀出一套可复用的方法。

Many skills sound strict, but are still easy to misuse.

Common failure modes:

- unclear boundaries
- vague trigger descriptions
- principles that never become workflow
- hallucinated output under weak context
- missing fallback behavior
- missing output contracts
- no validation mindset

This repository exists to make those problems visible and fixable.

---

## 核心目标 | Core Goal

帮助大家做出这样的 skill：

- 更容易被正确触发
- 更清楚自己是什么、不是什么
- 更擅长在流程中执行约束
- 更能在不确定时安全退化
- 更容易产出一致、稳定的结果

Help people build skills that are:

- easier to trigger correctly
- explicit about what they are and are not
- able to enforce constraints through workflow
- able to degrade safely under uncertainty
- more consistent and trustworthy in output

---

## 仓库内容 | What’s Inside

### 1. [`SKILL.md`](./SKILL.md)

主 skill，本身就是一个“审 skill / 强化 skill”的 skill。  
用于分析、规范、重写、强化其他 skill。

The main review skill.  
Use it to analyze, normalize, and strengthen other skills.

### 2. [`skill-patterns.md`](./skill-patterns.md)

可复用的 skill 设计模式库，持续沉淀优秀 skill 的共性。

目前包括：

- Role Lock
- Scope Split
- Constraint In Workflow
- Fallback Instead Of Hallucination
- Evidence Before Output
- Negative List
- Output Contract
- Deterministic Gate
- Validation Companion
- Persistent State
- Cross-Platform, Same Semantics

A reusable pattern library for skill design.  
It captures transferable mechanisms from strong skills.

### 3. [`research-hot-skills-2026-07-01.md`](./research-hot-skills-2026-07-01.md)

基于 ClawHub 和 GitHub 热门 skill 的研究笔记。  
主要总结“现在比较火、比较强的 skill，到底强在哪”。

A research note based on hot skills from ClawHub and GitHub.  
It summarizes the recurring qualities of popular, high-quality skills.

### 4. [`examples/`](./examples/)

示例目录，放“怎么审 skill、怎么改 skill、怎么提炼 pattern”的实战样例。

An examples directory for practical reviews, rewrites, and pattern extraction cases.

### 5. [`CONTRIBUTING.md`](./CONTRIBUTING.md)

贡献指南，说明适合提交什么内容、建议怎样沉淀 pattern、怎样写研究笔记和 review 示例。

A contributor guide describing what kinds of additions are most valuable to this repository.

### 6. [`scorecard.md`](./scorecard.md)

一张可以直接拿来给 skill 打分的评审表。  
适合做 review、重写前后对比、团队统一标准。

A practical scorecard for reviewing and comparing skill quality.

### 7. [`CHANGELOG.md`](./CHANGELOG.md)

记录仓库的重要演进，帮助后来者理解这个项目是怎么逐步长起来的。

A changelog for meaningful repository evolution.

---

## 我关注的优秀 skill 品质 | What Makes an Excellent Skill

这个仓库目前主要用这 10 个维度来判断一个 skill 是否优秀：

1. `Identity`  
   身份清晰，知道自己是什么、不是什么

2. `Trigger Discoverability`  
   容易被检索到，容易在正确时机被触发

3. `Scope Narrowness`  
   范围明确，不无限扩张

4. `Ordered Constraints`  
   关键限制有执行顺序，而不只是抽象原则

5. `Deterministic Gates`  
   有明确的确认门、完成门、验证门

6. `Output Contract`  
   输出结构稳定、可复核、可交付

7. `Fallback Behavior`  
   信息不足时能安全退化，而不是硬编

8. `Validation Story`  
   最好有 lint、schema、tests 或检查思路

9. `Persistent State`  
   长流程时考虑外部状态与可恢复性

10. `Portable Semantics`  
    跨平台迁移时，核心语义不跑偏

This repository currently evaluates skills across these 10 qualities:

- identity
- trigger discoverability
- scope narrowness
- ordered constraints
- deterministic gates
- output contract
- fallback behavior
- validation story
- persistent state
- portable semantics

---

## 怎么使用 | How to Use

适合这些场景：

- 你正在创建一个新 skill
- 你想审查一个现有 skill
- 你想学习一个外部优秀 skill
- 你想提炼可复用的边界模式
- 你想持续优化自己的 skill 体系

Use this library when:

- creating a new skill
- reviewing an existing skill
- studying a strong external skill
- extracting reusable boundary patterns
- improving a local skill ecosystem over time

### 典型用法 | Typical Prompts

- `用 shuxia-skill-library 审查这个 skill`
- `用 shuxia-skill-library 提炼这个外部 skill 的优秀边界设计`
- `用 shuxia-skill-library 重写这个 skill，让它更听话`

- `Use shuxia-skill-library to review this skill`
- `Use shuxia-skill-library to extract the best boundary ideas from this external skill`
- `Use shuxia-skill-library to rewrite this skill so it becomes more obedient`

---

## 这个仓库吸收什么样的好想法 | What This Library Learns From

这个仓库会持续吸收外部优秀 skill 和 skill 仓库里的好机制，尤其是这些方面：

- role framing
- scope split
- gating
- persistence
- artifact-oriented output
- validation
- anti-slop constraint

An early reference case already absorbed into this library is `huashu-design`, especially for:

- role lock
- scope split
- evidence before output
- fallback instead of hallucination
- anti-slop negative lists

---

## 适合谁 | Who This Is For

这个仓库适合：

- 想自己写 skill 的人
- 已经在维护技能库的人
- 想把 prompt 升级成“可复用机制”的人
- 想让 agent 更稳定、更可控的人

This repository is for:

- people who want to write their own skills
- people maintaining a local skill library
- people who want reusable mechanisms instead of one-off prompts
- people who want more stable and controllable agent behavior

如果你想参与完善这个仓库，现在也可以直接通过：

- GitHub Issues 提交 bug、pattern 提案、skill review 请求
- GitHub Pull Requests 提交文档、模式、研究笔记和示例增强

If you want to contribute, you can now use:

- GitHub Issues for bugs, pattern proposals, and skill review requests
- GitHub Pull Requests for docs, patterns, research notes, and examples

---

## 路线图 | Roadmap

接下来希望持续补的内容：

- 更多外部优秀 skill 的结构拆解
- 更细的 skill 评分标准
- 针对不同类型 skill 的审查模板
- skill review 示例集
- skill rewrite 示例集
- 中英文双语规范持续完善

Planned directions:

- more external skill breakdowns
- finer-grained review criteria
- review templates by skill type
- example sets for skill reviews
- example sets for skill rewrites
- stronger bilingual documentation

---

## 愿景 | Vision

我希望这个仓库最后能做到一件事：

**让更多人都能轻松做出自己真正满意的 skill。**

不是只会“写一个 skill”，  
而是能写出：

- 边界清楚的
- 约束到位的
- 输出稳定的
- 不容易失控的
- 长期可维护的 skill

The long-term vision is simple:

**help more people build skills they are genuinely satisfied with.**

Not just skills that exist,
but skills that are:

- clearly bounded
- properly constrained
- stable in output
- difficult to derail
- maintainable over time
