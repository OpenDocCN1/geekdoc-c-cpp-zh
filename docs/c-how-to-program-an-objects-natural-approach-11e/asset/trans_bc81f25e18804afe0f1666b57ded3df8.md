

不需要括号。乘法先执行，因为它的优先级高于加法。

## 二次多项式求值

为了更好地理解运算符优先级规则，考虑二次多项式 *y* = *ax² + bx + c* 的求值：

![](img/7b5e2088e71c7f78681d4ddbcf104c06_136_0.png)

在 C++ 中没有幂运算的算术运算符，因此我们将 *x²* 表示为 `x * x`。语句下方带圆圈的数字表示 C++ 应用运算符的顺序。赋值运算符最后应用，因为它在语句中的优先级最低。

假设上述二次多项式中的变量 *a*、*b*、*c* 和 *x* 按如下方式初始化：`a = 2`、`b = 3`、`c = 7` 和 `x = 5`。下图说明了运算符的应用顺序以及表达式的最终值：

- 1. `y = 2 * 5 * 5 + 3 * 5 + 7;` — 最左边的乘法。`2 * 5 is 10`。
- 2. `y = 10 * 5 + 3 * 5 + 7;` — 最左边的乘法。`10 * 5 is 50`。
- 3. `y = 50 + 3 * 5 + 7;` — 乘法先于加法。`3 * 5 is 15`。
- 4. `y = 50 + 15 + 7;` — 最左边的加法。`50 + 15 is 65`。
- 5. `y = 65 + 7;` — 最后的加法。`65 + 7 is 72`。
- 6. `y = 72` — 低优先级赋值；将 72 存入 *y*。

## 冗余括号

与代数中一样，在表达式中放置不必要的括号以使其更清晰是可接受的。这些括号称为冗余括号。例如，二次多项式可以加括号如下：

```
y = (a * x * x) + (b * x) + c;
```

## 使用 if 语句

图 2.5 中的程序（后面有多次执行示例）使用六个 if 语句来比较用户输入的两个整数。如果某个 if 语句的条件为真，则该 if 语句体中的输出语句执行。如果条件为假，则跳过体中的输出语句。

```cpp
// fig02_05.cpp
// Comparing integers using if statements, relational operators
// and equality operators.
#include <iostream> // enables program to perform input and output

using std::cout; // program uses cout
using std::cin; // program uses cin

// function main begins program execution
int main() {
   int number1{0}; // first integer to compare (initialized to 0)
   int number2{0}; // second integer to compare (initialized to 0)

   cout << "Enter two integers to compare: "; // prompt user for data
   cin >> number1 >> number2; // read two integers

   if (number1 == number2) {
      cout << number1 << " == " << number2 << "\n";
   }

   if (number1 != number2) {
      cout << number1 << " != " << number2 << "\n";
   }

   if (number1 < number2) {
      cout << number1 << " < " << number2 << "\n";
   }

   if (number1 > number2) {
      cout << number1 << " > " << number2 << "\n";
   }

   if (number1 <= number2) {
      cout << number1 << " <= " << number2 << "\n";
   }

   if (number1 >= number2) {
      cout << number1 << " >= " << number2 << "\n";
   }
} // end function main
```

```text
Enter two integers to compare: 3 7
3 != 7
3 < 7
3 <= 7
```

**图 2.5** | 使用 if 语句、关系运算符和相等运算符比较整数。（第 1 部分，共 2 部分。）

```text
Enter two integers to compare: 22 12
22 != 12
22 > 12
22 >= 12
```

```text
Enter two integers to compare: 7 7
7 == 7
7 <= 7
7 >= 7
```

**图 2.5** | 使用 if 语句、关系运算符和相等运算符比较整数。（第 2 部分，共 2 部分。）

### using 声明

第 6–7 行

```cpp
using std::cout; // program uses cout
using std::cin; // program uses cin
```

是 using 声明，它消除了像早期程序中那样重复 std:: 前缀的需要。现在我们在程序的其余部分可以直接写 cout 而不是 std::cout，写 cin 而不是 std::cin。

### using 指令

许多程序员倾向于使用 using 指令来代替第 6–7 行

```cpp
using namespace std;
```

它使你的程序无需 std:: 限定即可使用 std 命名空间中的名称。在早期章节中，我们将使用此指令来简化代码，² 但在第 6 章中，我们将重新使用 std::，这被认为是良好实践，并且可以帮助你避免一些微妙的编码错误。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_139_0.png)

### 变量声明与从用户读取输入

第 11–12 行

```cpp
int number1{0}; // first integer to compare (initialized to 0)
int number2{0}; // second integer to compare (initialized to 0)
```

声明程序中使用的变量并将它们初始化为 0。

第 15 行

```cpp
cin >> number1 >> number2; // read two integers from user
```

使用级联的流提取运算来输入两个整数。回想一下，由于第 7 行的原因，我们可以写 cin（而不是 std::cin）。该语句首先读取一个值到 number1，然后读取另一个值到 number2。

2. 在第 20 章中，我们将讨论在大型系统中使用 using 指令的一些缺点。

### 比较数字

第 17–19 行中的 if 语句

```cpp
if (number1 == number2) {
    cout << number1 << " == " << number2 << "\n";
}
```

确定变量 number1 和 number2 的值是否相等。如果相等，则输出语句（第 18 行）显示一行文本，指示这两个数字相等。对于从第 21、25、29、33 和 37 行开始的其他 if 语句中每个为真的条件，相应的输出语句会显示一行适当的文本。

### 花括号与块

图 2.5 中的每个 if 语句都包含一个缩进的单条语句体，以增强可读性。此外，请注意我们将每个语句体都括在一对花括号 { } 中，这形成了所谓的复合语句或块。

对于单条语句体，你不需要使用花括号，但对于多条语句体，必须包含花括号。忘记将多条语句体括在花括号中会导致错误。为避免此类错误，作为规则，始终将 if 语句的语句体括在花括号中。此外，缩进 if 语句块中的语句以增强可读性。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_140_0.png)

### 常见逻辑错误：在条件后放置分号

在 if 语句条件的右括号后紧跟一个分号通常是逻辑错误（虽然不是语法错误）。分号使 if 语句体为空，因此无论条件是否为真，if 语句都不执行任何操作。更糟糕的是，if 语句原来的语句体现在变成与 if 语句顺序执行的一条语句，并且总是执行，这常常导致程序产生不正确的结果。我们首选的三个编译器都会对此逻辑错误发出警告。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_140_1.png)

### 拆分过长语句

过长的语句可以分布在多行中。如果必须这样做，请选择有意义的断点，例如在逗号分隔列表中的逗号之后，或在长表达式中的运算符之后。如果一条语句被拆分为两行或多行，缩进所有后续行是一种良好的实践。

### 运算符优先级与结合性

除赋值运算符 = 外，本章介绍的所有运算符都从左到右结合。赋值运算符（=）从右到左结合。因此，像 `x = y = 0` 这样的表达式求值时，就如同写成了 `x = (y = 0)`，它首先将 0 赋给 y，然后将该赋值的结果——即 y 的值（现在为 0）——赋给 x。

在编写包含许多运算符的表达式时，请参阅 https://en.cppreference.com/w/cpp/language/operator_precedence 上的完整运算符优先级表。确认表达式中的运算符按你期望的顺序执行。如果你不确定复杂表达式中的求值顺序，可以将表达式拆分为一系列较小的语句，或使用括号来强制求值顺序，就像在代数表达式中那样。

