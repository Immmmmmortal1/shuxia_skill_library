# Contributing to shuxia-skill-library

感谢你愿意一起完善 `shuxia-skill-library`。

这个仓库的目标不是收集“更多 skill 文案”，而是持续沉淀：

- 更好的边界定义
- 更好的约束机制
- 更稳定的输出契约
- 更安全的 fallback 设计
- 更可复用的 skill 审查方法

如果你想贡献内容，最欢迎的是这些类型：

## 欢迎的贡献方向

### 1. 新的 skill 设计模式

例如：

- 更好的 trigger 设计
- 更好的 confirm gate
- 更好的 output contract
- 更好的 anti-slop 机制
- 更好的 long-running state 设计

请优先补到 [`skill-patterns.md`](./skill-patterns.md)。

建议格式：

- `Pattern name`
- `Definition`
- `Why it works`
- `How to encode`
- `Example source`

### 2. 优秀 skill 的结构拆解

如果你发现一个优秀 skill，不要只贴链接。

更有价值的贡献是：

- 这个 skill 的边界是怎么定义的
- 它是怎么防止 agent 跑偏的
- 它有哪些可以迁移到别的 skill 里的机制
- 它哪些规则只是 domain-specific，不应该盲目复用

请优先补成研究笔记，放在仓库根目录，文件名可以参考：

- `research-xxx.md`

### 3. skill review 示例

非常欢迎提交“审 skill 的示例”：

- 原 skill 有什么问题
- 用 `shuxia-skill-library` 怎么审
- 改写前后差异是什么
- 改写后为什么更听话

请优先补到 [`examples/`](./examples/) 目录。

### 4. README / 文档优化

如果你发现：

- 仓库定位不够清楚
- 说明不够适合新手
- 某些术语不够准确
- 中英双语表达还能更自然

也非常欢迎直接改进。

## 不太建议的贡献

以下内容一般不会优先合并：

- 只新增一个“写得很严厉”的 skill 模板，但没有机制分析
- 只贴外部 skill 链接，没有提炼可复用 pattern
- 完全 domain-specific 的规则，却没有说明适用边界
- 只强调“风格更好看”，但没有说明如何约束 agent 行为

## 提交建议

提交前建议先自查：

1. 这次改动有没有帮助 skill 更清楚地定义边界？
2. 这次改动有没有把重要约束从“口号”变成“流程”？
3. 这次改动是否让 skill 更容易触发、更不容易失控？
4. 这次改动是可复用的方法，还是只是一次性的偏好？

## 推荐的贡献格式

如果你要提一个新 pattern，建议用这种结构：

```md
## [PAT-XXX] Pattern Name

**Definition**
一句话定义

**Why it works**
为什么这个模式有效

**How to encode**
- 该怎么写进 skill

**Example source**
- 来源 skill / repo
```

如果你要提一个研究笔记，建议至少包含：

- 样本来源
- 观察到的共性
- 反复出现的高价值机制
- 哪些东西值得复用
- 哪些东西不要盲目照搬

## 最重要的一条

这个仓库不是为了证明“某个 skill 很厉害”。

而是为了回答：

**一个 skill 为什么会听话，为什么会跑偏，怎样才能被更多人稳定复用。**
