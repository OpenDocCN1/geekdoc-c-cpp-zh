
示例 8-3 展示了如何处理一维数组。

该示例展示了如何使用循环来处理数组。整个示例中使用了如下声明：

```cpp
double sales[10];
double sum, average;
```

第一条语句声明了一个 10 个组件的数组，每个组件的类型为 `double`。其他语句的含义是清晰的。

- **初始化数组**：以下循环将数组的每个组件初始化为 0.0。
```cpp
for (int index = 0; index < 10; index++)
sales[index] = 0.0;
```

- **读取数据到数组**：以下循环将数据输入数组。为了简单起见，我们假设数据是从键盘输入的。
```cpp
for (int index = 0; index < 10; index++)
cin >> sales[index];
```

- **打印数组**：以下循环输出数组。为了简单起见，我们假设输出到屏幕。
```cpp
for (int index = 0; index < 10; index++)
cout << sales[index] << " ";
```

- **计算数组的和和平均值**：由于其名称意味着某些数据，自然地使用以下 C++ 代码计算数组元素的和和金额：
```cpp
sum = 0;
for (int index = 0; index < 10; index++)
sum = sum + sales[index];
average = sum / 10;
```

- **数组中的最大元素**：我们现在讨论寻找数组中最大元素的算法。假设数组如图 8-6 所示所示。，我们假设第一个元素是最大的。然后我们将 `maxIndex` 指向的元素与数组中的后续元素进行比较。当我们发现更大的元素时，更新 `maxIndex`。该算法如下：

```cpp
maxIndex = 0;
for (int index = 1; index < 10; index++)
    if (sales[index] > sales[maxIndex])
        maxIndex = index;
```

`for` 循环执行后，`maxIndex = 7`，给出数组 `sales` 中最大元素的索引。`largestSales = sales[maxIndex] = 98.23`。

> 你可以编写一个寻找数组最小元素的算法，与寻找数组最大元素的算法相似。（参见本章末尾的编程练习 2。）

现在我们知道了如何声明和处理数组，让我们重写在本章开始时讨论的程序。回该程序读取五个测试分数，计算平均分，并输出所有低于平均分的测试分数。

# 示例 8-4

```cpp
//计算平均测试分数并输出平均
//测试分数以及所有低于平均
//分的测试分数的程序。
#include <iostream>
#include <iomanip>
using namespace std;
int main() {
    int test[5];
    int sum = 0;
    double average;
    int index;
```

```cpp
cout << fixed << showpoint << setprecision(2);
cout << "Enter five test scores: ";
```

```cpp
for (index = 0; index < 5; index++)
{
    cin >> test[index];
    sum = sum + test[index];
}
cout << endl;
```

```cpp
average = sum / 5.0;
```

```cpp
for (index = 0; index < 5; index++)
    if (test[index] < average)
        cout << " is less than the average "
            << "test score.";
return 0;
```

**示例运行：** 在此示例中，用户输入被阴影显示。

**Enter five test scores:** 78 87 65 94 60

平均分数 = 76.80
65 is less than the average test score.
60 is less than the average test score.

# 数组索引越界

考虑以下声明：
```cpp
double num[10];
int i;
```

组件 `num[i]` 是有效的，也就是说，如果 `i = 0, 1, 2, 3, 4, 5, 6, 7, 8 或 9`，则 `i` 是一个有效索引。

如果索引在 0 到 `ARRAY_SIZE - 1` 之间（即 `0 < index < ARRAY_SIZE`），则数组索引在**边界内**。如果索引为负数或大于 `ARRAY_SIZE - 1`，则该索引**越界**。

遗憾的是，C++ 不会检查索引是否在范围内——即是否在 0 到 `ARRAY_SIZE - 1` 之间。如果程序尝试访问由索引指定的组件，则内存位置将被更改，或者访问了你从未打算修改或访问的内存位置的数据，或者由于尝试访问受保护的内存导致程序立即停止。因此，如果索引在执行时越界，可能会发生奇怪的事情。管理这些内存是程序员的责任。

532 | 第 8 章：数组与字符串

考虑以下语句：

```cpp
int list[10];
```

如下循环可能会导致 `list` 的索引越界：
```cpp
for (int i = 0; i <= 10; i++)
    list[i] = 0;
```

当 `i` 变为 10 时，循环条件 `i <= 10` 求为真并执行循环体，导致在 `list[10]` 中存储 0。从逻辑上讲，`list[10]` 并不并不。

> 在新的编译器上，如果程序中的数组索引越界，程序可能会带有错误消息退出。例如，请参见本书附网站上的程序 `ExampleArrayOutOfBounds.cpp` 和 `ExampleArrayOutOfBoundsB.cpp`。

# 声明时的数组初始化

与任何简单变量一样，数组可以在声明时进行初始化。例如，以下 C++ 语句声明了一个包含五个组件的数组 `sales` 并初始化了它的组件。

```cpp
double sales[5] = {12.25, 32.50, 16.90, 23, 45.68};
```

值被放置在大花括号之间并用逗号分隔——这里，`sales[0] = 12.25`, `sales[1] = 32.50`, `sales[2] = 16.90`, `sales[3] = 23.00`, 且 `sales[4] = 45.68`。

在声明数组的同时进行初始化，没有必要指定数组的大小。大小由数组中初始值的数量决定。然而，你必须使用数组名后的括号。因此，上述语句等于：

```cpp
double sales[] = {12.25, 32.50, 16.90, 23, 45.68};
```

虽然在声明时初始化数组时并不需要指定数组的大小，但这是一个良好的做法。

# 声明时的数组部分初始化

当你同时声明并初始化数组时，不需要初始化数组的所有组件。这种过程被称为声明时的部分初始化。然而，如果你在声明时部分初始化数组，必须小心。以下示例解释了当声明并部分初始化数组时发生了什么。

语句：

```cpp
int list[10] = {0};
```

声明 `list` 为包含 10 个组件的数组并将所有组件初始化为 0。语句：

```cpp
int list[10] = {8, 5, 12};
```

声明 `list` 为包含 10 个组件的数组，并将 `list[0]` 初始化为 8，`list[1]` 初始化为 5，`list[2]` 初始化为 12，并将其他组件初始化为 0。因此，如果初始化语句中没有指定所有值，则未赋值的数组组件初始化为 0。注意，数组声明的大小并不重要。例如，语句：

```cpp
int list[] = {5, 6, 3};
```

声明 `list` 为包含 3 个组件的数组，并将 `list[0]` 初始化为 5，`list[1]` 初始化为 6，`list[2]` 初始化为 3。语句：

```cpp
int list[] = {4, 7};
```

声明 `list` 为包含 2 个组件的数组，并将 `list[0]` 初始化为 4，`list[1]` 初始化为 7。533 | 数组

# 数组作为函数参数

现在你已经学会了如何处理数组，一个自然产生的问题：数组是如何传递给函数的？

**仅通过引用传递：**在 C++ 中，数组仅通过引用传递。

因为数组是通过引用传递的，所以在声明数组作为形式参数时，**不需要**使用符号 `&`。

# 示例 8-5

考虑以下函数：

```cpp
void funcArrayParam(int listOne[], double listTwo[])
{
  .
  .
}
```

# 常量数组作为形式参数

记得当形式参数是引用参数时，形式形式参数改变，实际参数也会改变。然而，尽管数组总是通过引用传递，你仍然可以防止函数更改实际参数。你通过在形式参数的声明中使用保留关键字 `const` 来实现。

在这里，函数 `example` 可以修改数组 `x`，但不能修改数组 `y`。任何更改数组 `y` 的尝试都会导致编译错误。如果你不希望函数修改数组，将数组声明为常量作为形式参数是一种良好的编程实践。

# 示例 8-6

此示例展示了如何编写处理数组的函数，以及如何将数组声明为形式参数。

```cpp
//将 int 数组初始化为 0 的函数。
// 将要初始化的数组及其大小作为
// 参数传递。参数列表 listSize 指定了要初始
// 元素个数。
void initializeArray(int list[], int listSize)
{
    for (int index = 0; index < listSize; index++)
    list[index] = 0;
}
```

```cpp
//读取并存储到 int 数组中的函数。
// 将要存储数据的数组及其大小作为
// 参数传递。参数列表 listSize 指定了要读取
// 元素个数。
void fillArray(int list[], int listSize)
{
    for (int index = 0; index < listSize; index++)
    cin >> list[index];
}
```

```cpp
//打印 int 数组元素的函数。
// 将要打印的数组和元素个数作为
// 参数传递。参数 listSize
// 指定了要打印的元素个数。
void printArray(const int list[], int listSize)
{
    for (int index = 0; index < listSize; index++)
    cout << list[index] << " ";
}
```

```cpp
//计算并返回 int 数组元素之和的
// 函数。参数 listSize 指定了要相
// 元素个数。
int sumArray(const int list[], int listSize)
{
    int sum = 0;
    for (int index = 0; index < listSize; index++)
      sum = sum + list[index];
    return sum;
}
```

```cpp
//寻找并返回 int 数组中第一个
// 最大元素索引的函数。参数 listSize
```
