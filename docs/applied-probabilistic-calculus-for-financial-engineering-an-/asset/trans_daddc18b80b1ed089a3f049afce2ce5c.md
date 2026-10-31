
否则前一个向量保持不变。该方案的变体也已被提出。

直观上，该方案的效果是种群在搜索空间中的分布形状在大小和方向上向高适应度区域收敛。随着种群接近全局最优，分布会收缩，从而强化生成更小的差分向量。

关于 NP、F 和 CR 的选择，一般建议如下：Storn 等人（2006）指出：

> 将父代数量 NP 设为参数数量的 10 倍，选择差分权重因子 F = 0.8 和交叉常数 CR = 0.9。确保通过利用其完整的数值范围来初始化参数向量，即，如果参数允许在范围 [−100, 100] 内取值，那么从该范围内选取初始值是个好主意，而不是不必要地限制多样性。如果在优化过程中遇到误收敛，通常需要增加 NP 的值，但通常只需将 F 调整得略低于或高于 0.8 即可。如果同时增加 NP 并略微降低 F，则更有可能收敛，但通常需要更长时间，即 DE 变得更稳健（始终存在收敛速度/稳健性权衡）。

DE 对 F 的选择比对 CR 的选择敏感得多。CR 更像是一个微调元素。CR 的高值，如 CR = 1，如果收敛发生，则会带来更快的收敛。然而，有时你必须将 CR 降到 0 才能使 DE 对特定问题足够稳健。有关 DE 策略的更多细节，请参阅 Storn 和 Price（1997）以及 Price 等人（2006）。

## 作者
David Ardia, Katharine Mullen <mullen.kate@gmail.com>, Brian Peterson, and Joshua Ulrich.

## 另请参阅
DEoptim.control 用于控制参数，DEoptim-methods 用于 DEoptim 对象的方法，包括绘制结果的一些示例；optim 或 constrOptim 用于替代优化算法。

## 示例
```
## Rosenbrock Banana function
## The function has a global minimum f(x)=0 at the point (1,1).
## Note that the vector of parameters to be optimized must be the first argument of the objective function passed to
## DEoptim.
Rosenbrock <- function(x) {
n <- length(x)
## make it take some time ...
Sys.sleep(.001)
1.0 + sum (100 * (x[-n]^2 - x[-1])^2 + (x[-1] - 1)^2)
}
# get some run-time on simple problems
maxit <- 250
n <- 5
oneCore <- system.time( DEoptim(fn=Genrose, lower=rep(-25, n),
upper=rep(25, n),
control=list(NP=10*n, iterMax=maxit)))
withParallel <- system.time( DEoptim(fn=Genrose, lower=rep
(-25, n), upper=rep(25, n),
control=list(NP=10*n, iterMax=maxit, parallelType=1)))
## Compare timings
(oneCore)
(withParallel)
## End (Not run)
```

## B) DEoptim-methods

## 描述
DEoptim 对象的方法。

## 用法
```
## S3 method for class 'DEoptim'
summary(object, ...)
## S3 method for class 'DEoptim'
plot(x, plot.type = c("bestmemit", "bestvalit", "storepop"), ...)
```

## 参数
- **object**：DEoptim 类的对象；通常是调用 DEoptim 的结果。
- **x**：DEoptim 类的对象；通常是调用 DEoptim 的结果。
- **plot.type**：是否绘制每次迭代的最佳成员、每次迭代的最佳值或中间种群？
- **...**：传递给或从其他方法传递来的进一步参数。

## 细节
`DEoptim` 类的成员具有接受参数 `plot.type` 的 plot 方法。`plot.type = "bestmemit"` 会绘制代表每一代目标函数最低值的参数值。`plot.type = "bestvalit"` 绘制每一代目标函数的最佳值。`plot.type = "storepop"` 会绘制存储的种群（只有在通过适当设置 `DEoptim` 的控制参数保存这些种群时才可用）。存储中间种群使我们能够详细检查优化的进展。还存在一个 summary 方法，它返回最佳参数向量、目标函数的最佳值、优化运行的世代数以及目标函数被评估的次数。

## 备注
有关 R 包 `DEoptim` 的更多细节和示例可在 Mullen 等人（2011）以及 Ardia 等人（2011a, 2011b）中找到，或通过键入 `vignette("DEoptim")` 查看包的 vignette。请在出版物中引用该包。使用 `citation("DEoptim")`。

## 作者
David Ardia, Katharine Mullen <mullen.kate@gmail.com>, Brian Peterson, and Joshua Ulrich.

## 另请参阅
`DEoptim` 和 `DEoptim.control`.

## 示例
```
## Rosenbrock Banana function
## The function has a global minimum f(x)=0 at the point (1,1).
## Note that the vector of parameters to be optimized must be the first argument of the objective function passed to DEoptim.
Rosenbrock <- function(x) {
 x1 <- x[1]
 x2 <- x[2]
 100 * (x2 - x1 * x1)^2 + (1 - x1)^2
}
lower <- c(-10, -10)
upper <- -lower
set.seed(1234)
outDEoptim <- DEoptim(Rosenbrock, lower, upper)
## print output information
summary(outDEoptim)
## plot the best members
plot(outDEoptim, type = 'b')
## plot the best values
dev.new()
plot(outDEoptim, plot.type = "bestvalit", type = 'b', col = 'blue')
## rerun the optimization, and store intermediate populations
outDEoptim <- DEoptim(Rosenbrock, lower, upper,
DEoptim.control(itermax = 500,
storepopfrom = 1, storepopfreq = 2))
summary(outDEoptim)
## plot intermediate populations
dev.new()
plot(outDEoptim, plot.type = "storepop")
## Wild function
Wild <- function(x)
10 * sin(0.3 * x) * sin(1.3 * x^2) +
0.00001 * x^4 + 0.2 * x + 80
outDEoptim <- DEoptim(Wild, lower = -50, upper = 50,
DEoptim.control(trace = FALSE, storepopfrom = 50,
storepopfreq = 1))
plot(outDEoptim, type = 'b')
dev.new()
plot(outDEoptim, plot.type = "bestvalit", type = 'b')
## Not run:
## an example which a normal mixture model: requires package mvtnorm
library(mvtnorm)
## neg value of the density function
negPdfMix <- function(x) {
tmp <- 0.5 * dmvnorm(x, c(-3, -3)) + 0.5 * dmvnorm(x, c(3, 3))
-tmp
}
## wrapper plotting function
plotNegPdfMix <- function(x1,x2)
negPdfMix(cbind(x1, x2))
## contour plot of the mixture
x1 <- x2 <- seq(from = -10.0, to = 10.0, by = 0.1)
thexlim <- theylim <- range(x1)
z <- outer(x1, x2, FUN = plotNegPdfMix)
contour(x1, x2, z, nlevel = 20, las = 1, col = rainbow(20),
xlim = thexlim, ylim = theylim)
set.seed(1234)
outDEoptim <- DEoptim(negPdfMix, c(-10, -10), c(10, 10),
DEoptim.control(NP = 100, itermax = 100, storepopfrom = 1,
storepopfreq = 5))
## convergence plot
dev.new()
plot(outDEoptim)
## the intermediate populations indicate the bi-modality of the
## function
dev.new()
plot(outDEoptim, plot.type = "storepop")
## End(Not Run)
```

## CRAN 包 PortfolioAnalytics

## 在 R 域中：
```
> install.packages("PortfolioAnalytics")
Installing package into 'C:/Users/Bert/Documents/R/win-library/3.3'
(as 'lib' is unspecified)
--- Please select a CRAN mirror for use in this session ---
```

## 已选择一个 CRAN 镜像。
```
also installing the dependencies 'iterators', 'foreach'
> library(PortfolioAnalytics)
Attaching package: 'PerformanceAnalytics'
> ls("package:PortfolioAnalytics")
[1] "ac.ranking"           "add.constraint"       "add.objective"       "add.objective_v2"    "add.sub.portfolio"   "applyFUN"            "box_constraint"      "CCCgarch.MM"         "center"              "centroid.buckets"    "centroid.complete.mc" "centroid.sectors"    "centroid.sign"       "chart.Concentration"
```
```
function (R, order, ...) {
  if (length(order) != ncol(R))
    stop("The length of the order vector must equal the number of assets")
  nassets <- ncol(R)
  if (hasArg(max.value)) {
    max.value <- match.call(expand.dots = TRUE)$max.value
  } else {
    max.value <- median(colMeans(R))
  }
  c_hat <- scale.range(centroid(nassets), max.value)
  out <- vector("numeric", nassets)
  out[rev(order)] <- c_hat
  return(out)
}
```
```
<environment: namespace:PortfolioAnalytics>
> # Run 1
> data(edhec)
> R <- edhec[,1:4]
> ac.ranking(R, c(2, 3, 1, 4)) # Outputting:
[1] 0.01432457 -0.05000000 -0.01432457 0.05000000
> # Run 2
> data(edhec)
> R <- edhec[,1:10]
> ac.ranking(R, c(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)) # Outputting:
[1] -0.05000000 -0.032377611 -0.021216605 -0.012155458 -0.003968706
[6] 0.003968706 0.012155458 0.021216605 0.032377611 0.050000000
>
```

CRAN 包 DEoptim 投资组合优化 使用 CRAN 包：DEoptim:DEoptim-methods 用于使用 DEoptim 方法的投资组合优化。DEoptim：差分进化全局优化

## 在 R 域中：
```
> install.packages("DEoptim")
```
