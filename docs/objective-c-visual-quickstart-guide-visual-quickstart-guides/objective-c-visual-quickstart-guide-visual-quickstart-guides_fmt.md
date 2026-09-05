
# Objective-C：快速启动指南

## 献辞

## 致谢

你手中的这本书是许多人的心血。我特别感谢 Nancy Judy Ziajka，她不懈的努力让这本书变得尽可能完美；并感谢 Kalev 对整个手稿的细致审查。

vi

## 索引 223

## 引言

欢迎学习 Objective-C。本书将带你开启这门令人兴奋的语言的之旅，并为你提供立即开始使用 Objective-C 所需的内容。

通过 Objective-C，你可以编写利用许多面向对象特性的专业程序——从基础知识到高级的类继承和异常（运行时错误）处理。

Objective-C 运行在许多不同的平台上。在大多数情况下，你的代码在 Objective-C 支持的所有平台上都可以在无需更改的情况下运行，但在支持存在差异的地方，本书会为你指出。

本书从基础知识开始，一直延续到高级主题。你将首先查看如何启动 Objective-C 以及如何运行基础程序。从那里开始，你将探索数据处理，同样是从基础开始进到高级主题。

在学习了如何编写自己的函数之后，你将把函数和数据封装成对象——这是 Objective-C 编程的核心。当你开始学习面向对象编程时，一切都将打开了——我们将尽可能地挑战极限。

那么，计划就是：提供一次 Objective-C 的引导性之旅，带你从开始到最先进的主题。让我们从第 1 章开始吧。

# 第 1 章：入门：Objective-C

本书将带你开启 Objective-C 的引导之旅，从基础一直到高级内容。Objective-C 是一门跨平台语言，因此你会在许多系统中发现它：当然还有 Mac，还有 Linux、Windows 等等——而且它的核心代码在所有平台上都保持不变。

## 入门：核心 Objective-C

**3**

## 创建你的第一个程序

我们将通过创建并运行一个程序来直接进入 Objective-C 世界，我们先将其命名为 `first.m`。

我们将首先创建一个函数——也就是说一段你可以通过名称调用的代码——命名为 `main()`：

```objective-c
int main(void)
{
    .
}
```

正如你稍后看到的，函数可以传递数据，但此函数没有传递任何数据，这就是为什么我们在括号中使用了 `void` 关键字。函数还可以返回结果，`main()` 函数向 Objective-C 返回一个整数值，表示程序是否执行成功。`main()` 前面的 `int` 告诉 Objective-C 期望一个整数返回值。`main()` 函数的代码放在大括号 `{` 和 `}` 之间。

接下来，我们将使用名为 `printf()` 的内置 Objective-C 函数来显示一些文本。我们向括号内传递我们想要让 `printf()` 显示的文本：

```objective-c
int main(void)
{
    printf ("Welcome to Objective-C!");
}
```

- **tip**：Objective-C 代码文件的扩展名是 `.m`。

第 1 章

**4**

## 创建你的第一个程序

为了使用 `printf()` 函数，我们必须通过函数声明告诉 Objective-C 该函数的存在，正如我们在讨论如何创建函数时会看到的那样。`printf()` 等标准输入输出函数的包含在一个名为 `stdio.h` 的 Objective-C 文件中，其中 `.h` 代表“头文件”；我们如下所示在程序中包含 `stdio.h`，这样 Objective-C 就能识别 `printf()` 函数：

```objective-c
#include <stdio.h>

int main(void)
{
    printf ("Welcome to Objective-C!");
}
```

当程序结束时，Objective-C 将期待一个关于函数是否执行成功的指示。我们将向 Objective-C 返回一个值 `0`，这意味着没有错误。代码列表 1.1 显示了整个程序，你将在接下来的任务中逐步创建它。

- **tip**：注意，对于我们的目的来说，`#import` 和 `#include` 是相同的。你可以交替使用它们，并采用任何顺序。

```objective-c
#include <stdio.h>

int main(void)
{
    printf ("Welcome to Objective-C!");
    return 0;
}
```

**列表 1.1** 你的第一个 Objective-C 程序。

入门：核心 Objective-C

**5**

## 创建你的第一个程序

**在 Mac 上创建你的第一个 Objective-C 程序：**

1. 从 http://developer.apple.com/iphone 下载并安装 Xcode 集成开发环境。
2. 运行 Xcode。
3. 选择 File（文件） > New Project（新建项目）。
4. 在 New Project 窗口中，选择 Application（应用程序）。
5. 点击 Command-Line Tool（命令行工具）图标以选中它。
6. 从 Type（类型）下拉菜单中选择 Foundation。
7. 点击 Choose（选择）按钮。
8. 输入 `First` 作为你的应用程序名称。
9. 选择一个保存位置并点击 Save（保存）按钮。
10. 在文本编辑器窗口中输入列表 1.1 中的代码。
11. 选择 File（文件） > Save（保存）。

**在 Linux、UNIX 或 Windows 上创建你的第一个 Objective-C 程序：**

1. 打开文本编辑器。
2. 输入列表 1.1 中的代码。
3. 将文件保存为 `first.m` 到你选择的目录中。

第 1 章

**6**

## 编译并运行你的第一个程序

要运行 Objective-C 程序，你首先必须对其进行编译，这会让 Objective-C 将你的代码转换为计算机可以理解的机器语言。

当你运行第一个程序时，你应该看到以下结果：

`Welcome to Objective-C!`

Objective-C 语言内置于 Mac OS 10.6 中，但 Linux、UNIX 或 Windows 没有，因此你必须下载它。如果你使用 Linux 或 UNIX，请访问 http://www.GNUstep.org/resources/sources.html 下载并安装 GNUstep，它将提供 Objective-C 编译器。

如果你使用 Windows，请访问 http://www.GNUstep.org/experience/Windows.html 下载 GNUstep 安装程序并运行它。

**在 Mac 上编译并运行你的第一个 Objective-C 程序：**

1. 在 Xcode 的 Project 工具栏上点击 Build and Run（构建并运行）按钮。

你应该看到这条消息：

`Welcome to Objective-C!`

恭喜你，运行了第一个 Objective-C 程序！

入门：核心 Objective-C

**7**

## 编译并运行你的第一个程序

**在 Linux 或 UNIX 上编译并运行第一个 Objective-C 程序：**

1. 打开命令行提示符窗口。
2. 进入包含 `first.m` 的目录。
3. 如果你的电脑找不到编译器，请在 `gcc` 前加上 GNUstep 的路径：

   `gcc -o first.m`

4. 如下运行程序：

   `./first`

你应该看到这条消息：

`Welcome to Objective-C!`

恭喜你，运行了第一个 Objective-C 程序！

- **tip**：本书使用 `$` 作为通用命令提示符。

**在 Windows 上编译并运行第一个 Objective-C 程序：**

1. 选择 Start > Programs > GNUstep。
2. 在 shell 中进入包含 `first.m` 的目录。例如，如果 `first.m` 在 C:\，输入以下内容（`$` 是提示符）：

   `cd C:\`

3. 在 shell 中输入以下命令将 `first.m` 编译为 `first.exe`：

   `gcc -o first.m`

4. 如下执行 `first.exe`：

   `first`

你应该看到这个：

`Welcome to Objective-C!`

第 1 章

**8**

## 使用变量

在 Objective-C 中，你可以将数据存储在变量中，变量是数据的占位符。例如，假设你有 1 百万并想跟踪它；你可以如下将其存储在名为 `amount` 的变量中：

```objective-c
int amount = 1000000;
```

这段代码创建了一个存储整数（int 部分）的变量并将 `amount` 的初始化为 1000000。要显示 `amount` 的值，可以使用 `printf()`：

```objective-c
printf("The amount in your account is %i\n", amount);
```

`%i` 是占位符，会被后面的整数变量替换。`\n` 将文本移动到新行。当此程序运行时，你会看到 `amount` 的值：

`The amount in your account is 1000000`

**使用变量：**

1. 在新程序 `account.m` 中输入列表 2 中的代码。
2. 创建变量 `amount` 并将其初始化为 1000000（列表 3）。
3. 显示 `amount` 的值（列表 4）。
4. 构建并运行程序。

```objective-c
#include <stdio.h>

int main(void)
{
    int amount = 1000000;
    printf("The amount in your account is %i\n", amount);
}
```

**列表 2** `account.m`。

```objective-c
#include <stdio.h>

int main(void)
{
    int amount = 1000000;
}
```

**列表 3** `account.m`。

```objective-c
#include <stdio.h>

int main(void)
{
    printf("The amount in your account is %i\n", amount);
}
```

**列表 4** `account.m`。

入门：核心 Objective-C

**9**

## 显示数值

使用 `printf()` 函数显示存储在变量中的值是非常用的。在上一个任务中，你看到代码 `%i` 是整数变量的占位符。

| 代码 | 说明 |
| :--- | :--- |
| `%i` | 整数 |
| `%c` | 字符 |
| `%d` 或 `%i` | 有符号十进制 |
| `%e` | 使用 e 字符的科学计数法（系数/指数） |
| `%E` | 使用 E 字符的科学计数法（系数/指数） |
| `%f` | 浮点小数 |
| `%g` | %e 或 %f 中较短的 |
| `%G` | %E 或 %f 中较短的 |
| `%s` | 字符字符串 |
| `%u` | 无符号十进制 |

例如，如果你将上一个任务中的 `amount` 变量从 (int) 类型更改为浮点值 (float)，你可以使用 `printf()` 和 `%f`（用于 float）显示其值：

```objective-c
#include <stdio.h>

int main(void)
{
    float amount = 1000000.0;
    printf("The amount in your account is %f\n", amount);
}
```

在这个任务中，你将创建一个名为 `temperature.m` 的程序，它将显示时间（整数）和温度（浮点数）。为了做到，你将在 `printf()` 中使用逗号分隔你想要显示的变量值：

```objective-c
#include <stdio.h>

int main(void)
{
    int time = 4;
    float temperature = 73.6;
    printf("At %i o'clock, the temperature is %f degrees.\n", time, temperature);
    return 0;
}
```

# 第一章

## 在变量中显示值

然而，由于计算机精度的有限，你实际上看到的将不是 73.6 度，而是如下内容：

在下午 4 点，温度为 73.599998 度。

你需要对浮点值进行向上舍入，这可以通过使用代码 `%4.1f` 而不是简单的 `%f` 来实现。代码 `%4.1f` 告诉程序，你希望数字总长度为四位，其中小数点后保留一位。这让你得到“下午 4 点，温度为 73.6 度”，这正是你想要的结果。

**显示值：**

1. 创建一个名为 `temperature.m` 的新程序。
2. 在 `temperature.m` 中，输入列表 1.5 所示的代码。
3. 保存 `temperature.m`。
4. 运行 `temperature.m` 程序。你应该看到：在下午 4 点，温度为 73.6 度。

```c
#include <stdio.h>
int main(void)
{
    int time = 4;
    float temperature = 73.6;
    printf("At %i o’clock, the temperature is %4.1f degrees.\n", time, temperature);
    return 0;
}
```

列表 1.5 显示一个 int 和一个 float

## 使用数据类型

Objective-C 带有一些内置数据类型，你可以用它们来创建变量。例如，你已经见过了 `int` 类型，它可以用于创建整数变量。`int` 类型被称为原始类型（primitive），因为它是语言内置的，并且是一种简单类型。表 1.2 显示了 Objective-C 中的原始类型。在本次任务中，我们将创建一个名为 `datatype.m` 的程序，其中包含四个变量：一个字符、一个整数、一个长整型和一个浮点型。

```c
char c = 'a';
int i = 4;
long l = 12345321;
float f = 3.141526;
```

代码将显示它们的内容：字符是 'a'。整数是 4。长整型是 12345321。浮点型是 3.141526。

| 类型 | 大小 |
| :--- | :--- |
| `char` | 1 byte (8 bits) |
| `double` | 8 bytes |
| `float` | 4 bytes (浮点数，例如 3.141526) |
| `int` | 4 bytes (整数；例如，-1, 34) |
| `long` | 4 bytes |
| `long long` | 8 bytes |
| `short` | 2 bytes |

表 1.2 Objective-C 原始类型

**显示值：**

1. 创建一个名为 `datatype.m` 的新程序。
2. 在 `datatype.m` 中，输入列表 1.6 所示的代码。
3. 保存 `datatype.m`。
4. 运行 `datatype.m` 程序。你应该看到：字符是 'a'。整数是 4。长整型是 12345321。浮点型是 3.141526。

```c
#include <stdio.h>
int main(void)
{
    char c = 'a';
    int i = 4;
    long l = 12345321;
    float f = 3.141526;
    printf("The character is '%c'.\n", c);
    printf("The integer is %i.\n", i);
    printf("The long is %i.\n", l);
    printf("The float is %10.6f.\n", f);
    return 0;
}
```

列表 1.6 `datatype.m` 程序

## 添加注释

Objective-C 允许你在程序中包含英文注释，留给自己或他人。此类注释对于提供文档或指示如何修改代码非常有用。Objective-C 会忽略标记 `/*` 和 `*/` 之间的任何文本，因此你可以在代码中插入如下注释：

```c
/* Here is a comment. */
```

你还可以将此类注释改为多行注释，如下所示：

```c
/* Here
 * is
 * a
 * comment. */
```

Objective-C 还识别 C++ 语言中常用的另一种注释类型：以 `//` 开头的单行注释。Objective-C 会忽略行中 `//` 之后的所有内容，因此这些注释通常用于解释单行代码：`int i = 4; // Here is a comment.`。

在本次任务中，我们将为上一个任务的 `datatype.m` 程序添加注释。

**添加注释：**

1. 打开 `datatype.m` 进行编辑。
2. 在 `datatype.m` 中，输入列表 1.7 所示的注释。



```c
#include <stdio.h>
int main(void)
{
    /* Declare the variables. */
    char c = 'a';
    int i = 4;
    long l = 12345321;
    float f = 3.141526;
    /* Display the results. */
    printf("The character is '%c'.\n", c);
    printf("The integer is %i.\n", i);
    printf("The long is %i.\n", l);
    printf("The float is %10.6f.\n", f);
    return 0;
}
```

列表 1.7 带有注释的`datatype.m`程序。

3. 在`datatype.m`中，输入列表 1.8 所示的单行注释。

4. 保存`datatype.m`。

5. 运行`datatype.m`程序以确认 Objective-C 忽略了这些注释。

```c
#include <stdio.h>
int main(void)
{
    /* Declare the variables. */
    char c = 'a';
    int i = 4;
    long l = 12345321;
    float f = 3.141526;
    /* Display the results. */
    printf("The character is '%c'.\n", c);
    printf("The integer is %i.\n", i);
    printf("The long is %i.\n", l);
    printf("The float is %10.6f.\n", f);
    return 0;
}
```

列表 1.8`datatype.m`程序（带单行注释）

（注：此处根据原文逻辑，1.8 应包含单行注释，但示例中代码块与 1.7 重复，此处遵循原文结构）

（修正：根据原文提供的文本，列表 1.8 应该是包含单行注释的代码，此处翻译如下：）

```c
#include <stdio.h>
int main(void)
{
    /* Declare the variables. */
    char c = 'a';
    int i = 4; // Here is a comment.
    long l = 12345321;
    float f = 3.141526;
    /* Display the results. */
    printf("The character is '%c'.\n", c);
    printf("The integer is %i.\n", i);
    printf("The long is %i.\n", l);
    printf("The float is %10.6f.\n", f);
    return 0;
}
```

## 使用运算符

与大多数编程语言一样，Objective-C 提供了算术运算符执行数学运算。这些运算符可以让你对变量进行加、减、乘、除和模（见表 1.3）。例如，`10 + 2`得到 12，`10 - 2`得到 8，`10 * 2`得到 20，`10 / 2`得到 5，而`10 % 3`返回余数 1。

| 运算符 | 功能 |
| :--- | :--- |
| `+` | 加法 |
| `-` | 减法 |
| `/` | 除法 |
| `*` | 乘法 |
| `%` | 模 |

表 1.3 Objective-C 算术运算符

**使用 Objective-C 算术运算符：**

1. 创建一个名为`operators.m`的程序。
2. 在`operators.m`中，输入列表 1.9 所示的代码。这声明了操作数：`x`和`y`。
3. 使用这些运算符测试（见列表 1.10）。
4. 保存`operators.m`。
5. 运行`operators.m`程序。你应该看到：`5 + 2 = 7`、`5 - 2 = 3`、`5 * 2 = 10`、`5 / 2 = 2`。

```c
#include <stdio.h>
int main(void)
{
    float x = 5;
    float y = 2;
    return 0;
}
```

列表 1.9 Starting`operators.m`。

```c
#include <stdio.h>
int main(void)
{
    float x = 5;
    float y = 2;
    printf("%.0f + %.0f = %.0f\n", x, y, x + y);
    printf("%.0f - %.0f = %.0f\n", x, y, x - y);
    printf("%.0f * %.0f = %.0f\n", x, y, x * y);
    printf("%.0f / %.0f = %.1f\n", x, y, x / y);
    return 0;
}
```

列表 1.10 使用算术运算符的`operators.m`程序

### 使用赋值运算符

你已经看到可以使用赋值运算符`=`为变量赋值，如下所示：`x = 5`。你还可以将运算符与赋值运算符结合作为快捷方式。例如，你可以使用快捷赋值运算符`+= 5`来编写`x = x + 5`。表 1.4 列出了赋值运算符。

**使用 Objective-C 赋值运算符：**

1. 创建一个名为`assignment.m`的新程序。
2. 在`assignment.m`中，输入列表 1.11 所示的代码。

| 运算符 | 功能 |
| :--- | :--- |
| `=` | 赋值 |
| `+=` | 加赋值 |
| `-=` | 减法赋值 |
| `/=` | 除法赋值 |
| `*=` | 乘法赋值 |
| `%=` | 模赋值 |

```c
#include <stdio.h>
int main(void)
{
    float x = 0;
    float y = 5;
    return 0;
}
```

列表 1.11 Starting`assignment.m`。

### 使用赋值运算符

3. 添加代码来使用赋值运算符（Listing 1.12）。
4. 保存`assignment.m`。
5. 运行赋值程序。

你应该能看到以下内容：

`x = 0.`

`x = 5 -> x: 5.`

`x + = 5 -> x: 10.`

`x -= 5 -> x: 5.`

`x *= 5 -> x: 25.`

`x /= 5 -> x: 5.`

```c
#include <stdio.h>
int main(void)
{
    float x = 0;
    float y = 5;
    printf ("x = %2.0f.\n", x);
    x = y;
    printf ("x = %2.0f --> x: %2.0f.\n", y, x);
    x += y;
    printf ("x + = %2.0f --> x: %2.0f.\n", y, x);
    x -= y;
    printf ("x -= %2.0f --> x: %2.0f.\n", y, x);
    x *= y;
    printf ("x *= %2.0f --> x: %2.0f.\n", y, x);
    x /= y;
    printf ("x /= %2.0f --> x: %2.0f.\n", y, x);
    return 0;
}
```

**Listing 1.12** 使用赋值运算符的`assignment.m`程序。

### 入门：核心 Objective-C

### 使用自增和自减运算符

Objective-C 还支持另外两个运算符：`++`自增运算符和`--`自减运算符。例如，要增加名为`temperature`的变量的值，你编写`temperature++`，这会将该值加 1。要减少值，你输入`temperature--`，这会将该值减 1。

你可以在变量之前或之后使用`++`和`--`，位置会有区别。`++`表达式会先增加`x`的值，然后执行该行代码；而`x++`表达式则在执行当前行代码后，再增加`x`的值。

例如，假设你有以下代码：

```c
float x = 0;
float y = 5;
x = y++;
printf ("After x = y++ x: %2.0f.\n", x, y);
```

这段代码会打印`x: 5`并是`y: 6`，因为自增操作是在赋值后进行的。另一方面，假设你执行：

```c
x = ++y;
printf ("After x = ++y x: %2.0f.\n", x, y);
```

这段代码会打印`x: 7`，因为自增操作先完成了。

让我们测试自增运算符。

### 使用自增和自减运算符

要使用 Objective-C 自增运算符：

1. 创建名为`increment.m`的新程序。
2. 在`increment.m`中输入 Listing 1.13 所示的代码。该代码声明了两个变量`x`和`y`。
3. 添加代码使用自增运算符（Listing 1.14）。
4. 保存`increment.m`。
5. 运行`increment.m`程序。

你应该看到以下内容：

`x: 0 y: 5.`

`After x = y++ x: 5 y: 6.`

`After x = ++y x: 7 y: 7.`

```c
#include <stdio.h>
int main(void)
{
    float x = 0;
    float y = 5;
    
    return 0;
}
```

**Listing 1.13**`increment.m`程序。

```c
#include <stdio.h>
int main(void)
{
    float x = 0;
    float y = 5;
    printf ("x: %2.0f y: %2.0f.\n", x, y);
    x = y++;
    printf ("After x = y++ x: %2.0f.\n", x, y);
    x = ++y;
    printf ("
 x =yAfter x = ++y: %2.0f.\n", x, y);
    return 0;
}
```

**Listing 1.14** 使用自增运算符的`increment.m`程序。

### 入门：核心 Objective-C

### 使用类型转换运算符

假设你想在一个名为`cast.m`的程序中求两个浮点数的模。你可能会输入：

```c
float x = 5;
float y = 3;
int result = 0;
result = x % y;
```

然而，当你运行这段代码时，Objective-C 编译器会报错：`cast.m:12: error: invalid operands to %`。问题是该运算符需要整数操作数。为了解决这个问题，你可以使用`(int)`转换将浮点变量临时整数变量：

```c
float x = 5;
float y = 3;
int result = 0;
result = (int) x % (int) y;
```

现在一切正常了。你可以使用`cast`在类型之间转换：`(int)`、`(float)`等。

### 使用类型转换运算符

要使用转换运算符：

1. 创建名为`cast.m`的新程序。
2. 在`cast.m`中输入 Listing 1.15 所示的代码。该代码声明了三个变量：`x`、`y`和`result`。
3. 添加代码使用模运算符（Listing 1.16）。
4. 保存`cast.m`。
5. 运行`cast.m`程序。

你应该看到以下内容：`x: 5 y; 3`。`x mod y`的结果为 2。

```c
#include <stdio.h>
int main(void)
{
    float x = 5;
    float y = 3;
    int result = 0;
    
    return 0;
}
```

**Listing 1.15**`cast.m`程序。

```c
#include <stdio.h>
int main(void)
{
    float x = 5;
    float y = 3;
    int result = 0;
    printf ("x: %2.0f y; %2.0f.\n", x, y);
    result = (int) x % (int) y;
    printf ("The result of x mod y is %d.\n", result);
    return 0;
}
```

**Listing 1.16** 使用类型转换运算符的`cast.m`程序。

### 入门：核心 Objective-C

### 控制程序流程

本章完全关于通过按你想要的方式来控制代码。你将学习如何使用`if`语句进行选择、使用循环进行遍历。允许进行选择的主要语句是`if`语句。例如，假设你有一个名为`temperature`的变量，其设置为 72：

```c
#include <stdio.h>
int main(void)
{
    int temperature = 72;
    ...
```

### 控制程序流程

你可以使用`==`等于运算符测试`temperature`的值是否等于 72，如果是，则执行特定代码：

```c
#include <stdio.h>
int main(void)
{
    int temperature = 72;
    if (temperature == 72)
    {
        printf("Perfect weather.\n");
    }
    return 0;
}
```

你还可以添加`else`语句，如果`if`语句中的条件为假，则执行代码：

```c
#include <stdio.h>
int main(void)
{
    int temperature = 78;
    if (temperature == 72)
    {
        printf("Perfect weather.\n");
    }
    else
    {
        printf("Weather could be better.\n");
    }
    return 0;
}
```

### 控制程序流程

循环提供了控制程序流程的另一种工具。循环让你重复执行特定操作，例如对一组数字求和或绘制线条。例如，在`for`循环（最常见的循环类型）中，你初始化名为`loop_index`的变量（通常设置为 0），指定导致循环结束的条件以及在循环体执行后执行的操作。在示例中，循环在`loop_index`变量包含大于 5 的数字时结束；在循环体运行后，`loop_index`的值递增：

```c
#include <stdio.h>
int main(void)
{
    int loop_index;
    for (loop_index = 0; loop_index < 5; loop_index++)
    {
        printf("You’ll see this five times.\n");
    }
    return 0;
}
```

这个示例显示了文本“You’ll see this five times.”

关于`for`循环和 Objective-C 中其他循环的内容将在本章之后介绍。

# 第 2 章：使用 if 语句

`if`语句是程序流控制语句中最基础的一种。该语句允许你测试一个条件，如果条件为真，则允许你执行特定的代码。

例如，如果你设置一个名为`temperature`的变量为 72，你可以使用`if`语句来测试并确保变量确实包含 72。你将要测试的条件（在本例中为`temperature == 72`，使用`==`等于运算符）放在括号内，并将条件为真时要执行的代码放在括号后的大括号中，如下所示：

```c
#include <stdio.h>

int main(void)
{
    int temperature = 72;
    if (temperature == 72)
    {
        printf("Perfect weather.\n");
    }
    return 0;
}
```

在这种情况下，`temperature`确实等于 72，因此大括号中的代码将被执行。在这里，该代码会打印消息“Perfect weather.”

**使用 Objective-C if 语句：**

1. 创建名为`if.m`的新程序。
2. 在`if.m`中，输入 Listing 2.1 所示的代码。这段代码创建了`temperature`变量并检查它是否等于 72。
3. 添加代码以在`temperature`等于 72 时显示“perfect weather”消息（Listing 2.2）。
4. 保存`if.m`。
5. 运行`if.m`程序。

你应该看到：

`Perfect weather.`

```c
#include <stdio.h>

int main(void)
{
    int temperature = 72;
    if (temperature == 72)
    {
    }
    return 0;
}
```

Listing 2.1 启动`if.m`。



```c
#include <stdio.h>

int main(void)
{
    int temperature = 72;
    if (temperature == 72)
    {
        printf("Perfect weather.\n");
    }
    return 0;
}
```

Listing 2.2 The`if.m`程序。

## 使用`else`语句

`if`语句允许你指定当某个指定的条件（如`temperature == 72`）为真时运行的代码。`else`语句允许你指定当`if`语句结果为假时运行的备用代码。例如，你可以修改之前的任务，在温度不等于 72 时显示消息“Weather could be better.”。

```c
#include <stdio.h>

int main(void)
{
    int temperature = 78;
    if (temperature == 72)
    {
        printf("Perfect weather.\n");
    }
    else
    {
        printf("Weather could be better.\n");
    }
    return 0;
}
```

**提示：** 如果你使用`else`语句，它必须紧跟在`if`语句之后。

**使用 Objective-C`else`语句：**

1. 创建名为`else.m`的新程序。
2. 在`else.m`中，输入**Listing 2.3**所示的代码。这段代码创建了温度变量并检查它是否等于 72。
3. 添加`else`语句，在温度不等于 72 时显示备用文本（**Listing 2.4**）。
4. 保存`else.m`。
5. 运行`else.m`程序。

你应该看到：

Weather could be better.

```c
#include <stdio.h>

int main(void)
{
    int temperature = 78;
    if (temperature == 72)
    {
        printf("Perfect weather.\n");
    }
    return 0;
}
```

Listing 2.3 启动`else.m`。

```c
#include <stdio.h>

int main(void)
{
    int temperature = 78;
    if (temperature == 72)
    {
        printf("Perfect weather.\n");
    }
    else
    {
        printf("Weather could be better.\n");
    }
    return 0;
}
```

Listing 2.4 The`else.m`程序。

## 使用`switch`语句

如果你有很多条件需要测试，你可能想使用`switch`语句代替多个`if-else`语句。你可以使用`switch`语句测试字符串（将在后续章节出现）或整数。当`switch`语句中找到了你正在测试变量的值，就会执行相应的代码。

以下示例测试了各种温度，并为每个温度执行代码：

```c
#include <stdio.h>

int main(void)
{
    int temperature = 73;
    switch(temperature)
    {
        case 71:
            printf("Could a little warmer.\n");
            break;
        case 72:
            printf("Perfect weather.\n");
            break;
        case 73:
            printf("It’s little warm.\n");
            break;
        default:
            printf("Unknown temperature.\n");
    }
    return 0;
}
```

**使用 Objective-C`switch`语句：**

1. 创建名为`switch.m`的新程序。
2. 在`switch.m`中，输入**Listing 2.5**所示的代码。这段代码创建了温度变量和`switch`语句。
3. 添加`case`语句显示对应温度的消息（**Listing 2.6**）。
4. 保存`switch.m`。
5. 运行`switch.m`程序。

你应该看到：

It’s little warm.

**提示：** 如果没有`case`匹配你正在测试的变量，则执行`default case`。

```c
#include <stdio.h>

int main(void)
{
    int temperature = 73;
    switch(temperature)
    {
    }
    return 0;
}
```

Listing 2.5 启动`switch.m`。

```c
#include <stdio.h>

int main(void)
{
    int temperature = 73;
    switch(temperature)
    {
        case 71:
            printf("Could a little warmer.\n");
            break;
        case 72:
            printf("Perfect weather.\n");
            break;
        case 73:
            printf("It’s little warm.\n");
            break;
        default:
            printf("Unknown temperature.\n");
    }
    return 0;
}
```

Listing 2.6 The`switch.m`程序。

## 使用比较运算符

到目前为止，我们使用`==`等于运算符来比较值：

```c
#include <stdio.h>

int main(void)
{
    int temperature = 72;
    if (temperature == 72)
    {
        printf("Perfect weather.\n");
    }
    return 0;
}
```

等于运算符只是 Objective-C 比较运算符之一，列在表 2.1 中。

| 运算符 | 描述 |
| :--- | :--- |
| `==` | 等于 |
| `!=` | 不等于 |
| `>` | 大于 |
| `<` | 小于 |
| `>=` | 大于等于 |
| `<=` | 小于等于 |

**使用比较运算符：**

1. 创建名为`compare.m`的新程序。
2. 在`compare.m`中，输入**Listing 2.7**所示的代码。该程序将温度与 72 进行比较，如果温度小于 72，则执行代码。
3. 添加语句以在温度低于 72 时显示消息（**Listing 2.8**）。
4. 保存`compare.m`。
5. 运行`compare.m`程序。

你应该看到：

Could be a little warmer.

```c
#include <stdio.h>

int main(void)
{
    int temperature = 71;
    if (temperature < 72)
    {
    }
    return 0;
}
```

Listing 2.7 启动`compare.m`。

```c
#include <stdio.h>

int main(void)
{
    int temperature = 71;
    if (temperature < 72)
    {
        printf("Could be a little warmer.\n");
    }
    return 0;
}
```

Listing 2.8 The`compare.m`程序。

## 使用逻辑运算符

在上一个任务中，我们检查了温度是否小于 72：

```c
#include <stdio.h>

int main(void)
{
    int temperature = 71;
    if (temperature < 72)
    {
        printf("Could be a little warmer.\n");
    }
    return 0;
}
```

如果你想检查温度是否在 70 到 74 度之间该呢？对于这一点，你可以使用逻辑运算符。逻辑运算符允许你连接多个语句。表 2.2 列出了逻辑运算符。

| 运算符 | 描述 |
| :--- | :--- |
| `!` | 反转条件的真/假值 |
| `&&` | 结果表达式的两个语句都为真 |
| `\|` | 结果表达式任一语句为真即可 |

**使用逻辑运算符：**

1. 创建名为`logical.m`的新程序。
2. 在`logical.m`中，输入**Listing 2.9**所示的代码。这段代码设置了`if`语句来检查温度是否小于 74 且大于 70。
3. 如果温度在范围内，显示一条消息（**Listing 2.10**）。
4. 保存`logical.m`。
5. 运行`logical.m`程序。

你应该看到：

Nice weather.

```c
#include <stdio.h>

int main(void)
{
    int temperature = 71;
    if (temperature < 74 && temperature > 70)
    {
    }
    return 0;
}
```

Listing 2.9 启动`logical.m`。

```c
#include <stdio.h>

int main(void)
{
    int temperature = 71;
    if (temperature < 74 && temperature > 70)
    {
        printf("Nice weather.\n");
    }
    return 0;
}
```

Listing 2.10 The`logical.m`程序。

## 控制程序流

### 使用条件运算符

我们已经见过如何使用`if`语句在代码中做出决策，并执行与这些决策结果相匹配的代码。你也可以使用条件运算符来做出决策。该运算符允许你评估一个表达式并根据结果执行代码。条件运算符的格式如下：

```c
conditional ? expression1 : expression2;
```

Objective-C 评估`conditional`（条件），如果它为真，则执行`expression1`；如果为假，则执行`expression2`。该运算符返回的值是被执行的表达式的值。例如，你可能想将温度限制在 72 度，如果大于 72 度，则将其设置为 72 度。以下是条件运算符实现的方法：

```c
#include <stdio.h>

int main(void)
{
   int temperature = 78;
   temperature = temperature > 72 ? 72 : temperature;
   printf("The temperature is %i.\n", temperature);
   return 0;
}
```

在这里，如果温度大于 72，条件运算符将返回第一个表达式 72。如果它小于 72，则返回温度本身。

要使用 Objective-C 的条件运算符：

1. 创建一个名为`conditional.m`的新程序。
2. 在`conditional.m`中，输入**列表 2.11**所示的代码。这段代码创建了温度变量以及使用条件运算符确保温度被限制的语句。
3. 添加显示结果的代码（**列表 2.12**）。
4. 保存`conditional.m`。
5. 运行`conditional.m`程序。你应该能看到以下内容：

The temperature is 72.

```c
// Listing 2.11 Starting conditional.m
#include <stdio.h>

int main(void)
{
   int temperature = 78;
   temperature = temperature > 72 ? 72 : temperature;
   printf("The temperature is %i.\n", temperature);
   return 0;
}
```

```c
// Listing 2.12 The conditional.m program.
#include <stdio.h>

int main(void)
{
   int temperature = 78;
   temperature = temperature > 72 ? 72 : temperature;
   printf("The temperature is %i.\n", temperature);
   return 0;
}
```

### 使用`for`循环

循环擅长它们所擅长的：执行多次操作。循环允许你重复执行一段代码，通常在每次迭代中（即每次通过循环时）处理不同的数据。`for`循环的格式如下：

```c
for (initialization; end_condition; after_loop)
{
   body
}
```

在这里，`initialization`（初始化）是在循环开始前评估的表达式；你通常在此处将`loop_index`变量（用于跟踪循环执行的次数）设置为 0。`end_condition`（结束条件）规格是一个表达式（例如`loop_index < 5`），当它不再为真时，循环结束。`after_loop`（循环后）规格在循环体（位于`for`语句后的大括号内）执行后执行；你通常在这里递增循环索引的值。

这是一个使用`for`循环显示消息“You’ll see five times.”的示例：

```c
int main(void)
{
   int loop_index;
   for (loop_index = 0; loop_index < 5; loop_index++)
   {
      printf("You’ll see this five times.\n");
   }
   return 0;
}
```

要使用 Objective-C 的`for`循环：

1. 创建一个名为`for.m`的新程序。
2. 在`for.m`中，输入**列表 2.13**所示的代码。这段代码创建了一个执行五次的`for`循环。
3. 添加在每次循环时显示消息的代码（**列表 2.14**）。
4. 保存`for.m`。
5. 运行`for.m`程序。你应该能看到以下内容：

You’ll see this five times.

You’ll see this five times.

You’ll see this five times.

You’ll see this five times.

You’ll see this five times.

```c
// Listing 2.13 Starting for.m.
int main(void)
{
   int loop_index;
   for (loop_index = 0; loop_index < 5; loop_index++)
   {
      printf("You’ll see this five times.\n");
   }
   return 0;
}
```

```c
// Listing 2.14 The for.m program.
int main(void)
{
   int loop_index;
   for (loop_index = 0; loop_index < 5; loop_index++)
   {
      printf("You’ll see this five times.\n");
   }
   return 0;
}
```

### 使用`while`循环

Objective-C 提供了另一种流行的循环：`while`循环。该循环在特定条件为真时持续执行其循环体。`while`循环的格式如下：

```c
while (condition)
{
   body
}
```

`while`循环检查`condition`（条件），如果它为真，则执行循环中的代码。当条件经过测试并结果为假时，循环停止。这是一个显示消息“You’ll see five times.”的`while`循环示例：

```c
#include <stdio.h>

int main(void)
{
   int loop_index = 0;
   while (loop_index < 5)
   {
      printf("You’ll see five times.\n");
      loop_index++;
   }
   return 0;
}
```

要使用 Objective-C 的`while`循环：

1. 创建一个名为`while.m`的新程序。
2. 在`while.m`中，输入**列表 2.15**所示的代码。这段代码创建了一个执行五次的`while`循环。
3. 添加每次循环时显示消息并递增`loop_index`的代码（**列表 2.16**）。
4. 保存`while.m`。
5. 运行`while.m`程序。你应该能看到以下内容：



You’ll see this five times.

You’ll see this five times.

You’ll see this five times.

You’ll see this five times.

You’ll see this five times.

```c
// Listing 2.15 Starting while.m.
#include <stdio.h>

int main(void)
{
   int loop_index = 0;
   while (loop_index < 5)
   {
      printf("You’ll see five times.\n");
      loop_index++;
   }
   return 0;
}
```

```c
// Listing 2.16 The while.m program.
#include <stdio.h>

int main(void)
{
   int loop_index = 0;
   while (loop_index < 5)
   {
      printf("You’ll see five times.\n");
      loop_index++;
   }
   return 0;
}
```

### 使用 `do...while` 循环

Objective-C 提供的另一种流行的循环是 `do...while` 循环。与 `while` 循环一样，该循环在特定条件为真时持续执行其循环体，但与 `while` 循环不同，它在循环体执行之后才检查条件。`do...while` 循环的格式如下：

```c
do
{
   body
} while (condition);
```

`do...while` 循环执行循环体，然后检查 `condition` 表达式；如果为真，循环再次执行。当条件经过测试并结果为假时，循环停止。

为什么除了 `while` 循环外你还需要 `do...while` 循环？你通常在循环条件在循环内首次设置时使用 `do...while` 循环：例如，如果你从文件中读取并在文件末尾终止循环，你需要在循环终止之前至少尝试读取一次，以查看文件中是否有任何数据供你读取。

这是一个显示消息“You’ll see five times.”的示例。这次使用了 `do...while` 循环：

```c
#include <stdio.h>

int main(void)
{
   int loop_index = 0;
   do {
      printf("You’ll see this five times.\n");
      loop_index++;
   } while (loop_index < 5);
   return 0;
}
```

## 第 2 章

### 使用 `do...while` 循环

要使用 Objective-C 的 `do...while` 循环：

1. 创建名为 `do.m` 的新程序。

2. 在 `do.m` 中，输入**列表 2.17** 所示的代码。此代码创建了一个执行五次的 `do...while` 循环。

3. 添加代码以在每次循环时显示消息，并递增 `loop_index`，`do...while` 循环会在每次循环迭代后检查该 `loop_index`（**列表 2.18**）。

4. 保存 `do.m`。

5. 运行 `do.m` 程序。你应该能看到以下内容：

你会看到这五次。

你会看到这五次。

你会看到这五次。

你会看到这五次。

你会看到这五次。

```c
#include <stdio.h>

int main(void)
{
    int loop_index = 0;
    do {
        .
        .
        .
    } while (loop_index < 5);
    return 0;
}
```

**列表 2.17** 开始 `do.m`。

```c
#include <stdio.h>

int main(void)
{
    int loop_index = 0;
    do {
        printf("You’ll see this five times.\n");
        loop_index++;
    } while (loop_index < 5);
    return 0;
}
```

**列表 2.18** `do.m` 程序。

### 指导程序流

#### 使用 `break` 语句

有时，你可能想要跳出循环——即终止它。例如，假设你正在快乐地打印从 -1/5 到 1/5 的倒数：

```c
#include <stdio.h>

int main(void)
{
    float loop_index;
    for (loop_index = 5; loop_index > -5; loop_index--)
    {
        printf("1/%2.1f = %10.6f\n", loop_index, 1.0/loop_index);
    }
    return 0;
}
```

然而，当你遇到 1/0（除以零）时，Objective-C 将报告错误。为了避免这种情况，你可以使用 `break` 语句在尝试除以 0 之前中断循环执行：

```c
#include <stdio.h>

int main(void)
{
    float loop_index;
    for (loop_index = 5; loop_index > -5; loop_index--)
    {
        if (loop_index == 0.0) {
            break;
        }
        printf("1/%2.1f = %10.6f\n", loop_index, 1.0/loop_index);
    }
    return 0;
}
```

`break` 语句会导致循环结束——在这种情况下，避免了除以零。

要使用 Objective-C 的 `break` 语句：

1. 创建名为 `break.m` 的新程序。

2. 在 `break.m` 中，输入**列表 2.19** 所示的代码。此代码会打印从 -1/5 到 1/5 的倒数，但对 1/0 会报告错误。

3. 添加代码在尝试除以 0 之前中断循环执行（**列表 2.20**）。

4. 保存 `break.m`。

5. 运行 `break.m` 程序。你应该能看到以下内容：

```text
1/5.0 = 0.200000

1/4.0 = 0.250000

1/3.0 = 0.333333

1/2.0 = 0.500000

1/1.0 = 1.000000
```

```c
#include <stdio.h>

int main(void)
{
    float loop_index;
    for (loop_index = 5; loop_index > -5; loop_index--)
    {
        printf("1/%2.1f = %10.6f\n", loop_index, 1.0/loop_index);
    }
    return 0;
}
```

**列表 2.19** 开始 `break.m`。

```c
#include <stdio.h>

int main(void)
{
    float loop_index;
    for (loop_index = 5; loop_index > -5; loop_index--)
    {
        if (loop_index == 0.0) {
            break;
        }
        printf("1/%2.1f = %10.6f\n", loop_index, 1.0/loop_index);
    }
    return 0;
}
```

**列表 2.20** `break.m` 程序。

## 第 3 章：数据处理

本章完全关于在 Objective-C 中处理数据。你将使用数组、指针等更多内容。

数组是一组数据项（称为元素），你可以通过索引来引用它们。例如，如果你将数字存储在名为 `array` 的数组中，你可以这样使用索引访问每个元素：`array[0]` 指向第一个元素；`array[1]` 指向第二个元素；依此类推。以下代码创建了一个包含五个元素的数组，在 `array[0]` 中存储值为 5，然后显示该值：

```c
#include <stdio.h>

int main(void)
{
    int array[5];
    array[0] = 5;
    printf("array[0] is %i.\n", array[0]);
    return 0;
}
```

指针是存储数据项地址的特殊变量。你可以使用 `&` 运算符将名为 `integer` 的变量地址存储在指针中，例如：`pointer = &integer;`。你可以像这样通过 `*pointer` 引用 `integer` 的值：

```c
#include <stdio.h>

int main(void)
{
    int integer, *pointer;
    integer = 1;
    pointer = &integer;
    *pointer = 2;
    printf("The value of the integer is: %i", pointer);
    return 0;
}
```

指针在 Objective-C 中非常，因为你用它们来创建对象。例如，Objective-C 中的文本字符串通常是 `NSString` 对象（“NS”部分代表 NeXT）。

## 数据处理

### 初始化数组

在声明数组时，可以通过在大括号中包含初始化值来初始化数组元素：

```c
#include <stdio.h>

int main()
{
    int scores[5] = {92, 73, 57, 98, 89};
    printf("The array is %i elements long.", sizeof(scores) / sizeof(int));
    return 0;
}
```

**初始化数组：**

1. 创建一个名为 `initializearray.m` 的新程序。

2. 在 `initializearray.m` 中，输入**Listing 3.3** 所示的代码。这段代码创建了数组并初始化了其元素的值。

3. 使用 `sizeof` 运算符获取整个数组的大小，并除以单个元素的大小来计算数组元素个数（**Listing 3.4**）。

4. 保存 `initializearray.m`。

5. 运行 `initializearray.m` 程序。你应该看到以下内容：

   The array is 5 elements long.

**Listing 3.3** 开始 `initializearray.m`。

```c
#include <stdio.h>

int main()
{
    int scores[5] = {92, 73, 57, 98, 89};
    printf("The array is %i elements long.", sizeof(scores) / sizeof(int));
    return 0;
}
```

**Listing 3.4** `initializearray.m` 程序。

```c
#include <stdio.h>

int main()
{
    int scores[5] = {92, 73, 57, 98, 89};
    printf("The array is %i elements long.", sizeof(scores) / sizeof(int));
    return 0;
}
```

## 第 3 章

### 遍历数组

数组和循环是天生一对的。数组存储一组数据，而循环让你对这类数据集进行迭代。遍历数组中的长数据集是计算机非常擅长的工作之一。

例如，如果你有一个学生成绩数组并想找到他们的平均分，可以使用 `for` 循环：

```c
int student_index, scores[5] = {92, 73, 57, 98, 89};
float sum = 0;
for (student_index = 0, sum = 0; student_index < 5; student_index++)
{
    sum += scores[student_index];
}
printf("Average score is %2.1f", sum / 5);
```

**遍历数组：**

1. 创建一个名为 `arrayloop.m` 的新程序。

2. 在 `arrayloop.m` 中，输入**Listing 3.5** 所示的代码。这段代码创建了 `scores` 数组并对其初始化。

3. 添加代码来求数组中所有元素的和并找到它们的平均值（**Listing 3.6**）。

4. 保存 `arrayloop.m`。

5. 运行 `arrayloop.m` 程序。你应该看到以下内容：

   Average score is 81.8

**Listing 3.5** 开始 `arrayloop.m`。

```c
#include <stdio.h>

int main()
{
    int student_index, scores[5] = {92, 73, 57, 98, 89};
    float sum = 0;
    for (student_index = 0, sum = 0; student_index < 5; student_index++)
    {
        sum += scores[student_index];
    }
    printf("Average score is %2.1f", sum / 5);
    return 0;
}
```

**Listing 3.6** `arrayloop.m` 程序。

```c
#include <stdio.h>

int main()
{
    int student_index, scores[5] = {92, 73, 57, 98, 89};
    float sum = 0;
    for (student_index = 0, sum = 0; student_index < 5; student_index++)
    {
        sum += scores[student_index];
    }
    printf("Average score is %2.1f", sum / 5);
    return 0;
}
```

### 创建二维数组

到为止我们处理的是一维数组，但你也可以创建多维数组。访问一维数组元素使用 `array[number]`，而访问二维数组元素使用 `array[row][column]`。

例如，如果你有一个三次考试的学生成绩数组并想找到每次考试的平均分，可以使用二维数组。你使用嵌套列表初始化二维数组并使用嵌套 `for` 循环遍历列表：

```c
int test_index, student_index, scores[3][5] = {
    {92, 73, 57, 98, 89},
    {88, 76, 23, 95, 72},
    {94, 82, 63, 99, 94}
};
float sum;
for (test_index = 0; test_index < 3; test_index++)
{
    for (student_index = 0, sum = 0; student_index < 5; student_index++)
    {
        sum += scores[test_index][student_index];
    }
    printf("Average for test %i is %2.1f\n", test_index + 1, sum / 5);
}
```

**创建二维数组：**

1. 创建一个名为 `array2.m` 的程序。

2. 在 `array2.m` 中，输入**Listing 3.7** 中的代码。这段代码创建了一个数组并遍历每一行。

3. 添加代码遍历每一列并显示每次考试的平均分（**Listing 3.8**）。

4. 保存 `array2.m`。

5. 运行 `array2.m` 程序。你应该看到：

   Average for test 1 is 81.8

   Average for test 2 is 70.8

   Average for test 3 is 86.4

**Listing 3.7** 开始 `array2.m`。

```c
#include <stdio.h>

int main()
{
    int test_index, student_index, scores[3][5] = {
        {92, 73, 57, 98, 89},
        {88, 76, 23, 95, 72},
        {94, 82, 63, 99, 94}
    };
    float sum;
    for (test_index = 0; test_index < 3; test_index++)
    {
    }
    return 0;
}
```

**Listing 3.8** `array2.m` 程序。



```c
#include <stdio.h>

int main()
{
    int test_index, student_index, scores[3][5] = {
        {92, 73, 57, 98, 89},
        {88, 76, 23, 95, 72},
        {94, 82, 63, 99, 94}
    };
    float sum;
    for (test_index = 0; test_index < 3; test_index++)
    {
        for (student_index = 0, sum = 0; student_index < 5; student_index++)
        {
            sum += scores[test_index][student_index];
        }
        printf("Average for test %i is %2.1f\n", test_index + 1, sum / 5);
    }
    return 0;
}
```

### 51

## 使用指针

指针存储项目在内存中的地址。你通过在前面加星号（`*`）来声明指针：

```c
int integer, *pointer;
```

然后你可以使用 `&` 运算符获取内存中变量的地址并赋值给指针：

```c
integer = 1;
pointer = &integer;
```

使用星号，你可以引用指针指向的数据：

```c
pointer = 2;
```

### 使用指针

1. 创建一个名为 `pointers.m` 的程序。
2. 在 `pointers.m` 中，输入**Listing 3.9** 所示的代码。这段代码创建了指针并赋值名为 `integer` 的变量地址。
3. 给指针指向的内存位置分配一个新值并显示存储在该位置的数据（**Listing 3.10**）。
4. 保存 `pointers.m`。
5. 运行 `pointers.m` 程序。你应该看到：

   The value of the integer: 2

**Listing 3.9** 开始 `pointers.m`。

```c
#include <stdio.h>

int main()
{
    int integer, *pointer;
    integer = 1;
    pointer = &integer;
    *pointer = 2;
    printf("The value of the integer: %i", *pointer);
    return 0;
}
```

**Listing 3.10** `pointers.m` 程序。

```c
#include <stdio.h>

int main()
{
    int integer, *pointer;
    integer = 1;
    pointer = &integer;
    *pointer = 2;
    printf("The value of the integer: %i", *pointer);
    return 0;
}
```

### 52

## 指针运算

如果你指向内存中连续排列的项（例如数组），你可以递增或减少指针以指向下一个或上一个项。下面的示例打印了数组的第一个数字，然后通过递增指针打印第二个数字：

```c
float values[4] = {0.0, 1.0, 2.0, 3.0};
float *pointer = &values[0];
printf("%f\n", *pointer);
printf("%f\n", ++pointer);
```

### 使用指针运算

1. 创建一个名为 `pointermath.m` 的程序。
2. 在 `pointermath.m` 中，输入**Listing 3.11** 中的代码。这段代码指向数组的第一个元素并打印它。
3. 添加代码递增指针并打印下一个元素（**Listing 3.12**）。
4. 保存 `pointermath.m`。
5. 运行 `pointermath.m` 程序。你应该看到：

   0.000000

   1.000000

**Listing 3.11** 开始 `pointermath.m`。

```c
#include <stdio.h>

int main()
{
    float values[4] = {0.0, 1.0, 2.0, 3.0};
    float *pointer = &values[0];
    printf("%f\n", *pointer);
    return 0;
}
```

**Listing 3.12** `pointermath.m`。

```c
#include <stdio.h>

int main()
{
    float values[4] = {0.0, 1.0, 2.0, 3.0};
    float *pointer = &values[0];
    printf("%f\n", *pointer);
    printf("%f\n", ++pointer);
    return 0;
}
```

## 数据处理

### 指针与数组的转换

要将数组作为指针：

1. 创建一个名为 `pointersarray.m` 的新程序。
2. 在 `pointersarray.m` 中，输入**Listing 3.13** 所示的代码。这段代码创建了一个数组并将数组名赋值给指针。
3. 添加用于显示所赋值元素值的代码（**Listing 3.14**）。
4. 保存 `pointersarray.m`。
5. 运行 `pointersarray.m` 程序。你应该看到以下内容：

`values[2] = 3.141590`

```c
#include <stdio.h>

int main()
{
    double values[10];
    double *pointer = values;
    pointer[2] = 3.14159;
}
```

**Listing 3.13** 开始 `pointersarray.m`。

```c
#include <stdio.h>

int main()
{
    double values[10];
    double *pointer = values;
    pointer[2] = 3.14159;
    printf("values[2] = %10.6f", values[2]);
    return 0;
}
```

**Listing 3.14** `pointersarray.m` 程序。

### 使用字符串

你可能认为 Objective-C 像内置的 `float` 和 `char` 一样带有内置的字符串类型，但它并没有。相反，Objective-C 使用 Foundation 类 `NSString`。你首先需要包含 Foundation 类（这意味着在 Windows、Linux 和 UNIX 上你必须使用 Makefile）；然后你就可以创建一个 `NSString` 对象类。与所有的 Objective-C 对象一样，你会得到该对象的指针，并可以这样初始化你的字符串：

```objc
#include <Foundation.h>
NSString *helloString = @"Hello there.";
```

引号文本前的 `@` 符号表示你想使用 Objective-C 风格的字符串，而不是默认的 C 风格字符串（Objective-C 字符串内置的功能比 C 字符串得多）。

要使用 Objective-C 字符串：

1. 创建一个名为 `string.m` 的新程序。
2. 在 `string.m` 中，输入**Listing 3.15** 所示的代码来创建并显示字符串。要用 `printf()` 打印字符串，你需要通过向其发送消息 `cString` 将字符串转换为 C 风格（你通过这种方式向 Objective-C 对象发送消息来与其通信）。

```c
#include <stdio.h>
#include <Foundation.h>

int main(void)
{
    NSString *helloString = @"Hello there.";
    printf("%s\n", [helloString cString]);
    return 0;
}
```

**Listing 3.15** 创建 `string.m`。

3. 保存 `string.m`。
4. 如果你在使用 Linux、UNIX 或 Windows，创建一个名为 `GNUmakefile` 的文件，如 **Listing 3.16** 所示，并遵循本章前面“创建 NS-Class 对象”中的说明，使用 Makefile 编译 `string.m`。
5. 保存 `GNUmakefile`。
6. 编译并运行 `string.m` 程序（在 Linux、UNIX 和 Windows 中，你通过 `./obj/string` 运行程序）。你应该看到以下内容：

`Hello there.`

```makefile
include $(GNUSTEP_MAKEFILES)/common.make
TOOL_NAME=string
string_OBJC_FILES=string.m
include $(GNUSTEP_MAKEFILES)/tool.make
```

**Listing 3.16** `GNUmakefile` 文件。

### 向字符串对象传递消息

与其他 Objective-C 对象一样，你通过向 `NSString` 对象传递消息来与其通信。例如，向字符串传递消息 `length` 会返回其长度，向它传递消息 `substringFromIndex` 则可以让你获取子字符串。例如，如果你想将一个包含整数的字符串转换为实际整数，你可以使用 `intValue` 消息，你可以像这样发送它：

`printf("The number is %i\n", [numberString intValue]);`

调用 Objective-C 字符串方法：

1. 创建一个名为 `stringtoint.m` 的新程序。
2. 在 `stringtoint.m` 中，输入**Listing 3.17** 所示的代码。这段代码创建了一个名为 `numberString` 的字符串，对其进行初始化，然后向它发送消息 `intValue` 将转换为整数并打印该整数。
3. 保存 `stringtoint.m`。
4. 如果你在使用 Linux、UNIX 或 Windows，创建一个名为 `GNUmakefile` 的文件，如 **Listing 3.18** 所示，并遵循本章前面“创建 NS-Class 对象”中的说明，使用 Makefile 编译 `stringtoint.m`。
5. 保存 `GNUmakefile`。
6. 编译并运行 `stringtoint.m` 程序（在 Linux、UNIX 和 Windows 中，你通过 `./obj/string` 运行程序）。你应该看到以下内容：

`The number is 5`

```c
#include <stdio.h>
#include <Foundation.h>

int main(void)
{
    NSString *numberString = @"5";
    printf("The number is %i\n", [numberString intValue]);
    return 0;
}
```

**Listing 3.17** 创建 `stringtoint.m`。

（注：此处原文中 Listing 3.18 疑似为笔误，应指 Listing 3.17，译文保持对应逻辑或根据上下文微调）

## 从函数返回返回值

除了向函数传递数据外，你还可以让函数返回数据。它们可以返回单个数据项——例如整数，也可以返回数组或对象。

要声明一个函数返回一个值，你需要在函数定义或声明中首先指定该数据值的类型。例如，你可以修改上一个任务中的 `adder()` 函数，使其返回一个包含传递给它的两个值的和的整数值，如下所示：

```c
int adder(int x, int y)
```

为了实际返回传递给 `adder()` 函数的两个值的和，你需要使用 `return` 语句：

```c
int adder(int x, int y)
{
    return x + y;
}
```

它的原理是：要从函数返回值，你需要在 `return` 关键字之后放置你想要返回的值。现在，当你调用 `adder()` 函数并向该函数传递数据时，调用本身将用函数的返回值所替换。因此，为了将 5 加 10 并显示结果，你可以使用以下代码：

```c
int value1 = 5, value2 = 10;
printf("%i + %i = %i", value1, value2, adder(value1, value2));
```

## 创建函数

### 从函数返回值

要从函数返回返回值：

1. 创建一个名为 `functionreturn.m` 的新程序。
2. 在 `functionreturn.m` 中，输入**列表 4.7** 所示的代码。此代码创建了 `adder()` 函数，并设置为返回传递给它的两个整数之和。
3. 添加调用 `adder()` 函数的代码，并向其传递两个整数（**列表 4.8**）。
4. 保存 `functionreturn.m`。
5. 运行 `functionreturn.m` 程序。你应该能看到以下内容：

   5 + 10 = 15

```c
#include <stdio.h>

int adder(int x, int y)
{
    return x + y;
}
```

**列表 4.7** 开始 `functionreturn.m`。

```c
#include <stdio.h>

int adder(int x, int y)
{
    return x + y;
}

int main()
{
    int value1 = 5, value2 = 10;
    printf("%i + %i = %i", value1, value2, adder(value1, value2));
    return 0;
}
```

**列表 4.8** `functionreturn.m` 程序。

### 使用函数作用域

作用域是指数据可见的范围。函数定义了它们自己的作用域。也就是说，当你在函数中定义变量时，它变成了该函数的局部变量，并优于相同变量的其他版本。例如，你可以像这样定义一个名为 `number` 的整数并将其设置为 1：

```c
int number = 1;
```

然后，你还可以在函数内部定义一个名为 `number` 的整数：

```c
int number = 1;

void function(void)
{
    int number = 2;
    printf("In the function the number is %i\n", number);
}
```

`number` 的局部版本在函数中具有高优先级，因此这里的 `printf()` 语句将显示 `number` 的值为 2。如果 `number` 没有在函数中局部定义，则将使用来自函数外部的版本，`printf()` 语句将显示值为 1。在 Objective-C 中，任何代码块——即包含在花括号中的代码，如函数体或 `if` 语句体——都定义了自己的作用域，因此局部变量始终优于定义在代码块外的变量。

要使用函数作用域：

1. 创建一个名为 `functionscope.m` 的新程序。
2. 在 `functionscope.m` 中，输入**列表 4.9** 所示的代码。此代码声明了一个名为 `number` 的整数并在 `main()` 中显示其值，然后调用了一个函数。

```c
#include <stdio.h>

void function(void);

int number = 1;

int main()
{
    printf("In main the number is %i\n", number);
    function();
    return 0;
}
```

**列表 4.9** 开始 `functionscope.m`。

3. 添加在局部以及代码块中都重新定义 `number` 的函数（**列表 4.10**）。
4. 保存 `functionscope.m`。
5. 运行 `functionscope.m` 程序。你应该能看到以下内容：

   In main the number is 1

   In the function the number is 2

   In the block the number is 3

   After the block the number is 2

```c
#include <stdio.h>

void function(void);

int number = 1;

int main()
{
    printf("In main the number is %i\n", number);
    function();
    return 0;
}

void function(void)
{
    int number = 2;
    printf("In the function number is %i\n", number);
    {
        int number = 3;
        printf("In the block number is %i\n", number);
    }
    printf("After the block number is %i\n", number);
}
```

**列表 4.10** `functionscope.m` 程序。

### 向函数传递指针

当你向函数传递指针时，该函数可以使用该指针更改调用代码中的数据。例如，这里有一个将指针传递给函数以更改变量的示例：



```c
int data = 1;
int *datapointer = &data;
printf("Before changer(), data = %i\n", data);
changer(datapointer);
printf("After changer(), data = %i\n", data);

void changer(int *pointer)
{
    *pointer = 2;
}
```

要向函数传递指针：

1. 创建一个名为 `functionpointers.m` 的新程序。

2. 在 `functionpointers.m` 中，输入列表 4.11 所示的代码。此代码将一个指针传递给名为 `changer()` 的函数。

```c
#include <stdio.h>
void changer(int *);
int main()
{
    int data = 1;
    int *datapointer = &data;
    printf("Before changer(), data = %i\n", data);
    changer(datapointer);
    printf("After changer(), data = %i\n", data);
    return 0;
}
```

列表 4.11 开始 `functionpointers.m`。

3. 添加 `changer()` 函数的代码，它可以更改数据（列表 4.12）。

4. 保存 `functionpointers.m`。

5. 运行 `functionpointers.m` 程序。你应该能看到以下内容：

```text
Before changer(), data = 1

After changer(), data = 2
```

```c
#include <stdio.h>
void changer(int *);
int main()
{
    int data = 1;
    int *datapointer = &data;
    printf("Before changer(), data = %i\n", data);
    changer(datapointer);
    printf("After changer(), data = %i\n", data);
    return 0;
}

void changer(int *pointer)
{
    *pointer = 2;
}
```

列表 4.12 `functionpointers.m` 程序。

## 向函数传递数组

向函数传递数组：

1. 创建一个名为 `functionarrays.m` 的新程序。

2. 在 `functionarrays.m` 中，输入列表 4.13 所示的代码。此代码创建了一个数组并将其传递给名为 `adder()` 的函数。

```c
#include <stdio.h>
long adder(int array[], int number_elements);
int main()
{
    int data[] = {1, 2, 3, 4};
    int total = adder(data, sizeof(data)/sizeof(int));
    printf("The total is %i\n", total);
    return 0;
}
```

列表 4.13 开始 `functionarrays.m`。

3. 添加 `adder()` 函数的代码（列表 4.14）。

4. 保存 `functionarrays.m`。

5. 运行 `functionarrays.m` 程序。你应该能看到以下内容：

```text
The total is 10
```

```c
#include <stdio.h>
long adder(int array[], int number_elements);
int main()
{
    int data[] = {1, 2, 3, 4};
    int total = adder(data, sizeof(data)/sizeof(int));
    printf("The total is %i\n", total);
    return 0;
}

long adder(int array[], int number_elements)
{
    long sum = 0;
    int loop_index;
    for (loop_index = 0; loop_index < number_elements; loop_index++)
        sum = sum + array[loop_index];
    return sum;
}
```

列表 4.14 `functionarrays.m` 程序。

## 向函数传递常量数据

众所周知，如果你向函数传递指针，这些函数就可以更改指针所指向的数据。由于数组可以兼作指针，如果你在函数中作为指针传递数组，该函数就会更改你的原始数组。为了避免这种情况，当你将数组的副本传递给函数时，将其标记为常量以便其被更改。你使用 `const` 关键字将数据标记为常量：

```c
int data[] = {1, 2, 3, 4};
int total = adder(data, sizeof(data)/sizeof(int));
printf("The total is %i\n", total);

long adder(const int array[], int number_elements)
{
    long sum = 0;
    int loop_index;
    for(loop_index = 0; loop_index < number_elements; loop_index++)
        sum = sum + array[loop_index];
    return sum;
}
```

在本任务中，我们将修改上任务的代码以使用常量数组。

向函数传递常量数组：

1. 创建一个名为 `functionpassconstarrays.m` 的新程序。

2. 在 `functionpassconstarrays.m` 中，输入列表 4.15 所示的代码。此代码创建了一个数组并将其传递给名为 `adder()` 的函数，该函数的原型表明它接收常量数组。

3. 添加代码以创建 `adder()` 函数，在函数的参数列表中将传递给该函数的数组标记为常量（列表 4.16）。

4. 保存函数 `passconstarrays.m`。

5. 运行函数 `passconstarrays.m` 程序。

你应该看到以下内容：

```text
The total is 10
```

```c
#include <stdio.h>

long adder(const int array[], int number_elements);

int main( )
{
    int data[] = {1, 2, 3, 4};
    int total = adder(data, sizeof(data)/sizeof(int));
    printf("The total is %i\n", total);
    return 0;
}

long adder(const int array[], int number_elements)
{
    long sum = 0;
    int loop_index;
    for (loop_index = 0; loop_index < number_elements; loop_index++)
        sum = sum + array[loop_index];
    return sum;
}
```

列表 4.16 函数 `passconstarrays.m` 程序。

## 使用递归

在 Objective-C 中，函数可以调用自己，这个过程被称为递归，而且这个过程通常有用。例如，假设你正在编写一个计算阶乘的函数：例如，6! = 6 x 5 x 4 x 3 x 2 x 1 = 720。这里有一个递归调用自己来计算阶乘的函数：

```c
int factorial(int value)
{
    if (value == 1) {
        return value;
    } else {
        return value * factorial(value - 1);
    }
}
```

让我们使用这个函数来计算 6!。使用递归：

1. 创建一个名为 `functionrecursion.m` 的新程序。

2. 在 `functionrecursion.m` 中，输入列表 4.17 所示的代码。此代码调用 `factorial()` 函数，并向其传递值为 6。

3. 添加代码以实现递归的 `factorial()` 函数（列表 4.18）。

4. 保存 `functionrecursion.m`。

5. 运行 `functionrecursion.m` 程序。

你应该看到以下内容：

```text
6! = 720
```

```c
#include <stdio.h>
int main( )
{
    printf("6! = %i\n", factorial(6));
    return 0;
}
```

列表 4.17 开始 `functionrecursion.m`。

```c
#include <stdio.h>

int factorial(int value);
int main( )
{
    printf("6! = %i\n", factorial(6));
    return 0;
}

int factorial(int value)
{
    if (value == 1) {
        return value;
    } else {
        return value * factorial(value - 1);
    }
}
```

列表 4.18 函数 `functionrecursion.m` 程序。

## 使用函数指针

在 Objective-C 中，函数名实际上是指针。你可以将函数名传递给其他函数，在接收的函数中，如果你将传递的函数名视为指针，就可以调用它。例如，你可以将函数名传递给函数 `caller_function()`，它将调用传递的函数：

```c
void caller_function(void (*pointer_to_function)())
{
    pointer_to_function();
}
```

调用函数指针：

1. 创建一个名为 `functionpointers.m` 的新程序。

2. 在 `functionpointers.m` 中，输入列表 4.19 所示的代码。此代码设置了一个名为 `printem()` 的函数，并将其名传递给 `caller_function()`。

```c
#include <stdio.h>
void printem(void);
void caller_function(void (*pointer_to_function)());
int main( )
{
    caller_function(printem);
    return 0;
}
void printem(void)
{
    printf("there");
}
```

列表 4.19 开始 `functionpointers.m`。

3. 添加代码实现 `caller_function()`，它将调用你传递它的函数指针（列表 4.20）。

4. 保存 `functionpointers.m`。

5. 运行 `functionpointers.m` 程序。

你应该看到以下内容：

```text
there
```

```c
#include <stdio.h>
void printem(void);
void caller_function(void (*pointer_to_function)());
int main( )
{
    caller_function(printem);
    return 0;
}
void printem(void)
{
    printf("there");
}
void caller_function(void (*pointer_to_function)())
{
    pointer_to_function();
}
```

列表 4.20 `functionpointers.m` 程序。

## 类和对象

正如第 1 章所讨论的，引入面向对象编程是为了让你处理更大的问题，让你能够将编程组件封装成易于记忆的对象。第 1 章使用的示例是一个冰箱。与其在开放代码中启动泵、调节温度和启动压缩机，不如将所有这些动作封装到一个包含数据（如温度）和方法（即函数，如 `compressor()`）的对象中。你只需要把食物放入冰箱，冰箱就会为你冷却；这些细节是隐藏的。

面向对象编程（OOP）让你使用类和对象，Objective-C 有它自己的类和对象的语法，如果你以前没有用过 Objective-C，这种语法需要一些时间来学习。这是一个我们在本章中剖析的示例：

```objc
#include <stdio.h>
#include <Foundation.h>

@interface Container : NSObject
{
    int number;
}
-(void)setNumber:(int)n;
-(int)intValue;
@end

@implementation Container

-(void)setNumber:(int)n
{
    number = n;
}

-(int)intValue
{
    return number;
}
@end

int main(void)
{
    Container *object = [Container new];
    [object setNumber:5];
    printf("The number is %i\n", [object intValue]);
    return 0;
}
```

代码的结果如下：

```text
The number is 5
```

### 创建 Objective-C 类和对象

在此任务中，你将看到如何创建类和对象，以对 Objective-C 语法进行概述。后续将填充细节。

创建类和对象：

1. 创建一个以 `.m` 结尾的新程序文件。

2. 为了创建一个类，你需要创建一个 `@interface` 部分（列出类的数据和方法声明）以及一个 `@implementation` 部分（提供方法的实现），使用列表 5.1 所示的语法。

除了使用这种语法外，你通过发送消息与对象通信，而不是直接调用方法。例如，要向对象的 `setNumber` 方法发送消息以将其存储的设置为 5，你需要发送如下消息：`[object setNumber:5]`。

Objective-C 类通常基于 `Foundation` 类，因此如果你在 Linux、UNIX 或 Windows 上，你需要创建一个 `Makefile`，确保你在该文件所在的目录，并在 GNUstep shell 中输入 `make`（关于设置环境变量以使用 `make` 的更多信息请参见第三章介绍）。如果你在名为 `xxxx.m` 的文件中输入代码，`Makefile` 应该如下所示：

```makefile
include $(GNUSTEP_MAKEFILES)/common.make
TOOL_NAME=xxxx
OBJC_FILES=xxxx.m
include $(GNUSTEP_MAKEFILES)/tool.make
```

然后要运行你的代码，在 GNUstep 提示符处输入：

```text
./obj/*xxxx
```

列表 5.1 创建类。

### 类与对象

83

### 创建 Objective-C 类和对象

3. 在 `main()` 函数中，你通过向 `class_name` 发送方法名作为消息来执行类方法：`[class_name class_method_name]`。你也可以使用新消息 `new` 来创建对象（对象在 Objective-C 中被处理为指针），如下所示：`class_name *object = [class_name new]`。然后，你可以通过向对象发送方法名作为消息来执行对象方法，如下所示：`[object object_method_name]`。列表 5.2 显示了这些代码。

> **提示**：类方法（在名称前加有 `+` 定义）可以直接使用类名来运行，而对象方法（在名称前加有 `-` 定义）要求你在运行它们之前先创建一个对象。

```objectivec
#include <Foundation/Foundation.h>

@interface class_name : NSObject
{
    data_type variable_name;
    data_ptype variable_name;
}

-(return_type)object_method_name;
+(return_type)class_method_name;

@end

@implementation class_name

-(return_type)object_method_name
{
    [code]
}

+(return_type)class_method_name
{
    [code]
}

@end

int main(void)
{
    [class_name class_method_name];
    class_name *object = [class_name new];
    [object object_method_name];
    return 0;
}
```

列表 5.2 使用类方法并创建对象。

第 5 章

84

### 使用类方法



类方法是一种你仅使用类名即可执行的方法——不需要对象。在类的`@interface`部分和`@implementation`部分中，你通过在方法名称前加加号`"+"`来定义类方法，如下所示，其中类返回了某些文本：

```objectivec
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface Container
+(const char *)classMethod;
@end

@implementation Container
+(const char *)classMethod
{
    return "Hello there.";
}
@end
```

现在，你可以通过向类发送方法名作为消息来执行该类方法，如下：

```objectivec
int main(void)
{
    printf("%s\n", [Container classMethod]);
    return 0;
}
```

你将在此任务中看到此示例的运行。

## 使用类方法创建并执行类方法

1. 创建一个名为`classmethod.m`的程序。
2. 在`classmethod.m`中，输入列表 5.3 所示的代码。该代码创建一个名为`Container`的类，其中包含一个方法`classMethod`，它返回一个字符串。
3. 添加`main()`函数来执行`classMethod`并显示返回的字符串（列表 5.4）。
4. 保存`classmethod.m`。
5. 运行`classmethod.m`程序。你应该看到以下内容：

```
Hello there.
```

```objectivec
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface Container
+(const char *)classMethod;
@end

@implementation Container
+(const char *)classMethod
{
    return "Hello there.";
}
@end
...
```

列表 5.3 开始`classmethod.m`。

```objectivec
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface Container
+(const char *)classMethod;
@end

@implementation Container
+(const char *)classMethod
{
    return "Hello there.";
}

int main(void)
{
    printf("%s\n", [Container classMethod]);
    return 0;
}
```

列表 5.4 `classmethod.m`程序。

## 创建对象

在这个任务中，你将开始创建对象。在这里，你将创建一个带有空`@interface`（表示该类派自`NSObject`）和空`@implementation`部分的类：

```objectivec
@interface FirstClass : NSObject
@end

@implementation FirstClass
@end
```

你将通过向类发送`new`消息来创建一个对象，然后如所示显示消息“Object created.”：

```objectivec
FirstClass *object = [FirstClass new];
printf("Object created.");
return 0;
```

要创建一个对象：

1. 创建一个名为`object.m`的程序。
2. 在`object.m`中，输入列表 5.5 所示的代码。该代码创建了`FirstClass`类。
3. 添加创建`FirstClass`类新对象的代码，并显示指示对象已创建的消息（列表 5.6）。
4. 保存`object.m`。
5. 运行`object.m`程序（忽略关于未使用变量`"object"`的警告）。你应该看到以下内容：

```
Object created.
```

```objectivec
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface FirstClass : NSObject
@end

@implementation FirstClass
@end
```

列表 5.5 开始`object.m`。

```objectivec
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface FirstClass : NSObject
@end

@implementation FirstClass
@end

int main(void)
{
    FirstClass *object = [FirstClass new];
    printf("Object created.");
    return 0;
}
```

列表 5.6 `object.m`程序。

## 创建对象方法

虽然你可以仅通过类名执行类方法，但你需要一个对象才能执行对象方法——因为对象方法可以存储数据。你通过在`@interface`部分和`@implementation`部分中在方法原型和定义前加减号`"-"`来定义对象方法，如下所示，其中创建一个返回字符串的对象方法：

```objectivec
@interface ClassWithMethod : NSObject
-(const char *)stringValue;
@end

@implementation ClassWithMethod
-(const char *)stringValue
{
    return "Hello there.";
}
@end
```

要创建一个对象方法：

1. 创建一个名为`objectmethod.m`的程序。
2. 在`objectmethod.m`中，输入列表 5.7 所示的代码。该代码创建了`ClassWithMethod`类。
3. 添加`main()`函数来执行`stringValue`对象方法（列表 5.8）。
4. 保存`objectmethod.m`。
5. 运行`objectmethod.m`程序。你应该能看到以下内容：

```
Hello there.
```

```objectivec
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface ClassWithMethod : NSObject
-(const char *)stringValue;
@end

@implementation ClassWithMethod
-(const char *)stringValue
{
    return "Hello there.";
}
@end
```

列表 5.7 开始`objectmethod.m`。

```objectivec
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface ClassWithMethod : NSObject
-(const char *)stringValue;
@end

@implementation ClassWithMethod
-(const char *)stringValue
{
    return "Hello there.";
}

int main(void)
{
    ClassWithMethod *object = [ClassWithMethod new];
    printf("%s\n", [object stringValue]);
    return 0;
}
```

列表 5.8 `objectmethod.m`程序。

## 在对象中存储数据

在上一个任务中，你了解了如何设置一个方法。但对象可以同时包含方法和数据。在这个任务中，你将学习如何在对象中存储数据。你还将学习如何向对象方法传递参数。你在`@interface`部分设置数据。然后你的代码可以在方法中通过名称访问这些变量。例如，这里的代码存储了一个整数：

```objectivec
@interface Container : NSObject
{
    int number;
}

-(void)setNumber:(int n);
-(int)intValue;
@end

@implementation Container
-(void)setNumber:(int n)
{
    number = n;
}
@end
```

然后你可以执行该类的对象，向它发送值 5 进行存储：`[object setNumber:5];`。

要在对象中存储数据：

1. 创建一个名为`objectdata.m`的程序。
2. 在`objectdata.m`中，输入列表 5.9 所示的代码。该代码设置了一个名为`number`的内部整数以及一个名为`setNumber`的方法用于将值存储在该整数中。

```objectivec
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface Container : NSObject
{
    int number;
}

-(void)setNumber:(int n);
-(int)intValue;
@end

@implementation Container
-(void)setNumber:(int n)
{
    number = n;
}

-(int)intValue
{
    return number;
}

@end
```

3. 创建一个对象，设置内部存储的数字的值，并显示该数字（列表 5.10）。
4. 保存`objectdata.m`。
5. 运行`objectdata.m`程序。

你应该看到以下内容：

```
The number is 5
```

```objc
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface Container:NSObject
{
    int number;
}

-(void)setNumber:(int) n;

-(int)intValue;

@end

@implementation Container

-(void)setNumber:(int) n
{
    number = n;
}

-(int)intValue
{
    return number;
}

@end

int main(void)
{
    Container *object = [Container new];
    [object setNumber: 5];
    printf("The number is %i\n", [object intValue]);
    return 0;
}
```

列表 5.10 `objectdata.m`程序。

## 向方法传递多个参数

当你向方法传递多个参数时，可以命名这些参数以保持清晰。例如，你可以创建一个接收两个数字的方法，并命名第二个参数（你可以选择任何名称）：

```objc
-(void)setNumbers:(int) n1 second:(int) n2;
```

调用此方法时，通过名称指定第二个参数的值：

`[object setNumbers:5 second:10];`

**向方法传递多个参数：**

1. 创建名为`multipleargs.m`的新程序。
2. 在`multipleargs.m`中输入列表 5.11 所示的代码。这段代码创建了接受两个参数的`setNumbers`方法。

```objc
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface Container:NSObject
{
    int number1;
    int number2;
}

-(void)setNumbers:(int) n1 second:(int) n2;

-(int)intValue1;

-(int)intValue2;

@end

@implementation Container

-(void)setNumbers:(int) n1 second:(int) n2
{
    number1 = n1;
    number2 = n2;
}

-(int)intValue1
{
    return number1;
}

-(int)intValue2
{
    return number2;
}

@end
```

列表 5.11 `multipleargs.m`。

3. 添加调用`setNumbers`方法的代码（列表 5.12）。
4. 保存`multipleargs.m`。
5. 运行`multipleargs.m`程序。

你应该看到以下内容：

```
The first number is 5
The second number is 10
```

```objc
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface Container:NSObject
{
    int number1;
    int number2;
}

-(void)setNumbers:(int) n1 second:(int) n2;

-(int)intValue1;

-(int)intValue2;

@end

@implementation Container

-(void)setNumbers:(int) n1 second:(int) n2
{
    number1 = n1;
    number2 = n2;
}

-(int)intValue1
{
    return number1;
}

-(int)intValue2
{
    return number2;
}

@end

int main(void)
{
    Container *object = [Container new];
    [object setNumbers:5 second:10];
    printf("The first number is %i\n", [object intValue1]);
    printf("The second number is %i\n", [object intValue2]);
    return 0;
}
```

列表 5.12 `multipleargs.m`程序。

## 在头文件中存储接口

在 Objective-C 中，通常将类的接口部分（由`@interface`关键字声明的部分）放在扩展名为`.h`的其自己的头文件中。为了保持简单，我们在这里没有这样做，但过程非常简单。你只需要将类的`@implementation`部分存储在如`header.h`这样的文件中：

```objc
#include <Foundation/Foundation.h>

@interface Container:NSObject
{
    int number;
}

-(void)setNumber:(int) n;

-(int)intValue;

@end
```

然后在你的程序中包含`header.h`：

```objc
#include "header.h"
```

**在头文件中存储接口：**

1. 创建名为`header.m`的新程序。
2. 在`header.m`中输入列表 5.13 所示的代码。这段代码只是我们的示例，允许你在对象中存储数字，而接口部分在`header.h`中（确保在代码顶部使用`#include "header.h"`行）。

```objc
#include "header.h"
#include <stdio.h>
#include <Foundation/Foundation.h>

@implementation Container

-(void)setNumber:(int) n
{
    number = n;
}

-(int)intValue
{
    return number;
}

@end

int main(void)
{
    Container *object = [Container new];
    [object setNumber: 5];
    printf("The number is %i\n", [object intValue]);
    return 0;
}
```

列表 5.13 `header.m`程序。

3. 保存`header.m`。
4. 在与`header.m`相同的目录下创建`header.h`，并添加列表 5.14 所示的代码。
5. 保存`header.h`。
6. 运行`header.m`程序。

你应该看到以下内容：

```
The number is 5
```



```objc
#include <Foundation/Foundation.h>

@interface Container:NSObject
{
    int number;
}

-(void)setNumber:(int)n;
-(int)intValue;

@end
```

**Listing 5.14** `header.h` 文件。

94

## 在头文件中添加实现

Objective-C 允许将类的实现部分（跟随 `@implementation` 关键字的部分）存储在头文件中，加上接口（见前面的任务）。

**在头文件中存储接口和实现：**

1. 创建名为 `header2.m` 的程序。
2. 在 `header2.m` 中输入 **Listing 5.15** 所示的代码。这段代码在 `header.h` 中声明的对象。
3. 保存 `header2.m`。
4. 将接口代码添加到 `header2.h`（**Listing 5.16**）。
5. 保存 `header2.h`。
6. 运行 `header2.m` 程序。

你应该看到以下内容：

The number is 5

```objc
#include "header.h"
#include <stdio.h>
#include <Foundation/Foundation.h>

int main(void)
{
    Container *object = [Container new];
    [object setNumber: 5];
    printf("The number is %i\n", [object intValue]);
    return 0;
}
```

**Listing 5.15** `header2.m` 程序。

```objc
#include <Foundation/Foundation.h>

@interface Container:NSObject
{
    int number;
}

-(void)setNumber:(int)n;
-(int)intValue;

@end

@implementation Container

-(void)setNumber:(int)n
{
    number = n;
}

-(int)intValue
{
    return number;
}

@end
```

**Listing 5.16** `header2.h` 文件。

95

## 链接多个文件

你可以链接多个文件来创建一个执行文件。你只需要修改你的文件（`makefile`）来列出所有的 `.m` 文件，如下：

```makefile
include $(GNUSTEP)/common.make
TOOL_NAME = main
main_OBJC_FILES = main.m container.m
include $(GNUSTEP)/tool.make
```

**链接多个文件：**

1. 创建名为 `main.m` 的新程序。
2. 在 `main.m` 中输入 **Listing 5.17** 所示的代码。
3. 保存 `main.m`。
4. 创建名为 `container.h` 的新文件。
5. 在 `container.h` 中输入 **Listing 5.18** 所示的代码。
6. 保存 `container.h`。
7. 创建名为 `container.m` 的新文件。

```objc
#include "container.h"
#include <stdio.h>
#include <Foundation/Foundation.h>

int main(void)
{
    Container *object = [Container new];
    [object setNumber: 5];
    printf("The number is %i\n", [object intValue]);
    return 0;
}
```

**Listing 5.17** `main.m` 程序。

```objc
#include <Foundation/Foundation.h>

@interface Container:NSObject
{
    int number;
}

-(void)setNumber:(int)n;
-(int)intValue;

@end
```

**Listing 5.18** `container.h` 文件。

## 第 5 章

### 链接多个文件

8. 在 `container.m` 中，输入**列表 5.19**所示的代码。
9. 保存 `container.m`。
10. 创建名为 `GNUmakefile` 的新文件。
11. 在 `GNUmakefile` 中，输入**列表 5.20**所示的代码。
12. 保存 `GNUmakefile`。
13. 运行 `main.m` 程序。你应该看到以下内容：

数字是 5

```objc
#include "container.h"
#include <Foundation/Foundation.h>

@implementation Container

-(void)setNumber:(int)n
{
    number = n;
}

-(int)intValue
{
    return number;
}

@end
```

**列表 5.19** `container.m` 程序。

```makefile
include $(GNUSTEP_MAKEFILES)/common.make
TOOL_NAME = main
main_OBJC_FILES = main.m container.m
include $(GNUSTEP_MAKEFILES)/tool.make
```

**列表 5.20** `GNUmakefile` 文件。

### 类与对象

#### 使用构造函数

在 Objective-C 中，与许多 OOP 语言一样，你可以使用构造函数，它们是在创建对象时用于初始化对象中数据的特殊方法。构造函数可以命名为任何名称，但通常被命名为 `init`。构造函数返回指向对象的指针，你通过调用父类的 `init` 方法获取该指针（父类是当前类派生的类，通常是 `NSObject`）：

```objc
-(Container*)init:(int)n
{
    self = [super init];
    if (self) {
        [self setNumber:n];
    }
    return self;
}
```

在你的代码中，你可以在创建对象时向构造函数传递值。例如，以下代码将对象中存储的数字初始化为 3：

```objc
Container *object = [[Container new] init:3];
```

**要使用构造函数：**

1. 创建名为 `constructor.m` 的新程序。
2. 在 `constructor.m` 中，输入**列表 5.21**所示的代码。该代码带有 `Container` 类的接口启动 `constructor.m`。

```objc
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface Container:NSObject
{
    int number;
}

-(void)setNumber:(int)n;
-(int)intValue;
-(Container*)init:(int)n;

@end

. . .
```

**列表 5.21** 启动 `constructor.m`。

3. 输入代码以添加类方法的实现，并使用构造函数方法创建一个新的 `Container` 对象，并将该对象内部存储的整数初始化为 3（**列表 5.22**）。
4. 保存 `constructor.m`。
5. 运行 `constructor.m` 程序。你应该看到以下内容：

数字是 3

```objc
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface Container:NSObject
{
    int number;
}

-(void)setNumber:(int)n;
-(int)intValue;
-(Container*)init:(int)n;

@end

@implementation Container

-(void)setNumber:(int)n
{
    number = n;
}

-(int)intValue
{
    return number;
}

-(Container*)init:(int)n
{
    self = [super init];
    if (self) {
        [self setNumber:n];
    }
    return self;
}

@end

int main(void)
{
    Container *object = [[Container new] init:3];
    printf("The number is %i\n", [object intValue]);
    return 0;
}
```

**列表 5.22** `constructor.m`。

## 第 6 章：面向对象编程

在本章中，我们将深入探讨 Objective-C 中的面向对象编程。首先，我们来看访问修饰符。

### 访问修饰符

三种访问修饰符：`public`（默认值）、`private`（限制访问到声明该变量类的代码中）以及 `protected`（限制访问到该类及其派生类的代码）。

因此，通过声明一个变量为私有，将其访问限制在类实现代码中。例如，以下代码：

```objc
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface Access:NSObject
{
@public
    int publicVariable;
@private
    int privateVariable;
}

@end

@implementation Access
@end

int main(void)
{
    Access *a = [Access new];
    a->privateVariable = 2;
    printf("The private variable is %i\n", a->privateVariable);
    return 0;
}
```

上述代码将无法编译，因为它尝试在类外部访问私有变量。为了解决这个问题，我们可以通过定义公共方法来访问私有变量：

```objc
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface Access:NSObject
{
@public
    int publicVariable;
@private
    int privateVariable;
}

-(int)getPrivateVariable;

@end

@implementation Access

-(int)getPrivateVariable
{
    return privateVariable;
}

@end

int main(void)
{
    Access *a = [Access new];
    a->privateVariable = 2;
    printf("The private variable is %i\n", [a getPrivateVariable]);
    return 0;
}
```

**列表 6.2** 使用方法访问私有变量。

### 公共访问

公共访问是成员的默认设置，但你也可以用 `@public` 修饰符指示成员是公有的。

**要使用公共访问：**

1. 创建名为 `access.m` 的程序。
2. 输入代码以创建一个公共成员。
3. 在 `main(void)` 函数中访问公共成员。
4. 保存 `access.m`。
5. 运行 `access.m` 程序。你应该看到以下内容：

变量是 1

```objc
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface Access:NSObject
{
@public
    int publicVariable;
}

@end

@implementation Access
@end

int main(void)
{
    Access *a = [Access new];
    a->publicVariable = 1;
    printf("The public variable is %i\n", a->publicVariable);
    return 0;
}
```

**列表 6.1** 创建 `access.m`。

### 私有访问

你使用 `@private` 访问修饰符将类成员设为私有。将成员设为私有将其访问限制在声明这些成员的类中。

**要使用私有访问：**

1. 打开上一个任务中的 `access.m` 程序进行编辑。
2. 在 `access.m` 中输入**列表 6.3**中高亮的新代码。该代码创建了一个私有数据成员。

```objc
#include <stdio.h>
#include <Foundation/Foundation.h>

@interface Access:NSObject
{
@public
    int publicVariable;
@private
    int privateVariable;
}

@end

@implementation Access
@end
```

## 第 6 章

### 使用私有访问

3. 添加代码尝试从对象外部访问私有数据成员（**列表 6.4**）。
4. 保存 `access.m`。
5. 尝试运行 `access.m`。

当你尝试编译 `access.m` 时，你将得到一个警告或硬性错误（取决于你使用的 Objective-C 版本以及运行的平台），因为你正尝试从对象外部访问私有成员。（注意，警告在未来将变成硬性错误。）

```objective-c
#import <stdio.h>
#import <Foundation/NSObject.h>

@interface Access : NSObject {
@public
    int publicVariable;
@private
    int privateVariable;
}
@end

@implementation Access

@end

int main(void)
{
    Access *a = [Access new];
    a->publicVariable = 1;
    printf("The public variable is %i\n", a->publicVariable);
    // a->privateVariable = 2;
    // printf("The private variable is %i\n", a->privateVariable);
    return 0;
}
```

**列表 6.4** `access.m` 程序。

## 使用受保护访问

你使用 `@protected` 访问限定符将类成员设置为受保护。将成员设置为受保护会将访问权限限制在声明该成员的类以及基于该类的类中。

**使用受保护访问：**

1. 打开上一个任务中的 `access.m` 程序进行编辑。
2. 在 `access.m` 中，输入**列表 6.5** 中高亮的新代码。这段代码创建了一个受保护的数据成员。

```objective-c
#import <stdio.h>
#import <Foundation/NSObject.h>

@interface Access : NSObject {
@public
    int publicVariable;
@private
    int privateVariable;
@protected
    int protectedVariable;
}
@end

@implementation Access

@end
```

**列表 6.5** 开始 `access.m`。

3. 添加**列表 6.6** 所示的代码，尝试从包含该成员的对象外部访问受保护成员。
4. 保存 `access.m`。
5. 尝试运行 `access.m`。

当你尝试编译 `access.m` 时，你将得到一个警告或硬性错误（取决于你使用的 Objective-C 版本以及运行的平台），因为你正尝试从对象外部访问受保护成员。（注意，警告在未来将变成硬性错误。）



```objective-c
#import <stdio.h>
#import <Foundation/NSObject.h>

@interface Access : NSObject {
@public
    int publicVariable;
@private
    int privateVariable;
@protected
    int protectedVariable;
}
@end

@implementation Access

@end

int main(void)
{
    Access *a = [Access new];
    a->publicVariable = 1;
    printf("The public variable is %i\n", a->publicVariable);
    //a->privateVariable = 2;
    //printf("The private variable is %i\n", a->privateVariable);
    a->protectedVariable = 3;
    printf("The protected variable is %i\n", a->protectedVariable);
    return 0;
}
```

**列表 6.6** `object.m` 程序。

## 使用类变量

你可以为你的类创建类变量，但有一个问题：该类的每个对象都共享同一个变量，因此如果一个对象更改了类变量，所有对象的该变量都会发生改变。你使用 `static` 关键字创建类变量。类变量通常非常有用：例如，你可以使用类变量来跟踪程序中特定类的对象数量。你将在此任务中这样做。

### 使用类变量

1. 创建一个名为 `classvariables.m` 的新程序。
2. 在 `classvariables.m` 中，输入**列表 6.7** 所示的代码。这段代码创建了一个带有名为 `count` 变量的类。

```objective-c
#import <stdio.h>
#import <Foundation/NSObject.h>

@interface TheClass : NSObject
static int count;
+(int)getCount;
@end

@implementation TheClass

-(TheClass*)init
{
    self = [super init];
    count++;
    return self;
}

+(int)getCount
{
    return count;
}
@end
```

**列表 6.7** 开始 `classvariables.m`。

3. 添加代码创建两个对象并每次显示对象计数（**列表 6.8**）。
4. 保存 `classvariables.m`。
5. 运行 `classvariables.m` 程序。你应该看到以下内容：

```text
TheClass count is 1

TheClass count is 2
```

```objective-c
#import <stdio.h>
#import <Foundation/NSObject.h>

@interface TheClass : NSObject
static int count;
+(int)getCount;
@end

@implementation TheClass

-(TheClass*)init
{
    self = [super init];
    count++;
    return self;
}

+(int)getCount
{
    return count;
}
@end

int main(void)
{
    TheClass *tc1 = [TheClass new];
    printf("TheClass count is %i\n", [TheClass getCount]);
    TheClass *tc2 = [TheClass new];
    printf("TheClass count is %i\n", [TheClass getCount]);
    return 0;
}
```

**列表 6.8** `classvariables.m` 程序。

## 访问当前对象

有时，你需要在类内部访问当前对象。例如，你需要在构造函数中返回当前对象的指针。

要访问当前对象，使用 `self` 关键字。

### 访问当前对象

1. 打开上一个任务中的 `classvariables.m` 程序进行编辑。
2. 将构造函数返回的 `self`（**列表 6.9**）。

```objective-c
#import <stdio.h>
#import <Foundation/NSObject.h>

@interface TheClass : NSObject
static int count;
+(int)getCount;
@end

@implementation TheClass

-(TheClass*)init
{
    self = [super init];
    count++;
    return self;
}

+(int)getCount
{
    return count;
}
@end

int main(void)
{
    TheClass *tc1 = [TheClass new];
    printf("TheClass count is %i\n", [TheClass getCount]);
    TheClass *tc2 = [TheClass new];
    printf("TheClass count is %i\n", [TheClass getCount]);
    return 0;
}
```

**列表 6.9** 编辑 `classvariables.m`。

3. 使用 `self` 关键字获取**列表 6.10** 所示的当前对象的指针。这里，你从构造函数中返回当前对象的指针。

```objective-c
#import <stdio.h>
#import <Foundation/NSObject.h>

@interface TheClass : NSObject
static int count;
+(int)getCount;
@end

@implementation TheClass

-(TheClass*)init
{
    self = [super init];
    count++;
    return self;
}

+(int)getCount
{
    return count;
}
@end

int main(void)
{
    TheClass *tc1 = [TheClass new];
    printf("TheClass count is %i\n", [TheClass getCount]);
    TheClass *tc2 = [TheClass new];
    printf("TheClass count is %i\n", [TheClass getCount]);
    return 0;
}
```

**列表 6.10** 带有当前对象指针的 `classvariables.m` 程序。

## 创建对象类型的变量

在 Objective-C 中，`id` 类型可以代表任何类型的对象。当你希望一个变量包含多种对象时，这非常有用。在这个任务中，你创建了两种不同类型的对象，并将它们放在类型为 `id` 的同一个变量中。

### 使用 `id` 类型

1. 创建一个名为 `id.m` 的新程序。
2. 在 `id.m` 中，输入**列表 6.11** 所示的代码。这段代码创建了你将使用的两个类。

```objective-c
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1 : NSObject
-(void)print;
@end

@implementation Class1

-(void)print
{
    printf("This is Class 1.\n");
}
@end

@interface Class2 : NSObject
-(void)print;
@end

@implementation Class2

-(void)print
{
    printf("This is Class 2.\n");
}
@end
```

**列表 6.11** 开始 `id.m`。

### 为多个对象类型创建变量

3. 添加代码以创建两个不同类的对象，并将这些对象连续存储在 `id` 变量中（**列表 6.12**）。
4. 保存 `id.m`。
5. 运行 `id.m` 程序。你应该能看到以下内容：

```text
This is Class 1.

This is Class 2.
```

```objective-c
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1

-(void)print
{
    printf("This is Class 1.\n");
}
@end

@interface Class2:NSObject
-(void)print;
@end

@implementation Class2
-(void)print
{
    printf("This is Class 2.\n");
}
@end

int main(void)
{
    Class1 *c1 = [Class1 new];
    Class2 *c2 = [Class2 new];
    id container;
    container = c1;
    [container print];
    container = c2;
    [container print];
    return 0;
}
```

**列表 6.12** `id.m` 程序。

### 验证对象是否属于某个类

你可以使用 `isMemberOfClass` 方法来确定一个对象是否属于某个类。在下一个任务中，你将使用该方法来验证某个对象是否属于某个类（在这里称为 `Class1`）。你可以通过简单向类发送 `class` 消息来获取类的名称，例如：`[Class1 class]`。

#### 使用 `isMemberOfClass`

1. 创建名为 `isMemberOfClass.m` 的新程序。
2. 在 `isMemberOfClass.m` 中，输入**列表 6.13** 所示的代码。这段代码创建了 `Class1` 类。

```objective-c
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1

-(void)print
{
    printf("This is Class 1.\n");
}
@end

...
```

**列表 6.13** 开始 `isMemberOfClass.m`。

3. 添加代码以创建 `Class1` 类的对象，并验证该对象确实属于 `Class1` 类（**列表 6.14**）。
4. 保存 `isMemberOfClass.m`。
5. 运行 `isMemberOfClass.m` 程序。你应该能看到以下内容：

```text
c1 is a member of Class1.
```

```objective-c
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1

-(void)print
{
    printf("This is Class 1.\n");
}
@end

int main(void)
{
    Class1 *c1 = [Class1 new];
    if ([c1 isMemberOfClass:[Class1 class]] == YES ) {
        printf("c1 is a member of Class1.\n");
    }
    return 0;
}
```

**列表 6.14** `isMemberOfClass.m` 程序。

### 使用 `isKindOfClass` 检查对象的类

你也可以使用 `isKindOfClass` 来确定一个对象是否属于某个类。`isMemberOfClass` 和 `isKind` 之间有什么区别？你可以使用 `isKindOfClass` 来确定一个对象是否属于某个类——或者属于该类的任何派生类。例如，我们可以使用 `isKindOfClass` 来确定一个对象是否属于某个类。

#### 使用 `isKindOfClass`

1. 创建一个名为 `kind.m` 的新程序。
2. 在 `kind.m` 中，输入**列表 6.15** 所示的代码。这段代码创建了类的基类。

```objective-c
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1

-(void)print
{
    printf("This is Class 1.\n");
}
@end

...
```

**列表 6.15** 开始 `kind.m`。

3. 添加代码以创建 `Class1` 类的对象，并验证该对象是否属于 `Class1` 类或其派生类（**列表 6.16**）。
4. 保存 `kind.m`。
5. 运行 `kind.m` 程序。你应该能看到以下内容：

```text
c1 is a member of Class1.
```

```objective-c
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1

-(void)print
{
    printf("This is Class 1.\n");
}
@end

int main(void)
{
    Class1 *c1 = [Class1 new];
    if ([c1 isKindOfClass:[Class1 class]] == YES ) {
        printf("c1 is a member of Class1.\n");
    }
    return 0;
}
```

**列表 6.16** `kind.m` 程序。

### 验证对象是否支持方法

在 Objective-C 中，对象可以响应方法。但你知道一个对象是否支持某个方法吗？你可以使用 `respondsToSelector` 方法。

#### 使用 `respondsToSelector`

1. 创建名为 `responds.m` 的新程序。
2. 在 `responds.m` 中，输入**列表 6.17** 所示的代码。这段代码创建了支持该方法的 `Class1` 类。

```objective-c
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1

-(void)print
{
    printf("This is Class 1.\n");
}
@end

...
```

**列表 6.17** 开始 `responds.m`。

### 判断类是否支持方法

除了检查对象是否支持某个方法外，你还可以检查一个类是否创建支持该方法的对象。为了这一点，你可以使用 `instancesRespondToSelector` 方法。

#### 使用 `instancesRespondToSelector`

1. 创建名为 `instances.m` 的新程序。
2. 在 `instances.m` 中，输入**列表 6.19** 所示的代码。这段代码创建了支持 `print` 方法的 `Class1` 类。

```objective-c
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1

-(void)print
{
    printf("This is Class 1.\n");
}
@end

...
```

**列表 6.19** 开始 `instances.m`。



```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1

-(void)print
{
    printf("This is Class 1.\n");
}
@end

int main(void)
{
    if ([Class1 instancesRespondToSelector:@selector(print)] == YES) {
        printf("Class1 objects have a print method.\n");
    }
    return 0;
}
```

**列表 6.20** `instances.m` 程序。

## 使用面向对象的继承

本章讨论了从一个类派生出另一个类的过程——这一过程被称为*继承*。

在 Objective-C 中，你可以从一个类派生出另一个类。你所派生的类称为*基类*（base class），而基于基类派生的新类称为*派生类*（derived class）。

派生类可以继承基类的所有功能，也可以对这些功能进行自定义。例如，你可能有一个名为 `Animal` 的基类，它创建一个通用的动物。`Animal` 类可能有一个用于设置动物名称的方法 `setName`，以及另一个用于获取动物名称的方法 `getName`。那么，无论你想创建什么种类的动物，`Animal` 都可以作为它的基类，所有派生的动物都将拥有内置的 `setName` 和 `getName` 方法。

你可能会将 `Animal` 作为其他类（如 `Cat` 和 `Dog`）的基类。例如，如果你创建一个名为 `Cat` 的类，你可能需要的不仅仅是 `setName` 和 `getName` 方法；例如，你可能还会添加你自己的方法，即 `meow` 方法，用于打印“Meow”。

如果你也从 `Animal` 类派生出一个名为 `Dog` 的类，你可能会向它添加一个名为 `bark` 的方法。

那么，`Cat` 类将拥有 `setName`、`getName` 和 `meow` 方法。`Dog` 类将拥有 `setName`、`getName` 和 `bark` 方法。正如你所看到的，尽管 `Dog` 和 `Cat` 类共享某些功能，但由于它们都是动物类，它们也经过了自定义。

这就是继承背后的思想：当你想要创建共享某些功能的类时，就可以使用继承。通过使用继承，你可以节省大量工作。在这个示例中，除了 `Cat` 和 `Dog` 类之外，你可能还会使用 `Animal` 类派生出 `Tiger`、`Leopard`、`Lion`、`Squid` 和 `Ocelot` 类。

你还可以实现多级继承。例如，你可能会使用 `Dog` 类作为 `Terrier` 和 `Collie` 类的基类。

- **tip**：尽管 Objective-C 中的继承是一个强大的工具，但它缺乏 C++ 以及一些其他面向对象编程语言中具备的功能。例如，它缺乏运算符重载，也缺乏多重继承（即一个类可以继承自多个其他类）。

## 继承类

我们将首先看看如何从一个类派生出另一个类。事实上，你一直编写的程序已经在从 `NSObject` 继承类，而将这种能力扩展到任何类都是很容易。

在这里，你将基于 `NSObject` 创建一个类，`Class1`：

```objectivec
@interface Class1 : NSObject
@end
```

然后，你将基于 `Class1` 创建另一个类，`Class2`：

```objectivec
@interface Class2 : Class1
@end
```

这些类实际上不会执行任何操作——我们只是在查看继承的语法。在后续任务中，你将向基类和派生类添加数据成员和方法。

**继承一个类：**

1. 创建名为 `inheritance.m` 的新程序文件。

2. 在 `inheritance.m` 中，输入**列表 7.1**所示的代码以创建 `Class1` 基于其上的基类 `Class2`。

3. 在 `main()` 函数中显示一条消息以表示继承成功（**列表 7.2**）。

4. 保存 `inheritance.m`。

5. 运行 `inheritance.m` 程序。你应该看到以下内容：

   The inheritance worked.

**列表 7.1** 创建 `inheritance.m`。

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1 : NSObject
@end

@implementation Class1
@end

@interface Class2 : Class1
@end

@implementation Class2
@end
```

**列表 7.2** 继承成功的程序。

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1 : NSObject
@end

@implementation Class1
@end

@interface Class2 : Class1
@end

@implementation Class2
@end

int main(void) {
    printf("The inheritance worked.\n");
    return 0;
}
```

## 继承基类数据成员

当你将一个类建立在另一个类之上时，所有未声明为 `@private` 的成员在派生类中都是可访问的。在这个示例中，你将在基类中声明一个名为 `data` 的数据成员，并从派生类的对象引用它。

**继承基类数据：**

1. 创建一个名为 `inheritdata.m` 的程序。

2. 在 `inheritdata.m` 中，输入**列表 7.3**中高亮的代码。该代码创建了带有 `data` 数据成员的 `Class1`，并基于它派生出一个名为 `Class2` 的类。注意 `data` 被声明为 `@public`，这使得它可以从基类、派生类以及程序中的任何其他代码访问。

**列表 7.3** 开始 `inheritdata.m`。

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1 : NSObject
{
    @public
    int data;
}
@end

@implementation Class1
@end

@interface Class2 : Class1
@end

@implementation Class2
@end
```

3. 添加代码创建派生类 `Class2` 的对象，并使用该对象访问数据成员（**列表 7.4**）。

4. 保存 `inheritdata.m`。

5. 运行 `inheritdata.m` 程序。你应该看到以下内容：

   The data is 5.

**列表 7.4** `inheritdata.m` 程序。

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1 : NSObject
{
    @public
    int data;
}
@end

@implementation Class1
@end

@interface Class2 : Class1
@end

@implementation Class2
@end

int main(void) {
    Class2 *c2 = [Class2 new];
    c2->data = 5;
    printf("The data is %d.\n", c2->data);
    return 0;
}
```

## 继承基类方法

当派生类继承基类时，除非标记为 `@private`，否则基类的方法在派生类中是可用的。在这个任务中，派生类将继承一个有一个方法的基类，并添加一个方法。然后你调用这两个方法以验证它们运行正常。

**继承基类方法：**

1. 创建一个名为 `inheritmethods.m` 的程序。

2. 在 `inheritmethods.m` 中，输入**列表 7.5**中高亮的代码。该代码创建了 `Class1` 和 `Class2`，每个都有内置方法。

**列表 7.5** 开始 `inheritmethods.m`。

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1 : NSObject
-(void)print;
@end

@implementation Class1
-(void)print {
    printf("This is Class 1.\n");
}
@end

@interface Class2 : Class1
-(void)print2;
@end

@implementation Class2
-(void)print2 {
    printf("This is Class 2.\n");
}
@end
```

3. 添加代码创建派生类的对象，并调用基类方法和派生类方法以验证它们工作正常（**列表 7.6**）。

4. 保存 `inheritmethods.m`。

5. 运行 `inheritmethods.m` 程序。你应该看到以下内容：

   This is Class 1.

   This is Class 2.

**列表 7.6** `inheritmethods.m` 程序。

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>

@interface Class1 : NSObject
-(void)print;
@end

@implementation Class1
-(void)print {
    printf("This is Class 1.\n");
}
@end

@interface Class2 : Class1
-(void)print2;
@end

@implementation Class2
-(void)print2 {
    printf("This is Class 2.\n");
}
@end

int main(void) {
    Class2 *c2 = [Class2 new];
    [c2 print];
    [c2 print2];
    return 0;
}
```

# 第 7 章

## 方法重写（Override）

假设你在基类中有一个需要更改的方法。例如，假设在基类 `Class1` 中有一个名为 `print` 的方法，它输出“This is class 1.”。显然，在派生类 `Class2` 中，信息应该是“This is class 2.”。

你只需在派生类中重新定义该方法，就可以*覆盖*基类的 `print` 方法。当你在派生类中重写方法时，覆盖的方法必须与你正在覆盖的方法具有相同的原型（相同的返回值和参数）。

**重写基类方法：**

1. 创建一个名为 `override.m` 的新程序。

2. 在 `override.m` 中，输入列表 7.7 所示的代码。此代码创建了 `Class1` 并从中派生出 `Class2`。每个类都有一个名为 `print` 且具有相同的方法，因此 `Class2` 的版本将覆盖 `Class1` 的版本。

```objc
#import <stdio.h>
#include <Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1
-(void)print
{
    printf("This is class 1.");
}
@end

@interface Class2:Class1
-(void)print;
@end

@implementation Class2
-(void)print
{
    printf("This is class 2.");
}
@end
```

列表 7.7 开始 `override.m`。

3. 添加代码来创建 `Class2` 的对象并调用被重写的 `print` 方法（列表 7.8）。

4. 保存 `override.m`。

5. 运行 `override.m` 程序。你应该会看到：This is class 2.

```objc
#import <stdio.h>
#include <Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1
-(void)print
{
    printf("This is class 1.");
}
@end

@interface Class2:Class1
-(void)print;
@end

@implementation Class2
-(void)print
{
    printf("This is class 2.");
}
@end

int main(void)
{
    Class2 *c2 = [Class2 new];
    [c2 print];
    return 0;
}
```

列表 7.8 `override.m` 程序。

## 方法重载（Overloading）

你也可以对方法进行*重载*。当你重载一个方法时，你为它提供了多个定义，Objective-C 会根据参数列表选择正确的方法版本——对于重载方法的每个版本，参数的类型和数量必须是不同的。

**重载基类方法：**

1. 创建一个名为 `overload.m` 的新程序。

2. 在 `overload.m` 中，输入列表 7.9 所示的代码。此代码创建了 `Class1` 并从中派生出 `Class2`；`Class1` 有一个无参数的 `print` 方法，而 `Class2` 有一个接受一个参数的 `print` 方法。

```objc
#import <stdio.h>
#include <Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1
-(void)print
{
    printf("Hello there.");
}
@end

@interface Class2:Class1
-(void)print:(int)x;
@end

@implementation Class2
-(void)print:(int)x
{
    printf("Your number is %i.\n", x);
}
@end

int main(void)
{
    Class2 *c2 = [Class2 new];
    [c2 print];
    [c2 print:5];
    return 0;
}
```

列表 7.9 开始 `overload.m`。

3. 添加代码来创建 `Class2` 的对象并调用两个 `print` 方法：一个带参数，一个不带参数（列表 7.10）。

4. 保存 `overload.m`。

5. 运行 `overload.m` 程序。你应该看到看到：Hello there. Your number is 5.

```objc
#import <stdio.h>
#include <Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1
-(void)print
{
    printf("Hello there.");
}
@end

@interface Class2:Class1
-(void)print:(int)x;
@end

@implementation Class2
-(void)print:(int)x
{
    printf("Your number is %i.\n", x);
}
@end

int main(void)
{
    Class2 *c2 = [Class2 new];
    [c2 print];
    [c2 print:5];
    return 0;
}
```

列表 7.10 `overload.m` 程序。

## 多级继承

Objective-C 中的继承并不局限于单层。类可以继承任意数量级的基类。本例示例展示了两级继承。

**使用多级继承：**

1. 创建一个名为 `multilevel.m` 的新程序。

2. 在 `multilevel.m` 中，输入列表 7.11 所示的代码。此代码创建了你将使用的三个类。

```objc
#import <stdio.h>
#include <Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1
-(void)print
{
    printf("This is class 1.");
}
@end

@interface Class2:Class1
-(void)print2;
@end

@implementation Class2
-(void)print2
{
    printf("This is class 2.");
}
@end

@interface Class3:Class2
-(void)print3;
@end

@implementation Class3
-(void)print3
{
    printf("This is class 3.");
}
@end
```

列表 7.11 开始 `multilevel.m`。



3. 添加代码来创建不同类的对象并依次调用它们（列表 7.12）。

4. 保存`multilevel.m`。

5. 运行`multilevel.m`程序。你应该看到：This is class 1. This is class 2. This is class 3。

```objc
#import <stdio.h>
#include <Foundation.h>

@interface Class1:NSObject
-(void)print;
@end

@implementation Class1
-(void)print
{
    printf("This is class 1.");
}
@end

@interface Class2:Class1
-(void)print2;
@end

@implementation Class2
-(void)print2
{
    printf("This is class 2.");
}
@end

@interface Class3:Class2
-(void)print3;
@end

@implementation Class3
-(void)print3
{
    printf("This is class 3.");
}
@end

int main(void)
{
    Class3 *c3 = [Class3 new];
    [c3 print];
    [c3 print2];
    [c3 print3];
    return 0;
}
```

列表 7.12 The`multilevel.m`程序。

## 限制访问

默认情况下，基类的数据成员和方法对派生类是可见的，但这并不总是个好主意：例如，如果基类有一个派生类不需要访问的内部变量。在这种情况下，可以使用`private`修饰符将该数据成员标记为私有。你在上一章中见过`private`，但这里我们将在继承中使用它。

为了停止继承：

1. 创建一个名为`private.m`的新程序。

2. 在`private.m`中，输入列表 7.13 所示的代码。此代码创建了你将使用的类，并将基类的数据成员标记为私有。

```objc
#import <stdio.h>
#include <Foundation.h>

@interface Class1:NSObject
{
    @private
    int privateVariable;
}
@end

@implementation Class1
@end

@interface Class2:Class1
-(void)print;
@end

@implementation Class2
@end
```

列表 7.13 Starting`private.m`。

3. 添加代码，在派生类中尝试访问基类的私有变量（列表 7.14）。

4. 保存`private.m`。

5. 尝试运行`private.m`程序。根据你的平台，你可能会得到一个硬错误（程序无法编译）或一个警告，提示未来该警告将变为硬错误。

```objc
#import <stdio.h>
#include <Foundation.h>

@interface Class1:NSObject
{
    @private
    int privateVariable;
}
@end

@implementation Class1
@end

@interface Class2:Class1
-(void)print;
@end

@implementation Class2
-(void)print
{
    privateVariable = 5;
    printf("The private variable is %i.", privateVariable);
}
@end

int main(void)
{
    Class2 *c2 = [Class2 new];
    [c2 print];
    return 0;
}
```

列表 7.14 The`private.m`程序。

# 第 7 章：限制访问权限

如果你将类成员标记为`@protected`，你也可以限制继承。这种访问修饰符的限制性比`@private`要小；派生类仍然可以使用基类的受保护成员，但其他任何代码都无法使用。也就是说，受保护的成员仅对基类中的代码以及任何派生自基类的类可见。你已经在上一章中学习了`@protected`；在这里，你将在继承中使用它。

**若要限制继承权限：**

1. 创建一个名为`protected.m`的新程序。

2. 在`protected.m`中，输入列表 7.15 所示的代码。这段代码创建了你将使用的两个类。

```objectivec
#import <stdio.h>
#import <Foundation/NSObject.h>

@interface Class1 : NSObject {
@protected
    int protectedVariable;
}
@end
@implementation Class1

@end

@interface Class2 : Class1 

-(void) print;
@end

@implementation Class2

-(void) print
{
    protectedVariable = 5;
    printf("The protected variable is %i\n", protectedVariable);
}

@end
```

列表 7.15 开始`protected.m`。

## 限制访问权限

3. 添加派生类中访问受保护成员的代码（列表 7.16）。

4. 保存`protected.m`。

5. 运行`protected.m`程序。你应该看到以下内容：

protected variable is 5.

```objectivec
#import <stdio.h>
#import <Foundation/NSObject.h>

@interface Class1 : NSObject {
@protected
    int protectedVariable;
}
@end

@implementation Class1

@end

@interface Class2 : Class1

-(void) print;
@end

@implementation Class2

-(void) print
{
    protectedVariable = 5;
    printf("The protected variable is %i\n", protectedVariable);
}

@end

int main(void)
{
    Class2 *c = [Class2 new];
    [c print];
    return 0;
}
```

列表 7.16`protected.m`程序。

## 在继承中使用构造函数

如果基类有构造函数怎么办？当你使用`super`关键字时，可以调用基类的构造函数，并传递你想要的任何参数。`super`关键字允许你在代码中访问基类。在这个任务中，你将访问基类的构造函数。

提示：`Super`指的是超类，是基类的另一种称法。

**若要在继承中使用构造函数：**

1. 创建一个名为`constructor.m`的新程序。

2. 在`constructor.m`中，输入列表 7.17 所示的代码。这段代码创建了具有名为`init`的构造函数的`Class1`，该构造函数使用了`super`关键字。

```objectivec
#import <stdio.h>
#import <Foundation/NSObject.h>

@interface TheClass : NSObject
static int count;
+(int) getCount;
@end

@implementation TheClass

-(TheClass*)init
{
    self = [super init];
    count++;
    return self;
}

+(int) getCount
{
    return count;
}
@end

int main(void)
{
    TheClass *tc1 = [TheClass new];
    printf("TheClass count is %i\n", [TheClass getCount]);

    TheClass *tc2 = [TheClass new];
    printf("TheClass count is %i\n", [TheClass getCount]);
    return 0;
}
```

列表 7.17 开始`constructor.m`。

3. 输入创建`Class1`对象的代码，它将调用构造函数（列表 7.18）。

4. 保存`constructor.m`。

5. 运行`constructor.m`程序。你应该看到：

：Class count is 1

2

```objectivec
#import <stdio.h>
#import <Foundation/NSObject.h>

@interface TheClass : NSObject
static int count;
+(int) getCount;
@end

@implementation TheClass

-(TheClass*)init
{
    self = [super init];
    count++;
    return self;
}

+(int) getCount
{
    return count;
}
@end

int main(void)
{
    TheClass *tc1 = [TheClass new];
    printf("TheClass count is %i\n", [TheClass getCount]);

    TheClass *tc2 = [TheClass new];
    printf("TheClass count is %i\n", [TheClass getCount]);
    return 0;
}
```

列表 7.18`constructor.m`程序。

## 在继承中使用多态

多态是指使用不同的对象来执行相同的代码：也就是说，当你使用多态时，执行相同代码的接收消息的对象是可以在运行时决定的。

**若要使用多态：**

1. 创建一个名为`polymorphism.m`的新程序。

2. 在`polymorphism.m`中，输入列表 7.19 所示的代码。这段代码创建了你将使用的类。

```objectivec
#import <stdio.h>
#import <Foundation/NSObject.h>

@interface Class1 : NSObject
-(void) print;
@end

@implementation Class1

-(void) print
{
    printf("This is Class 1\n");
}
@end

@interface Class2 : NSObject
-(void) print;
@end

@implementation Class2

-(void) print
{
    printf("This is Class 2\n");
}

@end
```

列表 7.19 开始`polymorphism.m`。

3. 添加代码，用一个`id`类型的变量交替加载这两个对象，并执行相同的代码（列表 7.20）。

4. 保存`polymorphism.m`。

5. 运行`polymorphism.m`程序。你应该看到：

This is Class 1.

This is Class 2.

```objectivec
#import <stdio.h>
#import <Foundation/NSObject.h>

@interface Class1 : NSObject
-(void) print;
@end

@implementation Class1

-(void) print
{
    printf("This is Class 1\n");
}
@end

@interface Class2 : NSObject
-(void) print;
@end

@implementation Class2

-(void) print
{
    printf("This is Class 2\n");
}
@end

int main(void)
{
    Class1 *c1 = [Class1 new];
    Class2 *c2 = [Class2 new];
    id pointerToObject;
    int loopIndex;
    pointerToObject = c1;
    for(loopIndex = 0; loopIndex < 2; loopIndex++){
        [pointerToObject print];
        pointerToObject = c2;
    }
    return 0;
}
```

列表 7.20`polymorphism.m`程序。

## 类别、扮演与协议

在本章中，我们将学习 Objective-C 面向对象编程的三个特性：类别（Categories）、扮演（Posing）和协议（Protocols）。类别允许你通过添加方法来扩展类——为此你不需要访问基类的代码；你可以在不修改类定义的情况下为类创建新方法。当你无法访问类的源代码、或者不想修改源码，或者想要以不同的方式自定义类时，这非常有用。扮演涉及到让一个类“扮演”另一个类。假设你有一个类`Class1`以及另一个派自它的类`Class2`。你当然可以创建`Class1`的对象。但你也可以告诉`Class2`扮演`Class1`。从此以后创建`Class1`对象时，你实际上是在创建一个`Class2`对象。

# 第 8 章：分类、布局（协议）与协议

实现相同的功能还有其他方法——例如，你可以使用多态（参见上一章）。但使用布局（posing）可能会更整洁，因为你不需要在整个代码过程中不断跟踪变量中存储的是什么种类型的指针。

协议（Protocols）非常像 Java 中所谓的接口（interfaces）。协议是一个方法的规范，就像它的原型（prototype）一样。当你指定某个类使用特定的协议时，你实际上是在表示该类实现了这些方法。换句话说，协议允许你声明方法；而在你的类中定义具体的实现则由你决定。

这是 Objective-C 最接近多重继承的地方（在多重继承中你可以从多个类继承），因为通过使用协议，你可以确保所有的派生类都实现了相同的方法（尽管每个类中的具体实现可能不同）。这非常有用，例如你有名为`Animal`和`Pet`的两个基类，并想从它们派生名为`Cat`和`Dog`的类。你可以通过协议确保`Cat`和`Dog`实现了`Animal`和`Pet`的方法。当`Cat`和`Dog`使用由`Animal`和`Pet`定义的协议时，`Cat`和`Dog`都实现了一系列方法。

### 关于分类（Categories）

分类允许你通过定义新方法来扩展一个类，即使你无法访问该类的源代码或无法修改它也可以。假设你有一个类`Class1`，它在类的头文件中有一个单一的方法`method1`：

```objc
#include <Foundation.h>
@interface Class1 : NSObject
-(return_type)method1;
@end
```

同样，假设该方法定义在类的实现文件中：

```objc
#import <stdio.h>
#include <Foundation.h>
@implementation Class1
-(return_type)method1
{

}
@end
```

如果你想通过添加一个新方法`method2`来扩展`Class1`，你可以创建一个新的头文件，像所示列出该方法：

```objc
@interface Class1 (Extender)
-(return_type)method2;
@end
```

注意类名后面括号中的术语`Extender`。你可以在这里使用任何术语来表示你正在扩展基类，并为该扩展命名。当你在自己的文件中创建`method2`的实现时，使用相同的括号内术语：

```objc
#import <stdio.h>
#include <Foundation.h>
@implementation Class1 (Extender)
-(return_type)method2
{

}
@end
```

通过这种方式，Objective-C 允许你在不修改源代码文件的情况下扩展类。

### 分类：创建基类

在此项任务中，你将创建一个基类，并在下一个任务中通过分类来扩展它。你将创建一个名为`Class1`的类，其中包含一个名为`print`的方法。以下是`print`方法的样子；它只是打印消息“This is Class 1.”。

```objc
-(void)print
{
printf("This is Class 1.\n");
}
```

创建将被扩展的基类：

- 创建名为`class1.m`的程序。
- 在`class1.m`中，输入列表 8.1 中的代码。这段代码创建了`Class1`类。
- 在`class1.m`中，添加创建`print`方法的代码（列表 8.2）。
- 保存`class1.m`。
- 创建名为`class1.h`的头文件。
- 在`class1.h`中，输入列表 8.3 所示的代码。
- 保存`class1.h`。

现在你准备好扩展该类了。



```objc
#import <stdio.h>
#include <Foundation.h>
#import "Class1.h"

@implementation Class1

@end
```

**列表 8.1 开始 `class1.m`。**

```objc
#import <stdio.h>
#include <Foundation.h>
#import "Class1.h"

@implementation Class1

-(void) print
{
    printf("This is Class 1.\n");
}

@end
```

**列表 8.2 `class1.m` 程序。**

```objc
#include <Foundation.h>

@interface Class1 : NSObject
-(void)print;
@end
```

**列表 8.3 `class1.h` 文件。**

### 分类：创建分类

在之前的任务中，你创建了带有 `print` 方法的 `Class1`。在本文的任务中，你将扩展 `Class1` 以包含一个新方法 `print2`。`print2` 方法如下：

```objc
-(void)print2
{
    printf("This is Class 1 extended.\n");
}
```

在将此方法添加到 `Class1` 之后，你将在下一个任务中调用两个方法：`method1` 和 `method2`。

为类添加分类：

- 创建一个名为 `class1ender.m` 的程序。
- 在 `class1ender.m` 中，输入列表 8.4 中的代码。这段代码表示你想要扩展 `Class1`。
- 在 `class1ender.m` 中，添加创建 `print` 方法的代码（列表 8.5）。
- 保存 `class1ender.m`。
- 创建名为 `class1ender.h` 的文件。
- 在 `class1ender.h` 中，输入列表 8.6 中的代码。
- 保存 `class1ender.h`。

```objc
#import <stdio.h>
#include <Foundation.h>
#import "Class1.h"
#import "Class1ender.h"

@implementation Class1 (Extender)

-(void)print2
{
    printf("This is Class 1 extended.\n");
}

@end
```

**列表 8.4 开始 `class1ender.m`。**

**列表 8.5 `class1ender.m` 程序。**

```objc
@interface Class1 (Extender)
-(void)print2;
@end
```

**列表 8.6 `class1ender.h`。**

### 分类：整合

在之前的两个任务中，你创建了带有 `print` 方法的 `Class1` 并扩展了它。在本次任务中，你将让 `Class1` 类及其分类协同工作。

使用分类使用基类：

- 创建名为 `main.m` 的新程序。
- 在 `main.m` 中，输入列表 8.7 所示的代码。这段代码包含了 `class1.h` 和 `class1ender.h` 头文件，以确保代码了解 `Class1` 及其分类。
- 在 `main.m` 中，添加创建 `Class1` 对象的代码（列表 8.8）。

```objc
#import <stdio.h>
#import "Class1.h"
#import "Class1ender.h"

int main(void)
{
}
```

**列表 8.7 开始 `main.m`。**

```objc
#import <stdio.h>
#import "Class1.h"
#import "Class1ender.h"

int main(void)
{
    Class1 *c1 = [Class1 new];
}
```

**列表 8.8 编辑 `main.m`。**

- 在 `main.m` 中，添加列表 8.9 所示的代码。这段代码调用了 `Class1` 类的 `print` 方法以及你扩展 `Class1` 的 `print2` 方法。
- 保存 `main.m`。
- 如果你使用的是 Linux、UNIX 或 Windows，创建一个名为 `GNUmakefile` 的新文件。
- 在 `GNUmakefile` 中，输入列表 8.10 所示的代码。
- 保存 `GNUmakefile`。
- 运行 `main.m` 分类程序。你应该能看到来自 `print` 方法和扩展的 `print2` 方法的输出：

```objc
#import <stdio.h>
#import "Class1.h"
#import "Class1ender.h"
#import "FractionMath.h"

int main(void)
{
    Class1 *c1 = [Class1 new];
    [c1 print];
    [c1 print2];
    return 0;
}
```

**列表 8.9 调用 `print` 和 `print2` 方法。**

```makefile
include $(GNUSTEP_MAKEFILES)/common.make

TOOL_NAME = categories
categories_OBJC_FILES = Class1.m Class1ender.m main.m

include $(GNUSTEP_MAKEFILES)/tool.make
```

**列表 8.10 `GNUmakefile`。**

## 类别、代充（Posing）与协议（Protocols）

### 149 关于代充（Posing）

代充允许一个类代表另一个类。假设你有一个类 `Class1`，它在类的头文件中包含一个方法 `method1`：

```objectivec
#include <Foundation/Foundation.h>

@interface Class1 : NSObject

-(return_type)*method1;

@end
```

同样假设该方法定义在类的实现文件中：

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>

@implementation Class1

-(return_type)*method1
{
    .
    .
    .
}

@end
```

现在，假设该方法在另一个类的实现文件中被重定义，且 `Class2` 是基于 `Class1` 的：

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>

@implementation Class1 : Class2

-(return_type)*method1
{
    .
    .
    .
}

@end
```

你可以在主方法中这样让 `Class2` 代充 `Class1`：

```objectivec
[Class2 poseAsClass:[Class1 class]];
```

现在，当你像这样创建一个 `Class1` 的对象时：

```objectivec
Class1 *c2 = [Class1 new];
[c2 method1];
.
.
.
```

你实际上是在创建一个 `Class2` 的对象。在这段代码中运行的方法将是 `Class2` 实现中定义的 `method1`。

这种技术可以作为处理多态的快捷方法，但当你编写 `poseAsClass` 这一行之后的代码时，你必须记住你正在让一个类代充另一个类。

### 151 代充：创建基类

当一个类代充另一个类时，它可以作为该类的替身。你告诉 Objective-C 有一个类正在代充另一个类，从那以后在你的代码中，Objective-C 将使用正在代充的类作为原始类，即使你在代码中使用原始类也是如此。

要创建一个让其他类可以代充的基类：

1. 创建一个名为 `class1.m` 的文件。
2. 在 `class1.m` 中，输入 **Listing 8.11** 中的代码。这段代码创建了 `Class1` 类。
3. 在 `class1.m` 中，添加创建打印方法的代码（**Listing 8.12**）。
4. 保存 `class1.m`。
5. 创建一个名为 `class1.h` 的文件。
6. 在 `class1.h` 中，输入 **Listing 8.13** 中的代码。
7. 保存 `class1.h`。

**Listing 8.11 开始 `class1.m`。**

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>
#import "Class1.h"

@implementation Class1

-(void) print
{
    printf("This is Class 1.\n");
}

@end
```

**Listing 8.12 `class1.m` 程序。**

```objectivec
#include <Foundation/Foundation.h>

@interface Class1 : NSObject
-(void) print;

@end
```

**Listing 8.13 `class1.h` 文件。**

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>
#import "Class1.h"

@implementation Class1
    .
    .
    .
@end
```

### 152 代充：创建派生类

一个类只有在基于它所代充的类时才能进行代充，因此在这个任务中，你将从基类 `Class1` 派出一个类。这个新类将命名为 `Class2`，它将重定义 `print` 方法以显示一条这是 `Class2` 的消息：

```objectivec
@implementation Class2

-(void) print
{
    printf("This is Class2.");
}
```

通过这种方式，当 `Class2` 代充 `Class1` 并调用 `print` 方法时，你会看到“This is Class2.”而不是“This is Class1.”

创建派生类：

1. 创建一个名为 `class2.m` 的文件。
2. 在 `class2.m` 中，输入 **Listing 8.14** 中的代码。这段代码创建了 `Class2` 类。
3. 在 `class2.m` 中，添加创建 `print` 方法的代码（**Listing 8.15**）。
4. 保存 `class2.m`。
5. 创建一个名为 `class2.h` 的头文件。
6. 在 `class2.h` 中，输入 **Listing 8.16** 中的代码。
7. 保存 `class2.h`。

**Listing 8.14 开始 `class2.m`。**

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>
#import "Class1.h"
#import "Class2.h"

@implementation Class2

-(void) print
{
    printf("This is Class2.");
}

@end
```

**Listing 8.15 `class1.m` 程序。**

```objectivec
#include <Foundation/Foundation.h>

@import "Class1.h"

@interface Class2 : Class1
-(void) print;

@end
```

**Listing 8.16 `class2.h` 文件。**

### 153 代充：结合

要实现代充，你使用 `poseAsClass` 关键字。在示例中，为了让 `Class2` 代充 `Class1`，你可以使用这一行：

```objectivec
[Class2 poseAsClass:[Class1 class]];
```

从那时起，当你创建一个 `Class1` 对象时，你实际上是在创建一个 `Class2` 对象，正如任务中所所示。

让一个类代充另一个类：

1. 创建一个名为 `main.m` 的新程序。
2. 在 `main.m` 中，输入 **Listing 8.17** 所示的代码。这段代码创建了 `Class1` 对象并调用其 `print` 方法。
3. 在 `main.m` 中添加让 `Class2` 代充 `Class1` 的代码，创建一个 `Class1` 对象并调用其 `print` 方法（**Listing 8.18**）。这次调用的实际上 `Class2` 的 `print` 方法。

**Listing 8.17 开始 `main.m`。**

```objectivec
#import <stdio.h>
#import "Class1.h"
#import "Class2.h"

int main(void) {
    Class1 *c = [Class1 new];
    [c print];
    .
    .
    .
}
```

**Listing 8.18 `main.m` 程序。**

```objectivec
#import <stdio.h>
#import "Class1.h"
#import "Class2.h"

int main(void) {
    Class1 *c = [Class1 new];
    [c print];
    [Class2 poseAsClass:[Class1 class]];
    Class1 *c2 = [Class1 new];
    [c2 print];
    return 0;
}
```

4. 保存 `main.m`。
5. 如果你使用的是 Linux、UNIX 或 Windows，创建一个如 **Listing 8.19** 所示的 `GNUmakefile`。
6. 运行 `main.m` 程序。你应该看到：

This is Class 1.

This is Class 2.

**Listing 8.19 `GNUmakefile`**

```make
OBJS=main.o Class1.o Class2.o
TARGET=posing

$(TARGET): $(OBJS)
	clang -o $(TARGET) $(OBJS)
```

### 155 关于协议（Protocols）

协议允许你为可以在多个类使用的方法指定接口。例如，如果你有一个名为 `print` 的方法并想为它创建一个协议，你可以在文件中文件中，例如 `printing.h`：

```objectivec
@protocol Printing

-(void) print;

@end
```

然后你可以在其他类的接口中包含 `printing.h`。这样做会将 `print` 添加到这些类的接口中：

```objectivec
#include <Foundation/Foundation.h>
#import "printing.h"

@interface Class1 : NSObject
-(void) print;

@end
```

你还可以在另一个类 `Class2` 中包含 `printing.h`：

```objectivec
#import "Class1.h"
#import "printing.h"

@interface Class2 : Class1
-(void) print;

@end
```

现在，你可以为 `Class1` 以一种方式实现 `print`：

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>
#import "Class1.h"

@implementation Class1

-(void) print
{
    printf("This is Class 1.\n");
}

@end
```

你还可以为 `Class2` 以另一种方式实现 `print`：

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>
#import "Class1.h"
#import "Class2.h"

@implementation Class2

-(void) print
{
    printf("This is Class 2.\n");
}

@end
```

然后你可以像这样创建 `Class1` 和 `Class2` 的对象并调用它们的每个 `print` 方法：

## 分类、位置声明与协议

157

### 协议：定义协议/接口

### 协议与接口

当你为一个或多个方法定义一个协议时，你通常会将该协议存储在头文件中。你将在名为 `printing.h` 的文件中为名为 `print` 的方法创建一个名为 `Printing` 的协议：

```objectivec
@protocol Printing

-(void)print;

@end
```

然后，你将在名为 `ClassFirst.h` 的接口文件中为一个类使用该协议：

```objectivec
#include <Foundation/Foundation.h>
#import "printing.h"

@interface Class1 : NSObject
-(void)print;
@end
```

你还会在名为 `ClassSecond.h` 的接口文件中使用 `Printing` 协议，该类派自上述第一个类：

```objectivec
#include "Class1.h"
#import "printing.h"

@interface Class2 : Class1
@end
```



然后，你将在不同的地方（在下一个任务中）为`Class1`和`Class2`实现`print`方法。

## 第 8 章

### 协议：定义协议/接口

**定义协议和接口：**

1. 创建一个名为`printing.h`的新文件。
2. 在`printing.h`中，输入**列表 8.20** 所示的代码。这段代码为`print`方法创建了协议。
3. 保存`printing.h`。
4. 创建一个名为`ClassFirst.h`的新文件。
5. 在`ClassFirst.h`中，输入创建第一个类接口的代码，该接口使用了我们定义的这个协议（**列表 8.21**）。
6. 保存`ClassFirst.h`。
7. 创建一个名为`ClassSecond.h`的新文件。
8. 在`ClassSecond.h`中，存储用于设置第二个类接口的代码，该类派自第一个类，并且同样使用了`print`方法的新协议（**列表 8.22**）。
9. 保存`ClassSecond.h`。

```objectivec
@protocol Printing
-(void)print;
@end
```

**列表 8.20** `printing.h`文件。

```objectivec
#include <Foundation/Foundation.h>
#import "printing.h"

@interface Class1 : NSObject
-(void)print;
@end
```

**列表 8.21** `ClassFirst.h`文件。

```objectivec
#include "Class1.h"
#import "printing.h"

@interface Class2 : Class1
@end
```

**列表 8.22** `ClassSecond.h`文件。

### 协议：创建类实现

现在你已经定义了协议，并在两个类的接口中使用了它，你需要定义协议中方法的实现，在这里方法命名为`print`。

**使用协议定义实现：**

1. 创建一个名为`ClassFirst.m`的新程序。
2. 在`ClassFirst.m`中，输入**列表 8.23** 所示的代码。这段代码创建了`Class1`的实现。
3. 添加创建`print`方法实现的代码（**列表 8.24**）。
4. 保存`ClassFirst.m`。
5. 创建一个名为`ClassSecond.m`的新程序。

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>
#import "Class1.h"

@implementation Class1

@end
```

**列表 8.23** 开始`ClassFirst.m`。

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>
#import "Class1.h"

@implementation Class1
-(void)print {
    printf("This is Class 1\n");
}
@end
```

**列表 8.24** `ClassFirst.m`程序。

6. 在`ClassSecond.m`中，输入**列表 8.25** 所示的代码。这段代码创建了`Class2`的实现。
7. 在`ClassSecond.m`中，添加创建`Class2`中`print`方法实现的代码（**列表 8.26**）。
8. 保存`ClassSecond.m`。

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>
#import "Class1.h"
#import "Class2.h"

@implementation Class2

@end
```

**列表 8.25** 开始`ClassSecond.m`。

```objectivec
#import <stdio.h>
#include <Foundation/Foundation.h>
#import "Class1.h"
#import "Class2.h"

@implementation Class2
-(void)print {
    printf("This is Class 2\n");
}
@end
```

**列表 8.26** `ClassSecond.m`程序。

### 协议：整合在一起

现在你已经为`print`方法定义了协议并在两个类中实现了该方法，你可以创建这些类的对象并调用每个类中的`print`方法：

```objc
int main(void) {
    Class1 *c = [Class1 new];
    [c print];
    Class2 *c2 = [Class2 new];
    [c2 print];
    return 0;
}
```

每个方法将打印不同的内容，因此虽然协议定义了一个方法的接口，但实际实现取决于使用该方法的类。

**使用协议：**

1. 创建一个名为`main.m`的新程序。
2. 在`main.m`中，输入**列表 8.27** 所示的代码。这段代码创建了第一个类的对象。
3. 添加创建第二个类对象的代码（**列表 8.28**）。
4. 保存`main.m`。
5. 如果你使用的是 Linux、UNIX 或 Windows，创建一个名为`makefile`的文件。
6. 运行`main.m`程序。

```objc
#import <stdio.h>
#import "Class1.h"

int main(void) {
    Class1 *c = [Class1 new];
    [c print];
    return 0;
}
```

**列表 8.27** 开始`main.m`。

```objc
#import <stdio.h>
#import "Class1.h"
#import "Class2.h"

int main(void) {
    Class1 *c = [Class1 new];
    [c print];
    Class2 *c2 = [Class2 new];
    [c2 print];
    return 0;
}
```

**列表 8.28** `main.m`程序。

```makefile
TOOL_NAME=main
OBJC_FILES=Class1.m ClassSecond.m main.m

$(TOOL_NAME): $(OBJC_FILES)
	$(CC) $(CFLAGS) -o $(TOOL_NAME) $(OBJC_FILES)
```

**列表 8.29** GNUmakefile

## 第 9 章

### 数组与字典

在本章，我们将探索 Objective-C 的两个重要特性：数组和字典。你在第 3 章学过 C 语言数组。这些数组允许你通过索引处理数据。例如，这里是如何创建一个标准数组并显示关于它的信息：

```c
#include <stdio.h>
int main(void) {
    int scores[5] = {92, 73, 57, 98, 89};
    printf("The array is %i elements long.", sizeof(scores) / sizeof(int));
    return 0;
}
```

在本章中，你将使用带有的 Foundation 类来构建数组。你也可以使用 Foundation 类创建字典。Objective-C 中的字典就像数组，但它使用单词作为索引值，而不是数值。因此，虽然数组可以使用 0, 1, 2, 3 等数字进行索引，但字典同样可以使用“banana”、“apple”和“orange”。

此外，你还可以创建可变数组和字典：即可以在代码运行时更改其长度的数组和字典。你将在看到它们是如何工作的。这些以及更多内容在本章介绍，包括：`NSArray`、`NSMutableArray`、`NSMutableDictionary`和`NSDictionary`类，以及其他一些类。

### 使用数组和字典

### 创建数组

你可以使用 Foundation 的`NSArray`类来创建一个数组。此类数组是静态的，在运行时无法更改。

以下是创建这样一个数组的方法，并将其初始化为“red”（红色）、“white”（白色）和“blue”（蓝色）。

```objective-c
#import <Foundation/Foundation.h>

int main()
{
    NSArray *array = [[NSArray alloc] initWithObjects:@"red", @"white", @"blue", nil];
}
```

**创建一个静态数组：**

1. 创建一个名为`createarray.m`的程序。
2. 在`createarray.m`中，输入**列表 9.1** 所示的代码。这段代码创建了数组并用数据对其初始化。
3. 添加代码以显示表示成功的消息（**列表 9.2**）。
4. 这里的`createarray.m`。
5. 运行`createarray.m`程序（忽略关于未使用数组变量的警告）。

你应该能看到以下内容：

`Array has been created.`

**提示**

- 所有的数组都以`nil`对象结尾是一个好习惯，并且正如之前讨论过的，务必使用 @ 符号来区分 Objective-C 字符串和 C 风格字符串。
- 如果你使用的是 Linux、UNIX 或 Windows，则需要一个前面的章节详细介绍的 GNUmakefile 文件。

```objective-c
#import <Foundation/Foundation.h>

int main()
{
    NSArray *array = [[NSArray alloc] initWithObjects:@"red", @"white", @"blue", nil];
}
```

**列表 9.1** 开始`createarray.m`。

```objective-c
#import <Foundation/Foundation.h>

int main()
{
    NSArray *array = [[NSArray alloc] initWithObjects:@"red", @"white", @"blue", nil];
    printf("Array has been created.");
    return 0;
}
```

**列表 9.2** `createarray.m`程序。

### 访问数组元素

你已经在上一个任务中创建了一个数组。现在，你如何访问该数组中的单个元素呢？例如，如果你想访问`array[0]`处的元素怎么办？

要做到这一点，你向数组发送`objectAtIndex`消息，并带上你想要访问的索引值：

```objective-c
#import <Foundation/Foundation.h>

int main()
{
    NSArray *array = [[NSArray alloc] initWithObjects:@"red", @"white", @"blue", nil];
    printf("array[0] = %s", [array objectAtIndex:0] cString);
}
```

在这个任务中，你将看到如何使用`objectAtIndex`消息访问单个元素。

**访问单个元素：**

1. 创建一个名为`accesselements.m`的程序。
2. 在`accesslements.m`中，输入**列表 9.3** 所示的代码。这段代码创建了数组并用数据对其初始化。
3. 添加代码通过`objectAtIndex`访问你选择的元素，并在将其传递给`printf()`函数之前将 Objective-C 字符串转换为 C 风格字符串（**列表 9.4**）。
4. 保存`accesslements.m`。
5. 运行`accesslements.m`程序。你应该能看到以下内容：

`array[0]=red`

```objective-c
#import <Foundation/Foundation.h>

int main()
{
    NSArray *array = [[NSArray alloc] initWithObjects:@"red", @"white", @"blue", nil];
    return 0;
}
```

**列表 9.3** 开始`accesslements.m`。

```objective-c
#import <Foundation/Foundation.h>

int main()
{
    NSArray *array = [[NSArray alloc] initWithObjects:@"red", @"white", @"blue", nil];
    printf("array[0] = %s", [array objectAtIndex:0] cString);
    return 0;
}
```

**列表 9.4** `accesslements.m`程序。

**提示**

- 要向数组中插入对象，你可以使用`insertObjectAtIndex`消息。

### 使用枚举遍历数组

Objective-C 提供了一种简单的方法来遍历数组：你可以使用一个`NSEnumerator`对象。以下是为数组创建枚举器的方法：

```objective-c
NSArray *array = [[NSArray alloc] initWithObjects:@"red", @"white", @"blue", nil];
NSEnumerator *enumerator = [array objectEnumerator];
```

然后，你可以使用枚举器的`nextObject`消息，在循环遍历数组时获取下一个元素。

**使用枚举遍历数组：**

1. 创建一个名为`enumerator.m`的新程序。
2. 在`enumerator.m`中，输入**列表 9.5** 所示的代码。这段代码创建了数组、数组的枚举器以及一个用于数组对象的占位变量。

```objective-c
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(int argc, const char *argv[])
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSArray *array = [[NSArray alloc] initWithObjects:@"red", @"white", @"blue", nil];
    NSEnumerator *enumerator = [array objectEnumerator];
    id obj;
    // ...
}
```

**列表 9.5** 开始`enumerator.m`。

3. 在`enumerator.m`中，输入**列表 9.6** 所示的代码。这段代码使用`nextObject`消息在 while 循环从枚举器中获取下一个对象。我们还创建一个`NSAutoreleasePool`对象来跟踪内存。
4. 保存`enumerator.m`。
5. 如果你使用的是 Linux、UNIX 或 Windows，创建一个名为`GNUmakefile`的文件。
6. 运行`enumerator.m`程序。你应该看到以下内容：

`red`

`white`

`blue`

```objective-c
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(int argc, const char *argv[])
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSArray *array = [[NSArray alloc] initWithObjects:@"red", @"white", @"blue", nil];
    NSEnumerator *enumerator = [array objectEnumerator];
    id obj;
    while ((obj = [enumerator nextObject])) {
        printf("%s", [obj] cString);
    }
    [pool release];
    return 0;
}
```

**列表 9.6** 编辑`enumerator.m`。

**提示**

- 如果你想用`for`循环遍历数组，可以向数组发送`count`获取数组中的元素数量。

### 创建可变数组

使用`NSArray`创建的数组是固定数组——你无法在运行时更改它们的长度。然而，使用`NSMutableArray`类创建的数组长度在程序运行时是可以更改的。

在下一个任务中，你将使用`NSMutableArray`向数组添加元素。

**创建一个可变数组：**

1. 创建一个名为`createmutablearray.m`的新程序。
2. 在`createmutablearray.m`中，输入**列表 9.7** 所示的代码。这段代码创建了可变数组。



```objective-c
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(int argc, const char *argv[])
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSMutableArray *array = [[NSMutableArray alloc] initWithObjects:@"red", @"white", @"blue", nil];
    NSEnumerator *enumerator = [array objectEnumerator];
    id obj;
    // ...
}
```

**列表 9.7** 开始 `createmutablearray.m`。

3. 在 `createmutablearray.m` 中，输入**列表 9.8** 所示的代码。这段代码使用枚举器和 `nextObject` 消息在 `while` 循环从枚举器中获取下一个对象。

4. 保存 `createmutablearray.m`。

5. 如果你使用的是 Linux、UNIX 或 Windows，创建一个名为 `GNUmakefile` 的文件。

6. 运行 `createmutablearray.m` 程序。你应该能看到以下内容：

`red`

`white`

`blue`

```objective-c
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(int argc, const char *argv[])
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSMutableArray *array = [[NSMutableArray alloc] initWithObjects:@"red", @"white", @"blue", nil];
    NSEnumerator *enumerator = [array objectEnumerator];
    id obj;
    while ((obj = [enumerator nextObject])) {
        printf("%s\n", [obj description] cString);
    }
    [pool release];
    return 0;
}
```

**列表 9.8** 编辑 `createmutablearray.m`。

## 使用数组和字典

### 向可变数组中添加元素

在运行时向可变数组添加新元素非常简单：你只需要发送 `addObject` 消息。

**向可变数组添加元素：**

1. 创建一个名为 `addelements.m` 的文件。

2. 在 `addelements.m` 中，输入**列表 9.9** 所示的代码。这段代码创建了你将使用的可变数组，并将其初始化为“red”、“white”和“blue”。

```objc
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(int argc, const char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSMutableArray *array = [[NSMutableArray alloc] initWithWithObjects:@"red", @"white", @"blue", nil];
}
```

**列表 9.9** 开始 `addelements.m`。

3. 输入添加“orange”、“green”和“azure”元素的代码，然后遍历数组以打印所有元素的列表（**列表 9.10**）。

4. 保存 `addelements.m`。

5. 运行 `addelements.m` 程序。你应该看到以下内容：

`red`

`white`

`blue`

`orange`

`green`

`azure`

```objc
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(int argc, const char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSMutableArray *array = [[NSMutableArray alloc] initWithWithObjects:@"red", @"white", @"blue", nil];
    NSEnumerator *enumerator = [array objectEnumerator];
    id obj;
    [array addObject:@"orange"];
    [array addObject:@"green"];
    [array addObject:@"azure"];
    while ((obj = [enumerator nextObject])) {
        printf("%s\n", [[obj description] cString]);
    }
    [pool release];
    return 0;
}
```

**列表 9.10** `addelements.m` 程序。

### 数组排序

你可以通过向数组发送 `sortUsingSelector` 消息来对其进行排序。例如，这里是如何使用 `caseInsensitiveCompare` 选择器执行不区分大小写的排序：

```objc
[array sortUsingSelector:@selector(caseInsensitiveCompare:)];
```

**对数组排序：**

1. 创建一个名为 `sortarray.m` 的文件。

2. 在 `sortarray.m` 中，输入**列表 9.11** 中的代码。这段代码创建并打印了数组。

```objc
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(int argc, const char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSMutableArray *array = [[NSMutableArray alloc] initWithWithObjects:@"red", @"white", @"blue", nil];
    NSEnumerator *enumerator = [array objectEnumerator];
    id obj;
    [array addObject:@"orange"];
    [array addObject:@"green"];
    [array addObject:@"azure"];
    while ((obj = [enumerator nextObject])) {
        printf("%s\n", [obj description] cString);
    }
}
```

**列表 9.11** 开始 `sortarray.m`。

3. 添加排序数组的代码并打印它（**列表 9.12**）。

4. 保存 `sortarray.m`。

5. 运行 `sortarray.m` 程序。你应该看到未排序的数组，紧接着是这些：

`Sorting the array.`

`azure`

`blue`

`green`

`orange`

`red`

`white`

```objc
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(int argc, const char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSMutableArray *array = [[NSMutableArray alloc] initWithWithObjects:@"red", @"white", @"blue", nil];
    NSEnumerator *enumerator = [array objectEnumerator];
    id obj;
    [array addObject:@"orange"];
    [array addObject:@"green"];
    [array addObject:@"azure"];
    while ((obj = [enumerator nextObject])) {
        printf("%s\n", [[obj description] cString]);
    }
}
```

**列表 9.12** `sortarray.m` 程序。

### 释放内存

数组占用的内存可能是大量的。你可以通过向数组发送 `release` 消息来释放这些内存。

**释放数组内存：**

1. 将 `sortarray.m` 复制为名为 `releasemory.m` 的程序。

2. 在 `releasemory.m` 中，添加**列表 9.13** 中的代码。

3. 保存 `releasemory.m`。

4. 运行 `releasemory.m` 程序。你应该看到以下内容：

`red`

`white`

`blue`

`orange`

`green`

`azure`

`Sorting the array.`

`azure`

`blue`

`green`

`orange`

`red`

`white`

`Freeing memory.`

```objc
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(int argc, const char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSMutableArray *array = [[NSMutableArray alloc] initWithWithObjects:@"red", @"white", @"blue", nil];
    NSEnumerator *enumerator = [array objectEnumerator];
    id obj;
    while ((obj = [enumerator nextObject])) {
        printf("%s\n", [[obj description] cString]);
    }
    printf("Sorting the array.\n");
    [array sortUsingSelector:@selector(caseInsensitiveCompare:)];
    NSEnumerator *enumerator = [array objectEnumerator];
    while ((obj = [enumerator nextObject])) {
        printf("%s\n", [[obj description] cString]);
    }
    printf("Freeing memory.\n");
    [array release];
    [pool release];
    return 0;
}
```

**列表 9.13** `releasemory.m` 程序。

### 创建字典

字典允许你使用单词或其他对象作为键，并通过键检索或存储对象。在这个任务中，你创建一个字典来观察它是如何工作的。

**创建字典：**

1. 创建一个名为 `createdictionary.m` 的文件。

2. 在 `createdictionary.m` 中，输入**列表 9.14** 所示的代码。这段代码创建了字典并为其添加了键值对。

```objc
#import <Foundation/Foundation.h>
#import <stdio.h>

int main() {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSDictionary *dictionary = [[NSDictionary alloc] initWithWithObjectsAndKeys:
        @"banana", @"fruit",
        @"onion", @"vegetable",
        @"turkey", @"meat",
        nil];
}
```

**列表 9.14** 开始 `createdictionary.m`。

3. 添加显示特定键的值的代码（**列表 9.15**）。

4. 保存 `createdictionary.m`。

5. 运行 `createdictionary.m` 程序。你应该看到未排序的数组，紧接着是这些：

`Entry for fruit:banana`

```objc
#import <Foundation/Foundation.h>
#import <stdio.h>

int main() {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSDictionary *dictionary = [[NSDictionary alloc] initWithWithObjectsAndKeys:
        @"banana", @"fruit",
        @"onion", @"vegetable",
        @"turkey", @"meat",
        nil];
    printf("Entry for fruit: %s\n", [[dictionary objectForKey:@"fruit"] cString]);
    [dictionary release];
    [pool release];
    return 0;
}
```

**列表 9.15** `createdictionary.m` 程序。

## 第 9 章：枚举字典

你可以使用枚举器对象来遍历字典，就像使用枚举器遍历数组一样。在本次任务中，你将使用枚举器来打印字典的键和值。

**枚举字典的步骤：**

1. 创建一个名为 `enumeratordictionary.m` 的新程序。

2. 在 `enumeratordictionary.m` 中，输入**列表 9.16** 所示的代码。这段代码创建了你将使用的字典。

```objective-c
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(void)
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSDictionary *dictionary = [[NSDictionary alloc]
    initWithWithObjects:
        @"banana", @"fruit",
        @"onion", @"vegetable",
        @"turkey", @"meat",
        nil];
```

**列表 9.16** 开始编写 `enumeratordictionary.m`。

3. 添加创建枚举器并遍历字典的代码（**列表 9.17**）。

4. 保存 `enumeratordictionary.m`。

5. 运行 `enumeratordictionary.m` 程序。你应该看到以下内容：

`vegetable => onion`

`meat => turkey`

`fruit => banana`

```objective-c
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(void)
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSDictionary *dictionary = [[NSDictionary alloc]
    initWithWithObjects:
        @"banana", @"fruit",
        @"onion", @"vegetable",
        @"turkey", @"meat",
        nil];

    NSEnumerator *enumerator = [dictionary keyEnumerator];
    id key;
    while ((key = [enumerator nextObject]))
    {
        printf("%s => %s\n",
               [[key description] cString],
               [[[dictionary objectForKey: key] description] cString]);
    }
    [dictionary release];
    [pool release];
    return 0;
}
```

**列表 9.17** `enumeratordictionary.m` 程序。

### 创建可变字典

你可以通过添加项来扩展可变字典，或通过移除项来缩小它。在本次任务中，你将学习如何创建一个可变字典，并在下一个任务中将学习如何扩展它。

**创建可变字典的步骤：**



1. 创建一个名为`mutabledictionary.m`的新程序。

2. 在`mutabledictionary.m`中，输入**列表 9.18**所示的代码。这段代码创建了`NSMutableDictionary`类的一个对象。

3. 添加用于显示创建顺利的消息的代码，并在程序结束前释放可变字典所占用的内存（**列表 9.19**）。

4. 保存`mutabledictionary.m`。

5. 运行`mutabledictionary.m`程序。你应该看到：`Created dictionary.`。

```objective-c
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(void)
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSMutableDictionary *dictionary = [[NSMutableDictionary alloc] init];
    printf("Created dictionary.\n");
    [dictionary release];
    [pool release];
    return 0;
}
```

**列表 9.18** 开始编写`mutabledictionary.m`。

### 向可变字典添加对象

在上一个任务中，你创建了一个可变字典但没有向其中添加任何数据。在本次任务中，你将向可变字典添加键和值。

**向可变字典添加对象的步骤：**

1. 创建一个名为`addkeys.m`的新程序。

2. 在`addkeys.m`中，输入**列表 9.20**所示的代码。这段代码创建了可变字典，并使用`addObject`消息向字典添加键值对。

3. 添加打印可变字典内容的代码（**列表 9.21**）。

4. 保存`addkeys.m`。

5. 运行`addkeys.m`程序。你应该看到以下内容：

```
vegetable => onion

meat => turkey

fruit => banana
```

```objective-c
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(void)
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSMutableDictionary *dictionary = [[NSMutableDictionary alloc] init];
    [dictionary setObject:@"banana" forKey:@"fruit"];
    [dictionary setObject:@"onion" forKey:@"vegetable"];
    [dictionary setObject:@"turkey" forKey:@"meat"];

    NSEnumerator *enumerator = [dictionary keyEnumerator];
    id key;
    while ((key = [enumerator nextObject]))
    {
        printf("%s => %s\n",
               [[key description] cString],
               [[[dictionary objectForKey: key] description] cString]);
    }
    [dictionary release];
    [pool release];
    return 0;
}
```

**列表 9.21** `addkeys.m`程序。

# 第 10 章

## Objective-C 中的内存管理

在本章中，你将学习 Objective-C 中的内存管理。Objective-C 通过引用计数（retain count）来跟踪你创建的所有对象，当该计数降为零时，Objective-C 会自动释放分配给对象的内存。

例如，假设你创建了两个对象：

```objective-c
Class1 *object1 = [[Class1 alloc] init];
Class1 *object2 = [[Class1 alloc] init];
```

现在每个对象的引用计数均为 1，你可以通过询问每个对象的引用计数并打印结果来验证：

```objective-c
printf("object1 retain count: %i\n", [object1 retainCount]);
printf("object2 retain count: %i\n", [object2 retainCount]);
```

你也可以手动增加引用计数，如下：

```objective-c
[object1 retain];
[object1 retain];
[object2 retain];
```

当你向对象传递`retain`消息时，它会增加自己的引用计数。在这种情况下，`object1`的引用计数将从 1 增加到 2 再到 3，`object2`的将从 1 增加到 2。要减少引用计数，你需要发送`release`消息：

```objective-c
[object1 release];
[object2 release];
```

这两行将`object1`的引用计数减为 2，`object2`减为 1。当你发送`release`消息到零时，Objective-C 会自动释放该对象。你将自己实现`dealloc`方法。

```objective-c
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(void)
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSMutableDictionary *dictionary = [[NSMutableDictionary alloc] init];
    printf("Created dictionary.\n");
    [dictionary release];
    [pool release];
    return 0;
}
```

**列表 10.2** `createobject.m`程序。

# 第 10 章

## 显示引用计数（Retain Count）

当你创建对象时，Objective-C 使用引用计数（retain count）来跟踪它们。要查找该引用计数，你可以向对象发送一个`retainCount`消息。

例如，在上一个任务中，你创建了两个新对象：

```objectivec
Class1 *object1 = [[Class1 alloc] init];
Class1 *object2 = [[Class1 alloc] init];
```

你可以像下面一样显示它们的引用计数（结果为 1）：

```objectivec
printf("object1 retain count: %i\n", [object1 retainCount]);
printf("object2 retain count: %i\n", [object2 retainCount]);
```

**显示引用计数：**

1. 创建一个名为`retaincount.m`的程序。

2. 在`retaincount.m`中，输入**列表 10.3**所示的代码。这段代码创建了两个测试对象。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

@interface Class1: NSObject
@end

@implementation Class1

@end

int main(void)
{
    Class1 *object1 = [[Class1 alloc] init];
    Class1 *object2 = [[Class1 alloc] init];
    return 0;
}
```

**列表 10.3** 开始编写`retaincount.m`。

3. 添加代码来显示每个新对象的引用计数（**列表 10.4**）。

4. 保存`retaincount.m`。

5. 运行`retaincount.m`程序。你应该应该看到以下内容：

```
object1 retain count: 1
object2 retain count: 1
```

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

@interface Class1: NSObject
@end

@implementation Class1

@end

int main(void)
{
    Class1 *object1 = [[Class1 alloc] init];
    Class1 *object2 = [[Class1 alloc] init];
    printf("object1 retain count: %i\n", [object1 retainCount]);
    printf("object2 retain count: %i\n", [object2 retainCount]);
    return 0;
}
```

**列表 10.4** `retaincount.m`程序。

## 增加对象的引用计数

你可以通过向对象发送`retain`消息来手动增加其引用计数。在这个任务中，你将增加两个对象的引用计数，然后验证这些引用计数确实已经增加。

**增加引用计数：**

1. 创建一个名为`incrementcount.m`的新程序。

2. 在`incrementcount.m`中，输入**列表 10.5**所示的代码。这段代码创建了两个测试对象并显示它们的引用计数。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

@interface Class1: NSObject
@end

@implementation Class1

@end

int main(void)
{
    Class1 *object1 = [[Class1 alloc] init];
    Class1 *object2 = [[Class1 alloc] init];
    printf("object1 retain count: %i\n", [object1 retainCount]);
    printf("object2 retain count: %i\n", [object2 retainCount]);
    return 0;
}
```

**列表 10.5** 开始编写`incrementcount.m`。

3. 添加代码增加引用计数并显示结果（**列表 10.6**）。

4. 保存`incrementcount.m`。

5. 运行`incrementcount.m`程序。你应该应该看到以下内容：

```
object1 retain count: 1
object2 retain count: 1
object1 retain count: 3
object2 retain count: 2
```

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

@interface Class1: NSObject
@end

@implementation Class1

@end

int main(void)
{
    Class1 *object1 = [[Class1 alloc] init];
    Class1 *object2 = [[Class1 alloc] init];
    printf("object1 retain count: %i\n", [object1 retainCount]);
    printf("object2 retain count: %i\n", [object2 retainCount]);
    [object1 retain];
    [object1 retain];
    [object2 retain];
    printf("object1 retain count: %i\n", [object1 retainCount]);
    printf("object2 retain count: %i\n", [object2 retainCount]);
    return 0;
}
```

**列表 10.6** `incrementcount.m`程序。

## 减少对象的引用计数

你可以通过向对象发送`release`消息来减少其引用计数。你在这里执行此操作并确认引用计数已经减少。

**减少引用计数：**

1. 创建一个名为`decrementcount.m`的新程序。

2. 在`decrementcount.m`中，输入**列表 10.7**所示的代码。这段代码创建了两个测试对象并增加了它们的引用计数。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

@interface Class1: NSObject
@end

@implementation Class1

@end

int main(void)
{
    Class1 *object1 = [[Class1 alloc] init];
    Class1 *object2 = [[Class1 alloc] init];
    printf("object1 retain count: %i\n", [object1 retainCount]);
    printf("object2 retain count: %i\n", [object2 retainCount]);
    [object1 retain];
    [object1 retain];
    [object2 retain];
    printf("object1 retain count: %i\n", [object1 retainCount]);
    printf("object2 retain count: %i\n", [object2 retainCount]);
}
```

**列表 10.7** 开始编写`decrementcount.m`。

3. 添加代码将每个对象的引用计数减少 1，并显示每个对象的最终引用计数（**列表 10.8**）。

4. 保存`decrementcount.m`。

5. 运行`decrementcount.m`程序。你应该应该看到以下内容：

```
object1 retain count: 1
object2 retain count: 1
object1 retain count: 3
object2 retain count: 2
object1 retain count: 2
object2 retain count: 1
```

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

@interface Class1: NSObject
@end

@implementation Class1

@end

int main(void)
{
    Class1 *object1 = [[Class1 alloc] init];
    Class1 *object2 = [[Class1 alloc] init];
    printf("object1 retain count: %i\n", [object1 retainCount]);
    printf("object2 retain count: %i\n", [object2 retainCount]);
    [object1 retain];
    [object1 retain];
    [object2 retain];
    printf("object1 retain count: %i\n", [object1 retainCount]);
    printf("object2 retain count: %i\n", [object2 retainCount]);
    [object1 release];
    [object2 release];
    printf("object1 retain count: %i\n", [object1 retainCount]);
    printf("object2 retain count: %i\n", [object2 retainCount]);
    [object1 release];
    [object1 release];
    printf("object1 retain count: %i\n", [object1 retainCount]);
    printf("object2 retain count: %i\n", [object2 retainCount]);
    return 0;
}
```

**列表 10.8** 修改`decrementcount.m`。

## 从内存中释放对象

当对象的引用计数变为 0 时，Objective-C 会从内存中释放该对象。你可以通过重写对象的`dealloc`方法并显示消息来观察它是如何工作的。

**释放对象：**

1. 创建一个名为`dealloc.m`的程序。

2. 在`dealloc.m`中，输入**列表 10.9**所示的代码。这段代码重写了`dealloc`方法以便在对象释放时显示消息。



```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

@interface Class1: NSObject
-(void)dealloc;
@end

@implementation Class1

-(void)dealloc
{
    printf("Deallocating the object\n");
    [super dealloc];
}

@end
```

**列表 10.9** 开始编写 `dealloc.m`。

3. 添加**列表 10.10** 所示的代码。这段代码创建了两个 `Class1` 对象并将引用计数减少到零。此时，Objective-C 会释放对象，你可以通过来自重写的 `dealloc` 方法的消息来确认这一点。

4. 保存 `dealloc.m`。

5. 运行 `dealloc.m` 程序。你应该看到以下内容：

```
object1 retain count: 1
object2 retain count: 1
object1 retain count: 3
object2 retain count: 2
object1 retain count: 2
object2 retain count: 1
Deallocating the object
Deallocating the object
```

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

@interface Class1: NSObject
-(void)dealloc;
@end

@implementation Class1

-(void)dealloc
{
    printf("Deallocating the object\n");
    [super dealloc];
}

@end

int main(void)
{
    Class1 *object1 = [[Class1 alloc] init];
    Class1 *object2 = [[Class1 alloc] init];
    printf("object1 retain count: %i\n", [object1 retainCount]);
    printf("object2 retain count: %i\n", [object2 retainCount]);
    [object1 retain];
    [object1 retain];
    [object2 retain];
    printf("object1 retain count: %i\n", [object1 retainCount]);
    printf("object2 retain count: %i\n", [object2 retainCount]);
    [object1 release];
    [object2 release];
    printf("object1 retain count: %i\n", [object1 retainCount]);
    printf("object2 retain count: %i\n", [object2 retainCount]);
    [object1 release];
    [object1 release];
    [object2 release];
    return 0;
}
```

**列表 10.10** 修改 `dealloc.m`。

# 第 10 章

## 使用自动释放池 (Autorelease Pool)

如果你使用 `alloc` 或 `new` 来创建对象，你就负责自己管理该对象的内存（如果内存是一个问题的话）。但对于那些不是通过 `alloc` 或 `new` 创建的对象，你可以使用自动释放池让 Objective-C 为你管理它们。

只需要创建一个池对象，对象就会被自动放入其中。在程序结束时，你只需要释放（release）该池即可释放所有对象。

### 如何使用自动释放池：

1. 创建一个名为 `pool.m` 的文件。

2. 在 `pool.m` 中，输入如**列表 10.11** 所示的代码。这段代码创建了池以及一个由池管理的对象：`string1`。

3. 添加代码来打印对象的引用计数（retain count），并在程序结束时释放池（**列表 10.12**）。

4. 保存 `pool.m`。

5. 运行 `pool.m` 程序。你应该会看到以下内容：

`Pool-managed string’s retain count: 1`

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(void)
{
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc];
    NSString *string1 = [NSString stringWith:@"Pool-managed string"];
}
```

**列表 10.11** `pool.m`。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(void)
{
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc];
    NSString *string1 = [NSString stringWith:@"Pool-managed string"];
    printf("%s’s retain count: %x\n", [string1 cString], [string1 retainCount]);
    [pool release];
    return 0;
}
```

**列表 10.12** `pool.m`。

## 在 Objective-C 中管理内存

## 使用自管理的内存 (Self-Managed Memory)

如果你使用 `alloc` 或 `new` 创建对象，你就负责管理它们的内存（如果内存是一个问题的话）。这意味着当你完成一个对象并想要释放它的内存时，由你来操作，直到它的引用计数变为零，Objective-C 才会将其销毁（dealloc）。

在这个任务中，你将把一个自管理的对象添加到上一个任务的 `pool.m` 中，这样你就可以对比自管理内存和池管理内存的过程。

### 如何为对象使用自管理的内存：

1. 打开 `pool.m`。

2. 添加代码来创建一个自管理的字符串（**列表 10.13**）。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(void)
{
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc];
    NSString *string1 = [NSString stringWith:@"Pool-managed string"];
    NSString *string2 = [[NSString alloc] initWithString:@"Self-managed string"];
    printf("%s’s retain count: %x\n", [string1 cString], [string1 retainCount]);
    [pool release];
    return 0;
}
```

**列表 10.13** 编辑 `pool.m`。

3. 添加代码来打印自管理字符串的引用计数并释放该对象（**列表 10.14**）。

4. 保存 `pool.m`。

5. 运行编辑后的 `pool.m` 程序。你应该会看到以下内容：

`Pool-managed string’s retain count: 1`

`Self-managed string’s retain count: 1`

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main(void)
{
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc];
    NSString *string1 = [NSString stringWith:@"Pool-managed string"];
    NSString *string2 = [[NSString alloc] initWithString:@"Self-managed string"];
    printf("%s’s retain count: %x\n", [string1 cString], [string1 retainCount]);
    printf("%s’s retain count: %x\n", [string2 cString], [string2 retainCount]);
    [string2 release];
    [pool release];
    return 0;
}
```

**列表 10.14** 编辑后的 `pool.m` 程序。

## 创建类

如果你创建的自定义类在内部存储了其他对象，那么当整个对象被销毁时，你就负责释放这些内部对象。在本章剩余的任务中，你将通过一个名为 `Friend` 的示例来了解其工作原理，它内部存储了两个 `NSString` 对象，分别对应朋友的名字和姓。当 `Friend` 对象被销毁时，你需要手动释放这两个内部字符串。

### 如何创建 `Friend` 类：

1. 创建一个名为 `friends.m` 的文件。

2. 在 `friends.m` 中，输入如**列表 10.15** 所示的代码。这段代码创建了 `Friend` 类并在内部存储了朋友的姓。

3. 保存 `friends.m`。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

@interface Friend : NSObject
{
    NSString *firstName;
    NSString *lastName;
}

-(id)initWithName:(NSString*)first lastName:(NSString*)last;
-(void)setName:(NSString*)first lastName:(NSString*)last;
-(void)print;
@end

@implementation Friend

-(id)initWithName:(NSString*)first lastName:(NSString*)last
{
    self = [super init];
    if (self) {
        [self setName:first lastName:last];
    }
    return self;
}

-(void)setName:(NSString*)first lastName:(NSString*)last
{
    [self setFirst:first];
    [self setLast:last];
}

-(void)print
{
    printf("friend’s name is %s%s", [firstName cString], [lastName cString]);
}

@end
```

**列表 10.15** `friends.m`。

## 存储内部对象

在这个任务中，你将继续使用上一个任务中的 `Friend` 类。在这里，你会将姓的名字作为 `NSString` 对象存储在内部。

### 如何存储内部对象：

1. 打开 `friends.m`。

2. 添加代码将姓的名字作为 `NSString` 对象存储在 `Friend` 对象中（**列表 10.16**）。

3. 保存 `friends.m`。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

@interface Friend : NSObject
{
    NSString *firstName;
    NSString *lastName;
}

-(id)initWithName:(NSString*)first lastName:(NSString*)last;
-(void)setName:(NSString*)first lastName:(NSString*)last;
-(void)setFirst:(NSString*)first;
-(void)setLast:(NSString*)last;
-(void)print;
@end

@implementation Friend

-(id)initWithName:(NSString*)first lastName:(NSString*)last
{
    self = [super init];
    if (self) {
        [self setName:first lastName:last];
    }
    return self;
}

-(void)setName:(NSString*)first lastName:(NSString*)last
{
    [self setFirst:first];
    [self setLast:last];
}

-(void)setFirst:(NSString*)first
{
    [first retain];
    [firstName release];
    firstName = first;
}

-(void)setLast:(NSString*)last
{
    [last retain];
    [lastName release];
    lastName = last;
}

-(void)print
{
    printf("friend’s name is %s%s", [firstName cString], [lastName cString]);
}

@end
```

**列表 10.16** 编辑 `friends.m`。

## 创建 main 方法

在这个任务中，你将为示例创建 `main` 方法，以便在容器对象被销毁时释放内部对象。

### 如何创建 `main` 方法：

1. 打开 `friends.m`。

2. 添加代码创建一个名为 `dan` 的 `Friend` 类对象（**列表 10.17**）。

3. 添加代码来打印名字并释放该对象（**列表 10.18**）。

4. 保存 `friends.m`。

```objectivec
int main(void)
{
    NSString *first = [[NSString alloc] initWithString:@"Dan"];
    NSString *last = [[NSString alloc] initWithString:@"Green"];
    Friend *dan = [[Friend alloc] initWithName:first lastName:last];
    [first release];
    [last release];
    return 0;
}
```

**列表 10.17** 编辑 `friends.m`。

```objectivec
int main(void)
{
    NSString *first = [[NSString alloc] initWithString:@"Dan"];
    NSString *last = [[NSString alloc] initWithString:@"Green"];
    Friend *dan = [[Friend alloc] initWithName:first lastName:last];
    [first release];
    [last release];
    [dan print];
    [dan release];
    return 0;
}
```

**列表 10.18** 编辑 `friends.m`。

## 在 Objective-C 中管理内存

### 执行释放内存

### 释放内存：你自己

此任务将完成说明如何释放自定义对象内部内存的示例。在这里，当整个对象被 dealloc 时，你实际上释放了内部存储的对象。

**要释放内部内存：**

1. 打开 `friends.m`。

2. 添加代码以在完整的 `Friend` 对象被 dealloc 时释放内部字符串（**列表 10.19**）。



```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

@interface Friend : NSObject
{
    NSString *firstName;
    NSString *lastName;
}

-(Friend*)initWithName:(NSString*)first lastName:(NSString*)last;
-(void)setName:(NSString*)first lastName:(NSString*)last;
-(void)setFirst:(NSString*)first;
-(void)setLast:(NSString*)last;
-(void)print;

@end

@implementation Friend

-(Friend*)initWithName:(NSString*)first lastName:(NSString*)last
{
    self = [super init];
    if (self) {
        [self setName:first lastName:last];
    }
    return self;
}

-(void)setName:(NSString*)first lastName:(NSString*)last
{
    [self setFirst:first];
    [self setLast:last];
}

-(void)setFirst:(NSString*)first
{
    [first retain];
    [firstName release];
    firstName = first;
}
```

**列表 10.19** 编辑`friends.m`。

3. 保存`friends.m`。

4. 运行`friends.m`程序。你应该看到以下内容：

你的朋友的名字是 Dan Green

`Friends`对象已被`dealloc`，其内部存储的对象`first`和`last`已被释放。

```objectivec
-(void)setLast:(NSString*)last
{
    [last retain];
    [lastName release];
    lastName = last;
}

-(void)print
{
    printf("Your friend’s name is %s %s", [firstName cString], [lastName cString]);
}

-(void) dealloc
{
    [firstName release];
    [lastName release];
    [super dealloc];
}

@end

int main(void)
{
    NSString *first = [NSString alloc] initWithString:@"Dan"];
    NSString *last = [NSString alloc] initWithString:@"Green"];
    Friend *dan = [Friend alloc] initWithWithName:first lastName:last];
    [first release];
    [last release];
    [dan print];
    [dan release];
    return 0;
}
```

**列表 10.19** 继续。

## 异常处理

错误是生活中的常态。即使是最完美的程序员，有时也会编写产生运行时错误的代码。本章将关于处理此类情况。你通常会遇到两种错误：编译时错误和运行时错误。编译时错误是由编译器抛出的，你必须在继续运行程序之前修复它们。运行时错误发生在运行时，即使你的代码编译无误。运行时错误通常被称为异常。

Objective-C 可以处理异常，但其处理方式随平台而异。在本章中，我们将使用 GNUstep 的异常处理方式，这是最常用的方法。在这里，你使用诸如`NS_DURING`和`NS_HANDLER`等宏在异常发生时对其进行处理。例如，这段代码创建了一个自定义异常并对其进行报告：

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main( )
{
    AutoreleasePool *pool = [AutoreleasePool alloc]init];
    NS_DURING
    {
        NSException *myException = [NSException alloc] initWithName:@"MyException" reason:@"Meltdown!" userInfo:nil];
        [myException raise];
        [pool release];
    }
    NS_HANDLER
    {
        printf("In error handler.\n");
        if ([localException name] isEqualToString:@"MyException"]) {
            printf("Meltdown error.\n");
        }
    }
    NS_ENDHANDLER
    {
        printf("In end handler.");
    }
    return 0;
}
```

### 捕获异常

当你的代码可能导致异常时（例如除以零），你可以将其封装在`NS_DURING`宏中，如下所示：

```objectivec
NS_DURING
{
    /*Sensitive code]*/
}
```

这是 GNUstep 异常处理的第一步：在`NS_DURING`宏内部发生的任何异常都可以在`NS_HANDLER`宏中处理，将在下一个任务中介绍。

**要捕获异常：**

1. 创建一个名为`main.m`的程序。

2. 在`main.m`中输入**列表 11.1**所示的代码。这段代码创建了一个`NS_DURING`块。

3. 将你容易异常的代码添加到`NS_DURING`块中（**列表 11.2**）。

4. 保存`main.m`。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main( )
{
    NS_DURING
    {
        .
        .
    }
    return 0;
}
```

**列表 11.1** 开始`main.m`。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main( )
{
    NS_DURING
    {
        [Sensitive code]
    }
    return 0;
}
```

**列表 11.2** `main.m`。

### 处理异常

当异常发生时，你可以在`NS_HANDLER`宏中处理它，正如你在任务中将看到的那样。

**处理异常：**

1. 创建一个名为`main.m`的程序。

2. 在`main.m`中输入**列表 11.3**所示的代码。这段代码创建了`NS_DURING`块。

3. 添加`NS_HANDLER`宏来处理发生的异常（**列表 11.4**）。

4. 保存`main.m`。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main( )
{
    NS_DURING
    {
        .
        .
    }
    return 0;
}
```

**列表 11.3** 开始`main.m`。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main( )
{
    NS_DURING
    {
        .
        .
    }
    NS_HANDLER
    {
        .
        .
    }
    return 0;
}
```

**列表 11.4** `main.m`程序。

### 使用结束处理器

你可以在`NS_ENDHANDLER`块中处理异常。在`NS_HANDLER`块执行后，该块会运行，让你有机会清理。

**使用结束处理器：**

1. 创建一个新的名为`main.m`的程序。

2. 在`main.m`中输入**列表 11.5**所示的代码。这段代码包含了`NS_DURING`和`NS_HANDLER`块。

3. 添加`NS_ENDHANDLER`块，用于你想在`NS_HANDLER`块执行后运行的代码（**列表 11.6**）。

4. 保存`main.m`。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main( )
{
    NS_DURING
    {
        .
        .
        .
    }
    NS_HANDLER
    {
        .
        .
        .
    }
    return 0;
}
```

**列表 11.5** 开始`main.m`。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main( )
{
    NS_DURING
    {
        .
        .
        .
    }
    NS_HANDLER
    {
        .
        .
        .
    }
    NS_ENDHANDLER
    {
        .
        .
        .
    }
    return 0;
}
```

**列表 11.6** `main.m`程序。

## 创建异常

现在你将引发异常以便处理它并确认你的代码正常。在此任务中，你将创建一个异常对象；你将抛出该异常，导致异常实际发生。之后，你可以捕获并处理该异常。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main( )
{
    AutoreleasePool *pool = [AutoreleasePool alloc]init];
    NS_DURING
    {
        NSException *myException = [NSException alloc] initWithName:@"MyException" reason:@"Meltdown!" userInfo:nil];
        [myException raise];
        [pool release];
    }
    NS_HANDLER
    {
        printf("In error handler.\n");
        if ([localException name] isEqualToString:@"MyException"]) {
            printf("Meltdown error.\n");
        }
    }
    NS_ENDHANDLER
    {
        printf("In end handler.");
    }
    return 0;
}
```

**列表 11.7** 开始`main.m`。

## 第 11 章：创建异常

3. 添加代码以从异常处理程序和异常结束处理程序显示消息（**列表 11.8**）。

4. 保存`main.m`。

5. 运行`main.m`程序。

你应该看到以下内容：

在错误处理程序中。

在结束程序中。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main()
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NS_DURING
    {
        NSException *myException = [[NSException alloc] initWithName:@"MyException"
            reason:@"Meltdown!" userInfo:nil];
        [myException raise];
        [pool release];
    }
    NS_HANDLER
    {
        printf("In error handler.\n");
    }
    NS_ENDHANDLER
    {
        printf("In end handler.");
    }
    return 0;
}
```

**列表 11.8** `main.m`程序。

## 检查发生了什么异常

在异常处理块中，你可以通过`localException`引用发生的异常，它是 Objective-C 内置的一个对象。然后你可以通过向它发送`name`消息来找到它的名称，从而确定发生了什么异常。在这个任务中，你将确定发生了什么异常并显示相应的消息。

**要确定发生了什么异常：**

1. 创建一个名为`main.m`的新程序。

2. 在`main.m`中，输入**列表 11.9**所示的代码。此输入项创建了异常和异常处理代码。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main()
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NS_DURING
    {
        NSException *myException = [[NSException alloc] initWithName:@"MyException"
            reason:@"Meltdown!" userInfo:nil];
        [myException raise];
        [pool release];
    }
    NS_HANDLER
    {
        printf("In error handler.\n");
    }
    NS_ENDHANDLER
    {
        printf("In end handler.");
    }
    return 0;
}
```

**列表 11.9** `main.m`。

3. 输入代码以检查异常的名称并显示它（**列表 11.10**）。

4. 保存`main.m`。

5. 运行`main.m`程序。

你应该看到：

在错误处理程序中。

在结束程序中。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main()
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NS_DURING
    {
        NSException *myException = [[NSException alloc] initWithName:@"MyException"
            reason:@"Meltdown!" userInfo:nil];
        [myException raise];
        [pool release];
    }
    NS_HANDLER
    {
        printf("In error handler.\n");
    }
    NS_ENDHANDLER
    {
        printf("In end handler.");
    }
    return 0;
}
```

**列表 11.10** `main.m`程序。

## 处理多个异常

为了处理多个异常，你会在`NS_HANDLER`块中使用`if/else`。

1. 创建一个名为`main.m`的文件。

2. 在`main.m`中输入**列表 11.11**所示的代码。这会检查多个异常。

```objectivec
#import <Foundation/Foundation.h>
#import <stdio.h>

int main()
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NS_DURING
    {
        NSException *myException = [[NSException alloc] initWithName:@"MyException"
            reason:@"Meltdown!" userInfo:nil];
        [myException raise];
        [pool release];
    }
    NS_HANDLER
    {
        printf("In error handler.\n");
    }
    NS_ENDHANDLER
    {
        printf("In end handler.");
    }
    return 0;
}
```

**列表 11.11** `main.m`。

3. 输入代码以将未处理的异常传递回堆栈（**列表 11.12**）。



## 4. 保存 `main.m`

```objc
NS_DURING
{
}
NS_HANDLER
{
}
```

**列表 11.12** `main.m`

## 将异常传递回堆栈

有时在处理异常时，你可能希望将异常传递回堆栈中的调用代码。你可以简单通过在 `NS_HANDLER` 块中再次抛出异常来实现，正如在这个任务中所示。

**将异常传递回堆栈：**

1. 创建一个名为 `main.m` 的文件。
2. 在 `main.m` 中输入**列表 11.13**所示的代码。这设置了处理多个异常。

```objc
NS_DURING
{
}
NS_HANDLER
{
    if ([localException isEqualToString:@"Exception1"]) {
    } else if ([localException isEqualToString:@"Exception2"]) {
    } else {
        [localException raise];
    }
}
```

**列表 11.13** `main.m`

3. 输入代码将未处理的异常传递回堆栈（**列表 11.14**）。
4. 保存 `main.m`。

```objc
NS_DURING
{
}
NS_HANDLER
{
    if ([localException isEqualToString:@"Exception1"]) {
    } else if ([localException isEqualToString:@"Exception2"]) {
    } else {
        [localException raise];
    }
}
```

**列表 11.14** `main.m`

## 从异常处理程序返回返回值

如果你的异常处理程序位于函数中，你可能希望从该函数返回一个值——也就是说，即使函数发生了异常，你可能仍然想向调用代码返回一个值。然而，你不能直接在异常处理程序中使用 `return` 语句——你必须使用 `NS_RETURNVALUE`，正如在这个任务中所看到的。

**从异常处理程序返回返回值：**

1. 创建一个名为 `main.m` 的文件。
2. 在 `main.m` 中输入**列表 11.15**所示的代码。此输入项设置了处理多个异常的逻辑。

```objc
NS_DURING
{
}
NS_HANDLER
{
    if ([localException isEqualToString:@"Exception1"]) {
    } else if ([localException isEqualToString:@"Exception2"]) {
    } else {
        [localException raise];
    }
}
```

**列表 11.15** `main.m`

3. 添加代码从异常处理代码返回返回值（**列表 11.16**）。
4. 保存 `main.m`。

```objc
NS_DURING
{
}
NS_HANDLER
{
    if ([localException isEqualToString:@"Exception1"]) {
        NS_RETURNVALUE(0);
    } else if ([localException isEqualToString:@"Exception2"]) {
        NS_RETURNVALUE(1);
    } else {
        [localException raise];
    }
}
```

**列表 11.16** `main.m` 程序

## 异常处理

### 从异常处理程序返回 `void` 值

函数中的异常处理代码也可以从函数返回 `void` 值（如果你希望你的函数返回 `void` 值），但你需要使用一个特殊的宏 `NS_VALUERETURNVOID` 来实现这一操作。

**要从异常处理程序返回 `void` 值：**

1. 创建名为 `main.m` 的文件。
2. 在 `main.m` 中，输入**列表 11.17**所示的代码。此条目为多个异常设置了异常处理代码。

```objectivec
NS_DURING
{
    .
    .
    .
}
NS_HANDLER
{
    if ([[localException name isEqualToString:@"Exception1"])
    {
        .
        .
        .
    }
    else if ([[localException name isEqualToString:@"Exception2"])
    {
        .
        .
        .
    }
    else
    {
        [localException raise];
    }
}
NS_ENDHANDLER
    .
    .
    .
}
```

**列表 11.17** 开始 `main.m`

3. 添加从异常处理代码返回 `void` 的代码（**列表 11.18**）。
4. 保存 `main.m`。

```objectivec
NS_DURING
{
    .
    .
    .
}
NS_HANDLER
{
    if ([[localException name isEqualToString:@"Exception1"])
    {
        NS_VALUERETURNVOID;
    }
    else if ([[localException name isEqualToString:@"Exception2"])
    {
        NS_VALUERETURNVOID;
    }
    else
    {
        [localException raise];
    }
}
NS_ENDHANDLER
    .
    .
    .
}
```

**列表 11.18** `main.m` 程序

### 捕获未捕的异常

你可以通过调用 `NSSetUncaughtExceptionHandler(fn_ptr)` 设置一个特殊函数来捕获所有未处理的异常，其中 `fn_ptr` 是一个函数的指针（类似于标准指针，只是它指向的是形式为 `void UncaughtExceptionHandler(NSException *exception)` 的函数）。因此，如果你在其他地方都没有处理异常，它将在 `UncaughtExceptionHandler` 函数中被处理。

**要捕获未捕的异常：**

1. 创建名为 `main.m` 的文件。
2. 在 `main.m` 中，输入**列表 11.19**所示的代码。此代码设置了异常处理函数。

```objectivec
int main()
{
    NSSetUncaughtExceptionHandler(UncaughtExceptionHandler);
}
void UncaughtExceptionHandler(NSException *exception)
{
    // handle exception
}
```

**列表 11.19** 开始 `main.m`

3. 添加你的异常处理代码（**列表 11.20**）。
4. 保存 `main.m`。现在你的代码可以捕获之前未捕获的异常。

```objectivec
int main()
{
    NSSetUncaughtExceptionHandler(UncaughtExceptionHandler);
}
void UncaughtExceptionHandler(NSException *exception)
{
    if ([exception name isEqualToString:@"Exception1"])
    {
        .
        .
        .
    }
    else if ([exception name isEqualToString:@"Exception2"])
    {
        .
        .
        .
    }
    else
    {
        .
        .
        .
    }
}
```

**列表 11.20** `main.m` 程序

## 索引

- `enumerator.m` 程序, 167–168
- 等于运算符, 24, 26, 31
- 错误, 203。*另请* 异常
- 异常处理器
  - 从返回返回, 217–218
  - 返回 `void` 值, 219–220
- 异常, 203–222
  - 捕获, 205
  - 捕获未捕获的异常, 221–222
  - 检查/显示名称, 211–212
  - 检查多个, 213–214
  - 创建, 209–210
  - 处理, 206–208, 213–214
  - 向上调用栈传递, 215–216

### F

- 阶乘, 76
- 文件
  - 头文件（*参见* 头文件）
  - 链接多个, 95–96
  - 程序（*参见* 程序文件）
  - 源代码, 144
- `float` 数据类型, 11, 54
- 浮点值, 9, 11
- `for` 循环, 25, 35–36, 48, 168
- `for.m` 程序, 36
- `Foundation` 类, 54, 81, 163, 164
- `Foundation` 头文件, 44, 45。*另请参* 头文件
- `friends.m` 程序, 197–202
- `functionargs.m` 程序, 65
- 函数参数, 64–65
- 函数声明, 63
- `function.m` 程序, 61
- `functionpassconstantarrays.m` 程序, 74–75
- `functionpasspointers.m` 程序, 70–71
- `functionpointers.m` 程序, 77–78
- 函数原型, 62–63, 64
- `functionrecursion.m` 程序, 76
- `functionreturn.m` 程序, 67
- 函数, 59–78
  - 调用, 60, 76
  - 创建, 59–61
  - 声明, 62–63
  - 已定义, 3, 59
  - 定义, 60, 61
  - 向函数传递参数, 64–65
  - 向函数传递数组, 72–73
  - 向函数传递常量数据, 74–75
  - 向函数传递指针, 70–71
  - 目的, 59
  - 从返回返回, 66–67
  - 使用指针, 77–78
- 函数作用域, 68–69
- `functionscope.m` 程序, 68–69

### G

- `GNUmakefile`, 45, 55, 56, 81, 95–96
- `GNUstep`
  - 命令行提示符, 81
  - 下载/安装, 6
  - 环境变量, 45
  - 异常处理, 203, 205
  - `shell`, 81
- 大于运算符, 31
- 大于等于运算符, 31

### H

- `header2.h` 文件, 94
- `header2.m` 程序, 94
- 头文件
  - 向其添加实现, 94
  - 文件扩展名, 4
  - 用于 `NS`-类对象, 44, 45
  - 在其中放入函数原型, 63
  - 特定的
    - `class1extender.h`, 146
    - `class1.h`, 145, 151
    - `class2.h`, 152
    - `ClassFirst.h`, 158
    - `ClassSecond.h`, 158
    - `container.h`, 95
    - `header2.h`, 94
  - `printing.h`, 158
  - `stdio.h`, 4, 63
  - 在其中存储接口, 92–93
  - `header.m` 程序, 92–93
  - `.h` 文件扩展名, 4

### I

- `id.m` 程序, 111–112
- `id` 类型, 111–112
- `if.m` 程序, 26
- `if` 语句, 23–24, 26, 27, 213–214
- `@implementation` 关键字, 82, 92, 94
- `increment.m` 程序, 20
- 递增运算符, 19–20
- 不等于运算符, 31
- 继承, 119–139
  - 来自基类数据成员, 122–123
  - 基类方法, 124–125
  - 源自类, 121
  - 已定义, 119
  - 工作原理, 119–120
  - 多级, 120, 130–131
  - 多重, 142, 156
  - 重载基类方法, 128–129
  - 覆盖基类方法, 126–127
  - 多态, 138–139
  - 目的, 120
  - 限制, 134–135
  - 停止, 132–133
  - 使用构造函数, 136–137
  - `inheritdata.m` 程序, 122–123
  - `inheritmethods.m` 程序, 124–125
  - `init.m` 程序, 47
  - `init` 方法, 97
  - `insertObject` 消息, 166
  - `instances.m` 程序, 118
  - `instancesRespondTo` 方法, 118
  - `int` 数据类型, 11
  - 整数变量, 8, 9, 11
  - `@interface` 关键字, 82, 92
  - 接口，定义, 157–158
  - 内部对象, 198–199
  - `intValue` 函数, 56
  - I/O 函数, 4
  - `isKindOfClass.m` 程序, 115–116
  - `isMemberOfClass.m` 程序, 113–114, 15
  - 迭代，循环, 35

### L

- 小于运算符, 31
- 小于等于运算符, 31
- 链接文件, 95–96
- Linux
  - 编译/运行, 7
  - 在其中创建 `GNUmakefile`, 81
  - 在其中创建 `NS`-类对象, 45
  - 在其中创建程序, 5
- `localException` 对象, 211
- `logical.m` 程序, 32
- 逻辑运算符, 32
- `long` 数据类型, 11
- `loop-index` 变量, 25, 35
- 循环迭代, 35
- 循环, 35–42
  - 数组, 48, 167–168
  - 跳出, 35, 41–42
  - 跟踪, 35
  - 目的, 25, 35
  - 使用特定的 `do...while` 循环, 39–40
  - `for` 循环, 25, 35–36, 48, 168
  - `while` 循环, 37–38

### M

- Mac
  - 在上面编译/运行, 6
  - 在上面创建 `NS`-类对象, 45
  - 在上面创建程序, 5
- `main` 方法, 200
- `main.m` 程序
  - 捕获异常, 205, 221–222
  - 创建异常, 209–210
  - 处理异常, 206
  - 处理多个异常, 213–214
  - 识别异常, 211–212
  - 链接多个文件, 95
  - 将一个类作为另一个类, 153–154
  - 向上栈传递异常, 215–216
  - 从异常处理器返回, 217–220
  - 使用基类配合分类, 147–148
  - 使用 `end handler`, 207–208
  - 使用接口, 161–162
- `makefile`, 45, 54, 55, 81
- 内存
  - 释放内存, 192–193, 197–202
  - Objective-C 如何管理, 183–184
  - 释放数组, 175
  - 自管理, 195–196
- 方法
  - 添加到类, 141
  - 基类（*参见* 基类方法）
  - 类（*参见* 类方法）
  - 创建, 85, 87
  - 已定义, 56, 59
  - 定义实现, 159–160
  - 定义接口, 155–158
  - 用于初始化数据, 97
  - 对象, 81, 83, 87, 88
  - 重载, 128–129
  - 向方法传递参数, 90–91
  - 验证对象支持, 117–118
- `.m` 文件扩展名, 3
- 取模运算运算符, 15, 21–22
- 多级继承, 120, 130–131
- `multilevel.m` 程序, 130–131
- `multipleargs.m` 程序, 90–91
- 多个异常, 213–214
- 多重继承, 142, 156
- 乘法运算符, 15
- 可变数组, 169–172
- 可变字典, 180–182

### N

- `name` 消息, 211
- `nextObject` 消息, 167, 168
- `NeXtStep`, 44
- `nil` 对象, 165
- `not` 运算符, 32
- `NSArray` 类, 165
- `NS`-类对象, 45
- `NS_DURING` 宏, 205
- `NS_END` 宏, 207–208



# 索引

## N

- `NS_HANDLER` 宏, 215–216
- `NS_RETURN` 宏, 217–220
- `NS_VALUE` 宏, 56
- `NS_VOID` 宏, 219–220
- `NSString` 类, 44, 54
- `NSObject` 类, 81

## O

- `objectAtIndex` 消息, 166
- `object.m` 程序, 88–100
- Objective-C
  - 添加到类, 141
  - 数组，分类, 147–148
  - 语言, 1
  - 类, 19–139
  - 编译/运行, 6–7
  - 创建程序, 3–5
  - 字典, 180–182
  - 数据, 11
  - 声明, 62–63
  - 派生类, 152
  - 接口, 157–158
  - 异常, 203–222
  - 继承, 119–139
  - 内存管理, 183–184
  - 方法, 59–78
  - 多态, 138–139
  - 程序, 23–25
  - 运行时, 81–96
  - 作用域, 68–69
  - 变量, 8, 9, 11
  - 目的, 120
  - 使用, 103–104
  - 源代码, 141–154

## 程序（续）

- 特定的访问 accesselements.m, 166
- `access.m`, 102–105, 121
- `addelements.m`, 171–172
- `addkeys.m`, 181–182
- `array2.m`, 50
- `arrayloop.m`, 48
- `array.m`, 46
- `assignment.m`, 17–18
- `break.m`, 42
- `cast.m`, 22
- `class1extender.m`, 146
- `class1.m`, 145, 151
- `class2.m`, 152
- `ClassFirst.m`, 159
- `classmethod.m`, 85
- `ClassSecond.m`, 160
- `classvariables.m`, 109–110
- `compare.m`, 31
- `conditional.m`, 34
- `constructor.m`, 97–98, 136–137
- `container.m`, 96
- `createarray.m`, 165
- `createdictionary.m`, 176–177
- `createmutablearray.m`, 169–170
- `createmutabledictionary.m`, 180
- `createobject.m`, 185
- `datatype.m`, 11–12
- `dealloc.m`, 192–193
- `decrementcount.m`, 190–191
- `do.m`, 40
- `else.m`, 28
- `enumeration.m`, 57–58
- `enumeratordictionary.m`, 178–179
- `enumerator.m`, 167–168
- `for.m`, 36
- `friends.m`, 197–202
- `functionargs.m`, 65
- `function.m`, 61
- `functionpassconstantarrays.m`, 74–75
- `functionpasspointers.m`, 70–71
- `functionpointers.m`, 77–78
- `functionprototype.m`, 63
- `functionrecursion.m`, 76
- `functionreturn.m`, 67
- `functionscope.m`, 68–69
- `header2.m`, 94
- `header.m`, 92–93
- `id.m`, 111–112
- `if.m`, 26
- `increment.m`, 20
- `inheritdata.m`, 122–123
- `inheritmethods.m`, 124–125
- `initialarray.m`, 47
- `instances.m`, 118
- `isKindOfClass.m`, 115–116
- `isMemberOfClass.m`, 113–114, 115
- `logical.m`, 32
- `main.m`, 95, 147, 153, 161, 205–222
- `multilevel.m`, 130–131
- `multipleargs.m`, 90–91
- `objectdata.m`, 88–89
- `object.m`, 86, 108
- `objectmethod.m`, 87
- `operators.m`, 15–16
- `overload.m`, 128–129
- `override.m`, 126–127
- `math.m`, 52
- `pointersarray.m`, 53
- `pointers.m`, 51
- `pool.m`, 194–195, 196
- `private.m`, 132–133
- `protected.m`, 134–135
- `releasememory.m`, 175
- `responds.m`, 117
- `retaincount.m`, 186–187
- `sortarray.m`, 173–174
- `source.m`, 45
- `string.m`, 54
- `stringtoint.m`, 56
- `switch.m`, 30
- `temperature.m`, 10
- `while.m`, 38

## P

- protected access specifier, 99, 100, 105–106, 134
- `protected.m`, 134–135
- protocols, 155–162
  - creating class implementations for, 159–160
  - defined, 142
  - defining, 157–158
  - how they work, 155–156
  - purpose of, 155
  - using, 161–162
  - using multiple, 156
- prototypes, function, 62–63, 64
- public access specifier, 99, 100, 102

## R

- recursion, 60, 76
- `releasememory.m`, 175
- release message, 184, 194
- `responds.m`, 117
- `respondsToSelector()` function, 117
- retain count, 183–191
  - decrementing, 184–191
  - displaying, 186–187
  - incrementing, 183–184
  - purpose of, 183
- retain message, 186
- `retaincount.m`, 186–187
- release message, 184, 188
- run-time errors, 203. *See also* exceptions

## S

- scientific notation, 9
- scope, function, 68–69
- `self` keyword, 109–110
- self-managed memory, 195–196
- short data type, 11
- signed integers, 9
- `sortarray.m`, 173–174
- `sortUsing` message, 173
- source code, 144
- `source.m`, 45
- static arrays, 165
- `stdio.h` file, 4, 63
- `string.m`, 54
- strings, 29, 44, 54–56, 165
- `stringtoint.m`, 56
- subtraction operator, 15
- super classes, 97
- `super` keyword, 136
- `switch.m`, 30
- switch statement, 29–30

## T

- `temperature.m`, 10
- text strings, 29, 44. *See also* strings
- two-dimensional arrays, 49–50

## U

- UNIX
  - compiling/running programs in, 7
  - creating GNUmakefile in, 81
  - creating NS-class objects in, 45
  - creating programs in, 5
- unsigned decimal integers, 9

## V

- values
  - assigning to variables, 17–18
  - displaying in variables, 9–10
  - returning from functions, 66–67
- variables
  - assigning values to, 17–18
  - class, 99, 107–108
  - creating, 8, 111–112
  - displaying values in, 9–10
  - for multiple object types, 111–112
  - public *vs.* private, 100–104
  - purpose of, 8
- void value, 219–220

## W

- while loop, 37–38
- `while.m` program, 38
- Windows
  - compiling/running programs in, 7
  - creating GNUmakefile in, 81
  - creating NS-class objects in, 45
  - creating programs in, 5

## X

- Xcode, 5, 6, 45

From the Library of Wow! eBook
