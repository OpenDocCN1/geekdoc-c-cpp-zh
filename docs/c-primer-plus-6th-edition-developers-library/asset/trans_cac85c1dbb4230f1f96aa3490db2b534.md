

## 常量与 C 预处理器

有时你在程序中需要使用一个常量。例如，你可以这样给出圆的周长：

```
circumference = 3.14159 * diameter;
```

这里，常量 3.14159 代表世界闻名的常数 pi（π）。要使用一个常量，只需像示例中那样输入实际值即可。然而，使用符号常量是有充分理由的。也就是说，你可以使用如下语句，让计算机稍后代入实际值：

```
circumference = pi * diameter;
```

为什么使用符号常量更好？首先，名称比数字提供的信息更多。比较下面两个语句：

```
owed = 0.015 * housevalue;
owed = taxrate * housevalue;
```

如果你阅读一个长程序，第二种版本的含义更清晰。

另外，假设你已在多个地方使用了某个常量，并且有必要更改其值。毕竟，税率确实会变化。那么你只需要修改符号常量的定义，而不必在程序中查找并更改常量的每一个出现位置。

好吧，如何设置符号常量？一种方法是声明一个变量并将其设为所需常量。你可以这样写：

```
float taxrate;
taxrate = 0.015;
```

这提供了符号名称，但 taxrate 是一个变量，因此你的程序可能会意外更改其值。幸运的是，C 有几种更好的方法。

最初的更好方法是 C 预处理器。在第 2 章“介绍 C”中，你看到预处理器如何使用 #include 来合并来自另一个文件的信息。预处理器还允许你定义常量。只需在包含程序的文件顶部添加如下行：

```
#define TAXRATE 0.015
```

当你的程序被编译时，值 0.015 将在你使用 TAXRATE 的每个地方被替换。这称为编译时替换。到程序运行时，所有替换都已完成（见图 4.5）。这种定义的常量通常被称为显式常量。

```
#define TAXRATE 0.015
int main(void)
{
  
  
  
  bill=TAXRATE * sum;
{
  
  
  
}
```

你输入的内容

```
int main(void)
{
  
  
  
  bill=0.015 * sum;
  
  
  
}
```

预处理器
工作时

编译器

图 4.5 你输入的内容与编译的内容。

注意格式。首先是 #define。接下来是常量的符号名（TAXRATE），然后是常量的值（0.015）。（注意此构造不使用 = 号。）因此一般形式如下：

```
#define NAME value
```

你可以用你选择的符号名替换 NAME，并用适当的值替换 value。不使用分号，因为这是由预处理器处理的替换机制，而不是 C 语句。为什么 TAXRATE 是大写的？将常量以大写形式书写是合理的 C 传统。然后，当你在程序深处遇到它时，你立刻知道它是一个常量，而不是变量。将常量大写只是使程序更易读的另一种技巧。如果你不将常量大写，你的程序仍然可以工作，但养成大写常量的习惯是合理的。

其他较少见的命名约定包括在名称前加上 c_ 或 k_ 以表示常量，产生诸如 c_level 或 k_line 之类的名称。

你为符号常量使用的名称必须满足与变量名称相同的规则。你可以使用大写和小写字母、数字和下划线字符。第一个字符不能是数字。清单 4.4 显示了一个简单示例。

## 清单 4.4 pizza.c 程序

```
/* pizza.c -- uses defined constants in a pizza context */
#include <stdio.h>
#define PI 3.14159
int main(void)
{
    float area, circum, radius;

    printf("What is the radius of your pizza?\n");
    scanf("%f", &radius);
    area = PI * radius * radius;
    circum = 2.0 * PI *radius;
    printf("Your basic pizza parameters are as follows:\n");
    printf("circumference = %1.2f, area = %1.2f\n", circum, area);
    return 0;
}
```

printf() 语句中的 %1.2f 会使打印结果四舍五入到小数点后两位。当然，这个程序可能并不反映你主要的披萨关注点，但它确实在披萨程序世界中填补了一个小 niche。以下是示例运行：

```
What is the radius of your pizza?
6.0
Your basic pizza parameters are as follows:
circumference = 37.70, area = 113.10
```

#define 语句也可以用于字符和字符串常量。只需对前者使用单引号，对后者使用双引号。以下示例均有效：

```
#define BEEP '\a'
#define TEE 'T'
#define ESC '\033'
#define OOPS "Now you have done it!"
```

记住，符号名之后的所有内容都会被替换为它。不要犯这个常见错误：

```
/* the following is wrong */
#define TOES = 20
```

如果你这样做，TOES 会被替换为 = 20，而不是仅仅 20。在这种情况下，像这样的语句

```
digits = fingers + TOES;
```

会被转换为以下错误表示：

```
digits = fingers + = 20;
```

## const 修饰符

C90 增加了一种创建符号常量的第二种方法——使用 const 关键字将变量声明转换为常量声明：

```
const int MONTHS = 12;    // MONTHS a symbolic constant for 12
```

这使 MONTHS 成为只读值。也就是说，你可以显示 MONTHS 并在计算中使用它，但不能更改 MONTHS 的值。这种更新的方法比使用 #define 更灵活；它允许你声明类型，并更好地控制程序的哪些部分可以使用该常量。第 12 章“存储类、链接和内存管理”讨论了 const 的这种和其他用途。

实际上，C 还有第三种创建符号常量的方法，那就是第 14 章“结构和其他数据形式”中讨论的 enum 设施。

## 工作中的显式常量

C 头文件 limits.h 和 float.h 分别提供有关整数类型和浮点类型的大小限制的详细信息。每个文件都定义了一系列适用于你的实现的显式常量。例如，limits.h 文件包含类似以下的行：

```
#define INT_MAX   +32767
#define INT_MIN   -32768
```

你系统使用的 float.h 头文件。）此示例与 float 类型相关。等效常量已为 double 和 long double 类型定义，将名称中的 FLT 分别替换为 DBL 和 LDBL。（该表假设系统以 2 的幂表示浮点数。）

### 表 4.2 来自 float.h 的一些符号常量

| 符号常量 | 代表 |
|---|---|
| FLT_MANT_DIG | float 的尾数中的位数 |
| FLT_DIG | float 的最小有效十进制位数 |
| FLT_MIN_10_EXP | 具有完整有效数字的 float 的最小基数-10 负指数 |
| FLT_MAX_10_EXP | float 的最大基数-10 正指数 |
| FLT_MIN | 保持全精度的正 float 的最小值 |
| FLT_MAX | 正 float 的最大值 |
| FLT_EPSILON | 1.00 与大于 1.00 的最小 float 值之间的差值 |

清单 4.5 说明了使用 float.h 和 limits.h 中的数据。（注意，不完全支持 C99 标准的编译器可能不接受 LLONG_MIN 标识符。）

## 清单 4.5 defines.c 程序

```
// defines.c -- uses defined constants from limit.h and float.
#include <stdio.h>
#include <limits.h>    // integer limits
#include <float.h>    // floating-point limits
int main(void)
{
    printf("Some number limits for this system:\n");
    printf("Biggest int: %d\n", INT_MAX);
    printf("Smallest long long: %lld\n", LLONG_MIN);
    printf("One byte = %d bits on this system.\n", CHAR_BIT);
    printf("Largest double: %e\n", DBL_MAX);
    printf("Smallest normal float: %e\n", FLT_MIN);
    printf("float precision = %d digits\n", FLT_DIG);
    printf("float epsilon = %e\n", FLT_EPSILON);
    return 0;
}

