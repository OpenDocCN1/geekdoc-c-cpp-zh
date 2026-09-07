# C++ 编程：从问题分析到程序设计 [第5版]





这些是非合法的枚举类型，因为没有任何一个值是标识符。
然而，以下是合法的枚举类型：

如果一个值已经在某个枚举类型中使用，则它不能在同一个块的任何其他枚举类型中使用。同样的规则也适用于在任何块之外定义的枚举类型。示例 8–4 阐了这一概念。

## 示例 8-4

考虑以下语句：

```
enum mathStudent {JOHN, BILL, CINDY, LISA, RON};
enum compStudent {SUSAN, CATHY, JOHN, WILLIAM}; //非法
```

假设这些语句位于同一个程序的同一个块中。第二个枚举类型 `compStudent` 是不允许的，因为值 `JOHN` 已经在之前的枚举类型 `mathStudent` 中被使用了。

### 声明变量

一旦定义了类型，你就可以声明该类型的变量。声明枚举类型变量的语法与之前相同：

```
dataType identifier, identifier,...,;
```

语句：

```
enum sports {BASKETBALL, FOOTBALL, HOCKEY, BASEBALL, SOCCER,
VOLLEYBALL};
```

定义了一个名为 `sports` 的枚举类型。语句：

popularSport, mySport;

将 `popularSport` 和 `mySport` 声明为类型 `sports` 的变量。

### 赋值

一旦声明了变量，你就可以在其中存储值。假设前面的声明，语句：

```
popularSport = FOOTBALL;
```

将 `FOOTBALL` 存储在 `popularSport` 中。语句：

mySport = popularSport;

将 `popularSport` 的值 copies 复制到 `mySport` 中。

### 枚举类型的操作

枚举类型不允许进行算术运算。因此，以下语句是非法的：

```
mySport = popularSport + 2;               //非法
popularSport = FOOTBALL + SOCCER;     //非法
popularSport = popularSport * 2;       //非法
```

此外，枚举类型不允许进行自增和自减操作。因此，以下语句是非法的：

```
popularSport++;               //非法
popularSport--;               //非法
```

假设你想将 `popularSport` 的值加 1。你可以使用类型转换运算符：

```
popularSport = static_cast<sports>(popularSport + 1);
```

当使用该名称时，编译器假设用户理解其正在做什么。因此，前面的语句会被编译，并且在执行期间，它会将 `popularSport` 的值推进到列表中的下一个值。考虑以下语句：

```
popularSport = FOOTBALL;
popularSport = static_cast<sports>(popularSport + 1);
```

在第二个语句之后，`popularSport` 的值为 `HOCKEY`。同样，将 `BASKETBALL` 存储在 `popularSport` 中的结果如下：

```
popularSport = FOOTBALL;
popularSport = static_cast<sports>(popularSport - 1);
```

结果是将 `BASKETBALL` 存储在 `popularSport` 中。

### 关系运算符

由于枚举是一个有序的值集合，关系运算符可以与枚举类型一起使用。同样假设你拥有之前定义的 `sports` 枚举类型以及变量 `popularSport` 和 `mySport`。那么：

```
FOOTBALL <= SOCCER true
HOCKEY > BASKETBALL true
BASEBALL < FOOTBALL false
```

假设：

```
popularSport = SOCCER;
mySport = VOLLEYBALL;
```

那么：

```
popularSport < mySport is true
```

### 枚举类型与循环

回想枚举类型是一种整类型，使用类型转换运算符（即 `operator (type, name)`），你可以递增、递减和比较枚举类型的值。因此，你可以在循环中使用这些枚举类型。假设 `mySport` 是之前声明的变量。考虑以下 `for` 循环：

```
for (mySport = BASKETBALL; mySport < SOCCER;
mySport = static_cast<sports>(mySport + 1))
```

这个 `for` 循环有五次迭代。在循环中使用枚举增加了程序的可读性。

### 枚举类型的输入/输出

由于输入和输出只定义了 `int`、`char` 等内置类型，枚举类型既不能直接输入也不能直接输出。然而，你可以间接地进行。假设你拥有以下语句：

```
enum courses {ALGEBRA, ANALYSIS, BASIC, CHEMISTRY, HISTORY, PASCAL, PHILOSOPHY};
```

为了输入，例如使用以下结构：

```cpp
char ch1, ch2;

cout << "Enter the two letters of the course: " << endl;
cin >> ch1 >> ch2;

switch (ch1)
{
    case 'a':
    case 'A':
        if (ch2 == 'l' || ch2 == 'L')
            registered = ALGEBRA;
        else
            registered = ANALYSIS;
        break;
    case 'b':
    case 'B':
        registered = BASIC;
        break;
    case 'c':
    case 'C':
        if (ch2 == 'h' || ch2 == 'H')
            registered = CHEMISTRY;
        else
            registered = CPP;
        break;
    case 'h':
    case 'H':
        registered = HISTORY;
        break;
    case 'p':
    case 'P':
        if (ch2 == 'a' || ch2 == 'A')
            registered = PASCAL;
        else
            registered = PHILOSOPHY;
        break;
    default:
        cout << "Illegal input." << endl;
}
```

同样，你可以直接输出枚举类型：

```cpp
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
    case PASCAL:
        cout << "Pascal";
        break;
    case PHILOSOPHY:
        cout << "Philosophy";
        break;
}
```

### 函数与枚举类型

你可以像其他简单类型一样将枚举类型传递给函数——即通过值或引用。此外，就像简单类型一样，函数也可以返回枚举类型的值。通过这种机制，你可以使用函数来输入枚举类型。假设枚举类型定义之前：

```cpp
courses readCourse()
{
    courses registered;
    char ch1, ch2;

    cout << "Enter the two letters of the course: " << endl;
    cin >> ch1 >> ch2;

    switch (ch1)
    {
        case 'a':
        case 'A':
            if (ch2 == 'l' || ch2 == 'L')
                registered = ALGEBRA;
            else
                registered = ANALYSIS;
            break;
        case 'b':
        case 'B':
            registered = BASIC;
            break;
        case 'c':
        case 'C':
            if (ch2 == 'h' || ch2 == 'H')
                registered = CHEMISTRY;
            else
                registered = CPP;
            break;
        case 'h':
        case 'H':
            registered = HISTORY;
            break;
        case 'p':
        case 'P':
            if (ch2 == 'a' || ch2 == 'A')
                registered = PASCAL;
            else
                registered = PHILOSOPHY;
            break;
        default:
            cout << "Illegal input." << endl;
    }
    return registered;
}
//end readCourse
```

以下函数输出一个枚举类型值：

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
        case PASCAL:
            cout << "Pascal";
            break;
        case PHILOSOPHY:
            cout << "Philosophy";
            break;
    }
}
```






```cpp
case CPP:
out << "CPP";
break;
case HISTORY:
out << "History";
break;
case PASCAL:
out << "Pascal";
break;
case PHILOSOPHY:
out << "Philosophy";
break;
} // switch
//end printEnum
```

### 在定义枚举类型时声明变量

在之前的章节中，你首先定义了一个枚举，然后声明了该类型的变量。C++ 允许你将这些步骤合并为一。也就是说，你可以在定义枚举类型的同时声明该枚举类型的变量。例如，语句：

```cpp
enum {A, B, C, D, F} courseGrade;
```

这定义了一个枚举类型 `grades`，并声明了一个类型为 `grades` 的变量 `courseGrade`。

同样，该语句：

```cpp
enum {PENNY, NICKEL, DIME, HALFDOLLAR, DOLLAR} change, usCoins;
```

这定义了一个枚举类型 `coins`，并声明了两个类型为 `coins` 的变量 `change` 和 `usCoins`。

### 匿名数据类型

在变量声明中直接指定值而没有名称的数据类型被称为匿名类型。以下语句创建了一个匿名类型：

```cpp
enum {BASKETBALL, FOOTBALL, BASEBALL, HOCKEY} mySport;
```

该语句指定了值并声明了变量 `mySport`，但没有给数据类型命名。

然而，创建匿名类型有缺点。首先，由于该类型没有名称，你无法将匿名类型作为参数传递给函数，函数也无法返回匿名类型的值。其次，在一个匿名类型中使用的值可以在另一个匿名类型中使用，但这些类型的变量处理方式不同。考虑以下语句：

```cpp
enum {ENGLISH, FRENCH, SPANISH, GERMAN, RUSSIAN} languages;
enum {ENGLISH, FRENCH, SPANISH, GERMAN, RUSSIAN} foreignLanguages;
```

尽管变量 `languages` 和 `foreignLanguages` 具有相同的值，但编译器将它们视为不同类型的变量。因此，以下语句是非法的：

```cpp
languages = foreignLanguages; // 非法
```

尽管可以使用这些功能，但使用时要谨慎。为了避免混淆，请先定义枚举类型并声明变量。

我们将描述 C++ 中的 `typedef` 语句。

### typedef 语句

在 C++ 中，你可以使用 `typedef` 语句为之前定义的数据类型创建别名或代号。`typedef` 语句的一般语法为：

```cpp
typedef existingTypeName newTypeName;
```

在 C++ 中，`typedef` 是一个关键字。注意，`typedef` 语句不会创建任何数据类型；它只创建现有数据类型的别名。

> 示例 8-6

语句：
`typedef int integer;`

为数据类型 `int` 创建了别名 `integer`。同样，该语句：

`typedef double real;`
为数据类型 `double` 创建了别名 `real`。该语句：

`typedef double decimal;`
为数据类型 `double` 创建了别名 `decimal`。

使用 `typedef` 语句，你可以创建自己的布尔数据类型，如 8-7 所示。

> 示例 8-7

回想第 4 章，记得 C++ 中的逻辑（布尔）表达式求的值为 1 或 0，这些实际上是 `int` 值。作为一个逻辑值，1 代表真，0 代表假。考虑以下语句：

![](img/b08b54ded82fc9e3d8d95107a5b40e44_7_0.png)


```cpp
typedef int Boolean; // 第1行
const Boolean TRUE = 1; // 第2行
const Boolean FALSE = 0; // 第3行
Boolean flag; // 第4行
```

第 1 行的语句为数据类型 `int` 创建了别名 `Boolean`。第 2 行和第 3 行的语句声明了命名常量 `TRUE` 和 `FALSE`，并分别将它们初始化为 1 和 0。第 4 行的语句声明 `flag` 为 `Boolean` 类型的变量。因为 `flag` 是 `Boolean` 类型的变量，以下语句是：

```cpp
flag = TRUE;
```

### 编程示例：剪刀石头布游戏

孩子们经常玩剪刀石头布游戏。这个游戏有两个玩家，每个人选择三个物体中的一个：石头、纸或剪刀。如果玩家 1 选择石头而玩家 2 选择纸，则玩家 2 赢得游戏，因为纸盖住石头。游戏按照以下规则进行：

- 如果两个玩家都选择同一个物体，则平局。
- 如果一个玩家选择石头而另一个选择剪刀，则选择石头的人胜，因为石头可以打碎剪刀。
- 如果一个玩家选择石头而另一个选择纸，则选择纸的人胜，因为纸盖住石头。
- 如果一个玩家选择剪刀而另一个选择纸，则选择剪刀的人胜，因为剪刀可以剪纸。

编写一个交互式程序，允许两个玩家玩这个游戏。

- 用户在被要求玩游戏时的响应。
- 玩家的选择。

输入 此程序有两种类型的输入：

输出 玩家的选择以及每局的获胜者。游戏结束后，应该输出总局数和该玩家胜的次数。

两个玩家玩这个游戏。每个人通过键盘输入选择。每个玩家输入 R 代表石头，P 代表纸，或 S 代表剪刀。输出玩家的选择以及每局的获胜者。游戏结束后，应该输出总局数和该玩家胜的次数。

两个玩家玩这个游戏。每个人通过键盘输入选择。每个玩家输入 R 代表石头，P 代表纸，或 S 代表剪刀。输出玩家的选择以及每局的获胜者。游戏结束后，应该输出总局数和该玩家胜的次数。

### 编程示例：剪刀石头布游戏


两个玩家玩这个游戏。每个人通过键盘输入选择。每个玩家输入 R 代表石头，P 代表纸，或 S 代表剪刀。输出玩家的选择以及每局的获胜者。游戏结束后，应该输出总局数和该玩家胜的次数。

我们将使用枚举类型来描述物体。

```cpp
enum objectType {ROCK, PAPER, SCISSORS};
```

该程序分为以下函数，并对它们进行了详细说明：

- displayRules：显示关于游戏的信息。
- validSelection：检查玩家的选择是否有效。
- retrievePlay：由于枚举类型无法直接读取，该函数转换输入（R, r, P, p, S 或 s）并返回对象类型。
- gameResult：输出玩家的选择和获胜者。
- main：协调游戏。

变量（在 main 中）：

```cpp
int gameCount;
int winCount1;
int winCount2;
```

displayRules 函数没有参数。它仅由解释游戏和规则的输出语句组成。基本上，该函数的定义为：

```cpp
void displayRules() {
    cout << "欢迎来到剪刀石头布" << endl;
    cout << "游戏。" << endl;
    cout << "这是一个两个人的游戏。对于每局" << endl;
    cout << "游戏规则如下：" << endl;
    cout << "  1. 如果两个玩家都选择同一个物体，则" << endl;
    cout << "  平局。" << endl;
    cout << "  2. 石头打碎剪刀：选择石头的人" << endl;
    cout << "  获胜。" << endl;
    cout << "  3. 纸盖住石头：选择纸的人" << endl;
    cout << "  获胜。" << endl;
    cout << "  4. 剪刀剪纸：选择剪刀的人" << endl;
    cout << "  获胜。" << endl;
    cout << "  输入 R 或 r 选择石头，P 或 p 选择" << endl;
    cout << "  纸，以及 S 或 s 选择剪刀。" << endl;
}
```

validSelection 函数检查玩家的选择是否有效。让我们使用 switch 语句来检查有效选择。该函数的定义为：

```cpp
bool validSelection(char selection) {
    switch (selection) {
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





```cpp
case 's':
    return true;
    default:
        return false;
}
```

函数 `retrievePlay`：由于枚举无法直接读取，此函数转换输入的选择（R, r, P, p, S, s）并返回相应的对象类型。该函数有一个参数，类型为 `char`。它是一个返回值的函数，返回一个 `objectType` 类型的值。在伪代码中，该函数的算法如下：

```
if selection is 'R' or 'r'
    return ROCK;

if selection is 'P' or 'p'
    return PAPER;

if selection is 'S' or 's'
    return SCISSORS;
```

`retrievePlay` 函数的定义如下：

```cpp
object retrievePlay(char selection)
{
    object object;
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

函数 `gameResult`：此函数决定游戏是平局还是哪位玩家获胜。它输出玩家的选择和游戏的胜者。显然，该函数有三个参数：玩家 1 的选择、玩家 2 的选择以及一个用于返回胜者的参数。在伪代码中，该函数为：

- a. 如果 player1 和 player2 的选择相同，则这是一场平局。
- b. 否则
    - 1. 确定获胜的对象（调用函数 `winningObject`）。
2. 输出每个玩家的选择。
3. 确定胜者。
4. 通过引用参数将胜者返回给函数 `main`，以便 `main` 函数可以更新获胜者的胜利次数。

该函数的定义如下：

```cpp
void gameResult(objectType play1, objectType play2,
    int &winner)
{
    objectType winnerObject;
    if (play1 == play2) {
        winner = 0;
        cout << "Both players selected ";
        convertEnum(play1);
        cout << ". This game is a tie." << endl;
    } else {
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
        cout << "Player " << winner << " wins this game.";
        cout << endl;
    }
}
```

由于枚举类型无法直接输出，让我们编写函数 `convertEnum` 来输出 `objectType` 枚举的对象。该函数有一个参数，类型为 `objectType`。它输出与 `objectType` 对应的字符串。在伪代码中，该函数为：

```
{
if object is ROCK
    output "Rock"

if object is PAPER
    output "Paper"

if object is SCISSORS
    output "Scissors"
```

`convertEnum` 函数的定义：

```cpp
void convertEnum(objectType) {
    switch (object) {
        case ROCK:
            cout << "Rock";
            break;
        case PAPER:
            cout << "Paper";
            break;
        case SCISSORS:
            cout << "Scissors";
    }
}
```

函数 `winningObject`：为了决定游戏的胜者，你会查看玩家的选择以及游戏规则。例如，如果一个玩家选择 ROCK 而另一个选择 PAPER，那么选择 PAPER 的玩家获胜。换句话说，`winningObject` 函数接收两个 `objectType` 类型的对象，并返回获胜的对象。显然，该函数有两个 `objectType` 类型的参数，返回值也是 `objectType` 类型。

```cpp
objectType winningObject(objectType play1, objectType play2) {
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

函数 `displayResults`：游戏结束后，此函数输出最终结果——即总次数以及每个玩家的胜利次数。总次数存储在变量 `gameCount` 中，玩家 1 的胜利次数存储在 `winCount1` 中，玩家 2 的胜利次数存储在 `winCount2` 中。该函数有对应这三个变量的参数。它的定义如下：

```cpp
void displayResults(int gCount, int wCount1, int wCount2) {
    cout << "The total number of players: " << gCount
         << endl;
    cout << "The number of plays won by player 1: "
         << wCount1 << endl;
    cout << "The number of plays won by player 2: "
         << wCount2 << endl;
}
```

现在准备编写函数的算法：

1. 声明变量。
2. 初始化变量。
3. 显示规则。
4. 提示玩家游戏。
5. 当响应为是时：
    a. 提示玩家 1 选择。
    b. 提示玩家 2 选择。
    c. 如果选择都是合法的：
        i. 增加计数。
        ii. 确定胜者。
        iii. 获胜者的计数加 1。
    d. 提示玩家是否想再次游戏。
    e. 获取响应。
7. 输出游戏结果。

## 程序列表

```cpp
#include <iostream>
using namespace std;

enum objectType {ROCK, PAPER, SCISSORS};

//Function原型
void displayRules();
bool validSelection(char selection);
void convertEnum(objectType object);
objectType winningObject(objectType play1, objectType play2);
void gameResult(objectType play1, objectType play2, int &winner);
void displayResults(int gCount, int wCount1, int wCount2);

int main() {
    //Step 1
    int gameCount;
    int winCount1;
    int winCount2;
    int gamewinner;
    char response;
    char selection1;
    char selection2;

    //Step 2
    gameCount = 0;
    winCount1 = 0;
    winCount2 = 0;

    //Step 3
    displayRules();

    //Step 4
    cout << "Y/n to play the game: ";
    cin >> response;

    //Step 5
    while (response == 'Y' || response == 'y') { //Step 6
        //Step 6a
        cout << "Player 1 enter your selection: ";
        cin >> selection1;
        cout << endl;

        //Step 6b
        cout << "Player 2 enter your selection: ";
        cin >> selection2;
        cout << endl;

        //Step 6e
        if (validSelection(selection1) && validSelection(selection2)) {
            //Step 6e.i
            gameCount++;
            //Step 6e.ii
            objectType play1 = retrievePlay(selection1);
            objectType play2 = retrievePlay(selection2);
            gameResult(play1, play2, gamewinner);
            //Step 6e.iii
            if (gamewinner == 1)
                winCount1++;
            else if (gamewinner == 2)
                winCount2++;
        }
        //Step 6f
        cout << "Enter Y/y to play the game: ";
        cin >> response;
        cout << endl;
    } //end while

    //Step 7
    displayResults(gameCount, winCount1, winCount2);

    return 0;
} //end main

void displayRules() {
    cout << "Rules of the game:" << endl;
    cout << "1. Rock beats Scissors." << endl;
    cout << "2. Paper beats Rock." << endl;
    cout << "3. Scissors beats Paper." << endl;
}

bool validSelection(char selection) {
    if (selection == 'R' || selection == 'r' ||
        selection == 'P' || selection == 'p' ||
        selection == 'S' || selection == 's') {
        return true;
    }
    return false;
}

objectType retrievePlay(char selection) {
    objectType object;
    switch (selection) {
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

void convertEnum(objectType object) {
    switch (object) {
        case ROCK:
            cout << "Rock";
            break;
        case PAPER:
            cout << "Paper";
            break;
        case SCISSORS:
            cout << "Scissors";
    }
}

objectType winningObject(objectType play1, objectType play2) {
    if ((play1 == ROCK && play2 == SCISSORS)
        || (play2 == ROCK && play1 == SCISSORS))
        return ROCK;
    else if ((play1 == ROCK && play2 == PAPER)
        || (play2 == ROCK && play1 == PAPER))
        return PAPER;
    else
        return SCISSORS;
}

void gameResult(objectType play1, objectType play2, int &winner) {
    objectType winnerObject;
    if (play1 == play2) {
        winner = 0;
        cout << "Both players selected ";
        convertEnum(play1);
        cout << ". This game is a tie." << endl;
    } else {
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
        cout << "Player " << winner << " wins this game.";
        cout << endl;
    }
}

void displayResults(int gCount, int wCount1, int wCount2) {
    cout << "The total number of players: " << gCount
         << endl;
    cout << "The number of plays won by player 1: "
         << wCount1 << endl;
    cout << "The number of plays won by player 2: "
         << wCount2 << endl;
}
```




在后续章节中，除非另有说明，C++ 语法适用于所有标准。首先，我们将讨论 ANSI/ISO 标准 C++ 的命名空间机制，该机制在第 2 章中介绍。

当程序包含一个头文件（如 `iostream`）时，头文件中的全局标识符也会成为程序中的全局标识符。因此，如果程序中的一个全局标识符与头文件中的某个全局标识符同名，编译器将产生语法错误（例如“标识符重定义”）。当程序使用第三方库时，也会发生相同的问题。为了解决这个问题，第三方供应商开始使用特殊符号作为标识符的开头。在第 2 章中，你学过编译器供应商的全局标识符名称以下划线（`_`）开头以避免标识符冲突。

ANSI/ISO 标准 C++ 试图通过命名空间机制来解决全局标识符冲突的问题。

命名空间的通用语句为：

```cpp
namespace namespace_name
{
    members
}
```

其中 `members` 通常是命名常量、变量声明、函数或其他命名空间。注意 `namespace_name` 是一个 C++ 标识符。

在 C++ 中，`namespace` 是保留字。

### 示例 8-8

该语句：

```cpp
namespace globalType
{
    const int N = 10;
    const double RATE = 7.50;
    int count = 0;
    void printResult();
}
```

将 `globalType` 定义为一个包含四个成员的命名空间：命名常量 `N` 和 `RATE`、变量 `count` 以及函数 `printResult`。

命名空间成员的作用域是局限于命名空间的。你通常可以通过以下两种方式在命名空间外访问命名空间成员，如下所示。

访问命名空间成员的通用语法为：

```cpp
namespace_name::identifier
```

回在 C++ 中，`::` 被称为作用域解析运算符。
要访问 `globalType` 的成员 `RATE`，需要以下语句：

`globalType::RATE`

要访问成员 `printResult`（这是一个函数），需要以下语句：

`globalType::printResult();`

因此，要访问命名空间，你使用 `namespace_name`，后跟作用域解析运算符，最后是成员名。

为了简化对命名空间的访问，ANSI/ISO 标准 C++ 提供了 `using`语句。`using` 语句的语法如下：

- a. 简化所有命名空间成员的访问：
  `using namespace namespace_name;`
- b. 简化特定命名空间成员的访问：
  `using namespace_name::identifier;`

例如，`using`语句：
`using namespace globalType;`
简化了对 `globalType` 命名空间所有成员的访问。语句：
`using globalType::RATE;`
简化了对 `globalType` 命名空间成员 `RATE` 的访问。

在 C++ 中，`using` 是保留字。你通常将 `using`语句放在命名空间声明之后。例如，对于命名空间 `globalType`，你通常如下编写：

```cpp
namespace globalType
{
  const int N = 10;
  const double RATE = 7.50;
  int count = 0;
  void printResult();
}
using namespace globalType;
```

在使用 `using` 语句之后，访问命名空间成员时不需要在命名空间成员之前加上 `namespace_name` 和作用域解析运算符。然而，如果程序中的命名空间成员与全局标识符同名，为了在程序中访问该命名空间成员，必须在在该成员之前加上 `namespace_name` 和作用域解析运算符。同样，如果块中的命名空间成员与块中的标识符同名，为了在块中访问该命名空间成员，必须在其之前加上 `namespace_name` 和作用域解析运算符。

示例 8-9 到 8-12 阐明了命名空间机制的使用。

### 示例 8-9

考虑以下 C++ 代码：

```cpp
#include <iostream>
using namespace std;

int main()
{
}
```

在此示例中，访问 `iostream` 头文件的全局标识符（如 `cin`、`cout` 和 `endl`）不需要使用 `std::` 前缀。

### 示例 8-10

考虑以下 C++ 代码：

```cpp
#include <cmath>
int main() {
    double x = 15.3;
    double y;
    y = pow(x, 2);
}
```

此示例访问了 `cmath` 头文件的 `pow` 函数。

### 示例 8-11

考虑以下 C++ 代码：

```cpp
#include <iostream>
using namespace std;

int main() {
    string t;
}
```

在此示例中，访问 `iostream` 头文件的全局标识符不需要使用 `std::` 前缀。

### 示例 8-12

考虑以下 C++ 代码：

```cpp
#include <iostream>
using namespace std;
namespace expN {
    string t;
    void printResult();
    double u;
}
int main() {
    int one;
    int two;
    int three;
    double u;
}
```

string 类型

在第 2 章中，你被介绍了 `string` 类型。回想在 ANSI/ISO C++ 语言之前，标准 C++ 库并没有提供 `string` 类型。编译器供应商通常提供他们定义的字符串类型，且字符串操作的语法和语义随语言而异；`string` 类型是用户定义的类型，也是 C++ 语言的一部分；C++ 标准库提供了它。在使用 `string` 类型之前，程序必须包含 `string` 头文件：

```cpp
#include <string>
```

回想在 C++ 中，字符串是零或多个字符的序列，且字符串用双引号括起来。语句：

```cpp
string name = "William Jacob";
```

将 `name` 声明为字符串变量并初始化为 `"William Jacob"`。`name` 中第一个字符 `W` 的位置是 0；第二个字符 `i` 的位置是 1；以此类推。因此，字符串变量中第一个字符的位置从 0 开始，而不是 1。

变量可以存储任何大小的字符串。

第 3 章讨论了 `string` 类型的 I/O 操作；第 4 章解释了 `string` 类型的关系操作。我们建议复习第 3 章和第 4 章，回顾 `string` 类型的 I/O 和关系操作。

其他运算符，例如二进制运算符 `+`（用于字符串拼接操作）和数组索引运算符 `[]`，也为 `string` 类型进行了定义。让我们看看这些运算符在 `string` 类型上是如何工作的。

假设你有以下声明：

```cpp
string str1, str2, str3;
```


语句：

```
str1 = "Hello There";
```

将字符串 "Hello There" 存储在 str1 中。语句：

```
str2 = str1;
```

将 str1 的值拷贝到 str2 中。

如果 str1 = "Sunny"，则语句：

```
str2 = str1 + " Day";
```

将字符串 "Sunny Day" 存储到 str2 中。

假设 str1 = "Hello " 且 str2 = "There"。语句：

```
str3 = str1 + " " + str2;
```

将 "Hello There" 存储到 str3 中。此语句等同于语句：

```
str3 = str1 + ' ' + str2;
```

此外，语句：

```
str1 = str1 + " Mickey";
```

通过在其旧值末尾追加字符串 "Mickey" 来更新 str1 的值。因此，str1 的新值为 "Hello Mickey"。

> 若要运算符 + 能够与字符串数据类型配合使用，+ 的操作数必须是一个字符串变量。例如，以下语句将无法工作：

```
str1 = "Hello " + "there!"; //非法
str2 = "Sunny Day " + ' '! //非法
```

如果 str1 = "Hello there"，则语句：

```
str1[6] = 'T';
```

将 t 替换为字符 T。记住，字符串变量中第一个字符的位置是 0。因此，由于 t 是 str1 中的第七个字符，它的位置是 6。

在 C++ 中，[] 被称为数组下标运算符。

如前文所示，通过使用数组下标运算符结合字符的位置，你可以访问字符串中的单个字符。

### 示例 8-13

以下程序展示了前述语句的效果。

```
//Example string operations

#include <iostream>
#include <string>

using namespace std;

int main() {
    string name = "William Jacob";
    string str1, str2, str3, str4;

    cout << "Line 3: Name = " << name << endl;

    str1 = "Hello There";
    cout << "Line 5: str1 = " << str1 << endl;

    str2 = str1;
    cout << "Line 7: str2 = " << str2 << endl;

    str3 = "Sunny";
    str2 = str1 + " Day";
    cout << "Line 10: str2 = " << str2 << endl;

    str1 = "Hello";
    str2 = "There";
    str3 = str1 + " " + str2;
    cout << "Line 14: str3 = " << str3 << endl;

    str3 = str1 + ' ' + str2;
    cout << "Line 16: str3 = " << str3 << endl;

    str1 = str1 + " Mickey";
    cout << "Line 18: str1 = " << str1 << endl;

    str1 = "Hello there";
    cout << "Line 20: str1[6] = " << str1[6] << endl;

    str1[6] = 'T';
    cout << "Line 22: str1 = " << str1 << endl;

    //String input operations
    cout << "Line 23: Enter a string with ";
    cout << "no blanks: ";
    cin >> str1;

    char ch1;
    cin.get(ch1);
    cout << endl;
    cout << "Line 28: The string you entered = "
         << str1 << endl;
    cout << "Line 29: Enter a sentence: ";
    getline(cin, str2);
    cout << endl;
    cout << "Line 32: The sentence is: " << str2
         << endl;

    return 0;
}
```

**示例运行：** 在下面的示例运行中，用户输入被阴影显示。

- Line 3: Name = William Jacob
- Line 5: str1 = Hello There
- Line 7: str2 = Hello There
- Line 10: str2 = Sunny Day
- Line 14: str3 = Hello There
- Line 16: str3 = Hello There
- Line 18: str1 = Hello Mickey
- Line 20: str1[6] = t
- Line 22: str1 = Hello There
- Line 23: Enter a string with no blanks: Programming
- Line 28: The string you entered = Programming
- Line 29: Enter a sentence: Testing string operations
- Line 32: The sentence is: Testing string operations

上述输出是不言自明的，而其推导过程留给你们作为练习。

### 额外的字符串操作

数据类型 `string` 有一个数据类型 `string::size_type` 以及一个命名常量 `string::npos`，定义如下：

| string::size_type | 一个无符号整数（数据）类型 |
| string::npos | （数据）类型 `string:string::size_type` 的最大值，在许多机器上该数字为 4294967295 |

数据类型 `string` 包含了几个其他用于字符串处理的函数。下表描述了这些函数。在表中，我们假设 `strVar` 是字符串变量，而 `str` 是字符串变量、字符串常量或字符数组（数组将在第9章中讨论）。

#### 表格 8-1 某些字符串函数

| 表达式 | 效果 |
| :--- | :--- |
| strVar.at(index) | 返回指定位置的元素。 |
| strVar[index] | 返回指定位置的元素。 |
| strVar.append(n, ch) | 向 strVar 追加 n 个 ch；`pos` 和 `n` 类型为 `string:size_type`；`ch` 为字符。 |
| strVar.append(str) | 向 strVar 追加 str。 |
| strVar.clear() | 删除 strVar 中的所有字符。 |
| strVar.compare(str) | 比较 strVar 和 str。（此操作在第4章中讨论。） |
| strVar.empty() | 如果 strVar 为空返回 true，否则返回 false。 |
| strVar.erase() | 删除 strVar 中的所有字符。 |
| strVar.erase(pos, n) | 从 strVar 位置 pos 开始删除 n 个字符。 |
| strVar.find(str) | 返回 str 在 strVar 中首次出现的索引。如果未找到，则返回特殊值 `string::npos`。 |
| strVar.find(str, pos) | 返回 strVar 中从 pos 之后首次找到 str 的索引。 |
| strVar.find_first_of(str, pos) | 返回 strVar 中 str 任意字符首次出现的索引。搜索从 pos 开始。 |
| strVar.find_first_not_of(str, pos) | 返回 strVar 中任何不在 str 中的字符首次出现的索引。搜索从 pos 开始。 |
| strVar.insert(pos, n, ch) | 在 strVar 中插入 n 次 ch 的出现；`pos` 和 `n` 类型为 `string:size_type`；`ch` 为字符。 |
| strVar.insert(pos, str) | 将 str 的所有字符插入 strVar 的索引 pos 处。 |
| strVar.length() | 返回类型为 `string::size_type` 的值，表示 strVar 的字符数。 |

