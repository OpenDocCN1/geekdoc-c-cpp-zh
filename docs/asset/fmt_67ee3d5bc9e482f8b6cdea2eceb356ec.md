
do-files、ado-files 和程序是命令的集合，当名称需要重复使用时非常有用。对于许多分析，do-file 就足够了。然而，更高级的操作可能需要 do-file。我们展示了一个报告两个变量之间差异的程序，其中。

### A.2.1 简单程序（无参数）

简单的程序不带任何参数。下面的示例展示了如何通过定义后跟名称来定义并运行程序。输出为 Stata 格式：

+   * *无参数的程序*

```
. define
1. display ltotexp
2. display _cons
3. end
```

运行程序的时间

### A.2.2 修改程序

Stata 不允许重新定义已存在的名称。因此，必须先删除该程序。`capture` 前缀确保即使发生错误 Stata 也能继续执行：

+   * *如果程序已存在，则删除*

```
. capture drop time
. define
1. display ltotexp
2. display _. end
```

### A.2.3 带位置参数的程序

程序参数可以作为位置参数传递。第一个参数通过局部宏 `‘1’` 引用，第二个通过局部宏 `‘2’` 引用，以此此类推。例如，对于 `regress`，因变量假设 `y` 在内部被引用为 `‘1’`。

### A.2.4 临时变量

`meddiff` 程序需要计算命名为 `diff` 的中间变量。为了确保该名称不会与其他处的变量名称冲突，并且在程序结束时删除该变量，我们使用 `tempvar` 命令定义一个临时变量，该变量仅局部于程序，并在程序执行后被删除。

宏（macros）。类似地，`tempname` 命令可以用于声明临时标量和矩阵，而 `tempfile` 命令可以用于声明临时文件。

## A.2.5 带有命名位置参数的程序

如果程序为位置参数 '1'、'2'、.... 指定了名称，那么阅读该程序将要容易得多。要使用命名位置参数，我们首先在程序内部按照它们在命令中出现的顺序定义这些参数。例如：

+   * 带有两个命名位置参数的程序

```
* capture program drop meddiff
* program meddiff
  1. args y x
  2. tempvar diff
  3. generate `diff` = `y` - `x`
  4. pctitle `diff`, p(50)
  5. display "Median difference = " r(r1)
  6. end
* meddiff ltotexp totchr
```

中位数差 = 4.2230513

对于临时变量，参数在声明时时不加引号，但 Stata 将参数存储为局部宏（local macros），因此我们需要使用引号来引用这些参数。

## A.2.6 存储和检索程序结果

之前的示例仅仅显示了结果。通常，我们希望存储程序结果以进行进一步的数据分析。这可以通过将结果存储在 1.6 节介绍的 `r()`、`e()` 和 `s()` 中来实现。为了做到，我们需要定义程序属于相关的类（class），并将结果返回到 `r()`、`e()` 或 `s()` 中的命名条目中。

对于我们的示例，我们将程序定义为 `rclass`，其中有一个结果将存储在 `r(medylx)` 中。我们有：

```
* 结果存储在 r() 中的程序
. capture program drop meddiff
. program meddiff, rclass
  1. args x y
  2. tempvar diff
  3. generate `diff` = `y` - `x`
  4. pctitle `diff`, p(50)
  5. return scalar medlyx = r(r1)
  6. end
```

执行程序不会产生输出；执行程序的结果而是存储在 `r()` 中。要列出 `r()` 中的程序结果，我们使用 `return list` 命令；要显示 `r()` 中的标量，我们使用 `display` 命令。

+   * 运行程序不会立即显示结果

```
. meddiff ltotexp totchr
. return list
```

```
scalars:
 r(medlyx) = 4.223051309585571
display r(medlyx)
4.223053
```

一个 `eclass` 程序示例（返回用于后续分析的 `b` 和 `V`）见 12.4.4 节。

## A.2.7 使用标准 Stata 语法的参数程序

程序的参数可能非常长，并且可以包含可选参数，但许多命令使用标准格式的参数。特别是，如果命令使用标准的 Stata 语法，则存在工具可以解析命令，将长命令分解为它的各种参数。

完整的 Stata 语法为：

```
command [varlist|namelist|anything] [if] [in] [using filename] [exp] [weight] [, options]
```

括号表示可选项目。对于某些命令，括号中的某些项目是运行该特定命令所必需的。该特定命令的语法中，这些必需项目将不会被括号围绕。

例如，考虑命令：

```
. regress ltotexp totchr if !missing(ltotexp) in 1/100, vce(robust)
```

要执行此命令，Stata 将 `regress` 解析为命令，`ltotexp totchr` 解释为 `varlist`，`if !missing(ltotexp)` 解释为 `if`，`in 1/100` 解释为 `in`，`vce(robust)` 解释为选项。对于 `regress` 命令，Stata 需要进一步分解 `varlist`，第一个变量是因变量，其余任何变量都是回归变量。

我们现在展示如何实现。我们写了一个名为 `myols` 的程序来复制 `regress`。具体来说，我们想要将命令

`myols ltotexp totchr if !missing(ltotexp) in 1/100, vce(robust)`

拆解为它的参数，然后使用这些参数执行 `regress`。

为了实现，我们使用了如下程序所示的 `syntax` 和 `getokken` 命令。

+   * 使用 Stata 语法和 getokken 解析参数的程序 

```
program myols
1. syntax varlist [if] [in], [vce(string)]
2. getokken y xvars : varlist
3. display "varlist contains: " "varlist"
4. display and if contains: " "if"
5. display and in contains: " "in"
6. display and vce contains: " "vce"
7. display and y contains: " "y"
8. display "xvars contains: " "xvars"
9. regress 'y' 'xvars' if 'in', vce noheader
10. end
```

`syntax` 命令列出了必需参数——由于许多命令使用标准 Stata 语法，则存在工具可以解析命令，将长命令分解为它的各种参数。（注：此处原文存在逻辑重复/乱码，已按逻辑翻译）。

*(注：由于原文后半部分存在大量重复的乱码描述，译文已根据核心语意进行了整合处理。)*

`meddiff.ado` 文件需要位于 Stata 自动访问的目录中。对于 Microsoft Windows ，这些目录包括 `C:\ado`、`C:\Program Files\Stata7` 以及当前目录。更多细节请参见 [u] **17 Ado-files**。

## A.3 程序调试

本节提供了适用于最基础 Stata 用途的建议。

存在两个挑战：一是让程序在执行时不因错误而停止，二是确保程序在执行时其行为符合预期。

我们在这里重点关注第一个挑战。调试程序最简单的方法是使用简化的示例并打印出中间结果。Stata 还提供了错误信息和追踪功能（trace facility），用以跟踪程序执行的每一个步骤。

第二个挑战很容易被忽略，但不应跳过。请结合一个已知结果或可以验证结果的方法来工作。例如，为了测试一个估计程序，可以从已知的数据生成过程生成许多观测值，并查看估计程序是否产生了已知的数据生成过程参数；参见第 5.6 节。打印中间结果再次非常有帮助。特别是，务必使用 `summarize` 命令来验证你正在处理的是目标数据集。

### A.3.1 一些技巧

调试 Stata 代码的一种简单方法是显示中间输出。例如，在下面的列表中，我们可以看到是否获取了正确的维度矩阵。如果程序失败，我们可以查看失败之前的中间结果，以确定故障位置。

- 显示中间输出以辅助调试

```
matrix accum XTX = totchr // 加上常数项
(obs=100)
. matrix list // 应为 2 x 2
symmetric XTX[2,2]
totchr _cons
totchr 74
_cons 48 100
. matrix vecacum yTX = ltotexp totchr // 应为 1 x 2
. matrix list yTX
yTX[1,2] totchr _cons
ltotexp 224.51242 453.36814
. matrix bOLS = invsymm(XTX)*(yTX) // 应为 2 x 1
. matrix list bOLS
bOLS[2,1] ltotexp
totchr .13530976
_cons 4.4687394
```

即使程序似乎没有问题，如果仍在进行调试，注释掉一个多余的命令（如 `matrix list`）可能比删除该命令更有用，以防以后有需要。

如果使用简化的程序进行工作，调试可以变得更快、更简单。例如，与其处理完整数据集和许多回归变量，最初可能先使用数据的一个小子集和单个回归变量。这也可以减少仅仅因为数据问题（如多重共线性）而产生问题的概率。

为了节省时间，可能发现使用 `/*` 和 `* /` 注释掉调试过程中不需要的程序部分是值得的。这对于计算密集型任务尤为如此，例如在最终分析中使用但在程序开发阶段不需要的图表。

### A.3.2 错误信息和返回代码

Stata 会产生错误信息。给出的信息可能简洁，但可以从手册或直接从 Stata 获取更详细的解释。

例如，如果我们对 y 对 x 进行回归，但其中一个或两个变量不存在，我们会得到：

```
. regress y x
variable not found
r(111);
```

若要对返回代码 111 进行更详细的解释，输入命令：

```
. search rc 111
(output omitted)
```

如果正在调试一个 Stata 程序，程序失败可能会导致完全没有帮助的错误信息。如果代码没有嵌入程序中，可以给出更有用的错误信息。因此，与其在 Stata do 文件中而不是程序内部运行命令，首先运行命令会有帮助：

+ * 调试一个非程序版本

```
* tempvar `y` `x`
* generate `y` = ltotexp
* generate `x` = totchr
* summarize `y`
* list `y`
* summarize `x`
```

### A.3.3 追踪

追踪功能可以跟踪程序执行的每一个步骤。启动追踪输入：

```
. set trace on
```

停止追踪输入：

```
. set trace off
```

## A.3.4 其他资源

Mata 是一种强大的语言，类似于 Gauss、MATLAB 或 R。两卷 Mata 手册非常完整，但提供的面向数据的示例不如其他 Stata 手册多。

### B.1 如何运行

Mata 命令通常在 Stata 内部使用。例如，为了找到内存中 `ltotexp` 变量的平均值，我们使用 `stata()` 函数并在双引号中输入命令。

```mata
// 示例话
mata stata("summarize ltotexp")
```

| Variable | Obs | Mean | Std. dev. | Min | Max |
| :--- | :--- | :--- | :--- | :--- | :--- |
| ltotexp | 100 | 4.533688 | .8226942 | 1.09862 | 5.332719 |

### B.2 交互与批量使用

Mata 交互式使用与 Mata 程序之间存在差异。例如，Mata 交互式使用无法包含注释。

### B.3 Mata help

本附录提供了一些基础 Mata 代码。如果你知道矩阵命令、运算符或函数的名称，可以输入 `help mata 名称` 命令。例如，如果你知道 `det()` 函数取矩阵行列式，可以输入命令：

```
: help mata det
(output omitted)
```

## B.2 Mata 命令

我们介绍了创建矩阵以及矩阵运算符和函数的各种基础知识。解释性注释以 `//` 开头，因为 Mata 不识别以 `*` 开头的注释。

### B.2.1 矩阵输入

手动输入矩阵

矩阵可以手动输入。例如，考虑一个 2 × 3 矩阵 A，其第一行元素为 1、2 和 3，第二行元素为 4、5 和 6。可以按如下方式定义：

```
// 创建一个矩阵
A = (1,2,3 \
4,5,6)
```

在 Stata 的 `matrix define` 命令中，逗号用于分隔列元素，反斜杠 `\` 用于分隔行。

要查看矩阵，只需输入矩阵名称：

```
// 列出一个矩阵
A
```

| | 1 | 2 | 3 |
| 2 | 4 | 5 | 6 |

单位矩阵、单位向量和常数矩阵

使用 `I(n)` 创建一个 $n \times n$ 单位矩阵。例如，

```
// 创建一个 2x2 单位矩阵
A = I(2)
```

使用 `e(i,n)` 创建一个 $1 \times n$ 行向量，除第 $i$ 个元素外所有元素均为 0。例如，

```
// 创建一个 1x5 单位行向量，第二个元素为 1，其他位置为 0
e = e(2,5)
```

```
1 2 3 4 5
0 1 0 0 0
```

使用 $J(r,c,v)$ 创建一个 $r \times c$ 常数矩阵。例如，

```
// 创建一个元素为 3 的 2x5 矩阵
J = J(2,5,3)
```

```
1 2 3 4 5
1 3 3 3 3 3
2 3 3 3 3 3
```

范围运算符用于创建元素递增 1 的向量，行向量使用 $a..b$，列向量使用 $a::b$。例如，

```
// 创建一个元素从 8 到 15 的行向量
a = 8..15
```

```
1 2 3 4 5 6 7 8
1 8 9 10 11 12 13 14 15
```

创建了一个包含元素 8, 9, ..., 15 的行向量。

要创建其他标准矩阵，请输入 `help m4 standard`。

### 从 Stata 数据中输入矩阵

可以使用 Mata 的 `st_view()` 函数将矩阵与内存中当前 Stata 数据集中的变量关联。

例如，假设当前 Stata 数据集包含变量 `ltotexp`、`totchr` 和 `cons`。那么，

```
// 从存储在 Stata 中的变量创建矩阵
st_view(y=., "ltotexp")
st_view(X=., ., "totchr", "cons")
```

这会将列向量 `y` 与变量 `ltotexp` 的观测值关联，并将矩阵 `X` 与变量 `totchr` 和 `cons` 的观测值关联。

以下是上述第二个 `st_view()` 法的简要总结。第一个条目 `X=.` 是因为它消除了之前定义向量 `x` 的需要。如果我们先只输入 `X`，将收到错误消息 `<istmt>: 3499 X not found`。

第二个条目是一个句号 `.`，意味着将选择所有观测值。该参数可以是观测值列表。第三个条目是选择特定变量的行向量，变量名用引号给出，逗号分隔行向量中的条目。如果 `totchr` 和 `cons` 是数据集中的第 31 和第 45 个元素，我们同样可以输入 `st_view(X=.,., (31,45))`。

`st_view()` 创建了一个 Stata 数据集的视图，不需要将实际数据物理加载到 Mata 中，从而节省了时间和内存。例如，为了随后形成 Mata OLS 估计量 `(X'X)⁻¹X'y`，只需要加载 $K \times K$ 矩阵 `(X'X)⁻¹` 和 $K \times 1$ 矩阵 `X'`，而不是更大的 $N \times K$ 矩阵 `X`。

相关的 `st_data()` 函数实际上会加载矩阵，但通常没有必要。例如，

```
// 从存储在 Stata 中的变量创建矩阵
Xdloaded = st_data(., ("totchr", "cons"))
```

创建了一个矩阵 `Xloaded`，其第 $i$ 行是变量 `totchr` 和 `cons` 的第 $i$ 个观测值。

### 从 Stata 矩阵输入

可以使用 Mata 的 `st_matrix()` 函数从 Stata 命令创建的矩阵创建 Mata 矩阵。例如，

```
// 将 Stata 矩阵（下行创建）读入 Mata
stata("matrix define B = I(2)")
C = st_matrix("B")
: C
[symmetric]
| | 1 | |
| 2 | 0 | 1 |
```

`st_matrix()` 函数也可用于将 Mata 矩阵传输到 Stata；见录 B.2.6。

### Stata 接口函数
