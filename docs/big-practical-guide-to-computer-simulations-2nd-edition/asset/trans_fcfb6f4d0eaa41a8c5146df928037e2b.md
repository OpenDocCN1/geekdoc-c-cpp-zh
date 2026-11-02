
另一种替代方法是直接以能够处理几乎任意晶格类型的方式来编写程序。这可以通过在一个特殊的初始化子程序（此处不讨论）中建立近邻关系，并将其存储到数组 `next[]` 中来实现。这样，对于所有晶格类型和维度，子程序之外的代码都保持不变。由于代码应适用于所有可能的晶格维度，数组 `next` 是一维的。假设每个格点有 `num_n` 个近邻。那么格点 `i` 的近邻可以存储在 `next[i*num_n]`、`next[i*num_n+1]`、……、`next[i*num_n+num_n-1]` 中。请注意，格点从 1 开始编号。这意味着，一个具有 `N` 个自旋的系统需要一个大小为 `(N+1)*num_n` 的数组 `next`。使用自由边界条件时，缺失的近邻可以设为 0。使用宏 NEXT 可以使对该数组的访问更加容易：

```
#define NEXT(i,r)  next[(i)*num_n + r]
```

`NEXT(i,r)` 包含自旋 `i` 在方向 `r` 上的近邻。例如，对于方形系统，`r=0` 是 +x 方向，`r=1` 是 −x 方向，`r=2` 是 +y 方向，`r=3` 是 −y 方向。不过，采用哪种约定取决于你，但应确保它们一致。对于方形晶格的情况，`num_n=4`。请注意，每当使用宏 NEXT 时，都必须定义一个变量 `num_n`，用于存储近邻数。你也可以将 `num_n` 作为宏的第三个参数，但这样调用宏会显得稍微更令人困惑。不过，如何定义这样的宏取决于你的个人偏好。

NEXT 宏不能通过内联函数实现，因为你可能想直接设置值，例如 `NEXT(i,0)=i+1`。此外，使用内联函数时，你必须显式包含所有参数，即示例中的 `num_n`。最后这一要求可以通过使用全局变量来规避，但这同样是不好的编程风格。

当系统是伊辛自旋玻璃时，每对自旋之间相互作用的符号和大小可能不同。相互作用强度可以以类似于近邻关系的方式存储，例如存储在数组 `j[]` 中。可以通过宏 J 简化访问：

```
#define J(i,r)  j[(i)*num_n + r]
```

用于计算能量 $H = \sum_{\langle i,j\rangle} J_{ij}\sigma_i\sigma_j$ 的子程序可能如下所示（请注意，参数 `N` 表示自旋数，自旋值存储在数组 `sigma[]` 中）：

## 练习

（解答：可从 http://www.worldscientific.com/t/9019-supp 下载）

### (1) 结构及其大小

编写一个程序，使用 typedef 建立一个用于氨基酸（蛋白质的基本构建单元）的数据结构，并打印其大小。该结构应包含以下四个元素：

- 一个 char 类型的氨基酸“类型”
- 一个 int 类型的“电荷”（以电子电荷为单位）
- 一个用于位置的三维向量
- 一个用于速度的三维向量

主程序应使用 sizeof() 命令打印该数据结构的大小。请与各个元素大小之和进行比较！

解决方案源代码
DIR: c-programming
FILE(S): struct_size.c

### (2) 指针操作技巧

编写一个程序，其中包含一个 double 变量 value、一个应包含 value 地址的指针 p1，以及一个应包含 p1 地址的指针 p2。

执行以下步骤

- (a) 使用合适的数据类型定义 p1 和 p2。
- (b) 将所需的值赋给 value、p1 和 p2。
- (c) 使用 printf 和合适的转换说明符打印 value、p1 和 p2。
- 此外，分别仅通过 p1 和仅通过 p2 打印 value 的内容。

解决方案源代码
DIR: c-programming
FILE(S): pointers.c

### (3) 矩阵置换

编写一个程序，对给定的矩阵 test 进行置换，使相邻行交换。使用一个适当选择的置换矩阵 perm（从左侧）与 test 相乘。

该程序应

- (a) 包含三个矩阵的定义，其中一个是 n×n 置换矩阵（n 为偶数）perm，另外两个（test、result）是 n×n 矩阵，
- (b) 初始化 perm，使相邻行交换，
- (c) 以任意方式初始化 test，使得不同行可以区分，
- (d) 计算矩阵乘积 result = perm × test

解决方案源代码
DIR: c-programming
FILE(S): matrix.c

### (6) **函数积分**

编写一个函数，使用梯形法则在区间 $[x_1, x_2]$ 上对一维函数 $f(x)$ 进行积分，即计算

$$I = \sum_{t=0}^{t_{\max}-1} \frac{f(x_1 + t\Delta) + f(x_1 + (t+1)\Delta)}{2} \Delta$$ 
$$= \frac{f(x_1)}{2} \Delta + \sum_{t=1}^{t_{\max}-1} f(x_1 + t\Delta)\Delta + \frac{f(x_2)}{2} \Delta$$

其中 $t_{\max}$ 是积分步数，$\Delta = (x_2 - x_1)/t_{\max}$。函数原型如下：

| 解决方案源代码 |
|---|
| DIR: c-programming<br>FILE(S):<br>integration.c |

```
```c
/******************** integrate() ***********************/
/** Integrates a 1-dim function numerically using **/
/** the trapezoidal rule **/
/** PARAMETERS: (*)= return-parameter **/
/**    from: startpoint of interval **/
/**      to: endpoint of interval **/
/** num_steps: number of integration steps **/
/**      f: p. to function to be integrated **/
/** RETURNS: **/
/**    value of integral **/
/*******************************************************/
double integrate(double from, double to, int num_steps,
                 double (* f)(double))
```
```

在 `main()` 函数中测试该函数：对 `math.h` 中定义的 `sin()` 函数在不同区间上积分，例如 $[0, \pi/2]$、$[0, \pi]$。

### (7) **通过编译器优化代码**

获取程序 `optimization.c`，它针对一组数字，计算所有可能子集的数字之和。其耗时随数字个数呈指数增长，因此是观察编译器优化效果的良好测试平台。

| 获取源代码 |
|---|
| DIR: c-programming<br>FILE(S):<br>optimization.c |

通过 `cc -o optimization optimization.c -lm -Ox` 编译程序，其中 x 为 0、1、2 和 3。使用 `time optimization` 测量执行编译后程序的运行时间（请注意，标准版本的程序不会打印任何内容）。

源代码文件之间的依赖关系。此外，它还包含生成结果文件（称为目标，即最终程序和/或目标（.o）文件）的命令（例如编译器命令）。每一对依赖关系和命令称为*规则*。包含项目所有规则的文件称为*makefile*，通常命名为 **Makefile**，并且应放置在存储源文件的目录中。

一条规则可以按如下形式用两行编码

```
    (target) : (sources)
    <tab> (command(s))
```

第一行包含依赖关系，第二行包含命令。命令行必须以制表符 `<tab>` 开头，它在大多数编辑器中显示为一个空格。允许有多个目标依赖于相同的源文件。你可以在每行末尾使用反斜杠“\\”来扩展行。命令行可以留空。一个依赖/命令对的示例如下：

```
    simulation.o: simulation.c simulation.h
    <tab>   cc -c simulation.c
```

这意味着，如果 `simulation.c` 或 `simulation.h` 中任一文件发生了更改，就必须编译文件 `simulation.o`。在 UNIX shell 的命令行中输入 `make` 即可调用 `make` 程序。它利用每个文件随文件一起存储的最后修改日期和时间，来判断是否需要重新构建某些目标。每当至少一个源文件比相应的目标文件更新时，就会执行 `<tab>` 之后给出的命令。具体来说，如果目标文件根本不存在，也会执行该命令。在这种特殊情况下，规则第一行中冒号之后不必给出任何源文件。

也可以生成元规则，例如告诉如何处理所有具有特定后缀的文件。标准规则（例如告诉如何处理以 `.c` 结尾的文件）已经存在，但可以通过为每个文件声明不同的规则来更改。这个主题在 `make` 的手册页中有介绍。

`make` 工具总是只尝试构建 *makefile* 中的第一个目标，除非依赖关系强制要求构建其他目标。因此，如果你需要构建多个独立的目标文件 `object1`、`object2`、`object3`，整个编译过程必须由第一条规则触发，因此你的 *makefile* 应写成
