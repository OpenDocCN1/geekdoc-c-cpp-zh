

![](img/4913dd83a2a14bc205a0a92cce102c82_289_0.png)

图 14.1 初始网格（左），两步后的细化网格（中），四步后的细化网格（右）。*

![](img/4913dd83a2a14bc205a0a92cce102c82_289_1.png)

图 14.2 相对于网格尺寸 h 的 H^1-范数（左）和 L^2-范数（右）中的相对误差。

## 14.3 二维自适应 BEM-基 FEM

在均匀细化策略中，网格中的每个元素被分割为两个新元素，以获得下一个更细的网格。这种分割过程按下文所述执行。为了根据定理 14.1 获得最优收敛率，解必须是光滑的。这一假设在实际应用中经常被违反，其中奇异性可能由于不连续的材料参数或几何中的重入角而产生。因此，均匀细化的收敛速度会变慢。因此，必须根据问题调整网格，以恢复最优收敛率。对于自适应

*转载自《Numerische Mathematica》，多边形网格上 BEM-基 FEM 的残差误差估计，第 118 卷，2011 年，第 765-788 页，S. Weißer，© Springer-Verlag 2011，经 Springer 许可。†转载自《Computers & Mathematics with Applications》，第 67(7) 卷，S. Weißer，多边形网格上任意阶 Trefftz 类基函数及其在 BEM-基 FEM 中的实现，第 1390-1406 页，版权 (2014)，经 Elsevier 许可。

BEM-基 FEM，我们采用一种常用策略，即在每个步骤中仅选择若干元素进行细化，参见 [403]。关键要素是逐元素误差指示器 \(\eta_P\)，用于监测单个元素上的近似质量。在以下内容中，我们假设这些指示器在所需范数中界定真实误差，使得

```
\(\|u - u_h\| \le c \eta_R = c \left( \sum_{P \in \mathcal{T}_h} \eta_P^2 \right)^{1/2} . \quad (14.14)\)
```

在第 14.3.2 节中，我们介绍了一种基于残差的误差估计器，用于界定能量范数中的误差。

### 14.3.1 自适应 FEM 策略

自适应 BEM-基 FEM 依次细化对误差贡献最大的元素。该策略在四个步骤的循环中进行：

- **求解** 边值问题 (14.1) 通过在当前多边形网格上使用近似空间 \(V_h^k\) 的 BEM-基 FEM 进行近似。

- **估计** 在离散化 \(\mathcal{T}_h\) 上计算误差估计器 \(\eta_R\) 以及逐元素误差指示器 \(\eta_P\)（参见第 14.3.2 节）。

- **标记** 根据 Dörfler 策略 [125] 标记所有元素的一个最小子集 \(\mathcal{M}_h \subset \mathcal{T}_h$，使得

```
\(\left( \sum_{P \in \mathcal{M}_h} \eta_P^2 \right)^{1/2} \ge (1 - \theta) \eta_R,\)
```

其中 \(0 \le \theta < 1\) 是用户定义的参数。为了获得最小集 \(\mathcal{M}_h\)，可以根据指示器 \(\eta_P\) 对元素进行排序并标记指示器最大的元素。相反，我们实现了 [125] 中给出的标记算法以实现线性复杂度。此外，在数值实验中我们选择 \(\theta = 0.5\)。

- **细化** 每个标记元素都会被细化，从而为循环的下一个周期获得新网格。对于元素 \(P\) 的细化，我们通过其重心 \(\bar{\boldsymbol{x}}\) 且正交于其特征方向对 \(P\) 进行二等分，参见图 14.3，该方向由矩阵

```
\(M_{\text{Cov}} = \int_P (\boldsymbol{x} - \bar{\boldsymbol{x}})(\boldsymbol{x} - \bar{\boldsymbol{x}})^\top d\boldsymbol{x}, \quad \bar{\boldsymbol{x}} = \frac{1}{|P|} \int_P \boldsymbol{x} \, d\boldsymbol{x}.\)
```

有关更多详情，参见 [420]。此外，我们检查网格的规则性，如果对于任何 \(i = 1, \dots, n\) 都违反了 \(c_T h_P \le h|_{u_i, u_{i+1}}\)，则使用用户定义的参数 \(c_T\) 细化额外元素。

![](img/4913dd83a2a14bc205a0a92cce102c82_291_0.png)

自适应网格细化过程保持非常局部。在细化过程中，只有标记元素和退化元素被二等分。不需要处理悬挂节点并保持网格可接受，例如三角网格的红-蓝-绿细化程序中，参见 [403]。这一优势归功于具有非常灵活元素的多边形网格。

### 14.3.2 多边形网格的基于残差的误差估计

基于残差的事后误差估计界定了与双线性形式相关的能量范数中精确解与加勒金近似之间的差异。该估计中包含元素边上共法线导数的跳跃等。设 \(P \in \mathcal{T}_h\) 为具有边 \([v_i, v_{i+1}]\) 的多边形元素，\(P' \in \mathcal{T}_h\) 为包含该边的相邻元素。那么，在 \((v_i, v_{i+1})\) 上的跳跃由以下给出：

> \([u_h] = \frac{\partial u_h|_P}{\partial n_P} + \frac{\partial u_h|_{P'}}{\partial n_{P'}}.\)

我们定义所谓的边残差为

> \(R_{P,i} = \begin{cases} 0 & \text{for } (v_i, v_{i+1}) \subset \Gamma_D, \\ g_N - \frac{\partial u_h}{\partial n_P} & \text{for } (v_i, v_{i+1}) \subset \Gamma_N, \\ -\frac{1}{2}[u_h] & \text{for } (v_i, v_{i+1}) \subset \Omega. \end{cases}\)

现在所有要素都已具备，可以给出满足 (14.14) 的能量范数 \(\|\nabla \cdot \|_{L_2(\Omega)}\) 的基于残差的误差估计。

### 定理 14.2（可靠性）

设 \(\mathcal{T}_h\) 为规则网格。此外，设 \(u \in V\) 和 \(u_h \in V_h^k\) 分别为 (14.2) 和由 (14.3) 得到的加勒金近似的解。那么，基于残差的误差估计是可靠的，即，

```
\|\nabla(u - u_h)\|_{L_2(\Omega)} \le c \eta_R \quad \text{with} \quad \eta_R^2 = \sum_{P \in \mathcal{T}_h} \eta_P^2,
```

其中误差指示器定义为

```
\eta_P^2 = h_P^2 \|f + \Delta u_h\|_{L_2(P)}^2 + \sum_{i=1}^n h_{[v_i, v_{i+1}]} \|R_{P,i}\|_{L_2([v_i, v_{i+1}])}^2.
```

常数 \(c > 0\) 仅取决于网格的规则性参数和近似阶数 k。

根据前一定理，能量范数中的误差至少以误差估计器 \(\eta_R\) 相同的速率减小。为了获得一个可用于有效估计真实误差的良好估计器，重要的是误差不应减小得比 \(\eta_R\) 更快。这种行为在下一定理中显示，其中误差指示器 \(\eta_P\) 被界定为误差加上一些数据振荡的形式。对于下界，估计涉及元素 \(P\) 的邻域 \(\omega_P\)。该元素补片由 \(\bar{\omega}_P = \bigcup \{P' : P' \in \mathcal{T}_h, P \cap P' \neq \emptyset\}\) 给出。

### 定理 14.3（效率）

在定理 14.2 的假设下，基于残差的误差指示器是高效的，即，

```
\eta_P \le c \left( \|\nabla(u - u_h)\|_{L_2(\omega_P)}^2 + h_P^2 \|f - \bar{f}\|_{L_2(\omega_P)}^2 + \sum_{\substack{i=1, \dots, n, \\ [v_i, v_{i+1}] \subset \Gamma_D}} h_{[v_i, v_{i+1}]} \|g_N - \bar{g}_N\|_{L_2([v_i, v_{i+1}])}^2 \right)
```

其中 \(\bar{f}\) 和 \(\bar{g}_N\) 分别是数据 \(f\) 和 \(g_N\) 的分段多项式近似。常数 \(c > 0\) 仅取决于网格的规则性参数和近似阶数 k。

术语 \(\|f - \bar{f}\|_{L_2(\omega_P)}\) 和 \(\|g_N - \bar{g}_N\|_{L_2([v_i, v_{i+1}])}\) 通常称为数据振荡。它们通常是高阶项。

### 14.3.3 数值示例

设 \(\Omega = ((-1, 1) \times (-1, 1)) \setminus ([0, 1] \times [0, -1])\) 和 \(\Gamma_D = \partial \Omega\)。使用极坐标 \((r, \varphi)\) 对 \(x = (r \cos \varphi, r \sin \varphi)\)，边界数据 \(g_D\) 选择使得

```
u(r \cos \varphi, r \sin \varphi) = r^{2/3} \sin \left( \frac{2\varphi}{3} \right)
```

是边值问题的解

```
-\Delta u = 0 \quad \text{in } \Omega, \quad u = g_D \quad \text{on } \Gamma.
```

