
## Step 3:

计算 $Fit(S_i)$ 对于 $q_t$ 中的每个字符串 $S_i$ $(0 \leq i \leq M - 1)$。找出最佳字符串 $S_{best1}$（即适应度值最小的字符串）和最差字符串 $S_{worst1}$（即适应度值最大的字符串）。如果 $S_{best1}$ 或 $S_{worst1}$ 不唯一，则任意选择一个。

# Step 4: *(Selection or Reproduction)*

在 $q_t$ 的字符串上执行下面描述的选择操作，生成大小为 M 的交配池 $q_{mat}$。

# *Selection operation*

+   计算 $S_i$ 的选择概率 $p_i$ $(i = 0, 1, \ldots, M - 1)$

$$p_i = \frac{\frac{1}{Fit(S_i)}}{\sum_{i=0}^{M-1}\frac{1}{Fit(S_i)}}$$

> *Note:* 由于我们处理的是最小化问题，因此 $Fit(S_i)$ 越小，$p_i$ 的概率越高。

[PAGE 133]

+   计算 $S_i$ 的累积概率 $q_i$ $(i = 0, 1, \cdots, M - 1)$

\[q_i = \sum_{j=0}^{i} p_j.\]

+   对于 $j = 0, 1, \cdots, M - 1$，生成一个在 $[0, 1]$ 范围内的随机数 $r_j$。如果 $r_j \leq q_0$，选择 $S_0$；否则，如果 $q_{i-1} < r_j \leq q_i$，选择 $S_i$ $(1 \leq i \leq M - 1)$。

> *Note:* $p_0 = q_0$ 且 $p_i = q_i - q_{i-1}$ 对于 $1 \leq i \leq M - 1$。

> **Remark 2.** 由于 $p_i$ 越大，即 $(q_{i-1}, q_i]$ 的区间长度越大，随机数落在该区间的概率越高。换句话说，若 $Fit(S_i)$ 较小，则 $S_i$ 的选择概率更高。因此，从当前大小为 $M$ 的种群中，构建同样大小的交配池 $q_{mat}$，其中包含潜在的字符串。随后这些交配池中的字符串进行交叉和变异。该交配池构建策略与文献[49]中使用的策略相似。

# Step 5: *(Crossover)*

在 $q_{mat}$ 的字符串上执行下面描述的交叉操作，得到大小为 M 的种群 $q_{temp1}$。

# *Crossover operation*

形成 $M/2$ 对，每对由 $q_{mat}$ 中的第 $i$ 条和第 $(M/2 + i)$ 条字符串组成 ($i = 0, 1, \cdots, (M/2 - 1)$)。

```
for each pair of strings do
begin
    generate a random number R from [0, 1].
```

[PAGE 134]

```
if (R ≤ cp) do
//to produce two offsprings for the next generation.//
begin
    generate two random numbers from [0, n − 1] to
    define a matching section. Use this matching
    section to effect a cross through position-by-
    position exchange operation.
end.
end.
```

> *Note:* 部分匹配交叉（PMX）[47]是一种既实现反转又实现交叉的重新排序操作。

**Example 3.** 假设生成的两个随机数分别为 2 和 3。则对 $S_1 = ((00), (10), (11), (20), (21))$ 和 $S_2 = ((20), (00), (21), (10), (11))$ 进行 PMX 会得到两个子代 $S'_1 = ((00), (20), (21), (10), (11))$ 和 $S'_2 = ((10), (00), (11), (20), (21))$。

**Remark 3.** 我们使用了两点交叉操作和 PMX 操作。多点交叉以及其他重新排序操作，如顺序交叉（OX）和循环交叉（CX）[47]，也可以使用。

# Step 6: *(Mutation)*

在 $q_{temp1}$ 的字符串上执行下面描述的变异操作，得到大小为 M 的种群 $q_{temp2}$。

# *Mutation operation*

```
Set q ← m_probability(t)
for each string Sᵢ of qₜₑₘₚ₁ (0 ≤ i ≤ M − 1) do
```

[PAGE 135]

```
begin
    for each node node_j (0 ≤ j ≤ n − 1) of string S_i do
    begin
        generate a random number from [0, 1], say m.
        if (m ≤ q) do
        begin
            exchange node_j of S_i with any other
            randomly selected node node_k of S_i
            (0 ≤ k ≤ n − 1, k ≠ j)
        end
    end
end.
```

**Example 4.** 如果节点 (00) 被节点 (21) 替换，则变异后的字符串 $S_1 = ((00), (10), (11), (20), (21))$ 变为 $S'_1 = ((21), (10), (11), (20), (00))$。

# Step 7:

计算 $Fit(S_i)$ 对于 $q_{temp2}$ 中的每个字符串 $S_i$ $(0 \leq i \leq M − 1)$。找出最佳字符串 $S_{best2}$ 和最差字符串 $S_{worst2}$。如果 $S_{best2}$ 或 $S_{worst2}$ 不唯一，则任意选择一个。

# Step 8: (Elitism)

比较 $q_t$ 中的最佳字符串 $S_{best1}$ 与 $q_{temp2}$ 中的最佳字符串 $S_{best2}$。如果 $Fit(S_{best2}) > Fit(S_{best1})$，则用 $S_{best1}$ 替换 $S_{worst2}$。将 $q_{temp2}$ 重命名为 $q_t$。

# Step 9:

$t \leftarrow t + 1$；如果 $t < T$，则回到步骤 3。

Bhandari et al. [49] 提供了证明，表明在迭代次数趋于无穷时，任何初始种群的 EGA 都会收敛到全局最优解。

[PAGE 136]

<!-- no content -->

[PAGE 137]

![](img/6578f6fc95ac71d2c7109e594d9df12f_137_0.png)

# **FIGURE 3.10:** (a) Subgraph of cellular graph and (b) frequency assignment when $s_1=s_2$

and $j$ are within Distance 2 and 0 otherwise. With this frequency separation matrix, we apply the *Algorithm GA* over the subgraph shown in the figure. The resulting assignment is shown in Figure 3.10(b). Observe that the frequency channels $(0, 0)$, $(0, 1)$, $(0, 2)$, $(0, 3)$, $(0, 4)$, $(0, 5)$ and $(0, 6)$ are assigned repeatedly to the nodes over the subgraph in a regular and symmetrical way. The symmetry is clear from Figure 3.10(b). Using this symmetry, frequencies can be assigned to the nodes over the entire network. This assignment is shown in Figure 3.11 and is characterized as follows.

We first consider three directions $x$, $y$ and $z$ in the cellular graph in Figure 3.12. In each direction, we have definite types of lines and each type of line is identified by the sequence of frequencies assigned to the nodes lying on that line. A sequence is of Period $b$ if each frequency is periodically repeated at Distance $b$ on that line.

In $x$ direction, there is only one type of line (*type x*) identified by the repetitive sequence of Period 7 as $(0, 0)$ $(0, 1)$ $(0, 2)$ $(0, 3)$ $(0, 4)$ $(0, 5)$ $(0, 6)$ $\cdots$.

In $y$ direction, there is only one type of line (*type y*) identified by the repetitive sequence of Period 7 as $(0, 0)$ $(0, 5)$ $(0, 3)$ $(0, 1)$ $(0, 6)$ $(0, 4)$ $(0, 2)$ $\cdots$.

[PAGE 138]

![](img/6578f6fc95ac71d2c7109e594d9df12f_138_0.png)

**FIGURE 3.11:** Frequency assignment of two-band buffering system for $s_1 = s_2$

In $z$ direction, there is only one type of line (type $z$) identified by the repetitive sequence of Period 7 as (0, 0) (0, 4) (0, 1) (0, 5) (0, 2) (0, 6) (0, 3) · · ·.

It follows from Figure 3.11 that along any of the lines of type $x$, type $y$ and type $z$, there is no conflict. Therefore, this assignment is conflict-free over the entire network.

Hence, by using the scheme described above, the frequencies can be assigned to the nodes of the entire network using a bandwidth of $6s_2$, when $s_1 = s_2$.

We now generalize Lemma 3 and state the following theorem for the assignment of $w$ channels to every node of the entire cellular network.

[PAGE 139]

# Theorem 3.

In a hexagonal cellular network with homogeneous demand $w$ and two-band buffering, there exists a frequency assignment scheme for $s_1=s_2$, which requires a bandwidth of:

+   1. **Case 1.** $(w-1)7s_2+6s_2$ when $s_0\leq 7s_2$, and
+   2. **Case 2.** $(w-1)s_0+6s_2$ when $s_0\geq 7s_2$.

**Proof:** Follows from Lemma 3.

**Remark 4.** For the second case of Theorem 3, i.e., when $s_1=s_2$ and $s_0\geq 7s_2$, the required bandwidth is close to $ws_0$.

**Remark 5.** For $s_1=s_2$, the above assignment requires a bandwidth equal to the corresponding lower bound presented in Theorem 1 for different relative values of $s_0$, $s_1$, and $s_2$. Hence this assignment is optimal.

![](img/6578f6fc95ac71d2c7109e594d9df12f_139_0.png)

**FIGURE 3.12:** Three directions in hexagonal cellular graph

# 3.4.3.2　Scheme 2: for i) $s_2<s_1\leq 2s_2$ and ii) $s_1\geq 2s_2$

Consider the nine-node subgraph with nodes $a$, $b$, $c$, $d$, $e$, $f$, $g$, $h$ and $i$ of the cellular graph as shown in Figure 3.13.

Each node of this subgraph represents a cell of the cellular network. Suppose

