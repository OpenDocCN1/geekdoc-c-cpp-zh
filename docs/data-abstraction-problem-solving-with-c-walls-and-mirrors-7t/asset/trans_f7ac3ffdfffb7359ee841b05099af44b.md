

堆与二叉搜索树相似，但与二叉搜索树在两个重要方面有所不同：

- 虽然你可以将二叉搜索树视为已排序，但堆的顺序要弱得多。
- 虽然二叉搜索树有多种不同的形状，但堆始终是完全二叉树。

在我们对堆的定义中，根包含值最大的项。这样的堆也称为**最大堆**。另一方面，**最小堆**将值最小的项放在其根中。图17-1给出了最大堆和最小堆的示例。练习1和8以及编程问题3进一步探讨了最小堆。

### 图17-1 (a) 最大堆和 (b) 最小堆

![](img/288a0c22d14d2450c1e772f228f867b0_530_0.png)

ADT堆具有以下操作：

> **注意：ADT堆操作**
> - 测试堆是否为空
> - 获取堆中的节点数
> - 获取堆的高度
> - 获取堆中的项
> - 获取堆根中的项
> - 将新项插入堆中
> - 移除堆根中的项
> - 移除堆中的所有节点
>
> 根据堆是最大堆还是最小堆，移除和检索操作分别涉及堆中最大或最小的项。

### 图17-2 类Heap的UML图

| 堆 |
| --- |
| +isEmpty(): boolean |
| +getNumberOfNodes(): integer |
| +getHeight(): integer |
| +peekTop(): ItemType |
| +add(newData: ItemType): boolean |
| +remove(): boolean |
| +clear(): void |

以下契约更详细地指定了这些操作，堆类的UML图如图17-2所示。

### 抽象数据类型：堆

- 分层排序的有限数量的对象。

| 伪代码 | 描述 |
|---|---|
| isEmpty() | 任务：查看此堆是否为空。
输入：无。
输出：如果堆为空，则为真；否则为假。 |
| getNumberOfNodes() | 任务：获取此堆中的节点数。
输入：无。
输出：堆中的节点数。 |
| getHeight() | 任务：获取此堆的高度。
输入：无。
输出：堆的高度。 |
| peekTop() | 任务：获取此堆根（顶部）中的数据。
输入：无。假设堆不为空。
输出：堆根中的项。如果堆是最大堆，则此项是堆中最大的值。对于最小堆，该项是最小值。 |
| add(newData) | 任务：将newData插入此堆。
输入：newData是要插入的数据项。
输出：如果插入成功，则为真；否则为假。 |
| remove() | 任务：移除此堆根中的项。
输入：无。
输出：如果移除成功，则为真；否则为假。 |
| clear() | 任务：移除此堆中的所有节点。
输入：无。
输出：堆为空。 |

清单17-1中出现了最终确定ADT堆操作契约的接口。

```
LISTING 17-1 An interface for the ADT heap

/* Interface for the ADT heap.
   #file HeapInterface.h */

#ifndef HEAP_INTERFACE
#define HEAP_INTERFACE

template<class ItemType>
class HeapInterface
{
public:

/** Sees whether this heap is empty.
 @return True if the heap is empty, or false if not. */
virtual bool isEmpty() const = 0;

/** Gets the number of nodes in this heap.
 @return The number of nodes in the heap. */
virtual int getNumberOfNodes() const = 0;

/** Gets the height of this heap.
 @return The height of the heap. */
virtual int getHeight() const = 0;

/** Gets the data that is in the root (top) of this heap.
 For a maxheap, the data is the largest value in the heap;
 for a minheap, the data is the smallest value in the heap.
 @pre The heap is not empty.
 @post The root's data has been returned, and the heap is unchanged.
 @return The data in the root of the heap. */
virtual ItemType peekTop() const = 0;

/** Adds a new node containing the given data to this heap.
 @param newData  The data for the new node.
 @post The heap contains a new node.
 @return True if the addition is successful, or false if not. */
virtual bool add(const ItemType& newData) = 0;

/** Removes the root node from this heap.
 @return True if the removal is successful, or false if not. */
virtual bool remove() = 0;

/** Removes all nodes from this heap. */
virtual void clear() = 0;
}; // end HeapInterface
#endif
```

> 注意：不要将ADT堆与称为堆的内存单元集合混淆。当您使用new运算符时，此内存可用于分配给您的程序。包含此可用内存的堆不是ADT堆的实例。

> 问题1 第16章图16-16中的完全二叉树是堆吗？为什么？

## 17.2 基于数组的堆实现

由于堆是二叉树，如果您知道堆的最大大小，可以使用第16章第16.1.1节中讨论的二叉树的基于数组的实现。但是，由于堆是完全二叉树，您可以使用更简单的基于数组的实现来节省内存。如您在第15章中所见，高度为h的完全树在第h-1层是满的，且第h层从左到右填充。

### 图17-3 (a) 完全二叉树的逐层编号；(b) 其基于数组的实现

![](img/288a0c22d14d2450c1e772f228f867b0_533_0.png)

| | items |
|---|---|
| 0 | Jane |
| 1 | Bob |
| 2 | Tom |
| 3 | Alan |
| 4 | Elisa |
| 5 | Nancy |
| 6 | |
| 7 | |

图17-3a显示了一棵完全二叉树，其节点按照逐层方案编号。根编号为0，根的子节点——即树的下一层节点——从左到右编号为1和2。下一层的节点从左到右编号为3、4和5。您将这些节点按数字顺序放入数组items中。也就是说，items[i]包含编号为i的节点，如图17-3b所示。现在，给定任意节点items[i]，您可以轻松定位其子节点和父节点：

- 其左子节点（如果存在）是items[2 * i + 1]
- 其右子节点（如果存在）是items[2 * i + 2]
- 其父节点（如果存在）是items[(i - 1) / 2]

请记住，只有items[0]中的根没有父节点。

这种基于数组的表示要求完全二叉树。如果树中间缺少节点，编号方案就会出错，节点之间的父子关系将变得模糊。这一要求意味着对树的任何更改都必须保持其完全性。

正如您将看到的，堆的基于数组的表示在ADT优先队列的实现中很有用。

> 如果二叉树是完全的并保持完全，您可以使用内存高效的基于数组的实现

- 问题2 图17-1a所示的最大堆由什么数组表示？
- 问题3 图17-1b所示的最小堆由什么数组表示？
- 问题4 您可以使用什么标准来判断items[i]中的节点是否为叶节点？

### 问题5 以下数组表示什么完全二叉树？

| 5 | 1 | 2 | 8 | 6 | 10 | 3 | 9 | 4 | 7 |
|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

### 问题6 上一问题中的数组表示堆吗？

### 17.2.1 基于数组的堆操作算法

让我们假设我们的堆类具有以下私有数据成员：

- items：堆项的数组
- itemCount：等于堆中项数的整数
- maxItems：等于堆最大容量的整数

数组items对应完全二叉树的基于数组的表示，例如图17-3b所示的数组。我们将假设我们正在处理整数的最大堆。

**从堆中检索项。** 首先考虑堆的peekTop操作。堆中最大的项在哪里？因为每个树节点中的项大于或等于其任一子节点中的项，最大的项必须在树的根中——即堆的顶部。因此，peekTop操作只需执行以下步骤：

```
// Return the item in the root
return items[0]
```

**从堆中移除项。** 虽然peekTop操作返回堆中最大的项（我们知道它在根中），但堆操作remove必须将其移除。如图17-4a所示，移除堆的根会留下两个不相交的堆。因此，您不想实际移除根。相反，您移除树的最后一个节点并将您的项放在根中，如图17-4b所示。这一步的结果不一定是堆。但是，它是一个完全二叉树，其左子树和右子树都是堆。唯一的问题是根中的项通常位置不对。这种结构称为半堆。

因此，您需要一种将半堆转换为堆的方法。一种策略允许根中的项沿树向下滤，直到到达一个它不会位置不对的节点；也就是说，该项将停留在第一个节点，其中它大于或等于其每个子节点中的项。为了实现这一点，您首先将半堆根中的项与其子节点中的项进行比较。如果根中的项小于其子节点中较大的项，则将根中的项与该较大的项交换。为方便起见，我们将包含较大项的子节点称为较大子节点。这一步的结果如图17-4c所示。虽然在本示例中，值5仅经过一次交换就滤到了其正确位置，但通常可能需要更多交换。

我们需要记住，在移除根之前，数组表示原始堆。remove操作将仅在此数组内移动项。图17-5显示了图17-4中堆和半堆的数组。从图17-5a中的堆到图17-5b中的半堆的转换通过以下步骤完成：

```
// Copy the item from the last node and place it into the root
items[0] = items[itemCount - 1]

// Remove the last node
itemCount--
```

