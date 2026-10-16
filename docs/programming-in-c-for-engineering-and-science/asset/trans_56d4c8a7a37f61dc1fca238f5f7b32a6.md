

一般来说，assert() 机制可以描述如下：

## THE assert() MECHANISM

形式：
```
assert(boolean_expression);
```
其中：

boolean_expression 是任何求值为 true 或 false 的有效表达式。

## PURPOSE:

检查 boolean_expression 是否为 true。如果是，执行正常继续。如果为 false，则终止执行并显示诊断信息。

## 5.2.6 Boolean Character Functions

C 库 cctype 提供了许多布尔值函数，用于对字符值执行有用的检查。其中一些更有用的函数如表 5.1 所示。表中最后还包括了两个用于更改字符大小写的函数。

TABLE 5.1 Character Operations in cctype
| Operation | Description |
|---|---|
| isalnum(ch) | true if ch is a letter or a digit, false otherwise |
| isalpha(ch) | true if ch is a letter, false otherwise |
| iscntrl(ch) | true if ch is a control character, false otherwise |
| isdigit(ch) | true if ch is a decimal digit, false otherwise |
| isgraph(ch) | true if ch is a printing character except space, false otherwise |
| islower(ch) | true if ch is lower case, false otherwise |
| isprint(ch) | true if ch is a printing character, including space, false otherwise |
| ispunct(ch) | true if ch is a punctuation character (not a space, an alphabetic character, or a digit), false otherwise |
| isspace(ch) | true if ch is a white space character (space, '\f', '\n', '\r', '\t', or '\v'), false otherwise |
| isupper(ch) | true if ch is upper case, false otherwise |
| isxdigit(ch) | true if ch is a hexadecimal digit, false otherwise |
| toupper(ch) | returns the uppercase equivalent of ch (if ch is lower case) |
| tolower(ch) | returns the lowercase equivalent of ch (if ch is upper case) |

## 5.3 EXAMPLE: DIGITAL CIRCUITS—A BINARY HALF-ADDER

如前所述，乔治·布尔在 19 世纪中期奠定了电路设计的基礎。布尔形式化了逻辑的若干公理并开发了用于书写逻辑表达式的代数。7 在 1930 年代后期，随着数学家、工程师和物理学家致力于早期计算机的算术和逻辑电路设计，布尔代数的公理和定理变得极其重要。

7 有关布尔代数的更多信息可在本书网站上找到（参见前言）。

这些电路利用三种基本电子元件：与门、或门和非门或反相器，其符号如下：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_134_0.png)

这些门的输入（图中显示为其左侧的短线段）是电电压，并被解释为当其超过某一阈值时为 1（真），或当其低于该阈值时为 0（假）。这些门的输出（图中显示为其右侧的短线段）同样以二进制（0 或 1）解释。对于与门，只有当两个输入都为 1 时才产生 1。或门在任一输入为 1 时产生 1。非门的输出与其输入相反。这三种基本元件因此以与逻辑中的与、或、非运算符相同的方式表现，这意味着我们可以使用布尔表达式来设计和分析电路。

举例说明，考虑我们如何设计一个执行二进制加法的电路：

| + | 0 | 1 |
|---|---|---|
| 0 | 0 | 1 |
| 1 | 1 | 10 |

我们看到电路的输入将是被加的两个二进制数字，并且会有两个二进制输出：和位，即表中条目的最右位，以及进位位，当和为 1 + 1 时为 1，否则为 0。如果我们用 digit1 和 digit2 表示输入，用 sum 和 carry 表示输出，我们得到以下称为真值表的上表版本：

| digit1 | digit2 | carry | sum |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 0 |

注意最后两列的模式。进位输出只有在 digit1 和 digit2 都为 1（真）时才为 1（真），因此我们可以用与门来实现它。和输出只有在 digit1 和 digit2 中恰好有一个为 1（真）时才为 1（真）；即 digit1 或 digit2 为 1（真）但不同时为 1。我们可以用以下布尔表达式表达这些属性，

```
bool carry = digit1 && digit2,
    sum = (digit1 || digit2) && !(digit1 && digit2);
```

并设计以下称为二进制半加器的电路，它将两个二进制数字相加：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_135_0.png)

用程序模拟此类电路的操作是直接的，因为我们只需要对电路建模的布尔表达式进行编码，然后用电路输入的各种组合执行程序即可。例如，示例 5.3 中的程序模拟了二进制半加器的动作。所示的示例运行为 digit1 和 digit2 各读取一个二进制数字（0 或 1），并输出 digit1 和 digit2 的四种不同输入组合下 sum 和 carry 的结果值。一旦我们在本章后面学习了重复结构，我们将能够在不必反复重新执行程序的情况下做到这一点。

## Example 5.3 A Binary Half-Adder

```
/* This program calculates the outputs from boolean expressions that
   represent the logical circuit for a binary half-adder.

   Input:  two binary digits
   Output: two binary values representing the sum and carry that
           result when the input values are added
   ---------------------------------------------------------------*/

#include <iostream>    // cout, cin, <<, >>
using namespace std;

int main()
{
    cout << "Enter two binary inputs: ";
    short digit1, digit2; // the two binary inputs
    cin >> digit1 >> digit2;

    // the two circuit outputs
    bool sum = (digit1 || digit2) && !(digit1 && digit2),
        carry = (digit1 && digit2);
    cout << "Carry = " << carry << " Sum = " << sum << "\n\n";
}
```

## SAMPLE RUNS:

Enter two binary inputs: 0 0
Carry = 0 Sum = 0

```
Enter two binary inputs: 0 1
Carry = 0 Sum = 1

Enter two binary inputs: 1 0
Carry = 0 Sum = 1

Enter two binary inputs: 1 1
Carry = 1 Sum = 0
```

## 5.4 SELECTION: THE IF STATEMENT

如本章开头所述，一些问题需要一种选择其中一个替代动作的结构。在最简单的两种替代情况中，选择基于布尔表达式，其值为真时选择一个替代，为假时选择另一个。在流程图中，这通常被描绘为一个菱形框，其中包含布尔表达式，一个角标记为 true，另一个标记为 false：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_136_0.png)

正如该图清楚地指出的那样，执行将通过 statement₁ 或通过 statement₂，但不会同时通过两者，然后继续到下一个语句。它走哪条路线将由布尔表达式的真假决定。

这种选择结构可以用 C++ if 语句实现，其形式为

```
if (boolean_expression)
    statement₁
else
    statement₂
```

如果布尔表达式为真，则执行第一个语句并跳过后面的 else 及其语句，但如果布尔表达式为假，则跳过第一个语句并执行 else 部分的语句。因此，该语句确实实现了前面所示的两种替代选择结构。

本章开头的示例中的 if 语句（示例 5.1）具有这种形式：

```
if (index < CUTOFF)
    cout << "Safe condition\n";
else
    cout << "Hazardous condition\n";
```

如图所示缩进两个替代以将其区分开来是一种良好的编程实践，我们将在本教材中遵循这种做法。

作为另一个例子，考虑寻找两个实值的较大值的问题。这可以很容易地使用 if 语句完成，如以下代码段所示。

```
double maximum;
if (value1 > value2)
    maximum = value1;
else
    maximum = value2;
```

有时选择结构中的第二个替代为空，如下图所示，其中指定的语句要么被执行要么被跳过：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_137_0.png)

在这种情况下，if 语句中的 else 子句可以省略：

```
if (boolean_expression)
    statement
```

或者它可以是一个仅包含分号的空语句，

```
if (boolean_expression)
    statement
else;
```
