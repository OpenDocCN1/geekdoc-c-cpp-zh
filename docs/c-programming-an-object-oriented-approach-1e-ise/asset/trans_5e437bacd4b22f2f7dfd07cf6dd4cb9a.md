

## 程序 8.14 创建频率数组和直方图

```cpp
/********************************************************
 * The program reads a list of integers from a file and creates a *
 * frequency array and histogram for the list of integers between *
 * 0 and 9 (inclusive).                                      *
 *************************************************************/
#include <iostream>
#include <fstream>
#include <iomanip>
using namespace std;

int main( )
{
    // Declaration and initialization
    const int CAPACITY = 10;
    int frequencies [CAPACITY] = {0};
    ifstream integerFile;
    // Opening integer file
    integerFile.open ("integerFile.dat");
    if (!integerFile)
    {
        cout << "Error. Integer file cannot be opened." << endl;
        cout << "The program is terminated.";
        return 0;
    }
    // Reading from the integer file and creating frequency array
    int data;
    int size = 0;
    while (integerFile >> data )
    {
        if (data >= 0 && data <= 9)
        {
            size++;
            frequencies[data]++;
        }
    }
    // Closing integer file
    integerFile.close();
    // Printing frequencies and histogram
    cout << "There are " << size << " valid data items." << endl;

    for (int i = 0; i < 10; i++)
    {
        cout << setw(3) << i << " ";
        for (int f = 1; f <= frequencies[i]; f++)
        {
            cout << '*';
        }
        cout << " " << frequencies[i] << endl;
    }
    return 0;
}
```

**运行结果：**

```text
There are 202 valid data items.
0 ********************** 22
1 **** 4
2 ******************* 19
3 ************* 13
4 ******************** 20
5 ********************************* 33
6 **************************** 28
7 **************************** 28
8 ************************* 25
9 ********** 10
```

每行中的星号数量实际上就是对应整数的计数。下面显示了我们使用的整数文件的内容。请注意，列表中共有 205 个整数，但其中三个（以彩色显示）不在 0 到 9 的范围内。这意味着程序读取了全部 205 个整数，但频率数组仅由 202 个整数构成。

```text
13225732806467078542306758548965592352678
06467078542306758548967078542306758548965
270785423067585489651597078542306758965664
59707854230675896566427078542306758548965
132257328064671078542300646707854230675811
```

## 8.4.2 线性变换

我们之前提到过，在将二维数组线性变换为一维数组时，我们有两种选择：行变换和列变换。第一种方式是逐行进行变换；第二种方式是逐列进行变换（图 8.20）。

## 理解问题

我们必须找到一种逻辑，使我们能够将 N 行 M 列数组中的数据转换为包含 N × M 个元素的一维序列。

![](img/d68f6199646ca63591a6d8419e0ed4ba_391_0.png)

**图 8.20** 线性变换

## 设计算法

我们声明并初始化一个二维数组。对于小型数组，我们可以直接输入值；对于大型数组，我们会从文件中读取数据。我们定义四个函数：

- 1. 第一个函数逐行变换数组，并创建一个我们称之为 *rowArray* 的数组。
- 2. 第二个函数逐列变换数组，并创建一个我们称之为 *colArray* 的数组。
- 3. 第三个函数打印二维数组。
- 4. 第四个函数打印两个一维数组中的任意一个。

*main* 函数的工作非常简单。在声明并初始化二维数组之后，它调用第一个函数和第二个函数来创建一维数组。然后，它调用相应的函数来打印二维数组以及每一个一维数组。

## 编写程序

程序 8.15 给出了基于上述说明的代码。

## 程序 8.15 数组变换

```cpp
/**********************************************************************
 * The program shows how to transform a two-dimensional array to       *
 * two one-dimensional arrays using row-by-row or column-by-column    *
 * transformation.                                                     *
 **********************************************************************/
#include <iostream>
#include <iomanip>
using namespace std;
```

## 程序 8.15 数组变换（续）

```cpp
52 /************************************************************
53  * The function prints the contents of a two-dimensional array
54  * passed to it as a constant argument.
55  ************************************************************/
56 void printTwoDimensional (const int twoDimensional [][4],
57                            int rowSize)
58 {
59    for (int i = 0; i < rowSize; i++)
60    {
61       for (int j = 0; j < 4; j++)
62       {
63          cout << setw (4) << twoDimensional [i][j];
64       }
65       cout << endl;
66    }
67    cout << endl;
68 }
69
70 /************************************************************
71  * The function prints the contents of a one-dimensional array
72  * passed to it as a constant argument.
73  ************************************************************/
74 void printOneDimensional (const int oneDimensional[], int size)
75 {
76    for (int i = 0; i < size; i++)
77    {
78       cout << setw (4) << oneDimensional[i];
79    }
80    cout << endl;
81 }
82
83 int main ( )
84 {
85    // Declaration of three arrays and initialization of the first
86    int originArray [2][4] = {{0, 1, 2, 3}, {10, 11, 12, 13}};
87    int rowArray [8];
88    int colArray [8];
89    // Calling two functions to transform arrays
90    rowTransform (originArray, 2, rowArray);
91    colTransform (originArray, 2, colArray);
92    // Printing the two-dimensional array
93    cout << " Original Array " << endl;
94    printTwoDimensional (originArray, 2);
```

## 程序 8.15 数组变换（续）

```cpp
// Printing the row-transformed one-dimensional array
cout << "Row-Transformed Array: ";
printOneDimensional(rowArray, 8);
// Printing the col-transformed one-dimensional array
cout << "Column-Transformed Array: ";
printOneDimensional(colArray, 8);
return 0;
}
```

**运行结果：**

```text
Original Array
  0   1   2   3
 10  11  12  13

Row-Transformed Array:    0   1   2   3  10  11  12  13
Column-Transformed Array: 0  10   1  11   2  12   3  13
```

## 关键术语

- 数组声明
- 频率数组
- 直方图
- 线性化
- 多维数组
- 一维数组
- 平行数组
- 下标
- 三维数组
- 二维数组

## 小结

数组是相同类型数据项的序列。数组是一种复合类型；我们可以拥有除 `void` 之外任何类型的数组。数组具有三个属性：*类型、大小和容量*。要声明数组，我们指定其类型、名称和用方括号括起来的容量。在程序全局区域中声明的数组会使用默认值进行初始化。在函数内部声明的数组会使用先前操作遗留的垃圾值进行初始化。

在一维数组中，每个元素都可以通过单个下标来访问。访问二维数组中的元素需要两个下标，分别表示行和列。二维数组上有几种常见操作：折叠、转置和线性化。我们不仅限于二维；然而，超过三维的数组非常少见。

## 习题

**PR-1.** 给定以下声明，编写代码打印下标为偶数的数组元素。

```cpp
int arr[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
```

**PR-2.** 给定以下声明，编写代码打印数组的前五个元素。

```cpp
int arr [12] = {0, 10, 20, 39, 40, 50, 60, 70, 80, 90};
```

**PR-3.** 使用以下声明，编写代码将下标为偶数的元素填充为整数 0，将下标为奇数的元素填充为整数 1。

```cpp
int arr [10];
```

**PR-4.** 给定以下数组声明，编写代码将前五个元素填充为整数 5，将后五个元素填充为整数 10。

```cpp
int arr [10];
```

**PR-5.** 以下代码段的输出是什么？

```cpp
int arr [10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
for (int i = 0; i < 5; i++)
{
    cout << arr [i * 2] << " ";
}
```

**PR-6.** 以下代码段的输出是什么？

```cpp
int arr [10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
for (int i = 0; i < 5; i++)
{
    arr [i] = arr [i * 2 + 1];
    cout << arr [i] << endl;
}
```

**PR-7.** 以下代码段的输出是什么？

```cpp
int arr1 [5] = {0, 1, 2, 3, 4};
int arr2 [5];
for (int i = 0; i < 5; i++)
{
    arr2 [i] = arr1 [i];
    cout << arr1 [i] + arr2 [i] << endl;
}
```

**PR-8.** 以下代码段的输出是什么？

```cpp
int arr [5] = {0, 1, 2, 3, 4};
for (int i = 1; i <= 4; i++)
{
    cout << arr [i] << " ";
}
cout << endl;
```

**PR-9.** 编写代码，创建另一个数组 arr2，其元素与以下名为 arr1 的数组的顺序相反。

```cpp
int arr1 [10] = {0, 10, 20, 39, 40, 50, 60, 70, 80, 90};
```

