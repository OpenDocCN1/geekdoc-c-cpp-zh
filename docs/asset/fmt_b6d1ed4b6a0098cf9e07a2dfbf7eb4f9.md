
在两个给定范围 `A` 和 `B` 之间的面积。

# 用户定义函数

## 输入
下限 (`A`)
上限 (`B`)
梯形数量

![](img/177eacb192165f90062789304b5da281_326_0.png)

图 9.19 曲线下的面积

## 输出
给定范围内曲线下方的总面积。

## 算法

1. 输入下限、上限和梯形数量。
2. 计算梯形的宽度。
3. 初始化总面积。
4. 计算梯形面积并加到总面积中。
5. 重复步骤 4 直到完成所有梯形。
6. 打印总面积。

该算法以自顶向模块的形式实现，如图 9.20 所示。

![](img/177eacb192165f90062789304b5da281_326_1.png)

图 9.20 模块图

`f(x)` 的求值是通过独立函数完成的，以便方便修改以允许评估其他函数。

# 格罗希尔公司

## 316 ANSI C 编程

两次运行的结果显示，梯形数量越多，精度越高。对于范围 0 和 3，实际际面积为 12 个单位（通过解析法）。

```c
Program

#include <stdio.h>

/* 全局变量 */

float start_point,

end_point,

total_area;

num_traps;

int

main() {

    void input(void);

    float find_area(float a, float b, int n); /* 函数原型 */

    printf("AREA UNDER CURVE:\n");

    input();

    total_area = find_area(start_point, end_point, num_traps);

    printf("TOTAL AREA = %f\n", total_area);

}

void input(void) {

    printf("Enter lower limit:%f\n",

    scanf("%f", &start_point);

    printf("Enter upper limit:%f\n",

    scanf("%f", &end_point);

    printf("Enter number of trapezoids:%d\n",

    scanf("%d", &num_traps);

}

float find_area(float a, float b, int n) {

    float base, lower, h1, h2; /* 局部变量 */

    float function_x(float x); /* 原型 */

    float trap_area(float h1, float h2, float base); /* 原型*/

    base = (b-a)/n;

    for(lower=a; lower <= b; lower = lower + base) {

        h1 = function_x(lower);

        h2 = function_x(lower + base);

        total_area += trap_area(h1, h2, base);

    }

    return(total_area);

float trap_area(float h1, float h2, float base) {

    float area; /* 局部变量 */

    area = 0.5 * (h1 + h2) * base;

    return(area);

}

float function_x(float x) {

    /* f(x) = x^2 + 1 */

    return(x*x + 1);

}
```

## 输出
`AREA UNDER CURVE`
`Enter lower limit:0`
`Enter upper limit:3`
`Enter number of trapezoids:10`
`TOTAL AREA = 12.100000`
`AREA UNDER CURVE`
`Enter lower limit:0`
`Enter upper limit:3`
`Enter number of trapezoids:100`
`TOTAL AREA = 12.000500`

![](img/177eacb192165f90062789304b5da281_328.png)

# 复习题

### 9.1 判断下列陈述对错。
(a) 函数只能返回一个值。
(b) 函数至少有一个参数。
(c) 函数定义在主函数之前。
(d) 函数可以定义在主函数内部。
(e) 函数必须被调用一次，否则将发出警告。
(f) 任何名称都可以作为函数名。
(g) `void` 类型函数可以作为参数。
(h) 当值传递给函数时，内存中创建了它们的副本。
(i) 程序始终从主函数开始执行。
(j) 全局变量在所有块和函数中可见。
(k) 函数可以递归调用。
(l) 没有返回语句的函数是非法的。
(m) 全局变量不能声明为自动变量。
(n) 参数必须放在调用函数外部。
(o) 函数的返回类型默认为 `int`。
(p) 原型中使用的变量名应与定义中匹配。
(q) 按指针传递时，形式参数必须以前缀符号 `*`。
(r) 按指针传递时，函数调用中的实际参数可以是变量或常量。
(s) 向函数传递数组时，函数调用必须带有括号的数组名。
(t) 向函数传递字符串时，实际参数必须带有尺寸的括号。

### 9.2 空空：
(a) 函数使用的参数称为 ________。
(b) 函数内部定义的变量称为 ________。
(c) 默认情况下，C 函数的返回类型是 ________。
(d) 按指针传递时，形式参数必须以前缀 ________。
(e) 在原型声明中是 ________。
(f) 递归调用函数被称为 ________。
(g) 如果局部变量要在函数调用之间保留其值，它必须声明为 ________。
(h) ________帮助编译器检查实际参数与形式参数之间的匹配。
(j) 函数内部声明的变量假设存储类。

### 9.3 描述向函数传递参数的方法。它与其他用户定义函数有何不同？你倾向于何时使用每种？

### 9.4 什么是原型？为什么它是必要的？

### 9.5 区分各项：
(a) 实际参数和形式参数
(b) 全局变量和局部变量
(c) 自动变量和静态变量
(d) 变量的作用域和可见性
(e) `&` 运算符和 `*` 运算符

### 9.6 解释在遇到以下情况时可能会发生什么。
(a) 函数的实际参数少于形式参数。
(b) 一个实际参数的数据类型与相应的形式参数的类型不匹配。
(c) 原型中一个参数的数据类型与头行中相应的形式参数的类型不匹配。

# 麦格罗希尔公司

# 用户定义函数

### (d) 当所有参数均为相同类型时，函数调用中实际参数的顺序与函数中形式参数的顺序不同。

(e) 返回语句中使用的表达式类型与函数的返回类型不匹配。

### 9.8 下列原型声明中哪些是无效的？为什么？

- (a) `int (fun void)`
- (b) `double fun (void)`
- (c) `float fun (x, y, n);`
- (d) `void fun (void, void);`
- (e) `int fun (int a, b);`
- (f) `int fun (float, float, int);`
- (g) `void fun (int a, int a b);`

### 9.9 下列头文件行哪些是无效的？为什么？

- (a) `float average (float x, float y, float z);`
- (b) `double power (double a, int n - 1)`
- (c) `int product (int m, 10)`
- (d) `double minimum (double x; double y);`
- (e) `int mul (int *, *j)`
- (f) `exchange (int *a, int *b)`
- (g) `void sum (int a, int b, int &&);`

### 9.10 查找以下函数定义中的错误（如果有）：

- (a) `void abc (int a, int b)`
```c
int c;
return (c);
```
- (b) `int abc (int a, int b)`
```c
}
```
- (c) `int abc (int a, int b)`
```c
double c = a + b;
return (c);
```
- (d) `void abc (void)`
```c
}
return;
```
- (e) `int abc(void)`
```c
{
    ...
    ...
    return;
}
```

### 9.11 查找以下函数调用中的错误：

- (a) `void xyz ( );`
- (b) `yxy ( void );`
- (c) `xyz ( int x, int y);`
- (d) `dyzz ( );`
- (e) `xyz ( ) + xyz ( );`

### 9.12 一个除法两个浮点数的函数如下：

```c
divide (float x, float y)
{
    return (x / y);
}
```

以下“函数调用”的值将是什么：

- (a) `divide (10,2)`
- (b) `divide (9,2)`
- (c) `divide (4,5,1,9)`
- (d) `divide (2,0,3,0)`

### 9.13 如果我们按照如下所示更改头文件，对上述函数调用会产生什么影响：

- (a) `int divide (int x, int y)`
- (b) `double divide (float x, float y)`

### 9.14 确定以下程序的输出：

```c
prod (int m, int n);
main ()
{
    int x = 10;
    int y = 20;
    int p, q;
    p = prod (x,y);
    q = prod (p, prod (x,z));
    printf("%d %d\n", p,q);
}
int prod (int a, int b)
{
    return (a * b);
}
```

### 9.15 以下程序的输出将是什么：

```c
void test (int *a);
main ()
{}
```
```c
int x = 50;
test ( &x);
printf("%d\n", x);
void test (int *a)
{
  *a = *a + 50;
}
```

### 9.16 `test` 函数的代码如下：

```c
int test (int number)
{
  int m, n = 0;
  while (m % 2)
  {
    m = number % 10;
    n = n + 1;
    number = number / 10;
  }
  return n;
}
```

执行以下语句时，`x` 和 `y` 的值将是什么？
`x = test (35);`
`y = test (46);`

### 9.17 列举适用于将函数传递给指针的各种规则。
### 9.18 总结将数组传递给函数的规则？
### 9.19 规定数组传递给函数的规则是什么？
### 9.20 说明当我们把全局变量作为参数传递给函数时，可能遇到的问题。

# 编程练习

1. 编写一个函数交换两个变量 `x` 和 `y` 的值。在调用函数中说明其用法。假设 `x` 和 `y` 定义为全局变量。
2. 编写一个函数，可以在两个数字之间提供 `x` 个位置的空间。演示其应用。
3. 使用递归函数计算 `$f(x) = x^5 + \dots$`。
4. 一个 `n` 阶多项式可以评估为：`$P = a_nx^n+\dots+a_0$`。使用数组评估该多项式。
5. 斐波那契数定义为：
`$F_0 = 0$`
`$F_1 = 1$`
`$F_n = F_{n-1} + F_{n-2}$` 对于 `$n > 2$`。编写一个函数生成前 `n` 个数字。
6. 编写一个函数将浮点数保留到指定的位数，例如 `17.45` 保留为 `17.46`。
7. 编写一个函数，如果其参数是质数则返回 `1`，否则返回 `0`。
8. 编写一个函数扫描字符串并转换为小写字母。
9. 开发一个交互式程序，要求用户输入两个数字并显示：
(a) 它们
(b) 差
(c) 积
(d) 除
10. 开发一个程序，接收三角形的三边并显示其面积或周长。给定 `a`、`b`、`c`：
周长 = `a+b+c`
面积 = `$\sqrt{\dots}$`
11. 编写一个函数查找 `m n` 矩阵中的最大值。
12. 编写一个函数计算 `m n` 矩阵的平均值，按行和列显示。
13. 使用函数输出 `m n` 矩阵。
14. 开发一个程序执行以下任务：
(a) 读取无序的整数
(b) 按升序排序它们
(c) 合并矩阵
(d) 输出列表
使用主函数测试这些功能。
15. 使用自己的函数处理字符串的操作：
(a) 复制字符串到另一个
(b) 比较两个字符串
(c) 将字符串添加到末尾
使用驱动程序测试这些功能。
16. 编写一个函数 `find()`，执行以下任务：
(a) 接收字符数组
(b) 如果数组中找到指定的字符则返回 `1`。
17. 设计一个函数 `locate()`，接收两个字符数组 `s1` 和 `s2` 以及一个整数 `m`，并将 `s2` 插入到 `s1` 中（提示：`s2` 可能是一个文本）。
18. 编写一个函数，接收月份数字 `m` 并返回月份名称。例如，如果 `m = 3`，月份是三月。测试你的程序。
19. 在准备日历时，我们需要知道年份是否为闰年。设计一个函数 `leap()` 接收年份并返回相应信息。
20. 编写一个函数接收一个浮点值并将其保留两位小数。例如，`123.4567` 将变为 `123.46`（提示：寻求数学库可用函数的帮助）。

# 10 结构体与联合体

# **术语**

| 数组 | 结构体 | 点运算符 | 联合体 | 位域 |
| :--- | :--- | :--- | :--- | :--- |

## 10.1 引言

我们已经看到数组可以表示属于相同类型的一组数据，例如 `int` 或 `float`。然而，如果我们想用一个名称表示不同类型的数据集合，就无法使用数组。坦率地说，C 支持一种名为结构体的构造数据类型，它是封装不同类型数据的机制。结构体是处理一组相关数据的方便工具。例如，它可以表示一组属性，如学生姓名、学号和成绩。结构体类似于许多其他语言中的“记录”。更多结构示例包括：

- 时间：秒、分、小时
- 日期：日、月、年
- 书籍：作者、标题、价格、年份
- 城市：名称、国家、人口
- ...

结构体有助于更有意义地组织数据。这是一个我们在程序设计中可能经常需要的强大概念。本章专门研究结构体及其应用。还讨论了相关概念联合体。

## 10.2 定义结构体

与数组不同，必须先定义结构体的格式才能声明结构体变量。让我们通过一个示例来说明结构体定义和创建的过程。





# McGraw-Hill 公司

# 结构体与联合体

结构变量。考虑一个包含书名、作者、页数和价格的图书数据库。我们可以定义一个结构体来存储这些信息，如下所示：

```c
struct book_bank {
    char title[20];
    char author[15];
    int pages;
    float price;
}
```

该 `struct` 声明了一个包含四个数据字段细节的结构体，即 `title`、`author`、`pages` 和 `price`。这些字段被称为结构体元素或成员。每个成员可以属于不同的数据类型。`book_bank` 是结构体的名称，被称为结构体标签（structure tag）。该标签后续可用于声明具有该标签结构get变量。
注意，上述定义不包含任何变量。它仅仅描述了一个用于表示信息的格式模板，如下所示：

| title | array of 20 characters | 标题 | 20个字符数组 |
| :--- | :--- | :--- | :--- |
| author | array of 15 characters | 作者 | 15个字符数组 |
| pages | integer | 页数 | 整数 |
| price | float | 价格 | 浮点型 |

结构体定义的通用格式如下：

```c
struct tag_name {
    data_type member1;
    data_type member2;
};
```
等一下，让我重新读一遍图片：
```c
struct tag_name {
    data_type    member1;
    data_type    member2
}
```

在定义结构体时，你可能会注意到以下语法：
1. 模板以分号结束。
2. 虽然整个定义被视为一个语句，但每个成员在模板内部通过单独语句根据其名称和类型进行独立声明。
3. 像 `book_bank` 这样的标签名可以在程序的后续部分用于声明其类型的结构体变量。

# McGraw-Hill 公司
326 ANSI C 编程

## 数组 vs 结构体

- 1. 数组是相同类型相关相关数据元素的集合。结构体可以包含不同类型的元素。
- 2. 数组是派生数据类型，而结构体是程序员定义的类型。
- 3. 任何数组的行为都像内置数据类型。我们所做的只是声明一个数组变量并使用它。但在结构体的情况下，我们必须在声明和使用该类型的变量之前，首先定义并声明数据结构。

## 10.3 声明结构体变量

在定义结构体格式后，我们可以声明该类型的变量。结构体变量的声明与任何其他类型的变量声明相似。它包含以下元素：

- 1. 关键字 `struct`。
- 2. 结构体标签名。
- 3. 用逗号分隔的变量名列表。
- 4. 结束分号。

例如，语句

```c
struct book_bank book1, book2, book3;
```

将 `book1`、`book2` 和 `book3` 声明为该类型的变量。`struct` 的这些每个变量都有模板指定的四个成员。完整的声明可能像这样：

```c
struct book_bank {
    char title[20];
