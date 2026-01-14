---
title: 经典掷骰子问题：Reroll 策略与期望
tags: [Probability, Dynamic Programming, Brainteaser]
sidebar_label: "001. Reroll Dice"
---

# 掷骰子重投问题：最优策略分析

这是一道非常经典的 Quant 面试题。题目通常表述为：你掷一个公平的六面骰子，你可以选择接受当前点数，或者获得一次（且仅一次）重投的机会。如果你重投，你必须接受第二次的点数。

**问题：你的最优策略是什么？该策略下的期望收益是多少？**

---

### 💡 核心逻辑：倒推法 (Backward Induction)

解决这类决策问题的核心在于：**当你面临最后一次机会时，你的期望收益是多少？**

1. **最后一次投掷 (Step 2)**：
   如果你选择了重投，你就没有任何退路了。此时，掷骰子的期望值 $E_2$ 就是一个标准骰子的平均值：
   $$
   E_2 = \frac{1+2+3+4+5+6}{6} = 3.5
   $$

2. **第一次投掷的决策 (Step 1)**：
   现在你手里拿着第一次投出的点数 $X$。
   - 如果 $X > E_2$，你应该**停止**（保留当前点数）。
   - 如果 $X < E_2$，你应该**重投**（追求更高的期望）。
   - 如果 $X = E_2$，两者皆可（在离散情况下不会发生，$3.5$ 不是整数）。

:::tip 决策准则
因为 $E_2 = 3.5$，所以：
- 当 $X \in \{4, 5, 6\}$ 时：**Keep**
- 当 $X \in \{1, 2, 3\}$ 时：**Reroll**
:::

---

### 🔢 数学推导

总期望 $E_{total}$ 可以看作是两种情况的加权平均：

$$
\begin{aligned}
E_{total} &= P(X \ge 4) \cdot E[X | X \ge 4] + P(X \le 3) \cdot E_2 \\
&= \frac{3}{6} \cdot \left( \frac{4+5+6}{3} \right) + \frac{3}{6} \cdot 3.5 \\
&= \frac{1}{2} \cdot 5 + \frac{1}{2} \cdot 3.5 \\
&= 2.5 + 1.75 \\
&= 4.25
\end{aligned}
$$



---

### 💻 模拟验证 (Python)

我们可以写一个简单的蒙特卡洛模拟来验证这个结果，顺便测试你刚配置好的 **JetBrains Mono** 字体效果。

```python
import random

def simulate_reroll(trials=1000000):
    total_score = 0
    for _ in range(trials):
        first_roll = random.randint(1, 6)
        # 决策逻辑：如果第一次小于期望值 3.5，则重投
        if first_roll < 3.5:
            score = random.randint(1, 6)
        else:
            score = first_roll
        total_score += score
    return total_score / trials

print(f"模拟期望值: {simulate_reroll():.4f}") # 预期输出接近 4.25