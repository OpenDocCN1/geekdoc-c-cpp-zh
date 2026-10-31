
The downloaded binary packages are in
C:\\Users\\Bert\\AppData\\Local\\Temp\\RtmpUt?nvRV\\downloaded_packages
> library(FinancialMath)
> ls("package:FinancialMath")
 [1] "amort.period"      "amort.table"       "annuity.arith"
 [4] "annuity.geo"      "annuity.level"     "bear.call"
 [7] "bear.call.bls"    "bls.order1"        "bond"
[10] "bull.call"        "bull.call.bls"     "butterfly.spread"
[13] "butterfly.spread.bls" "cf.analysis"     "collar"
[16] "collar.bls"       "covered.call"      "covered.put"
[19] "forward"          "forward.prepaid"   "IRR"
[22] "NPV"              "option.call"       "option.put"
[25] "perpetuity.arith" "perpetuity.geo"    "perpetuity.level"
[28] "protective.put"   "rate.conv"         "straddle"
[31] "straddle.bls"     "strangle"           "strangle.bls"
[34] "swap.commodity"   "swap.rate"         "TVM"
[37] "yield.dollar"     "yield.time"
> straddle.bls
function (S, K, r, t, sd, position, plot = FALSE)
{
    all = list(S, K, r, t, sd, plot, position)
    if (any(lapply(all, is.null) == T))
        stop("Cannot input any variable as NULL.")
    if (any(lapply(all, length) != 1) == T)
        stop("All inputs must be of length 1.")
    num2 = list(S, K, r, t, sd)
    na.num2 = num2[which(lapply(num2, is.na) == F)]
    if (any(lapply(na.num2, is.numeric) == F))
        stop("S, K, r, t, and sd must be numeric.")
    nalist = list(S, K, r, t, sd, plot, position)
    if (any(lapply(nalist, is.na) == T))
        stop("Cannot input any variables as NA.")
    stopifnot(is.logical(plot))
    NA.Neg = array(c(S, K, r, t, sd))
    NA.Neg.Str = c("S", "K", "r", "t", "sd")
    app = apply(NA.Neg, 1, is.na)
    na.S = which(app == F & NA.Neg <= 0)
    if (length(na.S) > 0) {
errs = paste(NA.Neg.Str[na.S], collapse = " & ")
stop(cat("Error: ", errs, " must be positive real number(s).\n"))
}
na.s2 = which(app == F & NA.Neg == Inf)
if (length(na.s2) > 0) {
errs = paste(NA.Neg.Str[na.s2], collapse = " & ")
stop(cat("Error: ", errs, " cannot be infinite.\n"))
}
if (position != "long" & position != "short")
stop("Position must be either short or long.")
d1 = (log(S/K) + (r + sd^2/2) * t) / (sd * sqrt(t))
d2 = d1 - sd * sqrt(t)
callP = S * pnorm(d1) - K * exp(-r * t) * pnorm(d2)
putP = K * exp(-r * t) * pnorm(-d2) - S * pnorm(-d1)
stock = seq(0, K, length.out = 6)
stock = c(stock, round(seq(K, K * 2, length.out = 6)))
stock = unique(round(stock))
payoff = rep(0, length(stock))
profit = rep(0, length(stock))
if (position == "long") {
for (i in 1:length(stock)) {
if (stock[i] == K)
payoff[i] = 0
if (stock[i] < K)
payoff[i] = K - stock[i]
if (stock[i] > K)
payoff[i] = stock[i] - K
profit[i] = payoff[i] - (callP + putP) * exp(r * t)
}
cost = callP + putP
}
if (position == "short") {
for (i in 1:length(stock)) {
if (stock[i] == K)
payoff[i] = 0
if (stock[i] < K)
payoff[i] = stock[i] - K
if (stock[i] > K)
payoff[i] = K - stock[i]
profit[i] = payoff[i] + (callP + putP) * exp(r * t)
}
 cost = - (callP + putP)
}
if (plot == T) {
 if (position == "long") {
 lpos = "bottomright"
 m = "Purchased Straddle\nPayoff and Profit"
 }
 else {
 lpos = "topright"
 m = "Written Straddle\nPayoff and Profit"
 }
 plot(stock, profit, type = "l", xlab = "Stock Price",
 main = m, ylab = "S", ylim = c(min(profit, payoff),
 max(profit, payoff)), xaxt = "n", yaxt = "n",
 col = "steelblue", lwd = 2)
 lines(stock, payoff, lty = 2, lwd = 2, col = "firebrick")
 abline(h = 0, lty = 2, col = "gray")
 x = round(seq(min(payoff, profit), max(payoff, profit),
 length.out = 8))
 axis(2, at = x, labels = x, las = 2)
 axis(1, at = stock)
 legend(lpos, c("Profit", "Payoff"), lty = c(1, 2), col =
 c("steelblue",
 "firebrick"), lwd = c(2, 2))
}
 out1 = data.frame(stock, payoff, profit)
 names(out1) = c("Stock Price", "Payoff", "Profit")
 out2 = matrix(c(callP, putP, cost), nrow = 3)
 rownames(out2) = c("Call", "Put", "Net Cost")
 colnames(out2) = c("Premiums")
 out = list(Payoff = out1, Premiums = out2)
 return(out)
}
<environment: namespace:FinancialMath>
> straddle.bls(S=100,K=110,r=.03,t=1,sd=.2,position="short")
$Payoff
Stock Price Payoff Profit
1 0 -110 -92.136241
2 22 -88 -70.136241

## 买入跨式期权
收益与利润

![](img/551ca8853d2ba8528201e7a57e5006b4_307_0.png)

图4.18(a) 布莱克-斯科尔斯模型中的跨式期权投资。

## 4.4 在金融工程中使用R进行数据分析

在金融调查中，在准备好收集到的数据集（如3.1节所述）以进行金融分析后，第一步是将数据集输入R环境。一旦数据集被放入R环境，分析将处理数据以获得可信的结论，并可能提出明确的行动建议，以改善公共和个人数据的相关方面。接下来将介绍几种数据集输入的方法。

### 4.4.1 在R命令提示符下输入数据

数据框和数据集：对于许多金融研究者来说，数据框和数据集的术语可以互换使用。

数据集：在许多应用中，一个完整的数据集包含多个数据框，包括实际收集到的数据。

数据框：数据框的规则与之前介绍的数组和矩阵相似。然而，数据框比数组更复杂。在数组中，如果只有一个单元格是字符型，那么所有列都将是字符型。另一方面，数据框可以包含以下内容：

- 一列“IDnumber”（数值型）
- 一列“Name”（字符型）。

在数据框中：

- a) 每个变量可以有较长的变量描述，以及
- b) 因子可以有“水平”或值水平。

这些属性可以从其他软件格式（如SPSS、Stata等）的原始数据集中转换过来。它们也可以在R中创建。

### 4.4.1.1 使用EXCEL电子表格（在Windows平台上）创建用于R计算的数据框

例如，以一组典型的真实病例对照流行病学研究数据为例，考虑表B中的数据集，该数据集来自1977年在美国加利福尼亚州斯坦福大学进行的一项临床试验，旨在评估维持化疗对急性髓系白血病（AML）患者的疗效。通过化疗达到缓解状态后，进入研究的患者被随机分配到两组：

- 1) 维持组：该组接受维持化疗
- 2) 非维持组：该组不接受维持化疗，作为对照组。

该临床试验旨在确定维持化疗是否能延长至复发（即“死亡”）的时间。

步骤：（1）在Windows中创建一个名为AML.csv的急性髓系白血病（AML）数据文件
（2）将其作为数据文件AML输入到R中
（1）为R计算创建数据框
1. 使用EXCEL输入数据：
（a）打开Excel电子表格
（b）输入数据，使变量名位于Excel电子表格的第1行。
（c）将每一行数据视为研究中的一个个体。
（d）从A列开始。
2. 保存为.csv文件：
（a）点击：“文件”->“另存为”，然后在文件名框（底部上方框）中输入：AML
（b）在“保存在:”框（顶部）中，选择“本地磁盘（C:）”
然后，AML文件将保存在C:\驱动器的主目录下，但也可以选择其他目录。
在“保存类型”框（底部下方框）中，向下滚动，选择并单击CSV

（逗号分隔 = 逗号分隔值）

要使用右上角的“X”关闭Excel：单击X。

## 表B：*

AML维持治疗临床研究的数据（+表示删失值）

| 组别 | 完全缓解持续时间（周） |
|---|---|
| 1=维持组（11） | 9,13,13+,18,23,28+,31,34,45+,48,161+ } |
| 1=未删失 | |
| 0=非维持组（12） | 5,5,8,8,12,16+,23,27,30,33,43,45} |
| 0=删失（+） | |

注意：非维持组可被视为MBD***

AML临床研究数据：Tableman & Kim (2004)。 - 表B-1：23个数据点，取自Mara Tableman和Jong Sung Kim所著的《Survival Analysis Using S: Analysis of Time-to-Event Data》，由Chapman & Hall/CRC出版，Boca Raton，2004年。

癌症表观基因组以特定的DNA甲基化和染色质修饰模式为特征。介导这些变化的蛋白质由表观遗传基因编码，这里定义为DNA甲基转移酶（DNMT）、甲基-CpG结合域（MBD）蛋白、组蛋白乙酰转移酶（HAT）、组蛋白去乙酰化酶（HDAC）、组蛋白甲基转移酶（HMT）和组蛋白去甲基化酶。

- 3. 在Windows中，检查C:驱动器上是否有AML.csv文件，即C：AML
- 4. 将AML读入R：
   - （a）打开R
   - （b）使用read.csv()函数：
   - （c）实际上，也可以通过其他方式完成
- 5. 输出AML.csv文件以供检查

> aml <- read.csv("C:\\AML.csv", header = T, sep=",")
> aml <- read.csv("C:\\AML.csv")
> # Read in the AML.csv file from the C:Drive of the
> # Computer, and call it
> # aml
> aml # Outputting:
weeks group status
1 9 1 1
2 13 1 1

