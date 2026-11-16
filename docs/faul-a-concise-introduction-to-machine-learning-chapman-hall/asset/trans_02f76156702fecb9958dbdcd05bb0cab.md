

结合这两点，我们可以写出

$$
\mathcal{L}(\boldsymbol{\alpha}) = -\frac{1}{2} \left( N \log(2\pi) + \log |\mathbf{C}_{-i}| + \mathbf{t}^T \mathbf{C}_{-i}^{-1} \mathbf{t} - \log \alpha_i \right. \\
\left. + \log(\alpha_i + \mathbf{d}_i^T \mathbf{C}_{-i}^{-1} \mathbf{d}_i) - \frac{\mathbf{t}^T \mathbf{C}_{-i}^{-1} \mathbf{d}_i \mathbf{d}_i^T \mathbf{C}_{-i}^{-1} \mathbf{t}}{\alpha_i + \mathbf{d}_i^T \mathbf{C}_{-i}^{-1} \mathbf{d}_i} \right) \\
= \mathcal{L}(\boldsymbol{\alpha}_{-i}) + \frac{1}{2} \left( \log \alpha_i - \log(\alpha_i + \mathbf{d}_i^T \mathbf{C}_{-i}^{-1} \mathbf{d}_i) + \frac{(\mathbf{d}_i^T \mathbf{C}_{-i}^{-1} \mathbf{t})^2}{\alpha_i + \mathbf{d}_i^T \mathbf{C}_{-i}^{-1} \mathbf{d}_i} \right) \\
= \mathcal{L}(\boldsymbol{\alpha}_{-i}) + \ell(\alpha_i).
$$

因此，我们已将对 $\alpha_i$ 的依赖分离到 $\ell(\alpha_i)$ 中，而 $\mathcal{L}(\boldsymbol{\alpha}_{-i})$ 包含与 $\alpha_i$ 无关的对数证据部分。

我们定义以下量

$$s_i = \mathbf{d}_i^T \mathbf{C}_{-i}^{-1} \mathbf{d}_i \quad \text{and} \quad q_i = \mathbf{d}_i^T \mathbf{C}_{-i}^{-1} \mathbf{t},$$

它们与 $\alpha_i$ 无关。根据此定义

$$\ell(\alpha_i) = \frac{1}{2} \left( \log \alpha_i - \log(\alpha_i + s_i) + \frac{q_i^2}{\alpha_i + s_i} \right).$$

对数证据对 $\alpha_i$ 的导数由以下给出

$$
\frac{\partial \mathcal{L}(\boldsymbol{\alpha})}{\partial \alpha_i} = \frac{\partial \ell(\alpha_i)}{\partial \alpha_i} = \frac{1}{2} \left( \frac{1}{\alpha_i} - \frac{1}{\alpha_i + s_i} - \frac{q_i^2}{(\alpha_i + s_i)^2} \right) \\
= \frac{1}{2} (\alpha_i + s_i)^{-2} \left( s_i - q_i^2 + \frac{s_i^2}{\alpha_i} \right), \quad (8.8)
$$

因为 $\mathcal{L}(\boldsymbol{\alpha}_{-i})$ 与 $\alpha_i$ 无关。

如果 $s_i - q_i^2$ 非负，则导数始终为正，因为 $\alpha_i$ 为正，且 $\ell(\alpha_i)$ 单调递增。另一方面，如果 $s_i - q_i^2$ 为负，则方程 (8.8) 在以下情况下为零

$$\alpha_i = \frac{s_i^2}{q_i^2 - s_i}, \quad (8.9)$$

其中 $\ell(\alpha_i)$ 取得最大值。图 8.10 说明了这两种情况。在第一种情况中设置 $\alpha_i = \infty$，并在第二种情况中将 $\alpha_i$ 调整为 (8.9) 给出的值，会增加边缘似然的对数。对于 $\alpha_i = \infty$，$\mathbf{c}_i$ 的概率密度函数在零处变得无限尖锐。在实践中，这意味着 $d_i(\mathbf{x})$ 被视为对解释数据没有贡献，因此可以从模型中排除。这在模型中引入了 *稀疏性*。

为了避免出现许多不同的矩阵 $\mathbf{C}_{-i}$，定义以下内容很方便

$$
Q_i = \mathbf{d}_i^T \mathbf{C}^{-1} \mathbf{t}, \\
S_i = \mathbf{d}_i^T \mathbf{C}^{-1} \mathbf{d}_i.
$$

对于无穷大的 $\alpha_i$，我们有 $q_i = Q_i$ 和 $s_i = S_i$，因为在这种情况下 $\mathbf{C} = \mathbf{C}_{-i}$。而对于有限的 $\alpha_i$，

```
$s_i = \mathbf{d}_i^T \mathbf{C}_{-i}^{-1} \mathbf{d}_i = \mathbf{d}_i^T (\mathbf{C} + \mathbf{d}_i(-\alpha_i)^{-1} \mathbf{d}_i^T)^{-1} \mathbf{d}_i$
$= \mathbf{d}_i^T [\mathbf{C}^{-1} - \mathbf{C}^{-1} \mathbf{d}_i (-\alpha_i + \mathbf{d}_i^T \mathbf{C}^{-1} \mathbf{d}_i)^{-1} \mathbf{d}_i^T \mathbf{C}^{-1}] \mathbf{d}_i$
$= S_i + \frac{S_i^2}{\alpha_i - S_i} = \frac{\alpha_i S_i}{\alpha_i - S_i}.$
```

同样地，

```
$q_i = \frac{\alpha_i Q_i}{\alpha_i - S_i}.$
```

让我们更仔细地检查 $Q_i$。矩阵 $\Sigma$ 和 $\mathbf{C}$ 通过附录 A.1.3 中的 Woodbury 矩阵恒等式相关，

```
$\mathbf{C}^{-1} = (\sigma^2 \mathbf{I} + \mathbf{D} \mathbf{A}^{-1} \mathbf{D}^T)^{-1}$
$= \sigma^{-2} \mathbf{I} - \sigma^{-2} \mathbf{D} (\mathbf{A} + \mathbf{D}^T \sigma^{-2} \mathbf{D})^{-1} \mathbf{D}^T \sigma^{-2}$
$= \sigma^{-2} (\mathbf{I} - \sigma^{-2} \mathbf{D} \Sigma \mathbf{D}^T).$
```

使用此公式和 (8.7)，

```
$\mathbf{C}^{-1} \mathbf{t} = \sigma^{-2} (\mathbf{t} - \mathbf{D} \mu).$
```

然而，$\mathbf{D}\mu$ 正是我们对 $\mathbf{t}$ 的预测概率分布的均值。因此，$\mathbf{C}^{-1} \mathbf{t}$ 给出了每个样本的目标与预测均值之差，按噪声方差缩放。如果这个值很小，我们的当前模型足以解释数据。如果不是，我们将 $\mathbf{C}^{-1} \mathbf{t}$ 视为需要移除的误差。计算 $Q_i = \mathbf{d}_i^T \mathbf{C}^{-1} \mathbf{t}$ 检查 $\mathbf{d}_i$ 与此误差的对齐程度。如果正交，则 $\mathbf{d}_i$ 无法帮助移除此误差。如果对齐良好，则将 $\mathbf{d}_i$ 包含在模型中将是有益的。因此 $Q_i$ 被称为 *质量因子*。

另一方面，$S_i$ 被称为稀疏因子，因为，如下文所示，它有助于评估 $\mathbf{d}_i$ 与其他基函数的共线性程度。量 $s_i$ 是与基函数 $d_i$ 相关的惩罚项。它量化了 $d_i$ 能被其他基函数建模的程度。另一方面，$q_i$ 是一个质量项，衡量在当前模型下 $d_i$ 对解释数据的贡献程度。$s_i$ 和 $q_i$ 都依赖于 $\mathbf{C}_{-i}$，而 $\mathbf{C}_{-i}$ 又依赖于 $\alpha_{-i}$。因此，随着其他超参数 $\alpha_{-i}$ 的调整，$\alpha_i$ 的最优值会发生变化。

能够逐个优化超参数的可能性催生了以下算法。它用单个基函数及其最优超参数值初始化模型，并将其他超参数显著设置为无穷大。在算法开始时，当模型中只有一个基函数时，$\mathbf{D}$ 只有一列，$\Sigma$ 是一个 $1 \times 1$ 矩阵。$\mathbf{C}$ 是 $\sigma^2 \mathbf{I}$ 加上该单个基函数在样本点处与自身的外积。其逆矩阵可以使用附录 A.1.4 中的 Sherman-Morrison 公式轻松计算。然后找到基函数 $d_i(\mathbf{x})$，其中

![](img/d3c00252180686426c9e63ab889b535b_267_0.png)

将其超参数 \(\alpha_i\) 设置为最优值（给定当前模型）可使边缘似然获得最大增加，并相应更新模型。

当无法再实现边缘似然对数的显著增加时，算法收敛。由于 \(\alpha_i\) 的最优值可以是有限或无穷大，因此有三种可能的更新。如果 \(d_i(\mathbf{x})\) 不在模型中且最优 \(\alpha_i\) 是有限的，则将其添加到模型中。如果 \(d_i(\mathbf{x})\) 在模型中且最优 \(\alpha_i\) 是无穷大的，则将其从模型中删除。第三种情况是 \(d_i(\mathbf{x})\) 在模型中且最优 \(\alpha_i\) 是有限的，在这种情况下，\(\alpha_i\) 更新为此值。请注意，当最优 \(\alpha_i\) 是无穷大且 \(d_i(\mathbf{x})\) 已从模型中排除时，无需采取任何操作。在所有三种情况下，\(\mathbf{\Sigma}\) 和 \(\mu\) 都必须更新，因为 \(A\) 已更改。

矩阵 $\mathbf{D}$ 和 $\mathbf{\Sigma}$ 在算法运行期间大小会发生变化。然而，与字典中基函数的数量 $M$ 和样本数量 $N$ 相比，它们仍然相对较小。矩阵 $\mathbf{C}$ 在添加、删除基函数或重新估计其超参数时会发生秩 1 更新。这些秩 1 更新是基函数在样本点处与自身的外积的加法或减法，系数由超参数更新推导得出。然而，在实践中，$\mathbf{C}$ 及其逆矩阵并不被计算。

这里应当注意，候选基函数的字典不需要是静态的。新的候选基函数可以在任何时间点创建、评估，并可能添加到模型中。

在下面的更新公式中，边缘似然对数的变化用 \(\Delta \mathcal{L}\) 表示，更新后的量用波浪号表示（例如 \(\tilde{\mu}\)）：

