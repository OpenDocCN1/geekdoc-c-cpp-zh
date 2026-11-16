

### 定理 11.6.5 (Calderbank Bound)
设 $C_0$ 是长度为 $n$ 的二元线性码 $C$ 中的一个子码，其余维数为 $i \ge 1$。则

\(\rho(C_0) \le 2\rho(C) + 2^i - 1\)。

**Proof:** 设 $H$ 为 $C$ 的一份校验矩阵。我们可以向 $H$ 添加 $i$ 行，构成一份校验矩阵

\(H_0 = \begin{bmatrix} H \ H_1 \end{bmatrix}\)

用于 $C_0$。设 $H_0$ 的第 $j$ 列为 $h_0^j$，其中 $1 \le j \le n$。

设 \(\rho = \rho(C)\) 且 \(\rho_0 = \rho(C_0)\)。若 \(\rho_0 \le 2\rho + 1$，则 (11.20) 显然成立。因此假设 \(\rho_0 \ge 2\rho + 2$。必存在 $C_0$ 的某个综合症 $s_0^T$，它是 $H_0$ 的 $\rho_0$ 列之和，但不能更少。通过重排 $H_0$ 的列，我们可以假设

\(s_0^T = \sum_{j=1}^{\rho_0} h_0^j\)。

构建 Kneser 图 $K(\rho_0, \rho+1)$。该图的顶点集 $V$ 为 $\mathbb{F}_2^n$ 中权重为 $\rho+1$ 的向量集合。我们将每个向量 $\mathbf{v} \in \mathbb{F}_2^n$ 写作 $(\mathbf{v}', \mathbf{v}'')$，其中 $\mathbf{v}' \in \mathbb{F}_2^{\rho_0}$。我们希望建立 $K(\rho_0, \rho+1)$ 顶点的一个着色 $f$。对于每个 $\mathbf{v}' \in V$，存在一个 $\mathbf{x}_v \in C$，其与 $(\mathbf{v}', \mathbf{0})$ 的距离至多为 $\rho$，因为 $\rho(C) = \rho$。对于每个 $\mathbf{v}' \in V$，选取这样一个 $\mathbf{x}_v \in C$ 并定义

\(f(\mathbf{v}') = H_1 \mathbf{x}_{\mathbf{v}'}^T\)。

注意 $f(\mathbf{v}') \in \mathbb{F}_2^i$。我们首先证明 $H_1 \mathbf{x}_{\mathbf{v}'}^T \neq 0$。假设 $H_1 \mathbf{x}_{\mathbf{v}}^T = 0$。由于 $\mathbf{x}_v \in C$，故 $H \mathbf{x}_{\mathbf{v}}^T = \mathbf{0}$，因此 $H_0 \mathbf{x}_{\mathbf{v}}^T = \mathbf{0}$。于是，

\(H_0(\mathbf{v}', \mathbf{0})^T = H_0((\mathbf{v}', \mathbf{0}) - \mathbf{x}_v)^T\)。

因为 $wt(\mathbf{v}) = \rho+1$，(11.22) 的左边是 $H_0$ 中前 $\rho_0$ 列中的 $\rho+1$ 列的组合，而 (11.22) 的右边至多是 $H_0$ 的 $\rho$ 列的组合（因为 $wt((\mathbf{v}', \mathbf{0}) - \mathbf{x}_v) \le \rho$）。因此，在 (11.21) 的右边，我们可以用至多 $\rho$ 列的 $H_0$ 替换 $\rho+1$ 列的 $H_0$，这表明 $\mathbf{s}_0^T$ 是 $H_0$ 中至多 $\rho_0 - 1$ 列的线性组合，这产生了矛盾。这表明 $f(\mathbf{v}')$ 是 $\mathbb{F}_2^i$ 中 $2^i - 1$ 个非零元素之一。

我们现在证明 $f$ 确实是 $K(\rho_0, \rho+1)$ 的一个着色。设 $\{\mathbf{v}', \mathbf{w}'\}$ 为 $K(\rho_0, \rho+1)$ 的一条边。我们必须证明 $H_1 \mathbf{x}_{\mathbf{v}'}^T \neq H_1 \mathbf{x}_{\mathbf{w}'}^T$。假设 $H_1 \mathbf{x}_{\mathbf{v}'}^T = H_1 \mathbf{x}_{\mathbf{w}'}^T$。由于 $\mathbf{v}'$ 和 $\mathbf{w}'$ 属于 $V$，且 $\text{supp}(\mathbf{v}')$ 与 $\text{supp}(\mathbf{w}')$ 不相交，故 $wt(\mathbf{v}' + \mathbf{w}') = 2\rho + 2$。此外，$(\mathbf{v}' + \mathbf{w}', \mathbf{0})$ 与 $\mathbf{x}_v + \mathbf{x}_w$ 之间的距离至多为 $2\rho$。由于 $\mathbf{x}_v + \mathbf{x}_w \in C$，故 $H_1(\mathbf{x}_v + \mathbf{x}_w)^T = \mathbf{0}$ 且 $H(\mathbf{x}_v + \mathbf{x}_w)^T = \mathbf{0}$，因此 $H_0(\mathbf{x}_v + \mathbf{x}_w)^T = \mathbf{0}$。如同 (11.22) 中，

\(H_0(\mathbf{v}' + \mathbf{w}', \mathbf{0})^T = H_0((\mathbf{v}' + \mathbf{w}', \mathbf{0}) - (\mathbf{x}_v + \mathbf{x}_w))^T\)。

因为 \(wt(\mathbf{v}' + \mathbf{w}') = 2\rho + 2$，(11.23) 的左边是 $H_0$ 中前 $\rho_0$ 列中的 \(2\rho + 2$ 列的组合，而 (11.23) 的右边至多是 $H_0$ 的 \(2\rho$ 列的组合（因为 \(wt((\mathbf{v}' + \mathbf{w}', \mathbf{0}) - (\mathbf{x}_v + \mathbf{x}_w)) \le 2\rho$）。如同之前，在 (11.21) 的右边，我们可以用至多 \(2\rho$ 列的 $H_0$ 替换 \(2\rho + 2$ 列的 $H_0$，这表明 \(\mathbf{s}_0^T$ 是 $H_0$ 中至多 \(\rho_0 - 2$ 列的线性组合，这产生了矛盾。

因此，$f$ 是 $K(\rho_0, \rho + 1)$ 的一个至多有 \(2^i - 1$ 种颜色的着色。由于 \(\rho_0 \ge 2\rho + 2$，(11.19) 蕴含
\(\rho_0 - 2\rho = \chi(K(\rho_0, \rho + 1)) \le 2^i - 1\)。

注意，当 \(i = 1$ 时，Calderbank Bound 即为定理 11.6.3 的界。

**Exercise 659** 设 \(C\) 为一个满足 \(\rho(C) = 2$ 的二元码，且 \(C_i$ 为余维数为 \(i$ 的子码。对于哪些 \(i$ 的值，定理 11.6.4 中对 \(\rho(C_i)$ 的上界优于 Calderbank Bound？

**Exercise 660** 设 \(C\) 为一个满足 \(\rho(C) = 10$ 的二元码，且 \(C_i$ 为余维数为 \(i$ 的子码。对于哪些 \(i$ 的值，定理 11.6.4 中对 \(\rho(C_i)$ 的上界优于 Calderbank Bound？

There is another upper bound on \(\rho(C)\) due to Hou [139] that in some cases improves the bound of Theorem 11.6.4 and the Calderbank Bound. Its proof relies on knowledge of the graph \(G(n, s)\). The graph \(G(n, s)\) has vertex set \(\mathbb{F}_2^n\); two vertices \(v\) and \(w\) form an edge whenever \(d(v, w) > s\).

The following theorem of Kleitman [172] gives a lower bound on the chromatic number of \(G(n, 2r)\).

### 定理 11.6.6
设 \(n$ 和 \(r$ 为正整数，且 \(n \ge 2r + 1$。则

\(\chi(G(n, 2r)) \ge \frac{2^n}{\binom{n}{0} + \binom{n}{1} + \cdots + \binom{n}{r}}\)。

We now state the bound on \(\rho(C)\) due to Hou; we leave the details of the proof as an exercise.

### 定理 11.6.7 (Hou Bound)
设 \(C_0$ 为二元线性码 \(C$ 的一个余维数为 \(i \ge 1$ 的子码。设 \(\rho = \rho(C)$ 且 \(\rho_0 = \rho(C_0)$。则

\(\frac{2\rho}{\binom{\rho_0}{0} + \binom{\rho_0}{1} + \cdots + \binom{\rho_0}{\rho}} \le 2^i.\) (11.24)

**Proof:** 若 \(\rho_0 \le 2\rho$，则由练习 661 可知 (11.24) 成立。假设 \(\rho_0 \ge 2\rho + 1$。设 \(H_0$ 为 \(C_0$ 的校验矩阵，如同定理 11.6.5 证明中所述。类似地，定义从 \(G(\rho_0, 2\rho)$（而非 \(K(\rho_0, \rho + 1)$）的顶点到 \(\mathbb{F}_2^i$ 的同一映射 \(f$。如前所述，可知 \(f$ 是 \(G(\rho_0, 2\rho)$ 的一个 \(2^i$ 色着色，结果由定理 11.6.6 得出。

Exercise 661 Show that if \(\rho_0 \le 2\rho\), then (11.24) is true. \(\diamond\)

Exercise 662 Fill in the details of the proof of Theorem 11.6.7. \(\diamond\)

Exercise 663 Let \(\mathcal{C}\) be a binary code with \(\rho(\mathcal{C})=1\) and \(\mathcal{C}_i\) a subcode of codimension \(i\). For each \(i \ge 1\), which upper bound on \(\rho(\mathcal{C}_i)\) is better: the bound in Theorem 11.6.4, the Calderbank Bound, or the Hou Bound? \(\diamond\)

## 11.7 Ancestors, descendants, and orphans

In this concluding section of the chapter we examine relationships among coset leaders of a code \(\mathcal{C}\). There is a natural relationship among cosets, and we will discover that all cosets of \(\mathcal{C}\) of maximum weight (that is, those of weight \(\rho(\mathcal{C})\)) have a special place in this relationship. We will also introduce the concept of the Newton radius of a code and investigate it in light of this relationship among cosets.

There is a natural partial ordering \(\le\) on the vectors in \(\mathbb{F}_2^n\) as follows. For \(\mathbf{x}\) and \(\mathbf{y}\) in \(\mathbb{F}_2^n\), define \(\mathbf{x} \le \mathbf{y}\) provided that \(\text{supp}(\mathbf{x}) \subseteq \text{supp}(\mathbf{y})\). If \(\mathbf{x} \le \mathbf{y}\), we will also say that \(\mathbf{y}\) *covers* \(\mathbf{x}\). We now use this partial order on \(\mathbb{F}_2^n\) to define a partial order, also denoted \(\le\), on the set of cosets of a binary linear code \(\mathcal{C}\) of length \(n\). If \(\mathcal{C}_1\) and \(\mathcal{C}_2\) are two cosets of \(\mathcal{C}\), then \(\mathcal{C}_1 \le \mathcal{C}_2\) provided there are coset leaders \(\mathbf{x}_1\) of \(\mathcal{C}_1\) and \(\mathbf{x}_2\) of \(\mathcal{C}_2\) such that \(\mathbf{x}_1 \le \mathbf{x}_2\). As usual, \(\mathcal{C}_1 < \mathcal{C}_2\) means that \(\mathcal{C}_1 \le \mathcal{C}_2\) but \(\mathcal{C}_1 \neq \mathcal{C}_2\). Under this partial ordering the set of cosets of \(\mathcal{C}\) has a unique minimal element, the code \(\mathcal{C}\) itself.

### Example 11.7.1
Let \(\mathcal{C}\) be the \([5, 2, 3]\) binary code with generator matrix

![](img/0af7e79235839ec0eb8bcf8d229f37d4_477_0.png)

Then the cosets of \(\mathcal{C}\) with coset leaders are:

- \(\mathcal{C}_0 = 00000 + \mathcal{C}, \quad \mathcal{C}_4 = 00010 + \mathcal{C},\)
- \(\mathcal{C}_1 = 10000 + \mathcal{C}, \quad \mathcal{C}_5 = 00001 + \mathcal{C},\)
- \(\mathcal{C}_2 = 01000 + \mathcal{C}, \quad \mathcal{C}_6 = 10100 + \mathcal{C} = 01010 + \mathcal{C},\)
- \(\mathcal{C}_3 = 00100 + \mathcal{C}, \quad \mathcal{C}_7 = 10010 + \mathcal{C} = 01100 + \mathcal{C}.\)

The partial ordering of the cosets is depicted as

![](img/0af7e79235839ec0eb8bcf8d229f37d4_477_1.png)

