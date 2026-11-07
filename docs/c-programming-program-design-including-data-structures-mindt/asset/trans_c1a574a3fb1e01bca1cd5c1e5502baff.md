
共有 \(n!\) 种不同的排列。这 \(n!\) 种排列中的任意一种都可能是 \(L\) 的正确顺序。因此，比较树必须至少有 \(n!\) 个叶结点。

现在让我们考虑所有基于比较的排序算法的最坏情况。我们不加证明地给出以下结果。

**定理：** 设 \(L\) 是一个包含 \(n\) 个不同元素的列表。任何仅通过比较关键字来排序 \(L\) 的排序算法，在最坏情况下至少进行 \(O(n\log_2 n)\) 次关键字比较。

如前几节所分析，冒泡排序、选择排序和插入排序算法的阶为 \(O(n^2)\)。本章剩余部分讨论平均情况下阶为 \(O(n\log_2 n)\) 的排序算法。

## 快速排序：基于数组的列表

在上一节中，我们注意到基于比较的算法的下界是 \(O(n\log_2 n)\)。本章前面讨论的排序算法——冒泡排序、选择排序和插入排序——的阶为 \(O(n^2)\)。在本节及接下来的两节中，我们讨论阶为 \(O(n\log_2 n)\) 的排序算法。第一个算法是快速排序算法。

快速排序算法使用分治技术对列表进行排序。列表被划分为两个子列表，然后分别排序，再以某种方式合并成一个有序列表，使得合并后的列表是有序的。因此，一般算法如下：

```text
if (the list size is greater than 1)
{
    a. Partition the list into two sublists, say lowerSublist and
       upperSublist.
    b. Quick sort lowerSublist.
    c. Quick sort upperSublist.
    d. Combine the sorted lowerSublist and sorted upperSublist.
}
```

将列表划分为名为 lowerSublist 和 upperSublist 的两个子列表后，使用快速排序算法对这些子列表进行排序。换句话说，我们使用递归来实现快速排序算法。

这里描述的快速排序算法针对基于数组的列表。用于链表的算法可以用类似方式开发，留作练习。

在快速排序算法中，列表的划分方式使得合并已排序的 lowerSublist 和 upperSublist 变得很简单。因此，在快速排序中，所有排序工作都在划分列表时完成。由于所有排序工作都发生在列表划分过程中，我们首先详细描述划分过程。

要将列表划分为两个子列表，首先选择列表中的一个元素，称为 pivot（基准）。pivot 用于将列表划分为两个子列表：lowerSublist 和 upperSublist。lowerSublist 中的元素小于 pivot，而 **上子列表** 中的元素大于或等于 **基准**。例如，考虑图 18-19 中的列表。

![](img/b217c421655b51e7494cf3b89bb5432d_1361_0.png)
图 18-19 划分前的 *列表*

确定 **基准** 有几种方法。然而，选择 **基准** 时希望 **下子列表** 和 **上子列表** 的大小几乎相等。为说明起见，我们选择列表的中间元素作为 **基准**。我们描述的划分过程使用中间元素作为 **基准** 来划分此列表，在我们的例子中为 50，如图 18-20 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1361_1.png)
图 18-20 划分后的 *列表*

从图 18-20 可以看出，将 **列表** 划分为 **下子列表** 和 **上子列表** 后，**基准** 处于正确位置。因此，在排序 **下子列表** 和 **上子列表** 后，合并两个已排序子列表很简单。

划分算法如下（我们假设 **基准** 选为列表的中间元素）。

- 1. 确定 **基准**，并将 **基准** 与列表的第一个元素交换。

  假设索引 **smallIndex** 指向小于 **基准** 的最后一个元素。索引 **smallIndex** 初始化为列表的第一个元素。
- 2. 对于列表中的其余元素（从第二个元素开始）：
  如果当前元素小于 **基准**，
  - a. 递增 **smallIndex**。
  - b. 将当前元素与 **smallIndex** 指向的数组元素交换。
- 3. 将第一个元素，即 **基准**，与 **smallIndex** 指向的数组元素交换。

步骤 2 可以使用 **for** 循环实现，循环从列表的第二个元素开始。

步骤 1 确定基准并将基准移到第一个数组位置。在步骤 2 执行期间，列表元素按图 18-21 所示排列。（假设包含列表元素的数组名为 `list`。）

![](img/b217c421655b51e7494cf3b89bb5432d_1362_0.png)
图 18-21 步骤 2 执行期间的列表

如图 18-21 所示，`pivot` 位于第一个数组位置。下子列表中的元素小于 `pivot`；上子列表中的元素大于或等于 `pivot`。变量 `smallIndex` 包含下子列表最后一个元素的索引；变量 `index` 包含下一个需要移动的元素的索引，该元素可能在下子列表或上子列表中。如步骤 2 所示，如果列表的下一个元素（即 `list[index]`）小于 `pivot`，我们将 `smallIndex` 前进到下一个数组位置，并交换 `list[index]` 与 `list[smallIndex]`。接下来，我们说明步骤 2。

假设列表如图 18-22 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1362_1.png)
图 18-22 排序前的列表

步骤 1 要求我们确定 `pivot` 并将其与第一个数组元素交换。对于图 18-22 中的列表，中间元素位于位置 (0 + 13) / 2 = 6。也就是说，`pivot` 位于位置 6。因此，将 `pivot` 与第一个数组元素交换后，列表如图 18-23 所示。（注意，在图 18-23 中，52 与 32 交换。）

![](img/b217c421655b51e7494cf3b89bb5432d_1362_2.png)
图 18-23 将 pivot 移到第一个数组位置后的列表

假设在执行步骤 2 几次后，列表如图 18-24 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1363_0.png)
图 18-24 步骤 2 迭代几次后的列表

如图 18-24 所示，需要移入子列表的下一个列表元素由 index 指示。因为 `list[index] < pivot`，我们需要将元素 `list[index]` 移入下子列表。为此，我们首先将 `smallIndex` 前进到下一个数组位置，然后交换 `list[smallIndex]` 与 `list[index]`。结果列表如图 18-25 所示。（注意，11 与 96 交换。）

![](img/b217c421655b51e7494cf3b89bb5432d_1363_1.png)
图 18-25 将 11 移入下子列表后的列表

现在考虑图 18-26 中的列表。

![](img/b217c421655b51e7494cf3b89bb5432d_1363_2.png)
图 18-26 将 58 移入子列表前的列表

对于图 18-26 中的列表，`list[index]` 为 58，大于 `pivot`。因此，`list[index]` 应移入上子列表。这通过将 58 留在其位置并将上子列表的大小增加一、延伸到下一个数组位置来实现。将 58 移入上子列表后，列表如图 18-27 所示。

pivot 的位置，以便我们可以确定子列表的起始和结束位置。函数 `partition` 的定义如下：

```cpp
template <class elemType>
int partition(elemType list[], int first, int last)
{
    elemType pivot;

    int smallIndex;

    swap(list, first, (first + last) / 2);

    pivot = list[first];
    smallIndex = first;

    for (int index = first + 1; index <= last; index++)
        if (list[index] < pivot)
        {
            smallIndex++;
            swap(list, smallIndex, index);
        }

    swap(list, first, smallIndex);

    return smallIndex;
} //end partition
```

注意，形参 `first` 和 `last` 分别指定要划分的列表子列表的起始和结束索引。如果 `first = 0` 且 `last = length - 1`，则划分整个列表。

从函数 `partition` 的定义可以看出，列表中某些元素需要交换。下面的函数 `swap` 完成此操作。（注意，此 swap 函数与本章前面为选择排序算法给出的函数相同。）

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

一旦列表被划分为 `lowerSublist` 和 `upperSublist`，我们再次应用快速排序函数对两个子列表进行排序。因为两个子列表都使用相同的快速排序算法排序，实现此算法的最简单方法是使用递归。因此，本节给出快速排序算法的递归版本。正如所解释的
