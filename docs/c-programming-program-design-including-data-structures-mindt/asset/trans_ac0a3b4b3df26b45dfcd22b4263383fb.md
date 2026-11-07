

## 示例 17-4

| 中缀表达式 | 等价的后缀表达式 |
|---|---|
| `a + b` | `a b +` |
| `a + b * c` | `a b c * +` |
| `a * b + c` | `a b * c +` |
| `(a + b) * c` | `a b + c *` |
| `(a − b) * (c + a)` | `a b − c a + *` |
| `(a + b) * (c − d / e) + f` | `a b + c d e / − * f +` |

在 Łukasiewicz 发现后不久，人们意识到后缀表示法在计算机科学中有重要应用。事实上，许多编译器现在会先将算术表达式转换为某种形式的后缀表示法，然后再将该后缀表达式转换为机器代码。后缀表达式可以使用以下算法求值：

从左到右扫描表达式。当遇到运算符时，向后取出所需数量的操作数，执行运算，然后继续扫描。

考虑以下后缀表达式：

```
6 3 + 2 * =
```

下面使用栈和前述算法对该表达式求值。图 17-17 展示了该表达式的求值过程。

![](img/b217c421655b51e7494cf3b89bb5432d_1265_0.png)

图 17-17  对后缀表达式 `6 3 + 2 * =` 求值

读取第一个符号 6，它是一个数字。将该数字压入栈中（见图 17-17(a)）。读取下一个符号 3，它是一个数字。将该数字压入栈中（见图 17-17(b)）。读取下一个符号 +，它是一个运算符。由于运算符求值需要两个操作数，因此连续两次弹出栈顶元素（见图 17-17(c)）。执行运算，并将结果重新压入栈中（见图 17-17(d)）。

![](img/b217c421655b51e7494cf3b89bb5432d_1266_0.png)

读取下一个符号 2，它是一个数字。将该数字压入栈中（见图 17-17(e)）。读取下一个符号 *，它是一个运算符。由于运算符求值需要两个操作数，因此连续两次弹出栈顶元素（见图 17-17(f)）。执行运算，并将结果重新压入栈中（见图 17-17(g)）。

扫描下一个符号 =，这是等号，表示表达式结束。因此，输出结果。表达式的结果位于栈中，所以弹出并输出该结果（见图 17-17(h)）。

表达式 `6 3 + 2 * =` 的值为 18。

从上述讨论可以清楚地看出，当读取到一个非数字符号时，会出现以下情况：

- 1. 我们读取到的符号是以下符号之一：`+`、`-`、`*`、`/` 或 `=`。
  - a. 如果符号是 `+`、`-`、`*` 或 `/`，则该符号是一个运算符，因此必须对其求值。由于运算符需要两个操作数，栈中必须至少有两个元素；否则，表达式存在错误。
  - b. 如果符号是 `=`（等号），则表达式结束，我们必须输出答案。在此步骤中，栈中必须恰好包含一个元素；否则，表达式存在错误。
- 2. 我们读取到的符号不是 `+`、`-`、`*`、`/` 或 `=`。在这种情况下，表达式包含非法运算符。

同样显而易见的是，当表达式中遇到操作数（数字）时，由于运算符位于操作数之后，因此应将该操作数压入栈中。

考虑以下表达式：

- a. `7 6 + 3 ; 6 - =`
- b. `14 + 2 3 * =`
- c. `14 2 3 + =`

表达式 (a) 包含非法运算符，表达式 (b) 没有足够的操作数供 `+` 运算，表达式 (c) 包含过多的操作数。对于表达式 (c)，当遇到等号 (=) 时，栈中将有两个元素；直到准备输出表达式的值时，才能发现该错误。

为了使输入更易于读取，我们假设后缀表达式采用以下形式：

```
#6 #3 + #2 * =
```

符号 `#` 位于表达式中每个数字的前面。如果扫描到的符号是 `#`，则下一个输入是一个数字（即操作数）。如果扫描到的符号不是 `#`，那么它要么是一个运算符（可能是非法运算符），要么是表示表达式结束的等号。此外，我们假设每个表达式只包含 `+`、`-`、`*` 和 `/` 运算符。

该程序会输出完整的后缀表达式以及答案。如果表达式存在错误，则丢弃该表达式。在这种情况下，程序会输出该表达式以及适当的错误消息。由于表达式可能包含错误，因此在处理下一个表达式之前，必须清空栈。此外，还必须初始化栈，也就是说，栈必须为空。

### 主算法

根据前面的讨论，主算法的伪代码如下：

```
Read the first character
while not the end of input data
{
    a. initialize the stack
    b. process the expression
    c. output result
    d. get the next expression
}
```

为了简化 `main` 函数的复杂性，我们编写了四个函数：`evaluateExpression`、`evaluateOpr`、`discardExp` 和 `printResult`。如果可能，函数 `evaluateExpression` 会对表达式求值，并将结果留在栈中。如果后缀表达式没有错误，函数 `printResult` 会输出结果。函数 `evaluateOpr` 对运算符求值，而函数 `discardExp` 会在当前表达式存在任何错误时将其丢弃。

### 函数 `evaluateExpression`

函数 `evaluateExpression` 对每个后缀表达式求值。每个表达式都以符号 = 结尾。一般算法如下：

```
while (ch is not '=')    // process each expression
                         // marks the end of an expression
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
    } // end switch

    if no error was found, then
    {
        read next ch;
        output ch;
    }
    else
        Discard the expression
} //end while
```

根据该算法可知，此方法有五个参数：一个用于访问输入文件，一个用于访问输出文件，一个用于访问栈，一个用于传递表达式中的字符，以及一个用于指示表达式是否存在错误。该函数的定义如下：

```
void evaluateExpression(ifstream& inpF, ofstream& outf,
                        stackType<double>& stack,
                        char& ch, bool& isExpOk)
{
    double num;

    while (ch != '=')
    {
        switch (ch)
        {
        case '#':
            inpF >> num;
            outf << num << " ";
            if (!stack.isFullStack())
                stack.push(num);
            else
            {
                cout << "Stack overflow. "
                     << "Program terminates!" << endl;
                exit(0); //terminate the program
            }

            break;
        default:
            evaluateOpr(outf, stack, ch, isExpOk);
        } //end switch

        if (isExpOk) //if no error
        {
            inpF >> ch;
            outf << ch;

            if (ch != '#')
                outf << " ";
        }
        else
            discardExp(inpF, outf, ch);
    } //end while (ch != '=')
} //end evaluateExpression
```

注意，函数 `exit` 会终止程序。

### 函数 `evaluateOpr`

该函数在可能的情况下对表达式求值。对一个运算求值需要两个操作数，而操作数保存在栈中。因此，栈中必须至少包含两个数字。如果栈中的数字少于两个，则表达式存在错误。在这种情况下，将丢弃整个表达式，并输出适当的消息。该函数还会检查是否存在非法运算。该函数的伪代码如下：

```
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
            //onto the stack.
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
            // If (op2 != 0) perform the operation and
            // push the result onto the stack.
            stack.push(op1 / op2);
```

