

# 158 R 语言编程

以下演示了如何使用 `scan` 从我们的 `group1.txt` 文件中读取数据。

```
> A <- scan("group1.txt", what = integer(0))
Read 24 items
> storage.mode(A)
[1] "integer"
> A
[1] 25 26 30 35 38 24 29 31 24 28 39 27 20 25 29 31 22 28 34 34 35 29 20 40
```

通过将其设置为 `integer(0)`，数据被作为整数型（integer）而非双精度型（double）导入。遗憾的是，

```
> A <- cbind(A[seq(1, 20, by = 4)], A[seq(2, 20, by = 4)],
+ A[seq(3, 20, by = 4]), A[seq(4, 20, by = 4)]
```

这同时也使用了附录 B 中讨论的 `scan` 和 `cbind` 函数。保留输入文件中结构的一种更直接的方法，可以通过一个与输入文件中不同列对应的类型列表来实现。对于我们的示例，其形式可能如下：

```
> A <- scan("group1.txt", what = rep(list(integer(0)),4)
Read 6 records
> A
[[1]]
[1] 25 25 31 27 31 35

[[2]]
[1] 26 34 24 20 22 29

[[3]]
[1] 30 29 28 25 28

[[4]]
[1] 38 25 29 39 34 40
```

在指定 `what` 的值时，我们使用了 R 的复制函数 `rep`。该函数的原型作用于一个 R 对象并乘以该对象复制的次数。`rep` 返回一个与参数 `x` 类型相同的对象，包含 `x` 的指定倍数的副本。对于我们的情况，使用 `rep(list(integer(0)),4)` 等同于

``````
> scan("group1.txt", what = list(integer(0), integer(0), integer(0),
+ integer(0))
```

此外，注意在此实例中 `scan` 返回的是一个列表，这意味着需要使用 `[]` 运算符来访问其组件向量。数据的矩阵形式可以通过等方式恢复：

```
> A <- cbind(A[[1]], A[[2]], A[[3]], A[[4]])
```

虽然 `scan` 每次从文件中读取一个值，但 `readLines` 函数将一次读取文件的一行。将 `readLines` 应用于 `group1.txt` 产生结果：

```
> A <- readLines("group1.txt", n = 2)
> A
[1] "25 26 30 38" "25 34 29 25"
```

# 文件输入输出

在这里，参数 `n` 决定读取的（最大）行数，设置为 2，因此只从文件中读取前两行。`readLines` 函数设计用于读取文本输入，因此将文件中的每一行作为带引号的字符字符串返回。在这种特定情况下，结果是一个双元素数组。R 有用于处理字符串的函数，可以将字符串输入转换为数值，正如我们现在所演示的那样。

我们已经讨论过 `paste` 函数，它可以将字符串和数字连接成字符串。现在需要的是此操作的反向操作；输入被读取为包含由空格分隔的整数的字符串，我们需要提取输入子字符串。这可以通过如所示的 `strsplit` 函数完成：

```
> strsplit(A, split = " ")
[[1]]
[1] "25" "26" "30" "38"

[[2]]
[1] "25" "34" "29" "25"
```

通过为 `strsplit` 指定 `split` 参数为空格，得到了预期的结果。`strsplit` 的输出以列表结构返回。要将变量列表转换为整数值，需要应用 `unlist` 函数并对整数进行强制类型转换，例如：

```
> as.integer(unlist(A[1], split = " "))
+ as.integer(unlist(A[2], split = " "))
[1] 25 26 30 38
[2] 25 34 29 25
```

然后，复制了从 `group1.txt` 文件中读取的两行。顺带提一下，值得注意的是 R 有 `nchar` 和 `substr` 函数，可以计算字符数（包括空格）并从字符串中删除子字符串。

之前的示例标志着我们第一次接触这种在 R 中无处不在的函数，它执行 R 类似于 C++ 转换的操作。这个术语是强制转换（coercion）。在 `as.*` 的应用中，R 会忽略其当前数据类型并将对象视为另一种数据类型。`as.integer` 函数是一个示例，我们用它将字符字符串转换为数值（即双精度值）。对于 `as.*` 还有许多选择，例如 `as.matrix`（它将对象强制转换为矩阵对象）和 `as.Date`（它会将字符字符串视为 Date 类），这些都是本章中将遇到的示例。带有 `as` 前缀的函数有 500 多个相关函数。也可以导入具有更“奇特”来源的文件，如附录 B 所解释，有许多附加包包含读取和写入文件的函数，如 Minitab、S+、SAS、Stata。列表中的一个遗漏是 Excel，尽管它本身不是统计软件，但对于数据的存储和处理，它是标准。直接访问 Excel 有些问题，建议改为从 Excel 提取数据。例如，Excel 表格可以保存为 `.csv`（逗号分隔值）格式，然后用 `read.table(sep = ",")` 读取。一个名为 `read.csv` 的专门版本可处理 `.csv` 文件。在 R 中创建的数据可以通过保存并重新加载附录 B 中描述的工作区来保留。结果是将工作区的数据加载到内存中，以便处理大型或巨大的数据集。一种选项是与某些数据库管理系统工作，R 包 MySQL、Oracle、SQLite、DBI 可用于此。第 9.2 节提供了另一种选项。R 的 `write.table` 输出可将数据框或矩阵输出到文本文件。例如：

```
write.table(A, "filePath")
```

写入到带有行和列标题的文本文件中的数据框或矩阵。命令是：

```
write.table(A, "filePath",col.names = FALSE,
row.names = FALSE)

A <- read.table("group2.txt",na.string = c("n"))
write.table(A, "temp.txt")
system("cat.txt")
"Sample1" "Sample2" "Sample3" "Sample4"
"Row1" 25 26 30 38
"Row2" 25 34 29 25
"Row3" 31 24 28 29
"Row4" 27 20 25 29
"Row5" 31 28 34 28
"Row6" NA 20 20
system("cat.txt")
```

这将保存行和列标记。为了方便，R 会话有这些选项的输出。`scan` 的输出通用意义上讲包括写入文件。这一功能的示例是：

```
A <- read.table("group1.txt",file = "temp.txt")
cat(matrix(A,"\n")
system("cat.txt")
```

`.txt` 文件使用 `read.table` 导入为数据框。然后，它可以写入文本文件 `temp.txt`。由于 `cat` 不能直接与列表配合，为了解释这一点，使用 `as.matrix` 函数将数据对象 `A` 转换为矩阵对象。Unix 版本的 `cat` 揭示 R cat 函数在写入文件时忽略了数据的数组结构。R cat 函数中使用换行符 `"\n"` 标志着一行的结束，因此 Unix cat 应用于 `temp.txt` 时会产生回车。

`write` 函数是（主要）在保留数组结构的同时将矩阵写入文件的 cat 方法。在我们的 `group1.txt` 示例中，使用 `write` 产生的结果如下：

```
> A <- read_table("group1.txt")
> write(t(matrix(A)), file = "temp.txt", ncols = 4)
> system("cat.txt")
25 26 30 38
25 34 29 25
31 24 28 29
27 20 25 29
31 22 28 34
35 20 40 04
```

`write` 的事实基于 `cat`，使得转转置 `as.matrix(A)`（使用 `t` 函数），以便输出文件的内容看起来像它的 R 表示。`write.table` 和 `write` 都有一个逻辑参数，默认为 `FALSE`。要写入现有文件并保留其内容，可以将 `append` 参数设置为 `TRUE`。

一个被忽略的问题是 R 为数据输出提供的精度。以最大精度写入实数。相比之下，从下面可以看出当前 R 的精度：

```
> write(cos(1:3), file = "temp.txt", col.names = FALSE,
+ row.names = FALSE)
> system("cat.txt")
0.5403203506814
-0.41614836547142
-0.98992496600425
> getOption("digits")
[7]
> write(cos(1:3), file = "temp.txt")
> system("cat.txt")
0.540320-0.4161468-0.989925
> setOption(digits = 14)
> write(cos(1:3), file = "temp.txt")
> system("cat.txt")
0.5403203506814-0.41614836547142-0.98992496600425
```

余弦在 1、2 和 3 处的值已使用 `write.table` 写入了 `file.txt`。使用 `write` 只使用了有效数字精度。这是由于 `getOptions` 函数确定当前环境的 `digits` 选项设置为 7。为了允许 `write` 的精度，可以更改当前环境的 `digits`，此处在输出中产生了 14 位精度。查看所有当前选项设置使用 `options()`。

`cat` 的使用不仅限于写入数据文件。它提供了从（例如）函数向（R）标准输出输出的一种手段，如下所示：

```
> cat("a", "b", 1:3, "
ab 2 3
```

换行符也是必要的，以便在输入行提供输入提示。注意，输出中字符中的注释被丢弃了。相比之下，可以使用 R 的 `print` 函数来给出

