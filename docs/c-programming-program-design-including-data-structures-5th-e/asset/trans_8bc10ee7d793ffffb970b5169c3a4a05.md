
```cpp
template <class Type>
class doublyLinkedList
{
public:
    const doublyLinkedList<Type>& operator=
                   (const doublyLinkedList<Type>&);
    //Overload the assignment operator.

    void initializeList();
    //Function to initialize the list to an empty state.
    //Postcondition: first = NULL; last = NULL; count = 0;

    bool isEmptyList() const;
    //Function to determine whether the list is empty.
    //Postcondition: Returns true if the list is empty,
    //               otherwise returns false.

    void destroy();
    //Function to delete all the nodes from the list.
    //Postcondition: first = NULL; last = NULL; count = 0;

    void print() const;
    //Function to output the info contained in each node.

    void reversePrint() const;
    //Function to output the info contained in each node
    //in reverse order.

    int length() const;
    //Function to return the number of nodes in the list.
    //Postcondition: The value of count is returned.

    Type front() const;
    //Function to return the first element of the list.
    //Precondition: The list must exist and must not be empty.
    //Postcondition: If the list is empty, the program
    //               terminates; otherwise, the first
    //               element of the list is returned.

    Type back() const;
    //Function to return the last element of the list.
    //Precondition: The list must exist and must not be empty.
    //Postcondition: If the list is empty, the program
    //               terminates; otherwise, the last
    //               element of the list is returned.

    bool search(const Type& searchItem) const;
    //Function to determine whether searchItem is in the list.
    //Postcondition: Returns true if searchItem is found in
    //               the list, otherwise returns false.

    void insert(const Type& insertItem);
    //Function to insert insertItem in the list.
    //Precondition: If the list is nonempty, it must be in
    //              order.
    //Postcondition: insertItem is inserted at the proper place
    //               in the list; first points to the first
    //               node, last points to the last node of the
    //               new list, and count is incremented by 1.

    void deleteNode(const Type& deleteItem);
    //Function to delete deleteItem from the list.
    //Postcondition: If found, the node containing deleteItem
    //               is deleted from the list; first points
    //               to the first node of the new list, last
    //               points to the last node of the new list,
    //               and count is decremented by 1; otherwise
    //               an appropriate message is printed.

    doublyLinkedList();
    //default constructor
    //Initializes the list to an empty state.
    //Postcondition: first = NULL; last = NULL; count = 0;

    doublyLinkedList(const doublyLinkedList<Type>& otherList);
    //copy constructor
    ~doublyLinkedList();
    //destructor
    //Postcondition: The list object is destroyed.

protected:
    int count;
    nodeType<Type> *first;   //pointer to the first node
    nodeType<Type> *last;    //pointer to the last node

private:
    void copyList(const doublyLinkedList<Type>& otherList);
        //Function to make a copy of otherList.
        //Postcondition: A copy of otherList is created and
        //               assigned to this list.
};
```

我们将类 `doublyLinkedList` 的 UML 类图留作练习。

实现双向链表操作的函数与前面讨论的函数类似。这里，因为每个节点都有两个指针 `back` 和 `next`，所以有些操作需要调整每个节点中的两个指针。对于插入和删除操作，因为我们可以沿任一方向遍历链表，所以我们只使用一个指针来遍历链表。让我们称这个指针为 `current`。我们可以通过 `current` 指针以及 `current` 所指向节点的 `back` 指针来设置 `trailCurrent` 的值。这里给出每个函数的定义，但有四个例外。

## 定义

### 初始化链表

此操作将双向链表重新初始化为空状态。此任务可以通过使用 `destroy` 操作来完成。函数 `initializeList` 的定义为：

```cpp
template <class Type>
void doublyLinkedList<Type>::initializeList()
{
    destroy();
}
```

### 链表的长度

链表的长度（即链表中有多少个节点）存储在变量 `count` 中。因此，此函数返回该变量的值。

```cpp
template <class Type>
int doublyLinkedList<Type>::length() const
{
    return count;
}
```

### 打印链表

函数 `print` 输出每个节点中包含的信息。我们从第一个节点开始遍历链表。

```cpp
template <class Type>
void doublyLinkedList<Type>::print() const
{
    nodeType<Type> *current; //pointer to traverse the list

    current = first;  //set current to point to the first node

    while (current != NULL)
    {
        cout << current->info << " ";  //output info
        current = current->next;
    }//end while
}//end print
```

### 反向打印链表

此函数按相反顺序输出每个节点中包含的信息。我们从最后一个节点开始按相反顺序遍历链表。其定义为：

```cpp
template <class Type>
void doublyLinkedList<Type>::reversePrint() const
{
    nodeType<Type> *current; //pointer to traverse
                              //the list

    current = last;   //set current to point to the
                       //last node

    while (current != NULL)
    {
        cout << current->info << " ";
        current = current->back;
    }//end while
}//end reversePrint
```

### 查找链表

如果 `searchItem` 在链表中找到，则函数 `search` 返回 `true`；否则返回 `false`。该查找算法与有序链表的查找算法完全相同。

```cpp
template <class Type>
bool doublyLinkedList<Type>::search(const Type& searchItem) const
{
    bool found = false;
    nodeType<Type> *current; //pointer to traverse the list

    current = first;

    while (current != NULL && !found)
        if (current->info >= searchItem)
            found = true;
        else
            current = current->next;

    if (found)
        found = (current->info == searchItem); //test for
                                               //equality

    return found;
}//end search
```

### 第一个和最后一个元素

函数 `front` 返回链表的第一个元素，函数 `back` 返回链表的最后一个元素。如果链表为空，则这两个函数都会终止程序。它们的定义为：

```cpp
template <class Type>
Type doublyLinkedList<Type>::front() const
{
    assert(first != NULL);

    return first->info;
}

template <class Type>
Type doublyLinkedList<Type>::back() const
{
    assert(last != NULL);

    return last->info;
}
```

### 插入节点

因为我们是在双向链表中插入一个项，所以向链表中插入节点需要调整某些节点中的两个指针。和之前一样，我们找到新项应该插入的位置，创建节点，存储新项，并调整新节点以及链表中其他特定节点的链接字段。共有四种情况：

- **情况 1：** 在空链表中插入
- **情况 2：** 在非空链表的开头插入
- **情况 3：** 在非空链表的末尾插入
- **情况 4：** 在非空链表的某个位置插入

情况 1 和情况 2 都需要我们更改指针 `first` 的值。情况 3 和情况 4 类似。插入一个项后，`count` 增加 1。接下来，我们展示情况 4。

考虑图 17-40 所示的双向链表。

![](img/f97f778697507bb6fdd80c5991210cba_1087_0.png)

图 17-40 插入 20 之前的双向链表

假设要将 20 插入链表中。插入 20 后，得到的链表如图 17-41 所示。
