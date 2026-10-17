
$P(MC_2 \cap MC_3 \cap MC_4) = q_{p_1}q_{p_2}q_{m_1}q_{m_2}q_{m_3},$

以及

$P(MC_1 \cap MC_2 \cap MC_3 \cap MC_4) = q_{p_1}q_{p_2}q_{m_1}q_{m_2}q_{m_3},$

假设每个组件的 `MTTF` 和 `MTTR` 已如表 19.3 所示。考虑 $q_i = MTTR/(MTTF+MTTR)$；然后计算每个项的失效概率。因此，失效概率（不可用性）$P(\cup_{i=1}^4 MC_i) = 8.724 \times 10^{-5}$。由此，$A = 1 - P(\cup_{i=1}^4 MC_i) = 0.9999135$。另见示例 19.3 组合模型分析

## 表 20.11 项概率

| 项 | 概率 |
| :--- | :--- |
| $P(MC_1)$ | $8.724 \times 10^{-5}$ |
| $P(MC_2)$ | $3.714 \times 10^{-9}$ |
| $P(MC_3)$ | $3.3526 \times 10^{-9}$ |
| $P(MC_4)$ | $2.5345 \times 10^{-10}$ |
| $P(MC_1 \cap MC_2)$ | $3.319 \times 10^{-11}$ |
| $P(MC_1 \cap MC_3)$ | $3.319 \times 10^{-11}$ |
| $P(MC_1 \cap MC_4)$ | $2.2124 \times 10^{-14}$ |
| $P(MC_2 \cap MC_3)$ | $2.2124 \times 10^{-14}$ |
| $P(MC_2 \cap MC_4)$ | $2.5097 \times 10^{-12}$ |
| $P(MC_3 \cap MC_4)$ | $2.5097 \times 10^{-12}$ |
| $P(MC_1 \cap MC_2 \cap MC_3)$ | $2.2124 \times 10^{-14}$ |
| $P(MC_1 \cap MC_3 \cap MC_4)$ | $2.2124 \times 10^{-14}$ |
| $P(MC_1 \cap MC_2 \cap MC_3 \cap MC_4)$ | $2.2124 \times 10^{-14}$ |

## 互交积和

本节介绍了基于互交积和（`SDP`）的可靠性和可用性计算方法，基于等式 $A \cup B = A \cup (A^c \cap B)$。考虑集合 $A=\{a,b,c,d\}$ 和 $B=\{e,f\}$ 在全空间 $\Omega=\{a,b,c,d,e,f,g,h\}$ 中；则有 $A^c=\{e,f,g,h\}$，从而 $A \cup B=\{a,b,c,d\} \cup \{e,f\}=\{a,b,c,d,e,f\}$。考虑三个集合，我们有 $A \cup B \cup C = A \cup (A^c \cap B) \cup (B^c \cap C)$。对于 $n$ 个集合，有 $\bigcup_{i=1}^n A_i = A_1 \cup (A_1^c \cap A_2) \cup (A_1^c \cap A_2^c \cap A_3) \dots \cup (A_1^c \cap \dots \cap A_{n-1}^c \cap A_n)$。

## 计算系统的性能、可靠性和可用性评估

因此，所有集合的集概率为 $P(\bigcup_{i=1}^{n} A_i) = P(A_1) + P(A_1^c \cap A_2) + P(A_1^c \cap A_2^c \cap A_3) + \dots + P(A_1^c \cap \dots \cap A_{n-1}^c \cap A_n)$。图 18.1 所示的 `RBD` 由三个组件 `b_1`, `b_2` 和 `b_3` 组成。该 `RBD` 有两条最小路径，分别为 `MP_1={b_1, b_2}` 和 `MP_2={b_1, b_3}`。每个最小路径由相应的逻辑函数表示：

$\Psi_{MP_1} = b_1 \wedge b_2$,

$\Psi_{MP_2} = b_1 \wedge b_3$.

集合 `MP_1^c` 由逻辑函数 $\Psi_{MP_1^c} = \overline{b_1 \wedge b_2} = \overline{b}_1 \vee \overline{b}_2$ 表示。集合 `MP_1^c \cap MP_2^c` 也由逻辑函数 $\Psi_{MP_1^c \cap MP_2^c} = (\overline{b}_1 \vee \overline{b}_2) \wedge (b_1 \wedge \overline{b}_3)$ 表示。

$\Psi_{MP_1^c \cap MP_2^c} = (\overline{b}_1 \wedge b_1 \wedge \overline{b}_3) \vee (\overline{b}_2 \wedge b_1 \wedge \overline{b}_3)$。使用表 18.3 所示的转换规则，从 `b_i` 得到 `x_i`，从 `\overline{b}_i` 得到 `1-x_i`。由于 $E(x_i) = p_i$ 且 $E(1-x_i) = 1-p_i = q_i$，有：

$P(MP_1) = P(\Psi_{MP_1}) = p_1 p_2$.

$P(MP_1^c \cap MP_2^c) = P(\Psi_{MP_1^c \cap MP_2^c}) = q_2 p_1 p_3$.

因此

$P(MP_1 \cup MP_2) = P(MP_1) + P(MP_1^c \cap MP_2) = p_1 p_2 + q_2 p_1 p_3$.

## 组合模型分析

示例 20.6。由图 18.1 所示 `RBD` 表示的系统由最小路径组成：`MP_1={b_1, b_2}`, `MP_2={b_1, b_3}` 和 `MP_3={b_2, b_3}`。相应的函数为：

$\Psi_{MP_1} = b_1 \wedge b_2$,

$\Psi_{MP_2} = b_1 \wedge b_3$,

$\Psi_{MP_3} = b_2 \wedge b_3$.。`MP_i`, `MP_i'` 的补集也由逻辑函数 $\Psi_{MP_i^c} = \overline{b}_1 \vee \overline{b}_2$ 表示 `MP_1^c`，$\overline{b}_1 \vee \overline{b}_3$ 表示 `MP_2^c`，以及 $\overline{b}_2 \vee \overline{b}_3$ 表示 `MP_3^c`。利用上述结果，我们得到 $P(MP_1 \cup MP_2 \cup MP_3) = 0.9555$。$\square$

# 组合模型分析

$MC_4 \Rightarrow \overline{M_1} \wedge \overline{M_2} \wedge M_3$。

`MC_i` 的补集即 `MC_i^c, i = {1, 2, 3, 4}`，表示为：

$MC_1^c \Rightarrow \overline{P_1} \vee \overline{P_2} = P_1 \vee P_2$,

$MC_2^c \Rightarrow \overline{P_1} \wedge \overline{M_3} = P_1 \vee M_2 \vee M_3$,

$MC_3^c \Rightarrow \overline{M_1} \wedge \overline{P_2} = M_1 \vee M_3 \vee P_2$,

以及

$MC_4^c \Rightarrow \overline{M_2} \wedge \overline{M_3} = M_1 \vee M_2 \vee M_3$。

根据上述结果，我们得到：

$MC_1^c \cap MC_2 \Rightarrow (P_1 \vee P_2) \wedge (\overline{P_1} \wedge M_2 \wedge M_3) = \overline{P_1} \vee P_2 \wedge M_2 \wedge M_3$,

$MC_1^c \cap MC_2^c \cap MC_3 \Rightarrow (P_1 \vee P_2) \wedge (P_1 \vee M_2 \vee M_3) \wedge (M_1 \wedge M_3 \wedge P_2) = P_1 \wedge P_2 \wedge M_1 \wedge M_3$,

$MC_1^c \cap MC_2^c \cap MC_3^c \cap MC_4 \Rightarrow (P_1 \vee P_2) \wedge (P_1 \vee M_2 \vee M_3) \wedge (M_1 \vee M_3 \vee P_2) \wedge (\overline{M_1} \wedge \overline{M_2} \wedge M_3) = P_1 \wedge P_2 \wedge M_1 \wedge M_2 \wedge M_3$。

将 `q_i` 和 `p_i` 分别视为组件 `i` 的失效概率和成功概率，我们有：

$Q(MC_1) = q_{p1} \times q_{p2}$,

$Q(MC_1^c \cap MC_2) = q_{p1} \times p_{p2} \times q_{m2} \times q_{m3}$,

$Q(MC_1^c \cap MC_2^c \cap MC_3) = p_{p1} \times q_{p2} \times q_{m1} \times q_{m3}$,

$Q(MC_1^c \cap MC_2^c \cap MC_3^c \cap MC_4) = p_{p1} \times p_{p2} \times q_{m1} \times q_{m2} \times q_{m3}$。

因此，失效概率为：

$Q = Q(MC_1) + Q(MC_1^c \cap MC_2) + Q(MC_1^c \cap MC_2^c \cap MC_3) + Q(MC_1^c \cap MC_2^c \cap MC_3^c \cap MC_4)$。

由此：

$Q = q_{p1} \times q_{p2} \times q_{p1} \times p_{p2} \times q_{m2} \times q_{m3} + p_{p1} \times q_{p2} \times q_{m1} \times q_{m3} + p_{p1} \times p_{p2} \times q_{m1} \times q_{m2} \times q_{m3}$。

从 `Q` 得到成功概率 `P = 1 - Q`。组件 `i` 的不可用性为 `q_i = MTTR_i/(MTTF_i+MTTR_i)`，相应的可用性 `p_i=1-q_i`。根据表 19.3 所示的 `MTTR` 值，系统可用性 `A = P` 为 `0.999916`。

![](img/2d1450514bb14a0cdf0eb5048614afab_216_0.png)

## 20.7 边界估计方法

本节介绍了一些估计概率边界（即（不）可靠性和（不）可用性）的方法。这些方法可以比精确解法更快地提供精确概率的近似值，特别是在考虑大型模型时 [224]。

### 20.7.1 基于包含排斥原理的方法

如第 20.5 节所示，包含排斥法（`IEM`）在采用最小路径时产生连续的可靠性（及可用性）上限和下界，在考虑最小割集时产生相应的不可靠性（及不可用性）下界。因此，对于高可靠（高可用）系统，割集比路径更有用。另一方面，如果成功概率较低，路径则更好。

考虑图 20.10.a 所示的桥型模型。该模型具有最小路径 `MP_1={c_1, c_2}`、`MP_2={c_4, c_5}`、`MP_3={c_1, c_3, c_5}` 和 `MP_4={c_2, c_3, c_4}`，以及四个最小割集 `MC_1={c_1, c_4}`、`MC_2={c_2, c_5}`、`MC_3={c_1, c_3, c_5}` 和 `MC_4={c_2, c_3, c_4}`。

> 6 参见示例 20.5.1 所示的结果。

让我们先取最小割集，使用公式 20.5.2 的第一项，得到：

$Q_1 = P(MC_1) + P(MC_2) + P(MC_3) + P(MC_4) = q_1q_4 + q_2q_5 + q_2q_5 + q_1q_5$，其中 $q_i = 1 - p_i$ 是组件 `i` 的失效概率。如果 $p_i = 0.9, i \in \{1,2,3,4,5\}$，则 $Q_1 = 0.4, P_1 = 1 - Q_1 = 0.6$。使用公式 20.5.2 的第二项得到：

$Q_2 = Q_1 - P(MC_1 \cap MC_2) - P(MC_1 \cap MC_3) - P(MC_1 \cap MC_4) - P(MC_2 \cap MC_3) - P(MC_2 \cap MC_4) - P(MC_3 \cap MC_4) = Q_1 - q_1q_4q_2q_5 - q_1q_4q_1q_3q_5 - q_1q_4q_2q_3q_4 - q_2q_5q_1q_3q_5 - q_2q_5q_2q_3q_4 - q_1q_3q_5q_2q_3q_4$，$Q_2 = 0.0249, P_2 = 1 - Q_2 = 0.9751$。现在考虑公式 20.5.2 的第三项得到：

$Q_3 = Q_2 + P(MC_1 \cap MC_2 \cap MC_3) + P(MC_1 \cap MC_2 \cap MC_4) + P(MC_1 \cap MC_3 \cap MC_4) + P(MC_2 \cap MC_3 \cap MC_4) = Q_2 + q_1q_2q_3q_4q_5$，因此 $Q_3 = 0.0213, P_3 = 1 - Q_3 = 0.9787$。现在，最后考虑公式 20.5.2 的第四项得到：

$Q_4 = Q_3 - P(MC_1 \cap MC_2 \cap MC_3 \cap MC_4) = Q_3 - q_1q_2q_3q_4q_5$，我们得到 $Q_4 = 0.02152, P_4 = 0.97848$，$Q_4$ 和 $P_4$ 是精确结果。

现在考虑最小路径并取公式 20.5.2 的第一项：

$P_1 = P(MP_1) + P(MP_2) + P(MP_3) + P(MP_4) = p_1p_2 + p_3p_5 + p_3p_5 + p_4p_5$。如果 $p_i = 0.9, i \in \{1,2,3,4,5\}$,则 $P_1 = 3.078$。这个边界无用，因为大于 1。现在加上公式 20.5.2 的第二项得到：

$P_2 = P_1 - P(MP_1 \cap MP_2) - P(MP_1 \cap MP_3) - P(MP_1 \cap MP_4) - P(MP_2 \cap MP_3) - P(MP_2 \cap MP_4) - P(MP_3 \cap MP_4) = P_1 - p_1p_2p_4p_5 - p_1p_2p_1p_3p_5 - p_1p_2p_2p_3p_4 - p_3p_5p_1p_3p_5 - p_3p_5p_2p_3p_4 - p_1p_3p_5p_2p_3p_4$，因此 $P_2 = 0.72929$。现在考虑公式 20.5.2 的第三项得到：

$P_3 = P_2 + P(MP_1 \cap MP_2 \cap MP_3) + P(MP_1 \cap MP_2 \cap MP_4) + P(MP_1 \cap MP_3 \cap MP_4) + P(MP_2 \cap MP_3 \cap MP_4) = P_2 + p_1p_2p_3p_4p_5$，因此我们得到 $P_3 = 1.56897$。再次，这个边界没有用，因为它大于 1。最后，为了考虑公式 20.5.2 的第四项，得到：

$P_4 = P_3 - P(MP_1 \cap MP_2 \cap MP_3 \cap MP_4) = P_3 - p_1p_2p_3p_4p_5$，因此我们得到 $P_4 = 0_97848$，这是精确结果。

现在假设 $p = 0.99$。通过最小割集和路径得到的可靠性边界如表 20.12 所示，考虑 $i = \{1,2,3,4\}$。观察发现，采用第一项考虑最小割集就已经达到了精确结果。另一方面，最后结果外，从最小路径得到的边界都是无用的。

### 表 20.12

从最小割集和路径计算的可靠性边界 – 可靠系统

| i | $P_1$ - 最小割集 | $P_1$ - 最小路径 |
|---|---|---|
| 1 | 0.999798 | 3.9008 |
| 2 | 0.999798 | -1.85317 |
| 3 | 0.999798 | 1.95079 |
| 4 | 0.999798 | 0.999798 |

然而，对于极不可靠的系统，它们更好；即当 $p$ 很小（$q$ 接近 1）时，最小割集比最小路径更有用。假设 $q = 0.95$ ($p = 1-q$)。表 20.13 显示了通过最小割集和路径得到的可靠性边界。值得注意的是，对于 $i \in \{1,2,3\}$，通过最小割集得到的边界是用的，边界要么大于 1 要小于 0。只有在 $i=4$ 时才有结果。这是精确结果。但当使用最小路径时，边界为

## 20.7.2 基于不交积和的方法

`SDP` 方法在采用最小路径时计算系统可靠性（可用性）的连续下界。相反，当采用最小割集时，该方法提供不可靠性（可用性）的下界，从而提供系统可靠性（可用性）的上限。与通过加和减项来处理连续上限和下界的 `IEM` 不同，`SDP` 在计算边界时仅进行加法。
