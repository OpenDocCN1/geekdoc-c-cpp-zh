
我们现在对式 (11) 中的第一个方程关于 `$x$` 求微分，并将结果代入第二个方程。经过重命名 `f_i := f_i^2 - \frac{1}{\alpha_i}\partial_x f_i^1`，`\mathcal{I} = \{i=1,\dots,m\}` 并引入 `\beta_i = \frac{c_i^2}{a_i\alpha_i}`，我们有 `p_i = -\beta_i\partial_x q_i + p_i`。我们在图 `G` 上考虑具有简单节点处 Neumann 控制的半线性椭圆问题。

$$\begin{aligned}
\alpha_i q_i(x) - \beta_i\partial_{xx} q_i(x) + g_i(x;q_i(x)) &= f_i(x),\ x\in(0,\ell_i), i\in\mathcal{I}\\
\beta_j\partial_x q_j(n_k) &= \beta_i\partial_x q_i(n_k),\ i\neq j\in\mathcal{I}_k,\ k\in\mathcal{J}^M\setminus(\mathcal{J}_c\cup\mathcal{J}_v)\\
q_i(n_k) &= 0,\ i\in\mathcal{I}_k,\ n_k\in\mathcal{J}_D^\delta\\
\partial_x q_i(n_k) &= u_k,\ i\in\mathcal{I}_k,\ n_k\in\mathcal{J}_N^\delta\\
\sum_{i\in\mathcal{I}_k} d_{ik} q_i(n_k) &= 0,\ k\in\mathcal{J}^M,
\end{aligned}$$

$$s_j^v\big(-\beta_i\partial_x q_i(n_j)+\beta_k\partial_x q_k(n_j)\big)+(1-s_j^v)q_i(n_j)=-s_j^v\big(\bar p_i(n_j)-\bar p_k(n_j)\big),\ j\in\mathcal{J}_v,\ i\in\mathcal{I}_j^-,\ k\in\mathcal{I}_j^+$$

$$s_j^c\left(u_j - C\left(\frac{\left(-\beta_k\partial_x q_k(n_j)+\bar p_k(n_j)\right)^{\operatorname{sign}(q_k(n_j))\kappa}}{\left(-\beta_i\partial_x q_i(n_j)+\bar p_i(n_j)\right)}-1\right)\right)$$

$$+(1-s_j^c)\big(-\beta_i\partial_x q_i(n_j)+\beta_k\partial_x q_k(n_j)\big)=(1-s_j^c)\big(\bar p_i(n_j)-\bar p_k(n_j)\big)\quad j\in\mathcal{J}_c,\ i\in\mathcal{I}_j^-,\ k\in\mathcal{I}_j^+$$

其中我们设 `g_i(x;s):=\gamma_i(x)s|s|`。我们随后考虑如下最优控制问题：

$$\min_{(p,q,u,s)} I(p,q,u,s):=\sum_{i\in\mathcal{I}}\int_0^{\ell_i} I_i(p_i,q_i)dx + \frac{\nu}{2}\sum_{j\in\mathcal{J}^\delta}|u_j|^2 + \frac{\mu}{2}\sum_{j\in\mathcal{J}_v\cup\mathcal{J}_c}s_j^2$$

s.t.

$$(p,q,u,s)\text{ satisfies }(2.12).$$

在式 (2.8) 中，我们得到了一系列关于度量图上椭圆半线性系统的混合整数最优控制问题。我们有意对非线性部分关于时间进行离散化，使得表达式的分母包含前一时间层的 `p_i`。这种选择导致了单调非线性。因此，对于给定的控制 `(u,s)`，我们可以应用著名的 Brezis 定理关于非线性算子的满射性 [10]。在此精神下，我们可以将 [7, 11] 中的适定性结果推广到此情形。

设 `(u,s)\in\mathbb{R}^{|\mathcal{J}_N^\delta|}\times\{0,1\}^{|\mathcal{J}_v\cup\mathcal{J}_c|}` 为给定的控制且 `f\in\Pi_{i=1}^N L^2(0,\ell_i)` 为给定的右端项。则存在唯一的解 `q\in\Pi_{i=1}^N H^1(0,\ell_i)` 满足式 (2.12)。此外，式 (2.8) 中的最优控制问题存在唯一的优化解 `(u,s)`。

我们认识到，即使在瞬时控制范式下，最优控制问题式 (2.13) 对于现实网络中的计算来说也过于复杂。我们因此现在求助于域分解技术以将图简化为合适的子图。特别地，我们选择子图 `G_{sub}` 使得整数控制——按构造在给定的串联节点 `\mathcal{J}_v\cup\mathcal{J}_c` 处操作——在子图的内部节点处执行。也就是说，我们在多节点 `\mathcal{J}^M\setminus(\mathcal{J}_c\cup\mathcal{J}_v)` 处进行分解。该方法可以写成

使得整个图 `G` 被不相交地分解为子图 `G_{i_k}` 即 `G = \dot{\cup}_k G_{k}`。在子图之间的界面节点处——这些节点可以具有二重或更多重数——不假设离散控制。非常精确地说，该方法需要更多的记号，由于篇幅限制我们在此省略。完整的图景将在他处发表。

### 2.3 域分解

我们提供一种迭代的非重叠域分解，可解释为 Uzawa 方法（Alg3，按 Glowinski 的意义）。细节见专著 [12]。该算法的思想源于传输条件的解耦。为此，我们定义通量向量 `q^k := (d_{ik} q_i(n_k), i \in \mathcal{I}_k)^T` 和压力向量 `\partial q^k := (\beta_i \partial_x q_i(n_k), i \in \mathcal{I}_k)^T` 在给定节点 `n_k, k \in \mathcal{J}^M \setminus (\mathcal{J}_c \cup \mathcal{J}_v)` 处。给定向量 `z := (z_i, i \in \mathcal{I}_k)`，我们定义

`$(S^k(z))_i := \frac{2}{d_k} \sum_{j \in \mathcal{I}_k} z_j - z_i.$`  (2.14)

则 `$(S^k)^2 = I$` 且 `S^k(1) = 1` 对 `1 := (1, \dots, 1) \in \mathbb{R}^{d_k}`。在此记号下，一般概念很容易建立。我们对任意 `\sigma > 0` 设：

`q^{k} + \sigma \partial q^{k} = \sigma S^{k}(\partial q^{k}) - S^{k}(q^{k}).`  (2.15)

对式 (2.15) 两边应用 `S^k`，我们得到

`\sum_{i \in \mathcal{I}_k} d_{ik} q_i(n_k) = 0.`  (2.16)

但此时式 (2.15) 化简为

`\partial q_i(n_k) = \frac{1}{d_k} \sum_{k \in \mathcal{I}_k} \partial q_j(n_k), \ i \in \mathcal{I}_k,`

进而推出

`\beta_i \partial_x q_i(n_k) = \beta_j \partial_x q_j(n_k), \ i \neq j \in \mathcal{I}_k, \ k \in \mathcal{J}^M \setminus (\mathcal{J}_c \cup \mathcal{J}_v).`  (2.17)

显然，如果在多节点 `n_k` 处满足式 (2.16) 和 (2.17) 的传输条件，则式 (2.15) 也成立。因此，式 (2.15) 等价于式 (2.16) 和 (2.17) 的传输条件。这些新的式 (2.15) 条件现在在迭代格式中被松弛如下。我们用 `l` 表示迭代次数。

`$(p^k)^{l+1} + \sigma \partial (q^k)^{l+1} = \sigma S^k((\partial q^k)^l) - S^k((q^k)^l) := (g^k)^{l+1}.$`  (2.18)

我们有如下关系：

`$(g^k)^{l+1} = S^k (2\sigma\partial(q^k)^l - (g^k)^l).$`  (2.19)

这导致了不动点映射的定义。为此，我们需要研究界面关于 `g^k`，`k \in \mathcal{J}^M \setminus (\mathcal{J}_c \cup \mathcal{J}_v)` 的行为，即

`g \in X := \Pi_{k \in \mathcal{J}^M \setminus (\mathcal{J}_c \cup \mathcal{J}_v)} \Pi_{i \in \mathcal{I}_k} , \|g\|_X^2 := \sum_{k \in \mathcal{J}^M \setminus (\mathcal{J}_c \cup \mathcal{J}_v)} \sum_{i \in \mathcal{I}_k} (1/\sigma) |g_{i,k}|^2,`  (2.20)

`T : X \to X,`  (2.21)

`$(Tg)_{i,k} := S^k (2\sigma\partial(q^k) - g^k)_{i,k}, k \in \mathcal{J}^M \setminus (\mathcal{J}_c \cup \mathcal{J}_v), i \in \mathcal{I}_k,$`

`$(Tg)_k = \{(Tg)_{i,k}, i \in \mathcal{I}_k\},`

`Tg = \{(Tg)_k, k \in \mathcal{J}^M \setminus (\mathcal{J}_c \cup \mathcal{J}_v)\}.`

松弛的固定点迭代如下：对 `\varepsilon \in [0,1]`

`g^{l+1} = (1 - \varepsilon) T(g^l) + \varepsilon g^l.`  (2.22)

为了分析迭代的收敛性，我们需要具体说明方程。为了证明收敛，需要处理式 (2.12) 问题解与

`\alpha_i q_i^{l+1}(x) - \beta_i \partial_{xx} q_i^{l+1}(x) + g_i(q_i^{l+1}) = f_i(x), x \in (0,\ell_i), i \in \mathcal{I}`

`q_i(n_k)^{l+1} = 0, i \in \mathcal{I}_k, n_k \in \mathcal{J}_D^S`

`\partial_x q_i(n_k)^{l+1} = u_k, i \in \mathcal{I}_k, n_k \in \mathcal{J}_N^S`

`d_{ik} q_i^{l+1}(n_k) + \sigma\partial q_i^{l+1}(n_k) = \sigma\left( \frac{2}{d_k} \sum_{j \in \mathcal{I}_k} \beta_j \partial q_j^l(n_k) - \beta_i \partial_x q_i(n_k) \right) - \left( \frac{2}{d_k} \sum_{j \in \mathcal{I}_k} d_{ik} q_j^l(n_k) - d_k q_i(n_k) \right) = g_{ik}^{l+1}, k \in \mathcal{J}^M \setminus (\mathcal{J}_c \cup \mathcal{J}_v)`  (2.23)

`\sum_{i \in \mathcal{I}_j} \beta_i q_i^{l+1}(n_j) = 0, j \in \mathcal{J}_c \cup \mathcal{J}_v`

`s_j^v (-\beta_i \partial_x q_i(n_j)^{l+1} + \beta_k \partial_x q_k(n_j)^{l+1}) + (1 - s_j^v) q_i(n_j)^{l+1} = -s_j^v (\bar p_i(n_j) - \bar p_k(n_j)), j \in \mathcal{J}_v, i \in \mathcal{I}_j^-, k \in \mathcal{I}_j^+`

`s_j^c \{ u_j - C\left( \frac{(-\beta_i \partial_x q_k(n_j)^{l+1} + \bar p_k(n_j))}{(-\beta_i \partial_x q_i(n_j)^{l+1} + \bar p_i(n_j))} \right)^{\operatorname{sign}(q_k(n_j)^{l+1})_k} -1 \} + (1 - s_j^c)(-\beta_i \partial_x q_i(n_j)^{l+1} + \beta_k \partial_x q_k(n_j)^{l+1}) = (1 - s_j^c)(\bar p_i(n_j) - \bar p_k(n_j)) j \in \mathcal{J}_c, i \in \mathcal{I}_j^-, k \in \mathcal{I}_j^+.`

之间的误差。重要的是要理解式 (2.23) 是子图上的椭圆问题，其中在受控串联节点处保持原始传输条件。式 (2.23) 中边之间的唯一耦合是在节点 `\mathcal{J}_c \cup \mathcal{J}_v` 处！因此，我们引入 `e^{l+1} := q^{l+1} - q`。则 `e^{l+1}` 求解具有非线性

`g_i(e_i^{l+1}+q_i)-g_i(q_i)`，零右端项且在简单节点处齐次边界条件的非线性微分方程。我们假设

`$(g_i(x;s)-g_i(x;t))(s-t) \ge 0, \forall x \in (0,\ell_i), i \in \mathcal{I}.$`  (2.24)

则我们可以证明（见式 [13]），在式 (2.24) 假设下，对每个 `\varepsilon \in [0,1)`，式 (2.22) 与式 (2.23) 以及式 (2.20) 和 (2.21) 的迭代当 `l \to \infty` 时收敛。

### 2.4 最优控制问题的域分解

处理原始最优控制问题在域分解背景下有多种方式。我们概述两种策略。第一种可视为 Jacobi 型方法。这里我们将域分解关于控制问题的迭代置于外部，仅最小化与包含在子图 `G_k` 中的边相关的成本部分。在第二种方法中，我们固定整数控制 `s` 并将整个图的相应最优性系统分解为子图 `G_k`，采用另一种但非常相似的非重叠域分解，如 [13] 中所述。这是 [12] 中给出的虚拟控制范式的精髓。

#### 2.4.1 分解系统上的最优控制：Jacobi 型过程

这里，我们在子图 `G_r = (V_r, E_r)` 上引入如下混合整数控制问题，对应指标集 `\mathcal{I}^r, \mathcal{J}^r`。我们引入 `G_r` 内多节点和简单节点的指标集为 `\mathcal{J}^{r,M}, \mathcal{J}^{r,S}` 以及其他集合相应地。然后我们考察子图 `G_r` 上的如下问题：

`\alpha_i q_i^{l+1}(x) - \beta_i \partial_{xx} q_i^{l+1}(x) + g_i(q_i^{l+1}) = f_i(x), x \in (0,\ell_i), i \in \mathcal{I}^r`

`q_i(n_k)^{l+1} = 0, i \in \mathcal{I}^r, n_k \in \mathcal{J}_D^{r,S}`

`\partial_x q_i(n_k)^{l+1} = u_{k,i}, i \in \mathcal{I}^r, n_k \in \mathcal{J}_N^{r,S}`

`d_{ik} q_i^{l+1}(n_k) + \sigma\partial_x q_i^{l+1}(n_k)`

`= \sigma\left( \frac{2}{d_k} \sum_{j\in I_k} \beta_j \partial_x q_j^{l}(n_k) - \beta_i \partial_x q_i^{l}(n_k) \right)`

`- \left( \frac{2}{d_k} \sum_{j\in I_k} d_{jk} q_j^{l}(n_k) - d_{ik} q_i^{l}(n_k) \right) = g_{ik}^{l+1}, k \in \mathcal{I}^M \setminus (\mathcal{J}_c^r \cup \mathcal{J}_v^r)^r`  (2.25)

`\sum_{i\in T_j} \beta_i q_i^{l+1}(n_j) = 0, j \in \mathcal{J}_c^r \cup \mathcal{J}_v^r`

`s_j^v (-\beta_i \partial_x q_i(n_j)^{l+1} + \beta_k \partial_x q_k(n_j)^{l+1}) + (1 - s_j^v) q_i(n_j)^{l+1} = -s_j^v (\bar p_i(n_j) - \bar p_k(n_j)), j \in \mathcal{J}_v^r, i \in \mathcal{T}_j^{r,-}, k \in \mathcal{T}_j^{r,+}`
