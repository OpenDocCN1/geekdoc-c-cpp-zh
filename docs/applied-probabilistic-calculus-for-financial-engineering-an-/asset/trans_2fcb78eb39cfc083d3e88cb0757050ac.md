
```
$optim$bestval
[1] 67.46773

$optim$nfeval
[1] 402

$optim$iter
[1] 200

$member
$member$lower
par1
-50

$member$upper
par1
50

$member$bestmemit
par1
1  -25.66072
2  -15.80228
3  -15.80228
4  -15.50944
5  -15.50944
--------------------------------
198 -15.81515
199 -15.81515
200 -15.81515
$member$bestvalit

[1] 69.34871 68.83420 68.83420 67.56283 67.56283 67.56283
--------------------------------
[196] 67.46773 67.46773 67.46773 67.46773 67.46773
$member$Pop
[,1]
[1,] -15.66161
[2,] -15.66161
[3,] -15.81515
[4,] -15.66161
[5,] -15.81515
--------------------------------
[48,] -15.66162
[49,] -15.66161
[50,] -15.66161
```
```
$member$storepop
list()
attr(,"class")
[1] "DEoptim"
>
> Genrose <- function(x) {
+ ## One generalization of the Rosenbrock banana valley function
+ (n parameters)
+ n <- length(x)
+ ## make it take some time ...
+ Sys.sleep(.001)
+ 1.0 + sum (100 * (x[n-1]^2 - x[-1])^2 + (x[-1] - 1)^2)
+ }
>
> # get some run-time on simple problems
> maxIt <- 250
> n <- 5
> oneCore <- system.time (DEoptim(fn=Genrose, lower=rep(-25, n),
+ upper=rep(25, n),
+ control=list(NP=10*n, itermax=maxIt)))
Iteration: 1 bestvalit: 67180.992768 bestmemit: 0.787009
-4.017866 4.091383 -2.065631 -7.987533
Iteration: 2 bestvalit: 67180.992768 bestmemit: 0.787009
-4.017866 4.091383 -2.065631 -7.987533
Iteration: 3 bestvalit: 67180.992768 bestmemit: 0.787009
-4.017866 4.091383 -2.065631 -7.987533
Iteration: 4 bestvalit: 67180.992768 bestmemit: 0.787009
-4.017866 4.091383 -2.065631 -7.987533
Iteration: 5 bestvalit: 42308.544031 bestmemit: 0.787009
-4.017866 0.493543 -2.065631 -7.987533
------------------------------------------------
Iteration: 248 bestvalit: 1.079131 bestmemit: -1.005728
0.991545 0.993995 1.004214 1.004883
Iteration: 249 bestvalit: 1.079131 bestmemit: -1.005728
0.991545 0.993995 1.004214 1.004883
Iteration: 250 bestvalit: 1.079131 bestmemit: -1.005728
0.991545 0.993995 1.004214 1.004883
> withParallel <- system.time (DEoptim(fn=Genrose, lower=rep
(-25, n), upper=rep(25, n),
+ control=list(NP=10*n, itermax=maxIt, parallelType=1)))
Iteration: 1 bestvalit: 1036700.619060 bestmemit: 8.705266
3.108165 -7.886303 -3.630207 -7.869868
```
```
Iteration: 2 bestval: 1036700.619060 bestmemit: 8.705266
3.108165 -7.886303 -3.620207 -7.869868
Iteration: 3 bestval: 1021360.089135 bestmemit: -7.209533
-0.069988 -4.584420 -9.804176 15.312698
Iteration: 4 bestval: 312699.104689 bestmemit: -3.456957
5.659299 -6.193019 -5.52886 0.895982
Iteration: 5 bestval: 157845.822766 bestmemit: 1.055869
-5.262289 5.023291 -1.470410 -15.176823
----------------------------------------------------------------
Iteration: 248 bestval: 1.664090 bestmemit: -0.933494
0.874286 0.780743 0.630968 0.421854
Iteration: 249 bestval: 1.664090 bestmemit: -0.933494
0.874286 0.780743 0.630968 0.421854
Iteration: 250 bestval: 1.664090 bestmemit: -0.933494
0.874286 0.780743 0.630968 0.421854
> ##Compare timings
> (oneCore)
  user system elapsed
  0.00 0.00 12.58
> (withParallel)
  user system elapsed
  0.59 0.11 7.07
> ## End
```

## 6.4.4.3 投资组合优化的工作示例 -- 第 3 号 使用 CRAN 中的 `R` 代码 `PortfolioAnalytics` 进行投资组合优化

对于相当复杂的约束或目标函数，可以通过使用返回特定风险度量作为目标函数的函数来获得数值投资组合解。

该数值优化要么使用包含在包 `DEoptim` 中的微分进化优化器（参见工作示例第 3 号）执行，要么通过满足给定约束的随机生成的投资组合执行。

## 工作示例第 4 号：使用 `R` 代码 `PortfolioAnalytics` 进行投资组合优化

## `PortfolioAnalytics` 包

## 投资组合优化的数值方法

## 描述

`PortfolioAnalytics` 是一个 R 包，用于计算具有复杂约束和目标集的投资组合问题的数值解。该包的目标是帮助从业人员和研究人员解决具有反映现实世界应用的复杂约束和目标的投资组合优化问题。

该包的一个目标是提供一个通用接口来指定约束和目标，这些约束和目标可以由任何受支持的优化方法求解。受支持的优化方法包括以下内容：

- 随机投资组合
- 微分进化
- 粒子群优化
- 广义模拟退火
- 线性和二次规划例程

求解器可以通过 `optimize.portfolio` 和 `optimize.portfolio.rebalancing` 中的 optimize-method 参数指定。optimize-method 参数必须是 `random`、`DEoptim`、`pso`、`GenSA`、`ROI`、`quadprog`、`glpk` 中的一个，或使用微分进化优化器执行。

该包 `PortfolioAnalytics` 允许获得针对相当复杂的约束或目标函数的数值投资组合解。对于风险度量，可以使用返回特定风险度量作为目标函数的函数。

数值优化要么使用包含在包 `DEoptim` 中的微分进化优化器（参见工作示例第 2 号）执行，要么通过满足给定约束的随机生成的投资组合执行。

## 选定示例：

来自 `PortfolioAnalytics` 包

## 投资组合优化的数值方法

| ac.ranking | 资产排名 |
| 描述 | 从单次完整排序计算第一矩 |
| 用法 | `ac.ranking(R, order, ...)` |

## 参数

| R | 资产收益率的 xts 对象 |
| order | 预期资产收益率相对排名的索引向量，按升序排列。例如，`order = c(2, 3, 1, 4)` 表示 `R[,2] < R[,3] < R[,1] < R[,4]` 的预期收益率。 |
| ... | 任何其他透传参数 |

## 细节

该函数使用 Almgren 和 Chriss 在 Portfolios 中描述的解析近似，从单次完整排序计算估计的质心向量

```
Use Revolution R for scalability, fault tolerance and more.
http://www.revolutionanalytics.com
Loading required package: PerformanceAnalytics
Package PerformanceAnalytics (1.4.354) loaded.
Copyright (c) 2004-2014 Peter Carl and Brian G. Peterson, GPL-2
GPL-3
http://r-forge.r-project.org/projects/returnanalytics/
Attaching package: ‘PerformanceAnalytics’
The following object is masked from ‘package:graphics’:
    legend
Warning messages:
1: package ‘PortfolioAnalytics’ was built under R version 3.2.4
2: package ‘xts’ was built under R version 3.2.3
3: package ‘PerformanceAnalytics’ was built under R version 3.2.3
> ls("package:PortfolioAnalytics")
[1] "ac.ranking"                  "add.constraint"
[3] "add.objective"               "add.objective_v1"
[5] "add.objective_v2"            "add.sub.portfolio"
[7] "applyFUN"                    "black.litterman"
[9] "box_constraint"              "CCCGarch.MM"
[11] "center"                     "constrained.buckets"
[13] "centroid.complete.mc"        "centroid.sectors"
[15] "centroid.sign"               "chart.Concentration"
[17] "chart.EF.Weights"            "chart.EfficientFrontier"
[19] "chart.EfficientFrontierOverlay" "chart.GroupWeights"
[21] "chart.RiskBudget"            "chart.RiskReward"
[23] "chart.Weights"               "combine.optimizations"
[25] "combine.portfolios"          "combine.portfolios"
[27] "constrained_objective"       "constrained_objective_v1"
[29] "constrained_objective_v2"    "constraint"
[31] "constraint_ROI"              "create.EfficientFrontier"
[33] "diversification"             "diversification_constraint"
[35] "equal.weight"                "extractConstraints"
[37] "extractCoSkewness"           "extractCovariance"
[39] "extractEfficientFrontier"    "extractGroups"
[41] "extractObjectiveMeasures"    "extractStats"
[43] "extractWeights"              "factor_exposure_constraint"
[45] "fn_map"                      "generate_sequence"
[47] "group_constraint"            "H"
[49] "insert_objectives"           "inverse.volatility.weight"
[51] "is.constraint"               "is.objective"
[53] "is.portfolio"                "leverage_exposure_constraint"
[55] "meanetl.efficient.frontier"   "meanvar.efficient.frontier"
```
