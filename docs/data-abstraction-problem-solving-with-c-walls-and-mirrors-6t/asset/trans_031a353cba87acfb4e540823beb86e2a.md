

## 14.1.3 基于数组的实现

对于固定大小的队列不会带来问题的应用程序，你可以使用数组来表示队列。队列的一种简单数组实现可能包括以下定义，如图 14-7a 所示：

```
const int MAX_QUEUE = maximum size of queue;
..
ItemType items[MAX_QUEUE]; // Array of queue items
int front; // Index to front of queue
int back; // Index to back of queue
```

队列的一种简单数组实现

VideoNote 数组队列概述

图 14-7 (a) 队列的一种简单数组实现；(b) 右移可能导致队列看起来已满

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_431_0.png)

这里，front 和 back 分别是队列中队首和队尾条目的索引。最初，front 为 0，back 为 -1。要向队列添加新项，你递增 back 并将项放在 items[back] 中。要移除一项，你只需递增 front。当 back 小于 front 时，队列为空。当 back 等于 MAX_QUEUE - 1 时，队列已满。

右移可能导致队列已满的情况，即使队列中只包含少量条目

这种策略的问题是右移——即，经过一系列添加和移除操作后，队列中的项会向数组末端漂移，使其看起来已满。换句话说，即使队列中只包含少量项，back 也可能等于 MAX_QUEUE - 1。图 14-7b 说明了这种情况。

移动条目以补偿右移的代价很高

解决此问题的一种可能方案是将数组条目向左移动，无论是在每次从队列移除后，还是在 back 等于 MAX_QUEUE - 1 时。此方案保证队列始终可以包含多达 MAX_QUEUE 个项。然而，移动并不真正令人满意，因为它将主导实现的成本。

> **问题 4** 假设我们将图 14-7 中所示的队列简单数组实现更改为使队列的后端位于 items[0]。虽然从队首的重复移除不再会导致右移，但此实现会造成什么其他问题？

循环数组消除右移

一种更优雅的方案是将数组视为循环数组，如图 14-8 所示。要移除一项，你递增队列索引 front，要插入一项，你递增

图 14-8 作为队列实现的循环数组

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_432_0.png)

back。图 14-9 说明了一系列三个队列操作对 front、back 和数组的影响。请注意，front 和 back 会“顺时针”在数组中“前进”。

当 front 或 back 超过 MAX_QUEUE – 1 时，它应该回绕到 0。这种回绕消除了之前简单实现中出现的右移问题，因为这里循环数组没有末端。你通过在递增 front 和 back 时使用取模运算（即 C++ 的 % 运算符）来获得循环队列的回绕效果。例如，你可以使用以下语句将 newEntry 添加到队列中：

- 向队列添加

```
back = (back + 1) % MAX_QUEUE;
items[back] = newEntry;
```

请注意，如果在添加 newItem 之前 back 等于 MAX_QUEUE – 1，则第一条语句 back = (back + 1) % MAX_QUEUE 会将 back 回绕到索引 0。同样，你可以使用以下语句移除队首的条目：

- 从队列删除

```
front = (front + 1) % MAX_QUEUE;
```

要初始化队列，你将 front 设置为 0，back 设置为 MAX_QUEUE – 1。

图 14-9 图 14-8 中队列上三个连续操作的影响

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_432_1.png)

图 14-10 (a) 队列变为空时 front 超过 back；(b) 队列变为满时 back 追上 front

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_433_0.png)

此方案唯一的困难是检测队列何时为空或满。选择队列为空的条件似乎是合理的：

front 超过 back 一个槽位

因为这似乎表明当队列变为空时 front “超过” back，如图 14-10a 所示。然而，此条件也可能表示队列已满：因为队列是循环的，back 实际上可能在队列变满时“追上” front。图 14-10b 说明了这种情况。

显然，你需要一种方法来区分这两种情况。一种方法是保存队列中项的计数。在向队列添加项之前，检查计数是否等于 MAX_QUEUE；如果是，则队列已满。在从队列移除项之前，检查计数是否等于零；如果是，则队列为空。

头文件。清单 14-4 包含使用循环数组的基于数组的 ADT 队列实现的头文件，如上所述。由于数据存储在静态分配的内存中，编译器生成的析构函数和拷贝构造函数就足够了。1

> front 和 back 不能用于区分队列已满和队列为空的条件
>
> 通过计数队列项，你可以检测队列已满和队列为空的条件

清单 14-4 类 ArrayQueue 的头文件

```
/* ADT queue: Circular array-based implementation.
   #file ArrayQueue.h */
#ifndef _ARRAY_QUEUE
#define _ARRAY_QUEUE
#include "QueueInterface.h"
#include "PrecondViolatedExcep.h"
const int MAX_QUEUE = 50;
template<class ItemType>
class ArrayQueue : public QueueInterface<ItemType>
{
   private:
      ItemType items[MAX_QUEUE]; // Array of queue items
      int    front;              // Index to front of queue
      int    back;               // Index to back of queue
      int    count;              // Number of items currently in the queue
   public:
      ArrayQueue();
      // Copy constructor and destructor supplied by compiler
      bool isEmpty() const;
      bool enqueue(const ItemType& newEntry);
      bool dequeue();
      /** @throw PrecondViolatedExcep if queue is empty. */
      ItemType peekFront() const throw(PrecondViolatedExcep);
   }; // end ArrayQueue
#include "ArrayQueue.cpp"
#endif
```

实现文件。清单 14-5 包含 ArrayQueue 方法的定义，如它们在实现文件中出现。

清单 14-5 类 ArrayQueue 的实现文件

```
/* ADT queue: Circular array-based implementation.
   #file ArrayQueue.cpp */
#include "ArrayQueue.h"   // Header file
template<class ItemType>
ArrayQueue<ItemType>::ArrayQueue() : front(0), back(MAX_QUEUE - 1), count(0)
{  // end default constructor
template<class ItemType>
bool ArrayQueue<ItemType>::isEmpty() const
{  return count == 0;
}  // end isEmpty
template<class ItemType>
bool ArrayQueue<ItemType>::enqueue(const ItemType& newEntry)
{
   bool result = false;
   if (count < MAX_QUEUE)
   {
      // Queue has room for another item
      back = (back + 1) % MAX_QUEUE;
      items[back] = newEntry;
      count++;
      result = true;
   }  // end if

   return result;
}  // end enqueue

template<class ItemType>
bool ArrayQueue<ItemType>::dequeue()
{
   bool result = false;
   if (!isEmpty())
   {
      front = (front + 1) % MAX_QUEUE;
      count--;
      result = true;
   }  // end if

   return result;
}  // end dequeue

template<class ItemType>
ItemType ArrayQueue<ItemType>::peekFront() const
throw(PrecondViolatedExcep)
{
   // Enforce precondition
   if (isEmpty())
      throw PrecondViolatedExcep("peekFront() called with empty queue");

   // Queue is not empty; return front
   return items[front];
}  // end peekFront
```

**问题 5** 如果 ADT 队列有一个名为 clear 的方法，用于移除队列中的所有条目，那么在之前的基于数组的实现中，它的定义会是什么？

**变体。** 之前循环数组方法的几种常用变体不需要队列中条目的计数。一种方法使用布尔变量 isFull 来区分已满和空条件。然而，维护此变量的开销与维护计数器的开销差不多。一种更快的实现为数组 items 声明 MAX_QUEUE + 1 个位置，但仅使用其中 MAX_QUEUE 个位置作为队列项。你牺牲一个

isFull 标志可以替换计数器

