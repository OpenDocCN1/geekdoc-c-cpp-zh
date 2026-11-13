

## 将中缀表示法转换为后缀表示法

后缀求值之所以容易，正是因为每个运算符在读取时立即被使用。在该算法中，我们假设每个输入项要么是数字，要么是运算。为简单起见，我们假设所有运算都需要两个操作数。完整的求值算法如图 7.10 所示，并附有示例计算。

让我们研究示例，了解算法的工作原理。每当输入中出现一个运算，该运算的操作数就是最近看到的两个数字。例如，在图 7.10(c) 中，我们即将读取 * 符号。由于我们刚刚将 3 和 2 压入栈中，* 导致 3 * 2 的乘法，结果为 6。然后将结果 6 压入栈中，如图 7.10(d) 所示。

有时，“最近看到的数字”并非实际的输入数字，而是我们计算并重新压入栈中的数字。例如，在图 7.10(d) 中，我们即将读取第一个 +。此时，6 位于栈顶（是 3 * 2 乘法的结果）。6 下方是数字 5。因此，“最近看到的两个数字”是 6（我们计算得到的）和 5（位于 6 下方的数字）。我们将这两个数字相加，结果为 11（我们将其压入栈中，如图 7.10(e) 所示）。

过程如此继续。每当我们遇到一个运算，该运算就会立即应用于最近看到的两个数字，这两个数字始终位于栈顶的两个位置。当输入耗尽时，栈中剩余的数字即为整个表达式的值。

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_406_0.png)

### 图 7.10 求值后缀表达式

### 伪代码

```
1. Initialize a stack of double numbers.
2. do
   if (the next input is a number)
     Read the next input and push it onto the stack.
   else
     Read the next character, which is an operation symbol.
     Use top and pop to get the two numbers off the stack.
     Combine these two numbers with the operation (using the second number popped as the left operand), and push the result onto the stack.
   }
   while (there is more of the expression to read);
3. At this point, the stack contains one number, which is the value of the expression.
```

### 示例

求值后缀表达式
5 3 2 * + 4 - 5 +

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_407_0.png)

作为算术表达式。但是，为了保持示例简洁，我们在示例中只考虑算术表达式。

如果中缀表达式完全加括号，算法很简单。将中缀表示法转换为后缀表示法所需的全部操作，就是将每个运算符移动到与该运算对应的右括号位置，然后删除所有括号。例如，以下中缀表达式的运算符将移动到箭头指示的位置：

```
( ( ( A + 7 ) * ( B / C ) ) - ( 2 * D ) )
```

结果是后缀表达式：

```
A 7 + B C / * 2 D * -
```

将每个运算移动到其对应右括号位置的过程，更多是一种思路，而非完整算法。完整算法应从左到右读取表达式，并以某种方式记住运算，然后确定何时找到了对应的右括号。在该思路成为算法之前，我们还有工作要做。

首先，请注意，等价后缀表达式中的操作数（即数字和变量）的顺序，与我们最初使用的中缀表达式中的操作数顺序相同。因此，我们的算法可以简单地复制中缀表达式的操作数，省略括号，并在正确位置插入 +、* 等运算。问题是如何在后缀表达式中找到插入运算的位置。我们如何保存运算，又如何知道何时插入它们？回顾我们的示例。如果我们将运算压入栈中，那么我们需要的运算始终位于栈顶。何时插入运算？每当输入中遇到右括号时，我们就将运算插入输出。因此，算法的核心是将运算压入栈中，并在每次输入中遇到右括号时弹出一个运算。该算法如图 7.11 所示。算法会进行一些检查，以确保输入表达式完全加括号且括号匹配，尽管没有检查确保每个运算出现在其操作数之间（而非在操作数之前或之后）。

### 在中缀表达式中使用优先级规则

迄今为止，我们一直假设中缀表达式完全加括号。然而，在实际中，中缀表达式通常不完全加括号，计算机必须依赖优先级规则来确定缺失括号的运算顺序。这增加了显著的复杂性。

完全加括号表达式的算法

### 图 7.11 将完全加括号的中缀表达式转换为后缀表达式

```
Pseudocode
1. Initialize a stack of characters to hold the operation symbols and parentheses.
2. do if (the next input is a left parenthesis)
   Read the left parenthesis and push it onto the stack.
   else if (the next input is a number or other operand)
   Read the operand and write it to the output.
   else if (the next input is one of the operation symbols)
   Read the operation symbol and push it onto the stack.
   else {
   Read and discard the next input symbol (which should be a right parenthesis).
   There should be an operation symbol on top of the stack, so write this symbol
   to the output and pop it from the stack. (If there is no such symbol, then print an
   error message indicating that there were too few operations in the infix expression,
   and halt.) After popping the operation symbol, there should be a left parenthesis on
   the top of the stack, so pop and discard this left parenthesis.
   (If there was no left parenthesis, then the input did not have balanced
   parentheses, so print an error message and halt.)
   }
   while (there is more of the expression to read) ;
3. At this point, the stack should be empty. Otherwise print an error message indicating that the
   expression was not fully parenthesized.
```

让我们从一个示例开始。我们将在示例中使用常规的 C++ 优先级规则。考虑以下表达式：

```
2 * (A - B) + 3 + C
```

在这种情况下，先执行减法，然后执行乘法，最后从左到右执行两个加法。减法优先，因为括号表明 (A - B) 必须在将结果与任何其他操作数结合之前先求值。接下来执行乘法——在加法之前——因为乘法的优先级高于加法。两个加法优先级相同，且没有括号告诉我们先执行哪个加法。优先级相同的运算（+、-、* 和 /）从左到右执行（除非括号另有说明）。因此，左侧加法先于右侧加法发生。这种求值顺序意味着该表达式等同于以下完全加括号的表达式：

```
(((2 * (A - B)) + 3) + C)
```

