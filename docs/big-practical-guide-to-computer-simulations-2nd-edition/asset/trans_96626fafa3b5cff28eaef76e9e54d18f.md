
常量 4 的类型为 int，而常量 4.0 的类型为 double。尽管如此，你可以将 4 赋给浮点变量，因为在必要时类型会隐式转换，参见 Sec. 1.1.2。打印 float 或 double 数值时通常使用转换说明符 %f 表示定点记数，或 %e 表示科学记数法。

注意标准 C 不提供对复数的支持。这不是问题，因为有许多可自由获取的库包含了复数计算所需的所有操作，参见 Chap. 7。

- long int 和 long double
- 地址，也称为指针

在某些计算机系统上，这些数据类型会提供更多的内存。在这些情况下，如果需要更大的允许值范围或更高的精度，使用这些数据类型是有意义的。这些数据类型的变量使用方式与 int 或 double 分别相同。

主内存中的通用地址可以由例如以下方式定义的变量存储

```
void *address1, *address2;
```

请注意每个变量前面必须有一个 '*' 字符。在此情况下类型 void 表示“任何东西”，尽管有时它表示“无”（参见 Sec. 1.2）。如果想指定指针存储（或“指向”）特定类型变量的地址，则必须改写数据类型名称，例如

```
int *address3, *address4;
```

与 void 指针的一个重要区别是 address3+1 指的是 address3 的内存地址加上存储一个 int 值所需的字节数，而 address1+1 是 address1 的内存地址加一个字节。变量的实际地址是通过 & 运算符获得的（参见下一节），例如对于整数变量 sum

```
address1 = &sum;
```

printf() 对指针的转换说明符为 '%p'，结果以十六进制显示。例如

```
printf("address = %p\n", address1);
```

可能导致

address = 0xbfa0604

address1 指向的内存位置中存储的值可通过写 *address1 获得。因此，以下几行

```
int sum;
int *address1;

address1 = &sum;
sum = 12;
printf("%d \n", *address1);
```

运行时将输出 12。

指针的稍高级用法可在练习 (2) 中找到。

| 获取源代码 |
| --- |
| 目录: c-programming |
| 文件: address.c |

请注意，你可以通过 C 程序中的 sizeof() 函数确定任何数据类型实际使用的字节数，包括自定义的类型（参见 Sec. 1.1.4）。数据类型名称必须作为参数传递给该函数。例如，以下小型程序 sizeof.c 将打印每种类型使用的字节数：

| 获取源代码 |
| --- |
| 目录: c-programming |
| 文件: sizeof.c |

```
#include <stdio.h>

int main()
{
printf("int uses %d bytes\n", sizeof(int));
printf("short int uses %d bytes\n", sizeof(short int));
printf("char uses %d bytes\n", sizeof(char));
printf("long int uses %d bytes\n", sizeof(long int));
printf("double uses %d bytes\n", sizeof(double));
printf("float uses %d bytes\n", sizeof(float));
printf("long double uses %d bytes\n", sizeof(long double));
printf("pointers use %d bytes\n", sizeof(void *));
return(0);
}
```

请注意 printf 语句的格式字符串，即第一个参数，包含转换字符 %d，这意味着在打印格式字符串时，作为第二个参数传递的数字将以整数形式打印，替换转换字符。有关 printf 命令及其格式字符串的更多细节在 Sec. 1.3 中解释。因此，程序可能产生以下输出：

```
int uses 4 bytes
short int uses 2 bytes
char uses 1 bytes
long int uses 4 bytes
double uses 8 bytes
float uses 4 bytes
long double uses 12 bytes
pointers use 4 bytes
```

因此，使用 long int 与 int 相比并不会增加范围，但 long double 也是如此。sizeof() 命令在使用指针进行动态内存管理时尤其重要，参见 Sec. 1.4。

所有标准 C 数据类型的精度都是固定的。尽管如此，仍有可自由获取的库允许任意精度，包括相应的运算符，参见 Chap. 7。标准算术数据类型的运算符将在下一节讨论。

## 1.1.2 算术表达式

C 中的算术表达式基本上遵循传统算术的相同规则。标准运算加法（运算符 +）、减法（-）、乘法（运算符 *）和除法（/），以及通常的优先级规则对所有数值数据类型都已定义。此外，可以通过使用括号引入显式优先级。以下表达式给出一些示例：

```
total_charge = -elementary_charge*(num_electrons-num_protons);
weighted_avg_score = (1.0*scoreA+2.0*(scoreB1+scoreB2))/num_tests;
```

执行程序时，'=' 字符右侧表达式求值得到的值会被赋给 '=' 字符左侧显示的变量。请注意，赋值本身就是一个表达式，其结果是被赋的值。因此，赋值 x = 1.0 的结果是 1.0，并且可以像这样自行赋值

```
counter3 = ++counter1;
counter4 = --counter2;
printf("%d %d %d %d\n", counter1, counter2, counter3, counter4);
```

将导致

4 3 5 4

由于计算机使用二进制表示一切，特别是任何自然数 n 在二进制表示 n = Σ 2^i a_i 中都可以解释为 0 和 1 的序列 a_{k-1}...a_0。例如，数字 201 写成二进制序列（最高位在左侧）为 11001001。对于这些序列，有一些运算符可以直接作用于位。我们从涉及两个参数的运算符开始。

& 计算两个操作数的按位 AND。对于每一对位 (a,b)，& 操作定义如右侧表格所示：结果只有在 a AND b 均为 1 时才为 1。因此，对于数字 201（二进制 11001001）和 158（二进制 10011110），201 & 158 的结果为 136（二进制 10001000）。

| a | b | a&b |
| --- | --- | --- |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

| 计算两个操作数的按位 OR，定义如右侧表格所示：结果在 a OR b 为 1 时为 1。因此，对于数字 201 和 158，结果为 223（二进制 11011111）。

| a | b | a\|b |
| --- | --- | --- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

^ 计算两个操作数的按位 XOR，定义如右侧表格所示：结果在 a OR b 为 1 但不同时为 1 时为 1。因此，对于数字 201 和 158，结果为 87（二进制 01010111）。

| a | b | a^b |
| --- | --- | --- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

<< 表达式 seq << n 的求值结果是将存储在变量 seq 中（或一般由表达式得到）的位序列左移 n 位，这等价于乘以 2^n。因此，如果 seq 包含 51（二进制 00110011），seq << 2 将得到 204（二进制 11001100）。请注意，如果数字溢出，即相对于变量或表达式的类型过大，高位将被擦除。因此，如果 seq 为 unsigned char 类型，seq << 4 将得到 48（二进制 00110000）。

>> 同样，表达式 seq >> n 的求值结果是将存储在变量 seq 中的位序列右移 n 位，这等价于除以 2^n 的整数除法。

此外，~ 是一个一元反转运算符，它只是将所有 1 替换为 0，所有 0 替换为 1。因此，结果取决于标准位数，因为所有前导 0 将被设为 1。例如，变量 seq 包含值 12（二进制 1100，通常省略前导 0 时），~seq 的结果为（4 字节 = int 的 32 位）4294967283（二进制 11111111111111111111111111110011）。

对于浮点运算，有许多预定义函数，如三角函数、指数/对数、绝对值、贝塞尔函数、伽马函数、误差函数或最大值函数。这些函数的声明包含在头文件 math.h 中。因此，使用这些函数时必须包含此文件。编译时未使用 -Wall，请注意如果未包含 math.h 编译器不会报错，这可能导致错误结果。此外，math.h 包含有用常量的定义，如 π 值或欧拉数 e。以下简单程序 mathtest.c 说明了如何使用数学函数。

| 获取源代码 |
| --- |
| 目录: c-programming |
| 文件: mathtest.c |

```
#include <stdio.h>
#include <math.h>

int main()
{
    double z = 0.25*M_PI;
    printf("%f %f %f\n", sin(z), cos(z), tan(z));
    printf("%f %f\n", asin(sqrt(2.0)/2.0)/M_PI, acos(0.0)/M_PI);
    printf("%f %f %f %f\n", pow(M_E,1.5), exp(1.5), log(1.0), log(M_E));
    printf("%f %f %f\n", fabs(-3.4), floor(-3.4), floor(3.4));
    printf("%f %f\n", fmax(1.3,2.67), fmin(1.3,2.67));
    printf("%e %e %e %e\n", erf(0.0), erfc(0.0), erf(2.0), erfc(2.0));
    printf("%f %f %f\n", tgamma(4.0), tgamma(4.5), exp(gamma(5.0)));
    printf("%f %f %f\n", j0(2.0), j1(2.0), jn(1,2.0));
    return(0);
}
```
