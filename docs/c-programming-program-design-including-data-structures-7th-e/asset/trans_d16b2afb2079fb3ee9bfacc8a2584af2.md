

![](img/d0be7fc6d804b63484835c6c8bc67a07_1357_0.png)

**图18-30** 归并排序算法

从图18-30可以清楚地看到，在归并排序算法中，大部分排序工作都在合并已排序的子列表时完成。

归并排序的一般算法如下：

```
if (the list is of a size greater than 1)
{
    a. Divide the list into two sublists.
    b. Merge sort the first sublist.
    c. Merge sort the second sublist.
    d. Merge the first sublist and the second sublist.
}
```

如前所述，将列表分成两个子列表——第一个子列表和第二个子列表后，两个子列表使用归并排序算法进行排序。换句话说，我们使用递归来实现归并排序算法。

接下来，我们描述必要的算法，以完成以下任务：

- 将列表分成两个大小几乎相等的子列表。
- 对两个子列表进行归并排序。
- 合并已排序的子列表。

### 划分

由于数据存储在链表中，我们不知道列表的长度。此外，链表不是一种随机访问数据结构。因此，要将列表分成两个子列表，我们需要找到列表的中间节点。

考虑图18-31中的列表。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1358_0.png)

为了找到列表的中间位置，我们用两个指针遍历列表——比如 `middle` 和 `current`。指针 `middle` 被初始化为列表的第一个节点。由于这个列表有两个以上的节点，我们将 `current` 初始化为第三个节点。（回顾一下，只有当列表的元素多于一个时我们才会排序，因为大小为1的列表已经有序。此外，如果列表只有两个节点，我们将 `current` 设置为 `nullptr`。）考虑如图18-32所示的列表。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1358_1.png)

每次将 `middle` 向前移动一个节点，我们也将 `current` 向前移动一个节点。将 `current` 向前移动一个节点后，如果 `current` 不是 `nullptr`，我们再次将 `current` 向前移动一个节点。也就是说，在大多数情况下，每当 `middle` 向前移动一个节点，`current` 就向前移动两个节点。最终，`current` 变为 `nullptr`，并且 `middle` 指向第一个子列表的最后一个节点。例如，对于图18-32中的列表，当 `current` 变为 `nullptr` 时，`middle` 指向 info 为25的节点（见图18-33）。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1359_0.png)

**图18-33** 遍历列表后的 middle

现在很容易将列表分成两个子列表。首先，使用 **middle** 的链域，我们让一个指针指向 **middle** 之后的节点。然后，将 **middle** 的链域设置为 **nullptr**。图18-34显示了由此产生的子列表。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1359_1.png)

**图18-34** 分成两个列表后的列表

这一讨论转化为下面的 C++ 函数 **divideList**：

```cpp
template <class Type>
void unorderedLinkedList<Type>::
                 divideList(nodeType<Type>* first1,
                             nodeType<Type>* &first2)
{
    nodeType<Type>* middle;
    nodeType<Type>* current;

    if (first1 == nullptr)    //list is empty
        first2 = nullptr;
    else if (first1->link == nullptr)  //list has only one node
        first2 = nullptr;
    else
    {
        middle = first1;
        current = first1->link;

        if (current != nullptr)       //list has more than two nodes
            current = current->link;
        while (current != nullptr)
```

![](img/d0be7fc6d804b63484835c6c8bc67a07_1361_0.png)

**图18-36** 设置 `newHead` 和 `lastMerged` 并向前移动 `first1` 后的子列表

在图18-36中，`first1` 指向第一个子列表中尚未与第二个子列表合并的第一个节点。因此，我们再次比较 `first1` 和 `first2` 所指向的节点，并调整较小节点的链域以及合并后列表的最后一个节点的链域，以便将较小节点移动到合并后列表的末尾。对于图18-36所示的子列表，在调整必要的链域后，我们得到图18-37。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1361_1.png)

**图18-37** 将 info 为20的节点放到合并后列表末尾后的合并列表

我们对两个子列表的剩余元素继续此过程。每次将一个节点移动到合并列表时，我们将 `first1` 或 `first2` 向前移动到下一个节点。最终，`first1` 或 `first2` 变为 `nullptr`。如果 `first1` 变为 `nullptr`，则第一个子列表首先被耗尽，因此我们将第二个子列表的剩余节点连接到部分合并列表的末尾。如果 `first2` 变为 `nullptr`，则第二个子列表首先被耗尽，因此我们将第一个子列表的剩余节点连接到部分合并列表的末尾。

根据这一讨论，我们现在可以编写 C++ 函数 `mergeList` 来合并两个已排序的子列表。两个子列表的第一个节点的指针作为参数传递给函数 `mergeList`。

```cpp
template <class Type>
nodeType<Type>* unorderedLinkedList<Type>::
                mergeList(nodeType<Type>* first1,
                          nodeType<Type>* first2)
```

```cpp
template <class Type>
void unorderedLinkedList<Type>::recMergeSort(
                         nodeType<Type>* &head)
{
    nodeType<Type>* otherHead;

    if (head != nullptr)    //if the list is not empty
        if (head->link != nullptr) //if the list has more than
                                      //one node
        {
            divideList(head, otherHead);
            recMergeSort(head);
            recMergeSort(otherHead);
            head = mergeList(head, otherHead);
        }
} //end recMergeSort
```

现在我们可以给出函数 `mergeSort` 的定义，它应该作为类 `unorderedLinkedList` 的公有成员。（注意，函数 `divideList`、`mergeList` 和 `recMergeSort` 可以作为类 `unorderedLinkedList` 的私有成员，因为这些函数仅用于实现函数 `mergeSort`。）函数 `mergeSort` 调用函数 `recMergeSort`，并将 `first` 传递给该函数。它还将 `last` 设置为指向列表的最后一个节点。函数 `mergeSort` 的定义如下：

```cpp
template <class Type>
void unorderedLinkedList<Type>::mergeSort()
{
    recMergeSort(first);

    if (first == nullptr)
        last = nullptr;
    else
    {
        last = first;
        while (last->link != nullptr)
            last = last->link;
    }
} //end mergeSort
```

我们把它留作练习，请你编写一个程序来测试归并排序算法。请参阅本章末尾的编程练习13。

### 分析：归并排序

假设 $L$ 是一个包含 $n$ 个元素的列表，其中 $n > 0$。假设 $n$ 是2的幂，即对于某个非负整数 $m$，$n = 2^m$，这样我们可以将列表分成两个子列表，每个子列表的大小为：

$$
\frac{n}{2} = \frac{2^m}{2} = 2^{m-1}.
$$

此外，每个子列表也可以分成两个大小相同的子列表。每次调用函数 `recMergeSort` 都会对函数 `recMergeSort` 进行两次递归调用，且每次调用都会将子列表分成两个大小相同的子列表。假设 $m = 3$，即 $n = 2^3 = 8$。因此，原始列表的长度为8。第一次调用函数 `recMergeSort` 将原始列表分成两个子列表，每个大小为4。然后第一次调用对函数 `recMergeSort` 进行两次递归调用。这些递归调用中的每一个都将大小为4的子列表分成两个大小为2的子列表。现在我们有四个大小为2的子列表。下一组递归调用将每个大小为2的子列表分成大小为1的子列表。所以，现在我们有八个大小为1的子列表。因此，$2^3$ 中的指数3表示递归的层次（见图18-38）。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1364_0.png)

**图18-38** 长度为8的列表调用 `recMergeSort` 的递归层次

让我们考虑一般情况 $n = 2^m$。注意递归层次数为 $m$。还要注意，要将大小为 $s$ 的已排序列表与大小为 $t$ 的已排序列表合并，最大比较次数为 $s + t - 1$。

考虑函数 `mergeList`，它将两个已排序列表合并成一个已排序列表。注意，实际工作（比较和赋值）是在这里完成的。在第0层对函数 `recMergeSort` 的初始调用产生两个子列表，每个大小为 $n/2$。排序后要合并这两个列表，最大比较次数为：

$$
\frac{n}{2} + \frac{n}{2} - 1 = n - 1 = O(n).
$$

在第1层，我们合并两组已排序列表，其中每个子列表的大小为 $n/4$。要合并两个已排序子列表（每个大小为 $n/4$），我们最多需要：

$$
\frac{n}{4} + \frac{n}{4} - 1 = \frac{n}{2} - 1
$$

