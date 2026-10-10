
```cpp
void gameResult(typeType player1, typeType player2, typeType &winner) {
    if (player1 == player2) {
        cout << "平局!" << endl;
    } else if ((player1 == ROCK && player2 == SCISSORS) ||
               (player1 == PAPER && player2 == ROCK) ||
               (player1 == SCISSORS && player2 == PAPER)) {
        cout << "玩家1胜了!" << endl;
        winner = player1;
    } else {
        cout << "玩家2胜了!" << endl;
        winner = player2;
    }
}
```

448 | 第8章：用户自定义简单数据类型、命名空间和字符串类型

b. `else`

+ 1. 确定获胜对象。`（调用函数 winningObject）`

2. 输出每个玩家的选择。

3. 确定获胜者。

4. 通过引用参数将胜者返回给 `main` 函数，以便 `main` 函数能够更新胜者的获胜次数。

}

该函数的定义如下：

```cpp
void gameResult(objectType play1, objectType play2,
    int& winner)
{
    objectType winnerObject;

    if (play1 == play2) {
        winner = 0;
        cout << "Both players selected ";
        convertEnum(play1);
        cout << ". This game is a tie." << endl;
    }
    else {
        winnerObject = winningObject(play1, play2);

        // 输出每个玩家的选择
        cout << "Player 1 selected ";
        convertEnum(play1);
        cout << " and player 2 selected ";
        convertEnum(play2);
        cout << " ";

        // 决定胜者
        if (play1 == winnerObject)
            winner = 1;
        else if (play2 == winnerObject)
            winner = 2;

        // 输出胜者
        cout << "Player " << winner << " wins this game.";
        cout << endl;
    }
}
```

函数由于枚举类型无法直接输出，让我们编写函数 `convertEnum` 来输出枚举类型 `objectType` 对象。该函数有一个参数，类型为 `objectType`。它输出与 `objectType` 对应的字符串。在伪代码中，该函数如下：

# 编程示例：剪刀石头布游戏 | 449

```
if object is ROCK
output "Rock"
```

```
if object is PAPER
output "Paper"
```

```
if object is SCISSORS
output "SCISSORS"
```

函数 `convertEnum` 的定义如下：

```cpp
void convertEnum(objectType object)
{
  switch (object)
  {
    case ROCK:
      cout << "Rock"
      break;
    case PAPER:
      cout << "Paper"
      break;
    case SCISSORS:
      cout << "SCISSORS"
  }
}
```

函数为了决定比赛的胜负，你需要查看玩家的选择，然后根据游戏规则。例如，如果一个玩家选择石头而另一个玩家选择布，那么选择布的玩家获胜。在其他情况下，获胜对象是布。函数 `winningObject` 接收两个对象，决定并返回获胜对象。显然，该函数有两个 `objectType` 类型的参数。该函数的定义如下：

```cpp
objectType winningObject(objectType play1, objectType play2)
{
  if ((play1 == ROCK && play2 == SCISSORS)
  || (play2 == ROCK && play1 == SCISSORS))
    return ROCK;
  else if ((play1 == ROCK && play2 == PAPER)
  || (play2 == ROCK && play1 == PAPER))
    return PAPER;
  else
    return SCISSORS;
}
```

函数在游戏结束后，该函数输出最终结果——即总局数和每个玩家的获胜次数。总局数存储在变量 `gameCount` 中，玩家 1 的获胜次数存储在变量 `winCount1` 中，玩家 2 的获胜次数存储在变量 `winCount2` 中。该函数有三个参数对应这三个变量。本质上，该函数的定义如下：

```cpp
void displayResults(int gCount, int wCount1, int wCount2) {
    cout << "The total number of plays: " << gCount << endl;
    cout << "The number of plays by player 1: " << wCount1 << endl;
    cout << "The number of plays by player 2: " << wCount2 << endl;
}
```

我们现在准备好为 `main` 函数编写算法了：

# MAIN

算法

+ 1. 声明变量。

2. 初始化变量。

3. 显示规则。

4. 提示用户玩游戏。

5. 获取用户玩游戏的响应。

6. `while (response is yes)`

{

a. 提示玩家 1 做出选择。

b. 获取玩家 1 的选择。

c. 提示玩家 2 做出选择。

d. 获取玩家 2 的选择。

e. 如果两个选择都是合法的：

i. 总局数加 1。

ii. 声明比赛胜者。

iii. 胜者的获胜次数加 1。

}

f. 提示用户确定是否想再次玩。

g. 获取玩家的响应。

}

7. 输出游戏结果。

# 编程示例：剪刀石头布游戏 | 491

## 列表

```
************************************************
// Author: D. Malik
// Program: Rock, Paper, and Scissors
// This program plays the game of rock, paper, and scissors.
************************************************
```
```cpp
#include <iostream>

using namespace std;

enum objectType {ROCK, PAPER, SCISSORS};

// 函数原型

void rules();

objectType validSelection(objectType object);

void convertEnum(objectType object);

objectType winningObject(objectType play1, objectType play2);

void gameResult(objectType play1, objectType play2, int& winner);

void displayResults(int gCount, int wCount1, int wCount2);

int main() {

    // 声明变量

    int gameCount;

    int winCount1;

    int winCount2;

    objectType play1, play2;

    char response;

    int winner;

    // 初始化变量

    gameCount = 0;

    winCount1 = 0;

    winCount2 = 0;

    // 显示规则

    rules();

    // 提示用户玩游戏

    cout << "Do you want to play the game (y/n)? ";

    cin >> response;

    // 获取用户玩游戏的响应

    while (response == 'y' || response == 'Y') {

        // 提示玩家 1 做出选择

        cout << "Player 1, enter your selection: ";

        // 获取玩家 1 的选择

        cin >> play1;

        // 提示玩家 2 做出选择

        cout << "Player 2, enter your selection: ";

        // 获取玩家 2 的选择

        cin >> play2;

        // 如果两个选择都是合法的

        if (validSelection(play1) && validSelection(play2)) {

            // 总局数加 1

            gameCount++;

            // 声明比赛胜者

            winner = winningObject(play1, play2);

            // 胜者的获胜次数加 1

            if (winner == 1) {

                winCount1++;

            } else if (winner == 2) {

                winCount2++;

            }

            // 输出胜者

            gameResult(play1, play2, winner);

        }

        // 提示用户确定是否想再次玩

        cout << "Do you want to play again? (y/n): ";

        // 获取玩家的响应

        cin >> response;

    }

    // 输出游戏结果

    displayResults(gameCount, winCount1, winCount2);

    return 0;

}
```

4492 | 第8章：用户自定义简单数据类型、命名空间和字符串类型

# 命名空间

1998年，ANSI/ISO 标准 C++通过批准。大多数编译器也兼容 ANSI/ISO C++。`（要绝对确定，请检查您的编译器文档。）`这两个标准，Standard C++ 和 ANSI/ISO C++ 几乎相同。ANSI/ISO C++ 语言具有 Standard C++ 中不具备的功能，本章剩余部分将介绍这些功能。

# 示例 8-8

语句：

```
namespace globalType {

    const int N = 10;

    const double RATE = 7.50;

    int count = 0;

    void printResult();

}
```

定义 `globalType` 为具有四个成员的命名空间。

命名空间成员的作用域局限于命名空间。您通常可以通过以下两种方式在命名空间外部访问命名空间成员，下文所示。

454 | 第 8 章：自定义简单数据类型、命名空间和 string 类型

访问命名空间的通用语法为：

```
namespace_name::identifier
```

回想 C++ 中，`::` 被称为作用域解析运算符。

要访问命名空间 `globalType` 的成员 `RATE`，需要语句：

```
globalType::RATE
```

要访问成员 `printResult` `（这是一个函数）`，需要语句：

```
globalType::printResult();
```

因此，要访问命名空间的成员，你使用 `namespace_name`，后面跟着作用域运算符，然后是成员名。

为了简化命名空间的访问，ANSI/ISO C++ 提供了标准。使用 `using` 语句语法如下：

- A. 简化所有命名空间成员的访问：

```
using namespace namespace_name;
```

- B. 简化特定命名空间成员的访问：

```
using namespace_name::identifier;
```

例如，`using` 语句：

```
using namespace globalType;
```

简化了命名空间 `globalType` 中所有成员的访问。语句：

```
using globalType::RATE;
```

简化了命名空间 `globalType` 中成员 `RATE` 的访问。

在 C++ 中，`using` 是一个关键字。

你通常将 `using` 语句放在命名空间声明之后。对于命名空间 `globalType`，你通常这样写代码：

```
namespace globalType

{

  const int N = 10;

  const double RATE = 7.50;

  int count = 0;

  void printResult();

}

using namespace globalType;
```

在使用 `using` 语句后，访问命名空间成员时，不需要在成员前加上 `namespace_name` 和作用域运算符。然而，如果程序中的命名空间成员与全局标识符同名，为了在程序中访问该命名空间成员，`namespace_name` 和作用域运算符必须置于该成员之前。同样，如果命名空间成员与块中的某个标识符同名，要在块中访问该命名空间成员，`namespace_name` 和作用域运算符必须置于该成员之前。

示例 8-9 到 8-12 有助于明确命名空间机制的使用。

# 示例 8-9

考虑以下 C++ 代码：

```cpp
#include <iostream>

using namespace std;

int main() {

}
```

在此示例中，你可以直接引用头文件 `iostream` 中的全局标识符，如 `cin`、`cout` 和 `endl`，而无需在标识符名前加上 `std::` 前缀。明显的限制是，引用该全局标识符 `（来自头文件 iostream）` 的块 `（或函数）` 不能包含任何与该全局标识符同名的标识符。

# 示例 8-10

考虑以下 C++ 代码：

```cpp
#include <cmath>

int main() {

    double x = 15.3;

    double y;

}
```
```cpp
y = std::pow(x, 2);
...
}
```
此示例访问了头文件 `cmath` 中的函数 `pow`。

# 示例 8-11

考虑以下 C++ 代码：

```cpp
#include <iostream>
.
int main() {
  using namespace std;
.
```
```
在此示例中，`main` 函数可以引用头文件 `iostream` 中的全局标识符，而无需在标识符名前加上 `std::` 前缀。`using` 语句出现在 `main` 函数内部。因此，其他函数 `（如果有）` 应该在头文件 `iostream` 的全局标识符名前使用 `std::` 前缀，除非该函数内部有类似的 `using` 语句。

# 示例 8-12

考虑以下 C++ 代码：

```cpp
#include <iostream>

using namespace std; // 第 1 行

int t; // 第 2 行

double u; // 第 3 行

namespace expN {

  int x; // 第 4 行

  char t; // 第 5 行
```
# 命名空间 | 457
```cpp
double u; // 第 6 行

void printResult(); // 第 7 行

}
```
using namespace expN;

int main() {

    int one; // 第 8 行

    double t; // 第 9 行

    double three; // 第 10 行

}
```
```cpp
void expN::printResult() // 函数 printResult 的定义
{}
```
