
# removeNode(), removeNodeAt(), 和 deleteNode()

从链表中删除节点是一个复杂的操作。首先，你必须将该节点从链表中断开。然而，这样做会破坏连接。由于你移动了连接前驱节点和后继节点的链，将不再有任何东西连接它们。这意味着在删除节点后，你必须将前驱节点和后继节点连接起来。

你可以增强 `LinkedList` 类，包含三个成员函数，用于从链表中删除节点并将前驱节点和后继节点相互连接。这些函数是 `removeNode()`、`removeNodeAt()` 和 `deleteNode()`。

`removeNode()` 函数通过节点本身定位要删除的节点。`removeNodeAt()` 函数通过节点索引定位要删除的节点。`deleteNode()` 函数通过节点中的数据定位要删除的节点。

如果节点位于链表头部，`removeNode()` 函数会将 `front` 指针更新下一个节点。如果节点位于链表末尾，它将更新 `back` 指针为上一个节点。如果节点位于中间，它会将前驱节点连接到后继节点。

`removeNodeAt()` 函数的工作原理类似，但它首先找到给定索引处的节点。`deleteNode()` 函数的工作原理类似，但它首先搜索具有给定数据的节点。

以下代码显示了这三个函数的实现。

```cpp
void LinkedList::removeNode(NODE* node)
{
    if (node == NULL) return;

    if (node == front)
    {
        front = node->next;
        if (front != NULL)
        {
            front->previous = NULL;
        }
        else
        {
            back = NULL;
        }
    }

    if (node == back)
    {
        back = node->previous;
        if (back != NULL)
        {
            back->next = NULL;
        }
        else
        {
            front = NULL;
        }
    }

    if (node != front && node != back)
    {
        node->previous->next = node->next;
        node->next->previous = node->previous;
    }

    size--;
}

void LinkedList::removeNodeAt(int index)
{
    if (index < 0 || index >= size) return;

    NODE* node = findNode(index);
    if (node != NULL)
    {
        removeNode(node);
    }
}

void LinkedList::deleteNode(int data)
{
    NODE* current = front;
    while (current != NULL)
    {
        if (current->data == data)
        {
            removeNode(current);
            return;
        }
        current = current->next;
    }
}
```

**图 9-1**

| 索引 0 | 索引 1 | 索引 2 | 索引 3 | 索引 4 |
| :--- | :--- | :--- | :--- | :--- |
| NodeA | NodeB | NodeC | NodeD | NodeE |
| NULL | NodeA | NodeB | NodeC | NodeD |
| NULL | NULL | NodeA | NodeB | NodeC |
| NULL | NULL | NULL | NodeA | NodeB |
| NULL | NULL | NULL | NULL | NodeA |

# 第 9 章 栈与队列：插入、删除、查看、查找

如果要删除的节点不是链表中的唯一节点，且不是链表的头部或尾部节点，那么唯一的可能性就是该节点位于链表的中间。

第四个过程是移除链表中间的节点，然后将前一个和下一个节点连接起来。我将用一个示例来说说明，因为这个操作可能会让人困惑。

假设你正在删除 `NodeC`。前一个节点是 `NodeB`，下一个节点是 `NodeD`。首先使用以下语句将 `NodeB` 连接到 `NodeD`：

```cpp
node->previous->next = node->next;
```

将 `node`、`previous` 和 `next` 替换为实际节点的名称以便更好地理解此操作：

```cpp
NodeB->next = NodeC->next;
```

现在 `NodeB` 已连接到 `NodeD`，你需要将 `NodeD` 连接到 `NodeB`：

```cpp
node->next->previous = node->previous;
```

再次，将 `node`、`shown` 和 `previous` 替换为节点名称以查看此操作是如何工作的：

```cpp
NodeD->previous = NodeB;
```

现在 `NodeB` 和 `NodeD` 都已相互连接，`NodeC` 从链表中被移除。

尽管传递给 `removeNode()` 函数的节点不再位于链表中，但它仍然保留在内存中。因此，你需要通过调用 `delete` 来移除该节点。最后一步是调整 `LinkedList` 的 `size` 成员，以反映链表中少了一个节点。你通过减小 `size` 的值来实现。

图 9-2 显示了执行 `removeNode()` 函数后的链表。注意，`NodeC` 不再位于链表中，索引值已调整以反映链表中新的节点数量。

| 索引 0 | 索引 1 | 索引 2 | 索引 3 |
|---|---|---|---|
| NodeA | NodeB | NodeD | NodeE |
| NULL | 20 | B | A | 30 | D | B | 50 | E | D | 60 | NULL |

图 9-2 删除 NodeC 后的链表

## 数据结构解密

```cpp
void removeNode(NODE* node)
{
    if (node->previous == NULL && node->next == NULL)
    {
        back = NULL;
        front = NULL;
    }
    else if (node->previous == NULL)
    {
        front = node->next;
        node->next->previous = NULL;
    }
    else if (node->next == NULL)
    {
        back = node->previous;
        node->previous->next = NULL;
    }
    else
    {
        node->previous->next = node->next;
        node->next->previous = node->previous;
    }

    delete node;
    size--;
}
```

# removeAt()

`removeAt()` 函数通过节点的索引而不是内存中节点的引用来移除节点。记住，索引是节点在链表中的位置。假设你想删除链表的第三个节点。只需将索引 `2` 传递给 `removeAt()` 函数，`removeNode()` 就会在内部执行该操作。你不能直接调用 `removeNode()`，因为它是受保护的，而且在类外部你也不无法获取任何实际的指针值。记住索引从 0 开始。因此，你不需要知道要删除的节点的实际引用。接下来的代码展示了这一点。

`removeAt()` 函数的第一步是确定索引是否有效。为了做到这一点，`removeAt()` 函数判断索引是否小于 0 或大于链表大小减 1。它使用 `LinkedList` 类中 `size` 成员的值来确定链表的大小。如果任一条件为真，则索引无效，且不会尝试移除节点。

然而，如果两个条件均为假，`removeNodeAt()` 函数将开始从列表中移除节点的流程。此过程有两个步骤：首先，通过索引定位对应的节点，其次，调用 `removeNode()` 函数并传递引用。

`removeNodeAt()` 函数通过声明一个名为 `temp_node` 的节点临时指针并将其分配链表头部节点的引用来开始搜索节点。接下来，使用 `for` 循环遍历链表上的每个节点，直到找到索引所表示的节点为止。在每次迭代中，`temp_node` 被赋值为当前 `temp_node` 的 `next` 成员所引用的节点。

当到达索引时，`temp_node` 的值指向与传递 `removeNodeAt()` 函数的索引对应的节点。调用 `removeNode()` 并传递 `temp_node`。

```cpp
void removeNodeAt(int index)
{
    if(index < 0 || index > size-1)
    {
        return;
    }

    NODE* temp_node = front;
    for(int i=0; i<index; i++)
    {
        temp_node = temp_node->next;
    }

    removeNode(temp_node);
}
```

# deleteNode()

`deleteNode()` 函数使用节点中存储的数据来查找并移除链表中对应的节点。`deleteNode()` 函数通过声明一个名为 `temp_node` 的节点临时指针并将其分配链表头部节点的引用来搜索节点。接下来，使用 `for` 循环遍历链表上的每个节点，直到找到索引所表示的节点为止。在每次迭代中，`temp_node` 被赋值为当前 `temp_node` 的 `next` 成员所引用的节点。

当到达索引时，`temp_node` 的值指向与传递 `deleteNode()` 函数的索引对应的节点。调用 `removeNode()` 并传递 `temp_node`。

# findNode()

```cpp
int findNode(int data)
{
    int index = 0;
    NODE* temp_node = front;
    while (temp_node != NULL)
    {
        if (temp_node->data == data)
        {
            return index;
        }
        else
        {
            temp_node = temp_node->next;
            index++;
        }
    }
    return -1;
}
```

# 深度解析数据结构

一旦 `insertNodeAt()` 知道索引是有效的，它将继续创建新节点并将节点插入到链表中。此过程从创建节点结构的一个实例开始，并将数据作为函数的参数传递。该实例被赋值给 `new_node` 指针。

接下来，它必须确定链表中是否存在任何节点。你通过评估 `LinkedList` 类中 `size` 成员的值来实现这一点。如果该值为零，则链表为空，新节点将成为列表中的唯一节点。

你通过将 `new_node` 指针同时赋值给 `LinkedList` 类的 `front` 成员和 `back` 成员将新节点放入列表。节点的 `previous` 和 `next` 成员默认已设置为 `NULL`，所以你不需要对新节点进行任何操作。

```cpp
front = new_node;
back = new_node;
```

如果链表有一个或多个节点，`insertNodeAt()` 函数将通过评估传递给函数的索引值，确定是否将新节点插入到链表的第一个位置。如果索引值为零，新节点将成为链表的第一个节点。

以下是其工作原理：`new_node` 被赋值给指向 `front` 成员的节点的 `previous` 成员。接下来，`new_node` 的 `next` 成员被赋值给 `LinkedList` 类的 `front` 成员。最后，`new_node` 被赋值给 `front` 成员。

```cpp
front->previous = new_node;
new_node->next = front;
front = new_node;
```

如果新节点不会成为链表的第一个节点，`insertNodeAt()` 函数通过比较索引与 `LinkedList` 的 `size` 成员，决定该节点是否将成为链表的最后一个节点。如果这些值相等，则新节点被放在链表的末尾。记住索引 0 是列表头部，索引 `(size - 1)` 是列表末尾。

以下是其实现方式：`new_node` 被赋值给链表末尾的节点。接下来，末尾节点被赋值给 `new_node` 的 `previous` 成员。最后，`new_node` 被赋值给 `LinkedList` 类的 `back` 成员。

```cpp
back->next = new_node;
new_node->previous = back;
back = new_node;
```

到此时，如果新节点尚未插入到链表的头部或末尾，`insertNodeAt()` 函数将假设新节点要插入到链表的中间。

![](img/9d4e3b4f2864cf2e0756eefc7e2e4b3e_179_0.png)

# 第 9 章 栈与队列：插入、删除、查看、查找

此过程从声明一个名为 `temp` 的指针并并将链表头部节点赋值给它开始。接下来，函数找到索引处的节点。该节点将向右移动。然而，它并没有被设置为 `previous` 节点，而是被设置为索引位置，并将该位置的节点向右移动。它通过循环来实现这一点。在每次迭代中，节点被赋值给 `temp` 节点的 `next` 成员，`temp` 被赋值给下一个 `temp` 节点。这听起来很困惑，但如果你检查正在发生什么，就会变得清晰。

假设链表上有五个节点，如图 9-1 所示。头部节点是 `NodeA`，`temp` 的初始值是 `NodeA`。假设你想在索引 2 处插入 `NodeN`。

在第一次迭代之前，`temp = NodeE`。在第一次迭代期间，发生了以下情况：

```cpp
temp = temp->next;
temp = NodeA->NodeB;
temp = NodeB;
```

第一次迭代后，`temp` 被赋值为 `NodeB` 且 `i` 的值为 1，小于索引值，因此执行另一次迭代。发生了以下情况：

```cpp
temp = temp->next;
temp = NodeB->NodeC;
temp = NodeC;
```

现在 `temp` 指针指向 `NodeC`，`i` 的值为 2，等于索引值，因此没有额外的迭代，且 `temp` 指针指向 `NodeC`。

现在你已经到达了链表中的目标位置，是时候交换指针以将新节点插入列表了。以下是操作方法：

```cpp
new_node->next = temp;
new_node->previous = temp->previous;
temp->previous->next = new_node;
temp->previous = new_node;
```

感到困惑吗？你并不孤单，因为发生的情况并不直观。我将用节点替换指针来澄清这段代码。

```cpp
new_node->next = NodeC;
new_node->previous = NodeB;
NodeB->next = new_node;
NodeC->previous = new_node;
```

图 9-3 显示了将新节点 `NodeN` 插入列表索引 2 之后的链表。

| 头部 / 尾部 | 索引 0 | 索引 1 | 索引 2 | 索引 3 | 索引 4 | 索引 5 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Front = NodeA | A | B | N | C | D | E |
| Back = NodeE | NULL | A | B | C | D | E |

**图 9-3** 一个名为 NodeN 的新节点被放在链表的索引 2 位置。最后一步是增加 `LinkedList` 类 `size` 成员以反映新节点。以下是 `insertNodeAt()` 函数的完整定义：

```cpp
void insertNodeAt(int index, int data) {
    if (index < 0 || index > size) {
        return;
    }

    NODE* new_node = new NODE(data);
    if (size == 0) {
        front = new_node;
        back = new_node;
    } else if (index == 0) {
        front->previous = new_node;
        new_node->next = front;
```
