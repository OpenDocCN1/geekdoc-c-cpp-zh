
## 示例 7-6

以下语句：

```cpp
typedef int integer;
```

为数据类型 `int` 创建一个别名 integer。类似地，以下语句：

```cpp
typedef double real;
```

为数据类型 `double` 创建一个别名 real。以下语句：

```cpp
typedef double decimal;
```

为数据类型 `double` 创建一个别名 decimal。

使用 `typedef` 语句，你可以创建自己的布尔数据类型，如示例 7-7 所示。

## 示例 7-7

回顾第 4 章可知，C++ 中的逻辑（布尔）表达式求值为 1 或 0，它们实际上是 `int` 值。作为逻辑值，1 表示 `true`，0 表示 `false`。考虑以下语句：

```cpp
typedef int Boolean;        //Line 1
const Boolean TRUE = 1;     //Line 2
const Boolean FALSE = 0;    //Line 3
Boolean flag;               //Line 4
```

第 1 行的语句为数据类型 `int` 创建别名 Boolean。第 2 行和第 3 行的语句声明命名常量 TRUE 和 FALSE，并分别将它们初始化为 1 和 0。第 4 行的语句声明 flag 为 Boolean 类型的变量。由于 flag 是 Boolean 类型的变量，以下语句是合法的：

```cpp
flag = TRUE;
```

## 编程示例：石头、布、剪刀游戏

![](img/d0be7fc6d804b63484835c6c8bc67a07_527_0.png)

孩子们经常玩石头、布、剪刀游戏。这个游戏有两名玩家，每人从三个对象中选择一个：石头、布或剪刀。如果玩家 1 选择石头，玩家 2 选择布，则玩家 2 赢得游戏，因为布包住石头。游戏按照以下规则进行：

- 如果两名玩家选择同一个对象，则这局为平局。
- 如果一名玩家选择石头，另一名玩家选择剪刀，则选择石头的玩家赢得本局，因为石头砸坏剪刀。
- 如果一名玩家选择石头，另一名玩家选择布，则选择布的玩家赢得本局，因为布包住石头。
- 如果一名玩家选择剪刀，另一名玩家选择布，则选择剪刀的玩家赢得本局，因为剪刀剪开布。

编写一个交互式程序，让两个人可以玩这个游戏。

### 输入

该程序有两类输入：

- 当被询问是否要玩这个游戏时用户的回答。
- 玩家的选择。

### 输出

玩家的选择以及每局游戏的获胜者。游戏结束后，还应输出总游戏局数以及每位玩家获胜的次数。

### 问题分析与算法设计

两名玩家玩这个游戏。玩家通过键盘输入他们的选择。每位玩家输入 R 或 r 表示石头，P 或 p 表示布，S 或 s 表示剪刀。当第一名玩家输入选择时，第二名玩家看向别处。两个输入都完成后，如果输入有效，程序输出玩家的选择并宣布本局获胜者。游戏持续到其中一名玩家决定退出为止。游戏结束后，程序输出总游戏局数以及每位玩家获胜的次数。上述讨论可转化为以下算法：

- 1. 简要说明游戏及其玩法。
- 2. 询问用户是否想玩这个游戏。
- 3. 获取两名玩家的出拳选择。
- 4. 如果出拳选择有效，输出这些选择以及获胜者。
- 5. 更新总局数和获胜次数。
- 6. 只要用户同意玩这个游戏，就重复步骤 2 到 5。
- 7. 输出局数以及每位玩家获胜的次数。

我们将使用枚举类型来描述这些对象。

```cpp
enum objectType {ROCK, PAPER, SCISSORS};
```

### 变量（函数 main）

显然，在函数 main 中需要以下变量：

```cpp
int gameCount;   //variable to store the number of games played
int winCount1;   //variable to store the number of games won by player 1
int winCount2;   //variable to store the number of games won by player 2
int gameWinner;
char response;   //variable to get the user's response to play the game
char selection1;
char selection2;
objectType play1;   //player1's selection
objectType play2;   //player2's selection
```

本程序划分为以下函数，后续各节将详细描述。

- **displayRules:** 该函数显示关于游戏及其规则的一些简要信息。
- **validSelection:** 该函数检查玩家的选择是否有效。有效的选择只有 R、r、P、p、S 和 s。
- **retrievePlay:** 由于枚举类型不能直接读取，该函数转换输入的选择（R、r、P、p、S 或 s），并返回相应的对象类型。
- **gameResult:** 该函数输出玩家的选择以及游戏的获胜者。
- **convertEnum:** 该函数由函数 gameResult 调用，用于输出枚举类型值。
- **winningObject:** 该函数确定并返回获胜对象。
- **displayResults:** 游戏结束后，该函数显示最终结果。

### 函数 displayRules

该函数没有参数。它仅由输出语句组成，用于解释游戏和游戏规则。基本上，该函数的定义是：

```cpp
void displayRules()
{
    cout << "  Welcome to the game of Rock, Paper, "
         << "and Scissors." << endl;
    cout << "  This is a game for two players. For each "
         << "game, each" << endl;
    cout << " player selects one of the objects Rock, "
         << "Paper, or Scissors." << endl;
    cout << "The rules for winning the game are:" << endl;
    cout << "1. If both players select the same object, it "
         << "is a tie." << endl;
    cout << "2. Rock breaks Scissors: So player who selects "
         << "Rock wins." << endl;
    cout << "3. Paper covers Rock: So player who selects "
         << "Paper wins." << endl;
    cout << "4. Scissors cuts Paper: So player who selects "
         << "Scissors wins." << endl << endl;
    cout << "Enter R or r to select Rock, P or p to select "
         << "Paper, and S or s to select Scissors." << endl;
}
```

### 函数 validSelection

该函数检查玩家的选择是否有效。

```text
if selection is 'R' or 'r' or 'S' or 's' or 'P' or 'p', then
    it is a valid selection;
otherwise the selection is invalid.
```

我们使用 switch 语句检查选择是否有效。该函数的定义是：

```cpp
bool validSelection(char selection)
{
    switch (selection)
    {
    case 'R':
    case 'r':
    case 'P':
    case 'p':
    case 'S':
    case 's':
        return true;
    default:
        return false;
    }
}
```

### 函数 retrievePlay

由于枚举类型不能直接读取，该函数转换输入的选择（R、r、P、p、S 或 s），并返回相应的对象类型。因此，该函数有一个 char 类型的参数。它是一个有返回值的函数，返回 objectType 类型的值。用伪代码表示，该函数的算法是：

```text
if selection is 'R' or 'r'
    return ROCK;

if selection is 'P' or 'p'
    return PAPER;

if selection is 'S' or 's'
    return SCISSORS;
```

函数 `retrievePlay` 的定义是：

```cpp
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

该函数判断一局游戏是平局还是哪位玩家获胜。它输出玩家的选择以及游戏的获胜者。显然，该函数有三个参数：玩家 1 的选择、玩家 2 的选择，以及一个用于返回获胜者的参数。用伪代码表示，该函数为：

- a. 如果 player1 和 player2 的选择相同，那么
  这局为平局。
- b. 否则
  {
    - 1. 确定获胜对象。（调用函数 winningObject）
    - 2. 输出每位玩家的选择。
    - 3. 确定获胜玩家。
    - 4. 通过引用参数将获胜玩家返回给
      函数 main，以便函数 main 能够更新
      获胜玩家的获胜次数。
  }

该函数的定义是：

```cpp
void gameResult(objectType play1, objectType play2,
                int& winner)
{
    objectType winnerObject;

    if (play1 == play2)
    {
        winner = 0;
        cout << "Both players selected ";
```
