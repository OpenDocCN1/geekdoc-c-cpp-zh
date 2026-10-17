
```c
main() {
    int m;
    float x, average;
    printf("This program computes the average of a\n    set of numbers\n");
    printf("Enter values one after another\n");
    printf("Enter a NEGATIVE number at the end.\n\n");
    for (m = 1; m < 1000; ++m) {
        scanf("%f", &x);
        if (x < 0) {
            break;
        }
        sum += x;
    }
    average = sum/(float)(m-1);
    printf("\n");
    printf("Number of values = %d\n", m-1);
    printf("Sum = %f\n", sum);
    printf("Average = %f\n", average);
}
```

输出：

Output the average of a set of numbers

Enter values one after another

Enter a NEGATIVE number at the end.

21 23

Number of values = 2

Sum = 44.000000

Average = 22.000000

图 6.11 程序中使用 `break`

每个值在被读取时都会被测试是否为正数。如果是正数，则将其累加到总和；否则循环终止。退出时，计算平均值并打印结果。

# 程序 6.9

用于计算级数的程序

S = 1 + x² + x³ + ... + xⁿ

`goto` 语句用于在总和达到特定限制时退出循环。`goto` 的用法如下程序所示。

```c
#define ACCURACY 100
main() {
    int n;
    float x, sum = 1, term;
    printf("Enter the value of x: ");
    scanf("%f", &x);
    printf("Enter the number of terms: ");
    scanf("%d", &n);
    for (i = 2; i <= n; ++i) {
        term *= x;
        sum += term;
        if (sum > ACCURACY)
            goto stop;
    }
    printf("The sum is %f\n", sum);
stop:
    printf("The sum reached the limit: %f\n", sum);
}
```

图 6.12 程序中使用 `goto`

# 结构化编程

结构化编程是一种程序设计和开发的方法。它通过只使用基本的控制结构来使程序逻辑易于理解的纪律：

- 顺序（直线执行）
- 选择（分支）
- 重复（循环结构）

虽然顺序和循环结构已经足够满足所有的编程需求，但选择结构在某些情况下证明更具便利性。结构化编程反对使用 `goto`、`break` 和 `continue` 等跳转语句来实现无条件分支。在最纯的形式下，结构化编程等同于“少 `goto` 编程”。

不要跳转到 `goto` 语句！

174 ANSI C 语言编程

如果序列中包含任何负数，则平方根的计算过程应该跳过这些数字，因为负数的平方根是未定义的。使用 `continue` 语句来实现这一点。程序还会打印一条消息，说明该数字为负数，并记录负数的个数。

最终输出包括已计算的正值个数和遇到的负数个数。

程序：

```
9999 to STOP
Enter a number : 25.0
Number = 25.000000
Square root = 5.000000
Enter a number : 40.5
Number = 40.500000
Square root = 6.336961
Enter a number : -9
Number is negative
Enter a number : -10
Number = 16.000000
Square root = 4.000000
Enter a number : -14.75
Number is negative
Enter a number : 80
Number = 80.000000
Square root = 8.944272
Enter a number : 9999
Number of items done = 4
Negative items = 2
END OF DATA
```

图. 6.14 `continue` 语句的使用

## 避免 goto

如前所述，避免使用 `goto` 是一种良好的做法。这有很多原因。当使用 `goto` 时，许多编译器生成的代码效率较低。此外，使用大量的 `goto` 会使程序逻辑变得复杂，并导致某些代码无法到达。可以通过仔细的程序设计避免使用 `goto`。如果绝对必须使用 `goto`，应该对其进行记录。图 6.15 所示的 `goto` 会导致问题，因此必须避免。

![](img/177eacb192165f90062789304b5da281_186_0.png)

图 6.15 应当避免的 `goto` 跳转

## 跳出程序

我们刚刚看到可以使用 `break` 语句或 `goto` 语句跳出循环。同样，我们可以使用库函数 `exit()` 跳出程序。如果由于某种原因，我们希望跳出程序并返回操作系统，可以使用如下所示的 `exit()` 函数：

```
......
if (test-condition) exit(0);
......
```

`exit()` 函数接受一个整数值作为参数。通常使用 0 表示正常终止，使用非零值表示某些错误或异常情况。使用 `exit()` 函数需要包含头文件 `<stdlib.h>`。

## 6.6 简洁的测试表达式

我们在 `if`、`for` 和 `while` 语句中使用测试表达式，这些表达式会被求值并与零进行比较。由于每个整数表达式都有真/假值，我们不需要与零进行显式比较。例如，当 `x` 不为 0 时，表达式 `x` 为真，当 `x` 为 0 时为假。通过应用 `!` 运算符，我们可以编写不使用任何关系运算符的简洁表达式。

```
if (expression == 0)
```

等价于

```
if(expression)
```

同样地，

```
if (expression != 0)
```

等价于

```
if (expression)
```

例如，

`if (m%5==0 && n%5==0)` 与 `if (l%(m%5)&&(n%5))` 相同。

## 请记住

- 不要忘记在 `do...while` 语句末尾放置分号。
- 在 `while` 或 `for` 语句的控制表达式后放置分号不是语法错误——它很可能是一个逻辑错误。
- 在 `for` 语句的头部使用逗号代替分号是一个错误。
- 不要忘记在 `while` 或 `do...while` 循环的体中放置自增语句。
- 在测试表达式中使用错误的运算符是一个常见错误。确保循环的评估次数恰好符合要求。
- 避免使用 `=` 代替 `==` 运算符的常见错误。
- 不要在 `for` 语句和循环体中同时修改变量。这是一个逻辑错误。
- 不要对浮点数值进行等值比较。
- 避免使用 `while` 和 `for` 语句来实现退出控制（后测试）循环。请使用 `do...while` 语句。同样，不要将 `do...while` 用于前测试循环。
- 在循环体中反复对变量进行操作时，确保该变量在进入循环之前已正确初始化。
- 虽然法律上允许在 `for` 语句头部之外放置初始化、测试和递增部分，但应尽可能避免。
- 虽然允许在初始化和递增部分使用原子表达式，但要留意评估过程中的舍入和截断误差。
- 虽然可以将 `for` 之前的语句和循环体中的语句放在 `for` 头部，但应避免这样做，因为这会使程序更难以阅读。
- 在任何循环中使用 `break` 和 `continue` 语句被认为是非结构化编程。应尽可能消除这些跳转语句的使用。
- 避免在程序的任何地方使用 `goto`。
- 对循环体中的语句进行缩进，以增强可读性和理解性。
- 强烈建议在循环前后留出空白区域。
- 仅在需要跳出程序时才使用函数 `exit()`。

## 案例研究

### 1. 二项式系数表

问题：二项式系数用于二项分布的研究和冗余系统的可靠性研究。需要一个二项式系数表来确定二项式系数。二项式系数对于任何 `m` 和 `x` 的二项式系数可以通过如下方式计算：`B(m,x) = m! / x!(m-x)!`。此外，当 `x` 为 0 或 `m` 为 0 时，二项式系数为 1。图 6.16 显示了 `m=10` 的二项式系数表。

```
#define MAX 10
main()
{
    int value[MAX];
    int i, j, n, x;
    printf("%d; %d\n", m, x);
    for (n=0; n < MAX; n++) {
        printf("Enter employees in Group - %d : %d\n", n+1);
        scanf("%d", &x);
        value[n] = x;
        printf("%d\d\n", value[n]);
    }
    printf("\n");
    printf("\n\n");
    m = 0;
    do
    {
        printf("%d\n", x);
        x = 0;
        while (x <= m)
        {
            if(m == 0 || x == 0)
                printf("%d\n", 1);
            else
            {
                printf("%d\n", binom);
            }
            x = x + 1;
        }
        binom = binom * (m - x) / x;
        m = m + 1;
    } while (m <= MAX);
}
```

输出：

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |

|---|---|---|---|---|---|---|---|---|---|---|

| 0 | 1 | | | | | | | | | | |

| 1 | 1 | 1 | | | | | | | | | |

| 2 | 1 | 2 | 1 | | | | | | | | |

| 3 | 1 | 3 | 3 | 1 | | | | | | | |

| 4 | 1 | 4 | 6 | 4 | 1 | | | | | | |

| 5 | 1 | 5 | 10 | 10 | 5 | 1 | | | | | |

| 6 | 1 | 6 | 15 | 20 | 15 | 6 | 1 | | | | |

| 7 | 1 | 7 | 21 | 35 | 35 | 21 | 7 | 1 | | | |

| 8 | 1 | 8 | 28 | 56 | 70 | 56 | 28 | 8 | 1 | | |

| 9 | 1 | 9 | 36 | 84 | 126 | 126 | 84 | 36 | 9 | 1 | |

| 10 | 1 | 10 | 45 | 120 | 252 | 252 | 120 | 45 | 10 | 1 |

![](img/177eacb192165f90062789304b5da281_189_0.png)

### 2. 直方图

问题：在一个机构中，员工根据基本工资进行分组。薪资范围和每组的人数如下：

| 组别 | 薪资范围 | 人数 |

|---|---|---|

| 1 | 750 – 1500 | 12 |

| 2 | 1501 – 3000 | 23 |

| 3 | 3001 – 4500 | 35 |

| 4 | 4501 – 6000 | 20 |

| 5 | 6000 以上 | 11 |

绘制一个直方图来突出组的大小。

**问题分析：** 给定组的大小，需要绘制代表组大小的条形。每个条形都要写组号和大小。

图 6.17 读取属于每个组的人数并绘制直方图。该程序使用了四个 `for` 循环和两个 `if...else` 语句。

```
#define N 5
main()
{
    int value[N];
    int i, j, n, x;
    for (n=0; n < N; n++) {
        printf("Enter employees in Group - %d : %d\n", n+1);
        scanf("%d", &x);
        value[n] = x;
        printf("%d\d\n", value[n]);
    }
    printf("\n");
    printf("\n\n");
    for (n = 0; n < N; ++n) {
        for (i = 1; i <= 3; i++) {
            if (i == 2) {
                printf("Group-%d |%d\n", n+1);
            } else {
                for (j = 1; j <= value[n]; j++) {
                    printf("***\n");
                }
            }
            if (i == 2) {
                printf("%d\d\n", value[n]);
            } else {
                printf("\n");
            }
        }
    }
}
```

# McGraw-Hill 公司

180 ANSI C 编程

```c
}
    printf("\n");
    }
```

输出

输入组 - 1 中的员工：12

12

输入组 - 2 中的员工：23

23

输入组 - 3 中的员工：35

35

输入组 - 4 中的员工：20

20

输入组 - 5 中的员工：11

11

| | ************* |

| :--- | :--- |

| Group-1 | *************(12) |

| ************ | |

| ********************* | |

| Group-2 | *********************(23) |

| ********************* | |

| ******************************* | |

| Group-3 | ************************************(35) |

| ******************************* | |

| ************* | |

| Group-4 | ********************20) |

| ************* | |

| ************* | |

| Group-5 | ********(11) |

||********* | |

图 6.17 绘制直方图的程序

## 3. 最小成本

问题：单位运行的成本由两个部分 `C1` 和 `C2` 组成，可以用参数 `p` 如下表示：

```c
C1 = 30 - 8p
C2 = 10 + p
```

参数 `p` 的范围从 0 到 10。确定 `p` 的值，精度为 +0.1，使得运行成本达到最小。

## 程序分析：

总成本 `C1 + C2 = 40 - 8p + p²`

当 `p = 0` 时成本为 40，`p = 1` 时成本为 33，`p = 10` 时成本为 60。因此，成本先减后增。图 6.18 中的程序在 `p` 的连续间隔内（步长为 0.1）评估成本，并在成本开始增加时停止。该程序使用 `break` 和 `continue` 语句来退出循环。

```c
Program
main() {
    float p, cost, cost1;
    for (p = 0; p <= 10; p = p + 0.1) {
        cost = 40 - 8 * p * p;
        if(p == 0) {
            cost1 = cost;
            continue;
        }
        if (cost >= cost1) {
            break;
            cost1 = cost;
        }
        pl = p;
    }
    p = (p + pl)/2.0;
    cost = 40 - 8 * p * p;
    printf("\MINIMUM COST = %.2f AT p = %.1f\n", cost, p);
}
```

图 6.18 最小成本问题程序

## 4. 绘制两个函数

问题：我们有两个类型的函数：

```c
y1 = exp (-ax)
y2 = exp (-ax^2)
```

绘制这些函数在 `x` 从 0 到 5 变化时的图像。

问题分析：最初当 `x = 0` 时，`y1 = y2`，图像从相同点开始。当曲线在 `x = 2.0` 时相等时，它们交叉。程序应该具有适当的分支语句，在以下三种条件下打印图像点：

- 1. `y1 > y2`
