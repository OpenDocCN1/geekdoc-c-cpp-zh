
算术运算（此处为加法）与赋值相结合。该运算符是下面这句话的简写：“将右侧的值加到左侧的值上，并把结果赋回左侧。”

对于你见过的所有算术运算符，都有对应的组合赋值运算符版本。要查看列表，请参阅表 1.2。

表 1.2 组合赋值运算符

| 运算符 | 示例 | 等价于 |
|---|---|---|
| += | x += 5; | x = x + 5; |
| -= | x -= 5; | x = x - 5; |
| *= | x *= 5; | x = x * 5; |
| /= | x /= 5; | x = x / 5; |
| %= | x %= 5; | x = x % 5; |

## 使用自增和自减运算符

接下来，我使用自增运算符（++），它使变量的值增加 1。我使用该运算符将 lives 的值增加两次。首先在下面一行中使用它：

```
++lives;
```

然后在下面一行中再次使用它：

```
lives++;
```

每一行产生的净效果相同；它将 lives 从 3 增加到 4。

如你所见，你可以将运算符放在要递增的变量的前面或后面。当你把运算符放在变量前面时，该运算符称为前缀自增运算符；当你把它放在变量后面时，则称为后缀自增运算符。

此时，你可能会认为后缀版本和前缀版本没有区别，但那就错了。在只递增单个变量的情况下（正如你刚才看到的），两个运算符产生相同的最终结果。但在更复杂的表达式中，结果可能不同。

为了演示这一重要区别，我执行一个适合游戏关卡结束时的计算。我根据数量计算奖励

![](img/c7e8651578bccd573227f684823b8754_51_0.png)

图 1.7
一种可视化 *unsigned int* 变量从最大值“回绕”到最小值的方式。

### 提示

务必选择一个范围足够大的整数类型，以适应其预期用途。

## 使用常量

*常量*是一个你命名后不可更改的值。当你有一个在程序中频繁出现的不变值时，常量非常有用。例如，如果你正在编写一个太空射击游戏，每个从天空中击落的外星人值 150 分，你可以定义一个名为 `ALIEN_POINTS` 的常量，等于 150。然后，任何时候你需要一个外星人的分值，都可以使用 `ALIEN_POINTS` 而不是字面量 150。

常量提供两个重要好处。首先，它们使程序更清晰。一旦看到 `ALIEN_POINTS`，你就知道它是什么意思。如果你查看一些代码并看到 150，你可能不知道这个值代表什么。其次，常量使修改变得容易。例如，假设你对游戏进行了一些试玩测试，并决定每个外星人应该值 250 分。使用常量，你只需更改程序中 `ALIEN_POINTS` 的初始化。如果没有常量，你将不得不找出每一个出现 150 的地方并改为 250。

### 介绍 Game Stats 3.0 程序

Game Stats 3.0 程序使用常量来表示值。首先程序计算玩家的分数，然后计算策略游戏中一个单位的升级成本。图 1.8 显示了结果。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载此程序的代码。程序位于 Chapter 1 文件夹中；文件名是 `game_stats3.cpp`。

![](img/c7e8651578bccd573227f684823b8754_52_0.png)

图 1.8

每项计算都涉及一个常量，使幕后的代码更清晰。

```
// Game Stats 3.0
// Demonstrates constants

#include <iostream>
using namespace std;

int main()
{
    const int ALIEN_POINTS = 150;
    int aliensKilled = 10;
    int score = aliensKilled * ALIEN_POINTS;
    cout << "score: " << score << endl;

    enum difficulty {NOVICE, EASY, NORMAL, HARD, UNBEATABLE};
    difficulty myDifficulty = EASY;

    enum shipCost {FIGHTER_COST = 25, BOMBER_COST, CRUISER_COST = 50};
    shipCost myShipCost = BOMBER_COST;
    cout << "\nTo upgrade my ship to a Cruiser will cost "
         << (CRUISER_COST - myShipCost) << " Resource Points.\n";

    return 0;
}
```

### 使用常量

我定义一个常量 `ALIEN_POINTS` 来表示一个外星人的分值。

```
const int ALIEN_POINTS = 150;
```

我只是使用关键字 `const` 来修改定义。现在我可以像使用任何整数字面量一样使用 `ALIEN_POINTS`。另外，注意我为常量选择的名字全部大写。这只是一种约定，但很常见。全大写的标识符告诉程序员它表示一个常量值。

接下来我将该常量用在下面一行：

```
int score = aliensKilled * ALIEN_POINTS;
```

我通过将击杀的外星人数乘以每个外星人的分值来计算玩家的分数。在这里使用常量使这行代码非常清晰。

### 陷阱

> 你不能给常量赋新值。如果你尝试，会产生编译错误。

### 使用枚举

枚举是一组无符号整型常量，称为枚举器。通常枚举器是相关的并具有特定顺序。这里是一个枚举示例：

```
enum difficulty {NOVICE, EASY, NORMAL, HARD, UNBEATABLE};
```

这定义了一个名为 difficulty 的枚举。默认情况下，枚举器的值从零开始，每次加一。所以 NOVICE 是 0，EASY 是 1，NORMAL 是 2，HARD 是 3，UNBEATABLE 是 4。要定义自己的枚举，使用关键字 enum，后跟标识符，再后跟花括号中的枚举器列表。

接下来我创建一个这种新枚举类型的变量。

```
difficulty myDifficulty = EASY;
```

变量 myDifficulty 被设置为 EASY（等于 1）。myDifficulty 的类型是 difficulty，所以它只能保存枚举中定义的值之一。这意味着 myDifficulty 只能被赋值为 NOVICE、EASY、NORMAL、HARD、UNBEATABLE、0、1、2、3 或 4。

接下来我定义另一个枚举。

```
enum shipCost {FIGHTER_COST = 25, BOMBER_COST, CRUISER_COST = 50};
```

这行代码定义了枚举 shipCost，它表示策略游戏中三种飞船的资源点成本。在其中，我向某些枚举器赋予了特定的整数值。这些数字代表每艘飞船的资源点值。如果你愿意，可以给枚举器赋值。任何未被赋值的枚举器，其值等于前一个枚举器的值加一。因为我没有给 BOMBER_COST 赋值，所以它被初始化为 26。

接下来我定义这种新枚举类型的一个变量。

```
shipCost myShipCost = BOMBER_COST;
```

然后我演示如何在算术计算中使用枚举器。

```
(CRUISER_COST - myShipCost)
```

这段代码计算将 Bomber 升级为 Cruiser 的成本。计算等同于 50 - 26，结果为 24。

## 介绍 Lost Fortune

本章的最后一个项目 Lost Fortune 是一个个性化冒险游戏，玩家输入几条信息，计算机使用这些信息来增强一个基本的冒险故事。图 1.9 显示了一个示例运行。

我不会一次性展示所有代码，而是一节一节地介绍。你可以从 Course Technology 网站（www.courseptr.com/downloads）下载此程序的代码。程序位于 Chapter 1 文件夹中；文件名是 lost_fortune.cpp。

### 设置程序

首先我创建一些初始注释，引入两个必要的文件，并编写几条 using 指令。

```
// Lost Fortune
// A personalized adventure

#include <iostream>
#include <string>

using std::cout;
using std::cin;
using std::endl;
using std::string;
```

![](img/c7e8651578bccd573227f684823b8754_55_0.png)

图 1.9
故事融入了玩家提供的细节。

我引入了标准库中的 string 文件，这样我就可以使用字符串对象通过变量来访问字符串。字符串对象还有很多内容，但我先卖个关子。你将在第 3 章“for 循环、字符串和数组：Word Jumble”中了解更多。

另外，我使用 using 指令来明确列出我计划访问的 std 命名空间中的对象。这样，你可以清楚地看到 string 位于命名空间 std 中。

### 获取玩家信息

接下来我从玩家那里获取一些信息。

```
int main()
{
    const int GOLD_PIECES = 900;
    int adventurers, killed, survivors;
    string leader;
```
