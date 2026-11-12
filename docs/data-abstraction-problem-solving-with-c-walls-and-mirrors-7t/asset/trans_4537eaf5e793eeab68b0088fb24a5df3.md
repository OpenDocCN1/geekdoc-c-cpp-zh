

将一个半堆——一棵其子树都是堆但根可能位置不当的树——转换为堆。但是，堆中是否存在任何供 heapRebuild 处理的半堆呢？虽然图 17-8b 中的树不是半堆，但如果你查看其叶子，你会发现半堆——也就是说，每个叶子都是一个半堆。事实上，每个叶子都是一个堆，但为了简单起见，忽略这一事实。

你首先从右到左对叶子调用 heapRebuild。然后你向上移动树，知道当你到达节点 n 时，其子树都是堆，因此 heapRebuild 将根在 n 的半堆转换为堆。以下伪代码步骤将 itemCount 个项目的数组 items 转换为堆：

```
for (index = itemCount - 1 down to 0)
{
    // Assertion: The tree rooted at index is a semiheap
    heapRebuild(index)
    // Assertion: The tree rooted at index is a heap
}
```

实际上，你可以在之前的 for 语句中将 itemCount - 1 替换为 itemCount / 2。因此，我们的伪代码变为

```
for (index = itemCount / 2 down to 0)
{
    // Assertion: The tree rooted at index is a semiheap
    heapRebuild(index)
    // Assertion: The tree rooted at index is a heap
}
```

本章末尾的练习 11 要求你解释为什么可以进行此改进。图 17-9 追踪了图 17-8a 中数组的此算法。由于数组包含六个项目，for 语句中的 index 从 5 / 2 开始，即 2。

### 图 17-9 将数组转换为堆

| 步骤 | 数组 | 数组的树表示 |
|---|---|---|
| 原始数组 | 6 3 5 9 2 10 | 树图 |
| heapRebuild(2) 之后 | 6 3 10 9 2 5 | 树图 |
| heapRebuild(1) 之后 | 6 9 10 3 2 5 | 树图 |
| heapRebuild(0) 之后 | 10 9 6 3 2 5 | 树图 |

我们现在将此伪代码翻译为 C++ 以获得方法 heapCreate：

```
template<class ItemType>
void ArrayMaxHeap<ItemType>::heapCreate()
{
   for (int index = itemCount / 2; index >= 0; index--)
      heapRebuild(index);
} // end heapCreate
```

编程问题 1 要求你完成类 ArrayMaxHeap 的实现文件。
最后，我们将定义方法 peekTop，因为如果堆为空，它必须抛出异常。
你可能会想直接返回 items[0]，因为它始终包含堆顶，但如果你这样做，即使堆可能为空，peekTop 也会返回一个值。因此，你需要让 peekTop 测试空堆，如下面的定义所示：

```
template<class ItemType>
ItemType ArrayMaxHeap<ItemType>::peekTop() const throw(PrecondViolatedExcep)
{
   if (isEmpty())
      throw PrecondViolatedExcep("Attempted peek into an empty heap.");
   return items[0];
} // end peekTop
```

问题 10. 在检查点问题 5 所示的数组上执行以下伪代码语句：

```
for (index = n - 1 down to 0)
   heapRebuild(index)
```

## 17.3 优先队列 ADT 的堆实现

### 优先队列操作与堆操作类似

第 13 章的第 13.3 节介绍了优先队列 ADT，第 14 章的第 14.2 节提供了基于排序列表的实现。当时，我们提到使用堆来定义优先队列会产生更高效的实现。

一旦你实现了堆 ADT，优先队列 ADT 的实现就很简单，因为优先队列操作与堆操作完全类似。优先队列项中的优先级值对应于堆中的一个项。因此，优先队列的实现可以重用 ArrayMaxHeap。为此，我们可以将 ArrayMaxHeap 的实例用作优先队列类的数据成员，或者我们可以使用继承。虽然堆为优先队列提供了出色的实现，但优先队列不是堆。由于 ArrayMaxHeap 与优先队列类之间不存在 is-a 关系，因此公有继承不合适。但我们可以使用私有继承，这也是我们将要做的。让我们假设我们有一个优先队列 ADT 的接口，如第 13 章的练习 8 要求你编写的那样，以便我们也可以从中派生新类。

清单 17-3 包含优先队列类的头文件。

### 清单 17-3 类 Heap_PriorityQueue 的头文件

```
/* ADT priority queue: Heap-based implementation.
   File: Heap_PriorityQueue.h */
#ifndef HEAP_PRIORITY_QUEUE
#define HEAP_PRIORITY_QUEUE

#include "ArrayMaxHeap.h"
#include "PriorityQueueInterface.h"

template<class ItemType>
class Heap_PriorityQueue : public PriorityQueueInterface<ItemType>,
                           private ArrayMaxHeap<ItemType>
{
public:
    Heap_PriorityQueue();
    bool isEmpty() const;
    bool add(const ItemType& newEntry);
    bool remove();
    // @pre The priority queue is not empty.
    ItemType peek() const throw(PrecondViolatedExcep);
}; // end Heap_PriorityQueue

#include "Heap_PriorityQueue.cpp"
#endif
```

清单 17-4 中的每个方法定义都调用 ArrayMaxHeap 中的相应方法。注意方法 peek 如何处理由堆的 peekTop 方法抛出的异常，以便给出的消息提及优先队列而不是底层堆。

### 清单 17-4 类 Heap_PriorityQueue 的实现

```
/** Heap-based implementation of the ADT priority queue.
@file Heap_PriorityQueue.cpp  */

#include "Heap_PriorityQueue.h"

template<class ItemType>
Heap_PriorityQueue<ItemType>::Heap_PriorityQueue()
{
   ArrayMaxHeap<ItemType>();
}  // end constructor

template<class ItemType>
bool Heap_PriorityQueue<ItemType>::isEmpty() const
{
   return ArrayMaxHeap<ItemType>::isEmpty();
}  // end isEmpty

template<class ItemType>
bool Heap_PriorityQueue<ItemType>::add(const ItemType& newEntry)
{
   return ArrayMaxHeap<ItemType>::add(newEntry);
}  // end add

template<class ItemType>
bool Heap_PriorityQueue<ItemType>::remove()
{
   return ArrayMaxHeap<ItemType>::remove();
}  // end remove

template<class ItemType>
ItemType Heap_PriorityQueue<ItemType>::peek() const throw(PrecondViolatedExcep)
{
   try
   {
      return ArrayMaxHeap<ItemType>::peekTop();
   }
   catch (PrecondViolatedExcep e)
   {
      throw PrecondViolatedExcep("Attempted peek into an empty priority queue.");
   }  // end try/catch
}  // end peek
```

### 堆实现需要知道优先队列的最大大小

### 堆与二叉搜索树作为优先队列的比较。

堆与二叉搜索树作为优先队列的实现相比如何？如果你知道优先队列中项目的最大数量，堆是更好的实现。

### 堆始终是平衡的

因为堆是完全的，所以它始终是平衡的，这是其主要优势。如果二叉搜索树是平衡的，那么对于 n 个项目，两种实现都将具有相同的平均性能：它们都将是 O(log n)。然而，二叉搜索树的高度在插入和删除条目期间可能会增加，远远超过 log n，并将实现的效率在最坏情况下降低到 O(n)。堆实现避免了这种性能下降。在第 19 章中，你将看到如何保持搜索树平衡，但执行此操作的操作远比堆操作复杂。

### 有限且不同的优先级值。

如果你有有限数量的不同优先级值，例如整数 1 到 20，许多项目可能具有相同的不同优先级值。你可以将优先级值相同的项目按遇到它们的顺序放置。

### 队列堆

队列堆适应这种情况，每个不同的优先级值对应一个队列。要将项目插入优先队列，如果堆中尚未存在该项目优先级值的队列，则将其添加到堆中。然后将项目插入相应的队列。要从优先队列中删除项目，你删除堆中最高优先级值对应的队列前端的项目。如果此删除使队列为空，则从堆中删除该队列。本章末尾的编程问题 7 进一步讨论了不同的优先级值。

问题 11 考虑基于堆的优先队列 ADT 实现。假设 pQueue 是一个最初为空的优先队列，在以下伪代码操作序列之后，底层堆包含什么？

- pQueue.add(5)
- pQueue.add(9)
- pQueue.add(6)
- pQueue.add(7)
- pQueue.add(3)
- pQueue.add(4)
- pQueue.add(8)
- pQueue.remove()
- pQueue.add(9)
- pQueue.add(2)
- pQueue.remove()

