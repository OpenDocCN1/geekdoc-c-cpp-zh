
注意，函数 exit 会终止程序。

### 函数 `evaluateOpr`

该函数（如果可能）对表达式求值。求值一个运算需要两个操作数，而操作数保存在栈中。因此，栈中必须至少包含两个数。如果栈中包含的数少于两个，则表达式有错误。在这种情况下，整个表达式会被丢弃，并打印一条适当的消息。该函数还会检查任何非法运算。用伪代码表示，该函数为：

```text
if stack is empty
{
    error in the expression
    set expressionOk to false
}
else
{
    retrieve the top element of stack into op2
    pop stack
    if stack is empty
    {
        error in the expression
        set expressionOk to false
    }
    else
    {
        retrieve the top element of stack into op1
        pop stack

        //If the operation is legal, perform the
        //operation and push the result onto the stack.
        switch (ch)
        {
        case '+':
            //Perform the operation and push the result
            //onto the stack
            stack.push(op1 + op2);
            break;
        case '-':
            //Perform the operation and push the result
            //onto the stack.
            stack.push(op1 - op2);
            break;
        case '*':
            //Perform the operation and push the
            //result onto the stack.
            stack.push(op1 * op2);
            break;
        case '/':
            //If (op2 != 0), perform the operation and
            //push the result onto the stack.
            stack.push(op1 / op2);
            //Otherwise, report the error.
            //Set expressionOk to false.
            break;
        otherwise operation is illegal
        {
            output an appropriate message;
            set expressionOk to false
        }
    } //end switch
}
```

按照这个伪代码，函数 evaluateOpr 的定义为：

```cpp
void evaluateOpr(ofstream& out, stackType<double>& stack,
                 char& ch, bool& isExpOk)
{
    double op1, op2;

    if (stack.isEmptyStack())
    {
        out << " (Not enough operands)";
        isExpOk = false;
    }
    else
    {
        op2 = stack.top();
        stack.pop();

        if (stack.isEmptyStack())
        {
            out << " (Not enough operands)";
            isExpOk = false;
        }
        else
        {
            op1 = stack.top();
            stack.pop();

            switch (ch)
            {
            case '+':
                stack.push(op1 + op2);
                break;
            case '-':
                stack.push(op1 - op2);
                break;
            case '*':
                stack.push(op1 * op2);
                break;
            case '/':
                if (op2 != 0)
                    stack.push(op1 / op2);
                else
                {
                    out << " (Division by 0)";
                    isExpOk = false;
                }
                break;
            default:
                out << " (Illegal operator)";
                isExpOk = false;
            }//end switch
        }//end else
    }//end else
}//end evaluateOpr
```

### 函数 `discardExp`

每当在表达式中发现错误时，就会调用该函数。它只读取并写入输入数据，直到输入为 '='，即表达式的末尾。该函数的定义为：

```cpp
void discardExp(ifstream& in, ofstream& out, char& ch)
{
    while (ch != '=')
    {
        in.get(ch);
        out << ch;
    }
} //end discardExp
```

### 函数 `printResult`

如果后缀表达式不包含错误，函数 printResult 会打印结果；否则，它会输出一条适当的消息。表达式的结果在栈中，输出会发送到文件。因此，该函数必须能够访问栈和输出文件。假设方法 evaluateExpression 没有遇到任何错误。如果栈只有一个元素，那么表达式没有错误，并打印栈顶元素。如果栈为空或元素多于一个，则后缀表达式中有错误。在这种情况下，该方法会输出一条适当的错误消息。该方法的定义为：

```cpp
void printResult(ofstream& outF, stackType<double>& stack,
                 bool isExpOk)
{
    double result;

    if (isExpOk) //if no error, print the result
    {
        if (!stack.isEmptyStack())
        {
            result = stack.top();
            stack.pop();

            if (stack.isEmptyStack())
                outF << result << endl;
            else
                outF << " (Error: Too many operands)" << endl;
        } //end if
        else
            outF << " (Error in the expression)" << endl;
    }
    else
        outF << " (Error in the expression)" << endl;

    outF << "______________________________"
         << endl << endl;
} //end printResult
```

## 程序清单

```cpp
////////////////////////////////////////////////////////////
// Author: D.S. Malik
//
// Program: Postfix Calculator
// This program evaluates postfix expressions.
////////////////////////////////////////////////////////////

#include <iostream>
#include <iomanip>
#include <fstream>
#include "mystack.h"

using namespace std;

void evaluateExpression(ifstream& inF, ofstream& outF,
                        stackType<double>& stack,
                        char& ch, bool& isExpOk);

void evaluateOpr(ofstream& outF, stackType<double>& stack,
                 char& ch, bool& isExpOk);

void discardExp(ifstream& in, ofstream& out, char& ch);
void printResult(ofstream& outF, stackType<double>& stack,
                 bool isExpOk);

int main()
{
    bool expressionOk;
    char ch;
```

### 输出

```text
#35.00 #27.00 + #3.00 * = 186.00
#26.00 #28.00 + #32.00 #2.00 ; (Illegal operator) - #5 / = (Error in the expression)
#23.00 #30.00 #15.00 * / = 0.05
#2.00 #3.00 #4.00 + = (Error: Too many operands)
#20.00 #29.00 #9.00 * ; (Illegal operator) = (Error in the expression)
#25.00 #23.00 - + (Not enough operands) = (Error in the expression)
#34.00 #24.00 #12.00 #7.00 / * + #23.00 - = 52.14
```

## 消除递归：逆序打印链表的非递归算法

在第 16 章中，我们使用递归来逆序打印链表。在本节中，你将学习如何使用栈来设计一个逆序打印链表的非递归算法。

考虑图 17-18 所示的链表。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1212_0.png)

图 17-18 链表

要逆序打印该链表，首先需要到达链表的最后一个结点，这可以通过从第一个结点开始遍历链表来实现。然而，一旦到达最后一个结点，我们如何返回前一个结点，尤其是考虑到链接只沿一个方向？你可以使用适当的循环终止条件再次遍历链表，但这种方法可能会浪费大量计算机时间，特别是当链表非常大时。此外，如果对链表中的每个结点都这样做，程序的执行可能会非常慢。接下来，我们将展示如何有效地使用栈来逆序打印链表。

打印某个特定结点的 info 后，我们需要移动到紧挨在该结点后面的结点。例如，打印 15 之后，我们需要移动到 info 为 10 的结点。因此，在最初遍历链表以移动到最后一个结点时，我们必须保存指向每个结点的指针。例如，对于图 17-18 中的链表，我们必须保存指向 info 分别为 5 和 10 的每个结点的指针。打印 15 之后，我们返回到 info 为 10 的结点；打印 10 之后，我们返回到 info 为 5 的结点。由此可知，我们必须在栈中保存指向每个结点的指针，以实现后进先出原则。

由于链表中结点的数量通常未知，我们将使用栈的链式实现。假设 stack 是类型为 linkedListType 的对象，而 current 是与指针 first 同类型的指针。考虑以下语句：

```cpp
current = first;                 //Line 1

while (current != NULL)          //Line 2
{
    stack.push(current);         //Line 3
    current = current->link;     //Line 4
}
```

第 1 行的语句执行后，current 指向第一个结点（见图 17-19）。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1213_0.png)

因为 current 不为 NULL，所以第 3 行和第 4 行的语句会执行（见图 17-20）。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1213_1.png)
