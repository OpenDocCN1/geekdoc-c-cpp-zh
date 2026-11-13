

为了帮助确定算术表达式的求值顺序，我们一直在引用运算的优先级，例如 +、- 和 *。优先级只是运算从高到低的排序。优先级较高的运算会在优先级较低的运算之前求值。有时，两个不同的运算，例如 + 和 -，具有相同的优先级，在这种情况下，我们必须指定运算是从左到右还是从右到左求值。例如，在 C++ 中，* 和 / 具有相同的优先级（从左到右求值）；+ 和 - 也具有相同的优先级（从左到右求值），但 * 和 / 的优先级高于 + 和 -。这就是为什么我们先执行乘法再执行加法（当没有括号指示否则时）。

## 优先级使用规则

为了确保它们在我们脑海中依然清晰，让我们回顾一下 C++ 中对不完全加括号的算术表达式求值的规则：

- 1. 当存在括号时，括号决定运算顺序。一对匹配括号内的所有内容都会被求值，然后该值与括号外的内容组合。
- 2. 如果顺序未由括号指示，则先执行优先级较高的运算，再执行优先级较低的运算。
- 3. 优先级相同的算术运算按从左到右的顺序执行，除非括号另有指示。

在图 7.11 中，我们给出了一个将完全加括号的中缀表达式转换为等效后缀表达式的算法。现在，我们可以使算法更加通用。新版本（图 7.12，第 385 页）不要求输入完全加括号；算法使用优先级来决定先执行哪个运算。换句话说，表达式可以像我们通常书写的那样编写，在某些情况下省略括号。图 7.13（第 386 页）包含了我们算法将中缀表达式转换为相应后缀表达式的示例计算。现在先学习示例，然后返回此处阅读算法的详细信息。

## 中缀到后缀转换的正确性

为了使转换算法正确，我们必须检查以下项目：

- 1. 后缀表达式包含正确顺序的正确操作数。
- 2. 后缀表达式按照中缀表达式中括号指示的方式求值子表达式。
- 3. 后缀表达式根据优先级规则处理优先级不同的运算。
- 4. 中缀表达式中一串优先级相同的运算在转换为后缀表达式时会被正确处理。

- 1. 操作数顺序正确

让我们逐一考虑这四个问题。首先，我们需要知道后缀表达式中的操作数（数字和变量）与输入中缀表达式中的顺序相同，但这很容易看出。因为操作数在读取后立即写出，所以它们显然与输入中缀表达式中的顺序相同。

- 2. 括号处理正确

括号是对子表达式进行分组的一种方式。一对匹配括号内的所有内容都被括号外的任何内容视为一个单元。括号向括号外的运算传递以下信息：不要查看这些括号内部。我们会在内部自行处理，并为您提供一个单一值，以便与其他操作数组合。这意味着中缀表达式中一组匹配括号之间的所有运算都应该构成后缀表达式的一个子表达式，而使用此算法，它们确实如此。要看出它们确实构成一个子表达式，我们将展示以下内容：

### 中缀到后缀算法如何转换子表达式

主张：在算法读取左括号和读取右括号之间，会输出一对匹配括号之间的所有运算（且仅这些运算）。

一旦我们证明这一主张成立，我们就会知道中缀表达式中一对匹配括号之间的所有运算都将在输出的后缀表示中聚集在一起，因此它们将构成后缀表达式的一个子表达式。那么，让我们看看这一主张为何成立。

算法通过使用其栈来跟踪匹配括号内的表达式。当算法遇到左括号，即 '(' 时，它会将该括号压入栈中。现在考虑在压入左括号和遇到匹配的右括号（即匹配的 ')'）之间会发生什么。算法永远不会输出栈中位于左括号 '(' 下方的运算。因此，它只输出输入（中缀）表达式中匹配括号对内的运算。此外，它会输出所有这些运算。当它遇到匹配的右括号时，它会输出栈上剩余的所有运算，一直到该匹配的左括号。

- 3. 优先级处理正确

当中缀表达式包含一个低优先级运算，后跟一个高优先级运算符时，算法应按逆序输出这些运算。换句话说，高优先级运算必须先写出。检查算法会发现，这些运算确实是按逆序输出的。

当中缀表达式包含一系列优先级相同的运算时，它们表示从左到右的求值。这意味着运算应按从左到右的顺序输出。如果你检查算法，你会发现这是正确的。运算会被压入栈中，但当遇到下一个优先级相同的运算时，栈中的运算会被输出，新运算被压入栈中。要验证这一点，首先检查算法在遇到运算时栈为空的情况。这是最容易看到的情况。之后，其他情况会更清晰，因为它们类似。

- 4. 优先级相同的运算处理正确

## 图 7.12 将中缀表达式转换为后缀表达式（一般情况）

### 伪代码

```
1. Initialize a stack of characters to hold the operation symbols and parentheses.
2. do
    if (the next input is a left parenthesis)
        Read the left parenthesis and push it onto the stack.
    else if (the next input is a number or other operand)
        Read the operand and write it to the output.
    else if (the next input is one of the operation symbols)
    {
        do
            Print the top operation and pop it.
        while none of these three conditions are true:
            (1) The stack becomes empty, or
            (2) The next symbol on the stack is a left parenthesis, or
            (3) The next symbol on the stack is an operation with lower
                precedence than the next input symbol.
        Read the next input symbol, and push this symbol onto the stack.
    }
    else
    {
        Read and discard the next input symbol (which should be a right parenthesis).
        Print the top operation and pop it; keep printing and popping until the next
        symbol on the stack is a left parenthesis. (If no left parenthesis is encountered, then
        print an error message indicating unbalanced parentheses, and halt.) Finally, pop
        the left parenthesis.
    }
while (there is more of the expression to read) ;
3. Print and pop any remaining operations on the stack. (There should be no remaining left
parentheses; if there are, the input expression did not have balanced parentheses.)
```

## 图 7.13 图 7.12 算法的示例计算

### 示例

```
Convert the infix expression:
3 * X + ( Y - 12 ) - Z

(a) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The operand 3 is printed.
Output so far:
3

(b) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The * is pushed.
Output so far:
3

(c) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The operand X is printed.
Output so far:
3 X

(d) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
Pop and print the * since it has higher precedence than the +; then push the +.
Output so far:
3 X *

(e) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
Push the parenthesis.
Output so far:
3 X *

(f) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The operand Y is printed.
Output so far:
3 X * Y

(g) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The - is pushed.
Output so far:
3 X * Y

(h) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The operand 12 is printed.
Output so far:
3 X * Y 12

(i) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
Pop until left parenthesis.
Output so far:
3 X * Y 12 -

(j) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
Pop and print the + since it has precedence equal to the -; then push the -.
Output so far:
3 X * Y 12 - +

(k) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The operand Z is printed.
Output so far:
3 X * Y 12 - + Z

(l) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
Pop any remaining operations.
Output so far:
3 X * Y 12 - + Z -
```

