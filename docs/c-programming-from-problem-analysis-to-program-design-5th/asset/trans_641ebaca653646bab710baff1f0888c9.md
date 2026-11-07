
```
for (index = 0; index < length - 1; index++)
{
    a. Find the location, smallestIndex, of the smallest element in
       list[index]...list[length - 1]
    b. Swap the smallest element with list[index]. That is, swap
       list[smallestIndex] with list[index].
}
```

第一次循环时，我们在 list[0]...list[length - 1] 中找到最小元素，并将该最小元素与 list[0] 交换。第二次循环时，我们在 list[1]...list[length - 1] 中找到最小元素，并将该最小元素与 list[1] 交换，依此类推。

步骤 a 类似于第 9 章讨论的查找列表中最大项索引的算法。（另见第 9 章编程练习 2。）这里，我们查找列表中最小项的索引。步骤 a 的一般形式为：

```
smallestIndex = index; // assume first element is the smallest

for (location = index + 1; location < length; location++)
    if (list[location] < list[smallestIndex])
        smallestIndex = location; // current element in the list
                                  // is smaller than the smallest so
                                  // far, so update smallestIndex
```

步骤 b 将 list[smallestIndex] 的内容与 list[index] 交换。以下语句完成此任务：

```
temp = list[smallestIndex];
list[smallestIndex] = list[index];
list[index] = temp;
```

由此可知，交换这些值需要进行三次元素赋值。以下函数 selectionSort 实现了选择排序算法：

```
void selectionSort(int list[], int length)
{
    int index;
    int smallestIndex;
    int location;
    int temp;

    for (index = 0; index < length - 1; index++)
    {
        // Step a
        smallestIndex = index;

        for (location = index + 1; location < length; location++)
            if (list[location] < list[smallestIndex])
                smallestIndex = location;

        // Step b
        temp = list[smallestIndex];
        list[smallestIndex] = list[index];
        list[index] = temp;
    }
}
```

示例 10-3 中的程序说明了如何在程序中使用选择排序算法。

### 示例 10-3

```
// Selection sort

#include <iostream>

using namespace std;

void selectionSort(int list[], int length);

int main()
{
    int list[] = {2, 56, 34, 25, 73, 46, 89, 10, 5, 16}; // Line 1
    int i; // Line 2

    selectionSort(list, 10); // Line 3

    cout << "After sorting, the list elements are:"
         << endl; // Line 4
    for (i = 0; i < 10; i++) // Line 5
        cout << list[i] << " "; // Line 6

    cout << endl; // Line 7

    return 0; // Line 8
}

// place the definition of the function selectionSort given
// previously here.
```

### 示例运行：

```
After sorting, the list elements are:
2 5 10 16 25 34 46 56 73 89
```

该程序的工作方式与示例 10-1 中的程序相同。这里，我们使用选择排序算法对列表进行排序。

对于长度为 *n* 的列表，选择排序恰好进行 $\frac{n(n-1)}{2}$ 次关键字比较和 $3(n-1)$ 次元素赋值。因此，如果 $n = 1000$，那么为了对该列表排序，选择排序大约进行 500,000 次关键字比较和约 3000 次元素赋值。下一节将介绍减少比较次数的插入排序算法。

## 插入排序

如上一节所述，对于长度为 1000 的列表，冒泡排序和选择排序都会进行大约 500,000 次关键字比较，这个数字相当高。本节介绍一种称为插入排序的排序算法，它试图改善——也就是减少——关键字比较的次数。

插入排序算法通过将每个元素移动到其正确位置来对列表排序。考虑图 10-9 中给出的列表。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_613_0.png)

**图 10-9** 列表

该列表的长度为 8。此外，列表元素 list[0]、list[1]、list[2] 和 list[3] 已经按（升序）排列。也就是说，list[0]...list[3] 已排序（见图 10-10）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_613_1.png)

**图 10-10** 列表的已排序部分和未排序部分

接下来，我们考虑元素 list[4]，它是未排序列表的第一个元素。因为 list[4] < list[3]，所以需要将元素 list[4] 移动到其正确位置。因此，元素 list[4] 应移动到 list[2]（见图 10-11）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_613_2.png)

**图 10-11** 将 list[4] 移动到 list[2]

要将 `list[4]` 移动到 `list[2]`，首先将 `list[4]` 复制到临时内存空间 `temp` 中（见图 10-12）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_614_0.png)

**图 10-12** 将 `list[4]` 复制到 `temp`

接下来，我们将 `list[3]` 复制到 `list[4]`，然后将 `list[2]` 复制到 `list[3]`（见图 10-13）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_614_1.png)

**图 10-13** 在将 `list[3]` 复制到 `list[4]`、然后将 `list[2]` 复制到 `list[3]` 之前的 `list`

在将 `list[3]` 复制到 `list[4]`、并将 `list[2]` 复制到 `list[3]` 之后，列表如图 10-14 所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_614_2.png)

**图 10-14** 在将 `list[3]` 复制到 `list[4]`、然后将 `list[2]` 复制到 `list[3]` 之后的 `list`

现在我们将 temp 复制到 list[2]。图 10-15 显示了结果列表。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_615_0.png)

**图 10-15** 将 temp 复制到 list[2] 后的列表

现在 list[0]...list[4] 已排序，而 list[5]...list[7] 未排序。我们对结果列表重复此过程：将未排序列表的第一个元素移动到已排序列表中的正确位置。

从上述讨论可以看出，在排序阶段，包含该列表的数组被分为两个子列表：已排序子列表和未排序子列表。已排序子列表中的元素是有序的；未排序子列表中的元素将逐个移动到已排序子列表中的正确位置。我们使用一个索引——例如 firstOutOfOrder——指向未排序子列表中的第一个元素。最初，firstOutOfOrder 初始化为 1。

上述讨论可转化为以下伪代码：

```
for (firstOutOfOrder = 1; firstOutOfOrder < listLength;
                         firstOutOfOrder++)
    if (list[firstOutOfOrder] is less than list[firstOutOfOrder - 1])
    {
        copy list[firstOutOfOrder] into temp

        initialize location to firstOutOfOrder

        do
        {
            a. copy list[location - 1] into list[location]
            b. decrement location by 1 to consider the next element
               in the sorted portion of the array
        }
        while (location > 0 && the element in the sorted list at
                               location - 1 is greater than temp)

        copy temp into list[location]
    }
```

以下 C++ 函数实现了前面的算法：

```
void insertionSort(int list[], int listLength)
```

二分查找使用“分而治之”技术来搜索列表。首先，将查找项与列表的中间元素进行比较。如果查找项小于列表的中间元素，我们将搜索限制在列表的下半部分；否则，我们搜索列表的上半部分。

考虑以下长度为 12 的有序列表，如图 10-16 所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_617_0.png)

**图 10-16** 长度为 12 的列表

假设我们要确定 75 是否在列表中。最初，整个列表就是搜索列表（见图 10-17）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_617_1.png)

**图 10-17** 搜索列表，list[0]...list[11]

首先，我们将 75 与列表中的中间元素 list[5]（其值为 39）进行比较。由于 75 ≠ list[5] 且 75 > list[5]，接下来我们将搜索限制在 list[6]...list[11]，如图 10-18 所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_617_2.png)

**图 10-18** 搜索列表，list[6]...list[11]

现在对 list[6]...list[11] 重复上述过程，这是一个长度为 6 的列表。

由于我们经常需要确定列表的中间元素，二分查找算法通常针对基于数组的列表实现。为了确定……的中间元素
