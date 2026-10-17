
这建立了一个通用函数。`object1, object2, ...` 是带有省略号的通用函数的非省略号参数的数据类型。`object1, object2, ...` 是带有省略号的通用函数的非省略号参数的数据类型。这建立了一个通用函数。`setGeneric` 和 `setMethod` 的用法说明，我们最初将关注一个简单的“玩具”示例，该示例将以最少的技术细节演示这些思想。假设要在我们的 R 会话中引入一个新的双参数函数 `func`。这是通过以下命令完成的

```r
> setGeneric("func", function(object1, object2, ...)
+ standardGeneric("func"))
```

这建立了一个通用函数。`object1, object2, ...` 是带有省略号的通用函数的非省略号参数的数据类型。`object1, object2, ...` 是带有省略号的通用函数的非省略号参数的数据类型。这建立了一个通用函数。`setGeneric` 和 `setMethod` 的用法说明，我们最初将关注一个简单的“玩具”示例，该示例将以最少的技术细节演示这些思想。假设要在我们的 R 会话中引入一个新的双参数函数 `func`。这是通过以下命令完成的

```r
> setGeneric("func", function(object1, object2, ...)
+ standardGeneric("func"))
```

这建立了一个通用函数。`object1, object2, ...` 是带有省略号的通用函数的非省略号参数的数据类型。`object1, object2, ...` 是带有省略号的通用函数的非省略号参数的数据类型。这建立了一个通用函数。`setGeneric` 和 `setMethod` 的用法说明，我们最初将关注一个简单的“玩具”示例，该示例将以最少的技术细节演示这些思想。假设要在我们的 R 会话中引入一个新的双参数函数 `func`。这是通过以下命令完成的

```r
> setGeneric("func", function(object1, object2, ...)
+ standardGeneric("func"))
```

这建立了一个通用函数。`object1, object2, ...` 是带有省略号的通用函数的非省略号参数的数据类型。`object1, object2, ...` 是带有省略号的通用函数的非省略号参数的数据类型。这建立了一个通用函数。`setGeneric` 和 `setMethod` 的用法说明，我们最初将关注一个简单的“玩具”示例，该示例将以最少的技术细节演示这些思想。假设要在我们的 R 会话中引入一个新的双参数函数 `func`。这是通过以下命令完成的

```r
> setGenericGenericfunc", function(object1,,2,,
,,Generic,func
```

这建立了一个通用函数。`object1, object2, ...` 是带有省略号的通用函数的非省略号参数的数据类型。`object1, object2, ...` 是带有省略号的通用函数的非省略号参数的数据类型。这建立了一个通用函数。`setGeneric` 和 `setMethod` 的用法说明，我们最初将关注一个简单的“玩具”示例，该示例将以最少的技术细节演示这些思想。假设要在我们的 R 会话中引入一个新的双参数函数 `func`。这是通过以下命令完成的

```r
```

这建立了一个通用函数。`object1, object2, ...` 是带有省略号的通用函数的非省略号参数的数据类型。`object1, object2, ...` 是带有省略号的通用函数的非省略号参数的数据类型。这建立了一个通用函数。`setGeneric` 和 `setMethod` 的用法说明，我们最初将关注一个简单的“玩具”示例，该示例将以最少的技术细节演示这些思想。假设要在我们的 R 会话中引入一个新的双参数函数。

# 通用方法

```
Error in function (classes, fdef, mtable) :
  unable to find an inherited method for function "func"
  for signature "character", "missing"
> func("a", 2)
[1] "a" 2"
> func(2)
Error in function (classes, fdef, mtable) :
  unable to find an inherited method for function "func"
  for signature "numeric", "missing"
> func(c, 2)
[1] "missing and numeric"
> func(object2 = 2)
[1] "missing and numeric"
> setMethod("func", signature("ANY", "missing"))
+ func(object1, object2) print("ANY and missing")
[1] "func"
> func("a"
[1] "ANY and missing"
> func(2)
[1] "ANY and missing"
```

最初引入了两个额外的方法函数，其第一个参数分别为数值型、缺失或 ANY。这两个函数（以及之前任何针对 `func` 的方法函数）中没有任何一个函数的签名能够匹配只带一个参数（且隐含第二个参数缺失）的 `func` 调用，无论其值是字符型还是数值型。字符型和数值型参数的组合会导致匹配两个方法函数的签名：我们之前带有字符和数值型参数的方法，以及新的带有 ANY 和数值型参数的方法。前一个方法函数的字符和数值参数更具体，并且更紧密地（精确地）符合提供给函数的类型。因此，评估的是该函数。如果如果在 `func(, 2)` 语句中显式省略了第一个参数，则对于数值型 `object2` 数据类型，将分发带有缺失参数的方法函数；而隐式省略开头参数将不起作用并会生成错误消息。另一种选择是如 `func(object2 = 2)` 语句所示，为 `object2` 分配一个数值。最后，一个 `object1` 类为 ANY 而 `object2` 数据类型为缺失的方法函数将在 `func` 只提供一个参数时做出响应；由于提供了第一个参数的类型，`func` 的枢纽版本有足够的信息来调用适当的方法函数，该函数的签名将与第一个参数（或更广泛地说，提供给函数的参数类型）以及其他参数（在本例中仅为 `object2`）被指定为缺失相匹配。

在定义方法函数时，不需要显式指定参数；未指定的参数将被隐式分配数据类型 ANY。例如，

```
> setMethod("func", signature("ANY", "ANY")
+ func(object1, object2) print("ANY and ANY")
[1] "func"
```

以及

```
> setMethod("func", signature("ANY"))
+ func(object1) print("just ANY")
[1] "func"
```

是具有相同签名的函数。

# 210 在 R 中创建类和方法

现在让我们把学到的关于创建通用方法的知识应用到之前上一节的 `regrFit` 类中。我们的第一个示例说明将使用 S4 函数 `show`，它可以被显式或隐式地用于打印有关对象的信息。当在命令行中输入对象的名称时，它是被隐式调用的。

目前，`show` 的默认版本将应用于 `regr` 对象，该版本会为占用其槽位（slot）的对象采用适当版本的 `show`。对于大型数据集，这产生的输出可能远超需要，例如，整个 X 矩阵和响应向量都将被展示。因此，扩展 `show` 方法到 `regr` 对象以产生简洁且易于解释的输出可能是值得的。

要为 `show` 创建新方法，必须知道其父类或枢纽通用函数的参数，该函数将用于方法分发。要发现这些信息，可以在命令行中输入函数名作为部分的开头。如果该函数有 R 手册页面，这些页面也将提供参数细节。另一种选项是使用 `args` 函数，如：

```
args(show)
function(object)
NULL
```

这告诉我们 `show` 有一个命名参数。有了这些知识，为 `regr` 对象编写了一个（非常）简洁的 `show` 方法：

```
show.regr <- function(object){
cat("An object of class regr with,", ncol(object@X),
"predictors", "\n")
}
```

该方法使用了 5.2 节描述的方法进行输出。这被作为一个新方法安装了。然后，

```
+ setMethod("show", signature("regr"), show.regr)
+ regrCar
Object of class regr with 3 predictors
+ regrFit
Object of class regr with 3 predictors
```

表明 `show` 的新版本正用于 `regr` 对象。由于 `regrFit` 是 `regr` 的派生类，此版本的 `show` 也适用于 `regrFit` 对象。在某些情况下，进行回归分析时，对因变量进行转换。使用 `^` 运算符检查发现，它是 base 包中的一个 S4 函数。每当启动 R 会话时，`args` 的应用产生：

```
function(e1, e2)
```

因此，可以定义具有 `e1` 和 `e2` 参数的新方法。一个产生转换变量的 `regr` 对象的新方法是：

```
+ setMethod("-", signature("regr", "numeric"), function(e1, e2)
+ regr(e1@X, e1@y^e2)
```

现在可以用于 `regr` 或 `regrFit` 对象，如下输出显示了一个问题。尽管 `~` 运算符适用于 `regrFit` 对象，但由于 `yHat` 被删除了，可能想要一个替代版本。解决此问题的 `~` 版本通过继承来区分 `regr` 和 `regrFit` 对象，允许运算符适用于基类和派生类。有了这个新版本的 `~`，之前的计算现在将产生预期结果，例如：

```
> newRegCarFit <- regrCar*(.5)
> newRegCarFit@y
[1] 40413
```

这里提到的 `~` 运算符还有一些内容。它是 `Arith` 通用类的一部分，该类包含了算术运算符 `+`、`-`、`*`。通用泛是执行相关操作并在数学结构上可比较的集合。通过通用函数可以同时扩展所有运算符以适用于给定类的对象。我们将在下一节使用 `Compare` 通用泛来说。

`@` 和 `slot` 函数提供了访问对象槽位的方法。然而，类似于 C++ 设置，通常建议使用简单命名的访问函数。例如，我们可以为 `regr` 对象的系数创建一个访问函数：

```
> setGeneric("bHat", function(object) standardGeneric("bHat")
[1] "bHat"
> setMethod("bHat", signature = "regr", function(object) object@b)
[1] "bHat"
```

该方法同样适用于 `regr` 和 `regrFit` 对象，如下所示：

```
> bHat(regrCar)               disp wt qsec
19.777557655 -0.000127862 -5.034409167 0.926642353
> bHat(regrFit)             disp wt qsec
19.777557655 -0.000127862 -5.034409167 0.926642353
```

对我们运行示例中的系数进行检查表明，`regrCar` 可以简化为。因此，我们可能需要执行以下操作：

```
> regrCar <- c(20, 0, -5, 1)
> bHat(regrCar)
Error: could not find function "bHat-"
```

这个错误消息有点困惑，因为我们刚刚编写并成功使用了 `bHat` 访问函数。问题是我们在这里没有使用 `bHat`，而是尝试使用它的替换版本 `bHat<-`，而该版本尚未为 `regr` 类定义。这个疏忽很容易纠正：

```
> setGeneric("bHat-", function(x, value) standardGeneric("bHat-"))
```

我们使用使用代码替换方法名称：

```
> setMethod("bHat-", "regr", function(x, value)
+ {x@b <- value;}
[1] "bHat-"
```

然后，可以使用以下方式安装系数向量的替代版本：

```
> bHat(regrCar) <- c(20, 0, -5, 1)
> bHat(regrCar)
[1] 20 0 -5 1
```

`regr` 和 `regrFit` 对象其他槽位的创建访问函数是练习 6.3 的目标。

## 6.4 示例

为了结束本章讨论，我们将考虑与 5.6 节讨论的虚构 Guess5 彩票游戏对应的特定分析问题。该游戏涉及从一组编号为 1 到 40 的（虚拟）球中选择五个（虚拟）球。抽奖每周进行两次，在周一和周四，使用两台（虚拟）摇奖机（即 A 和 B 机）和（虚拟）球组（即 1 到 10 组）。每次抽样的机器和球组随机选择，并在实际抽奖前进行初步测试。

在 5.6 节中我们有一个包含 100 次 Guess5 抽奖的数据集。数据存储在 `guess5.txt` 文件中。文件中第一个抽奖如下：

```
> system("head -n 1 guess5.txt")
1952-01-17 A 6 T
10 38 23 20 15
36 15 11 7 37
20 9 25 2
29 14 16 31 34
12 38 26 2
16 19 22 26 3
```

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
