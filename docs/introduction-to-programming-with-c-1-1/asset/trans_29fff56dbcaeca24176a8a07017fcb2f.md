

## Continue 语句

它用于根据某些条件跳过循环的一部分。

### 工作原理

遇到 continue 语句时，循环体内的剩余语句将被跳过，并执行循环中的条件表达式。

### 图示表示

![](img/bb6d48ce0279cc8c245e23e6b7e31d4d_70_0.png)

## break 与 continue 语句的区别

|  | Break | Continue |
|---|---|---|
| 1 | 当执行 break 时，break 之后的语句将被跳过并导致循环终止。 | 当执行 continue 语句时，continue 之后的语句将被跳过并导致循环以下一轮迭代继续 |
| 2 | 它可以在 switch 语句中使用以将控制转移到 switch 外部 | 它不能在 switch 语句中使用 |
| 3 | **示例：**<br><pre>for(i=1;i&lt;=5;i++)<br>{<br>    if(i==3)<br>        break;<br>    printf("%d\t",i);<br>}<br></pre><br>**输出：**<br>`1 2` | **示例：**<br><pre>for(i=1;i&lt;=5;i++)<br>{<br>    if(i==3)<br>        continue;<br>    printf("%d\t",i);<br>}<br></pre><br>**输出：**<br>`1 2 4 5` |

## 嵌套循环

在另一个循环内的循环称为嵌套循环。

```c
for(; ;)
{
    ...........
    for(; ;)
    {
        ................
    }
}
```

## 样题

| 题目 | CO | RBT 等级 |
|---|---|---|
| 简要说明带示例的简单 if、if-else 和嵌套 if-else 语句 | CO2,CO3 | L2 |
| 举例说明 For、While 和 Do-While 循环的概念。 | CO2,CO3 | L2 |
| 说明 switch-case 语句的语法 | CO2,CO3 | L2 |
| 举例讨论 break 和 continue 语句。 | CO2,CO3 | L2 |
| 举例说明带语法的 for 循环 | CO2,CO3 | L2 |
| 将条件运算符应用于合适的程序 | CO2,CO3 | L3 |
| 设计流程图并编写算法交换三个数字 | CO2,CO3 | L3 |
| 举例说明条件运算符的语法和合适的编程示例。 | CO2,CO3 | L3 |
| 举例说明 while 和 do-while 循环，并论证在一种场景下哪一个更好 | CO2,CO3 | L4 |
| 类比：<br>**学生根据在 CIE 中获得的分数进行分类，类比如下：**<br>**Marks&gt;=75 Distinction**<br>**Marks &gt;=60 and &lt;75 First Class**<br>**Marks &gt;=50 and &lt;60 Second Class**<br>**Marks &gt;=40 and &lt;50 Third Class**<br>**Marks &lt;40 Fail**<br>为上述场景设计流程图并附带适当的提示和流程。 | CO2,CO3 | L4 |
| 设计流程图和伪代码在不使用任何循环语句的情况下求 ‘n’ 个自然数的和。 | CO2,CO3 | L6 |
| 设计流程图并编写算法交换三个数字 | CO2,CO3 | L6 |
| 举例说明 C 中的 switch-case 语句。 | CO2,CO3 | L6 |
| 编写算法求二次方程的根。 | CO2,CO3 | L6 |
| 设计流程图以查找学生的成绩为 distinction、first class、pass、fail 和 absent。 | CO2,CO3 | L6 |
| 编写 C 程序判断给定的年份是否为闰年。 | CO2,CO3 | L6 |
| 编写 C 程序求 1 到 100 的数的和 | CO2,CO3 | L6 |
| 编写 C 程序判断给定的三角形是等边、等腰还是不等边。 | CO2,CO3 | L6 |
| 以下程序的输出是什么<br><pre>#include &lt;stdio.h&gt;<br>void main()<br>{<br>    int i = 0;<br>    for (i = 0; i &lt; 5; i++)<br>        if (i &lt; 4)<br>        {<br>            printf("Hello");<br>            break;<br>        }<br>}</pre> | CO2,CO3 | L6 |
| 编写程序判断给定的数是偶数还是奇数 | CO2,CO3 | L6 |
| 编写 C 程序打印前十个质数。 | CO2,CO3 | L6 |
| 编写 C 程序打印到 100 的斐波那契数列。 | CO2,CO3 | L6 |
| 编写程序读取一个三位数并打印个位、十位、百位的数字。 | CO2,CO3 | L6 |
| 评估 For、While 和 Do-While 循环的概念并举例。 | CO2,CO3 | L5 |
| 举例说明带语法的 for 循环 | CO3 | L1 |
| 举例说明 while 和 do-while 循环，并论证在一种场景下哪一个更好 | CO2,CO3 | L4 |
| 举例说明不同的循环概念 | CO3 | L2 |
| 在你自己的示例中应用嵌套循环 | CO2,CO3 | L3 |
| 编写 C 程序求 1 到 100 的数的和 | CO3 | L6 |
| 以下程序的输出是什么<br><pre>#include&lt;stdio.h&gt;<br><br>void main()<br>{<br>    int i = 0;<br>    for (i = 0; i &gt; 5; i++)<br>        if (i &gt; 4)<br>        {<br>            printf("Hello");<br>            break;<br>        }<br>}</pre> | CO3 | L6 |
| 编写 C 程序打印前十个质数。 | CO3 | L6 |
| 编写 C 程序打印到 100 的斐波那契数列。 | CO3 | L6 |
| 编写程序读取一个三位数并打印个位、十位、百位的数字。 | CO3 | L6 |
| 编写 C 程序求给定数的阶乘。 | CO3 | L6 |
| 编写 C 程序求偶数和奇数的和 | CO3 | L6 |
| 编写 C 程序求给定数的反转。 | CO3 | L6 |
| 编写 C 程序判断给定数是否为质数 | CO3 | L6 |
| 编写 C 程序生成右三角形<br>1<br>1 2<br>1 2 3<br>1 2 3 4 | CO3 | L6 |

## 模块 3

## 数组、字符串和函数

## 什么是函数？

大型程序可以被划分为称为模块的可管理部分，其中每个模块执行特定任务。每个模块称为函数。它是一个自包含的小程序，称为程序段，用于执行某些特定且明确定义的任务。

它分为：

- 库函数/预定义函数
- 用户定义函数 UDF

## 库函数

由 C 编译器制造商编写的函数称为库函数。这些函数的实现细节对程序员来说是未知的。库函数也称为预定义或内置或内建或标准库函数。C 库包含执行标准和预定义任务的各种函数集合。这些函数可供我们在程序中使用。

- 例：sqrt(x) — 计算 x 的平方根
- Printf() — 用于在屏幕上打印数据
- Scanf() — 用于从键盘读取数据

```c
/* program to demonstrate the use of library function*/

#include<stdio.h>

#include<math.h>

void main()
{
    float s, n;
    printf("enter value of n\n");
    scanf("%f", &n);
    s = sqrt(n);
    printf("Square root = %f\n", s);
}
```

注意：printf 和 scanf 的声明可在 stdio.h 中找到，sqrt 的声明可在 math.h 头文件中找到。

main() 是一个用户定义函数，它通过按顺序执行每个语句来控制和协调所有活动。

## 被调用函数和调用函数

通过编写函数名来调用的函数称为“被调用函数”，而调用它的函数称为“调用函数”。

在上面的示例中，main() 是调用函数，sqrt() 是被调用函数

## 使用库函数的优点和缺点

### 优点

- 程序员的工作变得更容易，因为函数已经可用。
- 它减少了程序开发时间。

### 缺点

它们的数量有限，程序员不能完全依赖这些库函数。

## 用户定义函数

由用户/程序员编写以执行特定任务的函数称为用户定义函数。它们也称为程序员定义函数。

## 用户定义函数元素

- 函数定义
- 函数调用
- 函数声明

## 函数定义

为实现特定任务而编写的程序模块称为函数定义。每个函数定义由两部分组成：

- 函数头：由函数返回的值的数据类型、函数名和参数组成。
- 函数体：由执行特定任务的一组语句组成。

### 语法

```c
return_type function_name(parameters)
{
    Declaration part;

    Executable part;

    Return statement;
}
```

### 示例

![](img/bb6d48ce0279cc8c245e23e6b7e31d4d_78_0.png)

### 函数头

它由 3 部分组成。

- 返回类型：这是函数预期返回的值的数据类型。数据类型可以是 int、float、char、double、void 等（任何有效的 C 数据类型）
- 函数名：它是函数的名字。它可以是任何有效的标识符。
- 参数：这些是放在括号内的变量列表。所有这些变量都应分别声明，每个声明应以逗号分隔。

