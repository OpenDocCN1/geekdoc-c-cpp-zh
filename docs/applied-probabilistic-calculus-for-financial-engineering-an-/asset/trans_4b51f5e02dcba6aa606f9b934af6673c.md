
```
#
# The selected portfolio consists of the following investments:
#
# IBM = International Business Machines
# MS = Morgan Stanley
# DELL = Dell Computer
# C = Citigroup Inc.
# JPM = JPMorgan Chase and Company
# BAC = Bank of America Corporation
#
Covariance Risk Budgets:
IBM MS DELL C JPM BAC

Target Returns and Risks:
mean mu Cov Sigma CVaR VaR
0.0000 0.0566    0.1460 0.0000 0.0000

Description:
Tue Mar 22 08:31:47 2016 by user: Bert

$posteriorOptPortfolio
Title:
MV Tangency Portfolio
Estimator: getPosteriorEstim
Solver: solveQuadprog
Optimize: minRisk
Constraints: LongOnly

Portfolio Weights:
IBM MS DELL C JPM BAC
0.3633 0.1966 0.1622 0.0000 0.2779 0.0000

Covariance Risk Budgets:
IBM MS DELL C JPM BAC

Target Returns and Risks:
mean mu Cov Sigma CVaR VaR
0.0000 0.0689    0.1268 0.0000 0.0000

Description:
Tue Mar 22 08:31:47 2016 by user: Bert

attr(,"class")
```

图6.4(a) BL-1：为后续绘图准备空间。

![](img/551ca8853d2ba8528201e7a57e5006b4_451_0.png)

## 权重

![](img/551ca8853d2ba8528201e7a57e5006b4_451_1.png)

图6.4(b) BL-2：权重饼图输出（optPorts$priorOptimPortfolio）。

```
[1] "BLOptimPortfolios"
> par(mfrow = c(2, 1))
> # Output: Figure 6.4a: BL-1
>
(Providing space for following graphical outputs)
> weightsPie(optPorts$priorOptimPortfolio)
> # Output: Figure 6.4b: BL-2
>
A piechart of the Relative Distributions of IBM and MS in the Optimum Portfolio
>
> weightsPie(optPorts$posteriorOptimPortfolio)
> # Output: Figure 6.5: BL-3
>
> optPorts2 <- optimalPortfolios.fPort(marketPosterior,
```

## 权重

## 图6.5 BL3.

![](img/551ca8853d2ba8528201e7a57e5006b4_452_0.png)

```
+ constraints = "minW[1:6]=0.1", optimizer =
"minRiskPortfolio"
> optPorts2 # Output:
$priorOptimPortfolio
Title:
MV Minimum Risk Portfolio
Estimator: getPriorEstim
Solver: solveQuadprog
Optimize: minRisk
Constraints: minW

Portfolio Weights:
IBM MS DELL C JPM BAC
0.1137 0.1000 0.1000 0.1098 0.1000 0.4764

Covariance Risk Budgets:
IBM MS DELL C JPM BAC

Target Returns and Risks:
mean mu Cov Sigma CVaR VaR
0.0000 0.0157 0.0864 0.0000 0.0000

Description:
Tue Mar 22 12:12:53 2016 by user: Bert

$posteriorOptimPortfolio
Title:
MV Minimum Risk Portfolio
Estimator: getPosteriorEstim
Solver: solveQuadprog
Optimize: minRisk
Constraints: minW
```

```
Portfolio Weights:
 IBM  MS  DELL  C     JPM     BAC
 0.1000 0.1000 0.1000 0.1326 0.1000 0.4674

Covariance Risk Budgets:
 IBM  MS  DELL  C  JPM  BAC

Target Returns and Risks:
 mean  mu  Cov  Sigma  CVaR  VaR
 0.0000 0.0457 0.0000 0.0018 0.0000 0.0000

Description:
Tue Mar 22 12:12:53 2016 by user: Bert
attr(,"class")
[1] "BLOptimPortfolios"
>
> densityPlots(marketPosterior, assetSel="JPM")
> # Outputs Figure 6.6 BL-4
> dispersion(c(.376,.253,.360,.333,.360,.600,.397,.396,.578,
+ .775) / 100
+ sigma <- BCOP:::symmetricMatrix(dispersion, dim = 4)
> caps <- rep(1/4, 4)
> mu <- 2.5 * sigma %*% caps
> dim(mu) <- NULL
> marketDistribution <- mdistribution("mt", mean = mu, S =
+ sigma, df = 5)
> class(marketDistribution)
> pick <- matrix(0, ncol = 4, nrow = 1,
> dimnames = list(NULL, c("SP", "FTSE", "CAC", "DAX")))
> pick[1,"DAX"] <- 1
> viewDist <- list(distribution("unif", min = -0.02, max = 0))
> views <- COPViews(pick, viewDist = viewDist, confidences =
+ 0.2, assetNames = c("SP", "FTSE", "CAC", "DAX"))
```

![](img/551ca8853d2ba8528201e7a57e5006b4_453_0.png)

图6.6 BL-4。

![](img/551ca8853d2ba8528201e7a57e5006b4_454_0.png)

```r
> newPick <- matrix(0, 1, 2)
> dimnames(newPick) <- list(NULL, c("SP", "ETF"))
> newPick[1,] <- c(1,-1) # add a relative view
> views <- addViews(newPick)
> views <- list(distribution="norm", mean = 0.05, sd = 0.02), 0.5, views)
> marketPosterior <- COPPosterior(marketDistribution, views,
+ numSimulations = 5000)
> densityPlots(marketPosterior, assetsSelect = 4)
> # Output: Figure 6.7 BL-5
```

## 6.4.4 使用R进行投资组合优化的更多示例

### 6.4.4.1 投资组合优化示例——示例1：在CRAN中通过`PerformanceAnalytics`进行投资组合优化

R包`PerformanceAnalytics`是一个用于绩效和风险分析的计量经济学函数集合，旨在分析资产配置和投资组合优化中的非正态收益流。它主要在收益数据而非价格数据上进行测试，但大多数函数也能处理不规则的收益数据，并且越来越多的函数在可能的情况下也能处理价格数据。

`PortfolioAnalytics-package`

## 投资组合优化的数值方法

**描述** `PortfolioAnalytics`是一个R包，为具有复杂约束和目标集的组合问题提供数值解。该包旨在帮助从业者和研究人员解决反映现实应用的、具有复杂约束和目标的投资组合优化问题。

该包的目标之一是提供一个通用接口，用于指定可由任何支持的求解器（即优化方法）求解的约束和目标。目前，支持的优化方法包括：

- 随机投资组合
- 差分进化
- 粒子群优化
- 广义模拟退火
- 线性和二次规划例程

求解器可以通过`optimize.portfolio`和`optimize.portfolio.rebalancing`中的`optimize_method`参数指定。`optimize_method`参数必须是`random`、`DEoptim`、`pso`、`GenSA`、`ROI`、`quadprog`、`glpk`或`symphony`之一。关于随机投资组合的更多信息将在后面提供。差分进化算法通过`DEoptim`包实现，粒子群优化算法通过`pso`包实现，广义模拟退火通过`GenSA`包实现，线性与二次规划通过`ROI`包实现，该包充当`Rglpk`、`Rsymphony`的接口。

## 示例2

PortfolioAnalytics-package

投资组合优化的数值方法

indexes

六大经济指数

### 描述

从2000年1月31日到2009年12月31日的五个指数的月度数据。

以下是五个金融指数，以及通货膨胀因素：

- 1) 美国债券
- 2) 美国股票
- 3) 国际股票
- 4) 大宗商品
- 5) 美国短期国债
- 6) 通货膨胀因素

### 用法

```
data(indexes)
```

### 格式

CSV转换为带有月度观测数据的xts对象。

### 示例

```
data(indexes)
#preview the data
```

| 发布 | 2015-01-09 |
| 作者 | David Ardia [aut], Katharine Mullen [aut, cre], Brian Peterson [aut], Joshua Ulrich [aut], Kris Boudt [ctb] |
| 维护者 | Katharine Mullen <mullen.kate@gmail.com> |
| 错误报告 | NA |
| 许可证 | GPL-2 | GPL-3 [从: GPL (≥ 2) 扩展] |
| URL | NA |
| 需要编译 | 是 |
| 引用 | DEoptim 引用信息 |
| 材料 | README NEWS |
| 视图 | Optimization |
| CRAN 检查 | DEoptim 结果 |

它实现了差分进化算法，用于对实值参数向量的实值函数进行全局优化。

以下是该R代码的详细描述：

## DEoptim 差分进化优化

### 描述

通过差分进化算法执行进化全局优化。

### 用法

```
DEoptim(fn, lower, upper, control = DEoptim.control(), ..., fnMap=NULL)
```

### 参数

`fn`：要优化的函数（最小化）。该函数应以其第一个参数作为要优化的实值参数向量，并返回一个标量实数结果。不允许使用`NA`和`NaN`值。

`lower`、`upper`：两个向量，指定每个待优化参数的标量实值下界和上界，因此`lower`和`upper`的第i个元素适用于第i个参数。实现将在`lower`和`upper`之间搜索`fn`的全局最优/最小值。`control`：控制参数列表；参见`DEoptim.control`。`fnMap`：一个可选函数，将在每个种群创建之后、种群传递给目标函数之前运行。这允许用户施加整数/基数约束。`...`：要传递给`fn`的更多参数。

### 详情

`DEoptim`执行`fn`的优化（最小化）。

`control`参数是一个列表；详见`DEoptim.control`的帮助文件。

R的差分进化（DE）实现：`DEoptim`于2005年由David Ardia首次发布在综合R档案网络（CRAN）上。早期版本用纯R编写。自2.0-0版本（2009年发布）起，该包依赖一个C实现的DE接口，对于大多数问题，其运行速度明显快于纯R实现。C接口在许多方面类似于随《差分进化：全局优化的实用方法》一书分发的MS Visual C++ v5.0差分进化算法实现（作者为Price等人），该实现可能位于http://www.icsi.berkeley.edu/~storn/。自2.0-3版本起，C实现动态分配存储种群所需的内存，消除了对种群成员数量和可优化参数向量长度的限制。自2.2-0版本起，该包支持并行操作，因此可以使用所有可用的核心来评估目标函数。这可以通过内置的`parallel`包或`foreach`包来实现。如果需要并行操作，用户应设置`parallelType`，并确保目标函数所需的参数和包可用；详见`DEoptim.control`、下面的示例以及`sandbox`目录中的示例。

自公开以来，`DEoptim`包已被用来解决不同领域中的优化问题。

- 要对给定函数执行最大化（而非最小化），只需定义一个与要最大化的函数相反的新函数，并将`DEoptim`应用于该新函数。
- 要对`fn(x)`的参数`x`添加额外约束（除了边界约束之外），例如`x[1] + x[2]^2 < 2`，请将约束纳入要优化的函数中，例如

```
fn <- function(x) {
  if (x[1] + x[2]^2 >= 2) {
    r <- Inf
```
