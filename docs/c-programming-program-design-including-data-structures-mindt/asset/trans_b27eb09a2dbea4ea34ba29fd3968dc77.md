
![](img/b217c421655b51e7494cf3b89bb5432d_1258_0.png)

图 17-15 出栈操作前的栈

图 17-16 展示了出栈操作。

![](img/b217c421655b51e7494cf3b89bb5432d_1258_1.png)

图 17-16 出栈操作

语句

```cpp
temp = stackTop;
```

使 temp 指向栈顶。见图 17-16(a)。接下来，语句

```cpp
stackTop = stackTop->link;
```

使栈的第二个元素成为栈顶元素。见图 17-16(b)。

最后，语句

```cpp
delete temp;
```

释放 **temp** 所指向的内存。见图 17-16(c)。

函数 pop 的定义如下：

```cpp
template <class Type>
void linkedStackType<Type>::pop()
{
        nodeType<Type> *temp;    //pointer to deallocate memory

        if (stackTop != nullptr)
        {
                temp = stackTop;        //set temp to point to the top node

                stackTop = stackTop->link;        //advance stackTop to the
                                                  //next node

                delete temp;        //delete the top node
        }
        else
                cout << "Cannot remove from an empty stack." << endl;
}//end pop
```

## 复制栈

函数 **copyStack** 生成栈的完全相同副本。其定义类似于第16章给出的链表函数 **copyList** 的定义。函数 **copyStack** 的定义如下：

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
                current = otherStack.stackTop;  //set current to point
                                                //to the stack to be copied

                //copy the stackTop element of the stack
                stackTop = new nodeType<Type>;  //create the node

                stackTop->info = current->info; //copy the info
                stackTop->link = nullptr;    //set the link field of the
                                              //node to nullptr
                last = stackTop;              //set last to point to the node
                current = current->link;      //set current to point to
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
}//end copyStack
```

### 构造函数和析构函数

我们已经讨论了默认构造函数。为了完成栈操作的实现，接下来给出实现复制构造函数、析构函数以及重载赋值运算符的函数的定义。（这些函数类似于第16章中讨论的链表函数。）

```cpp
//copy constructor
template <class Type>
linkedStackType<Type>::linkedStackType
                         (const linkedStackType<Type>& otherStack)
{
    stackTop = nullptr;
    copyStack(otherStack);
}//end copy constructor

//destructor
template <class Type>
linkedStackType<Type>::~linkedStackType()
{
    initializeStack();
}//end destructor
```

### 重载赋值运算符（=）

为类 `linkedStackType` 重载赋值运算符的函数的定义如下：

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

前面讨论的栈的定义以及实现栈操作的函数是通用的。此外，与栈的数组表示一样，在栈的链式表示中，我们必须将栈的定义和实现栈操作的函数一起放在一个（头）文件中。客户端程序可以通过 include 语句包含这个头文件。

例17-3说明了如何在程序中使用 linkedStack 对象。

### 例17-3

假设类 `linkedStackType` 的定义以及实现栈操作的函数都包含在头文件 `"linkedStack.h"` 中。

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
    stack.push(28);
    stack.push(94);
    stack.push(37);

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

//Use the assignment operator to copy the elements
//of stack into otherStack
otherStack = stack;

cout << "Testing the copy constructor." << endl;

testCopy(otherStack);

cout << "After the copy constructor, otherStack: " << endl;

while (!otherStack.isEmptyStack())
{
    cout << otherStack.top() << endl;
    otherStack.pop();
}
return 0;
}

//Function to test the copy constructor
void testCopy(linkedStackType<int> OStack)
{
    cout << "Stack in the function testCopy:" << endl;

    while (!OStack.isEmptyStack())
    {
        cout << OStack.top() << endl;
        OStack.pop();
    }
}
```

### 示例运行：

```text
After the assignment operator, newStack:
37
94
28
Testing the copy constructor.
Stack in the function testCopy:
37
94
28
After the copy constructor, otherStack:
37
94
28
```

## 从 `class unorderedLinkedList` 派生的栈

如果我们将栈的 push 函数与第16章讨论的通用列表的 insertFirst 函数进行比较，就会发现实现这些操作的算法是相似的。比较其他函数——例如 initializeStack 和 initializeList、isEmptyList 和 isEmptyStack 等——可以看出，类 linkedStackType 可以从类 linkedListType 派生。此外，函数 pop 和 isFullStack 可以像上一节那样实现。注意，类 linkedListType 是抽象的，并没有实现所有操作。然而，类 unorderedLinkedListType 派生自类 linkedListType，并提供了类 linkedListType 的抽象函数的定义。因此，我们可以从类 unorderedLinkedListType 派生类 linkedStackType。接下来，我们定义从类 unorderedLinkedList 派生的类 linkedStackType。同时也给出实现栈操作的函数的定义。

```cpp
#include <iostream>
#include "unorderedLinkedList.h"

using namespace std;

template <class Type>
class linkedStackType: public unorderedLinkedList<Type>
{
public:
    void initializeStack();
    bool isEmptyStack() const;
    void push(const Type& newItem);
    Type top() const;
    void pop();
};

template <class Type>
void linkedStackType<Type>::initializeStack()
{
    unorderedLinkedList<Type>::initializeList();
}

template <class Type>
bool linkedStackType<Type>::isEmptyStack() const
{
    return unorderedLinkedList<Type>::isEmptyList();
}

template <class Type>
bool linkedStackType<Type>::isFullStack() const
{
    return false;
}

template <class Type>
void linkedStackType<Type>::push(const Type& newElement)
{
    unorderedLinkedList<Type>::insertFirst(newElement);
}

template <class Type>
Type linkedStackType<Type>::top() const
{
    return unorderedLinkedList<Type>::front();
}

template <class Type>
void linkedStackType<Type>::pop()
{
    nodeType<Type> *temp;

    temp = first;
    first = first->link;
    delete temp;
}
```

## 栈的应用：后缀表达式计算器

编写算术表达式的常用记法（我们在小学学到的记法）称为 **中缀表示法**，其中运算符写在操作数之间。例如，在表达式 $a + b$ 中，运算符 + 位于操作数 $a$ 和 $b$ 之间。在中缀表示法中，运算符具有优先级。也就是说，我们必须从左到右计算表达式，并且乘法和除法的优先级高于加法和减法。如果我们想以不同的顺序计算表达式，就必须使用括号。例如，在表达式 $a + b * c$ 中，我们先用操作数 $b$ 和 $c$ 计算 *，然后用操作数 $a$ 和 $b * c$ 的结果计算 +。

20世纪20年代初，波兰数学家扬·武卡谢维奇（Jan Lukasiewicz）发现，如果把运算符写在操作数之前（**前缀表示法**或**波兰表示法**；例如 $+\ a\ b$），就可以省略括号。20世纪50年代末，澳大利亚哲学家、早期计算机科学家查尔斯·L·汉布林（Charles L. Hamblin）提出了一种运算符跟在操作数之后的方案（后缀运算符），从而产生了 **逆波兰表示法**。其优点是运算符按计算所需的顺序出现。

例如，表达式

$a + b * c$

的后缀表达式为

$a\ b\ c\ *\ +$

下面的示例展示了各种中缀表达式及其等价的后缀表达式。
