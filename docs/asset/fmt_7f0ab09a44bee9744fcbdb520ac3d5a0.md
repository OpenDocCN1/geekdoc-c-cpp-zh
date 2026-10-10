
[3,] 3 6 9 12

> , 2

     [,1] [,2] [,3] [,4]

[1,] 13 16 19 22

[2,] 14 17 20 23

[3,] 15 18 21 24

> , 1

     [,1] [,2] [,3] [,4]

[1,] 1 4 7 10

[2,] 2 5 8 11

[3,] 3 6 9 12

> , 2

     [,1] [,2] [,3] [,4]

[1,] 13 16 19 22

[2,] 14 17 20 23

[3,] 15 18 21 24

> , 3

```

| [,1] [,2] [,3] [,4] |
| [1,] 1 4 7 10 |
| [2,] 2 5 8 11 |
| [3,] 3 6 9 12 |

| [,1] [,2] [,3] [,4] |
| [1,] 13 16 19 22 |
| [2,] 14 17 20 23 |
| [3,] 15 18 21 24 |

```

使用 `BR` 你有三个 `AR` 的副本。这些副本中的每一个都被拆分为其层，以便 R 可以将对象打印到屏幕上。如前所述，行由第一个数字索引，列由第二个数字索引，层由第三个数字索引。第四个数字索引块。

## 3.4.2 子集、提取和替换

即使是高维对象也可能难以概念化，R 以一致的方式索引它们。这使得提取这些结构中的元素变得简单，因为你现在知道如何子集矩阵——你只需在方括号中继续使用逗号作为访问维度的分隔符。这在以下示例中得到了突出显示。

假设你想要之前创建的数组 `AR` 的第二层的第二行。你只需输入 `AR` 的这些确切维度位置

```
AR[2,,2]

[1] 14 17 20 23
```

所需元素已作为长度为 4 的向量提取出来。如果你想要此向量的特定元素，例如第三个和第一个，按此顺序，你可以调用以下内容：

```
AR[2,c(3,1),2]

[1] 20 14
```

再次，这种字面意义的子集方法使得在 R 中处理高维对象变得可行。
导致多个向量的提取将作为返回矩阵中的列呈现。例如，要提取 `AR` 两层中的第一行，你输入以下内容：

```
AR[1,,]
     [,1] [,2]
[1,] 1 13
```

[2,] 4 16
[3,] 7 19
[4,] 10 22

返回的对象包含两个矩阵层各自的前几行。然而，它将这些向量中的每一个作为单个返回矩阵的一列返回。正如这个例子所示，当从数组中提取多个向量时，它们默认会作为列返回。这意味着提取的行不一定会作为行返回。

转向对象 `BR`，以下代码可获取位于第三个块中的三维数组的第一层矩阵的第二行第一列的单个元素。

```
R> BR[2,1,1,3]

[1] 2
```

同样，你只需查看方括号中索引的位置即可知道你要求 R 从数组中返回哪些值。以下示例突出了这一点：

```
R> BR[1,,1]

[,1] [,2]
[1,] 1 13
[2,] 4 16
[3,] 7 19
[4,] 10 22
```

这返回了第一个块的第一行的所有值。由于我在该子集 `[1,,,1]` 中将列和层索引留空，因此命令返回了该块中 `BR` 的所有列和两层的数值。

接下来，以下行返回数组 `BR` 的第二层的所有值，由三个矩阵组成：

```
R> BR[,,2]
, 1

[,1] [,2] [,3] [,4]
[1,] 13 16 19 22
[2,] 14 17 20 23
[3,] 15 18 21 24
,\, 2

[,1] [,2] [,3] [,4]
[1,] 13 16 19 22
[2,] 14 17 20 23
[3,] 15 18 21 24
```

56 Chapter 3

, , 3

```
[,1] [,2] [,3] [,4]
[1,] 13 16 19 22
[2,] 14 17 20 23
[3,] 15 18 21 24
```

这个最后的例子强调了前面提到的一个特性，即多个向量从 `AR` 返回为矩阵。总体而言，如果你的提取结果为 d 维矩阵数组，结果将是下一个更高维度的数组，d + 1。在最后一个例子中，你提取了多个（二維）矩阵，并将它们作为三维数组返回。这在下一个例子中再次得到证明：

```
R> BR[3:2,4,]
, 1

[,1] [,2]
[1,] 12 24
[2,] 11 23
```

, , 2

```
[,1] [,2]
[1,] 12 24
[2,] 11 23
```

, , 3

```
[,1] [,2]
[1,] 12 24
[2,] 11 23
```

这提取了所有层和所有数组块中第 4 列的第 3 行和第 2 行（按此顺序）的元素。请考虑以下最终示例：

```
R> BR[2,1,]
[,1] [,2] [,3]
[1,] 2 2 2
[2,] 5 5 5
[3,] 8 8 8
[4,] 11 11 11
```

你要求 R 返回存储在 `BR` 中的所有数组的第一层的整个第二行。

在高维数组中删除和覆盖元素遵循与独立向量和矩阵相同的规则。你以相同的方式指定维度位置，使用负索引进行（删除）或使用赋值运算符进行覆盖。

你可以使用 `array` 函数创建一维数组（向量）和二维数组（矩阵），你想要创建的（分别将 `dim` 参数设置为长度为 1 或 2）。请注意，尽管使用 `array` 而不是 `c` 创建的向量可能会被某些函数以不同的方式处理（请参阅帮助文件 `?array` 了解技术细节）。出于这个原因，以及为了使代码的大部分部分更易于阅读，在 R 编程中更常规的做法是使用特定的向量和矩阵创建函数 `c` 或 `matrix`。

## Exercise 3.3

- a. 创建并存储一个三维数组，具有六层 4 × 2 矩阵，用介于 4.8 和 0.1 之间的递减序列填充，长度合适。
- b. 提取并存储为新对象 (a) 的所有层中仅第二列的第四行和第一行元素，按此顺序。
- c. 使用 (b) 中形成的矩阵的第二行的四次重复来填充一个新数组，其维度为 2 × 2 × 2 × 3。
- d. 创建一个新数组，由删除 (a) 的第六层的结果组成。
- e. 用 -99 覆盖 (d) 的层 1、3 和 5 的第二列的第二行和第四行元素。

## Important Code in This Chapter

| Function/operator | Brief description | First occurrence |
|---|---|---|
| `[]` | Create a matrix | Section 3.1, p. 40 |
| `rbind` | Create a matrix (bind rows) | Section 3.1, p. 41 |
| `cbind` | Create a matrix (bind columns) | Section 3.1, p. 42 |
| `dim` | Get matrix dimensions | Section 3.1, p. 42 |
| `nrow` | Get number of rows | Section 3.3, p. 42 |
| `ncol` | Get number of columns | Section 3.1, p. 42 |
| `[ ]` | Matrix/array subsetting | Section 3.2, p. 43 |
| `diag` | Diagonal elements/identity matrix | Section 3.2, p. 44 |
| `t` | Matrix transpose | Section 3.3, p. 47 |
| `*` | Scalar multiplication | Section 3.3.3, p. 49 |
| `+` | Matrix addition/subtraction | Section 3.3.4, p. 49 |
| `%*%` | Matrix multiplication | Section 3.3.5, p. 50 |
| `solve` | Matrix inversion | Section 3.3.6, p. 51 |
| `array` | Create an array | Section 3.4.1, p. 53 |

# 4

## NON-NUMERIC VALUES

![](img/b2cfc85cbb129f60fe595a2bae074fe4_92_0.png)

到目前为止，你几乎只使用数值工作。但统计编程也需要非数值。 在本章中，我们将考虑三种重要的非数值数据类型：逻辑值、字符和因子。这些数据类型在有效使用 R 中发挥着重要作用，尤其是在我们进入第二部分复杂的 R 编程时。

### 4.1 Logical Values

逻辑值（也简单称为逻辑）基于一个简单的原则：逻辑值对象只能是 `TRUE` 或 `FALSE`。 这些可以解释为是/否、一/零、满足/不满足等。 这是一个出现在所有编程语言中的概念，逻辑值有许多重要的用途。 通常，它们表示是否满足某个条件或某个参数是否应打开或关闭。

你在使用第 2.3.2 节的 `sort` 函数和第 3.1 节的 `matrix` 函数时已经简要遇到了逻辑值。 使用 `sort` 时，`decreasing=TRUE` 返回从大到小排序的向量，而 `decreasing=FALSE` 则按相反顺序排序向量。 同样，在构造矩阵时，`byrow=TRUE` 按行填充矩阵；否则，矩阵按列填充。现在，你将更详细地查看使用逻辑的方法。

#### 4.1.1 TRUE OR FALSE?

R 中的逻辑值完全写为 `TRUE` 和 `FALSE`，但它们经常缩写为 `T` 或 `F`。 缩写版本对代码的执行没有影响，因此，例如，使用 `decreasing=T` 等同于在 `sort` 函数中使用 `decreasing=TRUE`。 （但如果你想使用这种便利，请不要创建名为 `T` 或 `F` 的对象——参见第 9.1.3 节。）

将逻辑值分配给对象与分配数值值相同。

```
R foo <- TRUE

R foo

[1] TRUE

R bar <- F

R bar

[1] FALSE
```

这给你一个值为 `TRUE` 的对象和一个值为 `FALSE` 的对象。 同样，向量可以填充逻辑值。

```
R baz <- c(T,F,F,F,T,F,T,T,T,F)

R baz

[1] TRUE FALSE FALSE TRUE TRUE TRUE TRUE FALSE TRUE FALSE

R length(x=baz)

[1] 12
```

矩阵（和其他更高维数组）可以用这些值创建。 使用之前的 `foo` 和 `baz`，你可以构造如下内容：

```
R qux <- matrix(data=baz,nrow=3,ncol=4,byrow=foo)

R qux

[1,] [2,] [3,] [4]
[1,] TRUE FALSE FALSE FALSE
[2,] TRUE FALSE TRUE TRUE
[3,] TRUE FALSE TRUE FALSE
```

#### 4.1.2 A Logical Outcome: Relational Operators

逻辑通常用于检查值之间的关系。 例如，你可能想知道某个数字是否大于预定义的阈值 `b`。 为此，使用表 4-1 中显示的标准关系运算符，它们产生逻辑值作为结果。

# Table 4-1: Relational Operators

| Operator | Interpretation |
|---|---|
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than equal to |
| `<=` | Less than equal to |

通常，这些运算符用于数值（尽管你将在第 4.2.1 节中查看一些其他可能性）。 这是一个例子：

```
R> 1==2

[1] FALSE

R> 1>2

[1] FALSE

R> (2-1)<2

[1] TRUE

R> 1!=(2+3)

[1] TRUE
```

结果应该毫不意外：1 等于 2 为 `FALSE`，2-1 大于 2 也为 `FALSE`，而 2 小于或等于 2 的结果为 `TRUE`，1 不等于 5（2+3）也为 `TRUE`。 当用于以某种方式可变的数量时，这类操作更有用，正如你很快会看到的那样。

你已经熟悉 R 在处理向量时的逐元素行为。 使用关系运算符时也适用相同的规则。 为了说明这一点，让我们首先创建两个向量并 double-check 它们的长度是否相等。

```
R foo <- c(3,2,1,4,1,2,1,-1,0,3)

R bar <- c(4,1,2,1,1,0,0,3,0,4)

R length(x=foo)==length(x=bar)

[1] TRUE
```

现在考虑以下四个评估：

```
R foo==bar

[1] FALSE FALSE FALSE FALSE TRUE FALSE FALSE FALSE TRUE FALSE

R foo>bar

[1] TRUE TRUE FALSE FALSE FALSE TRUE TRUE TRUE TRUE

R foo<=bar

[1] TRUE TRUE TRUE FALSE TRUE TRUE TRUE TRUE

R foo<=(bar+10)

[1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
```

第一行检查 `foo` 中的条目是否等于 `bar` 中对应的条目，这仅对第五个和第九个条目为真。返回的向量将为每对元素包含一个逻辑结果，因此其长度与被比较的向量相同。第二行以相同方式比较 `foo` 和 `bar`，这次检查 `foo` 中的条目是否小于 `bar` 中的条目。将此与第三次比较对比，后者询问条目是否小于或等于彼此。最后，第四行检查 `foo` 的成员是否小于或等于 `bar`，当 `bar` 的元素增加 10 时。自然地，结果全部为 `TRUE`。

向量回收也适用于逻辑值。让我们使用之前的 `foo`，并使用一个更短的向量 `baz`。

```
R baz <- foo[c(10,3)]

R baz

[1] 3 1
```

这里你创建 `baz` 为长度为 2 的向量，由 `foo` 的第 10 个和第 3 个元素组成。现在考虑以下内容：

```
R foo>baz

[1] FALSE TRUE FALSE TRUE TRUE TRUE FALSE TRUE
```

这里，`baz` 的元素被回收并与 `foo` 的 10 个元素进行比较。`foo` 的第 1 和第 2 个元素与 `baz` 的第 1 和第 2 个元素进行比较，`foo` 的第 3 和第 4 个元素与 `baz` 的第 1 和第 2 个元素进行比较，以此类推。你也可以将向量的所有值与单个值进行比较。以下是一个示例：

```
R foo<3

[1] FALSE TRUE FALSE TRUE TRUE TRUE TRUE FALSE
```

这是在 R 中处理数据集时的一种典型操作。
现在将 `foo` 和 `bar` 的内容重写为 5 × 2 列填充矩阵。

```
R foo.mat <- matrix(foo,nrow=5,ncol=2)

R foo.mat

[,1] [,2]
[1,] 3 2
[2,] 2 1
[3,] 1 -1
[4,] 4 0
[5,] 1 3

R bar.mat <- matrix(bar,nrow=5,ncol=2)

R bar.mat

[,1] [,2]
[1,] 4 0
[2,] 1 0
[3,] 2 3
[4,] 1 0
[5,] 1 4
```

这里应用相同的逐元素行为；如果比较矩阵，你会得到一个填充有逻辑值的相同大小的矩阵。

```
R foo.mat<bar.mat

[1] [2]
[1,] TRUE FALSE
[2,] FALSE FALSE
[3,] TRUE TRUE
[4,] FALSE TRUE
[5,] TRUE TRUE

R foo.mat<3

[1] [2]
[1,] FALSE TRUE
[2,] TRUE TRUE
[3,] TRUE TRUE
[4,] FALSE TRUE
[5,] FALSE TRUE
```

这种评估也适用于超过两个维度的数组。你可以使用两个有用的函数快速检查一组逻辑值：`any` 和 `all`。在检查向量时，`any` 如果向量中的任何逻辑为 `TRUE` 则返回 `TRUE`，否则返回 `FALSE`。函数 `all` 仅当所有逻辑都为 `TRUE` 时返回 `TRUE`，否则返回 `FALSE`。作为一个快速示例，让我们使用本节开头 `foo` 和 `bar` 比较的两个逻辑向量。

```
R quux <- foo==bar

R quux

[1] FALSE FALSE FALSE TRUE TRUE FALSE FALSE TRUE TRUE

R any(quux)

[1] TRUE

R all(quux)

[1] FALSE
```

这里，`quux` 包含两个 `TRUE`，其余为 `FALSE`——因此 `any` 的结果当然是 `TRUE`，但 `all` 的结果是 `FALSE`。遵循相同的规则，你会得到以下结果：

```
R quux <- foo<=(bar+10)

R quux

[1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE

R any(quux)

[1] TRUE

R> all(quux)

[1] TRUE
```
