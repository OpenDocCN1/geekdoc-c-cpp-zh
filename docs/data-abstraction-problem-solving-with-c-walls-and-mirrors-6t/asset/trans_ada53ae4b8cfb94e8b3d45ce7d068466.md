

## 方法 getNodeAt

私有方法 getNodeAt 通过遍历链来定位给定位置的节点。它返回指向所定位节点的指针。遍历从链的第一个节点开始，一个接一个地移动节点，并在过程中计数，直到到达所需的节点：

```
template <class ItemType>
Node<ItemType>* LinkedList<ItemType>::getNodeAt(int position) const
{
    // Debugging check of precondition
    assert((position >= 1) && (position <= itemCount));

    // Count from the beginning of the chain
    Node<ItemType>* curPtr = headPtr;
    for (int skip = 1; skip < position; skip++)
        curPtr = curPtr->getNext();

    return curPtr;
} // end getNodeAt
```

由于 getNodeAt 是私有方法，且仅由类中的其他方法调用，那些方法负责遵守其前置条件。因此，如果前置条件被违反，我们无需抛出异常。相反，我们在调试期间只需使用断言。

## 方法 insert

如你所知，你可以将新条目插入列表的第一个条目之前、最后一个条目之后，或两个相邻条目之间。对于第 4 章中 ADT bag 的链式实现和第 7 章中 ADT stack 的链式实现，我们始终将新节点插入链式节点链的开头。ADT list 要求我们以其他方式操作链。让我们探讨这些方式。

由于我们知道如何在节点链的开头插入新节点，让我们考虑在两个现有的相邻节点之间插入节点，这两个节点由指针变量 prevPtr 和 curPtr 指向，如图 9-5a 所示。如果指针变量 newNodePtr 指向新节点，你使新节点指向 curPtr 当前指向的节点（图 9-5b）。你还必须更改将在新节点之前的节点中的指针值，使其指向新节点，如图 9-5c 所示。如图所示，你可以使用一对赋值语句完成插入：

```
newNodePtr->setNext(curPtr);
prevPtr->setNext(newNodePtr);
```

在节点之间插入节点

现在，变量 curPtr 和 prevPtr 是如何获得适当值的？给定 newPosition（列表中新条目的所需位置），你遍历链直到找到新条目的适当位置。私有方法 getNodeAt 将为你执行此遍历。因此，

```
prevPtr = getNodeAt(newPosition - 1);
curPtr = prevPtr->getNext();
```

然后你使用 new 运算符创建一个新节点，newNodePtr 指向该节点。你初始化其数据部分，然后像刚才描述的那样将节点插入链中。

图 9-6 显示在链末尾插入新节点。这种插入可能是一种特殊情况，因为一对赋值语句

```
newNodePtr->setNext(curPtr);
prevPtr->setNext(newNodePtr);
```

if curPtr is nullptr, inserting at the end of a chain is not a special case

其目的是在 curPtr 和 prevPtr 指向的节点之间插入新节点。如果你要在链末尾插入新节点，curPtr 应该指向哪个节点？在这种情况下，将 curPtr 的值视为 nullptr 是合理的，因为在遍历列表时，当 curPtr 移过链的末尾时，它会变为 nullptr。请注意，如果 curPtr 的值为 nullptr 且 prevPtr 指向链中的最后一个节点，前面的一对赋值语句确实会将新节点插入链的末尾。因此，在链末尾插入不是一种特殊情况。总结一下，插入过程需要三个高级步骤：

向链中插入新节点的三个步骤

- 1. 创建一个新节点并在其中存储新数据。
- 2. 确定插入点。
- 3. 通过更改指针将新节点连接到链式链中。

这些步骤和前面的讨论在 insert 的以下定义中得到实现：

```
template<class ItemType>
bool LinkedList<ItemType>::insert(int newPosition,
                                  const ItemType& newEntry)
{
    bool ableToInsert = (newPosition > 1) &&
                        (newPosition <= itemCount + 1);
    if (ableToInsert)
    {
        // Create a new node containing the new entry
        Node<ItemType>* newNodePtr = new Node<ItemType>(newEntry);

        // Attach new node to chain
        if (newPosition == 1)
        {
            // Insert new node at beginning of chain
            newNodePtr->setNext(headPtr);
            headPtr = newNodePtr;
        }
        else
        {
            // Find node that will be before new node
            Node<ItemType>* prevPtr = getNodeAt(newPosition - 1);

            // Insert new node after node to which prevPtr points
            newNodePtr->setNext(prevPtr->getNext());
            prevPtr->setNext(newNodePtr);
        } // end if

        itemCount++; // Increase count of entries
    } // end if

    return ableToInsert;
} // end insert
```

如果你尚未开始测试核心组中的方法，现在应该开始了。

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_302_0.png)

**问题 5** 给定一个非空列表，它是 LinkedList 的一个实例，在什么位置插入新条目需要的操作最少？解释。

**问题 6** 在前面的方法 insert 中，第二条语句测试 newPosition 的值。它测试的布尔表达式应该是 isEmpty() || (newPosition == 1) 吗？解释。

**问题 7** insert 方法如何强制执行 getNodeAt 的前置条件？

方法 remove。要从列表中删除任何条目，你必须能够从链式节点链中删除任何节点。你已经知道如何删除链中的第一个节点，因为 the

### 图 9-5 在链式链的现有节点之间插入新节点

(a) 插入新节点之前

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_303_0.png)

(b) newNodePtr->setNext(curPtr) 执行后

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_303_1.png)

(c) prevPtr->setNext(newNodePtr) 执行后

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_303_2.png)

### 图 9-6 在链式链末尾插入新节点

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_303_3.png)

### 图 9-7 从链中删除节点

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_304_0.png)

第 4 章中 ADT bag 的链式实现和第 7 章中 ADT stack 的链式实现就是这样做的。让我们考虑删除内部节点。

如图 9-7 所示，你可以通过更改前驱节点中的指针值来删除 curPtr 指向的节点 N。你需要将此指针设置为指向 N 之后的节点，从而在链上绕过 N。（虚线表示旧的指针值。）请注意，此指针更改不会直接影响节点 N。节点 N 仍然存在，并且它指向删除前所指向的同一节点。然而，该节点已有效地从链中删除。例如，遍历链将永远无法到达节点 N。

要完成此指针更改，首先请注意，如果你只有指向 N 的指针 curPtr，你将无法直接访问 N 的前驱节点。毕竟，你不能沿链向后跟随链接。因此，你必须有图 9-7 中的指针变量 prevPtr。它指向 N 的前驱节点，并使你能够更改该节点的 next 指针，从而将节点 N 从链中删除。以下赋值语句就是你删除 curPtr 指向的节点所需的全部内容：

删除内部节点

```
prevPtr->setNext(curPtr->getNext());
```

之前的技术对任何节点 N 都有效吗，无论它出现在链式链的何处？不，如果要删除的节点是链中的第一个节点，则该技术无效，但它对链中的最后一个节点有效。因此，删除链中的第一个节点是一种特殊情况。由于我们已经知道如何删除第一个节点，让我们考虑删除最后一个节点。

图 9-8 显示删除 curPtr 指向的节点，该节点恰好是最后一个节点。仅凭该指针是不够的，因为你必须让变量 prevPtr 指向倒数第二个节点。你将倒数第二个节点中的指针设置为 nullptr。我们刚才用于删除内部节点的同一条语句将完成此指针更改，因为 curPtr->getNext() 的值是 nullptr：

```
prevPtr->setNext(curPtr->getNext());
```

### 图 9-8 删除最后一个节点

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_304_1.png)

