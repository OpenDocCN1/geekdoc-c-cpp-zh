

## 栈

栈是一种后进先出的数据结构；也就是说，数据项的取出顺序与它们放入栈中的顺序相反。

## 压栈与弹栈

向栈数据结构中添加数据项被称为将数据项压入栈。 从栈中移除数据项被称为将该项弹出栈。

## 自测练习

- 13. 给出模板类 Stack 的成员函数 push 的定义，该模板类描述于图 17.17 和 17.19 中。
- 14. 给出模板类 Stack 的拷贝构造函数的定义，该模板类描述于图 17.17 和 17.19 中。
- 15. 给出模板类 Stack 的重载赋值运算符的定义，该模板类描述于图 17.17 和 17.19 中。

## 示例：一个队列模板类

栈是一种后进先出的数据结构。 另一种常见的数据结构是队列，它以先进先出的方式处理数据。 队列可以用链表实现，其方式与我们对 Stack 模板类的实现类似。 然而，队列需要在链表的头部和链表的末尾各有一个指针，因为操作发生在两个位置。 从链表头部移除节点比从另一端移除节点更容易。 因此，我们的实现将从链表头部移除节点（我们现在称其为列表的前端），并将节点添加到列表的另一端，我们现在称其为列表的后端（或队列的后端）。

队列模板类的定义在图 17.20 中给出。 使用类 Queue 的示例应用程序显示在图 17.21 中。 成员函数的定义留作自测练习（但请记住，如果你在填写细节时遇到任何问题，答案在章节末尾给出）。

## 图 17.20 队列模板类的接口文件（第 1 部分，共 2 部分）

```
1
2 //This is the header file queue.h. This is the interface for the class
3 //Queue, which is a template class for a queue of items of type T.
4 #ifndef QUEUE_H
5 #define QUEUE_H
6 
7 namespace QueueSavitch
8 {
9   template<class T>
10   class Node
11   {
12   public:
13     Node( T theData, Node<T>* theLink ) : data(theData), link(theLink) {}
14     Node<T>* getLink( ) const { return link; }
15     const T getData( ) const { return data; }
16     void setData(const T& theData) { data = theData; }
17     void setLink(Node<T>* pointer) { link = pointer; }
18   private:
19     T data;
20     Node<T> *link;
21   };
22 
23   template<class T>
24   class Queue
25   {
26   public:
27     Queue( );
28     //Initializes the object to an empty queue.
29     Queue(const Queue<T>& aQueue);
30     Queue<T>& operator =(const Queue<T>& rightSide);
31     virtual ~Queue( );
32     void add(T item);
33     //Postcondition: item has been added to the back of the queue.
34     T remove( );
35     //Precondition: The queue is not empty.
36     //Returns the item at the front of the queue
37     //and removes that item from the queue.
```

这与我们在图 17.17 中为栈接口给出的模板类 Node 的定义相同。 请参阅“提示：关于命名空间的说明”以讨论这种重复。

你可能更喜欢用 const T& 替换参数类型 T。

拷贝构造函数

析构函数销毁队列并将所有内存归还给自由存储区。

## 图 17.20 队列模板类的接口文件（第 2 部分，共 2 部分）

```
37     bool isEmpty( ) const;
38     //Returns true if the queue is empty. Returns false otherwise.
39     private:
40     Node<T>* front; //Points to the head of a linked list.
41     //Items are removed at the head
42     Node<T>* back;  //Points to the node at the other end of the
43     //linked list.
44     //Items are added at this end.
45     };
46 #endif //QUEUE_H
```

## 图 17.21 使用队列模板类的程序（第 1 部分，共 2 部分）

```
//Program to demonstrate use of the Queue template class.
#include <iostream>
#include "queue.h"
#include "queue.cpp"
using std::cin;
using std::cout;
using std::endl;
using QueueSavitch::Queue;

int main( )
{
    char next, ans;    Contrast this with the similar program using
                       a stack instead of a queue that we gave in
                       Display 17.18.
    do
    {
        Queue<char> q;
        cout << "Enter a line of text:\n";
        cin.get(next);
        while (next != '\n')
        {
            q.add(next);
            cin.get(next);
        }
        cout << "You entered:\n";
        while ( ! q.isEmpty( ) )
            cout << q.remove( );
        cout << endl;
```

## 图 17.21 使用队列模板类的程序（第 2 部分，共 2 部分）

```
26      cout << "Again? (y/n): ";
27      cin >> ans;
28      cin.ignore(10000, '\n');
29  } while (ans != 'n' && ans != 'N');
30
31  return 0;
32 }
```

## 示例对话

```
Enter a line of text:
straw
You entered:
straw
Again?(y/n): y
Enter a line of text:
I love C++
You entered:
I love C++
Again?(y/n): n
```

## 队列

队列是一种*先进先出*的数据结构；也就是说，数据项是从队列中以与它们添加到队列中相同的顺序移除的。

## 提示：关于命名空间的说明

请注意，命名空间 StackSavitch（图 17.17）和 QueueSavitch（图 17.20）都定义了一个名为 Node 的模板类。 事实证明，Node 的两个定义是相同的，但这里讨论的要点无论两个定义是否相同都适用。 C++ 不允许你两次定义相同的标识符，即使两个定义相同，除非这两个名称以某种方式区分开。 在这种情况下，两个定义是允许的，因为它们位于两个不同的命名空间中。 甚至可以在同一个程序中使用 Stack 模板类和 Queue 模板类。 然而，你应该使用

```
using StackSavitch::Stack;
using QueueSavitch::Queue;
```

of the function f, you can access private members of C just as you can in the definitions of member functions of C. A class can be a friend of another class in the same way that a function can be a friend of a class. If the class F is a friend of the class C, then every member function of the class F is a friend of the class C. Thus, if, for example, the Queue template class were a friend of the Node template class, then the private link member variables would be directly available in the definitions of the member functions of Queue. The details are outlined in Display 17.22.

## 图 17.22 节点类的友元队列模板类（第 1 部分，共 2 部分）

```
//This is the header file queue.h. This is the interface for the class
//Queue, which is a template class for a queue of items of type T.
#ifndef QUEUE_H
#define QUEUE_H

namespace QueueSavitch
{
    template<class T>
    class Queue;

    template<class T>
    class Node
    {
    public:
        Node(T theData, Node<T>* theLink) : data(theData),
                                            link(theLink){}
        friend class Queue<T>;
    private:
        T data;
        Node<T> *link;
    };

    template<class T>
    class Queue
    {
        //The definition of the template class Queue is identical to the one given in Display 17.20.
        //However, the definitions of the member functions will be different from the ones we gave
        //in the self-Test Exercises for the nonfriend version of Queue.
    }
    //QueueSavitch

#endif //QUEUE_H
#include <iostream>
#include <cstdlib>
#include "queue.h"
using std::cout;
namespace QueueSavitch
```

前向声明。 不要忘记分号。

这是图 17.20 中给出的另一种方法。 在这个版本中，Queue 模板类是 Node 模板类的友元。

如果 Node<T> 仅在友元类 Queue<T> 的定义中使用，则不需要变异访问函数。

实现文件将包含这些定义以及其他成员函数的定义，同样修改以允许通过名称访问节点的 link 和 data 成员变量。

