
图 7.14 使用一个成绩`array`创建了一个`GradeBook`对象，然后调用成员函数`processGrades`来分析这些成绩。

## 7.7 对`array`进行排序与查找

在本节中，我们使用 C++ 标准库内置的`sort`函数将`array`中的元素按升序排列，并使用内置的`binary_search`函数判断某个值是否存在于该`array`中。

### 7.7.1 排序

**排序**数据——将其按升序或降序排列——是最重要的计算应用之一。银行会按账号对所有支票排序，以便在每月末准备个人银行对账单。电话公司会将电话号码簿按姓氏排序——并且在所有*相同*姓氏的条目中，再按名字排序——以便于查找电话号码。实际上，每个组织都必须对某些数据进行排序，而且在许多情况下，数据量非常庞大。数据排序是一个引人入胜的问题，它吸引了计算机科学领域一些最深入的研究。在[第 20 章]中，我们研究并实现了几种排序方案，讨论它们的性能，并引入大 O（读作“Big Oh”）记法来描述每种方案完成其任务所需的努力程度。

### 7.7.2 查找

通常可能需要确定一个`array`中是否包含与某个**键值**匹配的值。在`array`中查找特定元素的过程称为**查找**。在第 20 章中，我们研究并实现两种查找算法——用于查找*无序数组*的简单但较慢的*线性查找*，以及用于查找*有序数组*的更复杂但快得多的*二分查找*。

### 7.7.3 演示`sort`和`binary_search`函数

图 7.15 首先创建一个未排序的`string`类型`array`（第 12–13 行），并显示该`array`的内容（第 17–19 行）。接下来，第 21 行使用 C++ 标准库函数`sort`将`array` `colors`的元素按升序排序。`sort`函数的参数指定应排序的元素范围——在本例中为整个`array`。参数`colors.begin()`和`colors.end()`分别表示该`array`的开头和结尾——我们将在第 15 章讨论`begin`和`end`的完整细节。正如你将看到的，函数`sort`可用于排序几种不同类型数据结构中的元素。第 25–27 行显示排序后`array`的内容。

```cpp
// Fig. 7.15: Fig07_15.cpp
// Sorting and searching arrays.
#include <iostream>
#include <iomanip>
#include <array>
#include <string>
#include <algorithm> // contains sort and binary_search
using namespace std;

int main() {
   const size_t arraySize{7}; // size of array colors
   array<string, arraySize> colors{"red", "orange", "yellow",
      "green", "blue", "indigo", "violet"};

   // output original array
   cout << "Unsorted array:\n";
   for (string color : colors) {
      cout << color << " ";
   }

   sort(colors.begin(), colors.end()); // sort contents of colors

   // output sorted array
   cout << "\n\nSorted array:\n";
   for (string item : colors) {
      cout << item << " ";
   }

   // search for "indigo" in colors
   bool found{binary_search(colors.begin(), colors.end(), "indigo")};
   cout << "\n\n\"indigo\" " << (found ? "was" : "was not")
        << " found in colors" << endl;

   // search for "cyan" in colors
   found = binary_search(colors.begin(), colors.end(), "cyan");
   cout << "\"cyan\" " << (found ? "was" : "was not")
        << " found in colors" << endl;
}
```

```text
Unsorted array:
red orange yellow green blue indigo violet
Sorted array:
blue green indigo orange red violet yellow

"indigo" was found in colors
"cyan" was not found in colors
```

图 7.15 对`array`进行排序和查找。

第 30 行和第 35 行使用`binary_search`来确定某个值是否在`array`中。值序列必须首先按升序排序——`binary_search`*不会*为你验证这一点。该函数的前两个参数表示要搜索的元素范围，第三个参数是*搜索键*——即要在`array`中定位的值。该函数返回一个`bool`值，指示是否找到了该值。在第 16 章中，我们将使用 C++ 标准函数`find`来获取搜索键在`array`中的位置。

## 7.8 多维`array`

你可以使用具有两个维度（即下标）的`array`来表示由按**行**和**列**排列的信息组成的**值表**。要标识一个特定的表元素，我们必须指定两个下标——按照约定，第一个标识元素的*行*，第二个标识元素的*列*。需要两个下标来标识特定元素的`array`称为**二维数组**或**2-D 数组**。具有两个或更多维度的`array`称为**多维数组**。**图 7.16** 展示了一个二维`array`，即 **a**。该`array`包含三行四列，因此称其为 3 乘 4 的`array`。通常，具有 *m* 行和 *n* 列的`array`称为 *m* 乘 *n* 的`array`。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_944_0.png)

**图 7.16** 具有三行四列的二维`array`。

在`array` `a`中，每个元素在**图 7.16** 中通过形如`a[i][j]`的元素名称来标识，其中`a`是`array`的名称，`i`和`j`是唯一标识`a`中每个元素的下标。注意，第 0 行所有元素的名称都有*第一个*下标`0`；第 3 列所有元素的名称都有*第二个*下标`3`。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_945_0.png)

## 常见编程错误 7.5

*将二维`array`元素`a[x][y]`错误地引用为`a[x, y]`是一种错误。实际上，`a[x, y]`会被视为`a[y]`，因为 C++ 将表达式`x, y`（包含逗号运算符）简单地求值为`y`（逗号分隔表达式中的最后一个）。*

**图 7.17** 演示了在声明中初始化二维`array`。第 12–13 行分别声明了一个具有两行三列的`array`的`array`。注意嵌套的`array`类型声明。在每个`array`中，其元素的类型被指定为

```cpp
array<int, columns>
```

这表示每个`array`包含的元素是三个`int`值组成的`array`——常量`columns`的值为 3。

```cpp
// Fig. 7.17: fig07_17.cpp
// Initializing multidimensional arrays.
#include <iostream>
#include <array>
using namespace std;

const size_t rows{2};
const size_t columns{3};
void printArray(const array<array<int, columns>, rows>&);

int main() {
    array<array<int, columns>, rows> array1{1, 2, 3, 4, 5, 6};
    array<array<int, columns>, rows> array2{1, 2, 3, 4, 5};

    cout << "Values in array1 by row are:" << endl;
    printArray(array1);

    cout << "\nValues in array2 by row are:" << endl;
    printArray(array2);
}

// output array with two rows and three columns
void printArray(const array<array<int, columns>, rows>& a) {
    // loop through array's rows
    for (auto const& row : a) {
        // loop through columns of current row
        for (auto const& element : row) {
            cout << element << ' ';
        }

        cout << endl; // start new line of output
    }
}
```

```text
Values in array1 by row are:
1 2 3
4 5 6

Values in array2 by row are:
1 2 3
4 5 0
```

图 7.17 初始化多维`array`。

`array1`的声明（第 12 行）提供了六个初始化器。编译器先初始化第 0 行的元素，然后是第 1 行的元素。因此，前三个值将第 0 行的元素初始化为 1、2 和 3，后三个值将第 1 行的元素初始化为 4、5 和 6。`array2`的声明（第 13 行）只提供了五个初始化器。初始化器先赋值给第 0 行，然后是第 1 行。任何没有显式初始化器的元素都被初始化为零，因此`array2[1][2]`为 0。

程序调用函数`printArray`来输出每个`array`的元素。注意，函数原型（第 9 行）和定义（第 23–33 行）指定函数接收一个两行三列的`array`。该参数通过引用接收`array`，并声明为`const`，因为该函数不修改`array`的元素。

## 嵌套的基于范围的`for`语句

要处理二维`array`的元素，我们使用嵌套循环，其中*外层*循环遍历*行*，*内层*循环遍历给定行的*列*。函数`printArray`的嵌套循环是使用基于范围的`for`语句实现的。第 25 行和第 27 行引入了 C++11 的`auto`关键字，它告诉编译器根据变量的初始化值推断（确定）变量的数据类型。外层循环的范围
