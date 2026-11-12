

### FIGURE 17-4 (a) 移除堆根后的不相交堆；(b) 半堆；(c) 恢复的堆

![](img/288a0c22d14d2450c1e772f228f867b0_535_0.png)

![](img/288a0c22d14d2450c1e772f228f867b0_535_1.png)

![](img/288a0c22d14d2450c1e772f228f867b0_535_2.png)

将图 17-5b 中的半堆转换为图 17-5c 中的堆，可通过以下递归算法完成。请注意，如果算法不是从半堆开始，则无法正常工作。

```
// Converts a semiheap rooted at index rootIndex into a heap.
heapRebuild(rootIndex: integer, items: ArrayType, itemCount: integer)

// Recursively trickle the item at index rootIndex down to its proper position by
// swapping with its larger child; if the child is larger than the item.
// If the item is a leaf, nothing needs to be done.
if (the root is not a leaf)
{
   // The root must have a left child; assume it is the larger child
   largerChildIndex = 2 * rootIndex + 1   // Left child index

   if (the root has a right child)
   {
      rightChildIndex = largerChildIndex + 1   // Right child index
      if (items[rightChildIndex] > items[largerChildIndex] )
         largerChildIndex = rightChildIndex   // Larger child index
   }
   // If the item in the root is smaller than the item in the larger child, swap items
   if (items[rootIndex] < items[largerChildIndex])
   {
      Swap items[rootIndex] and items[largerChildIndex]
```

remove 的最后一步将半堆转换为堆

完全树中的每个非叶节点都有左子节点

```
// Transform the semiheap rooted at largerChildIndex into a heap
heapRebuild(largerChildIndex, items, itemCount)
}
}
// Else root is a leaf, so you are done
```

图 17-6 说明了 heapRebuild 的递归调用。

### FIGURE 17-5 图 17-4a 中堆的数组表示；(b) 图 17-4b 中的半堆；(c) 图 17-4c 中恢复的堆

![](img/288a0c22d14d2450c1e772f228f867b0_536_0.png)

### FIGURE 17-6 对 heapRebuild 的递归调用

![](img/288a0c22d14d2450c1e772f228f867b0_536_1.png)

现在，堆的 remove 操作如下使用 heapRebuild：

```
// Copy the item from the last node into the root
items[0] = items[itemCount - 1]
// Remove the last node
itemCount--
// Transform the semiheap back into a heap
heapRebuild(0, items, itemCount)
```

简要考虑 remove 的效率。由于树存储在数组中，删除节点需要交换数组条目，而不仅仅是更改几个指针。这些交换可能会让您担心，但它们不一定表示算法效率低下。最多，您需要交换多少个数组条目？在 remove 将树中最后一个节点的项复制到根之后，heapRebuild 会将此项沿树向下 trickle，直到找到其合适的位置。此项从根沿单一路径向下移动，最多到达叶节点。因此，heapRebuild 必须交换的数组项数量不超过树的高度。如您在第 15 章中所知，具有 n 个节点的完全二叉树的高度始终为 ⌈log₂(n + 1)⌉。由于每次交换需要三次数据移动，

3 x ⌈log₂(n + 1)⌉ + 1

次数据移动。因此，remove 是 O(log n)，这实际上非常高效。

## 向堆中添加项。

新项插入到树的底部，并向上 trickle 到其合适的位置，如图 17-7 所示。向上 trickle 节点很容易，因为 items[i] 中节点的父节点始终存储在 items[(i - 1) / 2] 中——当然，除非该节点是根。

![](img/288a0c22d14d2450c1e772f228f867b0_537_0.png)

add 的伪代码如下：

```
// Insert newData into the bottom of the tree
items[itemCount] = newData
// Trickle new item up to the appropriate spot in the tree
newDataIndex = itemCount
inPlace = false
while ((newDataIndex > 0) and !inPlace)
{
   parentIndex = (newDataIndex - 1) / 2
   if (items[newDataIndex] < items[parentIndex])
```

```
inPlace = true
else
{
 Swap items[newDataIndex] and items[parentIndex]
 newDataIndex = parentIndex
 }
}
itemCount++
```

insert 是 O(log n)

insert 的效率与 remove 类似。最坏情况下，insert 需要从叶节点到根节点的路径上交换数组条目。因此，交换次数不能超过树的高度。由于树的高度（完全树）始终为 \(\lfloor \log_2(n + 1) \rfloor\)，insert 也是 O(log n)。

- Question 7 第 16 章图 16-16 中的完全二叉树是半堆吗？
- Question 8 考虑图 17-1a 中的最大堆。插入 12 然后删除 12 后，绘制堆。
- Question 9 执行以下伪代码操作序列后，最初为空的堆 myHeap 包含什么？
- myHeap.add(2)
- myHeap.add(3)
- myHeap.add(4)
- myHeap.add(1)
- myHeap.add(9)
- myHeap.remove()
- myHeap.add(7)
- myHeap.add(6)
- myHeap.remove()
- myHeap.add(5)

## 17.2.2 实现

类 ArrayMaxHeap 的头文件在清单 17-2 中，该类是基于数组的堆 ADT 实现。此堆是最大堆。

```
LISTING 17-2 The header file for the class ArrayMaxHeap
/** Array-based implementation of the ADT heap.
 @file ArrayMaxHeap.h */
#ifndef _ARRAY_MAX_HEAP
#define _ARRAY_MAX_HEAP

#include "HeapInterface.h"
#include "PrecondViolatedExcep.h"

template<class ItemType>
class ArrayMaxHeap : public HeapInterface<ItemType>
{
```

```
private:
    static const int ROOT_INDEX = 0;    // Helps with readability
    static const int DEFAULT_CAPACITY = 21; // Small capacity to test for a full heap
    ItemType* items;    // Array of heap items
    int itemCount;    // Current count of heap items
    int maxItems;    // Maximum capacity of the heap

    // Most of the private utility methods use an array index as a parameter
    // and in calculations. This should be safe, even though the array is an
    // implementation detail, since the methods are private.

    // Returns the array index of the left child (if it exists).
    int getLeftChildIndex(const int nodeIndex) const;

    // Returns the array index of the right child (if it exists).
    int getRightChildIndex(const int nodeIndex) const;

    // Returns the array index of the parent node.
    int getParentIndex(const int nodeIndex) const;

    // Tests whether this node is a leaf.
    bool isLeaf(int nodeIndex) const;

    // Converts a semiheap to a heap.
    void rebuildSubtree(int subTreeRootIndex);

    // Creates a heap from an unordered array.
    void heapCreate();

public:
    ArrayMaxHeap();
    ArrayMaxHeap(const ItemType someArray[], const int arraySize);
    virtual ~ArrayMaxHeap();

    // HeapInterface Public Methods:
    bool isEmpty() const;
    int getNumberOfNodes() const;
    int getHeight() const;
    ItemType peekTop() const throw(PrecondViolatedExcep);
    bool add(const ItemType& newData);
    bool remove();
    void clear();
}; // end ArrayMaxHeap

#include "ArrayMaxHeap.cpp"
#endif
```

一些方法定义。让我们来看看 ArrayMaxHeap 中一些方法的定义，从私有方法开始。为了使代码更易读，我们建立了私有方法 getLeftChildIndex、getRightChildIndex 和 getParentIndex。这些方法的实现源于我们在 17.2 节开头的观察。例如，节点 items[i] 的左子节点是 items[2 * i + 1]，因此方法 getLeftChildIndex 具有以下定义：

```
template<class ItemType>
int ArrayMaxHeap<ItemType>::getLeftChildIndex(const int nodeIndex) const
{
```

```
return (2 * nodeIndex) + 1;
} // end getLeftChildIndex
```

递归私有方法 heapRebuild 密切遵循本章前面给出的伪代码，因此让我们假设已对其进行编码，并查看使用它的方法。第二个构造函数从条目数组创建堆。为此，该构造函数可以调用私有方法 heapCreate，而 heapCreate 则需要调用 heapRebuild。请考虑细节。

请注意，heapCreate 没有参数，但可以访问我们类的私有数据。特别是，heapCreate 可以使用数组 items 和计数器 itemCount。这两个数据成员将同时作为 heapCreate 的输入和输出。因此，如果构造函数将值放入 itemCount 和数组 items 中，它可以调用 heapCreate 将数组中的值重新排列为堆。

因此，我们可以按如下方式定义构造函数：

```
template<class ItemType>
ArrayMaxHeap<ItemType>::ArrayMaxHeap(const ItemType someArray[], const int arraySize):
    itemCount(arraySize), maxItems(2 * arraySize)
{
    // Allocate the array
    items = new ItemType[2 * arraySize];

    // Copy given values into the array
    for (int i = 0; i < itemCount; i++)
        items[i] = someArray[i];

    // Reorganize the array into a heap
    heapCreate();
} // end constructor
```

我们使用初始化列表来设置 itemCount 和 maxItems 的初始值。在分配数组 items 后，我们将给定数组 someArray 中的值复制到 items。最后，我们调用 heapCreate。

现在 heapCreate 必须从数组 items 中的值形成堆。实现此转换的一种方法是使用堆的 add 方法将项逐个插入堆中。但是，从数组中的项构建堆的更高效技术是可能的。

例如，假设数组的初始内容如图 17-8a 所示。首先，您将数组视为完全二叉树，从根开始，按从左到右的顺序将数组项分配给树节点。图 17-8b 显示了生成的树。接下来，通过反复调用 heapRebuild 将此树转换为堆。每次调用 heapRebuild

### FIGURE 17-8 (a) 数组的初始内容；(b) 数组对应的完全二叉树

| 6 | 3 | 5 | 9 | 2 | 10 |
|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 |

![](img/288a0c22d14d2450c1e772f228f867b0_540_0.png)

