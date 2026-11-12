

### 图 14-8 作为队列实现的循环数组

![](img/288a0c22d14d2450c1e772f228f867b0_432_0.png)

后。图 14-9 说明了三个连续队列操作对 front、back 和数组的影响。请注意，front 和 back 会沿数组顺时针“前进”。

当 front 或 back 其中之一超过 MAX_QUEUE - 1 时，它应绕回到 0。这种绕回消除了之前朴素实现中出现的向右漂移问题，因为在这里循环数组没有末尾。你在递增 front 和 back 时使用模运算（即 C++ 的 % 运算符）来获得循环队列的绕回效果。例如，你可以使用以下语句将 newEntry 添加到队列中：

```
Adding to a queue
back = (back + 1) % MAX_QUEUE;
items[back] = newEntry;
```

请注意，如果在添加 newEntry 之前 back 等于 MAX_QUEUE - 1，则第一条语句 back = (back + 1) % MAX_QUEUE 会将 back 绕回到索引 0。同样，你可以使用以下语句移除队列前端的条目：

```
Deleting from a queue
front = (front + 1) % MAX_QUEUE;
```

要初始化队列，请将 front 设置为 0，将 back 设置为 MAX_QUEUE - 1。

### 图 14-9 图 14-8 中队列上三个连续操作的效果

![](img/288a0c22d14d2450c1e772f228f867b0_432_1.png)

### 图 14-10 (a) 队列变为空时 front 超过 back；(b) 队列变为满时 back 追上 front

![](img/288a0c22d14d2450c1e772f228f867b0_433_0.png)

此方案唯一的困难是检测队列何时为空或满。将以下条件作为队列空条件似乎是合理的：

**front 在 back 前方一个位置**

front 和 back 无法用于区分队列满和队列空条件

通过计数队列项，你可以检测队列满和队列空条件

因为这似乎表明，如图 14-10a 所示，当队列变为空时 front “超过”了 back。然而，此条件也可能表示队列已满：因为队列是循环的，当队列变为满时，back 实际上可能会“追上” front。图 14-10b 说明了这种情况。

显然，你需要一种方法来区分这两种情况。一种方法是记录队列中项的数量。在向队列添加项之前，检查计数是否等于 MAX_QUEUE；如果是，则队列已满。在从队列移除项之前，检查计数是否等于零；如果是，则队列为空。

**头文件。** 清单 14-4 包含了使用循环数组的 ADT 队列的基于数组的实现的头文件，如刚才所述。由于数据存储在静态分配的内存中，编译器生成的析构函数和拷贝构造函数已足够。1

1 如果你使用动态分配的数组，则必须提供析构函数和拷贝构造函数。

```
LISTING 14-4 The header file for the class ArrayQueue

/** ADT queue: Circular array-based implementation.
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
   int front;                 // Index to front of queue
   int back;                  // Index to back of queue
   int count;                 // Number of items currently in the queue

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

**实现文件。** 清单 14-5 包含了 ArrayQueue 方法的定义，如实现文件中所示。

```
LISTING 14-5 The implementation file for the class ArrayQueue

/** ADT queue: Circular array-based implementation.
#file ArrayQueue.cpp */
#include "ArrayQueue.h"   // Header file

template<class ItemType>
ArrayQueue<ItemType>::ArrayQueue() : front(0), back(MAX_QUEUE - 1), count(0)
{  } // end default constructor

template<class ItemType>
bool ArrayQueue<ItemType>::isEmpty() const
{
   return count == 0;
} // end isEmpty
```

```
template<class ItemType>
bool ArrayQueue<ItemType>::enqueue(const ItemType& newEntry)
{
   bool result = false;
   if (count < MAX_QUEUE)
   // Queue has room for another item
   back = (back + 1) % MAX_QUEUE;
   items[back] = newEntry;
   count++;
   result = true;
   } // end if

   return result;
} // end enqueue

template<class ItemType>
bool ArrayQueue<ItemType>::dequeue()
{
   bool result = false;
   if (!isEmpty())
   {
   front = (front + 1) % MAX_QUEUE;
   count--;
   result = true;
   } // end if

   return result;
} // end dequeue

template<class ItemType>
ItemType ArrayQueue<ItemType>::peekFront() const
throw(PrecondViolatedExcep)
{
   // Enforce precondition
   if (isEmpty())
   throw PrecondViolatedExcep("peekFront() called with empty queue");

   // Queue is not empty; return front
   return items[front];
   // end peekFront
}
```

问题 5 如果 ADT 队列有一个名为 clear 的方法，用于移除队列中的所有条目，那么在之前的基于数组的实现中，它的定义应该是什么？

**变体。** 之前的循环数组方法有几种常用变体，不需要记录队列中条目的数量。一种方法使用布尔变量 isFull 来区分满和空条件。然而，维护此变量的开销与维护计数器的开销差不多。isFull 标志可以替代计数器。一种更快的实现为数组项声明了 MAX_QUEUE + 1 个位置，但仅使用其中 MAX_QUEUE 个位置来存储队列项。你牺牲了一个

### 图 14-11 更高效的循环实现：(a) 满队列；(b) 空队列

![](img/288a0c22d14d2450c1e772f228f867b0_436_0.png)

数组位置，并让 front 成为队列前端位置之前的位置的索引。如图 14-11 所示，如果

```
front equals (back + 1) % (MAX_QUEUE + 1)
```

则队列已满；但如果

```
front equals back
```

则队列为空。

使用额外的数组位置更节省时间

这种方法没有维护计数器或布尔变量的开销，因此在时间上更高效。编程问题 3 和 4 进一步讨论了这两种替代实现。

## 14.1.4 比较实现

我们建议了 ADT 队列的几种实现，它们将队列的条目存储在 ADT 列表的实例中、带有头指针和尾指针的链式节点链中、只有一个外部指针的循环链中、数组中或循环数组中。你已经了解了其中三种实现的细节。我们所有的 ADT 队列实现最终要么基于数组，要么基于链接。

在基于数组和基于链接的实现之间做出选择的原因与前面章节中讨论的相同。此处的讨论与第 4 章第 4.5 节中的讨论类似。我们在此重申要点，以队列为背景。

固定大小 动态大小

基于静态分配数组的实现会在数组已满时阻止入队操作向队列添加项。这种队列适用于操作系统中的许多数据结构，例如缓冲区。如果此限制不可接受，则必须使用动态分配的数组或基于链接的实现。

**重用已实现的类可节省时间**

假设你决定使用基于链接的实现。你应该选择使用链式链的实现，还是使用 ADT 列表的基于链接的实现？因为链式链实际上表示 ADT 列表中的项，使用 ADT 列表来表示队列不如直接使用链式链高效。然而，ADT 列表方法编写起来简单得多。

如果你决定使用链式链而不是 ADT 列表来表示队列，你应该使用线性链还是循环链？我们将此问题留给你在编程问题 1 中回答。

