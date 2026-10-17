
```cpp
template<class ItemType>
Node<ItemType>* LinkedList::getNodeAt(int position) const
{
    // 对精度的调试检查
    assert((position > 0) && (position <= itemCount));
    // 从链的开始计数
    Node<ItemType>* curPtr = headPtr;
    for (int skip = 0; skip < position; skip++)
        curPtr = curPtr->getNext();
    return curPtr;
} // 结束 getNodeAt
```

由于 `getNodeAt` 是一个私有方法，并且仅由类内部的方法调用，因此它在违反前条件时不会抛出异常。相反，在调试期间明智地使用断言。`insert` 方法。

我们知道，在链的开头、在末尾之后或在两个相邻节点之间插入新条目。基于链的实现需要考虑在链的开头、末尾之后或两个相邻节点之间插入新条目。正如第 7 章中基于链的实现所示，我们需要考虑在链的开头插入新节点。由于 `getNodeAt` 是一个私有方法，并且仅由类内部的方法调用，因此它在违反前条件时不会抛出异常。相反，在调试期间明智地使用断言。`insert` 方法。

我们知道，可以像图 9-5 所示那样，在链的开头、末尾之后或两个相邻节点之间插入新条目。正如图 9-5 所示，通过以下赋值语句在链的开头插入新节点，如 9-5 所示。

```cpp
newNodePtr.setNext(headPtr);
```

`prevPtr` 和 `curPtr`

这些方法。在链的末尾或在两个相邻节点之间插入新条目，如图 9-5b 的赋值语句所示。

```cpp
newNodePtr.setNext(curPtr);
```

图 9-5

![](img/d0cb86b2f18b2db569968ad7c743510e_301_0.png)

图 9-5a

![](img/d0cb86b2f18b2db569968ad7c743510e_301_1.png)

图 9-5b

末尾插入并不是一种特殊情况。总结来说，插入过程需要三个高级步骤：

- 1. 创建新节点并在其中存储数据。
- 2. 确定插入点。
- 3. 通过更改指针将新节点连接到链。

这些步骤实现在 `insert` 的定义中：

```cpp
template<class ItemType>
bool LinkedList<ItemType>::insert(int newPosition,
                               const ItemType& newEntry)
{
    bool ableToInsert = (newPosition >= 0) &&
                        (newPosition <= itemCount + 1);
    if (ableToInsert) {
        // 创建包含新条目的节点
        Node<ItemType>* newNodePtr = new Node<ItemType>(newEntry);
        // 将节点接到链
        if (newPosition == 0) {
            // 在链开头插入新节点
            newNodePtr->setNext(headPtr);
            headPtr = newNodePtr;
        } else {
            // 找到位于节点之前的节点
            Node<ItemType>* prevPtr = getNodeAt(newPosition - 1);
            // 在 prevPtr 指向的位置插入新节点
            newNodePtr->setNext(prevPtr->getNext());
            prevPtr->setNext(newNodePtr);
        }
    }
    itemCount++; // 增加条目计数
    return ableToInsert;
} // 结束 insert
```

# 276 第 9 章 列表实现

`prevPtr` 指向链的最后一个节点，由于这些赋值语句，在链的末尾插入新节点并不是一种特殊情况。总结来说，插入过程需要三个高级步骤：

- 1. 创建新节点并在其中存储数据。
- 2. 确定插入点。
- 3. 通过更改指针将新节点连接到链。

这些步骤实现在 `insert` 的定义中：

```cpp
template<class ItemType>
bool LinkedList<ItemType>::insert(int newPosition,
                               const ItemType& newEntry)
{
    bool ableToInsert = (newPosition >= 0) &&
                        (newPosition <= itemCount + 1);
    if (ableToInsert) {
        // 创建包含新条目的节点
        Node<ItemType>* newNodePtr = new Node<ItemType>(newEntry);
        // 将节点接到链
        if (newPosition == 0) {
            // 在链开头插入新节点
            newNodePtr->setNext(headPtr);
            headPtr = newNodePtr;
        } else {
            // 找到位于节点之前的节点
            Node<ItemType>* prevPtr = getNodeAt(newPosition - 1);
            // 在 prevPtr 指向的位置插入新节点
            newNodePtr->setNext(prevPtr->getNext());
            prevPtr->setNext(newNodePtr);
        }
    }
    itemCount++; // 增加条目计数
    return ableToInsert;
} // 结束 insert
```

如果你还没有开始在你的小组中测试这些方法，你应该这样做。

![](img/d0cb86b2f18b2db569968ad7c743510e_302_0.png)

**问题 5** 给定一个非空的 `LinkedList` 实例，在哪个位置插入新条目的操作最少？请解释。

**问题 6** 在之前的 `insert` 方法中，第二个 `if` 语句测试 `newPosition` 的值。它测试的布尔表达式应该是 `isEmpty() || (newPosition == 1)` 吗？请解释。

**问题 7** `insert` 方法如何强制执行 `getNodeAt` 的前条件？

`remove` 方法。要从列表中删除任何条目，你必须能够从节点链中删除节点。你已经知道如何删除链中的第一个节点，因为这

# ADT 列表的链式实现 27

图 9-5 在链链的现有节点之间插入新节点

(a) 插入新节点之前

![](img/d0cb86b2f18b2db569968ad7c743510e_303_0.png)

(b) 执行 `newNodePtr->setNext(curPtr)` 之后

![](img/d0cb86b2f18b2db569968ad7c743510e_303_1.png)

(c) 执行 `prevPtr->setNext(newNodePtr)` 之后

![](img/d0cb86b2f18b2db569968ad7c743510e_303_2.png)

图 9-6 在链节点链的末尾插入新节点

原本为 `nullptr`

![](img/d0cb86b2f18b2db569968ad7c743510e_303_3.png)

# 278 第 9 章 列表实现

图 9-7 从链中删除一个节点

![](img/d0cb86b2f18b2db569968ad7c743510e_304_0.png)

第 4 章中 ADT 容器和第 7 章中 ADT 栈的链式实现都是这样操作的。让我们考虑删除一个内部节点。

如图 9-7 所示，你可以通过修改 N 之前的一个指针的值，来移除 `curPtr` 指向的节点 N。你需要设置该指针使其指向 N 之后的节点，从而在链中跳过 N。（虚线表示旧的指针值）。注意，这种指针的变化 own并不直接影响节点 N。N 仍然存在，且它指向的节点也与之前相同。例如，对链进行遍历仍然可以到达节点 N。

为了完成这种指针更改，请注意：如果你只有一个 `curPtr` 指向 N，那么你没有直接的方法访问 N 之前的节点。毕竟，你无法反向沿着链中的链接。因此，你必须在图 9-7 中拥有变量 `prevPtr`。它指向链中 N 之前的节点，使你能够修改该节点的 `next` 指针，从而将节点 N 从链中移除。只需以下赋值语句即可移除 `curPtr` 指向的节点：

移除内部节点

```
prevPtr->setNext(curPtr->getNext());
```

上述技术是否适用于链链中的任何节点 N，无论它出现在链的什么位置？不适用。如果要删除的节点是链中的第一个节点，则它将不起作用；但对于链中的最后一个节点，它是有效的。因此，删除链中的第一个节点是一个特例。既然我们已经知道如何删除第一个节点，让我们考虑一下删除最后一个节点。

图 9-8 显示了删除 `curPtr` 指向的节点，即最后一个节点。仅靠该指针是不够的，因为我们我们有一个指向倒数第二个节点的变量 `prevPtr`。你将倒数第二个节点内的指针设置为 `nullPtr`。我们刚刚用于移除内部节点的相同赋值语句也会产生这种指针变化，因为 `curPtr->getNext()` 的值为 `nullPtr`：

```
prevPtr->setNext(curPtr->getNext());
```

图 9-8 移除最后一个节点

![](img/d0cb86b2f18b2db569968ad7c743510e_304_1.png)

# ADT 列表的链式实现 279

要移除链的第一个节点，请记住你必须更改 `headPtr` 的值以指向第二个节点。第二个节点成为链的新第一个节点。你可以通过赋值语句将此更改为 `headPtr`：

移除第一个节点是一个特例

```
headPtr = headPtr->getNext();
```

与删除内部节点的情况一样，指针跳过了旧节点，尽管它仍然存在。还要注意，如果要删除的节点是链中唯一的节点——即它既是第一个也是最后一个节点——那么之前的赋值语句将分配值 `nullptr`。记住，`headPtr` 中的值 `nullptr` 表示空链，因此该赋值语句正确处理了链中唯一节点的移除。

被移除的节点仍然存在。假设 `curPtr` 指向它，更改 `curPtr` 的值将导致移除的节点处于悬空状态。它仍然占用存储空间，而程序将无法访问它。会导致内存泄漏。因此，在更改 `curPtr` 的值之前，你应该使用以下语句：

```
curPtr->setNext(nullptr);
delete curPtr;
curPtr = nullptr;
```

通过使用 `delete` 删除节点并将内存返回系统。总结来说，删除过程有三个高级步骤：

1. 定位你想要删除的节点。
2. 通过更改指针将该节点从链中断开。
3. 将节点返回系统。

从链中删除节点的三个步骤

你将在下面的 `remove` 定义中看到这些步骤以及之前的讨论：

```
template<class ItemType>
bool linkedList<ItemType>::remove(int position)
{
  bool ableToRemove = (position >= 1) && (position <= itemCount);
  if (ableToRemove) {
    NodeItem* curPtr = nullptr;
    if (position == 1) {
      // 移除要删除节点之前的第一个节点
      curPtr = headPtr; // 保存指向节点的指针
      headPtr = headPtr->getNext();
    }
    else {
      // 找到要删除节点之前的节点
      Node<ItemType>* prevPtr = getNode(position - 1);
      // 指向要连接的节点
      curPtr = prevPtr->getNext();
      // 通过连接前一个节点和后续节点，
      // 从链中断开指定的节点
      prevPtr->setNext(curPtr->getNext());
    }
    // 将节点返回系统
    curPtr->setNext(nullptr);
```

# 280 第 9 章 列表实现

```
delete curPtr;
curPtr = nullptr;

itemCount--; // 减少条目计数
}
return ableToRemove;
// end remove
```

该方法。要从列表中移除所有条目，可以调用 `remove` 方法。因为最容易移除的是第一个，该方法可以反复调用 `remove(1)` 直到列表为空。此操作之所以有效，是因为如果你移除了列表中的第一个条目，剩余条目将重新编号。因此，要移除所有条目，你可以反复移除第一个条目。因此，`clear` 具有如下定义：

问题 8 `clear` 方法的链式实现包含以下循环：

```
while (!isEmpty())
remove(1);
```

- a. 你能正确地将循环替换为

`for (int position = getLength(); position >= 1; position--)`

`remove(1);` 吗？

- b. 如果将 `remove(1)` 替换为 `remove(position)`，你的 a 答案会有不同吗？

- c. 如果将 `for` 语句替换为

`for (int position = 1; position <= getLength(); position++)`，你的 a 和 b 答案会有不同吗？

析构函数。因为 `clear` 方法会反复调用直到列表为空，并且它重新定位了节点，因此析构函数可以简单地清空：

```
template<class ItemType>
LinkedList<ItemType>::LinkedList()
{
    clear();
} // end destructor
```

问题 9 审查类的析构函数，以便它删除每个节点。

剩余方法。这种 ADT 的链式实现不使用编译器生成的构造函数，因为那只会复制 `headPtr` 和 `itemCount`。相反，它必须复制节点及其内容。

`setEntry` 方法，以及 `set` 方法。

# 282 第 9 章 列表实现

```cpp
// 私有方法 insertNode：
// 在指定位置向 subChainPtr 指向的子链中添加节点。
// 返回扩展后子链的指针。
template<class ItemType>
Node<ItemType>* LinkedList<ItemType>::insertNode(int position,
Node<ItemType>* newNodePtr, Node<ItemType>* subChainPtr)
{
    if (position == 1) { // 在子链开头插入新节点
        newNodePtr->setNext(subChainPtr);
        subChainPtr = newNodePtr;
        itemCount++; // 增加条目计数
    }
    else {
        Node<ItemType>* afterPtr =
            insertNode(position - 1, newNodePtr, subChainPtr->getNext());
        subChainPtr->setNext(afterPtr);
    }
    return subChainPtr;
}
end insertNode;
```

递归方法 `insertNode` 将节点在指定位置添加到 `subChain` 指向的子链中。接下来我们将追踪并解释其逻辑。

**追踪向列表头部添加操作。** 考虑图 9-9 所示的列表。让我们使用如下调用在链的开头添加新条目：

```
myList->insert(1, newEntry);
```

公共方法 `insert` 将创建一个包含 `newEntry` 的新节点（图 9-b），然后通过以下调用调用私有方法 `insertNode`：

```
insertNode(1, newNodePtr, headPtr);
```

参数 `headPtr` 中的指针被复制给参数 `subChainPtr`，因此它也指向链中的第一个节点，如图 9-9c 所示。

新节点被链接到原始链的开头，如图 9-9d 所示。注意，`subChainPtr` 并没有改变，尽管它是与参数 `subChainPtr` 对应的参数。私有方法 `insert` 返回 `subChainPtr` 的值，而公共方法 `insert` 将该值赋值给 `headPtr`。完成添加后的链如图 9-e 所示。

**追踪向列表内部添加操作。** 当添加操作不在原始链的开头时会发生什么？让我们追踪在向图 9-a 所示的链中添加第三个节点时发生的情况。公共方法 `insert` 创建新节点并通过如下调用调用私有方法 `insertNode`：
