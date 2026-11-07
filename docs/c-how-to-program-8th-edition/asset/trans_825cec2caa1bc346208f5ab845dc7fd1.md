
## 商务沟通与谈判技巧

## 课程介绍

本课程旨在帮助学生掌握商务环境下的人际沟通策略与谈判技能，注重理论与实践结合，强化沟通中的临场判断与表达能力。

课程涵盖商务口头表达、非语言沟通、正式场合的演讲陈述、商务谈判流程中的准备、出价、退让与僵局处理等核心环节，适合管理类相关专业学生及职场人士选修。

## 课程信息

- 学分：2.0
- 学时：32
- 开课学期：第4学期

授课教师：王文峰

教师简介：长期从事商务沟通、组织管理与谈判策略方向研究，具有丰富的跨行业企业培训与经济管理教学经验。

![](img/bfd978e7e9b192bab46ec2a89e481263_797_0.png)

注重案例式与情景式教学，鼓励学生在模拟演练中提升沟通应变能力及职业素养。

第 27 和 33 行必须显式使用 `this`，以便编译器能正确解析模板定义中的标识符。**依赖名称**是依赖于模板参数的标识符。例如，对 `removeFromFront` 的调用（第 21 行）依赖于参数 data，而 data 的类型依赖于模板参数 STACK-TYPE。依赖名称的解析在模板实例化时进行。相比之下，像 `List` 超类中的 `isEmpty` 或 `print` 这样不接受参数的函数标识符，是**非依赖名称**。这类标识符通常在定义模板的位置解析。如果模板尚未实例化，那么具有非依赖名称的函数的代码尚不存在，某些编译器会生成编译错误。在第 27 和 33 行显式添加 `this->`，会使对基类成员函数的调用依赖于模板参数，并确保代码能够正确编译。

栈类模板在 main（图 20.14）中用于实例化类型为 `Stack<int>` 的整数栈 `intStack`（第 9 行）。将整数 0 到 2 压入 `intStack`（第 14–18 行），然后从 `intStack` 弹出（第 23–28 行）。程序使用 Stack 类模板创建类型为 `Stack<double>` 的 `doubleStack`（第 30 行）。将值 1.1、2.2 和 3.3 压入 `doubleStack`（第 36–41 行），然后从 `doubleStack` 弹出（第 46–51 行）。

```cpp
// Fig. 20.14: Fig20_14.cpp
// Template Stack class test program.
#include <iostream>
#include "Stack.h" // Stack class definition
using namespace std;

int main()
{
   Stack< int > intStack; // create Stack of ints

   cout << "processing an integer Stack" << endl;

   // push integers onto intStack
   for ( int i = 0; i < 3; ++i )
   {
      intStack.push( i );
      intStack.printStack();
   } // end for

   int popInteger; // store int popped from stack

   // pop integers from intStack
   while ( !intStack.isStackEmpty() )
   {
      intStack.pop( popInteger );
      cout << popInteger << " popped from stack" << endl;
      intStack.printStack();
   } // end while

   Stack< double > doubleStack; // create Stack of doubles
   double value = 1.1;
```

**图 20.14** | 一个简单的栈程序。（第 1 部分，共 2 部分。）

```cpp
cout << "processing a double Stack" << endl;

// push floating-point values onto doubleStack
for ( int j = 0; j < 3; ++j )
{
    doubleStack.push( value );
    doubleStack.printStack();
    value += 1.1;
} // end for

double popDouble; // store double popped from stack

// pop floating-point values from doubleStack
while ( !doubleStack.isStackEmpty() )
{
    doubleStack.pop( popDouble );
    cout << popDouble << " popped from stack" << endl;
    doubleStack.printStack();
} // end while
} // end main
```

```
processing an integer Stack
The list is: 0
The list is: 1 0
The list is: 2 1 0
2 popped from stack
The list is: 1 0
1 popped from stack
The list is: 0
0 popped from stack
The list is empty
processing a double Stack
The list is: 1.1
The list is: 2.2 1.1
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

**图 20.14** | 一个简单的栈程序。（第 2 部分，共 2 部分。）

实现 Stack 类模板的另一种方式是通过*组合*复用 List 类模板。图 20.15 是 Stack 类模板的新实现，其中包含一个名为 `stackList` 的 `List<STACKTYPE>` 对象（第 38 行）。此版本的 Stack 类模板使用图 20.4 中的 `List` 类。要测试这个类，请使用图 20.14 中的驱动程序，但在该文件的第 6 行包含新头文件——`Stackcomposition.h`。对于 `Stack` 类的两个版本，程序输出相同。

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
   } // end function isStackEmpty

   // printStack calls stackList object's print member function
   void printStack() const
   {
      stackList.print();
   } // end function printStack
private:
   List< STACKTYPE > stackList; // composed List object
}; // end of class Stack

#endif
```

**图 20.15** | 带有组合 List 对象的 Stack 类模板。

## 20.6 队列

一个**队列**类似于超市结账队伍——排在队伍中的*第一个*人*最先*得到服务，其他顾客在*队尾*进入队伍并*等待*接受服务。队列节点仅从队列头部移除，并且仅插入到队列尾部。因此，队列被称为先进先出（FIFO）数据结构。插入和移除操作分别称为**入队**（enqueue）和**出队**（dequeue）。

队列在计算机系统中有许多应用。具有单个处理器的计算机一次只能服务一个用户。其他用户的条目被放入队列。随着用户接受服务，每个条目逐渐前进到队列前端。队列前端的条目是下一个接受服务的条目。

队列还用于支持**打印后台处理**。例如，一台打印机可能由网络中的所有用户共享。许多用户可以在打印机已经忙碌时仍向打印机发送打印作业。这些打印作业被放入队列，直到打印机可用。一个称为**假脱机程序**（spooler）的程序管理该队列，以确保每当一个打印作业完成时，下一个打印作业被发送到打印机。

信息包在计算机网络中也会在队列中等待。每当一个包到达网络节点时，必须沿通往该包最终目的地的路径将其路由到网络上的下一个节点。路由节点一次路由一个包，因此额外的包会入队，直到路由器能够路由它们。

计算机网络中的文件服务器处理来自整个网络中许多客户端的文件访问请求。服务器服务客户端请求的能力有限。当超过该容量时，客户端请求会在队列中等待。

图 20.16–20.17 的程序通过私有继承（第 9 行）List 类模板（图 20.4）来创建 Queue 类模板（图 20.16）。Queue 具有成员函数 `enqueue`（第 13–16 行）、`dequeue`（第 19–22 行）、`isQueueEmpty`（第 25–28 行）和 `printQueue`（第 31–34 行）。这些本质上就是 List 类模板的 `insertAtBack`、`removeFromFront`、`isEmpty` 和 `print` 函数。当然，List 类模板还包含其他成员函数，我们不希望这些函数通过 Queue 类的公共接口被访问。因此，当我们指明 Queue 类模板要继承 List 类模板时，我们指定私有继承。这使得 List 类模板的所有成员函数在 Queue 类模板中成为私有。当我们实现 Queue 的成员函数时，让每个函数调用 List 类的相应成员函数——`enqueue` 调用 `insertAtBack`（第 15 行），`dequeue` 调用 `removeFromFront`（第 21 行），`isQueueEmpty` 调用 `isEmpty`（第 27 行），`printQueue` 调用 `print`（第 33 行）。与图 20.13 中的 Stack 示例一样，这种委托需要在 `isQueueEmpty` 和 `printQueue` 中显式使用 `this` 指针，以避免编译错误。

```cpp
1  // Fig. 20.16: Queue.h
2  // Template Queue class definition derived from class List.
3  #ifndef QUEUE_H
4  #define QUEUE_H
5
6  #include "List.h" // List class definition
7
8  template <typename QUEUETYPE >
9  class Queue : private List< QUEUETYPE >
10 {
11   public:
```

**图 20.16** | Queue 类模板定义。（第 1 部分，共 2 部分。）

