

## (图 7.5 续)

```cpp
int main()
{
    double answer;
    cout << "Type a fully parenthesized arithmetic expression:" << endl;
    answer = read_and_evaluate(cin);
    cout << "That evaluates to " << answer << endl;
    return EXIT_SUCCESS;
}
```

```cpp
double read_and_evaluate(istream& ins)
// Library facilities used: cstring, iostream, stack
{
    const char DECIMAL = '.';
    const char RIGHT_PARENTHESIS = ')';
    stack<double> numbers;
    stack<char> operations;
    double number;
    char symbol;
    // Loop continues while istream is not "bad" (tested by ins) and next character isn't newline.
    while (ins && ins.peek() != '\n')
    {
        if (isdigit(ins.peek()) || ins.peek() == DECIMAL)
        {
            ins >> number;
            numbers.push(number);
        }
        else if (strchr("+-*/", ins.peek()) != NULL)
        {
            ins >> symbol;
            operations.push(symbol);
        }
        else if (ins.peek() == RIGHT_PARENTHESIS)
        {
            ins.ignore();
            evaluate_stack_tops(numbers, operations);
        }
        else
            ins.ignore();
    }
    return numbers.top();
}
```

## (图 7.5 续)

```cpp
void evaluate_stack_tops(stack<double>& numbers, stack<char>& operations)
// Library facilities used: stack
{
    double operand1, operand2;
    operand2 = numbers.top();
    numbers.pop();
    operand1 = numbers.top();
    numbers.pop();
    switch (operations.top())
    {
        case '+': numbers.push(operand1 + operand2);
                  break;
        case '-': numbers.push(operand1 - operand2);
                  break;
        case '*': numbers.push(operand1 * operand2);
                  break;
        case '/': numbers.push(operand1 / operand2);
                  break;
    }
    operations.pop();
}
```

## 示例对话

键入一个完全加括号的算术表达式：
( ( 60 + 40/50 ) * ( 16 - 4 ) )
其值为 24

## 算术表达式求值——实现

图 7.5 中 read_and_evaluate 的实现受益于 istream 的三个函数：

- istream 的名称 ins 用作控制循环的布尔表达式的一部分。如前所述，只要 ins 未遇到错误输入（例如文件末尾），表达式 ins 就保持为真。
- 函数调用 ins.peek() 返回 ins 输入流的下一个字符（而不实际读取它）。
- 函数调用 ins.ignore() 从 ins 输入流读取并丢弃下一个字符。

我们的实现还使用了另外三个函数，我们将在下一节中讨论。

## 计算器程序中使用的函数

我们实现中使用的另外三个函数列于此：

- isdigit 函数（来自设施 <cctype>），原型如下：

  `bool isdigit(char c);`

  如果其参数是 '0' 到 '9' 之间的数字之一，则该函数返回 true；否则返回 false。

- strchr 函数（来自 <cstring>），原型如下：

  `char* strchr(const char s[], char c);`

  该函数扫描字符串 s 以查找字符 c 的出现。如果找到字符 c，则该函数返回指向 s 中该字符第一次出现位置的指针。否则，返回空指针。

- 一个名为 evaluate_stack_tops 的函数出现在第 366 页的图 7.5 中。该函数从 numbers 栈弹出两个数字，用 operations 栈中的一个运算符将它们组合，并将结果压回 numbers 栈。

## 算术表达式求值——测试与分析

像往常一样，你应该在最可能引起问题的边界值上测试你的程序。对于这个程序，一种边界值是仅包含一个数字且没有运算的情况。接下来最简单的表达式是只组合两个数字的表达式。为了测试运算是否正确执行，你应该为 +、-、* 和 / 中的每个运算测试简单表达式。这些简单表达式应只包含一个运算。请务必仔细测试除法和减法运算，以确保运算按正确顺序执行。毕竟，3/15 与 15/3 不同，3 - 15 与 15 - 3 也不同。这些或许是唯一的边界值。但同样重要的是，还要测试一些带有嵌套括号的情况。你还可以测试非法除法，例如 15/0。程序会怎么做？它可能会因除以零错误而崩溃。你能在程序中放置一个断言来捕获此错误，而不是允许除以零发生吗？

让我们估计程序在长度为 n 的输入上将使用的操作数量。我们将以下每项视为一个程序操作：读取或窥视符号、执行一个算术运算（+、-、* 或 /）、将条目压入栈中、以及检查或弹出栈中的条目。我们分别考虑每种操作。

读取字符所花费的时间。输入中只有 n 个符号，因此程序最多可读取 n 个符号。同样，没有字符会被“窥视”超过一次，因此这部分程序的操作不超过 2n 次。

评估算术运算所花费的时间。程序执行的每个算术运算都是对输入中运算符号的求值。由于输入中不超过 n 个算术运算，因此执行的算术运算最多为 n 次。实际上，操作次数远少于 n 次，因为许多输入符号是数字或括号。但可以肯定的是，不超过 n 个算术运算符号，因此可以安全地说执行的算术运算不超过 n 次。

### 压入操作次数。

由于不超过 n 个算术运算符号，可知压入 operations 栈的运算符号不超过 n 个。numbers 栈可能包含输入数字和从算术表达式求值得到的数字。同样，给出一个上界即可：输入数字不超过 n 个，求值的算术运算不超过 n 个。因此，压入 numbers 栈的数字最多为 2n 个。这给出了对栈上总压入操作次数 3n 的上界。

### top 和 pop 操作次数。

一旦知道压入两个栈的条目总数，就可以确定从两个栈弹出的条目数量的上限。毕竟，除非条目先被压入栈中，否则无法弹出。此外，我们的算法对每个项目最多使用一次 top。因此，从栈中进行的 top 和 pop 操作总数的上限为 6n。

### 操作总数。

现在，让我们汇总一下。操作总数不超过 2n 次读取/窥视，加上 n 次执行的算术运算，再加上 9n 次对 push、top 和 pop 的调用——总计 12n。实际操作次数会少于这个数字，因为我们在多个估计中使用了宽松的上界，但 12n 足以让我们得出结论：该程序的算法是 O(n)；这是一个线性算法。

## 算术表达式求值——增强

第 364 页图 7.5 中的程序是使用栈的一个绝佳示例。作为计算机科学家，你会发现自己在许多不同的情况下都会以这种方式使用栈。然而，该程序并不是一个完成程序的优秀示例。在我们将其视为完成产品之前，需要添加若干增强功能，使程序更加健壮和友好。

有些增强功能很简单。向主程序添加一个循环很有用（也很简单），该循环将允许用户求值更多表达式，直到有迹象表明用户已完成计算器的使用。其他增强功能稍微困难一些。一个很好的增强功能是允许不完全加括号的表达式，并在缺少括号时使用 C++ 优先级规则来决定运算顺序。我们将在第 7.4 节中讨论与此增强相关的主题，届时（惊喜！）我们将看到栈对此目的也很有用。

## 第 7.2 节自测练习

- 6. 在计算器程序中，两个栈分别保存哪些项目？
- 7. 你将如何修改第 364 页图 7.5 中的计算器程序，以允许使用符号 ^ 进行幂运算？描述更改内容；无需编写代码。

