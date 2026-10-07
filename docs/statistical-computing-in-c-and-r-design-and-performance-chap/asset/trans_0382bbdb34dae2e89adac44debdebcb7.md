

# 示例

25 17 21 3 10
16 8 32 6 29
22 26 7 14 12
29 16 37 26

文件中其他抽奖结果（第一行包含日期、机器和套次号）将产生 11 行文本，其中包含抽奖日的星期几（周一或周四分别标记为 M 或 T）。现在让我们假设 Guess5 游戏数据中的抽奖结果都存储为上述的格式。如果对对这些数据进行常规分析，可以通过创建一个专门处理此类类型数据的数据分析结构，从而节省时间和精力。实现这一点的的一种自然方法是构建与 Guess5 相关的类和函数，这正是我们将采取的方法。

设计过程的第一步是考虑哪些类对 Guess5 数据是有用且合适的。在表示最小数据“单元”时，可以将其视为某次抽奖的结果。为了历史目的，能够访问每次单次抽奖的信息，以及对不同时间点发生的异常抽奖进行诊断分析是至关重要的。这表明每次抽奖都有自己的“身份”，因此一个自然的起点是创建一个 Guess5 类，用于存储单次 Guess5 抽奖的信息。

在创建 Guess5 类时，我们需要考虑保留哪些抽奖结果信息。由于磨损和机器故障，结果可能会出现结构性问题。因此，可能需要查看对应于不同套次和机器的数据子。此外，抽奖日期提供了一个唯一标识符，有助于在文件中对数据进行排序和定位，这表明此类信息应该包含在内。这些考虑得出了可能构建在 Guess5 类对象中的属性“愿望清单”：

- a) Guess5 对象应该包含单次晚上抽奖的结果。
- b) 类成员应包括用于执行抽奖的抽奖机和球的套次号的标识符。其他可能的类成员可能代表抽奖的日期和星期几信息。
- c) 实际的抽奖结果（即 Guess5 抽奖和模拟实验中抽出的所有球号码）应以易于数据分析处理的形式存在；例如，矩阵形式。

一个符合我们 Guess5 抽奖结果设计指南的 R 类可以如下所示建立：

```
> setClass("g5", representation = "Date",
+ mName = "character", sNo = "integer", Day = "character",
+ data="matrix")
[1] "g5"
```

这创建了一个基础类 g5，其类成员包括抽奖日期 (drawDate)、机器名称 (mName)、球套次号 (sNo) 和星期几 (Day)。所有成员都派自 R 类。我们之前在第 5.6 节中处理过 Date 类。实际的抽奖结果将作为矩阵对象存储在槽（slot）中。

下一步是为该类创建一个构造函数。根据访问数据的方式，有多种方法。让我们假设数据以 54 元素数组的形式出现：前四个元素分别提供日期、机器名称、球套次号和星期几，接下来 50 个提供结果。适用于该场景的构造函数是：

# 在 R 中创建类和方法

```
g5 <- function(a){
  drawdate <- as.Date(a[1])
  mname <- a[2]
  sno <- as.integer(a[3])
  day <- a[4]
  A <- matrix(as.integer(a[5:50]), 10, 5, byrow = TRUE)
  g50bj <- new("g5", drawDate = drawdate, mName = mName, sno = sno,
  day = day, data = A)
}
```

输入数组的前四个元素被用于设置填充 g5 对象的 drawDate、mName 和 Slot 的值。然后，接下来的 50 个元素使用 `as.integer` 函数从字符转换为整数，并重塑为 10 x 5 矩阵。这些信息在构造函数中用于创建新对象。

将我们的 g5 构造函数应用于解析 `guess.txt` 文件中的数据产生了：

```
> a <- scan("guess.txt", what = character(0), n = 108)
Read 108 items
> g50bj1 <- g5(a[1:54]); g50bj2 <- g5(a[55:108])
> g50bj1
An object of class "g5"
Slot "drawDate"
[1] "1952-01-17"
```

```
Slot "mName"
[1] "A"
```

```
Slot "sno"
[1] 6
```

```
Slot "Day"
[1] "T"
```

```
Slot "data"
[1] [2] [3] [4] [5]
[1,] 10 38 23 20 15
[2,] 36 15 11 7 37
[3,] 20 10 9 25 2
[4,] 29 14 16 31 34
[5,] 12 38 26 2
[6,] 16 19 22 33
[7,] 25 17 21 3 10
[8,] 16 8 32 6
[9,] 22 26 7 14
[10,] 29 16 37 27
```

```
> g50bj2drawDate
[1] "1952-01-21"
```

`scan` 函数用于从 `guess.txt` 导入前两次抽奖或 108 个元素的信息。然后用 g5 构造函数处理以创建两个 g5 对象。检查这些对象是否与与第 5.6 节创建的抽奖数据一致。

# 示例

应该安装一个有效性检查函数以确保构造函数产生了有效的 g5 对象。用于该目的函数是：

```
validG5 <- function(object){
  if(object@mName != "A" & object@mName != "B")
    return(paste("Incorrect machine for date", object@drawDate))
  if(object@sNo < 1 | object@sNo > 10)
    return(paste("Incorrect set for date", object@drawDate))
  if(object@Day != "M" & object@Day != "T")
    return(paste("Incorrect day for date", object@drawDate))
  if(any(object@data < 1 | object@data > 40))
    return(paste("Incorrect ball number for date", object@drawDate))
  return(TRUE)
}
```

该函数可以通过命令 `setValidity("g5", validG5)` 检查错误输入，除非球套次、机器或星期不符合规定，否则效果将是拒绝。同样，执行一个检查以确保所有球号都在 1 到 40 之间。这种情况下的计算使用 `any` 函数执行，它接受逻辑数组作为参数，如果任何值超出 40 范围，将返回 TRUE 并打印发现错误的日期。现在我们创建了 g5 类，R 通用函数可以扩展为适用于 g5 对象。感兴趣的是 S3 函数 `summary`。我们可以使用上一节讨论的 S3 系统来定义一个适用于 g5 类的 `summary` 版本。另一个选项是将 `summary` 定义为 S4 通用函数：

```
> setGeneric("summary")
[1] "summary"
> summary
standardGeneric("summary")
function(object, ...) from "base"
standardGeneric("summary")
<environment: 0x1283c40>
Methods may be defined for arguments: object
UseMethods("summary") currently available.
```

输出的最后部分确认 `summary` 现在是一个具有相同参数 `object` 和省略号 `...` 的 S4 通用函数。用于我们目的的方法安装如下：

```
setMethod("summary", "g5", function(object){
  cat(paste("Drawings for", object@drawDate, "used Machine",
    object@mName, "Ball Set", object@sNo, "\n"))
  cat("Drawing results:\n")
  print(object@data)
}
```

对 g5 对象 `g50bj1` 的应用将产生：

```
> summary(g50bj1)
Drawings for 1952-01-17 used Machine A and Ball Set 6

```
Drawing results:
[,1] [2] [3,] [4] [5]
[1,] 10 38 23 20 15
[2,] 36 15 11 7 37
[3,] 20 10 9 25 2
[4,] 29 14 16 31 34
[5,] 12 38 26 2
[6,] 16 19 22 33
[7,] 25 17 21 3 10
[8,] 16 8 32 6
[9,] 22 26 7 14
[10,] 29 16 37 27
```

最终，我们将创建一个可以排序 g5 对象集合的函数。实现这一点的关键要素是拥有顺序关系，允许我们比较 g5 对象和另一个。对于我们的目的，结果将根据 `drawDate` 槽产生按时间顺序排序的安排。与其单独定义 `==`、`<=` 等，不如对我们之前的定义方法进行微调来同时定义所有运算符。区别在于现在方法函数将定义为名为 `Compare` 的函数组或集合。其他函数组包括在 S4 页面上描述的 `Arith`、`Logic`、`Math` 和 `Summary`。对于 `Compare`，帮助页描述组中的函数具有基本形式：

```
Compare(e1, e2)
```

因此，它们都是具有两个参数 `e1` 和 `e2` 的函数。它们所有的都可以使用以下方法扩展到 g5 类：

```
> setMethod("Compare", e1 = "g5", e2 = "g5")
+ function(e1, e2) callGeneric(e1@drawDate, e2@drawDate)
[1] "Compare"
```

这里出现的 `callGeneric` 用于方法分发；它将调用适用于实例 `Date` 类对象 `e1@drawDate` 和 `e2@drawDate` 的当前通用函数。这是足够的，因为 `Compare` 通用函数中的所有函数都有适用于 `Date` 类的方法，如 R 帮助页所示，结果如下：

```
> g50bj1 > g50bj2
[1] FALSE
> g50bj1 < g50bj2
[1] TRUE
> g50bj1 == g50bj2
[1] FALSE
> g50bj1 <= g50bj2
[1] TRUE
```

g50bj1（即 1952-01-17）早于于 `g50bj2` 的日期（即 1952-01-21）这一事实表明比较器运算符工作正常。到目前为止，重点一直放在构建单个 Guess 抽奖的对象上。在实践中，抽奖数据将包含来自多次抽奖的信息，如 `guess5.txt` 文件所示。因此，需要一个系统将 g5 对象集合封装在一个在数据分析上下文中易于使用的框架中。我们在这里开发的方法是处理原始

