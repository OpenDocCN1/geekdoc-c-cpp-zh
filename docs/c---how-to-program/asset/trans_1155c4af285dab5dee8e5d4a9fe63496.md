
编译器编译一条 `printf` 语句时，仅仅在目标程序中为对库函数的“调用”提供空间。但编译器*并不*知道库函数在哪里——*链接器*知道。当*链接器*运行时，它会定位库函数，并在目标程序中插入对这些库函数的正确调用。现在目标程序已完整，可以执行了。因此，链接后的程序称为*可执行文件*。如果函数名拼写错误，*链接器*会发现该错误，因为它无法将 C 程序中的名称与库中任何已知函数的名称匹配。

> **常见编程错误 2.1**
>
> *在程序中将输出函数 `printf` 的名称误拼为 `print`。*

> **良好编程实践 2.3**
>
> *在定义函数体的花括号内，将每个函数的整个函数体缩进一级（我们建议三个空格）。这种缩进强调程序的功能结构，并有助于使程序更易读。*

> **良好编程实践 2.4**
>
> *为你偏好的缩进大小设定一种约定，然后统一应用该约定。可以使用 Tab 键创建缩进，但制表位可能各不相同。专业风格指南通常建议使用空格而不是制表符。*

## 使用多个 printf

`printf` 函数可以用多种不同方式打印 `Welcome to C!`。例如，图 2.3 的程序产生与图 2.1 的程序相同的输出。这之所以可行，是因为每个 `printf` 都从上一个 `printf` 停止打印的位置继续打印。第一个 `printf`（第 8 行）打印 `Welcome`，后跟一个空格（但不换行），第二个 `printf`（第 9 行）紧接在空格之后在*同一行*开始打印。

```c
// Fig. 2.3: fig02_03.c
// Printing on one line with two printf statements.
#include <stdio.h>

// function main begins program execution
int main( void )
{
    printf( "Welcome " );
    printf( "to C!\n" );
} // end function main
```

```
Welcome to C!
```

**图 2.3** | 使用两条 `printf` 语句打印一行。

一个 `printf` 可以通过使用额外的换行符来打印*多*行，如图 2.4 所示。每次遇到 `\n`（换行）转义序列时，输出都会在下一行开头继续。

```c
// Fig. 2.4: fig02_04.c
// Printing multiple lines with a single printf.
#include <stdio.h>

// function main begins program execution
int main( void )
{
   printf( "Welcome\nto\nC!\n" );
} // end function main
```

```
Welcome
to
C!
```

**图 2.4** | 使用单个 `printf` 打印多行。

## 2.3 另一个简单的 C 程序：两个整数相加

下一个程序使用标准库函数 `scanf` 获取用户在键盘上输入的两个整数，计算这两个值的和，并使用 `printf` 打印结果。该程序及示例输出如图 2.5 所示。[在图 2.5 的输入/输出对话框中，我们用**粗体**强调用户输入的数字。]

```c
// Fig. 2.5: fig02_05.c
// Addition program.
#include <stdio.h>

// function main begins program execution
int main( void )
{
   int integer1; // first number to be entered by user
   int integer2; // second number to be entered by user

   printf( "Enter first integer\n" ); // prompt
   scanf( "%d", &integer1 ); // read an integer

   printf( "Enter second integer\n" ); // prompt
   scanf( "%d", &integer2 ); // read an integer

   int sum; // variable in which sum will be stored
   sum = integer1 + integer2; // assign total to sum

   printf( "Sum is %d\n", sum ); // print sum
} // end function main
```

```
Enter first integer
45
Enter second integer
72
Sum is 117
```

**图 2.5** | 加法程序。

第 1–2 行的注释说明了程序的目的。如前所述，每个程序都从 `main` 开始执行。左花括号 `{`（第 7 行）标记 `main` 函数体的开始，对应的右花括号 `}`（第 21 行）标记 `main` 的结束。

### 变量与变量定义

第 8–9 行

```c
int integer1; // first number to be entered by user
int integer2; // second number to be entered by user
```

是定义。名称 `integer1` 和 `integer2` 是变量名——内存中可存储值供程序使用的位置。这些定义指定变量 `integer1` 和 `integer2` 的类型为 `int`，这意味着它们将保存整数值，即诸如 7、–11、0、31914 等整数。

### 在使用变量之前定义变量

所有变量在程序中*使用之前*都必须定义名称和数据类型。C 标准允许将每个变量定义放在 `main` 中该变量在代码中首次使用之前的*任何位置*（不过一些较旧的编译器不允许这样做）。稍后你将明白为什么应把变量定义在*靠近*其首次使用的位置。

### 在一条语句中定义多个同类型变量

前面的定义可以合并为如下单条定义：

```c
int integer1, integer2;
```

但那样会难以像我们在第 8–9 行所做的那样，将注释与每个变量关联起来。

### 标识符与大小写敏感性

C 语言中的变量名可以是任何有效的标识符。标识符是由字母、数字和下划线（`_`）组成的一串字符，且*不能以*数字开头。C 语言区分大小写——在 C 中大写字母和小写字母不同，因此 `a1` 和 `A1` 是不同的标识符。

> **常见编程错误 2.2**
>
> 在本应使用小写字母的地方使用了大写字母（例如，输入 `Main` 而不是 `main`）。

> **错误预防提示 2.1**
>
> 避免让标识符以下划线字符（`_`）开头，以防止与编译器生成的标识符和标准库标识符发生冲突。

> **良好编程实践 2.5**
>
> 选择有意义的变量名有助于使程序具备自文档性——也就是说，需要的注释更少。

> **良好编程实践 2.6**
>
> 用作简单变量名的标识符的首字母应为小写字母。在本书后文，我们将对以大写字母开头的标识符以及全部使用大写字母的标识符赋予特殊含义。

![](img/d0d3b7423c2d9e5650be79209ea1885d_78_0.png)

### 良好编程实践 2.7

*多词变量名有助于提高程序的可读性。可以用下划线分隔单词，如 total_commissions；或者，如果把单词连在一起，则从第二个单词开始每个单词的首字母大写，如 totalCommissions。后一种风格——通常称为驼峰式命名法，因为大写和小写字母的模式类似骆驼的轮廓——更受推荐。*

### 提示消息

第 11 行

```c
printf("Enter first integer\n"); // prompt
```

显示字面量 "Enter first integer"，并将光标定位到下一行开头。这条消息称为提示，因为它告诉用户执行特定操作。

### `scanf` 函数与格式化输入

第 12 行

```c
scanf("%d", &integer1); // read an integer
```

使用 scanf（其中“f”代表“格式化”）从用户处获取一个值。该函数从标准输入读取，通常为键盘。

这个 scanf 有两个实参："%d" 和 &integer1。第一个是格式控制字符串，指示用户应输入的数据类型。%d 转换说明符表示数据应为整数（字母 d 代表“十进制整数”）。在此上下文中，% 被 scanf（以及 printf）视为开始一个转换说明符的特殊字符。

scanf 的第二个实参以 & 符号（&）开头——称为地址运算符——后跟变量名。& 与变量名结合时，会告诉 scanf 变量 integer1 在内存中存储的位置（或地址）。然后计算机将用户为 integer1 输入的值存储到该位置。使用 & 符号（&）常常令新手程序员或使用过不要求这种表示法的其他语言的人感到困惑。目前，只需记住在每次调用 scanf 时，在每个变量前加上 &。第 6 章和第 7 章将讨论此规则的一些例外情况。在学习了第 7 章中的指针之后，& 的用法将会变得清晰。

![](img/d0d3b7423c2d9e5650be79209ea1885d_78_1.png)

> **良好编程实践 2.8**
>
> *在每个逗号（,）后放置一个空格，以使程序更易读。*

当计算机执行前面的 scanf 时，它会等待用户为变量 integer1 输入一个值。用户通过输入一个整数，然后按下 Enter 键（有时标记为 Return 键）将数字发送给计算机来作出响应。然后计算机将这个数字（或值）赋给变量 integer1。此程序中对 integer1 的任何后续引用都将使用同一个值。函数 printf 和 scanf 促进用户与计算机之间的交互。这种交互类似于对话，通常称为交互式计算。

