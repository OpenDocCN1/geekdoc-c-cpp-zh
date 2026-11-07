
假设 `list[0...n − 1]` 是一个包含 n 个元素的列表，索引从 0 到 n − 1。我们想要重新排列，也就是排序，使 `list` 中的元素按递增顺序排列。冒泡排序算法的工作方式如下。

在一系列 n − 1 次迭代中，依次比较列表中的相邻元素 `list[index]` 和 `list[index + 1]`。如果 `list[index]` 大于 `list[index + 1]`，则交换元素 `list[index]` 和 `list[index + 1]`。

由此可知，较小的元素向顶部移动，较大的元素向底部移动。

在第一次迭代中，我们考虑 `list[0...n − 1]`。正如第一次迭代后你将看到的，列表中的最大元素被移动到列表的最后一个位置，即位置 n − 1。在第二次迭代中，我们考虑 `list[0...n − 2]`。第二次迭代后，列表中第二大的元素被移动到位置 n − 2，即列表的倒数第二个位置。在第三次迭代中，我们考虑 `list[0...n − 3]`，依此类推。正如你将看到的，每次迭代后，列表中未排序部分的大小都会缩小。

考虑包含五个元素的 `list[0...4]`，如图 18-6 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1335_0.png)

**图 18-6** 五个元素的列表

### 第 1 次迭代：排序 `list[0...4]`。图 18-7 展示了第一次迭代中 `list` 的元素如何重新排列。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1335_1.png)

**图 18-7** 第一次迭代期间列表中的元素

注意，在图 18-7 的第一个图中，`list[0] > list[1]`。因此，`list[0]` 和 `list[1]` 被交换。在第二个图中，比较 `list[1]` 和 `list[2]`。因为 `list[1] < list[2]`，所以它们不交换。图 18-7 的第三个图比较 `list[2]` 与 `list[3]`；因为 `list[2] > list[3]`，所以 `list[2]` 与 `list[3]` 交换。然后，在第四个图中，我们比较 `list[3]` 与 `list[4]`。因为 `list[3] > list[4]`，所以 `list[3]` 和 `list[4]` 被交换。

第一次迭代后，最大元素位于最后一个位置。因此，在下一次迭代中，我们考虑 `list[0...3]`。

### 第 2 次迭代：排序 `list[0...3]`。图 18-8 展示了第二次迭代中列表的元素如何重新排列。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1336_0.png)

**图 18-8** 第二次迭代期间列表中的元素

元素的比较和交换与第一次迭代中相同。这里只考虑列表元素 `list[0]` 到 `list[3]`。第二次迭代后，最后两个元素已处于正确位置。因此，在下一次迭代中，我们考虑 `list[0...2]`。

### 第 3 次迭代：排序 `list[0...2]`。图 18-9 展示了第三次迭代中列表的元素如何重新排列。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1336_1.png)

**图 18-9** 第三次迭代期间列表中的元素

### 第 4 次迭代：排序 `list[0...1]`。图 18-10 展示了第四次迭代中列表的元素如何重新排列。

第三次迭代后，最后三个元素已处于正确位置。因此，在下一次迭代中，我们考虑 `list[0...1]`。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1337_0.png)

**图 18-10** 第四次迭代期间列表中的元素

第四次迭代后，列表已排序。

以下 C++ 函数实现了冒泡排序算法：

```cpp
template <class elemType>
void bubbleSort(elemType list[], int length)
{
    for (int iteration = 1; iteration < length; iteration++)
    {
        for (int index = 0; index < length - iteration;
             index++)
        {
            if (list[index] > list[index + 1])
            {
                elemType temp = list[index];
                list[index] = list[index + 1];
                list[index + 1] = temp;
            }
        }
    }
} //end bubbleSort
```

示例 18-11 说明了如何在程序中使用冒泡排序算法。

### 示例 18-11（冒泡排序）

```cpp
#include <iostream>
#include "searchSortAlgorithms.h"

using namespace std;

template <class elemType>
void print(elemType list[], int length);
```

假设要用冒泡排序对长度为 $n$ 的列表 $L$ 进行排序。考虑本章给出的函数 `bubbleSort`。该函数包含嵌套的 *for* 循环。因为 $L$ 的长度为 $n$，所以外层循环执行 $n-1$ 次。对于外层循环的每次迭代，内层循环执行一定次数。让我们考虑外层循环的第一次迭代。在外层循环的第一次迭代期间，内层循环的迭代次数为 $n-1$。因此有 $n-1$ 次比较。类似地，在外层循环的第二次迭代期间，内层循环的迭代次数为 $n-2$，依此类推。因此，比较总次数为：

$$(n-1)+(n-2)+\cdots+2+1=\frac{n(n-1)}{2}=\frac{1}{2}n^2-\frac{1}{2}n=O(n^2).$$

在最坏情况下，*if* 语句体总是执行。因此，在最坏情况下，赋值次数为：

$$3\frac{n(n-1)}{2}=\frac{3}{2}n^2-\frac{3}{2}n=O(n^2).$$

如果列表已经有序，即最好情况，则赋值次数为 0。可以证明，平均而言，冒泡排序大约进行 $\frac{n(n-1)}{4}$ 次元素赋值。然而，本章给出的冒泡排序的比较次数始终为 $\frac{n(n-1)}{2}$。因此，要对大小为 1000 的列表进行排序，冒泡排序大约进行 500,000 次关键字比较和 250,000 次元素赋值。下一节介绍减少元素赋值次数的选择排序算法。

> **注意**
>
> 本章末尾的习题 9 给出了冒泡排序算法的一个版本，其中最好情况下的比较次数为 $O(n)$。

## 冒泡排序算法与 `class` `unorderedArrayListType`

第 13 章设计的类 `unorderedArrayListType` 不包含任何排序算法。既然你已经知道如何实现冒泡排序算法，就可以学习如何在类 `unorderedArrayListType` 中使用它。

为了在类 `unorderedArrayListType` 中使用二分查找算法，我们向该类添加函数 `sort`，并用适当的参数调用函数 `bubbleSort`。（注意，我们还添加了用于二分查找算法的函数。）

```cpp
template <class elemType>
class unorderedArrayListType: public arrayListType<elemType>
{
public:
    void insertAt(int location, const elemType& insertItem);
    void insertEnd(const elemType& insertItem);
    void replaceAt(int location, const elemType& repItem);
    int seqSearch(const elemType& searchItem) const;
    void remove(const elemType& removeItem);

    void sort();
    int binSearch(const elemType& item) const;

    unorderedArrayListType(int size = 100);
        //Constructor
};
```

成员函数 binSearch 和 sort 的定义如下：

```cpp
template <class elemType>
int unorderedArrayListType<elemType>::
                         binSearch(const elemType& item) const
{
    return binarySearch(list, length, item);
}
```

```cpp
template <class elemType>
void unorderedArrayListType<elemType>::sort()
{
    selectionSort(list, length);
}
```

我们把它留作练习，请你编写一个程序来测试成员函数 sort 和 binSearch。

## 选择排序：基于数组的列表

第 8 章介绍了基于数组的列表的选择排序算法。然而，第 8 章给出的选择排序算法只适用于 int 类型的数组。本节使用模板给出一个通用的选择排序算法。注意，这里给出的算法与第 8 章给出的算法略有不同。

假设 list 是要排序的数组，length 表示长度，即 list 中元素的数量。如第 9 章所述，选择排序包括以下步骤：

- a. 找到最小元素的位置。
- b. 将最小元素移到未排序列表的开头。

给定列表的起始索引 first 和结束索引 last，以下 C++ 函数返回 list[first]...list[last] 中最小元素的索引。
