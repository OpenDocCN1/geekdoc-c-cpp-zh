

尚需讨论 (14.3) 的设置以及如何计算相关积分。矩阵 \(\mathbf{K}\) 和右端项 \(\mathbf{f}\) 的构建与 FEM 中一样，通过汇集局部（单元级）刚度矩阵完成。因此，我们写出

\(b(\varphi_j, \varphi_i) = \sum_{P \in \mathcal{T}_h} \int_P \nabla \varphi_i \cdot \nabla \varphi_j \, d\mathbf{x}.\) (14.8)

困难在于将双线性形式应用于隐式定义的基函数，以及计算右端项上的积分 \((f, \varphi_i)_{L_2(P)}\)。边界积分 \((g_N, \varphi_i)_{L_2(\Gamma_N)}\) 的计算比较直接，因为基函数 \(\varphi_i\) 在边上是显式已知的。因此，这些积分通过在 \(\Gamma_N\) 上的每条边进行数值求积来处理。

为了计算 (14.8) 中的积分，我们区分三种情况，并在每个单元 \(P \in \mathcal{T}_h\) 上局部应用 Green 第一恒等式。详细内容留给读者。如果 \(\varphi_i|_P\) 和 \(\varphi_j|_P\) 对应谐波基函数 \(\phi_i\) 和 \(\phi_j\)，则得到

\(\int_P \nabla \phi_i \cdot \nabla \phi_j \, d\mathbf{x} = \int_{\partial P} \frac{\partial \phi_i}{\partial \mathbf{n}_P} \phi_j \, d\mathbf{s}_{\mathbf{x}}.\) (14.9)

如果 \(\varphi_i|_P\) 和 \(\varphi_j|_P\) 对应单元气泡函数 \(\phi_{i,j}\) 和 \(\phi_{i',j'}\)，则可以利用 (14.6) 得到

\(\int_P \nabla \phi_{i,j} \cdot \nabla \phi_{i',j'} \, d\mathbf{x} = \int_{\partial P} \frac{\partial \phi_{i,j}}{\partial \mathbf{n}_P} \phi_{i',j'} \, d\mathbf{s}_{\mathbf{x}} - \sum_{\ell=1}^n \alpha_\ell \int_{\partial P} \frac{\partial \phi_{i,j}}{\partial \mathbf{n}_P} \phi_{i',j'} \, d\mathbf{s}_{\mathbf{x}} + \int_P p_{i,j} \phi_{i',j'} \, d\mathbf{x}.\)

如果 \(\varphi_i|_P\) 对应谐波基函数，而 \(\varphi_j|_P\) 对应单元气泡函数，则得到 \(\int_P \nabla \varphi_i \cdot \nabla \varphi_j \, d\mathbf{x} = 0\)。因此，在 FE 计算中，线性方程组解耦。此外，除了未知项 \(\partial \phi_i / \partial \mathbf{n}_P\) 外，其余均为（分段）多项式，因此上述公式中的第一个和第三个积分可以解析计算。对 \(\partial \phi_i / \partial \mathbf{n}_P\) 的近似将在下一小节中讨论。

对于 \((f, \phi_i)_{L_2(\Omega)}\) 的计算，我们如同 (14.8) 那样进行。然后，我们通过对多边形单元进行数值求积来近似局部积分 \(\int_P f \phi_i \, d\mathbf{x}\)。具体做法是将多边形划分为三角形，并在其上应用标准求积规则，参见 [378]。或者，也可以直接在多边形上应用求积规则，例如参见 [102]。如果 \(\varphi_i|_P\) 对应谐波基函数 \(\phi_i\)，则我们使用表示公式

\(\phi_i(\mathbf{x}) = -\frac{1}{2\pi} \int_{\partial P} \ln|\mathbf{x}-\mathbf{y}| \frac{\partial \phi_i(\mathbf{y})}{\partial \mathbf{n}_P} \, d\mathbf{s}_{\mathbf{y}} - \frac{1}{2\pi} \int_{\partial P} \frac{\mathbf{n}_P \cdot (\mathbf{x}-\mathbf{y})}{|\mathbf{x}-\mathbf{y}|^2} \phi_i(\mathbf{y}) \, d\mathbf{s}_{\mathbf{y}}\) (14.10)

其中 \(\mathbf{x} \in P\)，参见下文。如果 \(\varphi_i|_P\) 对应单元气泡函数，则我们应用 (14.6)。我们再次强调，了解 \(\partial \phi_i / \partial \mathbf{n}_P\) 非常重要。

### 14.2.3 边界元方法简介

表示公式 (14.10) 对边界元方法至关重要，边界元方法用于近似边界积分公式。为了在数学上严谨，参见 [367]，我们记 \(\gamma_0 : H^1(P) \to H^{1/2}(\partial P)\) 为通常的迹算子，对连续函数满足 \(\gamma_0 v = v|_{\partial P}\)。此外，令 \(\gamma_1 v \in H^{-1/2}(\partial P)\) 为函数 \(v \in H^1(\Omega)\)（其中 \(\Delta v\) 属于 \(H^1(\Omega)\) 的对偶空间）的共法线导数，也称为 Neumann 迹。Neumann 迹 \(\gamma_1 v\) 由 Green 恒等式定义

\(\int_P \nabla v \cdot \nabla w \, dx = \int_{\partial P} \gamma_1 v \, \gamma_0 w \, ds_x - \int_P w \Delta v \, dx\)

其中 \(w \in H^1(P)\)，且对于足够正规的函数，它与 \(\partial v / \partial n_P\) 重合。因此，我们对谐波函数 \(v\) 在 \(P\) 内用边界积分算子表示 (14.10) 为 \(v = \tilde{\mathcal{V}}(\gamma_1 v) - \mathcal{W}(\gamma_0 v)\)。将迹算子 \(\gamma_0\) 和 \(\gamma_1\) 应用于表示公式，得到 Calderon 投影算子

\(\begin{pmatrix} \gamma_0 v \\ \gamma_1 v \end{pmatrix} = \begin{pmatrix} \frac{1}{2}\mathcal{I} - \mathcal{K} & \mathcal{V} \\ \mathcal{D} & \frac{1}{2}\mathcal{I} + \mathcal{K}' \end{pmatrix} \begin{pmatrix} \gamma_0 v \\ \gamma_1 v \end{pmatrix}, \quad (14.11)\)

其中 \(\mathcal{I}\) 为单位算子。单层势、双层势、伴随双层势以及超奇异积分算子具有如下映射性质

\(\mathcal{V}: H^{-1/2}(\partial P) \to H^{1/2}(\partial P), \quad \mathcal{K}: H^{1/2}(\partial P) \to H^{1/2}(\partial P),\)
\(\mathcal{K}': H^{-1/2}(\partial P) \to H^{-1/2}(\partial P), \quad \mathcal{D}: H^{1/2}(\partial P) \to H^{-1/2}(\partial P).\)

关于这些算子的详细研究，参见 [367]。(14.11) 中的第一个方程给出了边界积分方程 \(\mathcal{V}(\gamma_1 v) = (\frac{1}{2}\mathcal{I} + \mathcal{K})(\gamma_0 v)\)。因此，如果 \(\gamma_0 v\) 已知，Neumann 迹 \(t = \gamma_1 v\) 由以下 Galerkin 公式的解给出

\((\mathcal{V}t, \tau)_{L_2(\partial P)} = ((\frac{1}{2}\mathcal{I} + \mathcal{K})\gamma_0 v, \tau)_{L_2(\partial P)} \quad \forall \tau \in H^{-1/2}(\partial P).\)

该公式承认唯一解，因为已知当 \(h_P < 1\) 时 \(\mathcal{V}\) 可逆。为了获得 \(t \in H^{-1/2}(\partial P)\) 的近似，我们应用 BEM。我们用 \(\mathcal{P}^k_{pwd}(\partial P)\) 离散 \(H^{1/2}(\partial P)\)，并用 \(\mathcal{P}^{k-1}_{pwd}(\partial P)\) 离散 \(H^{-1/2}(\partial P)\)，其中

\(\mathcal{P}^k_{pwd}(\partial P) = \{ v \in L_2(\partial P) : v|_{[w_i, w_{i+1}]} \in \mathcal{P}^{k-1}([v_i, v_{i+1}]), i = 1, \dots, n \}\)

这是次数小于等于 \(k-1\) 且允许在 \(P\) 的顶点处不连续的分段多项式空间。令 \(\{\tau_i : i = 1, \dots, kn\}\) 为 \(\mathcal{P}^{k-1}_{pwd}(\partial P)\) 的一组基函数，其构造方式与 \(\{\lambda_i : i = 1, \dots, kn\}\) 类似。对于多项式数据 \(\gamma_0 v = \sum_{i=1}^{kn} v_i \lambda_i \in \mathcal{P}^k_{pwd}(\partial P)\)，采用试解 \(t = \sum_{i=1}^{kn} t_i \tau_i \in \mathcal{P}^{k-1}_{pwd}(\partial P)\)，得到线性方程组

\(\mathcal{V}t = (\frac{1}{2}\mathcal{M} + \mathcal{K})v, \quad (14.12)\)

其中 \(t = (t_1, \dots, t_{kn})\) 和 \(v = (v_1, \dots, v_{kn})\)，且

\(\mathcal{V} = ((\langle \mathcal{V}\tau_j, \tau_i \rangle_{L_2(\partial P)})_{i,j=1}^{kn}, \quad \mathcal{M} = ((\lambda_j, \tau_i)_{L_2(\partial P)})_{i,j=1}^{kn},\)
\(\mathcal{K} = ((\mathcal{K}\lambda_j, \tau_i)_{L_2(\partial P)})_{i,j=1}^{kn}, \quad \mathcal{D} = ((\mathcal{D}\lambda_j, \lambda_i)_{L_2(\partial P)})_{i,j=1}^{kn}.\)

如果我们类似地对 (14.11) 中的第二个方程应用 Galerkin 公式，并在右端项中将 \(\gamma_1 v\) 替换为 \(t_h\)，则得到矩阵

\(\mathcal{S} = \mathcal{D} + (\frac{1}{2}\mathcal{M}^\top + \mathcal{K}^\top)\mathcal{V}^{-1}(\frac{1}{2}\mathcal{M} + \mathcal{K}).\)

由于 \(\gamma_0 \phi_i = \lambda_i\)，矩阵项是以下量的良好近似

\(\mathcal{S} \approx ((\gamma_1 \phi_j, \gamma_0 \phi_i)_{L_2(\partial P)})_{i,j=1}^{kn}.\) (14.13)

矩阵 \(\mathcal{V}\)、\(\mathcal{K}\) 和 \(\mathcal{D}\) 的项是在 \(\partial P\) 上的二重积分。内层积分对应边界积分算子对基函数的作用，可以以封闭形式计算。外层积分对应 \(L_2\)-内积，通过数值求积近似。

在此我们强调，在上述描述中，边界元方法直接应用于多边形单元 \(P\) 天然给定的离散化上。例如，如果我们有一个五边形且关注 \(k=1\)，则 Dirichlet 迹在 \(\partial P\) 上由五个自由度精确描述，而 Neumann 迹由每条边上的一个常数近似。一般来说，BEM 使用 \(\partial P\) 的更细离散化，但就我们的目的而言，最粗且天然给定的离散化已足够。

最后，我们建立与基于 BEM 的全局 FEM 的联系。如果将 (14.13) 与 (14.8) 和 (14.9) 进行比较，我们看到 \(\mathcal{S}\) 是有限元公式中局部刚度矩阵的良好近似。此外，通过 (14.12) 得到的 \(\gamma_1 v = \partial_\nu \phi\) 的近似 \(t_h\) 用于表示公式 (14.10) 中，以求多边形单元 \(P\) 内部的基函数 \(\phi_i\)。在基于 BEM 的 FEM 模拟中，所有边界元矩阵对每个单元仅设置一次，并用于所有基函数。由于每个单元的顶点数量有限且我们不对单元边界进行进一步离散化，局部 BEM 矩阵规模较小，\(\mathcal{V}\) 的逆可以使用 LAPACK 子程序高效计算。

### 14.2.4 数值示例

定理 14.1 的理论结果在一个模型问题上得到说明。基于 BEM 的 FEM 应用于一系列均匀细化的多边形网格。在每次细化步骤中，求解边值问题

\(-\Delta u = f \text{ in } \Omega = (0, 1)^2, \quad u = 0 \text{ on } \Gamma\)

求解，其中 \(f\) 被选取使得 \(u(\boldsymbol{x}) = \sin(\pi x) \sin(\pi y)\) 是唯一解。初始网格及一些细化网格如图 14.11 所示。逐次细化的网格通过如 [420] 所述划分每个多边形单元得到，另见下一节。Galerkin 误差 \(\|u - u_h\|_{H^\ell(\Omega)}\) 分别针对 \(H^\ell\)-范数（\(\ell = 1\)）和 \(L_2\)-范数（\(\ell = 0\)）进行计算。在图 14.2 中，相对误差以网格尺寸 \(h = \max\{h_P : P \in \mathcal{T}_h\}\) 为横坐标，在对数坐标下绘制。曲线的斜率反映了近似阶 \(k = 1, 2, 3\) 的理论收敛率。

