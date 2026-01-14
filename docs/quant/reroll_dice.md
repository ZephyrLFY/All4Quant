---
title: 🎲 Reroll 策略与期望
tags: [Probability, Dynamic Programming, Brainteaser]
sidebar_label: "001. Reroll Dice"
---

### Question Description

> You are offered a game where you roll a fair 6-sided die once. You receive a payout equal to the number rolled (e.g., if you roll a 4, you get $4).
> 
> However, after seeing the first roll, you have the option to reject it and roll the die one more time. If you choose to roll a second time, you must accept the result of the second roll as your final payout.

**Question：What's the optimal strategy and the Expected Value under your strategy?**

---

### Solution

先考虑单独投掷一次骰子时的期望。

$$
E_{once} = \frac{1+2+3+4+5+6}{6} = 3.5
$$

Which means, if the result of your first roll is lower than 3.5 (1, 2, and 3), you should try to reroll. Otherwise, you should keep the result.

EV计算则是：

$$
\begin{aligned}
E_{total} &= P_{keep} \cdot E_{keep} + P_{reroll} \cdot E_{reroll} \\
&= 0.5 \cdot \frac{4+5+6}{3} + 0.5 \cdot E_{once} \\
&= 0.5 \cdot 5 + 0.5 \cdot 3.5 \\
&= 4.25
\end{aligned}
$$

---

### Follow Up

> Now imagine the same game, but you have the option to roll up to 3 times in total. If you roll a third time, you must keep that result.

**Question：What's the new optimal strategy and the new Expected Value?**

---

### Solution

由之前的计算结果可知，可以reroll一次的情况下，EV: 3.5 -> 4.25

所以我们第一次投掷完是否要reroll的策略需要进行微调：新阈值为4.25，即只有投到5，6时才keep

而第二次投掷的结果则需要跟3.5进行比较，因为这个时候已经回到了原问题

$$
\begin{aligned}
E_{total} &= P_{keep} \cdot E_{keep} + P_{reroll} \cdot E_{reroll} \\
&= \frac{1}{3} \cdot \frac{5+6}{2} + \frac{2}{3} \cdot 4.25 \\
&= \frac{14}{3}
\end{aligned}
$$

:::tip 问题降级
在followup中，第一次投掷之后面对的不再是另一次投掷机会，而是另两次，所以期望与投掷一次并不同，需要相对应地调整决策阈值。
:::
