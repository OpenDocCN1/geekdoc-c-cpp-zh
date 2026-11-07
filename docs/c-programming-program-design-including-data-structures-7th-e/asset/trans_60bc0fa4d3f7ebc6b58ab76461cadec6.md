
```cpp
{
    return (stackTop == nullptr);
} //end isEmptyStack

template <class Type>
bool linkedStackType<Type>::isFullStack() const
{
    return false;
} //end isFullStack
```

回顾一下，在栈的链式实现中，函数 isFullStack 并不适用，因为从逻辑上讲，栈永远不会满。但是，你必须提供它的定义，因为它在父类 `stackADT` 中作为抽象函数包含。

## 初始化栈

操作 initializeStack 将栈重新初始化为空状态。由于栈中可能包含一些元素，并且我们使用的是栈的链式实现，因此必须释放栈元素占用的内存，并将 stackTop 设置为 `nullptr`。该函数的定义如下：

```cpp
template <class Type>
void linkedStackType<Type>::initializeStack()
{
    nodeType<Type> *temp; //pointer to delete the node

    while (stackTop != nullptr)   //while there are elements in
                                  //the stack
    {
        temp = stackTop;          //set temp to point to the
                                   //current node
        stackTop = stackTop->link; //advance stackTop to the
                                    //next node
        delete temp;               //deallocate memory occupied by temp
    }
} //end initializeStack
```

接下来，我们考虑 push、top 和 pop 操作。从图 17-12(b) 可以清楚地看出，在 push 的情况下，newElement 将被添加到 stackTop 所指向的链表的开头。在 pop 的情况下，stackTop 所指向的节点将被删除。在这两种情况下，指针 stackTop 的值都会更新。top 操作返回 stackTop 所指向节点的 info。

## 入栈

考虑图 17-13 所示的栈。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1243_0.png)

**图 17-13**  入栈操作前的栈

图 17-14 展示了入栈操作的步骤。（假设要入栈的新元素是 'D'。）

![](img/d0be7fc6d804b63484835c6c8bc67a07_1243_1.png)

**图 17-14**  入栈操作

以下语句：

```cpp
newNode = new nodeType<Type>(); //create the new node
newNode->info = newElement;
```

创建一个节点，将该节点的地址存入变量 `newNode`，并将 `newElement` 存入 `newNode` 的 `info` 字段。见图 17-14(a)。

以下语句：

```cpp
newNode->link = stackTop;
```

将 `newNode` 插入到栈顶，如图 17-14(b) 所示。

最后，以下语句：

```cpp
stackTop = newNode;
```

更新 `stackTop` 的值，从而得到图 17-14(c)。

函数 push 的定义如下：

```cpp
template <class Type>
void linkedStackType<Type>::push(const Type& newElement)
{
    nodeType<Type> *newNode;  //pointer to create the new node

    newNode = new nodeType<Type>; //create the node

    newNode->info = newElement; //store newElement in the node
    newNode->link = stackTop; //insert newNode before stackTop
    stackTop = newNode;        //set stackTop to point to the
                               //top node
} //end push
```

在将元素入栈之前，我们不需要检查栈是否已满，因为在这种实现中，从逻辑上讲，栈永远不会满。

## 返回栈顶元素

返回栈顶元素的操作非常直接。其定义如下：

```cpp
template <class Type>
Type linkedStackType<Type>::top() const
{
    assert(stackTop != nullptr); //if stack is empty,
                                 //terminate the program

    return stackTop->info;        //return the top element
} //end top
```

## 出栈

现在考虑出栈操作，它删除栈顶元素。考虑图 17-15 所示的栈。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1245_0.png)

**图 17-15** 出栈操作前的栈

图 17-16 展示了出栈操作。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1245_1.png)

**图 17-16** 出栈操作

以下语句：

```cpp
temp = stackTop;
```

使 temp 指向栈顶。见图 17-16(a)。接下来，以下语句：

```cpp
stackTop = stackTop->link;
```

使栈的第二个元素成为栈顶元素。见图 17-16(b)。

最后，以下语句：

```cpp
delete temp;
```

释放 temp 所指向的内存。见图 17-16(c)。

函数 pop 的定义如下：

```cpp
template <class Type>
void linkedStackType<Type>::pop()
{
    nodeType<Type> *temp;    //pointer to deallocate memory

    if (stackTop != nullptr)
    {
        temp = stackTop;    //set temp to point to the top node

        stackTop = stackTop->link;    //advance stackTop to the
                                      //next node
        delete temp;    //delete the top node
    }
    else
        cout << "Cannot remove from an empty stack." << endl;
}//end pop
```

## 复制栈

函数 copyStack 创建栈的完全相同副本。其定义类似于第 16 章给出的链表 copyList 的定义。函数 copyStack 的定义如下：

```cpp
template <class Type>
void linkedStackType<Type>::copyStack
                       (const linkedStackType<Type>& otherStack)
{
    nodeType<Type> *newNode, *current, *last;

    if (stackTop != nullptr) //if stack is nonempty, make it empty
        initializeStack();

    if (otherStack.stackTop == nullptr)
        stackTop = nullptr;
    else
    {
        current = otherStack.stackTop;    //set current to point
                                          //to the stack to be copied

        //copy the stackTop element of the stack
        stackTop = new nodeType<Type>;    //create the node

        stackTop->info = current->info;   //copy the info
        stackTop->link = nullptr; //set the link field of the
                                 //node to nullptr
        last = stackTop;         //set last to point to the node
        current = current->link; //set current to point to
                                 //the next node

            //copy the remaining stack
        while (current != nullptr)
        {
            newNode = new nodeType<Type>;

            newNode->info = current->info;
            newNode->link = nullptr;
            last->link = newNode;
            last = newNode;
            current = current->link;
        }//end while
    }//end else
} //end copyStack
```

## 构造函数和析构函数

我们已经讨论了默认构造函数。为了完成栈操作的实现，接下来给出实现复制构造函数、析构函数以及重载赋值运算符的函数的定义。（这些函数类似于第 16 章中讨论的链表函数。）

```cpp
        //copy constructor
template <class Type>
linkedStackType<Type>::linkedStackType(
                             const linkedStackType<Type>& otherStack)
{
    stackTop = nullptr;
    copyStack(otherStack);
}//end copy constructor
```

```cpp
        //destructor
template <class Type>
linkedStackType<Type>::~linkedStackType()
{
    initializeStack();
}//end destructor
```

## 重载赋值运算符（=）

为类 linkedStackType 重载赋值运算符的函数的定义如下：

```cpp
template <class Type>
const linkedStackType<Type>& linkedStackType<Type>::operator=
                             (const linkedStackType<Type>& otherStack)
{
    if (this != &otherStack) //avoid self-copy
        copyStack(otherStack);

    return *this;
}//end operator=
```

栈的定义以及前面讨论的实现栈操作的函数都是泛型的。此外，正如栈的数组表示一样，在栈的链式表示中，我们必须将栈的定义和实现栈操作的函数一起放入一个（头）文件中。客户端程序可以通过 `include` 语句包含该头文件。

示例 17-3 说明了如何在程序中使用 `linkedStack` 对象。

## 示例 17-3

我们假设 `class linkedStackType` 的定义以及实现栈操作的函数包含在头文件 "linkedStack.h" 中。

```cpp
//This program tests various operations of a linked stack
#include <iostream>
#include "linkedStack.h"

using namespace std;

void testCopy(linkedStackType<int> OStack);

int main()
{
        linkedStackType<int> stack;
        linkedStackType<int> otherStack;
        linkedStackType<int> newStack;

        //Add elements into stack
        stack.push(34);
        stack.push(43);
        stack.push(27);

        //Use the assignment operator to copy the elements
        //of stack into newStack
        newStack = stack;

        cout << "After the assignment operator, newStack: "
             << endl;

        //Output the elements of newStack
        while (!newStack.isEmptyStack())
        {
                cout << newStack.top() << endl;
                newStack.pop();
        }
}
```
