
下面的程序测试有序链表上的各种操作：

```cpp
//Program to test the various operations on an ordered linked list
#include <iostream>
#include "OrderedLinkedList.h"

using namespace std;

int main()
{
    orderedLinkedList<int> list1, list2;        //Line 1
    int num;                                     //Line 2

    cout << "Line 3: Enter numbers ending "
         << "with -999." << endl;              //Line 3
    cin >> num;                                  //Line 4
    while (num != -999)                          //Line 5
    {
        list1.insert(num);                       //Line 6
        cin >> num;                              //Line 7
    }

    cout << endl;                                //Line 8

    cout << "Line 9: list1: ";                  //Line 9
    list1.print();                               //Line 10
    cout << endl;                                //Line 11

    list2 = list1; //test the assignment operator  //Line 12

    cout << "Line 13: list2: ";                 //Line 13
    list2.print();                               //Line 14
    cout << endl;                                //Line 15

    cout << "Line 16: Enter the number to be "
         << "deleted: ";                        //Line 16
    cin >> num;                                  //Line 17
    cout << endl;                                //Line 18

    list2.deleteNode(num);                       //Line 19

    cout << "Line 20: After deleting "
         << num << ", list2: " << endl;         //Line 20
    list2.print();                               //Line 21
    cout << endl;                                //Line 22

    return 0;
}
```

示例运行：在此示例运行中，用户输入以阴影显示。

```text
Line 3: Enter numbers ending with -999.
23 65 34 72 12 82 36 55 29 -999
Line 9: list1: 12 23 29 34 36 55 65 72 82
Line 13: list2: 12 23 29 34 36 55 65 72 82
Line 16: Enter the number to be deleted: 34
Line 20: After deleting 34, list2:
12 23 29 36 55 65 72 82
```

前面的输出不言自明。具体细节留作练习。

> **注意**
>
> 请注意，函数 `insert` 不会检查要插入的项是否已经在链表中，也就是说，它不检查重复项。本章末尾的编程练习 8 要求你修改函数 `insert` 的定义，使其在插入项之前检查该项是否已经在链表中。如果要插入的项已经在链表中，该函数会输出相应的错误消息。换句话说，不允许重复。

## 逆序打印链表（重新审视递归）

有序链表（如前所述构造）的节点按升序排列。然而，某些应用可能要求按降序打印数据，这意味着我们必须反向打印链表。现在我们讨论函数 `reversePrint`。给定指向链表的指针，该函数按逆序打印链表中的元素。

考虑图 16-37 中所示的链表。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1167_0.png)

**图 16-37** 链表

对于图 16-37 中的链表，输出应采用以下形式：

```text
20 15 10 5
```

由于链接只有一个方向，我们无法从最后一个节点开始向后遍历链表。让我们看看如何有效地利用递归来逆序打印链表。

让我们从递归的角度来思考。在打印完链表的其余部分（即第一个节点的尾部）之前，我们无法打印第一个节点的信息。类似地，在打印完第二个节点的尾部之前，我们无法打印第二个节点的信息，依此类推。每次考虑某个节点的尾部时，我们都将链表的大小减 1。最终，链表的大小会减小到零，此时递归将停止。我们先用伪代码编写该算法。（假设 current 是指向链表的指针。）

```cpp
if (current != nullptr)
{
    reversePrint(current->link);    //print the tail
    cout << current->info << endl;  //print the node
}
```

这里，我们看不到基本情况；它是隐藏的。只有当指向链表的指针不是 nullptr 时，才会打印链表。此外，在 if 语句体中，递归调用作用于链表的尾部。由于最终链表的尾部将为空，下一次调用中的 if 语句将失败，递归将停止。另外，请注意，语句（例如打印节点信息）出现在递归调用之后；因此，当控制权返回调用函数时，我们必须执行剩余的语句。回想一下，函数只有在最后一条语句执行完之后才会退出。（这里的“最后一条语句”不是指物理上的最后一条语句，而是指逻辑上的最后一条语句。）

让我们用 C++ 编写前面的函数，然后将其应用于链表。

```cpp
template <class Type>
void linkedListType<Type>::reversePrint
                (nodeType<Type> *current) const
{
    if (current != nullptr)
    {
        reversePrint(current->link);    //print the tail
        cout << current->info << " ";   //print the node
    }
}
```

考虑以下语句：

```cpp
reversePrint(first);
```

其中 `first` 是 `nodeType<Type>` 类型的指针。

让我们针对图 16-37 中所示的链表，跟踪这条语句（它是一个函数调用）的执行过程。因为形参是值参数，所以实参的值被传递给形参。参见图 16-38。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1169_0.png)

**图 16-38** 语句 `reversePrint(first);` 的执行

### printListReverse

既然我们已经编写了函数 `reversePrint`，现在可以编写函数 `printListReverse` 的定义了。其定义如下：

```cpp
template <class Type>
void linkedListType<Type>::printListReverse() const
{
    reversePrint(first);
    cout << endl;
}
```

## 双向链表

双向链表是一种链表，其中每个节点都有一个 next 指针和一个 back 指针。换句话说，每个节点都包含下一个节点的地址（最后一个节点除外），并且每个节点都包含前一个节点的地址（第一个节点除外）（参见图 16-39）。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1170_0.png)

**图 16-39** 双向链表

双向链表可以沿任一方向遍历。也就是说，我们可以从第一个节点开始遍历链表；或者，如果给定指向最后一个节点的指针，我们也可以从最后一个节点开始遍历链表。

和之前一样，双向链表的典型操作包括：

- 1. 初始化链表。
- 2. 销毁链表。
- 3. 判断链表是否为空。
- 4. 在链表中搜索给定项。
- 5. 获取链表的第一个元素。
- 6. 获取链表的最后一个元素。
- 7. 在链表中插入一项。
- 8. 从链表中删除一项。
- 9. 求链表的长度。
- 10. 打印链表。
- 11. 复制双向链表。

接下来，我们描述有序双向链表的这些操作。下面的类将双向链表定义为 ADT：

```cpp
//Definition of the node
template <class Type>
struct nodeType
{
    Type info;
    nodeType<Type> *next;
    nodeType<Type> *back;
};
```

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
       //Postcondition: first = nullptr; last = nullptr; count = 0;

    bool isEmptyList() const;
       //Function to determine whether the list is empty.
       //Postcondition: Returns true if the list is empty,
       //               otherwise returns false.

    void destroy();
       //Function to delete all the nodes from the list.
       //Postcondition: first = nullptr; last = nullptr; count = 0;

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
};
```
