

22. gets() 和 puts() 函数的参数是 __________ 变量。

23. 使用 gets() 函数时，不能在输入字符串中包含空白字符。 (True/False)

## 3.9 交互式编程

创建计算机与用户之间的交互式对话是现代编程风格。这些对话通常涉及某种问答交互形式，其中计算机提问，用户提供答案，或反之亦然。

在 C 语言中，这样的对话可以通过交替使用 scanf() 和 printf() 函数来创建。

### 程序 3.8：计算简单利息的程序

```
#include<stdio.h>
main()
{
/* Sample interactive program */
float principle, rate, time, interest;
printf(" Please enter the principle amount: ");
scanf("%f", &principle);
printf(" Please enter the rate of interest: ");
scanf("%f", &rate);
printf(" Please enter the period of deposit: ");
scanf("%f", &time);
interest=principle*rate*time/100.0;
printf("Principle=%7.2f\n", principle);
printf("Rate of interest=%5.2f\n",rate);
printf("Period of deposit=%5.2f\n", time);
printf("Interest=%7.2f\n", interest);
}
```

执行上述程序并观察结果。

## 3.10 总结

浮点数（或实数）在 32 位机器（所有 16 位和 32 位机器上）中以 32 位存储，精度为 6 位数字。浮点数在 C 中由关键字 float 定义。当 float 数字提供的精度不足时，可以使用类型 double 来定义数字。字符通常在内部存储中以 8 位（一个字节）存储。像整数数据类型一样，其他数据类型也提供扩展数据类型，如 long double 和 signed char。C 允许在表达式中混合使用不同类型的常量和变量，但在求值时它遵循非常严格的类型转换规则。当其中一个操作数为实数而另一个为整数时，表达式称为混合模式算术表达式。有时我们希望强制进行与自动转换不同方式的类型转换。即，通过使用类型转换运算符。所有关键字都有固定的含义，这些含义不能被更改。

getchar()、putchar()、scanf()、printf()、gets() 和 puts() 是 C 中常用的输入/输出函数。这些函数用于在计算机与标准输入/输出设备之间传输信息。getchar() 和 putchar() 是用于读取和写入单个字符的两个函数。scanf() 和 printf() 是两个格式化输入/输出函数。这些函数可以处理字符、数值和字符串。gets() 和 puts() 函数用于处理字符串。scanf()、printf()、gets() 和 puts() 函数用于交互式编程。

## 3.11 终结性问题

1. 以下哪些算术表达式是有效的？如果有效，给出表达式的值；否则给出原因。
- a)7.5 % 3
- b)14 % 3 + 7 %2
- c)21 % (int) 4.5
- d)15.25 + - 5.0

2. 找出以下声明语句中的错误，如有：
- Int x;
- float letter, DIGIT;
- double = p, q
- exponent alpha, beta;
- m,n,z:INTEGER
- short char c;
- long int m; count;
- long float temp;

3. 执行以下语句后 x 的值会是什么？
```
int x, y = 10;
char z = ‘a’;
x = y + z;
```

4. ______ 字符的值范围为 -128 到 127。

5. C 中常用的输入/输出函数有哪些？如何访问它们？

6. 区分 getchar() 和 putchar() 函数？

7. 使用 scanf() 函数输入字符串时，如何输入包含空白字符的单个字符串？

8. 区分 gets() 和 scanf() 函数。

9. C 程序包含以下语句：
```
#include<stdio.h>
int i, j, k;
```
编写适当的 scanf() 函数以输入 i、j 和 k 的数值，假设 a) i、j 和 k 的值均为十进制整数
b) i 的值为十进制整数，j 为八进制整数，k 为十六进制整数。
c) i 和 j 的值为十六进制整数，k 为八进制整数。

## 3.12 自测题答案

1. False
2. 64
3. True
4. long int
5. 2.2
6. True
7. 0

c) valid, answer is 1
d) valid, answer is 10.25

# 2. 以下语句中的错误

i) Int x;
可以写成
```
int x;
```
ii) double = p,q
可以写成
```
double p,q;
```
iii) exponent alpha, beta;
C 中没有 exponent 数据类型。
iv) m,n,z:INTEGER
可以写成
```
int m,n,z;
```
v) short char c;
C 中没有 short char 数据类型。
vi) long int m; count;
可以写成
```
long int m,count;
```
vii) long float temp;
C 中没有 long float 数据类型

5. C 中常用的输入/输出函数是：**getchar()**、**putchar()**、**scanf()**、**printf()**、**gets()** 和 **puts()**。这些函数可以通过包含头文件 stdio.h 在程序中访问。 6. **getchar()** 函数用于从键盘接受单个字符，**putchar()** 函数用于在用户屏幕上显示单个字符。
- 7. 通过使用控制字符串 `%[]`。
- 8. `gets()` 不是格式化输入函数，但 `scanf()` 函数是格式化输入函数。
- 9. a) `scanf("%d %d %d", &i, &j, &k);`
   b) `scanf("%d %o %x", &i, &j, &k);`
   c) `scanf("%x %x %o", &i, &j, &k);`

## 3.14 练习

- 1. 使用科学记数法表示以下数字：
   a) 0.001  b) -1.5
- 2. 将以下科学数字转换为十进制记数法： a) 1.0E+2  b) 0.001E-2
- 3. 什么是 unsigned char？解释。
- 4. 什么是 short char？解释。
5. 区分 float 和 double 数据类型。
6. 编写一个程序打印给定数字的因子。
7. 给定边长，编写 C 程序计算立方体的表面积和体积。
8. 编写一个程序反转一个数字并求各位数字之和。
9. 编写一个程序打印任意给定数字的乘法表。
10. 编写一个程序检查给定数字是否为回文数。

# 第 4 章 控制语句和决策制定

**结构：**
4.1 引言
目标
4.2 goto 语句
4.3 if 语句
if-else 语句
if 语句的嵌套
4.4 条件表达式
4.5 switch 语句
4.6 while 循环
4.7 do...while 循环
4.8 for 循环
**for** 循环的嵌套
4.9 **break** 语句和 **continue** 语句
4.10 总结
4.11 终结性问题
4.12 自测题答案
4.13 终结性问题答案
4.14 练习

## 4.1 引言

在上一单元中，你学习了 C 支持的数据类型和 C 中可用的输入/输出运算符类型。本单元将使你能够使用各种类型的控制语句在 C 中做出决策。语句是程序的“步骤”。大多数语句计算并赋值或调用函数，但我们最终还会遇到其他几种类型的语句。默认情况下，语句按顺序执行，一个接一个。我们可以通过使用 *控制流构造* 来修改该顺序，使得只有在某个条件为真或为假时才执行语句或一组语句。这涉及一种决策，以查看是否发生了特定条件，然后指示计算机相应地执行某些语句。

C 语言具有这种决策能力，并支持以下称为 *控制* 或 *决策制定* 语句的语句。
- - **if** 语句
- - **switch** 语句
- - **goto** 语句
- - 条件运算符语句

你还将在本单元学习循环。循环通常由两部分组成：一个或多个控制表达式控制循环的执行，以及主体，即反复执行的一条或多条语句。

就 C 而言，真/假条件可以表示为整数。（整数可以表示许多值；这里我们只关心两个值：“真”和“假”。只涉及两个值的数学研究称为布尔代数，以数学家乔治·布尔命名，他完善了这项研究。）在 C 中，“假”由值 0（零）表示，“真”由任何非零值表示。由于存在许多非零值（对于 int 类型的值，至少有 65,534 个），当我们需要为“真”选择特定值时，我们会选择 1。

Do...while 循环用于需要在执行测试之前先执行循环体主体的情况。for 循环用于需要执行循环体主体指定次数的情况。break 语句用于退出任何循环。

# 目标：

学习本单元后，你应该能够：
- 使用双向决策和多路径决策控制语句执行的流程。
- 无条件地从程序中的一个点分支到另一个点。
- 评估条件表达式。
- 通过在循环体执行前检查条件以及在循环体末尾检查条件来重复执行语句。
- 根据某些条件退出循环。
- 中断当前迭代并继续循环的下一次迭代。

## 4.2 goto 语句

C 支持 goto 语句以无条件地从程序中的一个点分支到另一个点。虽然它可能

