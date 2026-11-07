
如前所述，你还可以在函数 `readCourses` 中使用 `string` 类型，将值输入到 `courses` 类型的变量中。我们将细节留作练习。

下面的函数输出一个枚举类型值：

```cpp
void printEnum(courses registered)
{
    switch (registered)
    {
    case ALGEBRA:
        cout << "Algebra";
        break;
    case ANALYSIS:
        cout << "Analysis";
        break;
    case BASIC:
        cout << "Basic";
        break;
    case CHEMISTRY:
        cout << "Chemistry";
        break;
    case CPP:
        cout << "CPP";
        break;
    case HISTORY:
        cout << "History";
        break;
    case PYTHON:
        cout << "Python";
        break;
    case PHILOSOPHY:
        cout << "Philosophy";
        break;
    }//end switch
}//end printEnum
```

## 在定义枚举类型时声明变量

在前面的章节中，你先定义了一个枚举类型，然后声明了该类型的变量。C++ 允许将这两个步骤合并为一个步骤。也就是说，你可以在定义枚举类型时声明该枚举类型的变量。例如，语句：

```cpp
enum grades {A, B, C, D, F} courseGrade;
```

定义了枚举类型 `grades`，并声明了一个类型为 `grades` 的变量 `courseGrade`。

类似地，语句：

```cpp
enum coins {PENNY, NICKEL, DIME, HALFDOLLAR, DOLLAR} change, usCoins;
```

定义了枚举类型 `coins`，并声明了两个类型为 `coins` 的变量 `change` 和 `usCoins`。

## 匿名数据类型

如果在变量声明中直接指定值而不给出类型名，这样的数据类型称为**匿名类型**。下面的语句创建了一个匿名类型：

```cpp
enum {BASKETBALL, FOOTBALL, BASEBALL, HOCKEY} mySport;
```

这条语句指定了值并声明了一个变量 mySport，但没有为数据类型指定名称。

然而，创建匿名类型有缺点。首先，由于该类型没有名称，你不能将匿名类型作为参数传递给函数，函数也不能返回匿名类型的值。其次，一个匿名类型中使用的值可以在另一个匿名类型中使用，但这些类型的变量会被区别对待。考虑以下语句：

```cpp
enum {ENGLISH, FRENCH, SPANISH, GERMAN, RUSSIAN} languages;
enum {ENGLISH, FRENCH, SPANISH, GERMAN, RUSSIAN} foreignLanguages;
```

尽管变量 languages 和 foreignLanguages 具有相同的值，编译器仍将它们视为不同类型的变量。因此，下面的语句是非法的：

```cpp
languages = foreignLanguages;  //Illegal
```

尽管这些功能可用，但应谨慎使用。为避免混淆，请先定义枚举类型，然后声明变量。

现在介绍 C++ 中的 `typedef` 语句。

## typedef 语句

在 C++ 中，可以使用 `typedef` 语句为先前定义的数据类型创建同义词或别名。`typedef` 语句的一般语法是：

```cpp
typedef existingTypeName newTypeName;
```

在 C++ 中，`typedef` 是保留字。注意，`typedef` 语句不会创建新的数据类型；它只为现有数据类型创建别名。

### 示例 7-6

语句：

```cpp
typedef int integer;
```

为数据类型 int 创建了一个别名 integer。类似地，语句：

```cpp
typedef double real;
```

为数据类型 `double` 创建了一个别名 `real`。语句：

```cpp
typedef double decimal;
```

为数据类型 `double` 创建了一个别名 `decimal`。

### 示例 7-7

回顾第 4 章，C++ 中的逻辑（布尔）表达式求值为 1 或 0，它们实际上是 `int` 值。作为逻辑值，1 表示 `true`，0 表示 `false`。考虑以下语句：

```cpp
typedef int Boolean;        //Line 1
const Boolean TRUE = 1;     //Line 2
const Boolean FALSE = 0;    //Line 3
Boolean flag;               //Line 4
```

第 1 行的语句为数据类型 `int` 创建了一个别名 `Boolean`。第 2 行和第 3 行的语句声明了命名常量 `TRUE` 和 `FALSE`，并分别将它们初始化为 1 和 0。第 4 行的语句声明 `flag` 为 `Boolean` 类型的变量。由于 `flag` 是 `Boolean` 类型的变量，下面的语句是合法的：

```cpp
flag = TRUE;
```

## 编程示例：石头、剪刀、布游戏

![](img/b217c421655b51e7494cf3b89bb5432d_527_0.png)

孩子们经常玩石头、剪刀、布游戏。该游戏有两名玩家，每人从三个对象中选择一个：石头、布或剪刀。如果玩家 1 选择石头，玩家 2 选择布，则玩家 2 赢得游戏，因为布包住石头。游戏按照以下规则进行：

- 如果两名玩家选择相同的对象，则本局为平局。
- 如果一名玩家选择石头，另一名玩家选择剪刀，则选择石头的玩家赢得本局，因为石头砸坏剪刀。
- 如果一名玩家选择石头，另一名玩家选择布，则选择布的玩家赢得本局，因为布包住石头。
- 如果一名玩家选择剪刀，另一名玩家选择布，则选择剪刀的玩家赢得本局，因为剪刀剪布。

编写一个交互式程序，允许两个人玩这个游戏。

### 输入

该程序有两类输入：

- 询问用户是否要玩游戏时用户的回答。
- 玩家的选择。

### 输出

玩家的选择以及每局的获胜者。游戏结束后，还应输出总局数以及每名玩家获胜的次数。

### 问题分析与算法设计

两名玩家玩这个游戏。玩家通过键盘输入他们的选择。每名玩家输入 R 或 r 表示石头，P 或 p 表示布，S 或 s 表示剪刀。当第一名玩家输入选择时，第二名玩家应看向别处。两个输入都完成后，如果输入有效，程序会输出玩家的选择并宣布本局获胜者。游戏会一直继续，直到其中一名玩家决定退出游戏。游戏结束后，程序输出总局数以及每名玩家获胜的次数。上述讨论可转化为以下算法：

- 1. 简要说明游戏及其玩法。
- 2. 询问用户是否想玩该游戏。
- 3. 获取两名玩家的选择。
- 4. 如果选择有效，输出选择与获胜者。
- 5. 更新游戏总次数和获胜次数。
- 6. 当用户同意继续玩游戏时，重复步骤 2 到 5。
- 7. 输出局数以及每名玩家获胜的次数。

我们将使用以下枚举类型来描述这些对象。

```cpp
enum objectType {ROCK, PAPER, SCISSORS};
```

### 变量（函数 main）

显然，在函数 main 中需要以下变量：

```cpp
int gameCount;  //variable to store the number of
                  //games played
int winCount1;  //variable to store the number of games
                //won by player 1
int winCount2;  //variable to store the number of games
                //won by player 2
int gamewinner;
char response;   //variable to get the user's response to
                 //play the game
char selection1;
char selection2;
objectType play1;  //player1's selection
objectType play2;  //player2's selection
```

该程序分为以下函数，后续各节将详细介绍这些函数。

- **displayRules：** 此函数显示有关游戏及其规则的一些简要信息。
- **validSelection：** 此函数检查玩家的选择是否有效。唯一有效的选择是 `R`、`r`、`P`、`p`、`S` 和 `s`。
- **retrievePlay：** 由于枚举类型不能直接读取，此函数会转换输入的选择（`R`、`r`、`P`、`p`、`S` 或 `s`），并返回相应的对象类型。
- **gameResult：** 此函数输出玩家的选择以及游戏的获胜者。
- **convertEnum：** 此函数由函数 `gameResult` 调用，用于输出枚举类型值。
- **winningObject：** 此函数确定并返回获胜对象。
- **displayResults：** 游戏结束后，此函数显示最终结果。

### 函数 `displayRules`

此函数没有参数。它仅由解释游戏和游戏规则的输出语句组成。本质上，该函数的定义是：

```cpp
void displayRules()
{
    cout << "Welcome to the game of Rock, Paper, "
         << "and Scissors." << endl;
    cout << "This is a game for two players. For each "
         << "game, each" << endl;
    cout << "A player selects one of the objects, Rock, "
         << "Paper or Scissors." << endl;
    cout << "The rules for winning the game are: " << endl;
    cout << "1. If both players select the same object, it "
         << "is a tie." << endl;
    cout << "2. Rock breaks Scissors: So player who selects "
         << "Rock wins." << endl;
    cout << "3. Paper covers Rock: So player who selects "
         << "Paper wins." << endl;
    cout << "4. Scissors cut Paper: So player who selects "
         << "Scissors wins." << endl;
    cout << "Enter R or r to select Rock, P or p to select "
         << "Paper, and S or s to select Scissors." << endl;
}
```

### 函数 `validSelection`

此函数检查玩家的选择是否有效。

```
if selection is 'R' or 'r' or 'S' or 's' or 'P' or 'p', then it
    is a valid selection;
otherwise the selection is invalid.
```
