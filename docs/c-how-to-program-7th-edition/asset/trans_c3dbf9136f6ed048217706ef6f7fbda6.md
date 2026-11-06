
从列表前端开始。搜索名字以字母表末尾附近字母开头的人时，可以从列表后端开始。

在循环双向链表（图 20.12）中，最后一个节点的前向指针指向第一个节点，第一个节点的后向指针指向最后一个节点，从而闭合这个“环”。

![](img/023f159fdd47d944d48e08843cea732d_860_0.png)

图 20.12 | 循环双向链表。

## 20.5 栈

第14章“模板”解释了具有底层数组实现的栈类模板的概念。本节中，我们使用基于指针的链表实现作为底层实现。我们还会在第22章“标准模板库（STL）”中讨论栈。

栈数据结构只允许在栈顶向栈中添加节点和从栈中删除节点。因此，栈被称为后进先出（LIFO）数据结构。实现栈的一种方式是将其作为链表的受限版本。在这种实现中，栈中最后一个节点的链接成员被设置为空（零），以表示栈底。

用于操作栈的主要成员函数是 push 和 pop。函数 push 在栈顶插入一个新节点。函数 pop 从栈顶删除一个节点，将弹出的值存储在传递给调用函数的引用变量中，并在弹出操作成功时返回 true（否则返回 false）。

栈有许多有趣的应用。例如，当进行函数调用时，被调用函数必须知道如何返回其调用者，因此返回地址被压入栈中。如果发生一系列函数调用，连续的返回地址值按后进先出顺序压入栈中，以便每个函数都能返回其调用者。栈以与传统非递归调用相同的方式支持递归函数调用。第6.11节详细讨论函数调用栈。

栈为函数每次调用时的自动变量提供内存，并存储这些变量的值。当函数返回其调用者或抛出异常时，会调用每个局部对象的析构函数（如果有），该函数的自动变量所占空间从栈中弹出，这些变量对程序而言不再可见。

编译器在表达式求值和生成机器语言代码的过程中使用栈。习题探讨了栈的几种应用，包括使用栈开发你自己的完整可运行的编译器。

我们将利用链表与栈之间的密切关系，主要通过复用 List 类来实现栈类。首先，我们通过私有继承 List 类来实现栈类。然后，我们通过将 List 类作为栈类的私有成员进行组合，实现一个行为相同的栈类。当然，本章中的所有数据结构（包括这两个栈类）都实现为模板，以促进进一步的可复用性。

图 20.13–20.14 的程序主要通过私有继承（第9行）图 20.4 的 List 类模板来创建 Stack 类模板（图 20.13）。我们希望 Stack 具有成员函数 push（第13–16行）、pop（第19–22行）、isStackEmpty（第25–28行）和 printStack（第31–34行）。注意，这些本质上就是 List 类模板的 insertAtFront、removeFromFront、isEmpty 和 print 函数。当然，List 类模板还包含其他成员函数（即 insertAtBack 和 removeFromBack），我们不会通过 Stack 类的公共接口使它们可访问。因此，当我们指明 Stack 类模板要从 List 类模板继承时，我们指定私有继承。这会使 List 类模板的所有成员函数在 Stack 类模板中成为私有成员。在实现 Stack 的成员函数时，我们让这些函数分别调用 List 类的相应成员函数——push 调用 insertAtFront（第15行），pop 调用 removeFromFront（第21行），isStackEmpty 调用 isEmpty（第27行），printStack 调用 print（第33行）——这称为委托。

```cpp
// Fig. 20.13: Stack.h
// Template Stack class definition derived from class List.
#ifndef STACK_H
#define STACK_H

#include "List.h" // List class definition

template< typename STACKTYPE >
class Stack : private List< STACKTYPE >
{
public:
   // push calls the List function insertAtFront
   void push( const STACKTYPE &data )
   {
      insertAtFront( data );
   } // end function push

   // pop calls the List function removeFromFront
   bool pop( STACKTYPE &data )
   {
      return removeFromFront( data );
   } // end function pop

   // isStackEmpty calls the List function isEmpty
   bool isStackEmpty() const
   {
      return this->isEmpty();
   } // end function isStackEmpty
```

图 20.13  |  Stack 类模板定义。（第1部分，共2部分。）

```text
The list is: 3.3 2.2 1.1
3.3 popped from stack
The list is: 2.2 1.1
2.2 popped from stack
The list is: 1.1
1.1 popped from stack
The list is empty
All nodes destroyed
All nodes destroyed
```

图 20.14 | 一个简单的栈程序。（第3部分，共3部分。）

实现 Stack 类模板的另一种方式是通过组合复用 List 类模板。图 20.15 是 Stack 类模板的新实现，其中包含一个名为 stackList 的 List< STACKTYPE > 对象（第38行）。这个版本的 Stack 类模板使用图 20.4 中的 List 类。要测试这个类，请使用图 20.14 中的驱动程序，但在该文件的第6行包含新的头文件——Stackcomposition.h。对于两个版本的 Stack 类，程序的输出完全相同。

```cpp
// Fig. 20.15: Stackcomposition.h
// Template Stack class definition with composed List object.
#ifndef STACKCOMPOSITION_H
#define STACKCOMPOSITION_H

#include "List.h" // List class definition

template< typename STACKTYPE >
class Stack
{
public:
   // no constructor; List constructor does initialization

   // push calls stackList object's insertAtFront member function
   void push( const STACKTYPE &data )
   {
      stackList.insertAtFront( data );
   } // end function push

   // pop calls stackList object's removeFromFront member function
   bool pop( STACKTYPE &data )
   {
      return stackList.removeFromFront( data );
   } // end function pop

   // isStackEmpty calls stackList object's isEmpty member function
   bool isStackEmpty() const
   {
      return stackList.isEmpty();
   } // end function isEmpty

   // printStack calls stackList object's print member function
   void printStack() const
   {
      stackList.print();
   } // end function printStack

private:
   List< STACKTYPE > stackList; // composed List object
}; // end class Stack
#endif
```

图 20.15 | 含组合 List 对象的 Stack 类模板。（第1部分，共2部分。）

图 20.15 | 含组合 List 对象的 Stack 类模板。（第2部分，共2部分。）

## 20.6 队列

队列类似于超市结账队伍——排在第一位的人先得到服务，其他顾客从队尾加入队伍并等待服务。队列节点只从队列头部删除，并且只插入到队列尾部。因此，队列被称为先进先出（FIFO）数据结构。插入和删除操作称为入队（enqueue）和出队（dequeue）。

队列在计算机系统中有许多应用。具有单处理器的计算机一次只能服务一个用户。其他用户的条目被放入队列。随着用户得到服务，每个条目逐渐前进到队列前端。队列前端的条目是下一个接受服务的条目。

队列还用于支持打印假脱机。例如，一台打印机可能由网络中的所有用户共享。许多用户可以将打印作业发送到打印机，即使打印机已经忙碌。这些打印作业被放入队列，直到打印机可用。一个称为假脱机程序的程序管理该队列，以确保每当一个打印作业完成时，下一个打印作业被发送到打印机。

数据包在计算机网络中也会在队列中等待。每当一个数据包到达网络节点时，必须沿着通往该包最终目的地的路径将其路由到网络上的下一个节点。路由节点一次路由一个数据包，因此额外的数据包会入队，直到路由器能够路由它们。

计算机网络中的文件服务器处理来自整个网络中许多客户端的文件访问请求。服务器服务客户端请求的能力有限。当超出该容量时，客户端请求会在队列中等待。

图 20.16–20.17 的程序通过私有继承（第9行）图 20.4 的 List 类模板来创建 Queue 类模板（图 20.16）。Queue 具有成员函数 enqueue（第13–16行）、dequeue（第19–22行）、isEmptyQueue（第25–28行）和 printQueue（第31–34行）。这些本质上就是 List 类模板的 insertAtBack、removeFront、isEmpty 和 print 函数。当然，List 类模板还包含其他成员函数，我们不希望它们通过 Queue 类的公共接口变得可访问。因此，当我们指明 Queue 类模板要继承 List 类模板时，我们指定私有继承。这会使 List 类模板的所有成员函数在 Queue 类模板中成为私有成员。当
