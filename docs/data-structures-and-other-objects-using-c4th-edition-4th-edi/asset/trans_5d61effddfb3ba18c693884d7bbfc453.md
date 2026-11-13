

请注意，我们已经复制了链表的第一个节点。在循环的第一次迭代中，我们复制链表的第二个节点——即 source_ptr 指向的节点。复制节点的第一部分是调用我们的另一个工具 list_insert，如下所示：

```
list_insert(tail_ptr, source_ptr->data());
```

此函数调用会在我们正在创建的列表末尾添加一个新节点（即 tail_ptr 指向的节点之后），新节点中的数据是数字 20（即 source_ptr->data() 中的数据）。插入后立即，函数的指针如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_276_0.png)

循环体中的第二条语句将 tail_ptr 向前移动到新列表的新尾部，如下所示：

```
tail_ptr = tail_ptr->link();
```

这是我们让指针“移动到下一个节点”的常用方法，如我们在 list_search 等其他函数中所见。移动尾指针后，函数的指针配置如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_276_1.png)

在此示例中，source_ptr 将移动到第三个节点，循环体将再次执行一次以将第三个节点复制到新列表中。然后循环结束。list_copy 的完整实现如图 5.8 所示。

## 图 5.8 复制链表的函数

### 函数实现

```
void list_copy(const node* source_ptr, node*& head_ptr, node*& tail_ptr)
    // Precondition: source_ptr is the head pointer of a linked list.
    // Postcondition: head_ptr and tail_ptr are the head and tail pointers for a new list that contains
    // the same items as the list pointed to by source_ptr. NOTE: If there is insufficient
    // dynamic memory to create the new list, then bad_alloc is thrown.
    // Library facilities used: cstddef
{
    head_ptr = NULL;
    tail_ptr = NULL;

    // Handle the case of the empty list.
    if (source_ptr == NULL)
        return;

    // Make the head node for the newly created list, and put data in it.
    list_head_insert(head_ptr, source_ptr->data());
    tail_ptr = head_ptr;

    // Copy the rest of the nodes one at a time, adding at the tail of new list.
    source_ptr = source_ptr->link();
    while (source_ptr != NULL)
    {
        list_insert(tail_ptr, source_ptr->data()); // Loop for Step 4
        tail_ptr = tail_ptr->link();
        source_ptr = source_ptr->link();
    }
}
```

## 删除链表头部的节点

我们的工具包中还有三个函数，它们都用于从链表中删除节点。第一个删除函数删除头节点，如下所示：

```
void list_head_remove(node*& head_ptr);
// Precondition: head_ptr is the head pointer of a linked list,
// with at least one node.
// Postcondition: The head node has been removed and returned to the
// heap; head_ptr is now the head pointer of the new, shorter linked list.
```

与 list_head_insert 类似，头指针是引用参数，因为该函数使头指针指向不同的节点。

乍一看，似乎只需两步即可删除头节点：（1）将头指针移动到列表的下一个节点；（2）将原始头节点返回到堆中。这些步骤有一个小缺陷：在第 1 步中移动头指针后，我们就不再与原始头节点有任何联系了。因此，我们的完整伪代码需要三步：

- 1. 设置一个名为 remove_ptr 的指针，使其指向头节点。（这是我们保持与原始头节点联系的方式。）
- 2. 移动头指针，使其指向第二个节点（如果没有第二个节点，则变为 NULL）。
- 3. delete remove_ptr。（这将原始头节点返回到堆中。）

这三个步骤在图 5.9 的顶部（第 253 页）中实现。

## 删除非头部的节点

我们的第二个删除函数删除链表中不在头部的节点。该方法类似于在链表中间插入节点。要删除中间节点，我们必须设置一个指向要删除节点前一个节点的指针。例如，要从以下列表中删除 42，我们需要像下面这样设置 previous_ptr：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_278_0.png)

如您所见，previous_ptr 并不实际指向我们要删除的节点（即 42）；相反，它指向被删除节点的前一个节点。这是因为前一个节点的 link 字段必须重新赋值，因此我们需要一个指向该前节点的指针。使用 previous_ptr 的删除函数原型如下所示。

```
void list_remove(node* previous_ptr);
// Precondition: previous_ptr points to a node in a linked list,
//   and this is not the tail node of the list.
// Postcondition: The node after previous_ptr has been removed
//   from the linked list.
```

list_remove 所需的步骤与删除列表头部的步骤类似。以下是伪代码：

- 1. 设置一个名为 `remove_ptr` 的指针，使其指向被删除的节点。（这是 `previous_ptr` 指向的节点之后的节点。）
- 2. 重置 `previous_ptr` 的 link 字段，使其指向被删除节点之后的节点（如果被删除节点是尾节点，则为 NULL）。
- 3. `delete remove_ptr`。（这将被删除的节点返回到堆中。）

作为示例，让我们从刚才看到的列表中删除节点 42。`previous_ptr` 被设置为指向前一个节点，然后执行删除伪代码的第 1 步。第 1 步之后，指针如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_279_0.png)

伪代码的第 2 步需要使前一个节点的 link 指向我们要删除的节点之后的节点。此步骤更改下图中阴影指针：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_279_1.png)

此时，包含 42 的节点不再是链表的一部分。列表的第一个节点包含 10，下一个节点有 20，沿着指针我们到达第三个也是最后一个节点，包含 30。剩下的就是第 3 步，`delete remove_ptr`，它将已删除的节点返回到堆中。

完整实现如图 5.9 的中间部分所示。您应该检查该函数是否正常工作，即使删除的节点是列表的最后一个节点。在这种情况下，前一个节点的 link 应设置为 NULL，无需特殊代码即可实现。

## 清空链表

我们的最后一个函数删除链表中的所有节点，并将它们返回到堆中。该实现（图 5.9 中的 `list_clear`）是一个循环，反复调用 `list_head_remove`，直到所有节点都被删除。请注意，当列表的最后一个节点被删除时，头指针将为 null，这会停止循环。此外，头指针是引用参数，因此当函数返回时，调用程序中的实际头指针将为 null。

## 链表工具包——将各部分组合在一起

工具包的函数已完善。第 254 页的图 5.10 显示了工具包的一个头文件，名为 node1.h。除了文档外，该头文件还提供节点的类定义，以及函数的原型。在该文件中，我们已将 value_type 定义为 double，但如文档所示，value_type 可以更改为其他数据类型。

## 图 5.9 从链表中删除节点的函数

### 三个函数实现

```
void list_head_remove(node*& head_ptr)
// Precondition: head_ptr is the head pointer of a linked list, with at least one node.
// Postcondition: The head node has been removed and returned to the heap;
// head_ptr is now the head pointer of the new, shorter linked list.
{
    node *remove_ptr;
    remove_ptr = head_ptr;
    head_ptr = head_ptr->link();
    delete remove_ptr;
}
```

```
void list_remove(node* previous_ptr)
// Precondition: previous_ptr points to a node in a linked list, and this is not the tail node of the list.
// Postcondition: The node after previous_ptr has been removed from the linked list.
{
    node *remove_ptr;
    remove_ptr = previous_ptr->link();
    previous_ptr->set_link(remove_ptr->link());
    delete remove_ptr;
}
```

```
void list_clear(node*& head_ptr)
// Precondition: head_ptr is the head pointer of a linked list.
// Postcondition: All nodes of the list have been deleted, and head_ptr is now NULL.
// Library facilities used: cstdlib
{
    while (head_ptr != NULL)
        list_head_remove(head_ptr);
}
```

