
类似地，语句：

```cpp
enum coins {PENNY, NICKEL, DIME, HALFDOLLAR, DOLLAR} change, usCoins;
```

定义了枚举类型 coins，并声明了两个类型为 coins 的变量 change 和 usCoins。

## 匿名数据类型

在变量声明中直接指定值而不给出类型名的数据类型称为匿名类型。以下语句创建了一个匿名类型：

```cpp
enum {BASKETBALL, FOOTBALL, BASEBALL, HOCKEY} mySport;
```

该语句指定了值并声明了变量 mySport，但没有为数据类型命名。

然而，创建匿名类型有其缺点。首先，因为该类型没有名称，所以不能将匿名类型作为参数传递给函数，函数也不能返回匿名类型的值。其次，在一个匿名类型中使用的值可以在另一个匿名类型中使用，但这些类型的变量会被区别对待。考虑以下语句：

```cpp
enum {ENGLISH, FRENCH, SPANISH, GERMAN, RUSSIAN} languages;
enum {ENGLISH, FRENCH, SPANISH, GERMAN, RUSSIAN} foreignLanguages;
```

即使变量 languages 和 foreignLanguages 具有相同的值，编译器仍将它们视为不同类型的变量。因此，以下语句是非法的：

```cpp
languages = foreignLanguages; //illegal
```

即使可以使用这些功能，也要谨慎使用。为避免混淆，应先定义枚举类型，再声明变量。

现在描述 C++ 中的 typedef 语句。

## typedef 语句

在 C++ 中，可以使用 typedef 语句为先前定义的数据类型创建同义词或别名。typedef 语句的一般语法为：

```cpp
typedef existingTypeName newTypeName;
```

在 C++ 中，typedef 是保留字。注意，typedef 语句不会创建任何新数据类型；它只为已有数据类型创建别名。

### 示例 7-6

语句：

```cpp
typedef int integer;
```

为数据类型 int 创建别名 integer。类似地，语句：

```cpp
typedef double real;
```

为数据类型 double 创建别名 real。语句：

```cpp
typedef double decimal;
```

为数据类型 double 创建别名 decimal。

使用 typedef 语句，可以创建自己的布尔数据类型，如示例 7-7 所示。

### 示例 7-7

回顾第 4 章，C++ 中的逻辑（布尔）表达式求值为 1 或 0，实际上它们是 int 值。作为逻辑值，1 表示真，0 表示假。考虑以下语句：

```cpp
typedef int Boolean;        //Line 1
const Boolean TRUE = 1;     //Line 2
const Boolean FALSE = 0;    //Line 3
Boolean flag;               //Line 4
```

第 1 行语句为数据类型 int 创建别名 Boolean。第 2 行和第 3 行语句声明命名常量 TRUE 和 FALSE，并分别将它们初始化为 1 和 0。第 4 行语句声明 flag 为 Boolean 类型的变量。因为 flag 是 Boolean 类型的变量，所以以下语句合法：

```cpp
flag = TRUE;
```

## 编程示例：石头、布、剪刀游戏

儿童经常玩石头、布、剪刀游戏。这个游戏有两名玩家，每人从石头、布或剪刀三个对象中选择一个。如果玩家 1 选择石头，玩家 2 选择布，则玩家 2 获胜，因为布包住石头。游戏按照以下规则进行：

- 如果两名玩家选择相同的对象，则本轮为平局。
- 如果一名玩家选择石头，另一名选择剪刀，则选择石头的玩家赢得本轮，因为石头砸坏剪刀。
- 如果一名玩家选择石头，另一名选择布，则选择布的玩家赢得本轮，因为布包住石头。
- 如果一名玩家选择剪刀，另一名选择布，则选择剪刀的玩家赢得本轮，因为剪刀剪开布。

编写一个交互式程序，让两个人玩这个游戏。

### 输入

该程序有两类输入：

- 用户在被询问是否玩游戏时的回答。
- 玩家的选择。

### 输出

玩家的选择以及每轮获胜者。游戏结束后，还应输出总轮数以及每位玩家获胜的次数。

两名玩家玩这个游戏。玩家通过键盘输入选择。每位玩家输入 R 或 r 表示石头，P 或 p 表示布，S 或 s 表示剪刀。当第一位玩家输入选择时，第二位玩家看向别处。两个输入都完成后，如果输入有效，程序输出玩家的选择并宣布本轮获胜者。游戏继续，直到其中一位玩家决定退出游戏。游戏结束后，程序输出总轮数以及每位玩家获胜的次数。上述讨论可转化为以下算法：

- 1. 提供关于游戏及其玩法的简要说明。
- 2. 询问用户是否想玩这个游戏。
- 3. 获取两位玩家的出拳。
- 4. 如果出拳有效，输出出拳和获胜者。
- 5. 更新总游戏计数和获胜计数。
- 6. 当用户同意玩游戏时，重复步骤 2 到 5。
- 7. 输出游戏轮数以及每位玩家获胜的次数。

我们将使用枚举类型来描述这些对象。

```cpp
enum objectType {ROCK, PAPER, SCISSORS};
```

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_506_0.png)

很明显，在函数 `main` 中需要以下变量：

```cpp
int gameCount;    //variable to store the number of
                  //games played
int winCount1;    //variable to store the number of games
                  //won by player 1
int winCount2;    //variable to store the number of games
                  //won by player 2
int gamewinner;
char response;    //variable to get the user's response to
                  //play the game
char selection1;
char selection2;
objectType play1; //player1's selection
objectType play2; //player2's selection
```

本程序分为以下函数，后续各节将详细描述这些函数。

- **displayRules：** 该函数显示有关游戏及其规则的简要信息。
- **validSelection：** 该函数检查玩家的选择是否有效。唯一有效的选择是 R、r、P、p、S 和 s。
- **retrievePlay：** 因为枚举类型不能直接读取，该函数将输入的选项（R、r、P、p、S 或 s）转换为相应的对象类型并返回。
- **gameResult：** 该函数输出玩家的选择以及游戏获胜者。
- **convertEnum：** 该函数由函数 gameResult 调用，用于输出枚举类型值。
- **winningObject：** 该函数确定并返回获胜对象。
- **displayResults：** 游戏结束后，该函数显示最终结果。

### 函数 displayRules

该函数没有参数。它只包含输出语句，用于解释游戏和游戏规则。本质上，该函数的定义是：

```cpp
void displayRules()
{
    cout << " Welcome to the game of Rock, Paper, ";
    cout << " and Scissors." << endl;
    cout << " This is a game for two players. For each "
         << " game, each" << endl;
    cout << " player selects one of the objects Rock, "
         << "Paper, or Scissors." << endl;
    cout << "The rules for winning the game are: " << endl;
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

让我们使用 `switch` 语句检查选择是否有效。该函数的定义是：

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

因为枚举类型不能直接读取，该函数将输入的选项（R、r、P、p、S 或 s）转换为相应的对象类型并返回。因此，该函数有一个 char 类型的参数。它是一个有返回值的函数，返回 objectType 类型的值。用伪代码表示，该函数的算法是：

```text
if selection is 'R' or 'r'
    return ROCK;

if selection is 'P' or 'p'
    return PAPER;

if selection is 'S' or 's'
    return SCISSORS;
```
