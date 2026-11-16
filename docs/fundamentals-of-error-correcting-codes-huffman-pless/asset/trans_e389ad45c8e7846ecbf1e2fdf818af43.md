

### Example 7.5.4
设 $\mathcal{C}$ 为一个 $[16, 8, 4]$ 自偶双偶二进制码。由 Example 7.3.3，其权重分布由 $A_0(\mathcal{C}) = A_{16}(\mathcal{C}) = 1$，$A_4(\mathcal{C}) = A_{12}(\mathcal{C}) = 28$，以及 $A_8(\mathcal{C}) = 198$ 给出。按 Theorem 7.5.2 的记号，$S = \{4, 8, 12, 16\}$ 且 $s = 4$。因此 $\mathcal{C}$ 的覆盖半径至多为 4。假设 $\mathbf{v}$ 是 $\mathcal{C}$ 的一个权重为 4 的陪集的陪集领元。（注意我们不知道这样的陪集领元是否存在。）设 $\mathcal{D}$ 为由 $\mathcal{C}$ 和 $\mathbf{v}$ 生成的 $[16, 9, 4]$ 线性码；因此 $\mathcal{D} = \mathcal{C} \cup (\mathbf{v} + \mathcal{C})$。$\mathcal{D}$ 是一个偶码，且 $\mathcal{D}^\perp \subset \mathcal{C}$。设 $A_i = A_i(\mathcal{D}^\perp)$ 和 $A_i^\perp = A_i(\mathcal{D})$。由于 $\mathcal{D}$ 是偶码，$\mathcal{D}^\perp$ 包含全一向量。因此我们知道 $A_0 = A_{16} = 1$ 且对于除 $i = 4, 8,$ 或 $12$ 以外的所有其他 $i$，$A_i = 0$（因为 $\mathcal{D}^\perp \subset \mathcal{C}$）。因此利用 (7.8) 的前三个方程，我们得到

```
1 + A_4 + A_8 + A_{12} + 1 = 2^7.
4A_4 + 8A_8 + 12A_{12} + 16 = 2^6 \cdot 16.
16A_4 + 64A_8 + 144A_{12} + 256 = 2^5 \cdot 16 \cdot 17.
```

求解得 $A_4 = A_{12} = 12$ 且 $A_8 = 102$。由于 $\mathcal{D}$ 包含全一向量，$A_i^\perp = A_{16-i}^\perp$。由于 $\mathcal{D}$ 是具有最小权重 4 的偶码，对于奇数 $i$，$A_1^\perp = 0$，因此我们只需要 $A_4^\perp$、$A_8^\perp$ 和 $A_{12}^\perp$ 即可完全确定 $\mathcal{D}$ 的权重分布。利用 $(M_3)$、$(K)$ 或 $(P_1)$，我们发现 $A_4^\perp = 44$，$A_8^\perp = 64$，且 $A_{12}^\perp = 294$。陪集 $\mathbf{v} + \mathcal{C}$ 的权重分布为 $A_i(\mathbf{v} + \mathcal{C}) = A_i(\mathcal{D}) - A_i(\mathcal{C})$。因此，权重为 4 的陪集的权重分布被唯一确定为：

| 权重 | 4 | 6 | 8 | 10 | 12 |
|---|---|---|---|---|---|
| 向量数量 | 16 | 64 | 64 | 96 | 16 |

注意我们仍然不知道这样的陪集是否存在。

### Exercise 395
设 $\mathcal{C}$ 为一个 $[16, 8, 4]$ 自偶双偶二进制码。类比于 Example 7.5.4，设 $\mathbf{v}$ 为 $\mathcal{C}$ 的一个权重为 3 的陪集的陪集领元，并设 $\mathcal{D}$ 为 $[16, 9, 3]$ 码 $\mathcal{D} = \mathcal{C} \cup (\mathbf{v} + \mathcal{C})$。设 $A_i = A_i(\mathcal{D}^\perp)$ 和 $A_i^\perp = A_i(\mathcal{D})$。（与权重为 4 的陪集一样，我们不知道这样的陪集是否存在：）
- (a) 证明 $A_{16} = 0$ 且唯一未知的 $A_i$ 是 $A_4$、$A_8$ 和 $A_{12}$。
- (b) 证明 $A_4^\perp = A_{16-4}^\perp$ 且 $A_1^\perp = 0$。
- (c) 利用 (7.8) 的前三个方程计算 $A_4$、$A_8$ 和 $A_{12}$。
- (d) 由 Exercise 72，$\mathbf{v} + \mathcal{C}$ 仅含有奇权重向量。证明 $\mathcal{D}$ 中所有奇权重向量都在 $\mathbf{v} + \mathcal{C}$ 中。
- (e) 利用 $(M_3)$、$(K)$ 或 $(P_1)$ 求 $\mathbf{v} + \mathcal{C}$ 的权重分布。

### Exercise 396
设 $\mathcal{C}$ 为一个 $[16, 8, 4]$ 自偶双偶二进制码。类比于 Exercise 395，设 $\mathbf{v}$ 为 $\mathcal{C}$ 的一个权重为 1 的陪集的陪集领元，并设 $\mathcal{D}$ 为 $[16, 9, 1]$ 码 $\mathcal{D} = \mathcal{C} \cup (\mathbf{v} + \mathcal{C})$。设 $A_i = A_i(\mathcal{D}^\perp)$ 和 $A_i^\perp = A_i(\mathcal{D})$。
- (a) 为什么我们知道权重为 1 的陪集必须存在？
- (b) 证明 $A_{16} = 0$ 且唯一未知的 $A_i$ 是 $A_4$、$A_8$ 和 $A_{12}$。
- (c) 证明 $A_4^\perp = A_{16-4}^\perp$ 且 $A_1^\perp = 0$。
- (d) 利用 (7.8) 的前三个方程计算 $A_4$、$A_8$ 和 $A_{12}$。
- (e) 由 Exercise 72，$\mathbf{v} + \mathcal{C}$ 仅含有奇权重向量。证明 $\mathcal{D}$ 中所有奇权重向量都在 $\mathbf{v} + \mathcal{C}$ 中。
- (f) 利用 $(M_3)$、$(K)$ 或 $(P_1)$ 求 $\mathbf{v} + \mathcal{C}$ 的权重分布。

### Exercise 397
设 $\mathcal{C}$ 为一个 $[16, 8, 4]$ 自偶双偶二进制码。在完成 Exercises 395 和 396 后，做如下事情：(a) 证明 $\mathbb{F}_2^{16}$ 中所有奇权重向量都在 $\mathcal{C}$ 的一个权重为 1 或权重为 3 的陪集中。（b) 证明 $\mathcal{C}$ 恰好有 16 个权重为 1 的陪集和恰好 112 个权重为 3 的陪集。

注意，这个练习表明权重为 3 的陪集确实存在。

在计算 $[16, 8, 4]$ 码中权重为 2 的陪集的权重分布之前，我们先给出以下有用结果。

### Theorem 7.5.5
设 $\mathcal{C}$ 为 $\mathbb{F}_q$ 上长度为 $n$ 的码，且 $A \in \Gamma \operatorname{Aut}(\mathcal{C})$。设 $\mathbf{v} \in \mathbb{F}_q^n$。那么陪集 $\mathbf{v} + \mathcal{C}$ 的权重分布与陪集 $\mathbf{v}A + \mathcal{C}$ 的权重分布相同。

### Proof
若 $\mathbf{x} \in \mathbb{F}_q^n$，则对 $\mathbf{x}$ 应用 $A$ 会用非零标量重新缩放分量、置换分量，并通过一个域自同态将它们映射到其他域元素。因此 $w(\mathbf{x}) = w(\mathbf{x}A)$。由于 $A \in \Gamma \operatorname{Aut}(\mathcal{C})$，$\mathbf{v}A + \mathcal{C} = \{\mathbf{v}A + \mathbf{c} \mid \mathbf{c} \in \mathcal{C}\} = \{(\mathbf{v} + \mathbf{c})A \mid \mathbf{c} \in \mathcal{C}\}$，这意味着 $\mathbf{v}A + \mathcal{C}$ 和 $\mathbf{v} + \mathcal{C}$ 具有相同的权重分布。

### Example 7.5.6
设 $\mathcal{C}$ 为一个 $[16, 8, 4]$ 自偶双偶二进制码。由 [262]，直到等价性，存在两个这样的码。每个码的权重为 2 的陪集具有不同的权重分布。这两个码，分别记为 $\mathcal{C}_1$ 和 $\mathcal{C}_2$，具有生成矩阵 $G_1$ 和 $G_2$，其中

![](img/0af7e79235839ec0eb8bcf8d229f37d4_286_0.png)

和

![](img/0af7e79235839ec0eb8bcf8d229f37d4_286_1.png)

在本例中，我们计算 $\mathcal{C}_1$ 的权重为 2 的陪集的权重分布。注意 $\mathcal{C}_1$ 是一个 $[8, 4, 4]$ 码与自身的直和，唯一这样的码是由 Exercise 56 给出的 $\widehat{\mathcal{H}}_3$。设 $\mathbf{v}$ 为一个权重为 2 且是 $\mathcal{C}_1$ 的一个陪集的陪集领元的向量。由于我们想求 $\mathbf{v} + \mathcal{C}_1$ 的权重分布，由 Theorem 7.5.5，我们可以将 $\mathbf{v}$ 替换为 $\mathbf{v}A$，其中 $A$ 是 Exercise 398 中给出的 $\mathcal{C}_1$ 的自同构的乘积。我们使用该练习的记号。设 $\operatorname{supp}(\mathbf{v}) = \{a, b\}$；当我们将 $\mathbf{v}$ 替换为 $\mathbf{v}A$ 时，我们仍将此新向量的支持记为 $\{a, b\}$，其中 $a$ 和 $b$ 将具有不同的值。如果 $a$ 和 $b$ 都至少为 9，则对 $\mathbf{v}$ 应用 P3。因此我们可以假设 $1 \leq a < b \leq 8$ 或 $1 \leq a \leq 8 < b$。在第一种情况下，如果 $a \neq 1$，则应用 P3 的幂次后跟 P1，这样我们可以假设 $a = 1$；现在再次应用 P3 的幂次，这样我们可以假设 $b = 2$。在第二种情况下，如果 $a \neq 1$，则应用 P3 的幂次后跟 P1，这样我们可以假设 $a = 1$；如果 $b \neq 9$，则应用 P1 的幂次后跟 P2，这样我们可以假设 $b = 9$。因此，我们只需要考虑两个可能的陪集领元：

- (a) $\mathbf{v}_1 = 11000000000000000$，以及
- (b) $\mathbf{v}_2 = 10000000100000000$。

我们首先考虑 $\mathbf{v} = \mathbf{v}_1$。设 $\mathcal{D}$ 为 $[16, 9, 2]$ 码 $\mathcal{D} = \mathcal{C}_1 \cup (\mathbf{v}_1 + \mathcal{C}_1)$。设 $A_i = A_i(\mathcal{D}^\perp)$ 和 $A_i^\perp = A_i(\mathcal{D})$。$\mathcal{D}$ 是一个偶码，因此 $\mathcal{D}^\perp$ 包含全一向量。因此我们知道 $A_0 = A_{16} = 1$ 且对于除 $i = 4, 8,$ 或 $12$ 以外的所有其他 $i$，$A_i = 0$（由 $\mathcal{D}^\perp \subset \mathcal{C}_1$）。我们还知道 $A_1^\perp = 0$ 并且需要确定 $A_4^\perp$。在 $\mathbf{v}_1 + \mathcal{C}_1$ 中，除了 $\mathbf{v}_1$ 之外，唯一的权重为 2 的向量是 $\mathbf{v}_1 + \mathbf{c}$，其中 $\mathbf{c}$ 是支持包含 $\{1, 2\}$ 的权重为 4 的向量。通过检查 $G_1$，很明显这样的 $\mathbf{c}$ 的唯一选择是 $G_1$ 的前三行。因此 $A_2^\perp = 4$。因此利用 (7.8) 的前三个方程，我们得到

```
1 + A_4 + A_8 + A_{12} + 1 = 2^7,
4A_4 + 8A_8 + 12A_{12} + 16 = 2^6 \cdot 16,
16A_4 + 64A_8 + 144A_{12} + 256 = 2^5(16 \cdot 17 + 8).
```

求解得 $A_4 = A_{12} = 20$ 且 $A_8 = 86$。由于 $\mathcal{D}$ 包含全一向量，$A_i^\perp = A_{16-i}^\perp$。利用 $(M_3)$、$(K)$ 或 $(P_1)$，我们有 $A_4^\perp = 36$，$A_6^\perp = 60$，且 $A_8^\perp = 310$。由于 $A_i(\mathbf{v}_1 + \mathcal{C}_1) = A_i(\mathcal{D}) - A_i(\mathcal{C}_1)$，陪集 $\mathbf{v}_1 + \mathcal{C}_1$ 的权重分布为：

| 权重 | 2 | 4 | 6 | 8 | 10 | 12 | 14 |
|---|---|---|---|---|---|---|---|
| 向量数量 | 4 | 8 | 60 | 112 | 60 | 8 | 4 |

现在考虑 $\mathbf{v} = \mathbf{v}_2$。设 $\mathcal{D}$ 为 $[16, 9, 2]$ 码 $\mathcal{D} = \mathcal{C}_1 \cup (\mathbf{v}_2 + \mathcal{C}_1)$，它仍然是偶码。与 $\mathbf{v} = \mathbf{v}_1$ 的情况一样，$A_0 = A_{16} = 1$ 且只有 $A_4, A_8,$ 和 $A_{12}$ 需要确定，因为其他 $A_i$ 为 0。另外 $A_1^\perp = 0$，但 $A_2^\perp = 1$，因为显然没有支持包含 $\{1, 9\}$ 的权重为 4 的向量在 $\mathcal{C}_1$ 中。因此利用 (7.8) 的前三个方程，我们得到

```
1 + A_4 + A_8 + A_{12} + 1 = 2^7,
4A_4 + 8A_8 + 12A_{12} + 16 = 2^6 \cdot 16,
16A_4 + 64A_8 + 144A_{12} + 256 = 2^5(16 \cdot 17 + 2).
```

以与 $\mathbf{v} = \mathbf{v}_1$ 相同的方式，我们得到 $A_4 = A_{12} = 14$，$A_8 = 98$，$A_4^\perp = 42$，$A_6^\perp = 63$，且 $A_8^\perp = 298$。陪集 $\mathbf{v}_2 + \mathcal{C}_1$ 的权重分布为：

| 权重 | 2 | 4 | 6 | 8 | 10 | 12 | 14 |
|---|---|---|---|---|---|---|---|
| 向量数量 | 1 | 14 | 63 | 100 | 63 | 14 | 1 |

