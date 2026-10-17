
在线性回归模型中，拟合优度通常通过残差和来衡量。嵌套模型是通过从较大的（全模型）中选取预测变量的子集获得的。可以使用残差和对简化模型与全模型进行比较，并利用全模型和简化模型的残差和构建 F 检验。在 GLM 中，残差和并不总是有意义的，特别是响应变量是离散的时。因此，需要其他方法来检查拟合优度。通过计算被称为离度（Deviance）的统计量，该量最初由 `Nelder` 和 `Wedderburn` (1971) 提出。对于任何一组极端模型：即最小模型和饱和模型。最小模型包含一个参数（均值），而饱和模型每个观测值有一个参数。最小模型太简单了。另一方面，饱和模型是不提供信息的，因为它提供了完美的拟合。虽然饱和模型没有总结数据，但它们在实践中是有用的。最理想的模型是最小模型和饱和模型之间的。离度本质上是基于似然函数测量的模型与饱和模型之间的距离。`McCullagh` 和 `Nelder` (1989) 指出嵌套模型的离度差异可以用具有相应自由度的卡方分布来近似。

对于独立的二项分布随机变量 `$T_j, j=1,2,...,n, T \sim \text{Binomial}(\pi_j, m_j)$`，考虑 `$T_j$` 为二项分布。注意与之前将响应变量标记为 `$T$` 的符号稍不同。我们将泊松结果标记为 `$Y$`。那么，对于伯努利分布，可以证明离度为：

$D = 2\sum_{j=1}^n t_j \log\left(\frac{t_j}{m_j\hat{\pi}_j}\right) + (m_j - t_j) \log\left(\frac{m_j - t_j}{m_j-\hat{\pi}_j}\right) \quad (2.11)$

其中 `$\hat{\pi}_j = g^{-1}(\mathbf{x}_j\boldsymbol{\beta})$`。当 `$Y_j \sim \text{Poisson}(\lambda_j), j=1,2,...,n$` 时，可以证明离度为：

$D = 2\sum_{j=1}^n y_j \log\left(\frac{y_j}{\hat{\lambda}_j}\right) - (y_j-\hat{\lambda}_j) \quad (2.12)$

其中 `$\hat{\lambda}_j = g^{-1}(\mathbf{x}_j\boldsymbol{\beta})$`。

`Nelder` 和 `Wedderburn` 进一步提出了一种基于离度差异的顺序拟广义方差分析。这种分析之所以是因为嵌套（顺序）模型的离度相加性。`GENMOD` 程序可以提供广义方差分析。

另一个衡量 GLM 拟合优度的指标是 Pearson `$X^2$` 统计量。在 GLM 的背景下，它的定义为：

$X^2 = \sum_{j=1}^{n} \frac{(y_j-\hat{\mu}_j)^2}{v(\hat{\mu}_j)}$

其中 `$v(\hat{\mu}_j)$` 是考虑分布的估计方差函数。对于二项分布，其 Pearson `$X^2$` 统计量为：

$X^2 = \sum_{j=1}^{n} \frac{(t_j-m_j\hat{\pi}_j)^2}{m_j\hat{\pi}_j(1-\hat{\pi}_j)} \quad (2.13)$

以及泊松分布：

$X^2 = \sum_{j=1}^{n} \frac{(y_j-\hat{\lambda}_j)^2}{\hat{\lambda}_j} \quad (2.14)$

## SAS 中的过度离散模型

在某些正则条件下，两个统计量——离度（Deviance，`$D/\phi$`）和皮尔逊卡（`$X^2/\phi$`）的缩放版本都渐近于具有 `$(n-k)$` 个自由度的极限卡方分布。

## 2.6 广义线性模型的极大似然估计

设 `$y_j$` 代表随机变量 `$Y_j$` 的一个观测值，`$j=1,2,...,n$`，`$Y_j$` 来自于指数族中的给定分布。我们感兴趣的是找到 `$\beta$` 的极大似然估计（MLE）。对于某些分布，如二项分布和泊松分布，`$\phi$` 已知为 1。在随后的章节中，将分别获得参数向量 `$\beta$` 和离散（或过度离散）参数的极大似然估计。因此，根据第 1.6 节，对数似然函数为

```
$L(\beta, \phi; \mathbf{y}) = \sum_{j=1}^n \left\{ \frac{y_j - b(\theta_j)}{\phi} + c(y_j, f(\phi)) \right\}$
```

这里 `y` 代表观测向量 `$\mathbf{y} = (y_1, y_2, ..., y_n)$`。

我们现在考虑当 `$\phi$` 固定或已知时 `$\beta$` 的 MLE。`(2.15)` 对 `$\beta$` 的一阶导数构成的 `$k$` 维列向量是梯度或得分向量。即

```
$\mathbf{u}(\beta) = \frac{\partial L(\beta, \phi; \mathbf{y})}{\partial \beta}$
```

从技术上讲，`(2.15)` 中的每一项都是规范参数 `$\theta_j$` 的函数，而 `$\theta_j$` 是均值 `$\mu_j$` 的函数，`$\mu_j$` 是线性预测值 `$\eta_j$` 的函数，且 `$\eta_j = \mathbf{x}\beta$`。因此，获得梯度 `(2.16)` 需要使用链式法则。更多详细信息，请读者参考 `Hilbe` (2007) 中的第 2 章。

`(2.15)` 的二阶导数的 `$k \times k$` 矩阵是海森矩阵（Hessian），形式为

```
$\mathbf{H}(\beta) = \frac{\partial^2 L(\beta, \phi; \mathbf{y})}{\partial \beta \partial \beta}$
```

费雪信息矩阵 (FIM) 是海森矩阵期望值的负值。即

```
$\mathbf{I}(\beta) = -E \left[ \frac{\partial^2 L(\beta, \phi; \mathbf{y})}{\partial \beta \partial \beta} \right] = E \left[ \frac{\partial L(\beta, \phi; \mathbf{y})}{\partial \beta} \frac{\partial L(\beta, \phi; \mathbf{y})}{\partial \beta} \right]$
```

为了获得 `$\hat{\beta}$`（`$\beta$` 的 MLE），需要求解估计方程

```
$$\frac{\partial L(\beta;\phi;\mathbf{y})}{\partial \beta} = \mathbf{0}. \quad (2.19)$$
```

这些方程被称为极大似然得分方程。通常情况下，`(2.19)` 的解没有显式形式，因此通过迭代求解。有多种数值方法可用。Newton-Raphson 法的迭代步骤给出：

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + {\hat{H}(\hat{\beta}_{(S)})\}^{-1}\mathbf{u}(\hat{\beta}_{(S)}). \quad (2.20)$$
```

以及广泛使用的 Fisher Scoring 法（费雪评分法）实现如下

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + {\hat{I}(\hat{\beta}_{(S)})\}^{-1}\mathbf{u}(\hat{\beta}_{(S)}). \quad (2.21)$$
```

其中，`$\mathbf{u}(\hat{\beta}_{(S)})$` 是在 `$\hat{\beta}_{(S)}$` 处评估的对数似然函数 `(2.16)` 一阶导数的 `$k$` 维向量，`$\hat{H}(\hat{\beta}_{(S)})$` 是在 `$\beta=\hat{\beta}_{(S)}$` 处评估的 `$k\times k$` 海森矩阵 `(2.17)`，而 `$\hat{I}(\hat{\beta}_{(S)})$` 是在 `$\beta=\hat{\beta}_{(S)}$` 处评估的 `$k\times k$` 费雪信息矩阵 `(2.18)`。下标 `"$s$" ` 指步数或迭代。

前面的讨论适用于通用的 MLE 计算。在指数族的情况下，由于对数似然函数的导数与方程 `(1.9)` 和 `(1.10)` 中给出的一阶矩之间的关系，可以进一步简化。`Nelder` 和 `Wedderburn` (1972) 以及 `Wedderburn` (1974) 证明了极大似然方程 `(2.19)` 的解等同于迭代加权二二法程序。如果 `$\beta$` 的当前估计记为 `$\hat{\beta}_{(S)}$`，则改进的估计 `$\hat{\beta}_{(S+1)}$` 为

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + (\mathbf{D}^T\mathbf{D})^{-1}\mathbf{D}^T(\mathbf{y}-\mu). \quad (2.22)$$
```

`(2.22)` 右侧除观测向量 `$\mathbf{y}$` 外，所有项均在 `$\hat{\beta}_{(S)}$` 处评估，其中 `$n\times k$` 的一阶导矩阵为

```
$$\mathbf{D} = \begin{pmatrix} \frac{\partial \mu_1}{\partial \beta_1} & \dots & \frac{\partial \mu_1}{\partial \beta_k} \\ \vdots & \ddots & \vdots \\ \frac{\partial \mu_n}{\partial \beta_1} & \dots & \frac{\partial \mu_n}{\partial \beta_k} \end{pmatrix}^T,
```

`$\mathbf{V} = (\mathbf{d}_1, \dots, \mathbf{d}_n)$` 是 `$n\times n$` 的方差对角矩阵

```
$\mathbf{V} = \text{Diag}(\nu(\mu_1), \dots, \nu(\mu_n)) = \text{Diag}(v_1, \dots, v_n),$
```

而 `$\mathbf{\mu}$` 是 `$n$` 维均值列向量 `$\mathbf{\mu}=(\mu_1, \dots, \mu_n)$`。使用这些符号，`(2.22)` 可以写为

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + \left(\sum_{j=1}^{n} \mathbf{d}_j v_j^{-1} \mathbf{d}_j^T\right)^{-1} \sum_{j=1}^{n} v_j^{-1} (\mathbf{y}_j -\mu)$$
```

注意 `$\mathbf{d}_j$` 是一个 `$k$` 维列向量，而之前定义的协变量向量 `$\mathbf{x}_j$` 是 `$k$` 维行向量。如果假设使用规范连接，极大似然得分方程 `(2.19)` 变为

```
$X^T(\mathbf{y}-\mu) = 0$.
```

在这种情况下，方程 `(2.22)` 和 `(2.23)` 可以进一步简化。迭代程序简化到可以在任何计算机语言中轻松实现的程度。在规范连接下，我们有

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + (X^T\mathbf{V}X)^{-1} X^T(\mathbf{y}-\mu)$$
```

这可以写为

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + \left(\sum_{j=1}^{n} \mathbf{d}_j v_j^{-1} \mathbf{d}_j^T\right)^{-1} \sum_{j=1}^{n} v_j^{-1} (\mathbf{y}_j -\mu)$$
``` (注：此处原文公式似乎截断，已根据逻辑补全或保持对应结构)

此时，海森矩阵不包含 `V`，且渐近于 `I`。Newton-Raphson 法和 Scoring 方法是等价的。

在规范连接下，海森矩阵将不包含 `V`。这是一个良好的结果。MLE 估计的协方差矩阵渐近于 `I`。这 = `$\hat{\beta}_{(S+1)} v_j^{-1} (\mathbf{y}_j-\mu)$` 这种形式（注：原文此处逻辑存在混乱，翻译已尽量保留原文的结构）。在剂量-死亡研究中，我们关注对剂量的影响。当将观测百分比对剂量（或剂量的对数）绘图时，得到的图表类似于累积概率函数的 S 形状。`Bliss` (1933, 1935) 假设这种形状对应于累积正态分布（Probit 模型）。另一方面，`Berkson` (1944) 发现累积逻辑分布函数（Logit 模型）更合适。“probit”一词归于 `Bliss`，而“logistic”一词归于 `Pearl`。剂量-死亡分析是 GLM 的早期示例。

拟菊酯是发现于许多杀虫剂的一类化学物质。`Murray` (1938) 概述了同时评估杀虫剂的方法，即精确方法，以及可能的精度范围。不同浓度的拟菊酯在蝇身上进行了测试。

### 表 2.3：雄蝇的剂量-死亡数据

| 拟菊酯浓度 mg/100 cc (`$D_j$`) | 苍蝇数量 (`$m_j$`) | 死亡数量 (`$t_j$`) |
|---|---|---|
| 40 | 462 | 109 |
| 60 | 500 | 199 |
| 80 | 467 | 296 |
| 100 | 515 | 370 |
| 120 | 561 | 459 |
| 140 | 469 | 400 |
| 160 | 550 | 495 |
| 180 | 542 | 499 |
| 200 | 479 | 450 |
| 250 | 497 | 476 |
| 300 | 453 | 442 |

我们首先拟合逻辑回归模型，这等同于拟合具有二项分布和对连接的 GLM。在某些正则条件下，极大似然估计具有良好的性质。它们是无偏的或渐近无偏的。MLE 是渐近有效的，因为在样本量趋于无穷时，它们达到了 Cramer-Rao 下界。这意味着没有其他无偏估计量的渐近均方误差比 MLE 小。此外，它们是渐近正态的，也就是说随着样本量的增加，MLE 的分布趋向于高斯分布。

# SAS 中的过度离散模型

如果 `$\tilde{\pi}_j = \frac{t_j}{m_j}$` 是观测比例，其对应的逻辑回归（logit）定义为：

```
$$\ln\left(\frac{\tilde{\pi}_j}{1-\tilde{\pi}_j}\right) = \ln\left(\frac{t_j}{m_j-t_j}\right)$$$
```

在实践中，这些量被微调为

```
$$\ln\left(\frac{t_j+0.5}{m_j-t_j+0.5}\right)$$$
```

以避免在 `$t$` 为 0 或 `$m$` 时出现数值问题。估计的线性预测值为 `$\hat{\eta}_j = \hat{\beta}_0 + \hat{\beta}_1X_j$`。程序语句见程序 2.2。`GLIMMIX` 生成的结果见输出 2.2。

## 程序 2.2：拟虫酯的剂量-死亡数据拟合带 Logit 链接的二项模型

`Morel, J., and Nagaraj Neelander. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.` 更多资源请访问 `support.sas.com/publishing`。

表 2.4 汇总了直接来自输出 2.2 的极大似然结果。斜率 `$\beta_1$` 的幅度取决于变量 `"x"` 的尺度。对剂量进行常用对数变换将产生更大的 `$\beta_1$` 估计值。

**输出 2.2：拟虫酯剂量-死亡数据的 GLIMMIX 结果——带 Log 链接的二项模型**

| 蝇拟虫酯剂量-死亡，Murray (1938) 二项分布和 Log 链接的 GLM |
| --- |
| **GLIMMIX 过程** |
| 拟合统计量 |
| -2 对数似然 | 69.91 |
| Pearson 卡方 | 6.34 |
| Pearson 卡方 / DF | 0.70 |
| 参数估计值 |
| --- |
| 效应 | 估计值 | 标准误差 |
| **效应** | **估计值** | **标准误差** | **DF** | **Pr >|t|** |
| 截距 | -10.3279 | 0.3429 | | -30.12 | <0001 |
| x | 2.4582 | 0.07470 | 9 | 32.91 | <0001 |

**表 2.4：拟虫酯剂量-死亡数据带 Log 链接的二项模型的 MLE 结果**

| | 估计值 | 标准误差 |
| --- | --- | --- |
| `$\beta_0$` | -10.3279 | 0.3429 |
| `$\beta_1$` | 2.4582 | 0.0747 |
| -2 对数似然 | 69.91 | |

`GLIMMIX` 残差诊断图如图 2.2 所示。“残差预测值”并未显示离群值的存在或任何可感知的模式。残差与分位数图接近直线，表明残差具有渐近正态性。我们得出结论，逻辑回归模型拟合这些数据是可靠的。我们的结论也通过自由度归一化的 Pearson 卡方统计量证实，其值为 0.70（见输出 2.2）。

### 图 2.2：拟虫酯剂量-死亡数据带 Logit 链接的二项模型 GLIMMIX 残差诊断图

![](img/fa69b64c17ad451eb7eb4add92f5fb_44.png)

在剂量死亡研究中，感兴趣的量是 LD50，即杀死 50% 个体的剂量。该量也可以被认为是种体的中耐受水平。在逻辑回归模型下，LD50 可以通过求解方程轻松获得：

`$\beta_0 + \beta_1 LD50 = \ln\left(\frac{\pi}{1-\pi}\right)$`
