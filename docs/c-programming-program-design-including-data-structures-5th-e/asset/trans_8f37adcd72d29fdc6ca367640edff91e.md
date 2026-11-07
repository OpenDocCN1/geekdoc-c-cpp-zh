
```cpp
        stackTop->link = NULL;   //set the link field of the
                                 //node to NULL
        last = stackTop;         //set last to point to the node
        current = current->link; //set current to point to
                                 //the next node

            //copy the remaining stack
        while (current != NULL)
        {
            newNode = new nodeType<Type>;

            newNode->info = current->info;
            newNode->link = NULL;
            last->link = newNode;
            last = newNode;
            current = current->link;
        }//end while
    }//end else
} //end copyStack
```

## 构造函数和析构函数

我们已经讨论过默认构造函数。为了完成栈操作的实现，接下来给出用于实现复制构造函数和析构函数以及重载赋值运算符的函数定义。（这些函数类似于第 17 章中讨论的链表函数。）

```cpp
        //copy constructor
template <class Type>
linkedStackType<Type>::linkedStackType(
                        const linkedStackType<Type>& otherStack)
{
    stackTop = NULL;
    copyStack(otherStack);
}//end copy constructor

        //destructor
template <class Type>
linkedStackType<Type>::~linkedStackType()
{
    initializeStack();
}//end destructor
```

## 重载赋值运算符 (=)

为类 linkedStackType 重载赋值运算符的函数定义是：

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

前面讨论的栈的定义以及实现栈操作的函数是通用的。此外，正如栈的数组表示一样，在栈的链式表示中，我们必须将栈的定义和实现栈操作的函数一起放在一个（头）文件中。客户端程序可以通过 `include` 语句包含这个头文件。

例 18-3 说明了如何在程序中使用 `linkedStack` 对象。

### 例 18-3

我们假设类 `linkedStackType` 的定义以及实现栈操作的函数包含在头文件 "linkedStack.h" 中。

```cpp
//This program tests various operations of a linked stack
#include <iostream>
#include "linkedStack.h"

using namespace std;

void testCopy(linkedStackType<int> otherStack);

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
void testCopy(linkedStackType<int> otherStack)
{
    cout << "Stack in the function testCopy:" << endl;

    while (!otherStack.isEmptyStack())
    {
        cout << otherStack.top() << endl;
        otherStack.pop();
    }
}
```

### 示例运行：

```text
After the assignment operator, newStack:
27
43
34
Testing the copy constructor.
Stack in the function testCopy:
27
43
34
After the copy constructor, otherStack:
27
43
34
```

## 从 `class unorderedLinkedList` 派生的栈

如果将栈的 push 函数与第 17 章中讨论的用于一般链表的 `insertFirst` 函数进行比较，我们会发现实现这些操作的算法是相似的。对其他函数（如 `initializeStack` 和 `initializeList`、`isEmptyList` 和 `isEmptyStack` 等）的比较表明，`class linkedStackType` 可以从 `class linkedListType` 派生。此外，函数 `pop` 和 `isFullStack` 可以像上一节那样实现。注意，`class linkedListType` 是一个抽象类，并未实现所有操作。然而，`class unorderedLinkedListType` 派生自 `class linkedListType`，并提供了 `class linkedListType` 中抽象函数的定义。因此，我们可以从 `class unorderedLinkedListType` 派生 `class linkedStackType`。

接下来，我们定义从 `class unorderedLinkedList` 派生的 `class linkedStackType`。同时给出实现栈操作的函数定义。

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
    bool isFullStack() const;
    void push(const Type newItem);
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
    nodeType<Type> * temp;

    temp = first;
    first = first->link;
    delete temp;
}
```

## 栈的应用：后缀表达式计算器

书写算术表达式通常使用的记法（我们在小学学到的记法）称为**中缀**记法，其中运算符写在操作数之间。例如，在表达式 *a + b* 中，运算符 + 位于操作数 *a* 和 *b* 之间。在中缀记法中，运算符具有优先级。也就是说，我们必须从左到右计算表达式，并且乘法和除法的优先级高于加法和减法。如果我们想按不同顺序计算表达式，就必须使用圆括号。例如，在表达式 *a + b * c* 中，我们先使用操作数 *b* 和 *c* 计算 *，然后使用操作数 *a* 和 *b * c* 的结果计算 +。

20 世纪 20 年代初，波兰数学家扬·卢卡西维茨发现，如果将运算符写在操作数之前（**前缀**或**波兰表示法**；例如 + a b），则可以省略圆括号。20 世纪 50 年代末，澳大利亚哲学家和早期计算机科学家查尔斯·L·汉布林提出了一种方案，其中运算符跟在操作数之后（后缀运算符），从而产生了**逆波兰表示法**。其优点是运算符按计算所需的顺序出现。

例如，表达式：

*a + b * c*

的后缀表达式为：

*a b c * +*

下面的例子展示了各种中缀表达式及其等价的后缀表达式。

### 例 18-4

| 中缀表达式 | 等价的后缀表达式 |
|---|---|
| `a + b` | `a b +` |
| `a + b * c` | `a b c * +` |
| `a * b + c` | `a b * c +` |
| `(a + b) * c` | `a b + c *` |
| `(a − b) * (c + d)` | `a b − c d + *` |
| `(a + b) * (c − d / e) + f` | `a b + c d e / − * f +` |

卢卡西维茨发现后不久，人们认识到后缀表示法在编译科学中有重要应用。事实上，许多编译器现在首先将算术表达式转换为某种形式的后缀表示法，然后将该后缀表达式转换为机器代码。可以使用以下算法计算后缀表达式：

从左到右扫描表达式。当遇到运算符时，回退以获取所需数量的操作数，执行该运算，然后继续。

考虑以下后缀表达式：

`6 3 + 2 * =`

让我们使用栈和前面的算法来计算这个表达式。图 18–17 展示了该表达式如何求值。

![](img/f97f778697507bb6fdd80c5991210cba_1161_0.png)

**图 18-17** 计算后缀表达式：`6 3 + 2 * =`

