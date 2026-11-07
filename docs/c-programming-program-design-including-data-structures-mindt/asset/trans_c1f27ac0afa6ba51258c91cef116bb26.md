

**表 18-10** 长度为 *n* 的列表的快速排序算法分析

|  | 比较次数 | 交换次数 |
|---|---|---|
| 平均情况 | (1.39)*n* log₂ *n* + O(*n*) = O(*n* log₂ *n*) | (0.69)*n* log₂ *n* + O(*n*) = O(*n* log₂ *n*) |
| 最坏情况 | *n*²/2 − *n*/2 = O(*n*²) | *n*²/2 − 3*n*/2 = O(*n*²) |

## 归并排序：基于链表的列表

上一节中，我们描述了快速排序算法，并指出快速排序的平均情况行为为 O(*n* log₂ *n*)。然而，快速排序的最坏情况行为为 O(*n*²)。本节介绍一种行为始终为 O(*n* log₂ *n*) 的排序算法。

与快速排序算法一样，归并排序算法使用分治技术对列表进行排序。归并排序算法还会将列表划分为两个子表，对子表进行排序，然后将已排序的子表合并为一个有序列表。本节介绍基于链表的列表的归并排序算法。基于数组的列表的归并排序算法留给你来开发，可以使用为链表描述的技术来完成。

归并排序和快速排序算法在划分列表的方式上不同。如前所述，快速排序首先选择列表中的一个元素，称为枢轴（pivot），然后划分列表，使一个子表中的元素小于 pivot，另一个子表中的元素大于或等于 pivot。相比之下，归并排序将列表划分为两个大小几乎相等的子表。例如，考虑元素如下的列表：

```
list: 35 28 18 45 62 48 30 38
```

归并排序算法将此列表划分为两个子表，如下所示：

```
first sublist: 35 28 18 45
second sublist: 62 48 30 38
```

使用与原始列表相同的算法（即归并排序）对这两个子表进行排序。假设我们已经对两个子表进行了排序。也就是说，假设这些列表现在如下所示：

```
first sublist: 18 28 35 45
second sublist: 30 38 48 62
```

接下来，归并排序算法将两个已排序的子表合并（即归并）为一个有序列表。

图 18-30 进一步说明了归并排序过程。

接下来我们描述必要的算法，以

- 将列表划分为两个大小几乎相等的子表。
- 对两个子表进行归并排序。
- 合并已排序的子表。

### 划分

由于数据存储在链表中，我们不知道列表的长度。此外，链表不是随机访问数据结构。因此，要将列表划分为两个子表，我们需要找到列表的中间节点。

考虑图 18-31 中的列表。

![](img/b217c421655b51e7494cf3b89bb5432d_1369_0.png)

**图 18-31**  未排序的链表

为了找到列表的中间位置，我们用两个指针遍历列表——例如，`middle` 和 `current`。指针 `middle` 初始化为列表的第一个节点。由于此列表的节点数多于两个，我们将 `current` 初始化为第三个节点。（回想一下，我们仅当列表具有多于一个元素时才对其进行排序，因为大小为 1 的列表已经有序。此外，如果列表只有两个节点，我们将 `current` 设置为 `nullptr`。）考虑图 18-32 中所示的列表。

![](img/b217c421655b51e7494cf3b89bb5432d_1369_1.png)

**图 18-32**  遍历列表之前的 `middle` 和 `current`

每当我们让 `middle` 前进一个节点，就让 `current` 前进一个节点。在让 `current` 前进一个节点之后，如果 `current` 不是 `nullptr`，我们再次让 `current` 前进一个节点。也就是说，在大多数情况下，每当 `middle` 前进一个节点，`current` 就前进两个节点。最终，`current` 变为 `nullptr`，而 `middle` 指向第一个子表的最后一个节点。例如，对于图 18-32 中的列表，当 `current` 变为 `nullptr` 时，`middle` 指向 `info` 为 25 的节点（见图 18-33）。

![](img/b217c421655b51e7494cf3b89bb5432d_1370_0.png)

现在很容易将列表划分为两个子表。首先，使用 `middle` 的链接，我们将一个指针赋给后面的节点 `first2`。然后我们将 `middle` 的链接设置为 `nullptr`。图 18-34 显示了得到的子表。

![](img/b217c421655b51e7494cf3b89bb5432d_1370_1.png)

以上讨论可转化为以下 C++ 函数 `divideList`：

```cpp
template <class Type>
void unorderedLinkedList<Type>::
                     divideList(nodeType<Type>* first1,
                                 nodeType<Type>*& first2)
{
    nodeType<Type>* middle;
    nodeType<Type>* current;

    if (first1 == nullptr)   //list is empty
        first2 = nullptr;
    else if (first1->link == nullptr)  //list has only one node
        first2 = nullptr;
    else
    {
        middle = first1;
        current = first1->link;

        if (current != nullptr)  //list has more than two nodes
            current = current->link;

        while (current != nullptr)
        {
            middle = middle->link;
            current = current->link;
            if (current != nullptr)
                current = current->link;
        } //end while

        first2 = middle->link;  //first2 points to the first
                                //node of the second sublist
        middle->link = nullptr; //set the link of the last node
                                //of the first sublist to nullptr
    } //end else
} //end divideList
```

现在我们知道如何将列表划分为两个大小几乎相等的子表，接下来我们重点关注合并已排序的子表。回想一下，在归并排序中，大部分排序工作是在合并已排序子表时完成的。

### 合并

一旦子表已排序，归并排序算法的下一步就是合并已排序的子表。通过比较子表中的元素，然后调整具有较小 `info` 的节点的指针，将已排序的子表合并为一个有序列表。让我们在图 18-35 所示的子表上说明此过程。假设 `first1` 指向第一个子表的第一个节点，`first2` 指向第二个子表的第一个节点。

![](img/b217c421655b51e7494cf3b89bb5432d_1371_0.png)

图 18-35 合并前的子表

我们首先比较每个子表的第一个节点的 `info`，以确定合并后列表的第一个节点。我们将 `newHead` 设置为指向合并后列表的第一个节点。我们还使用指针 `lastMerged` 来跟踪合并后列表的最后一个节点。然后，具有较小节点的子表的第一个节点的指针前进到该子表的下一个节点。图 18-36 显示了在设置 `newHead` 和 `lastMerged` 并推进 `first1` 之后图 18-35 的子表。

![](img/b217c421655b51e7494cf3b89bb5432d_1372_0.png)

**图 18-36**  设置 `newHead` 和 `lastMerged` 并推进 `first1` 后的子表

在图 18-36 中，`first1` 指向第一个子表中尚未与第二个子表合并的第一个节点。因此，我们再次比较 `first1` 和 `first2` 所指向的节点，并调整较小节点的链接以及合并后列表的最后一个节点的链接，以便将较小节点移动到合并后列表的末尾。对于图 18-36 所示的子表，在调整必要的链接后，我们得到图 18-37。

![](img/b217c421655b51e7494cf3b89bb5432d_1372_1.png)

**图 18-37**  将 `info` 为 20 的节点放到合并后列表末尾后的合并列表

我们对两个子表的剩余元素继续此过程。每次将一个节点移动到合并后列表时，我们将 `first1` 或 `first2` 推进到下一个节点。最终，`first1` 或 `first2` 变为 `nullptr`。如果 `first1` 变为 `nullptr`，则第一个子表先耗尽，因此我们将第二个子表的剩余节点附加到部分合并列表的末尾。如果 `first2` 变为 `nullptr`，则第二个子表先耗尽，因此我们将第一个子表的剩余节点附加到部分合并列表的末尾。

根据以上讨论，我们现在可以编写 C++ 函数 `mergeList` 来合并两个已排序的子表。子表的第一个节点的指针作为参数传递给函数 `mergeList`。

```cpp
template <class Type>
nodeType<Type>* unorderedLinkedList<Type>::
                      mergeList(nodeType<Type>* first1,
                                nodeType<Type>* first2)
```

