

创建一个新节点，以便将其插入列表中。我们创建了七个公有成员函数，包括构造函数和析构函数。公有成员函数可以在列表中插入节点、从列表中删除节点、获取特定位置节点的数据值、打印所有节点的数据内容，以及返回列表中的节点数。我们的列表不是有序列表，因为使用单链表实现有序列表并不常见；通常会使用二叉搜索树等其他结构来实现这一目的。尽管 STL 中的列表结构使用了特定操作，例如在列表的前端和后端插入、删除以及获取元素中的数据，但在现阶段，我们只使用上述基本操作。程序 18.1 包含接口文件。

## 程序 18.1 — 文件 list.h

```cpp
/***************************************************************
 * The interface file for a List class as a singly linked list  *
 ***************************************************************/
#ifndef LIST_H
#define LIST_H
#include <iostream>
#include <cassert>
using namespace std;

// Definition of the Node as a struct
template <typename T>
struct Node
{
    T data;
    Node<T>* next;
};

// Definition of the class List
template <typename T>
class List
{
private:
    Node<T>* begin;
    int count;
    Node<T>* makeNode(const T& value);

public:
    List();
    ~List();
    void insert(int pos, const T& value);
    void erase(int pos);
    T& get(int pos) const;
    void print() const;
    int size() const;
};
#endif
```

## 实现文件

程序 18.2 是实现文件。

## 程序 18.2 — 文件 list.cpp

```cpp
/****************************************************************
 * The implementation file for a List class                    *
 ****************************************************************/
#ifndef LIST_CPP
#define LIST_CPP
#include "List.h"

// Constructor
template <typename T>
List<T>::List()
    : begin(0), count(0)
{
}

// Destructor
template <typename T>
List<T>::~List()
{
    Node<T>* del = begin;
    while (begin)
    {
        begin = begin->next;
        delete del;
        del = begin;
    }
}

// Insert member function
template <typename T>
void List<T>::insert(int pos, const T& value)
{
    if (pos < 0 || pos > count)
    {
        cout << "Error! The position is out of range." << endl;
        return;
    }

    Node<T>* add = makeNode(value);
    if (pos == 0)
    {
        add->next = begin;
        begin = add;
    }
    else
    {
        Node<T>* cur = begin;
        for (int i = 1; i < pos; i++)
        {
            cur = cur->next;
        }
        add->next = cur->next;
        cur->next = add;
    }
    count++;
}

// Erase member function
template <typename T>
void List<T>::erase(int pos)
{
    if (pos < 0 || pos > count - 1)
    {
        cout << "Error! The position is out of range." << endl;
        return;
    }

    if (pos == 0)
    {
        Node<T>* del = begin;
        begin = begin->next;
        delete del;
    }
    else
    {
        Node<T>* cur = begin;
        for (int i = 0; i < pos - 1; i++)
        {
            cur = cur->next;
        }
        Node<T>* del = cur->next;
        cur->next = cur->next->next;
        delete del;
    }
    count--;
}

// Get member function
template <typename T>
T& List<T>::get(int pos) const
{
    if (pos < 0 || pos > count - 1)
    {
        cout << "Error! Position out of range";
        assert(false);
    }
    else if (pos == 0)
    {
        return begin->data;
    }
    else
    {
        Node<T>* cur = begin;
        for (int i = 0; i < pos; i++)
        {
            cur = cur->next;
        }
        return cur->data;
    }
}

// Print member function
template <typename T>
void List<T>::print() const
{
    if (count == 0)
    {
        cout << "List is empty!" << endl;
        return;
    }

    Node<T>* cur = begin;
    while (cur != 0)
    {
        cout << cur->data << endl;
        cur = cur->next;
    }
}

// Size member function
template <typename T>
int List<T>::size() const
{
    return count;
}

// MakeNode member function (private)
template <typename T>
Node<T>* List<T>::makeNode(const T& value)
{
    Node<T>* temp = new Node<T>;
    temp->data = value;
    temp->next = 0;
    return temp;
}
#endif
```

**应用程序文件**

我们使用一个小型应用程序文件来测试单链表。我们创建一个姓名列表，并测试实现文件中定义的操作。请注意，我们使用*包含过程*而不是*单独编译过程*，因为我们希望不支持模板对象*单独编译过程*的编译器也能编译该文件。程序 18.3 展示了这一概念。

## 程序 18.3 — 文件 application.cpp

```cpp
/***************************************************************
 * The application file to test some operations in our list     *
 ***************************************************************/
#include "list.cpp"
#include <string>

int main()
{
    // Instantiation of a list object
    List<string> list;

    // Inserting six nodes in the list
    list.insert(0, "Michael");
    list.insert(1, "Jane");
    list.insert(2, "Sophie");
    list.insert(3, "Thomas");
    list.insert(4, "Rose");
    list.insert(5, "Richard");

    // Printing the values of nodes
    cout << "Printing the list" << endl;
    list.print();

    // Printing the values of three nodes
    cout << "Getting data in some nodes" << endl;
    cout << list.get(0) << endl;
    cout << list.get(3) << endl;
    cout << list.get(5) << endl;

    // Erasing three nodes from the list
    cout << "Erasing some nodes and printing after erasures" << endl;
    list.erase(0);
    list.erase(3);
    list.print();

    // Printing the list after erasures
    cout << "Checking the list size" << endl;
    cout << "List size: " << list.size();
    return 0;
}
```

```text
Run:
Printing the list
Michael
Jane
Sophie
Thomas
Rose
Richard
Getting data in some nodes
Michael
Thomas
Richard
Erasing some nodes and printing after erasures
Jane
Sophie
Thomas
Richard
Checking the list size
List size: 4
```

## 操作说明

大多数操作都很直观。其他操作则需要解释列表是如何被修改的。

**构造函数** 我们使用默认构造函数，将*count*成员设置为 0，并将空指针（0）存储在*begin*成员中。

**析构函数** 析构函数逐个删除所有节点，并释放堆内存。图 18.5 展示了包含两个节点的链表。

**插入** 插入操作在指定位置执行。我们有三种情况：在前端插入、在中间插入，或在末尾插入。在创建节点后，可以使用两个操作完成开头位置的插入，如图 18.6 所示。

中间位置的插入更加复杂，如图 18.7 所示。我们必须使用一个*cur*指针，并将其移动到插入位置之前的节点。然后就可以插入该节点。

![](img/d68f6199646ca63591a6d8419e0ed4ba_841_0.png)

末尾插入是中间插入的一种特殊情况，此时应将*cur*指针移动到最后一个节点。新节点插入最后一个节点之后。这里将其留作练习。

**删除** 删除操作针对特定节点执行。如果列表不为空，则有三种情况：删除第一个节点、删除中间节点，或删除最后一个节点。删除第一个节点非常简单，可以按照图 18.8 所示的方式完成。

删除中间节点则更加复杂。我们必须使用一个*cur*指针，使其指向待删除节点之前的节点。然后可以使用另一个指针*del*指向要删除的节点。接着即可删除该节点。图 18.9 展示了删除中间节点时涉及的操作。

删除末尾节点涉及类似的过程，但必须将*cur*指针移动到最后一个节点之前的节点。

![](img/d68f6199646ca63591a6d8419e0ed4ba_841_1.png)

