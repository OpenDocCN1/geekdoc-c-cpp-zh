
如图 18–24 所示，列表中下一个需要移入子表的元素由 `index` 指示。因为 `list[index] < pivot`，所以需要将元素 `list[index]` 移入下子表。为此，我们首先将 `smallIndex` 推进到下一个数组位置，然后将 `list[smallIndex]` 与 `list[index]` 交换。结果列表如图 18–25 所示。（注意，11 与 58 发生了交换。）

![](img/d0be7fc6d804b63484835c6c8bc67a07_1352_0.png)

**图 18-25** 将 11 移入下子表后的列表

现在考虑图 18–26 中的列表。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1352_1.png)

**图 18-26** 将 58 移入子表之前的列表

对于图 18–26 中的列表，`list[index]` 为 58，它大于枢轴。因此，`list[index]` 将被移入上子表。实现方法是：将 58 保留在其位置，并将上子表的大小增加一个位置，即扩展到下一个数组位置。将 58 移入上子表后，列表如图 18–27 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1352_2.png)

**图 18-27** 将 58 移入上子表后的列表

在将小于枢轴的元素移入下子表、将大于枢轴的元素移入上子表之后（即完全执行完第 2 步之后），得到的列表如图 18-28 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1353_0.png)

接下来，我们执行第 3 步，将 52（枢轴）移到列表中合适的位置。这是通过将 52 与 45 交换来实现的。得到的列表如图 18-29 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1353_1.png)

如图 18-29 所示，前面算法中的第 1、2、3 步将列表划分为两个子表。小于枢轴的元素位于下子表中；大于或等于枢轴的元素位于上子表中。

为了将列表划分为下子表和上子表，我们只需要跟踪下子表的最后一个元素，以及列表中下一个需要移入下子表或上子表的元素。实际上，上子表位于两个索引 `smallIndex` 和 `index` 之间。

现在编写函数 `partition` 来实现前面的划分算法。在重新排列列表元素之后，函数 `partition` 返回枢轴的位置，以便我们可以确定子表的起始和结束位置。函数 `partition` 的定义为：

```cpp
template <class elemType>
int partition(elemType list[], int first, int last)
{
    elemType pivot;

    int index, smallIndex;

    swap(list, first, (first + last) / 2);

    pivot = list[first];
    smallIndex = first;

    for (index = first + 1; index <= last; index++)
        if (list[index] < pivot)
        {
            smallIndex++;
            swap(list, smallIndex, index);
        }

    swap(list, first, smallIndex);

    return smallIndex;
} //end partition
```

注意，形参 `first` 和 `last` 分别指定要划分的列表子表的起始索引和结束索引。如果 `first = 0` 且 `last = length - 1`，则对整个列表进行划分。

从函数 `partition` 的定义可以看出，列表中的某些元素需要交换。下面的函数 `swap` 完成此任务。（注意，这个 `swap` 函数与本章前面为选择排序算法给出的 `swap` 函数相同。）

```cpp
template <class elemType>
void swap(elemType list[], int first, int second)
{
    elemType temp;

    temp = list[first];
    list[first] = list[second];
    list[second] = temp;
} //end swap
```

一旦列表被划分为 `lowerSublist` 和 `upperSublist`，我们再次应用快速排序函数对这两个子表进行排序。由于两个子表都使用相同的快速排序算法排序，实现该算法最简单的方法是使用递归。因此，本节给出快速排序算法的递归版本。如前所述，在重新排列列表元素之后，函数 `partition` 返回枢轴的索引，以便可以确定子表的起始索引和结束索引。

给定列表的起始索引和结束索引，下面的函数 `recQuickSort` 实现快速排序算法的递归版本：

```cpp
template <class elemType>
void recQuickSort(elemType list[], int first, int last)
{
    int pivotLocation;

    if (first < last)
    {
        pivotLocation = partition(list, first, last);
        recQuickSort(list, first, pivotLocation - 1);
        recQuickSort(list, pivotLocation + 1, last);
    }
} //end recQuickSort
```

最后，我们编写快速排序函数 `quickSort`，它在原始列表上调用函数 `recQuickSort`：

```cpp
template <class elemType>
void quickSort(elemType list[], int length)
{
    recQuickSort(list, 0, length - 1);
} //end quickSort
```

我们将编写程序测试快速排序算法留作练习。参见本章末尾的编程练习 10。

## 分析：快速排序

快速排序算法的一般分析超出了本书范围。不过，让我们确定最坏情况下的比较次数。假设列表 L 是一个包含 n 个元素的列表，n ≥ 0。在快速排序中，所有排序工作都由函数 `partition` 完成。从函数 `partition` 的定义可知，要划分长度为 k 的列表，函数 `partition` 进行 k − 1 次关键字比较。此外，在最坏情况下，划分之后，一个子表的长度为 k − 1，另一个子表的长度为 0。

由此可知，在最坏情况下，函数 `partition` 的第一次调用进行 n − 1 次关键字比较。在第二次调用中，函数 `partition` 划分长度为 n − 1 的列表，因此进行 n − 2 次关键字比较，依此类推。现在可以得出结论：在最坏情况下，要对长度为 n 的列表进行排序，快速排序进行的关键字比较总次数为：

(n − 1) + (n − 2) + ⋯ + 2 + 1 = n(n − 1)/2 = O(n²)。

表 18-10 总结了长度为 n 的列表的快速排序算法的行为。

**表 18-10 长度为 n 的列表的快速排序算法分析**

|  | 比较次数 | 交换次数 |
|---|---|---|
| 平均情况 | (1.39) log₂ n + O(n) = O(n log₂ n) | (0.69) log₂ n + O(n) = O(n log₂ n) |
| 最坏情况 | n²/2 − n/2 = O(n²) | n²/2 + 3n/2 − 2 = O(n²) |

## 归并排序：基于链表的列表

上一节中，我们描述了快速排序算法，并指出快速排序的平均情况行为为 O(n log₂ n)。然而，快速排序的最坏情况行为为 O(n²)。本节描述行为始终为 O(n log₂ n) 的排序算法。

与快速排序算法一样，归并排序算法使用分治技术对列表进行排序。归并排序算法也会将列表划分为两个子表，对子表排序，然后将已排序的子表合并为一个有序列表。本节描述基于链表的列表的归并排序算法。我们将基于数组的列表的归并排序算法留给你开发，可以使用为链表描述的技术来完成。

归并排序和快速排序算法在划分列表的方式上不同。如前所述，快速排序首先选择列表中的一个元素，称为枢轴，然后划分列表，使一个子表中的元素小于枢轴，另一个子表中的元素大于或等于枢轴。相比之下，归并排序将列表划分为两个大小几乎相等的子表。例如，考虑元素如下的列表：

```text
list: 35  28  18  45  62  48  30  38
```

归并排序算法将该列表划分为两个子表，如下所示：

```text
first sublist: 35  28  18  45
second sublist: 62  48  30  38
```

这两个子表使用与原始列表相同的算法（即归并排序）进行排序。假设我们已经对两个子表进行了排序。也就是说，假设这些列表现在如下所示：

```text
first sublist: 18  28  35  45
second sublist: 30  38  48  62
```

接下来，归并排序算法将两个已排序的子表合并（即归并）为一个有序列表。

图 18–30 进一步说明了归并排序过程。

