

![](img/59a3417a6d5906fae6d8000d4c2cff76_93_0.png)

# 图 5-3：判断数字是否为偶数的程序流程图

现在让我们分析该程序的工作原理。在遵循这段文字说明时，你可能会发现流程图是一个非常有视觉辅助工具。

程序首先提示用户输入一个数字。然后将该输入存储在整数变量 `num` 中。

程序接着计算关系表达式 `num % 2 == 0`，该表达式跟在 `if` 关键字后的括号内。该表达式涉及两个运算符：算术取模运算符 (`%`) 和关系相等运算符 (`==`)。由于算术运算符的优先级高于关系运算符，将先求值表达式 `num % 2`，然后将结果与零进行比较。

如果一个数字除以二的余数为零，则该数字为偶数。你在第 4 章中学习过取模运算符将返回整数除法的余数。因此，表达式 `num % 2` 将用户输入的数字除以二，并返回余数。该余数将使用关系相等运算符与零进行比较。

如果关系表达式为真（即用户输入的数字是偶数），则执行条件语句，输出“The number is even.”。如果关系表达式为假（即用户输入的数字是奇数），则跳过条件语句，不进行执行。

## 缩进

对条件语句进行缩进是一个良好的习惯。

```cpp
if ( num % 2 == 0 ); // 不要在这里放分号！
   cout << "The number is even" << endl;
```

虽然编译器不在乎你是否缩进，但缩进可以让你这个程序员更容易看出该语句是条件的。

## 常见错误

在多年入门编程课程中教授 C++ 期间，我注意到编写语句时存在几种常见错误。其中一些错误可能会导致编译器错误，并且容易避免。然而，其他错误更难识别，因为它们在编译时或运行时都不会产生错误，而是产生不符合逻辑的结果。

## 不要在此关系表达式后放置分号！

第一个常见错误是在关系表达式后放置了分号：

```cpp
if ( num % 2 == 0 ); // 不要在这里放分号！
cout << "The number is even" << endl;
```

由于编译器通常会忽略空格，接下来的 `if` 语句是相同的，而且视觉上更直观：

```cpp
if ( num % 2 == 0 )
    // 不要在这里放分号！
cout << "The number is even*" << endl;
```

不会产生编译器错误。编译器会从该语句认为这是一个空语句。空语句没有任何作用，在 C++ 中是完全合法的，而且在这里它确实是有用途的。

一个后果是，如果关系表达式为真，空语句将被执行。如果发生这种情况，到为止还没有造成损害。

然而，还有一个后果，即不符合逻辑的结果。代码语句 "The number is even" 无论关系表达式真假都会执行。换句话说，如果输入一个奇数，程序将输出 "The number is even."

Enter a whole number: 17
The number is even

代码语句无论关系表达式真假都会执行的原因是，该代码语句不再是语句的一部分。除非你使用大括号来解释跟在关键字和关系表达式之后的第一个语句是条件的。那个第一个条件语句由于其表达式后的分号而是一个空语句。

## 多个条件语句需要大括号

如前所述：

```cpp
if ( num % 2 == 0 )
    cout << "The number is even" << endl;
cout << "And the number is not odd" << endl;
```

注意：缩进告诉程序员哪个语句是条件的，哪个不是。编译器忽略缩进。

如果用户输入像 17 这样的奇数，由于关系表达式为假，语句 "The number is even" 将不会显示。然而，接下来的语句 "And the number is not odd" 将显示，该语句不属于 `if` 语句。

Enter a whole number: 17
And the number is not odd

如果你让多个语句成为整体语句的一部分，必须将这些语句括在大括号中：

```cpp
if ( num % 2 == 0 )
{
    cout << "The number is even" << endl;
    cout << "And the number is not odd" << endl;
}
```

现在，第二个语句只有在 `if` 表达式为真时才会执行。

当你想要让多个语句变为条件时忘记这些大括号是另一种常见的语法错误。

## 不要误用赋值运算符！

第三种常见的语法错误是使用赋值运算符代替关系相等运算符，因为赋值运算符看起来像等号：

```cpp
if ( num % 2 = 0 ) // 错误的运算符！
cout << "The number is even" << endl;
```

结果是，`if` 表达式将求值为一个比较的结果。相反，它将对括号内的表达式求值为赋值的最终结果，其中非零值被视为真，零被视为假。

注意：某些编译器会将此错误视为编译器错误。

![](img/59a3417a6d5906fae6d8000d4c2cff76_95_0.png)

## if / else 语句

测试数字是否为偶数的程序有一个问题：如果数字是奇数，则没有输出。虽然当关系表达式为真时有一个条件语句 $if$，但当关系表达式为假时没有对应的条件语句（`cout << "The number is odd"`）。

解决方案是在 `if` 语句中添加一个 `else` 部分。结果是一个 `if / else` 语句。

```cpp
if (relational expression)
    conditional statement;
else
    conditional statement;
```

因此，可以修改程序以为 `if` 语句添加一个 `else` 部分：

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    int num;
    cout << "Enter a whole number: ";
    cin >> num;
    if ( num % 2 == 0 )
        cout << "The number is even" << endl;
    else
        cout << "The number is odd" << endl;
        return 0;
}
```

运行这段代码。如果输入的数字是偶数，输出再次是 "The number is even."。然而，如果现在数字是奇数，输出不再是之前的，而是 "The number is odd,"。

Enter a whole number: 17
The number is odd

图 5-4 使用流程图说明了该程序。

![](img/59a3417a6d5906fae6d8000d4c2cff76_97_0.png)

**图 5-4：输出偶数或奇数的程序的流程图**

## 条件运算符

该程序可以使用条件运算符重写。

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    int num;
    cout << "Enter a whole number: ";
    cin >> num;
    cout << "The number is " << (num % 2 == 0) ? "even" : "odd" << endl;
    return 0;
}
```

条件运算符的语法是 [关系表达式] ? [真时的语句] : [假时的语句]

在这个例子中，关系表达式是 `num % 2 == 0`。如果关系表达式的值为真，输出 "even"。然而，如果关系表达式的值为假，输出 "odd"。

条件运算符需要三个操作数：关系表达式和两个条件语句。因此，它被视为三元运算符。

## 常见错误

就像 `if` 语句一样，我在入门编程课程中教授 C++ 时，注意到 `else` 语句有很多语法错误。

## 没有 if 就没有 else

你可以有一个没有 `else` 部分的表达式。但你可以在没有 `if` 的情况下有一个 `else` 部分。合法的部分必须是 `if` 语句的一部分。因此，`else` 部分的作用是“以上皆非”；没有 `if` 部分就没有

