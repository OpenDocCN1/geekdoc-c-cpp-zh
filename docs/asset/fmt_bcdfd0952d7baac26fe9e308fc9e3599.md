
# 示例输入对应的程序输出（加粗部分为输入）

XYZ 公司的交易代码是 XYZ
该股票目前的价格为 $9.62 每股。
你想买多少股股票？**100**
交易总成本为 $962.00

# 使用 CRC 卡片确定类之间的协作

在面向对象的设计过程中，你可以通过检查类的职责，确定类与类之间可能需要的许多协作。在第 13 章中，我们讨论了寻找类及其职责的过程。回顾该章节内容，类的职责包括：

- 类负责获晓的内容。
- 类负责执行的操作。

通常，你会发现为了完成一个或多个职责，某个类必须与另一个类协作。发现类职责和协作的一种流行方法是创建 CRC 卡。CRC 代表类（class）、职责（responsibilities）和协作（collaborations）。

你可以使用简单的索引卡片完成此过程。一旦完成了类的确定过程（已在第 13 章中讨论过），为每个类准备一张索引卡片。在卡片顶部写上类名。将卡片分为两列。在左列写下类的每项职责。在写每项职责时，思考该类是否需要与另一个类协作来完成该职责。问自己一些问题：

- 此类的对象是否需要从另一个对象获取数据以完成其职责？
- 此类的对象是否需要另一个对象来执行某项操作以完成该职责？

如果需要协作，请在右列对应项的职责旁边写下协作类的名称。如果某项职责不需要协作，只需在右列写“无”或留空。图 14-8 显示了 `StockPurchase` 类的 CRC 卡示例。

![](img/191adf3284699566e6a7b1008ce9bdb5_908_0.png)

从图中所示的 CRC 卡中我们可以看到 `StockPurchase` 类具有以下职责和协作：

- 职责：知道要购买的股票
  协作：`Stock` 类
- 职责：知道要购买的股数
  协作：无
- 职责：计算购买成本
  协作：`Stock` 类

当你完成应用程序中每个类的 CRC 卡后，你对每个类的职责以及类之间必须如何交互将有一个很好的了解。

# 检查点

（此处后续内容为重复不完整占位符，已按要求不重复输出）

## 14.9 专注于面向对象编程：模拟“骰汉”游戏

- `rollDice`：`Dealer.cpp` 的第 22 至 31 行。该成员函数模拟掷骰子的过程。第 25 和 26 行调用了 `Dice` 对象的 `roll` 方法。第 29 和 30 行将骰子的值保存在变量 `die1Value` 和 `die2Value` 成员变量中。
- `getChoOrHan`：`Dealer.cpp` 的第 38 至 53 行。该成员函数返回一个字符串，表示骰子和是“Cho”（偶数）还是“Han”（奇数）。
- `getDie1Value`：`Dealer.cpp` 的第 59 至 62 行。该成员函数返回第一个骰子的值（存储在 `die1Value` 成员变量中）。
- `getDie2Value`：`Dealer.cpp` 的第 68 至 71 行。该成员函数返回第二个骰子的值（存储在 `die2Value` 成员变量中）。

现在，让我们来看看 `Player` 类。

### Player.h 内容

```cpp
// Player 类的规范文件

#ifndef PLAYER_H
#define PLAYER_H
#include <string>

using namespace std;

class Player
{
private:
    string name;            // 玩家的名字
    string guess;           // 玩家的猜测
    int points;             // 玩家的得分

public:
    Player(string);         // 构造函数
    void makeGuess();       // 让玩家做出猜测
    void addPoints(int);    // 给玩家加分
    string getName();       // 返回玩家的名字
    string getGuess();      // 返回玩家的猜测
    int getPoints();        // 返回玩家的得分
};
#endif
```

### Player.cpp 内容

```cpp
// Player 类的实现文件

#include "Player.h"
#include <cstdlib>
#include <ctime>
#include <string>

using namespace std;

//****************************************************
// 构造函数
//****************************************************
Player::Player(string playerName)
{
    // 种子随机数生成器
    srand(time(0));

    name = playerName;
    guess = "";
    points = 0;
}

//****************************************************
// makeGuess 成员函数让玩家
// 做出猜测，可能是“Cho (偶数)”
// 或“Han (奇数)”。
//****************************************************
void Player::makeGuess()
{
    const int MIN_VALUE = 0;
    const int MAX_VALUE = 1;

    int guessNumber; // 用于玩家的猜测

    // 获取一个随机数，0 或 1。
    guessNumber = (rand() % (MAX_VALUE - MIN_VALUE + 1)) + MIN_VALUE;

    // 将随机数转换为 Cho 或 Han。
    if (guessNumber == 0)
        guess = "Cho (even)";
    else
        guess = "Han (odd)";
}

//****************************************************
// addPoints 成员函数向玩家的
// 当前余额增加指定数量的
// 分。
//****************************************************
void Player::addPoints(int newPoints)
{
    points += newPoints;
}

//****************************************************
// GetName 成员函数返回玩家
// 的名字。
//****************************************************
string Player::getName()
{
    return name;
}

//****************************************************
// getGuess 成员函数返回玩家
// 的猜测。
//****************************************************
string Player::getGuess()
{
    return guess;
}

//********************************************************************
// getPoints 成员函数返回玩家
// 的得分。
//********************************************************************
int Player::getPoints()
{
    return points;
}
```

以下是类成员的摘要：

- `name`：声明在 `Player.h` 的第 10 行。该成员变量将存储玩家的名字。
- `guess`：声明在 `Player.h` 的第 11 行。该成员变量将存储玩家的猜测。
- `points`：声明在 `Player.h` 的第 12 行。该成员变量将存储玩家的得分。
- 构造函数：`Player.cpp` 的第 11 至 19 行，接受玩家名字作为参数并赋值给 `name` 字段。`guess` 字段被赋值为空字符串，`points` 字段设置为 0。
- `makeGuess`：`Player.cpp` 的第 26 至 41 行。该函数让玩家做出猜测。该函数生成一个 0 或 1 的随机数。该语句将 0 或 1 的随机数转换为“Cho (偶数)”或“Han (奇数)”。
- `addPoints`：`Player.cpp` 的第 49 至 52 行。该函数将指定的分数增加到玩家当前的余额中。
- `getName`：`Player.cpp` 的第 58 至 61 行。该函数返回玩家的名字。
- `getGuess`：`Player.cpp` 的第 67 至 70 行。该函数返回玩家的猜测。
- `getPoints`：`Player.cpp` 的第 76 至 79 行。该函数返回玩家的得分。

# 程序 14-17

```cpp
// 显示玩家 1 号的结果。

cout << player1.getName() << " : ";
cout << player1.getPoints() << " points\n";

// 显示玩家 2 号的结果。

cout << player2.getName() << " : ";
cout << player2.getPoints() << " points\n";

// 确定大胜者。

if (player1.getPoints() > player2.getPoints()) {
    cout << player1.getName();
    cout << " is the grand winner!\n";
} else if (player2.getPoints() > player1.getPoints()) {
    cout << player2.getName();
    cout << " is the grand winner!\n";
} else {
    cout << "Both players are tied!\n";
}
```

# 程序输出（示例输入已加粗显示）

输入第一个玩家的名字：**Bill**
输入第二个玩家的名字：**Jill**

现在开始第 1 轮
庄主掷出了 4 和 6
结果：Cho（偶数）
玩家 Bill 猜了 Cho（偶数）
给 Bill 奖励 1 分
玩家 Jill 猜了 Cho（偶数）
给 Jill 奖励 1 分

现在开始第 2 轮
庄主掷出了 5 和 2
结果：Han（奇数）
玩家 Bill 猜了 Han（奇数）
给 Bill 奖励 1 分
玩家 Jill 猜了 Han（奇数）
给 Jill 奖励 1 分

现在开始第 3 轮
庄主掷出了 4 和 2
结果：Cho（偶数）
玩家 Bill 猜了 Cho（偶数）
给 Bill 奖励 1 分
玩家 Jill 猜了 Cho（偶数）
给 Jill 奖励 1 分
----------------------
现在开始第 4 轮
庄主掷出了 3 和 2
结果：Han（奇数）
玩家 Bill 猜了 Han（奇数）
给 Bill 奖励 1 分
玩家 Jill 猜了 Cho（偶数）

现在开始第 5 轮
庄主掷出了 4 和 6
结果：Cho（偶数）
玩家 Bill 猜了 Han（奇数）
玩家 Jill 猜了 Han（奇数）

游戏结束。结果如下：
Bill: 4 分
Jill: 3 分
Bill 是大胜者！

## 14.9 关注面向对象编程：模拟骰和（Cho-Han）游戏

让我们来看代码。以下是主函数的摘要：`MAX_ROUNDS`——轮数：

- 第 15 到 17 行进行了以下声明：`rounds`（要运行的轮数）、`player1Name`——用于存储玩家 1 号的名字，`player2Name`——用于存储玩家 2 号的名字。
- 第 20 到 23 行提示用户输入玩家的名字。
- 第 26 行创建了 `Dealer` 类的实例来代表玩家 1。注意 `player1Name` 被作为 `Player` 类的参数传递给构造函数。
- 第 30 行创建了另一个 `Player` 类的实例来代表玩家 2。注意 `player2Name` 作为另一个参数传递给构造函数。
- 第 33 行开始的循环迭代五次，导致游戏五轮的模拟。循环执行了以下操作：
  - 第 40 行调用庄主掷骰子。
  - 第 43 行调用玩家 1 进行猜测（Cho 或 Han）。
  - 第 44 行调用玩家 2 进行猜测（Cho 或 Han）。
  - 第 47 行将庄主、`player1` 和 `player2` 对象传递给 `roundResults` 函数。该函数显示这一轮的结果。
- 第 51 行将 `player1` 和 `player2` 对象传递给 `displayGrandWinner` 函数，该函数显示游戏的大胜者。

显示轮结果的 `roundResults` 函数出现在第 59 到 71 行。以下是函数的摘要：

- 该函数接受庄主、`player1` 和 `player2` 对象的引用作为参数。
- 第 62 和 63 行的语句显示骰子的值。Cho 或 Han。
- 第 66 行调用庄主的 `getChoOrHan` 函数显示结果，Cho 或 Han。
- 第 69 行调用 `checkGuess` 函数，将 `player1` 和庄主对象作为参数。`checkGuess` 函数将玩家的猜测与庄主的结果（Cho 或 Han）进行比较，如果猜测正确，则给玩家奖励积分。
- 第 70 行调用 `checkGuess` 函数，将 `player2` 和庄主对象作为参数。

`checkGuess` 函数将玩家的猜测与庄主的结果进行比较，为正确猜测的玩家奖励，出现在第 77 到 99 行。以下是函数的摘要：

- 该函数接受一个 `Player` 和 `Dealer` 对象的引用作为参数。
- 第 79 行声明常量 `POINTS_TO_ADD`，将其设置为 1，即如果猜测正确，要给玩家余额增加的分数。
- 第 82 行将玩家的猜测赋值给字符串对象 `guess`。
- 第 85 行将庄主的结果（Cho 或 Han）赋值给字符串对象 `choHanResult`。
- 第 88 和 89 行的语句显示玩家的名字和猜测。
- 第 92 行的 `if` 语句将玩家的猜测与庄主的结果进行比较。如果它们匹配，显示游戏大胜者的 `displayWinner` 函数出现在第 105 到 133 行。

- 将 `player1` 和 `player2` 对象传递给 `displayGrandWinner` 函数，该函数显示游戏大胜者。

```cpp
{
  int x = 0;
  square(5);
  cout << x << endl;
  return 0;
}
```

在这段代码中，第 10 行语句调用了 `square` 函数，但它没有对返回的值进行任何处理。与上一个示例一样，值 25 被存储为一个临时值。但在这个示例中，该值在语句执行完成后就永久丢失了。

因此，在程序执行期间，内存中存储了两种类型的值：

- 生命周期超过创建它的语句的值，并且它们拥有名称，使得程序中的其他语句可以访问它们。在 C++ 中，这些值被称为 **lvalues**。
- 临时的值，并且在创建它的语句之外无法被访问。在 C++ 中，这些值被称为 **rvalues**。

> 提示：也许理解 lvalue 最简单的方法是：它是一个可以写在赋值运算符左侧的表达式。

## 右值引用 (Rvalue References)

在第 6 章中，你学习了引用变量是指另一个变量内存位置的变量。例如，查看以下代码片段：

```cpp
int x = 34;
int &ref = x;
```

在这段代码中，变量 `ref` 是一个引用变量。在声明中，引用通过在类型和变量标识符之间使用符号 `&` 来指示。在 C++ 11 及更高版本中，这种类型的引用被称为 **lvalue引用**，因为它只能引用 lvalues。

C++ 11 还引入了**右值引用**（rvalue reference）的概念，它是一种只能引用那些否则没有名称的临时对象的引用。右值引用的声明方式与 lvalue 引用类似，区别在于使用双符号 `&&`。下面的代码使用右值引用来打印 5 的平方：

```cpp
int &&r1ValRef = square(5);
cout << r1ValRef << endl;
```
