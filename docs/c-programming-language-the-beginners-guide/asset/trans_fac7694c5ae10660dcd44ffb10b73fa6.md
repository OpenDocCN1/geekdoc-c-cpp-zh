

```c
#define ROWS 4
#define COLUMNS 5

int main()
{
    int grid[ROWS][COLUMNS];
    int x, y;

    /* initialize the array */
    for (x = 0; x < ROWS; x++)
        for (y = 0; y < COLUMNS; y++)
            grid[x][y] = 0;

    grid[2][2] = 1;

    /* display the grid */
    for (x = 0; x < ROWS; x++)
    {
        for (y = 0; y < COLUMNS; y++)
            printf("%d.%d: %d\t", x, y, grid[x][y]);
        putchar('\n');
    }

    return(0);
}
```

一个二维字符数组实际上就是一组字符串的集合，但有一个重要的注意事项：数组的维度必须足以容纳最长的字符串。记住，二维数组就是一个网格。这里，最长的字符串是六个字母长，加上一个用于空字符的元素。这样每个字符串就有七个元素。

当从二维字符数组打印字符串时，你只需要指定第一个维度，这在第14行完成。构建并运行代码。C语言还提供三维数组，甚至更多维的数组。当你创建这样的数组时，每个维度都需要一组方括号。事情很快就会变得相当复杂。现在，专注于练习二维数组。

作为思考，无论你信不信，如果你从头开始阅读这本书，你已经具备了编写一个基础井字棋电脑游戏所需的一切知识。试试吧。

## 第12章：C语言结构体

C语言中的另一种变量类型是结构体。它实际上是多种现有变量类型组合而成的单一单元。结构体变量就像数据库中的一条记录，包含许多部分。本章介绍结构体的概念。你将看到如何设置结构体、创建结构体变量，以及如何访问结构体成员。

我们将讨论如何向结构体中填充数据，以及将一个结构体放入另一个结构体中的有趣想法。下面的代码当然不是完整代码，但它展示了如何在C语言中创建结构体。

```c
#include <stdio.h>

int main()
{
    struct record {
        int account;
        float balance;
    };

    return(0);
}
```

关键字*struct*后面跟着结构体的名称。在这个例子中，名称是`record`。结构体成员包含在花括号中，每个成员以分号结尾，因为整个声明是一条语句。结构体成员是变量声明。在这个结构体内部，你会找到一个*int*成员和一个*float*成员。*int*成员名为`account`，*float*成员名为`balance`。

结构体声明本身只是创建了一种结构体类型，就像代码中的一种新变量类型。要使用结构体，你需要声明一个结构体类型的变量。在第9行，我们将输入以下内容：

```c
#include <stdio.h>

int main()
{
    struct record {
        int account;
        float balance;
    };

    struct record my_bank;

    return(0);
}
```

这条语句创建了一个名为*my_bank*的变量，类型为*record*结构体类型。要访问结构体的成员，你需要同时引用变量名和成员名。让我们添加两行新代码。结构体变量名在前，然后是一个点，再是成员名。它们必须被赋值为与变量类型匹配的值。在本例中，是一个整数和一个浮点值。

```c
#include <stdio.h>

int main()
{
    struct record {
        int account;
        float balance;
    };

    struct record my_bank;

    my_bank.account = 123456;
    my_bank.balance = 6543.21;

    return(0);
}
```

保存这些更改，然后构建并运行代码。要创建另一个名为*your_bank*的记录结构体变量，你只需复制现有的语句。你也可以通过复制之前的语句并将*my_bank*替换为*your_bank*来填充该结构体中的成员。

```c
#include <stdio.h>

int main()
{
    struct record {
        int account;
        float balance;
    };

    struct record my_bank;
    struct record your_bank;

    my_bank.account = 123456;
    my_bank.balance = 6543.21;
    printf("In account %d I have %.2f\n", my_bank.account, my_bank.balance);

    return(0);
}
```

你也可以预先设置结构体中的信息。请看下面的代码：

```c
#include <stdio.h>

int main()
{
    struct person {
        char name[32];
        int age;
    };

    struct person president = {
        "George Washington",
        67
    };

    printf("%s was %d years old\n", president.name, president.age);

    return(0);
}
```

在这段代码中，声明了一个名为*person*的结构体。第9行声明了一个person类型的变量，它被命名为`president`。president结构体变量立即被赋值为相应的值。这些值与结构体成员类型匹配，并包含在花括号中。运行这段代码以确保它工作正常。

在结构体中需要注意的一点是，如何将一个字符串赋给结构体成员。请看下面的代码：

```c
#include <stdio.h>

int main()
{
    struct person {
        char name[32];
        int age;
    };

    struct person president;

    president.name = "George Washington";
    president.age = 67;

    return(0);
}
```

如果你能看出哪里有问题，那很好。否则，构建代码并检查构建日志以查看具体的错误。正如你看到的，这是不兼容的。你不能对字符串使用赋值运算符。这是因为字符串不是变量，它们是数组。解决方法如下：

```c
#include <stdio.h>
#include <string.h>

int main()
{
    struct person {
        char name[32];
        int age;
    };

    struct person president;

    strcpy(president.name, "George Washington");
    president.age = 67;

    printf("%s was %d years old\n", president.name, president.age);

    return(0);
}
```

现在，它工作了。你可以将任何变量类型插入到C语言结构体中——甚至是另一个结构体。请看下面的代码：

```c
#include <stdio.h>
#include <string.h>

int main()
{
    struct date {
        int year;
        int month;
        int day;
    };

    struct person {
        char name[32];
        struct date birthday;
    };

    struct person friend;

    strcpy(friend.name, "George Washington");
    friend.birthday.year = 1732;
    friend.birthday.month = 2;
    friend.birthday.day = 22;

    return(0);
}
```

在这段代码中，你看到了两个结构体的定义。第一个`date`在第6行定义，它包含year、month和day成员。第二个结构体`person`在第11行声明，它包含一个name数组，以及一个以*birthday*变量形式出现的date结构体。

第15行声明了一个person结构体变量*friend*。第17行到第20行构建了一个friend变量，并使用*strcpy*来赋值字符串。对于结构体成员*birthday*，请注意在第18、19和20行中如何使用两个点来填充子结构体成员。这就是它的工作方式。这就是结构体中嵌套结构体被引用的方式。构建并运行这段代码。

顺便说一下，大多数程序员会在同一条语句中声明一个结构体并创建一个结构体变量。你可以在这里第14行做到这一点。在第14行末尾指定变量名friend，然后删除第15行。

```c
#include <stdio.h>
#include <string.h>

int main()
{
    struct date {
        int year;
        int month;
        int day;
    };

    struct person {
        char name[32];
        struct date birthday;
    } friend;

    strcpy(friend.name, "George Washington");
    friend.birthday.year = 1732;
    friend.birthday.month = 2;
    friend.birthday.day = 22;

    return(0);
}
```

## 数字时代下的阅读之变

随着互联网和移动设备的普及，人们的阅读习惯正在发生深刻变化。纸质书读者逐渐转向电子屏幕，信息的获取方式也从深度阅读转向碎片化浏览。

这一转变不仅是媒介形态的更替，更涉及认知方式的改变。研究表明，长时间的数字阅读可能会弱化读者的专注力和批判性思维。

- 阅读载体的变化：从纸张到屏幕
- 阅读时间的碎片化：通勤、等待、休息间隙
- 阅读深度的下降：浅层浏览与快速切换

> 媒介即讯息——麦克卢汉

面对这样的趋势，教育者与出版机构需要重新思考如何引导读者进行深度阅读，在数字环境中重建专注与反思的空间。

![](img/7d7500a0ed1507e3351945dfe5a0440d_213_0.png)

## 第13章：C语言时间函数

我们还没有遇到过没有某种内部时钟的可编程设备。计算机有时钟，而且由于互联网的存在，现代计算机能够精确地跟踪时间。当你的代码需要访问这些信息时，你可以使用C语言库中的各种时间函数。

在本章中，你将看到C语言中时间函数是如何工作的。你将学习如何检查时间、读取时间值，以及如何收集有关当前日期的信息。下面的代码使用了time函数直接生成的值，如第6行printf函数中的第二个参数所示：

```c
#include <stdio.h>
#include <time.h>

int main()
{
    printf("The current time is %ld\n", time(NULL));

    return(0);
}
```

你会看到占位符是`%ld`，它是一个长整型值，或者说一个非常大的整数。这就是time函数返回值的类型。time函数本身需要一个参数。在我们的示例中，我们使用NULL指针常量来让函数满意。同样让编译器满意的是

