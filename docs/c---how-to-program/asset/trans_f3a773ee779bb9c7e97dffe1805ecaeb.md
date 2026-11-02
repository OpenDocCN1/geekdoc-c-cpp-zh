

- 2. 从输入流中输入特定字符。
- 3. 跳过输入流中的特定字符。

## 9.11.1 scanf 语法

函数 scanf 的书写形式如下：

```
scanf(format-control-string, other-arguments);
```

format-control-string 描述输入的格式，other-arguments 是指向变量的指针，输入的数据将存储在这些变量中。

> **良好编程实践 9.1**
> 输入数据时，每次提示用户输入一个或少数几个数据项。避免要求用户在单个提示下输入大量数据项。

> **良好编程实践 9.2**
> 始终考虑当（而非如果）输入了错误数据时，用户和你的程序将如何处理——例如，在程序上下文中无意义的整数值，或缺少标点或空格的字符串。

## 9.11.2 scanf 转换说明符

图 9.17 总结了用于输入所有类型数据的转换说明符。本节其余部分提供了演示如何通过各种 scanf 转换说明符读取数据的程序。请注意，d 和 i 转换说明符在 scanf 输入时具有不同的含义，而在 printf 输出时它们可以互换使用。

| 转换说明符 | 描述 |
|---|---|
| *整数* | |
| d | 读取一个可选带符号的十进制整数。对应的参数是一个指向 int 的指针。 |
| i | 读取一个可选带符号的十进制、八进制或十六进制整数。对应的参数是一个指向 int 的指针。 |
| o | 读取一个八进制整数。对应的参数是一个指向 unsigned int 的指针。 |
| u | 读取一个无符号十进制整数。对应的参数是一个指向 unsigned int 的指针。 |
| x 或 X | 读取一个十六进制整数。对应的参数是一个指向 unsigned int 的指针。 |
| h、l 和 ll | 放置在任何一个整数转换说明符之前，分别表示要输入 short、long 或 long long 整数。 |
| *浮点数* | |
| e、E、f、g 或 G | 读取一个浮点值。对应的参数是一个指向浮点变量的指针。 |
| `l` 或 `L` | 放置在任何一个浮点转换说明符之前，表示要输入 double 或 long double 值。对应的参数是一个指向 double 或 long double 变量的指针。 |
| *字符和字符串* | |
| `c` | 读取一个字符。对应的参数是一个指向 char 的指针；不添加空字符（`'\0'`）。 |
| `s` | 读取一个字符串。对应的参数是一个指向 char 类型数组的指针，该数组必须足够大以容纳字符串和自动添加的终止空字符（`'\0'`）。 |
| *扫描集* | |
| `[scan characters]` | 在输入流中扫描一个字符集合，并将其存储在数组中。 |
| *其他* | |
| `p` | 读取一个地址，其形式与在 `printf` 语句中使用 `%p` 输出地址时所产生的形式相同。 |
| `n` | 存储在本次 `scanf` 调用中到目前为止已输入的字符数。对应的参数必须是指向 int 的指针。 |
| `%` | 跳过输入中的百分号（`%`）。 |

**图 9.17** | scanf 的转换说明符。

## 9.11.3 使用 scanf 读取整数

图 9.18 使用各种整数转换说明符读取整数，并将这些整数以十进制数形式显示。转换说明符 `%i` 可以输入十进制、八进制和十六进制整数。

```c
// Fig. 9.18: fig09_18.c
// 使用整数转换说明符读取输入
#include <stdio.h>

int main(void)
{
   int a;
   int b;
   int c;
   int d;
   int e;
   int f;
   int g;

   puts("Enter seven integers: ");
   scanf("%i%i%i%i%i%i%i", &a, &b, &c, &d, &e, &f, &g);

   puts("\nThe input displayed as decimal integers is");
   printf("%d %d %d %d %d %d %d\n", a, b, c, d, e, f, g);
}
```

```
Enter seven integers:
-70 -70 070 0x70 70 70 70

The input displayed as decimal integers is:
-70 -70 56 112 56 70 112
```

**图 9.18** | 使用整数转换说明符读取输入。

## 9.11.4 使用 scanf 读取浮点数

输入浮点数时，可以使用浮点转换说明符 e、E、f、g 或 G 中的任意一个。图 9.19 读取三个浮点数，分别使用三种类型的浮点转换说明符，并使用转换说明符 f 显示所有三个数。

```c
// Fig. 9.19: fig09_19.c
// 使用浮点转换说明符读取输入
#include <stdio.h>

// 函数 main 开始程序执行
int main(void)
{
   double a;
   double b;
   double c;

   puts("Enter three floating-point numbers:");
   scanf("%le%lf%lg", &a, &b, &c);

   printf("\nHere are the numbers entered in plain:");
   puts("floating-point notation:\n");
   printf("%f\n%f\n%f\n", a, b, c);
}
```

```
Enter three floating-point numbers:
1.27987 1.27987e+03 3.38476e-06

Here are the numbers entered in plain floating-point notation:
1.279870
1279.870000
0.000003
```

**图 9.19** | 使用浮点转换说明符读取输入。

## 9.11.5 使用 scanf 读取字符和字符串

字符和字符串分别使用转换说明符 c 和 s 输入。图 9.20 提示用户输入一个字符串。程序使用 %c 输入字符串的第一个字符并将其存储在字符变量 x 中，然后使用 %s 输入字符串的其余部分并将其存储在字符数组 y 中。

```c
// Fig. 9.20: fig09_20.c
// 读取字符和字符串
#include <stdio.h>

int main(void)
{
    char x;
    char y[9];

    printf("%s", "Enter a string: ");
    scanf("%c%*s", &x, y);

    puts("The input was:\n");
    printf("the character \"%c\" and the string \"%s\"\n", x, y);
}
```

```
Enter a string: Sunday
The input was:
the character "S" and the string "unday"
```

**图 9.20** | 读取字符和字符串。

## 9.11.6 在 scanf 中使用扫描集

可以使用扫描集输入一个字符序列。扫描集是用方括号 [] 括起来的一组字符，并且在格式控制字符串中由百分号引导。扫描集扫描输入流中的字符时，只寻找与扫描集中包含的字符相匹配的字符。每当一个字符匹配时，它就被存储在扫描集对应的参数中——即指向字符数组的指针。当遇到一个不在扫描集中的字符时，扫描集停止输入字符。如果输入流中的第一个字符与扫描集中的字符不匹配，则数组不会被修改。图 9.21 使用扫描集 [aeiou] 扫描输入流中的元音。请注意，输入的前七个字母被读取。第八个字母（h）不在扫描集中，因此扫描终止。

```c
// Fig. 9.21: fig09_21.c
// 使用扫描集
#include <stdio.h>

// 函数 main 开始程序执行
int main(void)
{
    char z[9]; // 定义数组 z

    printf("%s", "Enter a string: ");
    scanf("%[aeiou]", z); // 搜索字符集合

    printf("The input was \"%s\"\n", z);
}
```

```
Enter a string: oeeooahah
The input was "oeeooa"
```

**图 9.21** | 使用扫描集。

扫描集也可以通过使用反向扫描集来扫描不在扫描集中的字符。要创建反向扫描集，请在方括号内、扫描字符之前放置一个脱字符（^）。这将导致存储不出现在扫描集中的字符。当遇到包含在反向扫描集中的字符时，输入终止。图 9.22 使用反向扫描集 [^aeiou] 来搜索辅音——更准确地说是搜索“非元音”。

```c
// Fig. 9.22: fig09_22.c
// 使用反向扫描集
#include <stdio.h>

int main(void)
{
    char z[9];

    printf("%s", "Enter a string: ");
    scanf("%[^aeiou]", z); // 反向扫描集

    printf("The input was \"%s\"\n", z);
}
```

```
Enter a string: String
The input was "Str"
```

**图 9.22** | 使用反向扫描集。

## 9.11.7 在 scanf 中使用字段宽度

可以在 scanf 转换说明符中使用字段宽度来从输入流中读取特定数量的字符。图 9.23 输入一系列连续的数字，前两位作为两位数整数，其余数字作为另一个整数。

```c
// Fig. 9.23: fig09_23.c
// 使用字段宽度输入数据
#include <stdio.h>

int main(void)
{
```

**图 9.23** | 使用字段宽度输入数据。

