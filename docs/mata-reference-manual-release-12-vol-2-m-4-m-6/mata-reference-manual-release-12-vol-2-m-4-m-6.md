
# Mata 参考手册：第 12 版，第 2 卷，[M-4]-[M-6]

![](img/94f0e160fb245a717f6d9189ad47298e_0_0.png)

![](img/94f0e160fb245a717f6d9189ad47298e_1_0.png)

https://archive.org/details/matareferenceman0000unse_c3u8

![](img/94f0e160fb245a717f6d9189ad47298e_2_0.png)

- `editvalue()` 编辑值 417

# vii

# viii

- `_transpose()` ................................................................................. 原地转置 876
- `transposeonly()` ............................................................ 不带共轭的转置 877
- `tunc()` ........................................................................................ 舍入为整数 879
- `uniqrows()` ................................................................................ 获取排序后的唯一值 881
- `unitcircle()` ....................................................... 包含单位圆的复向量 882
- `unlink()` ............................................................................................ 删除文件 883
- `valofexternal()` ................................................................................ 获取外部全局变量的值 884
- `Vandermonde()` ................................................................... 范德蒙德矩阵 885
- `vec()` ................................................................................ 堆叠矩阵列 887

在阅读本手册时，你会发现对其他 Stata 手册的引用。例如：

第一个示例是对第 26 章的引用，第二个是对《基础参考手册》中 `regress` 条目的引用，而第三个是对《数据管理参考手册》中 `reshape` 条目的引用。

Stata 文档中的所有手册都有一个简写符号：

关于这些手册的详细信息可以在网上找到：

http://www.stata-press.com/manuals/

| 章节 | 描述 |
| :--- | :--- |
| [M-1] | 引言与建议 |

## 描述

Mata 是一种矩阵编程语言，适用于想要交互式地执行矩阵计算的人，也适用于那些想为 Stata 添加新功能的人。

本条目描述了本手册以及自 Stata 11 版本以来的变化。

本手册分为六部分。每个部分都按字母顺序组织，但在开头有一个介绍可以帮助你快速熟悉。

如果你是 Mata 初学者，这里有一份有用的阅读列表。从这里开始阅读：

你可能会在 [M-1] 章节中找到感兴趣的内容。关于目录，请查看：

当你看到不熟悉的术语时，请查看：

## [M-0] intro — Mata 手册简介

现在你已经了解了基础，如果你感兴趣，可以深入研究 Mata 的语法：它非常密集，但 [M-2] 中的其他条目会让你感兴趣。按字母顺序查找函数。

[M-2] 中的语法总结了 [M-2] 中的内容。如果你对面向对象感兴趣，请确保使用 [M-2]。[M-2] 中的函数是关于：

| 章节 | 描述 |
| [M-6] | Mata 常用术语表 |
| [M-5] | 函数 |
| [M-6] | Mata 常用术语表 |
| [M-6] | Mata 常用术语表 |
| [M-6] | Mata 常用术语表 |
| 章节 | 描述 |
| [M-6] | Mata 常用术语表 |
| 章节 | 描述 |
| [M-6] | Mata 常用术语表 |
| [M-6] | Mata 常用术语表 |
| [M-6] | Mata 常用术语表 |
| 章节 | 描述 |
| [M-6] | Mata 常用术语表 |
| [M-4] | 函数索引与指南 |
| 章节 | 描述 |

[M-1] intro — 介绍与建议

| 介绍性 | |
| first | 介绍与第一节课程 |
| interactive | 交互式使用 Mata |
| ado | 在 ado 文件中使用 Mata |
| help | 获取在线帮助 |
| Mata 的工作原理及查找示例 | |
| how | Mata 的工作原理 |
| source | 查看源代码 |
| 特殊主题 | |
| returnedargs | 用于返回结果的函数参数 |
| naming | 关于函数和变量命名的建议 |
| limits | 限制与内存利用 |
| tolerance | 容差的使用与规范 |
| permutation | 关于排列矩阵和向量的附记 |
| LAPACK | LAPACK 代数例程 |

## 描述

本节提供了 Mata 的介绍，以及适用于所有章节的参考材料。

## 备注

本节最重要的条目是 [M-1] **first**。另请参见 [M-6] **术语表**。

Stata 命令 `putmata` 和 `getmata` 用于将数据从 Stata 移动到 Mata 以及反之；参见 [D] **putmata**。

如果想寻找 Mata 的教科书式介绍，可以考虑 Baum (2009)，特别是第 13 和第 14 章。

Baum, C. F. 2009. An Introduction to Stata Programming. College Station, TX: Stata Press.

## 另请

- [M-0] intro — Mata 手册介绍
- [D] putmata — 将 Stata 变量放入 Mata 反之亦然

[M-1] ado — 在 ado 文件中使用 Mata

## 描述

本节为 ado 文件程序员提供了关于如何有效高效使用 Mata 的建议。

## 备注

对于那些兴趣通过添加新命令来扩展 Stata 的人，Mata 并不是 ado 文件的替代品。相反，使用 Mata 的正确方法是创建 ado 文件调用的子程序。下面我们将通过以下标题讨论如何实现这一点：

- 第一个示例
- 存储 Mata 函数的位置
- 向 Mata 函数传递参数
- 将结果返回给 ado 代码
- 建议：`metastract` 的使用
- 建议：一些实用函数

## 第一个示例

我们假设 Stata 无法生成求和，并且想为 Stata 写一个新命令来报告一个变量的和。以下是我们对如何实现它的初步尝试：

```
program varsum
  version 12
  syntax varname [if] [in]
  marksample touse
  mata: calcsum("varlist", "touse")
  display as txt " sum = " as res r(sum)
end
version 12
mata:
  void calcsum(string scalar varname, string scalar touse)
  {
    real colvector x
    st_view(x, ., varname, touse)
    st_numscalar("r(sum)", colsum(x))
  }
```

在 Stata 中运行此程序将得到以下输出：

注意以下几点：

3. ado 代码调用了 Mata 函数来执行计算。
4. Mata 函数接收的参数是 Stata 数据集中两个变量名：进行计算的变量和标识要用数据子集的变量。
5. Mata 函数将结果返回在 `r()` 中，ado 代码可以从中访问该结果。

我们上面展示的大纲是一个很好的方案，尽管我们将向你展示某些替代方案，这些方案在某些问题上更好。

## 存储 Mata 函数的位置

我们的 ado 文件包含了一个 Mata 函数。你有三个选择来放置 Mata 函数：

- 1. 你可以将 Mata 函数的代码放在 ado 文件中，就像我们所做的那样。为了正常工作，你的 `.ado` 文件必须存放在 Stata 能够找到的地方。
- 2. 你可以从 ado 文件中省略 Mata 函数的代码，单独编译 Mata 函数，并将编译后的代码（目标代码）存储在名为 `.mo` 的独立文件中。你将 `.ado` 和 `.mo` 文件都放在 Stata 能够找到的地方。
- 3. 你可以从 ado 文件中省略 Mata 函数的代码，单独编译 Mata 函数，并将编译后的代码存储在 mlib 库中。在这种情况下，你的 `.ado` 文件和 mlib 库都需要放置在 Stata 能够找到的地方。

我们将向你展示如何实现这些替代方案，但在那之前，让我们考虑每个方案的优缺点：

- 将 Mata 源代码放在 `.mo` 文件是最简单且方便的。缺点是 Mata 必须将源代码编译为目标代码，这会减慢执行速度。成本很小，因为这种情况频繁发生；Mata 在加载 ado 文件时编译代码，只要 ado 文件不被删除，Stata 和 Mata 就会反复使用相同的编译代码。
- 将你的代码保存为 `.mo` 文件可以避免 Mata 编译所有代码。源代码只编译一次——在创建创建 `.mo` 文件时——之后，Stata 将使用已经编译好的副本。这里有第二个优势：Mata 函数不再是 ado 文件的私有的，你可以在其他 ado 文件中使用 `calcsum()`。`calcsum()` 将成为你可用的一个工具函数。
- 将你的 Mata 代码保存在 mlib 库中与 (2) 具有相同的优点，唯一的区别是对于 Stata 扩展来说，这种方式更方便。mlib 库允许你将许多函数放在一起。

[M-1] ado — 在 ado 文件中使用 Mata

（注：此处原文文本似乎存在重复或逻辑混乱，已根据语意尽量翻译）

# [M-1] ado — 在 ado-files 中使用 Mata 15

在所有情况下，请参见 [M-5] `st_global()`。`st_global()` 可能不是你需要的函数，但在“备注”（Remarks）部分有一个非常实用的表格，会准确地告诉你应该使用哪一个函数。另请参见 [M-4] stata 中的所有其他 Stata 接口函数。

如果你想修改内存中的 Stata 数据集，请参见 [M-5] `st_store()` 和 [M-5] `st_view()`。

## 建议：`metastract` 的使用

`metastract` 设置决定了是否可以省略声明（[M-2] 声明）；默认情况下，你可以省略。也就是说，`metastract` 是关闭的，但你可以通过输入 `mata metastract on` 将其开启；参见 [M-3] `mata set`。有些用户会这样做，而另一些则不会。现在考虑一下在 ado-file 中直接包含 Mata 源代码会发生什么。当 ado-file 加载时，`metastract` 被关闭（或者答案是关闭的），这是因为当你在 ado-file 内部包含 Mata 源代码时，即使运行 ado-file 的用户之前开启了它，在加载 ado-file 时 `metastract` 也会被临时关闭。

例如，`varum.ado` 的内容如下：

begin `varum.ado`

```mata
program varum
version 12
syntax varname [if] [in]
marksample touse
mata: calcsum("varlist", "touse")
display as txt sum = " as res r(sum)
end
version 12
mata:
void calcsum(x, varname, touse) //（注意此处缺少声明）
{
    st_view(x, varname, touse)
    st_numscalar("r(sum)", colsum(x))
}
end varum.ado
```

即使由开启了 `metastract` 的用户运行，它也能正常工作。

同样地，在 ado-file 中，你可以开启 `metastract`，而这不会影响 ado-file 加载后的设置，因此 `varum.ado` 可以写为：

# [M-1] ado — 在 ado-files 中使用 Mata

```mata
program varsum
version 12
syntax varname [if] [in]
marksample touse
mata: calscum("varlist", "touse")
display as txt " sum = " as r(sum)
end
```

begin `varsum.ado`

```mata
version 12
mata:
void set metastract on
mata: calscum(string varname, string scalar touse)
{
    real matrix x
    st_view(x, , varname, touse)
    st_numscalar("sum", colsum(x))
}
end
```

end `varsum.ado`

这不仅可以工作，而且运行 `varsum` 也不会改变用户的 `metastract` 设置。

这种对 `metastract` 的保护和恢复仅在加载 ado-file 时会执行。

## 建议：一些实用的 Meta 函数

在 `calscum()` 子程序中，我们使用了 `colsum()` 函数——参见 [M-5] `sum()`——来获取总和：

```mata
void calscum(string varname, string scalar touse)
{
    real matrix x
    st_view(x, , varname, touse)
    st_numscalar("sum", colsum(x))
}
```

我们也可以这样编写 `calscum(string varname, string scalar touse)`：

```mata
{
    real matrix x
    real scalar i, sum
    st_view(x, , varname, touse)
    sum = 0
    for (i=1; i<=rows(x); i++) sum = sum + x[i]
    st_numscalar("sum", sum)
}
```

第一种方法更好。与其构建显式循环，不如调用计算所需结果的函数。与类似 ado 类的函数不同，当不存在这些函数时，你可以使用显式循环并获得良好的代码。

我们推荐的另一组函数记录在 [M-5] `cross()`、[M-5] `crossdev()` 和 [M-5] `quadcross()` 中。

[M-1] — 在 ado-files 中使用 Mata 17

`cross()` 执行如下形式的计算：

```
X'X
X'Z
X'diag(w)X
X'diag(w)Z
```

`crossdev()` 执行如下形式的计算：

```
(X:-x)'(X:-x)
(X:-x)'(Z:-z)
(X:-x)'diag(w)(X:-x)
(X:-x)'diag(w)(Z:-z)
```

这两个函数都值得关注，因为矩阵表达式在 Mata 中编写非常简单。然而，函数速度更快、内存内存更少，有时更准确。此外，还存在高精度的版本：`quad()`。

## 另请

- [M-2] version — 版本控制
- [M-1] intro — 简介

## Title

[M-1] first — 简介与首次会话

## Description

Mata 是 Stata 的组件。它是一种矩阵编程语言，可以交互式使用，也可以作为 do-files 和 ado-files 的扩展。

# [M-1] 首次 — 介绍与首次课程

我们特意将最后一个示例写成近乎不可读的形式，仅仅是为了强调 Mata 能够解释它。

Mata 还能理解字符串，你用双引号将其括起来：

```
: "Alpha" + "Beta"
AlphaBeta
```

就像 Stata 一样，Mata 也能理解简单和复杂的双引号：

```
: "Alpha" + "Beta"
AlphaBeta
```

你可以加上复数和实数：

```
: 1+2i + 3
4+2i
```

但你不能将实数或复数加到字符串：

```
: 2 + "alpha"
type mismatch: real + string not allowed
r(3000)
```

我们得到了一个运行时错误。Mata 确实理解 `2 + "alpha"`；但它无法执行我们的请求。

# 标量、向量和矩阵

除了理解标量（无论是实数、复数还是字符串）外，Mata 还能理解矩阵、复数和字符串元素的向量和矩阵：

```
: x = (1, 2)
```

```
: x
1 2
```

| 1 | 2 |
|---|---|

`x` 现在包含行向量 (1, 2)。我们可以相加向量：

```
: x + (3, 4)
1 2
```

| 1 | 4 | 6 |
|---|---|---|

“，” 是列连接运算符；像 `(1, 2)` 这样的内容是表达式，就像 `(1 + 2)` 是一个表达式一样：



: `y = (3, 4)`

: `z = (x, y)`

: `z`

```
| 1 | 2 | 3 | 4 |
|---|---|---|---|
```

在上面的例子中，我们可以省略括号并输入 `"y = 3, 4"` 然后输入 `"z = x, y"`，就像我们可以使用 `+` 运算符一样，尽管大多数人认为向量用括号括起来更具可读性。

![](img/94f0e160fb245a717f6d9189ad47298e_36_0.png)

# [M-1] 首次 — 介绍与首次课程

`\` 是行连接运算符：

```
: a = (1 \ 2)
: a

1 1
2 2

: b = (3 \ 4)
: c = (a \ b)
: c

1 1
2 2
3 3
4 4
```

使用列连接和行连接运算符，我们可以输入矩阵：

```
: A = (1, 2 \ 3, 4)
: A

1 1 2
2 3 4
```

这些运算符的使用不仅限于标量。记住，`x` 是行向量 `(1, 2)`，`y` 是行向量 `(3, 4)`，`a` 是列向量 `(1 \ 2)`，`b` 是列向量 `(3 \ 4)`。因此，

```
: x \ y

1 2
1 1 2
2 3 4
```

```
: a, b

1 2
1 1 3
2 3 4
```

但如果尝试尝试一些毫无意义的操作，就会得到一个错误：

```
: a, x
<istmt>: 3200 conformability error
```

我们创建复数向量和矩阵就像创建实数的一样。唯一的区别在于它们的元素是复数：

```
: Z = (1 + 1i, 2 + 3i \ 3 - 2i, -1 - 1i)
: Z

1 1+1i 2+3i
2 3-2i -1-1i
```

# [M-1] 首次 — 介绍与首次课程 2

同样，我们可以创建字符串向量和矩阵，即带有字符串元素的向量和矩阵：

```
: S = ("1st element", "2nd element" \ "another row", "last element")
```

| | |
|---|---|
| 1 | 1st element elementnd element |
| 2 | another row last element |

对于，单个元素可以长达 2,147,483,647 个字符。

## 使用函数

Mata 表达式也包含函数：

```
: sqrt(4)
2

: sqrt(-4)
```

当我们请求 `-4` 的平方根时，Mata 回复 `2`。此外，`.` 可以像其他数字一样存储：

```
: findout = sqrt(-4)
: findout
```

`.` 意味着没有计算结果。对负数取平方根不是错误，对 Mata 来说，`.` 和其他数字一样，并且所有运算符都是通用的。例如，加法是这样的：

```
: 2 +
```

仍然，Mata 为 `sqrt(-4)` 产生的 `.` 会让你惊讶。Mata 表示理解复数，所以答案应该是 `2i` 吗？如果你在复平面上工作，否则 `.` 可能是更好的答案。特别是，如果你请求一个实数的平方根，你会得到一个实数。如果你请求复数的平方根，你会得到一个复数：

```
: sqrt(-4 + 0i)
2i
```

`complex` 表示 `-4 + 0i` 是复数，它恰好虚部为 `0`。因此：

```
: areal = -4
: acomplex = -4 + 0i
: sqrt(areal)
: sqrt(acomplex)

2i
```

# [M-1] 首次 — 介绍与首次课程

如果你有实标量、向量或矩阵，并想将其转换为复数，请使用 `C()` 函数。它意味着“转换为复数”：

```
sqrt(C(areal))
2i
```

`C()` 在 [M-5] 中记录。`C()` 允许一个或两个参数。对于一个参数，它转换为复数。因此类型：

```
sqrt(-4 + 2i)
.4856272+.05813i
```

或者你可以输入：

```
sqrt(-4, 2i)
.4856272+.05813i
```

顺便说一下，使用一个参数时，`C()` 也会什么都不做：

```
sqrt(C(complex))
2i
```

## 区分实值和复值

几乎无法区分实值和虚部为零的复值：

- `areal = -4`
- `acomplex = -4 + 0i`
- `areal = -4`
- `acomplex = -4`

正如你所看到的，区别是重要的：`sqrt(areal)` 是 `2`，`sqrt(acomplex)` 是 `2i`。一种解决方案是 `eltype()` 函数：

- `eltype(areal)`
  `real`
- `eltype(complex)`
  `complex`

`eltype()` 也可以用于字符串，

- `astring = "hello"`
- `eltype(astring)`
  `string`

但这主要在编程上下文中有用。

## 使用矩阵和函数

某些函数是矩阵函数：它们需要一个矩阵并返回一个矩阵。Mata 的 `invsym(X)` 就是此类函数的示例。它返回对称实矩阵 `X` 的逆矩阵：

```
: X = (7, 53, 48 \ 53, 88, 48 \ 46, 48, 63)
: Xi = invsym(X)
: Xi

[symmetric]
```

| 1 | 2 | 3 |
|---|---|---|
| .0298458083 | | |
| -.0098470272 | .0212688926 | |
| -.015549706 | -.002885675 | .0337724301 |

```
: Xi * X
```

| 1 | 2 | 3 |
|---|---|---|
| -8.67362e-17 | -8.50015e-17 | |
| -1.387738e-16 | 1 | -1.02349e-16 |
| | 1.11022e-16 |

最后一个矩阵 `Xi * X` 因为不可避免的计算舍入误差与单位矩阵略有不同。

其他函数在数学上是标量函数。`sqrt()` 是一个例子，因为它讨论 `sqrt(X)` 没有意义的（也就是说，除非我们在讨论 Cholesky 平方根分解，否则讨论 `sqrt(X)` 没有意义的。Mata 有这样的矩阵函数；参见 [M-5] **cholesky**）。

当一个函数在数学上是标量函数时，对应的 Mata 函数通常允许向量和矩阵参数，然后 Mata 函数对每个元素单独进行计算：

```
: M = (1, 2 3, 4 \ 5, 6)
: M
```

| 1 | 2 |
|---|---|
| | |
| 3 | 4 |
| 5 | 6 |

```
: S = sqrt(M)
: S
```

| 1 | 2 | 1.41421356 |
|---|---|---|
| | 1.73205081 | 2 |
| | 2.23606797 | 2.44948943 |

```
: S[1,2]
2

: S[2,1]
3
```

# [M-1] 首次 — 首次课程

当函数以这种方式返回结果时，被称为逐元素的。

## 执行逐元素计算：冒号运算符

Mata 的运算符，如 `+`（加法）和 `*`（乘法），按照你预期的方式工作。特别是，`*` 执行矩阵乘法：

```
: A*B
```

| 1 | 19 | 22 |
| 2 | 43 | 50 |

结果的第一个元素的计算方式为 `1 * 5 + 2 * 7 = 19`。

有时，你真的想要逐元素的结果。当你需要时，在运算符前面加一个冒号：`:*` 执行逐元素乘法：

```
: A:*B
```

| 1 | 5 | 12 |
| 2 | 21 | 32 |

更多信息见 [M-2] op_colon。

## 编写程序

Mata 是一门完整的编程语言：它允许你创建自己的函数：

```
: function add(a,b) return(a+b)
```

这条语句创建了一个新函数，尽管你可能希望我们这样输入它：

```
: function add(a,b)
{
    return(a+b)
}
```

因为这使得程序可以包含许多行。无论是哪种情况，一旦定义，你就可以使用该函数：

```
: add(1,2)
3

: add(1+21,4-11)
5 + 11

: add((1,2), (3,4) )
2
```

| 1 | 4 | 6 |

# [M-1] 第一 — 介绍与第一节 27

```mat
: add(x,y)
  1 2
```

| | 4 | 6 |
|---|---|---|
| 1 | 2 | 4 |
| 2 | 6 | 8 |

```mat
: add(A,A)
  1 2
```

| | 2 | 4 |
|---|---|---|
| 1 | | |
| 2 | | | |

```mat
: Z1 = (1+1i, 1+1i \ 2, 2i)
: Z2 = (1+2i, -3+3i \ 6, -2+2i)
: add(Z1, Z2)
```

| | 2 + 3i | -2 + 4i |
|---|---|---|
| 1 | | |
| 2 | 2 + 6i | -2 + 4i |

```mat
: add("Alpha")
```

| | one | three | four |
|---|---|---|---|
| 1 | Alpha | | |
| 2 | two | three | four |

当然，我们的的小函数 `add()` 并没有做任何 `+` 运算符不做的事情，但我们可以编写一个实现它的程序。下面的程序将允许我们创建 $n \times n$ 的单位矩阵：

```mat
: real matrix id(real scalar n)
{
  real scalar i
  real matrix res
  res = J(n, n, 0)
  for (i=1; i<=n; i++) {
    res[i,i] = 1
  }
  return(res)
}
```

```mat
: I3 = id(3)
```

| | 1 | 2 | 3 |
|---|---|---|---|
| 1 | 1 | 0 | 0 |
| 2 | 0 | 1 | 0 |
| 3 | 0 | 0 | 1 |

![](img/94f0e42_0.png)

# [M-1] 第一 — 介绍与第一节

程序行 `res = J(n, n, 0)` 中的 `id()` 是一个内置函数，它返回一个 $n \times n$ 矩阵，其所有元素都等于 `val`。`for (i=1; i<=n; i++)` 从 `i=1` 开始，只要 `i<=n` 就会执行大括号内的内容（将 `res[i,i]` 设置为 1），然后再次回到 `for` 部分。最后一行——`return(res)`——表示返回我们刚刚创建的矩阵。

实际上，就像 `add()` 一样，我们不需要 `id()`，因为 Mata 有一个内置函数 `J()` 可以创建单位矩阵，但观察它是如何编程的非常有趣。

## 更多函数

Mata 在本手册中已经准备了一些函数，并说明了它们的功能；请参见 [M-1] 介绍。但现在重要的是，许多函数本身就是用 Mata 编写的！其中一个函数是 `pi()`；它不接受参数并返回 `pi` 的值。它的代码如下：

```mat
: pi()
3.141592653589793284623
```

没有理由输入上述函数，因为它已经作为 Mata 的一部分包含了：

当 Mata 列出结果时，显示的数字位数不多，但我们可以请求查看更多：

```mat
: printf("%7.10g", pi())
3.141592654
```

其他函数包括双曲函数 `tanh(u)`。`tanh(u)` 的代码为：

```mat
numeric matrix tanh(numeric matrix u)
{
  numeric matrix eu, emu
  eu = exp(u)
  emu = exp(-u)
  return((eu-emu))
}
```

在 Mata 提示符（而不是 Stata 提示符）输入：

```mat
: viewsource tanh
```

你会看到 `tanh` 的代码（注：此处的原文示例中代码块位置似乎错位，翻译时已根据逻辑进行了对齐）。

当一个函数的代码是在 Mata 中编写时（而不是用 C 语言编写的），`viewsource` 可以显示其代码；参见 [M-1] 源码。

# [M-1] 第一 — 介绍与第一节

回到函数 `tanh()`，

```mat
numeric matrix tanh(numeric matrix u)
{
    numeric matrix eu, emu
    eu = exp(u)
    emu = exp(-u)
    return ((eu-emu))
}
```

这是我们第一次看到这个词：意味着实数或复数。内置的（之前编写的）函数 `exp()` 类似于 `sqrt()`，允许实数或复数参数并相应地返回实数或复数结果。在 Mata 术语中：`exp()` 允许数值参数并返回数值结果。`tanh()` 与 `sqrt()` 和 `exp()` 共享另一个特征是：`exp()` 是逐元素操作。`tanh()` 是逐元素的，且我们小心地使用了 `./`（逐元素除法运算符）。

在任何情况下，都不需要输入函数，因为它们已经是 Mata 的一部分。你可以通过查看手册来获取更多关于它们的信息。

在另一种情况下，Mata 函数可能会很长。这里是 Mata 当 $A$ 为下三角时求解 $AX = B$ 的函数，将结果 $X$ 放回 $A$：

```mat
real scalar _solver(numeric matrix A, numeric matrix b,
real scalar usertol, numeric user)
{
    real scalar tol, rank, a_t, b_t, d_t
    real scalar n, m, i1, complex_case
    numeric rowvector sum
    numeric scalar zero, d

    d = ((n=rows(A))=cols(A)) _error(3205)
    if (n != rows(b))       _error(3200)
    if (isview(b))          _error(3104)
    m = cols(b)
    rank = n

    a_t = iscomplex(A)
    b_t = iscomplex(b)
    d_t = d.< iscomplex(d)

    complex_case = a_t | b_t | d_t

    if (complex_case) {
        if (!a_t) A = C(A)
        if (!b_t) b = C(b)
        if (d.< d_t) d = C(d)
        zero = 0
    } else {
        zero = 0
    }

    if (n==0 | m==0) return(0)
    tol = solve(A, usertol)
    if (abs(d) >= tol) {
        if (abs(d[1,1])<=tol) {
            b[1..] = J(1, m, zero)
            --rank
        } else {
            b[1..] = b[1..]./d
            if (missing(d)) rank = n
        }
    }
    for (i=2; i<=n; i++) {
        im1 = i - 1
        sum = A[i,im1,im1] * b[1,1,im1,m]
        if (abs(d[i,1])<=tol) {
            b[1..] = J(1, m, zero)
            --rank
        } else {
            b[1..] = (b[1..]-sum)../d
            if (missing(d)) rank = n
        }
    }
    if (abs(d)<=tol) {
        rank = 0
        b = J(rows(b), cols(b), zero)
    } else {
        b[1..] = b[1.../d
        for (i=2; i<=n; i++) {
            im1 = i - 1
            sum = A[i,im1,im1] * b[1,1,im1,m]
            b[i..] = (b[i..]-sum)../d
        }
    }
    return(rank)
}
```

如果该函数不是 Mata 的一部分，且你想使用它，可以将其输入到 `.ado` 文件或 `.ado` 文件的末尾（特别是如果你只是想将 `_solver()` 作为子程序使用）。在这些情况下，不要忘记进入和退出 Mata：

```mat
program mycommand
...
此处出现 do 文件
...
end

mata:
  此处出现 _solver() 代码
end
```

结束 ado 文件

敏锐的读者会注意到我们在 Mata 命令的末尾加了一个冒号。这是一个细节，这也是为什么我们说它在 [M-3] mata 中解释过。除了通过将代码放在 `.do` 和 `.ado` 文件中加载函数外，你还可以将函数的编译版本保存到 `.mo` 文件中（参见 [M-3] mata mosave）或保存到 `.mlib` 库中（参见 [M-3] mata mlib）。

`_solver()` 已经保存到 Mata 库中，你不需要它。

## Mata 环境



当你使用 Mata 时，有一组命令可以帮助你并操作它。最有用的命令是 `mata describe`；参见 [M-3]。

| | 2 + 3i | -2 + 4i |
|---|---|---|
| 1 | | |
| 2 | 2 + 6i | -2 + 4i |

## bytes type and extent

76 polymorphic matrix add()

200 real matrix id()

32 real matrix A[2,2]

32 real matrix B[2,2]

72 real matrix I[3,3]

48 real matrix M[3,2]

48 real matrix S[3,2]

47 string matrix S1[2,2]

44 string matrix S2[2,2]

72 real matrix X[3,3]

72 real matrix X[1,3]

64 complex matrix Z[2,2]

64 complex matrix Z1[2,2]

64 complex matrix Z2[2,2]

16 colvector a(2)

16 complex scalar area

8 real scalar b(2)

16 colvector c[4]

8 real scalar findout

16 real rowvector x(2)

16 real rowvector y(2)

32 real rowvector z[4]

## Mata 命令

当你使用 Mata 时，有一组命令可以帮助你并操作它。在 Mata 提示符下输入，另一个有用的命令是 `mata clear`（参见 [M-3] mata clear），它会清除 Mata 而不干扰 Stata：

```mat
: mata clear
: mata describe
```

## 退出 Mata

当你完成使用 Mata 后，在 Mata 提示符处输入 `end`：

```mat
: end
```

退出 Mata 不会清除它：

```mat
: mata
: x = 2
: y = (3 + 21)
: function add(a,b) return(a+b)
: end

```

```mat
+   : mata
mata (输入 end 退出)

+   : mata describe
## bytes type name and extent
76 polymorphic matrix add()
8 real scalar x
16 complex scalar y

: end
```

退出 Mata 会清除 Mata，正如 Stata 的 `clear mata` 命令一样；参见 [D] clear。

## 参见

+   [M-1] intro — 介绍与建议

## 标题

```
[M-1] help — 获取在线帮助
```

## 语法

```
help m# entryname
help mata functionname()
```

`help` 命令可以在 Stata 的点提示符（dot prompt）或 Mata 的冒号提示符（colon prompt）处发布。

## 描述

Stata 中的 Mata 帮助可用。本条目描述了如何访问它。

## 备注

- 要在线查看此条目，请在 Stata 的点提示符或 Mata 的冒号提示符处输入

`help mi help`

你这样输入是因为此条目是 [M-1] help。

例如，要查看函数 `max()` 的条目，请输入

- `help mata max()`

`max()` 的文档在 [M-5] minmax() 中记录，但这没关系；Stata 会找到相应的条目。

要从顶部进入 Mata 帮助系统，从那里你可以点击跳转到任何部分，或者输入：

- `help mata`

要访问 Mata 的 PDF 手册，请点击标题。

## 另

- [R] help — 显示在线帮助

- [M-3] mata help — 获取在线帮助

- [M-1] intro — 介绍与建议

## 标题

```
[M-1] how — Mata 的工作原理
```

## 描述

下面我们将揭开一些神秘面，向你展示 Mata 是如何工作的。我们怀疑每个人都会觉得这很有趣，而高级用户会发现这些描述对于预测 Mata 在遇到异常情况时会做什么很有用。

## 备注

备注在以下标题下的条目中呈现：

- 当你定义程序时发生了什么

- 当你进行交互式操作时发生了什么

- 当你输入一个 mata 环境命令时发生了什么

- 使用目标代码 I：无文件。

- 使用目标代码 II：.mlib 库

- Mata 环境

如果你是按照 [M-0] intro 中建议的顺序阅读条目的，请接下来接浏览 [M-1] intro 中你感兴趣的部分，然后查看 [M-2] 语法。

## 当你定义程序时会发生什么

假设你启动 Mata 并输入

```
: function try()
{
    real scalar i
    for (i=1; i<=10; i++) i
}
```

Mata 编译该程序：它读取你输入的内容并产生二进制代码，告诉 Mata 在执行执行程序时具体该做什么。事实上，给定上述程序，Mata 生成了二进制代码

```
00B4 3608 4000 0000 0100 0000 2000 0000
0000 0000 ffff ffff 0300 0000 0000 0000
0100 7472 7969 0400 0100 0000 0000 0000
0000 0000 0000 0000 0000 0000 0000 0000 0000 0000 0000 0000 0000 00000000000 0000
```

which looks meaningless to you and me, but Mata knows exactly what to make of it. 程序的编译版本被称为“目标代码”（object code），它是目标代码而不是源代码，Mata 将其存储在内存中。事实上，一旦目标代码被存储，源代码就会丢弃。这就是编译步骤——将文本转换为目标代码，使得 Mata 能够快速执行程序。随后，当需要执行程序时，Stata 遵循它之前记录的指令：

```
: try()
1
2
3
4
5
6
7
8
9
10
```

## 当你进行交互式操作时发生了什么

假设你输入

```
: x = 3
```

在 Mata 的术语中，这被称为 *istmt*——一个语句。显然，Mata 将 3 存储在 x 中，但它是怎么做到的？Mata 首先编译单条语句并将生成的目标代码存储在名称 `istmt` 下。当然，除非你不能定义一个名为

```
: function istmt()
{
    x = 3
}
```

程序，因为名称是无效的。Mata 有办法解决这个问题。在此刻，Mata 已经丢弃了代码 `x = 3` 并存储了相应的目标代码。接下来，Mata 执行 `istmt()`。完成后，只剩一件事要做，就是丢弃目标代码。结果就像你输入了

```
: mata drop istmt()
```

所以你输入

```
: x = 3
```

然后 Mata 执行

## 技术说明

上面的故事并不完全真实，因为由于，变量 `x` 对于函数 `istmt()` 是局部的，所以当 `istmt()` 执行结束时，变量 `x` 会丢弃。为了防止这种情况发生，Mata 将由 `istmt` 定义的所有变量设为全局。因此你可以输入

```
x = 3
```

跟着

```
y = x + 2
```

一切都如你预期：`y` 被设置为 5。

## 当你输入环境命令时会发生什么

当你处于冒号提示符并输入以 `mata` 开头的内容，例如

```
mata describe
```

或者

```
mata clear
```

事情完全发生了：Mata 冻结自己并将控制权临时移交给类似 Stata 的命令解释器。命令解释器访问 Mata 环境并对其进行报告或更改。完成后，解释器返回给 Mata，Mata 恢复运行并发布一个新的冒号提示符：

一旦在提示符输入了内容，Mata 将检查它是否以 `mata` 开头（此时解释过程重复），或者是函数定义（此时程序被编译但未执行），或者其他任何情况下 Mata 将尝试将其编译并执行 `istmt`。

## 使用目标代码 I：.mo 文件

一切都取决于 Mata 生成的目标代码，如果你愿意，可以将目标代码保存在磁盘上。这样做的好处是未来的某一天，你的程序无需编译即可执行，从而节省时间。如果你将目标代码发送给他人，他们可以在看不到背后源码的情况下使用你的程序。

在你输入之后，例如

```
: function try()
{
  real scalar i
  for (i=1; i<=10; i++)
}
```

Mata 已创建目标代码并丢弃了源码。如果你现在输入

```
: mata save
```

解释器将在当前目录下创建 `try.mo`；新文件将包含目标代码。

# [M-1] — Mata 的工作原理

未来的某一天，如果你在没有定义程序的情况下输入 `tryit()`，Mata 将沿着 ado-path（见 `sysdir`）查找名为 `try.mo` 的文件。找到文件后，Mata 将加载它（因此 Mata 现在拥有目标代码并按通常方式执行它）。

## 使用目标代码 II：.mlib 库

目标代码可以保存在 .mlib 库（文件）而不是 .mo 文件中。`mo` 文件包含一个程序的目标代码。.mlib 文件包含一组文件的目标代码。

第一步是选择一个名称（我们将选择 `lylib`——库名必须以小写开头*）并创建该空库：

```
: mlib create lylib
```

创建后，可以向库中添加新函数：

```
: mlib add lylib tryit()
```

可以随时添加新函数，既可以在创建后立即添加，也可以在之后——甚至是很久以后添加；见 `mlib`。我们提到过当 Mata 需要执行一个在内存中找不到的函数时，Mata 会查找同名的 .mo 文件。然而，在 Mata 这样做之前，Mata 会遍历它的库看看是否能在那里找到该函数。

## Mata 环境

Mata 的某些设置影响它的行为。你可以通过在提示符输入 `mata query` 来查看这些设置：

```
: mata query
```

| | |
| :--- | :--- |
| setastract | off |
| set matatum | off |
| set mataoptimize | on |
| set favor | space may be |
| set matacache | 400 kilobytes |
| set matolib | mataado |
| set matatomfirst | off |

你可以使用 `mata set` 更改这些设置。见 `set`。我们建议这些设置，除非我们承认部分吸引。

## 参考文献

Gould, W. W. 2006. Mata Matters: Precision. Stata Journal 6:550–560.

## 另见

[M-1] intro — 介绍与建议

# 40 交互式 — 交互使用 Mata

使用公式

```
b = (X'X)^{-1}X'y
V = s^2(X'X)^{-1}
```

其中

```
s^2 = e'e/(n - k)
e = y
n = rows(X)
k = cols(X)
```

我们开始输入：

+ - sysuse auto (1978 Automobile Data)

## 2. 创建时间序列变量

我们没有任何时间序列变量，但让我们假设我们有。如果我们的模型包含 `lnp`，我们将输入：

+ - gen lnp = gnp

这样我们得到了一个新变量 `lnp`，在后续步骤中用来替代 `gnp`。

## 3. 创建常数变量

+ - gen cons = 1

## 4. 移除不需要的变量

我们需要 `mpg`、`weight` 和 `cons` 变量，因此输入 `keep` 比删除它们更方便：

+ - keep mpg weight cons

## 5. 删除包含缺失值的观测值

我们的数据中没有缺失值，但让我们假设有，或者说我们不确定。这里有一个删除缺失值的简单技巧：

+ - regression mpg weight cons

(输出省略)

- keep if e(sample)

我们使用所有变量估计了一个回归，然后保留了观测值 `use`。选择哪个变量作为因变量、自变量的顺序并不重要，我们也可以输入：

+ - regression mpg weight cons

(输出省略)

- keep if e(sample)

# 41 交互式 — 交互使用 Mata

或者

+ - regress cons mpg weight foreign

(输出省略)

- keep if e(sample)

`regress` 输出的内容无关无关，即使某些变量被删除了。我们只是借用了 `regress` 识别无缺失值子集的能力。

使用 `regress` 会 Stata 进行许多不必要的计算，如果这让你反感，有一种更高级的替代方案：

+ - local 0 "mpg foreign cons"

- varlist

- marksample touse

- keep if touse

- drop touse

使用 `regress` 更简单。

## 6. 将变量放在大致相同的数值尺度上

这一步是可选的，但我们推荐这样做。你正准备使用由那些假设算术规则有效的人得出的公式，例如 $(a+b)-c = a+(b-c)$。在有限精度进行运算时，许多标准规则（如所示）会被违反，这会导致最终结果的舍入误差。

通过确保你的变量大致处于相同的尺度，你可以获得大量的保护，这意味着它们的均值和标准差大致相等。大致相等意味着它们之间相差了 1000 倍或 0 倍。所以让我们看看数据：

| Variable | Obs | Mean | Std.Dev. | Min | Max |
|---|---|---|---|---|---|
| mpg | 74 | 21.9973 | 5.785603 | 12 | 41 |
| weight | 74 | 3019.459 | 777.1936 | 1760 | 4840 |
| foreign | 74 | .2972973 | .4601885 | 0 | 1 |
| cons | 74 | .2972973 | 0 | 1 | 1 |

这里没有任何东西很困扰我们。变量 `weight` 是最大的，其均值和标准差是最小变量 `foreign` 的 1000 倍。忽略尺度差异我们会感到舒服，但仅仅是勉强。随着数据量的增长，我们的担忧也会增长。

解决这一担忧最简单的方法是对除 `weight`，使其不再以磅为单位，而是以千磅为单位测量：

```
replace weight = weight/1000
```

summarize

| Variable | Obs | Mean | Std.Dev. | Min | Max |
|---|---|---|---|---|---|
| mpg | 74 | 21.9973 | 5.785603 | 12 | 41 |
| weight | 74 | 3.019459 | .7771936 | 1.76 | 4.84 |
| foreign | 74 | .2972973 | .4601885 | 0 | 1 |
| cons | 74 | .2972973 | 0 | 1 | 1 |

这里没有任何东西很困扰我们。我们要做的是让变量的均值和标准差大致相等。如果 `weight` 有一个很大且合理的标准差，我们就会减去它，使其以某些数量的磅为单位。或者我们可以同时完成这两点：减去 2000 然后除以 100，使其以 100 磅为单位测量。请记住，“大致相等”的定义允许很大的余地，所以你不需要放弃。

## 7. 进入 Mata

输入

```
mata
: end
```

Mata 使用冒号 `:`，而 Stata 使用点号 `.`。

## 8. 使用 Mata 的 `st_view()` 函数访问数据

我们的矩阵公式是：

```
b = (X'X)^{-1}X'y
V = s^2(X'X)^{-1}
```

其中

```
s^2 = e'e/(n - k)
e = y - Xb
n = rows(X)
k = cols(X)
```

所以我们需要 `y` 和 `X`。`y` 是一个 $n \times k$ 的因变量向量，`X` 是一个 $n \times k$ 的自变量矩阵。行是观测值，列是变量。

我们如下创建向量和矩阵：

```
: st_view(y=., "mpg")
: st_view(X=., ("weight", "cons"))
```

让我们解释一下。`st_view()` 与所有其他函数不同，它返回的是一种名为 `view` 的特殊矩阵。`view` 在几乎每个方面看起来像普通矩阵，但它是底层数据集的视图。我们可以用 Mata 的 `st_data()` 函数创建 `y` 和 `X`，然后以自然的方式：

```
: y = st_data(., "mpg")
: X = st_data(., ("weight", "cons"))
```

# M-1 交互式 — 交互使用 Mata

`st_data()` 返回一个真实的矩阵，它是 Stata 存储在内存中的数据的拷贝。对于 `automobile-data` 示例，这是一个解决方案。但如果 `automobile-data` 更大，可能会内存不足，而 `views` 可以节省大量内存。你可以创建 `views`——创建很多——而且永远不会消耗多少内存！

`st_view()` 需要三个参数：要创建的矩阵名称、包含的观测值（行）以及变量（列）。如果我们想创建一个包含所有观测值和变量的矩阵 `Z`，我们可以输入：

```
: st_view(Z, .)
```

`st_view()` 理解第二和第三位置的缺失表示所有观测值和变量。让我们试试：



```
: st_view(Z, .)
err:mata: Z not found
```

这不起作用，因为 Mata 要求 `Z` 必须预定义。原因是技术性的，但在使用函数之前需要定义函数参数这不应该让你惊讶。Mata 只是不理解 `st_view()` 真的不需要定义 `Z`。解决 Mata 混淆的方法是定义 `Z`，然后让 `st_view()` 重新定义它：

如果你愿意，可以将所有内容合并为一个语句：

```
: st_view(Z=., ., .)
```

这就是定义 `y` 和 `X` 的方式：

```
: st_view(y=., "mpg")
: st_view(X=., ("weight", "cons"))
```

第二个参数指定了我们需要所有的观测值，第三个参数指定了我们需要的变量。输入变量时注意不要漏掉“额外的”括号。如果我们输入：

```
: st_view(X=., "weight", "cons")
```

你会被输入输入无效表达式。`st_view()` 期望三个参数，第三个参数是一个指定要选择变量的行向量：`("weight", "foreign", "cons")`

此时，我们建议你输入：

```
: y
(输出省略)
: X
(输出省略)
```

查看 `y` 和 `X` 确实包含我们的数据。如果你忘记了输入输入，这里是我们到为止的完整会话：

# 44 交互式 — 交互使用 Mata

```
+ - sysuse auto
- gen cons = 1
- keep mpg weight foreign cons
- regress mpg weight foreign cons
- keep e(sample)
- replace weight = weight/1000
-
- st_view(y=, "mpg")
- st_view(X=, ("Weight", "foreign", "cons"))
```

## 9. 执行你的矩阵计算

提醒你：我们的矩阵计算：

```
b = (X'X)^{-1}X'y
V = s^2(X'X)
```

其中

```
s^2 = e'e/(n - k)
e = y - Xb
n = rows(X)
k = cols(X)
```

让我们获取回归系数：

```
: b = invsym(X'X)*X'y
: b
```

| | | |
|---|---|---|
| 1 | -6.587886358 | |
| 2 | -1.650029004 | |
| 3 | 41.67970227 | |

让我们形成残差。定义 `n` 和 `k`，并获得 `s^2`：

```
: e = y - Xb
: n = rows(X)
: k = cols(X)
: s2 = (e'e)/(n-k)
```

所以我们能够计算方差矩阵：

```
: V = s2*invsym(X'X)
: V
: [symmetric]
```

| | | | |
|---|---|---|---|
| 1 | .4059128628 | | |
| 2 | .4064025078 | 1.157763273 | |
| 3 | -1.346459802 | -1.571315799 | 4.689594304 |

我们可以通过提取 `V` 的对角线并计算每个元素的平方根，以更具可读的方式呈现结果：

```
: se = sqrt(diagonal(V))
: (b, se)
```

| | | |
|---|---|---|
| 1 | -6.57886358 | .637129122 |
| 2 | -1.650029004 | 1.075994086 |
| 3 | 41.76970227 | 2.165547114 |

你知道，如果我们输入

```
: 2+3
5
```

Mata 会评估该表达式并向我们显示结果，这正是我们输入

```
: (b, se)
```

`(b, se)` 是一个表达式，Mata 对其进行了评估并显示了结果。该表达式的意思是形成一个第一列为 `b`、第二列为 `se` 的矩阵。我们可以使用 Mata 显示 `(b, se, b:/se/)` 来获取系数、标准误差及其 t 统计量的列表：

```
: (b, se, b:/se/)
```

| | | | |
|---|---|---|---|
| 1 | -6.57886358 | .637129122 | -10.34021793 |
| 2 | -1.650029004 | 1.075994086 | -1.533492633 |
| 3 | 41.76970227 | 2.165547114 | 19.24673077 |

在上面的表达式中，`b:/se` 意味着将 `b` 的元素除以 `se` 的元素。`:/` 被称为冒号运算符，你可以通过查看 [M-2] 运算符 了解更多关于它的信息。

我们可以通过输入来添加显著性水平：

```
: (b, b:/se, 2+xtail(n-k, abs(b:/se)))
```

| | | | | |
|---|---|---|---|---|
| 1 | -6.57886358 | .637129122 | -10.34021793 | 8.2286e-16 |
| 2 | -1.650029004 | 1.075994086 | -1.533492633 | .1295897129 |
| 3 | 41.76970227 | 2.165547114 | 19.24673077 | 6.8955e-30 |

这些是 `regress` 报告的结果；输入

```
: sysuse auto
: replace weight = weight/1000
: regress mpg weight foreign
```

并比较结果。

## 复习

我们完整的会话是

```
sysuse auto
  gen cons = 1
  keep mpg weight foreign cons
  regress mpg weight foreign cons
  keep if e(sample)
  replace weight = weight/1000
  mata
    st_view(y=, ., ., "spg")
    st_view(X=, ., ., "weight", "foreign", "cons")
    b = invsysym(X'*X)**y
    e = y - X*b
    n = rows(X)
    k = cols(X)
    s2 = (e'*e)/(n-k)
    s2+invsysym(X'*X)
    V
    se = sqrt(diagonal(V))
    (b, se)
    (b, se, b/se, 2*ttail(n-k, abs(b/se)))
  end
```

## 参考文献

Gould, W. W. 2006. Mata Matters: Interactive use. *Stata Journal* 6: 387–396.

# 另

- [M-1] 介绍和建议

## 标题

[M-1] LAPACK — LAPACK 线性代数程序

## 描述

LAPACK 代表 Linear Algebra PACKage（线性代数包），这是一组免费提供的 FORTRAN 90 例程，用于求解线性方程组、特征值问题和奇异值问题。许多 LAPACK 例程基于较旧的 EISPACK 和 LINPACK 例程，而更的 LAPACK 通过使用 BLAS（基础线性代数程序）进行大部分计算。

## 备注

LAPACK 和 BLAS 例程构成了 Mata 线性代数能力的基础。使用 LAPACK 例程的 Mata 函数总是注明这一点。

有关 LAPACK 的最新信息，请访问 http://www.netlib.org/lapack/

高级程序员可以直接访问 LAPACK 函数；参见 [M-5] lapack()。

## 致谢

我们感谢 LAPACK 作者的卓越工作：

E. Anderson, Z. Bai, C. Bischof, S. Blackford, J. Demmel, J. Dongarra, J. Du Croz, A. Greenbaum, S. Hammarling, A. McKinney, 以及 D. Sorensen。

## 参考文献

Anderson, E., Z. Bai, C. Bischof, S. Blackford, J. Demmel, J. Dongarra, J. Du Croz, A. Greenbaum, S. Hammarling, A. McKinney, and Sorensen. 1999. LAPACK Users' Guide. 3rd ed. Philadelphia: Society for Applied Mathematics.

## 另见

- [R] 版权 lapack — LAPACK 通知

- [M-5] lapack() — LAPACK 函数

- [M-1] intro — 介绍

## 标题

[M-1] limits — 限制与内存利用

## 总结

限制：

| | 最小值 | 最大值 |
|---|---|---|
| 标量、向量、矩阵 | 0 | 47647 |
| 列 | 0 | 47647 |
| 字符串元素，长度 | 0 | 47647 |
| Stata 的 matsize 在这些限制中不起作用。 | | |

大小估算：

| 内存需求 | |
|---|---|
| 实数矩阵 | oh + r*8 |
| 复数矩阵 | oh + r*16 |
| 指针矩阵 | oh + r*8 |
| 字符串矩阵 | oh + r*8 + total_length_of_strings |

其中 `r` 和 `c` 代表数量，

Stata 的 matsize 在这些限制中不起作用。# 描述

LAPACK 代表 Linear Algebra PACKage，是一组免费提供的 FORTRAN 90 例程，用于求解线性方程组、特征值

## 备注

LAPACK 和 BLAS 例程构成了 Mata 许多线性代数能力的基础。使用 LAPACK 例程的 Mata 函数总是注明这一事实。

有关 LAPACK 的最新信息，请访问 http://www.netlib.org/lapack/

高级程序员可以直接访问 LAPACK 函数；参见 [M-5] lapack()。

## 致谢

我们感谢 LAPACK 作者完成的卓越工作：

E. Anderson, Z. Bai, C. Bischof, S. Blackford, J. Demmel, J. Dongarra, J. Du Croz, A. Greenbaum, S. Hammarling, A. McKinney, 以及 Sorensen。

## 参考文献

Anderson, E., Z. Bai, C. Bischof, S. Blackford, J. Demmel, J. Dongarra, J. Du Croz, A. Greenbaum, S. Hammarling, A. McKinney, and Sorensen. 1999. LAPACK Users' Guide. 3rd ed. Philadelphia: Society for Applied Mathematics.

## 另见

- [R] 版权 lapack — LAPACK 通知

- [M-5] lapack() — LAPACK 函数

- [M-1] intro — 介绍

## 标题

[M-1] limits — 限制与内存利用

## 总结

限制：

| | 最小值 | 最大值 |
|---|---|---|
| 标量、向量、矩阵 | 0 | 47647 |
| 列 | 0 | 47647 |
| 字符串元素，长度 | 0 | 47647 |
| Stata 的 matsize 在这些限制中不起作用。 | | |

大小估算：

| 内存需求 | |
|---|---|
| 实数矩阵 | oh + r*8 |
| 复数矩阵 | oh + r*16 |
| 指针矩阵 | oh + r*8 |
| 字符串矩阵 | oh + r*8 + total_length_of_strings |

其中 `r` 和 `c` 代表数量，

Stata 的 matsize 在这些限制中不起作用。# 描述

LAPACK 代表 Linear Algebra PACKage，这是一组免费提供的 FORTRAN 90 例程，用于求解线性方程组、特征值问题和奇异值问题。许多 LAPACK 例程基于较旧的 EISPACK 和 LINPACK 例程，而更的 LAPACK 通过使用 BLAS（基础线性代数程序）进行大部分计算。

## 备注

LAPACK 和 BLAS 例程构成了 Mata 许多线性代数能力的基础。使用 LAPACK 例程的 Mata 函数总是注明这一点。

有关 LAPACK 的最新信息，请访问 http://www.netlib.org/lapack/

高级程序员可以直接访问 LAPACK 函数；参见 [M-5] lapack()。

## 致谢

我们感谢 LAPACK 作者完成的卓越工作：

E. Anderson, Z. Bai, C. Bischof, S. Blackford, J. Demmel, J. Dongarra, J. Du Croz, A. Greenbaum, S. Hammarling, A. McKinney, 以及 D. Sorensen。

## 参考文献

Anderson, E., Z. Bai, C. Bischof, S. Blackford, J. Demmel, J. Dongarra, J. Du Croz, A. Greenbaum, S. Hammarling, A. McKinney, and Sorensen. 1999. LAPACK Users' Guide. 3rd ed. Philadelphia: Society for Applied Mathematics.

## 另见

- [R] 版权 lapack — LAPACK 通知

- [M-5] lapack() — LAPACK 函数

- [M-1] intro — 介绍

## 标题

[M-1] limits — 限制与内存利用

## 总结

限制：

| | 最小值 | 最大值 |
|---|---|---|
| 标量、向量、矩阵 | 0 | 47647 |
| 列 | 0 | 47647 |
| 字符串元素，长度 | 0 | 47647 |
| Stata 的 matsize 在这些限制中不起作用。 | | |




# [M-1] LAPACK — LAPACK 线性代数程序

## 描述

`LAPACK` 代表 Linear Algebra PACKage（线性代数包），这是一组免费提供的 FORTRAN 90 例程，用于求解线性方程组、特征值问题和奇异值问题。许多 `LAPACK` 例程基于较旧的 `EISPACK` 和 `LINPACK` 例程，而更现代的 `LAPACK` 通过使用 `BLAS`（基础线性代数程序）进行大部分计算。

## 备注

`LAPACK` 和 `BLAS` 例程构成了 `Mata` 许多线性代数能力的基础。使用 `LAPACK` 例程的 `Mata` 函数总是注明这一点。

有关 `LAPACK` 的最新信息，请访问 `http://www.netlib.org/lapack/`

高级程序员可以直接访问 `LAPACK` 函数；参见 [M-5] `lapack()`。

## 致谢

我们感谢 `LAPACK` 作者完成的卓越工作：

`E. Anderson`, `Z. Bai`, `C. Bischof`, `S. Blackford`, `J. Demmel`, `J. Dongarra`, `J. Du Croz`, `A. Greenbaum`, `S. Hammarling`, `A. McKinney`, 以及 `D. Sorensen`。

## 参考文献

`Anderson, E., Z. Bai, C. Bischof, S. Blackford, J. Demmel, J. Dongarra, J. Du Croz, A. Greenbaum, S. Hammarling, A. McKinney, and Sorensen. 1999. LAPACK Users' Guide. 3rd ed. Philadelphia: Society for Applied Mathematics.`

## 另见

- [R] 版权 `lapack` — `LAPACK` 通知
- [M-5] `lapack()` — `LAPACK` 函数
- [M-1] `intro` — 介绍

---

# [M-1] limits — 限制与内存利用

## 总结

限制：

| | 最小值 | 最大值 |
|---|---|---|
| 标量、向量、矩阵 | 0 | 47647 |
| 列 | 0 | 47647 |
| 字符串元素，长度 | 0 | 47647 |
| `Stata` 的 `matsize` 在这些限制中不起作用。 | | |

大小估算：

| 内存需求 | |
|---|---|
| 实数矩阵 | `oh + r*8` |
| 复数矩阵 | `oh + r*16` |
| 指针矩阵 | `oh + r*8` |
| 字符串矩阵 | `oh + r*8 + total_length_of_strings` |

其中 `r` 和 `c` 代表数量，`Stata` 的 `matsize` 在这些限制中不起作用。

如果你将函数命名为计算机上已安装的用户编写的函数，将得到类似的结果。如果用户编写的函数当前不在内存中，你可以这样做。然而，在将来，这两个函数中的其中一个将占优先地位，无论是哪一个，某些功能将会出错。

## 如何确定函数名是否已被占用

使用 `mata which`（参见 [M-3] `mata which`）：

```
: mata which det_of_triangular()
function det_of_triangular() not found
  r(iii);
: mata which det()
et(): lmatabase
```

## 参见

- [M-2] `rewards` — 留用字
- [M-1] `intro` — 简介与建议

---

# [M-1] permutation — 关于置换矩阵和向量的旁论

## 语法

| 操作 | 置换矩阵表示法 | 置换向量表示法 |
|---|---|---|
| 置换行 | `$B = P*A$` | `$B = A[p,.]$` |
| 置换列 | `$B = A*P$` | `$B = A[.,p]$` |
| 逆置换行 | `$B = P'A$` | `$B = A; B[p,.] = A` 或 `$B = A[invorder(p),.]$` |
| 逆置换列 | `$B = A*P'$` | `$B = A; B[..p] = A` 或 `$B = A[., invorder(p)]$` |

*置换矩阵*（permutation matrix）是一个 `$n \times n$` 矩阵，它是单位矩阵的行（或列）置换。

*置换向量*（permutation vector）是一个包含 1 到 `$n$` 整数 `$1 \times n$` 或 `$n \times 1$` 向量。

以下置换矩阵和置换向量是等价的：

`$P = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 1 & 0 & 0 \end{bmatrix} \iff p = \begin{bmatrix} 2 \\ 3 \\ 1 \end{bmatrix}$`

都可以用于置换以下矩阵的行：

`$A = \begin{bmatrix} a & b & c & d \\ c & f & g & h \\ i & j & k \end{bmatrix} \text{产生 } \begin{bmatrix} e & f & g & h \\ i & j & k & l \\ u & b & c & d \end{bmatrix}$`

并置换以下矩阵的列：

`$P = \begin{bmatrix} m & n & o \\ p & q & r \\ s & t & u \\ v & w & x \end{bmatrix} \text{产生 } \begin{bmatrix} n & o & m \\ q & r & p \\ t & u & s \\ w & x & v \end{bmatrix}$`

置换矩阵是一种特殊的正交矩阵，通过乘法重新排列另一个矩阵的行或列。置换矩阵将重排转化为乘法形式。

置换向量也能重新排列另一个矩阵的行或列，但它们是通过下标（subscribing）实现的。从计算机的角度来看，这种实现相同目的替代方法更高效，因为它使用了更少的内存和计算时间。

两者之间的关系所示。

## 备注

备注在以下标题下给出：

- 置换矩阵
- 置换矩阵如何产生
- 置换向量

## 置换矩阵

置换矩阵是一个其行是单位矩阵置换的方阵。以下是所有 `$2 \times 2$` 置换矩阵的全集：

```
$$\begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} (1)$$
```

```
$$\begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix} (2)$$
```

设 `$P$` 为 `$n \times n$` 置换矩阵。如果 `$n \times m$` 矩阵 `$A$` 左乘 `$P$`，结果是重新排列它的行。例如：

```
$P * A = PA$
$\begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 1 & 0 & 0 \end{bmatrix} * \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix} = \begin{bmatrix} 4 & 5 & 6 \\ 7 & 8 & 9 \\ 1 & 2 & 3 \end{bmatrix} (3)$
```

上面，我们使用方阵 `$A$` 说明了重排，但 `$A$` 并不一定是方阵。

如果 `$m / n$` 矩阵 `$B$` 右乘 `$P$`，结果是重新排列它的列。我们再次用方阵 `$A$` 进行说明：

```
$A * P = AP$
$\begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix} * \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 1 & 0 & 0 \end{bmatrix} = \begin{bmatrix} 3 & 1 & 2 \\ 6 & 4 & 5 \\ 9 & 7 & 8 \end{bmatrix} (4)$
```

通过形成 `$PA$` 来重新排列 `$A$` 的行。由于置换矩阵是正交的，它们的逆等于转置。因此，置换矩阵 `$(P)$` 的逆我们一直在使用 `$(P^T)$`。

```
$$\begin{array}{ccccc} P' & & PA = A \\ \begin{array} 0 & 0 & 1 \end{array} & \begin{array} 4 & 5 & 6 \end{array} & \begin{array} 1 & 2 & 3 \end{array} \\ \begin{array} 1 & 0 & 0 \end{array} & \begin{array} 7 & 8 & 9 \end{array} & \begin{array} 4 & 5 & 6 \end{array}\end{array}$$
```

等等，OCR 文本“`$\begin{bmatrix} 0,1,0,0,1,0 \end{bmatrix} (3')$`”很乱。

让我们总结一下：

1. 置换矩阵 `$P$` 是其行是单位矩阵置换的方阵。
2. `$PA =$ A$` 的行置换。
3. `$AP =$ A$` 的列置换。
4. 逆置换由 `$P'$` 给出。
5. `$P'PA = A$`。
6. `$APP' = A$`。

## 置换矩阵如何产生

`Mata` 的某些函数隐式允许矩阵的行（或列）。例如，矩阵 `$A$` 的 LU 分解定义为

`$A = LU$`，其中 `$L$` 是下三角，`$U$` 是上三角。对于任何矩阵 `$A$`，都可以求解 `$L$` 和 `$U$`，且 `Mata` 有一个函数可以做到这一点（`ud`）。然而，`Mata` 的函数并没有按照所述解决问题。它求解的是 `$P'A = LU$`，其中 `$P'$` 是 `Mata` 生成的置换矩阵。需要明确的是，`Mata` 求解 `$L$` 和 `$U$`，但是针对 `$A$` 的行置换，而不是其本身，尽管函数告诉它选择了什么置换（函数返回 `$L, U$` 和 `$P'$`）。函数允许行是因为它可以产生更准确的答案。

你有时会读到函数采用了主元法（pivoting）。这意味着并不是给定的矩阵求解问题，而是针对原始矩阵的置换求解问题，并且函数以一种最小化结果舍入误差的方式选择置换，因为你将需要它。

例如，LU 分解的作用之一是计算逆。如果 `$A = LU$`，那么 `$A^{-1} = U^{-1}L^{-1}$`。计算三角矩阵的逆是一个简单的问题，因此计算逆的一种种配方是：

1. 将 `$A$` 分解为 `$L$` 和 `$U$`，
2. 计算 `$U^{-1}$`，
3. 计算 `$L^{-1}$`，以及
4. 将结果相乘。

应该是解决方案，但 LU 分解并没有将 `$A$` 分解为 `$L$` 和 `$U$`；它分解的是 `$P'A$`，尽管提供了 `$P$`。因此我们可以写：

```
$P'A = LU$
$A = PLU$
$A^{-1} = U^{-1}L^{-1}P'$
```

因此，我们问题的解决方案是按照计划使用 `$U$` 和 `$L$`——计算 `$U^{-1}L^{-1}$`——然后进行列置换，我们可以通过右乘 `$P'$` 来完成。

然而，我们还没有向你揭示一个细节：`Mata` 的 LU 分解函数并不返回置换矩阵 `$P$`。它返回 `$p$`，一个与 `$P$` 等价的置换向量，因此最后一步——通过右乘 `$P'$` 形成列置换的方法不同。那是下一节的主题。

置换向量比置换矩阵高效，但你会发现它们在数学上没有那么透明。因此，在使用返回置换向量的函数时——在使用置换行或列的函数时——用置换矩阵表示，然后转换回置换向量。

## 置换向量

置换向量用于 `Mata` 的下标运算符，因此在解释置换向量之前，让我们理解下标。不意外的是，`Mata` 允许下标。给定矩阵：

```
$A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix}$
```

`Mata` 明白

```
$A[2,3] = 6$
```

`Mata` 还理解如果其中一个下标指定为 `.`（缺失值），则选择整列或整行：

```
$A[.,3] = \begin{bmatrix} 3 \\ 6 \\ 9 \end{bmatrix}$
```

```
$A[2,.] = \begin{bmatrix} 4 & 5 & 6 \end{bmatrix}$
```

`Mata` 还理解如果任意下标指定了向量

在 `Mata` 中，我们实际上会将上述内容写作 `A[(2,3,2)]`，`Mata` 会理解为我们需要由 `A` 的第 2、3 和 2 行的所有列所组成的矩阵。同样，我们可以请求所有行以及第 2、3 和 2 列：

```
A[.,(2,3,2)] = \begin{bmatrix} 2 & 3 & 2 \\ 5 & 6 & 5 \\ 8 & 9 & 8 \end{bmatrix}
```

在上述示例中，我们将 `(2,3,2)` 写成一个行向量，因为这样看起来更符合逻辑，但我们也可以写成 `A[.,(2,3,2)]`。在下标操作中，`Mata` 不在乎向量是行还是列。

无论在任何情况下，我们都可以在 `Mata` 的下标中使用索引向量来选择矩阵的行和列，这意味着我们可以对它们进行置换。只需要我们指定的向量包含从 1 到 `$n$` 的整数的排列，否则我们就会重复某些行或列并遗漏其他。

置换向量是一个 `$n \times 1$` 或 `$1 \times n$` 的向量，包含从 1 到 `$n$` 的整数的排列。例如，等同于置换矩阵

```
P = \begin{bmatrix} 0 & 1 \\ 0 & 1 \\ 1 & 0 \end{bmatrix}
```

置换向量为

```
p = \begin{bmatrix} 2 \\ 3 \\ 1 \end{bmatrix}
```

可以使用 `p` 配合下标来置换 `A` 的行

```
A[.,p] = \begin{bmatrix} 4 & 5 & 6 \\ 7 & 8 & 9 \\ 1 & 2 & 3 \end{bmatrix}
```

同样，`A[.,p]` 会置换列。

此外，下标也可以用于等号赋值运算符的左侧。到目前为止，我们假设下标在赋值运算符的右侧，例如

```
B = A[p,,]
```

我们已经了解到，如果 `p = (2,3,1)`（或 `p = (2,3,1)`），结果是将 `A` 的第二行复制到 `B` 的第一行，将 `A` 的第三行复制到 `B` 的第二行，并将 `A` 的第一行复制到 `B` 的第三行。代码如下

```
B[p,,] = A
```

则执行的是反向操作：它将 `A` 的第一行复制到 `B` 的第二行，将 `A` 的第二行复制到 `B` 的第三行，并将 `A` 的第三行复制到 `B` 的第一行。`B[p,,]=A` 实际上是 `C=A[p,,]` 的逆操作，因为我们这样写代码：

---

# Mata 交互式使用示例

`(b, se)` 是一个表达式，`Mata` 对其进行了评估并显示了结果。该表达式的意思是形成一个第一列为 `b`、第二列为 `se` 的矩阵。我们可以使用 `Mata` 显示 `(b, se, b:/se/)` 来获取系数、标准误差及其 `t` 统计量的列表：

```
: (b, se, b:/se/)
```

| | | | |
|---|---|---|---|
| 1 | -6.57886358 | .637129122 | -10.34021793 |
| 2 | -1.650029004 | 1.075994086 | -1.533492633 |
| 3 | 41.76970227 | 2.165547114 | 19.24673077 |

在上面的表达式中，`b:/se` 意味着将 `b` 的元素除以 `se` 的元素。`:/ /` 被称为冒号运算符，你可以通过查看 [M-2] `op_colon` 了解更多关于它的信息。

我们可以通过输入来添加显著性水平：

```
: (b, b:/se, 2+xtail(n-k, abs(b:/se)))
```

| | | | | |
|---|---|---|---|---|
| 1 | -6.57886358 | .637129122 | -10.34021793 | 8.2286e-16 |
| 2 | -1.650029004 | 1.075994086 | -1.533492633 | .1295897129 |
| 3 | 41.76970227 | 2.165547114 | 19.24673077 | 6.8955e-30 |

这些是 `regress` 报告的结果；输入

```
: sysuse auto
: replace weight = weight/1000
: regress mpg weight foreign
```

并比较结果。

## 复习

我们完整的会话是

```
sysuse auto
  gen cons = 1
  keep mpg weight foreign cons
  regress mpg weight foreign cons
  keep if e(sample)
  replace weight = weight/1000
  mata
    st_view(y=, ., ., "spg")
    st_view(X=, ., ., "weight", "foreign", "cons")
    b = invsysym(X'*X)**y
    e = y - X*b
    n = rows(X)
    k = cols(X)
    s2 = (e'*e)/(n-k)
    s2+invsysym(X'*X)
    V
    se = sqrt(diagonal(V))
    (b, se)
    (b, se, b/se, 2*ttail(n-k, abs(b/se)))
  end
```

## 参考文献

`Gould, W. W. 2006. Mata Matters: Interactive use. *Stata Journal* 6: 387–396.`

## 另见

- [M-1] 介绍和建议



# [M-1] 置换 — 关于置换矩阵和向量的旁记

`C = A[p,,]`

`B[p,,] = C`

`B` 将等于 `C`，如果我们这样写代码：

```
C[p,..] = A
B = C[p,..]
```

`B` 也将等于 `C`。

然而，在左侧使用下标时，有一个陷阱需要注意：左侧的矩阵必须已经存在，且必须具有适当（此处为相同）维度。因此，在执行反向复制时，通常会这样写代码：

```
B = C
B[p,..] = C
```

第一行并不是多余；它确保了 `B` 存在且维度正确，尽管你也可以使用如下代码：

```
B = J(rows(C), cols(C), .)
B[p,..] = C
```

优先选择第一种构造，因为它确保了 `B` 与 `C` 的类型相同。如果你真的喜欢第二种形式，你应该这样写：

```
B = J(rows(C), cols(C), missingof(C))
B[p,..] = C
```

回到优选的代码：

```
B = C
B[p,..] = C
```

一些程序员将其合并为一条语句：

```
(B-C) [p,..] = C
```

此外，`Mata` 还提供了一个 `invorder \langle p\rangle`（参见 [M-5] invorder()），它将返回一个适用于右侧的倒置 `p`，因此你也可以这样写。

## 另见

- [M-5] invorder() — 置换向量操作
- [M-1] intro — 介绍与建议

# [M-1] returnedargs — 用于返回结果的函数参数

## 语法

`y = f(x, ...)`（按通常方式返回结果）
`g(x, ..., y)`（函数在参数 `y` 中返回结果）

## 描述

大多数 `Mata` 函数保持其参数不变并返回结果：

`: y = f(x, ...)`

然而，某些 `Mata` 函数不返回任何内容，而是通过一个或多个参数返回结果：

`: g(x, ..., y)`

如果你交互式地使用此类函数，且接收结果的参数尚未定义（上述示例中的 `y`），你将得到“变量未找到”的错误。解决方案是在调用函数之前定义参数以包含某些内容——任何内容：

`: y = .`
`: g(x, ..., y)`

你可以将其合并为一条语句：

`: g(x, ..., y=.)`

## 备注

大多数 `Mata` 函数保持其参数不变并返回结果：

`: y = f(x, ...)`

然而，某些 `Mata` 函数不返回任何内容，而是通过一个或多个参数返回结果：

`: g(x, ..., y)`

如果你交互式地使用此类函数，且接收结果的参数尚未定义（上述示例中的 `y`），你将得到“变量未找到”的错误。解决方案是在调用函数之前定义参数以包含某些内容：

`: y = .`
`: g(x, ..., y)`

你可以将其合并为一条语句：

`: g(x, ..., y=.)`

# [M-1] tolerance — 容差的使用与规范

## 语法

`somefunction(..., real scalar tol, ...)`

其中，关于参数 `tol`：

- 可选参数 `tol` 通常是可选的；不指定 `tol` 等同于指定 `tol = 1`。
- `tol > 0` 指定了通常容差所要乘以的倍数：`tol = 2` 意味着通常容差的两倍；`tol = 0.5` 意味着通常的容差。
- `tol < 0` 指定了用于容差的值的负值：`tol = -1e-14` 意味着 `1e-14` 为负值。

```
eta = 1e-14
```

```
eta = epsilon(1)（参见 [M-5] epsilon()）
```

```
eta = 1000*epsilon(trace(abs(A))/rows(A))
```

指定 `tol > 0` 将指定一个用于乘以 `eta` 的值。指定 `tol < 0` 将指定该值替换 `eta`。指定 `tol = 0` 则将 `eta` 设置为 0。

`eta` 的公式以及 `eta` 的用法可以在“备注”（Remarks）中找到。例如，备注可能会说，如果 `LU` 分解中 `U` 的任何对角线元素小于 `eta`，则 `A` 被声明为奇异矩阵。

## 描述

许多 `Mata` 函数的结果依赖于容差。`Mata` 提供了默认容差，但这些是可以被覆盖的。

## 备注

备注按以下标题列出：

- 问题
- 绝对容差与相对容差
- 指定容差

## 问题

在许多公式中，零是一个特殊数值；当数值出现时，有时无法计算出结果，或者有时需要进行特殊处理。由于舍入误差，在无限精度下计算的结果可能是 `1.03948e-15` 或 `-4.4376e-16` 等。如果这些小数值看起来完全是零（`1.03948e-15` 被视为零），某些公式会产生错误的结果；参见 [M-5] islice() 示例。因此，函数使用容差来确定一个数值何时小到可以视为零。

## 绝对容差

容差有两种类型：用于直接比较的绝对固定值。如果某个函数的容差为 `1e-14`，则计算出的 `8.99e-15` 被视为接近零，而 `1.00001e-14` 将被视为非零数值。

`1e-14` 小吗？这个数值对你来说可能是小的，但 `1e-14` 是否小取决于测量的内容及其单位。如果问题中的数值都在 `1e-12` 左右，你可能认为 `1e-14` 是合理的数值。这导致了相对容差的使用。与其将一个预定的小值视为零，不如指定一个值（例如 `1e-14`）并乘以某个系数，从而将其作为小的定义。

考虑以下矩阵：

```
5.5e-15  1.2e-16
1.3e-16  6.4e-15
```

矩阵的秩是多少？回答这个问题的一种方法是对矩阵进行 `LU` 分解，然后统计 `U` 中大于零的对角线元素的个数。在这里，我们将观察矩阵。绝对主义认为矩阵充满了舍入误差，且矩阵与零是不可分的：

```
0 0
0 0
```

矩阵的秩为 0。相对主义观点认为矩阵的秩为 2，因为除了 `1e-16` 的因子外，矩阵与零是不可分的：

| | |
| :--- | :--- |
| 5.5e-15 | 1.2 |
| 1.3e-16 | 64.0 |

在有人告诉矩阵如何产生及其单位之前，这个问题无法回答。然而，大多数 `Mata` 函数（默认）采用相对主义观点：矩阵是满秩的。由于大多数函数是通过相对容差实现的，因为 `Mata` 函数主要由统计学家使用，他们倾向于对数据矩阵进行 `X` 和 `X'` 等计算，这些矩阵可能包含很大的数字。这样的矩阵可能包含：

| | |
| :--- | :--- |
| 5.5e-15 | 1.2 |
| 1.3e-16 | 4.0 |

给定具有如此大元素的矩阵，人们往往会改变对“小”的观点。计算以下矩阵的秩：

| | |
| :--- | :--- |
| 5.5e-15 | 1.2 |
| 1.3e-16 | 64.0 |
| 5.5e-14 | 1.2 |
| 1.3e-16 | 13.0 |
| 5.5e-14 | 1.2 |
| 1.3e-16 | 13.0 |
| 5.5e-14 | 1.2 |
| 1.3e-16 | 8.05 |
| 5.5e-14 | 1.2 |
| 1.3e-16 | 7.05 |

这一次，正确地处理这个问题：我们将取 `LU` 分解并统计 `U` 对角线上的非零元素个数。对于上述矩阵，`U` 的对角线结果确实为 `(5.5e-14, 2.4e-13, 0.000087, 2.2e-16)`，与计算机精度相比，这仍然是一个体面的数字，但相对于对角线元素的平均值，这是一个非常小的数字（约为 `4.6e-9`）。

`eta` 的公式以及 `eta` 的用法可以在“备注”中找到。例如，备注可能会说，如果 `LU` 分解中 `U` 的任何对角线元素小于或等于 `eta`，则 `A` 被声明为奇异矩阵。

## 指定容差

大多数函数使用相对容差，但并没有规定。你必须阅读该函数的文档。

当容差出现时，指定 `tol > 0` 指定了通常容差所要乘以的倍数；指定 `tol < 0` 将指定该值替换 `eta`。指定 `tol = 0` 则将 `eta` 设置为 0。

## 参见

- [M-5] epsilon() — 精度
- [M-1] solve — 求解器
- [M-2] intro — 引言

# [M-2] intro — 语言定义

## 内容

| 语言定义 |

## 语法

| 运算符 | 说明 |
| :--- | :--- |
| 表达式 | 表达式 |
| 赋值运算符 | 赋值运算符 |
| 算术运算符 | 算术运算符 |
| 递增运算符 | 递增运算符 |
| 逻辑运算符 | 逻辑运算符 |
| 条件运算符 | 条件运算符 |
| 冒号运算符 | 冒号运算符 |
| 行和列运算符 | 行和列运算符 |
| 范围运算符 | 范围运算符 |
| 转置运算符 | 转置运算符 |
| 克罗内克积运算符 | 克罗内克积运算符 |

## 运算符

| 声明与参数 |
| :--- | :--- |
| 声明与类型 | 声明与类型 |
| 可选参数 | 可选参数 |
| 结构 | 结构 |
| 类 | 对象编程（类） |
| pragma | 抑制警告消息 |
| 版本 | 版本控制 |

## 声明与参数

## 控制流

- `if (exp) ... else ...`
- `for (exp1; exp2; exp3) stmt`
- `while (exp) stmt`
- `do...while (exp)`
- `break` 跳出 `for`, `while`, or `do` 循环
- `continue` 继续 `for`, `while`, or `do` 循环的下迭代
- `goto` 标签
- `return` 和 `return(exp)`

## 特殊话题

- 分号 — 使用分号
- `void` — 空矩阵
- 指针 — 指针
- 传递函数给函数

## 错误代码

错误代码

## 描述

本节定义了 `Mata` 语言。

## 备注

[M-2] 语法提供了一个密集且简短的概述，其他章节对其进行了扩展。另见 [M-1] intro 了解 `Mata`。

## 参见

[M-0] intro — `Mata` 介绍

# [M-2] break — 跳出 `for`, `while`, or `do` 循环

## 语法

```
for, while, or do {
    ...
    if (...) {
        ...
        break
    }
    stmtleftarrow break 跳到这里
    ...
}
```

## 描述

`break` 跳出最层的 `for`, `while`, or `do` 循环。执行循环关闭后的后续语句，就像循环正常结束一样。`break` 几乎总是出现在 `if` 之后。

## 备注

在以下代码中：

```
for (i=1; i<=rows(A); i++) {
    for (j=1; j<=cols(A); j++) {
        ...
        if (A[i,j]==0) break
    }
    printf("%xg\n", j)
}
```

当 `A[i,j]` 的任何元素为零时，将执行 `break` 语句。假设语句在 `i=2` 和 `j=3` 时执行。执行将继续 `printf()` 语句，这意味着 `j` 循环被取消，`i` 循环继续。退出循环时 `j` 的值为 3；当你跳出循环时，`j++` 不会被执行。

## 参见

- [M-2] do — `do ...while (exp)`
- [M-2] for — `for (exp1; exp2; exp3) stmt`
- [M-2] while — `while (exp) stmt`
- [M-2] continue — 继续 `for`, `while`, or `do` 循环的下迭代
- [M-2] intro — 语言定义

# [M-2] class — 面向对象编程（类）

## 语法

```mata
class classname [extends classname] {
  declaration(s)
}
```

语法在以下标题下显示：

- 引言
- 示例
- 成员变量的声明
- 方法（成员函数）的声明与定义
- 声明中的默认可见性

随后是“描述（Description）”和“备注（Remarks）”。

## 引言

`Stata` 的两种编程语言 `ado` 和 `Mata` 均支持面向对象编程。本手册条目解释了 `Mata` 中的面向对象编程。对面向对象编程感兴趣的用户通常希望在 `Mata` 中进行编程。请参阅 [p] class 以了解关于 `ado` 中的面向对象编程。

## 示例

下示例将在*描述（Description）*中进行详细阐释。

```mata
class coord {
  real scalar x, y
  real scalar length(), angle()
}

real scalar coord::length()
{
  return(sqrt(x^2 + y^2))
}

real scalar coord::angle()
{
  return(atan2(y, x)*360/(2*pi))
}

class rotated_coord extends coord {
  real scalar theta
  real scalar angle()
  void new()
}
```

```mata
real scalar rotated_coord::angle()
{
  return(super.angle() - theta)
}

void rotated_coord::new()
{
  theta = 0
}
```

可以交互式地使用该类：

```mata
: b = rotated_coord()
: b.x = b.y = 1
: b.angle() // 显示将为 45
: b.theta = 30
: b.angle() // 显示将为 15
```

注意，将类像函数一样使用会创建一个该类的实例。在其他函数内部使用类时，只要将成员实例声明为标量（`scalar`），就不需要显式创建实例：

```mata
void myFunc()
  class rotated_coord scalar b
  b.x = b.y = 1
  b.angle() // 显示将为 45
  b.theta = 30
  b.angle() // 显示将为 15
```

## 成员变量的声明

声明的形式为：

```mata
[exposure] [static] [final] matype name [name, ...]
```

其中：

```
exposure := public|protected|private
matype := eltype|orgtype|eltype|orgtype
eltype := transymorphic orgtype := matrix
numeric vector
real rowvector
complex colvector
string scalar
pointer
class class
struct structname
```

例如：

```mata
class S {
    real matrix             M
    private real scalar    type
    static real scalar      count
    class coord scalar      c
}
```

## 方法（成员函数）的声明与定义

声明的形式为：

```mata
[exposure] [static] [final] [virtual]
matatype name() [ , name() [...] ]
```

例如：

```mata
class T {
    real matrix             inverse()
    protected real scalar  type()
    class coord scalar      c
}
```

注意，函数参数即使被允许，也不进行声明。

成员函数（方法）和成员变量可以共享相同的名称，并且这种事实具有特殊意义。下方的 `type` 和 `c` 是变量，而 `type()` 和 `c()` 是函数：

```mata
class U {
    real matrix             M
    private real scalar    type
    static real scalar      count
    class coord scalar      c
    real matrix             inverse()
    protected real scalar  type()
    class coord scalar      c
}
```

成员函数是分开定义的，在类定义之后定义。例如：

```mata
class V {
    real matrix             M
    private real scalar    type
    static real scalar      count
    class coord scalar      c
    real matrix             inverse()
    protected real scalar  type()
    class coord scalar      c
}
```

```mata
real matrix V::inverse(...)
{
...
}
real scalar V::type(...)
{
...
}
class coord scalar V::c(...)
{
...
}
```




## 成员函数定义

当定义成员函数时，它们的类型必须与之前声明的类型相同。你可以省略可见性，以及 `static`、`final` 和 `virtual`。

## 声明中的默认可见性

除非显式声明，否则变量和函数都是公开的（`public`）。它们也不是静态的（`static`）、最终的（`final`）或虚拟的（`virtual`），但这不属于可见性范围，与本节无关。

你可以使用任何可见性修饰符 `public`、`protected` 和 `private`，后跟冒号，以创建一个具有不同默认值的块：

```mata
class V {

public:

    real matrix         M

    static real scalar  count

    class coord scalar  c

    real matrix         inverse()

    class coord scalar  c()

private:

    real scalar         type

protected:

    real scalar         type()

}
```

## 描述

`class` 为 Mata 提供了面向对象编程，也称为类编程。

类是绑定在一个名称下的一组变量或相关函数（方法），或两者兼有。类可以派生自其他类。让我们看看第一页（在“示例”下）的细节：

1. 首先，我们创建了一个名为 `coord` 的类。当我们编写代码时：

   ```mata
   class coord {

       real scalar x, y

       real scalar length(), angle()

   }
   ```

   指定了 `coord` 的每个元素都存储实数值，我们称之为 `x` 和 `y`。

2. 随后，我们定义了 `coord` 的方法：

   ```mata
   real scalar coord::length()
   {

     return(sqrt(x^2 + y^2))

   }

   real scalar coord::angle()
   {

     return(atan2(y, x)*360/(2*pi))

   }
   ```

3. 接下来，我们定义了一个派生自 `coord` 的类 `rotated_coord`：

   ```mata
   class rotated_coord extends coord {

     real scalar theta

     real scalar angle()

     void new()

   }
   ```

   ```mata
   real scalar rotated_coord::angle()
   {

     return(super.angle() - theta)

   }

   void rotated_coord::new()
   {

     theta = 0

   }
   ```

可以交互式地使用该类：

```mata
: b = rotated_coord()

: b.x = b.y = 1

: b.angle() // 显示将为 45

: b.theta = 30

: b.angle() // 显示将为 15
```

注意，将类像函数一样使用会创建一个该类的实例。在其他函数内部使用类时，只要将成员实例声明为标量（`scalar`），就不需要显式创建实例：

```mata
void myFunc()

  class rotated_coord scalar b

  b.x = b.y = 1

  b.angle() // 显示将为 45

  b.theta = 30

  b.angle() // 显示将为 15
```

## 类：面向对象编程

`b.x` 是指代 `b` 的 `x` 值的方式。你可以像在 Mata 中使用任何实标量变量一样使用 `b.x` 以及 `b.y`。

如果我们将 `b` 的 `theta` 重置为 30 度，`b` 的 `angle` 应该变为 15 度。这正是发生的情况：

```mata
: b.theta = 30

: b.angle()

  15
```

`b.angle()` 是指定成员函数 `angle()` 在实例 `b` 上运行的方式。现在你了解了一个类的实例，因此可以访问类中成员变量的所有值。然而，成员函数可以接受额外的参数。我们编写了：

```mata
real scalar rotated_coord(real scalar base)
{

  return(super.angle() - theta - base)

}
```

那么 `angle()` 就会接收一个参数，并且结果从 `base` 开始测量。

交互式地使用 `rotated_coord` 与在 Mata 程序内部使用它的区别在于，如果我们声明一个变量（例如 `b`）为类 `rotated_coord` 标量（强调 `scalar`），那么我们就不需要费心调用 `rotated_coord()` 来初始化 `b`。编写 `class rotated_coord b` 需要在它成为标量之前进行初始化，这会自动发生。如果我们也编写了 `rotated_coord()`，并不会有害，但会浪费我们和计算机的时间去循环执行我们的程序。

让我们展示一些在第一个示例中没有展示的内容。还记得我们为 `coord` 定义了 `length()` 吗？还记得我们没有为 `rotated_coord` 定义 `length()` 吗？尽管如此，`length()` 仍然是 `rotated_coord` 的概念，因为 `rotated_coord` 的定义是继承自 `coord` 的，而这种继承发生是因为在我们声明 `rotated_coord` 时，我们说了：

```mata
class rotated_coord extends coord
```

继承的发生是因为使用了 `extends`。让我们测试一下 `length()` 是否在我们的 `rotated_coord` 类实例 `b` 上有效：

```mata
: b.length()

  1.414213562
```

在上述代码中，我们避免了编写额外的、重复的代码。

让我们回顾一下。首先，我们定义了一个 `coord`。从它，我们定义了一个 `rotated_coord`。你现在可以以 `rotated_coord` 为起点，定义 `translated_and_rotated_coord`。这并不困难。

类有许多属性、特性和细节，但**继承**属性是面向对象编程的核心。

## 备注

备注在以下标题下给出：

- 符号和术语
- 类的声明和定义
- 将类保存到文件中
- 工作流建议
- 当你需要调和时
- 获取类的实例
- 构造函数和析构函数
- 设置成员变量和成员函数的暴露性
- 使成员变为最终（`final`）
- 使成员变为静态（`static`）
- 虚函数
- 使用 `this` 引用当前类
- 使用 `super` 访问父类概念
- 转换为父类
- 从成员函数访问外部函数
- 类的指针

## 符号和术语

### `::`（双冒号）

双冒号符号在文档中用作简写，表示变量或函数是类的成员；在两种情况下，双冒号符号也是 Mata 能够理解的语法。

`S::` 表示变量 `s` 是类 `S` 的成员。`S::` 是文档简写。

`S::f()` 表示函数 `f()` 是类 `S` 的成员。`S::f()` 是文档简写。

`S::f()` 是 Mata 本身在以下两种情况下可以理解的内容：

1. 在定义成员函数时使用符号 `S::f()`。
2. 符号 `S::f()` 可以作为调用静态成员函数的方法。

### ...的实例（an instance of）

当我们写下“让 `s` 为 `S` 的一个实例”时，我们说 `s` 是类 `S` 的实例，或者等价地，在某些 Mata 代码中，`s` 被声明为类 `S` 标量。

### 类定义与类声明

类的定义或声明是对该类的定义，如下所示：

```mata
class S {

    private real scalar    a, b

    real scalar          f(), g()

}
```

请注意，将 Mata 变量声明为类型 `class S`，例如以下代码中的 `S scalar` 行：

```mata
void myfunction() {

    class S scalar  s

    ...

}
```

并不是类定义，而是对类实例的声明。

## 类实例与继承

### 类实例

类实例是根据类定义定义的变量。在代码中：

```mata
void myfunction()

    class S Scalar s

    real scalar b

    ...

```

`s` 是一个类实例，或者更正式地说，是类 `S` 的实例。“实例”（instance）一词可以用于所有元素类型，而不仅仅是类。因此，`b` 是 `real` 的实例。然而，“实例”一词更多地用于类和结构体，因为我们需要将包含类或结构体的变量定义与类和结构体本身区分开来。

### 继承

继承是一个类定义使用另一个类的变量和函数的属性，就像它们是自己的变量和函数一样。当一个类这样做时，被称为它扩展（`extend`）了另一个类。`T` extending `S` 意味着 `T` 继承自 `S`。`T` 也被称为 `S` 的子类。

考虑以下定义：

```mata
class S {

    real scalar a, b

    void f()

}

class T extends S {

    real scalar c

}
```

让 `s` 为 `S` 的一个实例。那么 `s.f()` 的执行将 `s.b` 设为 0；它没有改变 `s.a`，尽管程序员可能也想将 `s.a` 设为零。

例如，让 `U` extend `T`，并假设 `S::f()` 和 `T::f()` 已经定义。根据继承规则，`U` 和 `T` 的实例调用 `f()` 时将调用 `T::f()`。这里 `S::f()` 被 `T::f()` 覆盖了。由于 `T::f()` 是基于 `S::f()` 实现的，`T::f()` 会认为有必要调用 `S::f()`。这是通过使用 `super` 前缀来实现的，即使用 `super` 访问父类概念。

## 成员与外部函数

### 成员

在类内部声明的变量或函数被称为类的成员变量、成员函数。成员函数也被称为方法。在接下来，让 `ex1` 为 `S` 的实例，并假设 `S` 包含函数 `f()` 和变量 `v`。

当成员变量和函数在成员函数内部使用时，可以通过名称 `v` 和 `f()` 直接引用它们。因此，如果我们编写 `S::g()` 的代码，我们可以：

```mata
real scalar S::g()
{

    return(f())

}
```

当成员变量和函数在成员函数外部使用时，即在普通函数中使用，引用必须以类实例为前缀。因此人们编写：

```mata
real scalar myg(class S ex1)
{

    return(ex1.f())

}
```

### 变量和方法覆盖

通常，当第二个变量或函数共享相同的名称时，第二个变量或函数会覆盖第一个变量或函数，第二个导致第一个被隐藏，从而倾向于访问第二个变量或执行第二个函数。这在 Mata 对类的实现中通过两种方式出现。

第一种方式：如果子类定义了同名的变量或函数，则父类中的变量或函数被称为被覆盖。例如，让 `U` extend `T`，并假设 `S::f()` 和 `T::f()` 已经定义。根据继承规则，`U` 和 `T` 的实例调用 `f()` 时将调用 `T::f()`。这里 `S::f()` 被 `T::f()` 覆盖了。

第二种方式是函数中的栈变量的优先级高于成员变量。例如：

```mata
class S {

    real scalar a, b

    void f()

}
```

以及：

```mata
void S::f()
{

    real scalar a

    a = 0

    b = 0

}
```

让 `s` 为 `S` 的一个实例。那么 `s.f()` 的执行将 `s.b` 设为 0；它没有改变 `s.a`，尽管程序员可能也想将 `s.a` 设为零。因为程序员在程序中声明了一个变量名，但程序的变量优先级高于成员变量 `a`。

解决此问题的一种方法是将 `a = 0` 这一行更改为 `this.a = 0`；请参见“引用当前类”。

## 类的声明与定义

假设我们通过以下代码声明了一个类：

```mata
class coord {

    real scalar x, y

    real scalar length(), angle()

}
```

此时，类 `coord` 被认为已经**声明但尚未定义**，因为其成员函数 `length()` 和 `angle()` 的代码尚未输入。尽管如此，该类已具有部分功能。具体而言：

1. 类可以正常工作。显然，如果尝试执行 `length()` 或 `angle()`，将抛出错误信息。
2. 类定义可以保存到 `.mo` 或 `.mlib` 文件中供以后使用，这与 Mata 中的规定相同。

类的成员函数的定义方式与普通 Mata 函数相同，但函数名被指定为 `className::functionname()`：

```mata
real scalar coord::length()
{

    return(sqrt(x^2 + y^2))

}

real scalar coord::angle()
{

    return(atan2(y, x)*360/(2*pi))

}
```

另一个区别是，成员函数可以直接访问类的成员变量和函数。上面的 `x` 和 `y` 是类 `coord` 实例的 `x` 和 `y` 值。

现在，类 `coord` 已定义。

## 将类保存到文件中

符号 `class()`——即类名、左括号和右括号——用于通过 Mata 的交互式命令（如 `mata describe`、`mata mosave` 和 `mata mlib`）引用整个类定义。

`mata describe coord()` 将显示：

```mata
: mata describe coord()
```

| # 字节数 | 名称和范围 |
|---|---|
| 344 | classdef scalar \| coord() |
| 176 | real scalar \| ::angle() |
| 136 | real scalar \| ::length() |

![类定义信息](img/94f0e160fb245a717f6d9189ad47298e_95_0.png)

可以通过输入以下命令将整个类定义（编译后的 `coord()` 及其所有编译后的成员函数）存储在 `.mo` 文件中：

```mata
: mata mosave coord()
```

可以通过输入以下命令将整个类定义存储在已存在的 `.mlib` 库 `lpersonal` 中：

```mata
: mata mlib add lpersonal coord()
```

保存类定义时，这两个命令都允许使用额外的 `complete` 选项。该选项规定只有当类定义完整时才保存类，否则将抛出错误信息。

```mata
: mata mlib add lpersonal coord(), complete
```




## 工作流建议

我们建议将类的源代码保存在单独的文件中，并让文件包含完整的定义。在 StataCorp，我们将`coord`保存在`coord.mata`文件中：

```mata
!! version 1.0.0 class coord

version 12

mata:

class coord {

    real scalar x, y

    real scalar length(), angle()

}

real scalar coord::length()

{

    return(sqrt(x^2 + y^2))

}

real scalar coord::angle()

{

    return(atan2(y, x)*360/(2*pi()))

}

end
```

注意，该文件不会清除 Mata，也不会将类保存到 .mo 或 .mlib 文件中：该文件仅记录源代码。有了此文件，要将`coord`保存到 .mo 文件中，我们只需要输入：

- `clear mata`
- `do coord.mata`
- `mata mosave coord(), replace`

（注意，尽管`coord.mata`没有 .do 后缀，但我们可以使用`do`命令像执行任何其他 do 文件一样执行它。）实际上，我们可能会将这些行放在另一个 do 文件中，例如`cr_coord.do`。

## [M-2] 类 — 面向对象编程（类）

我们同样使用文件来创建库，例如`begin cr_lourlib.do`：

```mata
version 12

clear mata

do coord.mata

do anotherfile.mata

do yetanotherfile.mata

/* 等. */

nmata:

mata mlib create lourlib, replace

mata mlib add *()

end
```

通过上述方法，在更新代码后很容易重新构建库。

### 需要重新编译时

如果你更改了类的声明，则需要重新编译所有使用该类的程序。这包括需要继承该类的其他类声明。例如，在开始的示例中，如果你更改了类声明中的任何内容：

```mata
class coord {

    real scalar

    real scalar length(), angle())

}
```

即使更改仅仅是反转了 x 和 y 的顺序，或者添加了新的变量或函数，你不仅必须重新编译`coord`的所有成员函数，还重新编译所有使用`coord`的函数，并且必须重新编译`rotated_coord`，因为`rotated_coord`继承了`coord`。

你必须这样做，因为 Mata 会严格编译你的代码。Mata 编译器会重构所有类并使用低级构造。优点是你不必牺牲。缺点是当你添加或删除函数时，必须重新编译。为了减少重新编译的需求（特别是当你分发代码时），你可能希望采用面向对象。假设你已经写了行，并且从另一个地方需要声明`wonderfulhandle`，然后通过调用初始化来使用系统：

```mata
wonderfulhandle = wonderful_init()
```

### 获取类的实例

声明一个类，例如

```mata
class coord {

    real scalar x, y

    real scalar length(), angle()

}
```

实际上创建了函数`coord()`。函数`coord()`将并返回类的实例：

- `coord()`——不带参数——返回类的标量实例。
- `coord(3)`——带一个参数 3——返回一个 1×3 向量，每个元素都是类的实例。
- `coord(2,3)`——带两个参数 2,3——返回一个 2×3 矩阵，每个元素都是类的实例。

函数`coord()`在交互式使用 Mata 时有用。它是交互式创建类的唯一方法。

在函数中，你可以通过`class scalar name`创建标量实例，但在所有情况下，你都需要使用函数`coord()`。在下面的示例中，程序员想要一个 coord 向量：

```mata
void myFunction() {

    real scalar i

    class coord vector v

    ...

    v = coord(3)

    for (i=1; i<=3; i++) v[i].x = v[i].y = 1

}
```

如果程序员省略了`class coord v`这一行，程序将产生编译时错误。变量声明在 Mata 通常是可选的，但类类型的变量声明不是可选的。

如果程序员省略了`v = coord(3)`这一行，将产生运行时错误。因为`v`被声明为向量，`v`初始为 1×0。程序员需要的第一件事是将`v`扩展为 1×3。

在实践中，很少需要类向量或矩阵。一个更典型的程序如下：

```mata
void myFunction() {

    real scalar i

    class coord scalar v

    ...

    v.x = v.y = 1

    ...

}
```

请特别注意`class coord v`这一行。程序员最常犯的错误是在声明中省略了`scalar`。如果你这样做，系统会假设它是一个矩阵，那么`v`就不是 1 x 1，而是 0 x 0。如果你确实省略了`scalar`，你有两种替代方案：要么回去把这个词加回来，要么在初始化`v.x`和`v.y`之前添加`v = coord()`这一行。采用哪种方法都可以。事实上，当你指定了`scalar`时，编译器仅仅是为你插入了`v = coord()`这一行。

### 构造函数与析构函数

在每次创建类的新实例时，你可以指定变量的初始化方式以及更多操作，在此之前，让我们先了解默认初始化。在

```mata
class coord {

    real scalar x, y

    real scalar length(), angle()

}
```

这里有两种方式。当类的实例被创建时（例如因为`x`和`y`是标量），`b.x`和`b.y`将以通常的方式填充。在这里，由于它们是缺失的。如果它们是向量、行向量、列向量或矩阵，它们的维度将被设为 1 x 0（向量和行向量）、0 x 1（列向量）和 0 x 0（矩阵）。

如果你想控制初始化，可以在类中声明一个名为`new()`的构造函数：

```mata
class coord {

    real scalar x, y

    real scalar length(), angle()

    void new()

}
```

函数`new()`必须声明为`void`且不能接受任何参数。你永远不需要手动调用`new()`——事实上，你是不允许那样做的。相反，每当类的新实例创建时，函数`new()`自动调用。

如果你希望每个`coord`实例在生命开始时`x`和`y`都等于 0，可以这样编写：

```mata
void coord::new() {

    x = y = 0

}
```

假设我们这样做了，并在创建新类`rotated_coord`时继承自`coord`，正如第一个示例所示。

```mata
class rotated_coord extends coord {

    real scalar theta

    real scalar angle()

    void new()

}

void rotated_coord::new() {

    theta = 0

}
```

当我们创建一个`rotated_coord`实例时，所有变量都已初始化为 0。这意味着函数`rotated_coord()`将知道要同时调用`coord::new()`和`rotated_coord::new()`，并按照相应的顺序调用它们。

在你你的新函数中，你不限于初始化值。`new()`是一个函数，你可以编写任何想要的代码，所以如果你想建立与射电望望远镜的连接并检查任何进入的消息，你可以这样做。更贴生活一点，如果你正在实现一个文件系统，可能会使用一个静态变量来计算打开文件的数量（我们稍后会解释静态成员变量）。

在实例创建的另一侧——实例销毁——你可以声明并创建一个`void destroy()`，它同样不接受任何参数，并在每次实例被销毁时被调用。`destroy()`被称为析构函数。`destroy()`的工作原理类似于`new()`，区别在于你不允许直接调用该函数。每当 Mata 释放与实例相关的内存时，Mata 会调用`destroy()`。在 Mata 中`destroy()`并没有太大作用，因为内存管理是自动的，释放内存不是你的责任。在其他一些面向对象的编程语言（如 C++）中，你需要负责内存管理，而析构函数正是释放与实例相关内存的地方。

尽管如此，`destroy()`在 Mata 中偶尔仍有用。让我们考虑一个需要计算自身存在的实例数量的系统，也许是为了在实例计数变为 0 时释放资源。这样的系统可能部分读取如下：

```mata
class bigsystem {

    static real scalar counter

    void new(), destroy()

}

void bigsystem::new() {

    counter = (counter == 0 ? 1 : counter+1)

}

void bigsystem::destroy() {

    counter--

}
```

注意`bigsystem::new()`必须处理两种初始化：第一次和后续的。当它第一次被调用时，`counter`为 0，`new()`必须将`counter`设置为 1。之后，`new()`将增加`counter`。

如果该系统需要在第一次初始化时获取资源（例如对射电望远镜的访问权限），并在最后销毁时释放它，并准备好重复过程，代码可以是：

```mata
void bigsystem::new() {

    if (counter == 0) {

        get_resource()

        counter = 1

    } else {

        ++counter

    }

}

void bigsystem::destroy() {

    if (--counter == 0) {

        release_resource()

    }

}
```

注意，每当实例销毁时都会运行`destroy()`，即使该销毁是由于用户中止（abort-error）引起的。射电望远镜将在最后一个实例销毁时释放。

### 设置成员变量可见性

可见性指定了谁可以访问成员变量。三个级别，从宽松到严格：`public`、`protected`和`private`。

- 公有的变量和函数可以被类外部的调用者访问。
- 受保护的变量和函数仅可以被类的成员函数访问。
- 私有的变量和函数仅可以被类的成员函数访问。

当你不指定时，变量和函数是公有的。为了代码可读性，你可以将成员变量声明为公有，但并非必须。

在编写大型系统时，通常的做法是将成员变量设为私有，并提供公共函数来设置和访问变量。这样，类的内部设计就可以被修改，而继承它的类不需要修改。

你可以通过在声明前加上`protected`或`private`将成员变量和函数设置为受保护或私有：

```mata
class myclass {

    private real matrix X

    private real vector y

    void setup()

    real matrix invert()

    protected real matrix invert_subroutine()

}
```

或者，你可以创建具有不同默认块：

```mata
class myclass {

    public:

        void setup()

        real matrix invert()

    protected:

        real matrix invert_subroutine()

    private:

        real matrix X

        real vector y

}
```

你可以自由地组合`public`、`private`和`protected`，无论是否带冒号。

### 使成员静态

静态是类成员变量函数的可选属性。在下文中，假设`ex1`和`ex2`都是`S`的实例，假设`c`是类的静态变量，假设`f()`是类的静态函数。

静态变量是一个值在所有实例间共享的变量。因此，`ex1.c`和`ex2.c`将始终保持相等。如果`ex1.c`被改变，例如通过`ex1.c=5`，那么`ex2.c`也是 5。

静态函数不使用类中非静态成员变量的值。因此，无论 ex1 和 ex2 如何不同，`ex1.f(3)`和`ex2.f(3)`都是相等的。

在成员函数之外，静态函数也可以通过编写类名、两个冒号 [作用域解析运算符] 来调用，因此即使没有类实例，也可以使用该函数。例如，等同于`ex1.f(3)`或`ex2.f(3)`的`S::f(3)`。

### 虚函数

当函数被声明为虚函数（virtual）时，继承规则的作用就像当一个类继承另一个类时，如果子类没有定义某个函数，它将继承父类的函数。然而，对于虚函数，父类可以访问子类对函数的定义，这就是为什么我们说在某种意义上，它是反向继承。

经典的启发性示例是关于动物的。在不失一般性的情况下，我们将使用动物来说明。定义了一个类`animal`。定义了扩展（继承自）`animal`的类`cow`和`sheep`。`animals`中定义的一个函数需要发出特定动物的声音，它调用虚函数`sound()`来完成。在动物级别，定义了函数`animal::sound()`来显示“Squeak!”。然而，由于函数`sound()`是虚函数，每个特定的动物类都应该定义它们自己的声音。类`cow::sound()`显示“Moo!”，而`sheep`定义了显示“Baa!”的`sheep::sound()`。结果是当动物调用`sound()`时，它的行为就像继承是反向的，调用了相应的`sound()`例程，用户会看到“Moo”或“Baa!”。如果添加了一个新物种，且程序员忘记定义`sound()`，那么`animal::sound()`将运行，用户会看到“Squeak!”。在这种情况下，这本应该是系统出故障的声音，但实际上它只是默认操作。

让我们编写这个示例的代码。首先，我们编写通常的情况：

```cpp
class animal {

    void sound()

    void poke()

}

void animal::sound() { "Squeak!" }

void animal::poke() {

    sound()

}

class cow extends animal {

}

class sheep extends animal {

}
```

在上面的示例中，当一个动物（牛或羊）被戳（poke）时，它会发出一种声音。戳操作定义在动物级别，因为除了它们发出的声音外，戳操作在动物之间很大程度上是通用的。如果`c`是`cow`的实例，那么可以通过编写`c.poke()`来戳那个特定的牛。然而，`c.poke()`继承自`animal`，执行的是通用操作，同时牛会发出的通用的吱叫。

现在我们让`sound()`变成虚函数：

```cpp
class animal {

    virtual void sound()

    void poke()

}

void animal::sound() { "Squeak!" }

void animal::poke() {

    sound()

}

class cow extends animal {

    virtual void sound()

}

void cow::sound() { "Moo!" }

class sheep extends animal {

    virtual void sound()

}

void sheep::sound() { "Baa!" }
```



现在让我们追踪一下通过编写 `c.poke()` 调用牛和羊的 `poke()` 函数时发生了什么。提醒你一下，没有 `cow::poke()`；但是 `c.poke()` 执行了 `animal::poke()`。`animal::poke()` 调用 `sound()`，如果 `sound()` 不是虚函数，它将调用 `animal::sound()`，这会发出吱叫。牛得到一个“Squeak!”，由于 `sound()` 是虚函数，因为它是用牛调用的，所以它调用了 `cow::sound()`，我们听到了“Moo!”。

关注语法，`cow` 和 `sheep` 在它们的声明中重复 `virtual sound()` 是重要的。如果你定义了函数 `S::f()`，那么它必须在 `S` 中声明。然而，考虑一种情况，我们有两个品种的牛：安格斯牛（Angus）和荷尔斯坦（Holstein），它们发出的声音略有不同。荷尔斯坦源于荷兰，其“哞”声中带有一点 U 的音，这种方式是英语使用者无法模仿的。因此，我们将声明两个新类：`angus` 牛和扩展自 `Holstein` 的类，并定义 `angus::sound()` 和 `holstein::sound()`。也许我们不会定义 `animal::sound()`；那么安格斯牛将获得通用的牛叫。

## 从成员函数中访问外部函数

在起始示例中，`coord` 类包含一个成员函数 `length()`。如果我们没有编写一个普通（非类）函数，我们就无法创建一个名为 `length()` 的函数。`length()` 这一名称被 Mata 保留用于其自身返回向量长度（元素个数）的函数；请参阅 `[M-5] rows`。我们允许在函数内部创建一个名为 `length()` 的函数。在成员函数之外，`c.length()` 是 `c` 的 `length()` 定义的无歧义引用，而 `length()` 本身是对 `length()` 通常定义的无歧义引用。

然而，在编写成员函数时可能会产生混淆。让我们为 `coord` 添加另一个成员函数：`ortho()`，其代码如下：

```mata
class coord scalar coord::ortho() {
    class coord scalar      newcoord
    real scalar             r, t

    r = length()
    t = angle()

    newcoord.x = r*cos(t)
    newcoord.y = r*sin(t)

    return(newcoord)
}
```

注意，在上面的代码中，我们调用了 `length()`。因为我们正在编写成员函数，并且类定义了一个同名的成员函数，因此 `length()` 被解释为对 `coord` 的 `length()` 定义的调用。如果 `coord` 没有定义这样的成员函数，那么 `length()` 将被解释为对 Mata 的 `length()` 的调用。

那么如果类提供了一个函数，外部存在同名的函数，而我们想在函数名前加上双冒号，我们该怎么办？如果我们想将 `length()` 解释为 Mata 的函数而不是类的函数，我们会写成：

```mata
r = ::length()
```

这里的名称 `length()` 并没有特殊之处。如果类提供了成员函数 `myfcn()`，且外部也有一个定义，而我们想要外部函数，我们就会编写 `::myfcn()`。事实上，类并不一定非要提供定义。我们不记得 `class coord` 是否包含 `myfcn()`，但无论如何我们都想要外部的 `myfcn()`，我们只需编写 `::myfcn()`。

在成员函数的定义内部，外部函数名称前放置双冒号被认为是一种良好的风格。这样，如果你返回并向类添加另一个成员函数，就不必担心某些已编写的成员函数假设该名称直接传递到了外部定义的函数。

## 类的指针

正如你可以获取任何其他 Mata 变量的指针一样，你也可以获取类实例的指针。回想我们在“Virtual functions of animals makes many sounds when poked”中的示例。

为了示例起见，我们将获取一个 `cow()` 实例的指针，并通过该指针访问 `poke()` 函数：

```mata
void pokeacow() {
    class cow scalar c
    pointer(class cow scalar scalar) scalar p

    p = &c
    p->poke()
}
```

你通过 `->` 运算符通过类的指针访问成员变量和函数，就像处理结构体一样。更多信息请参阅 `[M-2] struct` 中的 Pointers to structures。

## 另请

- `[M-2] declarations` — 声明与类型
- `[M-2] struct` — 结构
- `[P] class` — 类编程
- `[M-2] intro` — 语言定义

# `[M-2] comments` — 注释

## 语法

```mata
/* enclosed comment */

// rest-of-line comment
```

说明：

1. 注释可以出现在 do-files 和 ado-files 中；在交互模式下是不允许。
2. Stata 的行首星号注释在 Mata 中是不允许：
   - 在 Stata 中有效但在 Mata 中无效

## 描述

`/* */` 和 `//` 是在 Mata 程序中放置注释的方式。

## 备注

有两种注释样式：`/* */` 和 `//`。你可以使用其中一种、另一种或两者都使用。

备注在以下标题下：

```text
The /* */ enclosed comment

The // rest-of-line comment
```

### `/* */` 封闭式注释

封闭式注释可以出现在一行中：

- `*` 之后的内容使用了近似公式：`*/`

封闭式注释可以出现在行内，甚至出现在 Mata 表达式的中间：

```mata
x = x + /*left-single-quote*/ char(96)
```

封闭式注释本身可以包含多行：

```mata
/*
我们使用基于 sin(x) 的近似，对于小的 x 近似等于 x；x 单位为弧度
*/
```

封闭式注释可以嵌套，这对于注释掉本身包含注释的代码非常有用：

```mata
/*
for (i=1; i<=rows(x); i++) {
    x[i] = x[i] :/ value[i]
}
*/
```

### `//` 行尾注释

行尾注释可以单独出现在一行中：

```mata
// 之后的内容使用了近似公式：
```

或者它也可以出现在行的末尾：

```mata
x = x + char(96) // append single quote
```

在任何一种情况下，注释在行结束时结束。

## 另请

`[M-2] intro` — 语言定义

# `[M-2] continue` — 继续执行 for、while 或 do 循环的下次迭代

## 语法

```mata
for, while, or do {
    ...
    if (...)
}
```

## 描述

```mata
for, while, or do {
    ...
    if (...)
}
```

## 备注

有两种注释样式：`/* */` 和 `//`。你可以使用其中一种、另一种或两者都使用。

备注在以下标题下：

```text
The /* */ enclosed comment

The // rest-of-line comment
```

### `/* */` 封闭式注释

封闭式注释可以出现在一行中：

- `*` 之后的内容使用了近似公式：`*/`

封闭式注释可以出现在行内，甚至出现在 Mata 表达式的中间：

```mata
x = x + /*left-single-quote*/ char(96)
```

封闭式注释本身可以包含多行：

```mata
/*
我们使用基于 sin(x) 的近似，对于小的 x 近似等于 x；x 单位为弧度
*/
```

封闭式注释可以嵌套，这对于注释掉本身包含注释的代码非常有用：

```mata
/*
for (i=1; i<=rows(x); i++) {
    x[i] = x[i] :/ value[i]
}
*/
```

### `//` 行尾注释

行尾注释可以单独出现在一行中：

```mata
// 之后的内容使用了近似公式：
```

或者它也可以出现在行的末尾：

```mata
x = x + char(96) // append single quote
```

在任何一种情况下，注释在行结束时结束。

## 另请

`[M-2] intro` — 语言定义

# `[M-2] declarations` — 声明与类型

在上述函数中有三组声明。首先，函数名面前有一个声明：

```mata
real matrix swaprows(...)
{
    ...
}
```

该声明表示此函数将返回一个实数型矩阵（real matrix）。

第二组声明出现在括号内：

```mata
...
swaprows(real matrix A, real scalar i1, real scalar i2)
{
}
```

这些声明表示该函数期望接收三个参数，我们将它们命名为 `A`、`i1` 和 `i2`，并且我们期望它们分别是一个实数矩阵、一个实数标量和一个实数标量。

第三组声明出现在函数体的顶部：

```mata
...
swaprows(...)
{
    real matrix B
    real vector v
    ...
}
```

这些声明表示我们将在函数内部使用变量 `B` 和 `v`，而且事实上，`B` 将是一个实数矩阵，`v` 是一个行向量。

我们可以省略所有这些声明。我们的函数可以写成：

```mata
function swaprows(A, i1, i2)
{
    B = A
    v = B[i1, .]
```



`B[i1, .] = B[i2, .]`

`B[i2, .] = v`

`return(B)`

}

```

并且它可以正常运行。那么，我们为什么要声明这些呢？

1. 通过包含外部声明，我们告知其他程序预期的结果。它们可以依赖 `swaprows()` 返回一个实数矩阵，因为当 `swaprows()` 完成时，Mata 会验证该函数确实返回了实数矩阵，如果不是，将中止执行。

如果没有外部声明，任何情况都是可能的。我们的函数可以在一种情况下返回实数标量，在另一种情况下返回复数行向量，在另一种情况下什么都不返回。

包含外部声明会让调试变得更容易。

2. 通过包含参数声明，我们告知其他程序员他们应该向我们的函数传递什么。这使得我们的函数更容易理解。

我们还告诉了 Mata 预期，如果其他程序尝试错误地使用我们的函数，Mata 将停止执行。

与（1）一样，我们让调试变得更容易。

3. 通过包含内部声明，我们告诉了 Mata 需要哪些变量以及我们将如何使用它们。Mata 可以利用这些信息做两件事：首先，它可以确保我们正确使用了变量（再次让调试变得更容易）；其次，Mata 可以产生更高效的代码（让我们的函数更快）。

在交互操作中，我们承认有时会在没有声明的情况下定义函数。对于更严谨的工作，我们会包含它们。

## 类型、元素类型和组织类型

当你交互式使用 Mata 时，你只是随地创建新变量：

- `n = 2`
- `A = (1,2; 3,4)`
- `z = (sqrt(-4+0i), sqrt(4))`

当你创建一个变量时，你可能没有考虑类型，但 Mata 会考虑。上面的 `n` 在 Mata 看来是一个实数标量。`A` 是一个实数矩阵，`z` 是一个复数行向量。

Mata 将变量类型视为两个部分：

- 变量包含的元素的类型（例如实数或复数）。
- 这些元素是如何组织的（例如行向量或矩阵）。

我们将这两种类型分别称为 `eltype`（元素类型）和 `orgtype`（组织类型）。`eltype` 和 `orgtype` 如下：

| `eltype` | `orgtype` |
| --- | --- |
| `transmorphic` | `matrix` |
| `numeric` | `vector` |
| `real` | `rowvector` |
| `complex` | `colvector` |
| `string` | `scalar` |
| `pointer` | |

你可以每种选择一个，并描述 Mata 理解的所有类型。

## 隐式声明

当你不声明对象时，Mata 的行为就像你将其声明为 `transmorphic matrix`：

1. `transmorphic` 意味着矩阵可以是实数、复数、字符串或指针。
2. `matrix` 意味着组织形式为 $r \times c$，其中 $r \geq 0$ 且 $c \geq 0$。

# [M-2] 声明 — 声明与类型

在函数的某一点，一个 `transmorphic matrix` 可能是一个实数标量（`real` 是 `transmorphic` 的特例，而 `scalar` 在 `r = c = 1` 时是 `matrix` 的特例），而在另一点，它可能是一个字符串收集器（`string` 是 `transmorphic` 的特例，而 `colvector` 在 `c = 1` 时是 `matrix` 的特例）。考虑我们没有声明的 `swapsrows()` 函数：

```mata
function swapsrows(A, i1, i2)
{
    B = A
    v = B[i1, .]
    B[i1, .] = B[i2, .]
    B[i2, .] = v
    return(B)
}
```

编译该函数的结果就像该函数返回：

```mata
transomorphic matrix swapsrows(
    transmorphic matrix A,
    transmorphic matrix i1,
    transmorphic matrix i2
)
{
    transmorphic matrix B
    transmorphic matrix v

    B = A
    v = B[i1, .]
    B[i1, .] = B[i2, .]
    B[i2, .] = v
    return(B)
}
```

当我们声明变量时，我们对其施加了限制。

## 元素类型

六种 `eltype`：

1. `transmorphic` 意味着矩阵可以是实数、复数、字符串或指针。
2. `numeric` 意味着元素是实数或复数。
3. `real` 意味着元素是实数。
4. `complex` 意味着元素是复数。
5. `string` 意味着元素是字符。
6. `pointer` 意味着元素是内存地址。

## 组织类型

五种 `orgtype`：

1. `matrix` 意味着组织形式为 $r \times c$，其中 $r \geq 0$ 且 $c \geq 0$。
2. `vector` 意味着元素是线性组织的。
3. `rowvector` 意味着元素是水平组织的。
4. `colvector` 意味着元素是垂直组织的。
5. `scalar` 意味着只有一个元素。

## 变量声明

变量声明是出现在函数体顶部的声明：

```mata
... swaprows(...)
{
    real matrix B
    realvector v
    ...
}
```

这些声明是可选的。如果你省略了它们，Mata 会注意到你在代码中使用了 `B` 和 `v`。Mata 编译你的代码时会得像你已经声明这些变量为可变态（`transomorphic`）的一样，这意味着生成的编译代码效率可能比理想情况略低，但仅此而已。

只要你没有开启 `mata set metastatric`，变量声明都是可选的；请参阅 [M-3] `mata set`。有些程序员坚信变量确实应该被声明，因此 Mata 提供了一项机制，在他们忘记声明时抛出错误。

无论何种，这些声明（无论是显式的还是隐式的）都定义了我们将使用的变量。我们在函数中使用的变量是——无论某处是否浮动着其他变量，`B` 和 `v` 无关。私有变量在函数调用时创建，在函数结束时销毁。变量是私有的，但如上述所示，如果我们将变量传递给另一个函数，可能会改变它们的值。大多数函数不会这样做。

声明变量的语法是：

```mata
type varname [, varname [, ...]]

external [type] varname [, varname [, ...]]
```

`real matrix B` 和 `real rowvector` 符合第一种语法。

## 链接外部全局变量

第二种语法与链接全局变量有关。当你交互式地使用 Mata 并输入：

```mata
: n = 2
```

你创建了一个名为 `n` 的变量。该变量是全局的。当你在函数内部编写时：

```mata
myfunction(...)
{
    external n
}
```

你的函数将使用的 `n` 变量是全局变量 `n`。如果你的函数现在检查 `n` 的值，将发现它包含 `2`。

如果变量不存在，语句 `external n` 将创建它。假设我们之前没有定义过 `n`。如果 `myfunction()` 检查 `n` 的内容，它会发现 `n` 是一个 0 × 0。这是因为我们编写了：

```mata
external n
```

# [M-2] 声明 — 声明与类型

Mata 的行为就像我们编写了：

```mata
external transmorphic matrix n
```

让我们修改 `myfunction()` 为：

```mata
myfunction(...)
{
    external real scalar n
    ...
}
```

考虑以下情况：

- `n` 不存在。这里 `external real scalar n` 将创建 `n`——当然，是一个实数标量——并将其值设为缺失（missing）。
- 如果 `n` 被声明为向量（`vector`），将创建一个 1 × 0 向量。
- 如果 `n` 被声明为列向量（`colvector`），将创建一个 0 × 1 向量。
- 如果 `n` 被声明为矩阵（`matrix`），将创建一个 0 × 0 矩阵。
- `n` 已存在，且它是一个实数标量。我们的函数执行并使用全局 `n`。
- `n` 已存在，且是一个实数 1 × 1 行向量、列向量或矩阵。重要的是它是 1 × 1；我们的函数执行并使用全局 `n`。
- `n` 已存在，但它是复数、字符串或指针，或者它是实数但不是 1 × 1。Mata 会抛出错误消息并终止函数的执行。

复杂的程序系统有时发现通过全局变量进行通信非常方便。由于全局变量是全局的，我们建议你为全局变量起长名称。一种方法是将函数名作为前缀：

```mata
myfunction(...)
{
    external real scalar mysystem_n
}
```

关于全局变量另一种方法，请参阅 [M-5] `findexternal()` 和 [M-5] `valofexternal()`。

## 另另

- [M-2] `intro` — 语言定义

# [M-2] `do` — `do...while (exp)`

## 语法

```mata
do stmt while (exp)

do {
    stmts
} while (exp)
```

其中 `exp` 必须求值为一个实数标量。

## 描述

`do` 执行 `stmt` 或 `stmts` 一次或多次，直到 `exp` 为 0。

## 备注

`do` 的一个常见用法是循环直到收敛：

```mata
do {
    lasta = a
    a = get_new_a(lasta)
} while (mreldif(a, lasta) > 1e-10)
```

循环至少执行一次，在循环体执行之前，不会执行条件表达式。

## 另请

- [M-2] `for` — `for (exp1; exp2; exp3) stmt`
- [M-2] `while` — `while (exp) stmt`
- [M-2] `break` — 跳出 `for`、`while` 或 `do` 循环
- [M-2] `continue` — 继续 `for`、`while` 或 `do` 循环的下次迭代
- [M-2] `intro` — 语言定义

# [M-2] `errors` — 错误代码

## 描述

当发生错误时，Mata 会显示数字以及描述问题的文本。代码如下所示。

此外，错误代码可以作为 `_error()` 的参数，请参阅 [M-5] `error()`。

Mata 的错误代码是 Stata 返回代码的特例。特别地，它们是返回代码。特别地，它们是 3000–3999 范围内的返回代码。

## 备注

Mata 的错误消息分为两类：编译时发生的错误（代码 3000）和执行时发生的错误（代码 3001–3999）。

编译时错误如下：

```mata
:3000 invalid expression

r(3000);
```

运行时错误如下：

```mata
:3200 conformability error

solve(): - function error

function(): - function error

<istmt>: - function error
```



# [M-2] errors — 错误代码

上述显示`*`（乘法运算符）检测到了问题，`solve()`可能是问题的，因为必须问为什么`solve()`使用了乘法？

在任何情况下，让我们假设问题不在`solve()`。那么你可能会怀疑在`mysub()`上。如果你在之前的程序中使用`mysub()`没有任何问题，那么你现在可以将怀疑转向`myfunction()`。如果`myfunction()`一直很可靠，那么你不应该输入`myfunction(2,3)`。

## 错误代码

- 3000。（随情况而异）你输入的内容错误。`Mata`无法理解你的意思。
- 3001. 参数数量不。函数预期三个参数，但接收到两个。函数允许三个到五个参数，但你提供的过多或过少。请修复调用程序。
- 3002. 不允许相同的参数。你在这里调用函数时，使用了同一个变量多次。通常这不是问题，但在这里是，因为提供的参数是函数想要覆盖为不同结果的矩阵。例如，假设函数`f(A, B, C)`检查矩阵`A`并根据`B`和`C`返回计算。函数可能会抱怨你为`B`和`C`指定了同一个矩阵。
- 3010. 尝试引用空指针。程序引用了`*s`而`s`包含；[M-2] 指针。
- 3011. 无效左值。在赋值中，等号左的内容不是可以赋值；[M-2] op_assignment。
- 3012. 指针未定义操作。你已经尝试相加两个指针；[M-2] 指针。
- 3020. 类/父类编译时间不同。一个类被用于扩展另一个类，而父类在类被编译后已更新。
- 3021. 类编译时间不同。使用预定义类的函数在类最后一次更改后没有重新编译。
- 3101. 要求函数的地方发现了矩阵。函数的某个特定参数要求是函数，但发现的是矩阵。
- 3102. 要求矩阵的地方发现了函数。函数的某个特定参数要求是矩阵、向量或标量，但发现的是函数。
- 3103. 在需要数组的地方发现了视图 (view)。通常情况下，视图矩阵可以用于任何需要矩阵的地方，但有少数例外，特别是在低层例程以及希望将结果写回参数的例程中。这些情况下不接受视图。如果`V`是视图变量，只需编写代码`X = V`并用`X`代替即可。请参见 [M-5] sl_view()。
- 3104. 在需要视图的地方发现了数组。函数参数指定了一个不是视图的矩阵，但此处需要一个视图。请参见 [M-5] sl_view()。
- 3200. 维度不匹配错误。矩阵、向量或标量的行数和/或列数不符合要求。将一个 2 × 3 矩阵相加一个 1 × 4 矩阵会导致此错误。
- 3201. 需要向量。参数要求为 r × l 或 1 × c，但发现的是矩阵。
- 3202. 需要列向量。参数要求为 1 × c，但实际不是。
- 3203. 需要列向量。参数要求为 r × I，但实际不是。
- 3204. 在需要标量的地方发现了矩阵。参数要求为 1 × 1，但实际不是。
- 3205. 需要方阵。参数要求为 n × n，但实际不是。
- 3206. 包含 op.vars 的视图无效。视图中使用了因子变量，而现在该视图正被用于不支持因子变量的上下文。
- 3250. 类型不匹配。参数的类型 (etype) 与要求的不符。例如，可能期望一个实数 (real) 但收到了字符串 (string)。参见 [M-6] Glossary表中的 etype。
- 3251. 在需要数值的地方发现了数值。参数期望为实数或复数，但实际不是。
- 3252. 在需要复数的地方发现了非复数。参数期望为复数，但实际不是。
- 3253. 在需要实数的地方发现了非实。参数期望为实数，但实际不是。
- 3254. 在需要字符串的地方发现了非字符串。参数期望为字符串，但实际不是。
- 3255. 需要实数或字符串。参数期望为实数或字符串，但实际不是。
- 3256. 需要数值或字符串。参数期望为实数、复数或字符串，但实际不是。
- 3257. 在需要指针的地方发现了非指针。参数期望为指针，但实际不是。
- 3258. 在需要 void的地方发现了非 void。参数期望为 void，但实际不是。
- 3259. 在需要结构的地方发现了非结构。将一个非结构变量传递给一个期望该变量为结构的函数。
- 3260. 在需要类的地方发现了非类。将一个非类变量传递给一个期望该变量为类的函数。
- 3261. 在需要类/结构的地方发现了非类/非结构。将一个既不是类也不是结构的变量传递给一个期望该变量为类或结构的函数。
- 3300. 参数超出范围。参数的类型 (etype) 和原始类型 (orgtype) 是正确的，但参数包含无效值，例如你请求一个 4x5 矩阵的第 20 行。请参见 [M-6] Glossary表中的 etype 和 orgtype。
- 3301. 下标无效。下标超出范围（指向不存在的行或列）或包含错误数量的元素。请参见 [M-2] subscripts。
- 3302. 无效的 %fmt。用于格式化的 %fmt 无效。请参见 [M-5] printf() 并参见 [U] 12.5 Formats: 控制如何显示数据。
- 3303. 无效置换向量。指定的向量不符合置换向量的要求，即 el 向量必须包含 1 到 n 整数的置换。请参见 [M-1] permutation。
- 3304. 结构嵌套过深。结构可以包含包含结构的结构，依此类推，但深度限制为 500。
- 3305. 类嵌套过深。类可以包含包含类的类，依此类推，但深度限制为 500。
- 3351. 参数包含缺失值。通常情况下，`Mata`对缺失值具有容忍性，但也有例外。此函数不允许矩阵、向量或标量具有缺失值。
- 3352. 奇异矩阵。矩阵是奇异的，无法执行请求的结果。如果可能出现奇异矩阵，你可能使用了错误的函数。
- 3353. 矩阵非正定。矩阵是非正定的，无法计算请求的结果。如果可能出现正定矩阵，你可能使用了错误的函数。
- 3360. 无法收敛。发布此消息的函数使用的算法本应收敛，但实际上并未收敛，可能是因为输入矩阵在某些方面过于极端。

# [M-2] 错误 — 错误代码

- 3492. 结果字符串过长。函数尝试生成的字符串过长。由于`Mata`中字符串的最大长度为 2,147,483,647 个字符，不太可能是`Mata`施加的限制。请检查该函数的文档以确定限制的来源。
- 3498. (信息有所异)。函数尝试生成的字符串过长。由于`Mata`中字符串的最大长度为 2,147,483,647 个字符，不太可能是`Mata`施加的限制。请检查该函数的文档以确定限制的来源。
- 3499. 未找到。函数尝试生成的字符串过长。由于`Mata`中字符串的最大长度为 2,147,483,647 个字符，不太可能是`Mata`施加的限制。请检查该函数的文档以确定限制的来源。
- 3500. 无效变量。函数尝试生成的字符串过长。由于`Mata`中字符串的最大长度为 2,147,483,647 个字符，不太可能是`Mata`施加的限制。请检查该函数的文档以确定限制的来源。
- 3598. 未找到。函数尝试生成的字符串过长。由于`Mata`中字符串的最大长度为 2,147,483,647 个字符，不太可能是`Mata`施加的限制。请检查该函数的文档以确定限制的来源。
- 3601. 无效的文件句柄。函数尝试生成的字符串过长。由于`Mata`中字符串的最大长度为 2,147,483,647 个字符，不太可能是`Mata`施加的限制。请检查该函数的文档以确定限制的来源。
- 3602. 无效的文件。函数尝试生成的字符串过长。由于`Mata`中字符串的最大长度为 2,147,483,647 个字符，不太可能是`Mata`施加的限制。请检查该函数的文档以确定限制的来源。
- 3603. 无效的文件模式。函数尝试生成的字符串过长。由于`Mata`中字符串的最大长度为 2,147,483,647 个字符，不太可能是`Mata`施加的限制。请检查该函数的文档以确定限制的来源。
- 3611. 打开的文件过多。函数尝试生成的字符串过长。由于`Mata`中字符串的最大长度为 2,147,483,647 个字符，不太可能是`Mata`施加的限制。请检查该函数的文档以确定限制的来源。
- 3612. 文件太大（32位限制）。函数尝试生成的字符串过长。由于`Mata`中字符串的最大长度为 2,147,483,647 个字符，不太可能是`Mata`施加的限制。请检查该函数的文档以确定限制的来源。
- 3621. 尝试写入只读文件。函数尝试生成的字符串过长。由于`Mata`中字符串的最大长度为 2,147,483,647 个字符，不太可能是`Mata`施加的限制。请检查该函数的文档以确定限制的来源。
- 3622. 尝试读取只写文件。函数尝试生成的字符串过长。由于`Mata`中字符串的最大长度为 2,147,483,647 个字符，不太可能是`Mata`施加的限制。请检查该函数的文档以确定限制的来源。
- 3623. 尝试定位仅追加文件。函数尝试生成的字符串过长。由于`Mata`中字符串的最大长度为 2,147,483,647 个字符，不太可能是`Mata`施加的限制。请检查该函数的文档以确定限制的来源。
- 3698. 文件定位错误。尝试定位文件的无效部分，或由于其他原因定位失败；请参见 [M-5] fopen()。
- 3900. 内存不足。`Mata`内存不足；操作系统拒绝提供内存。没有`Mata`或`Stata`的设置可以影响此，也没有可以重置以获取更多内存。你必须解决操作系统的问题。
- 3901. 宏内存正在使用。此错误消息不应发生，如果发生过，请联系技术服务部门并报告该问题。
- 3930. LAPACK 例程错误。线性代数 LAPACK 例程——参见 [M-1] LAPACK——产生了`Mata`未预料到的错误。如果你应该收到此错误，请联系`Stata`公司。
- 3995. 未分配函数。此错误消息不应发生，如果发生过，请联系`Stata`公司。
- 3996. 内置未分配。此错误消息不应发生，如果发生过，请联系`Stata`公司。
- 3997. 未实现的操作码。此错误消息不应发生，如果发生过，请联系`Stata`公司。
- 3998. 栈溢出。你的程序嵌套深度过深。例如，想象通过递归调用自身来计算阶乘，然后请求 1e+100 的阶乘。在无限循环中调用自身的函数将导致此错误。
- 3999. 系统断言失败。`Mata`内部代码发生了意外情况。请联系技术服务并报告该问题。你不需要退出`Stata`或`Mata`。`Mata`已停止执行导致问题的操作。

## 另请

- [M-5] error() — 发布错误消息
- [M-2] intro — 语言定义

# [M-2] exp — 表达式

## 语法

exp

## 描述

`exp`用于语法图，表示“此处可以出现任何有效的表达式”。表达式的范围从简单的常量：

- 2
- "this"
- 3+2i

到变量名：

- A
- beta
- varwithverylongname

再到完整的标量、字符串或矩阵表达式：

```
sqrt(2)/2
substr(userid, 15, strlen(otherstr))
conj(X)*Y
```

## 备注

备注在以下标题下给出：

- 什么是表达式
- 赋值会抑制显示，(void) 亦如此
- 表达式的组成部分
- 数字字面量
- 字符串字面量
- 变量名
- 运算符
- 函数

## 什么是表达式

每个人都知道什么是表达式：表达式是像`2+3`和`invsym(X'*X)*Y'`这样的东西。简单的内容也是表达式，例如数值常量：

- 2 是一个表达式

以及字符串字面量：

- "hi there" 是一个表达式

以及函数调用：

```
sqrt(2) 是一个表达式
```

即使函数没有返回值（函数为 void），导致函数运行的代码也是一个表达式。例如，函数`swap()`（参见 [M-5] swap()）会交换其参数的值且不返回任何任何内容。尽管如此，

```
swap(A, B) 是一个表达式
```

## 赋值会抑制显示，(void) 亦如此

等号将表达式的结果赋值给变量。例如，

```
a = 2 + 3
```

将 5 赋值给`a`。当表达式的结果没有赋值给变量时，结果会在终端显示。这对于交互式输入的表达式和程序中编写的表达式都是如此。例如，给定程序：

```
function example(a, b)
{
  "the answer is"
  a+b
}
```

执行`example()`会产生：

```
: example(2, 3)
the answer is
5
```

5 的出现这一事实很容易理解；我们编写了表达式`a+b`但没有将它赋值给另一个变量。`"the answer is"`也出现的这一事实可能会让你感到惊讶。然而，我们在程序中编写了`"the answer is"`，这是一个表达式的示例，因为我们没有将其赋值给变量，所以它显示了。

在编程场景中，会有有时你想执行一个函数——称之为`setup()`——但不在乎函数返回什么，即使该函数不是 void（即它返回某些内容）。如果你这样写：

```
function example(...)
{
  setup(...)
  ...
}
```

结果将是显示`setup()`的返回值。你有两种替代方案。你可以将`setup()`的结果赋值给变量，尽管你之后不会使用该变量：

```
function example(...)
{
  result = setup(...)
  ...
}
```

或者你可以将结果类型强制转换为 void：

```
function example(...)
{
    (void) setup(...)
    ...
}
```

在表达式前面放置`(void)`可以防止结果被显示。

## 表达式的组成部分

表达式包含：

- 数字字面量
- 字符串字面量
- 变量名
- 运算符
- 函数

## 数字字面量

数字字面量就是数字：

- 2
- 3.14159
- -7.2
- 5i
- 1.213e+32
- 1.213E+32
- 1.921fb54442d18X+001
- 1.921fb54442d18X+001
- .a
- .b

但你可以在结尾加上一个`i`表示虚数，如上面的`5i`。要创建复数，你可以使用`+`运算符结合实数和虚数，如`2+5i`。在任何情况下，你可以在任何字面量的末尾加上`i`，例如`1.213e+32`是有效的，或者如`1.921fb54442d18X+001i`。

`1.921fb54442d18X+001`是一个看起来可怕的猛兽，无论是否有`i`都是如此。`1.921fb54442d18X+001`是二进制中表示浮点数的方式；它在 [U] **12.5 格式：控制数据的显示方式** 中描述。大多数人从未使用过它。

此外，数字字面量包括`Stata`的缺失值，`.a`、`.b`……`.z`。

复数变量可以像实变量一样包含缺失值，但它们只能有一个：`.a.bi`是不允许的。复数变量包含一个有效的复数值，或者包含`.a`、`.b`……`.z`。

## 字符串字面量

字符串字面量包含在双引号或复合双引号中：

```
"the answer is"
"a string"
""also a string"
""the "factor" of a matrix""
"""
"""



Mata 中的字符串包含 0 到 2,147,483,647 个字符。`""` 或 `"""` 是编写长度为 0 的字符串的方法。任何 ASCII 字符都可以出现在字符串字面量中，但没有规定在字符串字面量中输入不可打印字符。相反，你应该使用 `char()` 函数；参见 [M-5]。

（`e.w.` = elementwise）

## 运算符

运算符按优先级从低到高排序：

| 运算符 | 含义 | 文档 |
| :--- | :--- | :--- |
| `=` | 赋值 | [M-2] |
| `?` | 条件判断 | [M-2] |
| `#` | 矩阵连接 | [M-2] |
| `::` | 列连接 | [M-2] |
| `,` | 行连接 | [M-2] |
| `..` | 范围 | [M-2] |
| `\|` | 矩阵乘法积 | [M-2] |
| `*` | 乘法 | [M-2] |
| `&` | 逻辑与 | [M-2] |
| `\|` | 逻辑或 | [M-2] |
| `:=` | 赋值 | [M-2] |
| `==` | 等于 | [M-2] |
| `>=` | 大于等于 | [M-2] |
| `<=` | 小于等于 | [M-2] |
| `<` | 小于 | [M-2] |
| `>` | 大于 | [M-2] |
| `!==` | 不等于 | [M-2] |
| `+` | 加法 | [M-2] |
| `-` | 减法 | [M-2] |
| `++` | 递增 | [M-2] |
| `--` | 递减 | [M-2] |
| `+++` | 递增 | [M-2] |
| `---` | 递减 | [M-2] |

## 变量名

变量名区分大小写，且允许缩写：

```text
X

VariableName
```

变量名最大长度为 32 个字符。

# [M-2] `exp` — 表达式

## 语法

`exp`

## 描述

`exp` 用于语法图，表示“此处可以出现任何有效的表达式”。表达式的范围从简单的常量：

- `2`
- `"this"`
- `3+2i`

到变量名：

- `A`
- `beta`
- `varwithverylongname`

再到完整的标量、字符串或矩阵表达式：

```mata
sqrt(2)/2

substr(userid, 15, strlen(otherstr))

conj(X)*Y
```

## 备注

备注在以下标题下给出：

- 什么是表达式
- 赋值会抑制显示，`(void)` 亦如此
- 表达式的组成部分
- 数字字面量
- 字符串字面量
- 变量名
- 运算符
- 函数

## 什么是表达式

每个人都知道什么是表达式：表达式是像 `2+3` 和 `invsym(X'*X)*Y'` 这样的东西。简单的内容也是表达式，例如数值常量：

- `2` 是一个表达式

以及字符串字面量：

- `"hi there"` 是一个表达式

以及函数调用：

```mata
sqrt(2)
```

即使函数没有返回值（函数为 `void`），导致函数运行的代码也是一个表达式。例如，函数 `swap()`（参见 [M-5] `swap()`）会交换其参数的值且不返回任何内容。尽管如此：

```mata
swap(A, B)
```

仍然是一个表达式。

## 赋值会抑制显示，`(void)` 亦如此

等号将表达式的结果赋值给变量。例如：

```mata
a = 2 + 3
```

将 5 赋值给 `a`。当表达式的结果没有赋值给变量时，结果会在终端显示。这对于交互式输入的表达式和程序中编写的表达式都是如此。

例如，给定程序：

```mata
function example(a, b)
{
    "the answer is"
    a+b
}
```

执行 `example()` 会产生：

```text
: example(2, 3)

the answer is

5
```

5 的出现这一事实很容易理解；我们编写了表达式 `a+b`，但没有将它赋值给另一个变量。`"the answer is"` 也出现的这一事实可能会让你感到惊讶。然而，我们在程序中编写了 `"the answer is"`，这是一个表达式的示例，因为我们没有将其赋值给变量，所以它显示了。

在编程场景中，有时你想执行一个函数——称之为 `setup()`——但不在乎函数返回什么，即使该函数不是 `void`（即它返回某些内容）。如果你这样写：

```mata
function example(...)
{
    setup(...)
    ...
}
```

结果将是显示 `setup()` 的返回值。你有两种替代方案。你可以将 `setup()` 的结果赋值给变量，尽管你之后不会使用该变量：

```mata
function example(...)
{
    result = setup(...)
    ...
}
```

或者你可以将结果类型强制转换为 `void`：

```mata
function example(...)
{
    (void) setup(...)
    ...
}
```

在表达式前面放置 `(void)` 可以防止结果被显示。

## 表达式的组成部分

表达式包含：

- 数字字面量
- 字符串字面量
- 变量名
- 运算符
- 函数

## 数字字面量

数字字面量就是数字：

- `2`
- `3.14159`
- `-7.2`
- `5i`
- `1.213e+32`
- `1.213E+32`
- `1.921fb54442d18X+001`
- `.a`
- `.b`

但你可以在结尾加上一个 `i` 表示虚数，如上面的 `5i`。要创建复数，你可以使用 `+` 运算符结合实数和虚数，如 `2+5i`。在任何情况下，你可以在任何字面量的末尾加上 `i`，例如 `1.213e+32` 是有效的，或者如 `1.921fb54442d18X+001i`。

`1.921fb54442d18X+001` 是一个看起来可怕的猛兽，无论是否有 `i` 都是如此。`1.921fb54442d18X+001` 是二进制中表示浮点数的方式；它在 [U] **12.5 格式：控制数据的显示方式** 中描述。大多数人从未使用过它。

此外，数字字面量包括 Stata 的缺失值：`.a`、`.b`……`.z`。

复数变量可以像实变量一样包含缺失值，但它们只能有一个：`.a.bi` 是不允许的。复数变量包含一个有效的复数值，或者包含 `.a`、`.b`……`.z`。

## 字符串字面量

字符串字面量包含在双引号或复合双引号中：

```mata
"the answer is"

"a string"

""also a string"

""the "factor" of a matrix""

"""

"""
```

Mata 中的字符串包含 0 到 2,147,483,647 个字符。`""` 或 `"""` 是编写长度为 0 的字符串的方法。任何 ASCII 字符都可以出现在字符串字面量中，但没有规定在字符串字面量中输入不可打印字符。相反，你应该使用 `char()` 函数；参见 [M-5]。

## 变量名

变量名区分大小写，且允许缩写：

```mata
X

VariableName
```

变量名最大长度为 32 个字符。

## 函数

Mata 提供的函数在 [M-5] 中介绍。函数索引可以在 [M-4] `intro` 中找到。

## 参考文献

Gould, W. W. 2006. Mata Matters: Precision. Stata Journal 6: 550–560.

## 参见

[M-2] `intro` — 语言定义

# [M-2] `for` — `for (exp1; exp2; exp3) stmt`

## 语法

```mata
for (exp1; exp2; exp3) stmt

for (exp1; exp2; exp3) {
    stmts
}
```

`exp1` 和 `exp3` 是可选的，而 `exp2` 必须求值为实数标量（real scalar）。

## 描述

`for` 等价于：

```mata
exp1
while (exp2) {
    stmt(s)
    exp3
}
```

`stmt(s)` 执行零次或多次。只要 `exp2` 不等于 0，循环就会继续。

## 备注

为了理解 `for`，请输入以下程序：

```mata
function example(n)
{
    for (i=1; i<=n; i++) {
        printf("%g\n", i)
    }

    printf("done\n")
}
```

并运行 `example(3)`、`example(2)`、`example(1)`、`example(0)` 和 `example(-1)`。

`for` 的常见用法包括：

```mata
for (i=1; i<=rows(A); i++) {
    for (j=1; j<=cols(A); j++) {
        .
    }
}
```

## 参见

- [M-2] `semicolons` — 分号的使用
- [M-2] `do` — `do...while (exp)`
- [M-2] `while` — `while (exp) stmt`
- [M-2] `break` — 跳出 `for`、`while` 或 `do` 循环
- [M-2] `continue` — 继续进行 `for`、`while` 或 `do` 循环的下一次迭代
- [M-2] `intro` — 语言定义

# [M-2] 将函数传递给函数

## 语法

`example(...)`、`&somefunction()`，其中 `example()` 的代码为：

```mata
function example(..., f, ...)
{
    (*f)(...)
}
```

## 描述

函数可以接收其他函数作为参数。下面介绍了：

1. 如何调用一个接收函数作为参数的函数；
2. 如何编写一个接收函数作为参数的函数。

## 备注

备注位于以下标题下：

- 将函数传递给函数
- 编写接收函数的函数：简化约定
- 传递内置函数

## 将函数传递给函数

有人写了一个接收函数作为参数的程序。我们假设该函数是：

```mata
real scalar fderiv(function(), x)
```

且 `fderiv()` 在数值上计算 `function()` 在 `x` 处的导数。`fderiv()` 的文档要求你写一个接受一个参数并返回函数在该参数处求值的函数，例如：

```mata
real scalar expratio(real scalar x)
{
    return(exp(x)/exp(-x))
}
```

要调用 `fderiv()` 并使其计算 `expratio()` 在 3 处的导数，你的代码为：

```mata
fderiv(&expratio(), 3)
```

要将函数传递给函数，在函数名前加上 `&` 并再加上 `()`。编写 `&expratio()` 将函数 `expratio()` 的地址传递给 `fderiv()`。

[M-2] `ftof` — 将函数传递给函数 123

## 编写接收函数的函数：简化约定

为了接收函数，你在程序参数中包含一个变量来接收该函数——我们将使用 `f`，然后通过 `(*f)(...)` 调用传递的函数。`fderiv()` 的代码可能如下：

```mata
function fderiv(f, x)
{
    return ((*f)(x+1e-6) - (*f)(x)) / 1e-6
}
```

或者，如果你更喜欢显式声明：

```mata
real scalar fderiv(pointer scalar f, real scalar x)
{
    return ((*f)(x+1e-6) - (*f)(x)) / 1e-6
}
```

或者，如果你希望更加显式：

```mata
real scalar fderiv(pointer(real scalar function) scalar f)
{
    return ((*f)(x+1e-6) - (*f)(x)) / 1e-6
}
```

在任何情况下，使用指针时，输入 `(*f)...` 来执行传递的函数。更多信息请见 [M-2] `pointers`。

另外：函数 `fderiv()` 可以工作，但由于它使用的公式，将返回非常不准确的结果。

## 传递内置函数

你不能将内置函数传递给其他函数。例如 [M-5] `exp()` 是内置的，可以通过 [M-3] `mata` 发现：

```text
: mata which exp()

exp(): built-in
```

并不是所有官方函数都是内置的。许多函数在 Mata 库函数中实现，但 `exp()` 是内置的，编写 `&exp()` 将导致错误。如果你想将 `exp()` 传递给函数，请创建你自己的版本：

```mata
: function myexp(x) return(exp(x))
```

然后传递 `&myexp()`。

## 参见

[M-2] `intro` — 语言定义

# [M-2] `goto` — `goto label`

## 语法

```mata
label:
...
goto label
```

其中 `label:` 可能出现在 `goto` 之前或之后。

## 描述

`goto label` 控制跳转到 `label` 之后的语句。`label` 可以是任何八个字符内的名称。

## 备注

如今，良好的编程风格是避免使用 `goto`。在翻译 FORTRAN 程序时，`goto` 非常有用，例如：

```fortran
A = 4.0e0/3.0e0

10 B = A - 1.0e0

C = B + B + B

EPS = DABS(C - 1.0e0)
```



# [M-2] — 将函数传递给函数

## 语法

`example(...), &somefunction(), ...`

其中 `example()` 的代码为：

```
function example(..., f, ...)
{
    (*f)(...)
}
```

## 描述

函数可以接收其他函数作为参数。下面介绍了 (1) 如何调用一个接收函数作为参数的函数以及 (2) 如何编写一个接收函数作为参数的函数。

## 备注

备注位于以下标题下：
- 将函数传递给函数
- 编写接收函数的函数：简化约定
- 传递内置函数

# [M-2] op_arith — 算术运算符

## 语法

```
[M-2] op_arith — 算术运算符
```

- `a + b` 加法
- `a - b` 减法
- `a * b` 乘法
- `a / b` 除法
- `a ^ b` 幂
- `-a` 负号

其中 `a` 和 `b` 可以是矩阵。

## 描述

上述运算符执行基础算术运算。

## 备注

参见 [M-2] colon。

# 赋值会抑制显示

当你交互式地输入表达式或在程序中使用不带等号赋值运算符编写一个表达式时，该表达式的结果将显示在终端上：

```
: 2 + 3
5
```

当你将表达式赋值给变量时，结果不会显示：

```
: x = 2 + 3
```

# 等号赋值运算符

等号是一个运算符，因此除了编写

```
a = 2 + 3
```

，你还可以编写

```
a = b = 2 + 3
```

或者

```
y = x / (denominator = sqrt(a+b))
```

或者甚至

```
y1 = y2 = x / (denominator = sqrt(sum=a+b))
```

最后一种情况等同于

```
sum = a + b
denominator = sqrt(sum)
y2 = x / denominator
y1 = y2
```

等号的结合性是弱的，所以

```
a = b = 2 + 3
```

被解释为

```
a = b = (2 + 3)
```

而不是

```
a = (b=2) + 3
```

# lvals，出现在左侧的内容

出现在等号左侧的内容被称为 `lval`，left-hand-side value（左值）的缩写。例如，编写

```
sqrt(4) = 3
```

是没有意义的，事实上，你不编写这样的代码，因为 `sqrt(4)` 不是一个 `lval`：

```
sqrt(4) = 3
invalid lval
r(3000);
```

`lval` 是任何可以存储值的对象。标量（scalar）可以存储值

```
a = 3
x = sqrt(4)
```

矩阵可以存储值

```
A = (1, 2 \ 3, 4)
B = invsym(C)
```

矩阵行可以存储值

```
A[1..] = (7, 8)
```

矩阵列可以存储值

```
A[.,.] = (9 \ 10)
```

最后，矩阵元素可以存储值

```
A[1,2] = 7
```

`lval` 通常是上述形式之一。其他形式与指针变量有关，大多数程序员从不使用；它们在下方的 `Pointer_lvals` 中进行了讨论。

# 行、列和元素 lvals

当你向矩阵的行、列或元素赋值时，

```
A[1.,] = (7, 8)
A[.,2] = (9 \ 10)
A[1,2] = 7
```

该行、列或元素必须已经存在：

```
A = (1, 2 \ 3, 4)
A[3,4] = 4
```

```
<stmt>: 3301 subscript invalid
r(3301);
```

这通常不是一个问题，因为在你向行、列或元素赋值时，矩阵已经创建好了，但在需要先创建它的情况下，请使用 `J()` 函数。以下代码创建一个 3 x 4 矩阵，包含其索引之和：

```
A = J(3, 4, .)
for (i=1; i<=3; i++) {
    for (j=1; j<=4; j++) A[i,j] = i + j
}
```

# 指针 lvals

除了标准的 `lval`

```
A = (1, 2 \ 3, 4)
A[1..] = (7, 8)
A[.,2] = (9 \ 10)
A[1,2] = 7
```

还允许指针 `lval`。例如，

```
*p = 3
```

将 3 存储在指针标量 `p` 指向的地址中。

```
(*q) [1,2] = 4
```

将 4 存储在指针标量 `q` 指向的地址的 (1,2) 元素中，而

```
*Q[1,2] = 4
```

将 4 存储在指针矩阵 `Q` 的 (1,2) 元素指向的地址中。

```
*Q[2,1] [1,3] = 5
```

等同于

```
(*Q[2,1])[1,3] = 5
```

并将 5 存储在指针矩阵 `Q` 的 (2,1) 元素指向的地址的 (1,3) 元素中。

指针的指针、指针的指针的指针等也是允许的。例如，

```
**r = 3
```

将 3 存储在指针标量 `r` 指向的地址指向的地址中，

```
*(*((Q[1,2])) [2,1]) [3,4] = 7
```

将 7 存储在指针矩阵 `Q` 的 (1,2) 地址指向的 (2,1) 地址指向的 (3,4) 地址中。

## 兼容性 (Conformability)

```
a = b:
input:
b:   r × c
output:
a:   r × c
```

## 诊断 (Diagnostics)

如果内存不足以在 `a` 中存储 `b` 的副本，`a = b` 将中止。

## 另见

- `swap()` — 交换变量内容
- `exp` — 表达式
- `intro` — 语言定义

# [M-2] op_colon — 冒号运算符

## 语法

`a : b` 加法
`a : - b` 减法
`a : * b` 乘法
`a : / b` 除法
`a : ^ b` 幂
`a == b` 等于
`a != b` 不等于
`a > b` 大于
`a >= b` 大于等于
`a < b` 小于
`a <= b` 小于等于
`a : b` 逻辑与

## 描述

冒号运算符执行逐元素操作。

## 备注

冒号运算符的兼容性，如下：

`a ? b : c` 三元运算符

## 兼容性

```
a ? b : c
a: 1 × 1
b: r1 × c1
c: r2 × c2
result: r1 × c1 or r2 × c2
```

## 诊断

在 `a ? b : c` 中，如果 `a` 为真则评估 `b`，如果 `a` 为假则评估 `c`。然而，`++` 和 `--` 运算符总是会被执行：

`(k==0 ? i++ : j++)` 无论 `k` 的值如何，都会增加 `i` 和 `j`。

## 另见

- `exp` — 表达式
- `intro` — 语言定义

# [M-2] op_increment — 增减运算符

## 语法

`++i` 递增
`--i` 递减

`i++` 递增后
`i--` 递减后

其中 `i` 必须是标量。

## 描述

`++i` 和 `i++` 增加 `i`；它们执行 `i=i+1` 的操作。`++i` 在表达式求值之前执行操作，而 `i++` 在之后执行。
`--i` 和 `i--` 减少 `i`；它们执行 `i=i-1` 的操作。`--i` 在表达式求值之前执行操作，而 `i--` 在之后执行。

## 备注

这些运算符用于代码中，例如

```
x[i++] = 2
x[--i] = 3
...
for (i=0; i<100; i++) {
...
}
if (++n > 10) {
...
}
```

在这些表达式出现的地方，结果就像是替换了当前的 `i` 值，并且 `i` 增加了，无论是在表达式求值之前还是之后。例如，

`x[i++] = 2`

等同于

`x[i] = 2 ; i = i + 1`

以及

`x[++i] = 3`

等同于

`i = i + 1 ; x[i] = 3`

编码

```
for (i=0; i<100; i++) {
  ...
}
```

或

```
for (i=0; i<100; ++i) {
  ...
}
```

等于

```
for (i=0; i<100; i=i+1) {
  ...
}
```

因为无论增量操作是在原本为空的表达式之前还是之后执行都没有影响。

```
if (++n > 10) {
  ...
}
```

等于

```
n = n + 1
if (n > 10) {
  ...
}
```

而

```
if (n++ > 10) {
  ...
}
```

等于

```
if (n > 10) {
  n = n + 1
  ...
} else n = n + 1
```

`++` 和 `--` 运算符只能用于实数标量（real scalars），通常与索引或计数相关。它们能产生快速且可读良好的代码。

## 符合性

- `++i`, `--i`, `i++`, 和 `i--`:
  `i`: 1 x 1
  结果: 1 x 1

## 诊断

`++` 和 `--` 允许用于实数标量。也就是说，假设 `i` 是实数标量，则 `++i` 或 `i++` 是合法的，而 `x[i,j]++` 是无效的。

对非实数标量的变量应用 `++` 和 `--` 会报错。

`++i`, `i++`, `--i`, 和 `i--` 应该是表达式中对 `i` 的唯一引用。请勿编写如下代码，例如

```
x[i++] = y[i]
x[++i] = y[i]
x[i] = y[i++]
x[i] = y[++i]
```

上述表达式中 `i` 的值在形式上是未定义的；无论其值为何，你都无法依赖该值是由编译器的早期或后期版本获取的。相反，根据所需的结果编写：

```
++i; x[i] = y[i]
```

或者编写

```
x[i] = y[i] ; i++
```

然而，编写以下代码是非常合理的

```
x[++i] = y[j++]
```

也就是说，同一个表达式中可以出现多个 `++` 和 `--` 运算符；必须避免对 `++` 和 `--` 目标的多次引用。

## 参见

- [M-2] `exp` — 表达式
- [M-2] `intro` — 语言定义

# [M-2] op_join — 行连接和列连接运算符

## 语法

`a , b`

`a \ b`

## 描述

`，` 和 `\` 是 Mata 的行连接和列连接运算符。

## 备注

按以下标题给出：

- 逗号和反斜杠是运算符
- 逗号作为分隔符
- 关于误用逗号和反斜杠运算符的警告

## 逗号和反斜杠运算符

`，` 和 `\` 是运算符，这一点怎么强调都不为过。当你输入

```
: (1, 2 \ 3, 4)
```

| 1 | 2 |
|---|---|
| 1 | 3 |
| 2 | 4 |

人们不禁想：“啊，逗号和反斜杠是在输入矩阵时分隔元素的方法。”如果你这样想，你就无法体会 `，` 和 `\` 的威力。`，` 和 `\` 是运算符，程度与 `*` 和 `+` 运算符相同。

`,` 是接收 $r \times c_1$ 矩阵和 $r \times c_2$ 矩阵并返回 $r \times (c_1 + c_2)$ 矩阵的运算符。

`\` 是接收 $r_1 \times c$ 矩阵和 $r_2 \times c$ 矩阵并返回 $(r_1 + r_2) \times c$ 矩阵的运算符。

`，` 和 `\` 可以用于标量、向量或矩阵：

```
: a = (1 \ 2)
: b = (3 \ 4)
: a , b
```

| 1 | 2 |
|---|---|
| 1 | 3 |
| 2 | 4 |

```
: c = (1, 2)
: d = (3, 4)
: c \ d
```

| 1 | 2 |
|---|---|
| 1 | 3 |
| 2 | 4 |

`，` 的优先级比 `\` 紧，这意味着 `e, f\g, h` 被解释为 `(e, f) \ (g, h)`。在这里，`，` 和 `\` 与 `*` 和 `+` 运算符不同：`*` 的优先级比 `+` 紧，且 `e*f + g*h` 被解释为 `(e*f)+(g*h)`。

正如有时输入 `e*(f+g)*h` 有意义一样，输入 `e, (f\g), h` 也可能有意义：

```
: e = 1 \ 2
: f = 5 \ 6
: g = 3
: h = 4
: e, (g\h), f
```

| 1 | 1 | 3 | 5 |
|---|---|---|---|
| 2 | 2 | 4 | 6 |

## 逗号作为分隔符

`，` 在 Mata 中有第二含义：它是函数的参数分隔符。在 `myfunc(a, b)` 括号内的逗号不是行连接运算符：它是参数分隔符。如果你想调用第二个参数等于行向量 `(1,2)` 的 `myfunc()`，你必须输入

```
myfunc(a, (1,2))
```

而不是

```
myfunc(a, 1, 2)
```

否则 Mata 会认为你在参数列表内部使用了逗号，将其恢复到行连接含义。

## 关于误用逗号和反斜杠运算符的警告

误用或仅仅使用 `，` 和 `\` 会显著降低代码执行速度。当你使用 `，` 和 `\` 时，Mata 必须分配一个包含 `rows(a)` 的矩阵或向量，然后将 `a` 复制到新矩阵，然后复制 `c`。什么还没有发生，但现在

接上文。Mata 必须分配一个包含 `rows(a)` 的矩阵或向量，然后将 `(a \ b)` 复制到新矩阵，然后复制 `c`。发生了一些：`a` 被复制了两次！编码

```
res = (a \ b)
```

是方便的，但如果编写

```
res = J(rows(a)+rows(b), cols(a), .)
res[1..rows(a), .] = a
res[rows(a)+1..rows(a)+rows(b), .] = b
```

由于通常，即使在循环中，效率问题也会变得重要。上述运算符在标量上的工作正如你预期的那样，并且比较运算符和 `not` 运算符已经泛化到矩阵的使用。

`a==b` 如果 `a` 和 `b` 是 p-符合的、相同类型的，且对应的元素相等，则求为真。相同类型意味着 `a` 和 `b` 都是数值型、字符串型或指针。因此，询问一个 `n×2` 矩阵是否等于一个 `n×1` 向量或字符串变量是否等于实数变量并不是错误的；它们不相等。此外，如果 `a` 或 `b` 是 p-符合且行数或列数为零，则声明 `a==b` 为真。

```
a , b:
a: r × c1
b: r × c2
结果: r × (c1+c2)
```

```
a \ b:
a: r1 × c
b: r2 × c
结果: (r1 + r2) × c
```

如果 `a` 和 `b` 不是同一类型，`，` 和 `\` 会报错。

## 参见

- [M-2] `exp` — 表达式
- [M-2] `intro` — 语言定义

# [M-2] op_kronecker — Kronecker 积运算符

## 语法

`A#B`

其中 `A` 和 `B` 可以是实数或复数。

## 描述

`A#B` 返回 Kronecker 积。`#` 的优先级非常紧：`X*A#B*Y` 被解释为 `X*(A#B)*Y`。

## 备注

Kronecker 积也称为 Kronecker 积、直积、张量积和外积。Kronecker 积 `A#B` 是矩阵 `||a_{ij}*B||`。

## 符合性

`A#B`:
`A`: r1 × c1
`B`: r2 × c2
结果: r1*r2 × c1*c2

## 诊断

无。Leopold Kronecker (1821–1891) 出生于普鲁士的 Liegnitz（现波兰 Legnica），富家。他就读于柏林、波恩和布雷斯劳大学，完成了关于单位根的博士论文。多年来，Kronecker 在从事商业事务的同时致力于数学，特别在数论、椭圆函数和方程理论方面发表过。后来他在柏林大学授课，这是他作为科学院成员的权利。1883 年，他被任命为主席。Kronecker 开始认为数学参数应该只包含有限数字和有限次操作，这导致了与研究无理数或非构造性存在证明的人在数学和个人上日益增加的分歧。

## 参考

James, I. 2002. Remarkable Mathematicians: From Euler to von Neumann. Cambridge: Cambridge University Press.

## 参见

- [M-2] `exp` — 表达式
- [M-2] `intro` — 语言定义

# [M-2] op_logical — 逻辑运算符

## 语法

```
a == b    如果 a 等于 b 则为真
a != b    如果 a 不等于 b 则为真
a > b     如果 a 大于 b 则真
a >= b    如果 a 大于等于 b 则真
a < b     如果 a 小于 b 则真
a <= b    如果 a 小于等于 b 则真
!a        逻辑取非；如果 a==0 则真，否则为假
a & b     如果 a!=0 且 b!=0 则真
a | b     如果 a!=0 或 b!=0 则真
```

## 描述

逻辑运算符用于执行逻辑运算。

## 备注

逻辑运算符通常用于条件表达式中。

## 参见

- [M-2] `exp` — 表达式
- [M-2] `intro` — 语言定义

# 参考文献

Gould, W. W. 2006. Mata Matters: Precision. Stata Journal 6: 550–560.

# 参见

- [M-2] `semicolons` — 分号的使用
- [M-2] `do` — `do...while (exp)`
- [M-2] `while` — `while (exp) stmt`
- [M-2] `break` — 跳出 `for`, `while` 或 `do` 循环
- [M-2] `continue` — 继续进行 `for`, `while` 或 `do` 循环的下一次迭代
- [M-2] `intro` — 语言定义



`a && b`　`a & b` 的同义词

`a || b`　`a | b` 的同义词

## [M-2] op_logical — 逻辑运算符

### 描述

上述运算符执行逻辑比较，运算符`!`执行逻辑取反。所有运算符都求值为`1`或`0`，意味着真或假。

### 备注

按以下标题给出备注：

- 引言
- 在指针上使用逻辑运算符

## 引言

上述运算符在标量上的工作正如你预期的那样，并且比较运算符和`not`运算符已经泛化到矩阵的使用。

`a==b`：如果`a`和`b`是 p-符合的、相同类型的，且对应的元素相等，则求为真。相同类型意味着`a`和`b`都是数值型、字符串型或指针。因此，询问一个`nx2`矩阵是否等于一个`n×1`向量或字符串变量是否等于实数变量并不是错误的；它们不相等。此外，如果`a`或`b`是 p-符合且行数或列数为零，则声明`a==b`为真。

`a!=b`等于`(!(a==b)`；`a!=b`如果`a==b`求为假，则求为真，否则求为真。

剩余的比较运算符`>`、`>=`和`<=`的工作方式与`==`和`!=`不同，它们要求`a`和`b`必须 p 兼容（p-conformable），如果不符合，将报错并终止。如果对应的元素具有所述关系，则返回 true，否则返回 false。如果`a`或`b`是复数，则根据复数向量的长度进行比较；`a>b`等于`abs(a)>abs(b)`，因此`-3>2+0i`为真。

当`a`为标量时，`!a`如果`a`不等于零值为`0`，否则为`1`。应用于向量或矩阵时，按元素执行相同的操作：`!(-1,0,1,2,..)`等于`(0,1,0,0,0)`。

`&`和`&&`（与或）仅用于标量。由于许多人熟悉 C 语言编程，Meta 将`&&`作为`&`的同义词，将`||`作为`|`的同义词。

## 在指针上使用逻辑运算符

在指针表达式中，`NULL`被视为假，所有其他指针值（地址值）都被视为真。因此，以下代码等同于：

```text
pointer x               pointer x

if (x) {                if (x!=NULL) {

}                                 }
```

逻辑运算符`a==b`、`a!=b`、`a&b`和`a|b`可用于指针。

## 可转换性

| 表达式 | `a` | `b` | 结果 |
| :--- | :--- | :--- | :--- |
| `a==b`、`a!=b` | `a: r1 X c1` | `b: r2 X c2` | `1 X 1` |
| `a>b`、`a>=b`、`a<b`、`a<=b` | `a: r x c` | `b: r x c` | `1 x 1` |
| `!a` | `a: r x c` | - | `r x c` |
| `a&b`、`a|b` | `a: 1 X 1` | `b: 1 X 1` | `1 X 1` |

## 诊断

`a==b`和`a!=b`不会失败。

`a>b`、`a>=b`、`a<b`、`a<=b`如果`a`和`b`不 p 兼容、`a`和`b`不属于相同通用类型（数值与数值或字符串与字符串），或`a`或`b`为指针，则报错。

`!a`如果`a`不是实数则报错。

`a&b`和`a|b`如果`a`和`b`不是实数或不同指针，则报错。如果`a`和`b`是指针，指针值`NULL`被视为假，所有其他指针值被视为真。在所有情况下，返回等于`0`或`1`的实数。

## 另见

- [M-2] `exp` — 表达式
- [M-2] `intro` — 语言定义

# [M-2] op_range — 范围运算符

## 语法

- `a..b` 行范围
- `a::b` 列范围

## 描述

范围运算符创建从`a`到`b`计数的向量。

`a..b`返回行向量。

`a::b`返回列向量。

## 备注

- `a..b`和`a::b`从`a`开始计数直到但不超过`b`。如果`b>=a`则递增`1`，如果`b<a`则递减`1`。
- `1..4`创建行向量`(1,2,3,4)`。
- `1::4`创建列向量`(1\2\3\4)`。
- `-1..4`创建行向量`(-1,-2,-3,-4)`。
- `-1::-4`创建列向量`(-1\-2\-3\4)`。
- `1.5..4.5`创建行向量`(1.5, 2.5, 3.5, 4.5)`。
- `1.5::4.5`创建列向量`(1.5\2.5\3.5\4.5)`。
- `1.5..4.4`创建行向量`(1.5, 2.5, 3.5)`。
- `1.5::4.4`创建列向量`(1.5\2.5\3.5)`。
- `-1.5..-4.4`创建行向量`(-1.5,-2.5,-3.5)`。
- `-1.5::-4.4`创建列向量`(-1.5\-2.5\-3.5)`。
- `1..1`和`1::1`都返回`(1)`。

## 兼容性

```text
a..b

a: 1 × 1

b: 1 × 1

result: 1 × trunc(abs(b - a)) + 1
```

```text
a::b

a: 1 × 1

b: 1 × 1

result: 1 × trunc(abs(b - a)) + 1
```

## 诊断

`a..b`和`a::b`如果`a>=`或`b>=`则返回缺失（missing）。

## 另见

- [M-2] `exp` — 表达式
- [M-2] `intro` — 语言定义

# [M-2] op_transpose — 共轭转置

## 语法

`A'`

## 描述

`A'`返回`A`的转置，如果`A`是复数，则返回共轭转置。

## 备注

后置运算符可用于任何类型的矩阵或向量：实数、复数、字符串或指针：

- `a`: 1 2 3 | 1 2 3 | 2 4 5
- `a'`: 1 2 | 1 4 | 2 5
- `s`: 1 2 | 1 alpha
- `s'`: 1 2 | 1 alpha beta
- `p`: 1 2 | 1 2058 | 2 368 | 1d2058 | 2ba368
- `p'`: 1 2 | 1d2058 | 2ba368

### 转置运算符

- `z`: 1 2 | 1+2i | 3+4i | 5+6i | 7+8i
- `z'`: 1 2 | 1-2i | 3-4i | 5-6i | 7-8i

`'`应用于复数时，返回共轭转置。如果你不想要这样，`conj(z')`——`conj(z)`——没有区别；见 [M-5] `conj()`。

```text
conj(z')
```

- 1 2 | 1+2i | 3+4i | 5+6i | 7+8i

或者使用`transposeonly()`函数；见 [M-5] `transpose()`：

```text
transposeonly(z)
```

- 1 2 | 1+2i | 3+4i | 5+6i | 7+8i

`transposeonly()`执行得比`conj(z')`快。

对于实数和复数`A`，见 [M-5] `transpose()`，它提供了原地转置的方法并节省内存。

## 兼容性

| `A'` | `r × c` |
| :--- | :--- |
| `result:` | `c × r` |

## 诊断

转置运算符不会失败，但在处理复数时很容易误用。

用户想要形成`A*`，但当他尝试时，得到了兼容性错误。他认为`A`是列向量，但实际上是行向量。无论如何，他随后修正了`A*`，程序运行正常并产生了正确的答案。在测试中，`A`是实数。

后来，他用复数`A`运行程序，生成了错误的结果，尽管他过了一会儿才注意到。在考虑`A'`之前，转置运算符没有将`A`从行变为列，而是对`A`的每个元素取了共轭！他将代码改为`A*transposeonly()`。

用户无疑疑惑为什么`'`运算符没有被定义为等同于`transposeonly()`。如果是那样的话，与其讲述一个想要转置却被共轭转置的故事，不如说讲述一个需要共轭转置却被转置的故事。事实上，后者比前者多。

## 另见

- [M-5] `conj()` — 共轭
- [M-5] `transpose()` — 原地转置
- [M-5] `transposeonly()` — 不共轭转置
- [M-2] `exp` — 表达式
- [M-2] `intro` — 语言定义

# [M-2] optargs — 可选参数

## 语法

```text
function functionname(larg [, arg, ...]) {...}

function functionname(arg, larg [, ...]) {...}

function functionname(arg, arg, ...) {...}
```

竖线分隔必需参数和可选参数。竖线最多出现一次。

## 描述

Meta 函数可以有不同数量的参数。下面描述了如何编写允许可选参数的程序。

## 备注

备注位于以下标题下：

- 什么是可选参数？
- 如何编写可选参数
- 示例

## 什么是可选参数？

### 示例 1

你写了一个名为`ditty()`的函数。`ditty()`允许调用者指定两个或三个参数：

```text
real matrix ditty(real matrix A, real matrix B, real scalar scale)
real matrix ditty(real matrix A, real matrix B)
```

调用者只指定两个参数，结果相当于调用者指定的第三个参数等于：即`ditty(A, B)`等于

### 示例 2

你写了一个函数`gash()`。`gash()`允许调用者指定一个或两个参数：

```text
real matrix gash(real matrix A, real matrix B)
real matrix gash(real matrix A)
```

调用者只指定一个参数，结果相当于为第二个参数指定了`J(0,))`。

### 示例 3

你写了一个函数`easygoing()`。`easygoing()`取三个参数，但允许调用者指定三个、两个、一个，甚至没有参数：

```text
real scalar easygoing(real matrix A, real matrix B, real scalar scale)

real scalar easygoing(real matrix A, real matrix B)

real scalar easygoing(real matrix A)

real scalar easygoing()
```

如果没有指定`scale`，结果相当于指定了`scale = 1`。如果没有指定`B`，结果相当于指定了`B = A`。如果没有指定`A`，结果相当于指定了`A = I(2)`。

### 示例 4

你写了一个函数`midsection()`。`midsection()`取三个参数，但用户可以只指定两个——第一个和最后一个。

```text
real matrix midsection(real matrix A, real vector w, real matrix B)

real matrix midsection(real matrix A, real matrix B)
```

如果没有指定`w`，结果相当于指定了`w = J(1,cols(A),1)`。

## 如何编写可选参数

当你编写：

```text
function nebulous(a, b, c)
{
    ...
}
```

你表示函数`nebulous()`需要三个参数。如果调用者指定的少于或多，执行将终止。

如果你编写：

```text
function nebulous(a, b, |c)
{
    ...
}
```

你表示最后一个参数是可选的。注意`c`前面的竖线。

# [M-2] optargs — 可选参数

如果你编写代码：

```text
function nebulous(a, b, |c)
{
    ...
}
```

你是在表示最后两个参数是可选的；用户可以指定一个、两个或三个参数。

如果你编写代码：

```text
function nebulous(|a, b, c)
{
    ...
}
```

你是在表示所有参数都是可选的；用户可以指定零、一个、两个或三个参数。

用户未指定的参数将根据参数的类型进行填充。

| 如果参数类型是…… | 默认值将为…… |
| :--- | :--- |
| 未声明 | `J(0, 0, .)` |
| 变换矩阵 | `J(0, 0, .)` |
| 实数矩阵 | `J(0, 0, .)` |
| 复数矩阵 | `J(0, 0, 1i)` |
| 字符串矩阵 | `J(0, 0, "NULL")` |
| 指针矩阵 | `J(0, 0, NULL)` |
| 变换行向量 | `J(1, 0, .)` |
| 实行向量 | `J(1, 0, .)` |
| 复数行向量 | `J(1, 0, 1i)` |
| 字符串行向量 | `J(1, 0, "NULL")` |
| 指针行向量 | `J(1, 0, NULL)` |
| 变换列向量 | `J(0, 1, .)` |
| 实数列向量 | `J(0, 1, .)` |
| 复数列向量 | `J(0, 1, 1i)` |
| 字符串列向量 | `J(0, 1, "NULL")` |
| 指针列向量 | `J(0, 1, NULL)` |
| 变换向量 | `J(1, 0, .)` |
| 实数向量 | `J(1, 0, .)` |
| 复数向量 | `J(1, 0, 1i)` |
| 字符串向量 | `J(1, 0, "NULL")` |
| 指针向量 | `J(1, 0, NULL)` |
| 变换标量 | `J(1, 1, .)` |
| 实数标量 | `J(1, 1, .)` |
| 复数标量 | `J(1, 1, C(..))` |
| 字符串标量 | `J(1, 1, "NULL")` |
| 指针标量 | `J(1, 1, NULL)` |

此外，函数`args()`（参见 [M-5] `args()`）将返回用户指定的参数数量。

竖线只能指定一次。正如我们将看到的，这足够了。

## 重温示例

### 示例 1

在这个示例中，实数矩阵函数`ditty(A, B, scale)`允许实数标量`scale`可选。如果没有指定`scale`，结果就像指定了`scale=.`。可以编码：

```text
real matrix ditty(real matrix A, real matrix B, |real scale)
{
}
```

代码体的编写方式与`scale`不是可选的一样，因为如果调用者没有指定该参数，根据上表，缺失的参数将自动填充。

### 示例 2

实数矩阵函数`gash(A, B)`允许实数矩阵`B`可选，如果没有指定，则假设`B = J(0,0,..)`。因此，其编码方式与示例 1 直接：

```text
real matrix gash(real matrix A, |real matrix B)
{
}
```

### 示例 3

实数标量`easygoing(A, B, scale)`允许所有参数都可选。假设`scale = 1`、`B = A`，并在必要时`A = I(2)`。

```text
real scalar easygoing(real matrix A, real matrix B, |real scale)
...
```

### 示例 4

实数矩阵函数`midsection(A, w, B)`允许省略参数`w`。如果未指定`w`，则假设`w = J(1, cols(A))`。这里有一个解决方案：

```text
real matrix midsection(a1, a2, |a3)
{
    if (args()==3) return(midsection_u(a1, a2))
    else return(midsection_u(a1, J(1, cols(a1)), a2))
}

real matrix midsection_u(real matrix A, real vector w, real matrix B)
...
```

我们不会告诉调用者`midsection_u()`的存在，尽管`midsection_u()`是我们的程序。我们上面做的是让`midsection()`接收两个或三个参数，然后在正确的位置调用了`midsection_u()`。

另见 [M-2] `intro` — 引言

# [M-2] pointers — 指针

## 语法

```text
pointer[otype] orgtype [function]
```

其中`otype`是：

```text
[otype] orgtype [function]
```



且 `toype` 和 `orgtype` 是：

| `totype` | `orgtype` |
| --- | --- |
| `polymorphic` | `matrix` |
| `numeric` | `vector` |
| `real` | `rowvector` |
| `complex` | `colvector` |
| `string` | `scalar` |
| `pointer[otype]` | |

`pointer[otype] orgtype [function]` 可用于声明前、参数声明或变量定义。

## 描述

指针是包含其他对象地址的对象。`*` 运算符获取地址的内容。因此，如果 `p` 是指针，`*p` 指向它所指向的对象的内容。指针是一个高级编程概念。大多数程序（包括复杂的程序）都可以不用指针编写。然而，指针用于：

1. 将一组对象放在一个名称下并
2. 传递函数。

传递函数不需要理解指针的所有知识；见 `pointers-of`。

## 备注

- 什么是指针？
- 变量的指针
- 表达式的指针
- 函数的指针
- 指针的指针
- 指针数组
- 混合指针数组
- `NULL` 的定义
- 括号的使用
- 指针算术
- 列出指针
- 指针的声明
- 对象的指针的使用
- 效率

## 什么是指针？

指针是变量或函数的地址。假设地址包含一个矩阵。另一个变量可能包含 `327916`，如果存储了 `X`，则认为 `p` 指向 `X`。地址以十进制写，与其 `p` 包含 `327916`，我们更可能说 `p` 包含 `0x3ea8`，这是我们在十六进制中写数字的方式。无论我们如何写地址，`p` 都包含数字，该数字对应另一个变量的地址。在我们的程序中，如果我们引用 `p`，我们引用 `p` 的内容，即数字 `0x3ea8`。单目运算符 `*` 定义为“引用地址的内容”或“解引用”：`*p` 意味着 `X`。我们可以编码 `Y = *p` 或 `Y = X`，无论如何都会相同的结果。在我们的程序中，我们可以引用 `X[i,j]` 或 `(*p)[i,j]`，无论如何都会得到 `X` 的 `i,j` 元素。

单目运算符 `&` 是我们将地址放入 `p` 的方式。为了给 `p` 加载地址，我们编码 `p = &X`。特殊地址 `0`（零，十六进制表示也称为 `0X`）是记录指针变量指向空的方法。指针变量包含 `NULL` 或包含另一个变量的地址。它包含一个函数的地址。假设 `p` 包含 `0x3ea8` 且不是矩阵 `X` 的地址，而是函数 `f()`。为了将 `f()` 的地址放入 `p`，正如我们之前编码 `p = &X` 一样，我们编码 `p = &f(0)`。结尾的 `()` 告诉我们需要函数的地址。无论 `f()` 需要多少个参数，我们在结尾都编码 `()`，因为我们不是在执行 `f()`，只是获取它的地址。为了在其地址处执行函数，现在我们假设 `f()` 接收两个参数并调用它们为 `i` 和 `j`——`(*p)(i,j)`，就像当 `p` 包含矩阵 `X` 地址时我们编码 `(*p)[i,j]`

## 变量的指针

要创建一个变量的指针 `p`，你编码：

```
p = &varname
```

例如，`X` 是一个矩阵：

```
p = &X
```

在 `p` 中存储 `X` 的地址。随后，引用 `*p` 和引用 `X` 等于同一件事。如果 `X` 包含一个 3x3 矩阵且你编码：

```
*p = Hilbert(4)
```

那么你就会发现 `X` 包含了 4x4 的 Hilbert 矩阵。`X` 和 `*p` 是同一个矩阵。

如果 `X` 包含一个 3x3 且你编码：

```
(*p)[2,3] = 4
```

你将发现 `X[2,3]` 等于 4。

然而，你不能指向对象的内部。也就是说，你不能编码

```
p = &X[2,3]
```

并得到一个等同于 `X[2,3]` 的指针，即使你之后编码 `*p=2`；你会在 `X[2,3]` 中看到变化。我们将在下文的“表达式的指针”中解释。

顺便说，变量可以通过指针来维持存在。考虑以下程序：

```
pointer(real matrix) scalar example(real scalar n)
{
    real matrix tmp
    tmp = I(3)
    return(&tmp)
}
```

通常，变量 `tmp` 在 `example()` 执行结束后会被销毁。在这里，`tmp` 的存在通过对它的指针维持。我们可能会编码：

```
p = example(3)
```

结果是 `*p` 包含 3x3 的单位矩阵。当该矩阵不再被引用时，消耗的内存将被释放，这将在 `p` 本身被释放时，或在此之前 `p` 的值改变时，例如通过

```
p = NULL
```

关于结构体的指针，见 [M-2] struct。关于类的指针，见 [M-2] class。

## 表达式的指针

你可以编写：

```
p = &(2+3)
```

结果将创建一个*包含 5 的 p*。Mata 会创建一个临时变量来存储该表达式的求值结果，并将 `p` 设置为该临时变量的地址。当 `p` 被释放时，或者在此之前当 `p` 的值被改变时，该临时变量将被释放，正如在前一节的示例中 `tmp` 被释放的一样。

当你编写：

```
p = &X[2,3]
```

结果是相同的。表达式被求值，其结果被存储在一个临时变量中。这就是为什么随后编写 `*p=2` 不会改变 `X[2,3]`。`*p=2` 做的只是改变了临时变量的值。

将指针赋值为表达式的值是有用的。在下面的代码段中，创建 `n` 个 5 × 5 矩阵供以后使用：

```
pvec = J(1, n, NULL)
for (i=1; i<=n; i++) pvec[i] = &(J(5, 5, .))
```

## 函数的指针

当你编写：

```
p = &functionname
```

函数的地址被存储在 `p` 中。你稍后可以通过以下代码执行该函数：

> ... `(*p)(..)`

仔细区分：

```
p = &functionname
```

和

```
p = &(functionname())
```

后者将执行不带参数的 `functionname()`，然后将返回的结果赋值给一个临时变量。

例如，假设你想编写一个 `neat()` 函数，该函数将计算另一个函数的导数，你将该函数传递给 `neat()`。我们假定你的函数返回一个实数标量。

你可以这样操作：

```
real scalar neat(pointer(function) p, other args...)
{
  ...
```

尽管你对传递给你的函数的特征可以描述得更明确：

```
real scalar neat(pointer(real scalar function) p, other args...)
{
  ...
}
```

在任何情况下，在你的函数体内部，想要调用传递的函数的地方，编写：

`(*p)(arguments)`

例如，你可能会编写：

```
approx = ( (*p)(x+delta)-(*p)(x) / delta
```

`neat()` 函数的调用者想要将其与 `zeta_i_just_wrote()` 函数一起使用，会编写：

```
result = neat(&zeta_i_just_wrote(), other args...)
```

关于在复杂的数值计算中使用指针的示例，请参阅 Støvring (2007)。

## 指针的指针

允许指针的指针（指向指针的指针……），例如，如果 `X` 是矩阵：

```
p1 = &X
p2 = &p1
```

这里 `*p2` 等于 `p1`，而 `**p2` 等于 `X`。

同样，我们可以构造一个指向函数指针的指针：

```
q1 = &f()
q2 = &q1
```

这里 `*q2` 等于 `q1`，而 `**q2` 等于 `f`。

在构造指向指针的指针时，永远不要输入 `&&`——例如 `&&x`——来获取 `x` 的地址。请输入 `&(&x)` 或 `&&`。它是 `&` 的同义词，供习惯 C 语言编程的用户使用。

## 指针数组

你可以创建一个指针数组，例如：

```
P = (&X1, &X2, &X3)
```

或者

```
Q = (&f1(), &f2(), &f3())
```

这里 `*P[2]` 等于 `X2`，`*Q[2]` 等于 `f2()`。

## 混合指针数组

你可以创建混合指针数组，例如：

```
R = (&X
```

这里 `*R[2]` 等于 `f()`。

你不能创建与实数、复数或字符串元素混合的指针数组。Mata 会报错。

`NULL` 是特殊的指针值，意味着“指向无”或未定义。在许多方面，`NULL` 类似于 `0`——例如，编写 `if (X)` 等同于编写 `if (NULL)`，但在其他方面它与 `0` 不同。`0` 是数值；`NULL` 是指针值。

## 括号的使用

使用括号使意义更清晰。

在下表中，我们假设：

```
p = &X
P = (&X
```

其中 `X`, `X12`, `X21` 是矩阵，而 `f1()`, `f12()`, `f21()` 是函数。

| 表达式 | 含义 |
| :--- | :--- |
| `*p` | `X` |
| `*p[1,1]` | `X` |
| `(*p)` | `X[1,1]` |
| `*P` | `X12` |
| `(*P[1,2]) [3,4]` | `X12[3,4]` |
| `*q(a,b)` | 执行 `q()`；解引用 |
| `(*q) (a,b)` | `f(a,b)` |
| `(*q[1,1]) (a,b)` | `f12(a,b)` |
| `*Q[1,2] (a,b)` | 无意义 |
| `(*Q[1,2]) (a,b)` | `f12(a,b)` |

## 指针算术

指针的算术（即地址）是不允许的：

```
y = 2
x = &y
x+2
```

不要将表达式 `x+2` 与表达式 `*x+2` 混淆，后者是允许的并且实际上评估为 4。

你可以对指针值使用相等和不等运算符 `==` 和 `!=`：

```
if (p1 == p2) {
  ...
}
if (p1 != p2) {
  ...
}
```

此外，指针值可以赋值并与 `NULL` 值比较，这类似于但不同于零：`NULL` 是指针值。未赋值的指针值为 `NULL`，你可以将 `NULL` 值赋值给指针：

```
p = NULL
```

指针值可以与 `NULL` 比较：

```
if (p1 == NULL) {
if (p1 != NULL) {
```

但引用 `NULL` 指针将报错：

```
x = NULL
*x+2
```

对于逻辑表达式，你可以直接检查指针值：

```
if (p1) {
  ...
}
```

上述内容解释为编写了 `if (p1!=NULL)`。

## 列出指针

你可以列出指针：

```
y = 2
x = &y
x
```

`x` 是会话期间 `y` 的内存地址。如果你输入上述行，地址将会不同，但这并不重要。列出指针的值有助于调试，因为通过比较地址，你可以确定指针指向哪里以及哪些指针指向同一个东西。在列列表中，`NULL` 被呈现为 `NULL`。

## 指针的声明

指针的声明与所有声明一样（见 M-2）是可选的。基本语法是：

```
pointer(type or function)...
```

例如：

```
pointer(real matrix) p
```

声明 `p` 是一个指针标量，它指向一个实矩阵，并且

```
pointer(complex colvector) p2
```

声明 `p2` 是一个指针行向量，每个指针指向一个复列向量，并且

```
pointer(real scalar function) p3
```

声明 `p3` 是一个指针标量，它指向一个返回实标量的函数，并且

```
pointer(real matrix function) p4
```

声明 `p4` 是一个指向指针的列向量，这些指针的每个元素都是行向量，而这些元素每一个指向一个返回实矩阵的函数。

你可以省略想要的部分：

```
pointer() p5
```

声明 `p5` 是一个指针标量——指向不确定。

```
pointer scalar p5
```

意义相同。

```
pointer p6
```

声明 `p6` 是一个指针，但它是矩阵、向量还是标量未说明。

## 使用指针收集对象

假设你想编写分部分的函数：`result_setup()` 和 `repeated_result()`。在第一部分 `result_setup()` 中，你将从用户那里接收一个矩阵和一个函数，并将进行私有计算，供每次调用 `repeated_result()` 时使用。当 `repeated_result()` 被调用时，你需要知道矩阵、函数以及你之前进行的私有计算的值。

解决方案是采用以下设计。你要求用户编写：

```
resultinfo = result_setup(setup args...)
```

在第一次调用时，`value = repeated_result(resultinfo, other args...)`

在随后的调用中，设计是你将在 `resultinfo` 中的两个函数之间传递信息。这里 `resultinfo` 需要包含三内容：原始矩阵、原始函数以及你计算的私有结果。然而，用户不需要知道细节，你只需要要求将 `resultinfo` 声明为指针向量。

填充细节，你编写：

```
pointer vector result_setup(real matrix X, pointer(function) f)
{
    real matrix privmat
    pointer vector info
    ...
    privmat = =
    ...
    info = (&X, f, &privmat)
    return(info)
}
nreal matrix repeated_result(pointer vector info, ...)
{
    pointer(function) scalar f
    pointer(matrix) scalar X
    pointer(matrix) scalar privmat
    f = info[2]
    X = info[1]
    privmat = info[3]
    ...
    (*f)(..
    (*X)...
    (*privmat)...
}
```

# [M-2] pointers — 指针

不需要将 `info[]` 解载到各个标量中。使用传递值的行完全可以写成：

```
(*info[2])(..
(*info[1])...
(*info[3])
```

## 效率

在调用子程序时，传递指针标量参数的评估比传递指针标量本身更好，因为子程序的运行速度会快一点。假设 `p` 指向一个实矩阵。写成：

```
mysub(*p)
```

而不是

```
mysub(p)
```

然后将 `mysub()` 写为：

```
function mysub(real matrix X)
{
  X...
}
```

而不是

```
function mysub(pointer(real matrix) scalar p)
{
  (*p)...
}
```

解引用指针（从 `p` 获取 `*p`）并不耗费时间，但确实需要时间。如果 `mysub()` 循环并执行数十万或数百万次 `*p` 的求值，那么使用 `*p` 而不是 `p` 可能会非常重要。

## 诊断

前缀运算符 `*`（称为解引用运算符）如果应用于非指针对象，将报错并终止。

对解引用指针不能进行算术运算。算术运算符将报错并终止。

前缀运算符 `&` 如果应用于内置函数，将报错并终止。

## 参考文献

Søvring, H. 2007. A generic function evaluator implemented in Mata. Siata Journal 7: 542–555.

## 参见

[M-2] intro — 语言定义

## 标题

# [M-2] pragma — 抑制警告消息

## 语法

`pragma unset varname`

`pragma unused varname`

## 描述

`pragma` 告知编译器你的意图，这样编译器就可以避免呈现误导性的警告消息，并能够更好地优化代码。

## 备注

备注按以下标题给出：

`pragma unset`

`pragma unused`

## pragma unset

`pr pr`

`pragma unset X`

会抑制警告消息

`note: 变量 X 在代码之前可能被使用。`

该 `pragma` 对生成的编译代码没有影响。

通常，警告消息会标记你程序中的逻辑错误，例如：

```
: function problem(real matrix a, real scalar j)
> {\n> real scalar i
>
> j = i
>
> ...
> }
note: 变量 i 在设置之前可能被使用
```

然而，有时信息是误导性的。

```
: function notproblem(real matrix a, real scalar j)
> {
> real matrix V
>
> st_view(V, ...)
>
> ...
> }
note: 变量 V 在设置之前可能被使用
```

# [M-2] pragma — 抑制警告消息

在上面，函数 `st_view()`（参见 [M-5] st_view()）定义了 `V`，但编译器并不知道。

警告消息没有问题，但如果你想抑制它，可以将代码更改为：

```
: function unotproblem(real matrix a, real scalar j)
> {
>   real matrix V
>   pragma unset V
>   st_view(V, ...)
>   ...\n> }
```



`pragma unset V` 表示你清楚 `V` 未设置，对于警告消息，编译器应该像 `V` 在你的代码此处已设置了一样。

## pragma unused

`pragma unused X` 会抑制警告消息：

```
note: 参数 X 未使用
note: 变量 X 未使用
note: 变量 X 已设置但未使用
```

该 pragma 对生成的编译代码没有影响。

未使用变量通常出现在函数参数上。你编写了：

```
: function resolve(A, B, C)
> {
>   ...
>   pragma unused C
>   ...
> }
```

note: 参数 C 未使用

你清楚自己没有使用 `C`。你包含这个必要的参数是因为你试图符合某种标准，或者你知道之后可能想修改函数以包含 `C`。为了抑制警告消息，将代码更改为：

```
: function resolve(A, B, C)
> {
>   ...
>   pragma unused C
>   ...
> }
```

该 pragma 表示你清楚 `C` 是未使用的，为了警告消息，编译器应该像 `C` 在你的代码此处已使用了一样。

# [M-2] pragma — 抑制警告消息

未使用变量也会出现，通常情况下，它们应该被直接删除：

```
function resin(X, Y)
{
    real scalar i
    ...
    code in which i never appears
}

note: 变量 i 未使用
```

与其使用 pragma 来抑制消息，你应该删除 `real scalar i` 这一行。

对于设置但未使用的变量也会给出警告：

```
function thwart(X, Y)
{
    real scalar i
    ...
    i = 1
    ...
    code in which i never appears
}

note: 变量 i 已设置但未使用
```

在这里，你应该同时删除 `real scalar i` 和 `i = 1` 这两行。

然而，这种设置但未使用的变量可能是故意的：

```
function thwart(X, Y)
{
    real scalar i
    ...
    i = 1
    ...
    code in which i never appears
}

note: 变量 i 未使用
```

## 不返回内容的函数（void 函数）

如果一个函数不返回任何内容，则称为 void 函数。以下程序将矩阵的对角线设置为 1：

```
function fixdiag(matrix A)
{
  real scalar i
  for (i=1; i<=rows(A); i++) A[i,i] = 1
}
```

此函数甚至没有包含 `return` 语句；执行直接结束。这是可以的，尽管函数也可以写成：

```
function fixdiag(matrix A)
{
  real scalar i
  for (i=1; i<=rows(A); i++) A[i,i] = 1
  return
}
```

使用 `return` 是当函数有理由提前结束时：

```
void fixmatrix(matrix A, scalar how)
{
  real scalar i, j
  for (i=1; i<=rows(A); i++) A[i,i] = 1
  if (how==0) return
  for (i=1; i<=rows(A); i++) {
    for (j=1; j<i; j++) A[i,j] = 0
  }
}
```

# 另请

- [M-5] exit() — 终止执行
- [M-2] intro — 语言定义

## 标题

- [M-2] semicolons — 分号的使用

## 语法

```
stmt

stmt ;
```

## 描述

Mata 允许但不强制使用分号。下文将讨论分号的使用，以及关于 Stata 的 `#delim` 指令可能交互的建议；请参见 [P] #delim。

## 备注

备注在以下标题下给出：

- 分号的可选使用
- 即使使用分号，你不能在任何地方中断语句
- 使用分号创建多语句行
- 具有意义的分号
- 不要使用 `#delim`

## 分号的可选使用

你可以将程序写成如下所示：

```
real scalar foo(real matrix A)
{
  real scalar i, sum
  sum = 0
  for (i=1; i<=rows(A); i++) {
    sum = sum + A[i,i]
  }
  return(sum)
}
```

或者你可以将程序写成如下所示：

```
real scalar foo(real matrix A)
{
  real scalar i, sum;
  sum = 0;
  for (i=1; i<=rows(A); i++) {
    sum = sum + A[i,i];
  }
  return(sum);
}
```

也就是说，你可以在语句末尾省略或包含分号。这没有区别。你甚至混合两种样式：

```
real scalar foo(real matrix A)
{
    real scalar i, sum;

    sum = 0;
    for (i=1; i<=rows(A); i++) {
        sum = sum + A[1,i]
    }
    return(sum)
}
```

## 即使使用分号，你不能在任何地方中断语句

大多数使用分号的语言遵循以下规则：语句一直持续到分号为止。

Mata 遵循不同的规则：语句跨行持续，直到看起来完整为止，而分号强制结束语句。

例如，考虑某些程序中出现的语句 `x=b-c`。在代码中，它可能显示为：

```
x = b -
c
```

或者：

```
x = b -
c ;
```

无论哪种情况，Mata 都会将语句理解为 `x=b-c`，因为语句不可能在减号处结束：`x=b=` 没有意义。

相反：

```
x = b
- c
```

Mata 将其解释为两个语句：`x=b` 和 `-c`。

添加分号并无帮助：

```
x = b
- c;
```

`x = b` 本身仍然是一个完整的语句。改变的是第二条语句以分号结尾，这并不重要。

## 具有意义的分号

因此，记住在语句可能无法被解释为完整的地方中断多行语句，例如：

```
x = b -
c + (d
  + e)
function(A,
      B, C,
)
```

无论你是否使用分号。

## 使用分号创建多语句行

分号允许你在同一行编写多个语句。与其编写：

```
a = 2
b = 3
```

你可以编写：

```
a = 2 ; b = 3;
```

你甚至可以省略末尾的分号：

```
a = 2 ; b = 3
```

将语句分行或在同一行只是风格问题；不会改变含义。编写：

```
for (i=1; i<n; i++) a[i] = -a[i]; sum = sum[i];
```

仍然意味着：

```
for (i=1; i<n; i++) a[i] = -a[i];
sum = sum[i];
```

而且毫无疑问，程序员意图编写：

```
for (i=1; i<n; i++) {
  a[i] = -a[i];
  sum = sum[i];
}
```

具有不同的含义。

## 具有意义的分号

分号并非全是风格问题。`for` 语句的语法是：

```
for (exp1; exp2; exp3)
```

假设我们要编写的完整 `for` 循环是：

```
for (x=init(); iter(x))
```

并且后面没有语句。那么我们必须编写：

```
for (x=init(); iter(x));
```

在这里我们使用分号强制结束语句。假设我们省略了它，代码读取为：

```
for (x=init(); iter(x))
x = x
```

该语句在 Mata 看来是不完整的，因此它会将我们的代码解释为类似于：

```
for (x=init(); iter(x)) {
x = x
}
```

在这里的分号是有意义的。具有意义的分号只出现在 `for` 和 `while` 之后。

## 不要使用 `#delim`

下文关于 Stata 的 `#delim` 模式。如果你不知道它是什么，或者从不使用它，可以跳过。Stata 有一种可选能力允许其行持续到分号。在 Stata 中，你编写代码时分隔符变为分号，直到你的 do 文件结束或你编写：

```
#delim
```

我们建议当 Stata 处于 `#delim` 模式时不要使用 Mata。Mata 不会在意，你会让自己困惑。当 Mata 获取控制权时 `#delim` 是开启的。Mata 将关闭它，然后应用自己的规则，我们在上面已经总结。

# 另请

- [M-2] intro — 语言定义
- [P] #delim — 分隔符

## 标题

```
struct struct
```

## 语法

```
struct structname {
}
```

例如：

```
struct mystruct {
    real scalar n1, n2
    real matrix X
}
```

## 描述

结构包含一组绑定在一起的变量。结构不能交互式使用。它们用于编程。

## 备注

备注在以下标题下给出：

- 引言
- 结构和函数必须有不同的名称
- 结构变量必须显式声明
- 尽可能将结构变量声明为标量
- 结构的向量和矩阵
- 结构的结构
- 指向结构的指针
- 用于结构成员的运算符和函数
- 用于整个结构的运算符和函数
- 列出结构
- 泛型作为传递的使用
- 保存结构定义
- 保存结构变量

## 引言

以下是结构使用的概述：

```
struct mystruct {
    real scalar n1, n2
    real matrix X
}

function myfunc()
{
    struct mystruct scalar e
    ...
    e.n1 = ...
    e.n2 = ...
    e.X = ...
    mysubroutine(e, ...)
}

function mysubroutine(struct mystruct scalar x, ...)
{
    struct mystruct scalar y
    ...x.n1 ... x.n2 ... x.X...
    y = mysubfn(x)
    ...y.n1 ... y.n2 ... y.X...
    ...x.n1 ... x.n2 ... x.X...
}

struct mystruct scalar mysubfunc(struct mystruct scalar x)
{
    struct mystruct scalar result
    result = x
    ...result.n1 ... result.n2 ... result.X...
    return(result)
}
```

注意以下点：

1. 我们首先定义了结构。定义并不创建变量；定义定义了我们以后引用 `struct mystruct` 时的含义。此定义是在使用它的函数的定义之外且独立完成的。结构在函数之前定义。

2. 在 `myfunc()` 中，我们声明变量 `e` 是一个 `struct mystruct scalar`。我们像使用任何变量一样使用了 `e.n1`、`e.n2` 和 `e.X`。在调用 `mysubroutine()` 时，我们传递了整个结构。

3. 在 `mysubroutine()` 中，我们声明接收的第一个参数是 `struct scalar`。我们选择 `x` 而不是 `e` 是强调名称并不重要，`y` 也是 `struct scalar`。

4. `mysubfunc()` 只接受 `struct myst` 作为参数但也返回 `struct myst`。结构最好的用处之一是返回多个相关值。

`result=x` 行复制了结构中的所有值；我们不需要编写 `result.n1=x.n1`, `result.n2=x.n2` 和 `result.X=X`。

## [M-2] struct — 结构

当变量、参数或返回值是结构时，你必须显式声明它：

```
function makecalc() {
    struct twopart scalar t
    t.n1 = t.n2 = 0
...
}
function clear_twopart(struct twopart scalar t) {
    t.n1 = t.n2 = 0
}
struct twopart scalar new_twopart() {
    struct twopart scalar t
    t.n1 = t.n2 = 0
    return(t)
}
```

在上面的函数中，我们引用了变量 `t.n1` 和 `t.n2`。除非知道结构的定义，否则 Mata 编译器无法解释这些名称。

备注：所有的结构引用都在编译时解析的，而不是运行时。这意味着，像 `t.n1` 这样的项不会存储在编译代码中，也不会在执行期间解析。相反，Mata 编译器在编译代码时会访问结构定义。编译器知道 `t.n1` 指向结构的第一个元素，并生成高效的代码来访问它。

## 尽可能将结构变量声明为标量

在我们的声明中，我们编写了如下代码：

```
struct twopart t
```

并且没有简化代码：

```
struct twopart t
```

尽管更简洁的语句也是有效的。

结构变量可以是标量、向量或矩阵；当你没有指定是哪一种时，假设为矩阵。

我们大多数人都是标量，如果你告诉编译器这些结构是标量，它将生成更高效的代码。此外，当你使用结构向量或矩阵时，有一个额外的步骤来填充它，如下一节所述。

## 结构向量和结构矩阵

就像你可以拥有实数标量、向量或矩阵一样，你也可以拥有结构标量、向量或矩阵。以下都是有效的：

```
struct twopart scalar t
struct twopart vector t
struct twopart rowvector t
struct twopart colvector t
struct twopart matrix t
```

在一个 `struct twopart matrix` 矩阵中，矩阵的每个元素都是一个独立的结构。假设矩阵是 2 x 3。那么你可以引用以下变量中的任何一个：

```
t[1,1].n1
t[1,2].n1
t[1,3].n1
t[2,1].n1
t[2,2].n1
t[2,3].n1
```

对于 `t[i, j].n2` 也是如此。

如果 `struct twopart` 也包含一个矩阵 `X`，那么：

```
t[i,j].X
```

将指向第 (i,j) 个矩阵。

```
t[i,j].X[k,l]
```

将指向第 (i,j) 个矩阵的第 (k, l) 个元素。

如果 `t` 是一个 2 x 3 矩阵，你必须安排使其成为 2 x 3。在声明之后：

```
struct twopart matrix t
```

`t` 是 0 x 0。这与 `t` 是实矩阵且在声明后 `t` 为 0 x 0 的情况没有区别。

无论 `t` 是实矩阵还是 `struct twopart` 矩阵，你都通过赋值来分配 `t`。假设 `t` 是一个实矩阵。分配问题有三种解决方案：

- (1) `t = x`
- (2) `t = somefunction(...)`
- (3) `t = J(r, c, v)`

这三种方法都是如此自然，至于你甚至不会将它们视为分配；而是将其视为定义。

结构的情况也是一样。

让我们逐一来看：

1. `x` 包含一个 2 x 3 的 `struct twopart`。你编写：

```
t = x
```

现在 `t` 包含了 `x` 的拷贝。`t` 是 2 x 3。

2. `somefunction(...)` 返回一个 2 × 3 的 `struct twopart`。你编写：

```
t = somefunction(...)
```

现在 `t` 包含了 2 × 3 的结果。

Mata 函数 `J(r, c, v)` 返回一个 r × c 矩阵，其每个元素都被设置为 `v`。假设变量 `tpc` 包含一个 `struct twopart scalar`。你编写：

```
t = J(2, 3, tpc)
```

现在 `t` 是 2 x 3，其每个元素都是 `tpc` 的拷贝。这里是你可能这样做的方法：

```
function (...) {
  struct twopart scalar tpc
  struct twopart matrix t
  ...
  t = J(2, 3, tpc)
}
```

最后，还有第四种创建结构向量和矩阵的方法。当你定义：

```
struct twopart {
  real scalar n1, n2
}
```

Mata 不仅记录了结构定义，还创建了一个名为 `twopart()` 的函数，它返回一个 `struct twopart`。因此，与其忍受从预分配标量创建矩阵的繁琐过程，你只需要编写：

```
t = J(2, 3, twopart())
```

事实上，Mata 为你创建的函数 `twopart()` 允许 0、1 或 2 个参数：

```
twopart() 返回一个 1 × 1 结构
twopart(r) 返回一个 r × 1 结构
twopart(r, c) 返回一个 r × c 结构
```

所以你可以编写：

```
t = twopart(2, 3)
```

或者你可以编写：

```
t = J(2, 3, twopart())
```

哪种代码都没有区别。`t` 中是什么？每个元素包含一个独立的结构。在每个 `twopart` 中，标量被设置为 0（视情况而定），向量为 1 × 1，矩阵为 0 × 0。



## 结构的结构

结构可以包含其他结构：

```
struct twopart {
  real scalar n1, n2
}
struct twopart {
  struct twopart scalar t1, t2
}
```

如果`t`是`struct twopart scalar`，那么它的成员将是：

```
t.t1        struct twopart
t.t2        struct twopart
t.t1.n1     一个实标量
t.t1.n2     一个实标量
t.t2.n1     一个实标量
t.t2.n2     一个实标量
```

你也可以创建结构的结构、结构中的结构，等等。但你不能在结构中包含自身：

```
struct recursive {
  struct recursive r
}
```

你看到没有，即使在标量情况下，`recursive`也需要无限的内存？

## 结构指针

你可以这样做：

```
struct recursive {
  pointer scalar r
}
```

因此，如果`r`是`struct recursive scalar`，那么`r.r`就是下一个结构，或者如果没有结构，`r.r`为`NULL`。通过这种方式，你可以创建链表。

Mata 提供了`->`运算符来访问结构指针，假设`struct recursive`也有成员`n`，那么`rec.r->n`是有效的（假设`rec.r!=NULL`）。

`->`的语法是

```
exp1 -> exp2
```

其中`exp1`求值为结构指针，`exp2`索引结构。

## 用于结构成员的运算符和函数

所有的运算符、函数和 Mata 特性都可以作用于结构成员。也就是说，给定

```
struct example {
    real scalar n
    real matrix X
}
function (...) {
    real scalar rs
    real matrix rm
    struct example ex
    ...
}
```

那么`ex.n`和`ex.X`可以在任何地方使用，`rs`和`rm`是有效的。

## 用于整个结构的运算符和函数

某些运算符和函数可以用于整个结构，而不仅仅是结构的元素。给定

```
struct mystruct scalar ex1, ex2, ex3, ex4
struct mystruct matrix E, F, G
```

1. 你可以使用`==`和`!=`测试相等性：

```
if (ex1==ex2) ...
if (ex1!=ex2) ...
```

如果两个结构的成员相等，则它们相等。在示例中，`mystruct`本身不包含子结构。如果有，相等性的定义将涉及子结构、子子结构等。在示例中，`ex1`和`ex2`是标量。如果它们是矩阵，将比较每个元素，如果相应的元素相等则矩阵相等。

2. 你可以使用`==`和`: !=`形成相等和不等矩阵。

3. 你可以使用逗号和反斜杠运算符形成结构向量和矩阵：

```
ex = ex1, ex2 \ ex3, ex4
```

4. 你可以使用`&`获取结构指针：

```
ptr_to_ex1 = &ex1
```

5. 你可以使用下标操作来访问和拷贝结构成员：

```
ex1 = E[1,2]
E[1,2] = ex1
F = E[2..]
E[2..] = F
G = E[1,1\2,2]
E[1,1\2,2] = G
```

6. 你可以使用`rows()`和`cols()`函数获取矩阵结构的行数和列数。

7. 你可以使用结构使用`eltype()`和`orgtype()`。`eltype()`返回`struct`，`orgtype()`返回通常的结果。

8. 你可以使用大多数以`is`开头的函数，如`isreal()`、`iscomplex()`、`isring()`等。这些函数在真时返回 1，假时返回 0，对于结构通常返回 0。

9. 你可以对结构使用`swap()`。

## 列出结构

要列出结构变量的内容（用于调试目的），使用函数`liststruct()`；

[M-5] `liststruct()`。

不建议使用默认的未赋值表达式方法列出结构，因为显示的所有只是指针值而不是结构本身。

## 使用 transmorph 作为透传

`transmorph`矩阵理论上可以包含任何内容，所以当我们说结构必须显式声明时，那并不完全准确。假设函数`twopart()`返回一个`struct twopart scalar`。你可以编写

```
x = twopart()
```

而无需声明`x`（或将其声明为`x`），并且不会报错。你只是不能引用`x.n1`或`x.n2`，编译器不知道`x`包含一个`struct twopart`，并且无法解释变量引用。

这个属性在实现句柄和透传时非常好用。

假设你正在实现一个复杂的系统。为了固定想法，我们假设该系统寻找用户指定函数的最大值，并且系统具有许多功能。为了跟踪给定的问题，假设你的系统需要很多变量。一个变量记录要使用的方法。另一个变量记录是否使用数值导数。另一个记录当前的梯度向量。另一个记录迭代次数，等等。可能有几百个这样的变量。

## 192 [M-2] struct — 结构

你将所有变量绑定在一个结构中：

```
struct variables {
    real scalar method
    real scalar use_numeric_d
    real vector gradient
    real scalar iteration
}
```

你设计了一个包含许多函数的系统，某些函数调用其他函数，但由于所有状态变量都绑定在一个结构中，因此很容易将值从一个函数传递另一个另一个。

你还设计了一个易于使用的系统。从用户“打开”一个问题开始：

```
handle = maximize_open()
```

从该点开始，用户将句柄传递给其他的 maximize 例程：

```
maximize_set_use_numeric_d(handle, 1)
maximize_set_function_to_max(handle, &myfunc())
maximize_maximize_my_function(handle)
```

```
handle = maximize_open()
```

然后将句柄传递给其他的`maximize-*()`例程。如果用户认为他必须显式声明句柄，你可以告诉他声明它：

```
transmorphic scalar handle
```

这种私密性的优势是什么？你可以确定用户永远不会更改你的结构体`maxvariables`中的任何值，因为编译器甚至不知道它们是什么。

因此，你使得你的系统对用户错误更具健壮性。

# 保存编译后的结构定义

你保存编译后的结构定义就像保存编译后的函数定义一样；请参见 [M-3] `mata mosave`和 [M-3] `mata mlib`。

当你定义一个结构时，例如`twoport`：

```
struct twoport {
    real scalar n1, n2
}
```

这也会创建一个函数`twoport()`，用于创建该结构的实例。

将`twoport()`保存在`.mo`文件或`.mlib`库中，也会保存编译后的定义。一旦`twoport()`被保存，你就可以编写未来的程序，而无需再心心定义`twoport`。该定义将被自动找到。

# 保存结构变量

包含结构的变量可以保存到磁盘上，就像保存任何其他变量一样。不需要特殊操作。请参见 [M-3] `mata matsave`并查看 [M-5] `fopen()`中的函数`fputmatrix()`。`matamatsave`和`fputmatrix()`都可以处理结构变量，尽管它们的条目中没有提到它们。

# 引用

Gould, W. W. 2007. Mata Matters: Structures. Stata Journal 7: 556–570.

# 另

- [M-2] `declarations` — 声明与类型
- [M-2] `intro` — 语言定义

## 标题

[M-2] `subscripts` — 下标的使用

## 语法

```
x[real vector r, real vector c]
x[|real matrix sub|]
```

下标可以用等赋值运算符的左侧或右侧。

## 描述

下标有两种样式。

在`[subscript]`语法中——称为**列表下标**——指定一个元素或一个矩阵：

```
x[1,2] x 的第 1,2 元素；一个标量
x[(1\3\2), (4,5)] 由 x 的第 1, 3, 2 行和第 4, 5 列组成的 3×2 矩阵：
```

| $x_{14}$ | $x_{15}$ |
| $x_{34}$ | $x_{35}$ |
| $x_{24}$ | $x_{25}$ |

在`[|list|]`语法中——称为**范围下标**——指定一个元素或连续的子矩阵：

```
x[[1,2]] 等同于 x[[1,2]; 一个标量
x[[2,3 \ 4,7]] x 的 3×4 子矩阵：
```

| $x_{23}$ | $x_{24}$ | $x_{25}$ | $x_{26}$ | $x_{27}$ |
| $x_{33}$ | $x_{34}$ | $x_{35}$ | $x_{36}$ | $x_{37}$ |
| $x_{43}$ | $x_{44}$ | $x_{45}$ | $x_{46}$ | $x_{47}$ |

两种样式的下标都可以在表达式中使用，并可以用于等赋值运算符的左侧。

## 备注

备注在以下标题下给出：

- 列表下标
- 范围下标
- 何时使用列表下标以及何时使用范围下标
- 细微的区别

# 列表下标

列表下标——也简单称为下标——当你将下标封装在方括号`[` `]`中时获得。列表下标有两种基本形式：

```
x[ivec, jvec] 由矩阵 x 的行 ivec 和列 jvec 组成的矩阵
v[kvec] 由向量 v 的元素 kvec 组成的向量
```

其中`ivec`, `jvec`, `kvec`可以是向量或标量，因此两种基本形式包括

```
x[i,j] 标量 i,j 元素
x[i,jvec] 行 i、元素 jvec 的行向量
x[ivec,j] 列 j、元素 ivec 的列向量
v[k] 向量 v 的第 k 个元素标量
```

还可以指定缺失值来表示 i 的所有行或所有列：

```
x[.,.] x 的第 i 行行向量
x[.,j] x 的第 j 列列向量
x[ivec,.] 行 ivec、所有列的矩阵
x[.,jvec] 列 jvec 的矩阵
x[.,.] 整个矩阵
```

最后，当你省略参数时，Mata 假设缺失值：

```
x[i,.] 等同于 x[i,]
x[ivec,.] 等同于 x[ivec,]
x[.,j] 等同于 x[.,j]
x[.,jvec] 等同于 x[.,jvec]
x[,,] 等同于 x[,]
```

良好样式是将`ivec`指定为列向量，`jvec`为行向量，但这不是要求的：

```
x[(1\2\3), (1,2,3)] 良好样式
x[(1\2\3), (1,2,3)] 等同于 x[(1\2\3), (1,2,3)]
x[(1\2\3), (1,2,3)] 等同于 x[(1\2\3), (1,2,3)]
x[(1\2\3), (1,2,3)] 等同于 x[(1\2\3), (1,2,3)]
```

同样，当`v`是列向量时，良好样式是将`kvec`指定为列向量，当`v`是行向量时，将`kvec`指定为行向量，但这不是要求的，当`v`是行向量时返回的是列向量：

```
rowv[(1,2)] 良好样式指定行向量
rowv[(1,2)] 等同于 rowv[(1,2)]
colv[(1,2)] 良好样式指定列向量
colv[(1,2)] 等同于 colv[(1,2)]
```

# 范围下标

下标可以用变量名后的表达式中使用：

```
first =[1]
multiplier = x[3,4]
result = colsum(x[,j])
```

下标可以用表达式后从结果中提取子矩阵：

```
allneeded = invsym(x)((1:4),:) multiplier
```

下标可以用等赋值运算符的左侧：

```
x[1,1] = 1
x[1..,3]
x[(1:4), (1..)] = I(4)
```

下标出现在括号内。范围下标有四种基本形式：

- `x[li,j]` i,j 元素；等同于`x[i,j]`
- `v[lk]` 向量的第 k 个元素；等同于`v[k]`
- `x[li,j \ k]` 使用 (i,j) 作为左上角，(k,l) 作为右下角的子矩阵、向量或标量
- `v[li \ k]` 从元素到 k 的子向量或标量；当`v`是行向量时返回行向量，当`v`是列向量时返回列向量

当指定 l x2 或 1x1 下标时，可以指定缺失值表示所有行或所有列：

- `x[li,..]` x 的行；等同于`x[i,]`
- `x[.,j]` x 的列 j；等同于`x[.,j]`
- `x[..,..]` 整个矩阵；等同于`x[,,..]`
- `v[l..]` 整个向量；等同于`v[..]`

此外，当指定 2x2 下标时，可以指定缺失表示矩阵的行数或列数：

- `x[1,2 \ 4,..]` 等同于`x[1,2 \ cols(x)]`
- `x[1,2 ..3]` 等同于`x[1,2 \ rows(x)]`
- `x[1,2 ..]` 等同于`x[1,2 \ rows(x), cols(x)]`

对于范围下标，方括号内部在所有情况下都被解释为矩阵表达式，因此：

```
sub = (1,2)
x[[sub]]
```

# [M-2] subscripts — 下标的使用

`x[sub]`指向`x[1,2]`。

范围下标可以在列表下标相同的上下文中使用；它们可以用变量名后的表达式中使用：

```
submat = result[[1,1 \ 3,3]]
```

它们可以用于从计算结果中提取子矩阵：

```
allneeded = invsym(x)[[1,1 \ 4,4]]
```

它们可以用等赋值运算符的左侧：

```
x[[1,4 \ 1,4]] = I(4)
```

# 何时使用列表下标何时使用范围下标

范围下标能做的一切列表下标也能做。范围下标看似唯一的：

```
x[[il,jl \ i2,j2]]
```

被完美地模拟：

```
x((il::2,j2))
```

然而，范围下标的构造执行速度更快，这正是范围下标的目的：提供一种快速提取连续子矩阵的方法。在所有其他情况下，使用列表下标是因为它们更快。

使用列表下标引用标量值：

```
result = x[[1,3]]
x[[1,3]] = 2
```

使用列表下标提取整个行或列：

```
obs = x[[., 3]]
var = x[[4, ]]
```

使用列表下标置换矩阵的行列：

```
: x = (1,2,3,4 \ 5,6,7,8 \ 9,10,11,12)
: y = x((1\3(2), .])
: y
```

```
1 2 3 4
2 9 10 11 12
3 5 6 7 8
```

```
: y = x[[(1,3,2,4)]]
: y
```

```
1 1 3 2 4
2 5 7 6 8
3 9 11 10 12
```

等等，我漏了一个：

```
: y=x[[1\3(2), (1,3,2,4)]]
```

# [M-2] subscripts标 — 下标的使用

```
: y
1 2 3 4
```

| 1 | 1 | 2 | 3 | 4 |
| 2 | 9 | 11 | 10 | 12 |
| 3 | 5 | 7 | 6 | 8 |

使用列表下标复制行或列：

```
: y
1 2 3 4
```

| 1 | 2 | 3 | 4 |
| 2 | 5 | 6 | 7 | 8 |
| 3 | 9 | 10 | 11 | 12 |
| 4 | 1 | 2 | 3 | 4 |

```
: y = x(., (1,2,3,4,2])
: y
1 2 3 4 5
```

| 1 | 1 | 2 | 3 | 4 |
| 2 | 5 | 6 | 7 | 8 | 6 |
| 3 | 9 | 10 | 11 | 12 | 10 |

```
: y = x[(1\2\3\1), (1,2,3,4,2])
: y
1 2 3 4 5
```

| 1 | 1 | 2 | 3 | 4 |
| 2 | 5 | 6 | 7 | 8 | 6 |
| 3 | 9 | 10 | 11 | 12 | 10 |
| 4 | 1 | 2 | 3 | 4 | 2 |

# 细微的区别

`x[i, j]`和`x[[i, j]]`之间存在细微的区别。在`x[i, j]`中，有两个参数：`i`和`j`。逗号分隔这两个参数。在`x[[i, j]]`中，有一个参数：`i, j`。逗号是列连接操作符。

在 Mata 中，逗号大部分意味着列连接操作符：

```
newvec = oldvec, addedvalues
qsum = (x,1)'(x,1)
```

实际上只有两个例外。当你输入函数的参数时，逗号分隔一个参数与下一个参数：

```
result = f(a,b,c)
```

在上面的示例中，`f()`接收三个参数：`a`, `b`和`c`。如果我们想`f()`接收一个参数`(a,b,c)`，我们必须将计算括在括号中：

```
result = f((a,b,c))
```

# [M-2] subscripts标 — 下标的使用 199

这就是第一个例外。当你在函数内部输入参数时，逗号用于参数分隔。通过打开另一组括号，你可以回到逗号的通常含义——列连接操作符。

第二个例外是在列表下标索引中：

```
x[i,j]
```

在列表下标括号内部，逗号意味着参数分隔。这就是为什么你看到我们在括号内输入了向量：

```
x[(1\2\3), (1,2,3)]
```

这两个就是两个例外。范围下标不是例外。因此，在

```
x[i, j]
```



`x[[i,j]]` 中存在一个参数 `i`, `j`, `k`。使用范围下标，你可以编写如下程序结构：

```
IJ = (i,j)
RANGE = (1,2 \ 4,4)
x[[IJ]] ... x[[|RANGE|]]
```

你不能用列表下标进行这种操作。特别是，`x[[IJ]]` 将被解释为从向量 `x` 中提取元素 `i` 和 `j` 的请求。`x[[RANGE]]` 将始终是一个错误。

我们说过的列表下标 `x[i,j]` 比范围下标 `x[[i,j]]` 稍微快。确实如此，但如果 `IJ=(i,j)`，那么 `x[[IJ]]` 会比 `x[i,j]` 快。然而，你必须执行数百万次 `x[[IJ]]` 的引用才能测量出这种差异。

## 兼容性

```
x[i, j]
```

```
x: r c
i: m x or 1 x m (何种均可)
j: 1 n or n 1 (何种均可)
result: m n
```

```
x[i, .]:
```

```
x: r c
i: m x or 1 x m (何种均可)
result: m c
```

```
x[., j]:
```

```
x: r c
j: 1 n or n 1 (何种均可)
result: r n
```

```
x[., , .]:
```

```
x: r c
result: r c
```

# 200 [M-2] subscripts标 — 下标的使用

`x[i]:`

| | $n \times 1$ | $1 \times n$ |
| $i:$ | $m \times 1$ 或 $1 \times m$ 或 $m \times l$ |
| $result:$ | $n \times 1$ | $1 \times m$ |

`x[.]:`

| | $n \times 1$ | $1 \times n$ |
| $result:$ | $n \times 1$ | $1 \times n$ |

`x[|k|]:`

| | $r \times c$ |
| $k:$ | $1 \times 2$ |
| $result:$ | $1 \times 1$ if $k[1]<$ |
| | $1 \times c$ if $k[1]>=$ |
| | $r \times c$ if $k[2]<$ |
| | $r \times c$ if $k[2]>=$ |

`x[|l|]:`

| | $r \times c$ |
| $k:$ | $2 \times 2$ |
| $result:$ | $k[2]-k[1]+1 \times 2$ | (在上面的公式中，如果 $k[1]>=$，视为 $k[2]=c$) |

`x[|l|]:`

| | $r \times 1$ | $1 \times c$ |
| $k:$ | $2 \times 1$ |
| $result:$ | $k[2]-k[1]+1 \times 1$ | $1 \times c$ (如果 $k[2]>=$，视为 $k[2]=c$)

## 诊断

如果下标超出范围或引用不存在的行或列，两种下标样式都会终止。

## 参考文献

Gould, W. W. 2007. Mata Matters: Subscrib. Stata Journal 7: 106–16.

## 另见

[M-2] intro — 语言定义

## 标题

[M-2] syntax — 语法和结构

## 语法

基础语言语法是

```
istmt
where
istmt :=\  stmt
  function name(farglist) fstmt
  ftype name(farglist) fstmt
  ftype name(farglist) fstmt
stmt :=\  nothing
  ; (含义为空)
  version number
  { stmt ... }
  exp
  pragma pstmt
  if (exp) stmt
  if (exp) else stmt
  for (exp;exp;exp) stmt
  while (exp) stmt
  do stmt while (exp)
  break
  continue
  label:
  goto label
  return
  return(exp)
fstmt :=\  stmt
  type arlistlist
  external type arlistlist
arglist :=\  name
  name()
  name, arlistlist
  name(), arlistlist
farglist :=\  nothing
  efarglist
efarlist :=\  felement
  felement, efarglist
  | felement
  | felement, efarglist
```

`felement := name`
  `type name`
  `name()`
  `type name()`

`ftype := type`
  `void`

`type := elty`
  `orgtype`
  `eltype`

`eltype := transmorphic`
  `string`
  `numeric`
  `real`
  `complex`
  `pointer`
  `pointer(pirtype)`

`orgtype := matrix`
  `vector`
  `rowvector`
  `colvector`
  `scalar`

`prtype := nothing`
  `type`
  `type function`
  `function`

`pstm := unset name`
  `unused name`

`name := 最大32字符标识符`
`label := 最大8字符标识符`
`exp := [M-2] exp 中定义的表达式`

## 描述

Mata 是一种类 C 的编译语言，具有矩阵扩展和运行时链接。

## 备注

备注按以下标题给出：

- 分号的处理
- 类型和声明
- 空矩阵
- 空函数
- 算符
- 下标
- 隐含输入标记
- 函数传递约定
- 将函数传递给函数
- 可选参数

# [M-2] syntax — 语法和结构 203

在阅读 [M-2] syntax 之后，查看 [M-2] intro 以获取有关此处讨论内容的更多解释条目列表。

# 分号的处理

分号（`;`）被视为分隔符。它不是必须的，但可以用于将语句放在同一物理行：

```
x = 1 ; y = 2 ;
```

上述示例中的最后一个分号是不必要的，但是允许的。如果延续是明显的，单个语句可以延续到另一行。“明显”意味着例如有一个悬挂的左括号或悬挂的二元算符。

```
x = (
3)
x = x + 
2
```

更多信息请参见 [M-2] 分号。

# 类型和声明

变量或函数的类型由

```
eltype
```

其中 `eltype` 和 `orgtype` 分都是以下之一：

| eltype | orgtype |
|---|---|
| transmorphic | matrix |
| numeric | vector |
| real | rowvector |
| complex | colvector |
| string | scalar |
| pointer | |

例如，变量可以是实数标量、复数矩阵或字符串向量。

Mata 还有结构——`eltype` 为 `struct name`——但此处未包含。关于结构的讨论，请参见 [M-2] struct。

Mata 还有类——`eltype` 为 `class name`——但此处未包含。关于类的讨论，请参见 [M-2] class。

声明是可选的。当没有声明变量或函数的类型时，假设它为多态矩阵。特别是：

1. `eltype` 指定元素的类型。当未指定 `eltype` 时，假设为多态的。

# [M-2] 语法 — Mata 语言语法与语法 205

```
void function example(matrix A)
{
    real scalar i
    for (i=1; i<=rows(A); i++) A[i,i] = 1
    return(J(0, 0, ..))
}
```

或者

```
void function example(matrix A)
{
    real scalar i
    for (i=1; i<=rows(A); i++) A[i,i] = 1
    return(J(0, 0, ..))
}
```

因此，`void` 也是变态矩阵的一种特例（它实际上是一个 0 × 0 的实数矩阵）。由于声明是可选的（但出于风格和效率的考虑，建议都写上），上面的函数也可以被编码为：

```
function example(A)
{
    for (i=1; i<=rows(A); i++) A[i,i] = 1
}
```

参见 [M-2] 声明。

## 运算符

Mata 提供了常用的运算符；参见 [M-2] 表达式。

单元前缀运算符有：

| ! ++ & * |

前缀运算符 `& *` 与指针有关；参见 [M-2] 指针。

单元后置运算符有：

| / ++ |

注意这里包含了后置运算符 `'` 用于转置。此外，对于复数 `Z`，`Z'` 返回共轭转置。如果你想要不带共轭的转置，请参见 [M-5] transpose()。

二元运算符有：

| ? \ :: : & == <= < > |
| != = + - # |

此外还包含 `&& || |` 作为 `&` 和 `|` 的同义词。

运算符 `==` 和 `!=` 不需要满足兼容性，也不要求矩阵类型相同。在这种情况下，矩阵是不相等的（`==` 为假，`!=` 为真）。对于复数参数，`< <= >` 指复数向量的长度。然而，`==` 和 `!=` 指的不是长度，而是具体的分量。[M-2] op_logical。

# [M-2] 语法 — Mata 语言语法

运算符 `& \` 是行连接和列连接运算符。`(1,2,3)` 构造行向量；`(1\2\3')` 构造列向量；`(1,2,3')`。`(1,2,3,4)` 构造一个第一行为 `(1,2)`、第二行为 `(3,4)` 的矩阵；`a\b` 按行连接标量、向量或矩阵。`a\b` 按列连接两个标量、向量或矩阵。参见 [M-2] op_join。

`:` 和 `:` 指行到行和列到列的运算符。`1..5` 是 `(1,2,3,4,5)`。`1::5` 是 `(1\2\3\4\5)`。`5..1` 是 `(5\4\3\2\1)`。参见 [M-2] op_range。

对于 `| , ==, <=, <, =, +, -, *, /`，且 `@` 的优先级紧随在 `op` 之后。运算符执行逐元素操作。例如，`A*B` 指矩阵乘法。`A:B` 指逐元素乘。此外，逐元素操作被推广到 `A` 和 `B` 行数或列数不相同的情况。例如，如果 `A` 是一个 `1 x c` 行向量而 `B` 是 `r x c` 矩阵，则返回 `[[Cij]] = ||Aj|| * ||Bij||`。参见 [M-2] op_colon。

# 下标

`A[i, j]` 返回 `A` 的第 `i,j` 个元素。

如果 `A` 是 `1 x c`，`A[k]` 返回 `A[1,k]`；如果 `A` 是 `r x1`，则返回 `A[k,1]`。也就是说，除了声明的向量，`1 x c` 矩阵或 `r x1` 矩阵也可以通过一个索引访问。地，任何向量都可以通过两个索引访问。

`i`, `j` 和 `k` 也可以标量。例如，`A[(3\4\5)]` 返回一个 `3 x 1` 列向量，包含第 5 列的 3 行。

`i`, `j` 和 `k` 可以是缺失值。`A[., 4]` 返回 `A` 的第 4 列的列向量。

上述下标被称为列表样式下标（list-style subscripts）。Mata 提供了另一种格式范围样式下标（range-style subscripts），特别适用于选择子矩阵。`A[1,3\5,5]` 返回 `A` 中从 `A[3,3]` 开始的 `3 x 3` 子矩阵。

参见 [M-2] 下标。

# 隐式输入标记

在解释和编译一行时，Mata 对其看到的内容进行以下替换：

| 输入序列 | 解释 |
|---|---|
| `'name` | `*name` |
| `[` | `[,` |
| `]` | `,.]` |

因此，编码 `X'Z` 等于编码 `X'*Z`，编码 `x = z[1,]` 等于编码 `x = z[1,.]`。

# 参数传递约定

参数通过地址传递给函数，也称为按名或引用传递。它们不是按值传递的。当你编写：

```
f(A)
```

传递给 `f()` 的 `A` 的地址，而不是 `A` 中值的拷贝。`f()` 可以修改 `A`。
大多数函数不会修改其参数，但某些会。例如，`ludA(A, L, U, p)` 计算 `A` 的 LU 分解。该函数用矩阵替换 `L`, `U` 和 `p` 的内容，使得 `L[p,:]=A`。

老手可能听过 FORTRAN 程序，它调用子程序并传递第二个参数。

## 编译时和运行时版本控制

以下是详细说明。我们建议始终遵循上述建议。

实际上有两个版本号是重要的：编译时设置的版本号（它会影响源代码的解释方式），以及执行时用于提供子程序的库版本。

我们在前面的节中使用的 `version` 命令实际上是 Stata 的 `version` 命令（参见 [[P] version]），它同时设置了这两个版本：

```
version 12
mata:
  function example()
  {
  end
```

在上面的示例中，我们使用 Mata 语言的版本 12 语法编译 `example()`，并且 `example()` 调用的函数都将是对应的版本 12。在进入 Mata 之前设置 `version 12` 了这一切。

在下一个示例中，我们使用版本 12 语法编译并使用版本 12.2 函数：

```
version 12
mata:
  function example()
  {
    version 12.2
    ...
  end
```

在下一个示例中，我们使用版本 12.2 语法编译并使用版本 12 函数：

```
version 12.2
mata:
  function example()
  {
    version 12
    ...
  end
```

然而，你想要在不同的版本级别上进行编译和执行是非常罕见的。

## 另请参

- [M-5] callersversion() — 获取调用者的版本
- [M-2] intro — 语言定义

## 标题

[M-2] void — 空矩阵 (Void matrices)

## 语法

```
J(0, 0, .)   0 × 0 实型矩阵
J(r, 0, .)   r × 0 实型矩阵
J(0, c, .)   0 × c 实型矩阵
J(0, 0, 11)   0 × 0 复数型矩阵
J(r, 0, 11)  r × 0 复数型矩阵
J(0, c, 11)   0 × c 复数型矩阵
J(0, 0, "")   0 × 0 字符串矩阵
J(r, 0, "")  r × 0 字符串矩阵
J(0, c, "")  0 × c 字符串矩阵
J(0, 0, NULL) 0 × 0 指针矩阵
J(r, 0, NULL) r × 0 指针矩阵
J(0, c, NULL) 0 × c 指针矩阵
```

## 描述

Mata 允许 0 × 0、r × 0 和 0 × c 矩阵。这些矩阵被称为空矩阵 (void matrices)。

## 备注

备注在以下标题下给出：
- 空矩阵、向量、行向量和列向量
- 如何读取兼容性表 (conformability charts)

## 空矩阵、向量、行向量和列向量

空矩阵不包含任何内容，但它们具有维度信息（它们是 0 × 0、r × 0 或 0 × c）并且有一个元素类型（`eltype`，实实、复数、字符串或指针）：

1. 如果矩阵是 0 × 0、r × 0 或 0 × c，则称它是空矩阵。
2. 如果向量是 0 × 1 或 1 × 0，则称它是空向量。
3. 如果列向量是 0 × 1，则称它是空向量。
4. 如果行向量是 1 × 0，则称它是空向量。
5. 常量不能是空的，因为根据定义，它是 1 × 1。

函数 `J(r, c, val)` 创建包含 `val` 的 r × c 矩阵；参见 [M-5]。可以通过指定 `r` 和/或 `c` 为 0 来使用 `J()` 创建空矩阵。第三个参数的值并不重要，但它的元素类型很重要：

1. `J(0,0,.)` 创建 0×0 实型矩阵，`J(0,0,1)` 以及带有任何实型第三参数的 `J()` 也是。
2. `J(0,0,ii)` 创建 0×0 复数型矩阵，带有任何复数第三参数的 `J()` 也是。
3. `J(0,0,'')` 创建 0× 字符串矩阵，带有任何字符串第三参数的 `J()` 也是。
4. `J(0,0,NULL)` 创建 0×0 指针矩阵，带有任何指针第三参数的 `J()` 也是。

事实上，人们很少制造此类矩阵，因为它们在极端情况下会自然出现。同样，人们很少需要包含特殊代码来处理空矩阵，因为此类矩阵会处理自己。当行数或列数为零时，循环将消失。

## 如何读取兼容性表

通常情况下，不仅对带有空矩阵的函数和运算符进行了强调，而且根本没有提到这一事实。相反，信息隐藏在位于函数或运算符手册末尾的“兼容性”（Conformability）部分。

例如，某些函数的兼容性表可能如下：

```
somefunction(A, B, v):
 A:   r × c
 B:   c × k
 v:   1 × k or k × 1
 result: r × k
```

除其他内容外，上面的表说明了 `somefunction()` 如何处理空矩阵。`A` 必须是 r × c。该表并没有说：

```
A:   r × c, r > 0, c > 0
```




如果 `somefunction()` 不允许 A 为空，它就会那样写。因此，A 可以是 0×0。

## `[M-3] end` — 退出 Mata 并返回 Stata

### 语法

```mata
: end
```

### 描述

`end` 退出 Mata 并返回 Stata。

### 备注

当你从 Mata 返回到 Stata 时，Mata 不会清除自身；因此如果你稍后返回 Mata，你将回到之前的地方。请参阅 [M-3] mata。

### 另见

- [M-3] intro — 控制 Mata 的命令

## `[M-3] mata` — Mata 调用命令

### 语法

此处记录的 `mata` 命令用于在 Stata 中调用。它是你进入 Mata 的方式。你在 Stata 的点提示符（dot prompt）下输入 `mata`，而不是 Mata 的冒号提示符下。

| 语法 1 | 注释 |
| --- | --- |
| `mata` | `mata` 后面不加冒号 |
| `istmt` | 如果发生错误，你将留在 Mata 模式 |
| `istmt` | |
| `end` | 当输入 `end` 时退出 |

语法 1 是交互式使用 Mata 的最佳方式。

| 语法 2 | 注释 |
| --- | --- |
| `mata:` | `mata` 后面加冒号 |
| `istmt` | 如果发生错误，你会被从 Mata 中抛出 |
| `istmt` | |
| `end` | 否则，当你输入 `end` 时退出 |

语法 2 主要由程序员在 ado-files 中使用。程序员希望错误能停止一切操作。

| 语法 3 | 注释 |
| --- | --- |
| `mata istmt` | 极少使用 |

语法 3 是语法 1 的单行变体，但它并没有用。

| 语法 4 | 注释 |
| --- | --- |
| `mata: istmt` | 供程序员使用 |

语法 4 是语法 2 的单行变体，其存在的原因与语法 2 相同：供程序员在 ado-files 中使用。

### Mata 命令

`mata` 命令调用 Mata。`istmt` 是 Mata 能理解的内容；`istmt` 代表 Mata 的交互式语句（interactive statement）。

### 备注

备注在以下标题下给出：

- 引言
- 语法 3 和 4 之间的细微区别
- 语法 1 和 2 之间的细微区别

### 引言

交互使用请使用语法 1。输入 `mata`（不带冒号），按回车，然后就可以自由使用 Mata。输入 `end` 返回 Stata。（当你从 Mata 返回到 Stata 时，Mata 不会清除自身；因此如果你稍后再次输入 `mata` 后接 `回车`，你将回到之前的地方。）

编程使用请使用语法 2 或语法 4。在程序或 ado-file 内部，你可以直接调用 Mata 函数：

```stata
program myprog

mata: utility('varlist')

end
```

你甚至可以将该 Mata 函数包含在你的 ado-file 中：

```stata
program myprog

mata: utility('varlist')

end

mata:

function utility(string scalar varlist)
{
}

end myprog.ado
```

或者你也可以单独编译 `utility()` 并将其放入 `.mo` 文件或 Mata 库中。

### 语法 3 和 4 之间的细微区别

语法 3 和 4 都是单行语法。你输入 `mata`，后面可能带一个冒号，然后是 Mata `istmt`。

这两种语法的区别在于它们是否允许续行（continuation lines）。带有冒号时，不允许续行；不带冒号时，允许续行。

例如，让我们考虑：

```mata
function renorm(scalar a
```

无论函数有多长，它都是一个 `istmt`。如果你尝试在这里使用 `Mata::.` 来进入该 `istmt`，会发生以下情况：

```text
. mata: function renorm(scalar a, scalar b)
<istmt> incomplete
r(197);
```

当你到达第一行末尾并按回车时，你得到了错误信息。使用 `mata:` 命令时，`istmt` 必须全部挤在一行内。

现在尝试在不带冒号的情况下使用 `mata` 尝试同样的操作：

```text
. mata function renorm(scalar a, scalar b)
{
>
}
```

这成功了！不带冒号的单行 `mata` 允许续行，至少在这一点上，它似乎比带冒号的单行 `mata` 更好。但在编程语境下，这一特性可能会带来麻烦。考虑以下程序片段：

```stata
program example

mata utility("varlist")

replace 'x' = ...

end
```

我们使用了不带冒号的 `mata`，并且犯了一个错误：我们忘记了右括号。不带冒号的 `mata` 会寻找那个括号，因此会吞掉下一行——那一行并不是为 Mata 设计的。在这里我们会得到错误信息，因为 `"replace 'x' = ..."` 对 Mata 来说没有意义，但那个错误与我们应该收到的不同。在极少数糟糕的情况下，下一行对 Mata 来说是有意义的。

因此，不带冒号的单行 `mata` 也有程序员的用法。在我们上面的示例 ado-file 中，我们包含了例程 `utility()`，将其封装在 `mata:` 中，如果这样编写代码就是很满意的：

```stata
program myprog.ado

mata: utility("varlist")

end
```

```mata
function utility(string scalar varlist)
{
}

end myprog.ado
```

使用不带冒号的 `mata`，我们可以省略 `end`。我们承认我们有时会这样做。

### 语法 1 和 2 之间的细微区别

上述关于续行的说明均不适用于语法 1 和 2。多行 `mata`（或不带冒号的 `mata`）始终允许续行，因为 Mata 会话结束的地方足够清晰：这两种语法的区别在于 Mata 是宽容错误还是将你抛出到 Stata。多行 `mata` 宽容。程序员则希望严格。考虑以下内容（使用不带冒号的多行 `mata`）：

```stata
program example

...

mata
    result = myfunc("varlist")
    stata(J(0,0)
```

在上面的示例中，我们省略了 `"n"` 和 `result`。不带冒号的多行 `mata` 宽容了 `J(0,0)` 这种错误，Mata 随后会将控制权交给 Stata。不带冒号的多行 `mata`，这可能会产生严重后果。

### 另见

- [M-3] intro — 控制 Mata 的命令

## `[M-3] mata clear` — 清除 Mata 内存

### 语法

```mata
: mata clear
```

此命令用于 Mata 模式下的冒号提示符后。从 Stata 的点提示符使用此命令，输入：

```stata
. mata: clear
```

### 描述

`mata clear` 清除 Mata 的内存，相当于重置 Mata。所有函数、矩阵等都会被释放。

### 备注

Stata 可以调用 Mata，等等。在这种情况下，`mata clear` 只释放未使用的资源。Stata 的 `clear` 命令（见 [D] clear）会执行 `mata clear` 等操作。

清除单个矩阵请参考 [M-3] drop。

### 另见

- [M-3] drop — 删除矩阵或函数

## `[M-3] mata describe` — 描述 Mata 内存的内容

### 语法

```mata
: describe [namelist] all
: mata describe using libname
```

其中 `namelist` 定义见 [M-3]。如果未指定 `namelist`，则默认为 `()`。此命令用于 Mata 模式下的冒号提示符后。从 Stata 的点提示符使用此命令，输入：

```stata
mata: describe...
```

### 描述

`mata describe` 列出内存中矩阵和函数的名称，以及每个对象占用的内存量。

`mata describe using libname` 描述指定的 `.mlib` 库的内容；见 [M-3] mlib。

### 选项

`all` 指定如果自动加载的库位于内存中，也要包含在输出中。

### 备注

`mata describe` 通常不带参数执行，描述内存中的所有内容：

```text
mata describe

## bytes type name and extent

50 real matrix foo()

1,600 real matrix X[10,20]

8 real scalar x
```

`mata describe using libname` 列出存储在 `.mlib` 库中的函数：

```text
mata describe using libabase

## bytes type name and extent

984 auto numeric vector Corr()

340 auto real matrix Hilbert()

(output omitted)

528 auto transmorphic colvector vech()
```

### 诊断

报告的内存使用不包含开销（通常为 64 字节，但最近使用的标量可能为零）。

对于指针矩阵，报告的内存使用反映存储矩阵本身所需的内存，不包括兄弟节点占用的内存。

### 另见

- [M-5] `sizeof()` — 对象占用的字节数
- [M-3] intro — 控制 Mata 的命令

## `[M-3] mata drop` — 释放矩阵或函数

### 语法

```mata
: mata drop namelist
```

其中 `namelist` 定义在 [M-3] namelist 中。

此命令用于 Mata 模式，跟在 Mata 的冒号提示符之后。若要从 Stata 的点提示符使用此命令，请输入：

```stata
. mata: mata drop ...
```

### 描述

`mata drop` 从内存中清除指定的矩阵和函数。

### 备注

使用 `mata describe`（参见 [M-3] mata describe）确定内存中的内容。使用 `mata clear`（参见 [M-3] mata clear）删除所有矩阵和函数，或使用 Stata 的 `clear mata` 命令（[D] clear）。

要删除名为 A 的矩阵，请输入：

```mata
: mata drop A
```

要删除名为 `foo()` 的函数，请输入：

```mata
: mata drop foo()
```

要删除名为 A 的矩阵和名为 `foo()` 的函数，请输入：

```mata
: mata drop A foo()
```

### 另见

- [M-3] mata clear — 清除 Mata 内存
- [M-3] intro — 控制 Mata 的命令

## `[M-3] mata help` — 获取在线帮助

### 语法

```stata
: mata help...
: help...
```

`help` 前面不需要先加 `mata`。

### 描述

`mata help` 是 Stata 的帮助命令。因此，你无需退出 Mata 即可使用帮助。

### 备注

参见 [M-1] help。

你不需要输入 Mata 前缀：

- `mata help matan`（输出显示在 Stata 的查看器中）
- `help mata`（结果相同）

`help` 可用于获取 Mata 或 Stata 的帮助：

- `help mata missing()`
- `help missing()`

### 另见

- [M-1] help — 获取在线帮助
- [R] help — 显示在线帮助
- [M-3] intro — 控制 Mata 的命令

## `[M-3] mata matsave` — 保存和恢复矩阵

### 语法

```mata
: mata matsave filename namelist [ , replace]
: mata matuse filename [, replace]
: mata matdescribe filename
```

其中 `namelist` 是在 [M-3] namelists 中定义的矩阵名称列表。

如果指定的 `filename` 未带后缀名，则默认为 `.mmat`。

这些命令用于 Mata 模式，跟在 Mata 的冒号提示符之后。若要从 Stata 的点提示符使用这些命令，请输入：

- `mata: mata matsave ...`

### 描述

`mata matsave` 将指定的全局矩阵保存到 `filename` 中。

`mata matuse` 加载存储在 `filename` 中的矩阵。

`mata matdescribe` 描述 `filename` 的内容。

### `mata matsave` 的选项

`replace` 指定如果 `filename` 已经存在，则可以替换。

### `mata matuse` 的选项

`replace` 指定内存中任何与 `filename` 中存储的矩阵同名的矩阵都可以被替换。

### 备注

这些命令用于交互式使用；不用于程序内部。请参见 [M-5] `fopen()` 了解 Mata 用于读取和写文件的编程函数。在编程环境中，如果你有一个矩阵 X 并想将其写入文件 `mymatrix.file`，你的代码如下：

```mata
fh = fopen("mymatrix.myfile", "w")
fputmatrix(fh, X)
close(fh)
```

稍后，你可以通过编写代码读回：

```mata
fh = fopen("mymatrix.myfile", "r")
X = fgetmatrix(fh)
close(fh)
```




`mata matsave`、`mata matuse` 和 `mata matdescribe` 用于程序之外的交互式工作。你可以保存你的全局矩阵，并在稍后将它们重新取回来：

- `mata matsave mywork`（保存 `A`、`X`、`Z`、`beta`）
  `file mywork.mmat saved`

`mata matdescribe` 会告诉你文件的内容：

- `mata matuse mywork`（加载 `A`、`X`、`Z`、`beta`）
  `file mywork.mmat saved on 4 Apr 2009 08:46:39 contains X, X, Z, beta`

## 诊断

`mata matsave` 保存视图矩阵的内容。因此，当它们被 `mata matuse` 恢复时，无论 Stata 在内存中加载了什么数据，内容都是正确的。

## 另请

[M-3] intro — 控制 Mata 的命令

## 标题

[M-3] mata memory — report Mata 内存使用情况

## 语法

```
: mata memory
```

此命令用于 Mata 模式，跟在 Mata 的冒号提示符之后。若要从 Stata 的点提示符使用此命令，请输入：

```
mata: mata memory
```

## 描述

`mata memory` 提供了 Mata 当前内存利用的摘要。

## 备注

| | # | bytes |
| :--- | :--- | :--- |
| autloaded functions | 15 | 5,514 |
| adof functions | 0 | 0 |
| defined functions | 0 | 0 |
| matrices & scalars | 14 | 8,256 |
| overhead | | 1,972 |
| total | 29 | 15,742 |

函数分为三类：

1. 自动加载函数（Autoload functions），指的是从 `.mlib` 库文件和 `.mo` 对象文件中当前加载的库函数（并将会自动卸载）。
2. Ado 函数，指的是源代码出现在 ado-file 自身的函数。当 ado-file 被自动清除时，这些函数会被清除。
3. 定义函数（Defined functions），指的是通过交互式或来自 do-file 的函数，只有在执行 `mata clear`、`Mata drop`、`Stata clear` 或 `Stata clear all` 命令时才会清除；参见 [M-3] mata clear。

## 另请

- [M-3] memory limits — 内存限制
- [M-3] mata clear — 清除 Mata 内存
- [M-3] intro — 控制 Mata 的命令

## 标题

[M-3] mata mlib — 创建函数库

## 语法

```
: mata mlib create libname [ , dir(path) replace size(#) ]
: mata mlib add libname fcnlist() [ , dir(path) complete ]
: mata mlib index
: mata mlib query
```

其中 `fcnlist()` 是函数名称列表，例如

```
fcnlist() examples
myfunc()
otherfunc()
foo()
```

参见 [M-3] namelists

且 `libname` 是库的名称。你不需要添加 `.mlib` 后缀，因为它会自动为你添加。库示例：

| libname | 文件名 |
| :--- | :--- |
| `lmath` | `lmath.mlib` |
| `loremath` | `loremath.mlib` |
| `lnjc` | `lnjc.mlib` |

此命令用于 Mata 模式，跟在 Mata 的冒号提示符之后。若要从 Stata 的点提示符使用此命令，请输入：

```
mata: mlib...
```

## 描述

`mata mlib` 创建、添加并索引 `.mlib` 文件，这些是包含对象的库。

## [M-3] mata mlib — 创建函数库

`mata mlib create` 创建一个新的库。

`mata mlib add` 向库添加新成员。

`mata mlib index` 导致 Mata 构建新的搜索列表。
`mata mlib query` 列出要搜索的库。
默认可以包含 1024 个函数。

## 选项

`dir(path)` 指定写入文件的目录（文件夹）。默认为 `dir()`，意味着未指定时写入当前（工作）目录。`path` 可以是目录或 `sysdir` 简写 `STATA`、`UPDATES`、`BASE`、`SITE`、`PLUS`、`PERSONAL` 或 `OLDPLACE`；参见 [P] sysdir，建议使用 `dir(PERSONAL)`。
`complete` 用于保存类。它指定只有在类完整时才保存；否则将发出错误消息。参见 [M-2] class。
`replace` 指定如果文件已经存在，则可以替换。
`size(#)`。在 `mlib create` 时，指定新创建的库能够包含的最大成员数量，`2 ≤ # ≤ 2048`。默认是 `size(1024)`。

## 备注

备注在以下标题下：

- 背景
- 处理库的流程概述
- 创建 `mlib` 库
- 向 `.lib` 库添加成员
- 列出库的内容
- 让 Mata 知道搜索你的库
- 组织源代码的建议

另 [M-1] how 以了解对象代码。

## 背景

`.mlib` 文件包含一个或多个函数的对象代码。存储在库中的函数被称为库函数，Mata 的库函数也存储在 `.mlib` 库中。你也可以创建自己的库。

Mata 提供了两种存储对象代码的方式

1. 在 `.mo` 文件中，包含一个函数的代码
2. 在 `.mlib` 库文件中，可以包含最多 500 个函数的代码

## 处理库的流程概述

使用库非常简单：

- 首先，为你的库选择一个名称。我们将选择名称 `l1personal`。
- 其次，使用 `mata mlib create` 命令创建一个空库。
- 之后，你可以随时使用 `mata mlib add` 向库中添加新成员。

`.mlib` 库包含对象代码，而不是原始源代码，因此你需要自己跟踪源代码。此外，如果你想更新其中某个函数的对象代码，必须重新创建整个库；一旦成员被添加，就无法进行替换或删除。

我们首先展示操作层面的步骤，然后告诉我们我们是如何管理库和源代码的。

## 创建 `.mlib` 库

如果你还没有读过 [M-3] `mata mosave`，请先阅读它。

要在当前目录下创建一个名为 `l1personal.mlib` 的新空库，请输入：

```mata
mata mlib create l1personal
file l1personal.mlib created
```

如果 `l1personal.mlib` 已经存在且你想替换它，可以先删除现有文件，或者输入：

```mata
mata mlib create l1personal, replace
file l1personal.mlib created
```

要在你的 `PERSONAL` 目录（参见 [l|1] `sysdir`）下创建一个名为 `l1personal.mlib` 的新空库：

```mata
mata mlib create l1personal, dir(PERSONAL)
file c:\ado\personal\l1personal.mlib created
```

或者：

```mata
mata mlib create l1personal, dir(PERSONAL) replace
file c:\ado\personal\l1personal.mlib created
```

## 向 `.mlib` 库添加成员

一旦库存在（无论你是刚刚创建的空库，还是已经存在并包含某些函数），你都可以通过输入以下命令向其添加新函数：

```mata
mata mlib add libnameM()
```

例如，如果我们想向 `l1personal.mlib` 库添加 `example()` 函数，我们将输入：

```mata
mata mlib add l1personal example()
(1 function added)
```

在此操作过程中，我们不需要指定 `l1personal.mlib` 的存储位置；Mata 会沿着 ado-path 搜索它。

然而，在向库添加 `example()` 之前，你必须先编译它：

```mata
: function example(...)
{
  ...
}
: mata mlib add l1personal example()
(1 function added)
```

你可以在一条命令中向库添加多个函数：

```mata
: mata mlib add l1personal example2() example3()
(2 functions added)
```

你可以通过输入以下命令添加内存中当前所有的函数：

```mata
: mata mlib add another *()
(3 functions added)
```

在上面的示例中，我们向 `another.mlib` 添加了内容，因为我们已经向 `l1personal.mlib` 添加了 `example()`、`example2()` 和 `example3()`，再次尝试添加它们会导致错误。（在添加 `*` 之前，我们可以通过输入 `mata describe *` 来验证我们正在添加我们想要的内容；请参见 [M-3] `mata describe`。）

## 列出库的内容

一旦库存在，你可以通过输入以下命令列出其内容（它包含的函数名称）：

```mata
: mata describe using libname
```

在这里我们将输入：

```mata
: mata describe using l1personal
(library contains 3 members)
```

| bytes | type | name and extent |
| :--- | :--- | :--- |
| 32 | auto transmorphic matrix | `example()` |
| 32 | auto transmorphic matrix | `example2()` |
| 32 | auto transmorphic matrix | `example3()` |

`mata describe` 列出内存的内容，而 `mata describe using` 列出库的内容。

## 让 Mata 知道去搜索你的库

Mata 会自动找到你电脑上的 `.mlib` 库。这在 Mata 于会话期间首次调用时就会完成。所有操作都是自动的，除非 Mata 会感知在 Stata 会话期间创建的任何新库，因此在创建新库后，你必须告诉 Mata 关于它的。你通过要求 Mata 重建库索引来实现：

```mata
: mata mlib index
```

你不需要指定新库的名称。该名称并不重要，因为 Mata 会重建它的整个库索引。

你可以在创建新库后立即执行 `mata mlib create` 命令：

- `mata mlib create l1personal, dir(PERSONAL)`
- `mata mlib index`

或者在你创建并向库添加内容后：

- `mata mlib create l1personal, dir(PERSONAL)`
- `mata mlib add l1personal *`
- `mata mlib index`

这并不重要。在已知库更新后，Mata 不需要重建索引。只有在会话期间添加了新库时，才需要告知重建。

## 关于组织源代码的建议

假设你想创建并维护 `l1personal.mlib`。我们倾向的方法是使用 do-file：

```mata
mata:
mata clear
function definitions appear here
mata mlib create lpersonal, dir(PERSONAL) replace
mata mlib add l1personal *
mata mlib index
end
```

这样这样，我们创建或重建库所需要做的就是进入 Stata，切换到包含源代码的目录，然后输入：

- `do l1personal`

对于大型库，我们喜欢将不同部分的源代码放在不同的文件中：

```mata
mata:
mata clear
do function1.mata
do function2.mata
...
mata:
mata mlib create lpersonal, dir(PERSONAL) replace
mata mlib add lpersonal *
mata mlib index
end
```

## 标题

[M-3] mata rename — 重命名矩阵或函数

## 语法

```
: mata rename oldmatrixname newmatrixname
: mata rename oldfcnname() newfcnname()
```

此命令用于 Mata 模式（跟在 Mata 的冒号提示符后）。若要在 Stata 的点提示符下使用此命令，请输入

```
mata: mata rename ...
```

## 描述

`mata rename` 修改函数和全局矩阵的名称。

## 参见

[M-3] intro — 控制 Mata 的命令

## 标题

[M-3] mata set — 设置和显示 Mata 系统参数

## 语法

```
: mata query
: mata set matacache [# [, permanently]
: mata set matalum {off | on}
: mata set mataoptimize {on | off}
: mata set matafavor {space | speed} [, permanently]
: mata set matastric {off | on} [, permanently]
: mata set matalibs "libname;libname;..."
: mata set mataoffirst {off | on} [, permanently]
```

这些命令用于 Mata 模式（跟在 Mata 的冒号提示符后）。若要在 Stata 的点提示符下使用这些命令，请输入

- `mata: mata query`
- `mata: mata set ...`

## 描述

`mata query` 设置 Mata 系统参数的值。
`mata set` 设置系统参数的值：

`mata set matacache` 指定在 Mata 开始尝试删除当前未使用的自动加载函数之前，可能消耗的最大内存量（以千字节为单位）。默认值为 400，即 400 千字节。此参数影响 Stata 运行的效率。值设大一些并无害处，但一旦 `matacache` 足够大，更大的值将不会提高性能。

`mata set matalum` 开启或关闭程序行号追踪。默认设置为关闭。此设置会修改程序的编译方式。当开启 `matalum` 时，编译的程序将包含代码信息，以便在程序执行期间发生错误时可以报告行号。开启 `matalum` 会防止 Mata 进行优化，因此运行速度会较慢。在调试时，建议将此设置为关闭。

`mata set mataoptimize` 开启或关闭编译时优化。默认设置为开启。关闭 `mataoptimize` 后，编译的程序运行较慢，有时甚至慢得多。如果怀疑优化器有 bug，则将 `mataoptimize` 设置为 `off`。

`mata set metafavor` 指定在执行代码时，倾向于节省内存（`space`）还是运行速度（`speed`）。默认设置为 `space`。切换到 `speed` 会让 Mata 在某些情况下运行更快，但会消耗更多内存。参见 [M-5] `favored()`。

`mata set metastrict` 设置程序内部是否允许省略声明。默认设置为关闭。如果开启 `metastastrict`，省略声明的程序会导致编译时错误。在 ado 文件内部设置/重置 `metastastrict` 的行为可能异常；参见 [M-2] ado。

`mata set matolib` 设置要搜索的 `.mlib` 库名称和顺序；参见 [M-1] ado。`matolib` 通常设置为 `"matabase;ado"`。这样设置是正确的，因为 Mata 在第一次调用时会自动搜索 ado 路径。在 Mata 会话期间，删除或复制新库的最佳方法是使用 `matolib` 命令；参见 [M-3] matolib。手动设置 `matolib` 是为了修改搜索库的顺序。

`metamofirst` 表示优先搜索文件还是 `.mlib` 库。默认设置为关闭，即搜索库。

## 选项

`permanently` 指定除了当前更改外，该设置将在以后调用 Stata 时被记住并成为默认设置。

## 备注

备注位于以下标题下：

- Mata 的 set 与 Stata 命令的关系
- (c) 值

### Mata 的 set 与 Stata 的 set 命令的关系

```
: mata set ...
```

在 Mata 的冒号提示符下输入与

```
set ...
```

在 Stata 的点提示符下输入是相同的命令，因此你可以这样设置 Mata 的（甚至是 Stata 的）系统参数。

```
: mata query
```

在 Mata 的冒号提示符下输入与

```
. query mata
```




在 Stata 的点提示符下输入也是相同的。

# [M-3] `mata set` — 设置和显示 Mata 系统参数

## `c()` 值

以下内容涉及 Stata 多于 Mata。

Stata 的 `c()` 类包含了系统参数、设置以及其他常量。`c()` 值可以在 Stata 中引用，例如通过宏替换 `c(current_date)`，或者在表达式中（此时可以省略宏引号）。Stata 的 `c()` 在 Mata 中也通过 Mata 的函数可用；参见 [M-3] `c()`。

大多数 `set` 参数都可以通过 `c()` 获取，包括 Mata 的 `set` 参数：

- `c(matacache)` 返回缓存大小的数值标量。
- `c(matalum)` 返回 `"on"` 或 `"off"`。
- `c(mataoptimize)` 返回 `"on"` 或 `"off"`。
- `c(matafavor)` 返回 `"space"` 或 `"speed"`。
- `c(matastrict)` 返回 `"on"` 或 `"off"`。
- `c(matalibs)` 返回由分号分隔的库名称字符串。
- `c(matofirst)` 返回 `"on"` 或 `"off"`。

上述是 Stata 表达式。如果我们使用 Mata 的函数，我们会引用 `c("matacache")` 而不是 `c(matacache)`。然而，这些值的实际用法是在 Stata 中。

## 参见

- [R] `query` — 显示系统参数
- [R] `set` — 系统参数概述
- [P] `return` — 返回 `c()` 类值
- [M-3] `intro` — 控制 Mata 的命令

# [M-3] `mata stata` — 执行 Stata 命令

## 语法

```stata
: mata stata stata_command
```

此命令用于 Mata 模式（跟在 Mata 的冒号提示符后）。

## 描述

`mata stata stata_command` 将 `stata_command` 传递给 Stata 执行。

## 备注

`mata stata` 是一个方便工具，让你无需退出 Mata：

```stata
: mata stata
```

是交互式的。如果你想在函数中执行 Stata 命令，参见 [M-5] `stata()`。

## 参见

- [M-5] `stata()` — 执行 Stata 命令
- [M-3] `intro` — 控制 Mata 的命令

# [M-3] `mata which` — 识别函数

## 语法

```stata
: mata which fcnname
```

此命令用于 Mata 模式（跟在 Mata 的冒号提示符后）。若要在 Stata 的点提示符下使用此命令，请输入：

```stata
mata: mata which fcnname
```

## 描述

`mata which fcnname` 查找 `fcnname()` 并报告它是内置的、存储在 `.mlib` 中还是存储在 `.mo` 文件中。

## 备注

`mata which fcnname()` 查找 `fcnname()` 并报告其位置：

- `I()`：内置
- `assert()`：数据库
- `myfcn()`：`.mo`
- `nosuchfunction()`：未找到 `r(111)`

函数 `I()` 是内置的，它是 Mata 的一部分。

函数 `assert()` 是一个库函数，事实上，它的可执行代码位于 `matabase.mlib`。

函数 `myfcn()` 存在，其可执行代码存储在当前目录的 `myfcn.mo` 中。

函数 `nosuchfunction()` 不存在。

回到 `mata which matabase.mlib`，如果你想知道 `matabase.mlib` 存储在哪里，可以在 Stata 提示符下输入 `findfile matabase.mlib`：[P] `findfile`。

## 参见

- [M-3] `intro` — 控制 Mata 的命令

# M-3 name lists — 指定矩阵和函数名

## 语法

许多 Mata 命令允许或要求使用列表，例如：

```stata
: mata describe [namelist] [, all]
```

列表定义为矩阵和/或函数名的列表，例如：

```text
alpha beta()
```

上述列表指的是矩阵 `alpha` 和 `beta` 以及函数 `foo()`。

函数名始终以 `()` 结尾，因此：

- `alpha` 指矩阵 `alpha`
- `alpha()` 指同名的函数

名称也可以使用通配符 `*` 和 `?` 来指定：

- `*` 意味着这里可以是零或多个字符
- `?` 意味着这里正好有一个字符

因此：

- `*` 表示所有矩阵
- `(*)` 表示所有函数
- `*()` 表示所有矩阵和函数
- `s*` 表示所有 `s` 开头的矩阵
- `s*(` 表示所有 `s` 开头的函数
- `*e` 表示以 `e` 结尾的矩阵
- `*e()` 表示所有以 `e` 结尾的函数
- `s*e` 表示以 `s` 开头、以 `e` 结尾的矩阵
- `s*e()` 表示以 `s` 开头、以 `e` 结尾的函数
- `s?` 表示以 `s` 开头、以 `e` 结尾且中间有一个字符的矩阵
- `s?()` 表示以 `s` 开头、以 `e` 结尾且中间有一个字符的函数

## 描述

列表显示在语法图中。

## 备注

某些名称列表仅允许矩阵，而另一些仅允许函数。即使仅允许函数，你也必须包含 `()` 后缀。

## 另见

- [M-3] 简介 — 控制 Mata 的命令

# MATA 矩阵编程

[M-0]–[M-3]

Stata® 支持多种操作系统，包括 Windows®、Mac® OS X 和 Unix®。

有关 Stata 及 Stata 产品的更多信息，请联系：

StataCorp LP  
4905 Lakeway Drive  
College Station, TX 77884  
USA

电话：979-696-4600  
800-782-8272  
800-STATAPC

传真：979-696-4601

[www.stata.com](http://www.stata.com)  
service@stata.com

![](img/94f0e160fb245a717f6d9189ad47298e_267_0.png)

版权所有 © 2011

![](img/94f0e160fb245a717f6d9189ad47298e_267_1.png)

