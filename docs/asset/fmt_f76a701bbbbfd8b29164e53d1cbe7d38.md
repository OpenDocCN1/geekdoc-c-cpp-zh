
- 使用线性规划计算多项式模板边界，以及
- 使用 SOS 规划确定新策略，
直到达到不动点。策略迭代在 `$F^{\mathcal{R}}$` 的后置点集上导航，并需要先验地从一个不动点 `$w^0$` 开始。它的作用类似于一个收缩算子，并且可以在任何时间中断。感兴趣的读者可以参考 [52, 68]。

### 6.3.3 策略

策略迭代可用于计算单调自映射的固定点，该映射定义为一组仿射单调自映射的下界。我们建议设计一种策略迭代算法来计算 `$F^{\mathcal{R}}$` 的不动点。在本节中，我们给出了多项式模板背景下策略的正式定义，并定义了仿射单调自映射族。我们没有将策略的概念应用在 `$F^{\mathcal{R}}$` 上，而是应用在 `$F_i^{\mathcal{R}}$` 上，利用了对于所有 `$i \in \mathcal{I}$`，`$F_i^{\mathcal{R}}$` 是某个最小化问题的最优值这一事实。

策略迭代需要一个*选择*属性，即当给定元素 `$w \in \mathcal{F}(\mathbb{P}, \mathbb{R})$` 一个达到下界的策略时。在我们的语文中，由于我们将策略应用于 `$F^{\mathcal{R}}$`，这意味着计算 `$F^{\mathcal{R}}$` 时涉及的最小化问题有一个最优解。在我们的情况下，对于 `$w \in \mathcal{F}(\mathbb{P}, \mathbb{R})$` 和 `$p \in \mathbb{P}$`，最优解是一个向量 `$(\lambda, \sigma, \mu) \in \mathcal{F}(\mathbb{P}, \mathbb{R}_+) \times \Sigma[x] \times \Sigma[x]^i$`；使得利用 (6.3)，我们得到：

$$(F^{\mathcal{R}}(w))(p) = p \circ T^i + \sum_{q \in \mathcal{V}} \lambda(w(q) - q) - (\mu, r^i) + \sigma \text{ and } \deg(\sigma) \leq 2m \deg T^i, \deg(\mu, r^i) \leq 2m \deg T^i. \quad (6.5)$$

观察到等式 (6.5)，`$(F^{\mathcal{R}}(w))(p)$` 是一个标量，而右侧是一个多项式。该方程中的等意味着该多项式是一个常数多项式。我们引入 SOS 问题 `$(F^{\mathcal{R}}(w))(p)$` 的可行解集：

$$(Sol(w, i, p) = \{(\lambda, \sigma, \mu) \in \mathcal{F}(\mathbb{P}, \mathbb{R}_+) \times \Sigma[x] \times \Sigma[x]^i \text{ s. t. Eq. (6.5) holds}\}). \quad (6.6)$$

## 模板分析

由于策略迭代算法可以在任何步骤停止并仍然提供可靠的过近似，当 `Sol(w, i, p) = \emptyset` 时我们停止迭代。现在，我们对使得 `Sol(w, i, p)` 非空的元素 `$w \in \mathcal{F}(\mathbb{P}, \mathbb{R})$` 感兴趣：

$$FS(\mathbb{P}, \mathbb{R}) = \left\{ w \in \mathcal{F}(\mathbb{P}, \mathbb{R}) \ i \in \mathcal{I}, p \in \mathbb{P}, Sol(w, i, p) \neq \emptyset \right\} \quad (6.7)$$

符号 `$FS(\mathbb{P}, \mathbb{R})$` 引入自 [91]，用于定义满足 `$Sol(w, i, p) \neq \emptyset$` 的元素 `$w \in \mathcal{F}(\mathbb{P}, \mathbb{R})$`。在 [91, 第4.3节] 中，我们使用了 Slater 严格约束限定条件。在当前的非线性区域，我们无法使用相同的条件，这导致 `$FS(\mathbb{P}, \mathbb{R})$` 产生了一个更复杂的定义。

最后，我们可以策略定义为一种映射，它对于所有的 `$w \in FS(\mathbb{P}, \mathbb{R})$`，所有的 `$i \in \mathcal{I}$` 以及所有的 `$p \in \mathbb{P}$`，选择 `Sol(w, i, p)` 的向量。更正式地，我们有如下定义：

**定义 6.8** *SOS 策略迭代中的策略.* *一个映射 `$\pi: FS(\mathbb{P}, \mathbb{R}) \mapsto (\mathcal{I} \times \mathbb{P}) \mapsto \mathcal{F}(\mathbb{P}, \mathbb{R}_+) \times \Sigma[x] \times \Sigma[x^{\vee}] \times \Sigma[x^{n}]$`，使得：`$w \in FS(\mathbb{P}, \mathbb{R}), i \in \mathcal{I}, p \in \mathbb{P}, \pi(w)(i, p) = Sol(w, i, p)$`。*

我们用 `$\Pi$` 表示策略集。对于 `$\pi \in \Pi$`，令 `$\pi_{\lambda}$` 为从 `$FS(\mathbb{P}, \mathbb{R})$` 到 `$(\mathcal{I} \times \mathbb{P}) \mapsto \mathcal{F}(\mathbb{P}, \mathbb{R}_+)$` 的映射，它与 `$w \in FS(\mathbb{P}, \mathbb{R})$` 和 `$i \in \mathcal{I}, p \in \mathbb{P}$` 关联 `$\pi(w)(i, p)$` 的第一个元组，即 `$\pi(w)(i, p) = (\lambda, \sigma, \mu)$`。

如前，当策略固定时，策略迭代利用了映射的线性。对于 `$\pi \in \Pi, w \in FS(\mathbb{P}, \mathbb{R}), i \in \mathcal{I}$` 和 `$p \in \mathbb{P}$`，且 `$\lambda = \pi_{\lambda}(i, p)$`，我们定义映射 `$\phi_{w,i,p}^{\pi}: FS(\mathbb{P}, \mathbb{R}) \to \mathbb{R}$` 如下：

$$v \mapsto \phi_{w,i,p}^{\pi}(v) = \sum_{q \in \Lambda} \lambda(q)v(q) + (F_i^{\pi}(w))(p) - \sum_{q \in \Lambda} \lambda(q)w(q). \quad (6.8)$$

那么，对于 `$\pi \in \Pi$`，我们对于所有的 `$w \in FS(\mathbb{P}, \mathbb{R})$` 定义从 `$\mathcal{F}(\mathbb{P}, \mathbb{R})$` 到 `$\mathcal{F}(\mathbb{P}, \mathbb{R})$` 的映射 `$\Phi^{\pi}(w)$`。令 `$v \in \mathcal{F}(\mathbb{P}, \mathbb{R})$` 和 `$p \in \mathbb{P}$`：

$$\Phi^{\pi}(w)(p) = \sup_{i \in \mathcal{I}} \phi_{w,i,p}^{\pi}(v). \quad (6.9)$$

**示例 6.9.** *让我们考虑示例 6.3 和函数 `$w^0(q_1) = w^0(q_2) = 2.19$` 以及 `$w^0(0) = 0$。存在 SOS 多项式 `$\tilde{\mu}$` 和 `$\tilde{\sigma}$`使得对于所有的 `$x \in \mathbb{R}$`：*

$$(F_1^{\tilde{\mu}})(q_1) = (0.687x_1 + 0.555x_2 - 0.0001x_1^2) + \tilde{\lambda}(q_1)(2.19 - x_1^2) + \tilde{\lambda}(q_2)(2.19 - x_2^2) - \tilde{\mu}(x)(1 - x_1^2) + \tilde{\sigma}(x) = 1.5503$$，其中 `$\tilde{\lambda}(q_1) = \tilde{\lambda}(q_2) = 0$` 且 `$\tilde{\lambda}(p) = 2.0331$`。这意味着 `$\tilde{\lambda}, \tilde{\mu}$` 和 `$\tilde{\sigma}$` 使得 `$0.687x_1 + 0.555x_2 - 0.0001x_1^2 + \tilde{\lambda}(q_1)(2.19-x_1^2) + \tilde{\lambda}(q_2)(2.19-x_2^2) - \tilde{\mu}(x)(1-x_1^2) + \tilde{\sigma}(x)$` 实际上是一个常数多项式。*

那么 `$(\lambda, \tilde{\mu}, \tilde{\sigma}) \in \text{Sol}(w^0, 1, q_1)$`，我们可以定义策略 `$\pi(w^0)$` 使得 `$\pi(w^0)(1, q_1) = (0, \tilde{\mu})$`，因此 `$\lambda(w^0)(1, q_1) = (0, 0, 2.0331)$`。我们可以对于 `$v \in \mathcal{F}(\mathbb{P}, \mathbb{R})$` 定义仿射映射：`$\Phi_{w^0,q_1}^w(v) = \lambda(q_1)v(q_1) + \lambda(q_2)v(q_2) + \lambda(p)(p) + (F^R(w))(q_1) - \lambda(q_1)w(q_1) - \lambda(q_2)w(q_2) - 2.19v(p) + 1.5503$`。

让我们用 `$\mathcal{F}(\mathbb{P}, \mathbb{R})$` 表示在 `$p$` 上的有限值函数，即如果对于所有的 `$p \in \mathbb{P}$`，`$g(p) \in \mathbb{R}$`则 `$g \in \mathcal{F}(\mathbb{P}, \mathbb{R})$`。

## 命题 6.10 ($\Phi_{i,p}^w$ 的性质)

令 `$\pi \in \Pi, w \in FS(\mathbb{P}, \mathbb{R})$` 且 `$(i, p) \in \mathcal{I} \times \mathbb{P}$`。令 `$a = \pi(w)(i,p)$`。以下性质成立：

1. `$\Phi_{w,i,p}$` 在 `$\mathcal{F}(\mathbb{P}, \mathbb{R})$` 上是仿射的
2. `$\Phi_{w,i,p}^w$` 在 `$\mathcal{F}(\mathbb{P}, \mathbb{R})$` 上是单调的
3. 对于所有的 `$v \in \mathcal{F}(\mathbb{P}, \mathbb{R})$`，`$F^R(v) \leq \Phi_{w,i,p}^w(v)$`;
4. `$\Phi_{w,i,p}^w(w) = F^R(w)(p)$`。

命题 6.10 给出的性质暗示了映射 `$\Phi_{\pi}^w(w)$` 的一些有用性质。

## 命题 6.11 ($\Phi_{\pi}^w(w)$ 的性质)

令 `$\pi \in \Pi$` 和 `$w \in FS(\mathbb{P}, \mathbb{R})$`。以下性质成立：

1. `$\Phi_{\pi}^{(w)}$` 在 `$\mathcal{F}(\mathbb{P}, \mathbb{R})$` 上单调的
2. `$F^R \leq \Phi_{\pi}^{(w)}(w)$`;
3. `$\Phi_{\pi}^{(w)}(w) = F^R$`。

假设 `$\Phi_w^{(w)}$` 的最小不动点 `$\in \mathcal{F}(\mathbb{P}, \mathbb{R})$`。则 `$L$` 可以作为线性规划的唯一最优解计算：

$$\forall (i,p) \in \mathcal{I} \times \mathbb{P},$$

$$\inf_{p' \in \mathbb{P}} \begin{cases} v(p') \\ \Phi_{i,w,p}^{(w)}(i,p)(v) \leq v(p), \\ \forall q \in \mathbb{P}, \\ X^{Int^R}(q) \leq v(q) \end{cases} \quad (6.10)$$

记得函数 `$g:\mathbb{D} \to \mathbb{R}$` 在 `$x$` 处上连续的，当且仅当对于收敛于 `$x$` 的 `$(x_n)_{n \in \mathbb{N}}$`，`$\limsup_{n\to\infty} g(x_n) \leq g(x)$`。

## 命题 6.12

对于 `$p \in \mathbb{P}$`，`$w \to F^R(w)(p)$` 在 `$FS(\mathbb{P}, \mathbb{R}) \cap \mathcal{F}(\mathbb{P}, \mathbb{R})$` 上是上连续的。

## 基于模板的分析

`input`: `$w^0 \in F(\mathbb{P}, \mathbb{R})$`，`$F^R$` 的一个后不动点

`output`: 如果 `$\forall k \in \mathbb{N}, w^k \in \mathcal{FS}(\mathbb{P}, \mathbb{R})$`，则一个不动点 `$w = F^R(w)$`；否则返回一个后不动点

```
k=0;
while fixpoint not reached
  begin 为当前迭代值 $w^k$ 计算下一个策略 $\pi$
  使用 Eq. (6.4) 和 Eq. (6.3) 计算 $F^R(w^k)$
  if $w^k \in \mathcal{FS}(\mathbb{P}, \mathbb{R})$ then
    Define $\pi(w^k)$;
  else
    return $w^k$;
  end;
  begin 计算下一次迭代 $w^{k+1}$
  定义 $\pi^{\pi(w^k)}$ 并计算 $w^{\pi(w^k)}$ 的最小不动点 $w^{k+1}$
  Problem (6.10);
  k=k+1;
end
```

图 6.1. 基于 SOS 的 PPS 程序策略迭代算法。

### 6.3.4 策略迭代

现在我们描述策略迭代算法。假设我们在 `$F(\mathbb{P}, \mathbb{R})$` 中有一个 `$F^R$` 的后不动点 `$w^0$`。

让我们逐步详细介绍图 6.1 所示算法。在第 1 行，算法初始化，因此 `$k=0$`。在第 4 行，我们使用 Eq. (6.4) 计算 `$F^R(w^k)$` 并解决 Eq. (6.3) 涉及的 SOS 问题。在第 6 行，如果所有 `$i \in \mathcal{I}$` 和所有 `$p \in \mathbb{P}$`，Eq. (6.3) 涉及的 SOS 问题都有最优解，则策略 `$\pi$`可用，我们可以选择 Eq. (6.3) 问题的任何最优解作为策略。如果不存在最优解，则算法停止并返回 `$w^k$`。现在，如果已定义策略 `$\pi$`，算法跳转到第 12 行，我们根据 Eq. (6.9) 定义 `$w^{\pi(w^k)}$`。然后，求解 LP 问题 (6.10) 并定义新的模板边界 `$w^{k+1}$` 为 `$w^{\pi(w^k)}$` 的最小不动点。最后，在第 13 行，`$k$` 递增。

如果某个 `$k \in \mathbb{N}, w^k \notin \mathcal{FS}(\mathbb{P}, \mathbb{R})$` 且 `$w^{k-1} \in \mathcal{FS}(\mathbb{P}, \mathbb{R})$`，则算法停止并返回 `$w^k$`。因此，对于所有 `$i \geq k$`，设置 `$w^i = w^k$`。

定理 6.13 (算法 6.1 的收敛性)。满足以下结论：

- 1. 对于所有 `$k \in \mathbb{N}, w^k \in F(\mathbb{P}, \mathbb{R})$` 且 `$F^R(w^k) \leq w^k$`。
- 2. 算法生成的序列 `$(w^k)_{k \geq 0}$` 是递减的并收敛。
- 3. 令 `$w^{\infty} = \lim_{k \to \infty} w^k$`，则 `$F^R(w^{\infty}) \leq w^{\infty}$`。此外，如果对于所有 `$k \in \mathbb{N}, w^k \in \mathcal{FS}(\mathbb{P}, \mathbb{R})$` 且 `$w^{\infty} \in \mathcal{FS}(\mathbb{P}, \mathbb{R})$`，则 `$F^R(w^{\infty}) = w^{\infty}$`。

## 6.4 示例

回我们的运行示例由以下分段多项式系统给出：(`$X^{Init}, \{X^1, X^2\}, \{T^1, T^2\}$`)，其中：

```
$X^{Init} = [-1, 1] \times [-1, 1]$
$X^1 = \{x \in \mathbb{R}^2 | |x_2|^2 + 1 \leq 0\}$
$X^2 = \{x \in \mathbb{R}^2 | |x_2|^2 - 1 < 0\}$
```

相对于划分 `$\{X^1, X^2\}$` 的函数为：

```
$T^1(x_1, x_2) = (0.6872x_1 + 0.558x_2 - 0.0001x_1x_2 - 0.292x_1 + 0.0773x_2)$
$T^2(x_1, x_2) = (0.3691x_1 + 0.532x_2 - 0.0001x_1x_2 - 0.27x_1 + 0.12x_2)$
```

第一步包括构造模板基和作为 Problem (5.56) 解的可达边界 `$w$`。我们将 `$p$` 的次数固定为 6。从 MATLAB 生成的模板 `$p$` 定义如下：
