
我们得到 $\mathbf{D} = 2 \mathbf{J}^T \mathbf{g}$ 和 $\mathbf{H}^{\circ} = 2 \mathbf{J}^T \mathbf{J}$。因此，$\mathbf{h}$ 是以下方程的解：

$$\mathbf{J}^T \mathbf{J} \mathbf{h} = -\mathbf{J}^T \mathbf{g} \quad (4.12)$$

该方程对应于超定线性方程组

$$\mathbf{J} \mathbf{h} \approx -\mathbf{g} \quad (4.13)$$

这是线性代数中的经典最小二乘问题，参见第 1.7 节。其（最小范数）解为

$$\mathbf{h} = -\mathbf{J}^{-} \mathbf{g} = - (\mathbf{J}^T \mathbf{J})^{-} \mathbf{J}^T \mathbf{g} = -(\mathbf{H}^{\circ})^{-} \mathbf{D} \quad (4.14)$$

其中 $(\cdot)^{ - }$ 表示 Moore-Penrose 伪逆。无论 $\mathbf{H}^{\circ}$ 是否奇异，此公式都适用。

备注。可以通过另一种方式得出 (4.12)。由于我们的目标是最小化 $\mathcal{L} = \|\mathbf{g}\|^2$，可以用其线性近似 $\mathbf{g}(\mathbf{a}) + \mathbf{J}\mathbf{h}$ 替代 $\mathbf{g}(\mathbf{a}+\mathbf{h})$，并对 $\mathbf{h}$ 最小化 $\|\mathbf{g}(\mathbf{a}) + \mathbf{J}\mathbf{h}\|^2$；这正是经典最小二乘问题 (4.13)，其解由 (4.14) 给出。

备注。“正规方程”组

$$\mathbf{J}^{T} \mathbf{J} \mathbf{h} = -\mathbf{J}^{T} \mathbf{g}$$

可以通过几种方式在数值上求解。矩阵 $\mathbf{J}^{T} \mathbf{J}$ 的简单求逆或高斯消元法并不推荐，因为它们没有利用 $\mathbf{J}^{T} \mathbf{J}$ 的半正定性，且容易产生较大的舍入误差。一种更好的方法是对 $\mathbf{J}^{T} \mathbf{J}$ 进行 Cholesky 分解，它相当快速且精确。其缺点是在...

## 4.3 Levenberg-Marquardt 校正

高斯-牛顿法在有利条件下表现良好，此时其收敛速度快，但如上所述，它仍可能越过 $\mathcal{G}$ 取小值的区域；此外，如果设计矩阵 $\mathbf{N}=\mathbf{J}^{T}\mathbf{J}$ 恰好接近奇异，其性能可能会出问题。

### 扩展设计矩阵

Levenberg-Marquardt 校正旨在消除这些缺陷。设计矩阵 **N** 被扩展为

$$ \mathbf{N}_{\lambda}=\mathbf{N}+\lambda\mathbf{I}, \quad (4.15) $$

其中 $\lambda>0$ 是额外的控制参数，$\mathbf{I}$ 是 $k \times k$ 单位矩阵。换句话说，$\mathbf{N}$ 的对角元素增加了 $\lambda$。然后，求解新的系统以代替 (4.12)：

$$ \mathbf{N}_{\lambda} \mathbf{h}=-\mathbf{J}^{T} \mathbf{g} \quad (4.16) $$

来确定 **h**。注意，当 $\lambda>0$ 时，矩阵 $\mathbf{N}_{\lambda}$ 总是正定的（而 $\mathbf{N}$ 仅保证是半正定的），实际上 $\mathbf{N}_{\lambda}$ 的所有特征值都 $\geq\lambda$。

### 检查点

计算出 **h** 后，算法通过一个检查点。如果新的近似值 $\mathbf{a}'=\mathbf{a}+\mathbf{h}$ 降低了 $\mathcal{G}$ 的值，即如果 $\mathscr{G}(\mathbf{a}') < \mathscr{G}(\mathbf{a})$，则接受该值，并在下一次迭代之前将 $\lambda$ 乘以某个因子 $\alpha$（抑制校正项 $\lambda\mathbf{I}$）。

否则，拒绝新值 $\mathbf{a}' = \mathbf{a} + \mathbf{h}$，将 $\lambda$ 乘以某个因子 $\beta$ 并增大，并再次求解扩展法方程 $\mathbf{N}_\lambda\mathbf{h} = -\mathbf{J}^T\mathbf{g}$。这些递归尝试持续进行，直到增量 $\mathbf{h}$ 导致 $\mathscr{G}$ 的值变小。这是必然发生的，因为当 $\lambda$ 很大时，该方法趋近于最速下降法。

### 优点

换句话说，当 $\lambda$ 增加时，重新计算的向量 $\mathbf{h}$ 不仅变得更小，而且发生旋转，更好地对齐负梯度向量 $-\nabla\mathscr{G}(\mathbf{a})$。当 $\lambda \rightarrow \infty$ 时，$\mathbf{h}$ 的长度趋近于零，其方向收敛于 $-\nabla\mathscr{G}(\mathbf{a})$ 的方向（图 4.1）。

我们看到，Levenberg-Marquardt 校正结合了两种经典思想：

- (a) 函数的二次近似，这在最小值附近表现良好，并带来快速（近乎二次）的收敛。
- (b) 最速下降方案，确保在困难情况下的可靠性。

由于该算法基于这两个原则之间的合理平衡，有时被称为 Marquardt 折衷方案。

### 实际问题

在许多实现中，参数 $\lambda$ 初始化为一个小值，例如 $10^{-3}$ 或 $10^{-4}$。$\alpha$ 和 $\beta$ 的常见选择是 $\alpha = 0.1$ 和 $\beta = 10$。

*备注。* 与上一节中的方程 (4.12) 一样，新系统 $\mathbf{N}_\lambda\mathbf{h} = -\mathbf{J}^T\mathbf{g}$ 可以用许多方式在数值上求解，包括 Cholesky 分解、QR 分解和 SVD。然而，使用 QR 和 SVD 需要一种技巧，因为系统 (4.16) 尚未处于正确形式（ yet ）。技巧是将 (4.16) 重写为

$$ \mathbf{J}_\lambda^T\mathbf{J}_\lambda\mathbf{h} = -\mathbf{J}_\lambda^T\mathbf{g}_0, \quad (4.17) $$

其中矩阵 $\mathbf{J}_\lambda$ 是通过在 $\mathbf{J}$ 的底部附加 $k \times k$ 标量矩阵 $\sqrt{\lambda}\mathbf{I}$ 获得的，向量 $\mathbf{g}_0$ 是通过在 $\mathbf{g}$ 后面扩展 $k$ 个零得到的：

$$ \mathbf{J}_\lambda = \left[ \begin{array}{c} \mathbf{J} \\ \sqrt{\lambda}\mathbf{I} \end{array} \right], \quad \mathbf{g}_0 = \left[ \begin{array}{c} \mathbf{g} \\ \mathbf{0} \end{array} \right]. $$

现在系统 (4.17) 等价于最小二乘问题

$$ \mathbf{J}_\lambda \mathbf{h} \approx -\mathbf{g}_0, $$

其解为 $\mathbf{h} = -\mathbf{J}_\lambda^-\mathbf{g}_0$，可以通过 QR 或 SVD 计算（如上一节末尾所述）。

### 历史

Levenberg-Marquardt 校正在二十世纪中叶引入：它由 Levenberg [122] 于 1944 年发明，并于 1963 年由 Marquardt [131] 重新发现并增强。它在 1970 年代得到普及；见例如 [71]。该方法及其称为*信任域*的变体（见下一节）在过去几十年的最小二乘应用文献中占据主导地位。

## 4.4 信任域

为了完成我们对一般最小化方案的综述，我们将描述信任域方法，该方法目前构成了最先进的技术。

### 动机

Levenberg-Marquardt 算法足够灵活，可以避免经典最小化方案的明显陷阱，并几乎保证收敛到目标函数的最小值。然而，其缺点是控制参数 $\lambda$ 只是一个抽象变量，其值与当前问题没有明显的关系。因此，很难正确初始化 $\lambda$。此外，Levenberg-Marquardt 关于更新 $\lambda$ 的简单规则（通过任意选择的因子 $\alpha$ 和 $\beta$）往往导致不稳定、非最优的性能。

Levenberg-Marquardt 方法的一个变体在 1970 年代开发出来，解决了上述缺陷。Moré 在其撰写精良的 1978 年论文 [133] 中普及了该方法。最终，这种方法被称为*信任域*，并被几乎所有标准软件包采用，如 `MATLAB` 优化工具箱、`MINPACK` [134]、`ODRPACK` [22, 23] 等。我们在此描述其主要思想，更多技术细节请参阅 [133]。

### Levenberg-Marquardt 的几何描述

Levenberg-Marquardt 方法可以几何解释如下。回想高斯-牛顿法的一次迭代包括最小化二次函数

$$ \mathcal{L}(\mathbf{a}+\mathbf{h}) = \| \mathbf{g}(\mathbf{a}) + \mathbf{J}\mathbf{h} \|^2, $$

该函数在当前 [a] 的邻域内近似给定的函数 $\mathcal{G}(\mathbf{a}+\mathbf{h})$

迭代 **a**。图 4.1 展示了二维情况下 $\mathscr{L}(\mathbf{a}+\mathbf{h})$ 的等高线图（等值线集合）；这些等值线是同心椭圆。

![](img/86db288e3c266985d1648282179ae4b5_110_0.png)

图 4.1 $\mathscr{L}(\mathbf{a}+\mathbf{h})$ 的等值线是同心椭圆（实线椭圆），信赖域边界是以 **a** 为中心的虚线圆。

“纯”高斯-牛顿步（即当 $\lambda = 0$ 时）落在 $\mathscr{L}(\mathbf{a}+\mathbf{h})$ 的最小值处，即椭圆的中心 $\mathbf{b}_0$。当 $\lambda > 0$ 时，Levenberg-Marquardt 步（(4.16) 的解）落在另一个点 $\mathbf{b}_{\lambda} = \mathbf{a} + \mathbf{h}$，该点更接近 **a**。根据 (4.16)，在该点我们有：

$$\mathrm{grad}\ \mathscr{L}(\mathbf{a} + \mathbf{h}) = -\lambda\mathbf{h}.$$

相应地，向量 $\mathbf{h} = \mathbf{b}_{\lambda} - \mathbf{a}$ 正交于穿过 $\mathbf{b}_{\lambda}$ 的 $\mathscr{L}(\mathbf{a}+\mathbf{h})$ 等值线。这意味着 $\mathbf{b}_{\lambda}$ 提供了函数 $\mathscr{L}(\mathbf{a}+\mathbf{h})$ 在球 $\mathbb{B}(\mathbf{a},\Delta)$ 上的*受限*最小值，该球的中心为 **a**，半径为 $\Delta = \|\mathbf{h}\|$。换句话说，当 $\lambda > 0$ 时，Levenberg-Marquardt 步将二次近似 $\mathscr{L}(\mathbf{a}+\mathbf{h})$ 限制在以当前近似值 **a** 为圆心、半径 $\Delta$ 由 $\lambda$ 决定的某个球域内进行最小化。

随着 $\lambda > 0$ 增大，点 $\mathbf{b}_{\lambda}$ 逐渐靠近 **a**，且 $\Delta$ 减小。与此同时，向量 $\mathbf{h} = \mathbf{b}_{\lambda} - \mathbf{a}$ 发生旋转，并与等值线形成更大的夹角。在极限情况下 $\lambda \rightarrow \infty$，球 $\mathbb{B}(\mathbf{a},\Delta)$ 收缩为点 **a**，即 $\Delta \rightarrow 0$，向量 $\mathbf{h}$ 最终与最速下降方向对齐。

#### 替换控制参数

因此，$\lambda > 0$ 与 $\Delta \in (0, \|\mathbf{b}_0 - \mathbf{a}\|]$ 之间存在一一对应关系，因此可以使用 $\Delta$ 代替 $\lambda$ 作为控制参数，即从一次迭代调整到下一次迭代。由于 $\Delta$ 具有明确的含义（下文将进一步解释），其初始化以及在每次迭代中的更新可以比 Levenberg-Marquardt 方案中处理 $\lambda$ 的方式更加合理。

处理 $\Delta$ 的一个好处是可以直接控制参数空间中二次近似 $\mathscr{L}(\mathbf{a}+\mathbf{h})$ 被最小化的区域。这被称为*信赖域*，其背后的思想是在近似可以被*信赖*的地方最小化近似 $\mathscr{L}(\mathbf{a}+\mathbf{h})$，而不进入近似被认为不可靠的过远区域。

- 1. 初始化 $\mathbf{a}_0$ 和 $\Delta_0$，设置 $k=0$。
- 2. 在当前点 $\mathbf{a}_k$ 处计算向量 $\mathbf{g}_k$ 及其梯度 $\mathbf{J}_k$。
- 3. 对于当前的 $\mathbf{a}_k$ 和 $\Delta_k$，确定 $\lambda_k$。
- 4. 通过求解方程 $(\mathbf{J}_k^T \mathbf{J}_k + \lambda_k \mathbf{I})\mathbf{h}_k = -\mathbf{J}_k^T \mathbf{g}_k$ 来计算 $\mathbf{h}_k$。
- 5. 找到比值 $r_k = \mathrm{Ared}_k/\mathrm{Pred}_k$。
- 6. 如果 $r_k < 0$，重置 $\Delta_k := \frac{1}{2}\Delta_k$ 并返回步骤 3。
- 7. 如果 $r_k < 0.25$，更新 $\Delta_{k+1} = \frac{1}{2}\Delta_k$；如果 $r > 0.75$，更新 $\Delta_{k+1} = 2\Delta_k$。
- 8. 更新 $\mathbf{a}_{k+1} = \mathbf{a}_k + \mathbf{h}_k$，增加 $k$，并返回步骤 2。

表 4.2：信赖域算法。

#### 新的更新规则

这种对 $\Delta$ 的解释还引出了以下更新策略。在计算了步长 $\mathbf{h}$ 之后，我们找到目标函数的*实际减少量*（$\mathrm{Ared}$）与*预测减少量*（$\mathrm{Pred}$）的比值：

$$r = \frac{\mathrm{Ared}}{\mathrm{Pred}} = \frac{\mathscr{G}(\mathbf{a}) - \mathscr{G}(\mathbf{a}+\mathbf{h})}{\mathscr{G}(\mathbf{a}) - \mathscr{Q}(\mathbf{a}+\mathbf{h})}$$

应注意，$\mathscr{G}(\mathbf{a}) = \mathscr{Q}(\mathbf{a})$，因此分母始终为正，但仅当发生实际减少时分子才为正，在这种情况下我们当然应该接受步长 $\mathbf{h}$。

然而，我们根据 $r$ 的值来调整 $\Delta$。一种常见的策略如下。如果 $r < 0.25$，则二次近似被认为不太可靠（尽管目标函数有实际减少），我们在下一次迭代之前*减小*尺寸 $\Delta$（例如通过 $\Delta := \Delta/2$）。只有当 $r > 0.75$ 时，近似被认为足够准确，我们才*增加* $\Delta$（通过 $\Delta := 2\Delta$）。在中间情况 $0.25 \le r \le 0.75$ 中，我们保持 $\Delta$ *不变*。注意，这些规则与前一节中更新 $\lambda$ 的简单规则大不相同（在某种意义上，更为保守）！

#### 子问题

我们在表 4.2 中总结了信赖域方案的主要步骤。细心的读者应该注意到，我们尚未指定步骤 3。这被称为*信赖域子问题*：给定当前近似值 $\mathbf{a}$ 周围信赖域的尺寸 $\Delta > 0$，确定对应的参数 $\lambda \ge 0$。文献中有此类问题的多种解法，包括基于牛顿的方法 [70, 135]、狗腿法 [148, 149]、共轭梯度法 [172] 和二次型方法 [26]。我们发现，对于我们将圆拟合应用于数据这一特定场景，Moré [133] 描述的早期带括号法的基于牛顿的算法效果最好。

关于用于圆拟合的信赖域算法的 MATLAB 实现可以在我们的网页 [84] 上找到。

## 4.5 圆的 Levenberg-Marquardt 方法：完整版

将圆拟合到观测点涉及最小化以下函数：

$$\mathscr{F}\left( a,b,R\right) =\sum_{i=1}^{n}\left[ \sqrt{\left( x_{i}-a\right) ^{2}+\left( y_{i}-b\right) ^{2}}-R\right] ^{2}. \tag{4.18}$$

这是一个相对简单的表达式，因此 Levenberg-Marquardt 过程顺利进行。让我们引入简写符号：
