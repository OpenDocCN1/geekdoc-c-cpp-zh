
```cpp
template <class Type>
stackType<Type>::stackType(int stackSize)
{
    if (stackSize <= 0)
    {
        cout << "Size of the array to hold the stack must "
             << "be positive." << endl;
        cout << "Creating an array of size 100." << endl;

        maxStackSize = 100;
    }
    else
        maxStackSize = stackSize;    //set the stack size to
                                     //the value specified by
                                     //the parameter stackSize

    stackTop = 0;                    //set stackTop to 0
    list = new Type[maxStackSize];   //create the array to
                                     //hold the stack elements
}//end constructor
```

### 复制构造函数

当栈对象作为（值）参数传递给函数时，会调用复制构造函数。它将实参的成员变量值复制到形参对应的成员变量中。其定义如下：

```cpp
template <class Type>
stackType<Type>::stackType(const stackType<Type>& otherStack)
{
    list = nullptr;

    copyStack(otherStack);
}//end copy constructor
```

### 重载赋值运算符（=）

回想一下，对于带有指针成员变量的类，必须显式重载赋值运算符。为 stackType 类重载赋值运算符的函数定义如下：

```cpp
template <class Type>
const stackType<Type>& stackType<Type>::operator=
                  (const stackType<Type>& otherStack)
{
    if (this != &otherStack) //avoid self-copy
        copyStack(otherStack);

    return *this;
} //end operator=
```

### 栈头文件

既然你已经知道如何实现栈操作，就可以将类定义与实现栈操作的函数定义放在一起，创建栈头文件。为完整起见，接下来描述该头文件。（为节省篇幅，仅展示类定义；不提供文档说明。）假设包含 `class stackType` 定义的头文件名为 `myStack.h`。我们将在任何使用栈的程序中引用该头文件。

```cpp
//Header file: myStack.h

#ifndef H_StackType
#define H_StackType

#include <iostream>
#include <cassert>

#include "stackADT.h"

using namespace std;

template <class Type>
class stackType: public stackADT<Type>
{
public:
    const stackType<Type>& operator=(const stackType<Type>&);

    void initializeStack();

    bool isEmptyStack() const;

    bool isFullStack() const;

    void push(const Type& newItem);

    Type top() const;

    void pop();

    stackType(int stackSize = 100);

    stackType(const stackType<Type>& otherStack);

    ~stackType();

private:
    int maxStackSize;  //variable to store the maximum stack size
    int stackTop;      //variable to point to the top of the stack
    Type *list;        //pointer to the array that holds the
                       //stack elements

    void copyStack(const stackType<Type>& otherStack);
};

template <class Type>
void stackType<Type>::initializeStack()
{
    stackTop = 0;
}//end initializeStack

template <class Type>
bool stackType<Type>::isEmptyStack() const
{
    return (stackTop == 0);
}//end isEmptyStack

template <class Type>
bool stackType<Type>::isFullStack() const
{
    return (stackTop == maxStackSize);
} //end isFullStack

template <class Type>
void stackType<Type>::push(const Type& newItem)
{
    if (!isFullStack())
    {
        list[stackTop] = newItem;     //add newItem to the
                                      //top of the stack
        stackTop++; //increment stackTop
    }
    else
        cout << "Cannot add to a full stack." << endl;
}//end push

template <class Type>
Type stackType<Type>::top() const
{
    assert(stackTop != 0);             //if stack is empty,
                                       //terminate the program
    return list[stackTop - 1];          //return the element of the
                                       //stack indicated by
                                       //stackTop - 1
}//end top

template <class Type>
void stackType<Type>::pop()
{
    if (!isEmptyStack())
        stackTop--;                    //decrement stackTop
    else
        cout << "Cannot remove from an empty stack." << endl;
}//end pop

template <class Type>
stackType<Type>::stackType(int stackSize)
{
    if (stackSize <= 0)
    {
        cout << "Size of the array to hold the stack must "
             << "be positive." << endl;
        cout << "Creating an array of size 100." << endl;

        maxStackSize = 100;
    }
    else
        maxStackSize = stackSize;    //set the stack size to
                                     //the value specified by
                                     //the parameter stackSize

    stackTop = 0;                    //set stackTop to 0
    list = new Type[maxStackSize];   //create the array to
                                     //hold the stack elements
}//end constructor

template <class Type>
stackType<Type>::~stackType()         //destructor
{
    delete [] list;                  //deallocate the memory occupied
                                     //by the array
}//end destructor

template <class Type>
void stackType<Type>::copyStack(const stackType<Type>& otherStack)
{
    delete [] list;
    maxStackSize = otherStack.maxStackSize;
    stackTop = otherStack.stackTop;

    list = new Type[maxStackSize];

             //copy otherStack into this stack
    for (int j = 0; j < stackTop; j++)
        list[j] = otherStack.list[j];
} //end copyStack

template <class Type>
stackType<Type>::stackType(const stackType<Type>& otherStack)
{
    list = nullptr;

    copyStack(otherStack);
}//end copy constructor

template <class Type>
const stackType<Type>& stackType<Type>::operator=
                         (const stackType<Type>& otherStack)
{
    if (this != &otherStack)  //avoid self-copy
        copyStack(otherStack);

    return *this;
} //end operator=

#endif
```

## 示例 17-1

在给出编程示例之前，让我们先编写一个使用 `class` stackType 的简单程序，并测试一些栈操作。其中，我们将测试赋值运算符和复制构造函数。该程序及其输出如下：

```cpp
//Program to test the various operations of a stack

#include <iostream>
#include "myStack.h"

using namespace std;

void testCopyConstructor(stackType<int> otherStack);

int main()
{
        stackType<int> stack(50);
        stackType<int> copyStack(50);
        stackType<int> dummyStack(100);

        stack.initializeStack();
        stack.push(23);
        stack.push(45);
        stack.push(38);
        copyStack = stack;  //copy stack into copyStack

        cout << "The elements of copyStack: ";

        while (!copyStack.isEmptyStack())  //print copyStack
        {
                cout << copyStack.top() << " ";
                copyStack.pop();
        }
        cout << endl;

        copyStack = stack;
        testCopyConstructor(stack);  //test the copy constructor

        if (!stack.isEmptyStack())
                cout << "The original stack is not empty." << endl
                     << "The top element of the original stack: "
                     << copyStack.top() << endl;

        dummyStack = stack;  //copy stack into dummyStack
        cout << "The elements of dummyStack: ";

        while (!dummyStack.isEmptyStack())  //print dummyStack
        {
            cout << dummyStack.top() << " ";
            dummyStack.pop();
        }
        cout << endl;

        return 0;
}

void testCopyConstructor(stackType<int> otherStack)
{
    if (!otherStack.isEmptyStack())
        cout << "otherStack is not empty." << endl
             << "The top element of otherStack: "
             << otherStack.top() << endl;
}
```

## 示例运行

```text
The elements of copyStack: 38 45 23
otherStack is not empty.
The top element of otherStack: 38
The original stack is not empty.
The top element of the original stack: 38
The elements of dummyStack: 38 45 23
```

建议你逐步演练该程序。

## 编程示例：最高 GPA

![](img/d0be7fc6d804b63484835c6c8bc67a07_1234_0.png)

在本示例中，我们编写一个 C++ 程序，读取一个数据文件，其中包含每位学生的 GPA 及其后的学生姓名。然后，程序打印最高 GPA 以及所有获得该 GPA 的学生姓名。该程序只扫描输入文件一次。此外，我们假设班级中最多有 100 名学生。

**输入** 程序读取一个输入文件，其中包含每位学生的 GPA，其后是学生姓名。示例数据如下：

```text
3.4 Randy
3.2 Kathy
2.5 Colt
3.4 Tom
3.8 Ron
3.8 Mickey
3.6 Peter
```

