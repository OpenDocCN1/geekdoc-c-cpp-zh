

## The if Statement

基本的 if 语句允许你的程序在给定的条件表达式求值为 true 时执行单个语句，或用大括号括起来的语句块；如果条件求值为 false，则跳过该语句或语句块。这在图 3-1 中有所说明。

![](img/2359b0c604600c58fba3539c738a356e_158_0.png)

Figure 3-1

一个简单的 if 语句示例是：

```
if(letter == 'A')
    cout << "The first capital, alphabetically speaking.";
```

要测试的条件出现在关键字 if 之后紧跟的括号中，其后是条件为 true 时要执行的语句。请注意这里分号的位置。它放在 if 之后的条件与括号之间的语句之后；条件括号之后不应该有分号，因为这两行本质上构成一个单一的语句。你也可以看到 if 之后的语句是如何缩进的，以表明它仅在 if 条件返回 true 值时才执行。缩进对于程序执行不是必要的，但有助于你识别 if 条件与其所依赖的语句之间的关系。代码片段中的输出语句仅在变量 letter 的值为 'A' 时才执行。

你可以扩展此示例以在 letter 包含值 'A' 时更改其值：

```
if(letter == 'A')
{
    cout << "The first capital, alphabetically speaking.";
    letter = 'a';
}
```

由 if 语句控制的语句块由大括号分隔。这里仅当条件 (letter == 'A') 求值为 true 时才执行块中的语句。如果没有大括号，只有第一个语句才是 if 的对象，而将值 'a' 分配给
letter 的语句将始终执行。请注意，块中每个语句之后都有一个分号，而不是块末尾的闭合大括号之后。块中可以包含任意数量的语句。现在，由于 letter 的值为 'A'，你在输出相同消息后将其值更改为 'a'。如果条件返回 false，则这两个语句都不会执行。

## Nested if Statements

当 if 语句中的条件为 true 时要执行的语句也可以是一个 if。这种安排称为嵌套 if。仅当外部 if 的条件为 true 时，才会测试内部 if 的条件。一个嵌套在另一个内部的 if 也可包含嵌套的 if。你通常可以像这样一直嵌套 if，只要你知道自己在做什么。

## Try It Out   Using Nested Ifs

以下是带有工作示例的嵌套 if。

```
// Ex3_01.cpp
// A nested if demonstration
#include <iostream>

using std::cin;
using std::cout;
using std::endl;

int main()
{
    char letter = 0;                    // Store input in here

    cout << endl
         << "Enter a letter: ";        // Prompt for the input
    cin >> letter;                      // then read a character

    if(letter >= 'A')                   // Test for 'A' or larger
        if(letter <= 'Z')               // Test for 'Z' or smaller
        {
            cout << endl
                 << "You entered a capital letter."
                 << endl;
            return 0;
        }

    if(letter >= 'a')                   // Test for 'a' or larger
        if(letter <= 'z')               // Test for 'z' or smaller
        {
            cout << endl
                 << "You entered a small letter."
                 << endl;
            return 0;
        }

    cout << endl << "You did not enter a letter." << endl;
    return 0;
}
```

## How It Works

该程序以通常的注释行开始；然后是支持输入/输出的头文件的 `#include` 语句以及 `cin`、`cout` 和 `endl` 的 using 声明，它们是 `std` 命名空间。`main()` 体内的第一个动作是提示输入一个字母。这存储在名为 `letter` 的 `char` 变量中。

输入后的 `if` 语句检查输入的字符是否大于或等于 `'A'`。由于小写字母的 ASCII 码（97 到 122）大于大写字母的 ASCII 码（65 到 90），输入小写字母会导致程序执行第一个 `if` 块，因为 `(letter >= 'A')` 对所有字母都返回 true。在这种情况下，会执行嵌套的 `if`，它检查输入是否小于或等于 `'Z'`。如果它小于或等于 `'Z'`，你就知道你有一个大写字母，消息会被显示，然后你就完成了，因此你执行 `return` 语句以结束程序。两个语句都用大括号括起来，因此当嵌套 `if` 条件返回 true 时两者都会执行。

下一个 `if` 检查输入的字符是否为小写，使用与第一个 `if` 基本相同的机制，显示消息并返回。

如果输入的字符不是字母，则最后 `if` 块之后的输出语句会被执行。这会显示一条消息，表明输入的字符不是字母。然后执行 `return`。

你可以看到，由于对每个嵌套 if 和输出语句应用了缩进，它们之间的关系更容易跟踪。

此示例的典型输出是：

```
Enter a letter: T
You entered a capital letter.
```

你只需在检查大写的 `if` 中添加一个额外的语句，就很容易安排将大写更改为小写：

```
if(letter >= 'A')                 // Test for 'A' or larger
    if(letter <= 'Z')              // Test for 'Z' or smaller
    {
        cout << endl
             << "You entered a capital letter.";
             << endl;

        letter += 'a' - 'A';        // Convert to lowercase

        return 0;
    }
```

这涉及添加一个额外的语句。此用于将大写转换为小写的语句通过值 `'a' - 'A'` 增加 `letter` 变量。它之所以有效，是因为 `'A'` 到 `'Z'` 和 `'a'` 到 `'z'` 的 ASCII 码是两组连续的数值代码，因此表达式 `'a' - 'A'` 表示要添加到大写字母以获得等效小写字母的值。

此程序的典型输出是：

```
Enter an integer less than 2 billion: 123456
Your number is even,
```

## How It Works

读取输入值到 number 之后，值通过取除以二后的余数进行测试（使用你在上一章看到的余数运算符 %）并将其用作 if 的条件。在这种情况下，if 语句的条件返回一个整数，而不是布尔值。if 语句将条件返回的非零值解释为 true，并将零解释为 false。换句话说，if 语句的条件表达式：

```
(number % 2L)
```

等价于

```
(number % 2L != 0)
```

如果余数为 1，条件为 true，if 之后的语句立即执行。如果余数为 0，条件为 false，else 关键字之后的语句被执行。

> 在 if 语句中，条件可以是一个表达式，其结果为你在第 2 章看到的基本数据类型中的任何一种。当条件表达式求值为数值而不是 if 语句所需的 bool 值时，编译器会插入对表达式结果的自动强制转换为类型 bool。强制转换为类型 bool 的非零值会得到 true，而零值会得到 false。

由于整数除以二的余数只能为一或零，我已对代码进行了注释以表明这一事实。在任一结果之后，都会执行 return 语句以结束程序。

> else 关键字与语句的 if 部分类似，不带分号。同样，缩进被用作各种语句之间关系的可视指示。你可以清楚地看到哪个语句在 true 或非零结果时执行，哪个在 false 或零结果时执行。你应该始终缩进程序中的语句以显示其逻辑结构。

if-else 组合提供了在两个选项之间进行选择。if-else 的一般逻辑如图 3-2 所示。

