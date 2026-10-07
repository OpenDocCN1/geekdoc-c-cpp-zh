
## 4.3 样本外预测

我们现在考虑样本外预测。虽然我们关注预测的精确性，但请注意，当回归变量与用于拟合模型的变量越远时，样本外预测的可靠性就会变得越存。样本外预测的准确性通常是模型设定严苛测试的基础，但可能无法提供潜在缺陷模型特征的明确指示。

### 4.3.1 样本外预测

样本外预测本身对于生成预测很有用，也可以用于将拟合模型与未用于拟合模型的子空间进行对比。一些模型误指定的检验是基于样本外预测误差的。`predict` 命令可以生成样本内样本外的预测。

令 $X_p$ 表示 $q \times K$ 矩阵，代表一组 $q$ 个未用于估计的观测值，这些值被用来生成估计样本之外的预测。我们假设因变量是由与拟合模型相同的模型生成的，$q$ 个样本外的 $y$ 由 $y_p = X_p\beta + u_p$ 生成。因此，我们使用 $\hat{y}_p = X_p\hat{\beta}$ 来预测条件均值并对实际值进行预测。然后，$q$ 个预测误差的向量为 $\hat{u}_p = \hat{y}_p - y_p$。这些预测误差可以用多种方法来评估拟合的回归。

为了使预测具有意义，矩阵 $X_p$ 应该与用于估计的矩阵“相似”；也就是说，它在预测样本中的变化范围应该与估计样本的范围相似。否则，估计样本的估计可能不适用于预测样本，且估计样本与预测样本之间回归变量的差异将显著导致预测误差。基于预测的检验可以用于测试样本同质性。

条件均值的预测的方差矩阵为：

$$\widehat{E}(\mathbf{y}_p|\mathbf{X}_p) = \text{Var}(\mathbf{x}_p\widehat{\beta}) = \mathbf{x}_p\text{Var}(\widehat{\beta})\mathbf{x}_p'$$

该公式用于计算点预测条件均值的假设检验和置信区间。它可以使用默认标准误或稳健标准误。请注意，随着样本量的增大，$\text{Var}(\widehat{\beta})$ 会变小，因此预测的精确度会提高。

实际值的预测额外还需要预测误差项，因为 $\mathbf{y}_p = \mathbf{x}_p\beta + \mathbf{u}_p$。我们最好的估计是 $\mathbf{u}_p = 0$。由于误差与回归变量无关，因此实际值的预测的方差矩阵为：

$$\widehat{\mathbf{y}}_p|\mathbf{X}_p) = \text{Var}(\mathbf{x}_p\beta + \mathbf{u}_p) = \mathbf{x}_p\text{Var}(\widehat{\beta})\mathbf{x}_p' + \text{Var}(\mathbf{u}_p)$$

这个估计更为困难，因为它取决于 $\text{Var}(\mathbf{u}_p)$。此外，即使在大样本中，也可能存在巨大的预测误差，因为 $\text{Var}(\widehat{\mathbf{y}}_p) > \text{Var}(\mathbf{u}_p)$ 始终成立。

如果误差是独立同分布的 i.i.d. 则 $\text{Var}(\mathbf{u}_p) = \sigma^2\mathbf{I}$ 且 $\text{Var}(\widehat{\beta}) = \sigma^2(\mathbf{X}'\mathbf{X})^{-1}$，因此预测的方差简化为 $\sigma^2\{\mathbf{I} + \mathbf{x}_p'(\mathbf{X}'\mathbf{X})^{-1}\mathbf{x}_p\}$。那么，在单个样本外观测值的情况下，当 $\mathbf{x} = \mathbf{x}_p$ 时，因变量实际值预测的大样本 95% 置信区间为：

$$\widehat{\mathbf{y}}_p \pm 1.96\sqrt{\sigma^2\{1 + \mathbf{x}_p'(\mathbf{X}'\mathbf{X})^{-1}\mathbf{x}_p\}}$$

$s^2$ 是 $\sigma^2$ 的样本估计。当 $\mathbf{x} = \mathbf{x}_p$ 时，条件均值预测对应的对应样本 95% 置信区间为：

$$\hat{y}_p \pm 1.96\sqrt{s^2\mathbf{x}_p'(\mathbf{X}'\mathbf{X})^{-1}\mathbf{x}_p}$$

点预测和估计方差 $s^2$ 都可能对由于与样本期不同机制产生的离群值而敏感。

上述考虑促使了在前节中提到的用于测试残差同方差性和正态性的诊断程序。正态分布是对称的，因此其三阶矩为 0。标准正态分布的四阶矩等于 3。因此，偏离正态性由显著不同于 0 的偏系数和显著大于 3 的非正态峰度系数指示；例如见 3.7.5。

### 4.3.2 样本外预测示例

这里的示例基于具有 100 个观测值的生成数据。模型拟合到前 90 个观测值的子样本上，剩下的 10 个用于预测。我们展示了如何实现样本外预测。

在第一部分，使用 $y = x + u$ 生成了 100 个观测值。对前 90 个观测值拟合了正确指定的回归，并生成了 10 个样本外预测。为了比较，还对全样本进行了回归拟合，并生成了相应的 10 个样本内预测。误差已汇总。在这个示例中，数据生成过程 DGP 满足了基本假设，因此预测误差反映了估计误差和由于误差项带来的内在随机性。

```stata
* Out-of-sample OLS predictions using correctly specified model
clear all
* set obs 100
* seed 101
* generate u = rnormal()
* generate x = 10 + 4*rnormal()
* generate y = x + u
* regress y if _n < 91
* predict yhatis if _n > 90 // Predict 10 out-of-sample observations
* regress y
* predict yhatis if _n > 90 // Predict 10 in-sample observations
* generate ferroros = y - yhatis
```

使用样本外预测进行模型选择（特别是 $k$-折交叉验证）在第 28.2 节中有详细介绍。

## 4.4 预测边际 Predictive margins

线性回归之后，重点可能在于评估回归变量不同值处的条件均值。例如，在包含许多控制变量的回归之后，我们可能希望分别预测男性和女性的医疗支出，或者希望在几个不同的值处进行预测。这些都是预测均值 PMS，它们会随回归变量赋值的值而变化。

更广泛地说，还可以研究条件均值以外的量，例如逻辑回归后的条件概率。Lane 和 Nelder 1982 引入了“预测边际”一术，涵盖在回归变量的不同值处对感兴趣的量进行估计后预测。

### 4.4.1 预测边际

在线性回归之后，可以在单点 $x = x^*$ 处评估 PM，此时 $PM = x^\beta$；或者对个体的不同回归变量值进行评估并取平均。当在值 $x_i = x_i^*, i = 1, \dots, N$ 处评估时，PM 为：

```
PM = \frac{1}{N} \sum_{i=1}^{N} x_i^* \hat{\beta}
```

一般情况下，$g(x, \beta)$ 的预测边际计算方法为 $(1/N) \sum_{i=1}^{N} g(x_i^*, \hat{\beta})$。

- 设定评估点 $x_i^*$ 有许多方法。主要情况包括：
    1) 在样本值 $x_i, i = 1, \dots, N$ 处计算 PM 并取平均；
    2) 在样本均值 $\bar{x}$ 处计算，此时 $PM = \bar{x}'\hat{\beta}$；
    3) 在指定值 $x^*$ 处计算，此时 $PM = x^*\hat{\beta}$。

在实践中，对于具有多个回归变量的模型，通常使用这些方法的组合。考虑针对 $z$ 的各种指定值的预测边际 $z$ 通常一个标量变量，但也可能是多个变量，其中 $z$ 是拟合模型中回归变量的子组件：

```
\widehat{y}_i = \mathbf{x}_i' \hat{\beta} = \mathbf{z}_i' \hat{\alpha} + \mathbf{w}_i' \hat{\gamma}
```

令 $z_k$ 表示 $z$ 的第 $k$ 个指定值，此时：

```
(\widehat{y}_i^* = \mathbf{z}_k, \mathbf{w}_i^*) = \mathbf{z}_k' \hat{\alpha} + \mathbf{w}_i^{*'} \hat{\gamma})
```

那么 $x_i^* = \{\mathbf{z}_k, \mathbf{w}_i^*\}$，设定评估点 $x_i^*$ 有许多方法，因为设定剩余变量 $w_i^*$ 的值也有许多方法。

首先，我们可以将剩余回归变量设定为样本值，即 $w_i^* = w_i$。其次，我们可以将剩余回归变量设定为一个共同的指定值 $w_i^* = \mathbf{w}^*$。第三，我们可以将剩余回归变量设定为它们的样本均值，即 $w_i^* = \bar{w}$。最后，这些方法的任何组合都是可能的。例如，令 $\mathbf{w}_i' \hat{\gamma} = \mathbf{w}_1' \gamma_1 + \mathbf{w}_2' \gamma_2 + \mathbf{w}_3' \gamma_3$，我们可以在 $w_i^* = [\mathbf{w}_1^*, \mathbf{w}_2^*, \mathbf{w}_3^*]$ 处进行评估。此时，部分剩余回归变量设定为样本值，部分为指定值，另一部分为样本均值。

原则上，预测边际可以使用一个或多个 Stata 命令（通常是 `generate` 和 `predict`）计算。这些预测边际的标准误差可以通过自助 bootstrap 获得。简单的方法是直接使用强大的 `margins` 命令。该命令计算预测边际及其相关的标准误、$t$ 统计量和置信区间。它还可以用于计算平均边际效应 MES，而 `marginsplot` 命令则以图形形式呈现结果。相关讨论见于 100 多页文档。

### 4.4.2 margins 命令

估计命令（包括 `regress`）之后的 `margins` 命令语法如下：
