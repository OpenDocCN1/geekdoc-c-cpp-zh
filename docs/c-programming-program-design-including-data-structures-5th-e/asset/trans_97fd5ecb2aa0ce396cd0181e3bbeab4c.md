
```
case 's':
    return true;
default:
    return false;
}
}
```

### 函数 retrievePlay

由于枚举类型不能被直接读取，该函数会转换输入的选择（R、r、P、p、S 或 s），并返回相应的对象类型值。因此，该函数有一个参数，类型为 `char`。它是一个有返回值的函数，返回 `objectType` 类型的值。用伪代码表示，该函数的算法为：

```
if selection is 'R' or 'r'
    return ROCK;

if selection is 'P' or 'p'
    return PAPER;

if selection is 'S' or 's'
    return SCISSORS;
```

函数 retrievePlay 的定义如下：

```
objectType retrievePlay(char selection)
{
    objectType object;

    switch (selection)
    {
    case 'R':
    case 'r':
        object = ROCK;
        break;
    case 'P':
    case 'p':
        object = PAPER;
        break;
    case 'S':
    case 's':
        object = SCISSORS;
    }

    return object;
}
```

### 函数 gameResult

该函数判断一局游戏是平局还是哪位玩家获胜。它输出玩家的选择以及该局游戏的获胜者。显然，该函数有三个参数：玩家 1 的选择、玩家 2 的选择，以及一个用于返回获胜者的参数。用伪代码表示，该函数为：

- a. 如果 player1 和 player2 的选择相同，则这局是平局。
- b. 否则
  {
  - 1. 确定获胜对象。（调用函数 winningObject）
  - 2. 输出每位玩家的选择。
  - 3. 确定获胜玩家。
  - 4. 通过引用参数将获胜玩家返回给函数 main，以便函数 main 可以更新获胜玩家的胜场数。
  }

该函数的定义如下：

```
void gameResult(objectType play1, objectType play2,
                int& winner)
{
    objectType winnerObject;

    if (play1 == play2)
    {
        winner = 0;
        cout << "Both players selected ";
        convertEnum(play1);
        cout << ". This game is a tie." << endl;
    }
    else
    {
        winnerObject = winningObject(play1, play2);

        //Output each player's choice
        cout << "Player 1 selected ";
        convertEnum(play1);
        cout << " and player 2 selected ";
        convertEnum(play2);
        cout << ".";

        //Decide the winner
        if (play1 == winnerObject)
            winner = 1;
        else if (play2 == winnerObject)
            winner = 2;

        //Output the winner
        cout << "Player " << winner << " wins this game."
             << endl;
    }
}
```

### 函数 convertEnum

由于枚举类型不能直接输出，我们来编写函数 convertEnum 以输出枚举类型 objectType 的对象。该函数有一个参数，类型为 objectType。它输出与 objectType 对应的字符串。用伪代码表示，该函数为：

在变量 `winCount2` 中。该函数有三个参数分别对应这三个变量。本质上，该函数的定义是：

```
void displayResults(int gCount, int wCount1, int wCount2)
{
    cout << "The total number of plays: " << gCount
         << endl;
    cout << "The number of plays won by player 1: "
         << wCount1 << endl;
    cout << "The number of plays won by player 2: "
         << wCount2 << endl;
}
```

现在我们可以编写函数 main 的算法了。

### 主算法

- 1. 声明变量。
- 2. 初始化变量。
- 3. 显示规则。
- 4. 提示用户开始游戏。
- 5. 获取用户是否进行游戏的响应。
- 6. `while`（响应为 yes）
  {
  - a. 提示玩家 1 做出选择。
  - b. 获取玩家 1 的出拳。
  - c. 提示玩家 2 做出选择。
  - d. 获取玩家 2 的出拳。
  - e. 如果两个选择都合法：
    {
    - i. 增加总游戏局数。
    - ii. 判定该局游戏的获胜者。
    - iii. 将获胜者的胜场数增加 1。
    }
  - f. 提示用户确定是否想再玩一局。
  - g. 获取玩家的响应。
  }
- 7. 输出游戏结果。

## 程序清单

```cpp
//***********************************************************
// Author: D. S. Malik
//
// Program: Rock, Paper, and Scissors
// This program plays the game of rock, paper, and scissors.
//***********************************************************

#include <iostream>

using namespace std;

enum objectType {ROCK, PAPER, SCISSORS};

    //Function prototypes
void displayRules();
objectType retrievePlay(char selection);
bool validSelection(char selection);
void convertEnum(objectType object);
objectType winningObject(objectType play1, objectType play2);
void gameResult(objectType play1, objectType play2, int& winner);
void displayResults(int gCount, int wCount1, int wCount2);

int main()
{
    //Step 1
    int gameCount; //variable to store the number of
                   //games played
    int winCount1; //variable to store the number of games
                   //won by player 1
    int winCount2; //variable to store the number of games
                   //won by player 2

    int gameWinner;
    char response; //variable to get the user's response to
                   //play the game

    char selection1;
    char selection2;
    objectType play1;   //player1's selection
    objectType play2;   //player2's selection

    //Initialize variables; Step 2
    gameCount = 0;
    winCount1 = 0;
    winCount2 = 0;

    displayRules();                                     //Step 3

    cout << "Enter Y/y to play the game: ";             //Step 4
    cin >> response;                                    //Step 5
    cout << endl;

while (response == 'Y' || response == 'y')  //Step 6
{
    cout << "Player 1 enter your choice: ";       //Step 6a
    cin >> selection1;                             //Step 6b
    cout << endl;

    cout << "Player 2 enter your choice: ";       //Step 6c
    cin >> selection2;                             //Step 6d
    cout << endl;

        //Step 6e
    if (validSelection(selection1)
            && validSelection(selection2))
    {
        play1 = retrievePlay(selection1);
        play2 = retrievePlay(selection2);
        gameCount++;                               //Step 6e.i
        gameResult(play1, play2, gameWinner);      //Step 6e.ii

        if (gameWinner == 1)                       //Step 6e.iii
            winCount1++;
        else if (gameWinner == 2)
            winCount2++;
    }//end if

    cout << "Enter Y/y to play the game: ";       //Step 6f
    cin >> response;                               //Step 6g
    cout << endl;
}//end while

displayResults(gameCount, winCount1,
               winCount2);                        //Step 7

return 0;
}//end main

//Place the definitions of the functions displayRules,
//validSelection, retrievePlay, convertEnum, winningObject,
//gameResult, and displayResults as described previously here.
```

## 命名空间

1998 年 7 月，ANSI/ISO 标准 C++ 获得正式批准。大多数较新的编译器也与 ANSI/ISO 标准 C++ 兼容。（要完全确定，请查阅编译器的文档。）Standard C++ 和 ANSI/ISO 标准 C++ 这两个标准实际上几乎相同。ANSI/ISO 标准 C++ 语言具有一些 Standard C++ 中不可用的特性，本章剩余部分将讨论这些特性。

在后续章节中，除非另有说明，C++ 语法适用于这两个标准。首先，我们讨论 ANSI/ISO 标准 C++ 的命名空间机制，该机制在第 2 章中介绍过。

当程序包含诸如 `iostream` 这样的头文件时，该头文件中的全局标识符也会成为程序中的全局标识符。因此，如果程序中的某个全局标识符与头文件中的某个全局标识符同名，编译器就会生成语法错误（例如“标识符重定义”）。如果程序使用第三方库，也可能出现同样的问题。为了解决这个问题，第三方供应商会让其全局标识符以特殊符号开头。在第 2 章中你了解到，由于编译器供应商让其全局标识符名称以下划线（_）开头，为避免链接错误，你的程序中的标识符名称不应以下划线（_）开头。

ANSI/ISO 标准 C++ 试图通过 `namespace` 机制解决全局标识符名称重叠的问题。

`namespace` 语句的一般语法为：

```
    namespace namespace_name
    {
        members
    }
```

其中 members 通常是命名常量、变量声明、函数或另一个 `namespace`。注意 namespace_name 是 C++ 标识符。

在 C++ 中，`namespace` 是保留字。

### 示例 8-8

语句：

```
    namespace globalType
    {
        const int N = 10;
        const double RATE = 7.50;
        int count = 0;
        void printResult();
    }
```

将 globalType 定义为具有四个成员的 `namespace`：命名常量 N 和 RATE、变量 count 以及函数 printResult。

`namespace` 成员的作用域局限于该 `namespace`。通常可以通过以下两种方式之一在 `namespace` 外部访问 `namespace` 成员，如下所述。
