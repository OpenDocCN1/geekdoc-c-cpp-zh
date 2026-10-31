
## 示例
```
entries <- c(0.001005, 0.001328, -0.000579, -0.000675,
0.000121, 0.000128,
-0.000445, -0.000437, 0.001328, 0.007277, -0.001307,
-0.000610,
-0.002237, -0.000989, 0.001442,-0.001535, -0.000579,
-0.001307,
0.059852, 0.027588, 0.063497, 0.023036, 0.032967, 0.048039,
-0.000675, -0.000610, 0.027588, 0.029609, 0.026572, 0.021465,
0.020697, 0.029854, 0.000121,-0.002237, 0.063497, 0.026572,
0.102488, 0.042744, 0.039943, 0.065994, 0.000128,-0.000989,
0.023036, 0.021465, 0.042744, 0.032056, 0.019881, 0.032235,
-0.000445, 0.001442, 0.032267, 0.020697, 0.039943, 0.019881,
0.028355, 0.035064, -0.000437, -0.001535, 0.048039, 0.029854,
0.065994, 0.032235, 0.035064, 0.079958)
varcov <- matrix(entries, ncol = 8, nrow = 8)
mu <- c(0.08, 0.67, 6.41, 4.08, 7.43, 3.70, 4.80, 6.60) / 100
pick <- matrix(0, ncol = 8, nrow = 3, dimnames = list(NULL,
letters[1:8]))
pick[1,7] <- -1
pick[2,1] <- -1; pick[2,2] <- -1
pick[3, 3:6] <- c(0.9, -0.9, .1, -.1)
confidences <- c(1 / c(0.00709, 0.000141, 0.000866))
views <- BLViews(pick, c(0.0525, 0.0025, 0.02), confidences,
letters[1:8])
posterior <- posteriorEst(views, tau = 0.025, mu, varcov)
optimalPortfolios(posterior, doPlot = TRUE)
optimalPortfolios($Port(posterior, optimizer =
"tangencyPortfolio"
# An example based on one found in "Beyond Black-Litterman:
# Views on Non-normal Markets"
dispersion <-
c(.376,.253,.360,.333,.360,.600,.397,.396,.578,.775) / 1000
sigma <- BLCOP::symmetricMatrix(dispersion, dim = 4)
caps <- rep(1/4, 4)
mu <- -2.5 * sigma
dim(mu) <- NULL
marketDistribution <- mvdistribution("mt", mean = mu, S =
sigma, df = 5)
pick <- matrix(0, ncol = 4, nrow = 1, dimnames = list(NULL,
c("SP", "FTSE", "CAC", "DAX")))
pick[1,4] <- -1
vdist <- list(distribution="unif", min = -0.02, max = 0)
views <- COPViews(pick, vdist, 0.2, c("SP", "FTSE", "CAC", "DAX"))
posterior <- COPPosterior(marketDistribution, views)
optimalPortfolios <- fPort(myPosterior, spec = NULL, optimizer = "minriskPortfolio", inputData = NULL, numSimulations = 100)
## End
```

## 5 CRAN 包 PerformanceAnalytics——提供用于投资风险分析和投资组合绩效的许多有用程序。

| 包 'PerformanceAnalytics' | 2015 年 2 月 19 日 |
| 类型 | 包 |
| 标题 | 用于绩效和风险分析的计量经济学工具 |
| 版本 | 1.4.3541 |
| 日期 | 2014-09-15 04:39:58-0500 (Mon, Sep 15, 2014) |
| 描述 | 用于绩效和风险分析的计量经济学函数集合。该包旨在帮助从业人员和研究人员利用非正态收益流分析方面的最新研究。一般而言，它在常规尺度上的收益（而非价格）数据上测试最多，但大多数函数也适用于不规则收益数据，并且越来越多的函数可以在可能的情况下处理损益或价格数据 |
| 导入 | zoo |
| 依赖 | R (>= 3.0.0), xts (>= 0.9) |
| 建议 | Hmisc, MASS, quantmod, gamlss, gamlss.dist, robustbase, quantreg, gplots |
| 许可证 | GPL-2 | GPL-3 |
| 网址 | http://r-forge.r-project.org/projects/returnanalytics/ |
| 版权 | (c) 2004-2014 |
| 作者 | Brian G. Peterson [cre, aut, cph], Peter Carl [aut, cph] |

## 参数

R 一个 xts、向量、矩阵、数据框、timeSeries 或 zoo 对象，表示
资产收益
auto.grid 如果为 true，则绘制与 x
和 y 轴上的点对齐的网格
xaxis 如果为 true，则绘制 x 轴
yaxis 如果为 true，则绘制 y 轴
yaxis.right 如果为 true，则在绘图的
右侧绘制 y 轴
type 设置图表类型，与 plot 中相同
lty 设置线型，与 plot 中相同
lwd 设置线宽，与 plot 中相同
las 设置轴标签旋转，与 plot 中相同
main 设置图表标题，与 plot 中相同
ylab 设置 y 轴标签，与 plot 中相同
xlab 设置 x 轴标签，与 plot 中相同
date.format.in 允许在数据对象中指定其他日期格式，默认为 "%Y-%m-%d"
date.format 重新格式化 x 轴的日期；默认为 "%m/%y"
xlim 设置 x 轴限制，与 plot 中相同
ylim 设置 y 轴限制，与 plot 中相同
element.color 提供绘制图表元素的颜色，例如框线、轴线，
等。默认为 "darkgray"
event.lines 如果不为空，垂直线将被绘制以指示
在该时间段内发生了事件。event.lines 应为日期列表（例如，
c("09/03", "05/06"））
格式与 date.format 相同。此函数将
重新格式化的行名（日期）与 events.list 匹配，因此要获得匹配
格式必须正确。
event.labels 如果不为空且 event.lines 不为空，这将
应用文本标签列表（例如，
c("This Event", "That Event") 到绘制的垂直线。参见示例
下面。
period.areas 这些是阴影区域，由开始和结束
日期在 xts 范围的向量中描述，例如 c("1926-10::1927-11","1929-08::1933-03") 参见下面的示例。

event.color 用指定的颜色绘制 event.labels 中描述的事件

period.color 用指定的颜色绘制 period.areas 中描述的阴影区域

colorset 要使用的颜色调色板，默认为合理选择

pch 要使用的符号，另请参阅 plot

legend.loc 将图例放置在图表上的九个位置之一：bottomright、bottom、bottomleft、left、topleft、top、topright、right 或 center。

ylog TRUE/FALSE 将 y 轴设置为对数刻度，类似于 plot，默认为 FALSE

cex.axis 相对于当前 'cex' 设置用于轴注释的放大倍数，与 plot 中相同。

cex.legend 相对于当前 'cex' 设置用于调整图例大小的放大倍数。

cex.lab 相对于当前 'cex' 设置用于 x 和 y 轴标签的放大倍数。

cex.labels 相对于当前 'cex' 设置用于事件线标签的放大倍数。

cex.main 相对于当前 'cex' 设置用于图表标题的放大倍数。

major.ticks 是否绘制并标记主要刻度，默认为 'auto'

minor.ticks 是否绘制次要刻度，默认为 TRUE

grid.color 设置参考网格的颜色

grid.lty 定义网格的线型

xaxis.labels 允许对日期轴进行非日期标记，默认为 NULL

space 默认为 0

... 任何其他透传参数

作者
Peter Carl

另请参阅
plot, par, axTicksByTime

```
# These are start and end dates, formatted as xts ranges.
## http://www.nber.org/cycles.html
cycles.dates<-c("1857-06/1858-12",
"1860-10/1861-06",
"1865-04/1867-12",
"1869-06/1870-12",
"1873-10/1879-03",
"1882-03/1885-05",
"1887-03/1888-04",
"1890-07/1891-05",
"1893-01/1894-06",
"1895-12/1897-06",
"1899-06/1900-12",
"1902-09/1904-08",
"1907-05/1908-06",
"1910-01/1912-01",
"1913-01/1914-12",
"1918-08/1919-03",
"1920-01/1921-07",
"1923-05/1924-07",
"1926-10/1927-11",
"1929-08/1933-03",
"1937-05/1938-06",
"1945-02/1945-10",
"1948-11/1949-10",
"1953-07/1954-05",
"1957-08/1958-04",
"1960-04/1961-02",
"1969-12/1970-11",
"1973-11/1975-03",
"1980-01/1980-07",
"1981-07/1982-11",
"1990-07/1991-03",
"2001-03/2001-11",
"2007-12/2009-06"
)
# Event lists - FOR BEST RESULTS, KEEP THESE DATES IN ORDER
risk.dates <- c(
"Oct 87",
"Feb 94",
"Jul 97",
"Aug 98",
"Oct 98",
"Jul 00",
"Sep 01")
risk.labels <- c(
"Black Monday",
"Bond Crash",
"Asian Crisis",
"Russian Crisis",
"LTCM",
"Tech Bubble",
"Sept 11")
data(edhec)
R=edhec[, "Funds of Funds", drop=FALSE]
Return.cumulative = cumprod(1+R) - 1
chart.TimeSeries(Return.cumulative)
chart.TimeSeries(Return.cumulative, colorset = "darkblue",
legend.loc = "bottomright",
period.areas = cycles.dates,
period.color = "lightblue",
event.lines = risk.dates,
event.labels = risk.labels,
event.color = "red", lwd = 2)
```

## 练习 3 的解答：Black–Scholes 方程

3. 对于 Black–Scholes 方程 (RE-3.1)，

设

C = E f(S/E)                                    (RE-3.5)

对于某个函数 f，则

C/E = f(S/E)                                    (RE-3.6)

应用 (RE-3.5) 中所述的变量替换，将 Black–Scholes 方程 (RE-3.1) 化简为其更简单的形式：

∂C/∂t + 1/2 σ² E² ∂²C/∂E² - r E ∂C/∂E = 0      (RE-3.7)

即 (RE-3.2)。
