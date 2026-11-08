
清单1.26展示了`switch`语句如何相互嵌套。每当最内层`switch`语句中的`break`语句被执行时，控制流也会从外层`switch`语句中退出。

`switch`语句也常与`do-while`循环一起用于用户输入驱动的编程。考虑这样一个场景：用户决定执行某些操作，并不时地向程序提供输入，直到他想结束执行为止。这种场景可以通过将`switch`语句和`do-while`循环结合在一起来处理。

清单1.27展示了`switch`语句和`do-while`循环的用法：

**清单1.27：`switch`和`do-while`循环的用法**

```c
#include<stdio.h>
int main()
{
    int choice,varA,varB;
    char opt;

    do
    {
        printf("\n Enter two numbers ");
        scanf("%d %d",&varA,&varB);
        printf("\n 1: Addition ");
        printf("\n 2: Multiplication");
        printf("\n 3: Subtraction");
        printf("\n Enter your choice (1/2/3) ? ");
        scanf("%d",&choice);
        switch(choice)
        {
            case 1:
                printf("\n Sum is %d ",varA+varB);
                break;
            case 2:
                printf("\n Product is %d ",varA*varB);
                break;
            case 3:
                printf("\n Difference is %d ",varA-varB);
                break;
            default:
                printf("\n wrong Option");
        }
        fflush(stdin);
        printf("\n Want to continue (y/n) ?");
        scanf("%c",&opt);
    }while(opt != 'n');
    getch();
}
```

清单1.27的输出如下：

```text
    Enter two numbers 10 5


    1: Addition
    2: Multiplication
    3: Subtraction
    Enter your choice (1/2/3) ? 1

    Sum is 15
Want to continue (y/n) ?y
Enter two numbers 70 8

1: Addition
2: Multiplication
3: Subtraction
Enter your choice (1/2/3) ? 2

Product is 560
Want to continue (y/n) ?y

Enter two numbers 568 41

1: Addition
2: Multiplication
3: Subtraction
Enter your choice (1/2/3) ? 3

Difference is 527
Want to continue (y/n) ?n
```

清单1.27中的代码将持续执行，直到用户输入`n`作为选项。

## 块语句

C语言属于块结构化编程语言家族。块无非就是一组语句的集合。块结构化编程语言允许创建块、嵌套块以及在块内声明变量。如果仔细观察，我们可以发现C语言禁止在块中间声明变量。在C语言中，所有变量声明都必须在块的开头进行。如今许多编译器允许在块内的任意位置声明变量，但这并不属于ANSI标准的一部分。块语句总是以花括号开头并以花括号结尾。

清单1.28展示了如何在C语言中编写块语句：

**清单1.28：在C语言中编写块语句**

```c
#include<stdio.h>
int main()
{
    int i;
    for(i=1;i<10;i++)
    {
        int i;
        i=20;
        printf("\n I %d ",i);
    }
    printf("\n Another I %d ",i);
    getch();
}
```

清单1.28的输出如下：

```text
I 20
Another I 1
I 20
Another I 2
I 20
Another I 3
I 20
Another I 4
I 20
Another I 5
I 20
Another I 6
I 20
Another I 7
I 20
Another I 8
I 20
Another I 9
```

清单1.28中的代码展示了块在C程序中的应用。我们可以在块内使用之前已经定义过的同名变量。

## C语言中的循环

到目前为止，我们已经讨论了顺序语句和决策语句，例如`if`和`else`结构。这些指令集总是恰好执行一次。然而，在使用编程语言时，必须始终牢记，有些情况下我们需要重复执行某个操作。决策语句并不能为我们提供执行这些任务的灵活性。我们可以通过循环来处理这种情况。C语言中循环的一个重要方面是，能够重复执行部分指令，同时保持其他执行部分不变。

一个循环通常包含四个部分：

-   初始化
-   测试条件
-   增量
-   循环体

并不强制要求上述所有步骤都必须按相同顺序执行。

### while循环

让我们看一个现实生活中的场景：我们需要将数字累加到100，并将总和作为输出。图1.5中的控制流描述了如何使用`while`循环来解决该问题：

![](img/43c5f409f9b17790a628c4b4df854b61_80_0.png)

**图1.5：** `while`循环的流程图

图1.5展示了`while`循环的基本构建块。第一条语句定义了初始化，我们取`COUNT`变量并为其赋值为1。接下来是测试条件，这是一个决策语句。在测试条件中，我们检查`COUNT`的值是否小于100。如果值确实小于100，则执行某些任务，否则退出流程图。我们在`while`循环内执行的操作之一是使`COUNT`递增1。清单1.29展示了C语言中的循环概念：

**清单1.29：C语言中的`while`循环**

```c
#include<stdio.h>

int main()
{
    int count;
    int sum=0;

    count =1;                     /* Initialization   */
    while(count <= 100)           /* Test Condition */
    {
        sum += count;
        count++;                  /* Increment Statement */

    }
    printf("\n Sum = %d ",sum);
    getch();
    return 0;
}
```

在清单1.29中，紧跟在`while`后面的花括号内的语句构成了整个循环的循环体。首先执行测试条件，如果发现为真，则循环体中的所有语句都会被执行。这个过程不断重复，直到测试条件变为假。循环的每次执行也称为一次迭代。在清单1.29中，循环内的语句将执行100次。在第101次迭代时，测试条件失败，控制流退出循环。以下代码片段展示了如何构造一个`while`循环：

```text
    Initialization of loop-control variable
    while (test condition is true)
    {
        perform certain actions;

        increment loop-control variable;

    } end loop
```

应当记住，测试条件最终应变为假，否则`while`循环将永远无限执行下去。

考虑以下示例：

```c
    int count = 10;
    while(count < 15 )
    {
        printf("\n Inside while loop");
    }
```

该示例中的循环将无限执行下去，因为测试条件永远不会变为假。循环计数器可以以任何可能的方式修改。对循环计数器可以执行任何逻辑操作。

### while循环的嵌套

可以有多个`while`循环一个接一个地同时执行。这种执行方式称为`while`循环的嵌套。让我们考虑一个例子：需要显示从1到10所有数字的阶乘。为了解决这个问题，我们需要嵌套`while`循环。

清单1.30展示了`while`循环的嵌套：

**清单1.30：** `while`循环的嵌套

```c
#include<stdio.h>

int main()
{
    int factorial;
    int inner_count;
    int outer_count;

    outer_count=1;
    factorial=1;

    while(outer_count <= 10)
    {
        inner_count=1;
        while(inner_count <= outer_count)
        {
            factorial*=inner_count;
            inner_count++;
        }
        printf("\n Factorial of %d is %d ",outer_count,factorial);
        factorial=1;
        outer_count++;
    }
    getch();
}
```

清单1.30的输出如下：

```text
Factorial of 1 is 1
Factorial of 2 is 2
Factorial of 3 is 6
Factorial of 4 is 24
Factorial of 5 is 120
Factorial of 6 is 720
Factorial of 7 is 5040
Factorial of 8 is 40320
Factorial of 9 is 362880
Factorial of 10 is 3628800
```

如清单1.30所示，我们有两个嵌套的`while`循环。外层循环控制数据生成的范围，即它从1迭代到10。内层循环用于计算外层循环每次迭代的阶乘。

### for循环

`for`循环是C语言中最常用的循环之一。使用这种循环的主要优点是，可以在一条语句中同时完成循环控制变量的初始化、测试和增量操作。这使得`for`循环使用起来更加灵活。

