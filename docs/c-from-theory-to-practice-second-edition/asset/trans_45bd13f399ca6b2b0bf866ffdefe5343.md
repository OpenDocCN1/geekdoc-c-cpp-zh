
```
printf("This\tis\ta\x9text\n"); /* The hexadecimal number 9 corresponds to the horizontal tab. */
printf("This is a \"text\"\n");
printf("This is a \\text\\\n");
printf("Sample\rtext\n");
return 0;
}
```

程序输出：

```
(Hear a beep).
This    is    a    text
This is a "text"
This is a \text\
textle
```

在最后一个 printf() 中，\r 将光标移回行首，Samp 被覆盖，并打印 text。因此，输出为 textle。

如果你希望提高可读性，将 printf() 的格式字符串扩展到多行，请使用反斜杠。例如，下面的 printf() 写在三行上，但输出将显示在一行中。

```
printf("This printf uses three lines, but the \
text will appear \
on one line ");
```

## 转换说明

转换说明以 % 字符开头，后面跟一个或多个具有特殊含义的字符。在其最简单的形式中，% 后面跟表 2.3 中列出的转换说明符之一。

下面的程序演示了如何使用 printf() 以各种格式打印字符和数字。

```
#include <stdio.h>
int main(void)
{
    int len;
    printf("%c\n", 'w');
    printf("%d\n", -100);
    printf("%f\n", 1.56);
    printf("%s\n", "some text");
    printf("%e\n", 100.25);
    printf("%g\n", 0.000123);
    printf("%X\n", 15);
    printf("%o\n", 14);
    printf("test%n", &len);
    printf("%d%%\n", 100);
    return 0;
}
```

### 表 2.3 转换说明符

| 转换说明符 | 含义 |
| :--- | :--- |
| c | 显示与无符号整数值对应的字符。 |
| d, i | 显示有符号整数。 |
| u | 显示无符号整数。 |
| f | 显示浮点数。默认精度为六位数字。 |
| s | 显示字符序列。 |
| e, E | 以科学记数法显示浮点数。指数前带有选定的说明符 e 或 E。 |
| g, G | 如果指数小于 -4 或大于等于精度，则选择 %e 或 %E 形式；否则使用 %f 形式。 |
| p | 显示指针变量的值。 |
| x, X | 以十六进制形式显示无符号整数；%x 显示小写字母（a–f），而 %X 显示大写字母（A–F）。 |
| o | 以八进制显示无符号整数。 |
| n | 不显示任何内容。对应参数必须是指向整数的指针；到目前为止已打印的字符数将存储在该整数中。 |
| % | 显示字符 %。 |

程序输出：

- w（字符常量必须用单引号括起来）。
- -100
- 1.560000
- some text（字符串字面量必须用双引号括起来）。
- 1.002500e+002（等价于 1.0025 × 10² = 1.0025 × 100 = 100.25）。
- 1.23e-005（因为指数小于 -4，所以该数以科学记数法显示）。
- F（数字 15 等价于十六进制的 F）。
- 16（数字 14 等价于八进制的 16）。
- test（由于在遇到 %n 之前已打印四个字符，因此值 4 被存入 len。我们将在第 8 章讨论 & 运算符）。
- 100%（要显示 % 字符，必须写两次）。

## 返回值

printf() 返回已打印的字符数；如果发生错误，则返回负值。例如，考虑下面的程序：

```c
#include <stdio.h>
int main(void)
{
    printf("%d\n", printf("Test\n"));
    return 0;
}
```

## 可选字段

如前所述，最简单的转换说明以 % 字符开头，后面跟转换说明符。然而，转换说明在二者之间最多可以包含四个可选字段，如图 2.1 所示。本节将逐一回顾这些字段。

## 精度

精度取决于转换说明符，如下所示：

- d、i、o、u、x、X：指定输出数字的最小位数。如果数字位数较少，则添加前导零。
- e、E、f：指定小数点后的位数。
- g、G：指定有效数字的最大位数。
- s：指定输出字符的最大数量。

精度用点（.）指定，后面可以跟一个整数，或者在参数列表中用星号 * 和一个整数来指定精度。如果只出现点，则精度为零。例如，让我们使用各种精度显示一个浮点变量的值。默认精度为六位数字。输出值根据截断位的值向上或向下舍入。如果小于 5，则输出值向下舍入；否则向上舍入。

```
#include <stdio.h>
int main(void)
{
    float a = 1.2365;

    printf("%f\n", a);
    printf("%.2f\n", a);
    printf("%.*f\n", 3, a);
    printf("%.f\n", a);
    return 0;
}
```

![](img/b8da5dcf9ba7f1fad5213c453d095246_45_0.png)

图 2.1 转换说明。

说明：我们将在第 4 章看到，% 运算符用于求两个整数操作数相除的余数。其他运算符的用法与数学中相同。由于强制类型转换表达式 (double)i 将 i 的类型从 int 转换为 double，所以它们相除的结果是浮点数。如果省略强制类型转换并写成 i/j，则应使用 %d 而不是 %f，因为除法结果是整数。在这种情况下，程序将输出整数结果，即 2。注意，我们可以用一个 printf() 打印所有值。例如：

```
printf("%d %d %d %f %d\n", i+j, i-j, i*j, (double)i/j, i%j);
```

甚至：

```
printf("%d-%d=%d, %d-%d=%d, %d*%d=%d, %d/%d=%f, %d%%%d=%d\n", i, j, i+j, i, j, i-j, i, j, i*j, i, j, (double)i/j, i, j, i%j);
```

## C.2.4 下面的程序显示两个浮点数的平均值。这段代码中有错误吗？

```
#include <stdio.h>
int main(void)
{
    double i = 12, j = 5, avg;
    
    avg = i+j/2;
    printf("Avg = %.2f\n", avg);
    return 0;
}
```

答案：是的，有一个错误。因为除法运算符 / 的优先级高于加法运算符 +，所以先执行除法 5/2 = 2.5，然后执行加法 12+2.5，这导致程序显示错误值 14.50，而不是 8.50。通过将表达式 i+j 括在括号中可以消除这个错误。如附录 A 所示，因为括号在所有 C 运算符中优先级最高，所以先执行括号内的表达式。因此，正确的赋值是 avg = (i+j)/2。

## C.2.5 下面程序的输出是什么？

```
#include <stdio.h>
int main(void)
{
    int k;
    float i = 10.9, j = 20.3;
    
    k = (int)i + j;
    printf("%d %d\n", k, (int)(i + (int)j));
    return 0;
}
```

答案：强制类型转换表达式 (int)i 将 i 的类型从 float 转换为 int。由于 (int)i 的结果是 10，因此有 k = 10+20.3 = 30（不是 30.3，因为 k 是 int）。 (int)(i+(int)j) 的结果是 (int)(10.9+(int)20.3) = (int)(10.9+20) = (int)(30.9) = 30。因此，程序输出：30 30。

## U.2.2 修复错误，使程序能够运行并显示 m 的值。

```c
#include <stdio.h>
int main(void);
{
    int m;
    a = 10
    m = 2a+100
    printf("%f\n", m);
    return0;
}
```

## U.2.3 修复错误，使程序能够运行并显示 a、b 和 c 的值。

```c
#include <studio.h>
int main(void)
{
    int b = a/2; a = 10
    float c = 4,5 + a;
    printf("%d %d\n", a, c, b);
    return 0;
}
```

## U.2.4 修复错误，使程序能够运行并显示 a 与 b 的和。

```c
#include (stdio.h)

#define NUM 30;

int main(void)
{
    const int a;
    a = 10;
    NUM = a+2;
    a = NUM/2;
    b = a;
    printf('\n', a+b);
    return 0;
}
```

## U.2.5 编写一个程序，将两个负值赋给两个整型变量，并使用这些变量显示对应的正值。

## U.2.6 填空并完成程序，以显示以下输出。

```
21
21
15
25%
A
a
```

