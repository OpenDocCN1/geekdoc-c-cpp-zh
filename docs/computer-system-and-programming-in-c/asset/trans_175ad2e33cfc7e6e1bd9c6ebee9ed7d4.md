
## 示例

`%5d` 表示：“将变量作为十进制整数打印在 5 列的字段中”。如果要打印的值没有填满整个字段，则该值会右对齐，并在左侧用空格填充。

如果在格式说明符中包含减号（如 `%-5d`），则表示需要左对齐，该值将在右侧用空格填充。

## 编程示例

指定字段宽度在创建数值表格时很有用，如下面的程序所示。

```c
#include<stdio.h>
#include<conio.h>
void main( )
{
clrscr();
printf("\n%f %f %f", 10.0, 15.5, 135.9 );
printf("\n%f %f %f", 310.0, 1220.9, 3102.3 );
getch();
}
```

以下是输出：

```text
10.000000 15.500000 135.900000
310.000000 1220.900000 3102.300000
```

尽管数字已经打印出来，但数字没有正确对齐，因此难以阅读。更好的方法如下所示：

```c
void main( )
{
clrscr();
printf("\n%10.1f %10.1f %10.1f", 10.0, 15.5, 135.9 );
printf("\n%10.1f %10.1f %10.1f", 310.0, 1220.9, 3102.3 );
getch();
}
```

这会得到更好的输出：

```text
01234567890123456789012345678901
10.0                         15.5                         135.9
310.0                       1220.9                       3102.3
```

即使在显示字符串时，也可以使用格式说明符。下面的程序可以说明这一点：

```c
void main( )
{
char f[ ] = "Manish";
char s[ ] = "Varshney";
char f1[ ] = "Vineet";
char s1[ ] = "Agrawal";
printf ("\n%20s%20s", f, s );
printf ("\n%20s%20s", f1, s1 );
getch();
}
```

以下是输出：

```text
01234567890123456789012345678901234567890
                    Manish                         Varshney
                    Vineet                         Agrawal
```

上述输出的解释如下：

格式说明符 `%20s` 保留 20 列用于打印字符串，然后在这 20 列中右对齐打印该字符串。这有助于将不同长度的名称正确对齐。显然，格式 `%-20s` 会使字符串左对齐。

### 在 printf() 语句中使用转义序列

我们之前已经看到，换行符 `\n` 插入到 printf() 的格式字符串中时，如何将光标移到下一行的开头。换行符是一种“转义序列”，之所以这样称呼，是因为反斜杠符号 (\) 被视为“转义”字符——它使字符串脱离正常的解释方式，从而使下一个字符被识别为具有特殊含义的字符。

下面的示例展示了 `\n` 以及一个新的转义序列 `\t`（称为“制表符”）的用法。`\t` 将光标移动到下一个制表位。80 列屏幕通常有 10 个制表位。换句话说，屏幕被分成 10 个区域，每个区域有 8 列。打印一个制表符会将光标移到下一个打印区域的开头。

## 示例

```c
#include<stdio.h>
#include<conio.h>
void main( )
{
clrscr();
printf("You\tare\ta\tgood\tboy ");
getch();
}
```

上述代码的输出如下：

You are a good boy

下表列出了完整的转义序列。

| 转义序列 | 含义 |
|---|---|
| `\a` | 产生蜂鸣声或闪烁；光标位置不变。 |
| `\b` | 将光标移动到上一行的最后一列。 |
| `\f` | 将光标移动到下一页的开头。 |
| `\n` | 换行 |
| `\r` | 回车（将光标移动到当前行的第一列。） |
| `\t` | 水平制表符 |
| `\v` | 垂直制表符 |
| `\\` | 打印单个 `\` |
| `\"` | 用于引号 |
| `%%` | 打印 `%` |

## 标准输入函数 `scanf()`

`scanf()` 函数允许我们从键盘输入数据，这些数据将按特定方式格式化。转换说明符参数告诉 scanf 如何转换传入的数据。

`scanf()` 语句的一般语法如下：
`scanf("format string", list of addresses of variables);`

- 以下是与 `scanf()` 函数相关的重要点：
  - `scanf` 以字符串参数开始，并且可能包含其他参数。
  - 其他参数必须是指针。
  - `scanf` 返回成功输入的数量。

## 示例

```c
scanf("%d %f %c", &a, &b, &c);
```

请注意，我们向 `scanf()` 函数发送的是变量的地址（地址通过使用 '&'（“取地址”运算符）获得）。这是必要的，因为从键盘接收的值必须被放入与这些地址对应的变量中。通过键盘输入的值必须用空格、制表符或换行符分隔。不要在格式字符串中包含这些转义序列。

我们在 `printf()` 函数中学到的所有格式说明也都适用于 `scanf()` 函数。

## 编程问题

### 问题 1

编写一个程序，输入两个数字并打印这两个数字的和。

### 解决方案

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int a,b,c;
clrscr();
printf("\n Enter the value of a ");
scanf("%d",&a);
printf("\n Enter the value of b");
scanf("%d",&b);
c=a+b;
printf("The answer is %d \n",c);
}
```

上述程序的解释如下：
第一条指令声明了三个整型变量：a、b 和 c。前两个 `printf` 语句只是在屏幕上显示消息，请求用户输入值。然后 `scanf` 函数从键盘读取值到 a 和 b 中。这些值相加，结果 c 连同适当的消息显示在屏幕上。请注意，您可以在 `printf` 语句中将消息与值一起包含。

输入程序，编译并链接，结果就是你的第一个交互式程序。尝试修改它，让它完成一些更有挑战性的任务。也可以尝试修改消息。你只需要记住，不能存储超出整型变量范围的值，也不能计算结果超出范围或带有小数部分的值。

### 问题 2

编写一个程序，输入两个数字并打印这两个数字的加法、乘法、减法和除法。

### 解决方案

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int a,b,c;
printf("\n enter the values of a and b");
scanf("%d %d",&a,&b);
c=a+b;
printf("\n the addition is %d",c);
c=a-b;
printf("\n the subtraction is %d",c);
c=a*b;
printf("\n the multiplication is %d",c);
c=a/b;
printf("\n the division is %d",c);
getch();
}
```

## 非格式化控制台 I/O 函数

格式化与非格式化 I/O 函数的基本区别在于，格式化函数允许根据我们的需求对从键盘读取的输入或显示在 VDU（显示器）上的输出进行格式化。例如，如果要在屏幕上显示平均分和百分比的数值，那么这些输出在屏幕上的显示位置、两个值之间有多少空格、小数点后保留几位等细节，都可以通过格式化函数进行控制。

在非格式化控制台 I/O 函数中，我们无法按照需求进行格式化。

在这一类别中，我们将讨论以下非格式化 I/O 函数。

- getchar()
- putchar()
- getch()
- putch()
- getche()
- gets()
- puts()

### Getchar() 函数

getchar() 函数用于从键盘读取单个字符。

getchar() 函数的一般语法如下：

```c
int getchar (void);
```

**示例**

```c
/* getchar example: typewriter */
#include <stdio.h>
#include<conio.h>
void main ()
{
char c;
puts ("Enter text. Include a dot ('.') in a sentence to exit");
do
{
c=getchar();
putchar (c);
} while (c != '.');
getch();
}
```

上述程序的输出如下：

一个简单的打字机。每次按下 ENTER 键后，每个句子都会被回显，直到文本中包含句点 (.)。

### Putchar() 函数

putchar 是 C 编程语言中的一个函数，用于向标准输出流 stdout 写入单个字符。其原型如下：

```c
int putchar (int character)
```

要打印的字符作为参数传入函数，如果写入成功，则返回参数字符。否则，返回文件结束符（EOF）。

putchar 函数在 C 标准库头文件 stdio.h 中有定义。

**示例**

```c
/* putchar example: printing alphabet */
#include <stdio.h>
#include<conio.h>
void main ()
{
char c;
clrscr();
for (c = 'A'; c <= 'Z'; c++)
{
putchar (c);
}
getch();
}
```

### Getch() 函数

getch() 函数用于从控制台获取下一个可用按键。该

