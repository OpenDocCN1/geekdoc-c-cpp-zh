
```cpp
void SingleLinkedList::display()
{
    /*
    如果 head 指针为 NULL（列表为空）
    */
    if(head == NULL)
    {
        /*
        ... 显示错误消息
        */
        cout << "No nodes in list\n";
    }
    /* 否则 ... */
    else
    {
        /*
        ... 遍历列表 ...
        */
        for(SingleLinkedList* iter = head; iter != NULL; iter = iter->getNext())
        {
            /*
            ... 显示指向节点的值。
            */
            cout << iter->getVal() << endl;
        }
    }
}
```

/* 查找是否存在具有特定值的节点。 */

```cpp
bool SingleLinkedList::find(int pVal)
{
    /*
    初始化标志位，
    */
    bool found = false;
    /*
    创建一个临时指针，
    */
    SingleLinkedListNode * iter = head;
    /*
    遍历列表并 ...
    */
    while(iter != NULL)
    {
        /*
        如果节点的值与参数值匹配，
        */
        if(iter->getVal() == pVal)
        {
            /*
            将标志位设置为 true 并跳出
            */
            found = true;
            break;
        }
        /* 移动到下一个节点 */
        iter = iter->getNext();
    }
    return found;
}
```

/* 删除第一个节点的函数。 */

```cpp
void SingleLinkedList::delBeg()
{
    if(head == NULL)
    {
        /* ... 如果列表为空，则返回 ... */
        return;
    }
    /*
        ... 让 head 指针指向第二个节点
        */
    SingleLinkedList* temp = head;
    head = head->getNext();
    /*
        ... 删除第一个节点占据的内存
        */
    delete temp;
}
```

/* 删除最后一个节点的函数。 */

```cpp
void SingleLinkedList::delEnd()
{
    if(head == NULL)
    {
        /* ... 如果列表为空，则返回 ... */
        return;
    }
    if(head->getNext() == NULL)
    {
        /* ... 如果只有一个节点 ... */
        SingleLinkedList* temp = head;
        head = NULL;
        delete temp;
    }
    else
    {
        SingleLinkedList* iter = head;
        /* ... 遍历到最后一个节点 ... */
        while(iter->getNext()->getNext() != NULL)
        {
            iter = iter->getNext();
        }
        /* ... 删除最后一个节点 ... */
        SingleLinkedList* temp = iter->getNext();
        iter->setNext(NULL);
        delete temp;
    }
}
```

# 数据结构 307

245

| NULL | head |

| list1 | |

**图 9.16** 类构造函数的影响

`list1` 是 `SingleLinkedList` 类的对象。该框描绘了 `list1` 占据的内存块。从 `SingleLinkedList` 类的定义可以看出，该类的对象只有一个数据成员。该数据成员的名称为 `head`。类的构造函数会在对象创建时触发。它会将 `head` 指针的值设置为 `NULL`。

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

上面的框描绘了名为 `list1` 的对象（标记在框的底部）。由于它是 `SingleLinkedList` 类的对象，它只有一个数据成员——`head`（标记在框的右侧）。让我们来看在 `list1` 对象上调用 `appendNode()` 函数。

```cpp
list1.appendNode(5287);
```

如果函数定义得正确，那么在执行结束时，链表看起来应该像图 9.18 所示。

# 数据结构 309

| | 245 | 320 |

|---|---|---|

| head | 320 | 5287 | val |

| | list1 | NULL | next |

**图 9.18** `appendNode()` 函数的预期效果

让我们看看函数是否按预期执行。在函数执行之前，`head` 指针的值为 `NULL`。当函数开始执行时，参数 `pVal` 的值变为 5287，因为这是传递的值。之后，通过 `new` 运算符创建了一个临时节点，并让临时指针 `temp` 指向它（图 9.19）。

| | 695 | 320 |

|---|---|---|

| | 320 | 0 | val |

| temp | NULL | next |

**图 9.19** `appendNode()` 函数创建临时节点

下一语句是：

`temp->set(pVal);`

这将 `pVal` 的值（5287）拷贝到节点的 `val` 数据成员中。之后，`if` 语句将检查 `head` 指针的值是否为 `NULL`。此时测试结果为真，因为列表为空。`if` 块将执行，`temp` 的值将被拷贝到 `head`。这将导致 `head` 指针指向之前创建的临时节点。图 9.20 释了这一点。

| | 695 | 320 |

|---|---|---|

| | 320 | 5287 | val |

| temp | NULL | next |

| 245 | | |

| | 320 | |

| head | | |

**图 9.20** `temp` 指针的值拷贝到 `head` 指针

`else` 块不会执行，函数结束。由于 `temp` 是局部变量，它离开了作用域。

# 数据结构 313

对比图 9.25 和图 9.22，后者描述了我们预期的结果。如你所见，我们预期的函数行为与实际发生的情况完全吻的。因此，我们可以再次得出结论：我们的函数定义是正确的。

现在，请继续通过找出如果对同一个对象再次调用该函数时会发生什么，来验证该函数的定义是否正确。

现在，让我们来尝试理解 `display()` 函数。

```cpp
/*
 * 显示链表中所有节点的函数。
 */
void SingleLinkedList::display() {
 /*
 * 如果头指针为 NULL（列表为空）...
 if(head == NULL) {
  /*
  * ... 显示错误消息 ...
  cout << "No nodes in list\n";
  */
  ... 否则
 }
 else {
  /*
  * ... 让一个临时指针指向第一个节点，
  * 遍历链表并 ...
  */
 for(SingleLinkedListNode* iter = head; iter != NULL; iter = iter->getNext()) {
    /*
    * ... 显示指针指向节点的值。
    cout << iter->getVal() << endl;
    */
  }
}
}
```

与之前一样，让我们从链表类的一个新对象开始，这将创建一个空列表，然后在该新对象上调用 `display()` 函数（列表 9.14）。之后，我们将实际执行情况与预期的执行情况进行比较。

# 列表 9.14 执行 `display()` 函数

```cpp
/*
 * ListDisplay01.cpp 的开头
 */
#include "SingleLinkedList.h"
void main() {
 /*
 * 创建一个列表对象。
 */
SingleLinkedList list1;
/*
显示内容。
*/
list1.display();
}
/*
 * ListDisplay01.cpp 的结束
*/
```

# 输出

No nodes in list（列表中没有节点）

当列表为空时，我们预期函数会显示一条说列表为空的消息。让我们看看这种情况是否发生。

注意，由于构造函数的作用，`list1` 对象内部的头指针值在创建时会被设置为 `NULL`。因此，在调用 `display()` 函数时，它是 `NULL`。

现在，当函数开始执行时，`if` 块会将头指针的值与 `NULL` 进行比较。由于头指针的值为 `NULL`，`if` 语句中的测试表达式返回真。因此，`if` 块执行。这导致字符串 'No nodes in list' 显示在显示器上。自然地，`else` 块不执行，函数结束。这正符合我们预期的。

让我们看看列表不为空的其他情况（列表 9.15）。

# 列表 9.15 执行 `display()` 函数

```cpp
/*
ListDisplay02.cpp 的开头
*/
#include "SingleLinkedList.h"

void main()
{
/*
 创建一个列表对象。
 */
SingleLinkedList list1;
/*
 向列表中添加一个节点。
 */
list1.appendNode(5287);
/*
 再添加另一个节点。
 */
list1.appendNode(325);
/*
 显示内容。
 */
list1.display();
}
End of ListDisplay02.cpp 的结束
*/
```

我们现在知道，在上述调用两次 `appendNode()` 函数后，链表将看起来像图 9.26 一样。

![](img/5bfa77b13fdaa376725789bb8c00ee79_328_0.png)

**图 9.26** 在执行 `display()` 函数之前的列表状态

由于调用了 `display()` 函数，我们预期节点中的值将被显示。

# 数据结构 319

会将 `pVal1` 的值（即 5287）复制到节点的成员变量中。之后，`if` 语句中的测试表达式将检查头指针的值是否为 `NULL`。由于列表是空的，此时该测试将返回。`if` 块将执行，并将 `temp` 的值复制给 `head`。这将导致头指针也指向新创建的临时节点。图 9.32 所示所示。

![](img/5bfa77b13fdaa376725789bb8c00ee79_332_0.png)

**图 9.32** 临时节点的初始化以及头指针指向它

`else` 块将不会执行，函数将结束。由于 `temp` 是局部变量，它将离开作用域，我们留下一个类似于图 9.33 的链表。

![](img/5bfa77b13fdaa376725789bb8c00ee79_332_1.png)

**图 9.33** `prependNode()` 函数的观察效果

将图 9.33 与图 9.30 进行对比，后者描述了我们预期的结果。如你所示，我们预期的函数行为与实际发生的情况完全一致。

让我们在 `list1` 对象上两次调用该函数（列表 9.17），并验证该函数是否执行了其定义的任务。

- **列表 9.17** 执行 `prependNode()` 函数

```cpp
/*
 PrependNode2.cpp 的开始
 */
#include "SingleLinkedList.h"

void main()
{
 /*
创建一个列表对象
/*
SingleLinkedList list1;
/*
在 list1 对象上调用 prependNode 函数。
/*
list1.prependNode(5287);
/*
再次在 list1 对象上调用 prepend() 函数。
/*
list1.prependNode(325);
/*
 PrependNode2.cpp 的结束
/*
```

```

在该程序执行结束时（列表 9.17），我们预期的链表将如图 9.34 所示。

![](img/5bfa77b13fdaa376725789bb8c00ee79_333_0.png)

**图 9.34** `prependNode()` 函数的预期效果

让我们再次追踪该函数的执行，看看它是否按照我们的预期运行。让我们从对函数的第二次调用开始，因为我们已经看到了程序之前部分的效果。此时，链表看起来如下。

![](img/5bfa77b13fdaa376725789bb8c00ee79_333_1.png)

**图 9.35** `prependNode()` 函数添加第一个节点

# 数据结构 321

此时，函数被第二次调用。注意，此时头指针不为 `NULL`（它的值为 320，即它所指向的第一个节点的地址）。

执行过程与之前相同，直到 `if` 语句中的测试表达式检查头指针的值是否为 `NULL`。由于列表不空，该测试将返回 `false`。相反，`else` 块将执行。`else` 块的第一条语句将头指针的值复制到函数开始处创建的临时节点的 `next` 指针中。结果情况可以用图 9.36 描述。

![](img/5bfa77b13fdaa376725789bb8c00ee79_334_0.png)

**图 9.36** 将新节点连接旧节点

下一条语句将 `temp` 指针的值复制给头指针。因此，头指针最终指向了该临时节点。图 9.37 描述了这种情况。

![](img/5bfa77b13fdaa376725789bb8c00ee79_334_1.png)

**图 9.37** 头指针指向新节点

由于 `temp` 是局部变量，它将离开作用域，我们留下一个类似于图 9.38 的链表。

![](img/5bfa77b13fdaa376725789bb8c00ee79_335_0.png)

**图 9.38** `prependNode()` 函数的观察效果

# 322 C++ 对象面向编程

## 使用 C++ 进行面向对象编程

```cpp

/*

如果列表为空，则不执行任何操作（没有 else）。

*/
```
