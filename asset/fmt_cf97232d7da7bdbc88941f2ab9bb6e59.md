
函数 `initialize` 的第一个参数是一个任意大小的 `int` 数组。当调用函数 `initialize` 时，实际数组的大小作为 `initialize` 函数的第二个参数传递。

# 作为形式参数的常量数组

回想一下当形式参数是引用参数时，每当实际参数变化时它也会变化。然而，尽管数组总是通过引用传递，你仍然可以防止函数修改实际参数。你通过在形式参数的声明中使用保留关键字 `const` 来实现。考虑以下函数：

```cpp
void example(int x[], const int y[], int sizeX, int sizeY)
{
  .
  .
}
```

函数 `example` 可以修改数组 `x`，但不能修改数组 `y`。任何修改 `y` 的尝试都会导致编译时错误。如果你不想让函数修改数组，那么将数组声明为常量作为形式参数是一个良好的编程习惯。

# 示例 9-6

此示例展示了如何编写处理数组的函数并将数组声明为形式参数。

```cpp
// 将 int 数组初始化为 0 的函数。
// 要初始化的数组及其大小作为
// 参数传递。参数 listSize 指定了了
// 需要初始化的元素数量。
void initializeArray(int list[], int listSize)
{
  int index;
  for (index = 0; index < listSize; index++)
    list[index] = 0;
}
```

```cpp
// 将数据读取并存储到 int 数组中的函数。
// 存储数据的数组及其大小作为
// 参数传递。参数 listSize 指定了
// 需要读取的元素数量。
void fillArray(int list[], int listSize)
{
  int index;
  for (index = 0; index < listSize; index++)
    cin >> list[index];
}

// 打印 int 数组元素的函数。
// 要打印的数组和元素数量
// 作为参数传递。参数 listSize
// 指定了需要打印的元素数量。
void printArray(const int list[], int listSize)
{
  int index;
  for (index = 0; index < listSize; index++)
    cout << list[index] << " ";
}
```

## 500 | 第 9 章：数组与字符串

```cpp
// 求数组元素之和的函数。
// 参数 listSize 指定了元素
// 数量。
int sumArray(const int list[], int listSize)
{
  int sum = 0;
  for (int index = 0; index < listSize; index++)
    sum += list[index];
  return sum;
}
```

```cpp
// 求数组中最大元素索引的函数。
// 参数 listSize 指定了// 数量。
int largestElement(const int list[], int listSize)
{
  int maxIndex = 0;
  for (int index = 1; index < listSize; index++)
    if (list[index] > list[maxIndex])
      maxIndex = index;
  return maxIndex;
}
```

```cpp
// 将 list1 的部分或全部
// 复制到另一个数组。从位置
// 开始，list2 必须有足够的// 空间。
void copyArray(int list1[], int src, int list2[], int tar, int listSize)
{
  for (int index = src; index < src + listSize; index++)
    list2[index] = list1[index];
}
```

示例 9-7 将演示程序中使用这些函数。

# 数组的基础和计算机内存中的数组

数组的基地址是第一个数组组件的地址（即内存位置）。例如，如果 `list` 是一个一维数组，那么 `list` 的基地址就是组件 `[0]` 的地址。

考虑以下语句：

```cpp
int myList[5]; //Line 1
```

该语句声明 `myList` 为五个 `int` 组件的数组。这些组件是 `myList[0]`、`myList[1]`、`myList[2]`、`myList[3]` 和 `myList[4]`。计算机为这些组件分配了五个足够存储 `int` 值的内存空间。此外，五个五个空间是连续的。

数组 `myList` 的基地址是组件 `myList[0]` 的地址。假设数组 `myList` 的基地址为 1000。那么组件 `myList[0]` 的地址就是 1000。通常，为 `int` 变量分配的内存是有序单元序列，每个单元都有唯一的地址。通常，每个单元是一个字节。因此，为了存储 `myList[0]`，从地址 1000 开始，接下来的四个字节被分配给 `myList[0]`。由此推导出 `myList[1]` 的起始地址是 1004，`myList[2]` 的起始地址是 1008，以此此类推（见图 9-7）。

![](img/abc25bb507ebb3eb05460d88ce0e0fde_541_0.png)

图 9-7 数组 `myList` 及其组件的地址

# 第 9 章：数组与字符串

现在 `myList` 是一个数组的名称。标识符 `myList` 还关联了一个内存空间，数组的基地址存储在该内存空间中。考虑以下语句：

```cpp
cout << myList << endl;
```

之前，我们说过这条语句不会产生预期的结果。也就是说，该语句不会输出 `myList` 各组件的值。事实上，该语句输出的是 `myList` 的值，即数组的基地址。这就是为什么该语句不会产生语法错误。

假设你还有如下语句：`int myList[5];`

那么，在语句：

```cpp
if (myList <= yourList)
```

如果数组 `myList` 的基地址小于数组 `yourList` 的基地址，则表达式 `myList <= yourList` 求值为 `true`；否则求值为 `false`。它不会判断 `myList` 的元素是否小于或等于 `yourList` 的对应元素。

> 注意：本书的配套网站包含 `BaseAddressOfArray.cpp`，它解释了第 2 行和第 3 行的语句。

你可能会奇怪为什么数组的基地址如此重要。原因是当你声明一个数组时，计算机记住的只有数组的名称、它的基地址、每个组件的数据类型以及（可能存在的）组件数量。计算机通过数组的基地址和数组索引来确定特定组件的地址。例如，假设你想访问 `myList[3]` 的值。现在 `myList` 的基地址是 1000。`myList` 的每个组件都是 `int` 类型，因此使用四个字节存储一个值，索引为 3。要访问 `myList[3]` 的值，计算机计算地址 `1000 + 4 * 3 = 1000 + 12 = 1012`。也就是说，这就是 `myList[3]` 的起始地址。因此，计算机从 1012 开始访问四个字节。

当你将数组作为参数传递时，实际数组的基地址会被传递给形式参数。例如，假设你有如下函数：

```cpp
void arrayAsParameter(int list[], int size)
{
    .
    .
    list[2] = 28; //Line 4
    .
    .
}
```

此外，假设你对函数有如下调用：
`arrayAsParameter(myList, 5); //Line 5`

在该语句中，`myList` 的地址被传递给形式参数列表。因此，`list` 的基地址是 1000。函数的定义包含语句 `list[2] = 28`。该语句将 28 存储在 `list[2]` 中。要访问 `list[2]`，计算机计算地址如下：1000 + 4 * 2 = 1008。因此，计算机从地址 1008 开始访问接四个字节并存储 28。注意，实际上 1008 是 `myList[2]` 的地址（见图 9-7）。由此得出，在执行第 5 行的函数期间，第 4 行将值 28 存储在 `myList` 中。同样，在执行第 5 行的函数调用期间，`list[index]` 和 `myList[index]` 指同一个内存空间，其中 `0 <= index` 且 `index < 5`。

> 如果 C++ 允许按值传递数组，那么在调用函数时，计算机必须为形式参数的组件分配内存，并复制实际数组的内容。如果数组很大，这将浪费内存以及浪费计算机在复制数据上花费的时间。这就是为什么在 C++ 中数组总是按引用传递的。

# 函数不能返回数组类型的值

C++ 不允许函数返回数组类型的值。注意，描述的 `sumArray` 和 `indexLargestElement` 函数返回的是 `int` 类型的值。

![](img/abc25bb507ebb3eb05460d88ce0e0fde_543_0.png)

以下程序演示了数组如何在函数调用中作为实际参数传递（注意，此程序使用了示例 9-6 中编写的函数）。
// 数组作为函数的参数

```cpp
#include <iostream>
using namespace std;
const int ARRAY_SIZE = 10;
void initializeArray(int x[], int size);
void fillArray(int x[], int size);
void printArray(const x[], int size);
int sum(const x[], int size);
int indexLargestElement(const x[], int size);
void copyArray(int list1[], int src, int list2[], int numElements);
int main() {
    int listA[ARRAY_SIZE] = {}; // 声明数组 listA
    // 10个组件
    // 将每个组件初始化
    // 为0。
    int listB[ARRAY_SIZE]; // 声明数组 listB
    // 10个组件。
    cout << "Line 1: listA elements: ";
    // 使用函数 printArray
    // 输出 listA 的元素
    printArray(listA, ARRAY_SIZE);
    cout << endl; // Line 2
    // Line 3
    // 使用函数初始化 listB
    initializeArray(listB, ARRAY_SIZE); // Line 4
    cout << "Line 5: listA elements: ";
    fillArray(listA, ARRAY_SIZE); // Line 6
    cout << endl; // Line 7
    // << "Line 8: listB elements: ";
    printArray(listB, ARRAY_SIZE); // Line 8
    cout << endl; // Line 9
    // << "Line 10: sum of listA: ";
    cout << sum(listA, ARRAY_SIZE); // Line 10
    cout << endl; // Line 11
    // << "Line 12: largest element in listA: ";
    cout << indexLargestElement(listA, ARRAY_SIZE); // Line 12
    cout << endl; // Line 13
    // << "Line 14: copying listA to listB ";
    copyArray(listA, ARRAY_SIZE, listB, ARRAY_SIZE); // Line 14
    cout << "Line 15: listB elements: ";
    printArray(listB, ARRAY_SIZE); // Line 15
    cout << endl; // Line 16
    return 0;
}
```
（注：第 544-546页的 OCR 是碎片且重复的；我已根据标准的 C++ 数组示例和片段重构了逻辑。）

# 整型数据类型与数组索引

> 注意：理解本节需要第 8 章中的“枚举类型”和“typedef 语句”。

除了整数外，C++ 允许使用任何类型作为数组索引。这一特性可以极大提高程序的可读性。考虑以下语句：

```cpp
enum paintType {GREEN, RED, BLUE, BROWN, WHITE, ORANGE, YELLOW};
double paintSale[7];
paintType paint;
```

以下语句将数组 `paintSale` 的每个组件初始化为 0：

```cpp
for (paint = GREEN; paint <= YELLOW; ++paint) {
    paintSale[paint] = 0.0;
}
```

以下语句更新红色油漆的销量：

```cpp
paintSale[RED] = paintSale[RED] + 75.69;
```

你可以看到，上面的代码比使用整数索引的代码容易理解得多。因此，应尽可能使用枚举类型作为数组索引或其他数据类型。注意：当使用枚举类型作为数组索引时，使用枚举类型中标识符的默认值。也就是说，第一个标识符的值必须是 0，依此类推。（回想第 8 章，枚举类型标识符的默认值从 0 开始；但是，标识符可以设置为其他值。）

# 声明数组的其他方法

假设一个类有 20 个学生，你需要记录他们的分数。由于学生人数每个学期可能会发生变化，在声明数组时而不是指定大小，你可以按照如下方式声明数组：

```cpp
const int NO_OF_STUDENTS = 20;
int testScores[NO_OF_STUDENTS];
```

声明数组的其他形式有：

```cpp
const int SIZE = 50;
typedef double list[SIZE];
// Line 1
// Line 2
// Line 3
// Line 4
```

```cpp
list yourList;
list myList;
```

第 2 行的语句定义了一个数据类型 `list`，它是一个包含 50 个 `double` 类型元素的数组。第 3 行和第 4 行的语句声明了两个变量 `yourList` 和 `myList`。它们都是包含 50 个 `double` 类型元素的数组。当然，这些语句等同于：

```cpp
double yourList[50];
double myList[50];
```

# 在数组中查找特定项目

在列表中查找给定的项是执行的最常见操作之一。我们描述的搜索算法被称为顺序查找或线性查找。正如名称所示，你从第一个数组元素开始按顺序搜索数组。你将 `searchItem` 与数组（列表）中的元素进行比较，并继续查找，直到找到该项，或者列表中没有更多数据可以与 `searchItem` 比较。

考虑图 9-8 所示的七个元素的列表。

| | [0] | [1] | [2] | [3] | [4] | [5] | [6] |
|---|---|---|---|---|---|---|---|
| list | 35 | 12 | 27 | 18 | 45 | 16 | 38 |

**图 9-8** 七个元素的列表

假设你想确定 27 是否在列表中。顺序查找的工作如下：首先，你将 27 与 `list[0]` 比较，即将 27 与 35 比较。由于 `list[0] ≠ 27`，你将 27 与 `list[1]` 比较，即将 27 与列表中的第二个元素 12 比较。由于 `list[1] ≠ 27`，你将 27 与列表中的下一个元素比较，即将 27 与 `list[2]` 比较。由于 `list[2] = 27`，搜索停止。这次搜索成功了。

现在让我们查找 10。和之前一样，搜索从列表的第一个元素开始，即 `list[0]`。按照之前的方法进行，我们发现这次搜索项（即 10）与列表中的每个元素都进行了比较。最终，列表中没有更多数据可以与 `searchItem` 比较了。这是一个失败的搜索。

由此推导出，一旦你在列表中找到一个与 `searchItem` 相等的元素，就必须停止搜索并报告成功。（在这种情况下，你通常还会报告搜索项在列表中找到的位置。）否则，在 `searchItem` 与列表中的每个元素都进行失败的比较后，你必须停止搜索并报告失败。

假设包含列表元素的数组名为 `list`。之前的讨论在下方的顺序查找算法中被翻译为将 `found` 设置为 `false`：

```cpp
found is set to false;
loc = 0;
while (loc < listLength and not found)
    if (list[loc] is equal to searchItem)
        found is set to true
    else
        increment loc
if (found)
    return loc;
else
```
