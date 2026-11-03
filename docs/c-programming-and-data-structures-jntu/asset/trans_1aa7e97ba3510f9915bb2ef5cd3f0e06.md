

ANSI 标准还新增了两种预处理操作：

- # 字符串化运算符
- ## 记号粘贴运算符

### #elif 指令

#elif 使我们能够建立“if...else...if...”序列来测试多个条件。#elif 的一般使用形式如下：

```
#if expression 1
statement sequence 1
#elif expression 2
statement sequence 2
.....
#elif expression N
statement sequence N
#endif
```

例如：

```
#if MACHINE == HCL
#define FILE "hcl.h"
#elif MACHINE == WIPRO
#define FILE "wipro.h"
#elif MACHINE == DCM
#define FILE "dcm.h"
#endif
#include FILE
```

### #pragma 指令

#pragma 是一种面向实现的指令，允许我们向编译器指定各种指令。它采用以下形式：

```
#pragma name
```

其中，name 是我们想要的 pragma 名称。例如，在 Microsoft C 中，`#pragma loop_opt(on)` 会执行循环优化。如果编译器无法识别该指令，则会忽略它。

### #error 指令

#error 指令用于在调试过程中产生诊断信息。其一般形式为

```
#error error message
```

当遇到 #error 指令时，它会显示错误信息并终止处理。例如：

```
#if !defined(FILE_G)
#error NO GRAPHICS FACILITY
#endif
```

请注意，我们使用了与 #if 一起使用的特殊预处理运算符 defined。defined 是一个新增内容，它接受一个用括号括起来的名称。如果编译器不支持它，我们可以按如下方式替换：

|  |  |  |
|---|---|---|
| #if !defined | 替换为 | #ifndef |
| #if defined | 替换为 | #ifdef |

### 字符串化运算符（#）

ANSI C 提供了一个名为 # 的运算符，称为字符串化运算符，用于宏函数的定义。该运算符允许将宏定义中的形式参数转换为字符串。请看下面的例子：

```
#define sum(xy) printf(#xy " = %f\n", xy)
main()
{
    ...
    sum(a+b);
    ...
}
```

预处理器将把这一行

```
sum(a+b);
```

转换为

### 记号粘贴运算符（##）

ANSI 标准定义的记号粘贴运算符 ## 使我们能够在宏定义中把两个记号组合成一个记号。例如：

```
#define combine(s1,s2) s1 ## s2
main()
{
    ...
    ...
printf("%f", combine(total, sales));
...
}
```

预处理器将该语句转换为语句

```
printf("%f", totalsales);
```

再考虑一个宏定义：

```
#define print(i) printf("a" #i "=%f", a##i)
```

这个宏会把下面的语句转换为语句

```
printf("a5 = %f", a5);
```

## 案例研究

### 计算曲线下的面积

计算机在数值分析中的应用之一就是计算曲线下的面积。计算曲线下面积的一种简单方法是将面积划分为若干等宽的梯形，然后求出各梯形面积之和。梯形的面积由下式给出：

Area = 0.5 * (h1 + h2) * b

其中 h1 和 h2 是两侧的高度，b 是宽度，如下图所示：

![](img/65953ea584e494f3d396b2252cb5ea53_295_0.png)

图 10.19 中的程序计算函数 f(x) = x² + 1 在任意两个给定界限（例如 A 和 B）之间的曲线面积。

- 下限（A）
- 上限（B）
- 梯形数量
- 给定界限之间的曲线下总面积。

- 1. 输入下限、上限和梯形数量。
- 2. 计算梯形宽度。
- 3. 初始化总面积。
- 4. 计算梯形面积并累加到总面积。
- 5. 重复第 4 步，直到所有梯形计算完毕。
- 6. 输出总面积。

该算法采用自顶向下的模块化形式实现，如下所示：

![](img/65953ea584e494f3d396b2252cb5ea53_296_0.png)

对 f(x) 的求值使用了单独的函数，以便可以轻松修改，从而对其他函数求值。

两次运行的输出表明，梯形数量越多，精度越高。界限为 0 和 3 时的实际面积为 12 个单位（通过解析法求得）。

```
Program
/*
 AREA UNDER A CURVE
*/
#include <stdio.h>
/* GLOBAL VARIABLES */
float start_point, end_point, total_area;
int numtraps;

main()
{
void input(void);
float find_area(float a, float b, int n);
printf("AREA UNDER A CURVE\n");
printf("\n");

total_area = find_area(start_point, end_point, numtraps);
printf("TOTAL AREA = %f", total_area);
}
void input(void)
{
printf("\n Enter lower limit:");
scanf("%f", &start_point);
printf(" Enter upper limit:");
scanf("%f", &end_point);
printf("Enter number of trapezoids:");
scanf("%d", &numtraps);
}

float find_area(float a, float b, int n)
{
float base, lower, h1, h2; /* LOCAL VARIABLES */
float function_x(float x);
float trap_area(float h1, float h2, float base);

base = (b-a)/n;
lower = a;

for(lower = a; lower <=b - base; lower = lower + base)
{
h1 = function_x(lower);
h2 = function_x(lower + base);
total_area += trap_area(h1, h2, base);
}
return(total_area);
}

float trap_area(float height_1, float height_2, float base)
{
float area; /* LOCAL VARIABLES */
area = 0.5 * (height_1 + height_2) * base;
return(area);
}

float function_x(float x)
{
/* F(X) = X * X + 1 */
return(x*x + 1);
}
```

### 输出

```
AREA UNDER A CURVE
Enter lower limit: 0
Enter upper limit: 3
Enter number of trapezoids: 30
TOTAL AREA = 12.005000

AREA UNDER A CURVE
Enter lower limit: 0
Enter upper limit: 3
Enter number of trapezoids: 100
TOTAL AREA = 12.000438
```

图 10.19 计算曲线下的面积

## 要点回顾

C 语言的优势主要在于函数的高效使用。我们鼓励采用模块化、多函数的编程方法，同时也有必要记住关于函数的一些重要要点。

- 1. 函数可以返回值，也可以不返回值。如果返回值，也只能返回一个值。
- 2. 实参和形参的数据类型必须一致。否则，传入的将是垃圾值，而且不会生成任何错误信息。
- 3. 函数默认返回整型值。
- 4. 当函数需要返回非整型值时，必须在函数首部显式指定其类型。此类函数应在调用函数的开头声明。
- 5. 没有 return 语句的函数不能返回任何值。不过，函数中使用的全局变量会保留其值，以供以后使用。
- 6. 返回值的函数可以像其他 C 变量一样用于表达式（算术或关系表达式）。
- 7. 当返回值赋给变量时，该值会转换为接收它的变量的类型。
- 8. 函数不能作为赋值的目标。
- 9. return 语句可以出现在函数体的任何位置。一个函数也可以有多条 return 语句。
- 10. 函数可以放在 main 函数之后，也可以放在 main 函数之前。
- 11. 使用多个函数时，它们可以按任意顺序排列。
- 12. 函数被视为外部变量。因此，不能在另一个函数内部定义函数。
- 13. 函数内部声明的变量仅对该函数可见。它在函数被调用时创建，在函数结束时销毁。
- 14. 全局（外部）变量从声明位置开始到程序结束都可见。
- 15. 在函数内部声明为 static 的变量即使在函数退出后仍会保留其值。（由于 static 变量在编译期间初始化，因此它们只初始化一次。）
- 16. 多文件全局变量必须且只能在一个文件中以不带 extern 的方式声明。在其他需要引用它的地方使用 extern 声明。

## 复习题与练习

10.1 解释当程序中遇到下列情况时可能会发生什么。

- (a) 函数中的实参少于形参。
- (b) 其中一个实参的数据类型与对应形参的数据类型不匹配。
- (c) return (expression) 中表达式的类型与函数类型不匹配。
- (d) 在两个不同函数中声明了同名变量。

10.2 判断下列说法是否正确。

- (a) 函数应按照被调用的顺序排列。
- (b) C 函数只能返回一个值。
- (c) 可以向函数传递任意数量的参数。
- (d) C 函数至少应有一个参数。
- (e) 函数总是返回整型值。
- (f) 函数可以调用自身。
- (g) 全局变量只能在 main 函数中使用。
- (h) 形式参数的值可以在声明它们的函数内部改变。
- (i) 每个函数都应有 return 语句。

10.3 区分下列概念：

- (a) 实参与形参。
- (b) 全局变量与局部变量。
- (c) 自动变量与静态变量。
- (d) 全局变量与 extern 变量。

10.4 main 是一个用户自定义函数。它与其他用户自定义函数有何不同？

10.5 下列哪些函数首部无效？为什么？

- (a) average(x,y,z);
- (b) power(a,n-1)
- (c) product(m,10)
- (d) double minimum(float a; float b;)

10.6 下面的函数返回 x/y 的值。

```
divide(x,y)
float x,y;
{
    return(x/y);
}
```

下列函数调用的值是多少：

- (a) divide(10,2)
- (b) divide(9,2)
- (c) divide(4.5,1.5)

10.7 确定下列程序的输出：

```
main()
{
```

