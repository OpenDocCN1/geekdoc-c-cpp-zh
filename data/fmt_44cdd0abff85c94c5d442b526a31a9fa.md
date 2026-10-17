
$W^1=\begin{matrix} 63.0218 & 0.0163 & 0.0217 & 12.1557 & 8.8835 \\ 0.0163 & 0.0000 & 0.0000 & 0.0267 & 0.0031 \\ 0.0217 & 0.0000 & 0.0000 & 0.0094 & 0.0061 \\ 12.1557 & 0.0267 & 0.0094 & 4.2011 & 59.5733 \\ 8.8835 & 0.0031 & 0.0061 & 59.5733 & 3.0416 \end{matrix}.$

我们有

$\overline{X^1}=\{(x,y,u)|(1,x,y,u)E^1W^1E^1(1,x,y,u) \geq 0\} \geq X^1$

### 5.3.2.2 切换单元格

当从一个单元格到另一个单元格的转换被释放时，二次形式的局部正性也将被使用。目前，我们感兴趣的是满足 $(x, u) \in X^i$ 且其像在 $X^j$ 中的 $(x, u)$ 集合，我们用 $X^{ij}$ 表示集合：

$\left \begin{matrix} x \\ u \end{matrix} \in \mathbb{R}^{d+m} \left(\begin{matrix} x \\ u \end{matrix} \right) \in X^i \text{ 且 } (A^ix + Bu) \in X^j$

对于所有对 $i, j \in \mathcal{I}$。在 [35] 中，作者考虑了对 $(i, j)$，使得在时刻 $k$ 存在 $X^i$ 中的状态 $x_k$，其像 $x_{k+1}$ 在 $X^j$ 中。我们将在 5.3.2 节中根据 [51] 的建议使用线性规划讨论可能的切换计算。为了构造 $X^{ij}$ 的二次化，我们使用之前的方法，引入一个具有非负元素的 $(1+n_i) \times (1+n_j)$ 对称矩阵 $U^{ij}$ 以得到集合 $X^{ij}$：

$X^{ij} = \left(\begin{matrix} 1 \\ x \\ u \end{matrix}\right) \left(\begin{matrix} 1 \\ x \\ u \end{matrix}\right)^T E^{ij} U^{ij} E^{ij} \left(\begin{matrix} 1 \\ x \\ u \end{matrix}\right) \geq 0$

其中 $E^{ij} = \frac{E^{ij}_s}{E^{ij}_w}$，

$E^{ij} = \left( \begin{matrix} 1 & 0_{1\times(d+m)} \\ -T^s_j & \left( \begin{matrix} c^s_i & b^i & 0 \end{matrix} \right) -T^w_j & \left( \begin{matrix} A^i & B^i & 0_{dx\times m} & Id_{m\times m} \end{matrix} \right) \end{matrix} \right) \quad (5.21)$

# 80

# 第 5 章

```
$$\begin{aligned} T_l^i(x,u) \ll c_s^i \ (x,u) \in \mathbb{R}^{d+m} & T_l^i(A^i x + B^i u + b^i, u) \ll c_s^i \\ T_w^i(x,u) \le c_w^i & (5.22) \\ T_d^i(A^i x + B^i u + b^i, u) \le c_w^i \ & \neq 0. \end{aligned}$$
```

如果从 $i$ 到 $j$ 的切换是可触发的，我们记作 $i \to j$。回我们可以同时处理严格不等式和不等式。问题 (5.22) 是一个同时包含严格不等式和弱不等式的线性规划可行性问题。然而，我们只检查系统是否有解，并可以使用 Motzkin 对换定理 [1] 来检测不可行性。Motzkin 定理是一种备选定理，即我们对比两个线性系统，使得其中恰好有一个是行的。为了描述备选系统，我们必须分离严格不等式和弱不等式，并使用方程 (5.21) 中定义的矩阵 $E^U$ 和 $E^W$。问题 (5.22) 等价于检查集 $\{y=(x,u) \in \mathbb{R}^{d+m}|E^U y \ge 0, E^W y \gg 0\}$ 是否为空。为了检测可行性，我们测试定义的备选系统的不可行性：

```
$$\begin{aligned} (E^U)^T p^s + (E^W)^T p^w &=0 \\ \sum_{k} p_k^w &=1 (5.23) \\ p_k^w \ge 0, \forall k \in \mathbb{I} \\ p_i \ge 0, \forall i \neq \mathbb{I}. \end{aligned}$$
```

根据 Motzkin 对换定理 [1]，我们得到以下命题。

## **命题 5.9.** 问题 (5.22) 是可行的当且仅当问题 (5.23) 是不可行的。

然而，直接对矩阵进行推理可能会允许不可达的切换。对于某些初始条件，对于所有 $k \in \mathbb{N}$，条件 $(x_k, u_k) \in X^i$ 且 $(A^i x_k + B^i u_k + b^i, u) \in X'$ 不成立，其中问题 (5.22) 是行的。为了避免这种情况，我们必须知道系统所有可能的轨迹（我们需要计算这些），并移除所有未激活的切换。近似不可达转换的一种可靠方法是识别线性约束的不可满足集。

**示例 5.10.** 我们继续详细说明我们的运行示例。更具体地说，我们考虑可能的切换。例如，我们考虑单元格 $X^2$如果以下线性不等式组有解，则从单元格 $X^2$ 切换到单元格 $X^1$ 是可能的：

![](img/8a0fdace52018a374ebad28735935393_92_0.png)

图 5.7. 浅灰色表示 $X^2$ 的截断表示，深灰色表示 $X^2$ 内部法则对 $X^1$ 的逆像。

```
$-9x+7y+6u < 5$
$-0.8532x+2.5748y-10.4460 < -68$
$-3.3662x+2.1732y-1.1084u < -58$
$4x-8y+8u \leq -4$
$u \leq 3$
$-u \leq 3$. (5.24)
```

前两个约束包含限制 $(x,y,u)$ 的像属于 $X^1$，而后四个约束对应于 $X^2$ 的定义。这些集（$X^2$ 和由 $X^2$ 中定义的法则对 $X^1$ 的逆像）的表示如图 5.7 所示。我们在图 5.7 中看到方程 (5.24) 中定义的不等式组似乎没有解。我们使用方程 (5.23) 和命题 5.9 进行此检查。方程 (5.23) 的矩阵 $E_s^{21}$ 和 $E_w^{21}$ 在此示例中为：

$E_s^{21} = \begin{pmatrix} 5 & 9 & -7 & -6 \\ -68 & 0.8532 & -2.5748 & 10.446 \\ -58 & 3.3662 & -2.1732 & 1.1084 \end{pmatrix}$

$E_w^{21} = \begin{pmatrix} -4 & -4 & 8 & -8 \\ 3 & 0 & 0 & 1 \end{pmatrix}$

我们通过 MATLAB 和 Linprog 求解了方程 (5.23) 中的线性规划，找到了 $p = (0.8735, 0.0983, 0.0282)^\top$ 和 $q = (0.3325, 14.2500, 7.8461)^\top$。这意味着备选系统是行的，因此根据命题 5.9，从 $X^2$ 到 $X^1$ 的转换是不可能的。

### 5.3.3 耦合条件的局部不变性

类似于线性情况，我们依赖 SDP 求解器；优化问题的未知数最多是二次的。李雅诺夫函数 $V$ 是分段定义的，依赖于分析系统的单元划分。$V$ 定义为：

```
$V(x,u) = V^\top(x,u), \text{ if } \begin{pmatrix} x \\ u \end{pmatrix} \in X^i$
$= \begin{pmatrix} x \\ u \end{pmatrix} P^i \begin{pmatrix} x \\ u \end{pmatrix} + 2q^{i\top}\begin{pmatrix} x \\ u \end{pmatrix}.$
```

函数 $V^i$ 仅仅定义在 $X^i$ 上。$V$ 的水平 $\alpha \in \mathbb{R}$ 的下水平集表示为：

```
$S_\alpha = \bigcup_{i \in \mathcal{I}} S_{i,\alpha}$
$= \bigcup_{i \in \mathcal{I}} \left( \begin{pmatrix} x \\ u \end{pmatrix} \in X^i | \begin{pmatrix} x \\ u \end{pmatrix}^\top P^i \begin{pmatrix} x \\ u \end{pmatrix} + 2q^{i\top}x \leq \alpha \right)$
$= \bigcup_{i \in \mathcal{I}} \left( \begin{pmatrix} x \\ u \end{pmatrix} \in X^i | \begin{pmatrix} x \\ u \end{pmatrix}^\top \begin{pmatrix} -\alpha \\ q^{i\top} \end{pmatrix} \begin{pmatrix} P^i \\ q^i \end{pmatrix} x \leq 0 \right)$
```

集 $S_{i,\alpha}$ 是与水平 $\alpha$ 相关的 $V^i$ 下水平集。我们考虑矩阵和向量对 $\{(P^i, q^i)\}_{i \in \mathcal{I}}$ 以及实数 $\alpha \in \mathbb{R}$，使得 $S_\alpha$ 是分段仿不变的。为了获得不变性，我们必须约束系统的初始条件。最后，为了证明可达集是有边界，我们需要约束 $S_\alpha$ 有界。在推导半不等式约束之前，让我们说明命题 5.11 中的一个有用结果。该结果是 S 程序 (10) 的一个特例，允许我们安全地编码蕴含。蕴含必须涉及两侧二次不等式。

**命题 5.11.** *设 $A, B, C$ 为 $d \times d$ 矩阵。那么 $C+A+B \geq 0$ 意味着蕴含 $(y^\top Ay \leq 0 \wedge y^\top By \leq 0) \implies y^\top Cy \geq 0$。*

## 作为代数集的不变量

### 5.3.3.2 半不等式约束写入 $(x, u) \in X^i \cap S_{i,\alpha}$

假设 $(x, u) \in X^i \cap S_{i,\alpha}$（索引 $i$ 是唯一的）。不变性意味着如果我们对 $(x, u)$ 应用适用法则并假设 $(x, u)$ 的像属于某个单元格 $X^j$（记 $i \to j$），则 $(x, u)$ 的像属于 $S_{j,\alpha}$。注意如果 $(x, u) \in X^i$ 且其像应该在 $X^j$，则 $(x, u) \in X^j$。设 $(i, j) \in \mathcal{T}^2$ 使得 $i \to j$，转换成不等式的不变性给出：

```
$$\begin{pmatrix} x \\ u \end{pmatrix} \in X^i \wedge \begin{pmatrix} x \\ u \end{pmatrix} \in S_{i,\alpha}$
$\implies \begin{pmatrix} A^i x + B^i u + b^i \\ u \end{pmatrix} \in S_{j,\alpha}. \quad (5.25)$
```

可以使用 5.3.2 节的松弛作为单元的表示，并使用矩阵 $W^i$ 和 $U^{ij}$ 来编码它们的二次化。对于 $(i, j) \in \mathcal{T}^2$ 使得 $i \to j$，我们得到：

```
$$\begin{pmatrix} x \\ u \end{pmatrix}^T E^{ij}U^{ij} \begin{pmatrix} x \\ u \end{pmatrix} \ge 0$$
$$\wedge \begin{pmatrix} x \\ u \end{pmatrix}^T \begin{pmatrix} -\alpha & q^{i\top} \end{pmatrix} \begin{pmatrix} P^i \\ q^i \end{pmatrix} \le 0 \quad (5.26)$$
```

其中 $E^{ij}$ 是方程 (20) 中定义的矩阵，$F^i$ 在 (4) 中定义。最后，通过考虑半不等式约束作为方程 (27)，我们得到一个更强的条件。命题 5.11 证明了如果 $(P^i, q^i, q^j, U^{ij})$ 是方程 (27) 的解，那么 $(P^i, q^i, q^j, U^{ij})$ 满足方程 (26)。对于 $(i, j) \in \mathcal{T}^2$ 使得 $i \to j$：

```
$-F^{i\top} \begin{pmatrix} q^{i\top} & P^i \end{pmatrix} F^i + \begin{pmatrix} 0 \end{pmatrix} - E^{ij\top} U^{ij} \geq 0. \quad (27)$
```

注意 $\alpha$ 在计算过程中被消除了。

### 5.3.4 初始化与有界性

为了获得不变性，我们必须约束初始条件。最后，为了证明可达集是有边界，我们需要约束 $S_\alpha$ 有界。在推导半不等式约束之前，让我们先说明命题 5.11 中的一个有用结果。该结果是 S 程序 (10) 的一个特例，允许我们安全地编码蕴含。蕴含必须涉及两侧二次不等式。

**命题 5.11.** *设 $A, B, C$ 为 $d \times d$ 矩阵。那么 $C+A+B \geq 0$ 意味着蕴含 $(y^\top Ay \leq 0 \wedge y^\top By \leq 0) \implies y^\top Cy \geq 0$。*

由于 $X^0 \cap X^i$ 是多面体，因此其空性可以通过检查线性问题 (5.30) 的可行性并使用命题 5.9 的相同论证来判定。

```
$$ \begin{cases} (E^{0i})^T p^i q^i = 0 \\ \sum_{k} p_k^i = 1 \\ p_k^i \geq 0, \forall k \in \mathcal{I} \\ p_i \geq 0, \forall i \notin \mathcal{I} \end{cases} \quad (5.30) $$
```

# 作为半代数集合的不变量

输入：由 $T_{s,w}^i, C_{s,w}^i, A^i, B^i, b^i, \forall i \in \mathcal{I}$ 定义的分段线性系统

局部：$E^i, E_j^i, E_0^i, \forall i, j \in \mathcal{I}$

输出：$\alpha, \beta, P^i, q^i, Z^i, W^i, U^i, \forall i, j \in \mathcal{I}$

- 1 使用方程 (5.19) 计算单元 $E^i$ 的二次化，$\forall i \in \mathcal{I}$

- 2 过近似可行切换：使用方程 (5.22) 计算分段切换 $L \in \mathcal{T}^2$：

- 3 使用方程 (5.20) 计算切换 $E^{ij}$ 的二次化，$\forall i, j \in \mathcal{L}$；

- 4 使用方程 (5.29) 计算初始化 $E^0$ 的二次化，$\forall i \in \mathcal{I}$；

- 5 求解方程 (5.34) 的 SDP 问题

- 6 不变量：

- 7 $U\{(x,u)P_{opt}^i(x,u)^T + 2(x,u)q_{opt}^i \leq \alpha_{opt} \mid (x,u) \in X^i\}_{i \in \mathcal{I}}$

- 8 $\|(x,u)\| \leq \beta_{opt}$

图 5.8 用于分段线性动力系统计算分段二次不变量算法。

## 5.3.4.2 将有界性写为半定约束

下水平集 $S_\alpha$ 有界当且仅当对于所有 $i \in \mathcal{I}$，下水平集 $S_{i,\alpha}$ 有界。蕴含形式的有界约束为，对于所有 $i \in \mathcal{I}$，存在 $\beta \geq 0$：

$$(x,u) \in X^i \wedge \begin{pmatrix} x \\ u \end{pmatrix} \in S_{i,\alpha} \implies \|(x,u)\|_2^2 \leq \beta \quad (5.31)$$

其中 $\|\cdot\|_2$ 表示 $\mathbb{R}^{d+m}$ 的欧几里得范数

作为不变性，我们使用 $X^i$ 的二次化和 $S_{i,\alpha}$ 的定义。我们利用 $\|(x,u)\|_2^2 = \begin{pmatrix} x \\ u \end{pmatrix}^T E^i W^i E^i \begin{pmatrix} x \\ u \end{pmatrix} + Id(d+m) \times (d+m)$ 这一事实，并对于所有 $i \in \mathcal{I}$ 得到：

$$\begin{pmatrix} x \\ u \end{pmatrix}^T E^i W^i E^i \begin{pmatrix} x \\ u \end{pmatrix} \geq 0 \wedge$$
