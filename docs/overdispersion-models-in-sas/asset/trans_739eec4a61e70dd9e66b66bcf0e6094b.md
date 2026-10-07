

## 26 SAS 中的过离散模型

两种统计量的缩放版本，即偏差 ($D/\phi$) 和皮尔逊卡方 ($X^2/\phi$)，在某些正则条件下具有自由度为 $(n-k)$ 的极限卡方分布。

## 2.6 广义线性模型的极大似然估计

设 $y_j$ 表示随机变量 $Y_j$ 的实现，$j=1,2,...,n$，$Y_j$ 来自指数族中的给定分布。我们感兴趣的是寻找 $\beta$ 的 MLE。对于某些分布，在二项分布和泊松分布中，$\phi$ 已知为 1。在后面的章节中，参数向量 $\beta$ 和离散（或过离散）参数的极大似然估计都将被求得。因此，由第 1.6 节可知对数似然函数为

```
$L(\beta, \phi; \mathbf{y}) = \sum_{j=1}^n \left\{ \frac{y_j - b(\theta_j)}{\phi} + c(y_j, f(\phi)) \right\}$
```

这里 $y$ 表示观测向量 $\mathbf{y} = (y_1, y_2, ..., y_n)$。

我们现在考虑当 $\phi$ 固定或已知时 $\beta$ 的 MLE。对 (2.15) 关于 $\beta$ 的 k 维列向量的一阶导数是梯度或得分向量。即

```
$\mathbf{u}(\beta) = \frac{\partial L(\beta, \phi; \mathbf{y})}{\partial \beta}$
```

从技术上讲，(2.15) 中的每一项都是正则参数 $\theta_j$ 的函数，而 $\theta_j$ 是均值 $\mu_j$ 的函数，$\mu_j$ 是线性预测变量 $\eta_j$ 的函数，且 $\eta_j = \mathbf{x}\beta$。因此，求得梯度 (2.16) 需要链式法则。更多细节请参阅 Hilbe (2007) 第 2 章。

(2.15) 的二阶导数 $k \times k$ 矩阵是 Hessian，由下式给出

```
$\mathbf{H}(\beta) = \frac{\partial^2 L(\beta, \phi; \mathbf{y})}{\partial \beta \partial \beta}$
```

Fisher 信息矩阵 (FIM) 是 Hessian 期望值的负值。即

```
$\mathbf{I}(\beta) = -E \left[ \frac{\partial^2 L(\beta, \phi; \mathbf{y})}{\partial \beta \partial \beta} \right] = E \left[ \frac{\partial L(\beta, \phi; \mathbf{y})}{\partial \beta} \frac{\partial L(\beta, \phi; \mathbf{y})}{\partial \beta} \right]$
```

为了求得 $\hat{\beta}$，$\beta$ 的 MLE，需要求解估计方程

```
$$\frac{\partial L(\beta;\phi;\mathbf{y})}{\partial \beta} = \mathbf{0}. \quad (2.19)$$
```

这些方程被称为极大似然得分方程。更常见的是，(2.19) 的解没有显式形式，因此需要迭代求解。有多种数值方法可用。Newton-Raphson 方法的迭代过程为

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + {\hat{H}(\hat{\beta}_{(S)})\}^{-1}\mathbf{u}(\hat{\beta}_{(S)}). \quad (2.20)$$
```

而广泛使用的 Fisher 打分法实现如下

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + {\hat{I}(\hat{\beta}_{(S)})\}^{-1}\mathbf{u}(\hat{\beta}_{(S)}). \quad (2.21)$$
```

其中 $\mathbf{u}(\hat{\beta}_{(S)})$ 是在 $\hat{\beta}_{(S)}$ 处求值的对数似然函数 (2.16) 的一阶导数的 k 维向量，$\hat{H}(\hat{\beta}_{(S)})$ 是在 $\beta=\hat{\beta}_{(S)}$ 处求值的 $k\times k$ Hessian 矩阵 (2.17)，而 $\hat{I}(\hat{\beta}_{(S)})$ 是在 $\beta=\hat{\beta}_{(S)}}$ 处求值的 $k\times k$ Fisher 信息矩阵 (2.18)。下标 "$s$" 指步骤或迭代。

上述讨论适用于一般情况下 MLE 的计算。在指数族的情况下，由于对数似然函数导数与 (1.9) 和 (1.10) 中给出的第一矩之间的关系，进一步简化。Nelder 和 Wedderburn (1972) 以及 Wedderburn (1974) 表明，极大似然方程 (2.19) 的解等价于迭代加权最小二乘过程。如果 $\beta$ 的当前估计记为 $\hat{\beta}_{(S)}$，则改进的估计 $\hat{\beta}_{(S+1)}$ 为

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + (\mathbf{D}^T\mathbf{D})^{-1}\mathbf{D}^T(\mathbf{y}-\mu). \quad (2.22)$$
```

(2.22) 右侧除观测向量 $\mathbf{y}$ 外的所有项均在 $\hat{\beta}_{(S)}$ 处求值，$n\times k$ 一阶导数矩阵

```
$$\mathbf{D} = \begin{pmatrix} \frac{\partial \mu_1}{\partial \beta_1} & \dots & \frac{\partial \mu_1}{\partial \beta_k} \\ \vdots & \ddots & \vdots \\ \frac{\partial \mu_n}{\partial \beta_1} & \dots & \frac{\partial \mu_n}{\partial \beta_k} \end{pmatrix}^T,
```

$\mathbf{V} = (\mathbf{d}_1, \dots, \mathbf{d}_n),$ 方差的 $n\times n$ 对角矩阵

```
$\mathbf{V} = \text{Diag}(\nu(\mu_1), \dots, \nu(\mu_n)) = \text{Diag}(v_1, \dots, v_n),$
```

以及 $\mathbf{\mu}$ 为均值 $\mathbf{\mu}=(\mu_1, \dots, \mu_n)$ 的 $n$ 维列向量。利用这些记号，(2.22) 可写为

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + \left(\sum_{j=1}^{n} \mathbf{d}_j v_j^{-1} \mathbf{d}_j^T\right)^{-1} \sum_{j=1}^{n} v_j^{-1} (\mathbf{y}_j -\mu)$$
```

注意 $\mathbf{d}_j$ 是 k 维列向量，而协变量向量 $\mathbf{x}_j$，如前所述，是 k 维行向量。如果假设正则链接，则极大似然得分方程 (2.19) 变为

```
$X^T(\mathbf{y}-\mu) = 0$.
```

在这种情况下，方程 (2.22) 和 (2.23) 可以进一步简化。迭代过程简化到可以很容易地在任何计算机语言中实现。在正则链接下我们则有

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + (X^T\mathbf{V}X)^{-1} X^T(\mathbf{y}-\mu)$$
```

可以写为

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + \left(\sum_{j=1}^{n} \mathbf{x}_j^T v_j^{-1} \mathbf{x}_j\right)^{-1} \sum_{j=1}^{n} v_j^{-1} (\mathbf{y}_j -\mu)$$
```

注意在正则链接下 Hessian 不涉及 $V$，因此将与 $I$，FIM 相同。因此 Newton-Raphson 和打分法将是相同的。这确实是一个令人愉快的结果。MLE 的方差-协方差矩阵由该 Hessian 或 FIM 估计，具体取决于估计方法。

- 我们将使用一个研究非常充分的方法来说明 logit 和 probit 回归模型中带协变量的计算。我们还展示了 GLIMMIX 过程中可用的一些诊断图，这些图在实践中用于评估拟合质量很有用。在剂量-死亡率研究中，我们关注药物的效应，剂量通常表示为其对数的函数。当观察到的百分比对剂量（或剂量的对数）作图时，所得图形类似于累积概率函数的 S 形或 sigmoid 形。Bliss (1933, 1935) 假设这种形状对应于累积正态分布函数（Probit 模型）。另一方面，Berkson (1944) 发现使用累积 Logistic 分布函数（Logit 模型）更为合适。“probit”一词归因于 Bliss，而“logistic”一词归因于 Pearl 和 Reed (1920)，并在 Berkson 1944 年的论文中被采纳。剂量-死亡率数据的 probit 和 logistic 分析是 GLM 的早期例子。这类模型也称为定量反应模型。

- 除虫菊酯是一类存在于许多杀虫剂中的杀虫化学物质。Murray (1938) 概述了一种同时评估不同杀虫剂的方法，称为 Peet-Greedy 方法，以及可能的准确性范围。对雄蝇的副本测试了十一组不同浓度的总除虫菊酯。

## 表 2.3：雄蝇剂量-死亡率数据

| 浓度 除虫菊酯 mg/100 cc ($D_j$) | 蝇数 ($m_j$) | 死亡数 ($t_j$) |
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

我们首先拟合一个 logistic 回归模型，这等同于拟合二项分布和对数链接的 GLM。在某些正则条件下，极大似然估计具有最优性质。它们是无偏的或渐近无偏的。MLE 在渐近意义上是有效的，因为它们在样本量趋于无穷时达到 Cramer-Rao 下界。这意味着没有其他无偏估计量的渐近均方误差低于 MLE。此外，它们是渐近正态的；即，随着样本量的增加，MLE 的分布趋向于高斯分布。

