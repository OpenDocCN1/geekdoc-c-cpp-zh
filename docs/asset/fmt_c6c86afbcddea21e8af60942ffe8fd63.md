
注意：此程序可以不用 `goto` 语句编写。

# 2. 工资计算

**问题：** 一家制造公司将其员工分为四个等级。等级和相应的补贴所示：

| 等级 (Level) | 交通补贴 (Conveyance allowance) | 娱乐补贴 (Entertainment allowance) |
|---|---|---|
| 1 | 1000 | 500 |
| 2 | 750 | 200 |
| 3 | 500 | 100 |
| 4 | 250 | |

员工的总工资包括基本工资、房租和其他补贴。所得税根据总工资的比例扣除：

| 总工资 (Gross salary) | 税率 (Tax rate) |
|---|---|
| <= 2000 | 不税 |
| 2000 < Gross <= 4000 | 3% |
| 4000 < Gross <= 5000 | 5% |
| Gross > 5000 | 8% |

编写一个程序，读取员工编号、等级和基本工资，并计算扣税后的净工资。

## 问题分析
总工资 = 基本工资 + 房租 + 补贴
补贴取决于等级，而所得税取决于总工资。主要步骤为：
1. 读取数据。
2. 确定等级并计算补贴。
3. 计算总工资。
4. 计算所得税。
5. 计算净工资。
6. 输出结果。

## 程序
程序和测试数据见图 7.15。注意最后一条必须是可执行语句。标签 `stop` 不能是最后一行。

```c
#define CA1 1000
#define CA2 750
#define CA3 500
#define CA4 250
#define EA1 500
#define EA2 200
#define EA3 100
#define EA4 0
main() {
    int level, Jobnumber;
    float gross,
        basic,
        house_rent,
        perks,
        incometax;
    printf("nEnter level, job number, and basic pay\n");
    printf("Enter 0 (zero) for level to END\n");
    scanf("%d", &level);
    if (level == 0) goto stop;
    scanf("%d %f", &jobnumber, &basic);
    switch (level) {
        case 1:
            perks = CA1 + EA1;
            break;
        case 2:
            perks = CA2 + EA2;
            break;
        case 3:
            perks = CA3 + EA3;
            break;
        case 4:
            perks = CA4 + EA4;
            break;
        default:
            printf("Error in level code\n");
    }
    house_rent = 0.25 * basic;
    gross = house_rent + perks;
    if (gross < 2000)
        incometax = 0;
    else if (gross < 4000)
        incometax = 0.03 * gross;
    else if (gross < 5000)
        incometax = 0.05 * gross;
    else
        incometax = 0.08 * gross;
    net = gross - incometax;
    printf("%d %d.%.2f\n", level, Jobnumber, net);
    goto input;
stop: printf("\nEND OF THE PROGRAM\n");
}
```

## 输出
Enter level, job number, and basic pay
Enter 0 (zero) for level to END

（续）

| 1 1111 4000 |
| 1 1111 5980.00 |
| Enter level, job number, and basic pay |
| Enter 0 (zero) for level to END |
| 2 2222 3000 |
| 2 2222 4465.00 |
| Enter level, job number, and basic pay |
| Enter 0 (zero) for level to END |
| 3 3333 2500 |
| 3 3333 3007.00 |
| Enter level, job number, and basic pay |
| Enter 0 (zero) for level to END |
| 4 4444 1000 |
| 4 4444 1500.00 |
| Enter level, job number, and basic pay |
| Enter 0 (zero) for level to END |
| 0 |
| END OF THE PROGRAM |

图 7.15 工资计算

# 复习题

## 7.1 判断下列陈述对错：
(a) 当 `if` 嵌套时，最少的 `else` 会与最近的没有 `else` 子句的 `if` 关联。
(b) 可以有多个 `else` 子句。
(c) `switch` 语句总是可以替换为一系列 `if-else` 语句。
(d) `switch` 可以任意类型。
(e) 遇到 `break` 语句时程序停止执行。
(f) 每个 `if` 必须测试同一个变量。
(g) 任何表达式都可以用于 `if` 表达式。
(h) 每个 `case` 标签只能有一条语句。
(i) `switch` 语句需要 `default`。
(j) 谓词 `if (x >= 10) & (y == 5)` 等同于 `(x < 10) | (y != 5)`。

- (b) 多路选择可以使用 `else if` 语句或 语句来实现。
- (c) `switch` 语句执行的语句会导致退出结构。
- (d) 使用 `?` 运算符的三元条件表达式可以使用 ... 语句轻松编写。
- (e) 表达式 `(!x=)` 可以替换为表达式

## 7.3 找出下列任何代码段中的错误（若有）：
(a) `if (x + y = z && y > 0)` `printf (*);`
(b) `if (code < 1);` `else` `a = b + c` `a = 0`
(c) `if (p < 0) | (q < 0)` `printf ("* sign is negative");`

## 7.4 以下是程序段：
`x = 1;` `y = 1;` `if (n > 0)`

## 7.2 为下列语句填空：
(a) 只有当两个操作数都真时，运算符 才为真。

## 7.26 计算机概念与C语言编程

```c
x = x + 1;
else
y = y - 1;
z = 0;
printf("%d %d"
```

## 7.6 假设 x = 10，判断以下逻辑表达式的真假值：
- (a) x = 10 && x != 10 && x
- (b) x = 10 || x > 10 && !x
- (c) x = 10 || x > 10 || x
- (d) x != 10 || x > 10 || x

## 7.7 找出以下 switch 相关语句中的错误（如果有）。假设 x 和 y 的类型为 int 且 x=1, y=2
- (a) switch (y);
- (b) case 10;
- (c) switch (x + y);
- (d) switch (case 2: y = x + y; break;

## 7.8 在不使用复合关系的情况下重写以下每个项：
- (a) if (grade < 59 && grade >= 50)
- (b) if (number > 10 || number < 0)

```c
sum = sum + number;
if ((M1 > 60 && M2 > 60) || T > 200)
printf("Admitted");
else
```

## 7.8 简化以下复合逻辑表达式
- (a) (x < 10) || (y == 5) || (z < 0)
- (b) (x == y) && (z >= 5)
- (c) (x != y) && (z >= 5)
- (d) (x != 5) && (y == 10) && (z < 5)

## 7.9 假设初始 x = 5, y = 0, z = 1，执行以下代码段后值将是什么？
- (a) if (x && y) x = 10; else y = 10;
- (b) if (x || y || z) y = 10;

## 7.10 假设初始 x = 2, y = 1, z = 0，执行代码段后值将是什么？
- (a) switch (x) case 2: x = 1; y = x + 1; case 1: x = 0; break; default: x = 1; y = 0;
- (b) switch (y) case 0: x = 0; y = 0;

## 7.11 找出以下语句中的错误（如果有）：
- (a) if (x > 10) printf("\n10");
- (b) if x > 10 printf(" OK");
- (c) if (x == 10) printf("Good");

```c
(d) if (x + 10)
    printf("Welcome");
    goto print;
```

## 决策与分支 7.27

## 7.12 下述程序的输出是什么？
```c
main ()
{
    int m = 5;
    if (m < 3) printf("%d", m+1);
    else if (m < 5) printf("%d", m+2);
    else if (m < 7) printf("%d", m+3);
    else printf("%d", m);
}
```
```c
print:
printf("%d, %d, %d", m, n, p);
```

## 7.16 执行以下代码段后，x 的值将是？
```c
int x = 10, y = 5;
x = (x<y)?(y-x):(x-y);
```

## 7.13 下述程序的输出是什么？
```c
main ()
{
    int m = 1;
    if (m == 1)
    {
        printf(" Delhi ");
        if (m == 2)
            printf("Chennai ");
        else
            printf("Bangalore");
    }
    else
        printf(" END");
}
```

## 7.17 执行以下代码段后输出是什么？
```c
int x = 0;
if (x >= 0)
    printf("Number positive");
else
    printf("Number negative");
```

## 7.18 执行以下代码段后输出是什么？
```c
char c = 'a';
switch (c)
{
    case 'a':
        printf(" A ");
    case 'b':
        printf(" B ");
    default:
        printf(" C ");
}
```

## 7.14 下述程序的输出是什么？
```c
main ()
{
    int m;
    for (m = 1; m < 5; m++)
        printf("%d\n", m*2);
}
```

## 7.19 执行以下代码段后输出是什么？
```c
int x = 10, y = 20;
if ((x<y) || (x+5) > 10)
    printf("%d,", x);
else
    printf("%d,", y);
```

## 7.15 下述程序的输出是什么？
```c
main ()
{
    int m, n, p;
    for (m = 0; m < 3; m++)
        for (n = 0; n < 3; n++)
            for (p = 0; p < 3; p++)
                if (m + n + p == 2)
}
```

## 7.20 执行以下代码段的输出是什么？
```c
int a = 10, b = 5;
if (a > 5)
{
    printf("%d,", b);
}
else
    printf("%d,", a);
```

## 7.28 计算机概念与C语言编程

### 练习

## 7.1 写一个程序判断给定数字是奇数还是偶数，并打印 NUMBER EVEN 或 NUMBER ODD。
(a) 不使用 else 选项，以及
(b) 使用 else 选项。

## 7.2 写一个程序找到大于 100 小于 200 且被 2 和 3 整除的整数个数。

## 7.3 给未知数 x1 和 x2 的线性方程组：
```
ax1 + bx2 = m
cx1 + dx2 = n
```
只要分母 ad - bc 不等于零。写一个程序读取常数 a, b, c, d, m 和 n 的值并打印。

## 7.4 给出一个 0 到 100 分的列表，写一个程序统计并打印学生人数：
(a) 超过 80 分的，
(b) 超过 60 分的，
(c) 超过 40 分的，
(d) 达到 40 分的，
(e) 在 81 到 100 之间的，
(f) 在 61 到 80 之间的，
(g) 在 41 到 60 之间的，以及
(h) 在 0 到 40 之间的。程序应使用最少数量的 if 语句

## 7.5 进入专业课程取决于以下条件：
(a) 数学 >= 60
(b) 物理 >= 50
(c) 化学 >= 40
(d) 总分 >= 200 或数学与物理总分 >= 150。根据这三门课的成绩，写一个程序筛选合格候选人。

## 7.6 写一个程序打印如下所示的二维平方根表，提供 0 到 9.9 任意数字的平方根。对于每个情况，值 x 提供 3.2 和 3.9 的平方根。

| 平方根表 | 数字 | 0.0 | 0.1 | 0.2 | ... | 0.9 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0.0 | | | | | | |
| 1.0 | | | | | | |
| 2.0 | | | | | | |
| 3.0 | | x | | y | | |
| 9.0 | | | | | | |

## 7.7 下面是一个杨三角形：
```
1
2 3
4 5 6
7 8 9 10
11 ... 15
79 ... 91
```
(a) 写一个程序打印这个三角形。
(b) 修改程序产生如下形式的杨三角形：
```
1
0 1
1 0 1
0 1 0
```

## 决策与分支 7.29

## 7.8 某服装商店针对商品购买推出了季节性折扣：根据你的设计。包含适当的输出信息。

| 购买金额 | 机织布 | 手织品 |
| :--- | :--- | :--- |
| 0 – 100 | | 5% |
| 101 – 200 | 5% | 7.5% |
| 201 – 300 | 7.5% | 10.0% |
| 300 以上 | 10.0% | 15.0% |

## 7.11 写一个程序从键盘读取三个整数值，并输出说明它们是直角三角形。使用 switch 和 if 语句计算客户需要支付的金额。

## 7.12 电力局对用电收费如下：
前 200 度：每度 80 分
接下来的 100 度：每度 90 分
超过 300 度：每度 1.00 卢比
所有用户至少收取 100 卢比。如果总金额超过 400 卢比，则额外收取总金额 15% 的费用。

## 7.9 写一个程序读取 x 的值并计算函数：
```
y = {
1 for x < 0
0 for x = 0
-1 for x > 0}
```
写一个程序读取用户名和消耗量，并仅输出用户名结果。

## 7.13 写一个程序显示 0 到 100 之间被 6 整除但不能被 4 整除的所有整数和。程序应使用以下方式计数此类整数：
(a) if 语句，
(b) else if，
(c) 条件运算符 ?

## 7.14 写一个交互式程序，读取正数并判断是否为质数，并相应输出。

## 7.10 写一个程序计算二次方程的实根：
```
ax² + bx + c = 0
```
修改程序统计 100 到 200 之间所有的质数。
```
x1 = -b + √(b² - 4ac) / 2a
x2 = -b - √(b² - 4ac) / 2a
```
