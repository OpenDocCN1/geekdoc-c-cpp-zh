
## 反向构建链表

现在我们考虑反向构建链表的情况。对于前面给出的数据——2、15、8、24 和 34——链表如图 16-18 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1147_0.png)

图 16-18 反向构建后的链表

由于新节点总是插入到链表的开头，我们不需要知道链表的末尾，因此不需要指针 `last`。另外，将新节点插入到开头后，新节点就成为链表中的第一个节点。因此，我们需要更新指针 `first` 的值，使其正确指向链表中的第一个节点。于是可以看出，构建该链表只需要两个指针：一个指向链表，一个用于创建新节点。由于初始时链表为空，指针 `first` 必须初始化为 `nullptr`。用伪代码表示，算法如下：

1. 将 `first` 初始化为 `nullptr`。
2. 对于链表中的每一项，
   a. 创建新节点 `newNode`。
   b. 将该项存储到 `newNode` 中。
   c. 将 `newNode` 插入到 `first` 之前。
   d. 更新指针 `first` 的值。

下面的 C++ 函数反向构建链表，并返回所构建链表的指针：

```cpp
nodeType* buildListBackward()
{
    nodeType *first, *newNode;
    int num;

    cout << "Enter a list of integers ending with -999." << endl;
    cin >> num;

    first = nullptr;

    while (num != -999)
    {
        newNode = new nodeType; //create a node
        newNode->info = num;    //store the data in newNode
        newNode->link = first;  //put newNode at the beginning
                                //of the list
        first = newNode;        //updates the head pointer of
                                //the list, that is, first
        cin >> num;             //read the next number
    }

    return first;
} //end buildListBackward
```

## 链表作为 ADT

前面的章节介绍了链表的基本性质，以及如何构造和操作链表。由于链表是一种非常重要的数据结构，本节不讨论具体的链表（例如整数链表或字符串链表），而是将链表作为一种抽象数据类型（ADT）来讨论。本节使用模板给出链表的通用定义，该定义将在下一节以及本书后续内容中使用。本章末尾的编程示例也使用了链表的这个通用定义。

链表上的基本操作包括：

1. 初始化链表。
2. 判断链表是否为空。
3. 打印链表。
4. 求链表的长度。
5. 销毁链表。
6. 获取第一个节点中包含的 `info`。
7. 获取最后一个节点中包含的 `info`。
8. 在链表中查找给定项。
9. 在链表中插入一项。
10. 从链表中删除一项。
11. 复制该链表。

一般来说，链表有两种类型——有序链表，其元素按照某种标准排列；以及无序链表，其元素没有特定顺序。对于有序链表和无序链表，实现查找、插入和删除操作的算法略有不同。因此，我们将定义类 `linkedListType`，作为抽象类来实现链表上的基本操作。事实上，利用继承原则，我们将从类 `linkedListType` 派生出两个类——`unorderedLinkedList` 和 `orderedLinkedList`。

类 `unorderedLinkedList` 的对象会以无特定顺序排列链表元素，也就是说，这些链表可能未排序。另一方面，类 `orderedLinkedList` 的对象会按照某种比较标准排列元素，通常为小于或等于。也就是说，这些链表将按升序排列。

此外，在有序链表中插入或删除元素后，得到的链表仍将是有序的。

如果链表是无序的，我们可以在末尾或开头插入新项。此外，你可以按正向方式或反向方式构建这样的链表。函数 `buildListForward` 将新项插入到末尾，而函数 `buildListBackward` 将新项插入到开头。为了支持这两种操作，我们将编写两个函数：`insertFirst` 用于将新项插入到链表开头，`insertLast` 用于将新项插入到链表末尾。另外，为了使算法更高效，我们将在链表中使用两个指针：`first`，指向链表中的第一个节点；以及 `last`，指向链表中的最后一个节点。

## 链表节点的结构

回顾一下，链表的每个节点都必须存储数据以及链表中下一个节点的地址（链表最后一个节点除外）。因此，节点有两个成员变量。为了简化插入和删除等操作，我们将实现链表节点的类定义为 `struct`。`struct` `nodeType` 的定义如下：

```cpp
//Definition of the node

template <class Type>
struct nodeType
{
    Type info;
    nodeType<Type> *link;
};
```

> **注意**
> 用于实现链表节点的类被声明为 `struct`。本章末尾的编程练习 9 要求你重新定义用于实现链表节点的类，使 `class nodeType` 的成员变量为私有。

## `class linkedListType` 的成员变量

为了维护链表，我们使用两个指针：`first` 和 `last`。指针 `first` 指向链表中的第一个节点，`last` 指向链表中的最后一个节点。我们还记录链表中节点的数量。因此，`class linkedListType` 有三个成员变量，如下所示：

```cpp
protected:
    int count;              //variable to store the number of
                            //elements in the list

    nodeType<Type> *first;  //pointer to the first node
    nodeType<Type> *last;   //pointer to the last node
                            //of the list
```

## 链表迭代器

对链表执行的基本操作之一是处理链表中的每个节点。这需要从第一个节点开始遍历链表。此外，特定应用要求以非常特定的方式处理每个节点。实现这一点的一种常用技术是提供迭代器。那么什么是迭代器？迭代器是一种对象，它一次产生容器（例如链表）中的每个元素。迭代器上最常见的两个操作是 ++（递增运算符）和 *（解引用运算符）。递增运算符使迭代器前进到链表中的下一个节点，解引用运算符返回当前节点的信息。

请注意，迭代器是一个对象。因此，我们需要定义一个类，将其称为 `linkedListIterator`，用于为类 `linkedListType` 的对象创建迭代器。迭代器类将有一个成员变量，指向（当前）节点。

```cpp
template <class Type>
class linkedListIterator
{
public:
        linkedListIterator();
        //Default constructor
        //Postcondition: current = nullptr;

        linkedListIterator(nodeType<Type> *ptr);
        //Constructor with a parameter.
        //Postcondition: current = ptr;

        Type operator*();
        //Function to overload the dereferencing operator *.
        //Postcondition: Returns the info contained in the node.

        linkedListIterator<Type> operator++();
        //Overload the pre-increment operator.
        //Postcondition: The iterator is advanced to the next
        //              node

        bool operator==(const linkedListIterator<Type>& right) const;
        //Overload the equality operator.
        //Postcondition: Returns true if this iterator is equal to
        //              the iterator specified by right,
        //              otherwise it returns false.

        bool operator!=(const linkedListIterator<Type>& right) const;
        //Overload the not equal to operator.
        //Postcondition: Returns true if this iterator is not equal
        //              to the iterator specified by right,
        //              otherwise it returns false.

private:
        nodeType<Type> *current; //pointer to point to the current
                                  //node in the linked list
};
```
