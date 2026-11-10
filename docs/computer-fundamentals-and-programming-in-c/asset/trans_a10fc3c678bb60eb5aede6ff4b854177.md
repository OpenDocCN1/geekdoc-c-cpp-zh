

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_229_0.png)

图 10.5 if-else-if 结构的流程图

## 示例

- 9. 以下程序检查用户给定的数字是零、正数还是负数。

```c
#include <stdio.h>
int main()
{
    int x;

    printf("\n ENTER THE NUMBER:");
    scanf("%d", &x);

    if(x > 0)
        printf("x is positive \n");
    else if(x == 0)
        printf("x is zero \n");
    else
        printf("x is negative \n");

    return 0;
}
```

- 10. 该程序根据学生获得的分数打印等级。

```c
#include <stdio.h>
int main()
{
    int score;
    char grade;
    printf("\n ENTER SCORE : ");
    scanf("%d", &score);
    if(score >= 90)
        grade = 'A';
    else if(score >= 80)
        grade = 'B';
    else if(score >= 70)
        grade = 'C';
    else if(score >= 60)
        grade = 'D';
    else
        grade = 'F';
    printf("GRADE IS:%c", grade);
    return 0;
}
```

## 嵌套 if

当任一 if 语句写在另一个 if 语句之下时，这一组语句称为嵌套 if。下面给出嵌套 if 的简单示例。

测试是否能被 5 整除的 if 语句位于测试是否能被 3 整除的 if 语句内部；因此，它被视为嵌套 if 语句。

```c
if (number % 3 == 0)
{
    printf("number is divisible by 3. \n");
    if (number % 5 == 0)
    {
        printf("number is divisible by 3 and 5. \n");
    }
}
```

下面给出另一个示例。

```c
if(a > b)
    if(a > c)
        printf("%d", a);
```

这里，如果两个 if 条件都为真，则将打印 a。缩进使语句逻辑更加清晰。接下来，通过下面给出的示例进一步解释嵌套 if。

```c
if(a > b)
    if(a > c)
        printf("%d", a);
    else
        printf("%d", c);
```

这里需要注意的一个重要事实是：else 始终与最近（最内层）的 if 关联。在上面的示例中，else 部分对应于内层 if，即 if(a > c)。如果再加一个 else，则最后一个 else 对应于 if(a > b)。嵌套 if 的语法如下。

| 构造 1 | 构造 2 |
| --- | --- |
| if(TestExprA)<br>&nbsp;&nbsp;&nbsp;&nbsp;if(TestExprB)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stmtBT;<br>&nbsp;&nbsp;&nbsp;&nbsp;else<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stmtBF;<br>else<br>&nbsp;&nbsp;&nbsp;&nbsp;stmtAF; | if(TestExprA)<br>&nbsp;&nbsp;&nbsp;&nbsp;if(TestExprB)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stmtBT;<br>&nbsp;&nbsp;&nbsp;&nbsp;else<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stmtBF;<br>else<br>&nbsp;&nbsp;&nbsp;&nbsp;if(TestExprC)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stmtCT;<br>&nbsp;&nbsp;&nbsp;&nbsp;else<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stmtCF; |

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_230_0.png)

图 10.6 查找三个数中最大值的流程图

stmtBT、stmtBF、stmtCT 和 stmtCF 可以是简单语句或语句块。需要记住，语句块总是包含在花括号 { } 中。

在构造 1 中，如果 TestExprA 和 TestExprB 都求值为真，则将执行 stmtBT。如果 TestExprA 求值为真且 TestExprB 求值为假，则将执行 stmtBF。如果 TestExprA 为假，则将执行 stmtAF，并且不会检查 TestExprB。

在构造 2 中，如果 TestExprA 和 TestExprB 都求值为真，则将执行 stmtBT。如果 TestExprA 求值为真且 TestExprB 求值为假，则将执行 stmtBF。如果 TestExprA 为假，则将检查测试表达式 TestExprC。如果它为真，则将执行 stmtCT，否则将执行 stmtCF。

最后，下面给出使用嵌套 if 查找三个数中最大值的程序。所需流程图如图 10.6 所示。C 代码如下：

```c
#include <stdio.h>
int main()
{
    int a, b, c;
    printf("\nEnter the three numbers");
    scanf("%d %d %d", &a, &b, &c);
    if(a > b)
    {
        if(a > c)
            printf("%d", a);
        else
            printf("%d", c);
    }
    else
    {
        if(b > c)
            printf("%d", b);
        else
            printf("%d", c);
    }
    return 0;
}
```

### 悬空 else 问题

这个经典问题出现在每个 if 没有匹配的 else 时。为避免此问题，简单的 C 规则是：始终将 else 与当前块中最近未配对的 if 配对。考虑以下示例。

```c
if(TestExprA)
    if(TestExprB)
        stmtBT;
    else
        stmtAF;
```

如果 TestExprA 求值为真，则执行移动到嵌套 if 并求值 TestExprB。如果 TestExprB 求值为真，则将执行 stmtBT。如果 TestExprA 求值为假，则执行 stmtAF。但在上面的代码中，else 会自动与最近的 if 配对。然而，还需要将 else 与外层 if 关联。解决方案如下：

- 使用空 else
- 使用花括号括起第二个 if 为真时的操作

每种方式的形式如下：

| 使用空 else | 使用花括号 |
| --- | --- |
| if(TestExprA)<br>&nbsp;&nbsp;&nbsp;&nbsp;if(TestExprB)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stmtBT;<br>&nbsp;&nbsp;&nbsp;&nbsp;else<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;<br>else<br>&nbsp;&nbsp;&nbsp;&nbsp;stmtAF; | if(TestExprA)<br>{<br>&nbsp;&nbsp;&nbsp;&nbsp;if(TestExprB)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stmtBT;<br>}<br>else<br>&nbsp;&nbsp;&nbsp;&nbsp;stmtAF; |

现在，在这两种解决方案中，如果表达式 TestExprA 求值为假，则将执行语句 stmtAF。如果它求值为真，则检查 TestExprB。如果 TestExpr 求值为真，则执行 statement1。考虑以下带有悬空 else 问题的 C 程序。

```c
#include <stdio.h>
int main()
{
    int a = 2;
    int b = 2;
    if (a == 1)
        if (b == 2)
            printf("a was 1 and b was 2\n");
        else
            printf("a wasn't 1\n");
    return 0;
}
```

编译并运行后，该程序没有产生任何输出。按照程序的原始形式，程序员很可能以为 else 语句

```c
else
    printf("a wasn't 1\n");
```

会与第一个 if 关联，但事实并非如此。else 始终与紧邻其前的 if 关联，这一点从程序的替代版本中可以清楚看出。完全没有输出的原因是：没有与第一个 if 关联的 else 语句。

为了实现程序员最初可能想要的效果，有必要将程序重新排列成以下形式。

```c
int main()
{
    int a = 2;
    int b = 2;
    if (a == 1)
    {
        if (b == 2) printf("a was 1 and b was 2\n");
        else printf("a wasn't 1\n");
    }
    return 0;
}
```

### 注意

- 多路决策语句用于求值可能具有多个可能值的测试表达式。
- else 始终与最近未匹配的 if 关联。

### 检查你的进度

1. 以下程序的输出将是什么？

```c
(a) int main()
{
    printf("Hi!");
    if(-1)
        printf("Bye");
    return 0;
}
```

输出 Hi!Bye

```c
(b) int main()
{
    printf("Hi!");
    if(0)
        printf("Bye");
    return 0;
}
```

输出 Hi!

```c
(c) float x = 199.9;
if( x < 100)
    printf("one ");
if(x < 200)
    printf("two ");
if(x < 300)
    printf("three ");
```

输出 two three

```c
(d) int main()
{
    int i= -1;
    unsigned int j =1;
    if(i<j)
        printf("Less");
    else
        printf("Greater");
    return 0;
}
```

输出 Greater

### 10.4.2 条件运算符

考虑表达式中存在两个或多个备选值的情况。这种情况在编程中经常出现。例如，根据现有条件，表达式可能求值出两个或多个备选值。根据现有条件，特定函数要返回的值可能有两个或多个备选表达式。同样根据现有条件，函数调用中特定参数的值也可能有两个或多个备选表达式。C 的条件运算符正是为这类情况量身定制的。它具有以下简单格式：

```c
expr1 ? expr2 : expr3
```

它执行时首先求值 expr1（通常是一个关系表达式），然后根据第一个结果为真或为假，分别求值 expr2 或 expr3。

