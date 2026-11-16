

### 15.2.7 扩展到三维

我们现在简要考虑当 \(\Omega\) 是 \(\mathbb{R}^3\) 的子集时的情况。在这种情况下，\(\Omega_h\) 被假设为由具有平面面和直边的非常一般形状的多面体组成的网格，虚拟空间（15.13）通过取

\[
\begin{aligned}
V_h^P := \left\{ v_h \in H^1(P) : \Delta v_h \in \mathbb{P}_{k-2}(P); \right.\\
\left. v|_e \in V_h^f \text{ for each face } f \text{ of } P; \right.\\
\left. v_h|_{\partial P} \in C^0(\partial P) \right\},
\end{aligned}
\tag{15.13}
\]

其中 \(V_h^f\) 是面 \(f\) 上的二维离散空间，在 15.2.3 节中引入（约定 \(\mathbb{P}_{-1}(P) = \{0\}\)）。

与二维情况一样，可以考虑该空间的两个等价基：自然基，通过空间定义（15.13）的一组狄利克雷问题定义；虚拟基，通过与顶点值以及边、面和单元 \(P\) 内部上的矩相关的自由度定义。然而，在 3D 情况下，15.2.5 节的正交投影不能直接使用这些自由度计算，因为这将要求了解单元面上阶数高达 \(k-1\) 和 \(k\) 的矩，而这些矩无法从（15.13）中获得。

为绕过此问题，必须以这样的方式修改空间，使这些额外矩可用。一种方法是通过放松其定义中要求的条件来简单地扩展空间，以便可以将额外矩作为自由度。然而，这会导致空间维度的显著增加，因此最终矩阵的大小也会增加。相反，一种称为 *VEM 增强* 的过程已被开发（参见 [6, 82]），以产生与 \(V_h^P\) 具有相同虚拟自由度的空间，但其中这些矩可以计算。我们指出，尽管虚拟自由度保持不变，但 \(V_h^P\) 的自然基对于增强空间不再有效。

## 15.3 椭圆PDE的虚拟单元方法

### 15.3.1 模型问题

考虑标量变量 \(u\) 的扩散，它满足以下泊松问题（关于更一般椭圆问题的处理，我们参考 [29, 82]）：

\[
\begin{aligned}
-\text{div}(K\nabla u) &= f \text{ in } \Omega, \tag{15.14}\\
u &= g \text{ on } \partial\Omega. \tag{15.15}
\end{aligned}
\]

其中 \(K\) 是扩散张量，\(f\) 是强迫项，\(g\) 定义了（通常是非齐次的）狄利克雷边界条件。我们假设：

- (H1) \(\Omega\) 是 \(\mathbb{R}^2\) 的一个有界、开的多胞形子集；
- (H2) 扩散张量 \( K : \Omega \to \mathbb{R}^{d \times d} \) 是一个 \( d \times d \) 有界、可测且对称的张量。此外，我们假设 \( K \) 是强椭圆的，即，存在两个正常数 \( C_* \) 和 \( C^* \)，使得对几乎每个 \( \boldsymbol{x} \in \Omega \),

  \( C_* \|\boldsymbol{\xi}\|^2 \leqslant \boldsymbol{K}(\boldsymbol{x})\boldsymbol{\xi} \leqslant C^* \|\boldsymbol{\xi}\|^2 \quad \forall \boldsymbol{\xi} \in \mathbb{R}^d,\)

  其中 \( \|\boldsymbol{\xi}\|^2 = \boldsymbol{\xi} \cdot \boldsymbol{\xi} \) 是 \( \boldsymbol{\xi} \) 的欧几里得2-范数的平方；
- (H3) 两个函数 \( f \) 和 \( g \) 分别属于 \( L^2(\Omega) \) 和 \( H^{\frac{1}{2}}(\partial\Omega) \)。

问题（15.14）-（15.15）的变分形式为：

求 \( u \in H_g^1(\Omega) \)，使得

\( \mathcal{A}(u, v) := \int_\Omega K \nabla u \cdot \nabla v \, dV = \int_\Omega f v \, dV \quad \forall v \in H_0^1(\Omega), \quad (15.16) \)

其中

\( H_g^1(\Omega) := \{ u \in H^1(\Omega) \mid u|_{\partial\Omega} = g \}.\)

在假设（H1）-（H3）下，（15.16）存在唯一弱解，这源于双线性形式 \( \mathcal{A}(\cdot, \cdot) \) 的连续性和强制性。

### 15.3.2 符合性VEM概述

在符合性虚拟单元方法中，我们用对称双线性形式 \( \mathcal{A}_h(\cdot, \cdot) \) 近似对称双线性形式 \( \mathcal{A}(\cdot, \cdot) \)，该形式可以 *精确* 计算而无需评估虚拟空间的函数。此外，当其至少一个条目是次数 \( k \geqslant 1 \) 的多项式时，\( \mathcal{A}_h(\cdot, \cdot) \) 应该精确评估 \( \mathcal{A}(\cdot, \cdot) \)。此属性称为 *多项式一致性*，可表述为：

\( \mathcal{A}_h(v, p) = \mathcal{A}(v, p),\)

该性质对任何 \( v \in V_h \) 和在 \( \Omega_h \) 上定义的分段 \( k \) 次多项式函数 \( p \) 成立。多项式一致性属性决定了方法的精度。除此之外，当试函数和测试函数不是多项式时，我们仅要求 \( \mathcal{A}_h(\cdot, \cdot) \) 相对于 \( \mathcal{A}(\cdot, \cdot) \) 是 *稳定* 的。（15.16）的右侧也通过类似过程离散化。最后，原始问题的狄利克雷边界条件在虚拟单元公式中通过定义 \( V_{h,g}^k \) 为 \( V_h^k \) 的仿射子空间来施加，其函数在 \( \partial\Omega \) 上插值边界条件 \( g \)。在实际实现中，\( V_h^k \) 的虚拟函数上的边界条件通过限制其与 \( \partial\Omega \) 上的顶点和边相关的自由度，使其与 \( g \) 的顶点值和边界矩重合来施加。

（15.16）的虚拟单元近似为：求 \( u_h \in V_{h,0}^k \)，使得：

\( \mathcal{A}_h(u_h, v_h) = (f, v_h)_h \quad \forall v_h \in V_{h,0}^k. \quad (15.17) \)

该问题的良好设置性质通过上述稳定性属性从（15.16）的良好设置性质得出。（15.17）中的离散双线性形式定义为局部贡献之和

\[
\mathcal{A}_h(u_h, v_h) = \sum_{P \in \Omega_h} \mathcal{A}_h^P(u_h, v_h),
\]

其中每个单元项都是一致性项和稳定性项之和，

\[
\mathcal{A}_h^P(u_h, v_h) = \mathcal{A}_{cons}^P(u_h, v_h) + \mathcal{A}_{stab}^P(u_h, v_h),
\]

其中

\[
\mathcal{A}_{cons}^P(u_h, v_h) = \int_P K \Pi_{k-1}^\nabla \nabla u_h \cdot \Pi_{k-1}^\nabla \nabla v_h \, dV,
\]

\[
\mathcal{A}_{stab}^P(u_h, v_h) = \overline{\kappa}_P S_P((I - \Pi_k^\nabla) u_h, (I - \Pi_k^\nabla) v_h),
\]

其中 \(\Pi_{k-1}^\nabla\) 和 \(\Pi_k^\nabla\) 如 15.2.5 节中定义。这里，\(\overline{\kappa}_P\) 是 \(K\) 在 \(P\) 上的常数近似，例如其单元平均值或单元重心处的值，而 \(S_P: V_h^k \times V_h^k \to \mathbb{R}\) 是双线性形式

\[
S_P(u_h, v_h) := \sum_{r=1}^n \text{dof}_r(u_h) \text{dof}_r(v_h),
\]

其中，对于 \(w_h \in V_h^k\)，我们使用 \(\text{dof}_r(u_h)\) 表示 \(w_h\) 的第 \(r\) 个自由度的值，相对于局部自由度的某个任意但固定的顺序。这个双线性形式只是自由度向量空间 \(\mathbb{R}^n\) 上的欧几里得内积。右侧离散化为

\[
(f, v_h)_h := \sum_{P \in \Omega_h} \int_P f \Pi_{k-2}^0 v_h \, dV.
\]

**备注 15.4.** 这种近似在 \(k=1, 2\) 时在 \(L^2\)-范数中是次优的。然而，对于这些情况，可以构建右侧的替代近似，从而使方法最优。

在相当一般的网格假设 [82] 下，可以证明存在一个与 \(h\) 和 \(P\) 无关的常数 \(C\)，使得

\[
C^{-1} \mathcal{A}^P(v_h, v_h) \le \mathcal{A}_h^P(v_h, v_h) \le C \mathcal{A}^P(v_h, v_h)
\]

对所有 \(v_h \in V_h^k\)，这提供了方法的 *稳定性* 并确保存在唯一离散解。此外，当 \(u_h\) 或 \(v_h\) 中任何一个是多项式时，\(\mathcal{A}_h^P(\cdot, \cdot)\) 的第一项将非零，当两者都是多项式时，双线性形式将精确评估 \(\mathcal{A}^P(\cdot, \cdot)\)。

所有项都可以仅使用自由度以及评估和积分多项式的能力来计算。实现细节可见 [28, 386]。特别是，除了多项式子空间之外，永远不需要对虚拟函数进行点值评估。鉴于该方法的虚拟性质，数值解以其自由度的形式已知，即节点值和矩，从中通过插值获得全局连续解。

