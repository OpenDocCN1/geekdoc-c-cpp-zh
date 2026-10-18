

## DISPLAY 13.12 二叉树

![](img/88b1f375f11336dbd9dac8b1675d0698_797_0.png)

每个节点恰好有两个链接。还有其他种类的树，其节点中的链接数量不同，但二叉树是最常见的情况。

树并不是一种链表的形式，但确实以与链表中相似的方式使用链接（指针）。二叉树的节点类型的定义本质上与双向链表中的定义相同，但两个链接通常使用左和右的某种形式命名。以下是一个可用于构建二叉树的节点类型：

```
struct TreeNode
{
    int data;
    TreeNode *leftLink;
    TreeNode *rightLink;
};
```

在 Display 13.12 中，名为 root 的指针指向根节点（“顶部节点”）。根节点的作用类似于普通链表中头节点的作用（Display 13.10）。可以通过跟随链接从根节点到达树中的任何节点。

术语 tree 可能听起来像是误称。根位于树的顶部，而分支结构看起来更像根的分支结构而不是树的分支结构。术语的秘密在于将图片（Display 13.12）倒过来。图片随后确实类似于树的分支结构，而根节点就是树根开始的位置。分支末端的节点，其两个链接实例变量均设置为 NULL，被称为叶节点，这一术语现在可能更有意义了。

尽管本书中没有空间深入探讨该主题，但二叉树可用于高效地存储和检索数据。

## 类的链表

在前面的示例中，我们通过使用 struct 来保存列表中节点的 contents 来创建链表。也可以使用 class 而不是 struct 来创建相同的数据结构。逻辑是相同的，只是使用和定义 class 的语法应替换为 struct 的语法。

Display 13.13 和 13.14 说明了如何定义一个 Node 类。数据变量使用信息隐藏原则声明为 private，并创建了公共方法来访问数据值和链接中的下一个节点。Display 13.15 通过在列表前端插入新节点创建了一个包含五个节点的短列表

VideoNote
Walkthrough of Linked
Lists of Classes

## DISPLAY 13.13 Node 类的接口文件

```
//This is the header file for Node.h. This is the interface for
a node class that behaves similarly to the struct defined
in Display 13.4
namespace linkedlistofclasses
{
    class Node
    {
    public:
        Node();
        Node(int value, Node *next);
        //Constructors to initialize a node

        int getData() const;
        //Retrieve value for this node

        Node *getLink() const;
        //Retrieve next Node in the list

        void setData(int value);
        //Use to modify the value stored in the list

        void setLink(Node *next);
        //Use to change the reference to the next node

    private:
        int data;
        Node *link;
    };
    typedef Node* NodePtr;
} //linkedlistofclasses
//Node.h
```

## DISPLAY 13.14 Node 类的实现文件

```
//This is the implementation file Node.cpp.
//It implements logic for the Node class. The interface
//file is in the header file Node.h
#include <iostream>
#include "Node.h"

namespace linkedlistofclasses
{
    Node::Node() : data(0), link(NULL)
    {
        //deliberately empty
    }

    Node::Node(int value, Node *next) : data(value), link(next)
    {
        //deliberately empty
    }

    //Accessor and Mutator methods follow

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
} //linkedlistofclasses
//Node.cpp
```

## DISPLAY 13.15 使用 Node 类的程序（第 1 部分，共 3 部分）

//This program demonstrates the creation of a linked list
//using the Node class. Five nodes are created, output, then
//destroyed.

## DISPLAY 13.15 使用 Node 类的程序（第 2 部分，共 3 部分）

```
```cpp
#include <iostream>
#include "Node.h"

using namespace std;
using namespace linkedlistofclasses;

//This function inserts a new node onto the head of the list
//and is a class-based version of the same function defined
//in Display 13.4.
void headInsert(NodePtr& head, int theNumber)
{
    NodePtr tempPtr;
    //The constructor sets tempPtr->link to head and
    //sets the data value to theNumber
    tempPtr = new Node(theNumber, head);
    head = tempPtr;
}

int main()
{
    NodePtr head, tmp;

    //Create a list of nodes 4 -> 3 -> 2 -> 1 -> 0
    head = new Node(0, NULL);
    for (int i = 1; i < 5; i++)
    {
        headInsert(head, i);
    }
    //Iterate through the list and display each value
    tmp = head;
    while (tmp != NULL)
    {
        cout << tmp->getData() << endl;
        tmp = tmp->getLink();
    }
    //Delete all nodes in the list before exiting
    //the program.
    tmp = head;
    while (tmp != NULL)
    {
        NodePtr nodeToDelete = tmp;
        tmp = tmp->getLink();
        delete nodeToDelete;
    }
    return 0;
}
```
```

## DISPLAY 13.15 使用 Node 类的程序（第 3 部分，共 3 部分）

## Sample Dialogue

```
4
3
2
1
0
```

将新节点插入到列表的前端。headInsert 函数在逻辑上与 Display 13.4 中定义的相同函数相同，只是使用了为 Node 类定义的构造函数来设置数据。

## 13.2 栈和队列

> 但现在在前的，将要在后；在后的，将要在前。

马太福音 19:30

链表有许多应用。在本节中，我们给出它们可以用于的两个示例。我们使用链表来实现两种已知的数据结构，即栈和队列。在本节中，我们始终使用常规链表而不是双向链表。

## 栈

栈是一种数据结构，它以与数据存储顺序相反的顺序检索数据。假设你将字母 'A'、'B' 然后 'C' 放入栈中。当你从栈中取出这些字母时，它们将被移除

## DISPLAY 13.16 一个栈

![](img/88b1f375f11336dbd9dac8b1675d0698_801_0.png)

按 'C'、'B' 然后 'A' 的顺序。这次栈的使用在 Display 13.16 中进行了图解。如图所示，你可以将栈想象成地面上的一个洞。为了从栈中取出某样东西，你必须先移除上面想要取出的物品。因此，栈通常被称为后进先出（LIFO）数据结构。

栈被用于许多语言处理任务。在第 14 章中，我们将讨论计算机系统如何使用栈来跟踪 C++ 函数调用。然而，在这里我们只做一个非常简单的应用。我们在此示例中的目标是向你展示如何使用链表技术来实现特定的数据结构；栈是链表使用的一个简单示例。你不必阅读第 14 章就能理解此示例。

## 编程示例

## 一个栈类

我们的 Stack 类的接口在 Display 13.17 中给出。此特定栈用于存储类型为 char 的数据。你可以定义一个类似的栈来存储任何其他类型的数据。对栈可以执行两个基本操作：将项目添加到栈中以及从栈中移除项目。

## DISPLAY 13.17 栈类的接口文件（第 1 部分，共 2 部分）

```
1  //This is the header file stack.h. This is the interface for the class Stack,
2  //which is a class for a stack of symbols.
3  #ifndef STACK_H
4  #define STACK_H
5  namespace stacksavitch
6  {
7      struct StackFrame
8      {
9          char data;
10         StackFrame *link;
11     };
12     typedef StackFrame* StackFramePtr;
13     class Stack
14     {
15     public:
16         Stack();
17         //Initializes the object to an empty stack.
18         Stack(const Stack& aStack);
19         //Copy constructor.
20         ~Stack();
21         //Destroys the stack and returns all the memory to the freestore.
```

(continued)

