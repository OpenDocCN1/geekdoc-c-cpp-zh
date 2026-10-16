
一个 `if` 语句可以让程序执行一条语句或一个语句块，其中可以包括其他 `if` 语句。当你编写一个 `if` 语句

## 介绍 Score Rater 2.0 程序

Score Rater 2.0 程序也会对用户输入的分数进行评价。但这一次，程序使用了带 `else` 子句的 `if` 语句。图 2.2 和图 2.3 显示了程序根据用户输入的分数可能显示的两种不同消息。

![](img/34f09be0ed6217c465debc4490197d4f_68_0.png)

**图 2.2**

如果用户输入 1000 或更高的分数，他会得到祝贺。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载该程序的代码。程序位于第 2 章文件夹中；文件名为 `score_rater2.cpp`。

```cpp
// Score Rater 2.0

// Demonstrates an else clause

#include <iostream>

using namespace std;

int main()

{

    int score;

    cout << "Enter your score: ";

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

你已经看到了 `if` 语句的第一部分，它的工作方式与之前一样。如果 `score` 大于 1000，就会显示消息“You scored 1000 or more. Impressive!”。

```cpp
if (score >= 1000)
{
    cout << "You scored 1000 or more. Impressive!\n";
}
```

这里的新颖之处在于，`else` 子句为程序在表达式为假时提供了一条分支语句。因此，如果 `(score >= 1000)` 为假，程序就会跳过第一条消息，转而显示消息“You scored less than 1000.”。

```cpp
else
{
    cout << "You scored less than 1000.\n";
}
```

## 使用带 ELSE 子句的 IF 语句序列

你可以将带 `else` 子句的 `if` 语句串联起来，创建一系列按顺序测试的表达式。第一个测试为真的表达式所关联的语句会被执行；否则，会执行最后一个（可选的）`else` 子句所关联的语句。下面是这样一系列语句的形式：

```cpp
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

如果 `expression1` 为真，则执行 `statement1`，并跳过序列中的其余代码。否则，测试 `expression2`；如果为真，则执行 `statement2`，并跳过序列中的其余代码。计算机会依次检查每个表达式（一直到 `expressionN`），并执行第一个为真表达式所关联的语句。如果没有表达式为真，则执行最后一个 `else` 子句所关联的语句，即 `statementN+1`。

## 介绍评分器 3.0 程序

评分器 3.0 程序也会对用户输入的分数进行评级。但这一次，程序使用了一系列带 `else` 子句的 `if` 语句。图 2.4 显示了程序的运行结果。

![](img/34f09be0ed6217c465debc4490197d4f_71_0.png)

图 2.4

根据分数的不同，用户会收到多条消息中的一条。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载该程序的代码。程序位于第 2 章文件夹中；文件名是 `score_rater3.cpp`。

```cpp
// Score Rater 3.0
// Demonstrates if else-if else suite

#include <iostream>
using namespace std;

int main()
{
    int score;
    cout << "Enter your score: ";
    cin >> score;

    if (score >= 1000)
    {
        cout << "You scored 1000 or more. Impressive!\n";
    }
    else if (score >= 500)
    {
        cout << "You scored 500 or more. Nice.\n";
    }
    else if (score >= 250)
    {
        cout << "You scored 250 or more. Decent.\n";
    }
    else
    {
        cout << "You scored less than 250. Nothing to brag about.\n";
    }

    return 0;
}
```

## 创建带 else 子句的 if 语句序列

这个序列的第一部分你已经见过两次了，这次它的工作方式完全相同。如果 `score` 大于或等于 1000，就会显示“你得了 1000 分或更高。真厉害！”，然后程序会跳转到 `return` 语句。

```cpp
if (score >= 1000)
```

然而，如果表达式为 `false`，我们就知道 `score` 小于 1000，于是程序会计算序列中的下一个表达式：

```cpp
else if (score >= 500)
```

如果 `score` 大于或等于 500，就会显示“你得了 500 分或更高。不错。”，然后程序会跳转到 `return` 语句。然而，如果该表达式为 `false`，我们就知道 `score` 小于 500，于是程序会计算序列中的下一个表达式：

```cpp
else if (score >= 250)
```

如果 `score` 大于或等于 250，就会显示“你得了 250 分或更高。还行。”，然后程序会跳转到 `return` 语句。

然而，如果该表达式为 `false`，我们就知道 `score` 小于 250，此时会执行与最后一个 `else` 子句关联的语句，并显示“你得了不到 250 分。没什么可炫耀的。”

## 提示

虽然 `if else-if else` 语句组中的最后一个 `else` 子句不是必需的，但当序列中的所有表达式都不为 `true` 时，你可以用它来执行代码。

## 使用 switch 语句

你可以使用 `switch` 语句在代码中创建多个分支点。下面是 `switch` 语句的通用形式：

```cpp
switch (choice)
{
case value1:    statement1;
                break;
case value2:    statement2;
                break;
case value3:    statement3;
                break;
                .
                .
                .
case valueN:    statementN;
                break;
default:        statementN + 1;
}
```

该语句按顺序将 `choice` 与可能的值——`value1`、`value2` 和 `value3`——进行比较。如果 `choice` 与某个值相等，程序就执行相应的语句。当程序遇到 `break` 语句时，它会退出 `switch` 结构。如果 `choice` 与任何值都不匹配，则执行与可选的 `default` 关联的语句。

`break` 和 `default` 的使用都是可选的。不过，如果你省略了 `break`，程序会继续执行余下的语句，直到遇到 `break` 或 `default`，或者直到 `switch` 语句结束。通常你希望每个 `case` 都以一个 `break` 语句结束。

## 提示

虽然 `default` 分支不是必需的，但通常最好有一个作为兜底。

这里有一个例子可以巩固这些概念。假设 `choice` 等于 `value2`。程序会先将 `choice` 与 `value1` 进行比较。由于它们不相等，程序会继续执行。接下来，程序将 `choice` 与 `value2` 进行比较。由于它们相等，程序将执行 `statement2`。然后程序会遇到 `break` 语句并退出 `switch` 结构。

### 陷阱

你只能使用 `switch` 语句来测试 `int`（或可被当作 `int` 处理的值，例如 `char` 或枚举值）。`switch` 语句不适用于任何其他类型。

## 介绍菜单选择器程序

菜单选择器程序向用户显示一个菜单，其中列出了三个难度级别，并请他做出选择。如果用户输入的数字与列出的选项之一对应，程序就会显示一条消息确认该选择。如果用户做出了其他选择，程序会告诉他该选择无效。图 2.5 展示了程序的运行情况。

![](img/34f09be0ed6217c465debc4490197d4f_74_0.png)

图 2.5

看起来我选了简单的那条路。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载该程序的代码。程序位于第 2 章文件夹中；文件名是 `menu_chooser.cpp`。

```cpp
// Menu Chooser
// Demonstrates the switch statement

#include <iostream>

using namespace std;

int main()
{
    cout << "Difficulty Levels\n\n";
    cout << "1 - Easy\n";
    cout << "2 - Normal\n";
    cout << "3 - Hard\n\n";

    int choice;
    cout << "Choice: ";
    cin >> choice;

    switch (choice)
    {
    case 1:
        cout << "You picked Easy.\n";
        break;
    case 2:
        cout << "You picked Normal.\n";
        break;
    case 3:
        cout << "You picked Hard.\n";
        break;
    default:
        cout << "You made an illegal choice.\n";
    }

    return 0;
}
```

> **玩了一场激动人心的游戏**

> 你想再玩一次吗？(y/n): y

>

> **玩了一场激动人心的游戏**

> 你想再玩一次吗？(y/n): y

>

> **玩了一场激动人心的游戏**

> 你想再玩一次吗？(y/n): n

>

> 好的，再见..

## 图 2.6

这种重复是通过 `while` 循环实现的。

```cpp
// Play Again

// Demonstrates while loops

#include <iostream>

using namespace std;

int main()

{

    char again = 'y';

    while (again == 'y')

    {

        cout << "\n**Played an exciting game**";

        cout << "\nDo you want to play again? (y/n): ";

        cin >> again;

    }

    cout << "\nOkay, bye.";

    return 0;

}
```

## 使用 while 循环

程序在 `main()` 函数中首先声明名为 `again` 的 `char` 变量，并将其初始化为 `'y'`。然后，程序通过测试 `again` 是否等于 `'y'` 来开始 `while` 循环。由于确实如此，程序会显示消息“**玩了一场激动人心的游戏**”，询问用户是否想再玩一次，并将回复存储在 `again` 中。只要用户输入 `y`，循环就会继续。

你会注意到，我必须在循环之前初始化 `again`，因为循环表达式中使用了这个变量。由于 `while` 循环在循环体（即重复执行的语句组）之前对表达式求值，你必须确保表达式中的任何变量在循环开始前都有值。

## 使用 do 循环

与 `while` 循环一样，`do` 循环允许你根据表达式重复执行一段代码。不同之处在于，`do` 循环在每次循环迭代之后才测试其表达式。这意味着循环体至少会执行一次。下面是 `do` 循环的通用形式：

```cpp
do
    statement;
while (expression);
```

程序执行 `statement`，然后只要 `expression` 测试为 `true`，循环就会重复。一旦 `expression` 测试为 `false`，循环就会结束。

## 介绍再来一次 2.0 程序

再来一次 2.0 程序在用户看来与最初的再来一次程序完全相同。与它的前身一样，再来一次 2.0 通过显示消息“**玩了一场激动人心的游戏**”并询问用户是否想再玩一次，来模拟玩一场激动人心的游戏。只要用户输入 `y`，他就会继续玩。不过，这一次程序使用 `do` 循环来实现重复。图 2.7 展示了该程序。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载该程序的代码。程序位于第 2 章文件夹中；文件名是 `play_again2.cpp`。

```cpp
// Play Again 2.0
// Demonstrates do loops

#include <iostream>
```

我在循环体中获得用户为 `again` 输入的新值。然后在循环表达式中再次进行测试。如果 `again` 等于 `'y'`，则循环重复；否则循环结束。

### 在现实世界中

尽管 `while` 循环和 `do` 循环几乎可以互换使用，但大多数程序员使用 `while` 循环。虽然在某些情况下 `do` 循环可能看起来更自然，但 `while` 循环的优点是它的表达式正好出现在循环顶部；你无需到循环底部去找它。

### 陷阱

如果你曾经遇到过游戏陷入同一个无休止循环的情况，那么你可能经历过无限循环——一种没有终止的循环。下面是一个无限循环的简单示例：

```cpp
int test = 10;
while (test == 10)
{
    cout << test;
}
```

在这种情况下，循环会进入，因为 `test` 为 10。但由于 `test` 从未改变，循环永远不会停止。因此，用户将不得不强制终止正在运行的程序。这个故事的寓意是什么？确保循环的表达式最终能变为假，或者有另一种方式让循环结束，例如下一节“使用 `break` 和 `continue` 语句”中描述的那样。

## 使用 break 和 continue 语句

你可以改变在循环中看到的行为。可以使用 `break` 语句立即退出循环，也可以使用 `continue` 语句直接跳到循环顶部。虽然你应该谨慎使用这些功能，但它们有时确实很有用。

### 介绍挑剔计数器程序

挑剔计数器程序通过 `while` 循环从 1 数到 10。它之所以挑剔，是因为它不喜欢数字 5——它会跳过它。图 2.8 显示了该程序的一次运行。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载该程序的代码。该程序位于第 2 章文件夹中；文件名是 `finicky_counter.cpp`。

**图 2.8.** 使用 `continue` 语句跳过了数字 5，循环以 `break` 语句结束。

![](img/34f09be0ed6217c465debc4490197d4f_81_0.png)

```cpp
// Finicky Counter
// Demonstrates break and continue statements

#include <iostream>

using namespace std;

int main()
{
    int count = 0;
    while (true)
    {
        count += 1;

        // end loop if count is greater than 10
        if (count > 10)
        {
            break;
        }
    }
```

### 使用 continue 语句跳回循环顶部

就在显示 `count` 之前，我添加了以下几行：

```cpp
// skip the number 5
if (count == 5)
{
    continue;
}
```

`continue` 语句的意思是“跳回循环顶部”。在循环顶部，测试 `while` 表达式，如果为真，则再次进入循环。因此，当 `count` 等于 5 时，程序不会执行到 `cout << count << endl;` 语句，而是直接回到循环顶部。结果，5 被跳过，永远不会显示。

### 理解何时使用 break 和 continue
