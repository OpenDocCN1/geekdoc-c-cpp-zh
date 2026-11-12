

### 图 12-2 将字符串插入到链式节点的有序链中的位置

![](img/288a0c22d14d2450c1e772f228f867b0_381_0.png)

方法 insertSorted。向有序列表添加条目需要找到新条目在列表中的位置。由于条目已排序，您需要将新条目与有序列表中的条目进行比较，直到遇到一个不小于新条目的条目。图 12-2 描绘了一串链式节点，每个节点包含按字母顺序排序的字符串。该图显示了其他字符串“Ally”、“Cathy”、“Luke”、“Sue”和“Tom”将被插入链中的位置，以及到达这些位置所需进行的比较。

您可以从图中看出，在字符串比较中，Ally 小于 Bob，因此它将被插入链的开头。要查看 Luke 的插入位置，您会发现 Luke 大于 Bob 和 Jill 但小于 Mike。因此，Luke 在链中应位于 Mike 之前。另一方面，Sue 已经在某个节点中。您会发现 Sue 大于 Bob、Jill 和 Mike，但不大于 Sue。因此，您会将新条目 Sue 插入到现有条目 Sue 之前。最后，Tom 大于列表中的所有当前名称，因此您会将它添加到链的末尾。

> 注意：给定一个按升序排列条目的有序列表，您将新条目插入到第一个不小于新条目的条目之前。

如前几章所述，向链的开头添加新节点与在链中其他位置添加的方式不同。在开头添加很容易，因为 headPtr 引用链中的第一个节点。要在其他任何位置添加，您需要一个指向最终将出现在新节点之前的节点的指针。因此，在遍历链式节点以发现新条目所属位置时，必须保留对当前考虑节点之前的节点的引用。

以下高级算法描述了我们的策略：

```
// Adds a new entry to the sorted list.
add(newEntry)
    Allocate a new node containing newEntry
    Search the chain until either you find a node containing newEntry or you pass
    the point where it should be
    Let prevPtr point to the node before the insertion point
    if (the chain is empty or the new node belongs at the beginning of the chain)
        Add the new node to the beginning of the chain
    else
        Insert the new node after the node referenced by prevPtr
    Increment the length of the sorted list
```

假设我们在头文件中指定了私有方法 getNodeBefore，可以使用上述算法定义 insertSorted 方法，如下所示：

```cpp
template<class ItemType>
void LinkedSortedList<ItemType>::insertSorted(const ItemType& newEntry)
{
   Node<ItemType>* newNodePtr = new Node<ItemType>(newEntry);
   Node<ItemType>* prevPtr = getNodeBefore(newEntry);

   if (isEmpty() || (prevPtr == nullptr)) // Add at beginning
   {
      newNodePtr->setNext(headPtr);
      headPtr = newNodePtr;
   }
   else // Add after node before
   {
      Node<ItemType>* aftPtr = prevPtr->getNext();
      newNodePtr->setNext(aftPtr);
      prevPtr->setNext(newNodePtr);
   } // end if

   itemCount++;
} // end insertSorted
```

**私有方法 getNodeBefore。** 我们仍需要实现私有方法 getNodeBefore 以定位包含给定条目的节点之前的节点（无论该节点是否应包含或已包含该条目）。遍历列表时，我们需要两个指针。显然，我们需要一个指向当前节点的指针，以便将其条目与所需条目进行比较。但我们也必须保留一个指向前一个节点的指针，因为方法返回的就是这个指针。在以下实现中，这些指针为 curPtr 和 prevPtr。

```cpp
template<class ItemType>
Node<ItemType>* LinkedSortedList<ItemType>::
   getNodeBefore(const ItemType& anEntry) const
{
   Node<ItemType>* curPtr = headPtr;
   Node<ItemType>* prevPtr = nullptr;
   while ((curPtr != nullptr) && (anEntry > curPtr->getItem()))
   {
      prevPtr = curPtr;
      curPtr = curPtr->getNext();
   } // end while

   return prevPtr;
} // end getNodeBefore
```

本章末尾的编程问题要求您完成此有序列表的实现。

![](img/288a0c22d14d2450c1e772f228f867b0_382_0.png)

![](img/288a0c22d14d2450c1e772f228f867b0_382_1.png)

![](img/288a0c22d14d2450c1e772f228f867b0_382_2.png)

问题 7 假设您使用前面的方法 insertSorted 向有序列表添加一个条目。如果该条目已在列表中，该方法会将其插入到列表中的哪个位置？在条目的第一次出现之前，在条目的第一次出现之后，在条目的最后一次出现之后，还是其他位置？

问题 8 如果在方法 getNodeBefore 的 while 语句中将 > 改为 >=，上一个问题的答案会是什么？

## 12.2.3 链式实现的效率

insertSorted 的性能取决于方法 getNodeBefore 的效率。后者方法通过遍历节点链来定位插入点。此遍历为 O(n)，使得向有序列表添加成为 O(n) 操作。除了 isEmpty 和 getLength（它们是 O(1) 操作）之外，有序列表方法均为 O(n)。我们将这些观察留给您作为练习 11 来展示。

## 12.3 使用 ADT 列表的实现

如前几章所述，ADT 有序列表的链式实现重复了 ADT 列表相应实现中的大部分内容。我们能否避免这种工作重复并重用列表实现的部分内容？这个问题的答案是肯定的，您很快就会看到。

您当然可以使用 ADT 列表来创建和维护字符串的字母列表。因此，在实现 ADT 有序列表时考虑使用 ADT 列表是很自然的。基本上，您可以使用以下三种技术之一来实现：

- 封装
- 公有继承
- 私有继承

在大多数情况下，这三种方法中有一种或多种不适用于特定问题；通常，其中一种方法会是最佳选择。但是，我们将使用有序列表来演示所有三种技术。

### 12.3.1 封装

有序列表可以在列表中维护其条目，如图 12-3 所示。您在实现有序列表的类中使用列表作为数据字段。如 C++ 间奏 4 中所述，这种方法使用一种

### 图 12-3 包含其条目列表的有序列表实例

![](img/288a0c22d14d2450c1e772f228f867b0_383_0.png)

![](img/288a0c22d14d2450c1e772f228f867b0_383_1.png)

### 图 12-4 SortedListHasA 由 LinkedList 类的一个实例组成

![](img/288a0c22d14d2450c1e772f228f867b0_384_0.png)

称为组合的封装类型，并说明了有序列表类与列表类之间的 *has-a* 关系。如果我们将新类命名为 SortedListHasA 并使用 LinkedList 的一个实例（如第 9 章清单 9.2 所示），图 12-4 使用 UML 符号说明了这两个类之间的关系。

**头文件。** 清单 12-3 声明了类 SortedListHasA，使其 *拥有一个* 私有数据成员，该成员是包含有序列表中项目的 LinkedList 实例。我们的类将从接口 SortedListInterface 派生，如前面在清单 12-1 中给出。

```
LISTING 12-3 The header file for the class SortedListHasA

/** ADT sorted list using the ADT list.
 *   @file SortedListHasA.h */
#ifndef _SORTED_LIST_HAS_A
#define _SORTED_LIST_HAS_A

#include "SortedListInterface.h"
#include "ListInterface.h"
#include "Node.h"
#include "PrecondViolatedExcep.h"

template<class ItemType>
class SortedListHasA : public SortedListInterface<ItemType>
{
private:
   ListInterface<ItemType>* listPtr;

public:
   SortedListHasA();
   SortedListHasA(const SortedListHasA<ItemType>& sList);
   virtual ~SortedListHasA();

   void insertSorted(const ItemType& newEntry);
   bool removeSorted(const ItemType& anEntry);
   int getPosition(const ItemType& newEntry) const;

   // The following methods have the same specifications
   // as given in ListInterface in Chapter 8:
```

