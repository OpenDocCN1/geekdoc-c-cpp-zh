
### 表 18-2 查找项 34 时 first、last 和 mid 的值以及比较次数

| 迭代 | first | last | mid | list[mid] | 比较次数 |
|---:|---:|---:|---:|---:|---:|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 0 | 4 | 2 | 19 | 2 |
| 3 | 3 | 4 | 3 | 25 | 2 |
| 4 | 4 | 4 | 4 | 34 | 1（found 为 true） |

该项在位置 4 找到，总比较次数为 7。

现在让我们查找项 22，如表 18-3 所示。

### 表 18-3 查找项 22 时 first、last 和 mid 的值以及比较次数

| 迭代 | first | last | mid | list[mid] | 比较次数 |
|---:|---:|---:|---|---:|---:|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 0 | 4 | 2 | 19 | 2 |
| 3 | 3 | 4 | 3 | 25 | 2 |
| 4 | 3 | 2 | 循环停止（因为 first > last） |  |  |

这是一次不成功的查找。总比较次数为 6。

例 18-2 说明了如何在程序中使用二分查找算法。

### 例 18-2

```cpp
#include <iostream>
#include "searchSortAlgorithms.h"

using namespace std;

int main()
{
    int intList[] = {2, 16, 34, 45, 53,
                     56, 69, 70, 75, 96};             //Line 1

    int pos;                                           //Line 2

    pos = binarySearch(intList, 10, 45);               //Line 3

    if (pos != -1)                                     //Line 4
        cout << "Line 5: " << 45
             << " found at position "
             << pos;                                   //Line 5
    else                                                //Line 6
        cout << "Line 7: " << 45
             << " is not in intList" << endl;          //Line 7
    return 0;
}
```

### 示例运行：

第 5 行：在位置 3 找到 45

前面的程序工作如下。第 1 行的语句创建数组 intList。（注意，数组 intList 已排序。）第 2 行的语句声明 pos 为 int 变量。第 3 行的语句使用二分查找算法判断 45 是否在 intList 中。注意，数组 intList、其长度以及查找项 45 作为参数传递给函数 binarySearch。第 4 行到第 7 行的语句输出查找结果，该查找成功。

## 二分查找的性能

假设 L 是一个大小为 1024 的有序列表，我们想确定项 x 是否在 L 中。根据二分查找算法，while 循环的每次迭代都会将查找列表的大小减半。（例如，见图 18-2 和图 18-3。）因为 1024 = 2¹⁰，while 循环最多需要 11 次迭代来确定 x 是否在 L 中。因为 while 循环的每次迭代进行两次项（键）比较，也就是说，x 会与 L 中的元素比较两次，所以二分查找最多进行 22 次比较来确定 x 是否在 L 中。另一方面，回想一下，顺序查找平均会进行 512 次比较来确定 x 是否在 L 中。

为了更好地理解二分查找相对于顺序查找有多快，假设 L 的大小为 1048576。因为 1048576 = 2²⁰，因此二分查找中的 while 循环最多需要 21 次迭代来确定某个元素是否在 L 中。while 循环的每次迭代进行两次键（即项）比较。因此，为了确定某个项是否在 L 中，二分查找最多进行 42 次项比较。

注意，40 = 2 * 20 = 2 * log₂2²⁰ = 2 * log₂(1048576)。

一般来说，假设 $L$ 是一个大小为 $n$ 的有序列表。此外，假设 $n$ 是 2 的幂，即对于某个非负整数 $m$，有 $n = 2^m$。在 while 循环的每次迭代之后，大约一半的元素留待查找，也就是说，下一次迭代的查找子列表是当前子列表大小的一半。例如，在第一次迭代之后，查找子列表的大小约为 $n/2 = 2^{m-1}$。很容易看出，while 循环的最大迭代次数约为 $m + 1$。此外，$m = \log_2 n$。每次迭代进行两次键比较。因此，确定元素 $x$ 是否在 $L$ 中所需的最大比较次数为 $2(m + 1) = 2(\log_2 n + 1) = 2\log_2 n + 2$。

在成功查找的情况下，可以证明，对于长度为 $n$ 的列表，二分查找平均进行 $2\log_2 n - 3$ 次键比较。在不成功查找的情况下，可以证明，对于长度为 $n$ 的列表，二分查找大约进行 $2\log_2 n$ 次键比较。

## 二分查找算法与 orderedArrayListType 类

第 13 章设计的 orderedArrayListType 类不包含二分查找算法。既然你已经知道如何实现二分查找算法，就可以学习如何在 orderedArrayListType 类中使用它。

为了在 orderedArrayListType 类中使用二分查找算法，我们将函数 binSearch 添加到该类，并使用适当的参数调用函数 binarySearch。

```cpp
#include "arrayListType.h"
#include "searchSortAlgorithms.h"

template <class elemType>
class orderedArrayListType: public arrayListType<elemType>
{
public:
    void insertAt(int location, const elemType& insertItem);
    void insertEnd(const elemType& insertItem);
    void replaceAt(int location, const elemType& repItem);
    int seqSearch(const elemType& searchItem) const;
    void insert(const elemType& insertItem);
    void remove(const elemType& removeItem);

    int binSearch(const elemType& item) const;

    orderedArrayListType(int size = 100);
        //Constructor
};
```

成员函数 binSearch 的定义为：

```cpp
template <class elemType>
int orderedArrayListType<elemType>::
                         binSearch(const elemType& item) const
{
    return binarySearch(list, length, item);
}
```

## 渐近记号：大 O 记号

正如在编写算法和计算机程序之前要分析问题一样，在设计算法之后，也应该对算法进行分析。通常，设计特定算法有多种方式。有些算法执行所需的计算机时间很少，而另一些算法则需要相当多的时间。考虑以下示例。

### 例 18-3

考虑以下算法（假设所有变量都已正确声明）：

```cpp
cout << "Enter the first number: ";                 //Line 1
cin >> num1;                                       //Line 2
cout << endl;                                      //Line 3

cout << "Enter the second number: ";                //Line 4
cin >> num2;                                       //Line 5
cout << endl;                                      //Line 6

if (num1 >= num2)                                  //Line 7
    max = num1;                                    //Line 8
else                                                //Line 9
    max = num2;                                    //Line 10

cout << "The maximum number is: " << max << endl;  //Line 11
```

第 1 行到第 6 行各有一个操作，即 << 或 >>。第 7 行有一个操作，即 >=。第 8 行或第 9 行会执行；每行各有一个操作。第 11 行有三个操作。因此，前面代码中执行的操作总数为 6 + 1 + 1 + 3 = 11。在该算法中，执行的操作数是固定的。

### 例 18-4

考虑以下算法（假设所有变量都已正确声明）：

```cpp
cout << "Enter positive integers ending with -1"
     << endl;                                      //Line 1

count = 0;                                         //Line 2
sum = 0;                                           //Line 3

cin >> num;                                        //Line 4

while (num != -1)                         //Line 5
{
    sum = sum + num;                       //Line 6
    count++;                               //Line 7
    cin >> num;                            //Line 8
}

cout << "The sum of the numbers is: " << sum
     << endl;                              //Line 9

if (count != 0)                           //Line 10
    average = sum / count;                 //Line 11
else                                       //Line 12
    average = 0;                           //Line 13

cout << "The average is: " << average << endl; //Line 14
```

该算法在 while 循环之前有五个操作（第 1 行到第 4 行）。类似地，while 循环之后有九个或八个操作，取决于执行的是第 11 行还是第 13 行。

第 5 行有一个操作，而 while 循环内部有四个操作（第 6 行到第 8 行）。因此，第 5 行到第 8 行共有五个操作。如果 while 循环执行 10 次，这五个操作执行 10 次，另外在第 5 行还会执行一个额外操作来终止循环。因此，从第 5 行到第 8 行执行的操作数为 51。

如果 while 循环执行 10 次，执行的操作总数为：

5 × 10 + 1 + 5 + 9 或 5 × 10 + 1 + 5 + 8。

即：

5 × 10 + 15 或 5 × 10 + 14。

我们可以将其推广到 while 循环执行 n 次的情况。如果 while 循环执行 n 次，执行的操作数为：

5n + 15 或 5n + 14。

在这些表达式中，对于非常大的 n，项 5n 成为主导项，而项 15 和 14 变得可以忽略不计。

通常，在算法中，某些操作是主导操作。例如，在例 18-4 的算法中，为了对数字求和，主导操作在第 6 行。类似地，在查找算法中，由于查找项要与列表中的项进行比较，主导操作将是比较，即关系运算。因此，在查找算法的情况下，我们统计比较次数。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1278_0.png)

