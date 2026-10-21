

![](img/2359b0c604600c58fba3539c738a356e_202_0.png)

Figure 4-1

## 声明数组

你声明数组的方式与到目前为止所见的变量声明方式基本相同，唯一的区别是数组名后面紧跟的方括号内指定了数组中的元素个数。例如，你可以用下面的声明语句声明上一幅图所示的整数数组 height：

```
long height[6];
```

因为每个 long 值在内存中占用 4 字节，整个数组需要 24 字节。数组可以是任意大小，受限于运行程序的计算机所拥有的内存量。

你可以声明任意类型的数组。例如，要声明用于存储一系列发动机容量和功率输出的数组，可以写如下内容：

```
double cubic_inches[10];    // Engine size
double horsepower[10];     // Engine power output
```

如果你对汽车机械感兴趣，这将使你能够存储多达 10 台发动机的立方容量和功率输出，索引值从 0 到 9。就像之前对其他变量所做的那样，你可以在单个语句中声明给定类型的多个数组，但在实践中，最好将变量分别声明在不同的语句中。

## 试一试   使用数组

作为使用数组练习的基础，假设你记录了每次为汽车加油的汽油量以及每次的里程表读数。你可以编写一个程序来分析这些数据，以查看每次加油时的油耗情况：

```
// Ex4_01.cpp
// Calculating gas mileage
#include <iostream>
```
```
#include <iomanip>

using std::cin;
using std::cout;
using std::endl;
using std::setw;

int main()
{
    const int MAX = 20;                     // Maximum number of values
    double gas[ MAX ];                      // Gas quantity in gallons
    long miles[ MAX ];                      // Odometer readings
    int count = 0;                          // Loop counter
    char indicator = 'y';                   // Input indicator

    while( (indicator == 'y' || indicator == 'Y') && count < MAX )
    {
        cout << endl
             << "Enter gas quantity: ";
        cin >> gas[count];                  // Read gas quantity
        cout << "Enter odometer reading: ";
        cin >> miles[count];                // Read odometer value

        ++count;
        cout << "Do you want to enter another(y or n)? ";
        cin >> indicator;
    }

    if(count <= 1)                          // count = 1 after 1 entry completed
    {                                       // ... we need at least 2
        cout << endl
             << "Sorry - at least two readings are necessary.";
        return 0;
    }

    // Output results from 2nd entry to last entry
    for(int i = 1; i < count; i++)
        cout << endl
             << setw(2) << i << "."             // Output sequence number
             << "Gas purchased = " << gas[i] << " gallons" // Output gas
             << " resulted in "                 // Output miles per gallon
             << (miles[i] - miles[i - 1])/gas[i] << " miles per gallon.";

    cout << endl;
    return 0;
}
```

该程序假设每次都加满油箱，因此购买的汽油就是行驶记录距离所消耗的量。下面是此示例产生的输出示例：

```
Enter gas quantity: 12.8
Enter odometer reading: 25832
Do you want to enter another(y or n)? y

Enter gas quantity: 14.9
```
```
Enter odometer reading: 26337
Do you want to enter another(y or n)? y

Enter gas quantity: 11.8
Enter odometer reading: 26598
Do you want to enter another(y or n)? n
```

-   1. Gas purchased = 14.9 gallons resulted in 33.8926 miles per gallon.
-   2. Gas purchased = 11.8 gallons resulted in 22.1186 miles per gallon.

## 数组、字符串和指针

## 工作原理

因为你需要取两个里程表读数之差来计算所用汽油的行驶里程，所以你只使用第一组输入值的里程表读数——你忽略第一次购买的汽油，因为那是在更早行驶的里程中消耗的。

在输出中显示的第二阶段，交通状况一定非常糟糕——或者也许手刹一直都拉着。

用于存储输入数据的两个数组 gas 和 miles 的维度由名为 MAX 的常量值决定。通过更改 MAX 的值，你可以更改程序以适应不同的最大输入值数量。这种技术通常用于使程序在处理的信息量方面具有灵活性。当然，所有程序代码必须编写为考虑到数组维度，或由 const 变量指定的任何其他参数。但在实践中这并不困难，因此你没有理由不采用这种方法。你稍后还会看到如何在程序执行时为存储数据分配内存，这样你就不必提前固定为数据存储分配的内存量。

## 输入数据

数据值在 `while` 循环中读取。因为循环变量 `count` 可以从 0 运行到 `MAX - 1`，我们没有允许程序用户输入超过数组所能处理的值。你将变量 `count` 和 `indicator` 分别初始化为 0 和 'y'，以便 while 循环至少执行一次。每个所需输入值都有提示，并且值被读入适当的数组元素。用于存储特定值的元素由变量 `count` 决定，第一次输入时为 0。数组元素在 `cin` 语句中通过使用 `count` 作为索引来指定，然后 `count` 被递增以准备下一个值。

在输入每个值后，程序会提示确认是否输入另一个值。输入的字符被读入变量 `indicator`，然后在循环条件中进行测试。循环将终止，除非输入 'y' 或 'Y' 并且变量 `count` 小于指定的最大值 `MAX`。

输入循环结束后（无论以何种方式），`count` 的值包含每个数组中最后输入元素的索引值加一。（记住，你在输入每个新元素后递增它。）这将被检查以验证是否至少输入了两对值。如果不是这种情况，程序将以合适的消息结束，因为计算里程值需要两个里程表读数。

```
using std::endl;
using std::setw;

int main()
{
    int value[5] = { 1, 2, 3 };
    int junk [5];

    cout << endl;
    for(int i = 0; i < 5; i++)
        cout << setw(12) << value[i];

    cout << endl;
    for(int i = 0; i < 5; i++)
        cout << setw(12) << junk[i];

    cout << endl;
    return 0;
}
```

在此示例中，你声明了两个数组，其中第一个 value 部分初始化，第二个 junk 则完全未初始化。该程序生成两行输出，在我的计算机上看起来像这样：

```
          1           2           3           0           0
-858993460 -858993460 -858993460 -858993460 -858993460
```

第二行（对应 junk[0] 到 junk[4] 的值）在你的计算机上可能有所不同。

## 工作原理

数组 value 的前三个值是初始化值，最后两个的默认值是 0。在 junk 的情况下，所有值都是无意义的，因为你根本没有提供任何初始值。数组元素包含上次使用这些内存位置的程序遗留的任何值。

一种方便地将整个数组初始化为零的方法是简单地指定单个初始化值为 0。例如：

```
long data[100] = {0};      // Initialize all elements to zero
```

此语句声明数组 data，所有一百个元素都用 0 初始化。第一个元素由大括号之间的值初始化，其余元素初始化为零，因为你省略了这些值。

你也可以省略数值类型数组的维度，只要提供初始化值即可。数组中的元素数量由你指定的初始化值的数量决定。例如，数组声明

```
int value[] = { 2, 3, 4 };
```

定义了一个具有三个元素的数组，其初始值分别为 2、3 和 4。

