
## Weighted prediction

* `qui predict yhatols`

* `mean yhatols [pweight=swght], noheader`

```
| Mean | Std. err. | [95% conf. interval] |
|---|---|---|
| yhatols | 10670.83 | 138.0828 | 10400.08 | 10941.57 |
```
```stata
* mean yhatols [pweight=swght], noheader
```
（注：此处根据示例逻辑翻译，原文中表格内容对应如下）

| Mean | Std. err. | [95% conf. interval] |
|---|---|---|
| yhatols | 10670.83 | 138.0828 | 10400.08 | 10941.57 |
```stata
* mean yhatols, noheader // Unweighted prediction
```

```
| Mean | Std. err. | [95% conf. interval] |
|---|---|---|
| yhatols | 7135.206 | 78.5736 | 6981.144 | 7289.269 |
```

医疗费用的总体加权均值预测为 10671，而不加权预测给出的值低得多，为 7135.2。对于线性模型，标准边际效应 $\partial E(y_i|x_i)/\partial x_{ij}$ 对于所有观测值都等于 $\beta$，因此计算 ME 时加权不会产生差异。对于其他 ME（如弹性）以及非线性模型，加权会产生差异。

### 3.9 使用 Mata

Stata 提供了两种不同的计算方式：Stata 矩阵命令和 Mata 函数分别在附录 A 和 B 中讨论）。Mata 更加丰富，因为它是一种矩阵语言。我们通过使用与 3.5.2 节相同的 OLS 回归演示 Mata 的用法。从读取数据和定义局部宏开始：

```stata
* OLS with robust errors using Mata

* qui use medicare, clear

* keep age > 0 // Analysis for medical expenditures only (deleted)

* generate cons = 1

* local y

* local xlist
```

然后进入 Mata。使用 `st_view()` 函数将 Stata 变量转移到 Mata 矩阵 `$y$` 和 `$x$`，并将 `xlist` 中的每个项添加到逗号列表中。

```mata
    // Create y vector and X matrix from Stata

    st_view(y=, ., "y") // y is nx1

    st_view(X=, ., "list") // X is nk

    XXinv = cholinv(cross(X,X)) // XXinv is inverse of X'X

    b = XXinv*cross(X,y)             // b = [(X'X)^{-1]*X'y

    e = y - X*b

    n = rows(X)

    k = cols(X)

    s2 = (e.*e)/n-k

    vdef = s2*XXinv((e.*X)*n/(n-k))*XXinv // Default VCE not used

    vwhite("b",b)                  // Robust VCE

    st_matrix("b",b)               // Pass results from Mata to Stata

    st_matrix("V",vwhite)          // Pass results from Mata to Stata

end
```

回到 Stata 后，我们使用 `ereturn` 以类似于官方命令的格式显示结果，首先为 `$b$` 和 `$V$` 的列和行命名。

```stata
* Use Stata return display to present nicely formatted results

. matrix colnames b = `xlist'

. matrix colnames V = `xlist'

. matrix rownames V = `xlist'

. return post b V

. return display
```

| Coefficient | Std. err. | z | P|z| | [95% conf. interval] |
|---|---|---|---|---|---|
| suppins | .2556428 | .0465982 | 5.49 | 0.000 | .1643119 | .3469736 |
| phylum | .3020598 | .057705 | 5.23 | 0.000 | .18896 | .4151595 |
| actlim | .3560054 | .0634066 | 5.61 | 0.000 | .2317308 | .48028 |
| totchr | .3758201 | .0187185 | 20.08 | 0.000 | .3391326 | .4125077 |
| age | .0038016 | .0037028 | 1.03 | 0.305 | -.0034558 | .011059 |
| female | -.0843275 | .045654 | -1.85 | 0.065 | -.1738076 | .0051526 |
| income | .0025498 | .0010468 | 2.44 | 0.015 | .0004981 | .0046015 |
| cons | 6.703737 | .2827551 | 23.72 | 0.000 | .61499 | .7257575 |

当使用 `regress ... vce(robust)` 选项时，结果与 3.5.2 节中给出的完全相同。

### 3.10 额外资源

关键的 Stata 参考资料包括 `[U] Stata User's Guide` 和 `[R] regress`、`[R] regress postestimation`、`[R] estimates`、`[R] predict` 以及 `[R] test`。本章的内容出现在许多计量经济学教材中，例如 `Greene (2018)` 和 `Hansen (2022a)`；单变量统计请另参阅 `Hansen (2022b)`。

Stata 第 15 版本引入了一系列命令，包括 `putdoc` 和 `dynata`，用于将估计结果、汇总统计和图表导出并生成 Word、Excel、PDF 和 HTML 格式的报告。此外，这可以通过动态方式进行，使得 Stata 输出的任何变化都能立即反映文档中。详细信息请参阅 `[RPT] Stata Reporting Reference Manual`。对于格式化输出，Stata 17 引入了 `collect` 命令和更灵活的 `table` 版本。

### 3.11 练习

- 1. 仅使用前 100 个观测值拟合 3.5 节的模型。通过三种方式计算标准误：默认、异方差以及针对慢性问题数量进行聚类的聚类稳健标准误。使用 `estimates` 生成一个包含三组系数和标准误的表格，并对标准误之间的任何显著差异进行注释。使用 `vce(robust)`、`vce(hc2)` 和 `vce(hc3)` 选项获得三组替代异方差稳健标准误，构建类似的表格，并对不同标准误估计之间的差异进行注释。

- 2. 使用稳健标准误（而非 `female`）拟合 3.5 节的模型。在 5% 的水平下，检验人口统计学变量年龄、性别和收入的联合显著性。假设男性（而非女性）对医疗支出的影响与年龄增长 10 年相同。在约束条件 $\beta_{phyl} = \beta_{actlim}$ 下拟合模型，首先输入 `constraint1 phyl=actlim`，然后使用带有 `constraints(1)` 的 `nsreg`。

- 3. 拟合 3.6 节的模型并手动实现 RESET 测试，通过将 $y$ 对 $\tilde{y}$、$\tilde{y}^2$ 和 $\tilde{y}^3$ 回归，并联合检验 $\tilde{y}^2$、$\tilde{y}^3$ 和 $\tilde{y}^4$ 的系数是否为 0。为了获得与 `ostatest` 相同的结果，在此回归中你需要使用默认还是稳健的 VCE 估计？同样，通过将 $y$ 对 $\tilde{y}$ 和 $\tilde{y}^2$ 回归并检验 $\tilde{y}^2$ 的系数是否为 0 来使用 `linktest`。为了获得与 `linktest` 相同的结果，在此回归中你需要使用默认还是稳健的 VCE 估计？

- 4. 拟合 3.6 节的模型并使用 `hetstest z = x` 执行异方差的标准拉格朗日乘子检验。然后，将该测试实现为 $y_i^*$ 对截距和 $z_i$ 回归平方和的 0.5 倍，其中 $y_i^* = \tilde{u}_i^2/(N \sum \tilde{u}_j^2) - 1$，$\tilde{u}_i$ 是原始 OLS 回归的残差。接下来，使用带有 `iid` 选项的 `hetstest`，证明该测试等于 $N \times R^2$，其中 $R^2$ 是通过 $\tilde{u}_i^2$ 对截距和 $z_i$ 回归得到的。

- 5. 使用 3.7.6 节中的 DGP 生成一个样本量为 100 的样本。将 $y$ 对 $x$ 和截距进行回归。应用 RESET 遗漏变量检验。测试是否指示函数形式设定错误？接下来，使用后估计命令 `estatest` 生成 IM 综合诊断统计量。如果你只应用了这项测试，会对你的模型设定做哪些更改？在更改模型设定之前你会进行额外的测试吗？

- 6. 线性回归中偶尔使用的一种数据转换类型（尽管计量经济学中并不常见）是变量标准化。要标准化变量，从每个观测值中减去该变量的样本均值，并将结果除以该变量的样本标准差。得到的均值为零且标准差为一的变量与所有变量均均标准化的回归无关。回归系数被解释为衡量自变量变化一个标准差的影响，因此在某种意义上可以在变量之间进行比较。注意，对所有变量进行标准化后，重新估计 3.5.2 节的回归方程。不显著的系数与之前回归中的系数相同吗？哪个变量的系数最大？这意味着它是回归中最重要的变量吗？

# 第 4 章
# 线性回归扩展

## 4.1 引言

在本章中，我们考虑在应用工作中广泛使用的线性回归若干扩展。这些扩展源于现实情况：计量经济调查很少以简单报告线性回归的方式告终。更多情况下，回归是用于对数据进行深度分析、检验经济假设、进行预测（样本内或样本外）以及其他工具。本章将考虑这些主题。

实证应用的合理性部分取决于取决于模型的稳健性。因此，3.6 节和 3.7 节中考虑的各种检验是本章所考虑应用的自然准备工作。所考虑的所有应用都是基于条件均值，而不是高阶矩。这引出了问题：模型其他特征（包括高阶矩）的设定错误是否会导致条件均值的估计不一致，即使条件均值模型设定是正确的？这是一个计量经济学上微妙的问题。通常情况下，答案是肯定的。然而，对于线性回归模型，情况并非如此，因为 OLS 估计量的一致性只需要条件均值设定正确。

我们考虑了线性回归的四个主要应用：预测（样本内和样本外）、各种边际效应（MES）估计、回归分解以及基于双重差分（DID）的处理效应估计。

## 4.2 样本内预测

对于线性回归模型，给定 $\mathbf{x}=\mathbf{x}_p$ 时 $y$ 的条件均值估计量 $\hat{E}(y|\mathbf{x}_p)=\mathbf{x}'_p\beta$ 是条件预测值 $\hat{y}=\mathbf{x}'_p\beta$。我们从医疗支出线性模型开始预测，因为它更容易，然后再转向对线性模型。

我们在本节介绍样本内每个观测值的预测，并在下一节介绍样本外预测。关于预测的更多细节见 13.5–13.7 节，其中介绍了许多方法。获取总体平均预测的加权平均预测在 3.8 节中介绍。

### 4.2.1 predict 命令

预测是在 `regress` 之后通过 `predict` 命令获得的。`predict` 命令的语法为：

```
predict [type] newvar [if] [in] [ , statistic]
```
