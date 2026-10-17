
```cpp
/*
SingleLinkedListNode.h。
*/
#ifndef SINGLE_LINKED_LIST_NODE_H
#define SINGLE_LINKED_LIST_NODE_H
/*
节点类。
该类的每个实例都将是单链表中的一个节点。
*/
class SingleLinkedListNode{
    private:
    /*
    节点的数据部分。
    */
    int val;
    /*
    next 指针存在于每个节点中，并指向下一个节点（或为 NULL）
    */
    SingleLinkedListNode * next;
public:
    /*
    节点类的构造函数。它默认会将 next 指针置空。
    */
    SingleLinkedListNode();
    /*
    此函数设置数据部分的值。
    */
    void setValue(int);
    /*
    此函数返回数据部分。
    */
    int getVal();
    /*
    此函数设置 next 指针的值。
    */
    void setNext(SingleLinkedListNode *);
    /*
    此函数返回 next 指针的值。
    */
    SingleLinkedListNode * getNext();
    /*
类的析构函数。
*/
```

# 288 C++ 面向对象编程

```cpp
~SingleLinkedListNode();
};
#endif
```

> /*
SingleLinkedListNode.h 结束。
*/

头文件开头是一个注释，指定了头文件的名称并宣布了文件的开始。其之后是预处理指令，用于防止在其他源代码中多次包含该头文件（你一定在 C 语言课程中学习过这个）。接下来是节点类的声明。头文件的最后一行包含了预处理块的声明以及标记头文件结束的最后一行。

`SingleLinkedList` 类的每个对象都将是链表中的一个节点。该类有一个整数数据成员 `val`，它应该包含节点的值。在这个示例中，每个节点都有这个整数类型变量作为数据成员。然而，数据部分可以是任何类型，包括类对象。

节点类的另一个成员是一个指针。从它的定义可以很明显看出，`next` 应该指向另一个节点，即相同类的另一个对象。在我们的程序中，它要么被指向链表中的下一个节点，要么被赋值为 `NULL`（表示当前节点是链表的末尾）。

让我们看看实现文件（列表 9.2），它包含了节点类成员函数的定义。清晰地理解这些函数非常重要，因为它们是单链表类函数的构建模块。

## 9.2 链表节点类的实现文件

```cpp
/*
SingleLinkedList.cpp 开始。
*/
#include "SingleLinkedListNode.h"
```

```cpp
/*
节点类的构造函数。它默认会将
next 指针置空。
*/
```

```cpp
SingleLinkedListNode::SingleLinkedListNode()
{
    /* 将数据部分设为零。 */
    val = 0;
    /* 将 next 指针设为 NULL。 */
    next = NULL;
}
```

```cpp
/*
此函数设置数据部分的值。
*/
```

```cpp
void SingleLinkedList::setVal(int pVal)
{
    /*
    将数据部分的值设置为
    传递参数的值。
    */
    val = pVal;
}
```

```cpp
/*
 * 此函数返回数据部分。
 */
int SingleLinkedList::getVal()
```

（注：原文提供的文本在后半部分存在重复和逻辑混乱，上述翻译已根据您提供的文本内容进行了对应处理。）

# 292 使用 C++ 进行面向对象编程

## 列表 9.5 执行 getVal() 函数

```cpp
/*
GetVal.cpp 的开始
*/
#include <iostream>
#include "SingleLinkedListNode.h"

void main()
{
    SingleLinkedListNode * temp = new SingleLinkedListNode();
    temp -> setVal(10);
    int x = temp -> getVal();
    cout << x << endl;
}
/*
GetVal.cpp 的结束
*/
```

# 输出

10

接下来是 `setNext()` 函数。

```cpp
/*
该函数设置下一个指针（next）的值。
*/
void SingleLinkedListNode::setNext(SingleLinkedListNode * pNext)
{
    /*
    将下一个指针的值设置为传入
    参数的值。
    */
    next = pNext;
}
```

该函数将传递的参数值赋值给它的 `next` 数据成员变量。在学习链表类时，你会发现传递给节点类该函数的数值将是列表中下一个节点的地址。从参数 `pNext` 的定义中也可以显而易见地看出这一点。让我们通过实际程序（列表 9.6）和说明其语句效果的图表来理解这些影响。

## 列表 9.6 执行 setNext() 函数

```cpp
/*
SetNext.cpp 的开始
*/
#include <iostream>
#include "SingleLinkedListNode.h"

void main()
{
    /*
    创建一个新节点并将其地址赋值给
    指针。
    */
    SingleLinkedListNode * temp = new SingleLinkedListNode();

/*
 设置新节点中 val 数据成员的值。
 */
temp -> setVal(10);
/*
 创建另一个新节点并将其地址赋值给另一个指针。
 */
SingleLinkedListNode * temp1 = new
SingleLinkedListNode();
/*
 设置新节点中 val 数据成员的值。
 */
temp1 -> setVal(20);
/*
 让现有节点的 next 指针指向
新创建的节点。
 */
temp -> setNext(temp1);

} // SetNext.cpp 的结束
```

让我们逐条查看这些语句。

```cpp
/*
 创建一个新节点并将其地址赋值给指针。
 */
SingleLinkedListNode * temp = new SingleLinkedListNode();
```

这条语句将创建一个新节点并让指针 `temp` 指向它。图 9.8 以图示表示了结果。

![](img/5bfa77b13fdaa376725789bb8c00ee79_306_0.png)

图 9.8 创建临时节点

右侧的框表示节点类新创建的对象。它的数据成员——`val` 和 `next`——已经被标记。可以看出，它们的值分别被设置为 0 和 `NULL`（通过构造函数）。它们在框中被一条线隔开。让我们假设该节点的地址是 108。`temp` 指针的值将是 108。

```cpp
/*
 设置新节点中 val 数据成员的值。
 */
temp -> setVal(10);
```

这条语句将把 10 赋值给 `val` 数据成员。图 9.9 以图示表示了结果。

# 294 使用 C++ 进行面向对象编程

| | |

|---|---|

| 108 | val |

| temp | NULL next |

图 9.9 `setVal()` 函数的效果

```cpp
/*
创建另一个新节点并将其地址赋值给
另一个指针。
*/
SingleLinkedListNode* temp1 = new SingleLinkedListNode();
```

这条语句将创建一个新节点，且指针 `temp1` 指向它。图 9.10 以图示表示了结果。

| | |

|---|---|

| 320 | val |

| temp1 | NULL next |

图 9.10 创建临时节点

上面的图表不需要解释，因为上面已经解释过类似的语句。

```cpp
/*
设置新节点中 val 数据成员的值。
*/
temp1 -> setVal(20);
```

这条语句将把 20 赋值给 `val` 数据成员。图 9.11 以图示表示了结果。

| | |

|---|---|

| 320 | 20 val |

| temp1 | NULL next |

图 9.11 `setVal()` 函数的效果

```cpp
/*
 让现有节点的 next 指针指向
新创建的节点。
*/
temp -> setNext(temp1);
```

图 9.12 以图示表示了结果。

# 数据结构 295

| | |

|---|---|

| 108 | val |

| temp | next |

| 320 | |

| 20 | val |

| temp1 | NULL |

图 9.12 `setNext()` 函数的效果

我们可以从它的定义看出，`setNext` 函数将其参数的值赋值给被调用的对象的 `next` 数据成员。在上面的例子中，函数是针对 `temp` 指向的对象被调用的。作为参数传递的值是 `temp1` 的值，即 320。结果是，`temp` 指向对象的 `next` 指针值被设置为 320，它现在指向新创建的节点。

```cpp
/*
 Set the value of val data member in the new node.
 */
temp -> setVal(10);
```

这条语句将把 10 赋值给 `val` 数据成员。图 9.9 以图示表示了结果。

## 使用 C++ 进行面向对象编程

```cpp
void appendNode(int pVal);
/*
在列表开头插入一个节点的函数。
*/
```

```cpp
void prependNode(int pVal);
/*
查找是否存在具有特定值的节点。
*/
```

```cpp
bool find(int pVal);
/*
删除第一个节点的函数。
*/
```

```cpp
void delBeg();
/*
删除最后一个节点的函数。
*/
```

```cpp
void delEnd();
/*
显示列表中所有节点的函数。
*/
```

```cpp
void display();
/*
该类的析构函数。它将删除列表中所有节点占据的内存。
*/
~SingleLinkedList();
};
```

```cpp
#endif
/*
SingleLinkedList.h 结束
*/
```

与节点类的头文件一样，此头文件也以注释开头，说明了头文件的名称并宣布文件的开始。紧之后是预处理器指令，用于防止在其他源代码中多次包含该头文件。随后是链表类的声明。头文件的倒数第二行包含预处理器块的结束，最后一行包含标记头文件结束的注释。

`SingleLinkedList` 类的每个对象都是一个链表。该类有一个数据成员 `head`，它是一个指针。从它的定义可以看出，`head` 应该指向链表的第一个节点。在我们的程序中，它要么被指向链表的第一个节点，要么被赋予 `NULL` 值（表示当前列表为空）。

让我们查看实现文件（列表 9.10），该文件包含了单链表成员函数的定义。

# 列表 9.10 单链表的实现文件

```cpp
/*
SingleLinkedList.cpp 开始
*/
#include <iostream.h>
#include "SingleLinkedList.h"

/*
单链表类的构造函数。它将 head 指针置空。
*/
```

```cpp
SingleLinkedList::SingleLinkedList()
{
    /*
    默认将 head 指针置空。
    */
    head = NULL;
}
```

/* 在列表末尾添加一个节点的函数。 */

```cpp
void SingleLinkedList::appendNode(int pVal)
{
    /*
    创建一个临时节点，我们将将其附加到列表中。
    SingleLinkedList 类的构造函数将
    将该节点的 next 指针置空。
    */
    SingleLinkedList* temp = new SingleLinkedList();
    /*
    将传递给函数的参数值拷贝到新节点。
    */
    temp->setVal(pVal);
    /*
    如果 head 指针为 NULL（列表为空）
    */
    if(head == NULL)
    {
        /*
        ... 让 head 指针指向临时节点
        */
        head = temp;
    }
    /*
    否则 ... */
    else
    {
        /*
        ... 创建一个临时指针，
        */
        SingleLinkedList* iter;
        /*
        ... 让它指向第一个节点，遍历到列表末尾并...
        */
        for(iter = head; iter->getNext() != NULL)
            iter = iter->getNext();
        /*
        ... 让最后一个节点的 next 指针指向
        临时节点。
        */
        iter->setNext(temp);
    }
}
```

/* 在列表开头插入一个节点的函数。 */

```cpp
void SingleLinkedList::prepend(int pVal)
{
    /*
    创建一个临时节点，我们将将其置于列表开头。
    SingleLinkedListNode 类的构造函数将
    将该节点的指针置空。
    */
    SingleLinkedList* temp = new SingleLinkedList();
    /*
    将传递给函数的参数值拷贝到新节点。
    */
    temp->setVal(pVal);
    /*
    如果 head 指针为 NULL（列表为空） ...
    */
    if(head == NULL)
    {
        /*
        ... 让 head 指针指向临时节点
        ...
        */
        head = temp;
    }
    /*
    ... 否则 ... */
    else
    {
        /*
        ... 让临时节点的 next 指针
        指向第一个节点并 ...
        */
        temp->setNext(head);
        /*
        ... 让 head 指针指向临时
        节点。
        */
        head = temp;
    }
}
```

/* 显示列表中所有节点的函数。 */
