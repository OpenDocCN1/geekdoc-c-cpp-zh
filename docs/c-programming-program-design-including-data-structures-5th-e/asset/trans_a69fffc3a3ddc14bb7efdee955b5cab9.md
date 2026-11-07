
而 orderedLinkedList 将提供 search、insertFirst、insertLast 和 deleteNode 这些函数的单独定义；由于这些函数会访问实例变量，为了提供对实例变量的直接访问，这些实例变量被声明为 protected。

linkedListType 类的定义包含一个用于重载赋值运算符的成员函数。对于包含指针数据成员的类，必须显式重载赋值运算符（见第 13 章和第 14 章）。出于同样的原因，该类的定义还包含一个复制构造函数。

注意，linkedListType 类的定义包含成员函数 copyList，它被声明为私有成员。这是因为该函数仅用于实现复制构造函数和重载赋值运算符。

接下来，我们编写 linkedListType 类的非抽象函数的定义。

如果 first 为 NULL，则链表为空。因此，实现该操作的函数 isEmptyList 的定义如下：

```cpp
template <class Type>
bool linkedListType<Type>::isEmptyList() const
{
    return (first == NULL);
}
```

### 默认构造函数

默认构造函数 linkedListType 非常直接。它只是将链表初始化为空状态。回想一下，当声明 linkedListType 类型的对象且未传递任何值时，默认构造函数会自动执行。

```cpp
template <class Type>
linkedListType<Type>::linkedListType() //default constructor
{
    first = NULL;
    last = NULL;
    count = 0;
}
```

### 销毁链表

函数 destroyList 释放每个节点占用的内存。我们从第一个节点开始遍历链表，并通过调用 delete 运算符释放内存。我们需要一个临时指针来释放内存。一旦整个链表被销毁，我们必须将指针 first 和 last 设置为 NULL，并将 count 设置为 0。

```cpp
template <class Type>
void linkedListType<Type>::destroyList()
{
    nodeType<Type> * temp;      //pointer to deallocate the memory
                                //occupied by the node

    while (first != NULL)    //while there are nodes in the list
    {
        temp = first;       //set temp to the current node
        first = first->link; //advance first to the next node
        delete temp;        //deallocate the memory occupied by temp
    }

    last = NULL; //initialize last to NULL; first has already
                 //been set to NULL by the while loop
    count = 0;
}
```

### 初始化链表

函数 initializeList 将链表初始化为空状态。注意，当链表对象被声明时，默认构造函数或复制构造函数已经初始化了链表。实际上，此操作会重新将链表初始化为空状态，因此它必须删除链表中的节点（如果有）。此任务可以通过使用 destroyList 操作完成，该操作还会将指针 first 和 last 重置为 NULL，并将 count 设置为 0。

```cpp
template <class Type>
void linkedListType<Type>::initializeList()
{
    destroyList(); //if the list has any nodes, delete them
}
```

### 打印链表

成员函数 print 打印每个节点中包含的数据。为此，我们必须从第一个节点开始遍历链表。由于指针 first 始终指向链表中的第一个节点，我们需要另一个指针来遍历链表。（如果我们使用 first 遍历链表，整个链表将会丢失。）

```cpp
template <class Type>
void linkedListType<Type>::print() const
{
    nodeType<Type> *current; //pointer to traverse the list

    current = first;         //set current so that it points to
                             //the first node
    while (current != NULL)  //while more data to print
    {
        cout << current->info << " ";
        current = current->link;
    }
}//end print
```

### 链表的长度

链表长度（即链表中有多少个节点）存储在变量 count 中。因此，此函数返回该变量的值：

```cpp
template <class Type>
int linkedListType<Type>::length() const
{
    return count;
}
```

### 获取第一个节点的数据

函数 front 返回第一个节点中包含的 info，其定义很直接：

```cpp
template <class Type>
Type linkedListType<Type>::front() const
{
    assert(first != NULL);

    return first->info; //return the info of the first node
}//end front
```

注意，如果链表为空，assert 语句会终止程序。因此，在调用此函数之前，请检查链表是否非空。

### 获取最后一个节点的数据

函数 back 返回最后一个节点中包含的 info，其定义很直接：

```cpp
template <class Type>
Type linkedListType<Type>::back() const
{
    assert(last != NULL);

    return last->info; //return the info of the last node
}//end back
```

注意，如果链表为空，assert 语句会终止程序。因此，在调用此函数之前，请检查链表是否非空。

### begin 与 end

函数 begin 返回指向链表中第一个节点的迭代器，函数 end 返回指向链表中最后一个节点之后位置的迭代器。它们的定义是：

```cpp
template <class Type>
linkedListIterator<Type> linkedListType<Type>::begin()
{
    linkedListIterator<Type> temp(first);

    return temp;
}
```

```cpp
template <class Type>
linkedListIterator<Type> linkedListType<Type>::end()
{
    linkedListIterator<Type> temp(NULL);

    return temp;
}
```

### 复制链表

函数 copyList 创建链表的完全相同副本。因此，我们从第一个节点开始遍历要复制的链表。对于原链表中的每个节点，我们：

- a. 创建一个节点，并将其称为 newNode。
- b. 将（原链表中）节点的 info 复制到 newNode 中。
- c. 将 newNode 插入到正在创建的链表的末尾。

函数 copyList 的定义是：

```cpp
template <class Type>
void linkedListType<Type>::copyList
                    (const linkedListType<Type>& otherList)
{
    nodeType<Type> *newNode;  //pointer to create a node
    nodeType<Type> *current;   //pointer to traverse the list

    if (first != NULL) //if the list is nonempty, make it empty
        destroyList();

    if (otherList.first == NULL) //otherList is empty
    {
        first = NULL;
        last = NULL;
        count = 0;
    }
    else
    {
        current = otherList.first; //current points to the
                                   //list to be copied
        count = otherList.count;

        //copy the first node
        first = new nodeType<Type>;  //create the node
        first->info = current->info; //copy the info
        first->link = NULL;          //set the link field of
                                     //the node to NULL
        last = first;                //make last point to the
                                     //first node
        current = current->link;     //make current point to
                                     //the next node

        //copy the remaining list
        while (current != NULL)
        {
            newNode = new nodeType<Type>;   //create a node
            newNode->info = current->info;  //copy the info
            newNode->link = NULL;           //set the link of
                                            //newNode to NULL

            last->link = newNode;           //attach newNode after last
            last = newNode;                 //make last point to
                                            //the actual last node

            current = current->link;        //make current point
                                            //to the next node
        }//end while
    }//end else
}//end copyList
```

### 析构函数

当类对象超出作用域时，析构函数释放链表节点占用的内存。由于内存是动态分配的，重置指针 `first` 和 `last` 并不会释放链表中节点占用的内存。我们必须从第一个节点开始遍历链表，并删除链表中的每个节点。可以通过调用函数 `destroyList` 来销毁链表。因此，析构函数的定义是：

```cpp
template <class Type>
linkedListType<Type>::~linkedListType() //destructor
{
    destroyList();
}
```

### 复制构造函数

因为类 `linkedListType` 包含指针数据成员，所以该类的定义包含复制构造函数。回想一下，如果形参是值参数，复制构造函数会为该形参提供其自己的数据副本。当使用另一个对象声明并初始化一个对象时，复制构造函数也会执行。（更多信息，请参见第 13 章。）

复制构造函数创建链表的完全相同副本。这可以通过调用函数 `copyList` 来完成。因为函数 `copyList` 通过检查 `first` 的值来检查原链表是否为空，所以在调用函数 `copyList` 之前，我们必须先将指针 `first` 初始化为 `NULL`。

复制构造函数的定义是：

```cpp
template <class Type>
linkedListType<Type>::linkedListType
    (const linkedListType<Type>& otherList)
{
    first = NULL;
    copyList(otherList);
}//end copy constructor
```

