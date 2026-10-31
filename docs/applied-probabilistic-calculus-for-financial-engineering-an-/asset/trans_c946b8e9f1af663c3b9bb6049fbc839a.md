
- [33] "DefaultRiskyBondVaR"
- [34] "FilterStrategyLogNormalVaR"
- [35] "FrechetES"
- [36] "FrechetESPlot2DCl"
- [37] "FrechetVaR"
- [38] "FrechetVaRPlot2DCl"
- [39] "GaussianCopulaVaR"
- [40] "GParetoES"
- [41] "GParetoMEEPlot"
- [42] "GParetoMultipleMEEPlot"
- [43] "GParetoVaR"
- [44] "GumbelCopulaVaR"
- [45] "GumbelES"
- [46] "GumbelESPlot2DCl"
- [47] "GumbelVaR"
- [48] "GumbelVaRPlot2DCl"
- [49] "HillEstimator"
- [50] "HillPlot"
- [51] "HillQuantileEstimator"
- [52] "HSES"
- [53] "HSESDPerc"
- [54] "HSESFigure"
- [55] "HSESPlot2DCl"
- [56] "HSVaR"
- [57] "HSVaRDPerc"
- [58] "HSVaRESPlot2DCl"
- [59] "HSVaRFigure"
- [60] "HSVaRPlot2DCl"
- [61] "InsuranceVaR"
- [62] "InsuranceVaRES"
- [63] "JarqueBeraBacktest"
- [64] "KernelESBoxKernel"
- [65] "KernelESEpanechnikovKernel"
- [66] "KernelESNormalKernel"
- [67] "KernelESTriangleKernel"
- [68] "KernelVaRBoxKernel"
- [69] "KernelVaREpanechnikovKernel"
- [70] "KernelVaRNormalKernel"
- [71] "KernelVaRTriangleKernel"
- [72] "KSTestStat"
- [73] "KuiperTestStat"
- [74] "LogNormalES"
- [75] "LogNormalESDPerc"
- [76] "LogNormalESFigure"
- [77] "LogNormalESPlot2DCL"
- [78] "LogNormalESPlot2DHP"
- [79] "LogNormalESPlot3D"
- [80] "LogNormalVaR"
- [81] "LogNormalVaRDPerc"
- [82] "LogNormalVaRETlPlot2DCL"
- [83] "LogNormalVaRFigure"
- [84] "LogNormalVaRPlot2DCL"
- [85] "LogNormalVaRPlot2DHP"
- [86] "LogNormalVaRPlot3D"
- [87] "LogtES"
- [88] "LogtESDPerc"
- [89] "LogtESPlot2DCL"
- [90] "LogtESPlot2DHP"
- [91] "LogtESPlot3D"
- [92] "LogtVaR"
- [93] "LogtVaRDPerc"
- [94] "LogtVaRPlot2DCL"
- [95] "LogtVaRPlot2DHP"
- [96] "LogtVaRPlot3D"
- [97] "LongBlackScholesCallVaR"
- [98] "LongBlackScholesPutVaR"
- [99] "LopezBacktest"
- [100] "MEEPlot"
- [101] "NormalES"
- [102] "NormalESConfidenceInterval"
- [103] "NormalESDPerc"
- [104] "NormalESFigure"
- [105] "NormalESHotspots"
- [106] "NormalESPlot2DCL"
- [107] "NormalESPlot2DHP"
- [108] "NormalESPlot3D"
- [109] "NormalQQPlot"
- [110] "NormalQuantileStandardError"
- [111] "NormalSpectralRiskMeasure"
- [112] "NormalVaR"
- [113] "NormalVaRConfidenceInterval"
- [114] "NormalVaRDPerc"
- [115] "NormalVaRFigure"
- [116] "NormalVaRHotspots"
- [117] "NormalVaRPlot2DCL"
- [118] "NormalVaRPlot2DHP"

## 迎接人工智能新时代

人工智能（AI）已从科幻概念演变为正在改变我们世界的现实。AI 的影响无处不在，从医疗保健到交通运输。

其核心在于，AI 是关于创造能够思考、学习和做决策的机器。但这到底意味着什么？简单来说，就是教会计算机做那些通常需要人类智能的事情。

这项技术不仅仅关乎机器人或复杂算法；它关乎让我们的生活更轻松、更高效。

## 描述

使用二叉树方法估计美式看跌期权的价格。

## Usage

```
AmericanPutPriceBinomial(stockPrice, strike, r, sigma, maturity, numberSteps)
```

## Arguments

- `stockPrice` 标的股票的价格
- `strike` 期权的行权价
- `r` 无风险利率
- `sigma` 标的股票的波动率，为年化数值
- `maturity` 期权到期期限（天）
- `numberSteps` 二叉树中的时间步数

## Value

二项式美式看跌期权价格

## Author(s)

Dinesh Acharya

## Examples

```
# Estimates the price of an American Put
AmericanPutPriceBinomial(27.2, 25, .03, .2, 60, 30)
```

In the R domain:

```
> 
> # Estimates the price of an American Put
> AmericanPutPriceBinomial(27.2, 25, .03, .2, 60, 30)
> # Outputting:
[1] 0.1413597
> # The ES (Expected Shortfall) of this American Put Option
is 0.1413597.
> 
>
```

## Worked Examples III

[9] "AmericanPutVaRBinomial" 使用二叉树估计美式香草看跌期权的预期损失（ES）。

## 描述

使用二叉树对期权定价并采用历史方法计算 VaR，来估计美式看跌期权的 VaR。

## Usage

```
AmericanPutVaRBinomial(amountInvested, stockPrice, strike, r, volatility, maturity, numberSteps, cl, hp)
```

## Arguments

- **amountInvested** 支付看跌期权的总金额。
- **stockPrice** 标的股票的价格
- **strike** 期权的行权价
- **r** 无风险利率
- **volatility** 标的股票的波动率
- **maturity** 期权到期时间（天）
- **numberSteps** 二叉模型考虑的时间步数
- **cl** 计算 VaR 的置信水平
- **hp** 期权的持有期（天）

## Value

美式看跌期权的 VaR

## Author(s)

Dinesh Acharya

In the R domain:

```
> 
> # Market Risk of American call with given parameters.
> BlackScholesCallESSim(0.20, 27.2, 25, .16, .2, .05, 60, 30,
+ .95, 30)
> Outputting:
> [1] 0.003958873
> # The Market Risk of this American Call Option is 0.003958873.
> 
```

## Review Questions and Exercises

1 对比以下三种经典投资组合配置理论使用

- i) 马科维茨模型，
- ii) Black–Litterman 模型，以及
- iii) 资本资产定价模型（CAPM）

从以下方面比较这些模型：

- a 各模型的假设
- b 这些假设的优缺点

2 关于用于资产配置和投资组合优化的 Black–Litterman 模型，

- a 陈述并讨论该模型的基本假设以及其优势和劣势；
- b 陈述并讨论针对该模型提出的改进建议。

3 Black–Scholes 方程及欧式期权看涨期权的边界条件为

∂C/∂t + ½σ²S²∂²C/∂S² + rS∂C/∂S − rC = 0 (RE-3.1)

其中
C = 看涨期权的价值 = C(S, t)，
S = 固定的行权价，
t = 时间，
r = 无风险利率，
且
σ = 标的资产的波动率。

方程（RE-3.1）是一个相当复杂的二阶偏微分方程（pde）。
可以按如下方式稍作简化：
如果 S 固定且 E 可变，证明欧式期权价格 C = C(E, t) 也满足以下偏微分方程：

∂C/∂t + ½σ²E²∂²C/∂E² − rE∂C/∂E = 0 (RE-3.2)

## As an Example:

在 pde 的分析中，通过审慎的变量变换往往可以找到有用的解。一个典型例子是经典的热/质量扩散方程，可用分离变量法求解：

∂u/∂t = c² ∂²u/∂x²  (RE-3.3)

边界条件为：

u(0, t) = 0 = u(L, t), ∀t
 u(x, 0) = f(x), ∀t = 0

初始条件：u(x, 0)=f(x)，x 的给定函数。

一种初等方法是假设独立变量 x 和 t 可分离，于是可写

u(x, t) = X(x) T(t)  (RE-3.4)

经过一些初等步骤后，可得到最终解：

u(x, t) = Σ_{n=0}^∞ B_n sin(nπ/l x) exp(-n² π² c² t / l²)

其中

B_n = (2/l) ∫_0^l f(x) sin(nπ/l x) dx, ∀ positive integers n

## 4 CRAN 包 BLCOP——实现 Black–Litterman 资产配置和投资组合优化方法：

## BLCOP：Black–Litterman 与 Copula 观点汇聚框架

对 Black–Litterman 模型和 Atilio Meucci 的 Copula 观点汇聚框架的实现。

| 版本 | 0.3.1 |
|---|---|
| 依赖 | methods, MASS, quadprog |
| 导入 | RUnit (≥ 0.4.22), timeSeries, fBasics, fMultivar, fPortfolio (≥3011.81) |
| 建议 | sn, corpcor, mnormt |
| 发布 | 2015-02-04 |
| 作者 | Francisco Gochez, Richard Chandler-Mant, Suchen Jin, Jinjing Xie |
| 维护者 | Ava Yang <ayang at mango-solutions.com> |

许可证：GPL-3
需要编译：否
材料：NEWS
CRAN 检查：BLCOP 结果

## 下载：

在 R 环境中运行以下示例：

```
optimalPortfolios
```

*在先验和后验分布下计算最优投资组合*

## 描述

这些是包装函数，用于在先验和后验收益分布下计算最优投资组合。optimalPortfolios 可与用户提供的优化函数一起使用，如果未提供，则使用 quadprog 中的 solve.QP 进行简单的 Markowitz 最小风险优化。

optimalPortfolios.fPort 是一个通用实用函数，使用 fPortfolio 包中的例程计算最优投资组合。

## Usage

```
optimalPortfolios(result, optimizer = .optimalWeights.simpleMV,
..., doPlot = TRUE, beside = TRUE)
optimalPortfolios.fPort(result, spec = NULL,
constraints = "LongOnly",
optimizer = "minriskPortfolio",
inputData = NULL,
numSimulations = BLCOptions("numSimulations"))
```

## Arguments

result BL.Result 类的对象。

optimiser 对于 optimalPortfolios，优化函数。它应接受均值向量和方差-协方差矩阵作为参数，并返回最优权重向量。对于 optimalPortfolios，是执行投资组合优化的 fPortfolio 函数的名称。
