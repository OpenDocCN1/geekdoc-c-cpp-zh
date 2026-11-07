

```cpp
void deleteNode(const Type& deleteItem);
//Function to delete deleteItem from the list.
//Postcondition: If found, the node containing
//              deleteItem is deleted from the list.
//              first points to the first node, last
//              points to the last node of the updated
//              list, and count is decremented by 1.
};

//Place the definitions of the functions search,
//insertFirst, insertLast, and deleteNode here.
.
.
.
#endif
```

> **注意** 随书附带的网站包含多个演示如何使用 `unorderedLinkedList` 类的程序。

## 有序链表

上一节介绍了无序链表的操作。本节讨论有序链表。正如前面所述，我们从 `linkedListType` 类派生出 `orderedLinkedList` 类，并提供抽象函数 `insertFirst`、`insertLast`、`search` 和 `deleteNode` 的定义，以利用有序链表中的元素按照某种排序标准排列这一事实。为简单起见，我们假设有序链表中的元素按升序排列。

由于有序链表中的元素按照顺序排列，我们加入 `insert` 函数，以便在有序链表中的适当位置插入元素。

下面的类将有序链表定义为一个 ADT：

```cpp
template <class Type>
class orderedLinkedList: public linkedListType<Type>
{
public:
    bool search(const Type& searchItem) const;
    //Function to determine whether searchItem is in the list.
    //Postcondition: Returns true if searchItem is in the list,
    //              otherwise it returns false.

    void insert(const Type& newItem);
    //Function to insert newItem in the list.
    //Postcondition: first points to the new list, newItem
    //              is inserted at the proper place in the
    //              list, and count is incremented by 1.

    void insertFirst(const Type& newItem);
    //Function to insert newItem in the list.
    //Because the resulting list must be sorted, newItem is
    //inserted at the proper place in the list.
    //This function uses the function insert to insert newItem.
    //Postcondition: First points to the new list, newItem is
    //              inserted at the proper place in the list,
    //              and count is incremented by 1.
    //
    void insertLast(const Type& newItem);
    //Function to insert newItem at the end of the list.
    //Because the resulting list must be sorted, newItem is
    //inserted at the proper place in the list.
    //This function uses the function insert to insert newItem.
    //Postcondition: First points to the new list, newItem is
    //              inserted at the proper place in the list,
    //              and count is incremented by 1.
    //
    void deleteNode(const Type& deleteItem);
    //Function to delete deleteItem from the list.
    //Postcondition: If found, the node containing
    //              deleteItem is deleted from the list;
    //              first points to the first node of the
    //              new list, and count is decremented by 1.
    //              If deleteItem is not in the list, an
    //              appropriate message is printed.
};
```

图 16-29 展示了 `orderedLinkedList` 类的 UML 类图及其继承层次结构。

![](img/b217c421655b51e7494cf3b89bb5432d_1170_0.png)

**图 16-29** `orderedLinkedList` 类的 UML 类图及其继承层次结构

下面给出 `orderedLinkedList` 类成员函数的定义。

### 搜索链表

首先，我们讨论搜索操作。实现搜索操作的算法与前面讨论的一般链表搜索算法类似。这里，由于链表已经排序，我们可以在一定程度上改进搜索算法。与之前一样，我们从链表的第一个节点开始搜索。当找到一个节点，其 `info` 大于或等于搜索项时，或者已经搜索完整个链表时，我们就停止搜索。

下面的步骤描述了该算法：

- 1. 将搜索项与链表中的当前节点进行比较。如果当前节点的 `info` 大于或等于搜索项，则停止搜索；否则，将下一个节点设为当前节点。
- 2. 重复步骤 1，直到找到链表中大于或等于搜索项的项，或者链表中没有更多数据可与搜索项进行比较。

注意，循环不会显式检查搜索项是否等于链表中的某个项。因此，循环执行完毕后，我们必须检查搜索项是否等于链表中的项。

```cpp
template <class Type>
bool orderedLinkedList<Type>::search(const Type& searchItem) const
{
    bool found = false;
    nodeType<Type> *current; //pointer to traverse the list

    current = first; //start the search at the first node

    while (current != nullptr && !found)
        if (current->info >= searchItem)
            found = true;
        else
            current = current->link;

    if (found)
        found = (current->info == searchItem); //test for equality

    return found;
}//end search
```

### 插入节点

要在有序链表中插入一个项，我们首先找到新项应该插入的位置，然后将该项插入链表。为了找到新项的位置，我们像之前一样搜索链表。这里，我们使用两个指针 `current` 和 `trailCurrent` 来搜索链表。指针 `current` 指向其 `info` 正在与待插入项进行比较的节点，而 `trailCurrent` 指向 `current` 前面的节点。由于链表是有序的，搜索算法与之前相同。具体会出现以下几种情况：

- 情况 1：链表最初为空。包含新项的节点是唯一的节点，因此也是链表中的第一个节点。
- 情况 2：新项小于链表中的最小项。新项应插入链表的开头。在这种情况下，我们需要调整链表的头指针，即 `first`。此外，`count` 加 1。
- 情况 3：该项应插入链表中的某个位置。
  - 3a：新项大于链表中的所有项。在这种情况下，新项应插入链表末尾。因此，`current` 的值为 `nullptr`，新项插入到 `trailCurrent` 之后。此外，`count` 加 1。
  - 3b：新项应插入链表中间的某个位置。在这种情况下，新项插入到 `trailCurrent` 和 `current` 之间。此外，`count` 加 1。

下面的语句可以完成情况 3a 和 3b。假设 `newNode` 指向新节点。

```cpp
trailCurrent->link = newNode;
newNode->link = current;
```

下面分别说明这些情况。

情况 1：链表为空。

请考虑图 16-30(a) 所示的链表。

![](img/b217c421655b51e7494cf3b89bb5432d_1172_0.png)

**图 16-30** 链表

假设我们希望将 27 插入链表。为完成此任务，我们创建一个节点，将 27 复制到该节点中，将该节点的链接设置为 `nullptr`，并使 `first` 指向该节点。图 16-30(b) 展示了生成的链表。注意，插入 27 后，`first` 和 `count` 的值都会发生变化。

情况 2：链表不为空，并且待插入项小于链表中的最小项。请考虑图 16-31 所示的链表。

![](img/b217c421655b51e7494cf3b89bb5432d_1172_1.png)

**图 16-31** 插入 10 前的非空链表

假设要插入 10。将 10 插入链表后，包含 `info` 值 10 的节点成为 `list` 的第一个节点。这要求我们改变 `first` 的值。此外，`count` 加 1。图 16-32 展示了生成的链表。

![](img/b217c421655b51e7494cf3b89bb5432d_1173_0.png)

**图 16-32** 插入 10 后的链表

**情况 3：** 链表不为空，并且待插入项大于链表中的第一个项。如前所述，这种情况包含两种情形。

**情况 3a：** 待插入项大于链表中的最大项，也就是说，它应插入链表末尾。请考虑图 16-33 所示的链表。

![](img/b217c421655b51e7494cf3b89bb5432d_1173_1.png)

**图 16-33** 插入 65 前的链表

假设我们希望将 65 插入链表。插入 65 后，生成的链表如图 16-34 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1173_2.png)

**图 16-34** 插入 65 后的链表

