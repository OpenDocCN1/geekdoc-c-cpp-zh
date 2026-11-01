

![](img/c7e8651578bccd573227f684823b8754_77_0.png)

**图 2.6**

重复是通过 while 循环实现的。

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

## 使用 while 循环进行循环

程序在 `main()` 函数中做的第一件事是声明名为 `again` 的 char 变量并将其初始化为 `'y'`。然后程序通过测试 `again` 是否等于 `'y'` 来开始 while 循环。因为是，程序显示消息“**玩了一场激动人心的游戏**”，询问用户是否想再次游玩，并将回复存储在 `again` 中。只要用户输入 y，循环就会继续。

你会注意到我必须在循环之前初始化 `again`，因为该变量在循环表达式中使用。因为 while 循环在循环体（重复的语句组）之前评估其表达式，所以你必须确保表达式中的任何变量在循环开始前都有值。

## 使用 do 循环

与 while 循环类似，do 循环允许你根据表达式重复一段代码。不同之处在于 do 循环在每次循环迭代后测试其表达式。这意味着循环体至少执行一次。这是一个 do 循环的通用形式：

```cpp
do
    statement;
while (expression);
```

程序执行 `statement`，然后只要 `expression` 测试为真，循环就重复。一旦 `expression` 测试为假，循环结束。

### 介绍 Play Again 2.0 程序

Play Again 2.0 程序对用户来说看起来与原始的 Play Again 程序完全相同。Play Again 2.0 与其前身一样，通过显示消息“**玩了一场激动人心的游戏**”并询问用户是否想再次游玩来模拟激动人心的游戏。只要用户输入 y，他就会继续游玩。不过这次，程序使用 do 循环来实现重复。图 2.7 展示了该程序。

你可以从 Course Technology 网站 (www.courseptr.com/downloads) 下载此程序的代码。该程序位于第 2 章文件夹中；文件名是 play_again2.cpp。

```cpp
// Play Again 2.0
// Demonstrates do loops

#include <iostream>
```

在循环体中从用户获取 again 的新值。然后我在循环表达式中测试 again。如果 again 等于 'y'，循环重复；否则循环结束。

### IRW

尽管你可以相当互换地使用 while 和 do 循环，但大多数程序员使用 while 循环。尽管在某些情况下 do 循环可能看起来更自然，但 while 循环的优点是其表达式出现在循环顶部；你不必在循环底部寻找它。

### 陷阱

如果你曾经遇到游戏卡在同一个无尽循环中，你可能经历过无限循环——一个没有尽头的循环。这是一个无限循环的简单示例：

```cpp
int test = 10;
while (test == 10)
{
    cout << test;
}
```

在这种情况下，因为 test 是 10，所以进入了循环。但由于 test 从未改变，循环永远不会停止。因此，用户必须终止正在运行的程序才能结束它。这个故事的寓意是什么？确保循环的表达式最终可以变为假，或者存在另一种让循环结束的方式，例如在下一节“使用 break 和 continue 语句”中描述的那样。

## 使用 break 和 continue 语句

可以改变你在循环中看到的行为。你可以使用 `break` 语句立即退出循环，并使用 `continue` 语句直接跳转到循环顶部。虽然你应该谨慎使用这些功能，但有时它们确实很有用。

### 介绍 Finicky Counter 程序

Finicky Counter 程序通过 while 循环从 1 数到 10。它很挑剔，因为它不喜欢数字 5——它会跳过它。图 2.8 显示了程序的运行。

你可以从 Course Technology 网站 (www.courseptr.com/downloads) 下载此程序的代码。该程序位于第 2 章文件夹中；文件名是 finicky_counter.cpp。

```cpp
//skip the number 5
if (count == 5)
{
    continue;
}

cout << count << endl;
}

return 0;
}
```

### 创建 while (true) 循环

我用以下行设置循环：

```cpp
while (true)
```

从技术上讲，这创建了一个无限循环。在警告避免无限循环后不久出现这一点可能看起来很奇怪，但这个特定的循环实际上不是无限的，因为我在循环体中放置了一个退出条件。

> **提示**
>
> 尽管 while (true) 循环有时可能比传统循环更清晰，但你也应尽量减少对这些循环的使用。

### 使用 break 语句退出循环

这是我放入循环中的退出条件：

```cpp
//end loop if count is greater than 10
if (count > 10)
{
    break;
}
```

因为每次循环体开始时 count 都会增加 1，所以它最终会达到 11。当它这样做时，break 语句（意思是“跳出循环”）被执行，循环结束。

### 使用 continue 语句跳回循环顶部

在显示 count 之前，我包含了以下行：

```cpp
//skip the number 5
if (count == 5)
{
    continue;
}
```

continue 语句的意思是“跳回循环顶部”。在循环顶部，while 表达式会被测试，如果为真则再次进入循环。所以当 count 等于 5 时，程序不会执行到 `cout << count << endl;` 语句。相反，它会直接回到循环顶部。因此，5 被跳过并且永远不会显示。

### 了解何时使用 break 和 continue

你可以在创建的任何循环中使用 `break` 和 `continue`；它们不仅仅用于 while (true) 循环。但你应该谨慎使用它们。`break` 和 `continue` 都可能使程序员更难看到循环的流程。

## 使用逻辑运算符

到目前为止，你看到的表达式相当简单，用于评估其真假。然而，你可以使用逻辑运算符组合更简单的表达式以创建更复杂的表达式。表 2.2 列出了逻辑运算符。

**表 2.2 逻辑运算符**

| Operator | Description | Sample Expression |
| --- | --- | --- |
| ! | 逻辑非 | !expression |
| && | 逻辑与 | expression1 && expression2 |
| \|\| | 逻辑或 | expression1 \|\| expression2 |

### 介绍 Designers Network 程序

Designers Network 程序模拟了一个计算机网络，其中只有一群精选的游戏设计师是成员。像现实世界的计算机系统一样，

![](img/c7e8651578bccd573227f684823b8754_85_0.png)

**图 2.11**

看起来今天其中一位精英登录了。

你可以从 Course Technology 网站 (www.courseptr.com/downloads) 下载此程序的代码。该程序位于第 2 章文件夹中；文件名是 designers_network.cpp。

```cpp
// Designers Network
// Demonstrates logical operators

#include <iostream>
#include <string>
using namespace std;

int main()
{
    string username;
    string password;
    bool success;

    cout << "\tGame Designer's Network\n";

    do
    {
        cout << "\nUsername: ";
        cin >> username;

        cout << "Password: ";
        cin >> password;

        if (username == "S.Meier" && password == "civilization")
        {
            cout << "\nHey, Sid.";
            success = true;
        }
        else if (username == "S.Miyamoto" && password == "mariobros")
        {
            cout << "\nWhat's up, Shigeru?";
            success = true;
        }
        else if (username == "W.Wright" && password == "thesims")
        {
            cout << "\nHow goes it, Will?";
            success = true;
        }
        else if (username == "guest" || password == "guest")
        {
            cout << "\nWelcome, guest.";
            success = true;
        }
        else
        {
            cout << "\nYour login failed.";
            success = false;
        }
    } while (!success);

    return 0;
}
```
