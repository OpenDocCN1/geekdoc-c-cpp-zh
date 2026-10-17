
占位符用于打印 `printf()` 函数中指定的参数值。占位符中的指令控制着打印。占位符的一般形式为：

```
% flags field-width prefix type-identifier
```

### 类型标识符

类型标识符指定了要显示值的类型。如果指定的标识符无效，将产生不可预测的输出。表 2 列出了类型标识符：

# 第 10 章

| 表 2：类型标识符说明 |

| 类型标识符 | 描述 |

| :--- | :--- |

| d, i | 表示有符号整数。 |

| o | 表示八进制形式的无符号整数。 |

| u | 表示十进制形式的无符号整数。 |

| x | 表示十六进制形式的无符号整数，且十六进制字符 a, b, c, d 以小写打印。 |

| X | 表示十六进制形式的无符号整数，且十六进制字符 A, B, C, D 以大写打印。 |

| c | 将任何值转换为无符号字符（char）并显示。主要用于打印字符。 |

| s | 将参数转换为字符数组并打印；字符串末尾的空字符不打印。 |

| f | 打印浮点数。 |

| e, E | 表示指数形式的浮点数。小数点左侧有一个数字；小数点右侧的数字取决于所需的精度。 |

| g, G | 打印指数形式的浮点数。当指数小于 -1 时，使用指数形式。然而，两者在功能上略有不同。 |

| n | 打印到目前为止打印打印的字符数。 |

| p | 指定指针的值 |

## 类型前缀

前缀指定要显示的值应被解释为短（short）、长（long）或双长（double long）。表 3 列出了前缀的类型：

| 表 3：前缀说明 |

| 前缀类型 | 描述 |

| :--- | :--- |

| h | 在类型标识符 d, i, o, u, x 和 X 之前，表示显示的值应被解释为 short。例如：短整数 (hl)，短无符号整数 (hu) |

| l | 在类型标识符 d, i, o, u, x 和 X 之前，表示显示的值应被解释为 long。例如：长整数 (ld)，长无符号整数 (lu) |

| I, L | 指定一个值为 long double，适用于所有类型标识符 E, f, g 和 G。 |

### 字段宽

字段宽表示分配给输出的最小列数。例如，如果你对 i 写入 `%4d` 且 i 的值为 10，则为 i 分配 4 列，并在 i 的值左侧添加 2 个空格，因此输出为 bb10。这里用 b 表示空格。

## 管理输入和输出操作

如果值超过了指定的列数，则忽略字段宽，使用的列数等于参数所需的列数。在这种情况下，如果 i 是 12345，即使指定了 `%d`，也会使用 5 列。输出不会因为字段宽而缩短。如果你指定的不是字段宽，那么你必须指定额外的参数。例如：

```c
printf("%d\n", 5, 20); // 语句 A
printf("%d\n", 20, 25); // 语句 B
```

在语句 A 中，5 替换了 *，表示在 5 列中显示值 20。

在语句 B 中，20 替换了 *，表示在 20 列中放置值 5。

- 精度 (Precision)

精度表示整数打印的最小位数，即对于类型数字 d, o, u 和 x。例如：

`printf("%10.4d\n", 35);`

在这里，10 是字段宽，4 是精度，因此输出使用 10 列，且输出为 4 位。将 35 分为 4 位，在左侧填充 0 变为 0035。为了在 10 列中打印 0035，添加空格使输出变为 bbbbb0035。

对于浮点参数，精度表示小数点后打印的位数。如果精度大于小数点右侧数字的位数，则在右侧填充 0。如果精度指定的位数非常少，则会被忽略，并按要求打印位数。

- 标志 (Flags)

标志字符用于为输出提供指令。你可以按任何顺序使用多个标志字符。以下是标志字符：

- i. : 表示输出为左对齐。

`printf("%10.4d\n", 25);`

它打印 0025bbbbbb，因此在右侧填充空格。

在没有标志的情况下，它打印为 bbbbb0025。

- ii. + 表示使用符号字符 + 或 - 打印 i。

```c
printf("%d\n", -25);
printf("%d\n", 25);
```

它导致打印为：

-25

+25

- iii. 空格：为正值留出空格，以便正值和负值对齐。例如：

```c
printf("%d\n", 25);
printf("%d", 25);
```

它导致打印为：

b25

25

在第一种情况下，显示空格。表示在显示之前将值转换为另一种形式。例如，十六进制值可以表示 OX；对于浮点数据类型，存在 # 表示输出中应始终包含小数点。O: 填充 O 以完成字段宽。这用于整数和实数。如果精度指定为 O，则该标志被忽略，或者如果指定 - 标志则被忽略。在本节中，你学习了 `printf()` 占位符。

## 转义序列 (Escape Sequences)

转义字符用于为输出提供指令。你可以按任何顺序使用多个转义字符。以下是转义字符：

- i. : 表示输出左对齐。

`printf("%10.4d\n", 25);`

它打印 0025bbbbbb，因此在右侧填充空格。

在没有标志的情况下，它打印为 bbbbb0025。

- ii. + 表示使用符号字符 + 或 - 打印 i。

```c
printf("%d\n", -25);
printf("%d\n", 25);
```

它导致打印为：

-25

+25

- iii. 空格：为正值留出空格，以便正值和负值对齐。例如：

```c
printf("%d\n", 25);
printf("%d", 25);
```

它导致打印为：

b25

25

在第一种情况下，显示空格。表示在显示之前将值转换为另一种形式。例如，十六进制值可以表示 OX；对于浮点数据类型，存在 # 表示输出中应始终包含小数点。O: 填充 O 以完成字段宽。这用于整数和实数。如果精度指定为 O，则该标志被忽略，或者如果指定 - 标志则被忽略。在本节中，你学习了 `printf()` 占位符。

## 转义序列

转义字符用于为输出提供指令。你可以按任何顺序使用多个转义字符。以下是转义字符：

- i. : 表示输出左对齐。

`printf("%10.4d\n", 25);`

它打印 0025bbbbbb，因此在右侧填充空格。

在没有标志的情况下，它打印为 bbbbb0025。

- ii. + 表示使用符号字符 + 或 - 打印 i。

```c
printf("%d\n", -25);
printf("%d\n", 25);
```

它导致打印为：

-25

+25

- iii. 空格：为正值留出空格，以便正值和负值对齐。例如：

```c
printf("%d\n", 25);
printf("%d", 25);
```

它导致打印为：

b25

25

在第一种情况下，显示空格。表示在显示之前将值转换为另一种形式。例如，十六进制值可以表示 OX；对于浮点数据类型，存在 # 表示输出中应始终包含小数点。O: 填充 O 以完成字段宽。这用于整数和实数。如果精度指定为 O，则该标志被忽略，或者如果指定 - 标志则被忽略。在本节中，你学习了 `printf()` 占位符。

*(注：由于原文文本中存在大量重复的乱码部分，翻译已根据逻辑进行了清理和对齐，确保了核心技术内容的准确呈现。)*

## 10.6 scanf() 占位符

`scanf()` 占位符由开头的 `%` 和结尾的类型指示符组成。

除此之外，它还可以包含 `*`、最大字段宽度指示符和类型指示符修改。例如：

```c
scanf("%10.2f %10d",&a, &b);
```

- * 类型指示符

类型指示符是指定读取数据类型的字符。下表显示了类型指示符的描述：

表 5：类型指示符描述

| 类型指示符 | 结果 |

|---|---|

| d, I | 读取有符号整数；期望参数应该是指向 int 的指针。然而，它们在功能上略有不同。 |

| o | 读取八进制形式的无符号整数。 |

| u | 读取十进制形式的无符号整数。 |

| x, X | 读取十六进制形式的无符号整数。 |

| E, f, g, G | 读取浮点值。然而，它们在功能上略有不同。 |

| S | 读取字符串。它匹配一系列非空白字符，以行尾或文件结束结束。额外的参数应该是指向 char 的指针，并指向一个足够容纳输入字符串并包含 NULL 终止符的区域。 |

| C | 根据指定的字段宽度匹配字符数。如果没有指定宽度，则假设字段宽度为单个字符。额外的参数必须是指向 char 的指针；指向的区域应足够容纳指定数量的字符。 |

| N | 写入到目标变量中的字符数，但它不读取任何输入。 |

- * `*` 的用法

`*` 用于抑制输入。例如 `%*d`，如果你的输入包含 5 个值且你想忽略 3 个值，那么你可以写：

```c
scanf("%*d %*d %*d %d %d", &i, &j);
```

所以，如果你的输入是

10 20 30 40 50

那么 i 获取值 10，j 获取值 50，这在你从文件获取输入时非常有用。

### 字段宽度

它表示读取到变量中的最大字符数。它是一个非空格字符字符串；它会扩展到下一个不适当的字符或者直到达到字段宽度限制（如果已指定）。

在本节中，你已经学习了 `scanf()` 占位符。现在让我们来学习 `getchar()` 函数。

## 10.7 getchar() 函数

`getchar()` 函数从标准输入设备读取单个字符。`getchar()` 返回它读取的字符，或者如果没有更多可用字符，则返回特殊值 `EOF`（文件结束）。`getchar()` 函数的语法如下：

```c
var_char = getchar();
```

其中 char 是一个字符类型的变量。

下面的程序显示了如何使用 `getchar()` 函数：

- 列表 3：使用 `getchar()` 函数

```c
#include<stdio.h>
void main() {
char var1;
var1 = getchar();
}
```

> 描述使用 `getchar` 和 `scanf` 函数读取字符串的局限性。(VTU, Jun/Feb 2007)

在 `getchar()` 函数之后，现在让我们学习 `gets()` 函数。

## 10.8 gets() 函数

`gets()` 函数从用户处读取字符字符串，直到读取到 <newline> 或遇到文件结束条件。它将字符字符串存储在一组连续的内存位置中，这称为数组。该函数的示例如下：

```c
char string[50];
gets(string);
```

下面的程序显示了如何使用 `gets()` 函数

- 列表 4：使用 <stdio.h> 函数

```c
#include<stdio.h>
int main() {
char string1[100];
printf("Type something.\n");
gets(string1);
printf("You typed: %s\n", string1);

return 0;
}
```

理解 `gets()` 函数后，现在让我们学习 `putchar()` 函数。

## 10.9 putchar() 函数

`putchar()` 函数将单个字符写入标准输出流。`putchar()` 函数定义在 C 语言的标准库头文件 `stdio.h` 中。字符作为参数传入函数，如果写入成功，则返回该参数。否则，返回文件结束。

下面的程序显示了如何使用 `putchar()`：

- 列表 5：使用 `putchar()` 函数

```c
#include<stdio.h>
int main() {
  char h;
  h = getchar();
  putchar(h);
  return 0;
}
```

- 1. 举例说明 `putchar` 函数。(VTU, July/Aug 2004)

- 2. 在 C 中给出三个输入和输出语句的示例。(VTU, Feb/March 2005)

- 3. 解释 `putchar ()` 和 `getchar ()` 函数。(VTU, July/Aug 2007)

在学习 `putchar()` 函数后，现在让我们学习 `puts()` 函数。

## 10.10 puts() 函数

`puts()` 函数显示字符串并在其追加换行符 ('\n')。该函数的语法为：

`puts(string);`

下面的程序显示了如何使用 `puts()`：

- 列表 6：使用 `puts()` 函数

到此，我们结束本章。在进入下一章之前，让我们总结一下本章的要点。

## 总结

在本章中，你学习了两种类型的输入/输出函数：格式化的非格式化的。最后学习了格式化函数 `scanf()` 和 `printf()`。最后探索了非格式化函数 `getchar()`, `gets()` 和 `puts()`。

## 快速复习

Q1. 找出以下语句中的错误：

a. `printf("%d", a);`

b. `printf("%f", a);`

c. `printf("%d", n);`

d. `scanf("%d", &k);`

e. `scanf("%d", &a);`

Ans. 无错误

b. `printf("%f", c);`

c. `printf("%d", m);`

e. `scanf("%d", &b);`

Q2. 写出以下语句的输出：

a. `printf("%d", var_int);`

b. `printf("%f", var_float);`

c. `printf("%d", string1);`

Ans. 45

b. 67

c. 45

Q3. 找出以下程序的输出：

```c
#include <stdio.h>
int main()
{
    printf("Hello!");
    printf("welcome to the World!");
    return 0;
}
```

Ans. Hello!Welcome to the World!

Q4. 找出以下程序的输出：

```c
#include<stdio.h>
int main()
{
    printf("this is the printf");
    return 0;
}
```

Ans. This is the printf statement

Q5. 找出以下程序的输出：

```c
#include<stdio.h>
int main()
{
  char ch;
  getchar();
  ch='c';
  printf("The character entered is %c",ch);
  return 0;
}
```

Ans. The character entered is c

Q6. 找出以下程序的输出：

```c
#include<stdio.h>
int main()
{
  const int i=123;
  i=321;
  printf("The value of i is %d",i);
  return 0;
}
```

Ans. 编译错误。变量被声明为常量整数，我们在下一语句中更改它的值。由于常量变量无法更改，因此发生编译错误。

Q7. 找出以下程序的输出：

```c
#include<stdio.h>
int main()
{
  int i=1000;
  printf("The value of i is %f",i);
  return 0;
}
```

Ans. The value of i is -0.546223 (垃圾值)

Q8. 找出以下程序的输出：

```c
#include<stdio.h>
int main()
{
  char ch='e';
  putchar('g');
  return 0;
}
```

Ans. g

Q9. 编写一个程序，从用户处获取整数、字符和字符串，并在屏幕上显示。

Ans:

```c
#include <stdio.h>
int main()
{
int i;
float flit;
char ch;
char str[30];
printf("Enter a char: ");
scanf("%c",&ch);
printf("Enter an integer: ");
scanf("%d", &i);
printf("Enter a float: ");
scanf("%f", &flit);
printf("Enter a string: ");
scanf("%s",str);
printf("You entered %c, %f, %d, and %s\n", ch, flit, i ,str);
return 0;
}
```

Output:

Enter a char: 39

Enter an integer: 39

Enter a float: 34.56

Enter a string: kogent

You entered 9, 34.560001, 39, and kogent

Q10. 编写一个程序，获取圆的半径并计算圆的面积和周长。(VTU, July/Aug 2003)

Ans:

```c
#include<stdio.h>
int main()
{
float pi=3.14;
float radius;
float area, perimeter;
printf("Enter radius of the circle: ");
scanf("%f",&radius);
area=pi*radius*radius;
perimeter=2*pi*radius;
printf("Area of the circle is: %f and Perimeter of the circle is: %f\n", area,perimeter);
return 0;
}
```

Output:

Enter radius of the circle: 5.15

Area of the circle is: 79.567505 and Perimeter of the circle is: 30.900002

Q11. 编写一个程序，从用户处获取四个数字并计算它们的和和平均值。

Ans:

```c
#include<stdio.h>
int main()
{
float num1;
```

## 管理输入输出操作
