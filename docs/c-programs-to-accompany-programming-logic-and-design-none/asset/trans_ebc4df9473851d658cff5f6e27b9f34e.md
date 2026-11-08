
如图 4-2 所示，添加括号后仍然需要五步，但求值顺序改变了，结果也随之改变。

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_63_0.png)

图 4-2 使用带括号的关系运算符和逻辑运算符对表达式进行求值

## 比较字符串

在 C++ 中，比较字符串对象时，可以使用与比较数值数据类型（如 `int` 和 `double`）时相同的关系运算符。

下面的代码演示了如何使用相等运算符比较两个字符串对象，以及比较一个字符串对象和一个字符串常量：

```cpp
string s1 = "Hello";
string s2 = "World";
// The following test evaluates to false because "Hello" is not the
// same as "World".
if (s1 == s2)
    // code written here executes if true
else
    // code written here executes if false

// The following test evaluates to true because "Hello" is the same
// as "Hello".
if (s1 == "Hello")
    // code written here executes if true
else
    // code written here executes if false

// The following test evaluates to false because "Hello" is not the
// same as "hello".
if (s1 == "hello")
    // code written here executes if true
else
    // code written here executes if false
```

> **注意** 当两个字符串的内容相同时，它们相等。

> **注意** C++ 是区分大小写的，这意味着 C++ 不认为小写“h”与大写“H”相等，因为它们的 ASCII 值不同。小写“h”的 ASCII 值是 104，大写“H”的 ASCII 值是 72。ASCII 值表可在 *《编程逻辑与设计（第五版）》* 的附录 C“理解数制与计算机代码”中找到。

下面的代码演示了如何使用其他关系运算符比较两个 `string` 对象，以及比较一个 `string` 对象和一个 `string` 常量：

```cpp
string s1 = "Hello";
string s2 = "World";
// The following test evaluates to false because "Hello" is not
// greater than "World".
if (s1 > s2)
    // code written here executes if true
else
    // code written here executes if false

// The following test evaluates to true because "Hello" is the same as
// "Hello".
if (s1 <= "Hello")
    // code written here executes if true
else
    // code written here executes if false
```

当你比较 `string` 时，C++ 会比较 `string` 中各个字符的 ASCII 值，根据 `string` 中文本的字母顺序来确定一个 `string` 是否大于、小于或等于另一个 `string`。如前面的代码所示，值为 "Hello" 的 `string` 对象 s1 不大于值为 "World" 的 `string` 对象 s2，因为按字母顺序 World 排在 Hello 之后。

下面的代码示例展示了将关系运算符用于两个 `string` 对象的更多示例：

```cpp
string s1 = "whole";
string s2 = "whale";
// The next statement evaluates to true because the contents of
// s1, "whole", are greater than the contents of s2, "whale".
if (s1 > s2)
    // code written here executes if true
else
    // code written here executes if false

// The next statement evaluates to true because the contents of s2,
// "whale", are less than the contents of s1, "whole".
if (s2 < s1)
    // code written here executes if true
else
    // code written here executes if false

// The next statement evaluates to true because the contents of s1,
// "whole", are the same as the string constant, "whole".
if (s1 == "whole")
    // code written here executes if true
else
    // code written here executes if false
```

## 判断语句

程序中的每个判断都基于表达式计算结果为 `true` 还是 `false`。程序员使用判断语句来改变程序中的控制流。**控制流**是指语句执行的顺序。判断语句也被称为**分支语句**，因为它们让计算机做出决策，从程序中的一个或多个分支（或路径）中进行选择。

C++ 中有不同类型的判断语句。我们将从 `if` 语句开始。

### `if` 语句

`if` 语句是一种单路径判断语句。正如你在 *《编程逻辑与设计（第五版）》* 中学到的，`if` 语句也被称为“单分支”或“单边”语句。

当我们使用“单路径”这个术语时，意思是如果表达式计算结果为 `true`，程序将执行一条或多条语句；但如果表达式计算结果为 `false`，程序将不会执行这些语句。这里只定义了一条路径——即表达式计算结果为 `true` 时所走的路径。无论哪种情况，`if` 语句之后的下一条语句都会执行。

在 C++ 中编写 `if` 语句的语法（或规则集）如下：

```cpp
if (expression)
    statementA;
```

请注意，当你输入关键字 `if` 开始一条 `if` 语句时，需要在后面跟上放在括号内的表达式。

当编译器遇到 `if` 语句时，会计算括号内的表达式。如果表达式计算结果为 `true`，计算机将执行 `statementA`。如果括号内的表达式计算结果为 `false`，计算机将不会执行 `statementA`。请记住，无论表达式计算结果为 `true` 并执行 `statementA`，还是表达式计算结果为 `false` 而不执行 `statementA`，接下来都会执行 `if` 语句之后的下一条语句。

请注意，C++ 语句（例如 `if` 语句）可以是简单语句，也可以是块语句。**块**语句由多条 C++ 语句组成。C++ 将块定义为一对花括号内的语句。如果你希望程序在 `if` 语句中执行多条语句，则必须将这些语句括在一对花括号中，否则只会执行一条语句。下面的示例演示了一条 `if` 语句，它使用关系运算符 `<` 来测试变量 `customerAge` 的值是否小于 65。你会在第四行看到第一个左花括号，在第七行看到第二个右花括号。

```cpp
int customerAge = 53;
int discount = 10, numUnder_65 = 0;
if(customerAge < 65)
{
    discount = 0;
    numUnder_65 += 1;
}
cout << "Discount : " << discount << endl;
cout << "Number of customers under 65 is: " << numUnder_65 << endl;
```

在前面的代码中，名为 `customerAge` 的变量被初始化为 53。由于 53 小于 65，表达式 `customerAge < 65` 的计算结果为 true，因此块语句执行。块语句由花括号内的两条赋值语句组成：`discount = 0;` 和 `numUnder_65 += 1;`。如果表达式计算结果为 false，则块语句不执行。无论哪种情况，接下来要执行的语句都是输出语句 `cout << "Discount : " << discount << endl;`。

注意，在带有 `if` 和待测试表达式的那一行末尾，不要加上分号。这样做不会导致语法错误，但可能会在程序中造成逻辑错误。**逻辑错误**会导致程序产生不正确的结果。在 C++ 中，分号 (;) 被称为空语句，被视为合法语句。**空**语句是什么都不做的语句。请看下面的代码：

```cpp
if (customerAge < 65); // semicolon here is not correct
{
    discount = 0;
    numUnder_65 += 1;
}
```

如果你按照上面的代码编写 `if` 语句，程序将测试表达式 `customerAge < 65`。如果计算结果为 true，则执行空语句，这意味着程序什么也不做；然后执行语句 `discount = 0;`，因为这是 `if` 语句之后的下一条语句。这不会在程序中造成逻辑错误，但请考虑当 `if` 语句中的表达式计算结果为 false 时会发生什么。如果为 false，空语句不会执行，但语句 `discount = 0;` 仍会执行，因为它是 `if` 语句之后的下一条语句。

下面的代码使用 `if` 语句测试两个字符串对象是否相等：

```cpp
string dentPlan = "Y";
if (dentPlan == "Y")
    grossPay = grossPay - 23.50;
```
