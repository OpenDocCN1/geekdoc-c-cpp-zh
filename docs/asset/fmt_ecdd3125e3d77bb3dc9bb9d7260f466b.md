
## 动态栈

### 概念
栈可以基于链表实现，并在 `push` 或 `pop` 操作时扩展或收缩。

动态栈基于链表而不是数组构建。与数组栈相比，链表栈有两个优势：
1. 不需要指定栈的初始大小。动态栈在每次推入值时都会扩展一个节点。
2. 只要系统有可用内存，动态栈永远不会满出。

在本节中，我们将查看动态栈类 `DynIntStack`。该类是之前讨论过的 `IntStack` 类的动态版本。类声明如下：

### DynIntStack.h

```cpp
// DynIntStack 类的规范文件
#ifndef DYINTSTACK_H
#define DYINTSTACK_H

class DynIntStack
{
private:
    // 节点结构
    struct StackNode
    {
        int value;       // 节点的值
        StackNode *next; // 指向下一个节点的指针
    };

    StackNode *top; // 指向栈顶的指针

public:
    // 构造函数
    DynIntStack()
    { top = nullptr; }

    // 析构函数
    ~DynIntStack();

    // 栈操作
    void push(int);
    void pop(int &);
    bool isEmpty();
};

#endif
```

### DynIntStack.cpp

```cpp
#include <iostream>
#include "DynIntStack.h"

using namespace std;

/*************************************
// 析构函数
// 此函数删除列表中的每个节点。
//************************************
DynIntStack::~DynIntStack()
{
    StackNode *nodePtr = nullptr, *nextNode = nullptr;

    // 将节点 nodePtr 指向栈顶。
    nodePtr = top;

    // 遍历列表并删除每个节点。
    while (nodePtr != nullptr)
    {
        nextNode = nodePtr->next;
        delete nodePtr;
        nodePtr = nextNode;
    }
}

/****************************************************
// 成员函数将参数推入栈中。
****************************************************/

void DynIntStack::push(int num)
{
    StackNode *newNode = nullptr; // 指向新节点的指针

    // 分配新节点并将 num 存储其中。
    newNode = new StackNode;
    newNode->value = num;

    // 如果列表中没有节点，将 newNode 设置为第一个节点。
    if (isEmpty())
    {
        top = newNode;
        newNode->next = nullptr;
    }
    else // 否则，在 top 之前插入 newNode。
    {
        newNode->next = top;
        top = newNode;
    }
}

/****************************************************
// 成员函数弹出栈顶的值，并将其复制到作为参数传递的变量。
****************************************************/

void DynIntStack::pop(int &num)
{
    StackNode *temp = nullptr; // 临时指针

    // 首先确保栈不为空。
    if (isEmpty())
    {
        cout << "The stack is empty.\n";
    }
    else // 弹出栈顶值
    {
        num = top->value;
        temp = top->next;
        delete top;
        top = temp;
    }
}

/*******************************************************************
/* 成员函数 isEmpty 在栈为空时返回 true，否则返回 false。
********************************************************************/

bool DynIntStack::isEmpty()
{
    bool status;

    if (!top)
        status = true;
    else
        status = false;

    return status;
}
```

让我们查看 `DynIntStack.cpp` 中第 31 到 51 行的 `push` 操作。在第 36 和第 37 行，内存中分配了一个新节点，并将函数参数复制到它的 `value` 成员中：

```cpp
newNode = new StackNode;
newNode->value = num;
```

接下来，在第 41 行，`if` 语句调用 `isEmpty` 函数来确定栈是否为空：

```cpp
if (isEmpty())
{
    top = newNode;
    newNode->next = nullptr;
}
```

如果 `isEmpty` 返回 `true`，`top` 将指向新节点，并且新节点的 `next` 指针被设置为 `nullptr`。在执行这些语句后，列表中将有一个节点（栈中有一个值）。

如果 `isEmpty` 在 `if` 语句中返回 `false`，则执行第 46 到 50 行的后续语句：

```cpp
else // 否则，在 top 之前插入 newNode
{
    newNode->next = top;
    top = newNode;
}
```

注意 `newNode` 被插入到 `top` 所指向的节点之前的列表中。然后更新 `top` 指针指向新节点。完成后，`newNode` 位于栈顶。

现在，让我们查看第 59 到 75 行的 `pop` 函数。正如 `push` 函数必须在列表头部插入节点一样，`pop` 必须在列表头部删除节点。首先，函数在第 64 行调用 `isEmpty` 来确定栈中是否有节点。如果没有节点，则显示一条错误消息：

```cpp
if (isEmpty())
{
    cout << "The stack is empty.\n";
}
```

如果 `isEmpty` 返回 `false`，则执行第 68 到 74 行的语句：

```cpp
else // 弹出栈顶值
{
    num = top->value;
    temp = top->next;
    delete top;
    top = temp;
}
```

首先，栈顶节点的 `value` 成员被复制到 `num` 参数。这为程序后续使用保存了该值。接下来，让临时 `StackNode` `temp` 指向 `top->next`。如果列表中还有其他节点，这将导致 `temp` 指向第二个节点。如果没有更多节点，它将指向 `nullptr`。现在，可以安全地删除栈顶节点。将 `top` 指针设置为 `temp`。此操作将 `top` 指针向下移动一个节点。之前的第二个节点现在变成了第一个。

第 82 到 92 行的 `isEmpty` 函数非常简单。如果 `top` 是空指针，则列表（栈）为空。

程序 19-4 是一个演示 `DynIntStack` 类的驱动程序。

### 程序 19-4

```cpp
// 此程序演示了动态栈。
// 栈类。
#include <iostream>
#include "DynIntStack.h"
using namespace std;

int main()
{
    int catchVar;

    // 创建一个 DynIntStack 对象。
    DynIntStack stack;

    // 将 5, 10 和 15 入栈。
    cout << "Pushing 5\n";
    stack.push(5);
    cout << "Pushing 10\n";
    stack.push(10);
    cout << "Pushing 15\n";
    stack.push(15);

    // 从栈中弹出值。
    cout << "Popping...\n";
    stack.pop(catchVar);
    cout << catchVar << endl;
    stack.pop(catchVar);
    cout << catchVar << endl;
    stack.pop(catchVar);
    cout << catchVar << endl;

    // 尝试从栈中弹出另一个值。
    stack.pop(catchVar);
    cout << "The stack is empty.\n";

    return 0;
}
```

程序 19-5 展示了 `DynamicStack` 模板。该程序是程序 19-3 的修改。它创建了一个字符串栈，然后显示一个菜单，允许用户向栈中推入元素、从栈中弹出元素或退出程序。

### 程序 19-5

```cpp
#include <iostream>
#include <string>
#include "DynamicStack.h"

using namespace std;

// 菜单选择常量
const int PUSH_CHOICE = 1,
       POP_CHOICE = 2,
       QUIT_CHOICE = 3;

// 函数原型声明
void menu(int &);
void getStackSize(int &);
void pushItem(DynamicStack<string> &);
void popItem(DynamicStack<string> &);

int main()
{
    int choice; // 用于存储菜单选择

    // 创建栈。
    DynamicStack<string> stack;

    do
    {
        // 获取用户的菜单选择。
        menu(choice);

        // 执行用户的选择。
        if (choice != QUIT_CHOICE)
        {
            switch (choice)
            {
                case PUSH_CHOICE:
                    pushItem(stack);
                    break;
                case POP_CHOICE:
                    popItem(stack);
                    break;
            }
        }
    } while (choice != QUIT_CHOICE);

    return 0;
}
```

### menu 函数

```cpp
/****************************************************
// menu 函数显示菜单并获取用户的选择，
// 该选择被赋值给引用参数。
****************************************************/
```
