

这是一个对指向类型为 Node<T> 的节点的指针的引用参数。下面，我们重现了 Display 17.11 中的一个函数声明，以便你可以在上下文中看到此参数类型规范：

template<class T>
void headInsert(Node<T>*& head, const T& theData);

## Display 17.10 链表库的接口文件（第 1 部分，共 2 部分）

//This is the header file listtools.h. This contains type definitions and
//function declarations for manipulating a linked list to store data of any
//type T. The linked list is given as a pointer of type Node<T>* that points
//to the head (first) node of the list. The implementation of the functions
//is given in the file listtools.cpp.
#ifndef LISTTOOLS_H
#define LISTTOOLS_H
namespace LinkedListSavitch
{
template<class T>
class Node
{
public:
Node(const T& theData, Node<T>* theLink) : data(theData), link(theLink){}
Node<T>* getLink() const { return link; }
const T getData() const { return data; }
void setData(const T& theData) { data = theData; }
void setLink(Node<T>* pointer) { link = pointer; }
private:
T data;
Node<T> *link;
};
template<class T>
void headInsert(Node<T>*& head, const T& theData);
//Precondition: The pointer variable head points to
//the head of a linked list.
//Postcondition: A new node containing theData
//has been added at the head of the linked list.
template<class T>
void insert(Node<T>* afterMe, const T& theData);
//Precondition: afterMe points to a node in a linked list.
//Postcondition: A new node containing theData
//has been added after the node pointed to by afterMe.

使用 T 作为参数类型是可以接受的，我们在其中使用了 const T&。我们使用了常量引用参数，因为我们预计 T 经常会是一个类类型。

## Display 17.10 链表库的接口文件（第 2 部分，共 2 部分）

```cpp
34
35    template<class T>
36    void deleteNode(Node<T>** before);
37    //Precondition: The pointer before points to a node that has
38    //at least one node after it in the linked list.
39    //Postcondition: The node after the node pointed to by before
40    //has been removed from the linked list and its storage
41    //returned to the freestore.

42
43    template<class T>
44    void deleteFirstNode(Node<T>*& head);
45    //Precondition: The pointer head points to the first
46    //node in a linked list with at most one node.
47    //Postcondition: The node pointed to by head has been removed
48    //from the linked list and its storage returned to the freestore.

48    template<class T>
49    Node<T>* search(Node<T>* head, const T& target);
50    //Precondition: The pointer points to the head of a linked list.
51    //The pointer variable in the last node is NULL.
52    //== is defined for type T.
53    //(== is used as the criterion for being equal.)
54    //If the list is empty, then head is NULL.
55    //Returns a pointer that points to the first node that
56    //is equal to the target. If no node equals the target,
57    //then the function returns NULL.
58    }//LinkedListSavitch

59    #endif //LISTTOOLS_H
```

## Display 17.11 链表库的实现文件（第 1 部分，共 2 部分）

```cpp
1    //This is the implementation file listtools.cpp. This file contains
2    //function definitions for the functions declared in listtools.h.
3    #include <cstddef>
4    #include "listtools.h"

5    namespace LinkedListSavitch
6    {
7        template<class T>
8        void headInsert(Node<T>*& head, const T& theData)
9        {
10           head = new Node<T>(theData, head);
11       }
```

## Display 17.11 链表库的实现文件（第 2 部分，共 2 部分）

```
12  template<class T>
13  void insert(Node<T>* afterMe, const T& theData)
14  {
15      afterMe->setLink(new Node<T>(theData, afterMe->getLink()));
16  }
17
18  template<class T>
19  void deleteNode(Node<T>* before)
20  {
21      Node<T>* discard;
22      discard = before->getLink();
23      before->setLink(discard->getLink());
24      delete discard;
25  }
26
27  template<class T>
28  void deleteFirstNode(Node<T>*& head)
29  {
30      Node<T>* discard;
31      discard = head;
32      head = head->getLink();
33      delete discard;
34  }
35
36  //Uses cstddef:
37  template<class T>
38  Node<T>* search(Node<T>* head, const T& target)
39  {
40      Node<T>* here = head;
41
42      if (here == NULL) //if empty list
43      {
44          return NULL;
45      }
46      else
47      {
48          while (here->getData() != target && here->getLink() != NULL)
49              here = here->getLink();
50
51          if (here->getData() == target)
52              return here;
53          else
54              return NULL;
55      }
56  }//LinkedListSavitch
```

## 链表应用

> 但如今在前的，将要在后；在后的，将要在前。

马太福音 19:30

先来后到

一个常见的（更世俗的）说法

链表有 Display 17.12 应用。本节仅介绍其使用的两个小例子，即每个都使用链表作为其实现核心的两个类模板定义。

## 示例

## 一个栈模板类

栈是一种以与数据存储顺序相反的顺序检索数据的数据结构。假设你将字母 'A'、'B' 然后是 'C' 放入栈中。当你从栈中取出这些字母时，它们将被按 'C'、然后是 'B'、然后是 'A' 的顺序移除。栈的这种使用在 Display 17.12 中进行了图解。如图所示，你可以将栈想象成地面上的一个洞。为了从栈中取出某样东西，你必须先移除上面覆盖它的物品。因此栈通常被称为后进先出数据结构。

## 栈

栈是一种后进先出数据结构；也就是说，数据项是以与它们放入栈的顺序相反的顺序检索的。

栈用于许多语言处理任务。第 13 章讨论了计算机系统如何使用栈来跟踪 C++ 函数调用。然而，这里我们只关注一个非常简单的应用。我们的目标在这个例子中是展示如何使用链表技术来实现特定的数据结构，例如栈。

我们栈类的接口在 Display 17.13 中给出。这是一个模板类，具有类型参数 T 用于栈中存储的数据类型。一个存储在栈中的项是类型为 T 的值。在我们展示的示例中，T 被字符类型 char 替换。然而，在大多数应用中，存储在栈中的项很可能是一个结构体或类对象。存储在栈中的每个记录（类型为 T 的项）称为栈帧，这就解释了为什么我们在栈模板类的定义中偶尔使用 stackFrame 作为标识符名称。可以对栈执行两个基本

## Display 17.12 一个栈

pushing

![](img/9505fd46e120aa9c1406715936ff6251_709_0.png)

popping

![](img/9505fd46e120aa9c1406715936ff6251_709_1.png)

## Display 17.13 栈模板类的接口文件（第 1 部分，共 2 部分）

```
//This is the header file stack.h. This is the interface for the class
//Stack, which is a template class for a stack of items of type T.
#ifndef STACK_H
#define STACK_H

namespace StackSavitch
{
  template<class T>
  class Node
  {
   public:
     Node(T theData, Node<T>* theLink) : data(theData), link(theLink){}
     Node<T>* getLink() const { return link; }
     const T getData() const { return data; }
     void setData(const T& theData) { data = theData; }
     void setLink(Node<T>* pointer) { link = pointer; }
   private:
     T data;
     Node<T> *link;
  };

  template<class T>
  class Stack
  {
```

你可能更喜欢用 const T& 替换参数类型 T。

## Display 17.13 栈模板类的接口文件（第 2 部分，共 2 部分）

```
23 public:
24 Stack();
25 //Initializes the object to an empty stack.
26 Stack(const Stack<T>& aStack); // Copy constructor
27 Stack<T>& operator =(const Stack<T>& rightSide);
28 virtual ~Stack(); // The destructor destroys the stack and returns all the memory to the freestore.
29 void push(T stackFrame);
30 //Postcondition: stackFrame has been added to the stack.
31 T pop();
32 //Precondition: The stack is not empty.
33 //Returns the top stack frame and removes that top
34 //stack frame from the stack.
35 bool isEmpty() const;
36 //Returns true if the stack is empty. Returns false otherwise.
37 private:
38 Node<T> *top;
39 };
40 }//StackSavitch
41 #endif //STACK_H
```

操作：向栈中添加一项以及从栈中移除一项。向栈中添加一项，我们称执行此操作的成员函数为 push。从栈中弹出一项称为弹出操作，因此我们称执行此操作的成员函数为 pop。

名称 push 和 pop 源自对栈的一种特定可视化方式。栈类似于有时用于在食堂存放盘子的机制。该机制将盘子存储在台面上的一个孔中。盘子下面有一个弹簧，其张力调整为只有最上面的盘子突出在台面之上。如果这种机制被用作栈数据结构，数据将写在盘子上（这可能会违反某些健康法规，但仍然是一个很好的类比）。要向栈中添加一个盘子，你把它放在其他盘子上面，新盘子的重量会向下压弹簧。当你移除一个盘子时，下面的盘子会弹出。

Display 17.14 显示了一个简单的程序，说明了 Stack 类的使用。该程序一次读取一行文本的一个字符并将字符放入栈中。然后程序一次移除一个字符并将其写入屏幕。因为数据是从

