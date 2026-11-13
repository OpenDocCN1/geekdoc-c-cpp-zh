

## 第14.2节末尾的自测练习

- 12. 编写代码来声明一个生物体向量。在向量中放入10个新的生物体，初始大小为16盎司，生长速率为每周1盎司。随机抓取五个生物体，并将它们的生长速率改为每周2盎司。最后，计算所有生物体生长速率的总和，并打印结果。

- 13. 在上一个练习中，你开始有10个以每周1盎司的速度生长的生物体。五个随机生物体的生长速率被改为每周2盎司，因此你可能会认为所有生物体速率的总和应该是 5*1 + 5*2，即15。但是当我们运行程序时，总和只有14。为什么？

- 14. 设计并实现一个从animal类派生的新类。这个新类叫做carnivore，有一个新成员函数，原型如下所示：

```
void carnivore::chase(animal* prey, double chance);
```

当对某个食肉动物激活chase(prey, chance)时，该食肉动物会追逐猎物。实际捕获猎物的概率由参数chance给出（该参数应在0到1之间——例如0.75表示75%的概率）。如果猎物被捕获，这也将激活食肉动物的eat成员函数，并（遗憾的是）激活猎物的death成员函数。

注意：你可以使用rand函数（来自<cstdlib>）来确定动物是否被捕获，如下所示：

```
if (rand() / double(RAND_MAX) < chance)
{
    // Code for catching and eating the prey
}
```

## 14.3 虚成员函数和游戏类

本节演示虚成员函数，这是一种新型的成员函数，允许某些函数激活的方面被推迟到程序实际运行时。

### game类简介

为了使虚函数的解释更具体，我们将展示一个名为game的类示例，这将使我们更容易编写下棋、跳棋或奥赛等各种双人游戏的程序。我们考虑的游戏将让人类玩家与计算机对弈，由计算机做出（希望是）智能的走法。

game类的关键在于认识到，这些不同游戏的许多方面都可以以统一的方式处理。例如，每个游戏都需要一个在人类玩家和计算机之间来回进行的通用过程，并且每个游戏都需要一个从备选方案中选择计算机走法的合理过程。因此，我们的建议是拥有一个game类，它提供所有这些通用操作，并将作为许多派生类的基类，这些派生类用于玩各种双人游戏。

game类为其他游戏的实现提供了一个框架。例如，编写下棋程序的程序员可以实现一个派生的chess类，使用game作为基类。另一个编写奥赛程序的程序员，可以实现一个派生的othello类，也使用game作为其基类。

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_740_0.png)

我们提出的game类的定义如图14.12所示。

game类定义中包含大量信息，并使用了几种新技术。我们将简要解释定义的每个部分，然后我们将回过头来专注于必须理解的定义部分，以便编写派生类，例如chess、Othello，或者——正如我们将在示例中实际做的那样——一个用于玩名为Connect Four的游戏的派生类。

### 图14.12 game类的定义

```
class game
{
public:
// ENUM TYPE
enum { HUMAN, NEUTRAL, COMPUTER }; // Possible game outcomes

// CONSTRUCTOR and DESTRUCTOR
game() { move_number = 0; }
virtual ~game() { }

// PUBLIC MEMBER FUNCTIONS
// The play function should not be overridden. It plays one game, with the human player
// moving first and the computer second. The computer uses an alpha-beta look ahead
// algorithm to select its moves. The return value is the winner of the game (or
// NEUTRAL for a tie).
who play();
```

### （图14.12 续）

```
protected:
// OPTIONAL VIRTUAL FUNCTIONS (overriding these is optional)
virtual void display_message(const std::string& message) const;
virtual std::string get_user_move() const;
virtual who last_mover() const;
virtual int moves_completed() const;
virtual who next_mover() const;
virtual who opposite(who player) const;
virtual who winning() const;

// VIRTUAL FUNCTIONS THAT MUST BE OVERRIDDEN:
// The overriding function should call the original when it finishes.
// Have the next player make a specified move:
virtual void make_move(const std::string& move) { ++move_number; }

// Restart the game from the beginning:
virtual void restart() { move_number = 0; }

// PURE VIRTUAL FUNCTIONS (these must be provided for each derived class)
// Return a pointer to a copy of myself:
virtual game* clone() const = 0;

// Compute all the moves that the next player can make:
virtual void compute_moves(std::queue<std::string>& moves) const = 0;

// Display the status of the current game:
virtual void display_status() const = 0;

// Evaluate a board position (positive values are good for the player who just moved):
virtual int evaluate() const = 0;

// Return true if the current game is finished:
virtual bool is_game_over() const = 0;

// Return true if the given move is legal for the next player:
virtual bool is_legal(const std::string& move) const = 0;

private:
int move_number; // Number of moves made so far
// Other private items could go here, too.
};
```

### who类型

类以以下定义开始：

```
enum who { HUMAN, NEUTRAL, COMPUTER }; // Possible game outcomes
```

此定义定义了一个`enum`类型，你可能以前没有使用过。enum类型定义了一种简单的新数据类型，以及该类型变量可以赋予的值。在我们的示例中，新的enum类型称为`who`，类型为`who`的变量可以赋予三个名为`HUMAN`、`NEUTRAL`和`COMPUTER`的常量之一。我们将使用此类型的变量来跟踪谁赢得了游戏（平局使用`NEUTRAL`），或者轮到谁移动。

### 构造函数

game类有一个简单的构造函数，它将值零赋给其唯一的私有成员变量（`move_number`）。该变量跟踪在游戏进行期间已经进行了多少步。

### 公共play函数

game类有一个公共成员函数：

```
who play ();
```

激活此函数以进行一局游戏。例如，稍后我们将编写一个名为`connect4`的类，它从`game`类派生，并玩一种名为Connect Four的游戏。一个玩Connect Four游戏的简单`main`函数如下所示：

```
int main ()
{
    connect4 instance;
    connect4::who winner;
    winner = instance.play ();
    switch (winner)
    {
        case connect4::HUMAN: cout << "You win" << endl; break;
        case connect4::COMPUTER: cout << "I win" << endl; break;
        case connect4::NEUTRAL: cout << "A draw" << endl; break;
    }
    return EXIT_SUCCESS;
}
```

这玩一局Connect Four游戏。

该游戏是交互式的，允许用户在键盘上输入游戏走法（或者，正如我们将看到的，输入可以以其他方式到来）。`game`类的一个成员函数指导计算机的走法，搜索所有可能的走法，查看人类可能对这些走法做出的响应，查看对人类响应的可能响应，以此类推。

你可能正在思考指导计算机走法的细节。我们将在本节末尾讨论这一点，但目前，让我们假设某位明智而慷慨的程序员已经给我们提供了完整的game类，我们将使用它来实现Connect Four等游戏。game类的一个绝妙特性是，我们不需要知道play函数的工作细节，就可以编写我们的派生类。我们可以相信我们那位明智而慷慨的程序员正确地编写了play函数。这是编写良好的基类的一大好处：

> **编写良好的基类的好处**
> 
> 拥有一个编写良好的基类后，程序员可以编写派生类，而无需担心基类如何完成其工作。

因此，我们计划编写一个从game类派生的类。除其他外，我们的派生类将继承强大的play函数。我们无需立即理解play函数的细节，但我们确实需要了解game类定义的下一部分，它提供了一系列受保护的虚函数。

### 受保护成员

game类定义的下一部分如下开始：

```
protected:
// OPTIONAL VIRTUAL FUNCTIONS (overriding these is optional)
virtual void display_message(const std::string& message) const;
```

关键字`protected`表示，随后的项目将是一种新型成员，介于`public`和`private`之间。具体来说，受保护的成员可以被派生类使用（和覆盖），但除了在派生类内部之外，任何受保护的成员都是私有的。它不能在其他地方使用。

### 虚成员函数

game类中的第一个受保护成员函数是`display_message`。game类以一种简单的方式实现此函数，即将消息（作为参数）打印到标准输出（`cout`）。这工作正常，每当`play`函数需要打印消息时，它都通过激活`display_message`来完成。事实上，我们的`play`函数开头如下所示：

```
game::who game::play()
{
    display_message("Welcome!");
    ...
```

