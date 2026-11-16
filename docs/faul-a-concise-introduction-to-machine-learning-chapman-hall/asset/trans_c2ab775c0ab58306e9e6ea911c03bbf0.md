

![](img/d3c00252180686426c9e63ab889b535b_257_0.png)

![](img/d3c00252180686426c9e63ab889b535b_257_1.png)

![](img/d3c00252180686426c9e63ab889b535b_257_2.png)

![](img/d3c00252180686426c9e63ab889b535b_257_3.png)

图 8.9: 各种 \( L_p \) 范数的等高线。

对于 \( L_2 \) 正则化，我们最小化

```
\(\frac{1}{2}\|\mathbf{t} - \mathbf{Dc}\|^2 + \frac{1}{2}\lambda\|\mathbf{c}\|^2 = \frac{1}{2}\mathbf{t}^T\mathbf{t} - \mathbf{c}^T\mathbf{D}^T\mathbf{t} + \frac{1}{2}\mathbf{c}^T(\mathbf{D}^T\mathbf{D} + \lambda\mathbf{I})\mathbf{c}.\)
```

该函数的梯度为

```
\(-\mathbf{D}^T\mathbf{t} + (\mathbf{D}^T\mathbf{D} + \lambda\mathbf{I})\mathbf{c}.\)
```

将梯度设为零，我们得到最小值

```
\(\mathbf{c} = (\mathbf{D}^T\mathbf{D} + \lambda\mathbf{I})^{-1}\mathbf{D}^T\mathbf{t},\) (8.3)
```

由于矩阵 \(\mathbf{D}^T\mathbf{D} + \lambda\mathbf{I}\) 是正定的。如果 \(\mathbf{D}^T\mathbf{D}\) 接近奇异，在每个对角线项上添加 \(\lambda\) 将使其远离奇异性。因此，岭回归稳定了普通最小二乘法。

考虑正交归一基函数的情况（\(\mathbf{D}^T\mathbf{D} = \mathbf{I}\)）很有趣。此时，\( L_2 \) 正则化将普通最小二乘解的每个分量乘以因子 \((1+\lambda)^{-1}\) 进行缩减。另一方面，\( L_1 \) 正则化将每个分量向零移动 \(\lambda\)。如果分量比 \(\lambda\) 更接近零，则将其设为零。弹性网正则化结合了这两种效果。

岭回归在 MATLAB 中实现为 `ridge`，而 LASSO 实现为 `lasso`。后者还包含弹性网正则化，因为当 $\lambda = 1$ 时，弹性网变为 LASSO。

更一般地，$L_p$ 范数定义为

$$\|c\|_p = \left( \sum_{m=1}^M |c_m|^p \right)^{1/p}.$$

图 8.9 显示了不同 \( p \) 选择的等高线。\( L_2 \) 正则化不偏好任何轴，而对于减小的 \( p < 2 \)，\( L_p \) 正则化偏好更靠近轴的点。在极限情况下，\( L_0 \) 范数将解捕捉到轴上。这使得轴选择的重要性更加明显。理想情况下，应选择与主成分对齐的轴。这也使算法更加稳定。

## 8.11 贝叶斯回归

我们已经看到，通过最小化 \(\|\mathbf{t} - \mathbf{Dc}\|^2 = \|\epsilon\|^2\) 来寻找满足 \(\mathbf{t} = \mathbf{Dc} + \boldsymbol{\epsilon}\) 的合适系数 \(\mathbf{c}\)，会导致噪声被建模并产生过拟合。通过最小化 \(\|\mathbf{t} - \mathbf{Dc}\|^2 + \Omega(\mathbf{c})\)（其中 \(\Omega(\mathbf{c})\) 为某个惩罚函数）可以缓解这一问题。这会“微调”模型以偏好较不复杂的模型。我们现在要问的问题是，这种“微调”是否可以形式化。

为此，我们使用 *贝叶斯规则*，回顾如下

$P(A|B) = \frac{P(B|A)P(A)}{P(B)}$.

通常，该关系表示为 $P(A|B) \propto P(B|A)P(A)$，其中 \(\propto\) 表示两边成正比。因此，除以 \(P(B)\) 被省略。

将此应用于当前场景，

$p(\mathbf{c}|\mathbf{t}) = \frac{p(\mathbf{t}|\mathbf{c})p(\mathbf{c})}{p(\mathbf{t})}$.

换句话说，我们回答了这个问题：给定观测数据，系数的概率是多少？

由于噪声是 i.i.d. 正态分布，均值为 0，方差为 \(\sigma^2\)，给定设计矩阵 \(\mathbf{D}\)、系数 \(\mathbf{c}\) 和噪声方差 \(\sigma^2\)，\(\mathbf{t}\) 的概率可以写为

$p(\mathbf{t}|\mathbf{D}, \mathbf{c}, \sigma^2) = (2\pi)^{-N/2}\sigma^{-N} \exp \left( - \frac{\|\mathbf{t} - \mathbf{Dc}\|^2}{2\sigma^2} \right)$.

我们使用除数据本身之外的所有信息为 \(\mathbf{c}\) 定义一个 *先验分布*，量化我们对系数的信念。例如，一个简单的假设是每个系数 *先验* 服从均值为零、方差为 \(\alpha^{-1}\) 的正态分布。\(\mathbf{c}\) 的多元分布由以下给出

\(p(\mathbf{c}|\alpha) = \left(\frac{\alpha}{2\pi}\right)^{M/2} \exp\left(-\frac{\alpha}{2}\mathbf{c}^T\mathbf{c}\right).\)

在没有任何其他知识的情况下，这是一种可能的假设。\(\alpha\) 是一个超参数，被称为分布的精度。如果 \(\alpha\) 变得非常大，分布在其均值处变得尖锐，我们对该值的信心比 \(\alpha\) 很小且分布宽度很大时更大。

在观察到因变量 \(\mathbf{t}\) 的 \(N\) 个样本后，系数 \(\mathbf{c}\) 的 *后验分布* 由以下给出

\(p(\mathbf{c}|\mathbf{t}, \mathbf{D}, \alpha, \sigma^2) \propto p(\mathbf{t}|\mathbf{D}, \mathbf{c}, \sigma^2)p(\mathbf{c}|\alpha).\)

可以通过选择使后验分布或等价地其对数最大的 \(\mathbf{c}\) 来获得 \(\mathbf{c}\) 的估计，

\(\log p(\mathbf{c}|\mathbf{t}, \mathbf{D}, \alpha, \sigma^2) \propto \log p(\mathbf{t}|\mathbf{D}, \mathbf{c}, \sigma^2) + \log p(\mathbf{c}|\alpha).\)

第一项正是对数似然（8.1），当 \(\|\mathbf{t} - \mathbf{D}\mathbf{c}\|^2\) 最小时取得最大值。第二项 \(-\frac{\alpha}{2}\|\mathbf{c}\|^2 + \text{常数}\)，可以视为惩罚项的负值。事实上，对后验分布取负对数然后最小化而非最大化，重新得出了岭回归。

更一般地，设 \(\boldsymbol{\alpha}\) 包含控制联合分布 \(p(\mathbf{t}, \mathbf{c}|\mathbf{D}, \boldsymbol{\alpha}, \sigma^2)\) 的所有参数。通过对系数 \(\mathbf{c}\) 进行积分来消除对隐变量的依赖，从而对所有可能的解进行平均。这称为对 \(\mathbf{c}\) 进行 *边缘化*，其结果是 *边缘似然*

\(\mathcal{L}(\mathbf{t}|\mathbf{D}, \boldsymbol{\alpha}, \sigma^2) = \int p(\mathbf{t}, \mathbf{c}|\boldsymbol{\alpha}, \sigma^2) d\mathbf{c},\)

我们的目标是最大化它。\(\boldsymbol{\alpha}\) 的最大似然估计（*MLE*）是使 \(\mathcal{L}(\mathbf{t}|\mathbf{D}, \boldsymbol{\alpha}, \sigma^2)\) 最大化的值。在下一节中，我们将介绍一种寻找最大值的技术。

## 8.12 期望-*最大化*

在以下内容中，我们省略模型对设计矩阵 \(\mathbf{D}\) 的依赖。期望-*最大化*（*EM*）算法通过在两个步骤之间交替，迭代地达到最大值。推导需要一些展开。

根据链式法则，也称为 *乘法规则*，我们有

\(p(\mathbf{t}, \mathbf{c}|\boldsymbol{\alpha}, \sigma^2) = p(\mathbf{c}|\mathbf{t}, \boldsymbol{\alpha}, \sigma^2)p(\mathbf{t}|\boldsymbol{\alpha}, \sigma^2).\)

对两边取对数，得到

```
\log p(\mathbf{t}, \mathbf{c} | \boldsymbol{\alpha}, \sigma^2) = \log p(\mathbf{c}|\mathbf{t}, \boldsymbol{\alpha}, \sigma^2) + \log p(\mathbf{t}|\boldsymbol{\alpha}, \sigma^2).
```

两边都可以看作随机变量 c 的函数，因此我们可以对任何分布 q(c) 取期望。

```
\int q(\mathbf{c}) \log p(\mathbf{t}, \mathbf{c} | \boldsymbol{\alpha}, \sigma^2) d\mathbf{c} = \int q(\mathbf{c}) \log p(\mathbf{c} | \mathbf{t}, \boldsymbol{\alpha}, \sigma^2) d\mathbf{c}
+ \int q(\mathbf{c}) \log p(\mathbf{t} | \boldsymbol{\alpha}, \sigma^2) d\mathbf{c}
= \int q(\mathbf{c}) \log p(\mathbf{c}|\mathbf{t}, \boldsymbol{\alpha}, \sigma^2) + \log p(\mathbf{t}|\boldsymbol{\alpha}, \sigma^2),
```

由于 \(\int q(\mathbf{c}) d\mathbf{c} = 1\)。整理得到

```
\log p(\mathbf{t}|\boldsymbol{\alpha}, \sigma^2) = \log \mathcal{L}(\mathbf{t}|\boldsymbol{\alpha}, \sigma^2) = \int q(\mathbf{c}) \log p(\mathbf{t}, \mathbf{c} | \boldsymbol{\alpha}, \sigma^2) d\mathbf{c}
- \int q(\mathbf{c}) \log p(\mathbf{c} | \mathbf{t}, \boldsymbol{\alpha}, \sigma^2) d\mathbf{c}.
```

我们可以在右边减去并加上项 \(\int q(\mathbf{c}) \log q(\mathbf{c}) d\mathbf{c}\)，从而得到

```
\log \mathcal{L}(\mathbf{t}|\boldsymbol{\alpha}, \sigma^2) = \int q(\mathbf{c}) \log \frac{p(\mathbf{t}, \mathbf{c} | \boldsymbol{\alpha}, \sigma^2)}{q(\mathbf{c})} d\mathbf{c} - \int q(\mathbf{c}) \log \frac{p(\mathbf{c} | \mathbf{t}, \boldsymbol{\alpha}, \sigma^2)}{q(\mathbf{c})} d\mathbf{c} \quad (8.4)
```

利用对数的性质。\(\log \mathcal{L}(\mathbf{t}|\boldsymbol{\alpha}, \sigma^2)\) 也称为对数证据。

第二项（包括负号）是分布 q(c) 与后验分布 p(c|t, alpha, sigma^2) 之间的库尔贝克-莱布勒散度（KL 散度）。它也被称为歧视信息、信息散度和信息增益，因为通过观察 t 获得了信息。对于两个概率密度函数 p 和 q，库尔贝克-莱布勒散度定义为

```
D_{KL}(p||q) = - \int p(x) \log \frac{q(x)}{p(x)} dx = \mathbb{E}_p \left[ - \log \frac{q(x)}{p(x)} \right],
```

其中 \(\mathbb{E}_p\) 表示相对于分布 p 的期望。使用 Jensen 不等式，

```
D_{KL}(p||q) \ge - \log \mathbb{E}_p \left[ \frac{q(x)}{p(x)} \right] = - \log \int p(x) \frac{q(x)}{p(x)} dx = - \log \int q(x) dx = 0,
```

由于 \(\log 1 = 0\)（有关证明的更多细节，例如参见 [3]）。因此，库尔贝克-莱布勒散度始终为正，并且当且仅当 \(p(\mathbf{c}|\mathbf{t}, \boldsymbol{\alpha}, \sigma^2) = q(\mathbf{c})\) 几乎处处相等时为零。

