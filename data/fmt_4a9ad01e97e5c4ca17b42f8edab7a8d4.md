
> 类似 C++ 的语言是“移动目标”。随着其演进，可能会向语言中添加更多关键字。避免使用“`object`”等“负载”词作为标识符。即使“`object`”目前不是 C++ 中的关键字，它也可能成为关键字；因此，使用新编译器进行未来编译可能会破坏现有代码。

变量的声明可以放在程序的几乎任何位置，但它们必须在其对应的变量在程序中使用之前出现。例如，在图 2.5 的程序中，第 9 行的声明

```
int number1; // first integer to add
```

本可以放在第 14 行之前

```
std::cin >> number1; // read first integer from user into number1
```

第 13 行

```
std::cout << "Enter first integer: "; // prompt user for data
```

在屏幕上打印字符串`Enter first integer:`。我们喜欢将前面的语句读作“`std::cout` 获取字符字符串 `"Enter first integer: "`。”第 14 行

```
std::cin >> number1; // read first integer from user into number1
```

使用输入流对象`cin`（属于命名空间`std`）和流提取运算符`>>`从键盘获取值。使用流提取运算符与`std::cin`从标准输入流获取字符输入，通常是键盘。我们喜欢将前面的语句读作，“`std::cin`将值赋给`number1`”或简单地说“`std::cin`给`number1`。”

### Error-Prevention Tip 2.2

程序应验证所有输入值的正确性，以防止错误信息影响程序的计算。

当计算机执行前面的语句时，它会等待用户输入变量`number1`的值。用户通过输入整数（作为字符），然后按 Enter 键（有时称为 Return 键）将字符发送给计算机来响应。计算机将数字的字符表示形式转换为整数并分配（即复制）该数字（或值）给变量`number1`。此程序中对`number1`的任何后续引用都将使用此相同的值。

第 16 行

```
std::cout << "Enter second integer: "; // prompt user for data
```

在屏幕上打印`Enter second integer:`，提示用户采取行动。第 17 行

```
std::cin >> number2; // read second integer from user into number2
```

从用户处获取变量`number2`的值。

第 19 行的赋值语句

```
sum = number1 + number2; // add the numbers; store result in sum
```

计算变量`number1`和`number2`的和，并使用赋值运算符`=`将结果赋给变量`sum`。`=`运算符和`+`运算符称为二元运算符，因为每个运算符都有两个操作数。在`+`运算符的情况下，操作数是`number1`和`number2`。在前面的`=`运算符的情况下，操作数是`sum`和表达式`number1 + number2`的值。

第 21 行

```
std::cout << "Sum is " << sum << std::endl; // display sum; end line
```

显示字符字符串`Sum is`，然后是变量`sum`的数值，然后是`std::endl`——一种所谓的流操纵符。名称`endl`是“end line”的缩写，属于命名空间`std`。`std::endl`流操纵符输出换行符，然后“刷新输出缓冲区”。这仅意味着，在某些输出在机器中累积直到“值得”在屏幕上显示的系统上，`std::endl`会强制在那一刻显示任何累积的输出。当输出提示用户执行操作（例如输入数据）时，这可能很重要。

请注意，前面的语句输出多种不同类型的值。流插入运算符“知道”如何输出每种类型的数据。在单个语句中使用多个流插入运算符（`<<`）被称为连接、链接或级联流插入操作。输出多个数据块不需要多个语句。

计算也可以在输出语句中执行。我们本可以将第 19 行和第 21 行的语句合并为语句

```
std::cout << "Sum is " << number1 + number2 << std::endl;
```

从而消除对变量`sum`的需求。

C++ 的一个强大功能是你可以创建自己的数据类型，称为类（我们在第 3 章介绍此功能，并在第 9 章和第 10 章深入探讨）。然后你可以使用`>>`和`<<`运算符“教”C++ 如何输入和输出这些新数据类型的数值（这称为*运算符重载*——我们在第 11 章探讨此主题）。

### 2.5 Arithmetic

图 2.6 总结了 C++ 的*算术运算符*。*星号*（`*`）表示乘法，*百分号*（`%`）是稍后将讨论的取模运算符。图 2.6 中的算术运算符都是二元运算符。

*整数除法*（即分子和分母都是整数）产生整数商；例如，表达式`7 / 4`的值为 1，表达式`17 / 5`的值为 3。请注意，整数除法中任何小数部分都会被丢弃（即截断）——不会进行舍入。

C++ 提供了*取模运算符*`%`，它产生整数除法后的余数。取模运算符只能与整数操作数一起使用。表达式`x % y`产生`x`除以`y`后的余数。因此，`7 % 4`产生 3，`17 % 5`产生 2。在后面的章节中，我们将讨论取模运算符的许多有趣应用，例如确定一个数是否为另一个数的倍数（其特例是确定一个数是奇数还是偶数）。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_75_0.png)

> **Common Programming Error 2.3**
>
> 尝试对非整数操作数使用取模运算符（`%`）是编译错误。

| C++ operation | C++ arithmetic operator | Algebraic expression | C++ expression |
|---|---|---|---|
| Addition | `+` | f + 7 | `f + 7` |
| Subtraction | `-` | p − c | `p - c` |
| Multiplication | `*` | bm or b · m | `b * m` |
| Division | `/` | x / y or x ÷ y | `x / y` |
| Modulus | `%` | r mod s | `r % s` |

**Fig. 2.6**  |  Arithmetic operators.

### Parentheses for Grouping Subexpressions

括号在 C++ 表达式中的使用方式与代数表达式相同。例如，要将`a`乘以`b + c`，我们写成`a * ( b + c )`。

### Rules of Operator Precedence

C++ 以精确的顺序应用算术表达式中的运算符，该顺序由以下*运算符优先级规则*决定，这些规则通常与代数中遵循的规则相同：

1. 表达式中包含在一对括号内的运算符最先求值。括号被称为“最高优先级”。在*嵌套*或*嵌入*括号的情况下，例如

   ```
   ( ( a + b ) + c )
   ```

   最内层一对括号中的运算符最先应用。[*注：与代数一样，允许在表达式中放置不必要的括号以使表达式更清晰。这些称为*冗余括号*。]

2. 乘法、除法和取模运算随后应用。如果表达式包含多个乘法、除法和取模运算，则运算符从左到右应用。乘法、除法和取模被认为处于同一优先级级别。

3. 加法和减法运算最后应用。如果表达式包含多个加法和减法运算，则运算符从左到右应用。加法和减法也具有相同的优先级级别。

运算符优先级的规则集定义了 C++ 应用运算符的顺序。当我们说某些运算符从左到右应用时，我们指的是运算符的*结合性*。例如，在表达式

```
a + b + c
```

中，加法运算符（`+`）从左到右结合，因此先计算`a + b`，然后将`c`加到该和上以确定整个表达式的值。我们将看到某些运算符从右到左结合。图 2.7 总结了这些运算符优先级的规则。随着引入更多 C++ 运算符，该表将被扩展。完整的优先级图表包含在附录 A 中。

### 良好的编程实践 2.5

在复杂算术表达式中使用冗余括号可以使表达式更清晰。

| 运算符 | 操作 | 求值顺序（优先级） |
|---|---|---|
| `( )` | 括号 | 最先求值。如果括号嵌套，则最内层一对中的表达式最先求值。如果有若干对“同一级别”的括号（即未嵌套），则从左到右求值。 |
| `*` | 乘法 | 第二求值。如果有若干个，则从左到右求值。 |
| `/` | 除法 | |
| `%` | 取模 | |
| `+` | 加法 | 最后求值。如果有若干个，则从左到右求值。 |
| `-` | 减法 | |

图 2.7 | 算术运算符的优先级。

### 2.6 决策：相等与关系运算符

本节介绍 C++ 的 if 语句的一个简单版本，允许程序根据某个条件的真假采取不同的行动。如果条件满足，即条件为真，则 if 语句体中的语句被执行。如果条件不满足，即条件为假，则体语句不被执行。我们很快会看到一个例子。

if 语句中的条件可以通过使用图 2.8 中总结的相等运算符和关系运算符来形成。所有关系运算符具有相同的优先级级别并从左到右结合。两个相等运算符具有相同的优先级级别，该级别低于关系运算符的优先级，并从左到右结合。

> **常见编程错误 2.4**
>
> 将相等运算符`==`与赋值运算符`=`混淆会导致逻辑错误。相等运算符应读作“等于”，赋值运算符应读作“得到”或“得到的值”或“被赋值为”。有些人喜欢将相等运算符读作“双等号”。正如我们在第 5.9 节中讨论的那样，混淆这些运算符可能不一定会导致易于识别的语法错误，但可能导致极其微妙的逻辑错误。

以下示例使用六个 if 语句比较用户输入的两个数字。如果这些 if 语句中的任何一个的条件得到满足，则与该 if 语句关联的输出语句将被执行。图 2.9 显示了该程序以及三次示例执行的输入/输出对话框。

第 6–8 行

```
using std::cout;  // program uses cout
using std::cin;   // program uses cin
using std::endl; // program uses endl
```

是使用声明，消除了在早期程序中重复`std::`前缀的需要。一旦我们插入这些使用声明，我们就可以在程序的其余部分中写`cout`而不是`std::cout`，`cin`而不是`std::cin`以及`endl`而不是`std::endl`，分别在程序的其余部分中。[注：从本书此点起，每个示例都包含一个或多个使用声明。]

| 标准代数相等或关系运算符 | C++ 相等或关系运算符 | C++ 条件示例 | C++ 条件含义 |
|---|---|---|---|
| *关系运算符* |  |  |  |
| > | `>` | `x > y` | x 大于 y |
| < | `<` | `x < y` | x 小于 y |
| ≥ | `>=` | `x >= y` | x 大于或等于 y |
| ≤ | `<=` | `x <= y` | x 小于或等于 y |
| *相等运算符* |  |  |  |
| = | `==` | `x == y` | x 等于 y |
| ≠ | `!=` | `x != y` | x 不等于 y |

**图 2.8** | 相等和关系运算符。

```
// Fig. 2.9: fig02_09.cpp
// Comparing integers using if statements, relational operators
// and equality operators.
#include <iostream> // allows program to perform input and output

using std::cout; // program uses cout
using std::cin; // program uses cin
using std::endl; // program uses endl

// function main begins program execution
int main()
{
    int number1; // first integer to compare
    int number2; // second integer to compare

    cout << "Enter two integers to compare: "; // prompt user for data
    cin >> number1 >> number2; // read two integers from user

    if ( number1 == number2 )
        cout << number1 << " == " << number2 << endl;

    if ( number1 != number2 )
        cout << number1 << " != " << number2 << endl;

    if ( number1 < number2 )
        cout << number1 << " < " << number2 << endl;

    if ( number1 > number2 )
        cout << number1 << " > " << number2 << endl;

    if ( number1 <= number2 )
        cout << number1 << " <= " << number2 << endl;

    if ( number1 >= number2 )
        cout << number1 << " >= " << number2 << endl;

    return 0; // indicate that program ended successfully
} // end function main
```

```
Enter two integers to compare: 3 7
3 != 7
3 < 7
3 <= 7
```

图 2.9 | 使用 if 语句、关系运算符和相等运算符比较整数。（第 1 部分，共 2 部分。）

```
Enter two integers to compare: 22 12
22 != 12
22 > 12
22 >= 12
```

图 2.9 | 使用 if 语句、关系运算符和相等运算符比较整数。（第 1 部分，共 2 部分。）

```
Enter two integers to compare: 7 7
7 == 7
7 <= 7
7 >= 7
```

图 2.9 | 使用 if 语句、关系运算符和相等运算符比较整数。

（第 2 部分，共 2 部分。）

### 良好的编程实践 2.6

> 将使用声明放在引用的`#include`之后立即放置。

第 13–14 行

```
int number1; // first integer to compare
int number2; // second integer to compare
```

声明程序中使用的变量。请记住，变量可以在一个声明中声明，也可以在单独的声明中声明。

程序使用级联流提取操作（第 17 行）输入两个整数。请记住，由于第 7 行，我们可以使用`cin`（而不是`std::cin`）。首先将值读入变量`number1`，然后将值读入变量`number2`。

第 19–20 行的 if 语句

```
if ( number1 == number2 )
    cout << number1 << " == " << number2 << endl;
```

比较变量`number1`和`number2`的值以测试相等性。如果值相等，则第 20 行的语句显示一行文本，表明数字相等。如果从第 22、25、28、31 和 34 行开始的 if 语句中的一个或多个条件为真，则相应的体语句显示适当的文本行。

请注意，图 2.9 中的每个 if 语句在其体中只有一个语句，并且每个体语句都是缩进的。在第 4 章中，我们将展示如何指定具有多语句体的 if 语句（通过将体语句括在一对大括号`{ }`中，创建所谓的复合语句或块）。

### 常见编程错误 2.5

> 在 if 语句中条件后的右括号后立即放置分号通常是逻辑错误（尽管不是语法错误）。分号导致 if 语句的体为空，因此无论其条件是否为真，if 语句都不执行任何操作。更糟糕的是，if 语句的原始体语句现在成为与 if 语句顺序排列的语句，并且始终执行，这通常会导致程序产生错误的结果。

图 2.10 显示了本章中介绍的运算符的优先级和结合性。运算符按从上到下递减的优先级顺序显示。请注意：

所有这些运算符，除了赋值运算符`=`之外，都从左到右结合。加法是左结合的，因此像`x + y + z`这样的表达式会被求值，就好像它被写成`(x + y) + z`一样。赋值运算符`=`从右到左结合，因此像`x = y = 0`这样的表达式会被求值，就好像它被写成`x = (y = 0)`一样，正如我们很快就会看到的那样，它首先将`0`赋给`y`，然后将该赋值的結果——`0`——赋给`x`。

| Operators | Associativity | Type |
|---|---|---|
| `()` | left to right | parentheses |
| `*   /   %` | left to right | multiplicative |
| `+   −` | left to right | additive |
| `<<   >>` | left to right | stream insertion/extraction |
| `<   <=   >   >=` | left to right | relational |
| `==   !=` | left to right | equality |
| `=` | right to left | assignment |
