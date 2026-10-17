
图 11-53 会员程序

![](img/d64a28a68f49d61137bf2f3170ac40ad_484_0.png)

图 11-54 会员程序的示例运行

# 小测验 11-3

- 1. 编写一个 C++ `if` 从，判断存储在 `prices[x]` 变量中的值是否小于最小变量。数组和变量均为 `double` 数据类型。
- 2. 按字母或数字顺序排列数据的过程叫做

- 3. 编写一个 `for` 循环，统计名为 `orders` 的 `int` 数组中 10 个元素中数字 3 的次数。使用名为 `x` 的变量来跟踪数组下标。将 `x` 初始化为 0。

> 小测验问题的答案位于附录 A。

# 实验 11-1 停止并分析

学习图 11-55 中的程序，然后回答问题。国内数组包含了公司在 1 月至 6 月期间在国内的销量。国际数组包含了公司在同一期间的国际上销量。

> 实验的答案位于附录 A。

```cpp
//Lablab11-1.cpp - 计算总销售额

//Created/revised by <your name> on <current date>

#include <iostream>

using namespace std;

int main() {

    // 声明数组和变量

    int domestic[6] = {12000, 45000, 32000,

    67000, 24000, 55000};

    int international[6] = {10000, 56000, 42000,

    23000, 56000, 34000};

    int totalSales = 0;

    // 累加销售额

    for (int x = 0; x < 6; x += 1)
        totalSales += domestic[x] + international[x];

    //  for

    // 显示总销售额

    cout << "Total sales: " << totalSales << endl;

    system("pause");

    return 0;

} // main 函数结束
```

图 11-55 实验 11-1 代码

# 第 11 章 一维数组

问题

- 1. 国内数组和国际数组之间存在什么关系？
- 2. `domestic[1]` 元素存储了什么值？
- 3. 如何计算 2 月份公司的总销售额？
- 4. 国际数组中最大的下标是多少？
- 5. 如果将第 17 行的语句改为 `for (int x = 1; x <= 6; x += 1)`，更改将如何影响循环中的赋值语句？
- 6. 按照启动 C++ 并打开 `Lab11-1 cpp` 文件的说明操作。文件位于 `Cpp6\Chap11\Lab11-1 Project` 文件夹或 `Cpp6\Chap11` 文件夹中。运行程序。公司总销售额为 $412000。
- 7. 修改程序以显示国内销量、国际总销量和公司总销售额。保存并运行程序。
- 8. 现在修改程序，使其也显示每个月的销售额。使用 1 到 6 的月份数字。保存并运行程序。

![](img/d64a28a68f49d61137bf2f3170ac40ad_484.png)

# 并行一维数组

图 11-57 显示了整个降雨程序的代码，图 11-58 显示了程序完成的人工检查表，假设用户输入了以下 12 个降雨量：2.44, 2.36, 2.76, 1.2, .47, .04, .23, .54, .63, 1.54 和 2.16。输入降雨量后，用户选择选项 1，接着选择选项 2，然后选择 3。

```cpp
//Lab1-2.cpp
//将每月降雨量存储在数组中
//显示每月降雨量或
//年度降雨总量
//创建/修改：<你的姓名> <当前日期>
#include <iostream>
using namespace std;
//函数原型声明
void displayMonthly(double rain[], int numElements);
void displayTotal(double rain[], int numElements);
int main()
{
    //声明数组和变量
    double rainfall[12] = {0.0};
    int choice = 0;
    //获取降雨量
    for (int x = 0; x < 12; x += 1)
    {
        cout << "Enter rainfall for month "
        << x + 1 << ": ";
        cin >> rainfall[x];
    }
    do
    {
        //显示菜单并获取菜单选项
        cout << "1 Display monthly amounts" << endl;
        cout << "2 Display total amount" << endl;
        cout << "3 End Program" << endl;
        cout << "Enter your choice: ";
        cin >> choice;
        //调用相应的函数或结束程序
        if (choice == 1)
            displayMonthly(rainfall, 12);
        else
            if (choice == 2)
                displayTotal(rainfall, 12);
        //结束 if
    } while (choice == 1 || choice == 2);
```

图 11-57 降雨程序（续）

# 第 11 章 一维数组

（续）

```cpp
47
48     system("pause");
49     return 0;
50 } //main 函数的结束
51
52 //函数定义****
53 void displayMonthly(double rain[], int numElements)
54 {
55     cout << "Monthly rainfall amount:" << endl;
56     for (int x = 0; x < numElements; x += 1)
57         cout << rain[x] << endl;
58     //结束 for
59 }
60
61 void displayTotal(double rain[], int numElements)
62 {
63     double total = 0.0;
64     for (int x = 0; x < numElements; x += 1)
65         total = total + rain[x];
66     //结束 for
67     cout << "Total rainfall: " << total << endl;
68 } //displayTotal 函数结束
```

图 11-57 降雨程序

![](img/d64a28a68f49d61137bf2f3170ac40ad_490_0.png)

图 11-58 降雨程序的人工检查表

# 并行一维数组

（续）

![](img/d64a28a68f49d61137bf2f3170ac40ad_491_0.png)

11-58 降雨程序的人工检查表

问题解决过程的最后一步是对程序进行（在必要时）评估和修改。记住，你通过将指令输入计算机，然后使用计算机运行（执行）它来评估程序。在程序运行时，你输入与在人工检查程序时相同的示例数据。

# 指南

请按照启动 C++ 开发工具的说明进行操作。根据你所使用的开发工具，你可能需要创建一个新项目；如果是的话，将项目命名为 `Lab11-2 Project` 并将其保存到 `Cpp\Chap11` 文件夹中。将图 11-57 所示的指令输入到名为 `Lab11-2.cpp` 的源文件中。（将该文件保存在项目文件夹或 `Cpp\Chap11` 文件夹中）。现在按照运行 `Lab11-2.cpp` 的相应说明进行。使用你人工检查程序时使用的相同数据测试程序。（总降雨量应为 14.37。）如有必要，修正程序中的任何错误（bug）。

# 实验 11-3 修改

如有必要，创建一个名为 `Lab11-3 Project` 的新项目。将（或复制）`Lab11-2.cpp` 的指令输入到名为 `Lab11-3.cpp` 的新源文件中。修改 `Lab11-3.cpp` 中的第一个注释：对程序进行以下两处修改。首先，将 `void getTotal()` 改为返回值的函数 `int getTotal()`。`getTotal` 函数应该计算总降雨量并将结果返回给 `main` 函数以便在屏幕上显示。其次，当用户输入 1、2 或 3 以外的菜单选项时，`main` 函数应该显示适当的消息。它应该显示菜单。保存并运行程序。

# 实验 11-4 人工检查

人工检查 11-59 中的代码。输出将是什么？

| 学生 | 期中成绩 | 期末成绩 |
| :--- | :--- | :--- |
| 1 | 90 | 100 |
| 2 | 88 | 68 |
| 3 | 77 | 75 |
| 4 | 85 | 85 |
| 5 | 45 | 32 |

```cpp
//Lab1-2.cpp
//将每月降雨量存储在数组中
//显示每月降雨量或
//年度降雨总量
//创建/修改：<你的姓名> <当前日期>
#include <iostream>
using namespace std;
//函数原型声明
void displayMonthly(double rain[], int numElements);
void displayTotal(double rain[], int numElements);
int main()
{
    //声明数组和变量
    double rainfall[12] = {0.0};
    int choice = 0;
    //获取降雨量
    for (int x = 0; x < 12; x += 1)
    {
        cout << "Enter rainfall for month "
        << x + 1 << ": ";
        cin >> rainfall[x];
    }
    do
    {
        //显示菜单并获取菜单选项
        cout << "1 Display monthly amounts" << endl;
        cout << "2 Display total amount" << endl;
        cout << "3 End Program" << endl;
        cout << "Enter your choice: ";
        cin >> choice;
        //调用相应的函数或结束程序
        if (choice == 1)
            displayMonthly(rainfall, 12);
        else
            if (choice == 2)
                displayTotal(rainfall, 12);
        //结束 if
    } while (choice == 1 || choice == 2);
```

图 11-57 降雨程序（续）

# 第 11 章 一维数组

（续）

```cpp
47
48     system("pause");
49     return 0;
50 } //main 函数的结束
51
52 //函数定义****
53 void displayMonthly(double rain[], int numElements)
54 {
55     cout << "Monthly rainfall amount:" << endl;
56     for (int x = 0; x < numElements; x += 1)
57         cout << rain[x] << endl;
58     //结束 for
59 }
60
61 void displayTotal(double rain[], int numElements)
62 {
63     double total = 0.0;
64     for (int x = 0; x < numElements; x += 1)
65         total = total + rain[x];
66     //结束 for
67     cout << "Total rainfall: " << total << endl;
68 } //displayTotal 函数结束
```
