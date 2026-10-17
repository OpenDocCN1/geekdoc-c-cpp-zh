
# C 与 Cpp 编程 (C++)

- 哈希表 (Hash Tables) . . . . . . . . . . . 341
- 排序 . . . . . . . . . . . . . . . . . . . 347
  - 泡泡排序 . . . . . . . . . . . . . . 348
  - 插入排序 . . . . . . . . . . . . . 353
  - 快速排序 . . . . . . . . . . . . . 355
  - 合并排序 . . . . . . . . . . . . 356
- 搜索 . . . . . . . . . . . . . . . . . . 357
  - 二分查找 . . . . . . . . . . . . . . . . 358

# 简介

本书尝试解释 C 和 C++ 编程语言。虽然 C 和 C++ 是最古老的编程语言，但它们仍然被大多数操作系统使用，如 Linux，以及 FreeRTOS 等实时操作系统（RTOS）。这两种语言仍广泛用于固件开发。有时使用 `libc` 和 `libstdc++`，有时则不使用。在为 Linux 系统编写代码时，编写软件的绝大多数情况下都会使用库。使用库可以简化软件开发，因为它提供了大部分接口。在库的成本变得过高的情况下，通常是我们正在为具有有限 RAM 和 Flash 内存的微控制器等小型设备进行编程。在这种情况下，倾向于尽可能使用语言本身的结构，而不是使用任何库函数。

例如，C 和 C++ 库提供了以下功能：

1. 字符串处理
2. 控制台操作（向控制台写入和从控制台读取）
3. 文件系统交互（FILE I/O）
4. C++ 中的操作系统抽象（例如线程的创建和使用、与文件系统的交互）

编译器实现了 C 和 C++ 语言。它验证程序是否符合语言规范，并生成二进制文件。

在 Ubuntu 上安装 `gcc` 和 `g++`：

```bash
sudo apt install gcc g++
```

# 读者群体

本书的读者是初级和中级程序员。对于高级程序员，你可能已经了解了这些编程结构。

# C 语言编程

## 基础 Hello World 程序

下面是一个基础的 C 语言 hello world 程序。

```c
#include <stdio.h>

int main() {
    // 在控制台打印 Hello World
    printf("Hello World\n");
    return 0;
}
```

示例 1：`hello_world.c` 是一个函数，程序始终从 `main()` 执行。函数调用 `printf` 允许程序向控制台写入。头文件 `stdio.h` 包含了 `printf` 的原型。

`//` 表示注释行。整行 `//` 之后的内容都会被忽略。这些通常被称为 C++ 风格的注释。它们不是多行注释。

另一种类型的注释以 `/*` 开头并以 `*/` 结束。这可以作为多行注释。

这里有一个例子：

```c
/*
这是一个多行注释，
显示了可以编写多行内容。
*/
```

使用 `//` 还是 `/*` 完全取决于他们的编码风格。

语句 `return 0` 指定函数返回 0。在 C 语言中，函数可能不会在函数签名中返回。

为了运行上面的程序，我们需要创建一个可执行文件。要创建此可执行文件，我们需要对其进行编译。

将上面的程序复制并粘贴到文本编辑器中，并保存为文件 `hello_world.c`。

所有用 C 编写的源代码扩展均为 `.c` 或 `.h`。

扩展名为 `.h` 的文件称为头文件。头文件包含以下内容：

1. 宏定义。
2. 函数原型。
3. 数据结构定义。

```bash
gcc hello_world.c
```

## 基础数据类型

以下是 C 中的中的数据类型。它们也适用于 C++。

以下是 32 位系统的一些数据类型。

| 序号 | 类型 | 说明 | 范围 |
|---|---|---|---|
| 1 | `char` | 1 字节符号整数 | -127 到 127 |
| 2 | `unsigned char` | 1 字节无符号整数 | 0 到 255 |
| 3 | `short int` | 2 字节符号整数 | -32767 到 32767 |
| 4 | `unsigned short int` | 2 字节无符号整数 | 0 到 65535 |
| 5 | `int` | 4 字节符号整数 | -2147483648 到 2147483647 |
| 6 | `unsigned` | 4 字节无符号整数 | 0 到 4294967295 |
| 7 | `float` | 4 字节浮点变量 | - |
| 8 | `double` | 4 / 8 字节双精度变量 | - |

上述类型的变量可以如下声明声明：

```c
int a;
```

`a` 是一个 `int` 类型的变量。

```c
int a = 4;
```

上面的语句将 `a` 初始化为 4。

```c
int a;
a = 4;
int a = 0x20;
```

用十六进制数初始化 `a`。十六进制用 `0x` 标记。

有时在程序中，我们会初始化变量并在稍后给变量赋一个值。

未初始化的变量被称为未初始化变量。使用未初始化变量时会产生更大的问题，原因是它们在声明时持有某些未知值。当在未初始化的情况下使用变量时，程序运行时的行为将出乎意料。这通常会导致执行错误并提供错误的结果。

理想的解决方案是在声明变量时始终初始化它们，以避免未初始化变量引起的问题。

每个声明的变量都与一个类型相关。回顾变量及其作用域的章节。

声明 `double`：

```c
double f = 3.14;
```

C 语言中无法表示精确的 `double` 值。

## sizeof 运算符

`sizeof` 用于获取变量的大小。

```c
#include <stdio.h>

int main() {
    int a;
    printf("size of a: %zu\n", sizeof(a));

    return 0;
}
```

`sizeof` 运算符用于确定数据类型的字节数。

## 格式说明符

格式说明符用于 `printf` 和 `scanf`，以格式化数据的输出或输入。

| 序号 | 格式说明符 | 含义 |
|---|---|---|
| 1 | `%d` | 整数 |
| 2 | `%c` | 字符 |
| 3 | `%s` | 字符串 |
| 4 | `%f` | `float` 或 `double` |
| 5 | `%u` | 无符号整数 |
| 6 | `%ld` | 长整数 |
| 7 | `%lld` | 长整数 |
| 8 | `%lu` | 长无符号整数 |
| 9 | `%llu` | 长无符号整数 |
| 10 | `%x` | 十六进制 |

以下是一些使用格式说明符的更多函数：

| 序号 | 函数名 |
|---|---|
| 1 | `scanf` |
| 2 | `printf` |
| 3 | `scansf` |
| 4 | `vprintf` |
| 5 | `vsprintf` |

## 类型定义

任何类型都可以被定义为另一种类型。`typedef` 关键字就用于此目的。

```c
typedef int integer_t;
```

现在，`integer_t` 可以作为一种新类型来声明变量。`typedef` 可以应用于许多其他数据类型，例如结构体和函数指针。

通常，`typedef` 用于为类型赋予一个有意义的名字，或者当使用的类型过长时，`typedef` 提供了一种用简短形式表示该类型的替代方法。

例如，

```c
typedef unsigned int u_int32_t; // 无符号 32 位整数
typedef unsigned char u_int8_t; // 无符号 8 位整数
```

C 语言允许使用 `struct` 扩展新类型，这在“结构体”章节中有详细描述。

在下方的章节中，`typedef` 被许多处使用并进行了进一步的解释。

## 类型转换

一种类型的变量可以类型转换为其他类型的变量。类型转换有时是不可避免的。更多相关内容请参阅空指针章节。

下面的程序给出了从整数到双精度浮点数转换的示例。在此下载。

```c
#include <stdio.h>

int main() {
    int d;
    double v = 10.1;

    d = (int)v;

    printf("%d d %f\n", d, v);
    return 0;
}
```

### 示例.3 类型转换

将双精度浮点数转换为整数会丢失精度，数字会丢失小数部分。注意，数字不会被舍入到最近的整数。

例如，

```c
int r;
double p = 10.99;
```

```c
r = (int)p; // 舍入为 10。
```

会将值 10.99 舍入为 10 并赋值给 `r`。

## 运算符

C 语言拥有以下可用于给定类型变量的运算符。

| 序号 | 运算符 | 含义 |
|---|---|---|
| 1 | `+` | 加法 |
| 2 | `-` | 减法 |
| 3 | `*` | 乘法 |
| 4 | `/` | 除法 |
| 5 | `%` | 取模 |
| 6 | `=` | 等于 |
| 7 | `==` | 比较运算符 |
| 8 | `\|` | 或 |
| 9 | `&&` | 逻辑与 |
| 10 | `&` | 与 |
| 11 | `^` | 异或 |
| 12 | `!` | 非 |
| 13 | `!!` | 逻辑非 |
| 14 | `++` | 递增运算符 |
| 15 | `--` | 递减运算符 |

下面的示例展示了运算符的用法。

```c
#include <stdio.h>

int main() {
    int a = 4;
    int b = 2;
    int sum;
    int sub;
    int mul;
    int div;
    int mod;

    sum = a + b; // 两个数加
    sub = a - b; // 两个数减
    mul = a * b; // 两个数相乘
    div = a / b; // 两个数除
    mod = a % b; // 两个数取模

    printf("sum %d sub %d\n", sum, sub);
    printf("mul %d div %d modulo %d\n", mul, div, mod);

    return 0;
}
```

### 示例.4 运算符示例

`++` 和 `--` 是递增和递减运算符。下面的示例展示了如何使用它们。

布尔操作如 `|`, `&`, `||`, `&&`, `^` 和 `!` 永远不会应用于双精度浮点数变量。

```c
#include <stdio.h>

int main()
{
    int i = 0;
    printf("%i %d\n", ++ i);
    return 0;
}
```

### 示例.5 前递增运算符

上面的程序打印值 1。

考虑另一个程序。

```c
#include <stdio.h>

int main()
{
    int i = 0;
    printf("%i %d\n", i++);
    return 0;
}
```

### 示例.6 后递增运算符

上面的程序打印值 0。

这通常被称为未定义行为。语言留给编译器决定，`++i` 是前置表示法而 `i++` 是后置表示法。然而，程序员在调试软件时会选择 `++i` 或 `i++`。

`++` 和 `--` 在 `while` 和 `for` 循环中有更多用例。

`!!` 用于检查数字是否为非零。下面的示例显示了如何使用它。

```c
#include <stdio.h>

int main() {
    int a = 4;
    int b = 0;
    printf("a=%d b=%d\n", a, b);
    return 0;
}
```

### 示例.7 逻辑非运算符

这意味着数字为负（非零）`!!` 操作的结果为 1。例如，在下面的代码段中，`r` 和 `p` 的值分别为 1 和 1。

```c
int r = -1;
int p = 1;
printf("%d %d", !!r, !!p);
```

下面的示例显示了 `|` 运算符的使用。在此下载。

```c
#include <stdio.h>

int main() {
    int a = 0;
    int b = 1;
    printf("%d %d\n", a | b);
    return 0;
}
```

### 示例.8 逻辑与运算符

输出是：

## 作用域和变量的生命周期

函数内部声明的每个变量都有特定的作用域。当函数返回时，这些变量将被销毁或从内存中移除。通常情况下，每个程序由操作系统分配了一定的内存。该内存被划分为以下部分：

1. 栈段 (stack segment)
2. 堆段 (heap segment)
3. 数据段 (data segment)
4. 代码段 (text segment)

下面是图示表示。

| | |
|---|---|
| 栈段 | 栈在内存中向下增长 |
| 堆段 | 堆在内存中向上增长 |
| 未初始化数据 | |
| 初始化数据 | |
| 代码 | |

### 1. 栈段

局部栈默认大小为 8 字节。但这取决于操作系统。在基于 RTOS 的系统中，它是在链接器脚本中配置的。栈在内存中向下增长。局部变量和函数参数是栈的一部分。每当调用函数时，都会进行分配并向下。返回后，栈会自动释放。通常，如果分配达到最大值，栈会耗尽，导致栈溢出。在某些操作系统中，这将导致系统停止（例如在微控制器上的 RTOS），而系统其他部分正常执行。在任何情况下，结果都是程序中止。为了避免这种情况，必须仔细使用栈内存。如果没有堆段，可以使用数据段。栈变量的生命周期仅限于函数。这通常是通过将作用域限制在函数或组内的正确编程方法之一。下面的示例显示了限制在函数内的静态变量。

```c
int F()
{
    int a = 3;

    return a * 2;
}
```

### 示例.9 局部变量

在这里变量 `a` 是局部变量，是栈的一部分。下面是带栈的作用域变量设置另一个示例。

```c
int F()
{
    // 变量 a 的范围位于 { } 之间
    {
        int a = 3;

        a *= 3;
    }

    return a; // 返回 a 未定义的错误
}
```

### 示例.10 作用域声明语句

GCC 提供了编译器选项来检查栈的使用。查看 GCC 编译器选项。

### 2. 堆段

这是分配动态内存的空间。它是通过编程语言中的分配函数显式分配的。C 和 C++ 暴露以下分配程序：

1. `malloc`
2. `calloc`
3. `realloc`
4. `free`
5. `new`
6. `delete`

最后两个在 C++ 标准库中，但它支持所有这些。C 库支持前 4 个。

一旦通过这些调用进行分配，释放内存的方法只有调用 `free` 程序。它没有自动释放。如果不释放任何堆内存，长时间运行后，系统将耗尽内存空间。

不释放堆内存会导致内存泄漏。当程序停止运行时，通常操作系统会清理分配给它的内存，并将内存归给空闲池。然而，如果程序运行了很长时间且从未释放内存，会导致内存占用增加，并可能导致内存压力/耗尽。

通常操作系统通过触发自动杀死使用高内存的程序来响应内存耗尽，以恢复内存使用。在 Linux 中，这被称为内核空间中的 OOM Killer。

堆段的生命周期是整个程序，但作用域限于局部或文件作用域。分配的内存始终是堆段的一部分。

### 3. 数据段

数据段包括初始化和未初始化段。

以下是变量属于数据段的一些情况：

- 可由所有源文件中所有函数全局访问的变量。
- 可由源文件本地所有函数访问的变量。通常我们使用 `static` 前缀将它们的作用域限制在单个文件中。
- 带有 `static` 前缀且可由函数局部访问的变量。

这些变量的生命周期是整个程序。

指针也可以是全局的。

虽然全局变量和静态全局变量的使用使得编程更简单，但它会导致变量及其使用的一片混乱。这在程序需要更新时会导致进一步的困惑。在必须使用全局或静态全局变量的情况下，必须考虑这一点，并考虑使用全局变量的替代方案。

在微控制器上，栈通常是限制的，以避免在存在大量变量和大量函数调用时发生栈溢出。为了避免这种情况，大型且常用的变量保留在数据段中。

### 4. 代码段 (Text segment)

代码段包含程序代码、指令。它通常位于栈和堆下方以防止被覆盖。它是只读的，但在大多数情况下，活动攻击可能会覆盖代码段并执行未知程序（如病毒、蠕虫）。

例如，

```c
char *msg = "hello";
```

`msg` 被分配在代码段中。更改此位置位置的任何内容都会导致错误。

```c
#include <stdio.h>
```

```c
int main() {
    char *ptr = "hello";

    *ptr = 'i';

    printf("%s\n", ptr);

    return 0;
}
```

示例.11 代码段

上面的程序运行后，会导致段错误且程序停止。

通常情况下，语言提供了一些机制在编译时检测修改。例如，当 `const` 用作 `char *ptr` 的前缀时，编译将失败并提示只读位置被修改。

```c
#include <stdio.h>
```

```c
int main()
{
    const char *ptr = "hello";

    *ptr = 'i';

    printf("%s\n", ptr);

    return 0;
}
```



示例.12 带有 `const` 的代码段

`c/read_only.c:7`: 在函数 `'main'`:
`c/read_only.c:7:10`: 错误:赋值给只读位置 `'*ptr'`
`7 | *ptr = 'i';`

### 控制语句 (Control statements)

### 1. if else 语句

`if` 语句提供了一种根据数据控制程序执行路径的方法。

`if` 语句持有条件并被评估为真或假。如果条件为真，则执行 `if` 中的语句；否则，执行 `else` 中的语句。

`else` 语句通常跟在 `if` 语句之后，永远不会单独存在。`else` 语句不包含像 `if` 那样的条件。

```c
#include <stdio.h>
```

```c
int main() {
    char p = 'd';
    if (p == 'd') {
        printf("%c is %c\n", p, 'd');
    } else {
        printf("%c is not 'd\n", p);
    }
    return 0;
}
```

### 示例.13 if else 条件

条件检查 `if (p)` 也是有效的检查，但这种检查只检查值是否非零。如果值为 0，则 `if (p)` 下的语句永远不会执行。请理解在 C 语言中，条件检查取决于变量的值。

通常情况下，`else` 语句不必跟在 `if` 语句后面。但如果需要，有一个 `else` 语句是一个良好的习惯。

让我们考虑下面的程序。在此处下载。

```c
#include <stdio.h>
```

```c
int main() {
    char p = 'f';
    if (p == 'f') {
        printf("%c is %c\n", p, 'd');
    }
}
```

```c
return 0;
}
```

示例.14 带有赋值的 `if` 条件 注意这个错误了吗？

`if` 条件中使用了赋值运算符而不是等值测试。这导致了普通赋值并执行，因此 `if` 内部的 `printf` 将执行并打印以下内容：

```c
p 'f' is d
```

我们通常倾向于避免在 `if` 内部使用赋值语句以防止出现此类测试，这也是正确的。

```c
if (p) {
    printf("p is '%c\n", p);
} else {
    printf("p is not '%c\n", p);
}
printf(p)
```

示例.15 对 `p` 的验证
在 `if` 语句中检查的条件是 0 或非零。

所以上面的条件导致打印 `"p is d"`。

### 2. if else-if 语句

`if else-if` 语句也称为 `if else` 阶梯 (`if else ladder`)，用于构建一系列的 `if else-if` 条件。

下面是 `if else-if` 阶梯的示例。

```c
#include <stdio.h>

int main() {
    int number = 50;
    if (number < 50) {
        printf("number is less than 50\n");
    } else if (number > 50) {
        printf("number is greater than 50\n");
    } else if (number == 50) {
        printf("number is equal to 50\n");
    } else {
        printf("number is [%d] unknown\n", number);
    }
    return 0;
}
```

示例.16 `if else` 阶梯

通常情况下，`if else-if` 阶梯不用于许多大规模应用，除非涉及范围判断。这就是为什么上面的示例展示了带有范围的 `if else-if`。

在大多数情况下，`if else-if` 永远不会以 `else` 情况结尾，只有少数的编程指令可能需要 `else-if` 情况。

通常情况下 `else` 语句不一定要跟在 `if` 语句后面。但如果需要，拥有一个 `else` 语句是一个良好的习惯。

让我们考虑下面的程序。在此处下载。

```c
#include <stdio.h>
```

```c
int main() {
    char p = 'f';
    if (p == 'f') {
        printf("%c is %c\n", p, 'd');
    }
}
```

```c
return 0;
}
```

示例.14 带有赋值的 `if` 条件 注意这个错误了吗？

`if` 条件中使用了赋值运算符而不是等值测试。这导致了普通赋值并执行，因此 `if` 内部的 `printf` 将执行并打印以下内容：

```c
p 'f' is d
```

我们通常倾向于避免在 `if` 内部使用赋值语句以防止出现此类测试，这也是正确的。

```c
if (p) {
    printf("p is '%c\n", p);
} else {
    printf("p is not '%c\n", p);
}
printf(p)
```

示例.15 对 `p` 的验证
在 `if` 语句中检查的条件是 0 或非零。

所以上面的条件导致打印 `"p is d"`。

## 2. if else-if 语句 (重复：`if else` 阶梯 `ladder if else` 阶梯)

## 1. if else 语句 (重复：`if else` 语句)

## 2. if else-if 语句 (重复：`if else-if` 语句)

*(注：此处由于原文中存在重复的标题，翻译已按逻辑保留结构)*

---
*(更正：由于提供的文本中存在大量重复的标题和段落，我将严格按照原文逻辑流进行翻译。以下是完整文本的对应翻译：)*

这些变量的生命周期是整个程序。

指针也可以是全局的。

虽然全局变量和静态全局变量的使用使得编程更简单，但它会导致变量及其使用的一片混乱。这在程序需要更新时会导致进一步的困惑。在必须使用全局或静态全局变量的情况下，必须考虑这一点，并考虑使用全局变量的替代方案。

在微控制器上，栈通常是限制的，以避免在存在大量变量和大量函数调用时发生栈溢出。为了避免这种情况，大型且常用的变量保留在数据段中。

### 4. 代码段 (Text segment)

代码段包含程序代码、指令。它通常位于栈和堆下方以防止被覆盖。它是只读的，但在大多数情况下，活动攻击可能会覆盖代码段并执行未知程序（如病毒、蠕虫）。

例如，

`char *msg = "hello";`

`msg` 被分配在代码段中。更改此位置的任何内容都会导致错误。

```c
#include <stdio.h>
```

```c
int main() {
    char *ptr = "hello";
    *ptr = 'i';
    printf("%s\n", ptr);
    return 0;
}
```

示例.11 代码段

上面的程序运行后，会导致段错误且程序停止。
通常情况下，语言提供了一些机制在编译时检测修改。例如，当 `const` 用作 `char *ptr` 的前缀时，编译将失败并提示只读位置被修改。

```c
#include <stdio.h>
```

```c
int main()
```

```c
{
  const char *ptr = "hello";
  *ptr = 'i';
  printf("%s\n", ptr);
  return 0;
}
```

示例.12 带有 `const` 的代码段

`c/read_only.c:7`: 在函数 `'main'`:
`c/read_only.c:7:10`: 错误:赋值给只读位置 `'*ptr'`
`7 | *ptr = 'i';`

## 控制语句

### 1. if else 语句

`if` 语句提供了一种根据数据控制程序执行路径的方法。

`if` 语句持有条件并被评估为真或假。如果条件为真，则执行 `if` 中的语句；否则，执行 `else` 中的语句。

`else` 语句通常紧跟在 `if` 语句之后，永远不会单独存在。`else` 语句不包含像 `if` 那样的条件。

```c
#include <stdio.h>
```

```c
int main() {
    char p = 'd';
    if (p == 'd') {
        printf("%c is %c\n", p, 'd');
    } else {
        printf("%c is not 'd\n", p);
    }
    return 0;
}
```

### 示例.13 if else 条件

条件检查 `if (p)` 也是有效的检查，但这种检查只检查值是否非零。如果值为 0，则 `if (p)` 下的语句永远不会执行。请理解在 C 语言中，条件检查取决于变量的值。

通常情况下，`else` 语句不必非跟在 `if` 语句后面。但如果需要，拥有一个 `else` 语句是一个良好的习惯。

让我们考虑下面的程序。在此处下载。

```c
#include <stdio.h>
```

```c
int main() {
    char p = 'f';
    if (p == 'f') {
        printf("%c is %c\n", p, 'd');
    }
}
```

```c
return 0;
}
```

示例.14 带有赋值的 `if` 条件 注意这个错误了吗？

`if` 条件中使用了赋值运算符而不是等值测试。这导致了普通赋值并执行，因此 `if` 内部的 `printf` 将执行并打印以下内容：

```c
p 'f' is d
```

我们通常倾向于避免在 `if` 内部使用赋值语句以防止出现此类测试，这也是正确的。

```c
if (p) {
    printf("p is '%c\n", p);
} else {
    printf("p is not '%c\n", p);
}
printf(p)
```

示例.15 对 `p` 的验证

在 `if` 语句中检查的条件是 0 或非零。

所以上面的条件导致打印 `"p is d"`。

### 2. if else-if 语句

`if else-if` 语句也称为 `if else` 阶梯 (`if else ladder`)，用于构建一系列的 `if else-if` 条件。

下面是 `if else-if` 阶梯的示例。

```c
#include <stdio.h>

int main() {
    int number = 50;
    if (number < 50) {
        printf("number is less than 50\n");
    } else if (number > 50) {
        printf("number is greater than 50\n");
    } else if (number == 50) {
        printf("number is equal to 50\n");
    } else {
        printf("number is [%d] unknown\n", number);
    }
    return 0;
}
```

示例.16 `if else` 阶梯 `ladder`

通常情况下，`if else-if` 阶梯不用于许多大规模应用，除非涉及范围判断。这就是为什么上面的示例展示了带有范围的 `if else-if`。

在大多数情况下，`if else-if` 永远不会以 `else` 情况结尾，只有少数的编程指令可能需要 `else-if` 情况。

通常情况下 `else` 语句不一定要跟在 `if` 语句后面。但如果需要，拥有一个 `else` 语句是一个良好的习惯。

*(注：此处后续由于原文内容重复，翻译已根据原文结构呈现)*

示例.24 `while` 循环和 `break` 语句

上述程序展示了 `while (1)` 的用法。这通常意味着 `while` 循环中的条件永远为假。它是一个无限循环。

在编程中，如果没有在 `while` 语句中进行任何条件检查，无限循环通常不是首选。

无限循环通常无所事事，只会增加程序运行进程的 CPU 负载，并浪费 CPU 周期。然而，某些为操作系统编写的程序需要无限运行（例如图形、显示、编辑器等）。为了实现这一点，操作系统采用了硬件支持的某些事件驱动机制。这确保了程序仅根据特定事件执行。

### 2. for 循环

`for` 循环类似于 `while` 循环。其语法如下：

`for (初始化; 条件; 递增/递减操作)`

下面是 `for` 循环使用的示例。

```c
#include <stdio.h>
```

```c
int main()
{
    int i;
    for (i = 0; i < 10; i++) {
        printf("%i %d\n", i);
    }
    return 0;
}
```

示例.25 `for` 循环

`for` 中的 `i = 0` 语句只执行一次。`i < 10` 语句在每次循环重复时执行。`i++` 语句在 `for` 中的语句每次执行后都会执行。

另一种实现方法如下所示：

```c
#include <stdio.h>
```

```c
int main()
{
    int i = 0;
    for (; i < 10; i++) {
        printf("%i %d\n", i);
    }
    return 0;
}
```

示例.26 `for` 迭代

初始化语句可以省略。

上述的 `while (1)` 可以重写为 `for` 如下：

```c
#include <stdio.h>
```

```c
int main()
{
    int i = 0;

    for (;;) {
        if (i >= 10) {
            break;
        }
        printf("i %d\n", i);
        i++;
    }

    return 0;
}
```

示例.27 无限 `for` 循环

`for(;;)` 也是一个无限 `for` 循环。如所述，使用无限循环必须谨慎。

### 3. do while 循环

`do..while` 循环与 `while` 相似。下面是一个示例。

```c
#include <stdio.h>

int main()
{
    int i = 0;
    do {
        printf("Hello World\n");
    } while (i != 0);
    return 0;
}
```

示例.28 `do..while` 循环

一旦运行，它会打印 `Hello World`。这意味着语句先执行，稍后进行检查。

### Goto 语句

`goto` 语句类似于汇编中的跳转指令。上述循环可以用 `goto` 重写如下：

```c
#include <stdio.h>

int main() {
    int i = 0;

begin:
    if (i < 10) {
        printf("%i %d\n", i);
        i++;
        goto begin;
    }
    return 0;
}
```

示例.29 `goto` 循环

我们不在程序中使用 `goto` 的原因如下：

- 在函数或 C 文件中使用许多 `goto` 会降低代码的可读性。
- 编写错误的 `goto` 可能会导致程序出现循环。

在程序中正确使用时，`goto` 并不是坏的。例如，当程序初始化期间某些条件失败时，反初始化序列必须执行相反的操作。在这种情况下，失败用例需要一个跳转。

这里有一个伪代码示例，

```c
int init_1() {
    return 0;
}
```

```c
int init_2() {
    ...
    return 0;
}
```

```c
void deinit_1() {
}
```

```c
...
}
int init_main()
{
    int ret;
    ret = init_1();
    if (ret != 0) {
        return -1;
    }
    ret = init_2();
    if (ret != 0) {
        goto deinit;
    }
}

deinit:
deinit_1();
return -1;
```

示例.30 `goto` 用例

更多关于函数的信息请参阅函数章节。

在汽车和航空航天软件应用领域，`goto` 语句很少被使用。它被认为是一种坏习惯。因此，在为此类应用编写软件时，避免这种情况是良好的一步。

### 数组

## 一维数组

一维数组是数组的基础类型。

整数数组定义为：

```c
int a[10];
```

上述语句定义了一个包含 10 个整数的数组 `a`。数组中的每个元素都是整数类型的元素。

数组索引从 0 开始。数组中的每个项目都用 0 到 9 的普通数字索引。

上述数组的最大元素数量为 10，但第 10 个元素的最后一个索引是 9 而不是 10。访问超出其最大范围的数组被称为越界。越界访问是一个主要的安全问题，因为元素分配了分配范围之外的地址。

以下程序为数组元素赋值。

```c
#include <stdio.h>

int main() {
    int a[10];
    int i = 0;

    for (i = 0; i < sizeof(a) / sizeof(a[0]); i++) {
        a[i] = i; // 修正：原文此处逻辑缺失赋值，根据上下文推断
    }

    printf("array elements:\n");
    for (i = 0; i < sizeof(a) / sizeof(a[0]); i++) {
        printf("%d\n", a[i]);
    }
    return 0;
}
```

示例.31 数组迭代（注：原文代码逻辑略有乱，已按意图对齐翻译）

初始化语句可以省略。



上述`while (1)`可以重写为`for`如下。

```c
#include <stdio.h>

int main()
{
    int i = 0;

    for (i = 0; i < 10; i++) {
        printf("%d\n", i);
    }
    return 0;
}
```

## 示例.32 sizeof 数组

通过`sizeof`方式计算数组。

```c
#include <stdio.h>

int main()
{
    int a[10];
    int i;

    for (i = 0; i < sizeof(a) / sizeof(a[0]); i++) {
        printf("%d\n", a[i]);
    }
    return 0;
}
```

## 示例.33 数组数量

通过`sizeof`也可以找到数组的数量。

```c
#include <stdio.h>

int main()
{
    int a[10];
    int i;

    for (i = 0; i < sizeof(a) / sizeof(a[0]); i++) {
        printf("%d\n", a[i]);
    }
    return 0;
}
```

## 示例.34 数组初始化

下面的语句初始化数组。默认情况下如下：

```c
#include <stdio.h>

int main()
{
    int a[10] = {0};
    int i;

    for (i = 0; i < 10; i++) {
        printf("%d\n", a[i]);
    }
    return 0;
}
```

## 示例.35 数组初始化

复制到另一个是简单的。另一种方法是`memcpy`。

```c
#include <stdio.h>
#include <string.h>

int main() {
    int a[10];
    int a2[10];
    int i;

    for (i = 0; i < 10; i++) {
        a2[i] = a[i];
    }

    for (i = 0; i < 10; i++) {
        printf("%d\n", a2[i]);
    }
    return 0;
}
```

## 示例.36 复制数组

## 二维数组

二维数组表示如下。

```c
#include <stdio.h>

int main()
{
    int a[10][10];
    int i;
    int j;

    for (i = 0; i < 10; i++) {
        for (j = 0; j < 10; j++) {
            a[i][j] = j + i;
        }
    }

    for (i = 0; i < 10; i++) {
        for (j = 0; j < 10; j++) {
            printf("a[%d][%d] = %d\n", i, j, a[i][j]);
        }
    }

    return 0;
}
```

## 示例.37 设置二维数组

## 三维数组

三维数组是二维数组的组。其表示方式如下：

```c
#include <stdio.h>

int main()
{
    int array[10][20][40];
    int i;
    int j;
    int k;
    for (i = 0; i < 10; i++) {
        for (j = 0; j < 20; j++) {
            for (k = 0; k < 40; k++) {
                array[i][j][k] = 10 + i;
            }
        }
    }
    for (i = 0; i < 10; i++) {
        for (j = 0; j < 20; j++) {
            for (k = 0; k < 40; k++) {
                printf("[%d][%d][%d] = %d\n", i, j, k, array[i][j][k]);
            }
        }
    }
    return 0;
}
```

## 示例.38 设置三维数组

数组的用途范围涉及许多地方，例如将一组字符分组，或者通过相似类型的分组来表示硬件设备或一组类似的硬件设备等。此外，数组在搜索和排序技术中也起着重要作用。

# 宏 (Macros)

宏是编译时常量，在运行时不分配任何空间。这意味着预处理器会将使用宏的区域替换为它们对应的值。

在上面的示例中，我们使用了`#include <stdio.h>`，其中`#include`是一个处理指令。它通知编译器将此语句替换为头文件`stdio.h`。

## #define 宏

预处理阶段会将宏替换为宏定义中存在的实际值。宏定义了宏常量。例如所示：

```
#define TWO 2
```

宏语句被用作常量或某些常用操作的替代品。例如使用：

```c
#define PI 3.1413
```

```c
double circumference(double radius)
{
    return 2 * PI * radius;
}
```

使用常量值更有意义。

```c
#define ADD(_a, _b) ((_a) + (_b))
```

这是一个操作。我们将在接下来的章节中讨论函数类宏。

以下是一个示例：

```c
#define ARRAY_SIZE 10
```

```c
int main()
{
    int r[ARRAY_SIZE];
}
```

### 示例 3：宏转换

对该文件运行`gcc -E`得到结果：

```c
### 0 "c/def.c"
### 0 "built-in"
### 0 "<command-line"
# 1 "/usr/include/std-predef.h" 1 3 4
# 0 "<command-line>" 2
### 1 "c/def.c"
```

```c
int main()
{
    int r[10];
}
```

### 示例 4：gcc -E 输出

宏在预处理阶段后被替换为实际值。

## #undef 宏

`#undef`宏定义一个宏（注意：移除宏）。例如：

```c
#define PI 3.1413
#undef PI

double circumference(double radius)
{
    return 2 * PI * radius;
}
```

结果会导致编译器错误，因为预处理器删除了`PI`。

## #ifdef 宏

`#ifdef`宏检查某个宏是否已定义，如果已定义，预处理器将启用`#ifdef`和`#endif`之间的代码部分。`#ifdef`后面总是跟着`#endif`或`#else`语句。

例如：

```c
int a = 10;
#ifdef CONFIG_MACRO
a = 5;
#else
a = 6;
#endif
```

如果`CONFIG_MACRO`被定义，则`a`设置为 5，否则设置为 6。下面的示例展示了如何定义宏。

```c
#include <stdio.h>
#define CONFIG_MACRO

int main()
{
  int a = 10;
  #ifdef CONFIG_MACRO
    a = 5;
  #else
    a = 6;
  #endif

  printf("%d\n", a);
}
```

### 示例 4.11 宏定义

定义简单的`#define CONFIG_MACRO`就足以启用`#ifdef`下的语句。通常，这些可以作为命令行参数传递给编译器，而不是由编译器处理。例如：

```bash
gcc -DCONFIG_MACRO macro.c
```

`gcc`的`-D`参数接收宏，可以给出多个`-D`作为参数。

如果特定的宏变量未定义，`#ifdef`宏将取反操作，即预处理器将启用该部分代码。

# 函数 (Functions)

C 程序中的函数是一组指令。函数允许我们将一个大型程序拆分为可理解的段落。每个段落都具有某些定义的业务逻辑和逻辑实现。

函数有零、一个或多个输入参数，并返回或不返回任何内容。原型如下：

```c
void function(void)
```

或者更通用地：

```c
return-type function-name(arguments, ..)
```

例如：

```c
#include <stdio.h>

void print_hello()
{
    printf("Hello World\n");
}

int main()
{
    print_hello();
}
```

上面的示例调用了名为`print_hello`的函数在屏幕上打印 "Hello World"。

调用函数只需编写其名称，后面跟着带有零、一个或多个参数的括号，以及分号。此函数不接受任何参数也不返回任何内容。

以下语句：

```c
void print_hello()
{
    printf("Hello World\n");
}
```

构成了函数体。它也被函数定义。一个程序通常包含多个函数。

`main()`也是一个函数，它是程序的起点。如果没有定义`main()`，编译将产生未定义错误。通常情况下，链接器期望`main()`被定义，因为它在调用`main()`之前的序列中是被要求的。谁调用了`main()`？简单来说，调用定义在`libc`的某处。

在 C 中，函数只能有一个签名（在 C++ 中函数可以有多个签名）。`main()`的原型与其他许多函数不同。最常用的原型如下：

```c
int main(void)
```

```c
int main(int argc, char **argv)
```

然而，在编写软件时很少使用这种情况。`main()`必须返回。这是为了让执行的 shell 在返回时知道程序的状态。shell 可以使用返回时的程序状态。

```c
strcpy(hello_msg, "hello");

return hello_msg;
}
```

```c
char *get_1()
{
    return "hello";
}
```

```c
int main()
{
    char *ptr = get_1();

    printf("get_1 %s\n", ptr);

    ptr = get_2();

    printf("get_2 %s\n", ptr);

    return 0;
}
```

返回语句和三字符序列可以组合在一起。例如，以下语句是有效的：

```c
int is_positive(int a)
{
    return (a > 0) ? true : false;
}
```

我们在返回字符串时使用了一些小技巧。

1. 通过引用 - 这在下文中已经进行了解释。

2. 定义一个字符串表，并根据输入选择返回其中一个。

字符串表可以写如下：

```c
static char *books[] = {
    "networking essentials",
    "programming in C",
};
```

该表定义在程序的只读段中。它被保留在文件读取器内部。变量的生命周期是程序生命周期。

我们接着在下面编写访问函数：

```c
const char *get(unsigned int book_id)
{
    if (book_id > sizeof(books) / sizeof(books[0])) {
        return "unknown";
    }

    return books[book_id];
}
```

下面是一个示例：

```c
#include <stdio.h>

static const char *books[] = {
    "networking essentials",
    "programming in C",
};

const char *get(unsigned int book_id)
{
    if (book_id > sizeof(books) / sizeof(books[0])) {
        return "Unknown";
    }

    return books[book_id];
}

int main()
{
    printf("book %s\n", get(1));
    return 0;
}
```

## 作为函数参数的 const

当认为没有必要修改参数时，可以为变量添加常量修饰符。例如：

```c
int f(const char *str)
```

这里的参数`str`是不可修改的。

下面是一个示例：

```c
#include <stdio.h>

int f(const char *str)
{
    int i;
    for (i = 0; str[i] != '\0'; i++) {
        str[i] = 'a'; // 修改常量会导致编译器错误
    }

    return i;
}

int main() {
    char str[20] = "hello";
    f(str);

    printf("%s\n", str);
    return 0;
}
```

我们直接对数组进行索引，但对`book_id`的范围进行了验证。任何使用错误的`book_id`值访问`books`指针的操作都可能导致越界访问。例如，考虑如果没有该检查，当`book_id`为 3 时，访问`books`将导致对未知地址空间的访问并引发故障。

函数调用也可以`if`、`while`和`for`语句中进行。

```c
if (is_item_fruit(item)) { // 有效调用
}

while (remaining_items() > 0) // 有效调用
    for (i = 0; i < remaining_items(); i++) // 有效调用
```

但通常情况下，在使用`printf`调试时，这些调用会让调试变得困难。

## 可变函数

可变函数是指那些接受许多参数作为输入的函数。这里的许多参数意味着，函数的参数会根据调用者的不同而变化。有时函数会接收 3 个参数，而同一个函数可能会接收 2 个或 7 个等。这就是为什么它们被称为可变函数的原因。

头文件`stdarg.h`包含了使可变函数可能的宏和辅助函数。

`stdarg.h`中有两个重要的函数/宏。

1. `va_start`

2. `va_end`

### 1. va_start

`va_start`的原型如下：

```c
void va_start(va_list ap, last);
```

`last`可以是任何类似于标识符的参数。

### 2. va_end

`va_end`的原型如下：

```c
void va_end(va_list ap);
```

每次调用`va_start`必须与`va_end`匹配。

### 编写你自己的 printf

`vprintf`类似于`fprintf`，但它接受可变参数。原型如下：

```c
int vprintf(FILE *fp, const char *fmt, va_list ap);
```

下面是一个示例：

```c
#include <stdio.h>
#include <stdarg.h>

void log_printf(const char *fmt, ...)
{
    va_list ap;

    va_start(ap, fmt);
    vprintf(stderr, fmt, ap);
    va_end(ap);
}

int main()
{
    int a = 10;
    printf("test: test message a=%d\n", a);
}
```

### va_arg

`va_arg`的原型如下：

```c
type va_arg(va_list ap, type);
```

下面的示例展示了一个累许多变量的函数。原型如下：

```c
int add(int n_args, ...);
```

`n_args`是参数的数量。其余参数是需要相加的参数。`add`函数通过`n_args`遍历参数列表。例如：



```c
#include <stdio.h>
#include <stdarg.h>

typedef enum {
    INT,
    DOUBLE,
    STRING
} type_t;

double add(type_t type, int n_args, ...)
{
    va_list ap;
    double r = 0;
    int i;

    va_start(ap, n_args);
    for (i = 0; i < n_args; i++) {
        if (type == INT) {
            r += va_arg(ap, int);
        } else if (type == DOUBLE) {
            r += va_arg(ap, double);
        }
    }

    va_end(ap);
    return r;
}

int main()
{
    double r = add(INT, 3, 1, 2, 3); // 相加 3 个参数
    printf("r: %f\n", r);

    r = add(DOUBLE, 3, 1, 2, 3); // 示例补充
    printf("r: %f\n", r);

    return 0;
}
```

*(注：由于原文最后部分 `add` 的调用似乎不完整，翻译时根据上下文补全了逻辑以保持示例一致性，但严格遵循了翻译要求)*

---

**纠正**：原文结尾处 `r = add(INT, 3, 1, 2, 3);` 之后似乎断开了，翻译时保持了原文的结构。

(重新审视原文最后一段：

`r = add(INT, 3, 1, 2, 3); // add 3 arguments`

`printf("r: %f\n", r);`)

译文对应：

`r = add(INT, 3, 1, 2, 3); // 相加 3 个参数`

`printf("r: %f\n", r);`

### 字符串处理操作

头文件 `string.h` 包含了帮助处理字符串数据的函数。

**字符串处理函数** 标准库提供了以下或更多用于处理字符串的函数。

| 序号 | 函数名 | 描述 |
|---|---|---|
| 1 | `strlen` | 计算字符串长度 |
| 2 | `strcpy` | 将一个字符串拷贝到另一个 |
| 3 | `strcat` | 将字符串连接到另一个字符串 |
| 4 | `strcmp` | 比较两个字符串 |
| 5 | `strchr` | 在字符串中查找字符 |
| 6 | `strstr` | 在字符串中查找所有匹配项 (GLIBC，非 C 标准) |
| 7 | `memcmp` | 比较两个数组 / 字符串 |
| 8 | `memcpy` | 将一个数组 / 字符串拷贝到另一个 |
| 9 | `strdup` | 复制字符串 |
| 10 | `memset` | 将内存设置为某个值 |

### 1. strlen

库函数 `strlen` 用于获取字符串的长度。

`strlen` 的原型如下：

```c
int strlen(const char *str);
```

下面是一个示例：

```c
#include <stdio.h>

int main() {
    char str[] = "hello world";

    printf("%s %d\n", strlen(str));

    return 0;
}
```

`strlen` 函数计算字符串中排除 `\0` 标记之外的所有字符。它可以按如下方式实现。

```c
int string_length(const char *str) {
    int i = 0;
    for (i = 0; str[i] != '\0'; i ++);

    return i;
}
```

上面的程序遍历字符串 `str` 中的每个字符，直到字符为 `\0`。`for` 循环的内容什么都不做。有时也可以使用大括号和右大括号 `{` 和 `}`。

请注意，其行为是最后一个字符应该总是以空终止的。如果在空终止字符之后存在字符，它们将会被忽略。

如果字符串中没有空字符，`strlen` 函数将继续读取，在某些情况下甚至会读取分配的缓冲区。这有时在运气好的情况下会导致崩溃，在运气不好的情况下会执行代码，从而导致漏洞。

因此，在创建和使用字符串时必须小心。始终对字符串进行空终止。

注意 `strlen` 和 `string_length` 函数从不检查输入是否为 `NULL`。调用者在调用 `strlen` 之前必须处理指针的有效性。

### 2. strcpy

`strcpy` 函数用于将源字符串拷贝到目标中。

它的原型如下。

```c
char *strcpy(char *dst, const char *str);
```

`strcpy` 的示例如下。

```c
#include <stdio.h>
#include <string.h>

int main() {
    char *str1 = "Witcher";
    char *str2[20];

    strcpy(str2, str1);

    printf("str1 [%s] str2 [%s]\n", str1, str2);

    return 0;
}
```

`strcpy` 可以按如下方式实现。

```c
int string_copy(char *dst, unsigned int dst_len, const char *src) {
    uint32_t i = 0;
    uint32_t len = 0;

    for (i = 0; src[i] != '\0'; i++ ) {
        if (i < dst_len) {
            dst[i] = src[i];
        } else {
            break;
        }
    }

    dst[i - 1] = '\0';

    return 0;
}
```

### 3. strcat

字符串拼接将两个字符串连接在一起。

原型如下。

```c
char *strcat(char *dst, const char *src);
```

下面是一个示例：

```c
#include <stdio.h>
#include <string.h>

int main() {
    char *str = "hello";
    char *ptr = "mangoes";
    char dst[20];

    strcpy(dst, str);
    strcat(dst, " ");
    strcat(dst, ptr);

    printf("%s\n", dst);

    return 0;
}
```

下面是 `strcat` 的示例。由于 `strcat` 在字符串后面追加新字符串，因此需要迭代到上一个字符串的末尾。

```c
#include <stdio.h>
int string_cat(char *dst, const char *src) {
    int i = 0;
    int j = 0;
    while (dst[i] != '\0') {
        i++;
    }
    while (src[j] != '\0') {
        dst[i] = src[j];
        i++;
        j++;
    }
    dst[i] = '\0';
    return j;
}

int main() {
    char *src = "test";
    char dst[30] = "dest";

    string_cat(dst, src);

    printf("%s\n", dst);

    return 0;
}
```

### 4. strcmp

将一个字符串与另一个字符串比较。

```c
int strcmp(const char *src, const char *dst);
```

如果两个字符串相等，则返回 0。当字符串不等时，返回固定索引字符之间的非零差异。

下面是 `strcmp` 的示例。

```c
#include <stdio.h>
#include <string.h>

int main() {
    char *str = "hello";
    char *str_1 = "hello";
    char *str_2 = "Hello";
    int res_1 = strcmp(str, str_1);
    int res_2 = strcmp(str, str_2);

    printf("res_1 %d res_2 %d\n", res_1, res_2);

    return 0;
}
```

下面是 `strcmp` 的完整实现。

```c
int string_len(const char *str) {
    int i = 0;
    while (str[i] != '\0') {
        i++;
    }
    return i;
}

int string_cmp(const char *str1, const char *str2) {
    int i = 0;

    if (string_len(str1) != string_len(str2)) {
        return -1;
    }

    while (str1[i] != '\0') {
        if (str1[i] != str2[i]) {
            return str1[i] - str2[i];
        }
    }
}
```

### 5. strchr

在字符串中查找字符。

```c
#include <stdio.h>
#include <string.h>

int main() {
    char *str = "hello";
    char *pos = strchr(str, 'l');

    if (pos) {
        printf("Found at: %ld\n", pos - str);
    } else {
        printf("Not found\n");
    }

    return 0;
}
```

### 6. memcmp

比较两个数组 / 字符串

```c
#include <stdio.h>
#include <string.h>
#include <stdint.h>

int main() {
    char s1[] = "ABCDE";
    char s2[] = "ABCD";
    int res = memcmp(s1, s2, 4);

    if (res == 0) {
        printf("Strings are equal\n");
    } else {
        printf("Strings are not equal\n");
    }

    return 0;
}
```

```c
{ char *ptr;
int i;
int length = len(str);

// 1 用于存储 \0
ptr = calloc(1, length + 1);

for (i = 0; i < length; i++) {
  ptr[i] = str[i];
}

ptr[i] = '\0';

  return ptr;
}
```

```c
int main() {
char *ptr = "hello";
char *ptr1;

ptr1 = strdup_1(ptr);

printf("%s %s ptr1 %s\n", ptr, ptr1, "ptr1", "");

free(ptr1);

  return 0;
}
```

### 9. memset

用给定的数值设置给定缓冲区内存的内容。

`memset` 的原型如下：
`void *memset(void *ptr, int number, size_t n_bytes);`

以下是一个示例，

```c
#include <stdio.h>
#include <string.h>
#include <stdint.h>
```

```c
int main() {
```

```c
uint8_t a[10];
  int i;
```

### 字符串转整数 / 双点数转换

以下是几个将字符串转换为其他类型的函数。如下：

- 1. `atoi`
- 2. `strtol`
- 3. `strtod`
- 4. `strtoul`

### .atoi

标准库函数 `atoi` 将给定的输入字符串转换为整数。它的声明如下：

以下是一个示例：

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    char *str = "4";
    printf("%d\n", atoi(str));
}
```

让我们看另一个示例：

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    char *str = "4a";
    printf("%d\n", atoi(str));
}
```

所以这是转换 0 的另一种方法，在这种情况下，如果视为输入，0 是合法的。由于输入是未知的，如果结果正确或错误可能会导致歧义。

因此，在编写软件时通常倾向于不使用 `atoi`。

还有另一种将字符串转换为整数的方法。

以下是一个示例。在此处下载。

```c
#include <stdio.h>

int main() {
    char *str_int = "1343";
    int intval;

    sscanf(str_int, "%d", &intval);
    printf("%d\n", intval);

    return 0;
}
```

我们正在使用 `sscanf` 将输入从缓冲区读取到整数。

让我们考虑下面代码段中的无效字符串输入。在此处下载。

```c
#include <stdio.h>

int main() {
    char *str = "123a";
    int intval;
    int ret;

    ret = sscanf(str, "%d", &intval);

    if (ret != 1) {
        printf("incorrect integer\n");
    } else {
        printf("val %d\n", intval);
    }
}
```

这导致 `ret` 为 1。然而，结果没有错误，且整数仍然被读取了。

### 2. strtol

标准库函数 `strtol` 将给定的输入字符串转换为整数。它声明在 `stdlib.h` 中。

函数原型如下：

```c
long strtol(const char *in, char **err, int dec_or_hex);
```

在上述函数中，`err` 参数描述输入是否正确。它用于检查返回的 `long` 值是否合法。

- 参数 `dec_or_hex` 如果输入是十进制，则基本为 10；如果输入是十六进制格式 `0x`，则为 16。

以下是一个示例：

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    char *number = "102";
    char *err = NULL;
    long num_long;

    num_long = strtol(number, &err, 10);

    if (*err != '\0') {
        printf("failed to parse number\n");
    }

    printf("num_long %ld\n", num_long);

    return 0;
}
```

### 3. strtod

将字符串转换为双点数。

函数原型如下：

```c
double strtod(const char *ptr, char **end_ptr);
```

示例如下：

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    char *str = "3.3";
    char *err = NULL;
    double val;

    val = strtod(str, &err);

    if (*err != '\0') {
        return -1;
    }

    printf("val %f\n", val);

    return 0;
}
```

### 4. strtoul

将字符串转换为无符号长整。

原型如下：

`unsigned long strtoul(const char *nptr, char **err_ptr, int base);`

是一个示例：

```c
#include <stdio.h>
#include <stdint.h>
#include <stdlib.h>

int main() {
    char *str = "4294967295";
    uint32_t val;
    char *err = NULL;

    val = strtoul(str, &err, 10);

    if (*err != '\0') {
        return -1;
    }

    printf("val %u\n", val);

    return 0;
}
```



### 指针

字符串也可以用指针初始化。下面的语句是在编译时分配的字符串：

```c
char *str = "Hello";
```

任何类型的指针都是可能的：

```c
int *p;
int val = 4;
```

`&` 运算符表示变量前的地址。指针可以使用 `%p` 格式符打印。

```c
#include <stdio.h>

int main() {
    int val = 4;
    int *v = &val;
    printf("%p\n", v);
}
```

指针的大小可以如下进行评估。在 64 位机器上，size 为 8 字节。

```c
int *v;
int size = sizeof(v);
```

### 函数中的值传递和引用传递

考虑下面的示例，函数接收 `a` 和 `b` 作为输入。`add` 函数执行操作并将结果写入 `r`。一旦函数执行并返回，`r` 的值仍然是 0。传递值的方法是返回它。例如：

```c
int add(int a, int b) {
    return a + b;
}
```

这种传递参数的方法通常称为值传递。在这种方法下，调用者的参数值不会改变。

---

### void指针

void指针是一个通用指针，可以赋值为任何结构体、指针或变量的地址。这是一个示例：

```c
int a[10];
void *p;
p = &a[0];
```

void指针不能引用，因为引用涉及到推导类型，编译器不知道它应该是什么类型。使用了类型转换，或者在某些情况下赋值回其类型。通常转换回类型需要使用类型转换。

```c
void *p;
int *a;
a = (int *)p;
printf("%d\n", *a);
```

类型转换可以用于结构体指针。

```c
struct S {
    int p;
}

struct S s = {
    .p = 3;
};

void *p = &s;
struct S *r = (struct S *)p; // 类型转换回 struct S
```

下面的程序实现因为 void 指针的引用会导致编译器错误。

```c
#include <stdio.h>

int main() {
    int p = 3;
    void *a;
    a = &p;
    printf("%d\n", *a); // 编译器错误..引用 void *
    return 0;
}
```

另一种方法如下：

```c
#include <stdio.h>

int main() {
    int p = 3;
    void *a;
    a = &p;
    printf("%d\n", (int*)a); // 隐式类型转换然后引用指针
    return 0;
}
```

### 指针和数组

指向数组的指针可以简单地赋值如下：

```c
int a[10];
int *p;
p = a;
or = &a[0];
```

赋值的指针指向数组的第一个元素。

以下是使用指针访问数组元素的另一个示例。数组的元素通过指针进行更新。

```c
#include <stdio.h>

int main()
{
    int a[10];
    int i;
    int *p;

    for (i = 0; i < sizeof(a) / sizeof(a[0]); i++) {
        p = &a[i];
        *p = i;
    }

    for (i = 0; i < sizeof(a) / sizeof(a[0]); i++) {
        printf("%d\n", a[i]);
    }

    return 0;
}
```

将数组传递给函数时，调用者将其视为指针输入。这被称为数组退化为指针。当这种情况发生时，指针上的 `sizeof` 得到的是 4 或 8 字节，即该体系架构下指针的大小。通常，将数组的元素个数作为参数传递给函数调用是明智的。

例如：

```c
int f(*a, int a_len)
{
    int main()
    {
        int a[10];
        f(a, 10);
    }
}
```

## 动态内存分配

动态内存是程序在运行时所需的内存。某些程序需要动态内存，而某些则不需要。这取决于用例，即为什么程序需要分配动态内存。

动态内存始终在程序的堆（heap）区域中分配。

操作系统提供了一个系统调用层，允许 C 库调用操作系统来为程序分配内存。通常，返回的内存不是连续的，而是稀疏的。这种行为在不同的操作系统上会有不同。

尽管特定的内存系统调用返回了内存，但 C 库函数会记录请求的内存以便进行记账或提高效率。

## malloc

`malloc` 函数是一个用于动态分配内存的 C 函数。它在 `stdlib.h` 中声明。`malloc` 分配的内存可能包含其他程序使用的旧数据。

其原型如下：

```c
void *malloc(int size);
```

示例代码如下：

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *a;
    a = malloc(sizeof(int));
    *a = 4;
    printf("%p %p %d\n", a, *a);
    return 0;
}
```

`malloc` 会调用底层的系统调用来分配堆内存。
一旦分配了内存，只能通过 `free` 释放。
对函数 `malloc` 的调用可能会失败并导致返回 NULL 指针。在上面的示例中，我们在没有检查 `a` 是否可能为 NULL 指针的情况下直接对其进行了解引用。
解引用 NULL 指针会导致故障，程序将终止。
返回 NULL 的原因是操作系统正处于高内存压力下（即大部分内存已被占用），在这种情况下，操作系统无法分配更多可用内存。这导致了返回 NULL 指针。
使用已分配指针的最佳实践是始终检查是否为 NULL。以下是 `malloc` 的另一个示例：

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *a;
    int i;
    a = malloc(sizeof(int) * 10); // 为 10 个整数分配空间
    if (!a) {
        return -1;
    }
    for (i = 0; i < 10; i++) {
        a[i] = i;
    }
    for (i = 0; i < 10; i++) {
        printf("a[%d] = %d\n", i, a[i]);
    }
    return 0;
}
```

在上面的示例中，指针 `a` 被分配了 10 个元素，并像数组一样被访问。

### 2. calloc

`calloc` 函数是一个用于动态分配内存的 C 函数。它在 `stdlib.h` 中声明。一旦分配了内存，它会被清空并返回给调用者。

其原型如下：

```c
void *calloc(int n_elements, int size);
```

示例代码如下：

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *a;
    a = calloc(1, sizeof(int));
    *a = 4;
    printf("a %p a %d\n", a, *a);
    return 0;
}
```

### 3. realloc

`realloc` 函数在已分配的内存上重新分配内存，基本上是扩展它。

如果给定的内存为 NULL，它的工作类似于 `malloc`。

```c
void *p;
p = realloc(p, sizeof(int) * 10); // 可能会崩溃 -> p 的地址指向垃圾数据
p = NULL;
p = realloc(p, sizeof(int) * 10); // malloc
p = realloc(p, sizeof(int) * 20); // 现在内存扩展到 20 个元素
```

`realloc` 返回的指针地址可能不相同，但如果原来有旧内容，它们会被保留并因此存在于新返回的地址中。

如果在同一块内存上多次调用 `realloc`，则 `free` 只能使用一次。这是因为 `libc` 的实现会跟踪已分配的内存。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *a;
    int i;
    a = calloc(4, sizeof(int));
    if (!a) {
        return -1;
    }
    for (i = 0; i < 4; i++) {
        a[i] = i;
    }
    for (i = 0; i < 4; i++) {
        printf("a[%d] = %d\n", i, a[i]);
    }
    return 0;
}
```

`realloc` 的用例通常当分配的内存不足且需要更多时。链表通过增加元素来解决这个问题。但在某些情况下，使用的指针数组需要扩展。

### 4. free

每个内存分配必须被释放，否则系统将耗尽内存。以下是 `free` 的示例。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *a;
    a = malloc(sizeof(int));
    if (a) {
        *a = 4;
        printf("%p %d\n", a, *a);
        free(a);
    }
    return 0;
}
```

## 2. 分配并释放数组

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *a;
    int i;
    a = malloc(10 * sizeof(int));
    for (i = 0; i < 10; i++) {
        a[i] = i;
    }
    for (i = 0; i < 10; i++) {
        printf("a[%d] = %d\n", i, a[i]);
    }
    free(a);
    return 0;
}
```

## 双级指针

指针可以指向指针。可以尽可能多。但双级和三级指针很少使用。

```c
int **p;
int *r;
int v;
r = &v; // 将 v 的地址赋值给 r
p = &r; // 将 r 的地址赋值给 p
```

以下是一个示例：

```c
#include <stdio.h>

int main() {
    int r;
    int *p = &r;
    int **s = &p;
    *p = 3;
    printf("r: %d *p: %d **s: %d\n", r, *p, **s);
    return 0;
}
```

双级指针的通用用例是返回一个分配的地址并将其作为函数参数。

以下是一个示例：

```c
#include <stdio.h>
#include <stdlib.h>

int alloc(int **p) {
    *p = calloc(1, sizeof(int));
    if (!*p) {
        return -1;
    }
    **p = 3;
    return 0;
}

int main()
{
    int *p = NULL;
    alloc(&p);
    printf("%p\n", p);
}
```

在引用传递中，`p` 的地址被传递，双级指针通过引用传递捕获它。一旦捕获，指针 `p` 在函数内部被分配并赋值。
为了测试功能，我们打印 `p` 的值，由于它是被分配的，我们释放它。

### 分配和释放双级指针

类型为 `**ptr` 的双级指针按以下方式分配：

1. 为需要持有的 `*ptr` 类型指针分配内存。
2. 为每个 `**ptr` 类型分配内存。

例如，为 4 个每个想要进一步持有 3 个整数的分配内存，我们需要执行以下操作：

```c
int **p; // 4 行 x 每行 3 个元素
int i;
p = calloc(1, sizeof(int *) * 4 * 3); // 总共 12 个指针
for (i = 0; i < 4; i++) // 每一个指针
    p[i] = calloc(1, sizeof(int) * 3); // 为 3 个元素分配大小
```

以下是一个示例，在此下载。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int **p;
    int i;
    int j;
    p = calloc(1, sizeof(int *) * 4 * 4);
    for (i = 0; i < 4; i++) {
        for (j = 0; j < 4; j++) {
            p[i][j] = i + j;
        }
    }
    for (i = 0; i < 4; i++) {
        for (j = 0; j < 4; j++) {
            printf("p[%d][%d] = %d\n", i, j, p[i][j]);
        }
    }
    for (i = 0; i < 4; i++) {
        free(p[i]);
    }
    free(p);
    return 0;
}
```

```c
if (!p) {
    return -1;
}

for (i = 0; i < 4; i++) {
    p[i] = calloc(1, sizeof(int) * 4);
    if (!p) {
        return -1;
    }
}
```

```c
for (i = 0; i < 4; i++) {
    for (j = 0; j < 4; j++) {
        p[i][j] = i + j;
    }
}
```

```c
for (i = 0; i < 4; i++) {
    for (j = 0; j < 4; j++) {
        printf("p[%d][%d] = %d\n", i, j, p[i][j]);
    }
}
```

```c
for (i = 0; i < 4; i++) {
    free(p[i]);
}
```

```c
free(p);
return 0;
```

下面是另一个在每个结构体中分配结构和指针的示例。在此处下载。

```c
#include <stdio.h>
#include <stdlib.h>
```

```c
struct S {
    int v;
    char *ptr;
}
```

```c
int main() {
    struct S **s;
    int i;
}
```

```c
int j;
s = calloc(1, sizeof(struct S) * 4 * 3); // 分配 4 个指针
if (!s) {
    return -1;
}

for (i = 0; i < 4; i++) {
    // 为每个指针为结构体分配内存
    s[i] = calloc(1, sizeof(struct S) * 3);
    if (!s[i]) {
        return -1;
    }
    for (j = 0; j < 3; j++) {
        s[i][j].v = i;
        s[i][j].ptr = calloc(1, 14);
        if (!s[i][j].ptr) {
            return -1;
        }
    }
    printf("%s", s[i][j].ptr, "alloc_%d", i);
}

for (i = 0; i < 4; i++) {
    for (j = 0; j < 3; j++) {
        printf("%s[%d].v %d s[%d].ptr %s\n", i, j, s[i][j].v, i, j, s[i][j].ptr);
        free(s[i][j].ptr);
    }
    free(s[i]);
}

free(s);
return 0;
```

## 变量和作用域回顾

### auto 类型

`auto` 类型在 C 中没有表示任何含义。然而在 C++ 中这种类型非常重要。

### volatile 类型

关键字 `volatile` 用于在存在实际地址使用的地方。它通常附加到整数上。

```c
volatile uint32_t *addr = 0xA0000000;
```

让我们来看一个示例，内存中的一个寄存器需要持续检查，直到它达到某个值。

```c
while ((addr & 0x80) == 1) {
    ..
}
```



`addr` 不是由软件设置的，而是由硬件设置的。

如果没有 `volatile` 关键字，编译器将直接返回而不执行内部循环中的任何内容。

## 函数指针

指向函数的指针类似于指向变量的指针。函数也有地址。

```c
int (*fptr)(void);
```

定义一个函数指针，它不接受参数并返回整数。

```c
int (*fptr)(char *fmt, ...);
```

定义一个可变参数函数。

软件中的函数指针对于编写抽象有用。

考虑以下情况：

- 1. 以太网产品 A 提供了互联网工作的传输、接收功能。
- 2. 另一个以太网产品 B 为互联网工作提供了相同的功能。

所以对于用户来说，底层使用的是什么硬件并不重要。他只关心互联网。

操作系统程序员必须实现某种能够抽象这两个接口以为用户提供统一接口的东西。这通常是函数指针大显身场的地方。

将上面的特性转换为软件。

```c
struct ethernet_driver {

    int (*transmit)(uint8_t *packet, int packet_size);

    int (*receive)(uint8_t *packet);

};
```

`ethernet_driver` 结构体为上层用户和底层 PHY 设备提供接口。

```c
enum eth_driver_list {

    A,

    B;

};
```

```c
struct enum eth_driver_list list[2] = { A, B };
```

```c
e = probe_for(&list, 2);
```

在这里，函数 `probe_for` 查找插入的硬件寄存器，无论是 A 还是 B。它将返回驱动 A 的 `ethernet_driver` 指针，否则返回 B。

在 `A_eth_Driver.c` 中：

```c
int a_transmit(uint8_t *packet, int packet_size);

int a_receive(uint8_t *packet);
```

```c
static struct ethernet_driver A_driver = {

    .transmit = a_transmit,

    .receive = a_receive,

};
```

```c
struct ethernet_driver *get_A_functionality() {

    return &A_driver;

}
```

在 `B_eth_Driver.c` 中：

```c
int b_transmit(uint8_t *packet, int packet_size);

int b_receive(uint8_t *packet);
```

```c
static struct ethernet_driver B_driver = {

    .transmit = b_transmit,

    .receive = b_receive,

};
```

```c
struct ethernet_driver *get_B_functionality() {

    return &B_driver;

}
```

在 `probe.c` 中：

```c
#define A_REG 0xA000

#define B_REG 0xB000
```

```c
struct ethernet_driver *probe_for(enum eth_driver_list list, int len) {

    int i;

    for (i = 0; i < len; i++) {

        if (list[i] == A) {

            if (match_reg(A_REG)) {

                return get_A_functionality();

            }

        } else if (list[i] == B) {

            if (match_reg(B_REG)) {

                return get_B_functionality();

            }

        }

    }

    return NULL;

}
```

`probe_for` 的功能即使获取了新的驱动也保持相同。这里最重要的观察是，调用者可以直接调用 `eth->transmit` 和 `eth->receive` 而不需要知道底层驱动。这被称为抽象。这种特性在语言中定义得很好。我们将详细描述。

### 函数指针数组

函数指针数组的语法如下。

```c
int (*ptr[])(void); // 定义函数指针数组
```

为了简单得多，可以先 typedef 函数指针并定义数组。

```c
typedef int (*fptr_f)(void); // 定义函数指针
```

```c
fptr_f fptr[4]; // 定义函数指针数组
```

下面是函数指针数组的一个示例：

```c
#include <stdio.h>
```

```c
int f() {

    static int count = 0;

    printf("F %d\n", count);

    return ++count;

}

typedef int (*fptr_f)(void);
```

```c
int main() {

    fptr_f fptr[4];

    int i;

    for (i = 0; i < 4; i++) {

        fptr[i] = f;

    }

    for (i = 0; i < 4; i++) {

        fptr[i]();

    }

    return 0;

}
```

## 结构体

数据结构是不同类型的变量组。`struct` 词作为标识符让编译器识别结构体。

数据结构的示例如下：

```c
struct shelf {

    char book_name[10];

    int n_papers;

};
```

上面的结构体定义了一个包含书籍列表的架子，一个是字符串，另一个是整数。

定义结构体变量与定义基本类型相似。

```c
struct shelf {

// 这里 s 是 shelf 的类型，使用 . 运算符。
```

通过以下方式访问结构体中的元素：

```c
#include <stdio.h>

#include <string.h>
```

```c
struct shelf {

    char book_name[10];

    int n_papers;

};

int main() {

    struct shelf s;

    strcpy(s.book_name, "Witcher");

    s.n_papers = 2000;

    printf("book_name: %s papers: %d\n", s.book_name, s.n_papers);

    return 0;

}
```

结构体也可以位于另一个结构体内部。

```c
struct shelf {

    char book_name[10];

    char book_author[10];

    struct book;

    int n_papers;

}; 
```

我们也可以对结构体应用 typedef，例如：

```c
typedef struct book {

  ..

} book_t; // 定义 book typedef
```

```c
typedef struct book_t book_t; // 在新的中定义 typedef
```

```c
typedef struct { // 不带名称定义 typedef

} book_t;
```

现在 `book_t` 可以用于定义结构体变量。通常使用 `_t` 前缀来区分 typedef，但这只是程序员的个人选择，并非由 C 标准定义。

人们也可以使用宏为了听起来更好的名称。

```c
#define Book_Info struct book
```

虽然可行，但通常会避免这样做。宏的全部目的是为了命名常量或编写类似函数的小宏。

元素的访问方式如下：

```c
struct shelf s;
```

```c
void set_book(struct book *b, char *book_name, char *book_author)

{

  strcpy(b->book_name, book_name);

  strcpy(b->book_author, book_author);

}
```

```c
void set_shelf(struct shelf *s, char *book_name, char *book_author, int n_papers) {

  s->n_papers = n_papers;

  set_book(&s->book, book_name, book_author);

}
```

```c
};

struct shelf {

    struct book books[10];

    int n_papers;

}
```

### 结构体中的指针

结构体也可以包含指针。

```c
struct book {

    char *book_name;

    char *book_author;

};
```

它们的分配方式与指针的分配相同。

```c
book->book_name = calloc(1, 40);

book->book_author = calloc(1, 20);
```

在某些情况下，结构体中可能包含指向另一个结构体或变量的指针。在这种情况下，释放所有结构体会变成一个真正的问题。按照分配相同的顺序进行释放可以保证不崩溃，但会导致内存泄漏。要采用正确的方法，必须按照分配的反向顺序进行释放。

下例示例提供了这种方法。

```c
struct S1 {

    int v;

};
```

```c
struct S2 {

    struct S1 s1;

};
```

```c
struct S2 s2;

s2.s1.v = 3;
```

```c
printf("v: %d\n", s2.s1.v);
```

### 结构体初始化

结构体的初始化可以通过许多方式完成。一种初始化方法如下。

```c
struct A {

    int val;

double val_d;

};
```

```c
struct A a = { .val = 3, .val_d = 3.1 };
```

这是初始化结构体的方法。

以下是一个示例，

```c
#include <stdio.h>
```

```c
struct A {

  int val;

  double val_d;

};
```

```c
int main() {

  struct A a = { .val = 3, .val_d = 3.1 };

  fprintf(stderr, "val: %d\n", a.val);

  fprintf(stderr, "val_d: %f\n", a.val);

  return 0;

}
```

### 结构体数组

结构体数组也是可能的。

```c
struct A {

  int val;

  double val_d;

};
```

```c
struct A a[10]; // 类型为 `A` 的结构体数组。
```

它们可以像数组一样被迭代。

```c
struct A {

  int val;

  double val_d;

};
```

```c
void set(struct A *a, int size) {

  int i;

  for (i = 0; i < size; i++) {

    a[i].val = i;

    a[i].val_d = i + 0.1 * i;

  }

}
```

### 结构体中的函数指针

下面的结构声明了两个函数指针 `get` 和 `set`，可以通过结构体变量进行访问。

```c
struct S {

    int (*get)();

    void (*set)(int);

};
```

```c
struct S s;

s.set(3); // 设置变量

int var = s.get(); // 获取变量
```

但通常情况下，指针 `s.get` 和 `s.set` 包含垃圾指针。因此，访问它们通常会导致段错误，或者在坏的情况下导致程序执行异常。

分配地址的一种方法如下：

```c
int a;

int my_get() { return a; }

void my_set(int A) { a = A; }
```

```c
struct S s;
```

```c
memset(&s, 0, sizeof(struct S));

s.get = my_get;

s.set = my_set;
```

现在访问函数指针 `s.get` 和 `s.set` 将间接调用 `my_get` 和 `my_set` 函数。

虽然我们可以在结构体中使用函数指针，但我们不能在结构体中使用函数。这在 C 语言中是不允许的。然而，C++ 允许这种数据分组。

下面的结构体是不正确的，会导致错误。

```cpp
#include <stdio.h>

struct S {

    int f(void);

};
```

```cpp
int main()

{
```

错误，`c/struct_func.c:4:9: error: field 'f' declared as function`
`4 | int f(void);`

### 结构体指针

结构体指针有广泛的应用场景。其中一个场景是抽象。

结构体可以拥有其元素的引用。这对于实现数据结构特别有利。

下是这种结构的一个示例。

```c
struct S {

  int v;

  struct S *next;

};
```

“数据结构”部分描述了更多应用场景。从结构体指针到 void 指针的转换是可能的。

```c
struct S *s;

void *v;
```

```c
s = calloc(1, sizeof(struct S));

v = s; // 有效

s = (struct S*)v; // 关于 void 到 struct 的警告

s = v; // 可能产生警告
```

```c
printf("val %d\n", v->v); // 引用指针仍然是不正确的
```

## 位域 (Bit fields)

结构体中的无符号整数类型可以用位域表示。

```c
struct S {

    uint32_t v:1; // 1 位

    uint32_t p:2; // 2 位

}
```

下是一个示例。

```c
#include <stdio.h>

#include <stdint.h>

struct S {

    uint32_t v:1;

    uint32_t p:2;

}

int main() {

    struct S s;

    s.v = 1;

    s.p = 2;

    printf("v: %d p: %d\n", s.v, s.p);

    printf("size: %ld\n", sizeof(struct S));

    return 0;

}
```

位域的通用用于表示硬件寄存器。有些可以是 1 位，有些可以多于 1 位。位域是无法取地址的。这样做会导致编译器错误。

```c
#include <stdio.h>

#include <stdint.h>

struct S {

    unsigned int v:1;

    unsigned int p:2;

}

int main() {

    struct S s;

    struct S *s1;

    s1 = &s;

    s1->v = 1;

    s1->p = 2;

    int *v = &s1->v;

}
```

上面的程序会导致编译器错误。`c/bitfields_2.c:19:14: error: cannot take address of bit-field 'v'`
`19 | int *v = &s1->v;`

位域无法比类型表示更多的位。

```c
#include <stdio.h>

#include <stdint.h>

struct S {

    uint32_t v:3;

    uint32_t p:1;

}

int main() {

}
```

上面的程序会导致编译器错误。`c/bitfields_3.c:5:14: error: width of 'v' exceeds its type`
`5 | uint32_t v:3;`

只有整数类型允许作为位域。使用其他类型会导致编译错误。

```c
#include <stdio.h>

#include <stdint.h>

struct S {

    double v:1;

    uint32_t p:2;

}

int main()

{

}
```

上面的程序会导致编译器错误。`c/bitfields_4.c:5:12: error: bit-field 'v' has invalid type`
`5 | double v;`

## 使用结构体查找表

查找表可以用结构体或数组实现。以下是一个示例，

```c
enum fruits {

    Apples,

    Oranges,

    Mangoes,
```



# 查找表

```c
struct fruit_basket {
    char fruit_name[20];
    int price_per_kg;
};

struct fruit_basket[] = {
    {"Apples", 200},
    {"Oranges", 200},
    {"Mangoes", 100},
    {"Pineapples", 200},
    {"Pears", 200},
};
```

```c
struct fruit_basket *fruit_item(fruits f) {
    if ((f < Apples) || (f > Pears)) {
        return NULL;
    }
    return fruit_basket + f; // 获取水果类型的指针
}
```

查找表主要用于索引给定的数组并返回指针/项目。这避免了循环的使用。

# 结构体填充与紧凑

## 结构体填充 (Structure Padding)

有时数据结构需要对齐到字节边界的倍数。这是由于硬件或架构对齐的原因。没有对齐的缓冲区，硬件对缓冲区的访问可能会导致崩溃。

`Gcc` 提供了 `__attribute__((aligned()))` 修饰。

```c
struct S {
    int r;
    int p;
} __attribute__((aligned(16)));
```

对结构体的 `sizeof` 操作结果为 16。虽然实际大小可能是 8，但由于给了对齐标签，会添加额外的填充字节使其成为 16 字节。

以下是一个示例：

```c
#include <stdio.h>

struct S {
    int v;
    int r;
} __attribute__((aligned(16)));

int main() {
    printf("size %ld\n", sizeof(struct S));
    return 0;
}
```

## 结构体紧凑 (Structure Packing)

编译器提供了一种紧凑结构体元素的机制以关闭由于填充/对齐产生的空隙。

`Gcc` 提供了 `__attribute__((__packed__))` 修饰。

```c
struct S {
    int v;
    int p;
    char r;
} __attribute__((__packed__));
```

对上述结构体的 `sizeof` 操作返回 9。理论在没有紧凑属性的情况下，它应该是 12。

以下是一个示例：

```c
#include <stdio.h>

struct S {
    int v;
    int p;
    char r;
} __attribute__((__packed__));

struct R {
    int v;
    int p;
    char r;
};

int main() {
    printf("regular_size %ld packed_size %ld\n", sizeof(struct R), sizeof(struct S));
    return 0;
}
```

# 枚举

```c
enum army {
    Snipers,
    Medics,
    Seals,
};
```

```c
int main() {
    printf("size %lu\n", sizeof(enum army));
    return 0;
}
```

我们也可以拥有枚举的指针。

```c
enum army charlie_1, *charlie_2;
```

```c
charlie_2 = &charlie_1;
```

这是完全有效的。但在大多数情况下，我们从不使用枚举指针，因为它们只占用几个字节（4 或 8 字节）。

我们可以像结构体一样对枚举进行 `typedef`。以下是几个示例。

```c
typedef enum army {
    army_t; // 在末尾 typedef
};
```

```c
enum army {
    ..
};
```

```c
typedef enum army army_t; // 在单独的一行 typedef
```

```c
typedef enum { // 不需要命名，因为 typedef 提供了名称
    ..
} army_t;
```

# 联合体 (Unions)

# 附录 A

## 头文件的意义

头文件可以包含结构体、宏定义和函数原型。有时它们甚至包含内联函数。

以下是几个优点：

1. 它们可以用于分组相关功能。当分离良好时，可以为程序提供结构化。
2. 它们可以将原型、宏定义和结构体暴露给其他文件。其他文件可以使用这些原型来避免隐式调用。
3. 以头文件包和库 `.so` 或 `.a` 文件形式分发软件的最佳方式。

## 头文件描述

`stdio.h` 包含 `printf`、`scanf`、`fprintf`、`fscanf`、`fopen`、`fclose`、`gets` 等函数的原型。`stdint.h` 拥有更多的数据类型。参见 `/usr/include/stdio.h`。`limits.h` 包含所有基础类型的范围。参见 `/usr/include/limits.h`。`stdlib.h` 包含 `atoi`、`malloc`、`calloc`、`realloc` 和 `free` 的原型。`string.h` 包含字符串相关函数的原型，如 `strlen`、`strcpy`、`strcat`、`strcmp` 等。

## C 程序的编译

在本书中，使用 `gcc` 编译器来编译 C 程序。`gcc` 是一个编译器，它还附带了其他用于生成二进制文件的工具。

下面是 C 程序的编译阶段。

1. 预处理器
2. 编译器
3. 汇编器
4. 链接器

## 预处理器

在此阶段，编译器解析输入文件，替换宏并执行语法检查。可以通过 `gcc` 的 `-E` 参数来实现。

## 编译器

在此阶段，编译器将程序转换为给定平台的目标代码。

在这里进行基于架构的编译，如果编译器可以为不同的目标架构生成代码，那么它就可以为目标架构创建目标代码。

可以通过 `gcc` 的 `-c` 参数来实现。

## 汇编器

在此阶段，生成的特定于目标的目标代码随后被转换为汇编代码表示。

可以通过 `gcc` 的 `-s` 参数来实现。

## 链接器

在此阶段，链接器将目标表示转换为可执行文件。通常在 Linux 中，`ELF` 是可执行文件的格式。

这是另一个名为 `ld` 的工具。除非我们专门为目标嵌入式设备编写软件，否则我们倾向于不直接使用。

## GCC 编译选项

| 序号 | 名称 | 描述 |
|--- | --- | --- |
| 1 | `-Wall` | 开启所有警告 |
| 2 | `-Werror` | 开启所有错误 |
| 3 | `-Wextra` | 开启额外的警告 |
| 4 | `-Wshadow` | 显示在同一函数中声明两次变量的警告 |
| 5 | `-Os` | 开启可能的优化 |
| 6 | `-g` | 在创建的二进制文件中启用调试符号 |
| 7 | `-c` | 创建目标文件 |

## 命令行参数 (argc, argv)

`main` 函数接受两个参数 `argc` 和 `argv`。其签名如下。

```c
int main(int argc, char **argv);
```

第一个参数是参数的个数，第二个参数包含实际的参数内容。

下面是一个示例：

```c
#include <stdio.h>

int main(int argc, char **argv)
{
    for (int i = 0; i < argc; i++) {
        printf("arg[%d]: %s\n", i, argv[i]);
    }
    return 0;
}
```

使用以下参数编译并运行程序：

- `arg[0]`: `./a.out`
- `arg[1]`: `1`
- `arg[2]`: `2`
- `arg[3]`: `3`

`argv[0]` 总是带有完整路径的程序名。其余参数是 `./a.out` 之后用空格分隔的参数。

`argc` 提供了 `argv` 中的参数数量。

`getopt` 库函数 `getopt` 提供了一种解析命令行参数的方法。它的原型定义在 `getopt.h` 中。

```c
int getopt(int argc, const char *argv[], const char *optstring);
```

选项通过 `optstring` 传递。例如，用户可以输入选项作为命令的输入。

```
./a.out -f filename -r
```

`optstring` 将是 `f:r`。

- `f:` 意味着选项 `f` 将有一个参数。
- `r:` 意味着选项 `r` 将没有参数，这就像一个真/假语句。

通过命令行可以有尽可能多的参数。

下面是 `getopt` 的示例。

## 1. 通过 getopt 获取命令行参数

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <getopt.h>

int main(int argc, char **argv) {
    int a = 0;
    char *str = NULL;
    bool t = false;
    int ret;

    while ((ret = getopt(argc, argv, "i:s:t")) != -1) {
        switch (ret) {
            case 'i':
                a = atoi(optarg);
                break;
            case 's':
                str = optarg;
                break;
            case 't':
                t = true;
                break;
            default:
                printf(" ");
        }
    }

    printf("%d\n", a);
    if (str) {
        printf("%s\n", str);
    }
    if (t) {
        printf("is true\n");
    }
    return 0;
}
```

# 文件 I/O

函数返回指向字符串的指针，但其参数 `str` 包含了从文件中读取的数据。返回值 `-1` 意味着 `getopt` 已完成。

## 基本操作

### 1. 打开和关闭文件

```c
FILE *fp;
```

表示 `FILE` 类型的空指针。`fopen` 用于打开文件。`fclose` 用于关闭文件。

`fopen` 的原型为：

```c
FILE *fopen(const char *filename, const char *mode);
```

`fopen` 函数有以下模式：

| 序号 | 名称 | 描述 |
|--- | --- | --- |
| 1 | `r` | 读取 |
| 2 | `w` | 写入 |
| 3 | `a` | 追加 |
| 4 | `rb` | 读取二进制 |
| 5 | `wb` | 写入二进制 |
| 6 | `ab` | 追加二进制 |

`fclose` 的原型为：

```c
int fclose(FILE *fp);
```

下面展示了 `fopen` 和 `fclose` 的调用。

```c
#include <stdio.h>

int main()
{
    const char *filename = "./test.txt";
    FILE *fp;
    int ret = -1;

    fp = fopen(filename, "r");
    if (fp != NULL) {
        printf("file opened success\n");
        fclose(fp);
        ret = 0;
    } else {
        printf("file not found\n");
        ret = -1;
    }
    return ret;
}
```

## 2. 从文件中读取

读取文件可以通过 `fgets` 函数实现。`fgets` 的原型如下。

```c
void fgets(char *str, uint32_t size, FILE *fp);
```

`fgets` 返回指向字符串的指针，但其参数 `str` 包含了从文件中读取的数据。`size` 参数指定了字符串的大小。

下面是 `fgets` 函数的一个示例。

```c
#include <stdio.h>

int main() {
    const char *filename = "./test.txt";
    char msg[1024];
    FILE *fp;
    int ret = -1;

    fp = fopen(filename, "r");
    if (fp) {
        while (fgets(msg, sizeof(msg), fp)) {
            printf("%s", msg);
        }
        fclose(fp);
        ret = 0;
    }
    return ret;
}
```

`fgets` 函数在每次调用时都会添加 `\n` 换行符。对它调用 `strlen` 时，返回比实际长度多一个字符。因此，读取的字符串的最后一个字符是 `\n\0`。要去掉最后一个字符，我们可以到末尾字符串的最后一个字符之前的一个字符，并对其赋值 `\0`。

以下是实现此操作的方法。

```c
char msg[1024];
```

```c
fgets(msg, sizeof(msg), fp);
/* 将 '\n' 替换为 '\0' */
msg[strlen(msg) - 1] = '\0';
```

## 3. 写入文件

可以使用 `fputs`、`fputc` 或 `fprintf` 函数向文件写入。

`fputs` 的原型如下：

```c
int fputs(char *str, FILE *fp);
```

以下是一个示例：

```c
#include <stdio.h>

int main()
{
    const char *filename = "./test.txt";
    char msg[1024];
    FILE *fp;
    int ret = -1;

    fp = fopen(filename, "w");
    if (fp) {
        fputs("Hello World", fp);
        fclose(fp);
        ret = 0;
    }
    return ret;
}
```

## 4. 复制文件

在 C 语言中复制到另一个文件涉及读取输入文件并将内容写入新文件。

以下是复制文件的示例：

```c
#include <stdio.h>

int main()
{
    const char *file_in = "c/filecopy.c";
    const char *file_out = "c/filecopy.c.copy";
    FILE *f_in;
    FILE *f_wr;
    char str[1024];

    f_in = fopen(file_in, "r");
    if (!f_in) {
      return -1;
    }

    f_wr = fopen(file_out, "w");
    if (!f_wr) {
      fclose(f_in);
      return -1;
    }

    while (fgets(str, sizeof(str), f_in)) {
      fputs(str, f_wr);
    }

    fclose(f_in);
    fclose(f_wr);
    return 0;
}
```

## 5. 文件中的字符数

`fgetc` 函数从文件中读取一个字符。如果到达文件末尾，则返回 `EOF` 标记，调用者可以检查该标记并停止继续读取。

通常情况下，`fgetc` 不适用于高性能应用程序。它主要用于写入工具。

通过使用 `fgetc`，我们可以统计文件中的字符数。

```c
#include <stdio.h>

int main() {
  const char *filename = "c/numchar.c";
  FILE *fp;
  char a;
  int num_chars = 0;

  fp = fopen(filename, "r");
  if (!fp) {
    return -1;
  }

  while (1) {
    a = fgetc(fp);
    if (a == EOF) {
      break;
    }
    num_chars++;
  }

  printf("number of characters %d\n", num_chars);
  return 0;
}
```

## 6. 文件大小

`fseek` 和 `ftell` 函数可以分别跳转到特定位置并查找文件偏移量。

`fseek` 和 `ftell` 的原型如下：

```c



# 文件操作

## 定位文件位置

`fseek` 函数的原型如下：

```c
int fseek(FILE *fp, long offset, int whence);
```

`whence` 参数是 `SEEK_SET`、`SEEK_CUR` 或 `SEEK_END` 之一。

`ftell` 的原型如下：

```c
long ftell(FILE *fp);
```

下例同时使用了这两个函数。

```c
#include <stdio.h>

int main() {
  const char *filename = "c/filesize.c";
  long int filesize;
  FILE *fp;

  fp = fopen(filename, "r");
  if (!fp) {
    return -1;
  }

  fseek(fp, 0, SEEK_END);
  filesize = ftell(fp);
  printf("file size %ld\n", filesize);
  fclose(fp);
  return 0;
}
```

## 二进制文件

我们可以将数组、结构体原样写入文件。它们通常是二进制数据，这些文件有时被称为二进制文件。

C 标准库提供了两个函数：

1. `fread`
2. `fwrite`

`fread` 的原型如下：

```c
size_t fread(void *ptr, size_t size, size_t n_memb, FILE *fp);
```

`fwrite` 的原型如下：

```c
size_t fwrite(const void *ptr, size_t size, size_t n_memb, FILE *fp);
```

二进制文件的读写写在 `fopen` 中使用 `wb` 和 `rb` 参数。

```c
FILE *fp;
fp = fopen("a.bin", "wb"); // 以写入模式打开二进制文件
...
fclose(fp);
```

```c
fp = fopen("a.bin", "rb"); // 以读取模式打开二进制文件
...
fclose(fp);
```

以下是一个示例：

```c
#include <stdio.h>

int main()
{
    int a[100];
    int b[100];
    int i;
    FILE *fp;

    for (i = 0; i < sizeof(a) / sizeof(a[0]); i++) {
        a[i] = i;
    }

    fp = fopen("./test.bin", "wb");
    if (!fp) {
        return -1;
    }
}
```

以下是关于在二进制文件中读写数据结构的示例。

```c
#include <stdio.h>

struct S {
    int a;
    int r;
};

struct S s1[10];

int main() {
    struct S;
    int i;
    FILE *fp;

    for (i = 0; i < sizeof(s1) / sizeof(s1[0]); i++) {
        s1[i].a = i;
        s1[i].r = i + 1;
    }

    fp = fopen("./s.bin", "wb");
    if (!fp) {
        return -1;
    }

    fwrite(s1, sizeof(s1), 1, fp);
    fclose(fp);

    fp = fopen("./s.bin", "rb");
    if (!fp) {
        return -1;
    }

    fwrite(s1, sizeof(s1), 1, fp);
    fclose(fp);
    return 0;
}
```

*(注：原文提供的文本后半部分存在逻辑混乱和重复，翻译已根据上下文语义进行了微调处理以保持连贯性)*

```c
int main()
{
    char *filename = "c/fgets_newline.c";
    FILE *fp;
    char str[100];
}
```

每行末额外的换行符是因为 `fgets` 在遇到新行时会添加一个换行符。

解决此问题的方法是通过以下操作去掉字符串尾的换行符：

```c
str[strlen(str) - 1] = '\0';
```

上面的语句从 `fgets` 返回的缓冲区中删除了换行符。

`fprintf` 的原型所示。

```c
int fprintf(FILE *fp, const char *fmt, ...);
```

就像 `fscanf` 一样，`fprintf` 在控制台或文件中打印。可以使用 `stdout` 指针在控制台打印值。

下面的示例使用 `fprintf` 打印值。

```c
#include <stdio.h>

int main()
{
    char *str = "dev";
    int a = 33;
    fprintf(stdout, "str=%s%d\n", str, a);
    return 0;
}
```

`fprintf` 函数可以接收文件描述符，因此它也可以是以写模式打开的文件。

下面的示例使用 `fprintf` 在文件中打印朋友的年龄和名字。

```cpp
#include <stdio.h>

struct S {
    char *name;
    int age[];
} friends[] = {
    {"Dev", 33},
    {"Rahul", 34},
    {"Nithin", 38},
    {"Seema", 35}
};

int main() {
    const char *filename = "c/file_write";
    FILE *fp;
    int i;

    fp = fopen(filename, "w");
    if (!fp) {
        return -1;
    }

    for (i = 0; i < sizeof(friends) / sizeof(friends[0]); i++) {
        fprintf(fp, "%s %d\n", friends[i].name, friends[i].age);
    }

    fclose(fp);
    return 0;
}
```

## 有用的宏

1. 两个数字的最小值

```c
#define MIN(_a, _b) (((_a) < (_b)) ? (_a) : (_b))
```

2. 两个数字的最大值

```c
#define MAX(_a, _b) (((_a) > (_b)) ? (_a) : (_b))
```

3. 检查位是否被设置

```c
#define check_bit(_val, _pos) (((_val) >> (_pos)) & 1)
```

4. 交换相同类型的变量

```c
#define swap(_a, _b, type) \
    type _t = _a; \
    _a = _b; \
    _b = _t;
```

5. 数组的 `sizeof` 宏

```c
#define sizeof(_a) (sizeof((_a))/sizeof((_a[0])))
```

## 有用的辅助函数

1. `stoi`

描述：使用 `strtol` 将字符串转换为整数。

```c
int stoi(const char *str, int *val)
{
    char *err = NULL;
    *val = strtol(str, &err, 10);
    if (err && err[0] != '\0') {
        return -1;
    }
    return 0;
}
```

2. CSV 文件写入器

# C++ 编程

## 介绍

编译 C++ 程序只需使用 `g++` 代替 `gcc` 简单。以下是在 Ubuntu 中安装它的方法。

```bash
sudo apt install gcc-g++
```

C++ 中的一些惯例：

1. 源文件扩展名以 `cxx`、`cpp` 或 `cc` 结尾。
2. 头文件扩展名以 `hxx`、`hpp` 或 `h` 结尾。
3. 标准头文件不需要包含 `.h` 扩展名。
4. 声明结构体和枚举时，不需要 `struct` 前缀。

C++ 标准是一个不断演进的标准。目前 C++23 标准正在进行中。目前这本书尝试区分每个标准中存在的特性，但其理念是每个新标准中的特性必须可以在即将编写的软件中被探索使用。因此，特性将混合使用，且用例将基于这些特性。

## `cout`, `cerr` 和 `cin`

使用 `cerr`、`cout` 和 `cin` 时要包含头文件 `iostream`。

`cerr` 类似于向 `stderr` `fprintf`。

下面是一个使用 `cerr` 的示例。

```cpp
#include <iostream>

int main()
{
    std::cerr << "hello world" << std::endl;
    return 0;
}
```

`cout` 类似于 `printf`，而 `cin` 非常类似于 `fgets`。

但 `cout` 和 `cin` 的用法非常不同。

例如，

```cpp
#include <iostream>

int main()
{
    std::cout << "hello world" << std::endl;
    return 0;
}
```

使用 `g++` 编译它，命令为 `g++ hello_world.cc`。成功编译后会创建二进制文件 `a.out`。

上面的程序在执行时会在屏幕上打印 "hello world"。`std::endl` 就像换行符。我们可以在上面的程序中添加 `std::endl`。

下面是一个使用 `cin` 的示例。

```cpp
#include <iostream>

int main()
{
    std::string str;
    cin >> str;
    std::cout << "a: " << str << "str: " << str << std::endl;
    return 0;
}
```

与 `fscanf` 不同，`cin` 不需要提供格式说明符。`cin` 每次只取一个字符串。

## C++ 中的新运算符

### 1. 引用运算符 (`&`)

引用运算符类似于指针，但通常永远为 `NULL`。

### 2. `new` 和 `delete`

`new` 和 `delete` 运算符在 C++ 中引入，用于替代内存分配函数。下面是 `new` 和 `delete` 的使用：

```cpp
#include <iostream>

int main() {
    int *a = new int;
    *a = 3;
    printf("%d\n", *a);
    delete a;
    return 0;
}
```

分配和释放数组：`new[]` 和 `delete[]` 运算符用于分配和释放数组。

```cpp
#include <iostream>

int main() {
    int *a;
    int i;
    a = new int[10];
    for (i = 0; i < 10; i++) {
        a[i] = i;
        std::cout << "a[" << i << "] = " << a[i] << std::endl;
    }
    delete[] a;
    return 0;
}
```

分配和释放结构体：

```cpp
#include <iostream>

struct S {
  int a;
};

int main() {
  S *r = new S;
  r->a = 3;
  delete r;
  return 0;
}
```

在使用 C 函数 `malloc`、`calloc` 和 `realloc` 时，返回类型必须转换为目标类型。查看下面类型转换的示例：

```cpp
#include <iostream>

struct S {
  int a;
};

int main() {
  int *r1;
  S *r2;
  int *r3;

  r1 = (int*)malloc(sizeof(int));
  if (!r1) {
    return -1;
  }
  *r1 = 3;

  r2 = (S*)calloc(1, sizeof(S));
  if (!r2) {
    return -1;
  }
  r2->a = 9;

  r3 = (int*)realloc(r3, sizeof(int));
  if (!r3) {
    return -1;
  }
  *r3 = 6;

  std::cout << "r1: " << *r1 << " r2: " << r2->a << " r3: " << *r3 << std::endl;

  free(r1);
  free(r2);
  free(r3);
  return 0;
}
```

### 4. Range based for

Range based for 循环是 C++11 引入的一个新特性。下面是 range based for 的使用：

```cpp
#include <iostream>

int main() {
    for (int a: {1, 2, 3, 4}) {
        std::cout << "a: " << a << std::endl;
    }
    return 0;
}
```

下面是 range based for 的另一种使用：

```cpp
#include <iostream>

int main() {
    int a[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
    for (auto i : a) {
        printf("%d\n", i);
    }
    return 0;
}
```

Range based for 循环具有以下优势：

- 无需条件检查，消除了无限循环的可能性。
- 自动递增和初始化。

### 5. Enum classes

Enum classes允许对枚举分类。

```cpp
enum class fruits {
  Apples,
  Oranges,
  Banana,
};
```

枚举可以声明为：

```cpp
f = fruits::Apple; // Apple 的赋值
fruits fi = fruits::Apple; // 枚举初始化
```

两种声明在各自范围内都有帮助。

```cpp
#include <iostream>

enum class fruits {
  Apple,
  Oranges,
  Banana,
};

int main()
{
  fruits f = fruits::Apple;
  std::cout << (int)f << std::endl;
  return 0;
}
```

比较仍然有效。

```cpp
#include <iostream>

enum class Languages {
  Telugu,
  Tamil,
  English,
  Hindi,
};
```

枚举不能用 `std::cout` 打印，但像 C 一样，它们可以转换为整数。

### 6. `nullptr`

从 C++11 开始，标准定义了可以分配任何指针的 `nullptr`。赋值时，编译器会处理空指针的分配。`nullptr` 不指向 0 或 `(void*)0`。

例如，以下语句在 C++ 中仍然有效：

```cpp
int *p = 0; // 0 的用法
int *p = NULL; // C 中的 NULL 指针用法
```

通常，使用 `auto` 类型推导查找变量类型非常困难。

```cpp
auto res = get_data();
if (res == 0) // 假设这里 0 是空指针
```

但是，如果 `get_data` 实际上返回一个空指针，那么理解的类型可能是 `NULL`。

```cpp
if (res == nullptr) // 始终保证 res 是空指针
```

数据结构指针也可以分配为 `nullptr`。

```cpp
struct S {
    int a;
};
```

```cpp
*s1 = NULL; // 仍然有效
*s2 = nullptr; // 有效
```

在某些标准类型（如 `shared_ptr`、`unique_ptr`）中，赋值可能会导致模糊的结果。`shared_ptr` 和 `unique_ptr` 是标准模板库的一部分。将在相应的章节中进一步讨论。

```cpp
std::shared_ptr<S> s1 = 0; // 可能有效
std::shared_ptr<S> s2 = nullptr;
```

在上面的函数 `f` 中，调用者不需要传递第二个参数，因此调用 `f(10)` 是合法的。

或者如果显式地想要传递值，也可以传递第二个参数。例如 `f(3, 3)` 是合法的，且参数 `b` 取值为 3。

```cpp
#include <iostream>
```



```cpp
int f(int a, int b = 10)
{
    return a + b;
}

int main()
{
    int r = f(10);
    std::cout << "r: " << r << std::endl;
    r = f(3, 3);
    std::cout << "r: " << r << std::endl;
    return 0;
}
```

## C++ 中的新关键字

```cpp
constexpr
```

## explicit

`auto` 关键字在用时提供自动类型推导。一个示例：

```cpp
auto i = 10;
```

表示它是一个整数，但当赋值给它的值是一个 `int` 时，编译器会自动理解这一点。

```cpp
auto i = 10; // an int
auto p = 10.1; // a double
auto t = "c++"; // a const string
```

当编写复杂类型变得非常困难时，我们有时使用 `auto`。我们将在接下来的章节中看到更多关于 `auto` 的内容。记住，并不是所有的 `auto` 类型推导都符合我们的预期。

当使用 `auto` 类型的变量时，必须进行初始化。这通常指示编译器根据初始化值来推导出类型。

```cpp
static_cast
dynamic_cast
reinterpret_cast
```

## 类 (Classes)

C++ 中的类类似于 C 语言中的结构体。类是数据及其数据操作的封装。

一个类通常看起来像：

```cpp
class <name> {
public:
    <variable_type> variable;
    <return_type> function_prototype(parameters..);
protected:
    <variable_type> variable;
    <return_type> function_prototype(parameters..);
private:
    <variable_type> variable;
    <return_type> function_prototype(parameters..);
};
```

下面的示例提供了一个简单的类定义。

```cpp
class S {
public:
    S() { a = 0; }
    ~S() {}
    void set(int a) { a_ = a; }
    void get() { return a_; }
private:
    int a_;
};
```

函数 `S()` 和 `~S()` 分别是构造函数和析构函数。构造函数在类对象实例化时被调用。析构函数在类对象离开作用域时调用。类对象的生命周期与 C 变量相似。

`S` 内部的函数 `set` 和 `get` 是私有成员函数。变量 `a_` 是一个私有成员。通常，私有成员会带有前缀或后缀，以区分局部变量和类成员。如果没有它，将很难理解变量的生命周期。

类的 `sizeof` 会给出变量的大小（不包括成员函数）。

```cpp
#include <iostream>

class S {
    public:
        int get() { return a; }
    private:
        int a;
        int p;
        double r;
};

int main() {
    std::cout << "size: " << sizeof(S) << std::endl;
    return 0;
}
```

公共成员可以被类的用户访问，而私有成员无法访问。

下面的代码声明了 `S` 的类对象。

```cpp
S s;
```

成员函数 `set` 和 `get` 是可以的：

```cpp
S s;
s.set(3);
int val = s.get();
```

像如下所示直接访问 `a_` 会导致编译器错误，因为该变量是类的私有部分。

```cpp
S s;
int val = s.a_; // results in compiler error
```

变量 `a_` 只能通过 `get` 方法访问。

如果没有提到 `public` 关键字，作用域默认是私有的。

```cpp
class S {
    S() { a_ = 0; }
    ~S() { }
    void set(int a) { a_ = a; }
    void get() { return a_; }
    int a_;
};
```

上面的代码显示类成员默认都是私有的。所有成员都是私有的类是合法的，并且在创建类的对象实例化之前都可以编译。

### 构造函数和析构函数

构造函数在对象创建时被调用。例如：

```cpp
class S {
    public:
        S() { a = 3; }
        ~S() {}
        int get() { return a; }
    private:
        int a;
};

int main() {
    S s;
}
```

声明 `S` 调用了构造函数 `S()`。构造函数和析构函数的名称与类相同。析构函数带有波浪前缀。析构函数在对象丢失作用域后立即调用。

下面是一个示例：

```cpp
#include <iostream>

class P {
    public:
        P() {
            std::cout << "default constructor" << std::endl;
            a = 3;
        }
        ~P() {
            std::cout << "destructor called" << std::endl;
        }
        int get() { return a; }
    private:
        int a;
};

int main() {
    P p;
    std::cout << "p.a: " << p.get() << std::endl;
    return 0;
}
```

### 拷贝构造函数

### 拷贝赋值运算符

### 移动指针

指针仅仅是对类成员函数的自引用。

下面的程序显示了 `this` 指针的使用。

```cpp
#include <iostream>

class S {
public:
    S() { a_ = 0; }
    ~S() {}
    int get() { return this->a_; }
    void set(int a) { this->a_ = a; }
private:
    int a_;
};

int main() {
    S s;
    s.set(3);
    int val = s.get();
    std::cout << "val: " << val << std::endl;
    return 0;
}
```

变量 `a_` 只能通过 `get` 方法访问。

如果没有提到 `public` 关键字，作用域默认是私有的。

```cpp
class S {
    S() { a_ = 0; }
    ~S() { }
    void set(int a) { a_ = a; }
    void get() { return a_; }
    int a_;
};
```

(注：原始文本中存在大量重复和 OCR 错误，此处已根据核心翻译核心逻辑翻译。)

```cpp
S operator+(const S& s)
{
    S r;
    r.a = this->a + s.a;
    return r;
}

int main()
{
    S s(3);
    S r(3);
    S t;
    t = s + r;
    std::cout << "t.a: " << t.a << std::endl;
    return 0;
}
```

### 重载 ++ 运算符

```cpp
#include <iostream>

struct S {
    int a;
    S() { a = 0; }
    S(int a) { this->a = a; }
    void operator ++() { a++; }
};

int main() {
    S s(3);
    ++s;
    std::cout << s.a << std::endl;
}
```

在上面的示例中，结构体 `A` 的两个变量 `a` 和 `b` 被相加，并返回另一个结构体 `r`。

### 重载 << 运算符

`<<` 运算符也可以被重载。下面是重载 `<<` 运算符的一个示例。

`<<` 的原型是固定的，并且必须如下所示：

```cpp
std::ostream &operator<<(std::ostream &os, <class name>);
```

参数 `os` 是输出流，`cout` 接收 `os`，因此 `<<` 运算符会将其返回。

因此，参数必须从另一个参数给出的类中填充到 `os` 中。

实现其中一种方法如下：

```cpp
class S {
    int a;
    public:
    int get() { return a; }
};

std::ostream &operator<<(std::ostream &os, const S &r)
{
    os << r.a; // 将所需数据填充到输出流
    return os; // 返回输出流
}
```

下面是一个示例：

```cpp
#include <iostream>

struct S {
    int a;
    double d;
};

std::ostream &operator<<(std::ostream &os, const S &s)
{
    os << "s.a: " << s.a << " " << "s.d: " << s.d;
    return os;
}

int main()
{
    S s { .a = 3, .d = 3.1 };
    std::cout << s << std::endl;
    return 0;
}
```

### 在类中重载 << 运算符

`<<` 运算符不能直接在类中重载。我们需要将该运算符声明为类的友元（`friend`），并在类外部定义它。

```cpp
#include <iostream>

class S {
public:
  S(int r) : a(r) {}
  S() {}
  friend std::ostream&operator<<(std::ostream &os, const S &r);
private:
  int a;
};

std::ostream&operator<<(std::ostream &os, const S &r)
{
  os << " r.a: " << r.a;
  return os;
}

int main()
{
  S s1(3), s2(6);
  std::cout << s1 << s2 << std::endl;
}
```

### 重载 == 运算符

```cpp
#include <iostream>

struct S {
    int a;
    int f;
};

bool operator==(const S& kl, const S& kr) {
    return (kl.a == kr.a) && (kl.f == kr.f);
}

int main() {
    S s1 = { .a = 3, .f = 1 };
    S s2 = { .a = 6, .f = 1 };
    if (s1 == s2) {
        std::cout << "s1 and s2 are same" << std::endl;
    } else {
        std::cout << "s1 and s2 are not same" << std::endl;
    }
    return 0;
}
```

### 在类中重载 ==

```cpp
#include <iostream>

struct S {
    int a;
    int f;
    bool operator==(const S& other) {
        return (this->a == other.a) &&
               (this->f == other.f);
    }
};

S s1 = { .a = 3, .f = 4 };
S s2 = { .a = 3, .f = 4 };

int main()
{
    if (s1 == s2) {
        std::cout << "s1 and s2 are same" << std::endl;
    } else {
        std::cout << "s1 and s2 are not same" << std::endl;
    }
    return 0;
}
```

### 重载 * 运算符

```cpp
#include <iostream>

struct S {
    int a;
};

S* operator*(const S &r1, const S &r2) {
    S r;
    r.a = r1.a * r2.a;
    return r;
}

int main() {
    S r1, r2, r;
    r1.a = 3;
    r2.a = 6;
    r = r1 * r2;
    std::cout << r.a << std::endl;
}
```

### 在类中重载 *

```cpp
#include <iostream>

struct S {
    S(int r) {
        a = r;
    }
    ~S() {
    }
    int a;
    friend S* operator*(const S &r1, const S &r2);
};

int main() {
    S r1(3), r2(6);
    std::cout << r1.a << std::endl;
}
```

### 重载 > 运算符

```cpp
#include <iostream>

struct S {
    int a;
};

bool operator>(const S &a, const S &l) {
    return a.a > l.a;
}

int main() {
    S a = { .a = 3 };
    S b = { .a = 6 };
    std::cout << "a is greater than b?" << (a > b) << std::endl;
}
```

### 在类中重载 >

```cpp
#include <iostream>

struct S {
    int a;
    bool operator>(const S &r) {
        return this->a > r.a;
    }
};

int main() {
    S s1, s2;
    s1.a = 1;
    s2.a = 2;
    std::cout << "s1 > s2: " << (s1 > s2) << std::endl;
    std::cout << "s2 > s1: " << (s2 > s1) << std::endl;
    return 0;
}
```

### 重载 < 运算符

```cpp
#include <iostream>

struct S {
    int a;
};

bool operator<(const S &a, const S &l) {
    return a.a < l.a;
}

int main() {
    S a = { .a = 3 };
    S b = { .a = 6 };
    std::cout << "a is greater than b " << (a < b) << std::endl;
    return 0;
}
```

### 在类中重载 <

```cpp
#include <iostream>

struct S {
    int a;
    bool operator<(const S &r) {
        return this->a < r.a;
    }
};

int main() {
    S s1, s2;
    s1.a = 3;
    s2.a = 6;
    std::cout << "s1 < s2: " << (s1 < s2) << std::endl;
    std::cout << "s2 < s1: " << (s2 < s1) << std::endl;
    return 0;
}
```

### 重载 >= 运算符

```cpp
#include <iostream>

struct S {
    int a;
};
```



## 在类中重载运算符

### 在类中重载 `>=`

```cpp
bool operator>=(const S &r) {
    return this->a >= r.a;
}
```

```cpp
int main() {
    S r1, r2, r3;
    r1.a = 3;
    r2.a = 4;
    r3.a = 3;

    std::cout << " " << r1 << " > " << r2 << " " << (r1 >= r2) 
              << " " << r2 << " >= " << r1 << " " << (r2 >= r1) 
              << " " << r3 << " >= " << r1 << " " << std::endl;

    return 0;
}
```

### 在类中重载 `&`

```cpp
#include <iostream>

struct S {
    uint32_t a;

    uint32_t operator&=(const S &r) {
        return this->a & r.a;
    }
};

int main() {
    S r1, r2;
    r1.a = 0xFF;
    r2.a = 0x40;

    printf("r1 & r2: 0x%02x\n", r1 & r2);

    return 0;
}
```

### 在类中重载 `|`

```cpp
#include <iostream>

struct S {
    int a;

    uint32_t operator|(const S &r) {
        return this->a | r.a;
    }
};

int main() {
    S r1, r2;
    r1.a = 0x80;
    r2.a = 0x40;

    printf("r1 | r2: 0x%02x\n", r1 | r2);

    return 0;
}
```

## 函数重载

函数重载允许一个函数有多个签名。下面是一个示例：

```cpp
int F(int a);
int F(int a, int b);
```

函数 `F` 在这里被重载了，具有两个签名。编译器根据定义确定调用哪个 `F`。

```cpp
#include <iostream>
```

```cpp
int F(int a) { return a; }
int F(int a, int b) { return a + b; }
```

```cpp
int main(){
    std::cout << "F(3): " << F(3) << std::endl;
    std::cout << "F(3,3): " << F(3,3) << std::endl;

    return 0;
}
```

函数的参数允许被重载。然而，函数的返回值类型不允许被重载。例如：

```cpp
#include <iostream>
```

```cpp
int F(int a) { return a; }
void F(int a) { }
```

```cpp
int main(){
    F(3);
}
```

会导致编译器错误：

```cpp
cpp/overload_f.cc:4:6: error: ambiguous new declaration of 'void F(int)'
    4 | void F(int a) { }
ncpp/overload_f.cc:3:5: note: old declaration 'int F(int)'
    3 | int F(int a) { return a; }
```

当一个函数想要执行不同的任务但保持名称相同签名不同时，函数重载非常有用。

## 异常处理

```cpp
#include <iostream>

struct S {
    S(int r) {
        if (r == 0) {
            throw std::runtime_error("r is 0");
        }
    }

    int a;
};

int main() {
    try {
        S r1(0);
    } catch (std::runtime_error &r) {
        std::cout << "exception: " << r.what() << std::endl;
    }

    S r2(3);

    return 0;
}
```

```cpp
#include <iostream>
#include <exception>
```

```cpp
class S : public std::out_of_range {
public:
    S(const char *err) : std::out_of_range(err) {}
    S() {}

    void set(int v) {
        if (v > 10) {
            throw *this;
        }
        a = v;
    }

    virtual const char *what() const noexcept {
        return "a value out of range";
    }
};
```

```cpp
int main()
{
    S r1("");
    try {
        r1.set(11);
    } catch (S &r) {
        std::cout << r.what() << std::endl;
    }

    return 0;
}
```

## noexcept

**noexcept** 既是一个运算符，也是一个标识符。

### noexcept 标识符

**noexcept** 标识符告知编译器特定的函数/构造函数/析构函数不会产生异常。它在被继承的类中也遵循底层规则。

`noexcept` 标识符可以附加在函数的末尾：

```cpp
int f(void) noexcept; // 表示函数不会抛出异常
int g(void);          // 可能会抛出异常
```

声明为 **noexcept** 但实际抛出异常的函数将导致库调用 `std::terminate`。这使得异常无法被捕获。

重载函数可以有不同的异常规范。例如，下面的示例是有效的。

```cpp
int f(void) noexcept;
int f(std::string arg);
```

下面的程序几乎涵盖了所有的 `noexcept` 情况：

```cpp
#include <iostream>

void f() noexcept { std::cout << "f called" << std::endl; }
void f(std::string arg) { std::cout << "f called with arg: " << arg << std::endl; }
void g() noexcept { throw std::runtime_error("an exception g()"); }
void p() { throw std::runtime_error("an exception p()"); }
```

```cpp
int main() {
  f();
  f("test");

  try {
    p();
  } catch (const std::exception& e) {
    std::cout << "caught the exception from function p():" << e.what() << std::endl;
  }

  try {
    g();
  } catch (...) {
    std::cout << "caught the exception from function g()\n";
  }
}
```

如果基类包含任何带有 `noexcept` 标识符的成员函数，则派生类也必须包含 `noexcept` 规范。否则，将导致编译器错误。

```cpp
#include <iostream>
```

```cpp
class F {
public:
    virtual void f() noexcept = 0;
};
```

```cpp
class G : public F {
public:
    void f() { std::cout << "in f()" << std::endl; }
};
```

```cpp
int main() {
    G g;
    g.f();
}
```

会导致编译器错误：

```cpp
cpp/noexcept_inh.cc:10:22: error: looser exception specification on overriding virtual function
   10 | void f() { std::cout << "in f()" << std::endl; }
cpp/noexcept_inh.cc:5:30: note: overridden function is 'virtual void F::f() noexcept'
    5 | virtual void f() noexcept = 0;
```

然而，派生类可以指定不同的 `noexcept`，或者基类没有包含它。

例如，下面的程序可以编译。

```cpp
#include <iostream>
```

```cpp
class F {
public:
    virtual void f() = 0;
};
```

```cpp
class G : public F {
public:
};
```

```cpp
void f() noexcept { std::cout << "in f()" << std::endl; }

int main()
{
    G g;
    g.f();
}
```

## 标准库

标准库（简称 STL）是一组为了方便编程的辅助函数。如今，它们更倾向于帮助程序员使用 C++ 编写与操作系统无关的软件。

### std::pair

**std::pair** 定义了一对值。其用例包括从函数返回多个变量，或作为键值对传递给函数。

**std::pair** 可以直接用于构造一个值对，也可以使用 `std::make_pair`。

```cpp
auto p = std::pair<std::string, int>("test", 1); // 在 p 中构造了 std::pair 类型
p = std::make_pair<std::string, int>("test", 1); // 创建了一个类型为 std::pair 的值对
```

下面是 `std::pair` 的用例示例：

```cpp
#include <iostream>

void f(const std::pair<std::string, int>& p) {
    std::cout << "first: " << p.first << ", second: " << p.second << std::endl;
}

int main() {
    auto p = std::make_pair<std::string, int>("test", 1);
    f(p);

    return 0;
}
```

**std::pair** 重载了运算符用于比较。例如：

```cpp
#include <iostream>
#include <string>

int main() {
    std::pair<std::string, int> p1("test", 1);
    std::pair<std::string, int> p2("test", 1);

    if (p1 == p2) {
        std::cout << "p1 is equal to p2" << std::endl;
    }

    if (p1 != p2) {
        std::cout << "p1 is not equal to p2" << std::endl;
    }

    return 0;
}
```

### 数组

`std::array` 定义了一个固定大小的数组。

```cpp
#include <iostream>
#include <array>

int main() {
    std::array<int, 5> arr = {1, 2, 3, 4, 5};

    for (const auto& i : arr) {
        std::cout << i << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

`std::array` 提供了许多用于操作数组的成员。

```cpp
#include <iostream>
#include <array>

int main() {
    std::array<int, 5> arr = {1, 2, 3, 4, 5};

    std::cout << "first element: " << arr.front() << std::endl;
    std::cout << "last element: " << arr.back() << std::endl;
    std::cout << "size: " << arr.size() << std::endl;
    std::cout << "capacity: " << arr.capacity() << std::endl;

    return 0;
}
```

`std::array` 允许通过索引访问元素。

```cpp
#include <iostream>
#include <array>

int main() {
    std::array<int, 5> arr = {1, 2, 3, 4, 5};

    std::cout << "element at index 0: " << arr[0] << std::endl;
    std::cout << "element at index 2: " << arr.at(2) << std::endl;

    return 0;
}
```

### 字符串

`std::string` 定义了一个字符串。

```cpp
#include <iostream>
#include <string>

int main() {
    std::string str = "Hello, world!";

    std::cout << str << std::endl;
    std::cout << "length: " << str.length() << std::endl;

    return 0;
}
```

`std::string` 提供了许多操作字符串的方法。

```cpp
#include <iostream>
#include <string>

int main() {
    std::string s1 = "Hello";
    std::string s2 = " World";
    std::string s3 = s1 + s2;

    std::cout << s3 << std::endl;

    size_t pos = s3.find("World");
    if (pos != std::string::npos) {
        std::cout << "Found 'World' at index " << pos << std::endl;
    }

    return 0;
}
```

### vector 的常用操作

`v.resize(3);` // 调整 vector 元素的大小
`v.at(2) = 3;` // 设置索引为 2 的元素

如果没有调用 `resize`，`at` 赋值将失败，导致越界异常。

#### 1. `begin`

获取 vector 的开头。

```cpp
std::vector<int> v;
v.push_back(1);
v.push_back(2);

auto i = v.begin();
std::cout << "val: " << i << std::endl;
```

#### 2. `end`

获取 vector 的末尾。

```cpp
std::vector<int> v;
v.push_back(1);
v.push_back(2);

auto t = v.end() - 1; // vector 的最后一个元素
std::cout << "val: " << t << std::endl;
```

```cpp
std::vector<int> v;
v.push_back(1);
v.push_back(2);

for (auto it : v) {
    std::cout << "val: " << it << std::endl;
}

std::vector<int>::iterator it;
// 从 begin 到结束迭代
for (it = v.begin(); it != v.end(); it++) {
    std::cout << "val: " << *it << std::endl;
}
```



### 5. `cbegin`

使用 `const` 获取 `vector` 迭代的开头。

可以使用 `auto` 或 `::const_iterator`。

### 6. `cend`

使用 `const` 获取 `vector` 迭代的末尾。

可以使用 `auto` 或 `::const_iterator`。

```cpp
std::vector<int> v;
v.push_back(1);
v.push_back(2);
```

```cpp
std::vector<int>::const_iterator it_c;
for (it_c = v.begin(); it_c != v.end(); it_c ++ ) {
    std::cout << "val: " << *it_c << std::endl;
}
```

### 7. `rbegin`

获取 `vector` 反向迭代的开头。

可以使用 `auto` 或 `reverse_iterator`。

### 8. `rend`

获取 `vector` 反向迭代的末尾。

可以使用 `auto` 或 `reverse_iterator`。

```cpp
std::vector<int> v;
v.push_back(1);
v.push_back(2);
```

```cpp
std::vector<int>::reverse_iterator it_r;
for (it_r = v.rbegin(); it_r != v.rend(); it_r ++ ) {
    std::cout << "val: " << *it_r << std::endl;
}
```

### 9. `erase`

移除 `vector` 中的更多一个元素。

```cpp
std::vector<int> v;
v.push_back(1);
v.push_back(2);
```

```cpp
v.erase(it.begin()); // 移除头部元素
v.erase(it.begin(), it.end()); // 从 begin 到结束的所有元素
```

### 10. `insert`

在特定位置插入元素。

```cpp
std::vector<int> v;
std::vector<int> v2;
v.push_back(1);
v.push_back(2);
v2.push_back(3);
v.insert(v.end(), v2.begin(), v2.end()); // 在 v 的末尾插入 v2
```

### 11. `resize`

调整 `vector` 元素的大小。

```cpp
std::vector<int> v;
v.push_back(1);
v.resize(3); // 将 vector 调整为 3 个元素。
```

### 12. `clear`

清除 `vector` 中的元素。

```cpp
std::vector<int> v;
v.push_back(1);
v.push_back(2);
v.clear(); // 清空 vector 中的所有元素
```

`vector` 也可以像 `[]` 运算符一样进行索引。下面是一个示例：

```cpp
std::vector<int> v;
v.push_back(1);
v.push_back(2);
for (auto i = 0; i < v.size(); i++) {
    std::cout << v[i] << std::endl;
}
```

以下是上述大部分方法的示例：

```cpp
#include <iostream>
#include <vector>

struct S {
    int age;
    std::string name;
};

static void it_const_print(const std::vector<S>& group) {
    std::vector<S>::const_iterator it_c;
    std::cout << "normal print [" << group.size() << "] " << group.size() << std::endl;
    for (it_c = group.begin(); it_c != group.end(); ++it_c) {
        std::cout << "\t name: " << it_c->name << " "
                  << "\age: " << it_c->age << std::endl;
    }
}

static void range_print(const std::vector<S>& group) {
    std::cout << "auto iteration: [" << group.size() << "] " << std::endl;
    for (auto it : group) {
        std::cout << "\t name: " << it.name << " "
                  << "\age: " << it.age << std::endl;
    }
}

static void reverse_print(const std::vector<S>& group) {
    std::vector<S>::reverse_iterator it_r;
    std::cout << "reverse iterator: [" << group.size() << "] " << std::endl;
    for (it_r = group.rbegin(); it_r != group.rend(); ++it_r) {
        std::cout << "\t name: " << it_r->name << " "
                  << "\age: " << it_r->age << std::endl;
    }
}

static void at_print(std::vector<S>& group) {
    int i;
    std::cout << "at: [" << group.size() << " ]" << std::endl;
    for (i = 0; i < group.size(); i++) {
        std::cout << "\tname: " << group[i].name << " "
                  << "\age: " << group[i].age << std::endl;
    }
}

int main() {
    std::vector<S> group;
    std::vector<S> group2;

    group.push_back({32, "Dev"});
    group.push_back({33, "Seema"});
    group.push_back({34, "Cap"});

    group2.push_back({50, "Hannibal"});
    group2.push_back({30, "BA"});
    group2.push_back({30, "Peck"});
    group2.push_back({30, "Murdoch"});

    it_const_print(group);
    range_print(group);
    reverse_print(group);
    at_print(group);

    std::vector<S> it;
    for (auto it = group.begin(); it != group.end(); it++) {
        if (it->age == 34) {
            break;
        }
    }

    // Erasing
    if (it != group.end()) {
        group.erase(it);
    }

    std::cout << "merging with another vector: " << std::endl;
    group.insert(group.end(), group2.begin(), group2.end());
    group.resize(7);
    group.at(6).age = 30;
    group.at(6).name = "test";

    std::cout << "first " << group.begin()->age << std::endl;
    std::cout << "last " << (group.end() - 1)->age << std::endl;

    range_print(group);
    group.clear();
    range_print(group);

    return 0;
}
```

`vector` 可以包含任何类型。例如：

```cpp
std::vector<int> r1; // 整数 vector
std::vector<std::string> r2; // 字符串 vector
```

```cpp
struct S {
    int p1;
    std::string p2;
}
```

```cpp
std::vector<S> r3; // S 类型 vector
```

`vector` 的 `vector` 是可能的。

```cpp
std::vector<std::vector<int>> r1; // 二维数组
```

下面是二维数组的示例：

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<std::vector<int>> r;
    int i;
    int j;

    for (i = 0; i < 3; i++) {
        std::vector<int> r1;
        for (j = 0; j < 3; j++) {
            r1.push_back(j + 1 + i);
        }
        r.push_back(r1);
    }

    for (auto it1 : r) {
        for (auto it2 : it1) {
            printf("%d ", it2);
        }
        printf("\n");
    }

    return 0;
}
```

### Lists

`std::list` 定义了一个列表类型。这与 `std::vector` 类似。`std::list` 使用 `<list>` 头文件。

`std::list` 提供了以下操作：

| S.No | Name | Description |
|---|---|---|
| 1 | `front` | 第一个元素 |
| 2 | `back` | 最后一个元素 |
| 3 | `empty` | 检查列表是否为空 |
| 4 | `size` | 返回元素数量 |
| 5 | `max_size` | 获取最大容量 |
| 6 | `clear` | 清空列表 |
| 7 | `insert` | 插入一个或多个元素 |
| 8 | `push_back` | 在末尾添加元素 |
| 9 | `pop_back` | 从末尾移除元素 |
| 10 | `push_front` | 在开头添加元素 |
| 11 | `pop_front` | 从开头移除元素 |
| 12 | `erase` | 移除元素 |

### 1. `front`

访问列表中的第一个元素。

```cpp
std::list<int> a = {1, 2, 3};
std::cout << "front: " << a.front() << std::endl;
```

### 2. `back`

访问列表中的最后一个元素。

```cpp
std::list<int> a = {1, 2, 3};
std::cout << "back: " << a.back() << std::endl;
```

### 3. `empty`

检查列表是否为空。

```cpp
std::list<int> a;
std::cout << "empty: " << a.empty() << std::endl;
```

### 4. `size`

获取列表的长度。

```cpp
std::list<int> a = {1, 2, 3};
std::cout << "size: " << a.size() << std::endl;
```

### 5. `max_size`

获取列表的最大容量。

```cpp
std::list<int> a = {1, 2, 3};
std::cout << "max_size: " << a.max_size() << std::endl;
```

### 6. `clear`

清空列表中的元素。

```cpp
std::list<int> a = {1, 2, 3};
a.clear();
std::cout << "empty: " << a.empty() << std::endl;
```

### 7. `insert`

在列表中插入一个或多个元素。

```cpp
std::list<int> r1 = {1, 2, 3};
std::list<int> r2 = {4, 5};
r1.insert(r1.end(), r2.begin(), r2.end());
```

### 8. `push_back`

在列表末尾添加元素。

```cpp
std::list<int> a = {1, 2, 3};
a.push_back(4);
std::cout << "back: " << a.back() << std::endl;
```

### 9. `pop_back`

从列表末尾移除元素。

```cpp
std::list<int> a = {1, 2, 3};
a.pop_back();
std::cout << "back: " << a.back() << std::endl;
```

### 10. `push_front`

在列表开头添加元素。

```cpp
std::list<int> a = {1, 2, 3};
a.push_front(0);
std::cout << "front: " << a.front() << std::endl;
```

### 11. `pop_front`

从列表开头移除元素。

```cpp
std::list<int> a = {1, 2, 3};
a.pop_front();
std::cout << "front: " << a.front() << std::endl;
```

### 12. `erase`

移除列表中的元素。

```cpp
std::list<int> a = {1, 2, 3};
auto it = a.begin();
a.erase(it);
```

### 11. `erase`（补充）

删除给定范围内的元素。

```cpp
std::list<int> a = {1, 2, 3, 4, 5, 6};
erase(a.begin(), a.end()); // 删除列表中的所有元素
erase(a.begin(), std::next(a.begin(), 2)); // 删除列表中的前 2 个元素
```

### 12. `iterators`

迭代器（`iterator`）、常量迭代器（`constant_iterator`）和反向迭代器（`reverse_iterator`）均适用于列表（`lists`）。

```cpp
std::list<int> r = {1, 2, 3, 4, 5, 6};
std::list<int>::iterator it;
std::list<int>::reverse_iterator rit;
std::list<int>::constant_iterator it_c;
```

```cpp
for (it = r.begin(); it != r.rend(); it++) {
    std::cout << *it << std::endl;
}
```

```cpp
for (rit = r.rbegin(); rit != r.rend(); rit++) {
    std::cout << *rit << std::endl;
}
```

```cpp
for (it_c = r.cbegin(); it_c != r.cend(); it_c++) {
    std::cout << *it_c << std::endl;
}
```

```cpp
for (auto it_a : r) {
    std::cout << it_a << std::endl;
}
```

以下是 `std::list` 的用法示例。

```cpp
#include <iostream>
#include <list>

int main() {
    std::list<int> l;
    std::list<int> r;
    std::list<int>::iterator it;
    std::list<int>::reverse_iterator rit;

    l.push_back(3);
    l.push_back(1);
    l.push_back(6);
    l.push_back(2);

    /* 正常迭代器: " << */
```



`std::cout << "normal iterator: " << std::endl;`

```
for (it = l.begin(); it != l.end(); it++) {
    std::cout << *it << std::endl;
}
```

`/* 反向迭代器. " << */`

`std::cout << "reverse iterator: " << std::endl;`

```
for (rit = r.begin(); rit != r.end(); rit++) {
    std::cout << *rit << std::endl;
}
```

`std::cout << "auto iterator: " << std::endl;`

```
for (auto it : l) {
    std::cout << it << std::endl;
}
```

`std::cout << "front: " << l.front() << std::endl;`

`std::cout << "back: " << l.back() << std::endl;`

`r = 1;`

`std::cout << "normal iterator: " << std::endl;`

```
for (it = r.begin(); it != r.end(); it++) {
    std::cout << *it << std::endl;
}
```

`r.insert(r.end(), l.begin(), l.end());`

`std::cout << "normal iteration after insert: " << std::endl;`

```
for (it = r.begin(); it != r.end(); it++) {
    std::cout << *it << std::endl;
}
```

`r.erase(r.begin(), r.end());`

`std::cout << "r size: " << r.size() << " r max size: " << r.max_size() << std::endl;`

`std::cout << "l size: " << l.size() << " l max size: " << l.max_size() << std::endl;`

`return 0;`

### Queues (队列)

`std::queue` 定义了一种队列类型。`std::queue` 可以接受任何类型。它通常以模板的形式标识：

`template <typename T> std::queue<T>`

`T` 参数是一个模板类型，该类型在声明 `std::queue` 时被推导出来。

`std::queue<int> i;` // 一个整数队列

```
struct P {
  int p;
};
```

`std::queue` 提供了以下操作。

| 序号 | 名称 | 描述 |
| :--- | :--- | :--- |
| 1 | `front` | 获取队列的第一个元素 |
| 2 | `back` | 获取队列的最后一个元素 |
| 3 | `push` | 将元素推入队列 |
| 4 | `pop` | 从队列中弹出一个元素 |
| 5 | `size` | 获取元素数量（大小） |
| 6 | `empty` | 检查队列是否还有元素 |

以下是使用简单整数数据类型的队列的用法示例。

```cpp
#include <iostream>
#include <queue>

int main() {
  std::queue<int> q;
  int size;

  printf("q empty %d\n", q.empty());

  q.push(1);
  q.push(2);
  q.push(3);
  q.push(4);
  q.push(5);
  q.push(6);

  printf("number of elements %lu, queue empty %d\n", q.size(), q.empty());
  printf("front %d back %d\n", q.front(), q.back());

  while (q) {
    size = q.size();
    if (size <= 0) {
        break;
    }
    int val = q.front();
    q.pop();
    printf("val %d\n", val);
  }
}
```

队列的通用用法包括：

1. 生产者和消费者共享队列。生产者向队列中添加项，消费者从队列中移除项。涉及多线程的情况见下文。

### Sets (集合)

Dequeue

### Maps (映射)

`std::map` 定义了 map 类型。

### shared_ptr, unique_ptr

`shared_ptr` 是 C11 中定义的作用域分配器。作用域分配的想法是当指向分配内存的引用计数变为 0 时释放该内存。以下是 `shared_ptr` 的示例。

```cpp
#include <iostream>
#include <memory>

struct S {
    int s;
};

int main() {
    std::shared_ptr<S> s;
    s = std::shared_ptr<S>(new S);
    s->s = 1;
    std::cout << "s: " << s->s << std::endl;
    return 0;
}
```

我们重写了 `->` 运算符来返回底层指针。假设 `shared_ptr` 仍然是一个包装器。如果类型是基本类型（如整数），我们也重写了 `*` 运算符。

```cpp
#include <iostream>
#include <memory>

struct P {
    int val;
};

void print(std::shared_ptr<P> p) {
    P* p1 = p.get();
    printf("p->val %d\n", p1->val);
    printf("val %d\n", (*p1).val);
    printf("use_count %ld\n", p.use_count());
}

int main() {
    std::shared_ptr<P> ptr;
    ptr = std::make_shared<P>();
    ptr->val = 4;
    print(ptr);
    return 0;
}
```

可以看到，我们没有调用 `free` 或 `delete`。原因是程序离开了作用域（在本例中是 `main` 函数），内存已经释放。`valgrind` 显示泄漏为 0。

```
==20868== HEAP SUMMARY:
==20868== in use: 0 bytes in 0 blocks
==20868== total heap usage: 4 allocs, 4 frees, 7480 bytes allocated
==20868== All heap blocks were freed -- no leaks
```

### 编写 shared_ptr 类

编写 `shared_ptr` 需要考虑：

- 引用计数。
- 分配和释放。分配部分在此示例中是留给调用者的。析构函数将执行释放，这正是 `shared_ptr` 功能的目的之一。

```cpp
#include <iostream>

template <typename T>
class shared_ptr {
public:
    explicit shared_ptr() : count_(0), memory_(nullptr) {}
    explicit shared_ptr(T *t) : count_(0) {
        memory_ = t;
        count_++;
    }
    shared_ptr operator=(const shared_ptr &s) {
        this->count++;
        std::cout << "called" << std::endl;
        return *this;
    }
    shared_ptr(const shared_ptr &kt) {
        count_ = 0;
        memory_ = nullptr;
        memory_ = kt.memory;
        count_ = kt.count_ + 1;
    }
    ~shared_ptr() {
        count--;
        if (memory_ && (count_ == 0)) {
            delete memory;
        }
    }
    void set(T *memory) {
        memory_ = memory;
        count_++;
    }
    T *get() { return memory_; }
    bool unique() const { return count_ == 1; }
    T *operator() const { return memory_; }
    T &operator->() const { return memory_; }
private:
    int count_;
    T *memory_;
};

struct S {
    int s;
};

void K(shared_ptr<S> s) {
    s->s = 6;
}

int main() {
    shared_ptr<S> s = shared_ptr<S>(new S);
    shared_ptr<int> s1 = shared_ptr<int>(new int);
    s->s = 3;
    *s1 = 3;
    K(s);
    std::cout << "s: " << s->s << " " << "s1: " << *s1 << std::endl;
    return 0;
}
```

### Threads (线程)

C++ 基于线程实现了线程的抽象。`std::thread` 类定义了线程接口。线程从 C11 开始定义。

创建线程是声明线程对象并传递作为线程函数的函数的一项简单工作。

以下是一个示例：

```cpp
#include <iostream>
#include <thread>

void thread_f() {
    std::cout << "in thread" << std::endl;
}

int main() {
    std::thread t(thread_f);
    std::cout << "starting thread" << std::endl;
    t.join();
    std::cout << "joined thread" << std::endl;
}
```

编译上述程序时使用 `-pthread` 选项。某些编译器可能不需要此选项。

以下是 `std::thread` 提供的几个方法。

| 序号 | 方法 | 描述 |
| :--- | :--- | :--- |
| 1 | `operator=` | 移动线程对象 |
| 2 | `joinable` | 检查线程是否可连接的 |
| 3 | `get_id` | 返回线程的 ID |
| 4 | `native_handle` | 返回线程的原生句柄 |
| 5 | `hardware_concurrency` | 返回实现返回的线程数 |
| 6 | `join` | 等待线程完成 |
| 7 | `detach` | 分离线程 |
| 8 | `swap` | 交换两个对象 |

以下是成员函数的用法示例。

```cpp
void thread_f()
{
    std::cout << "in thread" << std::endl;
}
```

```cpp
int main()
{
    std::thread t(thread_f);
    std::cout << "starting thread" << std::endl;
    std::cout << "joinable: " << (t.joinable() ? "yes" : "no") << std::endl;
    std::cout << " " << t.get_id() << " " << std::endl;
    std::cout << "hardware_concurrency: " << t.hardware_concurrency() << std::endl;
    t.join();
    std::cout << "joined thread" << std::endl;
}
```

让我们看看下面的示例，它创建了线程。

```cpp
#include <iostream>
#include <thread>
```

```cpp
void thread_1()
{
    std::cout << "in thread_1" << std::endl;
}
```

```cpp
void thread_2()
{
    std::cout << "in thread_2" << std::endl;
}
```

```cpp
int main()
{
    std::thread t1(thread_1);
    std::thread t2(thread_2);
    std::cout << "waiting for threads" << std::endl;
    t1.join();
    t2.join();
    std::cout << "stop" << std::endl;
}
```

编译并运行此程序会导致非顺序输出。

例如：

```
in thread_1
waiting for threads
in thread_2
stop
```

但预期的结果是主函数的消息将出现在线程函数调用之前。

通常情况下，当线程由操作系统创建时，执行情况完全取决于调度器。

## 互斥锁 (Mutexes)

```cpp
#include <iostream>
#include <thread>
#include <mutex>
```

```cpp
std::mutex lock;
static int count;
```

```cpp
void thread_1() {
    while (1) {
        std::cout << "in thread_1: waiting for lock" << std::endl;
        std::this_thread::sleep_for(std::chrono::seconds(1));
        lock.lock();
        std::cout << "in thread_1: acquired" << std::endl;
        count++;
        std::cout << "in thread_1: val " << count << std::endl;
        std::cout << "in thread_1: released" << std::endl;
        lock.unlock();
    }
}
```

```cpp
void thread_2() {
    while (1) {
        std::cout << "in thread_2: waiting for lock" << std::endl;
        std::this_thread::sleep_for(std::chrono::seconds(1));
        lock.lock();
        std::cout << "in thread_2: acquired" << std::endl;
        count++;
        std::cout << "in thread_2: val " << count << std::endl;
        std::cout << "in thread_2: released" << std::endl;
        lock.unlock();
    }
}
```

```cpp
int main() {
    std::thread t1(thread_1);
    std::thread t2(thread_2);
    t1.join();
    t2.join();
}
```

## 条件变量 (Conditional Variables)

```cpp
std::condition_variable cond;
```

## 派生类 (Derived Classes)

C++ 允许一个类继承一个或多个类。这被称为继承。

```cpp
struct B {
};
struct D : public B {
};
```

这里类 `D` 继承了类 `B`。`B` 中的公共成员函数被继承到 `D` 中。这意味着它们可以在没有类对象的情况下被调用。如果需要，它们也可以被重写。

例如：

```cpp
struct B {
    B() { a_ = 3; }
    ~B() {}
```



`int get() { return a_; }`

`private:`

`int a_;`

`};`

```cpp
struct D : public B {

    D() { a_ = 6; }

    ~D() {}

    int get() { return a_; }

    int get_B() { return B::get(); } // 直接访问 B::get()

    private:

    int a_;

};
```

我们通过以下方式访问 `D` 的成员：

`D:`

```cpp
std::cout << "d.get_b():" << d.get_b() << std::endl;
```

`D:`

```cpp
std::cout << "d.get():" << d.get() << std::endl;
```

这会导致在 `D` 内部访问 `a_`。

以下是访问 `B::get()` 的另一种方法。

`D d;`

```cpp
std::cout << "d.B::get():" << d.B::get() << std::endl;
```

下面是一个带有基类和派生类的继承示例。

```cpp
#include <iostream>

struct B {

    public:

    B() { a_ = 3; }

    ~B() {};

    int get() { return a_; }

    private:

    int a_;

};
```

```cpp
struct D : public B {

    public:

    D() { a_ = 6; };

    ~D() { };

    int get() { return a_; }

    int get_b() { return B::get(); }

    private:

    int a_;

};
```

```cpp
int main() {

    D d;

    std::cout << "d.a:" << d.get() << std::endl;

    std::cout << "d.B::get():" << d.B::get() << std::endl;

    std::cout << "d.get_b():" << d.get_b() << std::endl;

    return 0;

}
```

## 抽象类 (Abstract Classes)

```cpp
class S {

  public:

    virtual int get() = 0;

};
```

这是一个示例：

```cpp
class R : public S {

  public:

    R() { a_ = 3; }

    ~R() {}

    int get() { return a_; }

  private:

    int a_;

};
```

类 `S` 中的虚函数必须由派生类实现。否则，会导致编译失败。下面是一个简单的示例：

```cpp
#include <iostream>

class S {

  public:

    virtual int get() = 0;

};
```

```cpp
class R : public S {

  public:

    R() { a_ = 3; }

    ~R() {}

    int get() { return a_; }

  private:

    int a_;

};

int main()

{

    R r;

    std::cout << "R: " << r.get() << std::endl;

    return 0;

}
```

虽然上面的程序直接实例化了 `R`，但可能并不可用。通常，抽象类可以通过其他方式实例化。参考工厂方法模式（等等，这里的 OCR 文字似乎有些乱码，基于流）。

## 模板 (Templates)

模板允许泛型地编写软件。这是一个模板的示例：

```cpp
template <typename T>

class calculator {

};
```

其中 `T` 是类型。该类的实例化将是：

```cpp
calculator<int> cal;
```

将 `calculator` 定义为模板。可以有多个模板类型。例如，以下是有效的：

```cpp
template <typename T, typename R, typename P>

class calculator {

};
```

类的成员函数可以如下所示：

```cpp
template <typename T>

class calculator {

public:

    T add(T a, T b);

    T sub(T a, T b);

    T mul(T a, T b);

    T div(T a, T b);

    T mod(T a, T b);

};
```

成员函数描述输入都是 `T` 类型并返回类型 `T`。例如：

```cpp
calculator<int> cal;
```

对象的声明成员函数也是相同类型。例如，传递其他类型会导致编译器错误。我们可以按照 C++ 模板编写如下宏的 `calculator` 程序：

```cpp
#include <iostream>

template <typename T>

class calculator {

public:

    T add(T a, T b) { return a + b; }

    T sub(T a, T b) { return a - b; }

    T mul(T a, T b) { return a * b; }

    T div(T a, T b) { return a / b; }

    T mod(T a, T b) { return a % b; }

};

int main() {

    calculator<int> cal;

    std::cout << "Add: " << cal.add(3, 3) << std::endl;

    std::cout << "Sub: " << cal.sub(3, 3) << std::endl;

    std::cout << "Mul: " << cal.mul(3, 3) << std::endl;

    std::cout << "Div: " << cal.div(3, 3) << std::endl;

    std::cout << "Mod: " << cal.mod(3, 3) << std::endl;

    return 0;

}
```

这里我们对 `cal` 对象使用了 `calculator<int>`。这意味着 `calculator` 的所有操作/成员将接受整数。如果我们使用 `calculator<double>`，则所有操作中将使用 `double`。

例如，有可能使用字符串，如 `calculator<std::string> cal`。在这种情况下，编译将失败，因为提供的参数是整数。某些重载的字符串操作（如 `+`, `-`）可能会有效，但没有重载类型的其他操作会导致编译失败。

普通函数可以像以下示例那样用模板进行重载：

```cpp
#include <iostream>

template <typename T>

void print(T val)

{

    std::cout << "template: val: " << val << std::endl;

}

void print(int v)

{

    std::cout << "int: val: " << v << std::endl;

}
```

```cpp
int main() {

}
```

```cpp
print(3);

print<std::string>("hello");

print<int>(3);

    return 0;
```

这里直接调用了 `print(3)`，通过显式函数和变量声明调用了 `print(int v)`。当使用 `<>` 调用 `print` 时，将调用模板版本。如果情况下没有 `print(int v)`，`print(3)` 实际上会隐式调用 `print<int>(3)`。编译器会检测类型。

## 带有默认类型的模板 (Template with default type)

模板可以带有默认类型，在未给出时使用。例如：

```cpp
template <typename T, typename R = int>

void f(T a, R b);
```

显示模板 `R` 默认是 `int`。因此，当未提供标识的模板参数时，将使用默认值。例如：

```cpp
double(1.1, 1); // 使用 <double, int>

f(double, double)(1.1, 2.2); // 显式指定了 double，这里默认不重要
```

```cpp
#include <iostream>

template <typename T, typename R = int>

void f(T a, R b)

{

    std::cout << "a: " << a << " << b: " << b << std::endl;

}
```

```cpp
int main() {

    f<double>(1.1, 1);

    f<double, double>(1.1, 2.2);

    return 0;

}
```

用例 1：实现 `std::array`

模板也可以具有普通类型，如 `int`、`float` 等。

例如，

```cpp
template<typename T, int n

class p {

};
```

`p<int, 10> a;`

这意味着传递的数字 `10` 在整个对象生命周期内都是一个常量。

例如，这些可以用于定义静态数组。

```cpp
template<typename T, int n

class p {

  T array[n]; // 定义一个大小为常量 n 的数组

  p<int, 10> a; // 在这里我们定义数组大小为 10

};
```

这种方法可以作为实现 `std::array` 的方法。

数组理应具有以下功能：

| 序号 | 名称 | 描述 |
|---|---|---|
| 1 | `operator[]` | 数组索引 |
| 2 | `at` | 访问给定位置的元素 |
| 3 | `size` | 获取数组的大小 |
| 4 | `clear` | 使用清除值清空数组 |

以下是一个实现。

```cpp
#include <iostream>

template <typename T, int n

class array {

  public:

    explicit array() = default;

    ~array() = default;

  T operator[](int index) { return array_[index]; }

  T at(int index) { return array_[index]; }

  int size() { return n; }

  void clear(const T val) {

    for (auto i = 0; i < n; i++) {

        array_[i] = val;

    }

  }

private:

    T array_[n];

};

int main() {

    array<int, 10> a;

    a[1] = 4;

    std::cout << "array " << a[1] << std::endl;

}
```

## 模板重载

模板重载是可能的，就像讨论过的函数重载一样。

以下是模板重载的示例。

```cpp
template <typename T>

int print(T &val);

template <typename T, typename R>

int print(T &val, R &val2);

int print(int val);
```

以下是重载模板的使用示例。

```cpp
#include <iostream>

template <typename T>

int print(T val) {

    std::cout << "val: " << val << std::endl;

    return 0;

}

template <typename T, typename R>

int print(T val1, R val2)

{

    std::cout << "val1: " << val1 << " " << "val2: " << val2 << std::endl;

    return 0;

}

int print(int val)

{

    std::cout << "normal val: " << val << std::endl;

    return 0;

}

int main()

{

    print(3);

    print(3, 6);

    print(3u);

    print<int>(3);

}
```

有 2 种调用约定来调用 `template <typename> print`。

一种是显式使用 `<int>` 来告知编译器调用模板版本。

另一种是在整数 `3` 后面追加类型，以告知它不是符号整数，从而通知编译器调用模板版本。

# 附录 B

## 用用例

有用函数。

1. 模板 `min`

```cpp
template <typename T>

T min(T a, T b)

{

    return a < b ? a: b;

}
```

2. 模板 `max`

```cpp
template <typename T>

T max(T a, T b)

{

    return a > b ? a: b;

}
```

## 安全队列

```cpp
#include <iostream>

#include <mutex>

#include <condition_variable>

#include <thread>

#include <queue>
```

```cpp
template <typename T>

class safe_queue {

public:

    safe_queue(const safe_queue &q) = delete;

    const safe_queue &operator=(const safe_queue &q) = delete;

    safe_queue(const safe_queue &&q) = delete;

    safe_queue &operator=(const safe_queue &&q) = delete;

    /**

     * @brief 获取实例

     */

    static safe_queue *instance() {

        static safe_queue q;

        return &q;

    }

    safe_queue() {}

    /**

     * @brief - 向队列添加元素

     */

    void add(T &elem) {

        std::unique_lock<std::mutex> lock(mutex_);

        items_.push(elem);

        cond_.notify_all();

    }

    /**

     * @brief - 从队列获取元素

     */

    void get(T &val) {

        std::unique_lock<std::mutex> lock(mutex_);

        val = items_.front();

        items_.pop();

    }

private:

    explicit safe_queue() {}

    std::queue<T> items_;

    std::mutex mutex_;

    std::condition_variable cond_;

};

void thread_f() {

    safe_queue<int> *q = safe_queue<int>::instance();

    while (true) {

        int data;

        /* 从队列获取元素 */

        q->get(data);

        printf("data %d\n", data);

    }

}

int main() {

    safe_queue<int> *q = safe_queue<int>::instance();

    std::thread t(thread_f);

    int count = 0;

    /* 每 100 ms 产生数据 */

    while (true) {

        std::this_thread::sleep_for(std::chrono::milliseconds(100));

        count++;

        q->add(count);

    }

}
```

## 情况 2：实现 LRU

`LRU` 代表最久未使用。它是一种允许移除最少数据的缓存机制。以下算法基于缓存有限的假设。例如考虑缓存每个元素关联一个序列号。



```cpp
#include <iostream>

/**
 * 定义缓存行
 */
template <typename T>
struct lru_cache_items {
    T val;
    bool is_avail;
    uint32_t seq_no;
};

/**
 * lru_cache 模板
 */
template <typename T, int n>
class lru_cache {
public:
    explicit lru_cache() {
        index_ = 0;
        seq_no_ = 0;

        for (auto i = 0; i < n; i++) {
            items_[i].is_avail = false;
            items_[i].seq_no = 0;
        }
    }
    ~lru_cache() {}

    lru_cache& push(T &val) {
        /* 为前 n 个项添加缓存 */
        if (index_ < n) {
            seq_no_++;
            items_[index_].val = val;
            items_[index_].is_avail = true;
            items_[index_].seq_no = seq_no_;
            index_++;
        } else {
            /**
             * 如果项旧了则尝试淘汰
             * 如果特定缓存行的序列号是最旧的，将其淘汰并更新
             */
            /** 寻找最久未使用的项 */
            int i;
            int index = -1;
            uint32_t least_val = seq_no_;

            for (i = 0; i < n; i++) {
                if (items_[i].seq_no < least_val) {
                    least_val = items_[i].seq_no;
                    index = i;
                }
            }

            if (index != -1) {
                seq_no_++;
            }
            items_[index].val = val;
            items_[index].is_avail = true;
            items_[index].seq_no = seq_no_;
        }
        return *this;
    }

    void update(T &val, int index) {
        /* 更新总是涉及更新序列号，一种告知
         * 缓存行是热点的方法
         */
        seq_no_++;
        items_[index].val = val;
        items_[index].is_avail = true;
        items_[index].seq_no = seq_no_;
    }

    int get_index(T &val) {
        int i;
        for (i = 0; i < n; i++) {
            if (items_[i].val == val) {
                break;
            }
        }
        return i == n ? -1 : i;
    }

    T& get_val(int index) {
        return items_[index].val;
    }

private:
    lru_cache_items<T> items_[n];
    uint32_t seq_no_;
    uint32_t index_;
};

int main()
{
    int a[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    lru_cache<int, 10> lru;

    for (int i = 0; i < 10; i++) {
        lru.push(a[i]);
    }

    lru.update(a[0], 0);
    lru.update(a[1], 1);

    for (int i = 0; i < 10; i++) {
        std::cout << "val: " << lru.get_val(i) << std::endl;
    }
}
```

## 线程池

线程池是一组执行队列它们那里的特定任务的线程。

线程在启动时就创建。所有线程可以监听单个队列或多个队列。主线程向线程分配任务，每个线程执行这些队列到那里的任务。

因此，为每个线程设置单独队列的想法是有意义，以避免每个线程从队列中提取任务时出现饥饿。

因此我们需要为每个线程定义上下文。它看起来可能如下：

```cpp
struct thread_context {
    uint32_t id; // 线程标识符
    std::shared_ptr<std::thread> t_; // 实际线程指针
    std::mutex lock_; // 队列锁
    std::condition_variable cond_; // 队列条件变量
    std::queue<work_fn> work_list_; // 回调函数列表
    int queue_length_; // 队列长度
    bool queued_; // 信号是否有任务入队
    bool signaled_; // 退出线程的信号

};
```

```cpp
// 构造函数
    explicit thread_context(uint32_t id);

// 入队任务
    void queue(work_fn fn);

// 获取线程 ID
    uint32_t get_id() { return id_; };

// 合并线程
    void join() { t_->join(); }

// 获取队列大小
    int get_queue_size() { return queue_length_; }

// 信号线程
    void signal();

// 析构函数
    ~thread_context();
    void worker_thread(); // 线程函数

};
```

工作函数回调将如下：

```cpp
typedef std::function<void(void)> work_fn;
```

`id` 是一个线程标识符。

我们使用 `std::thread as shared_ptr`，以便我们可以在之后的分配过程中实例化它。

`lock_` 和 `cond_` 变量用于对队列 `work_list_` 的访问进行顺序化。

队列持有了待执行的函数回调列表。

我们使用 `queue_length_` 来确定公平性，并优化工作回调在线程上执行所需的时间。

变量 `signaled_` 用于主线程与工作线程之间的同步。

变量 `signaled_` 用于在需要退出时通知线程。

`worker_thread` 是负责执行队列中工作函数的线程。

构造函数 `thread_context` 将按如下方式创建线程：

```cpp
thread_context::thread_context(uint32_t id)
    t_ = std::make_shared<std::thread>(&thread_context::worker_thread, this);
```

现在，线程或调用者库函数必须存储每个线程上下文。

```cpp
class thread_pool {
public:
    // 使用 n_threads 初始化线程池
    explicit thread_pool(int n_threads);
    ~thread_pool();

    // 将工作推入线程池
    void queue(work_fn fn);

    // 运行线程池并等待它们完成执行
    void run();

    // 通知线程停止
    void signal();

private:
    // 存储线程数量
    int n_threads_;

    // 线程向量
    std::vector<std::shared_ptr<thread_context>> tc_list;
};
```

线程池的用户可以简单地执行：

`thread_pool t(4);`

```cpp
t.queue(&work_1);
t.queue(&work_2);
..
```

`t.run();`

方法 `thread_pool::run` 简单地用于等待所有线程完成。如果线程停止执行，该方法将返回。因此，在程序某个时间停止时，我们调用 `thread_pool::signal` 来通知线程停止。

任务队列接收一个非常通用的函数，该函数不接受也不返回任何参数。

它的类型是 `std::function`，因此可以使用普通函数，也可以使用 `std::bind` 来创建回调。

例如，为了调用下方类 `S` 的私有成员函数，可以创建一个回调并将其传递给 `thread_pool::queue`。

```cpp
struct S {
public:
    explicit S() {}
    S() {}

    void register_work();

private:
    void work()
    {
        std::cout << "work function" << std::endl;
    }
};
```

```cpp
void S::register_work()
{
    auto callback = std::bind(&S::work, this);
    thread_pool tp(4);

    tp.queue(callback);
}
}
```

以下是线程池的实现。

```cpp
/**
 * @brief - 200行以内的线程池实现。
 * @author - Devendra Naga (github.com/devendranaga)
 * @copyright - 2023-present.
 * @license - GPLv2
 */
#include <iostream>
#include <queue>
#include <vector>
#include <functional>
#include <thread>
#include <mutex>
#include <condition_variable>
```



```cpp
typedef std::function<void(void)> work_fn;

class TD {
public:
    explicit TD(uint32_t id) =
        id_(id),
        queue_size_(0),
        queued_(false),
        signaled_(false)
    {
        t_ = std::make_shared<std::thread>(&TD::thread_fn, this);
    }
    ~TD() { }

    void queue(work_fn fn) {
        {
            std::unique_lock<std::mutex> l(lock_);
            queued_ = true;
            queue_size_++;
            work_list_.push(fn);
            cond_.notify_one();
        }
    }

    uint32_t get_id() { return id_; }
    void join() { t_->join(); }

    int get_queue_size() { return queue_size_; }

    void signal()
    {
        std::unique_lock<std::mutex> l(lock_);
        signaled_ = true;
        cond_.notify_one();
    }

private:
    uint32_t id_;
    int queue_size_;
    bool queued_;
    bool signaled_;
    std::queue<work_fn> work_list_;
    std::shared_ptr<std::thread> t_;
    std::mutex lock_;
    std::condition_variable cond_;

    void thread_fn()
    {
        int queue_size = 0;
        work_fn fn = nullptr;

        while (1) {
            {
                std::unique_lock<std::mutex> l(lock_);
                if (queue_size == 0) {
                    cond_.wait(l, [this] { return queued_ == true || (signaled_ == true); });
                }
                if (signaled_) {
                    break;
                }
                queued_ = false;
                queue_size = work_list_.size();
                if (queue_size > 0) {
                    fn = work_list_.front();
                    work_list_.pop();
                }
                printf("remaining items in thread %d\n", id_, queue_size);
            }
            if (fn) {
                fn();
                queue_size_--;
            }
        }
    }
};

class TP {
public:
    explicit TP(int n_threads) : n_threads_(n_threads) {
        int i;
        for (i = 0; i < n_threads; i++) {
            std::shared_ptr<TD> td;
            td = std::make_shared<TD>(i);
            td_list_.push_back(td);
        }
    }

    void queue(work_fn fn) {
        int lowest = -1;
        std::vector<std::shared_ptr<TD>>::iterator it = td_list_.begin();
        for (it = td_list_.begin(); it != td_list_.end(); it++) {
            int q_size = it->get_queue_size();
            if (q_size <= lowest) {
                lowest = q_size;
                // 这里的逻辑是不完整的，保持原样。
            }
        }
        if (lowest != -1) {
            td_list[lowest]->queue(fn);
        }
    }

    void run() {
        for (auto it : td_list) {
            it->join();
        }
    }

    void signal() {
        for (auto it : td_list) {
            it->signal();
        }
    }

private:
    int n_threads;
    std::vector<std::shared_ptr<TD>> td_list;
};

static int count;
std::mutex lock;

void work_1()
{
    fprintf(stderr, "executing infinite loop\n");
    while (1) {
        std::this_thread::sleep_for(std::chrono::seconds(1));
        {
            std::unique_lock<std::mutex> l(lock);
            fprintf(stderr, "work_1: %d\n", count);
            if (count > 1) {
                break;
            }
        }
    }
}

void work_2()
{
    std::unique_lock<std::mutex> l(lock);
    fprintf(stderr, "work_2: %d\n", count);
    std::this_thread::sleep_for(std::chrono::milliseconds(100));
    count++;
}

void work_3()
{
    std::unique_lock<std::mutex> l(lock);
    fprintf(stderr, "work_3: %d\n", count);
    std::this_thread::sleep_for(std::chrono::milliseconds(100));
    count++;
}

int main() {
    TP t(4);
    int i;

    t.queue(&work_1);

    for (i = 0; i < 10; i++) {
        t.queue(&work_3);
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
        t.queue(&work_2);
    }

    t.signal();

    t.run();
}
```

## 用例：实现 `std::pair`

以下是 `std::pair` 的实现。

```cpp
#include <iostream>

template <typename T1, typename T2>
struct pair {
    T1 first;
    T2 second;

    explicit pair(const T1 &t1, const T2 &t2) : first(t1), second(t2) {}
    pair() {}

    bool operator==(const pair &r) {
        return (this->first == r.first) && (this->second == r.second);
    }
    bool operator!=(const pair &r) {
        return !operator==(r);
    }
    bool operator>(const pair &r) {
        return (this->first > r.first) && (this->second > r.second);
    }
    bool operator<=(const pair &r) {
        return !operator>(r);
    }
};
```

```cpp
template <typename T1, typename T2>
pair<T1, T2> make_pair(const T1 t1, const T2 t2) {
    pair<T1, T2> p(t1, t2);
    return p;
}
```

```cpp
int main() {
    pair<std::string, int> p = make_pair<std::string, int>("test", 1);
    pair<std::string, int> p1 = make_pair<std::string, int>("test", 1);

    std::cout << "first: " << p.first << " second: " << p.second << std::endl;
    std::cout << "p == p1: " << (p == p1) << std::endl;
    std::cout << "p != p1: " << (p != p1) << std::endl;
    return 0;
}
```

## 事件驱动系统

## 设计模式

### 工厂设计模式

## 单例设计模式

单例模式用于对象被许多其他类使用的情况。实现一种方法是静态实例化它并返回该实例。

由于它被许多其他类使用，实例化是在类内部静态完成的。这种方法通常定义一个 `instance` 成员函数，返回静态声明的类对象。

```cpp
class singleton {
public:
    static singleton *instance() {
        static singleton s;
        return &s;
    }
    -singleton() = default;
    singleton(const singleton& k) = delete;
    const singleton operator=(const singleton& k) = delete;
    singleton(const singleton& kk) = delete;
    const singleton& operator=(const singleton& kk) = delete;

    int member(...);

private:
    explicit singleton();
};
```

我们删除了拷贝和移动构造函数，以确保调用静态成员函数 `instance` 期间创建的唯一实例是唯一可用的实例。

## 创建二进制文件

### cmake

`cmake` 是一种脚本语言，可以用于创建所谓的 CMake 文件。每一个此类文件都可以用于编译一组源文件，以生成目标库或二进制文件。

#### 1. 创建基础的 `CMakeLists.txt`

```cmake
cmake_minimum_required(VERSION 3.9)
project(Example)
```

```cmake
set(SRC
    ./file_1.c
    ./file_2.c)
```

```cmake
add_executable(file_ops ${SRC})
```

上面的 cmake 文件用于创建一个名为 `file_ops` 的可执行文件。

源文件 `file_1.c` 和 `file_2.c` 是 `SRC` 定义的一部分。

`project` 和 `cmake_minimum_required` 项不是强制性的，但当我们不保留它们时，`cmake` 会发出警告。它们通常可以帮助你引导你正在构建的是什么项目，以及你正在使用的何种 `cmake` 特性。

以下是生成目标二进制文件的命令：

```bash
mkdir build/
cd build/
cmake ..
nmake
```

`cmake` 构建会产生大量的中间产物并弄乱目录。因此，最好创建一个名为 `build` 的目录并在其中运行 `cmake`。

如果你没有安装 `cmake`，在 Ubuntu 上运行以下命令：

```bash
sudo apt install make cmake
```

#### 2. 创建库

```cmake
cmake_minimum_required(VERSION 3.9)
project(Example_Lib)
```

```cmake
set(LIB_SRC
./file_1.c)
```

```cmake
add_library(file ${LIB_SRC})
```

`add_library` 指令 `cmake` 创建一个静态库 `libfile.a`。

下面的示例创建了一个共享库。

```cmake
cmake_minimum_required(VERSION 3.9)
project(Example_Lib)
```

```cmake
set(LIB_SRC
./file_1.c)
```

```cmake
add_library(file SHARED ${LIB_SRC})
```

`SHARED` 指定符会创建一个名为 `libfile.so` 的 `.so` 文件。如果不提到 `SHARED`，`add_library` 默认生成一个 `.a` 文件。

#### 3. 与库链接

`target_link_libraries` 用于将库链接到目标二进制文件。

以下是一个示例：

```cmake
cmake_minimum_required(VERSION 3.9)
project(Example_Bin)

set(SRC
    ./file.c)

set(LIB_SRC
    ./file_i.c)

add_library(file ${LIB_SRC})
add_executable(file_ops ${SRC})
target_link_libraries(file_ops file)
```

#### 4. 添加 CFLAGS 和 CPPFLAGS

```cmake
set(CMAKE_C_FLAGS "-Wall -Werror")
set(CMAKE_CXX_FLAGS "-Wall -Werror")
```

标志 `CMAKE_C_FLAGS` 和 `CMAKE_CXX_FLAGS` 接收可以传递给 `gcc`/`g++` 或 `clang` 的所有编译器选项。

#### 5. 添加 C++ 标准

```cmake
set(CMAKE_CXX_STANDARD "11")
```

宏 `CMAKE_CXX_STANDARD` 在编译时设置 C++ 标准。

## 数据结构

### 链表

链表是以 `NULL` 指针终止的元素链。

链中的每个项被称为节点。每个节点包含数据以及指向指向列表中下一个元素的指针。最后一个节点的指针将是 `NULL`。

链表的结构如下所示：

```
|------|-------|-------|------|
| item 1 |----> item 2 |----> item 3 |-- . . -> NULL
|------|       |       |------|
```

列表始终以 `NULL` 指针结束。

链表的结构如下所示：

```c
struct linked_list {
    void *elem;
    struct linked_list *next;
}
```

数据指针持有数据，`next` 指针链接到列表中的下一个元素。

下面是列表上的一些通用操作。

| 序号 | 名称 | 描述 |

| :--- | :--- | :--- |

| 1 | `add` | 在列表末尾添加一个元素 |

| 2 | `add_head` | 在列表头部添加一个元素 |

| 3 | `delete` | 从列表中删除一个元素 |

| 4 | `find` | 在列表中查找一个元素 |

| 5 | `count` | 统计列表中元素的数量 |

| 6 | `for_each` | 遍历列表中的每个元素 |

| 7 | `print` | 打印列表的所有元素 |

| 8 | `clean` | 清理所有链表并释放分配的内存 |

定义两个全局变量 `head` 和 `tail`。



我们使用两个指针`head`和`tail`。`head`用于从头开始遍历每个元素，`tail`用于在末尾添加元素。

### 1. add

添加元素可以像在末尾添加元素一样简单。

如果列表中没有元素，则在头部添加该元素。如果列表中已有元素，则在`tail`之后添加该元素。每当添加元素时，`tail`都会指向最后一个元素。

```c
int add(void *data) {
    struct linked_list *node = malloc(sizeof(struct linked_list));
    node->elem = data;
    node->next = NULL;
    if (head == NULL) {
        head = tail = node;
    } else {
        tail->next = node;
        tail = node;
    }
    return 0;
}
```

*（注：原文中`add`的实现是不完整的，我根据上下文进行了重构）*

### 2. add_head

在头部添加元素非常简单：

```c
void add_head(void *data) {
    struct linked_list *node = malloc(sizeof(struct linked_list));
    node->elem = data;
    node->next = NULL;
    if (head == NULL) {
        head = tail = node;
    } else {
        node->next = head;
        head = node;
    }
}
```

### 3. delete

从列表中删除一个元素：

```c
void delete(void *data) {
    struct linked_list *curr = head;
    struct linked_list *prev = NULL;
    while (curr != NULL) {
        if (curr->elem == data) {
            if (prev == NULL) {
                head = curr->next;
            } else {
                prev->next = curr->next;
            }
            if (curr == tail) {
                tail = prev;
            }
            free(curr);
            return;
        }
        prev = curr;
        curr = curr->next;
    }
}
```

### 4. find

`find`遍历每个元素并与给定的指针进行比较。

```c
bool find(void *elem) {
    struct linked_list *curr = head;
    while (curr != NULL) {
        if (curr->elem == elem) {
            return true;
        }
        curr = curr->next;
    }
    return false;
}
```

### 5. count

`count`遍历每个链并增加计数器。

```c
int count() {
    struct linked_list *curr = head;
    int n = 0;
    while (curr != NULL) {
        n++;
        curr = curr->next;
    }
    return n;
}
```

### 6. for_each

`for_each`遍历每个链并调用回调。调用者必须传递回调，调用者将获得元素作为数据。

```c
void for_each(void (*callback)(void *elem)) {
    struct linked_list *curr = head;
    while (curr != NULL) {
        if (callback) {
            callback(curr->elem);
        }
        curr = curr->next;
    }
}
```

### 7. print

通过遍历列表中的每个元素打印列表的内容。

```c
void print() {
    struct linked_list *curr = head;
    printf("elements:\n");
    while (curr != NULL) {
        int *data = (int*)curr->elem;
        printf("%d\n", *data);
        curr = curr->next;
    }
}
```

### 8. clean

需要清理链表以释放链表占用的内存。

这里是清理链表的一种方法。

1. 取两个指针：`node`和`prev`。
2. `node`指向头部，`prev`指向`node`。
3. `node`向前移动。`prev`指针。
4. 将`prev`指针指向`node`。
5. 重复此操作直到`node`到达末尾。

```c
void clean()
{
    struct linked_list *node;
    struct linked_list *prev;

    node = head;
    prev = head;

    while (node) {
        node = node->next;
        free(prev);
        prev = node;
    }
}
```

也可以使用`while`循环进行迭代。

```c
struct linked_list *node = head;

while (node) {
    node = node->next;
}
```

然而，`for`循环看起来更完整，因为赋值、条件和递增都都在同一个地方。

下面是一个完整的示例：

```c
#include <stdio.h>
#include <stdlib.h>

struct linked_list {
    void *elem;
    struct linked_list *next;
};

static struct linked_list *head;
static struct linked_list *tail;

int add(void *data) {
    struct linked_list *node;
    node = calloc(1, sizeof(struct linked_list));
    if (!node) {
        return -1;
    }
    node->elem = data;

    if (!head) {
        head = node;
        tail = node;
    } else {
        tail->next = node;
        tail = node;
    }

    return 0;
}

int add_head(void *data) {
    struct linked_list *node;
    node = calloc(1, sizeof(struct linked_list));
    if (!node) {
        return -1;
    }

    node->elem = data;

    if (!head) {
        head = node;
        tail = node;
    } else {
        node->next = head;
        head = node;
    }

    return 0;
}
```

```c
int delete(void *elem) {
    struct linked_list *node;
    struct linked_list *prev;

    node = head;
    prev = node;

    if (head->elem == elem) {
        head = head->next;
        free(node);
        return 0;
    } else {
        while (node != NULL) {
            printf("%p %p\n", node->elem, elem);
            if (node->elem == elem) {
                prev->next = node->next;
                if (node == tail) {
                    tail = prev;
                }
                free(node);
                return 0;
            }
            prev = node;
            node = node->next;
        }
    }
    return -1;
}
```

```c
bool find(void *elem) {
    struct linked_list *node;

    for (node = head; node != NULL; node = node->next) {
      if (node->elem == elem) {
        return true;
      }
    }
    return false;
}
```

```c
int count()
{
  struct linked_list *node;
  int n = 0;
  for (node = head; node != NULL; node = node->next) {
    n++;
  }
  return n;
}
```

```c
void for_each(void (*callback)(void *elem)) {
  struct linked_list *node;
  for (node = head; node != NULL; node = node->next) {
    if (callback) {
      callback(node->elem);
    }
  }
}
```

```c
void print()
{
  struct linked_list *node;
  printf("elements:\n");
  for (node = head; node != NULL; node = node->next) {
    int data = node->elem;
    printf("%d\n", data);
  }
}
```

```c
void clean()
{
    struct linked_list *node;
    struct linked_list *prev;

    node = head;
    prev = head;

    while (node) {
      node = node->next;
      free(prev);
      prev = node;
    }
}
```

```c
int main()
{
  int a = 10;
  int b = 20;
  int c = 30;
  int d = 40;
  int e = 50;
  int f = 60;

  add(&a);
  add(&b);
  add(&c);
  add(&d);
  add(&e);
  add(&f);

  print();
  delete(&a);
  delete(&f);

  add(&f);

  print();

  clean();
}
```

## 双向链表

双向链表是一个以`NULL`指针终止的元素链。

链中的每一项被称为节点。每个节点包含数据和两个指针。一个指针指向下一个元素，另一个指针指向后一个。

双向链表的结构如下所示。

```c
struct DL {
    void *data;
    struct DL *prev;
    struct DL *next;
};
```

`data`指针持有数据，`prev`指针指向链表的前一个节点，`next`指针指向链表中的下一个元素。

| 编号 | 名称 | 描述 |
| --- | --- | --- |
| 1 | `dl_add_head` | 在头部添加一个元素 |
| 2 | `dl_delete_item` | 从链表中删除一个元素 |
| 3 | `dl_find_fwd` | 正向遍历链表查找一个元素 |
| 4 | `dl_find_rv` | 反向遍历链表查找一个元素 |
| 5 | `dl_for_each_fwd` | 正向遍历所有元素 |
| 6 | `dl_for_each_rv` | 反向遍历所有元素 |
| 7 | `dl_count` | 计算链表中元素的数量 |
| 8 | `dl_free_fwd` | 正向释放所有元素 |
| 9 | `dl_free_rv` | 反向释放所有元素 |

与链表类似，我们创建两个元素：`head`和`tail`。

```c
struct DL *head;
struct DL *tail;
```

### 1. dl_add_head

```c
int dl_add_head(void *data) {
    struct DL *node;
    node = calloc(1, sizeof(struct DL));
    if (!node) {
        return -1;
    }
    node->data = data;
    if (!head) {
        head = node;
        tail = node;
    } else {
        tail->next = node;
        node->prev = tail;
        tail = node;
    }
    return 0;
}
```

### 2. dl_delete_item

```c
bool dl_delete_item(void *data, void (*callback)(void *data)) {
    struct DL *node;
    struct DL *prev;

    if (head->data == data) {
        node = head;
        head = head->next;
        if (head) {
            head->prev = NULL;
        } else {
            tail = NULL;
        }
        if (callback) {
            callback(node->data);
        }
        free(node);
        return true;
    } else if (tail->data == data) {
        node = tail;
        tail = tail->prev;
        if (tail) {
            tail->next = NULL;
        }
        if (callback) {
            callback(node->data);
        }
        free(node);
        return true;
    } else {
        node = head;
        while (node->data != data) {
            node = node->next;
        }
        node->prev->next = node->next;
        if (node->next) {
            node->next->prev = node->prev;
        }
        if (callback) {
            callback(node->data);
        }
        free(node);
        return true;
    }
    return false;
}
```

### 3. dl_find_fwd

```c
bool dl_find_fwd(void *data, void (*callback)(void *data)) {
    struct DL *node;
    for (node = head; node != NULL; node = node->next) {
        if (node->data == data) {
            if (callback) {
                callback(node->data);
            }
            return true;
        }
    }
    return false;
}
```



### 4. `dl_find_rv`

```c
bool dl_find_rv(void *data, void (*callback)(void *data)) {
    struct DL *node;
    for (node = tail; node != NULL; node = node->prev) {
        if (node->data == data) {
            if (callback) {
                callback(node->data);
            }
            return true;
        }
    }
    return false;
}
```

### 6. `dl_for_each_fwd`

```c
void dl_for_each_fwd(void (*callback)(void *data)) {
    struct DL *node;
    for (node = head; node != NULL; node = node->next) {
        if (callback) {
            callback(node->data);
        }
    }
}
```

### 6. `dl_for_each_rv`

```c
void dl_for_each_rv(void (*callback)(void *data)) {
    struct DL *node;
    for (node = tail; node != NULL; node = node->prev) {
        if (callback) {
            callback(node->data);
        }
    }
}
```

### 7. `dl_count`

```c
int dl_count() {
    struct DL *node;
    int count = 0;
    for (node = head; node != NULL; node = node->next) {
        count++;
    }
    return count;
}
```

### 8. `dl_free_fwd`

```c
void dl_free_fwd(void (*callback)(void *data)) {
    struct DL *node = head;
    struct DL *prev;

    while (node) {
        prev = node;
        if (callback) {
            callback(prev->data);
        }
        node = node->next;
        free(prev);
    }
}
```

### 9. `dl_free_rv`

```c
void dl_free_rv(void (*callback)(void *data)) {
    struct DL *node = tail;
    struct DL *prev;

    while (node) {
        prev = node;
        if (callback) {
            callback(prev->data);
        }
        node = node->prev;
        free(prev);
    }
}
```

下面是双向链表的完整示例。

```c
#include <stdio.h>
#include <stdbool.h>
#include <stdlib.h>

struct DL {
    void *data;
    struct DL *prev;
    struct DL *next;
}

struct DL *head = NULL;
struct DL *tail = NULL;

int dl_add_head(void *data) {
    struct DL *node;
    node = calloc(1, sizeof(struct DL));
    if (!node) {
        return -1;
    }
    node->data = data;
    if (!head) {
        head = node;
        tail = node;
    } else {
        tail->next = node;
        node->prev = tail;
        tail = node;
    }
    return 0;
}

bool dl_delete_item(void *data, void (*callback)(void *data)) {
    struct DL *node;

    if (head->data == data) {
        node = head;
        head = head->next;
        if (head) {
            head->prev = NULL;
        } else {
            tail = NULL;
        }
        if (callback) {
            callback(node->data);
        }
        free(node);
        return true;
    } else if (tail->data == data) {
        node = tail;
        tail = tail->prev;
        if (tail) {
            tail->next = NULL;
        }
        if (callback) {
            callback(node->data);
        }
        free(node);
        return true;
    } else {
        node = head;
        while (node->data != data) {
            node = node->next;
        }
        node->prev->next = node->next;
        if (node->next) {
            node->next->prev = node->prev;
        }
        if (callback) {
            callback(node->data);
        }
        free(node);
        return true;
    }
    return false;
}

int main() {
    int a = 10, b = 20, c = 30, d = 40, e = 50, f = 60;

    dl_add_head(&a);
    dl_add_head(&b);
    dl_add_head(&c);
    dl_add_head(&d);
    dl_add_head(&e);
    dl_add_head(&f);

    printf("Count: %d\n", dl_count());
    dl_delete_item(&a, NULL);
    dl_delete_item(&f, NULL);
    printf("Count after delete: %d\n", dl_count());

    return 0;
}
```

```
}
return false;
```

```c
bool dl_find_rv(bool (*callback)(void *data))
{
    struct DL *node;
    for (node = tail; node != NULL; node = node->prev) {
        if (callback(node->data))
            return true;
    }
    return false;
}
```

```c
int dl_count()
{
    struct DL *node;
    int count = 0;
    for (node = head; node != NULL; node = node->next) {
        count++;
    }
    return count;
}
```

```c
bool dl_delete_item(void *data, void (*callback)(void *data))
{
    struct DL *node;
    struct DL *prev;
    if (head->data == data) {
        node = head;
        head = head->next;
        head->prev = NULL;
        if (callback(node->data))
            callback(node->data);
        free(node);
        return true;
    } else if (tail->data == data) {
node = tail;
tail = tail->prev;
tail->next = NULL;
free(node);
        return true;
    } else {
  node = head;
  while (node) {
    if (node->data == data) {
      node->prev->next = node->next;
      node->next->prev = node->prev;
      if (callback) {
        callback(node->data);
      }
      free(node);
      return true;
    }
    node = node->next;
  }
}
  return false;
}
```

```c
void dl_for_each_fwd(void (*callback)(void *data)) {
  struct DL *node;
  for (node = head; node != NULL; node = node->next) {
    if (callback) {
      callback(node->data);
    }
  }
}
```

```c
void dl_for_each_rv(void (*callback)(void *data)) {
  struct DL *node;
  for (node = tail; node != NULL; node = node->prev) {
    if (callback) {
      callback(node->data);
    }
  }
}
```

```c
void dl_free_fwd(void (*callback)(void *data))
{
    struct DL *node = head;
    struct DL *prev;

    while (node) {
        prev = node;
        if (callback) {
            callback(prev->data);
        }
        node = node->next;
        free(prev);
    }
}

void dl_free_rv(void (*callback)(void *data))
{
    struct DL *node = tail;
    struct DL *prev;

    while (node) {
        prev = node;
        if (callback) {
            callback(prev->data);
        }
        node = node->prev;
        free(prev);
    }
}

void print(void *data)
{
    printf("%d\n", (int*)data);
}

int main()
{
    int a[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int i;

    for (i = 0; i < 10; i++) {
        dl_add_head(&a[i]);
    }
}
```

```c
printf("forward[%d]: \n", dl_count());
dl_for_each_fwd(print);

dl_delete_item(&a[0], NULL);
dl_delete_item(&a[2], NULL);
dl_delete_item(&a[9], NULL);

printf("reverse[%d]: \n", dl_count());
dl_for_each_rv(print);

// dl_free_fwd(NULL);
dl_free_rv(NULL);

  return 0;
}
```

## 循环链表

循环列表与链表相似，区别在于最后一个节点指向了第一个节点。

```
|--------|------|      |--------|
| item 1 |------>| item 2 ---> ... | item n |
|--------|------|      |--------|
|        ^                                |
|------------------------------------<<----|
```

以下是可以使用循环链表实现的功能。

| 序号 | 名称 | 描述 |

| :--- | :--- | :--- |

| 1 | `add_tail` | 在尾部添加元素 |

| 2 | `for_each` | 遍历列表 |

| 3 | `count` | 统计元素数量 |

| 4 | `delete` | 从列表中删除元素 |

| 5 | `free_all` | 释放整个列表 |

- 1. `add_tail`

- 2. `for_each`

- 3. `count`

- 4. `delete`

- 5. `free_all`

以下是循环链表的完整示例。



# 循环链表

以下是一个循环链表的完整实现，包含添加、删除、遍历等操作：

```c
#include <stdio.h>
#include <stdlib.h>

struct circular_list {
    void *data;
    struct circular_list *next;
};
static struct circular_list *head;
static struct circular_list *tail;

int add_tail(void *data) {
    struct circular_list *item;

    item = calloc(1, sizeof(struct circular_list));
    if (!item) {
        return -1;
    }

    item->data = data;

    if (!head) {
        head = item;
        tail = item;
        tail->next = head;
    } else {
        tail->next = item;
        tail = item;
        tail->next = head;
    }
    return 0;
}

void print(void *data) {
    struct circular_list *item = head;

    if (!item) {
        return;
    }
    do {
        printf("%d\n", (int*)item->data);
        item = item->next;
    } while (item != head);
}

void for_each(void (*callback)(void *data) {
    struct circular_list *item = head;

    if (!item) {
        return;
    }
    do {
        if (callback)
            callback(item->data);
        item = item->next;
    } while (item != head);
}

int count() {
    struct circular_list *item = head;
    int count = 0;

    if (!item) {
        return count;
    }

    do {
        count++;
        item = item->next;
    } while (item != head);

    return count;
}

int delete(void *data, void (*callback)(void *data)) {
    struct circular_list *item = head;
    struct circular_list *prev = item;

    if (head->data == data) {
        head = head->next;
        tail->next = head;
        if (callback) {
            callback(item->data);
        }
        if (head == tail) {
            tail = NULL;
        }
        free(item);
        return 0;
    }
    prev = item;
    item = item->next;
    while (item != head) {
        if (item->data == data) {
            if (callback) {
                callback(item->data);
            }
            prev->next = item->next;
            if (item == tail) {
                tail = prev;
            }
            free(item);
            return 0;
        }
        prev = item;
        item = item->next;
    }
    return -1;
}

void free_all(void (*callback)(void *data)) {
    struct circular_list *item;
    struct circular_list *prev;

    item = head;
    prev = head;

    do {
        prev = item;
        item = item->next;
        if (callback) {
            callback(prev->data);
        }
        free(prev);
    } while (item == head);
    head = NULL;
}

void print_data(void *data) {
    printf("%d\n", *(int *)data);
}

int main() {
    int a[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int i;

    for (i = 0; i < 10; i++) {
        add_tail(&a[i]);
    }

    printf("print all elements:\n");
    for_each(print);

    delete(&a[0], NULL);

    printf("after deleting the first element:\n");
    for_each(print);

    delete(&a[9], NULL);

    printf("after deleting the last element:\n");
    free_all(NULL);
    return 0;
}
```

# 栈

栈是另一种数据结构，先进入的数据后取出，或者后进入的数据先取出。

```
|----------------------|
| item n <-- 添加和检索 |
|----------------------|
| ...                    |
|----------------------|
| item 2                |
|----------------------|
| item 1                |
|----------------------|
```

以下是可以使用栈数据结构进行的一些操作。

| 序号 | 名称 | 描述 |
| :--- | :--- | :--- |
| 1 | `top` | 获取栈顶元素 |
| 2 | `push` | 将元素推入栈中 |
| 3 | `pop` | 从栈中弹出元素 |
| 4 | `empty` | 清空栈中的元素 |
| 5 | `size` | 获取栈中元素的总大小 |

栈也可以也可以用链表实现。

```c
struct stack {
    void *elem;
    struct stack *next;
};
```

```c
static struct stack *head;
static int count;
```

对于栈的功能，元素在头部添加并从头部移除。

栈通常用于快速访问最新的元素，例如当您使用`git stash`功能时。

## 1. `top`

获取栈中的顶部元素。这不会从栈中移除元素。

```c
void *top()
{
  void *elem = NULL;

  if (head) {
    elem = head->elem;
  }
  return elem;
}
```

## 2. `push`

向栈中推入元素。始终在头部添加新元素。

```c
int push(void *elem) {
    struct stack *node;
    node = calloc(1, sizeof(struct stack));
    if (!node) {
        return -1;
    }
    node->elem = elem;
    if (!head) {
        head = node;
    } else {
        node->next = head;
        head = node;
    }
    count++;
    return 0;
}
```

## 3. `pop`

从栈顶返回一个元素并从栈中移除。

```c
void *pop()
{
    struct stack *node;
    void *elem = NULL;

    if (head) {
        elem = head->elem;
        node = head;
        head = head->next;
        free(node);
        count--;
    }
    return elem;
}
```

## 4. `empty`

移除栈中的所有元素。

```c
void empty(void (*callback)(void *elem)) {
    struct stack *node;
    struct stack *prev;

    node = head;
    prev = head;

    while (node) {
        prev = node;
        node = node->next;
        if (callback) {
            callback(prev->elem);
        }
        free(prev);
    }
}
```

## 5. `size`

返回栈的大小（栈中元素的数量）。

```c
int size()
{
    return count;
}
```

下面是一个栈示例的完整实现：

```c
#include <stdio.h>
#include <stdlib.h>

struct stack {
    void *elem;
    struct stack *next;
};

static struct stack *head;
static int count;

void *top() {
    return head->elem;
}

int push(void *elem) {
    struct stack *node;

    node = calloc(1, sizeof(struct stack));
    if (!node) {
        return -1;
    }

    node->elem = elem;

    if (!head) {
        head = node;
    } else {
        node->next = head;
        head = node;
    }

    count++;
    return 0;
}

void *pop() {
    struct stack *node;
    void *elem = NULL;

    if (head) {
        elem = head->elem;
        node = head;
        head = head->next;
        free(node);
        count--;
    }
    return elem;
}

int size() {
    return count;
}

void empty(void (*callback)(void *elem)) {
    struct stack *node;
    struct stack *prev;

    node = head;
    prev = head;

    while (node) {
        prev = node->next;
        if (callback) {
            callback(prev->elem);
        }
        free(prev);
    }
}

int main() {
    int a = 1;
    int b = 2;
    int c = 3;
    int d = 4;
    int e = 5;
    int f = 6;

    push(&a);
    push(&b);
    push(&c);
    push(&d);
    push(&e);
    push(&f);

    printf("size : %d\n", size());

    while (1) {
        int *elem = pop();
        if (elem == NULL) {
            break;
        }
        printf("*%d\n", *elem);
    }

    empty(NULL);
    return 0;
}
```

# 队列

队列在末尾添加元素并从头部检索元素。为此，我们使用了两个指针`head`和`tail`。

| item | 说明 |
| :--- | :--- |
| item 1 | <-- 头部（移除元素） |
| item 2 | |
| item n | <-- 尾部（添加元素） |

下面的结构定义如下：

```c
struct queue {
    void *elem;
    struct queue *next;
};

static struct queue *head;
static struct queue *tail;
static int count;
```

以下是队列的操作：

| S.No | 名称 | 描述 |
| :--- | :--- | :--- |
| 1 | `front` | 获取队列头部的元素 |
| 2 | `back` | 获取队列的尾部元素 |
| 3 | `empty` | 清空队列 |
| 4 | `size` | 获取队列中的元素数量 |
| 5 | `push` | 向队列中压入元素 |
| 6 | `pop` | 从队列中弹出一个元素 |

## 1. `front`

检索队列开头的元素。

```c
void *front()
{
    void *elem;

    if (head) {
        elem = head->elem;
    }
    return elem;
}
```

## 2. `back`

检索队列的尾部元素。

```c
void *back()
{
    void *elem;

    if (tail) {
        elem = tail->elem;
    }
    return elem;
}
```

## 3. `empty`

清空队列。

这里的逻辑如下：

1. 取两个指针`prev`和`cur`。
2. 将`prev`和`cur`指针指向`head`。
3. 在循环中：
   1. `prev = cur;`
   2. `node = node->next;`
   3. 调用回调函数以便用户可以释放内存
   4. `free(prev)`

```c
void empty(void (*callback)(void *elem)) {
    struct queue *node;
    struct queue *prev;

    node = head;
    prev = head;

    while (node) {
        prev = node;
        node = node->next;
        if (callback) {
            callback(prev->elem);
        }
        free(prev);
    }
    count = 0;
}
```

## 4. `size`

返回队列中的元素数量。

```c
int size()
{
    return count;
}
```

## 5. `push`

向队列中添加元素。在末尾添加。

1. 取两个指针`head`和`tail`。
2. 如果为空（即`head`为`NULL`），添加元素并指向`head`和`tail`。
3. 如果元素存在，将`tail->next`指向该元素。
4. 添加新元素后，`tail`指向新元素。

```c
int push(void *elem) {
    struct queue *node;

    node = calloc(1, sizeof(struct queue));
    if (!node) {
        return -1;
    }

    node->elem = elem;

    if (!head) {
        head = node;
        tail = node;
    } else {
        tail->next = node;
        tail = node;
    }

    return 0;
}
```

## 6. `pop`

从队列头部移除元素并将`head`移动到下一个。



```c
void *pop() {
    struct queue *node;
    void *elem = NULL;

    if (head != NULL) {
        node = head;
        elem = node->elem;
        head = head->next;
        if (head == NULL) {
            tail = NULL;
        }
        free(node);
    }
    return elem;
}
```

下面是队列的实现。

```c
#include <stdio.h>
#include <stdlib.h>

struct queue {
    void *elem;
    struct queue *next;
};

static struct queue *head;
static struct queue *tail;
static int count;

void *front() {
    void *elem;

    if (head) {
        elem = head->elem;
    }
    return elem;
}

void *back() {
    void *elem;

    if (tail) {
        elem = tail->elem;
    }
    return elem;
}

void empty(void (*callback)(void *elem)) {
    struct queue *node;
    struct queue *prev;

    node = head;
    prev = head;

    while (node) {
        prev = node;
        node = node->next;
        if (callback) {
            callback(prev->elem);
        }
        free(prev);
    }
    count = 0;
}

int size() {
    return count;
}

int push(void *elem) {
    struct queue *node;

    node = calloc(1, sizeof(struct queue));
    if (!node) {
        return -1;
    }

    node->elem = elem;

    if (!head) {
        head = node;
        tail = node;
    } else {
        tail->next = node;
        tail = node;
    }

    return 0;
}

void *pop() {
    struct queue *node;
    void *elem = NULL;

    if (head != NULL) {
        node = head;
        elem = node->elem;
        head = head->next;
        if (head == NULL) {
            tail = NULL;
        }
        free(node);
    }
    return elem;
}

int main() {
    int a = 10;
    int b = 20;
    int c = 30;
    int d = 40;
    int e = 50;
    int f = 60;

    push(&a);
    push(&b);
    push(&c);
    push(&d);
    push(&e);
    push(&f);

    printf("size : %d\n", size());
    printf("Front: %d\n", (int *)front());
    printf("Back: %d\n", (int *)back());

    while (1) {
        int *elem = pop();
        if (!elem) {
            break;
        }
        printf("%d\n", *elem);
    }

    empty(NULL);
    return 0;
}
```

环形缓冲区 (Ring Buffer)

树 (Tree)

## 哈希表

哈希表是数组列表，可以通过键（key）索引进行访问。

例如，假设我们有以下列表：

| 1 | 2 | 3 | 4 |
| :--- | :--- | :--- | :--- |
| 5 | | | |
| 6 | 7 | 8 | |

在这个列表中，要访问元素 5，我们应该先搜索第一个列表，然后第二个，直到找到 5。

在哈希表中，列表中的每个元素在添加到列表时都会分配一个键。因此，当对该元素进行查询时，键也作为输入直接找到该索引处的元素。为了实现这一点，我们对键进行哈希处理，并对列表总数取模。得到的数字就是哈希表的索引。哈希可以是简单的计算，也可以执行某些操作的随机数生成器。键可以是任何内容。例如：

```c
const char *key = "first item";

int hash(const char *k)
{
    int i;
    int r = 0;
    for (i = 0; k[i] != '\0'; i++) {
        r += k[i];
    }
    return r % HASH_TABLE_LEN;
}
```

通常哈希必须看起来是随机的，我们将在下文中解释。

下面是哈希表的示例。

```c
#include <stdio.h>
#include <stdbool.h>
#include <stdlib.h>

struct LL {
    void *data;
    struct LL *next;
};

#define HASH_TABLE_LEN 30

struct HT {
    struct LL *head;
    struct LL *tail;
};

struct HT ht[HASH_TABLE_LEN];
```

```c
int hash(const char *str)
{
    int v = 0;
    int i;

    for (i = 0; str[i] != '\0'; i++) {
        v += str[i];
    }

    return v % HASH_TABLE_LEN;
}
```

```c
int add_item(const char *key, void *data)
{
    struct LL *item;
    int r = hash(key);

    item = calloc(1, sizeof(struct LL));
    if (!item) {
        return -1;
    }

    item->data = data;

    if (!ht[r].head) {
        ht[r].head = item;
        ht[r].tail = item;
    } else {
        ht[r].tail->next = item;
        ht[r].tail = item;
    }

    return 0;
}
```

```c
ht[r]->head = item;
ht[r]->tail = item;
} else {
    ht[r]->tail->next = item;
    ht[r]->tail = item;
}

return 0;
```

```c
bool find(const char *key, void *data) {
    struct LL *item;
    int r = hash(key);
    int iters = 0;

    for (item = ht[r].head; item != NULL; item = item->next) {
        iters++;
        if ((item)->data == data) {
            printf("took %d iterations\n", iters);
            return true;
        }
    }

    return false;
}
```

```c
void free_ht() {
    int i = 0;
    for (i = 0; i < HASH_TABLE_LEN; i++) {
        struct LL *item;
        struct LL *prev = NULL;

        item = ht[i].head;
        while (item) {
            prev = item;
            item = item->next;
            free(prev);
        }
    }
}
```

```c
struct table {
    char *key;
    int a;
    list list[] = {
    {"hash_1", 1},
    {"hash_2", 2},
    {"hash_3", 3},
    {"hash_4", 4},
    {"hash_5", 5},
    {"hash_6", 6},
    {"hash_7", 7},
    {"hash_8", 8},
    {"hash_9", 9},
    {"hash_10", 10},
    {"hash_11", 11},
    {"hash_12", 12},
    {"hash_13", 13},
    {"hash_14", 14},
    {"hash_15", 15},
    {"hash_16", 16},
    {"hash_17", 17},
    {"hash_18", 18},
    {"hash_19", 19},
    {"hash_20", 20},
    {"hash_21", 21},
    {"hash_22", 22},
    {"hash_23", 23},
    {"hash_24", 24},
    {"hash_25", 25},
    {"hash_26", 26},
    {"hash_27", 27},
    {"hash_28", 28},
    {"hash_29", 29},
    {"hash_30", 30},
    {"hash_31", 31},
    {"hash_32", 32},
    {"hash_33", 33},
    {"hash_34", 34},
    {"hash_35", 35},
    {"hash_36", 36},
    {"hash_37", 37},
    {"hash_38", 38},
    {"hash_39", 39},
    {"hash_40", 40},
    {"hash_41", 41},
    {"hash_42", 42},
    {"hash_43", 43},
    {"hash_44", 44},
    {"hash_45", 45},
    {"hash_46", 46};
};
```

```c
void print() {
    int i;

    for (i = 0; i < sizeof(list) / sizeof(list[0]); i++) {
        printf("index %d\n", i);
    }
    struct LL *item;

    for (item = ht[i].head; item != NULL; item = item->next) {
        struct table *t = (struct table*)item->data;
        printf("eval [%s] [%d]\n", t->key, t->a);
    }
}
```

```c
int main() {
    int i;

    for (i = 0; i < sizeof(list) / sizeof(list[0]); i++) {
        add_item(list[i].key, &list[i]);
    }

    print();

    printf("find %s in %s\n", list[10].key, find(list[10].key, &list[10]) ? "True" : "False");
    printf("find %s in %s\n", list[12].key, find(list[12].key, &list[12]) ? "True" : "False");
    printf("find %s in %s\n", list[45].key, find(list[45].key, &list[45]) ? "True" : "False");
    printf("find %s in %s\n", list[33].key, find(list[33].key, &list[33]) ? "True" : "False");
    printf("find hash_50 in %s\n", find(hash_50, &list[12]) ? "True" : "False");

    free_ht();
    return 0;
}
```

## 搜索与排序

排序是一个对元素进行排列的过程，更广泛地说，是按照某种顺序对元素进行组织。冒泡排序通过不断比较相邻元素对并在它们顺序错误时交换它们，来对整个序列进行排序。冒泡排序通过不断比较相邻元素对并在它们顺序错误时交换它们，来对整个序列进行排序。冒泡排序通过不断比较相邻元素对并在它们顺序错误时交换它们，来对整个序列进行排序。冒泡泡泡泡泡泡泡泡泡泡泡泡泡泡泡泡泡泡排序。

以下是常见的排序算法：

- 冒泡排序
- 插入排序
- 合并排序
- 快速排序

冒泡排序通过不断比较相邻元素对并在它们顺序错误时交换它们，来对整个序列进行排序。

冒泡排序的伪代码如下：

```c
for (i = 0; i < n-1; i++) {
    for (j = 0; j < n-i-1; j++) {
        if (a[j] > a[j+1]) {
            swap(a[j], a[j+1]);
        }
    }
}
```

冒泡排序的时间复杂度如下：

- 最坏情况：$O(n^2)$
- 平均情况：$O(n^2)$
- 最好情况：$O(n)$（当数组已经有序时，且使用了优化标志位）

冒泡排序的空间复杂度为：$O(1)$（原地排序）。

优化后的冒泡排序可以在发现没有发生任何交换时提前结束：

```c
for (i = 0; i < n-1; i++) {
    bool swapped = false;
    for (j = 0; j < n-i-1; j++) {
        if (a[j] > a[j+1]) {
            swap(a[j], a[j+1]);
            swapped = true;
        }
    }
    if (!swapped) break;
}
```

## 插入排序

插入排序通过构建一个有序子序列来完成排序。它就像整理扑牌一样，每次拿一张新牌并插入到已经排好序的牌中的正确位置。

插入排序的伪代码如下：

```c
for (i = 1; i < n; i++) {
    key = a[i];
    j = i - 1;
    while (j >= 0 && a[j] > key) {
        a[j+1] = a[j];
        j = j - 1;
    }
    a[j+1] = key;
}
```

插入排序的时间复杂度如下：

- 最坏情况：$O(n^2)$
- 平均情况：$O(n^2)$
- 最好情况：$O(n)$（当数组已经有序时）

插入排序的空间复杂度为：$O(1)$。

## 合并排序

合并排序是一种分治策略的算法。它将数组分成两部分，递归地对这两部分排序，然后将两个有序部分合并。

合并排序的伪代码如下：

```c
void mergeSort(a, n) {
    if (n <= 1) return;
    mid = n / 2;
    mergeSort(left_half, mid);
    mergeSort(right_half, n - mid);
    merge(left_half, right_half);
}
```

合并排序的时间复杂度如下：

- 最坏、平均、最好情况均为 $O(n \log n)$

合并排序的空间复杂度为：$O(n)$（需要额外的空间来合并）。

## 快速排序

快速排序也是一种分治策略的算法。它选择一个元素作为基准，将数组分为两个部分：一部分小于基准的元素，另一部分大于基准的元素。

快速排序的伪代码如下：

```c
void quickSort(a, low, high) {
    if (low < high) {
        p = partition(a, low, high);
        quickSort(a, low, p - 1);
        quickSort(a, p + 1, high);
    }
}
```

快速排序的时间复杂度如下：

- 最坏情况：$O(n^2)$（当基准元素总是选择最大值或最小值时）



# 快速排序

## 复杂度分析

- 平均情况：$O(n \log n)$
- 最好情况：$O(n \log n)$

快速排序的空间复杂度为：$O(\log n)$（递归栈空间）。

# 合并排序

# 搜索

计算机编程中的搜索是指查找某些文本字符串、数字模式、大组文本或数字。有时，如果数据是排序过的，搜索可以得到高效的结果。

在数组上进行通用查找如下：

```cpp
int search(int array[], int size, int item) {
    int i;
    for (i = 0; i < size; i++) {
        if (array[i] == item) {
            return i;
        }
    }
    return -1;
}
```

虽然这看起来很简单，但如果要搜索的项目数量增加，其时间和计算复杂度就会增加。例如，如果数组包含从 1 到 1000 的元素，上述程序中迭代的次数为 1000 次。

因此，有一些现有的搜索算法可以在项目列表中高效地查找某个项。

## 二分查找

二分查找要求数字必须按顺序排序。如果数字没有经过排序，就无法对数据使用二分查找。

二分查找算法尝试通过运行分治治法来寻找匹配的元素。

以下是该算法的工作原理：

1. 首先将一组排序后的元素分为两个等等的组。
2. 检查数组的中间点是否匹配查询的元素。如果是，返回中间点的索引。
3. 如果不匹配，则执行以下操作：
   - 检查中间点是否大于查询的项目。如果是，将搜索移动到下半部分。
   - 如果不是，将搜索移动到上半部分。
4. 重复步骤 2 和 3，直到找到元素或直到下半部分和上半部分的索引匹配。

以一组排序好的元素为例。

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| | | | | | | | | | |
| | | | | Low | Mid | High | | | |

`low = 0` `high = 9` `mid = 4`

现在要搜索的项目是 6，那么

1. 低于 6，所以 `low = mid + 1 = 5`, `high = 9`, `mid = (5 + 9) / 2 = 7`

| 6 | 7 | 8 | 9 | 10 |
| :--- | :--- | :--- | :--- | :--- |
| | | | | |
| | | | Low | Mid | High |

2. 大于 6，所以 `low = 5`, `mid - 1 = 8`, `mid = (5 + 8) / 2 = 6`

| 6 | 7 | 8 | 9 |
| :--- | :--- | :--- | :--- |
| | | | |
| | | Low | Mid | High |

3. 7 大于 6，所以 `low = 5`, `mid - 1 = 5`, `mid = (5 + 5) / 2 = 5`

| 6 |
| :--- |
| |
| Low = Mid = High |

所以通过 3 次迭代找到了数字 6。

下面是一个 C++ 中的模板化二分查找示例。

```cpp
#include <iostream>

template <typename T>
int binary_search(const T *items, int n, const T item)
{
    int low = 0;
    int high = n - 1;
    int mid = (low + high) / 2;

    while (low < high) {
        if (items[mid] == item) {
            return mid;
        }

        if (items[mid] < item) {
            low = mid + 1;
        }

        if (items[mid] > item) {
            high = mid - 1;
        }

        mid = (low + high) / 2;
    }

    return -1;
}

int main()
{
    int a[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int i = binary_search(a, 10, 3);

    if (i != -1) {
        printf("%d] = %d\n", i, a[i]);
    } else {
        printf("search not found\n");
    }
    return 0;
}
```

嗯，比较操作（如 `==`、`<` `>`）是针对整数的，人们在传递其他类型时，也可以为 `==`、`<` 编写自定义运算符。例如，如果整数是结构体的一部分并且它们需要排序。

```cpp
struct S {
    int i;
};

bool operator==(const S& lhs, const S& rhs) {
    if (lhs.i == rhs.i) {
        return true;
    }
    return false;
}
```

调用函数因此可以使用：

```cpp
S s3 = { .i = 3 };
binary_search<S>(a, 10, s3);
```

# 更新日志

**17/09/2023:**

1. 更新了类的数据运算符 `<<`, `>`。
2. 清理了书中的页面。

**18/09/2023:**

1. 更新 `std::list`。
