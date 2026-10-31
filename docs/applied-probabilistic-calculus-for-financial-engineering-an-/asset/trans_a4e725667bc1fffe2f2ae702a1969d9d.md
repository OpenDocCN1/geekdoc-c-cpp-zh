
错误：找不到对象 'x'
>     # 当然，xs 刚刚被删除了！
> y    # 调用 y
错误：找不到对象 'y'  # 因为 ys 也已被
    # 删除了！

>
> x <- 1:10  # 让 x = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
> x
# 输出 x（仅作检查！）
[1] 1 2 3 4 5 6 7 8 9 10
> w <- 1 + sqrt(x)/2   # 是加权向量
>                     # 标准差
> dummy <- data.frame(x = x, y = x + rnorm(x)*w)
> # 创建一个包含 2 列 x 和 y 的数据框，用于检查
> dummy  # 输出数据框 dummy

|   | x | y |
|---|---|---|
|1|1|1.311612|
|2|2|4.392003|
|3|3|3.669256|
|4|4|3.345255|
|5|5|7.371759|
|6|6|-0.190287|
|7|7|10.835873|
|8|8|4.936543|
|9|9|7.901261|
|10|10|10.712029|

>
> fm <- lm(y~x, data=dummy)
> # 进行简单的线性回归
> summary(fm)  # 对 y 关于 x 进行简单的线性回归拟合，
>              # 然后检查分析并输出：
Call:
lm(formula = y ~ x, data = dummy)

Residuals:
     Min       1Q   Median       3Q      Max 
-6.0140  -0.8133  -0.0385   1.7291   4.2218 

Coefficients:
| | Estimate | Std. Error | t value | Pr(>|t|) |
|---|---|---|---|---|
|(Intercept)|1.0814|2.0604|0.525|0.6139|
|x|0.7904|0.3321|2.380|0.0445 *|

---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
Residual standard error: 3.016 on 8 degrees of freedom
Multiple R-squared: 0.4146, Adjusted R-squared: 0.3414
F-statistic: 5.665 on 1 and 8 DF,  p-value: 0.04453

|   | x | y |
|---|---|---|
|1|1|1.311612|
|2|2|4.392003|
|3|3|3.669256|
|4|4|3.345255|
|5|5|7.371759|
|6|6|-0.190287|
|7|7|10.835873|
|8|8|4.936543|
|9|9|7.901261|
|10|10|10.712029|
> fm <- lm(y~x, data=dummy)
> # 进行简单的线性回归
> summary(fm)
> # 对 y 关于 x 进行简单的线性回归拟合，
> # 然后检查分析并输出：
Call:
lm(formula = y ~ x, data = dummy)
Residuals:
    Min      1Q  Median      3Q     Max 
-6.0140 -0.8133 -0.0385 1.7291 4.2218 
Coefficients:
| | Estimate | Std. Error | t value | Pr(>|t|) |
|---|---|---|---|---|
|(Intercept)|1.0814|2.0604|0.525|0.6139|
|x|0.7904|0.3321|2.380|0.0445 *|

---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
Residual standard error: 3.016 on 8 degrees of freedom
Multiple R-squared: 0.4146,    Adjusted R-squared: 0.3414 
F-statistic: 5.665 on 1 and 8 DF,  p-value: 0.04453
> fm1 <- lm(y~x, data=dummy, weight=1/w^2)
> summary(fm1)  # 知道标准差后，
>               # 进行加权
>               # 回归并输出：
Call:
lm(formula = y ~ x, data = dummy, weights = 1/w^2)
Residuals:
    Min      1Q  Median      3Q     Max 
-2.69867 -0.46190 -0.00072 0.90031 1.83202 
Coefficients:
| | Estimate | Std. Error | t value | Pr(>|t|) |
|---|---|---|---|---|
|(Intercept)|1.2130|1.6294|0.744|0.4779|
|x|0.7668|0.3043|2.520|0.0358 *|

---
Signif. codes: 0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
Residual standard error: 1.356 on 8 degrees of freedom
Multiple R-squared: 0.4424, Adjusted R-squared: 0.3728
F-statistic: 6.348 on 1 and 8 DF, p-value: 0.03583
> attach(dummy)  # 将数据框中的列作为
> variables
> lrf <- lowess(x, y)
> plot (x, y) # 绘制标准散点图，
>             # 输出：图 4.6

![](img/551ca8853d2ba8528201e7a57e5006b4_274_0.png)

图 4.6 添加局部回归线。

> abline(0, 1, lty=3) # 添加真实回归线：
> # （截距 = 0，斜率 = 1），
> # 输出：图 4.7。

> abline(coef(fm)) # 添加未加权回归线：
> # 输出图 4.8

![](img/551ca8853d2ba8528201e7a57e5006b4_275_0.png)

**图 4.7** 添加真实回归线（截距 = 0，斜率 = 1）。

![](img/551ca8853d2ba8528201e7a57e5006b4_275_1.png)

**图 4.8** 添加未加权回归线。

## 残差与拟合值

![](img/551ca8853d2ba8528201e7a57e5006b4_277_0.png)

图 4.10 检查异方差性的标准诊断图。

## 残差 Rankit 图

![](img/551ca8853d2ba8528201e7a57e5006b4_277_1.png)

图 4.11 检查偏度、峰度和异常值的正态分数图。

> 
> rm(fm, fm1, lrf, x, dummy) # 删除这 5 个对象
> fm
错误：找不到对象 'fm'    # 已检查！
> fm1
错误：找不到对象 'fm1'    # 已检查！
> lrf
错误：找不到对象 'lrf'    # 已检查！
> x
错误：找不到对象 'x'      # 已检查！
> dummy
错误：找不到对象 'dummy'  # 检查！
# 本次练习结束！

## 4.2.2 R 环境 – 这很重要！

通过第 4.2.1 节中的第一次练习可以看出：

从技术上讲，R 是一种表达式语言，语法简单，几乎不言自明。它区分大小写，因此 x 和 X 是不同的符号，指代不同的变量。允许使用所有字母数字符号，外加 '.' 和 '_'，限制是名称必须以 '.' 或字母开头，且如果以 '.' 开头，第二字符不能是数字。命令提示符 > 表示 R 已准备好输入。

在这里输入命令供 R 处理，按 ENTER 键后执行。命令由表达式或赋值组成。当给出表达式作为命令时，它会立即求值、打印并丢弃值。赋值会求值表达式并将值传递给变量——但值不会自动打印。要打印计算值，只需在下一条命令中再次输入该变量即可。命令可通过换行或分号 (';') 分隔。多个基本命令可通过大括号 ('{' 和 '}') 组合成一个复合表达式。

注释以井号/数字符号 ('#') 开始，可几乎放在任何位置：该符号之后行尾的所有内容均为注释。注释不能用于函数定义的参数列表中或字符串内部。如果一行末尾命令不完整，R 会给出不同的提示，默认为 '+' 号。

在第二行及后续行中，继续读取输入直到命令在语法上完成。命令的结果打印到输出设备：如果结果是数组，如向量或矩阵，则

## 4.3 R 作为计算器

### 4.3.1 使用 R 进行数学运算

要学习统计分析和计算，可以先把 R 编程语言视为一个简单的计算器。

从这里开始：只需输入一个算术表达式，按 <Enter> 键，答案就会出现在下一行

> 
> 2 + 3
[1] 5
>

好！其他计算呢？例如：13 - 7，3 x 5，12 /4，7^2，√2，e^3，e^x，ln 5 = loge5，(4 + √3)(4 - √3)，(4 + i√3)(4 - i√3)，……等等。试试：

> 
> 13 - 7
[1] 6
> 3*5
[1] 15
> 12/4
[1] 3
> 7^2
[1] 49
> sqrt(2)
[1] 1.414214
> 
> exp(3)
[1] 20.08554
> 
> exp(1i*pi)  [i is used for the complex number i = √-1.]
[1] -1-0i  [This is just the famous Euler’s Identity equation: e^{iπ}+1 = 0.]
> log(5)
[1] 1.609438
> (4 + sqrt(3))*(4 - sqrt(3))
[1] 13
[Checking: (4+√3)(4-√3)=42-(√3)2=16-3=13 (Checked!)]
> (4+1i*sqrt(3))*(4-1i*sqrt(3))
[1] 19+0i [Checking: (4+1i√3)(4-1i√3)=42-(i√3)2=16-(-3)=19 (Checked!)]

*Remark:* The [1] in front of the computed result is R's way of outputting numbers. It becomes useful when the result is a long vector. The number N in the brackets [N] is the index of the first number on that line. For example, if one generated 23 random numbers from a normal distribution

> 
> x <- rnorm(23)
> x
[1] -0.5561324 0.2478934 -0.8243522 1.0697415 1.5681899
[6] -0.3396776 -0.7356282 0.7781117 1.2822569 -0.5413498
[11] 0.3348587 -0.6711245 -0.7789205 -1.1138432 -1.9582234
[16] -0.3193033 -0.1942829 0.4973501 -1.5363843 -0.3729301
[21] 0.5741554 -0.4651683 -0.2317168
> 

*Remark:* After the random numbers have been generated, there is no output until one calls for x, namely, x has become a vector with 23 elements, call that a 23-vector. The [11] on the third line of the output indicates that 0.3348587 is the 11th element in the 23-vector x. The numbers of outputs per line depends on the length of each element as well as the width of the page.

## 4.3.2 R 中值的赋值及使用向量和矩阵的计算

R 设计为动态类型语言，即在任何时候都可以更改任何变量的数据类型。例如，可以先将 x 设为数值，如迄今所做，设 x=7；接下来可以把 x 设为向量，如 x=c(1, 2, 3, 4)；然后又可以把 x 设为词对象，如 "Hi!"。请观察以下 R 环境：

> 
> x <- 7
> x
[1] 7
> x <- c(1, 2, 3, 4) # x 被赋值为 4 维向量。
> 
[1] 1 2 3 4
> x <- c("Hi!") # x 被赋值为字符字符串。
> x
[1] "Hi!"
> x <- c("Greetings & Salutations!")
> x
[1] "Greetings & Salutations!"

