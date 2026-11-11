
![](img/57c0d966bb33c67a5a188e6bf39e4e02_533_0.png)

由于指针 temp 现在指向下一个节点，我们可以再次执行以下语句：

```cpp
cout<<temp->data<<endl;
```

这将打印值 **20**，因为此时指针 temp 所指向节点的数据值是 20，如图 10.24 所示。因此，打印节点值的过程可以继续，直到指针 temp 超出链表。于是，可以使用下面的 while 循环遍历整个链表。请注意，当 temp=NULL 时 while 循环终止，这表明该指针已经越过链表的最后一个节点。不要混淆这两个条件：temp->next=NULL 表示 temp 指向链表的最后一个节点，而 temp=NULL 表示 temp 已经越过链表的最后一个节点。这里，我们正在遍历并打印链表中存储的数据值，而且还需要打印最后一个节点的数据值。因此，只要条件 temp !=NULL 为真，while 循环就应持续运行。

```cpp
void traverse()
{
    Node *temp;
    temp=head;
    cout<<"The elements of the linked list are as below:"<<endl;
    /*Traverse the list until it ends*/
    while(temp!=NULL)
    {
        cout<<temp->data<<endl;
        temp=temp->next;
    }
}
```

### 10.3.5 在链表中查找元素

现在让我们编写一个函数 find()，用于查找链表中是否存在某个特定数据值。该函数将接收一个整数参数 (x)，并从链表的第一个节点开始查找值 x 是否存在。如下方代码所示，指针 temp 被初始化为链表的第一个节点，并且如果满足以下任一条件，遍历循环就会终止：

- 1. **在链表中找到元素 x：** 如果我们要查找的数据元素 x 在链表中被找到，就不需要继续向后遍历链表。这意味着我们应该

```cpp
{
    /*Node found*/
    cout<<"Element found"<<endl;
}
}
```

### 10.3.6 删除链表中的元素

为了理解从现有链表中删除节点的算法，让我们考虑下图 10.25 所示的由四个节点创建的链表。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_535_0.png)

让我们理解从图 10.25 所示的链表中删除数据值为 30 的节点的过程。

如果要删除的节点是 x，那么我们可以使用下面的 while 循环查找数据值为 x 的节点，该循环在上一节编写 find() 函数时讨论过。

```cpp
Node *temp;
temp=head;
while(temp!=NULL && temp->data!=x)
{
    temp=temp->next;
}
```

如果要删除节点的数据值为 30，那么上述 while 循环在执行完毕后会使指针 temp 指向待删除的节点，如图 10.26 所示。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_535_1.png)

即使我们已经找到待删除的节点，并且指针 temp 指向它，仅使用指针 temp 也无法从链表中删除该节点。这是因为删除操作的要求是：待删除节点的“前一个节点”的 next 指针必须指向待删除节点的“下一个节点”，从而从链表中移除对“待删除节点”的所有引用。这意味着，要删除数据值为 30 的节点，我们应该让 20 的 next 指向 40，因为 20 是 30 的前一个节点，而 40 是 30 的下一个节点。因此，对节点 30 的所有引用现在都将从链表中移除，如图 10.27 所示，从而从链表中删除数据为 30 的节点。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_536_0.png)

为了设置待删除节点的“前一个节点”的 next 指针，我们需要再增加一个指针，使其始终指向待删除节点的“前一个节点”。我们将这个指针命名为 prev。指针 prev 的职责是始终指向 temp 所指向节点的前一个节点。这意味着，初始时当指针 temp 指向第一个节点，指针 prev 应指向 NULL，因为“第一个节点”之前没有节点。因此，指针 prev 的初始值被设置为 NULL，如下面的语句所示：

```cpp
Node *prev=NULL;
```

另外，每次我们让指针 temp 移动到下一个节点时，都会将指针 temp 的旧值保存到指针 prev 中，如下面的语句所示。这将确保指针 prev 始终指向指针 temp 的前一个节点。

```cpp
while(temp!=NULL && temp->data!=x)
{
    prev=temp;       /*store the old value of temp in prev*/
    temp=temp->next; /*move temp ahead*/
}
```

因此，当指针 temp 停在数据值为 30 的节点时，指针 prev 将指向数据值为 20 的节点，如图 10.28 所示。这是因为数据值为 20 的节点是数据值为 30 的节点的前一个节点。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_537_0.png)

图 10.28：**指针 prev 和 temp**

要让 20 的 next 指向 40，我们需要将 prev 所指向节点的 next 指针设置为指向 temp 的“下一个节点”。这是因为 prev 的 next 指针指向数据值为 20 的节点的下一个值，而节点 temp 的 next 指针指向数据值为 40 的节点。因此，下面的语句将从链表中移除节点 30，如图 10.29 所示。

```cpp
prev->next=temp->next;
```

另外，请注意第一个节点之前没有节点，因此如果要删除的节点是第一个节点，我们就需要修改头指针，使 head 指向链表中的第二个节点，这意味着第一个节点已从链表中删除。因此，如果要删除的节点是第一个节点（temp==head），我们就不会执行上面的语句，因为第一个节点的 prev 指向 NULL。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_537_1.png)

图 10.29：**删除数据值为 30 的节点**

因此，如果要删除的节点是链表的第一个节点，则必须执行下面的代码块来修改链表的头指针：

```cpp
if(temp==head)
{
    head=head->next ;
}
```

以下是从链表中删除值为 x 的节点的完整算法：

```cpp
void remove(int x)
{
    Node *temp;
    temp=head;
    Node *prev=NULL;
    while(temp!=NULL && temp->data!=x)
    {
        prev=temp;      /*store the old value of temp in prev*/
        temp=temp->next; /*move temp ahead*/
    }
    if(temp==head)
    {
        /*Node to be deleted is the first node*/
        head=head->next;
    }
    else
    {
        /*Node to be deleted is not the first node*/
        prev->next=temp->next;
    }
}
```

> **从链表中删除一个节点的含义是什么？我们是释放分配给该节点的内存，还是仅仅将该节点从链表中解除链接？**
>
> 我们编写的删除算法只是将节点从链表中解除链接。目前我们还没有编写显式的 delete 语句，因为我们在 RAM 中创建了完整的链表，而且它本来也不是持久化的。当我们将一个节点从链表中解除链接时，在对链表执行任何进一步操作时，该特定节点将不会被视为链表的一部分。因此，解除节点链接等同于从链表中删除它。然而，及时释放程序占用的未使用内存始终是一种良好做法，这可以通过 C++ 中的 delete 关键字来完成。我们将在本章后面讨论 delete 关键字。

### 10.3.7 链表的创建与操作

创建链表的完整源代码如下所示。主程序是菜单驱动的，将向用户提供以下选项来对链表执行操作。
