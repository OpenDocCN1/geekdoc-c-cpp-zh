
## 链表迭代器

对链表执行的基本操作之一是处理链表中的每个节点。这需要从第一个节点开始遍历链表。此外，特定应用要求以非常特定的方式处理每个节点。实现这一点的一种常用技术是提供迭代器。那么什么是迭代器？迭代器是一种对象，它一次一个元素地生成容器（例如链表）的每个元素。迭代器上最常见的两个操作是 ++（自增运算符）和 *（解引用运算符）。自增运算符使迭代器前进到链表中的下一个节点，解引用运算符返回当前节点的 info 信息。

注意，迭代器是一个对象。因此，我们需要定义一个类，将其称为 linkedListIterator，以操作 linkedListType 类的对象。迭代器类将有一个成员变量指向（当前）节点。

```cpp
template <class Type>
class linkedListIterator
{
public:
    linkedListIterator();
        //Default constructor.
        //Postcondition: current == NULL;

    linkedListIterator(nodeType<Type> *ptr);
        //Constructor with a parameter.
        //Postcondition: current = ptr

    Type operator*();
        //Function to overload the dereferencing operator *.
        //Postcondition: Returns the info contained in the node.

    linkedListIterator<Type> operator++();
        //Overload the pre-increment operator.
        //Postcondition: The iterator is advanced to the next
        //             node.

    bool operator==(const linkedListIterator<Type>& right) const;
        //Overload the equality operator.
        //Postcondition: Returns true if this iterator is equal to
        //             the iterator specified by right,
        //             otherwise it returns false.

    bool operator!=(const linkedListIterator<Type>& right) const;
        //Overload the not equal to operator.
        //Postcondition: Returns true if this iterator is not equal
        //             to the iterator specified by right,
        //             otherwise it returns false.

private:
    nodeType<Type> *current; //pointer to point to the current
                             //node in the linked list
};
```

图 16-19 展示了类 `linkedListIterator` 的 UML 类图。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1091_0.png)

**图 16-19** 类 `linkedListIterator` 的 UML 类图

类 `linkedListIterator` 的函数定义如下：

```cpp
template <class Type>
linkedListIterator<Type>::linkedListIterator()
{
    current = NULL;
}

template <class Type>
linkedListIterator<Type>::linkedListIterator(nodeType<Type> *ptr)
{
    current = ptr;
}

template <class Type>
Type linkedListIterator<Type>::operator*()
{
    return current->info;
}

template <class Type>
linkedListIterator<Type> linkedListIterator<Type>::operator++()
{
    current = current->link;

    return *this;
}

template <class Type>
bool linkedListIterator<Type>::operator==(const linkedListIterator<Type>& right) const
{
    return (current == right.current);
}

template <class Type>
bool linkedListIterator<Type>::operator!=(const linkedListIterator<Type>& right) const
{
    return (current != right.current);
}
```

现在我们已经定义了实现链表节点和链表迭代器的类，接下来我们描述类 linkedListType，以实现链表的基本属性。

以下抽象类定义了链表作为 ADT 的基本属性：

```cpp
template <class Type>
class linkedListType
{
public:
    const linkedListType<Type>& operator=
                          (const linkedListType<Type>&);
    //Overload the assignment operator

    void initializeList();
    //Initialize the list to an empty state.
    //Postcondition: first = NULL, last = NULL, count = 0;

    bool isEmptyList() const;
    //Function to determine whether the list is empty.
    //Postcondition: Returns true if the list is empty,
    //              otherwise it returns false.

    void print() const;
    //Function to output the data contained in each node.
    //Postcondition: none

    int length() const;
    //Function to return the number of nodes in the list.
    //Postcondition: The value of count is returned.

    void destroyList();
    //Function to delete all the nodes from the list.
    //Postcondition: first = NULL, last = NULL, count = 0;

    Type front() const;
    //Function to return the first element of the list.
    //Precondition: The list must exist and must not be
    //             empty.
    //Postcondition: If the list is empty, the program
    //               terminates; otherwise, the first
    //               element of the list is returned.

    Type back() const;
    //Function to return the last element of the list.
    //Precondition: The list must exist and must not be
    //             empty.
    //Postcondition: If the list is empty, the program
    //               terminates; otherwise, the last
    //               element of the list is returned.

    virtual bool search(const Type& searchItem) const = 0;
    //Function to determine whether searchItem is in the list.
    //Postcondition: Returns true if searchItem is in the
    //              list, otherwise the value false is
    //              returned.

    virtual void insertFirst(const Type& newItem) = 0;
    //Function to insert newItem at the beginning of the list.
    //Postcondition: first points to the new item if newItem is
    //              inserted at the beginning of the list,
    //              last points at the last node in the list,
    //              and count is incremented by 1.

    virtual void insertLast(const Type& newItem) = 0;
    //Function to insert newItem at the end of the list.
    //Postcondition: first points to the newItem, if newItem
    //              is inserted at the end of the list,
    //              last points to the last node in the list,
    //              and count is incremented by 1.

    virtual void deleteItem(const Type& deleteItem) = 0;
    //Function to delete deleteItem from the list.
    //Postcondition: If found, the node containing
    //              deleteItem is deleted from the list.
    //              first points to the first node, last
    //              points to the last node of the updated
    //              list, and count is decremented by 1.

    linkedListIterator<Type> begin();
    //Function to return an iterator at the beginning of the
    //linked list.
    //Postcondition: Returns an iterator such that current is
    //              set to first.

    linkedListIterator<Type> end();
    //Function to return an iterator one element past the
    //last element of the linked list.
    //Postcondition: Returns an iterator such that current is
    //              set to NULL.

    linkedListType();
    //default constructor
    //Initializes the list to an empty state.
    //Postcondition: first = NULL, last = NULL, count = 0;

    linkedListType(const linkedListType<Type>& otherList);
    //copy constructor

    ~linkedListType();
    //destructor
    //Deletes all the nodes from the list.
    //Postcondition: The list object is destroyed.

protected:
    int count;       //variable to store the number of
                     //elements in the list
    nodeType<Type> *first; //pointer to the first node of the list
    nodeType<Type> *last;  //pointer to the last node of the list

private:
    void copyList(const linkedListType<Type>& otherList);
    //Function to make a copy of otherList.
    //Postcondition: A copy of otherList is created and
    //               assigned to this list.
};
```

图 16-20 展示了类 linkedListType 的 UML 类图。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1094_0.png)

**图 16-20** 类 linkedListType 的 UML 类图

注意，通常，在 UML 图中，抽象类和抽象函数的名称以斜体显示。

类 linkedListType 的实例变量 first 和 last（如前所定义）是 protected，因为如前所述，我们将从类 linkedListType 派生类 unorderedLinkedList 和 orderedLinkedList。因为每个类 unorderedLinkedList
