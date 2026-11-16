

### 广义割集公式 (Myung et al. [128])

我们可以用连通性约束替换子回路消除约束 (2.2)，从而得到在 [128] 中引入的所谓的 *广义割集公式*：

```
min \(\sum_{e \in E} c_e x_e\)
s.t. (2.1), (2.3), (2.4), (2.5) and
\(x(\delta(S)) \ge z_i + z_j - 1, \forall i \in S \subset V, j \notin S\) (2.6)
```

其中，对于所有 \(S \subset V\)，割集 \(\delta(S)\) 通常定义为：

```
\(\delta(S) = \{e = \{i, j\} \in E \mid i \in S, j \notin S\}.\)
```

我们用 \(P_{cut}\) 表示该公式线性规划松弛的可行集。Myung et al. [128] 证明了以下关系成立：\(P_{sub} \subset P_{cut}\)。

### 广义多割公式 (Pop [142])

我们的下一个模型，即所谓的 *广义多割公式*，是通过用多割替换简单割集得到的。给定节点的一个划分 \(V = C_0 \cup C_1 \cup \dots \cup C_k\)，我们将多割 \(\delta(C_0, C_1, \dots, C_k)\) 定义为连接不同 \(C_i\) 和 \(C_j\) 的边集。GMSTP 的广义多割公式为：

```
\(\sum_{e \in E} c_e x_e\)
s.t. (2.1), (2.3), (2.4), (2.5) and
\(x(\delta(C_0, C_1, \dots, C_k)) \ge \sum_{j=0}^k z_{ij} - 1,\)
\(\forall C_0, C_1, \dots, C_k \text{ node partitions of } V \text{ and } \forall i \in C_j \text{ for } j = 0, 1, \dots, k.\) (2.7)
```

令 \(P_{mcut}\) 表示该模型线性规划松弛的可行集。显然，\(P_{mcut} \subseteq P_{cut}\)，此外，可以证明以下结果成立：

### 提议 2.3 (Pop [142])。\(P_{sub} = P_{mcut}\)。

证明。令 \((x, z) \in P_{sub}\)，且 \(C_0, C_1, \dots, C_k\) 为 \(V\) 的一个节点划分。

Since

```
\(E = E(C_0) \cup E(C_1) \cup \dots \cup E(C_k) \cup \delta(C_0, C_1, \dots, C_k),\)
```

我们得到

```
\(x(\delta(C_0, C_1, \dots, C_k) = x(E) - x(E(C_0)) - x(E(C_1)) - \dots - x(E(C_k)).\)
```

对于所有 \(j = 0, 1, \dots, k\) 和 \(i \in C_j\)，我们有：

\(x(E(C_j)) \le z(C_j) - z_{ij}\)。

因此我们得到：

\(x(\delta(C_0, C_1, \dots, C_k) \ge z(V) - 1 - \sum_{j=0}^k [z(C_j) - z_{ij}] = \sum_{j=0}^k z_{ij} - 1\)。

反之，令 \((x, z) \in P_{mcut}\)，\(i \in S \subset V\)，并考虑不等式 (2.7)，其中 \(C_0 = S\)，而 \(C_1, \dots, C_k\) 为并集为 \(V \setminus S\) 的单元素集。则

\(x(\delta(S, C_1, \dots, C_k)) \ge \sum_{j=0}^k z_{ij} - 1 = z_i + z(V \setminus S) - 1\)，

其中 \(i \in S \subset V\)。因此

\(x(E(S)) = x(E) - x(\delta(S, C_1, \dots, C_k)) \le z(V) - 1 - z_i - z(V \setminus S) + 1 = z(S) - z_i\)。

### 簇子打包公式 (Feremans [37])

我们可以通过用簇子打包约束替换子回路消除约束 (2.2) 来加强 GMSTP 的广义子回路公式：

\(x(E(S)) \le z(S \setminus V_k), \quad \forall S \subset V, 2 \le |S| \le n - 1, k \in K\)

我们观察到这些约束被以下约束所支配：

\(x(E(S')) \le z(S' \setminus V_k) = z(S') - 1\)

其中 \(S' = S \cup V_k\)。因此，我们得到了由 Feremans [37] 引入的 GMSTP 的簇子打包公式：

```
min \(\sum_{e \in E} c_e x_e\)
s.t. (2.1), (2.3), (2.4), (2.5) and
\(x(E(S)) \le z(S) - 1, \forall S \subset V, 2 \le |S| \le n - 1, |\{k : V_k \subseteq S\}| \neq 0 \quad (2.8)\)
```

簇子打包约束 (2.8) 保证，从任何节点子集 S（\(2 \le |S| \le n - 1\)）中选取的边数不能大于从该集合中选取的节点数减 1。我们将用 \(P_{spack}\) 表示簇子打包公式线性规划松弛的可行集。

## 2.3.2 基于树形图性质的公式

考虑有向图 \(D = (V, A)\)，它是通过将每条边 \(e = (i, j) \in E\) 替换为 \(A\) 中的反向弧 \((i, j)\) 和 \((j, i)\) 得到的，这些弧的权重与边 \((i, j) \in E\) 相同。由 Myung et al. [128] 引入的 GMSTP 的有向版本，称为广义最小生成树形图问题，定义在有向图 \(D = (V, A)\) 上，根设在给定的簇上，此处不失一般性地选择为 \(V_1\)，并由确定一棵最小成本树形图组成，该树形图包含每个簇中的恰好一个节点。

本节将介绍的接下来两个公式由 Feremans et al. [37] 引入。

### 有向广义外集公式 (Feremans [37])

我们首先考虑 GMSTP 的有向广义外集公式。在此模型中，我们考虑有向图 \(D = (V, A)\)，簇 \(V_1\) 不失一般性地被选为根，并记 \(K_1 = K \setminus \{1\}\)。

```
min \sum_{e \in E} c_e x_e
s.t. \quad z(V_k) = 1, \quad \forall k \in K = \{1, \dots, m\}
x(E) = m - 1
w(\delta^-(S)) \ge z_i, \quad \forall i \in S \subseteq V \setminus V_1 \quad (2.9)
w_{ij} \le z_i \quad \forall i \in V_1, j \notin V_1 \quad (2.10)
w_{ij} + w_{ji} = x_e \quad \forall e = (i, j) \in E \quad (2.11)
x, z, w \in \{0, 1\}. \quad (2.12)
```

在此模型中，约束 (2.9) 和 (2.10) 保证从选定的根节点到任何其他选定节点存在一条仅包含选定节点的路径。令 \(P_{rcut}\) 表示该模型线性规划松弛可行集投影到 \((x, z)\)-空间。

Myung et al. 在 [128] 中考虑的另一种可能的有向广义外集公式，是通过用以下约束替换 (2.3) 得到的：

```
w(\delta^-(V_1)) = 0 \quad (2.13)
w(\delta^-(V_k)) \le 1, \quad \forall k \in K_1. \quad (2.14)
```

### 有向子打包公式 (Feremans [37])

我们现在介绍一种基于分支的 GMSTP 公式。如同之前的公式一样，考虑有向图 \(D = (V, A)\)，其中 \(V_1\) 被选为簇根。

GMSTP 的有向子打包公式定义如下：

```
min \sum_{e \in E} c_e x_e
s.t. z(V_k) = 1, \forall k \in K = \{1, \dots, m\}
x(E) = m - 1
w(A(S)) \le z(S - i), \forall i \in S \subset V, 2 \le |S| \le n - 1 (2.15)
w(\delta^-(j)) = z_j, \forall j \in V \setminus V_1 (2.16)
w_{ij} + w_{ji} = x_e, \forall e = (i, j) \in E
x, z, w \in \{0, 1\}.
```

令 \(P_{dbsub}\) 表示该模型线性规划松弛可行集投影到 \((x, z)\)-空间。显然，\(P_{dbsub} \subseteq P_{sub}\)。Feremans [37] 建立了以下结果：\(P_{dbsub} = P_{dcut} \cap P_{sub}\)。在此，我们现在给出该结果的另一个证明，参见 Pop [142]。

### 提议 2.4。\(P_{branch} = P_{dcut} \cap P_{sub}\)。

**证明。** 首先，我们证明 \(P_{dcut} \cap P_{sub} \subseteq P_{branch}\)。令 \((x, z) \in P_{dcut} \cap P_{sub}\)。利用关系 (2.13) 和 (2.14)，可以轻松看出约束 (2.16) 得到满足。因此，\((x, z) \in P_{branch}\)。

我们证明 \(P_{branch} \subseteq P_{dcut} \cap P_{sub}\)。显然 \(P_{branch} \subseteq P_{sub}\)。因此，只需证明 \(P_{branch} \subseteq P_{dcut}\)。

令 \((x, z) \in P_{branch}\)。对于所有 \(i \in V_1\) 和 \(j \notin V_1\)，取 \(S = \{i, j\} \subset V\)。那么根据 (2.14)，我们有 \(w_{ij} + w_{ji} \ge z_i$，这蕴含 (2.9)。

我们现在证明，对于 \(l \in V_k, k \in K_1\)，有 \(w(\delta^-(l)) \le z_l\)。取 \(V^l = \{i \in V \mid (i, l) \in \delta^-(l)\}\) 和 \(S^l = V^l \cup \{l\}\)，则 \(w(\delta^-(l)) = w(A(S^l))\)，并选择 \(i_l \in V^l\)。

```
1 = \sum_{l \in V_k} w(\delta^-(l)) = \sum_{l \in V_k} w(A(S^l)) \le \sum_{l \in V_k} z(S^l \setminus \{i_l\})
= \sum_{l \in V_k} z_l + \sum_{l \in V_k} \sum_{j \in V \setminus \{i_l\}} z_j = 1 + \sum_{l \in V_k} \sum_{j \in V \setminus \{i_l\}} z_j.
```

因此，对于所有 \(l\)，只有一个 \(i_l \in V^l\) 满足 \(z_{i_l} \neq 0$，且

```
w(\delta^-(l)) = w(A(S^l)) \le z(S^l \setminus \{i_l\}) = z_l.
```

对于每个 \(i \in S \subset V \setminus V_1\)

```
w(A(S)) = \sum_{i \in S} w(\delta^-(i)) - w(\delta^-(S)) \le z(S \setminus \{i\}).
```

