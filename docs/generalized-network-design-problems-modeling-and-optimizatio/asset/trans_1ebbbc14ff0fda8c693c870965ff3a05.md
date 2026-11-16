

![](img/8ee31706d554c7b9e05caa9ab83aec83_178_0.png)

图 6.1. 分层网络设计示例。

固定费用网络设计（GFCND）问题，由 Thomadsen 和 Stidsen [200] 引入。

GFCND 问题属于广义网络设计问题类，这类问题通过考虑相对于图节点划分为节点集的给定划分的相关问题，从经典网络设计问题自然得出。

## 6.1 GFCNDP 的定义

给定一个 n 节点无向图 G = (V, E) 以及 V 划分为 m 个簇 V1,...,Vm，我们假设每个簇内的节点通过簇网络内部连接，而簇之间则未连接，但必须通过骨干网络连接，以便进行通信。我们还假设，不同簇中任意两个选定节点（枢纽）之间存在一条带有正成本的跨簇边。除了边建立成本之外，每条跨簇边都有一个所需容量，该容量取决于通信需求以及需求的路由方式。

GFCNDP 旨在寻找连接每个给定簇中恰好一个枢纽的最便宜骨干网络。该问题涉及两个相关决策

- 从每个簇 |Vi| 中选择一个枢纽，对所有 i = 1, ..., m。
- 寻找连接恰好所选枢纽的最便宜骨干网络。

在图 6.2(a) 中展示了五个节点集（簇）。各簇的节点数量可能不同。我们假设每个簇中的所有节点都通过跨簇网络连接。

![](img/8ee31706d554c7b9e05caa9ab83aec83_179_0.png)

图 6.2. 广义固定费用网络设计 (a) 节点集（簇），(b) 骨干网络。

另一方面，簇之间未连接，但必须通过骨干网络连接，以便进行通信。在图 6.2 b) 中展示了这样一种可能的骨干网络。

## 6.2 GFCNDP 的整数规划公式

给定一个无向图 \( G = (V, E) \)，相关的有向图是通过将每条边 \( e = \{i, j\} \in E \) 替换为反向弧 \( (i, j) \) 和 \( (j, i) \) 得到的，这些弧的权重与边 \( \{i, j\} \in E \) 相同。为了将 GFCND 问题建模为混合整数规划问题，我们定义以下相关集合、参数和决策变量

### 集合和符号：

- \( V \) – 所有节点的集合，\( i \in V \)。
- \( V_1, \dots, V_m \) – \( V \) 划分为 \( m \) 个称为 *簇* 的子集。
- \( E \) – 边的集合（无序节点对），\( e \in E \)。
- \( A \) – 弧的集合（有序节点对），\( a \in A \)。
- \( D \) – 商品集合，表示任何无序簇对之间需要满足的需求，\( d \in D \)。
- \( s_a \) 和 \( t_a \) – 分别表示弧 \( a \) 的起始节点和终止节点。
- \( s_d \) 和 \( t_d \) – 分别表示需求 \( d \) 的起始簇和终止簇。

### 参数：

- $c_e$ – 边 $e$ 的固定成本，$e \in E$。
- $g_a$ – 弧 $a$ 的容量成本，即使用该弧的每单位需求的成本。
- $b_d$ – 需求 $d$ 的通信需求量。

### 决策变量：

- 二进制决策变量

\( z_i = \left\{ \begin{array}{ll} 1 & \text{如果节点 } i \text{ 被选为枢纽节点} \\ 0 & \text{否则} \end{array} \right. \) ,
\( x_e = \left\{ \begin{array}{ll} 1 & \text{如果边 } e \in E \text{ 在两个枢纽节点之间被选中} \\ 0 & \text{否则} \end{array} \right. \) ,
\( w_a = \left\{ \begin{array}{ll} 1 & \text{如果弧 } a \in A \text{ 在两个枢纽节点之间被选中} \\ 0 & \text{否则} \end{array} \right. \) .

- 分数连续流变量：\( f_{ij}^d \) 反映每条弧 \( (i, j) \in A \) 和商品 \( d \in D \) 的运输决策。

我们的第一个模型使用上述定义的二进制决策变量和多商品流变量 \( f_a^d \)。

```
\(\min \sum_{e \in E} c_e x_e + \sum_{d \in D, a \in A} g_a b_d f_a^d\)
\(s.t.\)
\( z(V_k) = 1, \quad \forall k \in K = \{1, \dots, m\}, \) (6.1)
\( \sum_{a \in \delta^+(i)} f_a^d - \sum_{a \in \delta^-(i)} f_a^d = \left\{ \begin{array}{ll} z_i, & i \in s_d \\ -z_i, & i \in t_d \\ 0 & \text{otherwise} \end{array} \right. \quad d \in D, i \in V, \) (6.2)
\( x_e \le z_i, \quad \forall e \in E \text{ and } i \in e, \) (6.3)
\( f_{ij}^d \le w_{ij}, \quad \forall a = (i, j) \in A, d \in D, \) (6.4)
\( w_{ij} + w_{ji} = x_e, \quad \forall e = \{i, j\} \in E, \) (6.5)
\( f_a^d \ge 0, \quad \forall a = (i, j) \in A, d \in D, \) (6.6)
\( x, z, w \in \{0, 1\}. \) (6.7)
```

在上述 GFCNDP 的混合整数规划公式中，目标函数表示边建立成本和边容量需求成本的组合，约束 (6.1) 保证从每个簇中恰好选择一个枢纽节点，流守恒约束 (6.2) 保证每个源-目的簇对之间的需求得到满足。右侧如果需求源自簇 $s_d$ 则为 $z_i$，如果需求结束于簇 $t_d$ 则为 $-z_i$，否则为 0。限制 (6.3) 保证仅在选定枢纽之间建立边。限制 (6.4) 不仅确保尊重弧容量，而且如果弧在设计中未被选中，则强制任何商品的流量为 0，约束 (6.5) 关联附加到边上的变量与附加到弧上的变量之间的连接。最后，约束 (6.7) 和 (6.8) 定义变量的定义域。

我们将此模型称为定向多商品流模型。我们令 $P_{\text{mcflow}}$ 表示该模型线性规划松弛可行集投影到 $(x, z)$-空间。

通过消除二进制变量 $w_{ij}$，我们得到一个密切相关的公式。所得公式由约束 (6.1)、(6.2)、(6.3)、(6.6)、(6.7) 加上

```
$f_{ij}^d + f_{ji}^{d'} \le x_e, \quad \forall d \in D \text{ and } \forall e \in E. \quad (6.8)$
```

我们将此模型称为 GFCNDP 的 *双向流公式*，并令 $P_{\text{bidflow}}$ 表示其在 $(x, z)$-空间中的可行解集。请注意，由于在构建双向流公式时我们消除了变量 $w_a$，因此该模型定义在无向图 $G = (V, E)$ 上，尽管对于每个需求 $d \in D$，我们在边 $e = \{i, j\}$ 上两个方向都执行流量 $f_{ij}^d$ 和 $f_{ji}^d$。该模型由 Thoradsen 和 Stidsen [200] 引入，基于此，作者提出了一种用于求解 GFCNDP 的分支-切割-定价算法。

在双向流公式中，我们称之为双向流不等式的约束 (6.8) 关联了在边 $\{i, j\}$ 上不同方向流动的不同需求的流量。

以下结果成立：

### 提议 6.1。

$P_{\text{mcflow}} = P_{\text{bidflow}}$。

**证明。** 如果 $(w, x, z, f) \in P_{\text{mcflow}}$，那么，使用约束 (6.4) 我们有

```
$f_{ij}^d + f_{ji}^{d'} \le w_{ij} + w_{ji} = x_e, \quad \forall e = \{i, j\} \in E \text{ and } \forall d, d' \in D.$
```

另一方面，假设 $(x, z, f) \in P_{\text{bidflow}}$。从约束 (6.8) 我们得到

```
$\max_d f_{ij}^d + \max_{d'} f_{ji}^{d'} \le x_e. \quad \forall e = \{i, j\} \in E.$
```

因此，我们可以选择 $w$ 使得 $\max_d f_{ij}^d \le w_{ij}$ 且对所有 $e = (i, j) \in E$ 有 $x_e = w_{ij} + w_{ji}$。例如，取

```
$w_{ij} = \frac{1}{2}(x_e + \max_d f_{ij}^d - \max_{d'} f_{ji}^{d'}).$
```

显然，$(w, x, z, f) \in P_{\text{mcflow}}$。

令 \( G' \) 为由 \( G \) 通过将簇 \( V_i \) 的所有节点替换为表示 \( V_i \) 的超级节点而得到的图。为方便起见，我们将 \( V_i \) 与表示它的超级节点识别。我们将此图称为全局图，并假设顶点集为 \( \{V_1, ..., V_m\} \) 的 \( G' \) 是完全图。我们将此全局图的节点集表示为 \( V_g \)，\( V_g = \{1, ..., m\} \)，边集表示为 \( E_g \)，\( E_g = \{e_g = (i, j) \mid i, j \in \{1, ..., m\} \} \)，弧集表示为 \( A_g \)。

我们的最后一个公式旨在区分全局（即跨簇）连接和局部（即不同簇节点之间）连接。Pop [142] 引入的局部-全局方法已成功应用于广义最小生成树问题 [160, 150] 和广义旅行商问题 [79] 的强整数规划公式、精确算法和求解程序。

我们引入二进制变量 \( y_{ij} \) (\( i, j \in \{1, ..., m\} \)) 来描述全局连接，因此如果簇 \( V_i \) 连接到簇 \( V_j \) 则 \( y_{ij} = 1 \)，否则 \( y_{ij} = 0 \)。这个由 \( P_{FCND} \) 表示的多面体可以由以下多项式数量的约束表示：

```
\sum_{a_g \in \delta^+(i)} F_{a_g}^d - \sum_{a_g \in \delta^-(i)} F_{a_g}^d = \begin{cases} 1, & i \in s_{gd} \\ -1, & i \in t_{gd} \\ 0, & \text{otherwise} \end{cases} \quad \forall d \in D, i \in V_g, \quad (6.9)
F_{ij}^d + F_{ji}^d \leq y_e \kappa_e, \quad \forall e_g = (i, j) \in E_g, d \in D. \quad (6.10)
y_{ij} \in \{0, 1\}, \quad \forall i, j \in V_g. \quad (6.11)
F_{a_g}^d \geq 0, \quad \forall a_g \in A_g, d \in D. \quad (6.12)
```

其中连续决策变量 \( F_{a_g}^d \) 对应于在弧 \( a_g \) 上路由的需求 \( d \) 的分数，其与决策变量 \( f_a^d \) 的关系由 \( F_{a_g}^d = \sum_{(a=(i,j)) \in A \mid i \in V_k, j \in V_l} f_a^d \) 给出。\( \kappa_e = (k,l) \in A_g \)。

如果 0-1 向量 \( y \) 对应于收缩图上的固定费用网络设计问题，则可以通过求解以下整数线性规划问题来获得成本最小化的相应局部解 \( x, z \in \{0, 1\}^{|E|} \)：

```
\min \sum_{e \in E} c_e x_e
s.t.
z(V_k) = 1, \quad \forall k \in K = \{1, ..., m\},
x(V_l, V_r) = y_{lr}, \quad \forall l, r \in K = \{1, ..., m\}, l \neq r,
x(i, V_r) \leq z_i, \quad \forall r \in K, \forall i \in V \setminus V_r,
x_e, z_i \in \{0, 1\}, \quad \forall e = \{i, j\} \in E, \forall i \in V,
```

其中 \( x(V_l, V_r) = \sum_{i \in V_l, j \in V_r} x_{ij} \) 且 \( x(i, V_r) = \sum_{j \in V_r} x_{ij} \)。

