

```cpp
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

## 从 unorderedLinkedList 类派生的栈

如果我们将栈的 push 函数与第 16 章中为一般列表讨论的 insertFirst 函数进行比较，就会发现实现这些操作的算法是相似的。对其他函数——例如 initializeStack 和 initializeList、isEmptyList 和 isEmptyStack 等——的比较表明，类 linkedStackType 可以从类 unorderedLinkedListType 派生。此外，函数 pop 和 isFullStack 可以像上一节那样实现。注意，类 linkedListType 是一个抽象类，并没有实现所有操作。然而，类 unorderedLinkedListType 派生自类 linkedListType，并提供了类 linkedListType 的抽象函数的定义。因此，我们可以从类 unorderedLinkedListType 派生出类 linkedStackType。

接下来，我们定义派生自类 unorderedLinkedList 的类 linkedStackType。同时给出实现栈操作的函数定义。

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

书写算术表达式的常用记法（我们在小学学到的记法）称为**中缀**记法，其中运算符写在操作数之间。例如，在表达式 *a* + *b* 中，运算符 + 位于操作数 *a* 和 *b* 之间。在中缀记法中，运算符具有优先级。也就是说，我们必须从左到右对表达式求值，并且乘法和除法的优先级高于加法和减法。如果我们想以不同的顺序对表达式求值，就必须加上括号。例如，在表达式 *a* + *b* \* *c* 中，我们首先使用操作数 *b* 和 *c* 对 \* 求值，然后使用操作数 *a* 和 *b* \* *c* 的结果对 + 求值。

20 世纪 20 年代初，波兰数学家扬·武卡谢维奇（Jan Lukasiewicz）发现，如果把运算符写在操作数之前（**前缀**或**波兰**表示法；例如 + *a* *b*），就可以省略括号。20 世纪 50 年代末，澳大利亚哲学家、早期计算机科学家查尔斯·L·汉布林（Charles L. Hamblin）提出了一种方案，让运算符*跟随*操作数（后缀运算符），从而产生了**逆波兰**表示法。这种表示法的优点是运算符按计算所需的顺序出现。

例如，表达式：

*a* + *b* \* *c*

的后缀表达式是：

*a* *b* *c* \* +

下面的例子展示了各种中缀表达式及其等价的后缀表达式。

读取第一个符号 6，它是一个数字。将该数字压入栈中（见图 17–17(a)）。读取下一个符号 3，它是一个数字。将该数字压入栈中（见图 17–17(b)）。读取下一个符号 +，它是一个运算符。因为一个运算符需要两个操作数才能求值，所以从栈中弹出两次（见图 17–17(c)）。执行该运算，并将结果放回栈中（见图 17–17(d)）。

读取下一个符号 2，它是一个数字。将该数字压入栈中（见图 17–17(e)）。读取下一个符号 *，它是一个运算符。因为一个运算符需要两个操作数才能求值，所以从栈中弹出两次（见图 17–17(f)）。执行该运算，并将结果放回栈中（见图 17–17(g)）。

扫描下一个符号 =，它是等号，表示表达式的结束。因此，打印结果。表达式的结果在栈中，所以弹出并打印（见图 17–17(h)）。

表达式 6 3 + 2 * = 18 的值为 18。

从以上讨论可以清楚地看出，当我们读取一个不是数字的符号时，会出现以下情况：

- 1. 我们读取的符号是以下之一：+、-、*、/ 或 =。
  - a. 如果符号是 +、-、* 或 /，则该符号是运算符，因此我们必须对其求值。因为一个运算符需要两个操作数，所以栈中必须至少有两个元素；否则，表达式有错误。
  - b. 如果符号是 =（等号），则表达式结束，我们必须打印答案。在此步骤中，栈中必须恰好包含一个元素；否则，表达式有错误。
- 2. 我们读取的符号不是 +、-、*、/ 或 =。在这种情况下，表达式包含非法运算符。

同样清楚的是，当在表达式中遇到操作数（数字）时，它会被压入栈中，因为运算符位于操作数之后。

考虑以下表达式：

- a. 7 6 + 3 ; 6 - =
- b. 14 + 2 3 * =
- c. 14 2 3 + =

表达式 (a) 含有一个非法运算符，表达式 (b) 没有足够的操作数用于 +，而表达式 (c) 的操作数过多。对于表达式 (c)，当我们遇到等号（=）时，栈中将有两个元素，并且直到我们准备打印表达式的值时才能发现这个错误。

为了使输入更易于阅读，我们假设后缀表达式采用以下形式：

```text
#6 #3 + #2 * =
```

符号 # 位于表达式中每个数字之前。如果扫描到的符号是 #，则下一个输入是一个数字（即一个操作数）。如果扫描到的符号不是 #，那么它要么是一个运算符（可能是非法的），要么是一个等号（表示表达式的结束）。此外，我们假设每个表达式只包含 +、-、* 和 / 运算符。

该程序输出整个后缀表达式及其答案。如果表达式有错误，则丢弃该表达式。在这种情况下，程序会输出该表达式以及相应的错误消息。由于一个表达式可能包含错误，因此我们必须在处理下一个表达式之前清空栈。此外，栈必须初始化；也就是说，栈必须为空。

### 主算法

根据前面的讨论，主算法的伪代码如下：

```text
Read the first character
while not the end of input data
{
    a. initialize the stack
    b. process the expression
    c. output result
    d. get the next expression
}
```

为了简化 main 函数的复杂性，我们编写四个函数：evaluateExpression、evaluateOpr、discardExp 和 printResult。函数 evaluateExpression 在可能的情况下对表达式求值，并将结果留在栈中。如果后缀表达式没有错误，函数 printResult 输出结果。函数 evaluateOpr 对一个运算符求值，而函数 discardExp 在表达式中存在任何错误时丢弃当前表达式。

### 函数 `evaluateExpression`

函数 `evaluateExpression` 对每个后缀表达式求值。每个表达式以符号 = 结束。一般算法如下：

```text
while (ch is not = '=')  //process each expression
                         //= marks the end of an expression
{
    switch (ch)
    {
    case '#':
        read a number
        output the number;
        push the number onto the stack;
        break;
    default:
        assume that ch is an operation
        evaluate the operation;
    } //end switch
```

