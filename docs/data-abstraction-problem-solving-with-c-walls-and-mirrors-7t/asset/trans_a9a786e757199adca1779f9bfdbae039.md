

## 14.2 ADT 优先队列的一个实现

虽然我们可以将优先队列的条目放入数组或链式节点链中，但这样做就像实现第 12 章中已经完成的 ADT 有序列表。与其重复那些实现，不如使用有序列表来包含优先队列的条目。清单 14-6 中的头文件定义了一个优先队列类，其私有数据成员是 LinkedSortedList 类的一个实例，如第 12 章清单 12-2 所示。

```
LISTING 14-6 A header file for the class SL_PriorityQueue.

/* ADT priority queue: ADT sorted list implementation.
@file SL_PriorityQueue.h */
#ifndef SL_PRIORITY_QUEUE_
#define SL_PRIORITY_QUEUE_

#include "PriorityQueueInterface.h"
#include "LinkedSortedList.h"
#include "PrecondViolatedExcep.h"

template<class ItemType>
class SL_PriorityQueue : public PriorityQueueInterface<ItemType>
{
private:
   LinkedSortedList<ItemType>* slistPtr; // Pointer to sorted list of
                                      // items in the priority queue
public:
   SL_PriorityQueue();
   SL_PriorityQueue(const SL_PriorityQueue& pq);
   ~SL_PriorityQueue();
   bool isEmpty() const;
   bool add(const ItemType& newEntry);
   bool remove();
   //@throw PrecondViolatedExcep if priority queue is empty.
   ItemType peek() const throw(PrecondViolatedExcep);
}; // end SL_PriorityQueue

#include "SL_PriorityQueue.cpp"
#endif
```

在实现类 SL_PriorityQueue 之前，我们需要考虑有序列表的行为。LinkedSortedList 以有序顺序维护有序列表中的条目。它通过相互比较条目来实现这一点。对于优先队列，我们希望这些比较基于条目的优先级。假设每个条目都是一个将其优先级作为数据成员的对象。你将在 C++ 间奏 5 中学习如何使比较运算符（如 >）基于其两个操作数的特定方面进行比较。目前，让我们假设比较是根据优先级进行的。请注意，最高优先级值可以是最大值，也可以是最小值，具体取决于手头的应用。

为了让你了解如何实现这个类，让我们来看看 add 和 remove 操作的定义：

```
template<class ItemType>
bool SL_PriorityQueue<ItemType>::add(const ItemType& newEntry)
{
   slistPtr->insertSorted(newEntry);
   return true;
} // end add

template<class ItemType>
bool SL_PriorityQueue<ItemType>::remove()
{
   // The highest-priority item is at the end of the sorted list
   return slistPtr->remove(slistPtr->getLength());
} // end remove
```

我们将把此实现的其余部分作为练习留给你。但是，请注意，我们将在第 17 章介绍 ADT 堆时讨论一种更高效的实现。

> **问题 6** 为 ADT 优先队列的有序列表实现定义方法 peek。

## 摘要

- 1. 队列的入队和出队操作需要高效访问队列的两端。因此，基于链表的队列实现使用同时具有头指针和尾指针的线性链式链。或者，你可以使用循环链式链。
- 2. 基于数组的队列实现容易出现向右漂移。这种现象可能使队列看起来已满，但实际上并未满。移动数组中的元素是补偿向右漂移的一种方法。更高效的解决方案是使用循环数组。
- 3. 如果使用循环数组实现队列，则必须能够区分队列已满和队列为空的条件。你可以通过计算队列中的元素数量、使用布尔变量 isFull 或留空一个数组位置来做出此区分。
- 4. 你可以使用数组、链式节点链或有序列表来包含优先队列中的条目。通过使用 ADT 堆，可以实现更高效的实现，我们将在本书后面部分讨论。

## 练习

- 1. 实现清单 14-3 中声明的类 LinkedQueue 的拷贝构造函数。提示：查看第 7 章清单 7-4 中 ADT 栈的拷贝构造函数。
- 2. 重复上一个练习，但改为实现一个内存安全的拷贝构造函数。如果内存分配失败，此构造函数应释放故障前分配的所有内存，然后抛出异常。
- 3. 清单 14-3 中声明的类 LinkedQueue 的析构函数可以反复调用 dequeue。虽然易于编写，但由于反复调用方法，此析构函数可能效率低下。编写另一个析构函数实现，直接释放链式链而不调用 dequeue。
- 4. 在程序调试期间，显示队列内容的操作很有用。向 ADT 队列添加一个 display 操作，使 display 假设并使用 ADT 队列的基于链表的实现。
- 5. 考虑一个名为 getNumberOfElements 的方法，它返回队列中的元素数量而不更改队列。返回类型为 int，且不接受任何参数。
  - a. 将 getNumberOfElements 添加到本章给出的基于数组的 ADT 队列中。
  - b. 将 getNumberOfElements 添加到本章给出的基于链表的 ADT 队列中。
- 6. 证明第 14.1.3 节中描述的使用额外数组元素的队列实现比计数器变体更高效，尽管它在测试中似乎执行了两次额外的加法：

  front equals (back + 1) % (MAX_QUEUE + 1)
- 7. 考虑类 ListQueue，它使用 ADT 列表来表示队列中的项目来实现 ADT 队列。当 ADT 列表的实现为
  - a. 基于数组
  - b. 基于链表
时，讨论队列 enqueue 和 dequeue 操作的效率。
- 8. 如清单 14-1 所示，类 ListQueue 将队列的 front 维护在队列条目列表的末尾，并将队列的 back 放在该列表的开头。请注意，该列表是类 LinkedList 的一个对象。如果我们将队列的 front 维护在列表的开头，将队列的 back 维护在列表的末尾，则对 enqueue 和 dequeue 操作的效率有何影响？
- 9. 完成类 SL_PriorityQueue 的实现，如第 14.2 节所述。
- 10. 实现类 SL_PriorityQueue，假设低值表示更高优先级。这种优先队列在操作系统和其他类似应用中很有用。当底层有序列表具有基于链表的实现时，使用最低值表示最高优先级会使优先队列操作更高效。描述此优势成立的原因。

## 编程问题

- 1. 编写一个基于链表的队列实现，使用循环链式链来表示队列中的项目。你需要一个单一的尾指针。完成后，将你的实现与本章中使用带有两个外部指针的线性链式链的实现进行比较。哪种实现更容易编写？哪种更容易理解？哪种更高效？
- 2. 编写一个基于数组的队列实现，使用可调整大小的循环数组来表示队列中的项目。
- 3. 修订本章给出的基于数组的队列实现。不要计算队列中的项目数量，而是使用布尔变量 isFull 来区分已满和空条件。
- 4. 本章描述了另一种基于数组的队列实现，它不使用任何特殊数据成员（如 count 或 isFull（见上一个编程问题））来区分已满和空条件。在此实现中，你为数组元素声明 MAX_QUEUE + 1 个位置，但仅使用其中 MAX_QUEUE 个位置作为队列项。你通过将 front 设为队列前端前一个位置的索引来牺牲一个数组位置。如果 front 等于 (back + 1) % (MAX_QUEUE + 1)，则队列已满；如果 front 等于 back，则队列为空。实现这种基于数组的方法。
- 5. 上一章的练习 9 定义了双端队列，即 dequeue。使用循环数组来包含 dequeue 中的项目来实现 ADT dequeue。
- 6. 重复上一个编程问题，但在链式链中维护 dequeue 的条目。
- 7. 实现 ADT dequeue，如上一章练习 9 所述，作为 ArrayQueue 的派生类，如清单 14-4 和 14-5 所示。

