

数据结构 307

245

| NULL | head |
| list1 | |

**图 9.16** 类构造函数的影响

list1 是 `SingleLinkedList` 类的对象。该框描绘了 list1 占据的内存块。从 `SingleLinkedList` 类的定义可以看出，该类的对象只有一个数据成员。该数据成员的名称为 `head`。类的构造函数会在对象创建时触发。它会将 `head` 指针的值设置为 `NULL`。

让我们来看下一个函数 `appendNode()`。

```cpp
/*
在列表末尾添加节点的函数。
*/
void SingleLinkedList::appendNode(int pVal)
{
    /*
    创建一个临时节点，我们将将其添加到
    列表中。
    SingleLinkedListNode 类的构造函数将
    将该节点的 next 指针置空。
    */
    SingleLinkedNode * temp = new SingleLinkedListNode();
    /*
    将传递给函数的参数值拷贝到
    新节点中。
    */
    temp->set(pVal);
    /* 如果 head 指针为 NULL（列表为空） ...
    */
    if(head == NULL)
    {
        /* 让 head 指针指向临时节点
        */
        head = temp;
    }
    /* 否则 ...
    else
    {
        /* 创建一个临时指针， ...
        */
        SingleLinkedNode * iter;
        /*
        让它指向第一个节点，遍历到
        列表的末尾并 ...
        */
        for(iter = head->getNext(); iter != NULL;
        iter = iter->getNext());
```

# 308 使用 C++ 的面向对象编程

```cpp
/*
... 让最后一个节点的 next 指针指向
临时节点。
*/
iter->setNext(temp);
```上述函数设计用于向链表列表中一个节点。让我们先了解我们希望该函数做什么。然后，通过研究该函数的定义（列表 9.12），我们将判断它是否真的执行了我们想要的操作。

# 列表 9.12 执行 appendNode() 函数

```cpp
/*
AppendNode01.cpp 的开始
*/
#include "SingleLinkedList.h"
void main() {
    /*
    创建一个列表
    */
    SingleLinkedList list1;
    /*
    在 list1 对象上调用 appendNode() 函数。
    */
    list1.appendNode(5287);
}
/*
AppendNode01.cpp 的结束
*/
```在上述程序的第一条语句之后，由于 `SingleLinkedList` 类的构造函数，对象内部的 `head` 指针的值将被设置为 `NULL`。这可以用图 9.17 来表示。

| 245 | |
| NULL | head |
| list1 | |

**图 9.17** 构造函数的影响

上面的框描绘了名为 list1 的对象（标记在框的底部）。由于它是 `SingleLinkedList` 类的对象，它只有一个数据成员——`head`（标记在框的右侧）。让我们来看在 list1 对象上调用 `appendNode()` 函数。

```cpp
list1.appendNode(5287);
```

如果函数定义得正确，那么在执行结束时，链表看起来应该像图 9.18 所示。

# 数据结构 309

| | 245 | 320 |
|---|---|---|
| head | 320 | 5287 | val |
| | list1 | NULL | next |

**图 9.18** appendNode() 函数的预期效果

让我们看看函数是否按预期执行。在函数执行之前，`head` 指针的值为 `NULL`。当函数开始执行时，参数 `pVal` 的值变为 5287，因为这是传递的值。之后，通过 `new` 运算符创建了一个临时节点，并让临时指针 `temp` 指向它（图 9.19）。

| | 695 | 320 |
|---|---|---|
| | 320 | 0 | val |
| temp | NULL | next |

**图 9.19** appendNode() 函数创建临时节点

下一语句是：
temp->set(pVal);

这将 `pVal` 的值（5287）拷贝到节点的 `val` 数据成员中。之后，`if` 语句将检查 `head` 指针的值是否为 `NULL`。此时测试结果为真，因为列表为空。`if` 块将执行，`temp` 的值将被拷贝到 `head`。这将导致 `head` 指针指向之前创建的临时节点。图 9.20 释了这一点。

| | 695 | 320 |
|---|---|---|
| | 320 | 5287 | val |
| temp | NULL | next |
| 245 | | |
| | 320 | |
| head | | |

**图 9.20** temp 指针的值拷贝到 head 指针

`else` 块不会执行，函数结束。由于 `temp` 是局部变量，它离开了作用域。

