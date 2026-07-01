# Review Example: huashu-design

这个示例展示如何用 `shuxia-skill-library` 的视角审查一个优秀 skill。

---

## Skill Type

`huashu-design` 更像是一个 `HTML-native design workflow skill`，不是普通的前端开发 skill。

---

## Primary Boundary

它最核心的边界是：

**只做 HTML-native 的高保真设计产出，不做生产级前端开发。**

这条边界很关键，因为它先切断了“什么都能做”的膨胀路径。

---

## Boundary Mechanisms

### 1. Role Lock

它先定义自己是：

- HTML-native designer

而不是：

- production frontend engineer

这是一种很强的身份边界。

### 2. Scope Split

它会明确告诉你：

- 什么任务适合它
- 什么任务不适合它

这让 skill 更容易被正确路由。

### 3. Evidence Before Output

它强调：

- existing context
- brand assets
- official materials

这些必须先于高保真设计输出。

这大幅减少了“凭空做一个 generic hi-fi 页面”的概率。

### 4. Fallback Instead Of Hallucination

当上下文不足时，它不会直接乱生成。

更好的做法是：

- 进入方向探索模式
- 先给多个设计方向
- 再让用户选

这是一种非常成熟的 fallback。

### 5. Negative List

它不只说“要做好”，还明确说“不要掉进哪些默认套路”。

这种 anti-slop 机制很重要。

---

## What Makes It Obedient

它“听话”的根本原因不是语气严格，而是：

- 关键约束被写进了 workflow
- 不确定时有 fallback
- 适用与不适用场景被写清楚了
- 生成前有事实与资产门槛

也就是说，它不是靠“强调”，而是靠“结构”。

---

## Reusable Patterns

从 `huashu-design` 里最值得复用的包括：

- `Role Lock`
- `Scope Split`
- `Evidence Before Output`
- `Fallback Instead Of Hallucination`
- `Negative List`

---

## Local Improvements You Could Apply Elsewhere

如果把这些经验迁移到其他 skill，优先迁移的是：

1. 给 skill 加“我是什么 / 我不是什么”
2. 加“适用 / 不适用场景”
3. 把关键约束移到 workflow 里
4. 给上下文不足场景设计 fallback
5. 补 anti-slop 或 anti-pattern 清单

---

## Summary

`huashu-design` 的优秀，不在于它写得有多酷，而在于它把：

- 边界
- 约束
- fallback
- 反失控机制

都做成了可执行的流程。
