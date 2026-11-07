
## 重载赋值运算符

为类 `linkedListType` 重载赋值运算符的函数定义与复制构造函数的定义类似。为了完整起见，我们给出它的定义。

```cpp
//Overload the assignment operator
template <class Type>
const linkedListType<Type>& linkedListType<Type>::operator=
                         (const linkedListType<Type>& otherList)
{
    if (this != &otherList) //avoid self-copy
    {
        copyList(otherList);
    }//end else

        return *this;
}
```

## 无序链表

如前一节所述，我们从抽象类 `linkedListType` 派生出类 `unorderedLinkedList`，并实现操作 search、insertFirst、insertLast 和 deleteNode。

下面的类将无序链表定义为一种 ADT。

```cpp
template <class Type>
class unorderedLinkedList: public linkedListType<Type>
{
public:
    bool search(const Type& searchItem) const;
    //Function to determine whether searchItem is in the list.
    //Postcondition: Returns true if searchItem is in the
    //              list, otherwise the value false is
    //              returned.

    void insertFirst(const Type& newItem);
    //Function to insert newItem at the beginning of the list.
    //Postcondition: first points to the new list, newItem is
    //              inserted at the beginning of the list,
    //              last points to the last node in the
    //              list, and count is incremented by 1.

    void insertLast(const Type& newItem);
    //Function to insert newItem at the end of the list.
    //Postcondition: first points to the new list, newItem
    //              is inserted at the end of the list,
    //              last points to the last node in the
    //              list, and count is incremented by 1.

    void deleteNode(const Type& deleteItem);
    //Function to delete deleteItem from the list.
    //Postcondition: If found, the node containing
    //                deleteItem is deleted from the list.
    //                first points to the first node, last
    //                points to the last node of the updated
    //                list, and count is decremented by 1.
};
```

![](img/f97f778697507bb6fdd80c5991210cba_1058_0.png)

图17-21展示了类 `unorderedLinkedList` 的UML类图及继承层次结构。

![](img/f97f778697507bb6fdd80c5991210cba_1059_0.png)

**图17-21** 类 `unorderedLinkedList` 的UML类图及继承层次结构

接下来，我们给出类 `unorderedLinkedList` 的成员函数定义。

### 搜索链表

成员函数 search 在链表中查找给定项。如果找到该项，则返回 true；否则返回 false。因为链表不是随机访问数据结构，我们必须从第一个节点开始顺序搜索链表。

该函数包含以下步骤：

- 1. 将查找项与链表中的当前节点进行比较。如果当前节点的 info 与查找项相同，则停止搜索；否则，将下一个节点设为当前节点。
- 2. 重复步骤1，直到找到该项，或者链表中没有更多数据可与查找项比较。

```cpp
template <class Type>
bool unorderedLinkedList<Type>::
                         search(const Type& searchItem) const
{
    nodeType<Type>* current; //pointer to traverse the list
    bool found = false;
    current = first;         //set current to point to the first
                             //node in the list
```

```cpp
newNode->link = first;        //insert newNode before first
first = newNode;              //make first point to newNode

count++;                      //increment count

if (last == NULL)             //if the list was empty, newNode is also
                               //the last node in the list
    last = newNode;
}//end insertFirst
```

### 插入尾节点

成员函数 `insertLast` 的定义与成员函数 `insertFirst` 的定义类似。这里，我们将新节点插入到 last 之后。本质上，函数 `insertLast` 如下：

```cpp
template <class Type>
void unorderedLinkedList<Type>::insertLast(const Type& newItem)
{
    nodeType<Type> *newNode;  //pointer to create the new node

    newNode = new nodeType<Type>; //create the new node
    newNode->info = newItem;      //store the new item in the node
    newNode->link = NULL;         //set the link field of newNode
                                  //to NULL

    if (first == NULL)   //if the list is empty, newNode is
                         //both the first and last node
    {
        first = newNode;
        last = newNode;
        count++;         //increment count
    }
    else                 //the list is not empty, insert newNode after last
    {
        last->link = newNode; //insert newNode after last
        last = newNode;       //make last point to the actual
                              //last node in the list
        count++;              //increment count
    }
}//end insertLast
```

### 删除节点

接下来，我们讨论成员函数 `deleteNode` 的实现，它从链表中删除具有给定 info 的节点。我们需要考虑以下几种情况：

- 1. **情况1：** 链表为空。
- 2. **情况2：** 第一个节点就是具有给定 info 的节点。在这种情况下，我们需要调整指针 first。
- 3. **情况3：** 具有给定 info 的节点位于链表中的某个位置。如果要删除的节点是最后一个节点，那么我们必须调整指针 last。
- 4. **情况4：** 链表中不包含具有给定 info 的节点。

如果链表为空，我们可以简单地打印一条消息，指出链表为空。如果链表不为空，我们在链表中搜索具有给定 info 的节点，如果找到这样的节点，就删除该节点。删除节点后，count 减1。用伪代码表示，算法为：

```
if list is empty
    output(cannot delete from an empty list);
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

如果链表为空，则如伪代码所示输出一条错误消息。

**情况2：** 链表不为空。要删除的节点是第一个节点。

这种情况有两种情形：链表只有一个节点，以及链表有多个节点。考虑如图17-22所示的只有一个节点的链表。

![](img/f97f778697507bb6fdd80c5991210cba_1062_0.png)

**图17-22** *只有一个节点的链表*

假设我们要删除37。删除后，链表变为空。因此，删除后，first 和 last 都被设置为 NULL，count 被设置为0。

现在考虑如图17-23所示的具有多个节点的链表。

![](img/f97f778697507bb6fdd80c5991210cba_1063_0.png)

**图17-23** *具有多个节点的链表*

假设要删除的节点是28。删除该节点后，第二个节点成为第一个节点。因此，删除该节点后，指针 first 的值发生变化；也就是说，删除后，first 包含 info 为17的节点的地址，并且 count 减1。图17-24展示了删除28后的链表。

![](img/f97f778697507bb6fdd80c5991210cba_1063_1.png)

**图17-24** *删除 info 为28的节点后的链表*

**情况3：** 要删除的节点不是第一个节点，而是位于链表中的某个位置。

这种情况有两个子情况：(a) 要删除的节点不是最后一个节点；(b) 要删除的节点是最后一个节点。下面说明这两种情况。

**情况3a：** 要删除的节点不是最后一个节点。

考虑如图17-25所示的链表。

![](img/f97f778697507bb6fdd80c5991210cba_1063_2.png)

**图17-25** *删除37之前的链表*

假设要删除的节点是37。删除该节点后，得到的链表如图17-26所示。（注意，删除37不需要我们改变
