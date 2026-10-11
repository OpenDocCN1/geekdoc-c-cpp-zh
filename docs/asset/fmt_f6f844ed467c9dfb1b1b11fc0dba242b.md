
`newArrayIndex = itemCount`

`inPlace = false`

`while (newArrayIndex >= 0) and !inPlace`

{

  `parentIndex = (newArrayIndex - 1) / 2`

  `if (items[newArrayIndex] < items[parentIndex])`

  {

    `Swap items[newArrayIndex] and items[parentIndex]`

    `newArrayIndex = parentIndex`

  }

  `else`

  {

    `inPlace = true`

  }

}

```
**insert** 是 $O(\log n)$
`insert` 的效率类似于 `remove`。在最坏的情况下，`insert` 需要交换从叶节点到根节点路径上的项。因此，交换次数不能超过树的高度。完全树的高度始终是 $\log_2(n + 1)$，`insert` 也是 $O(\log n)$。

- **问题 7**：第 16 章中的满二叉树是半堆吗？
- **问题 8**：考虑图 17-1a 中的最大堆。如果你插入 12 然后移除 12，请画出该堆。
- **问题 9**：在执行以下伪代码操作后，初始空的 `maxHeap` 包含什么？

```
myHeap.add(2)

myHeap.add(3)

myHeap.add(4)

myHeap.add(1)

myHeap.add(9)

myHeap.remove()

myHeap.add(7)

myHeap.add(6)

myHeap.remove()

myHeap.add(5)
```

## 17.2.2 实现

ADT 堆的基于数组实现的 `ArrayHeap` 类头文件位于列表 17-2。这个堆是一个最大堆。

### 列表 17-2 ArrayMaxHeap 类头文件

```cpp
/* ADT 堆的基于数组的实现
@file ArrayHeap.h */

#ifndef _ARRAY_MAX_HEAP
#define _ARRAY_MAX_HEAP
#include "HeapInterface.h"
#include "PreViolatedException.h"
template<class ItemType>
class ArrayHeap : public HeapInterface<ItemType>
{
private:
    static const int ROOT_INDEX = 0; // 有助于可读性
    static const int DEFAULT_CAPACITY = 21; // 测试满堆的小容量
    ItemType* items; // 堆项数组
    int itemCount; // 堆项的当前计数
    int maxItems; // 堆的最大容量
    // 大多数实用方法使用数组索引作为参数
    // 并进行计算。这应该是安全的，尽管数组是
    // 实现细节，因为这些方法是私有的。
    // 返回左孩子的数组索引（如果存在）。
    int getLeftChildIndex(int nodeIndex) const;
    // 返回右孩子的数组索引（如果存在）。
    int getRightChildIndex(int nodeIndex) const;
    // 返回父节点的数组索引
    int getParentIndex(int nodeIndex) const;
    // 测试节点是否为叶节点。
    bool isLeaf(int nodeIndex) const;
    // 将半堆转换为堆。
    void heapRebuild(int subtreeRootIndex);
    // 从无序数组创建堆。
    void heapCreate();
public:
    ArrayHeap();
    ArrayMaxHeap(const ItemType someArray[], const int arraySize);
    virtual ~ArrayMaxHeap();
    // 接口公共方法
    bool isEmpty() const;
    int getNumberOfNodes() const;
    int getHeight() const;
    ItemType peek() const throw(PreViolatedException);
    bool add(const ItemType& newData);
    bool remove();
    void clear();
}; // end ArrayHeap
#endif // _ARRAY_MAX_HEAP
```

## 514 第17章 堆

```cpp
return (2 * nodeIndex) + 1;
} // end getChildIndex
```

递归方法 `heapRebuild` 严格遵循本章之前给出的伪代码；让我们假设我们已经编写了它，并在一个使用它的方法中使用。第二个构造函数从条目数组创建一个堆。为了实现这一点，该构造函数可以调用私有方法 `heapRebuild`，而该方法又会调用 `heapRebuild`。请考虑这些细节。

注意 `heapCreate` 带有参数，但它可以访问我们类的私有数据。特别地，`heapCreate`可以使用数组项和计数器 `itemCount`。这两个数据成员将作为 `heapCreate` 输出的输入。如果构造函数将值放入 `itemCount` 和数组 `items` 中，它就可以调用 `heapCreate` 将数组中的值重新排列为堆。

因此，我们如下定义构造函数：

```cpp
template class ItemType;
ArrayMaxHeap<ItemType>::
ArrayMaxHeap(const ItemType someArray[], const int arraySize):
    ArrayMaxHeap(arraySize), maxItems(2 * arraySize)
{
    // 分配数组
    items = new ItemType[2 * arraySize];
    // 将值拷贝到数组
    for (int i = 0; i < itemCount; i++)
        items[i] = someArray[i];
    // 将数组重新组织为堆
    heapCreate();
}
```

我们使用初始化器来设置 `itemCount` 和 `maxItems` 的初始值。在分配数组项后，我们将值从给数组 `someArray` 拷贝到 `items` 中。最后，我们调用 `heapCreate`。现在 `heapCreate` 必须根据数组 `items` 中的值形成堆。完成这种转换的方法是使用堆的 `add` 方法逐个将项插入堆中。然而，利用项构建堆更高效的方法如图17-8所示。例如，假设数组的初始内容所示，将数组项分配给节点，从根节点开始从左到右向下遍历。图17-8显示了生成的树。接下来，通过重复调用 `heapRebuild` 将这棵树转换为堆。

# 图 17-8 (a) 数组的初始内容；(b) 数组的完全二叉树

![](img/d0cb86b2f18b2db569968ad7c743510e_540_0.png)

(a)

(b) 将半堆——子树都是堆但根节点位置错误的树——转换为堆。但是是否有半堆供 `heapRebuild` 处理呢？虽然树17-8不是半堆，但如果你查看它的叶子节点，你会发现半堆——即每个叶子节点都是半堆。事实上，为了简单起见，请忽略每个子都是堆这一事实。

你首先从左到右对叶子节点调用 `heapRebuild1`。然后向上遍历树，因为当你到达节点 N 时，它的子树已经是堆，因此 `heapRebuild` 将将半堆 N 转换为堆。以下伪代码步骤转换 `itemCount` 个数组项：

```cpp
for (index = itemCount - 1 down to 0)
  // 断言：该索引处的树是半堆
  heapRebuild1(index)
  // 断言：该索引处的树是堆
```

实际上，你可以在上一个 `for` 语句中将 `itemCount - 1` 替换为 `itemCount / 2`。因此，我们的伪代码变为：

```cpp
for (index = itemCount / 2 down to 0)
  // 断言：该索引处的树是半堆
  heapRebuild1(index)
  // 断言：该索引处的树是堆
```

本章末的练习11要求你解释为什么这种改进是可能的。图17-9追踪了该算法应用于图17-8a中的数组。由于数组包含六个项，`for` 语句中的 `index` 从 5 / 2（即 2）开始。

```cpp
template<class ItemType>
ItemType Heap_PriorityQueue<ItemType>::peek() const throw (PrecondViolatedEx)
{
  try {
    return ArrayMaxHeap<ItemType>::peekTop();
  } catch (PrecondViolatedEx e) {
    throw PrecondViolatedEx("Attempted peek into an empty priority queue.");
  } // end try/catch
} // end peek
```

堆的实现需要知道优先队列的最大尺寸。

堆与二叉搜索树作为优先队列。作为优先队列的实现，堆与二叉搜索树相比如何？如果你知道优先队列中的最大数量，堆是更好的实现。因为堆是完全树，所以它总是平衡的，这是它的主要优势。如果二叉搜索树是平衡的，那么两种实现在 n 个元素平均性能将是相同的：都是 O(log n)。然而，二叉树的高度在插入和删除条目期间可能会增加，导致 log n 增大，并在最坏情况下将实现效率退化为 O(n)。堆的实现避免了这种下降。在第 19 章中，你将看到如何保持搜索树的平衡，但执行这些操作的方法比堆的操作复杂得多。

堆总是平衡的。

有限且离的优先级值。如果你有一组不同的优先级值（例如从 1 到 20 的整数），许多元素可能会具有相同的优先级值。你可以按照遇到的顺序放置优先级值相同的元素。队列堆（heap of queues）可以适应这种情况，为每个不同的优先级值提供一个队列。要向优先队列插入一个元素，如果该优先级值尚不存在，则将元素的优先级值添加到堆中。然后将元素插入相应的队列中。要从优先队列中删除元素，从与堆中最高优先级值对应的队列头部删除它。如果删除后队列为空，则从堆中移除该元素。本章末的编程问题 7 进一步讨论了优先级值。

队列堆。

问题 11 考虑一种基于堆的 ADT 优先队列实现。假设 pname 是一个初始为空的优先队列，在执行以下伪代码操作序列后，底层堆包含什么？

```cpp
pqueue.add(5)
pqueue.add(9)
pqueue.add(6)
pqueue.add(7)
pqueue.add(3)
pqueue.add(4)
pqueue.remove()
pqueue.add(9)
pqueue.add(2)
pqueue.remove()
```

![](img/d0cb86b2f18b2db569968ad7c743510e_544_0.png)

# 17.4 堆排序

如其名所示，堆排序算法使用堆来对处于特定顺序的元素数组进行排序。假设我们使用一个堆和一个大小等于堆元素数量的数组。调用 `peekTop` 获取堆中最大的元素，我们可以将该元素放在数组的末尾。调用 `remove` 从堆中移除它。通过反复调用 `peekTop` 和 `remove`，我们可以按降序从堆中移动元素，并按递减的位置顺序放在数组中。结果是一个按升序排序的数组。

虽然这种方法可行，但它使用的内存和时间比所需的更多。让我们从一个无序值的数组开始。我们的第一步是将数组转换为堆。回想我们在 17.2.2 节中对 ADT 堆实现中的 `heapCreate` 方法。该方法将数组元素（堆类的一个数据成员）转换成堆。`heapCreate` 的体体简单如下：

```cpp
for (int index = itemCount / 2; index >= 0; index--)
    heapRebuild(index);
```

作为 `ArrayHeap` 类，`heapCreate` 和 `heapRebuild` 都可以访问类的数据成员，包括数组元素及其条目数量 `itemCount`。要在堆排序中使用 `heapRebuild`，我们必须重新审视它接受数组及其大小作为参数。我们将 `heapRebuild` 定义为 `ArrayHeap` 外部的函数：

```cpp
void heapRebuild(int index, ItemType array[], int n)
```

将数组转换为堆后，堆排序将数组分为两个区域——堆区域和排序区域，如图 17-10 所示。堆区域位于 `array[0..last]`，排序区域位于 `array[last+1..n]`。初始时，堆区域是整个数组，排序区域是空的。

![](img/d0cb86b2f18b2db569968ad7c743510e_545_0.png)

算法的每一步将元素 $i$ 从堆区域移动到排序区域。在此过程中，以下语句是正确的——它们是算法不变式：

- 排序区域包含 `array[]` 中的最大值，并且它们按顺序排序——即 `array[n-1]` 是最大的，`array[n-2]` 是第二，以此类推。
- 堆区域中的元素形成一个堆。

为了使不变式成立，$i$ 必须是堆区域中的最大值，因此 $i$ 必须是堆的根。为了实现这一点，我们将堆根元素与堆中的最后一个元素交换——即交换 `array[0]` 和 `array[last]`——并减少 `last` 的值。结果是从根交换到 `array[last]` 的元素成为排序区域中最小元素（位于排序区域的第一个位置）。移动后，你必须将堆区域转换回堆，因为新的根可能不在位置。你可以使用 `heapRebuild()` 调整现在的根元素，使堆区域再次成为堆。以下算法总结了这些步骤：

```cpp
// Sort anArray[0..n-1]
heapSort(anArray: ArrayType, n: integer) {
    // 构建初始堆
    for (index = n / 2 down to 0) {
        // 断言：index 处的树是堆
        heapRebuild(index, anArray, n)
        // 断言：index 处的树是堆
    }
    // 断言：anArray[0] 是 array[0..n-1] 中的最大元素
    // 通过交换元素将堆区域根元素移动到区域开头并调整大小
    Swap(anArray[0], anArray[n-1])
    heapSize = n - 1 // 减少堆区域大小，扩大排序区域
    while (heapSize > 1) {
        // 再次建立堆
        heapRebuild(0, anArray, heapSize)
        // 通过交换元素将堆区域根元素移动到区域开头并调整大小
        Swap(anArray[0], anArray[heapSize])
        heapSize-- // 减少堆区域大小，扩大排序区域
    }
}
```
