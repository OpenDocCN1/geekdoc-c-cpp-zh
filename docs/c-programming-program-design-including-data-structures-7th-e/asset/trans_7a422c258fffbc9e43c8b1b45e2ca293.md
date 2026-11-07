
```cpp
while (current != nullptr && !found)  //search the list
    if (current->info == searchItem)  //searchItem is found
        found = true;
    else
        current = current->link;  //make current point to
                                   //the next node
return found;
}//end search
```

> **注意** 函数 search 也可以写成：

```cpp
template <class Type>
bool unorderedLinkedList<Type>::search(const Type& searchItem) const
{
    nodeType<Type> * current;  //pointer to traverse the list

    current = first;  //set current to point to the first
                      //node in the list

    while (current != nullptr)             //search the list
        if (current->info == searchItem)   //searchItem is found
            return true;
        else
            current = current->link;      //make current point to
                                           //the next node

    return false;  //searchItem is not in the list, return false
}//end search
```

## 插入第一个节点

函数 insertFirst 将新元素插入到链表开头——也就是说，插入到由 first 指向的节点之前。实现该函数所需的步骤如下：

- 1. 创建一个新节点。
- 2. 将新元素存储到新节点中。
- 3. 将该节点插入到 first 之前。
- 4. 将 count 加 1。

```cpp
template <class Type>
void unorderedLinkedList<Type>::insertFirst(const Type& newItem)
{
    nodeType<Type> * newNode;  //pointer to create the new node
    newNode = new nodeType<Type>;  //create the new node
    newNode->info = newItem;  //store the new item in the node
    newNode->link = first;     //insert newNode before first
    first = newNode;            //make first point to the
                                //actual first node
    count++;                    //increment count

    if (last == nullptr)        //if the list was empty, newNode is also
                                //the last node in the list
        last = newNode;
}//end insertFirst
```

## 插入最后一个节点

成员函数 insertLast 的定义与成员函数 insertFirst 的定义类似。这里，我们将新节点插入到 last 之后。函数 insertLast 本质上如下：

```cpp
template <class Type>
void unorderedLinkedList<Type>::insertLast(const Type& newItem)
{
    nodeType<Type> * newNode;  //pointer to create the new node

    newNode = new nodeType<Type>;  //create the new node
    newNode->info = newItem;       //store the new item in the node
    newNode->link = nullptr;       //set the link field of newNode
                                   //to nullptr

    if (first == nullptr)          //if the list is empty, newNode is
                                   //both the first and last node
    {
        first = newNode;
        last = newNode;
        count++;                   //increment count
    }
    else                           //the list is not empty, insert newNode after last
    {
        last->link = newNode;      //insert newNode after last
        last = newNode;            //make last point to the actual
                                   //last node in the list
        count++;                   //increment count
    }
}//end insertLast
```

## 删除节点

接下来，我们讨论成员函数 deleteNode 的实现，该函数从链表中删除具有给定 info 的节点。我们需要考虑几种情况：

- 1. **情况1：** 链表为空。
- 2. **情况2：** 第一个节点就是具有给定 info 的节点。在这种情况下，我们需要调整指针 `first`。

**情况3：** 具有给定 info 的节点位于链表中的某个位置。如果要删除的节点是最后一个节点，那么我们必须调整指针 last。

**情况4：** 链表中不包含具有给定 info 的节点。

如果链表为空，我们只需输出一条表示链表为空的消息。如果链表不为空，我们在链表中搜索具有给定 info 的节点，如果找到这样的节点，就删除该节点。删除节点后，count 减 1。用伪代码表示，算法如下：

```
if list is empty
    Output(cannot delete from an empty list);
else
{
    if the first node is the node with the given info
        adjust the head pointer, that is, first, and deallocate
        the memory;
    else
    {
        search the list for the node with the given info
        if such a node is found, delete it and adjust the
        values of last (if necessary) and count.
    }
}
```

**情况1：** 链表为空。

如果链表为空，则输出如伪代码所示的错误消息。

**情况2：** 链表不为空。要删除的节点是第一个节点。

这种情况有两种情形：链表只有一个节点，以及链表有多个节点。考虑如图 16–22 所示的只有一个节点的链表。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1151_0.png)

*图 16-22* 只有一个节点的链表

假设我们要删除 37。删除后，链表变为空。因此，删除后，first 和 last 都被设置为 `nullptr`，count 被设置为 0。

现在考虑如图 16–23 所示的具有多个节点的链表。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1152_0.png)

**图 16-23** 具有多个节点的链表

假设要删除的节点是 28。删除该节点后，第二个节点成为第一个节点。因此，删除该节点后，指针 first 的值发生变化；也就是说，删除后，first 包含 info 为 17 的节点的地址，并且 count 减 1。图 16-24 显示了删除 28 后的链表。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1152_1.png)

**图 16-24** 删除 info 为 28 的节点后的链表

**情况3：** 要删除的节点不是第一个节点，而是位于链表中的某个位置。

这种情况有两个子情况：(a) 要删除的节点不是最后一个节点，(b) 要删除的节点是最后一个节点。下面说明这两种情况。

**情况3a：** 要删除的节点不是最后一个节点。

考虑图 16-25 所示的链表。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1152_2.png)

**图 16-25** 删除 37 之前的链表

假设要删除的节点是 37。删除该节点后，得到的链表如图 16-26 所示。（注意，删除 37 不需要我们更改

由情况2、情况3和情况4可知，删除节点需要遍历链表。由于链表不是随机存取数据结构，我们必须顺序搜索链表。我们单独处理情况1，因为它不需要遍历链表。我们从第二个节点开始顺序搜索链表。如果要删除的节点位于链表中间，我们需要调整该节点前一个节点的 link 字段。因此，我们需要一个指向前一个节点的指针。当我们搜索具有给定 info 的节点时，使用两个指针：一个用于检查当前节点的 info，另一个用于跟踪当前节点之前的节点。如果要删除的节点是最后一个节点，我们必须调整指针 last。

函数 deleteNode 的定义如下：

```cpp
template <class Type>
void unorderedLinkedList<Type>::deleteNode(const Type& deleteItem)
{
    nodeType<Type> *current; //pointer to traverse the list
    nodeType<Type> *trailCurrent; //pointer just before current
    bool found;

    if (first == nullptr)    //Case 1: the list is empty
        cout << "Cannot delete from an empty list."
             << endl;
    else
    {
        if (first->info == deleteItem) //Case 2
        {
            current = first;
            first = first->link;
            count--;

            if (first == nullptr)    //the list has only one node
                last = nullptr;

            delete current;
        }
        else //search the list for the node with the given info
        {
            found = false;
            trailCurrent = first;    //set trailCurrent to point
                                     //to the first node
            current = first->link;   //set current to point to
                                     //the second node

            while (current != nullptr && !found)
            {
                if (current->info != deleteItem)
                {
                    trailCurrent = current;
                    current = current->link;
                }
                else
                    found = true;
            }//end while
        }
    }
}
```
