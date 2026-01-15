---
title: 🪙 抛硬币的序列问题
tags: [Probability, Markov Chains, Expected Value, Brainteaser]
sidebar_label: "002. Flip Coin"
---

### Question Description

> You are flipping a fair coin. What is the expected number of flips required to see the sequence HH (two consecutive Heads) for the first time?

---

### Solution

这种题的关键是状态转移方程。我们可以设 $E$ 为从初始状态开始达到 HH 所需的期望次数，$E_H$ 为已经掷出一个 H 的状态下还需要抛掷的期望次数：

$$
E = 1 + \frac{1}{2}E + \frac{1}{2}E_H
$$

其中$\frac{1}{2}E$表示抛出一次T之后回到了原点。而
$$
E_H = 1 + \frac{1}{2}E + \frac{1}{2} \cdot 0
$$

同样，$\frac{1}{2}E$表示抛出一次T之后回到了原点，后一项则是再次抛出H，这时目标达成，不需要再抛了，所以期望数为0.

然后我们把$E_H$代入第一个式子，可得

$$
\begin{aligned}
E &= 1 + \frac{1}{2}E + \frac{1}{2}E_H \\
&= 1 + \frac{1}{2}E + \frac{1}{2} \cdot (1 + \frac{1}{2}E) \\
&= \frac{3}{2} + \frac{3}{4}E \\
\end{aligned}
$$

求解得出$E = 6$

---

### Follow Up 1

> What about HT? 期望投掷数会变化吗？

---

### Solution

同理，

$$
E = 1 + \frac{1}{2}E + \frac{1}{2}E_H
$$

$$
E_H = 1 + \frac{1}{2}E_H + \frac{1}{2} \cdot 0
$$

求得$E_H = 2$, 继续求得$E = 4$

:::tip 为什么期望投掷数比HH少？
HH：投出H之后，第二次没有投出H而是投出T时，会回到原点，进度清零。

HT：投出H之后，第二次如果没有投出T而是投出H时，只会保持现状，进度不会清零。
:::

---

### Follow Up 2

> What about HTT?

---

### Solution

同理，

$$
E = 1 + \frac{1}{2}E + \frac{1}{2}E_H
$$

$$
E_H = 1 + \frac{1}{2}E_H + \frac{1}{2}E_{HT}
$$

$$
E_{HT} = 1 + \frac{1}{2}E_H + \frac{1}{2} \cdot 0
$$

联立式子2和3，求得$E_H = 6$, 代入式子1继续求得$E = 8$

---

### Follow Up 3: Squence Race

> You and I are playing a game. We flip a fair coin repeatedly.
> 
> - You win if the sequence HH appears first.
> - I win if the sequence HT appears first.

**Question: What is the probability that you win? (i.e., $P(\text{HH before HT})$)**

---

### Solution

50% v.s. 50%

这是马尔可夫过程。由于两者获胜的条件都是先出现一次H，那么第二次是H还是T完全独立于第一次投掷。

---

### Follow Up 4: New Sequence Race

> Same game as in followup 3. But
> 
> - You win if the sequence HH appears first.
> - I win if the sequence TH appears first.

**Question: What is the probability that you win?**

---

### Solution

Consider about the situation when "T" appears before "HH". In this case, "HH" will never win.

So, the probability for "HH" to win is $\frac{1}{2} \cdot \frac{1}{2} = \frac{1}{4}$
