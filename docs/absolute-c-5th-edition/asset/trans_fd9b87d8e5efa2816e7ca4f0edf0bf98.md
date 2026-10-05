

# 函数中的数组 201

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

# 陷阱：（续）

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

# 示例：（续）

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

