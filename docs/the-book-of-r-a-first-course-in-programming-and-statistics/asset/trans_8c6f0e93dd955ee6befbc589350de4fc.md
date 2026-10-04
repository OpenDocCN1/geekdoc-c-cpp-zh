

[1] TRUE FALSE TRUE TRUE TRUE FALSE

```
$dick
[1] "g'day mate"
```

```
$harry
[,1] [,2]
[1,] 2 6
[2,] 4 8
```

对象 baz 现在包含了三个命名组件：tom, dick, harry。

```
R> names(baz)
[1] "tom" "dick" "harry"
```

如果你想重命名这些成员，可以简单地将一个长度为 3 的字符向量赋值给 `names(baz)`，就像你之前做的那样。当使用 `names` 函数时，名称始终以带引号的字符字符串提供并返回。然而，如果你在创建列表时（在 `list` 函数内部）指定名称，或者使用 `names` 提取成员，它们将是不带引号的。

## 5.1.3 嵌套

如前所述，列表的成员本身也可以是另一个列表。当这样这样嵌套列表时，跟踪任何成员的深度对于后续的子集划分或提取非常重要。请注意，你可以使用 `$` 操作符和新名称向任何现有列表添加组件。这里有一个使用之前提到的 foo 和 baz 的示例：

```
R> baz <- foo
R> baz
$tom
[1] TRUE TRUE TRUE TRUE FALSE
```

```
$dick
[1] "g'day mate"
```

```
$harry
[,1] [,2]
[1,] 2 6
[2,] 4 8
```

```
$matrix
[,1] [2]
[1,] 1 3
[2,] 2 4
```

```
$logical
[1] TRUE TRUE
```

```
$string
[1] "hello you!"
```

在这里你为列表定义了第四个组件，名为 baz。成员 baz 被赋值了整个列表。你可以通过打印新的 baz 看到，现在有三个组件。命名和索引现在是分层的，你可以使用其中一种（或将它们结合）来检索内部列表的成员。

```
R> baz$logical[1:3]
[1] TRUE FALSE
R> baz[[4]][[2]][1:3]
[1] TRUE FALSE
R> baz[[4]]$logical[1:3]
[1] TRUE FALSE
```

这些都返回了存储在第二个组件（`[[2]]））中的逻辑向量的前三个元素，该组件在列表中也被命名为 logical，而它反过来又是列表 baz 的第四个组件。只要你了解子集划分的每一层返回的是什么，就可以继续使用名称和数字索引进行子集划分。考虑这一行：子集的第一层是 `baz[[4]]`，它是一个包含三个组件的列表。第二层划分通过调用 `baz[[4]]$logical` 提取逻辑部分。该组件代表一个长度为 4 的向量，因此第三层划分通过 `baz[[4]]$logical[1:3]` 获取该向量。

列表通常用于返回各种 R 函数的输出。但在系统资源中，它们可能会迅速变成大型对象。通常建议，当你只有一种类型的数据时，应该坚持使用向量、矩阵或数组结构来记录和存储观测值。

## 练习 5.1

a. 创建一个列表，按此顺序包含：一个在 -4 到 4 之间 20 个均匀间隔数字的序列；一个按列填充的 3x3 逻辑向量矩阵 `c(F,T,T,F,T,T,F,F)`；一个包含字符串 "don" 和 "quixote" 的字符向量；以及一个包含观测值 `c("LOW","MED","LOW","MED","HIGH")` 的因子向量。然后执行以下操作：

i. 顺序提取逻辑矩阵第 2 列和第 3 列的第 2 和第 1 个原始元素。
ii. 使用 `sub` 将列表内部 'quixote' 覆盖为 'Quixote'，将 'don' 覆盖为 'Don'。然后使用新覆盖的列表成员，将控制台屏幕精确拼接为以下语句：
"Windmills! ATTACK!"
"Don Quixote"
iii. 获取从 -4 到 4 的序列中所有大于 1 的值。
iv. 使用 `which` 确定因子向量中哪些索引被分配了 "MED" 级别。

b. 创建新列表，将 (a) 中的因子作为名为 "facs" 的组件；将数值向量 `c(3,2,1,3,3,4,1,5,4)` 作为名为 "nums" 的组件；以及由 (a) 列表前三个成员组成的嵌套列表（使用列表切片来获取），名为 "oldlist"。然后执行以下操作：

i. 提取 "facs" 中对应于 "nums" 中大于或等于 3 的元素。
ii. 在列表中添加一个名为 "flags" 的新成员。该成员应该是一个长度为 6 的逻辑向量，通过对 "oldlist" 组件中逻辑矩阵第三列进行两次重复获得。
iii. 使用 "flags" 和逻辑取反运算符 `!` 提取 "num" 中对应于 FALSE 的项。
iv. 使用单个字符串 "Don Quixote" 覆盖 "oldlist" 的字符字符串向量组件。

## 5.2 数据框 (Data Frames)

数据框是 R 展示数据集最自然的方式，它包含了一个针对一个或多个变量的记录观测值集合。与列表一样，数据框对变量的数据类型没有限制；你可以存储数值数据、因子数据等。R 数据框可以被视为电子表格，其中每一行是一个观测值，每一列是一个变量。数据框是等长度向量的列表，这就是为什么它对数据分析非常有用。

## 5.2.1 构建

要从零创建数据框，请使用 `data.frame` 函数。你提供等长度的向量，如果它们的长度不等，R 将尝试循环短向量以匹配最长向量——这可能会导致错误。这里有一个示例：

```
R> baz <- data.frame(
  sequence=seq(-4, 4, length.out=20),
  matrix=matrix(c(F,T,T,F,T,T,F,F), nrow=3, ncol=3),
  quixote=c("don", "quixote"),
  sex=factor(c("LOW","MED","LOW","MED","HIGH"))
)
```

```
R> names(baz)
[1] "sequence" "matrix" "quixote" "sex"
```

```
R> baz
  sequence matrix quixote  sex
1       -4      F      don  LOW
2      -3.58      T quixote  MED
3      -3.16      T      don  LOW
4      -2.74      F quixote  MED
5      -2.32      T      don  HIGH
6      -1.89      T quixote  MED
7      -1.47      F      don  LOW
8      -1.05      T quixote  MED
9      -0.63      F      don  LOW
10     -0.21      T quixote  MED
11     0.21      F      don  LOW
12     0.63      T quixote  MED
13     1.05      F      don  LOW
14     1.47      T quixote  MED
15     1.89      F      don  HIGH
16     2.32      T quixote  MED
17     2.74      F      don  LOW
18     3.16      T quixote  MED
19     3.58      F      don  LOW
20     4.00      T quixote  MED
``` (注：由于原文示例中输出部分存在逻辑混乱或对齐不齐，译文保持了原始逻辑的对应关系)

