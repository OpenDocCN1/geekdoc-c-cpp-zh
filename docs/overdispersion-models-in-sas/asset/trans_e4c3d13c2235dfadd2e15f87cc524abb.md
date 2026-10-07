

## 22 SAS 中的过离散模型

## 图 2.1：增重示例的诊断图

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_34_0.png)

## 2.4 广义线性模型 (GLM)

广义线性模型 (GLM) 是线性回归模型的扩展，用于容纳非正态的响应变量，甚至可能是离散的。GLM 形式化捕捉了当响应服从指数族分布的一个成员时，最大似然估计计算中的本质共同性，并且响应变量的均值通过已知的非线性函数与预测变量的未知线性组合相关联。因此，GLM 为线性回归、二项逻辑回归和泊松回归模型等常用模型的大类提供了一种统一的方法。为了理解 GLM，需要三个基本概念：随机成分（响应变量）、系统成分（预测变量）和链接函数。

$Y_j, j=1,2,...,n$, 表示 $n$ 个独立随机变量，属于指数族中的特定分布。我们有 $E(Y_j)=\mu_j$ 且由于 $Y_j$ 属于指数族。

$Var(Y_j)=\phi v(\mu_j)$。

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS.. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

在 GLM 框架中，均值 $\mu_j$, $j=1,2,...,n$, 依赖于已知协变量的 $k$ 维行向量 $\mathbf{x}_j$ 和未知参数的 $k$ 维列向量 $\mathbf{\beta}$，通过一个两次可微的光滑函数 $g(\cdot)$ 使得

```
$g(\mu_j) = \mathbf{x}_j\mathbf{\beta} = \sum_{i=1}^k x_{ji}\beta_i. (2.10)$
```

函数 $g(\cdot)$ 称为 **链接函数**，而 $\mathbf{x\beta}$ 称为 **线性预测变量**。请回忆链接函数先前在第 6 章第 1.6 节中定义过。线性预测变量通常表示为 $\eta_j = \mathbf{x}_j\mathbf{\beta}$。在第 2.2 节讨论的经典回归模型中，
$\mu_j = \mathbf{x}_j\mathbf{\beta} = \sum_{i=1}^k x_{ji}\beta_i$，因此链接函数为恒等函数。注意 $\mu_j = g^{-1}(\mathbf{x}_j\mathbf{\beta})$ 而 $g^{-1}(\cdot)$ 为均值函数。在第 1 章表 1.2 中我们提供了伯努利和泊松分布的均值和规范链接函数。从现在开始，$g(\cdot)$ 将用于表示任何链接函数，包括规范链接函数。因此，GLM 的主要特征是：

- 1. **随机成分**：$Y_j$, $j=1,2,...,n$ 的分量是独立的并且服从指数族中的一个分布。

- 2. **系统成分**：线性预测变量 $\eta_j = \mathbf{x}_j\mathbf{\beta}$, $j=1,2,...,n$，使得 $\mathbf{x}_j$ 为已知协变量的向量，而 $\mathbf{\beta}$ 为未知参数向量。

- 3. **链接函数**：随机部分与系统部分之间的联系即 $g(\mu_j) = \eta_j$, $j=1,2,...,n$。

表 2.2 给出了各种族成员的 GLM 的这三个关键成分。在所有这些例子中，随机成分是 $Y_j$ 而线性预测变量是 $\eta_j = \mathbf{x}_j\mathbf{\beta}$。请注意分布允许不止一个链接函数，并且选择不限于规范链接。这不是一个详尽的列表。可用链接函数的完整列表可在 GENMOD GLIMMIX 文档中找到。

## 表 2.2：选定分布的一些链接函数和均值函数

| $Y_j$ 的分布 | 链接函数 | 均值函数 |
|---|---|---|
| Normal($\mu_j, \sigma^2$) | 恒等：$\mu_j = \mathbf{x}\beta$ | 恒等：$\mu_j = \mathbf{x}\beta$ |
| Normal($\mu_j, \sigma^2$) | 对数：$\ln(\mu_j) = \mathbf{x}\beta$ | 指数：$\mu_j = e^{\mathbf{x}\beta}$ |
| Bernoulli($\pi_j$) | Logit：$\ln\frac{\pi_j}{1-\pi_j} = \mathbf{x}\beta$ | Logistic：$\pi_j = \frac{e^{\mathbf{x}\beta}}{1+e^{\mathbf{x}\beta}}$ |
| Bernoulli($\pi_j$) | Probit：$\Phi^{-1}(\pi_j) = \mathbf{x}\beta$ | Normal：$\pi_j = \Phi(\mathbf{x}\beta)$ |
| Poisson($\lambda_j$) | 对数：$\ln(\lambda_j) = \mathbf{x}\beta$ | 指数：$\lambda_j = e^{\mathbf{x}\beta}$ |
| Poisson($\lambda_j$) | 恒等：$\lambda_j = \mathbf{x}\beta$ | 恒等：$\lambda_j = \mathbf{x}\beta$ |

这里，$\Phi(\cdot)$ 表示标准正态分布的累积概率函数，

给定为，$\Phi(x) = \frac{1}{\sqrt{2\pi}} \int \exp\left(-\frac{Z^2}{2}\right) dZ$。

## 2.5 偏差和 Pearson 卡方统计量

在线性回归模型中，拟合优度通常用残差平方和来衡量。嵌套模型是通过从较大的（完整）模型中取预测变量的子集得到的。可以用残差平方和将简化模型与完整模型进行比较，并且可以使用完整模型和简化模型的残差平方和构造 F 检验。在 GLM 中，残差平方和可能并不总是具有意义，尤其是在响应变量为离散时。因此，需要替代的拟合优度检验方法。通过计算偏差统计量，该统计量最初由 Nelder 和 Woodburn 于 1971 年提出。他们指出，对于任何一组，两个极端模型都是可以设想的：即最小模型和饱和模型。最小模型只包含一个参数（均值），而饱和模型对每个观测值都有一个参数。最小模型过于简单。另一方面，饱和模型在提供完美拟合估计最大允许参数数量的意义上是无信息的。尽管饱和模型不能概括数据，但在实践中很有用。最理想的模型可能介于最小模型和饱和模型之间。偏差本质上是模型与饱和模型之间的距离，以对数似然函数的形式衡量。McCullagh 和 Nelder（1989）指出，嵌套模型偏差的差异可以用卡方分布近似，其自由度为两个模型比较的参数。

对于独立二项随机变量 $T_j, j=1,2,...,n, T \sim \text{Binomial}(\pi_j, m_j)$，考虑 $t_j$ 为 $T_j$ 的二项分布。请注意通过用字母 $T$ 表示响应变量而与之前的记号略有不同，即二项分布。我们将用字母 Y 表示泊松和伯努利结果。然后，对于二项分布，可以证明偏差为

```
$D = 2\sum_{j=1}^{n} t_j \log\left(\frac{t_j}{m_j\hat{\pi}_j}\right) + (m_j - t_j) \log\left(\frac{m_j - t_j}{m_j-\hat{\pi}_j}\right) \quad (2.11)$
```

其中 $\hat{\pi}_j = g^{-1}(x_j\hat{\beta}_j)$。当 $Y_j \sim \text{Poisson}(\lambda_j), j=1,2,...,n$ 时，可以证明偏差为

```
$D = 2\sum_{j=1}^{n} y_j \log\left(\frac{y_j}{\hat{\lambda}_j}\right) - (y-\hat{\lambda}_j) \quad (2.12)$
```

其中 $\hat{\lambda}_j = g^{-1}(x_j\hat{\beta}_j)$。

Nelder 和 Wedderburn 更进一步，提出了广义方差分析，用于使用偏差差异进行模型的顺序拟合，类似于基于平方差的经典方差分析。这种分析是可能的，因为嵌套（顺序）模型的偏差具有可加性。GENMOD 过程可以提供广义方差分析。

GLM 拟合优度的另一个重要衡量指标是 Pearson $X^2$ 统计量。在 GLM 的背景下，它定义为

```
$X^2 = \sum_{j=1}^{n} \frac{(y_j-\hat{\mu}_j)^2}{v(\hat{\mu}_j)}$
```

其中 $v(\hat{\mu}_j)$ 为所考虑分布的估计方差函数。对于二项分布，Pearson $X^2$ 统计量为

```
$X^2 = \sum_{j=1}^{n} \frac{(t_j-m_j\hat{\pi}_j)^2}{m_j\hat{\pi}_j(1-\hat{\pi}_j)} \quad (2.13)$
```

对于泊松分布

```
$X^2 = \sum_{j=1}^{n} \frac{(y_j-\hat{\lambda}_j)^2}{\hat{\lambda}_j} \quad (2.14)$
```

