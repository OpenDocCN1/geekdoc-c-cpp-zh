

```cpp
public:
    ArrayStack(); // Default constructor
    bool isEmpty() const;
    bool push(const ItemType& newEntry);
    bool pop();
    ItemType peek() const;
}; // end ArrayStack
#include "ArrayStack.cpp"
#endif
```

前一个头文件中声明的方法的实现如清单 7-2 所示。这些定义很简单，但请注意，方法 peek 使用 assert 来强制执行其前提条件，即栈中至少包含一个条目。本章稍后，我们将修改 peek，如果客户端在栈为空时调用它，则抛出异常。

### 清单 7-2 基于数组的栈的实现文件

```cpp
/** @file ArrayStack.cpp */
#include <cassert> // For assert
#include "ArrayStack.h" // Header file
template<class ItemType>
ArrayStack<ItemType>::ArrayStack() : top(-1)
{ } // end default constructor
// Copy constructor and destructor are supplied by the compiler
template<class ItemType>
bool ArrayStack<ItemType>::isEmpty() const
{
   return top < 0;
} // end isEmpty
template<class ItemType>
bool ArrayStack<ItemType>::push(const ItemType& newEntry)
{
   bool result = false;
   if (top < MAX_STACK - 1) // Does stack have room for newEntry?
   {
      top++;
      items[top] = newEntry;
      result = true;
   } // end if
   return result;
} // end push
template<class ItemType>
bool ArrayStack<ItemType>::pop()
{
    bool result = false;
    if (!isEmpty())
    {
        top--;
        result = true;
    } // end if
    return result;
} // end pop

template<class ItemType>
ItemType ArrayStack<ItemType>::peek() const
{
    assert (!isEmpty()); // Enforce precondition

    // Stack is not empty; return top
    return items[top];
} // end peek
// end of implementation file
```

使用栈的程序可以如下开始：

```cpp
#include <iostream>
#include <string>
#include "ArrayStack.h"

using namespace std;

int main()
{
    StackInterface<string>* stackPtr = new ArrayStack<string>();
    string anItem = "";
    cout << "Enter a string: ";
    cin >> anItem; // Read an item
    stackPtr->push(anItem); // Push item onto stack
    ...
```

### 私有数据成员对客户端隐藏

通过将栈实现为类，并将 items 和 top 声明为私有，你可以确保客户端不能违反 ADT 的边界。如果你没有在类中隐藏实现，或者将数组 items 设为公有，客户端可以直接访问 items 中的条目，而不是使用 ADT 栈操作。因此，客户端可以访问栈中的任何条目，而不仅仅是栈顶条目。你可能会觉得这种能力很有吸引力，但实际上它违反了 ADT 栈的规范。如果你确实需要随机访问 ADT 中的所有项目，请不要使用栈！

最后，请注意 push 将 newEntry 作为常量引用参数接收。因此，push 将 newEntry 用作其实际参数的别名，并且不会进行副本。

> **问题 1** 在第 6 章中，第 6.2 节出现的算法涉及字符串。在什么条件下，你会为这些算法中的栈选择基于数组的实现？

## 7.2 基于链接的实现

许多应用程序需要栈的基于链接的实现，以便栈可以动态地增长和缩小。图 7-2 说明了这种实现，其中 topPtr 是指向链接节点头的指针。

与我们为基于数组的实现所做的一样，我们从基于 StackInterface 的头文件开始，如清单 7-3 所示。指针 topPtr 指向第 4 章中我们在 LinkedBag 类实现中使用的 Node 类的一个实例。

由于节点的内存是动态分配的，你必须为基于链接的栈实现编写拷贝构造函数和虚析构函数。如你在第 4 章中所见，如果栈的浅拷贝就足够了，你可以省略拷贝构造函数，在这种情况下，编译器会生成一个执行浅拷贝的拷贝构造函数。基于数组的实现就是这种情况。

如果我们没有为 LinkedStack 类编写自己的拷贝构造函数，编译器生成的拷贝构造函数只会复制指针 topPtr。因此，topPtr 及其副本都将指向相同的链接节点；栈本身不会被复制。你必须编写一个拷贝构造函数，它显式地复制链接栈中的所有节点。

### 图 7-2 栈的基于链接的实现

![](img/288a0c22d14d2450c1e772f228f867b0_271_0.png)

### 清单 7-3 类 LinkedStack 的头文件

```cpp
/** ADT stack: Link-based implementation.
 @file LinkedStack.h */
#ifndef _LINKED_STACK
#define _LINKED_STACK
#include "StackInterface.h"
#include "Node.h"
template<class ItemType>
class LinkedStack : public StackInterface<ItemType>
{
private:
   Node<ItemType>* topPtr; // Pointer to first node in the chain;
                           // this node contains the stack's top
public:
// Constructors and destructor:
   LinkedStack(); // Default constructor
   LinkedStack(const LinkedStack<ItemType>& aStack); // Copy constructor
   virtual ~LinkedStack(); // Destructor
// Stack operations:
   bool isEmpty() const;
   bool push(const ItemType& newItem);
   bool pop() throw( );
   ItemType peek() const;
}; // end LinkedStack
#include "LinkedStack.cpp"
#endif
```

你需要一个显式拷贝构造函数和一个虚析构函数

清单 7-4 给出了 LinkedStack 的实现文件。请注意 LinkedStack 和 LinkedBag（如第 4 章所示）的拷贝构造函数之间的相似之处。

### 清单 7-4 类 LinkedStack 的实现文件

```cpp
/** @file LinkedStack.cpp */
#include <cassert> // For assert
#include "LinkedStack.h" // Header file
template<class ItemType>
LinkedStack<ItemType>::LinkedStack() : topPtr(nullptr)
{ } // end default constructor
template<class ItemType>
LinkedStack<ItemType>::
LinkedStack(const LinkedStack<ItemType>& aStack)
{
   // Point to nodes in original chain
   Node<ItemType>* origChainPtr = aStack.topPtr;

   if (origChainPtr == nullptr)
      topPtr = nullptr;   // Original bag is empty
   else
   {
      // Copy first node
      topPtr = new Node<ItemType>();
      topPtr->setItem(origChainPtr->getItem());

      // Point to first node in new chain
      Node<ItemType>* newChainPtr = topPtr;

      // Copy remaining nodes
      while (origChainPtr != nullptr)
      {
         // Advance original-chain pointer
         origChainPtr = origChainPtr->getNext();

         // Get next item from original chain
         ItemType nextItem = origChainPtr->getItem();

         // Create a new node containing the next item
         Node<ItemType>* newNodePtr = new Node<ItemType>(nextItem);

         // Link new node to end of new chain
         newChainPtr->setNext(newNodePtr);

         // Advance pointer to new last node
         newChainPtr = newChainPtr->getNext();
      }  // end while

      newChainPtr->setNext(nullptr);   // Flag end of chain
   }  // end if
}  // end copy constructor

template<class ItemType>
LinkedStack<ItemType>::~LinkedStack()
{
   // Pop until stack is empty
   while (!isEmpty())
      pop();
}  // end destructor

template<class ItemType>
bool LinkedStack<ItemType>::isEmpty() const
{
   return topPtr == nullptr;
}  // end isEmpty

template<class ItemType>
bool LinkedStack<ItemType>::push(const ItemType& newItem)
{
   Node<ItemType>* newNodePtr = new Node<ItemType>(newItem, topPtr);
   topPtr = newNodePtr;
   newNodePtr = nullptr;

   return true;
} // end push

template<class ItemType>
bool LinkedStack<ItemType>::pop()
{
   bool result = false;
   if (!isEmpty())
   {
      // Stack is not empty; delete top
      Node<ItemType>* nodeToDeletePtr = topPtr;
      topPtr = topPtr->getNext();

      // Return deleted node to system
      nodeToDeletePtr->setNext(nullptr);
      delete nodeToDeletePtr;

      nodeToDeletePtr = nullptr;

      result = true;
   } // end if

   return result;
} // end pop

template<class ItemType>
ItemType LinkedStack<ItemType>::peek() const
{
   assert(!isEmpty()); // Enforce precondition

   // Stack is not empty; return top
   return topPtr->getItem();
} // end peek
// end of implementation file
```

**问题 3** 在第 6 章中，第 6.2 节出现的算法涉及字符串。在什么条件下，你会选择基于链接的实现？

### 注：比较实现

你已经看到了 ADT 栈的两种实现，一种使用数组，另一种使用链接节点来包含栈中的项目。第 4 章第 4.5 节的讨论同样适用于此。如果栈中的项目数不超过数组的固定大小，基于数组的实现是一个合理的选择。例如，当我们读取和更正输入行时，如果系统只允许行长度为 80 个字符，你可以合理地使用静态分配的数组来表示栈。对于可能很大但通常不大的栈，基于数组的实现会浪费存储。在这种情况下，基于链接的实现是更好的选择。

