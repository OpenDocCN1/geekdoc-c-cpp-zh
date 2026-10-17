
树不是链表的形式，但它使用指针的方式与链表中的方式相似。二叉树节点类型定义与双向链表基本相同，但两个链接通常使用 `left` 和 `right` 命名。以下是用于构建二叉树的节点类型：

```cpp
struct TreeNode {
    int data;
    TreeNode *leftLink;
    TreeNode *rightLink;
};
```

# 第 13 章 / 指针与链表

位于分支末端且两个 `link` 实例变量都设置为 `NULL` 的节点被称为叶子节点，这个术语听起来可能很有道理。

虽然我们在书中不必深入探讨这个主题，但二叉树可以高效地存储和检索数据。

## 类的链表

在之前的示例中，我们通过一个 `struct` 来存储链表中节点的内容，从而创建了链表。可以使用 `class` 代替 `struct` 来创建相同的数据结构。其逻辑是完全相同的，只是使用和定义 `class` 的语法可以替换 `struct` 的语法。

显示 13.13 和 13.14 展示了如何定义一个 `Node` 类。数据根据信息隐藏原则被声明为 `private`，并创建了 `public` 方法来访问数据以及链表中的下一个节点。显示 13.15 通过插入新节点创建了一个包含五个节点的短列表。

![](img/67be1289808bc3852827f7f3e32e9d82_793_0.png)

### 显示 13.13 Node 类的接口文件

```
// 这是 Node.h 的头文件。这是 node 类的接口，
// 它的行为与显示 13.4 中定义的 struct 类似
namespace linkedlistofclasses
{
    class Node {
    public:
        Node();
        Node(int value, Node *next);
        // 用于初始化的构造函数
        int getData() const;
        // 获取此节点的值
        Node *getLink() const;
        // 获取链表中的下一个 Node
        void setData(int value);
        // 用于修改列表中存储的值
        void setLink(Node *next);
        // 改变指向下一个节点的引用
    private:
        int data;
        Node *link;
    };
    typedef Node NodePtr;
}//linkedlistofclasses
{
//Node.h
```

### 显示 13.14 Node 类的实现文件

```cpp
 // 这是 Node.cpp 的实现文件。
// 它实现了 Node 类的逻辑。接口
// 位于头文件 Node.h 中
#include <iostream>
#include "Node.h"

namespace linkedlistofclasses
{
    Node::Node() : data(0), link(NULL)
{
        // 故意留空
    }

    Node::Node(int value, Node *next) : data(value), link(next)
    {
        // 故意留空
    }

    // 访问器和修改器方法

    int Node::getData() const
{
        return data;
    }

    Node* Node::getLink() const
{
        return link;
    }

    void Node::setData(int value)
{
        data = value;
    }

    void Node::setLink(Node *next)
{
        link = next;
    }
}//linkedlistofclasses
//Node.cpp
```

### 显示 13.15 使用 Node 类的程序（3 部分中的 1）

// 此程序演示了如何使用 Node 类

// 创建链表。创建了五个节点，输出，然后

// 销毁了它们。

(继续)

### 显示 13.15 使用 Node 类的程序（3 部分之 2）

```cpp
#include <iostream>
#include "Node.h"

using namespace std;
using namespace linkedlistofclasses;

// 此函数将新节点插入到链表的头部，
// 与显示 13.4 中定义的相同函数的类版本
// 在逻辑上是完全相同的。
void headInsert(NodePtr& head, int theNumber)
{
    NodePtr tempPtr;
    // 构造函数将 tempPtr->link 设置为 head
    // 并将数据值设置为 theNumber
    tempPtr = new Node(theNumber, head);
    head = tempPtr;
}

int main() {
    NodePtr head, tmp;
    // 创建一个包含 4 个节点的链表 -> 3 -> 2 -> 1 -> 0
    head = new Node(0, NULL);
    for (int i = 1; i < 5; i++) {
        headInsert(head, i);
    }
    // 遍历链表并显示每个值
    tmp = head;
    while (tmp != NULL) {
        cout << tmp->getData() << endl;
        tmp = tmp->getLink();
    }
    // 在退出程序前删除链表中所有的节点
    tmp = head;
    while (tmp != NULL) {
        NodePtr nodeToDelete = tmp;
        tmp = tmp->getLink();
        delete nodeToDelete;
    }
    return 0;
}
```

## 13.2 栈与队列

### 显示 13.15 使用 Node 类的程序（3 部分之 3）

#### 示例对话

```
4
3
2
1
0
```

到链表的头部。`headInsert` 函数在逻辑上与显示 13.4 中定义的相同函数相同，不同之处为 `Node` 类定义的构造函数被用于设置数据。

> 但许多现在在前的人将必在后，许多现在在后的人将必在前。
>
> 马太福音 19:30

链表有许多应用。在本节中，我们提供了两个它们用途的示例。我们使用链表来实现栈和队列。我们使用链表来提供栈和队列的实现。在本节中，我们使用栈和队列。

栈是一种数据结构，它以相反的顺序存储数据。

栈有许多应用。在本节中，我们提供了两个它们用途的示例。我们使用链表来实现栈和队列。我们使用链表来提供栈和队列的实现。

栈是一种数据结构，它以相反的顺序存储数据。

栈有许多应用。在本节中，我们提供了两个它们用途的示例。我们使用链表来实现栈和队列。我们使用链表来提供栈和队列的实现。

栈是一种数据结构，它以相反的顺序存储数据。

栈有许多应用。在本节中，我们提供了两个它们用途的示例。我们使用链表来实现栈和队列。我们使用链表来提供栈和队列的实现。

栈是一种数据结构，它以相反的顺序存储数据。

栈有许多应用。在本节中，我们提供了两个它们用途的示例。我们使用链表来实现栈和队列。我们使用链表来提供栈和队列的实现。

### 栈

栈的元素访问方式是后进先出（LIFO）的。这种此程序演示了如何理解栈的逻辑。栈是一种数据结构，它以相反的顺序存储数据。

栈有许多应用。在本节中，我们提供了两个它们用途的示例。我们使用链表来实现栈和队列。我们使用链表来提供栈和队列的实现。

### 栈

栈的元素访问方式是后进先出（LIFO）的。这种此程序演示了如何理解栈的逻辑。栈是一种数据结构，它以相反的顺序存储数据。

### 栈

栈的元素访问方式是后进先出（LIFO）的。这种此程序演示了如何理解栈的逻辑。栈是一种数据结构，它以相反的顺序存储数据。

### 栈

栈的元素访问方式是后进先出（LIFO）的。这种此程序演示了如何理解栈的逻辑。栈是一种数据结构，它以相反的顺序存储数据。

### 栈

栈是一种数据结构，它以相反的顺序存储数据。

## 13.2 栈与队列

### 显示 13.18 栈程序（3 部分之 1）

### 栈

栈的元素访问方式是后进先出（LIFO）的。这种此程序演示了如何理解栈的逻辑。栈是一种数据结构，它以相反的顺序存储数据。

### 栈

栈的元素访问方式是后进先出（LIFO）的。这种此程序演示了如何理解栈的逻辑。栈是一种数据结构，它以相反的顺序存储数据。

### 栈

栈的元素访问方式是后进先出（LIFO）的。这种此程序演示了如何理解栈的逻辑。栈是一种数据结构，它以相反的顺序存储数据。

## 13.2 栈与队列

### 显示 13.18 栈程序（3 部分之 2）

### 栈是一种数据结构，它以相反的顺序存储数据。

### 栈

栈的元素访问方式是后进先出（LIFO）的。这种此程序演示了如何理解栈的逻辑。栈是一种数据结构，它以相反的顺序存储数据。

### 栈

栈的元素访问方式是后进先出（LIFO）的。这种此程序演示了如何理解栈的逻辑。栈是一种数据结构，它以相反的顺序存储数据。

### 栈

栈是一种数据结构，它以相反的顺序存储数据。

### 栈

栈的元素访问方式是后进先出（LIFO）的。这种此程序演示了如何理解栈的逻辑。栈是一种数据结构，它以相反的顺序存储数据。

### 栈

栈的元素访问方式是后进先出（LIFO）的。这种此程序演示了如何理解栈的逻辑。栈是一种数据结构，它以相反的顺序存储数据。

## 13.2 栈与队列

### 显示 13.18 栈程序（3 部分之 3）

### 显示 13.18 使用 Stack 类的程序（部分 2/2）

```cpp
stack s;
char next, ans;

do {
  cout << "Enter a word: ";
  cin.get(next);
  while (next != '\n') {
    s.push(next);
    cin.get(next);
  }

  cout << "Written backward that is: ";
  while ( s.empty() ) {
    cout << s.pop();
  }
  cout << endl;

  cout << "Again?(y/n): ";
  cin >> ans;
  cin.ignore(10000, '\n');
} while (ans != '\n' && ans != 'N');

return 0;
```

> `<cin` 的 `ignore` 成员在第 8 章中讨论。它会丢弃当前输入行上剩余的输入，最多 10000 个字符或直到输入回车键。它还会丢弃行尾的换行符 `'\n'`。

#### 示例对话

| 输入一个单词：straw |

| 反向写入的结果是：warts |

| 再次吗?(y/n): y |

| 输入一个单词：C++ |

| 反向写入的结果是：++C |

| 再次吗?(y/n): n |

屏幕。因为从栈中数据的顺序与其进入栈的顺序相反，所以输出显示的是反向的单词。如显示 13.19 所示，我们的 `Stack` 类是用链表实现的，其中链表的头部作为栈的顶。成员变量 `top` 是一个指向链表头部的指针。

## 13.2 栈与队列

### 显示 13.19 Stack 类的实现（部分 1/2）

```cpp
// 这些是实现文件 stack.cpp。
// 这些是 Stack 类的实现。
// Stack 类的接口在头文件 stack.h 中。
#include <iostream>
#include <cstddef>
#include "stack.h"
using namespace std;

namespace stacksavitch {
    // 使用了 cstddef;
    Stack() : top(NULL)
    {
        // 函数体故意为空。
    }

    Stack(const Stack& aStack)
    // 拷贝构造函数的定义见自测试练习 11。
    {
        char next;
        while (! empty())
            next = pop(); // pop 调用 delete。
    }

    // 使用了 cstddef;
    bool empty() const
    {
        return (top == NULL);
    }

    void push(char theSymbol)
    // 剩余定义见自测试练习 10。
    // 使用了 iostream 和 cstddef;
    char pop()
    {
        if (empty()) {
            cout << "Error: popping an empty stack.\n";
            exit(1);
        }
    }
}
```

（续）

### 显示 13.19 Stack 类的实现（部分 2/2）

```cpp
char result = top->data;
StackFramePtr tempPtr;
tempPtr = top;
top = top->link;

delete tempPtr;
return result;
}
// stacksavitch
```

编写成员函数 `push` 的定义是自测练习 10。然而，我们已经给出了该任务的算法。`push` 成员函数的代码基本上与显示 13.4 所示的 `headInsert` 函数相同，不同之处在成员函数中我们使用了一个名为 `top` 的指针来代替之前的指针。

空栈是一个空链表，因此空栈通过将指针 `top` 设置为 `NULL` 来实现。一旦你意识到 `NULL` 代表空栈，默认构造函数和成员函数 `empty` 的实现就显而易见了。

拷贝构造函数的定义有点复杂，但没有使用任何我们讨论过的技术。细节留给自测试练习 11。

### 自测试练习

10. 给出显示 13.17 中描述的 `Stack` 类成员函数 `push` 的定义。

11. 给出显示 13.17 中描述的 `Stack` 类拷贝构造函数的定义。

## 队列

栈是一个后进先出的结构。队列是一个先进先出（FIFO）结构。队列可以用链表实现，其中链表的头部是队列的头部，链表的尾部是队列的尾部。元素按照添加的顺序被移除。

### 显示 13.22 使用 Queue 类的程序（第 2/2 部分）

#### 示例对话

```
Enter a word: straw
you entered: straw
Again?(y/n): y
enter a word: C++
You entered: C++
Again?(y/n): n
```

如显示 13.21 和 13.23 所示，我们的队列类是用链表实现的，其中链表的头部作为队列的队。成员变量 `front` 是一个指向链表头部的指针。节点在链表的头部被移除。成员变量 `back` 是一个指向链表另一端节点的指针。节点在链表的这一端被添加。

空队列只是一个空列表，因此，空队列通过将指针 `front` 和 `back` 设置为 `NULL` 来实现。实现的其余细节与我们之前看到的内容相似。

### 显示 13.23 Queue 类的实现（第 1/3 部分）

```cpp
// 这是实现文件 queue.cpp。
// 这是这是 Queue 类的实现。
#include <iostream>
#include <cdblib>
#include <cstddef>
#include "queue.h"
using namespace std;
namespace queueswitch
{
    // 使用 cstddef;
    Queue::Queue() : front(NULL), back(NULL)
    {
        // 刻意留。
    }
Queue::Queue(const Queue& aQueue) // 构造函数见自测练习 12。
(继续)
```

## 13.2 栈与队列

### 显示 13.23 Queue 类的实现（第 2/3 部分）
