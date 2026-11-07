

```text
//Otherwise, report the error.
//Set expressionOk to false.
break;
otherwise // operation is illegal
{
    output an appropriate message;
    set expressionOk to false;
}
}
} //end switch
}
```

按照此伪代码，函数 `evaluateOpr` 的定义如下：

```cpp
void evaluateOpr(ostream& out, stackType<double>& stack,
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
            } //end switch
        } //end else
    } //end else
} //end evaluateOpr
```

### 函数 `discardExp`

每当在表达式中发现错误时，就会调用此函数。它只读取和写入输入数据，直到输入字符为表达式末尾的 `=` 为止。此函数的定义如下：

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

如果后缀表达式没有错误，函数 `printResult` 将打印结果；否则，它会输出适当的消息。表达式的结果存储在栈中，输出则发送到文件。因此，此函数必须能够访问栈和输出文件。假设方法 `evaluateExpression` 没有遇到任何错误。如果栈中只有一个元素，则表达式没有错误，并打印栈顶元素。如果栈为空或包含多个元素，则后缀表达式中存在错误。在这种情况下，此方法会输出适当的错误消息。此函数的定义如下：

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

    outF << "________________________________________"
         << endl << endl;
} //end printResult
```

## 程序清单

```cpp
//***********************************************************
// Author: D.S. Malik
//
// Program: Postfix Calculator
// This program evaluates postfix expressions.
//***********************************************************

#include <iostream>
#include <iomanip>
#include <fstream>
#include "mystack.h"

using namespace std;

void evaluateExpression(ifstream& infP, ofstream& outF,
                        stackType<double>& stack,
                        char& ch, bool& isExpOk);
void evaluateOpr(ofstream& out, stackType<double>& stack,
                 char& ch, bool& isExpOk);
void discardExp(ifstream& in, ofstream& out, char& ch);
void printResult(ofstream& outF, stackType<double>& stack,
                 bool isExpOk);

int main()
{
    bool expressionOk;
    char ch;
    stackType<double> stack(100);
    ifstream infile;
    ofstream outfile;

    infile.open("RpnData.txt");

    if (!infile)
    {
        cout << "Cannot open the input file. "
             << "Program terminates!" << endl;
        return 1;
    }

    outfile.open("RpnOutput.txt");

    outfile << fixed << showpoint;
    outfile << setprecision(2);

    infile >> ch;
    while (infile)
    {
        stack.initializeStack();
        expressionOk = true;
        outfile << ch;

        evaluateExpression(infile, outfile, stack, ch,
                           expressionOk);
        printResult(outfile, stack, expressionOk);
        infile >> ch; //begin processing the next expression
    } //end while

    infile.close();
    outfile.close();

    return 0;
} //end main

//Place the definitions of the function evaluateExpression,
//evaluateOpr, discardExp, and printResult as described
//previously here.
```

### 示例运行

**输入文件**

```text
#35 #27 + #3 * =
#26 #28 + #32 #2 / = #5 / =
#23 #30 #15 * / =
#2 #3 #4 + =
#20 #29 #9 * =
#25 #23 - + =
#34 #24 #12 #7 / * + #23 - =
```

**输出**

```text
#35.00 #27.00 + #3.00 * = 186.00

#26.00 #28.00 + #32.00 #2.00; (Illegal operator) - #5 / = (Error in the expression)

#23.00 #30.00 #15.00 * / = 0.05

#2.00 #3.00 #4.00 + = (Error: Too many operands)

#20.00 #29.00 #9.00 *; (Illegal operator) = (Error in the expression)

#25.00 #23.00 - + (Not enough operands) = (Error in the expression)

#34.00 #24.00 #12.00 #7.00 / * + #23.00 - = 52.14
```

## 移除递归：反向打印链表的非递归算法

在第 16 章中，我们使用递归来反向打印链表。在本节中，你将学习如何使用栈来设计一种非递归算法，以反向打印链表。

请考虑图 17-18 所示的链表。

![](img/b217c421655b51e7494cf3b89bb5432d_1274_0.png)

**图 17-18**  链表

要反向打印链表，首先需要到达链表的最后一个结点，这可以通过从第一个结点开始遍历链表来实现。然而，一旦到达最后一个结点，我们该如何返回前一个结点呢？特别是当链接只有一个方向时。你可以再次使用适当的循环终止条件遍历链表，但这种方法可能会浪费大量计算机时间，尤其是在链表非常大的情况下。此外，如果对链表中的每个结点都这样做，程序的执行速度可能会非常慢。下面将介绍如何有效地使用栈来反向打印链表。

打印某个结点的信息后，需要移动到紧跟在该结点后面的结点。例如，打印 15 后，需要移动到具有 **信息 10** 的结点。因此，在最初遍历链表并移动到最后一个结点的过程中，必须保存每个结点的指针。例如，对于图 17-18 中的链表，必须保存具有 **信息 5** 和 **10** 的结点的指针。打印 15 后，返回到具有 **信息 10** 的结点；打印 10 后，返回到具有 **信息 5** 的结点。由此可知，我们必须将每个结点的指针保存在栈中，以实现后进先出（LIFO）原则。

由于链表中的结点数通常是未知的，因此我们将使用栈的链式实现。假设栈是 `linkedListType` 类型的对象，并且 `current` 是一个指针，其类型与指针 `first` 相同。请考虑以下语句：

```cpp
current = first;                 //Line 1

while (current != nullptr)       //Line 2
{
    stack.push(current);          //Line 3
    current = current->link;      //Line 4
}
```

执行第 1 行的语句后，`current` 指向第一个结点（见图 17-19）。

![](img/b217c421655b51e7494cf3b89bb5432d_1275_0.png)

**图 17-19**  执行语句 `current = first;` 后的链表

由于 `current` 不等于 `nullptr`，因此第 3 行和第 4 行的语句会执行（见图 17-20）。

![](img/b217c421655b51e7494cf3b89bb5432d_1275_1.png)

**图 17-20**  执行语句 `stack.push(current);` 和 `current = current->link;` 后的链表和栈

