
```cpp
void showTheWorld(int a[], int sizeOf)
//前置条件：sizeOf 是数组 a 的声明大小。
//a 的所有索引变量都已赋值。
//后置条件：a 中的值已写入屏幕。

cout << "The array contains the following values:\n"
for (int i = 0; i < sizeOf; i++)
    cout << a[i] << " ";
cout << endl;
```

该函数可以工作，但作为额外的安全措施，你可以如下在函数头中添加 `const` 修饰符：

```cpp
void showTheWorld(const int a[], int sizeOf)
```

有了这个 `const` 修饰符，如果你的函数定义包含更改数组参数中任何值的错误，计算机将发出错误信息。例如，这个版本的 `showTheWorld` 包含一个无意更改数组参数值的错误。幸运的是，这个版本的函数定义包含了数组已被更改。此错误信息将帮助你解释错误：

带有数组的语法如下：

### 语法
`Type_Returned` `Function_Name`(..., `Base_Type` `Array_Name`[ ], ...);

如果你还没有听过指针，我们将在第10章讨论这些。

# 函数中的数组

如果在之前的函数定义中没有使用 `const` 修饰符，并且犯了所示的错误，该函数将通过编译且没有任何错误信息。然而，代码将包含一个无限循环，不断递增 `a[0]` 并将其新值写入屏幕。

这个错误的 `showTheWorld` 版本的问题在于，在 `for` 循环中递增了错误的项。索引变量 `[i]` 被递增，但在这个错误的版本中，索引 `i` 从值 0 开始且从不改变。`a[i]`（等同于 `a[0]`）被递增。当我们包含索引变量 `[i]` 时，我们包含了 `const` 修饰符，这会改变数组中的值，而计算机将发出警告信息。该错误信息可以作为发现错误的线索。

你通常情况下，在你的程序中，除了函数定义外，还有一个函数声明。当你在函数定义中使用 `const` 修饰符时，你必须在函数声明也未使用它，以确保函数头和函数声明保持一致。

修饰符可以用于任何类型的参数，但通常只用于数组参数和类的引用传递参数（后者将在第 6 章和第 7 章中讨论）。

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_230_0.png)

# 陷阱：const 参数的使用不一致

`const` 参数修饰符是一个“全有全无”的假设。如果你对特定类型的某个数组参数使用了它，那么你就应该对其他具有该类型且不被函数改变的数组参数使用它。原因在于函数调用中的函数调用。考虑函数 `showDifference` 的定义，它在这里与定义的函数声明一起给出：

```cpp
double computeAverage(int a[], int numberUsed);
// 返回数组 a 中前 numberUsed 个元素的平均值。
// 数组保持不变。

void showDifference(const int a[], int numberUsed)
{
    double average = computeAverage(a, numberUsed);
    cout << "Average of the " << numberUsed
    cout << " numbers = " << average << endl;
    cout << "The numbers are \n";
    for (int index = 0; index < numberUsed; index++)
        cout << a[index] << " differs from average by "
             << (a[index] - average) << endl;
}
```

所示代码会在大多数编译器上给出错误信息或警告信息。然而，函数 `computeAverage` 并没有改变其参数 `a`。当

（续）

# 第 5 章 数组

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_231_0.png)

### 陷阱：（续）

当编译器处理 `showDifference` 的函数定义时，它会认为 `computeAverage` 会（或至少可能）改变其参数 `a` 的值。这是因为它正在翻译 `showDifference` 的函数定义，编译器对 `computeAverage` 函数所知道的就是它的函数声明，而该声明并没有包含 `const` 来告诉编译器参数 `a` 不会被改变。因此，如果你在函数 `showDifference` 中对参数 `a` 使用 `const`，那么你也应该在函数 `computeAverage` 中对参数 `a` 使用 `const` 修饰符。

`computeAverage` 的函数声明如下：

```cpp
double computeAverage(const int a[], int numberUsed);
```

# 返回数组的函数

函数不能以返回 `int` 或 `double` 类型相同的方式返回数组。有一种方法可以获得与返回数组的函数大致等的东西。做法是返回指向数组的指针。我们将在第 10 章讨论数组与指针的交互这一话题。在学习指针之前，你没有办法编写一个返回数组的函数。

# 示例：生产图

显示 5.4 包含一个使用数组和多个数组参数的程序。这个为 Apex 塑料勺制造公司的程序显示了一个条形图，显示了每个制造工厂在任何给定周的生产率。工厂为每个部门保留了单独的数据，例如茶勺部门、汤匙部门、鸡尾酒勺部门、涂层勺部门等。此外，四个工厂中的每个部门数量不同。

正如你从 5.4 的示例对话所示，图表使用星号代表每个 1000 个生产单位。由于输出是以 1000 为单位的，因此必须通过除以 1000 来进行缩放。这产生了一个问题，计算机必须显示若干星号。它不能为 1600 个单位显示 1.6 个星号。因此，我们四舍五入到最近的千位。因此，1600 将等于 2000 并产生两个星号。

数组 `production` 存储四个工厂的总产量。在 C++ 中，数组索引始终从 0 开始。但由于工厂的编号是 1 到 4 而不是 0 到 3，我们将 `n` 号工厂的总产量放在索引变量 `[n-1]` 中。第 1 号工厂的总输出将保存在 `production[0]` 中，第 2 号工厂的数据保存在 `production[1]` 中，以此此类推。

# 函数中的数组

### 示例：（续）

由于输出是以千个单位为单位，程序将缩放数组元素的值。如果第 3 号工厂的总输出为 4040 个单位，则 `production[2]` 的值最初被设置为 4040。这个 4040 的值将被缩放为 4，使得 `production[2]` 的值变为 4，并输出四个星号来代表第 3 号工厂的产量。这种缩放是由函数 `scale` 完成的，它将整个数组 `production` 作为参数并更改存储在数组中的值。

`round` 函数将其舍入到最近的整数。例如，`round(2.3)` 返回 2，`round(2.6)` 返回 3。`round` 函数在第 3 章中名为“四舍入函数”的编程示例中讨论过。

# 示例 5.4 生产函数图（4 部分中的 1 部分）

```cpp
// 读取数据并显示每个工厂生产率的条形图。
#include <iostream>
#include <cmath>
using namespace std;
const int NUMBER_OF_PLANTS = 4;
void inputData(int a[], int lastPlantNumber);
// 前置条件：lastPlantNumber 是数组 a 的声明大小。
// 后置条件：对于 plantNumber=1 到 lastPlantNumber，
// a[plantNumber-1] 等于 plantNumber 号工厂的总产量。
```

```cpp
void scale(int a[], int size);
// 前置条件：a[0] 到 [size-1] 为非负值。
// 后置条件：a[i] 已更改为原 a[i] 中值的 1000 倍（舍入为
// 整数），对于所有 0 <= i < size-1。
```

```cpp
void graph(const int asterisk[], int lastPlantNumber);
// 前置条件：a[0] 到 [lastPlantNumber-1] 为非负值。
// 后置条件：显示了一个条形图，显示工厂 N
// 生产了 (N-1) 个 1000 单位，对于满足以下条件的 N：
// 1 < N <= lastPlantNumber
```

```cpp
void getTotal(int &sum);
// 从键盘读取非负整数并将
// 其总和放在 sum 中。
```

```cpp
int round(double number);
// 前置条件：number >= 0。
// 返回舍入到最近整数的 number。
```

# 示例 5.4 生产图程序（4 部分中的 2 部分）

```cpp
void printAsterisks(int n);
// 在屏幕上打印 n 个星号
```

```cpp
int main()
{
    int production[NUMBER_OF_PLANTS];

    cout << "此程序显示公司每个\n"
         << "工厂的产量。\n";

    inputData(production, NUMBER_OF_PLANTS);
    scale(production, NUMBER_OF_PLANTS);
    graph(production, NUMBER_OF_PLANTS);
    return 0;
}
```

```cpp
void getTotal(int &sum)
{
    sum = 0;
    int next;
    cout << "输入每个部门的单位数量。\n"
         << "列表末尾附加一个负数。\n";
    cin >> next;
    while (next >= 0)
    {
        sum = sum + next;
        cin >> next;
    }
}
```

```cpp
void scale(int a[], int size)
{}
```

## 函数中的数组

## 显示 5.4 生产图表程序（4/4 部分）

```cpp
for (int index = 0; index < size; index++)
    a[index] = round(a[index]/1000.0);
```

```cpp
int round(double number)
{
    return static_cast<int>(floor(number + 0.5));
}
```

```cpp
void graph(const int asteriskCount[], int lastPlantNumber)
{
    cout << "\nUnits produced in thousands of units:\n";
    for (int plantNumber = 1;
         plantNumber <= lastPlantNumber; plantNumber++)
    {
        cout << "Plant #" << plantNumber << ": ";
        printAsterisks(asteriskCount[plantNumber - 1]);
        cout << endl;
    }
}
```

```cpp
void printAsterisks(int n)
{
    for (int count = 1; count <= n; count++)
        cout << "*";
}
```

### 示例对话

> 该程序显示了显示公司每个工厂的图表。

输入 1 号工厂的生产数据

输入每个部门的产量数量。

在列表末尾添加一个负数。

2000 3000 1000 -1

总 = 6000

输入 2 号工厂的生产数据

输入每个部门的产量数量。

在列表末尾添加一个负数。

2050 3002 1300 -1

总 = 6352

（续）

# 第 5 章 数组

显示 5.4 生产图表程序（4/4 部分）

```text
输入 3 号工厂的生产数据
输入每个部门的产量数量。
在列表末尾添加一个负数。
5000 4020 500 4348 -1
总 = 13868

输入 4 号工厂的生产数据
输入每个部门的产量数量。
在列表末尾添加一个负数。
2507 6050 0189 -1
总 = 10366

产量（单位：千件）：
```

- 工厂 #1 ******

- 工厂 #2 ******

- 工厂 #3 ************

- 工厂 #4 *******

### 自测练习

- 13. 为一个名为 `oneMore` 的函数编写定义，该函数有一个一个整数数组的形式参数，并将每个数组元素的值增加 1。添加任何所需的其他形式参数。

- 14. 考虑以下函数定义：

```cpp
void too2(int a[], int howMany)
{
    for (int index = 0; index < howMany; index++)
        a[index] = 2;
}
```

以下哪些函数调用是允许的？

`int myArray(29);`

`too2(myArray, 29);`

`too2(myArray, 10);`

`too2(myArray, 55);`

`"Hey too. Please come over here."`

`int myArray[100];`

`too2(yourArray, 100);`

`too2(myArray[3], 29);`

### 自测练习（续）

- 15. 在以下可以更改为常量数组参数的数组参数之前插入 `const`。

```cpp
void output(double a[], int size);
// 前置条件：a[0] 到 a[size - 1] 有值。
// 后置条件：a[0] 到 a[size - 1] 已写入。
void drop0(int a[], int size);
// 前置条件：a[0] 到 a[size - 1] 有值。
// 后置条件：a[0] 到 a[size - 1] 中的所有奇数已更改为 0。
```

- 16. 写一个名为 `outorder` 的函数，接受一个 double 数组和一个 int 类型参数 `size` 作为参数，并返回一个 int 类型的值。该函数将测试该数组是否乱序，即数组是否遵循以下条件：

```cpp
a[0] <= a[1] <= a[2] <=
```

如果元素没有乱序，函数返回 -1；否则，它将返回数组中第一个乱序元素的索引。例如，考虑声明

```cpp
double a[10] = {1.2, 2.1, 3.3, 2.5, 4.5, 7.9, 5.4, 8.7, 9.9, 1.0};
```

在前面的数组中，`a[2]` 和 `a[3]` 是第一对乱序的元素，`a[3]` 是第一个乱序元素，因此函数返回 3。如果数组是有序的，函数将返回 -1。

## 5.3 使用数组进行编程

孩子，永远不要只凭直觉印象，要专注于细节。

> 亚瑟·柯南·道尔，《身份案》（夏洛克·福尔斯）

本节讨论了部分填充数组，并对数组的排序和搜索进行了简要介绍。本节不包含关于 C++ 语言的新材料，但包含了更多关于 C++ 数组参数的练习。

## 部分填充数组

通常在编写程序时，数组所需的尺寸是未知的，或者尺寸可能会在程序的每次运行之间发生变化。处理这种情况的一种常见且简单的方法是将数组声明为可能需要的最大尺寸。

# 第 5 章 数组

部分填充数组需要一些小心。在编写程序时，数组所需的尺寸是未知的，或者尺寸可能会在程序的每次运行之间发生变化。处理这种情况的一种常见且简单的方法是将数组声明为可能需要的最大尺寸。

## 210 第 5 章 数组

## 显示 5.5 部分填充数组（22 中的 2 部分）

```cpp
39    numberUsed = index;
40 }

41 double computeAverage(const int a[], int numberUsed)
42 {
43     double total = 0;
44     for (int index = 0; index < numberUsed; index++)
45         total = total + a[index];
46     if (numberUsed > 0)
47 {
48         return (total/numberUsed);
49     }
50     else
51 {
52         cout << "ERROR: number of elements is 0 in computeAverage.\n";
53         cout << "return 0;\n";
54     }
55 }
```
