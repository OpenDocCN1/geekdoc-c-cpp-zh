

`scan()` 函数每次读取一个标记（token），并按指示对其进行相应处理。

示例：

假设要扫描并读取的文件中包含三元组数据（例如金融市场中每个日期对应的当日最高价和最低价）：

| 15-Oct-1987 | 2439.78 | 2345.63 |
| 16-Oct-1987 | 2396.21 | 2207.73 |
| 19-Oct-1987 | 2164.16 | 1677.55 |
| 20-Oct-1987 | 2067.47 | 1616.23 |
| 21-Oct-1987 | 2087.07 | 1951.76 |

使用一个列表来调用 `scan()`，让它期望读取一个重复出现的 3 标记序列：

```
> triplets <- scan("triples.txt", what=list(character(0),
+                     numeric(0), numeric(0)))
```

给列表元素命名后，`scan()` 会将这些名称赋给相应的数据：

```
> triplets <- scan("triples.txt",
+                  what=list(date=character(0),
+                           high=numeric(0), low=numeric(0)))
Reads 5 records.
> triplets # Outputs:
$date
[1] "15-Oct-1987" "16-Oct-1987" "19-Oct-1987" "20-Oct-1987"
"21-Oct-1987"
$high
[1] 2439.78 2396.21 2164.16 2067.47 2087.07
$low
[1] 2345.63 2207.73 1677.55 1616.23 1951.76
```

## 4.4.1.6 使用 source() 函数进行数据录入与分析

R 函数 `source()` 同样来自 CRAN 的 `base` 包。该函数从控制台或文件读取数据，并将其读入向量或列表。其用法形式如下：

```
source(file, local = FALSE, echo = verbose, print.eval = echo,
verbose = getOption("verbose"),
prompt.echo = getOption("prompt"),
max.deparse.length = 150, chdir = FALSE,
encoding = getOption("encoding"),
continue.echo = getOption("continue"),
skip.echo = 0, keep.source =
getOption("keep.source"))
```

对于存储在外部文件中的命令，例如工作目录“work”下的“commands.R”，可以使用以下命令在 R 环境中执行它们：

```
> source("command.R")
```

`source()` 函数指示 R 读取文本并执行其中的内容。因此，当有一长段或经常使用的 R 代码时，可以将其保存在文本文件中。这样可以避免重新输入代码即可再次运行，并使用 `source()` 函数读取和执行这些代码。

例如，假设 `howdy.R` 文件包含熟悉的问候语：

```
print("Hi, My Friend!")
```

然后，通过 `source()` 调用该文件，即可执行文件内容，如下面的 R 代码片段所示：

```
> source("howdy.R")
[1] "Hi, My Friend!"
```

设置 `echo=TRUE` 会在执行这些脚本行之前回显它们，并在每行前显示 R 提示符：

```
> source("howdy.R", echo=TRUE)
> print("Hi, My Friend!")
[1] "Hi, My Friend!"
```

## 4.4.1.7 使用 R 中的电子表格接口进行数据录入与分析

这种方法使用 R 的 `Utils` 包中的以下函数：

- 用于录入数据的电子表格接口

这是一种电子表格式编辑器，用于录入或编辑数据，包含以下 R 函数：

```
data.entry(..., Modes = NULL, Names = NULL)
dataentry(data, modes)
de(..., Modes = list(), Names = NULL)
```

这些 R 函数的参数为：

变量列表：目前应为数值向量或字符向量，也可以是包含此类向量的列表。

Modes 用于指定变量的模式。
Names 用于指定变量的名称。
data 数值向量和/或字符向量的列表。
modes 长度最多与 `data` 相同的列表，用于给出其中（部分）变量的模式。允许使用 `list()`。

`data.entry()` 函数会编辑现有对象，并将更改保存到原对象名。

而 `edit()` 函数也会编辑现有对象，但不会将更改保存到原对象名，因此必须将结果赋给某个对象名（即使赋回原名也可以）。要录入一个向量，需要先初始化该向量，然后调用 `data.entry()` 函数。例如：

首先进入 R 环境，并设置：

```
> x <- c(2, 4, 6, 8, 10)
> # X is initially defined as an array of 5 elements.
> x # Just checking - to make sure!
[1] 2 4 6 8 10 # x is indeed set to be an array of 5 elements
>
> data.entry(x) # Entering the Data Editor:
> # The Data Editor window pops up, and looking at the first
> # column: it is now named "x", with the first 5 rows (all on first
> # column) filled, respectively, by the numbers 2, 4, 6, 8, 10
> # One can now edit this dataset by, say, changing all the
> # entries to 2, then closing the Data Editor window, and
> # returning to the R console window:
> x
[1] 2 2 2 2 2 # x is indeed changed!
> # Thus one can change the entries for x via the Data Editor,
> # and save the changes.
```

在使用 `data.entry(x)` 和 `edit()` 进行数据录入时，存在一些限制：

- i) 使用电子表格编辑器无法录入数组和非表格形式的列表。
- ii) 使用 `edit()` 创建新的数据框时，必须指定对象名才能保存数据框。
- iii) 这不是录入数据库数据的首选方式，因为人们通常希望原始数据位于文本编辑器中，或能够直接从数据文件读入。

## 4.4.1.8 使用 R 进行金融数学计算：CRAN 的 FinancialMath 包

为了说明 R 在金融数学中的易用性，考虑一个简单的贷款偿还过程示例，例如一笔房产抵押贷款。

这里使用两个示例来计算贷款偿还过程。

**示例（A）：** 一笔 100 万美元的贷款，年利率为 2.5%，分 30 年（即 360 个月）按月等额还款。还应考虑在贷款存续期内需偿还的利率和利息总额。

```
amort.table(Loan=1000000,n=360,
            i=0.025,pf=360,plot=TRUE)
```

**示例（B）：** 示例 A 显示每月还款额为 $2,812.31。假设借款人有能力每月支付更多，例如 $5,000.00，那么这种替代还款方案会对整体还款过程产生什么影响，尤其是整个贷款存续期内需要支付的总利息？

| 字段 | 值 |
|---|---|
| 软件包 | `FinancialMath` |
| 日期 | 2016 年 12 月 16 日 |
| 类型 | 软件包 |
| 标题 | 面向精算师的金融数学 |
| 版本 | 0.1.1 |
| 作者 | [aut, cre] |
| Kameron Penn |  |
| Jack Schmidt | [aut] |
| 维护者 | Kameron Penn <kameron.penn.financialmath@gmail.com> |
| 描述 | 包含北美精算师协会和意外险精算协会《金融数学》考试所需的金融数学函数及入门级衍生工具函数，并涵盖“金融经济学模型”考试中的部分主题。 |
| 许可证 | GPL-2 |
| 编码 | UTF-8 |
| LazyData | true |
| 需要编译 | no |
| 存储库 | CRAN |
| 日期/发布时间 | 2016-12-16 22:51:34 |

amort.table **分期偿还表**

### 描述

生成一份用于还清贷款的分期偿还表，同时求解付款次数、贷款金额或每期付款金额中的一个。表中给出每个周期的付款金额、支付利息、偿还本金和贷款余额。如果 `n` 最终不是整数，还会输出大额尾付、尾款支付和最后一期常规付款。同时给出支付的总利息和总付款额。它还可以绘制每笔付款中利息占比相对于期数的图。

### 用法

```
amort.table(Loan=NA, n=NA, pmt=NA, i=0.025,
    ic=1, pf=1, plot=TRUE)
```

### 参数

- Loan 贷款金额
- n 付款次数/期数
- pmt 等额付款的金额
- i 名义利率，每年转换 ic 次
- ic 每年的利率转换频率
- pf 付款频率，即每年付款次数
- plot 指示是否绘制每笔付款中利息占比相对于期数的图

### 详细信息

有效利率：eff.i = [1 + (i/ic)]^ic - 1
j = (1 + eff.i)^(1/pf) - 1
Loan = pmt * a_nj
第 t 期期末余额：B_t = pmt * a_{n-t}j
第 t 期期末支付的利息：i_t = B_{t-1}*
第 t 期期末偿还的本金：p_t = pmt - i_t
总付款额 = pmt * n
支付的总利息 = pmt * n - Loan
若 n = n* + k，其中 n* 是整数且 0 < k < 1：
最后一期常规付款（在第 n* 期）= pmt * s_{k/j}
尾款支付（在第 n* + 1 期）= Loan * (1 + j)^{n*+1} - pmt * s_{n* j}
大额尾付（在第 n* 期）= Loan * (1 + j)^{n*} - pmt * a_{n*j} + pmt

