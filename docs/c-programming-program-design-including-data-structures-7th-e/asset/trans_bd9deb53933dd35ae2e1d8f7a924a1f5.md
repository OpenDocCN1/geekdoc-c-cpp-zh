

```cpp
template <class Type>
int linkedListType<Type>::length() const
{
    return count;
}
```

## 获取第一个节点的数据

函数 front 返回第一个节点中包含的信息，其定义很直接：

```cpp
template <class Type>
Type linkedListType<Type>::front() const
{
    assert(first != nullptr);

    return first->info; // return the info of the first node
}//end function
```

注意，如果链表为空，assert 语句会终止程序。因此，在调用此函数之前，请检查链表是否非空。

## 获取最后一个节点的数据

函数 back 返回最后一个节点中包含的信息，其定义很直接：

```cpp
template <class Type>
Type linkedListType<Type>::back() const
{
    assert(last != nullptr);

    return last->info; // return the info of the last node
}//end function
```

注意，如果链表为空，assert 语句会终止程序。因此，在调用此函数之前，请检查链表是否非空。

## begin 与 end

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
    linkedListIterator<Type> temp(nullptr);

    return temp;
}
```

## 复制链表

函数 copyList 制作链表的完全相同的副本。因此，我们从第一个节点开始遍历要复制的链表。对于原链表中的每个节点，我们：

- a. 创建一个节点，并将其称为 newNode。
- b. 将该节点（原链表中）的信息复制到 newNode 中。
- c. 将 newNode 插入到正在创建的链表的末尾。

函数 copyList 的定义是：

```cpp
template <class Type>
void linkedListType<Type>::copyList
                         (const linkedListType<Type>& otherList)
{
    nodeType<Type> *newNode;  //pointer to create a node
    nodeType<Type> *current;  //pointer to traverse the list

    if (first != nullptr)  //if the list is nonempty, make it empty
        destroyList();

    if (otherList.first == nullptr)  //otherList is empty
    {
        first = nullptr;
        last = nullptr;
        count = 0;
    }
    else
    {
        current = otherList.first;  //current points to the
                                    //list to be copied
        count = otherList.count;

                    //copy the first node
        first = new nodeType<Type>;  //create the node
        first->info = current->info; //copy the info
        first->link = nullptr;       //set the link field of
                                     //the node to nullptr
        last = first;                //make last point to the
                                     //first node
        current = current->link;     //make current point to
                                     //the next node

        // copy the remaining list
        while (current != nullptr)
        {
            newNode = new nodeType<Type>;  //create a node
            newNode->info = current->info;  //copy the info
            newNode->link = nullptr;        //set the link of
                                            //newNode to nullptr
            last->link = newNode;           //attach newNode after last
            last = newNode;                 //make last point to
                                            //the actual last node
            current = current->link;        //make current point
                                            //to the next node
        }//end while
    }//end else
}//end copyList
```

## 析构函数

当类对象超出作用域时，析构函数释放链表节点占用的内存。由于内存是动态分配的，仅重置指针 first 和 last 并不会释放链表中节点占用的内存。我们必须从第一个节点开始遍历链表，并删除链表中的每个节点。可以通过调用函数 destroyList 来销毁链表。因此，析构函数的定义是：

```cpp
template <class Type>
linkedListType<Type>::~linkedListType() //destructor
{
    destroyList();
}
```

## 复制构造函数

因为类 linkedListType 包含指针数据成员，所以该类的定义包含复制构造函数。回想一下，如果形参是值参数，复制构造函数会为该形参提供其自己的数据副本。当使用另一个对象声明并初始化一个对象时，复制构造函数也会执行。（更多信息请参见第 12 章。）

复制构造函数制作链表的完全相同的副本。这可以通过调用函数 copyList 来完成。因为函数 copyList 通过检查 first 的值来检查原链表是否为空，所以在调用函数 copyList 之前，我们必须先将指针 first 初始化为 nullptr。

复制构造函数的定义是：

```cpp
template <class Type>
linkedListType<Type>::linkedListType
                    (const linkedListType<Type>& otherList)
{
    first = nullptr;
    copyList(otherList);
}//end copy constructor
```

## 重载赋值运算符

为类 linkedListType 重载赋值运算符的函数的定义与复制构造函数的定义类似。为完整起见，我们给出其定义。

```cpp
//overload the assignment operator
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

如前一节所述，我们从抽象类 linkedListType 派生类 unorderedLinkedList，并实现操作 search、insertFirst、insertLast 和 deleteNode。

以下类将无序链表定义为 ADT：

```cpp
template <class Type>
class unorderedLinkedList: public linkedListType<Type>
{
public:
    bool search(const Type& searchItem) const;
        //Function to determine whether searchItem is in the list.
        //Postcondition: Returns true if searchItem is in the
        //               list, otherwise the value false is
        //               returned.

    void insertFirst(const Type& newItem);
        //Function to insert newItem at the beginning of the list.
        //Postcondition: first points to the new list, newItem is
        //               inserted at the beginning of the list,
        //               last points to the last node in the
        //               list, and count is incremented by 1.

    void insertLast(const Type& newItem);
        //Function to insert newItem at the end of the list.
        //Postcondition: first points to the new list, newItem
        //               is inserted at the end of the list,
        //               last points to the last node in the
        //               list, and count is incremented by 1.

    void deleteNode(const Type& deleteItem);
        //Function to delete deleteItem from the list.
        //Postcondition: If found, the node containing
        //                 deleteItem is deleted from the list.
        //                 first points to the first node, last
        //                 points to the last node of the updated
        //                 list, and count is decremented by 1.
};
```

图 16-21 显示了类 unorderedLinkedList 的 UML 类图以及继承层次结构。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1148_0.png)

**图 16-21**  类 unorderedLinkedList 的 UML 类图及继承层次结构

接下来，我们给出类 unorderedLinkedList 的成员函数的定义。

### 搜索链表

成员函数 search 在链表中搜索给定项。如果找到该项，则返回 `true`；否则返回 `false`。由于链表不是随机访问数据结构，我们必须从第一个节点开始按顺序搜索链表。

此函数有以下步骤：

- 1. 将搜索项与链表中的当前节点进行比较。如果当前节点的信息与搜索项相同，则停止搜索；否则，将下一个节点设为当前节点。
- 2. 重复步骤 1，直到找到该项，或者链表中没有更多数据可与搜索项比较。

```cpp
template <class Type>
bool unorderedLinkedList<Type>::
                 search(const Type& searchItem) const
{
    nodeType<Type> *current; //pointer to traverse the list
    bool found = false;
    current = first; //set current to point to the first
                     //node in the list

