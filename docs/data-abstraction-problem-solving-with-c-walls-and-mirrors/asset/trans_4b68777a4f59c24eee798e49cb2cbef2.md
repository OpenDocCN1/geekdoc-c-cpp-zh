

# 图 14-3 一个带有一个外部指针的循环链接节点链

![](img/d0cb86b2f18b2db569968ad7c743510e_427_0.png)

**注意：** 如果你使用仅带头指针的线性链来实现队列，那么入队操作将非常低效。向队列添加每个元素都需要遍历到链的末尾。随着队列长度的增加，遍历时间——以及入队的时间需求——也会增加。

列表 14-3 显示了类定义的头文件。

# 列表 14-3 LinkedQueue 类的头文件

```cpp
/** ADT 队列：基于链的实现。
@file LinkedQueue.h */

#ifndef LINKED_QUEUE
#define LINKED_QUEUE

#include "QueueInterface.h"
#include "Node.h"
#include "PreconditionViolatedEx.h"

template<class ItemType>
class LinkedQueue : public QueueInterface<ItemType>
{
private:
    // 队列实现为链接节点的链，该链有两个外部指针：
    // 一个指向队列头的头指针和一个指向队列尾部的尾指针。
    NodeItemType* backPtr;
    NodeItemType* frontPtr;
public:
    LinkedQueue();
    LinkedQueue(const LinkedQueue& aQueue);
    ~LinkedQueue();
    bool isEmpty() const;
    bool enqueue(const ItemType& newEntry);
    bool dequeue();

(继续)
```

# 402 第 14 章 队列和优先级队列的实现

```cpp
/* 如果队列为空，抛出 PrecondViolatedExec */
ItemType peekFront() const throw (PrecondViolatedExec);
}; // endLinkedQueue
#include "LinkedQueue.cpp"
#endif
```

`enqueue` 方法。在表示队列的链的末尾插入由 `newNodePtr` 指向的新节点，需要改变三个指针：新节点中的 `next` 指针、当前尾部节点的 `next` 指针以及外部指针 `backPtr`。图 14-44 展示了在非空队列中添加元素时的这些变化，并指示了它们发生的顺序。执行此添加操作的语句为：

```cpp
newNodePtr->setNext(nullPtr);
backPtr->setNext(newNodePtr);
backPtr = newNodePtr;
```

# 图 14-44 向非空队列添加元素

![](img/d0cb86b2f18b2db569968ad7c743510e_428_0.png)

向空队列添加元素是一个特殊情况，如图 14-5 所示。如果 `newNodePtr` 指向新节点，则以下语句将该节点添加到空链中：

```cpp
frontPtr = newNodePtr;
backPtr = newNodePtr;
```

这些语句可以很容易地推导出：该链只有一个节点，该节点既是链中的第一个节点，也是最后一个节点。

# 图 14-5 向空队列添加元素：(a) 入队前；(b) 入队后

![](img/d0cb86b2f18b2db569968ad7c743510e_429_0.png)

(a)

```cpp
frontPtr = newNodePtr;
backPtr = newNodePtr;
```

(b)

```cpp
frontPtr;
backPtr;
```

因此，我们对 `enqueue` 方法有如下定义：

```cpp
template<class ItemType>
bool LinkedQueue<ItemType>::enqueue(const ItemType& newEntry)
{
    Node<ItemType>* newNode = new Node<ItemType>(newEntry);
    // 插入新节点
    if (isEmpty())
        frontPtr = newNodePtr;            // 队列原本为空
    else
        backPtr->setNext(newNodePtr);     // 新节点位于尾部
    return true;
} // end enqueue
```

**dequeue 方法。** 从队列中移除元素涉及删除链的第一个节点。这比移除最后一个节点要简单，因为我们不需要删除最后一个。图 14-6 展示了从包含多个元素的队列中移除第一个元素。注意，你只需要更改外部指针 `frontPtr`。从只有一个元素的队列中移除元素是一个特殊情况，会将外部指针 `backPtr` 和 `frontPtr` 设置为 `nullptr`。
`dequeue` 方法的定义了如何实现这两种情况：

```cpp
template<class ItemType>
bool LinkedQueue<ItemType>::dequeue()
{
    bool result = false;
    if (!isEmpty())
    {
        // 队列不空；移除头部
        Node<ItemType>* nodeToDeletePtr = frontPtr;
        if (frontPtr == backPtr)
        {
            // 特殊情况：队列只有一个节点
            frontPtr = nullptr;
            backPtr = nullptr;
        }
        else
            frontPtr = frontPtr->getNext();
        // 将删除的节点返回系统
        nodeToDeletePtr->setNext(nullptr);
        delete nodeToDeletePtr;
        nodeToDeletePtr = nullptr;

        result = true;
    } // end if
    return result;
} // end dequeue
```

# 图 14-6 从包含多个元素的队列中移除元素

![](img/d0cb86b2f18b2db569968ad7c743510e_430_0.png)

- 1. nodeToDeletePtr = frontPtr;
- 2. frontPtr = frontPtr->getNext();
- 3. nodeToDeletePtr->setNext(nullPtr);
- 4. delete nodeToDeletePtr;

**获取。** `peekFront` 方法在检查队列不为空后，简单地返回 `frontPtr->getItem()` 的值。我们将该实现的其余部分留给你们作为练习。（参见本章末尾的练习 1 到 3。）

**问题 1** 为什么当使用链接节点链来实现队列时，尾指针是理想的？

**问题 2** 如果你使用一个仅带尾指针的循环链（如图 14-3 所示），你如何访问第一个节点中的数据？

**问题 3** 如果 ADT 队列有一个用于移除队列中所有条目的 `clear` 方法，那么在之前的基于链的实现中，它的定义会是什么？

# 14.1.3 基于数组的实现

对于固定大小队列不是问题的应用，可以使用数组来表示队列。一个原始的基于数组的实现可能包含以下定义，如图 14-7 所示：

```cpp
const int MAX_QUEUE = // 队列的最大大小
type items[MAX_QUEUE]; // 队列数组
int front;             // 头部索引
int back;              // 尾部索引
```

# 图 14-7 (a) 原始基于数组的实现 (b) 右移会导致队列满

![](img/d0cb86b2f18b2db569968ad7c743510e_431_0.png)
![](img/d0cb86b2f18b2db569968ad7c743510e_431_1.png)

这种策略的问题是右移——即在经过一系列添加和移除操作后，队列会向末尾偏移，使其看起来是满的。换句话说，当队列仅包含几个元素时，`back` 可能等于 `MAX_QUEUE–1`。

解决此问题的可能方案是将数组向左移动，可以在每次移除后或当 `back` 等于 `MAX_QUEUE–1` 时移动。这种方案保证了队列始终包含 `MAX_QUEUE` 个元素。然而，移动并不理想，因为它会增加实现的成本。

> 问题 4 假设我们更改图 14-7 所示的基于数组的队列实现，使得队列尾部位于 `items[0]`。虽然从头部反复移除会导致右移，这种实现会产生什么其他问题？

一种更优雅的解决方案是将数组视为循环，如图 14-8 所示。移除元素时，增加队列头部索引；插入元素时，增加尾部索引。

# 406 第 14 章 队列和优先级队列的实现

# 图 14-8 作为队列实现的循环数组

![](img/d0cb86b2f18b2db569968ad7c743510e_432_0.png)

图 14-9 展示了连续三次队列操作对 `front`、`back` 以及数组的影响。注意 `front` 和 `back` 沿数组顺时针“前进”。

当 `front` 或 `back` 进到 `MAX_QUEUE – 1` 时，它们应该绕回 0。这解决了之前原始实现中出现的右移问题，因为这里的循环数组没有末尾。你通过使用模运算（即 C++ 的 `%` 运算符）在增加 `front` 和 `back` 时来获得循环队列的回绕效果。使用以下语句将 `newEntry` 移除队列：

```cpp
back = (back + 1) % MAX_QUEUE;
items[back] = newEntry;
```

注意如果在添加 `newItem` 之前 `back` 等于 `MAX_QUEUE – 1`，第一条语句 `back = (back + 1) % MAX_QUEUE` 将产生回到索引 0 的效果。同样，你可以使用语句移除队列头部元素：

```cpp
front = (front + 1) % MAX_QUEUE;
```

初始化队列时，将 `front` 设置为 0，`back` 设置为 `MAX_QUEUE – 1`。

# 图 14-9 对图 14-8 中队列连续三次操作的影响

```cpp
dequeue();
dequeue();
dequeue(9);
```

![](img/d0cb86b2f18b2db569968ad7c743510e_432_1.png)

