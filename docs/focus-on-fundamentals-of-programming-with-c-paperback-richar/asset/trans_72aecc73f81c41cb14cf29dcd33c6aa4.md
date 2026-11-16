
程序的输出应同时发送到终端窗口（您的屏幕）以及请求的 `csis.txt` 输出文件。请务必阅读关于捕获程序输出的文档。您的全名和 Palomar ID 号必须作为注释出现在包含 `main()` 的源文件中。请务必将 `csis.txt` 输出文件包含在 zip 压缩包中。

第一天您在银行存入一分钱。第二天您存入两分钱。第三天您存入四分钱。第四天您存入八分钱，以此类推。假设您每天将存款翻倍，请编写一个 C 程序 penny.c，用于确定需要多少天才能累积至少一百万美元。（假设不支付任何利息。）请注意，要累积的金额必须在运行时输入。

对于每一天，您的输出应包括当天的存款金额以及截至当天的银行总余额。您的输出应按以下表格形式显示：

```
Please enter the amount of money you want to accumulate: 1000000

DAY       DEPOSIT       BALANCE
---       -------       -------
1         0.01          0.01
2         0.02          0.03
3         0.04          0.07
4         0.08          0.15
...       ...           ...

It took XX days to accumulate at least $1000000.00.
```

您的程序应包含 main() 函数、一个用于输出表头的函数以及一个用于生成表格的函数。生成表格的函数应接收一个 double 类型的输入参数，用于指定您想要累积的金额。该函数的输出应按小数点对齐列，并向 main() 提供一个返回值，告知累积资金花费了多少天。然后应按上述方式输出该返回值。

请记住，main() 函数应作为程序中的第一个函数出现。请务必为程序中使用的每个函数使用函数原型。

程序的输出应同时发送到终端窗口（您的屏幕）以及请求的 csis.txt 输出文件。请务必阅读关于捕获程序输出的文档。您的全名和 Palomar ID 号必须作为注释出现在包含 main() 的源文件中。请务必将 csis.txt 输出文件包含在 zip 压缩包中。

斐波那契数列是一系列数字：

```
0, 1, 1, 2, 3, 5, 8, 13, 21, ...
```

序列中的每个附加数字都是通过将其前两个数字相加得到的。

编写一个程序 fibonacci.c，用于计算前 20 个斐波那契数。您的程序应包含一个函数 fib()，该函数从 main() 接收一个输入参数，告诉函数要输出多少个斐波那契数。

请记住，main() 函数应作为程序中的第一个函数出现。请务必为程序中使用的每个函数使用函数原型。

程序的输出应同时发送到终端窗口（您的屏幕）以及请求的 csis.txt 输出文件。请务必阅读关于捕获程序输出的文档。您的全名和 Palomar ID 号必须作为注释出现在包含 main() 的源文件中。请务必将 csis.txt 输出文件包含在 zip 压缩包中。

## 第 9 章 输入-输出

- 流
- getchar()
- putchar()
- 文本文件
- 输入-输出作业

## 流

C 语言本身没有用于执行 I/O 操作的任何特殊语句。所有 I/O 操作都必须通过对标准 I/O 库的函数调用来完成。

```
#include <stdio.h>
```

它包含与标准 I/O 库相关的声明和宏定义。

每个程序在开始执行时都可以访问三个数据文件流：一个用于输入，两个用于输出：

```
stdin (standard input) – the usual source of input characters (keyboard)
stdout (standard output) – the usual destination for output characters (screen)
stderr (standard error output) – where error messages are sent (screen)
```

可以通过在命令行执行程序时添加重定向请求，使相同的程序将其标准输出写入文件而不是终端：

```
foo > outFile.txt
```

这将创建一个包含 foo 输出的文件。printf() 显示的任何值都不会显示在终端上，而是会写入名为 outFile.txt 的文件中。如果有任何错误消息，它们将继续显示在终端窗口上，而不是被埋在输出文件内部。

![](img/0603fdf2eefeabaf26542250cc2fb439_198_0.png)

标准输入也可以进行类似的重定向。任何通常从终端读取数据的函数调用，例如 getchar() 和 scanf()，都可以改为从文件读取信息。例如，我们可以使用存储在名为 inFile.txt 的文件中的数据来运行程序 foo：

```
foo < inFile.txt
```

![](img/0603fdf2eefeabaf26542250cc2fb439_199_1.png)

最后，我们可以同时结合输入重定向和输出重定向：

```
foo < inFile.txt > outFile.txt
```

![](img/0603fdf2eefeabaf26542250cc2fb439_200_0.png)

### getchar()

I/O 并非 C 语言本身的一部分，而是编写大多数程序所需的基本扩展。

getchar() 从标准输入（键盘）返回下一个字符，并将其作为函数返回值返回。如果没有更多输入，则改为返回 EOF（文件结束）。因此，在使用之前，通常会将 getchar() 返回的值与 EOF 进行比较。

在程序执行过程中的某个时刻，用户可以通过输入 ^z（控制 Z）（或在某些环境中输入 ^d）来指示“没有更多输入”，此时 getchar() 将返回 EOF。

getchar() 和 EOF 定义在名为 stdio.h 的标准头文件中，我们必须在所有编译中包含它：

```
#include <stdio.h>
```

某些 C 表达式成为我们的标准词汇，例如：

```
while ( (c = getchar()) != EOF)
```

此表达式用于从标准输入一次获取一个字符的循环开头。请仔细查看该表达式，并注意那对“额外”的括号。你能弄清楚为什么需要它们吗？

接下来，考虑以下两者之间的区别：

```
while (c = getchar())
and
while (c == getchar())
```

要看出区别可能需要很长时间，有时甚至需要更长时间来决定你真正想要哪一个！

下面是一个程序，用于统计从输入流读取的字符数，直到遇到 EOF：

```
// count1.c
#include <stdio.h>
int main(void) {
    int c, count = 0;
    while ((c = getchar()) != EOF) {
        ++count;
    }
    printf("%d\n", count);
    return 0;
}
```

请注意，c 被声明为 int 而不是 char。这是因为 EOF 被赋予定义的值 -1。在某些机器上，char 只能是正值，因此为了返回 -1，我们将 c 定义为 int。

我们可以用 for 语句替换上面的 while 语句：

```
// count2.c
#include <stdio.h>
int main(void) {
    int count;
    for (count = 0; getchar() != EOF; ++count) {
        ;
    }
    printf("%d\n", count);
    return 0;
}
```

我们也可以统计换行符：

```
// count3.c

#include <stdio.h>

void main(void) {
    int c, count = 0;

    while ((c = getchar()) != EOF) {
        if (c == '\n') {
            ++count;
        }
    }

    printf("%d\n", count);
    return 0;
}
```

下面是一个将程序输入映射为小写的程序：

```
// map1.c

#include <stdio.h>
#include <ctype.h>

void main(void) {
    int c;

    while ((c = getchar()) != EOF) {
        printf("%c", isupper(c) ? tolower(c) : c);
    }

    return 0;
}
```

下面是一个表达式，用于跳过输入流中的空白字符：

```
// skipBlanks.c

while ((c = getchar()) == ' ') {
    ;
}
