# C++ 入门指南与高级编程



![](img/cover01225.jpeg)







# 第 1 章 第一个程序

## 1.1 什么是程序？

实际上，每个人都早已熟悉程序了，但人们通常通过程序来理解不同的内容：
* 派对宣言 ↔ 想法
* 剧院节目 ↔ 进度安排
* 音乐谱 ↔ 严格的指令序列
* Windows 程序 ↔ 与计算机的交互操作

软件包含了上述列表中的所有四个方面。一个典型的练习是完成以下操作：

### 我应该做什么？

1. 纸上的想法。（应该做什么？）
2. 用编程语言描述想法。草拟。（计算机如何实现这个想法？）
3. 编辑源代码/源文件。（我使用哪些表达式？）
4. 编译并链接文件。（翻译成处理器语言）

结构图：
程序代码
使用不同的数据集测试程序。

1. . 编程中的学习过程通常按照上述概述从自底向上进行。
2.  软件 = 程序 + 代码 + 想法。

备注：我之前的意思完全不同。

## 1.2 C 语言中的“HELLO WORLD”程序

想法：一个只在屏幕上打印消息的最简单程序。
源代码 (`HelloWorld.c`)：

```c
/* 注释开始，结束 */
预定义函数/变量/常量
int main() {
    printf("Hello, World!\n");
    return 0;
}
```

输入、编译并执行程序：
0. 开启电脑，登录。

登录：
1. 打开终端或文件管理器并切换到工作目录。
`LINUX> cd progs`
2. 在你选择的编辑器中源文件中输入源文本。
`LINUX> edit HelloWorld.c`
`LINUX> emacs HelloWorld.c`
3. 编译源文件。
`LINUX> gcc HelloWorld.c`
4. 执行程序。
`LINUX> a.out` 或 `LINUX> ./a.out` 或 `WIN> ./a.exe`

备注：生成的程序默认名为 `a.out`。如果指定名称（例如 `myprog`），应这样调用：
`LINUX> gcc -o myprog HelloWorld.c`
`LINUX> myprog`

在考虑编译器之前，先使用具体的命令行进行编译。

## 1.3 C++ 中的“Hello World”程序

想法和结构图同 1.2 节，源代码 (`HelloWorld.cc`)：

```cpp
#include <iostream>
/* 行内注释 */
int main() {
    std::cout << "Hello, World!" << std::endl;
    return 0;
}
```

预定义类和方法
主程序的开始
简单指令
块语句

编译、执行程序：
0. 同 1.2 节所示。
2. 编辑源文件。
`LINUX> edit HelloWorld.cc`
3. 编译源文件。
`LINUX> g++ HelloWorld.cc`
4. 执行程序。`LINUX> a.out` 或 `LINUX> ./a.out` 或 `WIN> ./a.exe`

备注：`HelloWorld.c` 的源代码也可以用 C++ 编写并替换为：
`LINUX> g++ HelloWorld.c`

然而，此时源代码行 `#include <stdio.h>` 是绝对必要的。
* C 指令是 C++ 指令的子集。
* C 注释 `/**/` 也可以在 C++ 中使用。
* C++ 注释 `//` 属于 C++ 语法，因此不应在 C 程序中使用。否则会导致移植性问题，即不是每个 C 编译器都能编译该源代码。

编程提示：（几乎）总是“正确的意味着”一个对等，因为一个想法旨在由计算机程序来实现。
==> 找到你自己的编程风格（并改进它）。

## 1.4 编程时的内部细节

## 1.4 编程时的内部细节

方便更改每次编译的调用：
`LINUX> g++ -v HelloWorld.cc`

生成的较长屏幕输出显示了编译的几个阶段。以下是关于如何查看每个阶段以更好地理解过程的提示：

a) 预处理：
头文件 (`*.hh` 和 `*.h`）被添加到源文件中（加上宏定义、条件编译）。
`LINUX> g++ -E HelloWorld.cc > HelloWorld.ii`
添加 `> HelloWorld.ii` 将屏幕输出重定向到 `HelloWorld.ii` 文件。可以使用编辑器查看此 `HelloWorld.ii` 文件，它是一个长的 C++ 源文件。

b) 生成汇编代码：
在这里生成了（特定处理器的）编程语言的源文本文件。
`LINUX> g++ -S HelloWorld.cc`
生成的 `HelloWorld.s` 文件可以使用编辑器查看。

c) 生成目标代码：
现在创建了一个包含处理器的直接控制命令（即数字）的文件。
`LINUX> g++ -c HelloWorld.cc`
文件 `HelloWorld.o` 无法在普通文本编辑器中查看，但可以使用：
`LINUX> hex HelloWorld.o`

d) 链接：
将所有目标文件和执行所需的库绑定，合并成执行程序 `a.out`。
`LINUX> g++ HelloWorld.o`

## 1.5 讲座中的符号

LINUX 下命令行中的命令：
`LINUX> g++ [-o myprog] filename.cc`

方括号 `[ ]` 标记命令或定义中的可选部分。每个文件名由可选的基础名称（文件名）和标识文件类型的后缀（`.cc`）组成。

• 后缀后的某些文件类型：后缀文件类型
* Cc 源文件
* `.H` 头文件（也用于 C++），带有预定义程序模块的源文件
* `.cc[.cpp]` C++ 源文件
* `.hh[.hpp]` C++ 头文件
* `.O` 目标文件

语句 `<type>` 意味着该占位符必须被相应类型的表达式替换。

# 8 数据类型类

## 8.1 类定义数据和方法
## 8.2 构造函数
## 8.3 析构函数
## 8.4 赋值运算符
## 8.5 打印运算符
## 8.6 数据封装

# 9 文件输入与输出

## 9.1 复制文件
## 9.2 通过文件进行数据输入输出
## 9.3 切换输入输出

# 10 输出格式

# 11 技巧

## 11.1 处理器命令
## 11.2 程序内计时
## 11.3 性能分析
## 11.4 调试

# 7.8 蛋大更大示例：二分法 86





自从此脚本的第一个版本以来，较新版本的头文件已与旧的头文件一起提供，例如用 `iostream` 代替 `iostream.h`。在某些情况下，像 `g++` 这样的编译器在编译第 4 页的源代码时会产生烦人的多行警告。可以使用 `LINUX> g++ -Wno-deprecated HelloWorld.cc` 删除此错误信息。

![](img/image00844.jpeg)!(Images/image00845.jpeg)右（推荐）使用新的头文件，请自己修改我们的小程序：

![](img/image00846.jpeg)

![](img/image00847.jpeg)我想要作用域运算符不需要每次都写，因此我倾向于这种写法：

![](img/image00848.jpeg)

# 第 2 章：简单数据类型

## 2.1 变量

### 2.1.1 变量定义

每个有意义的程序都会以某种形式数据。这些数据存储在变量中。

i) 变量是数据存储空间的符号表示（标识符/名称）。
ii) 它由类型和存储类描述。
iii) 变量的内容（即内存空间中的数据）在程序执行期间会发生。

变量声明的通用形式：

```
[< storage class >] <type> <identifier1> [, identifier2] ;
```

| 类型 | 内存（字节 (g++)） | 内容 |
| :--- | :--- | :--- |
| ![](img/image00849.jpeg) | | |
| ![](img/image00850.jpeg) | | |
| char | 1 | 字符符号 'H', 'e', 'n' |
| boolean | 1 | 布尔型变量 false, true [仅限 C++] |
| ![](img/image00851.jpeg)!(Images/image00852.jpeg) | 4 | -32768 到 32767 |
| short [int] | 2 | 整数 -32768 到 32767 |
| long [int] | 4 | -32768 到 32767 |
| float | 4 | 浮点数 1.1, -1.56e-32 |
| double | 8 | 1.1, -1.56e-32, 5.68e+287 |
| ![](img/image00851.jpeg)!(Images/image00854.jpeg) | unsigned [int] | 4 | 常用数字 0 到 32767 |
| ![](img/image00855.jpeg) | long long [int] | 8 | 整数 -2³¹ 到 2³¹ |
| long double | 12 | 浮点数 5.68e+287, 5.68e+420 |

备注：
- 字符数据恰好存储一个 ASCII 或特殊字符。
- ![](img/image00856.jpeg)!(Images/image00857.jpeg)整数组类型（`int`）的内存需求可能取决于编译器和操作系统（16/32 位）。因此，建议阅读相关的编译器指令，或使用 `sizeof` 运算符通过 `sizeof( <type> )` 或 `sizeof( <variable> )` 确定所需的实际字节数。参见以下示例：

![](img/image00858.jpeg)

![](img/image00859.jpeg)我们通常使用基本类型 `int` 用于适当的整数子范围，使用 `unsigned int` 用于常用数字。`unsigned` 标记也可以用于其他整数类型。

### 2.1.2 变量的命名

![](img/image00860.jpeg)!(Images/image00861.jpeg)!(Images/image00862.jpeg)变量名以字母或下划线开头，后续字符也可以是数字。名称中不允许使用空格和运算符字符 `()`，变量名也不允许是 C++ 语法的关键字（参见附录）。

![](img/image00840.jpeg)!(Images/image00863.jpeg)!(Images/image00840.jpeg)!(Images/image00864.jpeg)C/C++ 是区分大小敏感的，即 `totalHosen` 和 `toteHosen` 是不同的标识符！

![](img/image00865.jpeg)根据原始 C 标准，变量标识符的前 8 个字符是有效的，即 `a2345678A` 和 `a2345678B` 不再被视为不同的标识符。编译器现在认为更多字符是有效的（C99 标准：63 个字符）。

## 2.2 常量

大多数程序（包括 `HelloWorld.cc`）在程序过程中都会使用不可改变的值，所谓的常量。

### 2.2.1 整数常量

十进制常量（基 10）：
- `100 // int; 100`
- `512L // long; 512`
- `128053 // long; 128053`

八进制常量（基 8）：
- `020 // int; 16`
- `01000L // long; 512`
- `0177 // int; 127`

十六进制常量（基 16）：
- `0x5 // int; 5`
- `0x200 // long; 512`
- `0xffff // int; 65535`

### 2.2.2 浮点常量

浮点常量总是被解释为 `double`。例如：

| 常量 | 值 |
| :--- | :--- |
| 10E | 10000 |
| 1. | 1 |
| .78 | 0.78 |
| 2e-3 | 0.002 |
| -3.25 | -3.25 |

### 2.2.3 字符常量

字符常量包含：

| 字符 | 描述 |
| :--- | :--- |
| 'a' | 字符 |
| ' ' | 空格 |
| '_' | 下划线 |
| '\n' | 换行 |

### 2.2.4 字符串常量

字符串常量：

| 字符串 | 描述 |
| :--- | :--- |
| "Hello World" | 字符串 |
| "" | 空字符串 |

### 2.2.5 宏常量

在预处理器中，`define` 替换标识符：

```
#define N 5
```

### 2.2.6 使用 `const` 声明常量

在代码中使用 `const` 标记，例如：

```
const int N = 5;
```

# 第 3 章：表达式、运算符与函数

- 表达式由操作数和运算符组成。
- 变量、常量或表达式。
- 运算符对操作数执行操作。

## 3.1 赋值运算符

赋值运算符 `<operand_A> = <operand_B>` 将右操作数赋值给左操作数，后者必须是变量。

例如，在语句序列中：

```
x = 0
y = x + 4
```
`x` 的值为 0，`y` 的值为 4。其中 `x+4` 是一个由操作数 `x`, `4` 和运算符 `+` 组成的表达式。`x = 0` 和 `y = x + 4` 都是表达式。首先分号 `;` 将这些表达式转换为语句。

也可以多次赋值：

```cpp
x = 1
x = 2
```

## 3.2 算术运算符

### 3.2.1 一元运算符

一元运算符只有一个操作数。

| 运算符 | 描述 | 示例 |
| :--- | :--- | :--- |
| - | 取反 | -a |

### 3.2.2 二元运算符

二元运算符有两个操作数。操作的结果取决于运算符。

| 运算符 | 描述 | 示例 |
| :--- | :--- | :--- |
| `+` | 加法 | `b + a` |
| `-` | 减法 | `b - a` |
| `*` | 乘法 | `b * a` |
| `/` | 除法（整数） | `b/a` |
| `%` | 整数除法的余数 | `b % a` |

整数整数计算的是除法的整数部分，即 `8 / 3` 返回结果 `2`。然而，如果结果是 `2.666666`，则必须将至少一个运算符转换为浮点数，如示例所示。

### 3.3 比较运算符 15





![](img/image00879.jpeg)!(Images/image00880.jpeg) 关于优先级规则，如果文献证明你过时了，运算符的顺序可能会出错。“先点计算后减法计算”的规则在 C/C++ 中同样适用。类似于学校里的圆括号表达式 `(<expression>)` 先计算。

## 3.3 比较运算符

比较运算符是二元运算符。结果值始终是一个整数值，其中 `FALSE` 返回 `0`，`TRUE` 返回非零。

|  | 说明 | 示例 |
| :--- | :--- | :--- |
| `>` | 大于 | `b > a` |
| `>=` | 大于等于 | `b >= 3.14` |
| `<` | 小于 | `a < b / 3` |
| `<=` 小于等于 | `b * a <= c` |
| `==` | 等于（浮点数请注意！） | `a == b` |
| `!=` | 不等于（浮点数请注意！） | `a != 3.14` |

![](img/image00881.jpeg)

一种典型的错误发生在使用 `=` 而不是相等运算符 `==` 测试相等性时。这里写的是赋值运算符 `=`。编译器接受这两种源代码（取决于编译器），如果代码是错误的，可能会发出警告。

![](img/image00882.jpeg)

在错误的代码中触发了未知的副作用，测试中变量 `i` 没有正确的写法，因此我们使用 `i = i`。即下文所示，正确的代码没有副作用的。

![](img/image00883.jpeg)

## 3.4 逻辑运算符

## 3.4 逻辑运算符

现在将 `!` 和 `&&` 视为逻辑运算符：

| 运算符 | 说明 | 示例 |
| :--- | :--- | :--- |
| `!` | 逻辑非 | `!(3>4)` // `TRUE` |

### 二元逻辑运算符：

| 运算符 | 说明 | 示例 |
| :--- | :--- | :--- |
| `&&` | 逻辑与 | `(3>4) && (3<=4)` // `FALSE` |
| `||` | 逻辑或 | `(3>4) || (3<=4)` // `TRUE` |

![](img/image00884.jpeg) 逻辑与和逻辑或的真值表在代数中已知（否则请参见文献）。

![](img/image00885.jpeg)

## 3.5 位运算符

位是最小的信息单位，恰好有两种可能的状态：

![](img/image00886.jpeg) 位设置：
```
≡ (0)
≡ (1)
```
![](img/image00887.jpeg)  真

![](img/image00888.jpeg)!(Images/image00889.jpeg) 一个字节由 8 位组成，因此一个 `short int` 数字的长度为 16 位。位操作中的运算符通常出现在整数表达式中。

### 3.5.1 一元位运算符

![](img/image00890.jpeg)
| 运算符 | 说明 | 示例 |
| :--- | :--- | :--- |
| `~` | 二进制补码，操作数的按位取反 | `~k` |

### 3.5.2 二元位运算符

![](img/image00891.jpeg)
| 运算符 | 说明 | 示例 |
| :--- | :--- | :--- |
| `&` | 按位与操作数 | `k & l` |
| `\|` | 按位或 | `k \| l` |
| `^` | 按位异或 | `k ^ l` |
| `<<` | 将 `<op1>` 向左移 `<op2>` 位 | `op1 << op2` |
| `>>` | 将 `<op1>` 向右移 `<op2>` 位 | `op1 >> op2` |

```
k << 2 // = k*4
k >> 2 // = k/4
```

| 真值表: x | y | x & y | x \| y | x ^ y |
| :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | 0 | 0 | 0 |
| 0 | L | 0 | L | L |
| L | 0 | 0 | L | L |
| L | L | L | L | 0 |

![](img/image00892.jpeg) 这些运算符在以下示例中演示：

```
l = 5; // 0..000101 = 5
k = 6; // 0..000110 = 6
```
![](img/image00893.jpeg) 位操作在测试一个整数是偶数还是奇数时非常有用。最低位可以配合整数区分奇偶数（参见上述代码中数字 `5` 和 `6` 的位表示）。因此，如果此位与一个设置位进行或运算，对于奇数，最低位将保持不变。这在下面的代码中被利用。

![](img/image00894.jpeg)!(Images/image00895.jpeg)

## 3.6 与预定义函数的操作

### 3.6.1 数学函数

头文件 `math.h` 包含了表 3.1 总结的数学函数和常量。实数 `x` 的舍入可以通过 `ceil(x+0.5)` 实现（忽略 4.5 的舍入规则）。

| 函数/常量 | 说明 |
| :--- | :--- |
| `sqrt(x)` | 平方 (`x > 0`) |
| `exp(x)` | $e^x$ |
| `log(x)` | 自然对数 (`x > 0`) |
| `pow(x,y)` | 幂 ($x^y$ 如果 $y$ 不是整数) |
| `fabs(x)` | $x$ 的绝对值 |
| `fmod(x,y)` | $x/y$ 的实数余数 (`y = 0`) |
| `ceil(x)` | 向上取整 |
| `floor(x)` | 向下取整 |
| `sin(x)`, `cos(x)`, `tan(x)` | 三角函数 |
| `asin(x)`, `acos(x)` | 反三角函数 ($x$ 在 [-1, 1] 之间) |
| `atan(x)` | 反三角函数 |
| `M_E` | 欧拉数 $e$ |
| `M_PI` | $\pi$ |

表 3.1: 数学函数
![](img/image00904.jpeg) 允许程序员负责参数范围。`math.h` 中的函数存储在特殊的数学库中，因此编译和链接命令必须考虑该库 `m`，即：

```
g++ 361.cc -lm
```

### 3.6.2 字符串函数

![](img/image00906.jpeg) 头文件 `string.h` 包含了以下字符串定义：

| 函数 | 说明 |
| :--- | :--- |
| `strcat(s1,s2)` | 在 `s1` 后附加 `s2` |
| `strcmp(s1,s2)` | 字符串 `s1` 和 `s2` 的字典比较 |
| `strcpy(s1,s2)` | 将 `s2` 拷贝到 `s1` |
| `strlen(s)` | 字符串 `s` 的字符数 (`sizeof(s1)-1`) |
| `strchr(s,c)` | 在字符串 `s` 中查找字符 `c` |

表 3.2: 经典函数
![](img/image00908.jpeg) 这些函数（以及其他）细节可以通过以下方式获取：

```
man string
man strcmp
```

## 3.7 增减运算符

### 3.7.1 前置符号

![](img/image00909.jpeg)!(Images/image00910.jpeg)

### 3.7.2 后置符号

![](img/image00911.jpeg)!(Images/image00912.jpeg) 后置符号主要用于循环中的索引变量（§ 4）。

## 3.8 复合赋值

赋值的形式为：

```
<lvalue> = <lvalue> <operator> <expression>
```
变为：
```
<lvalue> <operator>= <expression>
```
这里 `<operator>` $\in$ $\{+,-*,%,&|,^,<<,>>\}$ 来自 § 3.2 和 § 3.5。

## 3.9 其他有用常量

![](img/image00913.jpeg)

## 3.9 附加常量

系统相关的数值范围等，选择以下常量非常有帮助：

| 函数 | 说明 |
| :--- | :--- |
| `FLT_DIG` | `float` 的有效数字位数 |
| `FLT_MIN` | 最小的可表示正数 |
| `FLT_MAX` | 最大的可表示正数 |
| `FLT_EPSILON` | 使 `1.0 + ε = 1.0` 的最小正数 |
| `DBL_DIG` | `double` |
| `LDBL_DIG` | `long doubles` |

表 3.3: `float.h` 的一些常量
![](img/image00916.jpeg)
| 函数 | 说明 |
| :--- | :--- |
| `INT_MIN` | 最小的可表示整数 |
| `INT_MAX` | 最大的可表示正整数 |
| `SHRT_DIG` | `short int` |
| `LONG_DIG` | `long int` |
| `LLONG_DIG` | `long long int` |

表 3.4: `limits.h` 的一些常量
在 Linux 发行版中可以直接在文件 `/usr/lib/gcc-lib/i686-pc-linux-gnu/3.2.3/include/float.h` 和 `/usr/include/limits.h` 下检查更多常量。相应的头文件也可以用命令搜索：

```
find /usr -name float.h -print
```

# 第 4 章：控制结构

## 4.1 简单语句

简单语句由表达式和语句末尾的分号组成：

```
<expression> ;
```
示例：
```
cout << "Hello World" << endl;
i = 1 ;
```

## 4.2 块

块（也称为复合语句）是使用大括号对声明和语句的总结：

```
{
<statement_1>
...
<statement_n>
}
```
![](img/image00917.jpeg)




![](img/image00918.gif)

![](img/image00919.jpeg)在 C 语言中，声明部分必须紧随块的开头。在 C++ 中，你可以允许代码块存在多个部分，它们必须位于变量名相应的首次使用之前。然而，为了程序的清晰性，不应过度利用这一特性。

- 块末尾的右括号 `}` 后面不需要加分号。
- 块可以用来替代语句。
- 块之间可以相互嵌套。

![](img/image00920.jpeg)![](img/image00921.jpeg)在块中声明的变量在该块内可见，即该变量在块外部不存在（局部性）。相反，可以访问上级块的变量。

![](img/image00922.jpeg)

## 4.3 分支

分支（也称为备选）的标准形式为：

```c++
if ( <logical expression> )
    <statement_A> 
else
    <statement_B>
```

例如，每次选择都会依次应用。`else` 分支可以被忽略（简单备选）。

结构图：

![](img/image00923.gif)

正如常见的情况一样，具体问题可以通过多种方式进行编程。

![](img/image00924.jpeg)示例：我们考虑海维德函数（Heaviside function）的计算：

```c++
y(x) = 1 if x ≥ 0
     = 0 if x < 0
```

![](img/image00925.jpeg)并给出四种实现变体。

![](img/image00926.jpeg)

选项 A：简单备选

![](img/image00927.jpeg)

变体 b：双分支

![](img/image00928.jpeg)

变体 c：带有阻塞的双备选

![](img/image00929.jpeg)

变体 d：决策运算符。

在双分支中，如果每个分支只对同一个变量进行一次赋值（如版本 b 和 c 所示），可以使用决策运算符：

```c++
<logical expression> ? <expression A> : <expression B>
```

![](img/image00840.jpeg)![](img/image00840.jpeg)示例：另一个示例是符号函数（signum function）的计算：

![](img/image00931.jpeg)
```c++
y(x) = 1 if x > 0
     = 0 if x = 0
     = -1 if x < 0
```

![](img/image00932.gif)![](img/image00933.jpeg)我们提供了几种实现变体。结构图：

我们考虑两种实现变体，框架程序与第 28 页上的框架程序相同。

![](img/image00934.jpeg)选项 A：备选嵌套

变体 b：else 分支现在使用一个 if-else 语句，变体 a 可以稍微修改。

![](img/image00935.jpeg)

通常情况下，这种多路径决策可以写作：

```c++
if ( <logical expression_1> )
    <statement_1>
else if ( <logical expression_2> )
    <instruction_2>
    ...
else if ( <logical expression_(n-1)> )
    <statement_(n-1)> 
else
    <statement_n>
```

其中 `else` 分支是可选的。

![](img/image00936.jpeg)示例：确定输入的两个数的最小值和最大值。

结构图：

![](img/image00937.gif)

![](img/image00938.jpeg)

![](img/image00939.jpeg)示例：确定输入的三个数中的最小值。结构图：

![](img/image00940.gif)

![](img/image00941.jpeg)

## 4.4 计数循环 (for 循环)

计数循环代表预先确定的循环次数，在运行循环之前进行测试。其通用形式为：

```c++
for (<expression_1>; <expression_2>; <expression_3>)
    <statement>
```

最好的示例是将计数循环作为允许的输入。

![](img/image00942.jpeg)示例：计算 计算前 5 个自然数的和。

![](img/image00943.jpeg)在上面的程序示例中，`i` 是循环的运行变量，初始化为 `i = 1` (`<expression_1>`)，通过 `i = i+1` (`<expression_3>`) 继续。测试 `i <= n` (`<expression_2>`) 关于循环容量的上限。在循环内部，`sum = sum + i;`（语句）是循环的实际计算步骤。求和变量 `sum` 必须在进入循环之前初始化。

该求和循环的紧凑版本（正确但非常难以读）为：

```c++
for (sum = 0, i = 1; i <= n; sum += i, i++)
```

语句结束符 `;` 与表达式列表中的分隔符 `,` 之间进行了区分。这些列表从左到右处理。

![](img/image00944.jpeg)`<expression_2>` 始终是一个逻辑表达式，`<expression_3>` 是操作运行变量的算术表达式，例如：

```c++
i++
j = d-2; d += 2
x = x+h // float 类型
k = 2*k // 翻倍
l = l/4 // 四分之一 - 注意整数
```

结构图：

![](img/image00945.gif)

控制变量可以是简单变量，例如 `int` 或 `double`。

![](img/image00946.jpeg)

![](img/image00844.jpeg)![](img/image00947.jpeg)![](img/image00948.jpeg)在使用浮点数 (`float`, `double`) 作为变量时要小心。由于内部数字表示，正确的终止测试可能不容易实现。

结构图：

![](img/image00949.gif)示例：这是一个双倍和。

![](img/image00950.jpeg)n![](img/image00951.jpeg)
```c++
sum = 1
i = 2
k = 1
```

![](img/image00952.jpeg)
```c++
k = 1
i = 1
```

![](img/image00953.jpeg)![](img/image00954.jpeg)求和变量 `sum` 必须在进入循环之前初始化。

![](img/image00955.jpeg)后续示例说明了浮点数的问题以及关于它们的一些提示。

![](img/image00956.jpeg)示例：区间 `[0, 1` 的离散节点输出。

## 4.6 非拒绝循环 (do-while 循环)



非拒绝循环（non-rejecting cycle）是指不预先固定执行次数，其终止测试在循环执行后进行。因此，非拒绝循环至少执行一次循环内部的指令。

通用形式为

```markdown
of the 

<statement>

while (<logical expression>) ;
```

![](img/image00976.gif) 结构图 (Structogram):

![](img/image00977.jpeg) 

**示例：** 从键盘读取字符，直到输入 `x` 为止。

![](img/image00978.jpeg)

考虑一个更有挑战性的例子，即从 `sin(x) = x/2` 中确定 `x \in (0, π)` 的根。对于这个问题，你需要考虑等效零问题：确定以下函数的零点 `x0 \in (0, π)`

![](img/image00979.jpeg)
函数 `f(x) := sin(x)x/2 = 0` 。

**分析法：** 没有实际的解。

**图形法：** 绘制函数 `f(x)` 并手动缩小（减半）低分辨率区间。重复此过程，直到 `x0` 可以被足够精确地确定，即达到预定的位数。

![](img/image00980.jpeg) ![](img/image00981.jpeg) `f(x) =sin(x)-x/20.25`

![](img/image00982.jpeg) 0.2
0
–0.2
0.3
0.2
0.2
0.15
–0.4
0.1
–0.6
–0.8
0.1
0.05
-1
02
–1.202
–1.4
–0.05
–1.6

**数值法：** 上述图形过程可以应用于纯数值计算。具有计算机经验的并可以使用正确的 MAPLE - 

![](img/image00983.jpeg) ![](img/image00984.jpeg) ![](img/image00985.jpeg) 调用 `ffsolve(sin(x)=x/2,x=0.1..3)` 返回近似结果 `x0 = 1.895494267` 。我们正在开发一个程序，通过二分法确定区间 `[a, b]` 内 `f (x) := sin(x) x/2` 的零点，为了简化，假设 `f(a) > 0` 且 `f(b) < 0`。区间的中点标记为 `c := (a + b)/2`。然后我们如下所示：

```markdown
x0 \in [c, b] if f (c) > 0
```

![](img/image00986.jpeg) ![](img/image00987.jpeg) 
```markdown
{x0 \in [a, c] iff f(c) < 0
```

![](img/image00988.jpeg) 通过重新定义区间边界 `a` 和 `b`，可以将零搜索缩小到更小的（减半的）区间。我们使用非拒绝循环演示其实现。

**结构图：**

![](img/image00989.gif)

上述二分法也可以通过拒绝循环（rejecting cycle）来实现。

![](img/image00990.gif)

![](img/image00991.jpeg)

由于浮点数的精度有限，中止测试 `f(c) = 0` 通常会导致程序无限循环。因此，使用给定精度 `0 < ε < 1` 的中断测试如 `|f(c)| < ε` 更好。

![](img/image00992.jpeg) 例如：在冷却循环 `(for)` 后面至少执行一次循环直到结束，以及通过不同的结束 `(while)`，这与非拒绝循环 `(do while)` 是等价的。这些等价的示例可以在 4.8 的正确应用中使用。如果冷却循环中始终结果为 `FALSE`（即在循环中没有执行循环体），那么在不同的结束循环中，之前之后是等价的。然而如果结束循环不再等价，那么在这种情况下循环也会被处理一次。参见示例文件 `Loops.cc`。

## 4.7 多路选择 (switch 语句)

额外的选择功能允许个人根据特定变量的值做出反应。

```markdown
switch (<expression>)
{
    case <const_expression_1>:
        <statement_1> [break;]
    ...
    case <const_expression_n> :
        <statement_n> [break;]
    default:
        <statement_default;
}
```

![](img/image00994.jpeg) ![](img/image00995.jpeg) **示例：** 输出整数输入 `{1, 2, 3}`。

上面的 `switch` 语句也可以用于多路分支（由于这个），但在 `switch` 语句中，各个分支是显式的，并且通过 `break;` 语句离开。如果没有 `break;`，

## 4.8 无条件控制转移

无条件的控制转移允许你跳转到程序的其他部分。使用 `goto` 语句来实现此，但通常不建议使用。



1[`www.ee.surrey.ac.uk/Personal/R.Knott/Fib onacci/fibFormula.html`](http://www.ee.surrey.ac.uk/Personal/R.Knott/Fibonacci/fibFormula.html)

![](img/image01022.jpeg)另一个例子，需要确定向量的最小值和最大值，并交换对应的向量元素（类似于主元选择）。这包括两个子任务：

a) 确定最小和值（并标记位置）。结构图：

![](img/image01023.gif)

b) `VexchangeMin/Max Entryage`。在 `Vectorlange0` 或 `identicalNo` 时，向量元素不需要交换。

![](img/image01024.gif)结构图：

在 `Vexchange` 处

显而易见的第一个想法 `x[kmin] = x[kmax]` `x[kmax] = x[kmin]` 

并没有成功。为什么？

![](img/image01025.jpeg)

## 5.1.2 多维字段

到目前为止考虑的 1D 文件夹是彼此存储的（线性内存模型），例如，行向量

如下

`x0x1x2x3x4`

![](img/image01026.jpeg) `double x[5];`

被约定并保存为

| x0 | x1 | x2 | x3 | x4 |

其中每个单元长度为 8 字节。

![](img/image01027.jpeg)二维（静态）数组，例如，具有 `N = 4` 行 `M = 3` 列的矩阵 `A`

![](img/image01028.jpeg)`A00A01A02A10A11A12`

`AN×MA20A21A22`

`A30A31A32`

![](img/image01029.jpeg)![](img/image01029.jpeg)![](img/image01029.jpeg) 也可以只能线性地存储在内存中，即：

| A00 | A01 | A02 | A10 | A11 | A12 | A20 | A21 | A22 | A30 | A31 | A32 |

![](img/image01030.jpeg)这为 2D 字段声明提供了两种方案：方案 1：作为二维数组。

```c
doubleA[N][M]; // 声明
A[3][1] =5.0;// 初始化 A(3,1)
```

![](img/image01031.jpeg)方案 2：作为 1D 数组。

```c
doubleA[N*M]; // 声明 
A[3*M+1] =5.0;// 初始化 A(3,1)
```

示例：作为一个例子，我们考虑具有 `N = 4` 行和 `M = 3` 列的矩阵 `AN×M` 与长度为 `M` 的行向量 `uM` 的乘法。结果是一个长度为 `N` 的行向量 `f`，即：

![](img/image01032.jpeg)![](img/image01033.jpeg)`f:=AN×M uM` 。`f = [f0, f1, . . . , fN−1]T` 的分量计算为

`M−1`

![](img/image01034.jpeg)be :=hey,j · andj∀i =0, . . . , N − 1. . 

`j=0` 高维文件夹可以类似于方案 1 进行声明和使用。在方案 2 中，`double B[L,N,M];` 使用 `B[i*M*N+j*M+k]` 进行访问。



## 5.2 结构体结构体定义了一种组合不同类型组件的新数据类型。类型声明

```c
struct <struct_identifier>
{
<data declaration>
};
```

允许声明此类类型的变量

`<struct_identifier> <var_identifier>;`

![](img/image01035.jpeg)![](img/image01036.jpeg)示例：我们定义了一种类型来存储学生的个人信息。

赋值 `robbi = arni;` 将完整数据集从一个变量拷贝到另一个。变量 `arni`（类型为 `Student`）的组件 `firstname` 通过 `arni.firstname` 访问。

数据以如下形式保存

| matriculation | sketch | Surname | First name |

在编译器设置或 -选项之前，组件之间会有较小的未使用存储空间（执行数据对齐以获得更快的数据访问）。

![](img/image01037.jpeg)student 结构可以很容易扩展以包含有多个专业的学生。

![](img/image01038.jpeg)

![](img/image01039.jpeg)

![](img/image01040.jpeg)![](img/image01041.jpeg)student 结构已经包含了字段作为组件。另一方面，数据类型可以进一步排列成字段。

![](img/image01042.jpeg)在上面的例子中，`p` 是一个 `3D` 类型的变量，可以访问。



## 5.3 联合体联合体的所有组件共享相同的存储区域。声明

```c
union <union_identifier>
{
<data declaration>
};
```

允许声明此类类型的变量

`union <union_identifier> <var_identifier>;`





![](img/image01064.jpeg)结果，因此设置了表达式¨ckef[1]`，*(f+1)`，*(pint+1)`，

![](img/image01065.jpeg)`pint[1]` 表示对数组元素 `f1` 的相同访问。

|  | f0 |  | f1 |  |

![](img/image01066.jpeg)`pint`

![](img/image01067.jpeg)由 `(pint+1)` 表示的地址将导致 `(pint 中的地址) + sizeof(int)`。在这种情况下，`int` 指定了 `Pointer`（指针）针所指向的数据类型。访问其他数组元素 `fi`（`i = 0 . . . N 1`）也是类似的。

以下运算符适用于指针：

- 比较操作符：`==`, `!=`, `<`, `>`, `<=`, `>=`
- 加法 `+` 和减法 `-`

![](img/image01068.jpeg)自增`++`，自减`--` 以及复合运算符 `+=`, `-=`

![](img/image01069.jpeg)`![]`(Images/image01070.jpeg)`![]`(Images/image01071.jpeg)为了演示，我们考虑一个示例，在该示例中首先以传统方式定义并初始化数组，然后使用指针操作进行输出。

## 6.4 使用指针变量的动态数组

![](img/image01072.jpeg)到目前为止，一个指向已提供（已分配）内存的 fu¨ronessimple 变量，结构，字段。foot¨right。然而，指针也可以添加到类型 origrightSpoak 是一个动态 H。Mr. Jerez 和我们使用了新的结论¨sselnew`。通过这种方式分配的内存可以使用 `delete` 进行更改并再次释放。

![](img/image01073.jpeg)

语句 `px = new double[n];` 为指针 `px` 分配了 `n*sizeof(double)` 字节。动态字段 `px` 的处理方式与静态字段相同。然而，动态字段可以更好地利用现有的存储空间，因为这些空间可以使用 `delete` 命令释放并再次用于其他用途。

![](img/image01074.jpeg)危险：上述动态字段声明仅对 fu¨rightC++有效。在 C 中使用了不同的命令 - 以下是区别。

![](img/image01075.jpeg)C++C

```cpp
#include <malloc.h>

px = newdouble[n];
px = (double*) malloc(n*sizeof(double)); delete []px; free(px);
```

![](img/image01076.jpeg)`![]`(Images/image01077.jpeg)例如，我们在一维动态字段之间 latet  himself  on the one handbyH  one  one-dimensional dynamic field（类似于 5.1.2 中的变体 2）以及通过指向指针字段的指针。对于一个具有 `n` 行 `m` 列的矩阵，它看起来如下：

![](img/image01078.jpeg)首先必须为行指针分配内存，然后才能请求单独行的内存。在释放内存时，必须再次释放所有行。对于 `n = 3` 和 `m = 4` 的情况，图显示了数据是如何存储在内存中的。

![](img/image01079.jpeg)`![]`(Images/image01080.jpeg)`![]`(Images/image01081.jpeg)`![]`(Images/image01082.jpeg)`![]`(Images/image01083.jpeg)...

注意：不能保证矩阵的各个行在内存中是连续排列。因此，动态二维数组的存储与静态二维数组的存储有所不同，尽管元素访问的语法 `b[i][j]` 是相同的。另一方面，这种矩阵存储更加灵活，因为行也可以具有不同的长度（稀疏矩阵或具有形状的矩阵）。

![](img/image01084.jpeg)`![]`(Images/image01085.jpeg)showrightknockouẗnenturn 出现在结构或通用类型中。然而，在使用动态字段时应该小心，因为否则 fu¨right 静态变量可能会导致不关键的操作 plomoreHtoto mirasulömprograminreceivewasearnknockoutcan 发生。

数据存储在在 (A)、(B) 和 (C) 时是什么样子的？

![](img/image01086.gif) 

- robbi 没有它自己的动态字段。

![](img/image01087.jpeg)`delete [] arni.pfirstname;`因此也释放了 `robbi.pfirstname` 指向的内存区域，因此 `robbi.pfirstname` 指向不再保留的内存区域，程序可以根据需要使用该区域。

![](img/image01088.jpeg)`tiny = new char[5];`taket himselfennfriibecomenSpoak placeU.Ni.eandbhe writesyn spa¨ter。

![](img/image01089.jpeg)在 LINUX-gcc 下，在 (C) 时 `robbi.pfirstname` 指向与指针 `tiny` 相同的地址，因此可以使用以下代码输出来自 `robbi.pfirstname` 的数据

```cpp
cout << robbi.pfirstname << endl;
```

输出 `tiny`。

![](img/image01090.jpeg)方式：

robbi 自己的动态字段被分配。robbi 的动态字段被复制到。

## 6.5 结构指针

![](img/image01092.jpeg)`![]`(Images/image01093.jpeg)我们考虑结构 `Student` 并定义指向它的指针。

## 6.6 引用

![](img/image01095.jpeg)

第 7 章

函数

## 7.1 函数定义和声明

函数的用途：

![](img/image01097.jpeg)早些部分将再次编写。为了使程序更易于管理和设计，程序的这部分作为函数编写一次，并在程序的其他部分使用其函数名调用。

![](img/image01099.jpeg)其他程序员提供的完成函数，类似于 3.6 中的 `pow(x,y)` 和 `strcmp(s1,s2)`。

函数定义的一般形式如下

```cpp
<storage class><type><function_name> (parameter_list)

{

<agreements>

<instructions>
}
```

`<type>` 指定返回值的类型。`<function_name>`和 `(parameter_list)`的组合唯一标识一个函数，因此被用作函数的签名。每个函数只需要定义一次。

区别在于函数声明

```cpp
<storage class><type><function_name> (parameter_list) ;
```

在每个源文件中调用函数 <function_name>。

71

7.2. 参数传递

(i) 在上面的示例中，允许有多个相同的函数声明

```cpp
double sgn(double x);
```

(ii) 带有其他参数列表的函数声明是允许的，例如：

```cpp
double sgn(double* x); double sgn(int x);
```



由于参数与初始定义不同。然而，我们尚未定义这些新函数。

(iii) `Ae togetheradditionedeclarationn`（见 § 7.2）

```cpp
double sgn(double& x);
```

这是不允许的，因为其签名与 (i) 一。因此，编译器无法确定语句中是 (iii) 的函数还是 (i) 的函数：

```cpp
y = sgn(x);
```

这意味着。

(iv) 同名的不同函数通过其不同的参数列表来识别，见项目 (iii)。

(v) 函数的 `derightRu¨cvalueof` 不能用于识别它，这些声明被收紧了：

```cpp
double sgn(int x); int sgn(int x);
```




![](img/image00863.jpeg)!(Images/image0126.jpeg)!(Images/image0127.jpeg) 还有定义的数据结构，例如来自 5.2 的 `Student` 和来自 6 的 `Student2` 以及头文件 `student.hh` 中的全局常量。

![](img/image01128.jpeg)

新函数 `Copy Student` 定义在 `student.cc` 中，该函数拷贝 `correct.cc` 中定义的内容。

![](img/image01129.jpeg)由于 `Student2` 结构被使用，头文件 `student.hh` 必须包含在 `student.cc` 中。新函数 `Copy Student` 现在可以在主程序 `Ex752.cc` 中拷贝结构。当然，主程序需要头文件 `student.hh`。

命令

```
LINUX> g++ Ex752.cc student.cc
```

最后创建程序 `a.out`。

### 7.5.3 使用库的简单示例

库被用于在链接时避免重复编译大量的源文件。同时，库的优势在于你可以将编译好的函数（连同头文件）以紧凑的形式提供给他人，而无需暴露你的编程秘密（知识产权）。这在 7.5.2 中演示。

*   生成目标文件 `student.o`（编译）

    ```
    LINUX> g++ -c student.cc
    ```

![](img/image01131.jpeg) 生成 `libstud.a`（归档）目标文件 `student.o`。库标识符 `stud`是可以自由选择的。

```
LINUX> ar r libstud.a student.o
```

归档选项（这里是 `r`）随编译器的不同而异。(Images/image01132.jpeg)!(Images/image01133.jpeg) 从当前目录编译并带上库链接主程序：

```
LINUX> g++ Ex752.cc -L. -lstud
```

不使用库编译和链接程序所需的步骤如下：

```
g++ -c student.cc
```

---

```
g++ -c Ex752.cc
student.o
```

---

![](img/image01135.jpeg) 另一种方式也是模块化的：(Images/image01136.jpeg)

```
Ex752.cc, student.cc
g++ Ex752.cc student.cc
```

使用 `libstud.a` 库时，过程如下：(Images/image01137.jpeg)

```
student.cc
g++ -c student.cc
g++ -c student.o
```

a-b 且例如。--> `libstud.a` (Images/image01138.jpeg)

```
g++ Ex752.o
```

![](img/image01139.jpeg)
```
Ex752.cc
Ex752.o
```
-L. -lstud 我们已经可以使用现有的库，例如：(Images/image01140.jpeg)

```
Ex752.cc, libstud.a
g++ Ex752.cc -L. -lstud
a.out
```

## 7.6 主程序

到为止用于主程序的语法：

```cpp
main()
{
    ...
}
```

始终被编译器使用，因为没有指定类型 `int` 的函数默认返回 `0`，表示主程序处理无。程序处理可以在任何时间停止，也可以在函数中使用指令 `exit(<int_value>)`。此时 `<int_value>` 是程序的返回值，可以用于诊断。(Images/image01141.jpeg)上述程序在 `n < 0` 时立即中断并返回错误代码 `1`。`exit` 语句也可以用于 `fun()`。与其他函数一样，主程序也可以带参数调用，但参数列表（更准确说是参数类型）规定如下：

```cpp
int main(int argc, char* argv[])
{
    ...
}
```

*   `argv[0]` 程序名
*   `argv[1] ... argv[argc-1]` 调用程序时的参数作为字符串
*   `argc` 始终 $\ge 1$，程序名始终

Images/image01142.jpeg)!(Images/image01143.jpeg) `atoi(char*)`（等于 ASCII 到 int）转换为整数，并在 `stdlib.h` 中声明。通过 `atoi(char*)` 让自己接受一个浮点数作为参数。编译链接后，可以启动程序 `a.out`：

```
LINUX> a.out
```

或

```
LINUX> a.out 5
```

在一种情况下，从键盘读取 `n` 的值；在另一种情况下，从命令行获取并赋值值 5。关于命令行参数传递的优雅且真实的 C++ 解决方案可以在 [Str, pp.126] 中找到。

## 7.7 递归函数

C/C++ 中的函数可以递归调用。示例要实现的幂：

```
xk = x * xk-1
```
 $x \in, k \in$ 也可以是 $k = 0$。

![](img/image01145.jpeg)!(Images/image01146.jpeg)!(Images/image01147.jpeg)

## 7.8 示例：二分法

第 39 页的示例是关于在区间 $(a,b)$ 内确定 $f(x) := \sin(x)$ 的零点，其中 $a = 0$ 且 $b = 1$。只要 $f(a) > 0 > f(b)$，该问题（对于连续函数）就可以使用二分法求解。二分算法本质上由以下区间 $[a, b]$ 的步骤组成：

(i) $c := (a + b)/2$
(ii) 如果 $|f(c)|$ 足够接近 0
(iii) 如果 $f(c) > 0$
    Bisect(c, b)
(iv) 否则
    Bisect(a, c)

这种递归结构图给出了 `Bisect()` 函数的定义，带参数调用：

```
x0 = Bisect(a, b, 1e-6);
```

这是第 1 版本的程序。





![](img/image01159.jpeg)![](img/image01160.jpeg)我们的程序可以顺利地运行 `f(x) = sin(x) x/2`，并根据输入参数 `a = 1` 和 `b = 2` 得正确解 `x0 = 1.89549`，`a = 0` 和 `b = 2` 也是如此。然而，这里没有找到（平凡的）解 `x0 = 0`，因为输入了 `a = 0`。当 `a = 0`, `b = 1` 或 `a = 1`, `b = 0.1` (`x0 := 0 [a, b]`) 时，程序运行一段时间后因段错误终止，因为递归没有停止，在某一点为函数调用预留的内存（栈）不再足够。

![](img/image01161.jpeg)现在我们采取保护保护程序，例如能够找到存在的 `x0 = 0` 以及 `[0, 1]`？关于函数值 `f(a)` 和 `f(b)`（假设 `a < b`）可能出现哪些情况？

(i) `f (a)>0 > f(b)`（即 `f(a) > 0` 且 `f(b) < 0`），例如 `a = 1`, `b = 2`

==⇒ `Bisect3()` 中的标准情况。

(ii) `f(a) > 0` 和 `f(b) > 0`，分别 `a = 0.5`, `b = 1.5`

![](img/image01162.jpeg)`f(a) < 0` 和 `f (b) < 0`，例如 `a=1`, `b= 0.5`

![](img/image01163.jpeg)可能都不为零。

（区间内可能存在零，我们用二分法找不到它们！）

![](img/image01164.jpeg)(iii)`f (a) = 0` 或 `f (b) = 0`，更好的是 `|f (a)| < ε` 等。

==⇒ `a` 或 `b` 是零点，`a` 和 `b` 都是零点。

(iv) `f(a) < 0 < f(b)`，例如 `a = −1`, `b = 0.1`

交换 `a` 和 `b`==⇒ 情况 (i)。

(v) `a =b`==⇒ 包含在 (ii) 和 (iii) 中。

`b < a`==⇒ 进入 (i) 或 (iv)。

![](img/image01165.jpeg)这种分类导致了下面的结构图和第 4 版本。

结构图 (Structogram):

![](img/image01166.gif)

![](img/image01167.jpeg)![](img/image01168.jpeg)最后我们在程序中定义了更多函数 `h(x) = 3 ex`, `t(x) = 1 x2`，询问用户使用哪种数学函数进行根，并计算区间内的根。这种选择可以通过 `switch` 语句轻松实现，并引导产生第 5 版本。

![](img/image01169.jpeg)注释：三个函数 `Bisect[1-3]()` 的参数列表不同。因此，所有三个函数都可以以 `Bisect()` 的名称使用，因为它们的签名不同，编译器确切知道应该使用哪个 `Bisect()` 函数。

# 第 8 章：数据类型类 (class)

![](img/image01170.jpeg)![](img/image01171.jpeg)学生 2 6.4 节包含了动态数据结构，通过这些结构必须特殊地实现对应变量的初始化和复制（另见 7.5.2）。C++ 类概念的众多优势之一是，带有动态组件的数据结构可以像简单数据类型一样在主程序中处理。当然，这需要一些准备工作。

![](img/image01172.jpeg)`class` 是带有关联方法（函数）的数据类型，将在结构体中创建并以类似的方式使用。类的方法始终可以访问类的数据。

![](img/image01173.jpeg)![](img/image01174.jpeg)从结构体 `Student2` 我们推导出一个类 `Students`。我们将类的所有声明保存在头文件 `studenten.hh` 中，将所有定义保存在 `studenten.cc` 中。在 `studs.hh` 和 `studs.cc` 文件中可以关于指针初始化的修改变体。

![](img/image01175.jpeg)

![](img/image01176.jpeg)

## 8.1 类声明数据和方法

![](img/image01177.jpeg)这是 `Students` 类的声明，包含了绝对必要的方法。让我们按照给顺序查看它们。

## 8.2 构造函数

构造函数用于类数据的初始初始化。通常，一个类应该至少包含以下构造函数：

- 默认构造函数的定义（无参数）

8.2 构造函数

![](img/image01178.jpeg)`::` 表示作用域运算符。默认构造函数在主程序中使用，以便所有数据已初始化。

- 参数构造函数

![](img/image01179.jpeg)通过参数构造函数，创建并初始化 `Students` 变量：`Students("arni", "Schwarz")`。

- 拷贝构造函数

![](img/image01180.jpeg)拷贝构造函数允许创建同类的变量：`Students(arni)`。

## 8.3 析构函数

![](img/image01181.jpeg)每个类都有析构函数，在离开块时自动调用。析构函数的主要任务是释放动态内存。

## 8.4 赋值运算符

![](img/image01182.jpeg)构造函数总是访问未初始化的数据。为了给已初始化的变量赋值，必须定义赋值运算符：`robbi = arni`。

## 8.5 打印运算符

![](img/image01183.jpeg)`friend` 标识符允许 `ostream` 类定义新方法。其定义如下：

```
ostream & operator<<(ostream & s, const students & orig)
```

![](img/image01184.jpeg)输出用法：

```
cout << robbi << endl;
```

![](img/image01185.jpeg)我们使用 6.4 中的示例 `Ex43-correct.cc`（或 `Ex752.cc`）更容易编写和扩展。命令行：

```
LINUX> g++ Ex851.cc students.cc
```

生成了可执行程序。

## 8.6 数据封装

![](img/image01187.jpeg)`students` 中的数据被分类为 `public`，这意味着任何人都可以访问这些数据，如 `mike.pfirstname`。为了保护数据免受意外访问，我们将数据封装到类中，仅提供访问方法。相关的分类是由 `private` 逻辑指定的。因此，修改 `students` 类的声明部分在

![](img/image01189.jpeg)

```
//students2.hh
#include <iostream.h>

class students
{
// students 中的数据现在是私有的！！
private:
    long int register;
    int skz;
    char *pname, *pfirstname;

// students 中的方法
public:
    //构造函数、析构函数、访问运算符
    ...

    // 输出运算符
    friend ostream & operator<<(ostream & s, const students & orig);

    //访问私有数据的方法
    // 操作数据的方法
    void SetFirstName(const char firstname[]);

    void SetName(const char name[]);

    void SetMatrikel(const longinternalmat_nr); void SetSKZ(constintskz_nr);

    // 不操作 students 数据的方法
    const long int& GetMatrikel() const;

    const int& GetSKZ() const; const char* GetFirstName() const; const char* GetName() const;
};
```




![](img/image01190.jpeg)![](img/image01191.jpeg);

在上述方法中有两个 `const` 声明。声明行末尾的 `const` 表示 `Student` 中的数据不会被对应的方法修改，例如 `GetSKZ()`。行首的 `const` 属于结果类型，表示通过引用 `int&` 指向的数据不能被更改。这确保了数据不会通过指针或引用被无意操作。

访问方法的定义如下：

![](img/image01192.jpeg)![](img/image01193.jpeg)

![](img/image01194.jpeg)![](img/image01195.jpeg)这些新的访问方法用法如下所示：

某些访问函数，例如 `SetSKZ()` 和 `GetSKZ()` 非常短，由于传递参数的开销，调用函数实际上是不划划的。在这种情况下，方法的声明和定义在头文件中链接，并且方法/函数被定义为内联（inline）的。这些内联行每次都会替换函数调用。

![](img/image01196.jpeg)![](img/image01197.jpeg)

# 第 9 章

# 文件输入与输出

用于 I/O 的对象 `cin` 和 `cout` 是（在 `iostream.h` 中）预定义的 `stream` 类型变量。为了从文件读取或写入文件，现在创建了新的流变量，即用于输入的 `ifstream` 类型和用于输出的 `ofstream` 类型。文件名在变量创建时（C++ 构造函数）传递。

103

![](img/image01198.jpeg)

## 9.1 复制文件

![](img/image01199.jpeg)![](img/image01200.jpeg)以下程序将输入文件复制到输出文件，但不包含空格、制表符和换行符。

另一方面，如果你想完全相同复制文件，必须逐字符地读取和写入。可以使用相应流类的 `get()` 和 `put()` 方法。

![](img/image01201.jpeg)

## 9.2 通过文件进行输入输出

## 9.2 通过文件进行输入输出

![](img/image01202.jpeg)![](img/image00844.jpeg)![](img/image01203.jpeg)通过文件和终端的输入输出可以结合使用。

## 9.3 切换输入/输出

![](img/image00844.jpeg)![](img/image01204.jpeg)有时需要在需要在文件 IO 和终端 IO 之间进行切换。遗憾的是，在这种情况下，你必须对 `istream` 和 `ostream` 类型进行操作。

![](img/image01205.gif)

![](img/image01206.jpeg)

![](img/image01207.jpeg)![](img/image00844.jpeg)![](img/image00844.jpeg)![](img/image01208.jpeg)在示例中可以找到使用命令行参数切换输入输出的所有方便方法。

# 输出格式化

输出和流（`<<`）可以高度格式化。这里给出少量格式化的示例，更多请参阅文献。

![](img/image01209.jpeg)我们使用这些变量 `double da = 1.0/3.0`, `db = 21./2`, `dc = 1234.56789;`

![](img/image01210.jpeg)标准输出：

```cpp
cout << da << endl << db << endl << dc << endl << endl;
```

![](img/image01211.jpeg)输出中的有效位数（此处为 12）：

```cpp
cout.precision(12); cout << ...;
```

![](img/image01212.jpeg)固定的小数位数（此处为 6）：
```cpp
cout.precision(6); cout.setf(ios::fixed, ios::floatfield); cout << ...;
```

![](img/image01213.jpeg)科学计数法输出：
```cpp
cout.setf(ios::scientific, ios::floatfield); cout << ...;
```

![](img/image01214.jpeg)标准版输出：
```cpp
cout.setf(0, ios::floatfield); cout << ...;
```

![](img/image01215.jpeg)对齐 G（右对齐）通配符（16 个字符）：
```cpp
cout.setf(ios::right, ios::adjustfield); cout.width(16);
cout << da << endl;
cout.width(16); cout << db << endl;
cout.width(16); cout << dc << endl;
```

107

108 第 10 章 输出格式化

使用标准操器的通用解决方案见 [Str00, § 1.4.6.2, pp.679]。

![](img/image01216.jpeg)整数的十六进制输出：
```cpp
cout.setf(ios::hex, ios::basefield); cout << "127 = " << 127 << endl;
```

# 技巧与窍门

## 11.1 预处理器命令

我们已经知道预处理器

```cpp
#include <math.h>
```

![](img/image01217.jpeg)![](img/image01218.jpeg)在适当的位置插入 `math.h` 的内容。同样，源代码的某些部分根据依赖关系包含或忽略。

```cpp
#ifdef MY_DEBUG
cout << "In debug";
#endif

#ifndef MY_DEBUG
#define MY_DEBUG
#endif
```

![](img/image01219.jpeg)在示例中可以找到使用命令行参数切换输入输出的所有方便方法。

```cpp
#ifdef MY_DEBUG
cout << "PI = " << M_PI << endl;
#else
#endif
```

```cpp
#ifndef MY_DEBUG
#define M_PI 3.14159
#endif
```

系数 `a_k` 和值 `xk` 在文件 `Ex121.cc` 中。函数值通过两种数学等的方式计算。变体 1 使用 `pow()` 函数，而变体 2 通过连续相法计算 `xk` 的值。

不同的运行时行为可以通过时间测量来证明，并通过逐步激活编译器优化选项来改进，例如：

```bash
g++ Ex121.cc
g++ -O Ex121.cc
g++ -O3 Ex121.cc
```

通过以下方式启动程序：
```bash
a.out < input.1121
```

## 11.2 程序中的计时

![](img/image01221.jpeg)到 `time.h` 文件 `ostream` 提供某些程序部分的时间。

![](img/image01222.jpeg)



[content]

编译器开关 `-pg` 为程序中的留了一些额外功能，以便在程序运行后可以使用 `gprof` 分析其运行时行为。最后一条命令（也可以是编辑器）将在屏幕上显示此分析的重定向输出。

## 11.4 调试

通常需要逐步跟踪程序流，并在必要时为了控制目的输出变量值等内容。接下来：

```cpp
cout << "AA" << variable << endl;
...
cout << "BB" << variable << endl;
...
```

通常可以使用专业的调试工具。这里再次展示了一个演示了在 LINUX 下运行的（免费的）程序。

```bash
LINUX> g++ -g Ex1121.cc
LINUX> ddd a.out &
```

各种调试器的处理方式差异很大。使用 `ddd` 调试器时，可以通过 `set args < input.1121` 指定输入文件，并使用 `run` 启动测试运行，程序会在之前设置的断点处停止。在那里，可以使用源代码逐步跟踪程序。

## 参考文献

- [Cap01] Derek Capper. *面向科学家、工程师和数学家的 C++ 简介*. Springer, 2001.
- [CF88] Matthew Clauss and Günther rightfisherman. *C 语言编程*. Verlag Technique, 1988.
- [Cor93] microsoft corp. *C++ 编程快速入门指南*. Microsoft Press, 1993.
- [Dav00] Stephen R Davis. *初学者学 C++*. boarding school Thomson Publ., Bonn/Albany/Attenkirchen, 第 2 版, 2000.
- [Erl99] Helmut Erlenkotter. *入门之前的 C 语言编程*. Romney, 1999.
- [God98] Edward Gode. *ANSI C++：简明精要*. O'Reilly, 1998.
- [Her00] Diet Herrmann. *自然自然爱好者的 C++*. Addison-Wesley, Bonn, 第 4 版, 2000.
- [Her01] Dietmar Herrmann. *C 和 C++ 高效编程*. vieweg, 第 5 版版, 2001.
- [HT03] Andrew Hunt and David Thomas. *实用型程序员*. Hanser 教科, 2003.
- [Jos94] Nicolai Josuttis. *C++ 面向对象编程：从类到类库*. Addison-Wesley, Bonn/Paris/Reading, 第 3 版, 1994.
- [KPP02] Ulla Kirch-Prinz and Peter Prinz. *关于面向对象编程的一切*. Galileo Press, 2002.
- [KPP03] Ulla Kirch-Prinz and Peter Prinz. *面向 C 程序员的 C++*. Galileo Press, 2003 年 10 月.
- [Mey97] Scott Meyers. *更有效地使用 C++ 程序*. Addison-Wesley, 1997.
- [Mey98] Scott Meyers. *C++ 高效编程*. Addison-Wesley, 第 3 版, 订版, 1998.
- [OT93] Andrew Oram and Steve Talbott. *使用 make 管理项目*. O'Reilly, 1993.
- [SB95] Gregory Satir and Doug Brown. *C++：核心语言*. O'Reilly, 1995.
- [SK98] Martin Schader and Stefan Kuhlins. *C++ 编程*. Romney Vieweg, 第 5 版修订版, 1998.
- [Str00] Bjarne Stroustrup. *C++ 程序语言*. Addison-Wesley, 第 4 版修订版, 2000.
- [Str03] Thomas Strasser. *风格化编程：系统性介绍*. dpunkt, 2003.

## 索引

- `#define`, 109
- `#if`, 110
- `#ifdef`, 109
- `#ifndef`, 109
- `#include`, 109
- `abort 测试`, 41, 38
- `拒绝循环`, 38
- `替代方案`, 27
- `指令`, 3, 4, 25
- `argc`, 84
- `argv[]`, 84
- `数组`, 见字段汇编器, 5
- `atod()`, 85
- `atoi()`, 85
- `onzaestyp`, 45, 57
- `表达式`, 13 版
- `代价`, 103
- `文件`, 103
- `格式化`, 107
- `换行`, 9
- `char`, 7
- `类`, 93-101
- `数据封装`, 99
- `声明`, 94 方法
- `见方法`, 93
- `编译`, 20
- `条件判断`, 109
- `g++`, 4-6, 83, 111, 112
- `gcc`, 3
- `调试`, 112
- `delete`, 62
- `do-while 循环`, 见非拒绝循环
- `double`, 7
- `记事本`, 3 输入
- `cin`, 103
- `决策运算符`, 29
- `enum`, 见枚举类型
- `false`, 15
- `布尔`, 13 版
- `库`, 5, 10, 109
- `性能分析`, 111
- `导出`, 3, 4
- `源文件`, 6, 80
- `引用`, 68
- `符号值`, 29, 72
- `sizeof()`, 8
- `string.h`, 21
- `strcat()`, 21
- `strchr()`, 21
- `strcmp()`, 21
- `strcpy()`, 21
- `strlen()`, 21
- `struct`, 见结构体, 45, 52-55
- `在结构体中`, 54
- `指针向上`, 67
- `指针向下`, 65
- `大学生`, 82
- `类`, 94
- `结构体`, 53
- `学生 2`, 65, 82
- `后缀`, 6
- `switch`
- `time.h`
- `clock()`, 110
- `true`, 15, 17, 57
- `union`, 45, 56
- `使用空间`, 6
- `变量`, 7–8
- `存储类`, 7
- `类型`, 7
- `while 循环`, 请见非拒绝循环
- `真值表`, 18

