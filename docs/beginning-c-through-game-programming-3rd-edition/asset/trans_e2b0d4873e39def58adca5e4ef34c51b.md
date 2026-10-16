

值也可以被解释为真或假。任何非零值都可以解释为真，而 0 可以解释为假。

一种常见的可解释为真或假的表达式涉及比较事物。比较通常通过内置的关系运算符来完成。表 2.1 列出了这些运算符和一些示例表达式。

表 2.1 关系运算符

运算符 | 含义 | 示例表达式 | 计算结果
---|---|---|---
== | 等于 | 5 == 5 | 真
 |  | 5 == 8 | 假
!= | 不等于 | 5 != 8 | 真
 |  | 5 != 5 | 假
> | 大于 | 8 > 5 | 真
 |  | 5 > 8 | 假
< | 小于 | 5 < 8 | 真
 |  | 8 < 5 | 假
>= | 大于或等于 | 8 >= 5 | 真
 |  | 5 >= 8 | 假
<= | 小于或等于 | 5 <= 8 | 真
 |  | 8 <= 5 | 假

## 使用 IF 语句

好了，是时候让真和假的概念发挥作用了。你可以使用 if 语句来测试一个表达式是否为真，并根据结果执行一些代码。下面是 if 语句的一种简单形式：

```
if (expression)
    statement;
```

如果 expression 为真，则执行 statement。否则，跳过 statement，程序分支到 if 语句之后的语句。

### 提示

> 每当你看到前面的代码示例中那样的一般性语句时，你都可以用单个语句或语句块来替换它，因为语句块被视为一个整体。

## 介绍 Score Rater 程序

Score Rater 程序使用 if 语句对玩家的分数进行评价。图 2.1 显示了该程序的运行效果。

![](img/34f09be0ed6217c465debc4490197d4f_63_0.png)

图 2.1
根据不同的 if 语句，消息会被显示（或不会显示）。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载该程序的代码。程序位于第 2 章文件夹中；文件名为 score_rater.cpp。

```
// Score Rater
// Demonstrates the if statement

#include <iostream>
using namespace std;

int main()
{
    if (true)
    {
        cout << "This is always displayed.\n\n";
    }
```

```
if (false)
{
    cout << "This is never displayed.\n\n";
}

int score = 1000;

if (score)
{
    cout << "At least you didn't score zero.\n\n";
}

if (score >= 250)
{
    cout << "You scored 250 or more. Decent.\n\n";
}

if (score >= 500)
{
    cout << "You scored 500 or more. Nice.\n\n";

    if (score >= 1000)
    {
        cout << "You scored 1000 or more. Impressive!\n";
    }
}

return 0;
}
```

## 测试真和假

在第一个 if 语句中，我测试了 true。因为 true 本来就是真的，所以程序显示消息“This is always displayed.”

```
if (true)
{
    cout << "This is always displayed.\n\n";
}
```

在下一个 if 语句中，我测试了 false。因为 false 不是真的，所以程序不会显示消息“This is never displayed.”

```
if (false)
{
    cout << "This is never displayed.\n\n";
}
```

### 陷阱

注意，在 if 语句中，你测试的表达式右括号后面不要加分号。如果你加了分号，就会创建一条与 if 语句配对的空语句，这实际上会使 if 语句失去作用。下面是一个例子：

```
if (false);
{
    cout << "This is never displayed.\n\n";
}
```

在 (false) 后面加上分号后，我创建了一条与 if 语句关联的空语句。前面的代码等同于：

```
if (false)
    ; // 一条空语句，什么也不做
{
    cout << "This is never displayed.\n\n";
}
```

我只是玩了下空白符，这并不会改变代码的含义。现在问题应该很清楚了。if 语句看到 false 值，于是跳过下一条语句（空语句）。然后程序继续愉快地执行 if 语句之后的语句，也就是显示消息“This is never displayed.”

要警惕这种错误。这是一个容易犯的错误，而且由于它并不违法，不会产生编译错误。

## 将值解释为真或假

你可以将任何值解释为真或假。任何非零值都可以解释为真，而 0 可以解释为假。我在下一个 if 语句中对此进行了测试：

```
if (score)
{
    cout << "At least you didn't score zero.\n\n";
}
```

score 是 1000，所以它是非零值，被解释为真。结果，消息“Okay, at least you didn't score zero.”被显示出来。

## 使用关系运算符

你可能在 `if` 语句中使用的最常见表达式，就是通过关系运算符比较值。这正是我接下来要演示的内容。我测试了分数是否大于或等于 250。

```
if (score >= 250)
{
    cout << "You scored 250 or more. Decent.\n\n";
}
```

因为 `score` 是 1000，所以语句块被执行，显示出玩家获得了不错分数的消息。如果 `score` 小于 1000，语句块就会被跳过，程序会继续执行语句块之后的语句。

### 陷阱

等于的关系运算符是 `==`（连续两个等号）。不要把它与 `=`（一个等号）混淆，后者是赋值运算符。

虽然用赋值运算符代替等于的关系运算符并不违法，但结果可能出乎你的意料。看看这段代码：

```
int score = 500;
if (score = 1000)
{
    cout << "You scored 1000 or more. Impressive!\n";
}
```

这段代码的结果是，`score` 被设置为 1000，并且消息“You scored 1000 or more. Impressive!”被显示出来。过程是这样的：虽然 `score` 在 `if` 语句之前是 500，但那已经改变了。当 `if` 语句的表达式 (`score = 1000`) 被求值时，`score` 被赋值为 1000。赋值语句的求值结果是 1000，因为这是一个非零值，所以表达式被解释为 `true`。结果，字符串被显示出来。

要警惕这种类型的错误。它很容易犯，并且在某些情况下（比如这个例子），它不会引起编译错误。

## 嵌套 if 语句

一个 `if` 语句可以让程序执行一条语句或一个语句块，其中可以包括其他 `if` 语句。当你编写一个 `if` 语句

## 介绍 Score Rater 2.0 程序

Score Rater 2.0 程序也会对用户输入的分数进行评价。但这一次，程序使用了带 `else` 子句的 `if` 语句。图 2.2 和图 2.3 显示了程序根据用户输入的分数可能显示的两种不同消息。

![](img/34f09be0ed6217c465debc4490197d4f_68_0.png)

**图 2.2**  
如果用户输入 1000 或更高的分数，他会得到祝贺。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载该程序的代码。程序位于第 2 章文件夹中；文件名为 `score_rater2.cpp`。

```
```cpp
// Score Rater 2.0
// Demonstrates an else clause

#include <iostream>
using namespace std;

int main()
{
    int score;
    cout << "Enter your score: ";
```
```

```
cin >> score;

if (score >= 1000)
{
    cout << "You scored 1000 or more. Impressive!\n";
}
else
{
    cout << "You scored less than 1000.\n";
}

return 0;
}
```

![](img/34f09be0ed6217c465debc4490197d4f_69_0.png)

图 2.3
如果用户输入小于 1000 的分数，则不会有庆祝。

## 创建两条分支路径

你已经看到了 if 语句的第一部分，它的工作方式与之前一样。如果 score 大于 1000，就会显示消息“You scored 1000 or more. Impressive!”。

```
if (score >= 1000)
{
    cout << "You scored 1000 or more. Impressive!\n";
}
```

这里的新颖之处在于，else 子句为程序在表达式为假时提供了一条分支语句。因此，如果 (score >= 1000) 为假，程序就会跳过第一条消息，转而显示消息“You scored less than 1000.”。

```
else
{
    cout << "You scored less than 1000.\n";
}
```

## 使用带 ELSE 子句的 IF 语句序列

你可以将带 else 子句的 if 语句串联起来，创建一系列按顺序测试的表达式。第一个测试为真的表达式所关联的语句会被执行；否则，会执行最后一个（可选的）else 子句所关联的语句。下面是这样一系列语句的形式：

```
if (expression1)
    statement1;
else if (expression2)
    statement2;
...
else if (expressionN)
    statementN;
else
    statementN+1;
```

如果 expression1 为真，则执行 statement1，并跳过序列中的其余代码。否则，测试 expression2；如果为真，则执行 statement2，并跳过序列中的其余代码。计算机会依次检查每个表达式（一直到 expressionN），并执行第一个为真表达式所关联的语句。如果没有表达式为真，则执行最后一个 else 子句所关联的语句，即 statementN+1。

