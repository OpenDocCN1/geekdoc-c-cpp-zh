

![](img/be6359df08208122bec6fad1103de211_37_0.png)

**图 1.7 do-while 结构**

请注意，测试条件用括号括起来，后面跟一个分号。语句块中的语句用花括号括起来。如果 do-while 循环体中只有一条语句，则花括号可选。

do-while 循环在条件为真时继续执行，当条件变为假时，控制权跳转到 do-while 循环之后的语句。

使用 do-while 循环的主要缺点是它至少执行一次，因此即使用户输入了一些无效数据，循环也会执行。但是，do-while 循环广泛用于为菜单驱动程序打印选项列表。例如，请考虑以下代码。

```
#include <stdio.h>
int main()
{
    int i = 1;
    do
    {
        printf("\n %d", i);
        i = i + 1;
    } while(i<=10);
    return 0;
}
```

你认为输出会是什么？是的，代码将打印 1 到 10 的数字。

### 编程示例

- 6. 编写一个程序来计算前 n 个数的平均值。

```
#include <stdio.h>
#include <math.h>
int main()
{
    int n, i = 0, sum = 0;
    float avg = 0.0;
    printf("\n Enter the value of n : ");
    scanf("%d", &n);
    do
    {
        sum = sum + i;
        i = i + 1;
    } while(i <= n);
    avg = (float)sum / n;
    printf("\n The sum of first %d numbers = %d", n, sum);
    printf("\n The average of first %d numbers = %.2f", n, avg);
    return 0;
}
Output
Enter the value of n : 20
The sum of first 20 numbers = 210
The average of first 20 numbers = 10.50
```

## for 循环

与 while 和 do-while 循环一样，for 循环提供了一种机制，用于重复执行任务，直到特定条件为真。for 循环的语法和一般形式如图 1.8 所示。

```
Syntax of for Loop

for (initialization; condition;
increment/decrement/update)
{
statement block;
}
statement;
```

![](img/be6359df08208122bec6fad1103de211_38_0.png)

**图 1.8 for 循环结构**

使用 for 循环时，循环变量仅初始化一次。在每次迭代中，循环变量的值会被更新并检查条件。如果条件为真，则执行循环的语句块；否则，跳过 for 循环语句块中的语句，控制权跳转到 for 循环体之后的语句。

在 for 循环的语法中，循环变量的初始化允许程序员为其赋值。其次，条件指定，只要条件表达式为真，循环就应继续重复自身。循环的每次迭代都必须使退出循环的条件变得可达。因此，在每次迭代中，都必须更新循环变量。更新循环变量可能包括递增循环变量、递减循环变量或将其设置为其他值（例如 i + 2，其中 i 是循环变量）。

请注意，for 循环的每个部分都用分号与其他部分分隔。某个部分可能为空，尽管分号仍然必须存在。但是，如果条件为空，则其被评估为真，循环将重复，直到有其他东西停止它。

for 循环广泛用于执行单条或一组语句有限次数。以下代码展示了如何使用 for 循环打印前 n 个数字。

```
#include <stdio.h>
int main()
{
    int i, n;
    printf("\n Enter the value of n :");
    scanf("%d", &n);
    for(i=1;i<=n;i++)
    {
        printf("\n %d", i);
    }
}
```

在代码中，i 是循环变量。最初，它被初始化为 1。假设用户输入 10 作为 n 的值。然后检查条件，由于条件为真（因为 i 小于 n），执行 for 循环中的语句并打印 i 的值。每次迭代后，i 的值递增。当 i 超过 n 的值时，控制权跳转到 return 0 语句。

### 编程示例

- 7. 编写一个程序来判断给定数字是质数还是合数。

```
#include <stdio.h>
#include <conio.h>
int main()
{
    int flag = 0, i, num;
    clrscr();
    printf("\n Enter any number : ");
    scanf("%d", &num);
    for(i=2; i<=num/2; i++)
    {
        if(num%i == 0)
        {
            flag =1;
            break;
        }
    }
    if(flag == 1)
        printf("\n %d is a composite number", num);
    else
        printf("\n %d is a prime number", num);
    return 0;
}
Output
Enter any number : 37
37 is a prime number
```

## 1.9.3 break 和 continue 语句

### break 语句

在 C 语言中，break 语句用于终止其出现所在的最近封闭循环的执行。我们已经在 switch 语句中见过它的用法。break 语句广泛用于 for、while 和 do-while 循环。当编译器遇到 break 语句时，控制权传递到 break 语句所在循环之后的语句。其语法非常简单，只需输入关键字 break 后跟一个分号。

`break;`

以下示例展示了 break 语句用于终止其嵌入的循环的方式。

```
#include <stdio.h>
int main()
{
    int i = 0;
    while(i<10)
    {
        if (i==5)
        break;
        printf("\t %d", i);
        i = i + 1;
    }
    return 0;
}
```

输出

0 1 2 3 4

一旦 i 等于 5，break 语句就会被执行，控制权跳转到 while 循环之后的语句。

因此，break 语句用于从循环体中的任何点退出循环，绕过其正常的终止表达式。

### continue 语句

与 break 语句类似，continue 语句只能出现在循环体中。当编译器遇到 continue 语句时，循环中其余的语句将被跳过，控制权无条件转移到最近封闭循环的循环继续部分。其语法非常简单，只需输入关键字 continue 后跟一个分号。

`continue;`

同样与 break 语句类似，continue 语句不能在没有封闭 for、while 或 do-while 循环的情况下使用。当在 while 循环和 do-while 循环中遇到 continue 语句时，控制权转移到测试控制表达式的代码。但是，如果放在 for 循环中，continue 语句会导致分支到更新循环变量的代码。例如，请考虑以下代码：

```
#include <stdio.h>
int main()
{
    int i;
    for(i = 0; i <= 10; i++)
    {
        if (i == 5)
            continue;
        printf("\t %d", i);
    }
    return 0;
}
```

输出

0 1 2 3 4 6 7 8 9 10

请注意，该代码旨在打印 0 到 10 的数字。但是，一旦 i 等于 5，就会遇到 continue 语句，因此跳过 printf() 语句，控制权传递到递增 i 值的表达式。

因此，我们得出结论，continue 语句在某种程度上与 break 语句相反。它强制执行循环的下一次迭代，跳过其自身与循环测试条件之间的任何代码。它通常用于在发生错误时重新启动语句序列。

## 1.10 函数

C 语言使其程序员能够将程序分解为通常称为函数的段，每个函数可以或多或少独立于其他函数编写。程序中的每个函数都应该执行一个定义明确的任务。因此，一个函数的程序代码与其他函数完全隔离。

![](img/be6359df08208122bec6fad1103de211_41_0.png)

**图 1.9 main() 调用 func1()**

每个函数都通过向其传递信息以及将函数生成的结果传回给外部世界来进行接口。这个接口基本上由函数名称指定。例如，请看图 1.9，它解释了 main() 函数如何调用另一个函数来执行定义明确的任务。

在图中，我们可以看到 main() 调用一个名为 func1() 的函数。因此，main() 被称为调用函数，func1() 被称为被调用函数。编译器一旦遇到函数调用，控制权就跳转到属于被调用函数的语句。被调用函数执行后，控制权返回到调用程序。

main() 函数可以被调用任意多次。例如，放置在 for 循环、while 循环或 do-while 循环中的函数调用可能会在条件保持为真之前多次调用同一个函数。

不仅 main()，任何函数都可以调用任何其他函数。例如，请看图 1.10，它展示了一个函数调用另一个函数，而另一个函数又调用其他函数。

![](img/be6359df08208122bec6fad1103de211_41_1.png)

**图 1.10 函数调用另一个函数**

