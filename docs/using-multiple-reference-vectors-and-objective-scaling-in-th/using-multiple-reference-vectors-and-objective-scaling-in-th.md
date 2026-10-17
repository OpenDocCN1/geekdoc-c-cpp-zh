
# 可行性泵中使用多参考向量与目标缩放的使用指南

Gioni Mei<sup>a</sup> Timo Berthold<sup>b,*</sup> Domenico Salvagnin<sup>c</sup>

* *a 德国柏林 Zuse 研究所, Takstraße 7, 14195
* *b 德国法兰克福 Fair Isac Deutschland GmbH, An der Weise 10, 60322
* *c 意大利帕多瓦大学, Via Gradenigo 6/B, 35131, Padova

## 文章摘要

关键词：混合整数规划、原始启发式算法

可行性泵（Feasibility Pump, FP）是混合整数规划（MIP）中最为人知的原始启发式算法之一：超过 15 篇论文对其所有步骤提出了各种修改。至今为止，还没有变体考虑跨多次迭代的信息，但它们都保持了朝着单一参考点优化的原则。在本文中我们评估了在 FP 算法所有阶段中使用多个参考向量的效果。特别是，我们使用主循环期间获得的 LP 可行向量在进入计算核心之前收紧变量域，我们将该过程称为 mRENS。我们考虑在 mRENS 中引入多个参考向量以进一步探索优化方向，并引入替代性的目标缩放项，以平衡距离函数与原始 MIP 目标之间的贡献。

我们的计算实验表明，新方法可以提高在广义 MIP 测试集上的性能。具体而言，我们的改进在嵌入式设置中提供了 29.3% 的解改进和 4.0% 的运行改进，在大型 MIP 实例集上的迭代次数减少了 16.0%。此外，该方法的成功率在前几次迭代中持续增加。我们还观察到适中的性能，这使得我们版本的 FP 适用于该算法的两个主要用例。

> * 通讯作者。
> 邮箱：timoberthold@fico.com (T. Berthold)。

# 1. 引言

混合整数规划广泛用于建模和解决源于现实世界应用的挑战性优化问题。我们用矩阵和向量符号将混合整数规划（MIP）定义如下：

**定义 1.1.**（混合整数规划）设 $m, n \in \mathbb{Z}_{\ge0}$。给定矩阵 $A \in \mathbb{Q}^{m\times n}$，向量 $b \in \mathbb{Q}^{m}, c \in \mathbb{Q}^{n}, u \in \mathbb{Q}^{n} \cup \{\pm\infty\}$ 以及索引集 $I \in \mathbb{N} :=\{1,\dots,n\}$，形式如下的问题：

```
\begin{aligned} \min_{x\in X} & & c^T x \ \text{s.t.} & & Ax \le b \ & & l \le x \le u \ & & x_j \in \mathbb{Z} \quad \text{for all } j\in I, \end{aligned} (1)
```

被称为混合整数规划（MIP）。

为给定的混合整数规划（MIP）模型寻找可行解是非常重要的，这是一个 $NP$-完全问题，在实践中可能极其困难，且通常通过原始启发式算法来处理 [1,2]。寻找 MIP 初始可行解的最成功方案是可行性泵，它最初由 Fischetti, Glover 和 Lodi 提出 [3]。

所有 FP 算法的核心思想是构造两个点序列，希望它们收敛到给定优化问题（即 MIP）的可行解。其中一个序列的点对于连续松弛（通常是 LP 松弛）是可行的，但在整数上可能是不可行的。另一个点序列是整数的，但可能会违反某些施加的（线性）约束。每个序列的下一个点总是通过最小化与该序列上上点的距离来生成的，在两种情况下都使用不同的度量（例如 $\ell_{1}$ 和 $\ell_{2}$ 范数）。关于 FP 变体的概述，请参考 [4]。

本文的结构如下：在第 2 节中，我们描述了 FP 的核心思想，专注于可行性泵 2.0 (OFP)，这是我们工作的基础。在第 3 和 4 节中，我们描述了两个贡献之一，即 FP 算法所有阶段的变体，在每个阶段考虑多个参考向量。第 5 节介绍了我们的第二个贡献，即应用替代的目标缩放方法，以更好地平衡最优性和可行性的考虑。最后，在第 6 和 7 节中，我们展示了计算结果，并在嵌入式和独立设置下进行了详细比较。

# 2. 可行性泵 2.0

可行性泵（FP）最初由 Fischetti 等人引入 [3]。在算法（Algorithm 1）中，我们概述了 FP 的原理。在主循环（泵循环）中，算法构造了两个向量序列 $\{\tilde{x}^k\}_{k=1}^K$ 和 $\{\hat{x}^k\}_{k=1}^K$，其中 $K$ 有限。这些序列满足 MIP 的可行性要求，更准确地说，第一个序列包含 LP 可行向量 $P = \{x \in \mathbb{R}^n | Ax \le b, l \le x \le u\}$，第二个序列包含整数向量，即满足完整性约束但不是 LP 可行的。FP 的目标是迭代减少两个序列之间的距离并收敛到可行解。两个向量 $\tilde{x}^k$ 和 $\hat{x}^k$ 之间的距离定义为：

$$\Delta(\tilde{x}^k, \hat{x}^k) := \sum_{j \in I} |\tilde{x}^k - \hat{x}^k|$$

在每次迭代中，$\hat{x}^k$ 都通过最小化与序列上上一个点的距离来生成，在两种情况下都使用不同的度量（例如 $\ell_{1}$ 和 $\ell_{2}$ 范数）。

步骤优先考虑质量而非可行性，并逐渐增加可行性相对于解质量的优先级。欧几里得范数 $\|\Delta\|_2$ 和 $\|c\|_2$ 的目的是将项 $\Delta(x, \tilde{x}^k)$ 和 $c^T x$ 置于同一尺度上。其中 $\|\Delta\|_2$ 是 $\Delta(x, \tilde{x}^k)$ 中目标函数向量的欧几里得范数，等于 $\sqrt{|\mathcal{I}|}$。

OFP 在重启机制中引入了调整。重新访问整数向量并不意味着算法停止，因为参数 $\alpha_k$ 是动态调整的。因此，如果当前整数向量 $\tilde{x}^k$ 等于 $\bar{x}$ 且 $r \in \{1, \dots, k-2\}$，作者建议仅当 $\alpha_l - \alpha_k < \delta$ 时才应用重启程序，其中 $\delta \in [0, 1]$ 为固定阈值参数。

Fischetti 和 Salvagnin [7] 引入了可行泵（FP2.0），它在 FP 的舍入步骤中集成了约束规划技术。注意，OFP 和 FP2.0 可以结合。所得算法被称为 *目标可行性泵 2.0 (FP2)*，并被认为是我们实现的基准算法。参见 Berthold 等 [4] 的概述以了解（更多）FP 的变体。

# 3. 阶段 3 中的多个参考向量

当嵌入 MIP 求解器时，原始启发式通常只运行很短时间。因此，FP 中计算量巨大的阶段 3 通常被禁用，或仅在某些情况下使用，例如，最近整数向量到 LP 多面体 $P$ 的距离低于某一阈值。因此，我们设计了一种替代的阶段 3，它使用从 FP 和大邻域搜索启发式 RENS [8,9] 获取的多个参考向量。值得注意的是，传统的阶段 3 求解的是一个与原始问题同维的辅助 MIP，而我们的替代方法将求解一个子 MIP，该子 MIP 可以显著小得多，因此在实践中求解速度快得多。

### 3.1. 多参考 RENS

RENS 的核心思想是在其 LP 弛弛 $\bar{x}^0$ 的最优解附近搜索 MIP 的解。具体而言，RENS 根据整数变量在 $\bar{x}^0$ 中的值，对原始 MIP 求解一个整数变量边界更紧凑的子 MIP。为此，对于每个 $j \in Z$，如果 $\bar{x}^0$ 是整数，则 $x_j$ 固定在该值；否则，$x_j$ 的边界被收紧到 $\bar{x}^0$ 最近的整数值，$L_j$ 设置为 $[L_j^0]$，$u_j$ 设置为 $[U_j^0]$。总结来说，RENS 求解子 MIP

```
$\min \min x \in \mathbb{R}^n
Ax \leq b
ns.t.
L_j \leq x_j \leq u_j \text{for all } j \notin \mathcal{I}.
[L_j^0] \leq x_j \leq [U_j^0] \text{for all } j \in \mathcal{I}.
x_j \in \mathbb{Z} \text{for all } j \in \mathcal{I}$.
```

在实践中，如果只有一小比例的整数变量被分配了更紧的边界，求解 (3) 可能会产生计算开销。相反，在许多情况下，RENS 收紧了过多的变量边界，导致 (3) 不可行 [8]。在接下来，我们建议将 RENS 与从 FP 阶段 1 和阶段 2 获取的信息结合。通过循环，FP 生成了一系列 LP 可行的向量 $\tilde{x}^0, \dots, \tilde{x}^k$，这些向量可以作为 RENS 的参考向量。设 $\tilde{X}$ 为 $\{\tilde{x}^0, \dots, \tilde{x}^k\}$ 的子集。我们提出了改进版的 RENS，其中变量边界根据它们在 $\tilde{X}$ 向量中所取的值进行收紧。更准确地说，我们称之为多参考 RENS (mRENS)，对于每个 $j \in \mathcal{I}$，我们将 $l_j$ 设置为 $[\min_{x \in \tilde{X}} x_j]$，并将 $u_j$ 设置为 $[\max_{x \in \tilde{X}} x_j]$。总结来说，mRENS 求解子 MIP

```
$$\begin{aligned} \min_{x \in \mathbb{R}^n} & c^T x \ \text{s.t.} & Ax \leq b \\ l_j \leq x_j \leq u_j & \text{for all } j \notin \mathcal{I}. \\ [\min_{x \in \tilde{X}} \tilde{x}_j] \leq x_j \leq [\max_{x \in \tilde{X}} \tilde{x}_j] & \text{for all } j \in \mathcal{I}. \\ x_j \in Z & \text{for all } j \in \mathcal{I}. \end{aligned}$ (4)
```

注意如果 $\tilde{x}^0 \in \tilde{X}$，则 RENS 子 MIP 本身是 mRENS 子 MIP 的子 MIP。

# 4. 阶段 1 和阶段 2 中的多个参考向量

接下来，我们研究如何在阶段 1 和阶段 2 中使用多个参考向量。所述，投影步骤的目标涉及到当前迭代获取的整数向量 $\tilde{x}^k$ 的距离。从几何角度来看，距离函数指向一个可能违反 MIP 完整性约束的方向，其系数取决于 $\tilde{x}^k$ 的值，属于 $\{-1, 0, 1\}$，这使得可能的距离函数减少到 $3^n$。我们通过考虑多个整数向量（见 (2)）距离函数的锥组合来扩大这个集合可能会导致可行的 MIP 解或容易舍入的 LP 解。此外，它们可以在当前距离函数系数为零的维度上作为“打破者”。设 $\mathcal{L} = \{1, \dots, k\}$ 为循环期间获取的整数向量集。通过 $\Delta(x, \tilde{X}, \Lambda_{\mathcal{L}})$，我们表示到整数向量 $\tilde{x}^i, i \in \mathcal{L}$ 的 $L_1$ 距离的锥组合，更精确地说：

```
$\Delta(x, \tilde{X}, \Lambda_{\mathcal{L}}) := \sum_{i \in \mathcal{L}} \lambda_i \Delta(x, \tilde{x}^i),$ (5)
```

其中 $\Lambda_{\mathcal{L}} = \{\lambda_1, \dots, \lambda_k\}$，对于所有 $i \in \mathcal{L}$ $\lambda_i \geq 0$ 是锥权重，$\tilde{X}_{\mathcal{L}} = \{\tilde{x}^1, \dots, \tilde{x}^k\}$。

我们建议在 FP 的投影步骤中使用 (5) 的变体。因此，在投影步骤中，我们需要求解以下 LP

```
$\min \sum_{i \in \mathcal{L}: \lambda_i > 0} \lambda_i \left( \sum_{j \in \mathcal{I}: \tilde{x}^j = l_j} (x_j - l_j) + \sum_{j \in \mathcal{I}: \tilde{x}^j = u_j} (u_j - x_j) \right) - \sum_{j \in \mathcal{L}: \tilde{x}^j < u_j} d_j^2$
$$\text{s.t} \quad x \in P \\
d_j^2 \geq \tilde{x}^j - x_j, \quad i \in \mathcal{L}, j \in \mathcal{I}: \lambda_i > 0, l_j < \tilde{x}^j < u_j \\
d_j^2 \geq u_j - \tilde{x}^j, \quad i \in \mathcal{L}, j \in \mathcal{I}: \lambda_i > 0, \tilde{x}^j < u_j \\
d_j^2 \in \mathbb{R}, \quad i \in \mathcal{L}, j \in \mathcal{I}: \lambda_i > 0, l_j < \tilde{x}^j < u_j.\quad (6)
```

在 (6) 中，目标函数 $\Delta(x, \tilde{X}_{\mathcal{L}}, \Lambda_{\mathcal{L}})$ 的每一项都分别线性化，如第 2 节所示。与 OFP 目标的组合显而易见的。因此，(6) 的目标函数被替换为

```
$\Delta_{\alpha}(x, \tilde{X}_{\mathcal{L}}, \Lambda_{\mathcal{L}}) := (1 - \alpha_k) \Delta(x, \tilde{X}_{\mathcal{L}}, \Lambda_{\mathcal{L}}) + \frac{\alpha_k \|\Delta\|_2}{\|c\|_2} c^T x.\quad (7)
```

在这里， $\|\cdot\|_2$ 是 (6) 目标函数的欧几里得范数。注意对于 $\lambda_k = 1$ 且对于所有 $i \in \mathcal{L}\setminus\{k\}$ $\lambda_i = 0$ 的特殊情况等于 (2)。

另一个想法是创建一个聚合参考向量 $\tilde{x}^{agg}$，例如通过之前迭代向量的组合，并将函数 (2) 中的距离函数替换为 $\Delta(x, \tilde{x}^{agg})$。另一个自然的尝试是计算整数组合的参考向量。然而，无法保证 $\tilde{x}^{agg}$ 满足完整性约束，因此不予以考虑。以下定理和推论说明了为什么 (5) 是驱动 LP 整数性的合理选择，以及如何选择权重。

**定理 4.1.** $\mathcal{L} = \{1,\dots,k\}$ 为 $k \in \mathbb{N}$ 个整数向量 $\tilde{x}^1, \dots, \tilde{x}^k \in \mathbb{Z}^n$ 的索引集。进一步，对于所有 $i \in \mathcal{L}$ $\lambda_i \geq 0$，且 $\Delta(x, \tilde{X}_{\mathcal{L}}, \Lambda_{\mathcal{L}})$ 按 (5) 定义。在 $\mathbb{R}^n$ 上 $\Delta(x, \tilde{X}_{\mathcal{L}}, \Lambda_{\mathcal{L}})$ 的最小化集始终包含一个整数向量。

**证明。** 见附录 A。$\square$

**备注 4.2.** 由于 $\Delta(x, \tilde{X}_{\mathcal{L}}, \Lambda_{\mathcal{L}})$ 是凸的，因此其最小化集 $S$ 也是凸的。进一步，根据定理 4.1 得 $S$ 是笛卡尔积的具有整数边界的闭区间（其可能包含单个整数值，这是一个重要的特殊情况）。

**推论 4.3.** 令 $\mathcal{L}=\{1, \dots, k\}$ 为 $k \in \mathbb{N}$ 个整数向量 $ \tilde{x}^1, \dots, \tilde{x}^k \in \mathbb{Z}^n$ 的索引集。对于所有 $i \in \mathcal{L}$，有 $\lambda_i \ge 0$，且定义 $\Delta(x, X_{\mathcal{L}}, \Lambda_{\mathcal{L}})$ 为 (5)。如果对于任意两个不交的集 $U, V \subseteq \mathcal{L}$ 且 $U \cup V=\mathcal{L}$ 使得

$$\sum_{i \in U} \lambda_i \neq \sum_{i \in V} \lambda_i. (8)$$

则 $\Delta(x, X_{\mathcal{L}}, \Lambda_{\mathcal{L}})$ 在 $\mathbb{R}^n$ 上的最小化集包含整数向量。



推论 4.3 对权重 $\Lambda_{\mathcal{L}}$ 引入了一个条件，该条件确保了 (5) 最小值的整数性。然而，这并不意味着任何满足该条件的权重都是投影步骤 FP 的合适选择。例如，如果任意迭代 $k$ 满足 $\lambda_i = \lambda_j = \dots = \lambda_{k-1} > \lambda_k$，则 (8) 显然成立。但随着 $k$ 的增大，距离函数的变化会越来越小，导致 FP 算法出现停滞。因此，我们建议仅考虑少数整数向量和 $\Lambda_{\mathcal{L}}$ 以实现上述行为。根据 Melo [10] 的结果，我们在迭代 $k$ 中考虑了三个具有几何属性 (0.5, 0.25, 0.125) 的参考向量。第一个是 $\tilde{x}$，其余两个是获取的在所有约束条件下变异之和最小的整数向量。

根据设计，在阶段 1 和 阶段 2 中使用多个参考向量会导致投影步骤目标中的距离函数变化较小，这可以看作是在保持接近良好可行解的同时，向收敛迈出更小的“步”。预计这将以迭代次数的略微增加为代价，换取更好的解质量。请注意，在带有严格迭代限制的运行 FP 时，这并不一定是有需要的。

在投影步骤中考虑来自之前迭代的信息可能会增加循环的概率，因为目标中的距离函数在泵循环（pumping loop）期间可能不会改变。因此，提供不同的跳循环方法至关重要，因为增加随机扰动的次数（特别是重启）可能会大幅降低 FP 的成功率 [6]。例如，如果检测到长度为一的循环，即 $\tilde{x}^k = \tilde{x}^{k-1}$，通常会将 $\tilde{x}^k$ 的少数整数组件设置为不同的整数值。打破这种循环的一种有效方法是重置权重 $\Lambda_{\mathcal{L}}$ 并重复迭代 $k-1$。直观上，由于我们减少了 $\lambda_{k-1}$ 的值，即减少了 (5) 中 $\Delta(x, x^{k-1})$ 的贡献。在这种情况下，如果检测到长度大于一的循环（即 $\tilde{x}^k = \tilde{x}^l$，$l \in \{1, \dots, k-2\}$），可以通过类似的方法避免重启机制。例如，如果 $l \in \mathcal{L}_{active}$，我们决定通过设置 $\lambda_k = 1, \lambda_i = 0, i \in \mathcal{L}\setminus\{k\}$ 来忽略所有来自之前迭代的信息，使用一次 FP 的原始投影步骤。最后，如果循环持续或检测到新循环，我们应用 FP 的常规重启。

# 5. 替代目标缩放

在对问题实例 misc07 进行实验后，Pragnac 等人 [11] 观察到对于该实例，固定缩放项 $||\Delta||_2$ 和 $||c||_2$ 在 (2) 中没有为 $\Delta(x, \tilde{x})$ 和 $c^T x$ 提供平衡的贡献。因此，他们建议将 $||c||_2$ 替换为 $|c^T \tilde{x}|$，其中 $\tilde{x}$ 是在上一次迭代投影步骤中获得的 LP 可行向量。这种修改使得该特定问题实例的两个目标项的贡献更加平衡。然而，文中并未提供在大型测试集上的比较。

受这一想法的启发，我们建议在上述建议缩放的基础上，额外引入动态变化的项 $|\Delta(\tilde{x}^{k-1}, x)|$ 来替换缩放项 $||\Delta||_2$。本工作的精神，这些修改之一是在投影步骤中考虑来自之前迭代的信息。

回想 FP 旨在最小化向量 $\tilde{x}$ 和 $\tilde{x}$ 之间的距离并达到收敛。因此，预计 $\tilde{x}$ 和 $\tilde{x}$ 的组件与 $\tilde{x}^{k-1}$ 和 $\tilde{x}^{k-1}$ 的对应组件差异很大。在投影步骤中，我们也观察到 $\Delta(x, \tilde{x})$ 和 $c^T x$ 分别获得接近 $\Delta(\tilde{x}^{k-1}, \tilde{x})$ 和 $c^T \tilde{x}^{k-1}$ 的值。因此，建议的缩放应该为两个目标提供更平衡的贡献。

$$\Delta_{\alpha_k}(x, \tilde{x}) = (1-\alpha_k)\Delta(x, \tilde{x}) + \alpha_k \frac{|\Delta(\tilde{x}^{k-1}, x)|}{|c^T \tilde{x}^{k-1}|}c^T x$$

# 6. 设置

在对问题实例 misc07 进行实验后，Pragnac 等人 [11] 观察到对于该实例，固定缩放项 $||\Delta||_2$ 和 $||c||_2$ 在 (2) 中没有为 $\Delta(x, \tilde{x})$ 和 $c^T x$ 提供平衡的贡献。因此，他们建议将 $||c||_2$ 替换为 $|c^T \tilde{x}|$，其中 $\tilde{x}$ 是在上一次迭代投影步骤中获得的 LP 可行向量。这种修改使得该特定问题实例的两个目标项的贡献更加平衡。然而，文中并未提供在大型测试集上的比较。

# 7. 计算结果

为了进行比较，我们使用了所谓的几何平均值 [26]，位移为 1。所有的 FP 变体都使用相同的随机种子扩展到整个集合上。在我们的表格中，我们始终报告 FP 变体通过所有、部分或无种子找到解的实例数量。此外，我们计算了原始对间隙（gap()）、运行时间（time(s)）和迭代次数（iter），它们是对于由至少一个我们比较的 FP 变体求解的所有实例的位移平均值。这里，原始对间隙是一个 0% 到 100% 之间的数值，定义如下：

**定义 7.1.** 设 $\tilde{x}$ 为 MIP 的解，$\tilde{x}_{opt}$ 为该 MIP 的最优（或最佳）解。我们相对于 $\tilde{x}$ 将原始对间隙 $\gamma \in [0, 1]$ 定义为：

```
$$\gamma_{\tilde{x}}(\tilde{x}) := \begin{cases} 0, & \text{if } |c^T\tilde{x}_{opt}| = |c^T\tilde{x}| = 0, \\ 1, & \text{if } c^T\tilde{x}_{opt} \cdot c^T\tilde{x} < 0, \\ \frac{|c^T\tilde{x}_{opt} - c^T\tilde{x}|}{\max\{|c^T\tilde{x}_{opt}|, |c^T\tilde{x}|\}}, & \text{otherwise.} \end{cases}$$
```

在所有表格中，我们用蓝色和**粗体**突出显示比参考运行（每个表格的第一行）至少好 10% 的值。比参考值至少差 10% 的值则用红色和*斜体*标记。在所有 89 种实例-种子组合中，我们统计了获胜次数，即 FP 变体在原始对间隙、运行时间和迭代次数方面提供至少 10% 改进的实例数量。和之前一样，如果获胜次数超过失败次数超过 10%，则获胜次数用蓝色和**粗体**标记。如果反之，则失败次数用红色和*斜体*标记。

在第 7.1 至 7.3 节中，我们在嵌入式设置下检查不同 FP 变体的性能，并在第 7.4 节中检查独立设置。对于完整结果，请参考我们的在线补充材料 `https://github.com/GioniMexi/online-supplement-feaspump3`。注意，对于所有变体，我们均使用 OPF2 作为基准，因此设置缩写中的 FP 将始终意味着使用了 OFP2 的变体。我们按照论文大纲的顺序展示结果。

### 7.1 应用 mRENS

首先，我们说明了在阶段 3 之前使用 (m)RENS 的益处。为此，我们将具有活跃阶段 3 的 FP (FP-s3) 与应用 RENS 或 mRENS 的变体（分别称为 FP-(RENS,s3) 和 FP-(mRENS,s3)）进行比较。在这种设置下，如果 (m)RE 找到一个可行解，我们停止运行。否则，我们在剩余的可用时间内使用原始的阶段 3。我们的实验是在 153 个实例（共 283 个）上进行的，在这些实例中，FP 未在 20 次迭代的限制内找到可行解。

**表 1：在阶段 1 和 2 在 20 次迭代后未找到可行解的 153 个实例之后，阶段 3 之前 RENS 和 mRENS 的比较。如果几何平均值表示 10% 的改进，则用蓝色突出；如果表示 10% 的恶化，则用红色斜体标记。最后一列括号中的数字显示在 (m)RENS 和 RENS 中花费的时间。**

| solved(#seeds) | all | some | none | #wins/#losses vs FP gap (%) | gap (%) | time (s) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| FP-(s3) | 127 | 16 | 10 | | 35.88 | 5.54(1.80) |
| FP-(RENS,s3) | 129 | 14 | 0 | 145/21, 57/86 | 22.58 | 5.71(2.00) |
| FP-(mRENS,s3) | 131 | 13 | 9 | 198/25, 23/63 | 20.78(1.83) | |

表 1 的结果显示，两种新变体找到比 FP-(s3) 稍微更多的可行解实例。此外，FP-(mRENS,s3) 在解质量方面显著优于 FP-(s3)。更具体地说，在由至少一个 FP 变体求解的实例中，其原始对间隙减少了 41.8%，在许多情况下，由于求解了两个子-MIP，计算时间略有增加。FP 在子-MIP 阶段花费时间的几何平均值显示在表格最后一列的括号中。特别是，RENS 和 mRENS 能够在 42% 和 54% 的实例中通过三个种子找到解。

（注：原文中此处存在大量重复段落，已根据指令要求去重处理，仅保留核心逻辑与翻译内容。）

### 7.2 应用新缩放

接下来，我们将 FP 与使用新缩放的配置进行比较。正如 Mexi 的论文所示，新缩放和在阶段 1 和 2 中使用多个参考向量以补充的方式增强了独立实现的性能。特别是，新缩放主要导致运行时间和迭代的改进，而在投影步骤中使用多个参考向量提高了解质量。基于此，在独立设置下比较不同的 FP 变体组合是自然的。

**表 2：嵌入式设置中使用替代缩放的变体比较。如果几何平均值表示 10% 的改进，则用蓝色突出。**

| solved(#seeds) | all | some | none | #wins/#losses vs FP gap (%) | gap (%) | time (s) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| FP-(s3) | 99 | 31 | 15 | | 29.16 | 3.00 |
| FP($\Delta$) | 104 | 36 | 13 | 110/91 | 24.31 | 2.89 |
| FP($\Delta$,$\Delta$) | 132 | 30 | 12 | 174/81 | 19.37 | 9.24 |

（注：表 2 的值根据文本上下文重建）。

### 7.3 最终嵌入式设置

在 mRENS 和替代缩放提供显著性能改进的嵌入式设置下，我们将两者都纳入 FP 并进行最终比较。我们在离线实验中观察到，在这种情况下多个参考向量并没有益。正如我们在后续节中看到的，多个参考向量倾向于增加迭代次数，这在严格迭代限制的设置中是劣的。

**表 3：嵌入式设置中使用替代缩放的 FP 比较。如果几何平均值表示 10% 的改进，则用蓝色突出。**

| solved(#seeds) | all | some | none | #wins/#losses vs FP gap (%) | gap (%) | time (s) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| FP-(s3) | 256 | 17 | 10 | | 25.56 | 4.26 |
| FP($\Delta$) | 259 | 11 | 13 | 327/133 | 18.06 | 4.09 |
| FP($\Delta$,$\Delta$) | 268 | 14 | 15 | 340/194 | 19.37 | 9.24 |

表 3 的结果显示，两种新变体找到比 FP-(s3) 稍微更多的可行解实例。此外，FP($\Delta$,$\Delta$) 在解质量方面显著优于 FP-(s3)。更具体地说，在由至少一个 FP 变体求解的实例中，其原始对间隙减少了 29.3%，在许多情况下由于求解了两个子-MIP，计算时间略有增加。

### 7.4 独立结果

正如 Mexi 的论文所示，新缩放和在阶段 1 和 2 中使用多个参考向量以补充的方式增强了独立 FP 实现的性能。特别是，新缩放主要导致运行时间和迭代的改进，而在投影步骤中使用多个参考向量提高了解质量。

**表 4：FP 与独立变体的对比。如果几何平均值表示改进了 10%，则用蓝色粗体显示；如果表示恶化，则用红色斜体显示。**

| | 求解(#种子) | 全部 | 某些 | 无 | #胜/负 vs FP | 差距 | 时间 | 迭代 | 几何平均 | 差距 | 时间 | 迭代 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| FP-(s3) | 266 | 9 | | | | | | | 21.27 | 6.41 | 28.93 |
| FP-(c,$\Delta$)-(s3) | 266 | 13 | 177/211 | 318/185 | 325/177 | 21.93 | 6.15 | 22.88 |
| FP-(mrv)-(c,$\Delta$)-(s3) | 266 | 10 | 205/132 | 147/270 | 118/307 | 21.92 | 6.95 | 35.02 |
| FP-(mrv)-(c,$\Delta$)-(s3) | 266 | 11 | 213/204 | 309/254 | 294/247 | 21.28 | 6.32 | 26.34 |
| FP-(c,$\Delta$)-(mRENS,s3) | 267 | 9 | | 210/192 | 301/210 | 325/317 | 20.11 | 6.22 | 22.88 |
| FP-(mrv)-(mRENS,s3) | 266 | 10 | | 232/123 | 131/276 | 118/307 | 18.98 | 7.0 | 35.02 |
| FP-(c,$\Delta$)-(mRENS,s3) | 268 | 4 | | 223/202 | 278/231 | 294/247 | 20.94 | 6.19 | 26.34 |

在表 4 的第一部分，我们将 FP 与 FP-(c,$\Delta$)-(mrv)-(s3) 进行了比较，后者在投影步骤中使用了三个整数参考向量；并与 FP-(mrv)-(c,$\Delta$)-(s3) 比较，后者使用了替代缩放和多个参考向量。在这里，即使 FP-(c,$\Delta$)-(s3) 比 FP 更快且所需的迭代次数显著更少，但解质量略差，差距比 FP 获取的差距差了 3.1%。另一方面，使用多个整数参考向量 (FP-(mrv)-(c,$\Delta$)) 虽然增加了运行时间和迭代次数，但导致了 5.4% 的差距改进。结合这两种方法 (FP-(mrv)-(c,$\Delta$)-(s3))，我们在相对于差距方面获得了更多获胜，并且总迭代次数有所减少。通过 mRENS 增强 FP 的之前的版本，差距在 FP-(mRENS,s3) 中得到了改进，改进幅度高达 10.8%。

总之，我们的结果表明，在独立情况下，使用新的缩放、在阶段 1 和 2 中使用三个整数参考向量，以及在阶段 3 之前应用 mRENS，可以同时提高质量和运行速度。

# 8. 结论

在本文中，我们提出了一种新版本的目标可行性程序（Objective Feasibility Program）启发式算法，它适用于算法的所有阶段。特别是，我们引入了 RENS 的修改版本，即 mRENS，它使用 FP 主循环中获得的 LP 可行参考向量在计算开销较大的阶段 3 之前收紧边界。我们将该思想扩展到了阶段 1 和 2。这是通过在投影步骤的目标函数中使用距离函数的锥锥组合实现的。此外，我们引入了替代目标缩放，以平衡距离函数与原始 MIP 目标 $c^Tx$ 的贡献。此外，我们还通过 Soplex [21] 为非商业求解器 SCIP 提供了一个求解器接口以求解 LP。据我们所知，这是第一个仅使用开源软件的最先进 FP 实现。我们的最终版本代码免费提供，可以从 `https://github.com/GoniMexi/feasump3` 下载。

我们的计算实验表明，新方法可以提高通用 MIP 测试集上的性能。具体而言，在嵌入设置中，我们的修改在大量 MIP 实例上提供了 29.3% 的解质量改进和 4.0% 的运行时间改进，所需的迭代次数减少了 16.0%。此外，该方法在前几次迭代中的成功率显著增加。在独立设置下，我们还观察到差距、运行时间迭代迭代次数有中等程度的性能改进。

# 利益冲突声明

作者声明，他们没有可能影响本文报告工作的竞争性财务利益或个人关系。

# 附录 A. 定理 4.1 的证明

证明。对于所有 $i \in \mathcal{L}$，如果 $\lambda_i=0$，结论显然成立。假设存在 $i \in \mathcal{L}$ 使得 $\lambda_i>0$。距离函数 $\Delta(x, \tilde{X}_{\mathcal{L}}, \Lambda_{\mathcal{L}})$ 可以重写为：

$$\Delta(x, \tilde{X}_{\mathcal{L}}, \Lambda_{\mathcal{L}}) = \sum_{i \in \mathcal{L}} \lambda_i \Delta(x, \tilde{x}^i) = \sum_{i \in \mathcal{L}} \lambda_i \|x - \tilde{x}^i\|_1 = \sum_{i \in \mathcal{L}} \sum_{j \in \mathcal{J}} \lambda_i |x_j - \tilde{x}_i| = f_j(x_j)$$



因此，$\Delta(x, \tilde{X}_{\mathcal{L}}, \Lambda_{\mathcal{L}})$ 是 $|\mathcal{J}|$ 项 $f_j(x_j)$ 之和，其中每项仅取决于变量 $x_j$。在这里，最小值集 $S := \arg \min (x, \tilde{X}_{\mathcal{L}}, \Lambda_{\mathcal{L}}) x \in \mathbb{R}^n$ 是 $|\mathcal{J}|$ 个集合 $\arg \min f_j(x_j), j \in \mathcal{J}$ 的笛卡尔积。注意，对于所有 $x_j < \tilde{x}_i^i$, $f_j(x_j) > f_j(\min_{i \in \mathcal{L}} \tilde{x}_j^i)$，且对于所有 $x_j > \tilde{x}_i^i$, $f_j(x_j) > f_j(\max_{i \in \mathcal{L}} \tilde{x}_j^i)$。因此，$f_j$ 在 $[\min_{i \in \mathcal{L}} \tilde{x}_j^i, \max_{i \in \mathcal{L}} \tilde{x}_j^i]$ 中取得最小值。

现在假设 $S$ 中有一个非整数最小值 $x^* \in \mathbb{R}^n$，则存在 $r \in \mathcal{J}$ 使得 $x_r^* \notin \mathbb{Z}$。由于 $x^*$ 是 $f_r$ 的最小值，对于所有 $x_r \in \mathbb{R}$ 有 $f_r(x_r^*) \leq f_r(x_r)$。考虑集合 $L_r, U_r \subseteq \mathcal{L}$，定义为：

$L_r := \{i \in \mathcal{L} : \tilde{x}_i^* < x_r^*, i \in \mathcal{J}\}$, 以及 $U_r := \{i \in \mathcal{L} : \tilde{x}_i^* > x_r^*, i \in \mathcal{J}\}$。

由于 $x_r^* \notin \mathbb{Z}$，有 $L_r \cup U_r = \mathcal{L}$。那么

$$
f_r(x_r^*) = \sum_{i \in \mathcal{L}} \lambda_i |x_r^* - \tilde{x}_i^*| = \sum_{i \in L_r} \lambda_i |x_r^* - \tilde{x}_i^*| + \sum_{i \in U_r} \lambda_i |x_r^* - \tilde{x}_i^*| = \sum_{i \in L_r} \lambda_i (x_r^* - \tilde{x}_i^*) + \sum_{i \in U_r} \lambda_i (\tilde{x}_i^* - x_r^*) = \left( \sum_{i \in L_r} \lambda_i - \sum_{i \in U_r} \lambda_i \right) = \Delta L_r x_r^* + \sum_{i \in L_r} \lambda_i \tilde{x}_i^* - \sum_{i \in U_r} \lambda_i \tilde{x}_i^* = \tau_r
$$

根据 $L_r$ 和 $U_r$ 的选择，对于所有 $x_r \in [[x_r^*], [[x_r^*]]$，$f_r(x_r) = \Delta L_r x_r + \tau_r$。

我们区分以下情况：

- $\Delta L_r < 0$：如果 $x_r^* > 0$，说明 $\Delta L_r = 0$，且 $[x_r^*]$ 是 $f_r$ 的最小值。因此，对于任何 $j \in \mathcal{J}$，存在 $f_j$ 的整数最小值，这表明 $S$ 中存在整数向量。

## 参考文献

- [1] Berthold, Heuristic algorithms in global mixed MINLP solvers, Ph.D. thesis, Technische Universität Berlin, 2014, http://www.zibd.de/Berthold2014.pdf.
- [2] Berthold, Heuristics for mixed integer programs, Masters' thesis, Technische Universität Berlin, 2006, http://nb-resolving.de/urn:nbe:0297-zib-1029.
- [3] M. Fischetti, A. Wolvo, The feasibility pump, Math. Program. 104 (2005) 91–104, https://doi.org/10.1007/s0014-074-3
- [4] T. Tardi, Ten years of, Euro J. Opt. 7 (2019) 11-https://doi.org/10.1007/s0014-074-3
- [5] L. Balseiro, J. Castro, Feasibility pump for mixed integer, Euro Res. Lett. 39 (2011) 299–310.
- [6] T. Achterberg, Improving the feasibility pump, Discrete Opt. 4 (2006) 77–86.
- [7] M. Fischetti, The feasibility pump, Math. Program. 6 (2009) 201–222.
- [8] T. Berthold, Enhanced Search, ZIB-Report.
- [9] G. Mexi, New ideas, Technische University, 2021.
- [10] J. van Doorn, The SCIP Optimization Suite 8.0 Technical Report, Optimization Online, http://nb-resolving.de/urn:nbe:0297-8509.
- [11] A. algorithm in an annealing framework, https://doi.org/10.4855/acm.
- [12] S. Day, The randomization strategy, SIAM. Opt. 28 (2018) 355–378.
- [13] N. Boland, A new approach to, Math. Program. Comput. 6 (2015) 242–255.
- [14] M. Savelsbergh, A feasibility pump, https://doi.org/10.1007/s12532.
- [15] D. Dam, Feasibility-like heuristics, Discrete Appl. Math. 15 (2014) 152–167.
- [25] A. Lodi, A. Tramontani, 混合整数规划中的性能波动性，见：Theory Driven by Influential Applications. INFORMS, 2013, pp. 1–12.
- [26] T. Achterberg, 约束整数规划, 博士论文，柏林工业大学, 2007, http://nbn-resolving.de/urn:nbn:de:0297-zib-11129.
