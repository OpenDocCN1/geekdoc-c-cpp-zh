

对于面向对象的设计，你首先应该考虑的是关注的对象是什么。从那里，你可以弄清楚需要哪些类来表示这些对象。

从非常一般的意义上说，你可能需要
- 一种通用的游戏类来跟踪它是谁的等等；
- 一个游戏类来保存棋盘的当前状态；以及
- 一种描述移动的方式，其中所有游戏共有的一个是 2 名玩家轮流进行。

这些都是抽象的，所以它们很可能会成为抽象类。你也需要这些类的具体版本：Connect 4 的特定类以及 Connect 4 和 Reversi 的特定移动。这些听起来像是子类。

一旦你考虑了类，你就可以开始寻找层次结构。在这种情况下，有几个明显的关联。抽象的 gameboard 将是具体 Connect 4 和 Reversi 游戏的父类。同样，抽象的 gamemove 应该是 Connect 4 和 Reversi 移动的父类。

一旦你对层次结构有了大致的想法，你需要考虑每个类应该具有的确切成员变量和函数，以及哪些应该是 public、protected 和 private。对于你的抽象类，你需要考虑虚函数。

## Lecture 21 | Using Classes to Build a Game Engine in C++

为了跟踪你正在做的事情，你可以使用统一建模语言（UML），这是一种由面向对象程序员为软件行业创建蓝图而开发的符号系统。

在 UML 中，当你描述一个类时，你使用一个矩形，顶部是一个框中的类名，然后是另外 2 个框：一个给出成员变量，即属性，以及底部的框给出成员函数，也称为操作的方法。

| Class name |
|---|---n| VARIABLES: | attributes methods |
| FUNCTIONS: | operations |

用于指定类元素的常用缩写是 public (+)、private (-) 或 protected (#)。

斜体用于抽象类和虚函数。

在开始时思考游戏类。总体而言，一个游戏需要有一个 gameboard，这也是另一个类，用来跟踪棋盘的当前状态，称为 board。

gameboard 将是一个抽象类，这意味着你必须有具体的 gameboard 类，例如 Connect 4 或 Reversi 棋盘。

为了在 game class 中存储一个抽象的 gameboard，你将使用指向 gameboard 的指针。

> 请记住，即使对象是子类型，也可以有一个指向父类型的指针。

gameboard 不是你希望游戏内部的东西直接访问的东西；你希望确保只进行有效的移动，玩家不会连续进行两次移动等等。因为你希望修改程序运行游戏时可以采取的任何操作，这应该是 game class 的私有变量——只有游戏可以直接访问，其他人（无论是玩家还是计算机）只能通过 game classes 访问。

在 UML 中，你将在指定变量的框中写 board : gameboard*。注释说明它是一个私有成员变量。board 是变量的名称，gameboard* 表示变量将是一个指向 gameboard 的指针。

你还需要考虑 game class 需要提供哪些函数。

你可能希望有用于进行回合或宣布获胜者的函数——这将是 protected。这些都将是不带参数且不返回任何内容的函数，所以你会写 # take_turn () 和 # declare_winner ()。

你可以使用你的 UML 图来组织这一点。你希望类提供的函数将进入最后一个框。对于每一个，你会考虑想要给它什么名称，以及它接受什么参数类型和返回什么。最后，你会考虑函数应该是 public、私有还是 protected。

同样，你需要在游戏中进行移动。像 gameboard 一样，gamemove 是一个抽象类。因此，你将需要一个 gamove*，一个名为 turn 的指针来跟踪移动。

最后，你希望有一个公共函数来启动游戏并在游戏结束前保持运行。你将调用它 start_turn () 和 start_game ()。

你需要跟踪下一个移动的玩家。所以，你将有一个名为 playerturn 的私有成员，它是一个整数。也许你还想跟踪游戏中已经发生的回合数。更复杂的 game class 可能会保留其他信息。

你需要一个构造函数，它将接受 2 个参数：一个用于 gameboard，一个用于 gamemove。构造函数必须是 public。在你的 UML 中，你将写 *，表示它是构造函数；然后在括号中写 2 个参数（board，其类型为 gameboard*，以及 turn，其类型为 gamemove）。

| Game |
| board : gameboard*
| turn : gamove*
| playerturn : int
| numturns : int |
| + (board : gameboard, turn : gamemove)
| # check_winner () : int
| # take_turn ()
| # declare_winner ()
| + start_game () |

请注意，对于每个 UML 条目，你将有一行代码。UML 本身不是代码，而且术语的顺序不同。例如：

检查获胜者的函数不会接受任何参数，并且它将返回一个整数，表示玩家是否获胜，或者平局。这是你希望从 game class 调用而不是在类外部调用的函数，所以你将使其受保护。使用 UML 记法，你会写 # check_winner () : int。

```
board : gameboard* in becomes
gameboard* : board; in code
```

```
turn : gamove* in becomes
gamemove* : turn; in code
```

在,, 你是从人类显而易见的东西开始的 board、turn、playerturn、numturn 等。但在 C++ 中，你是从类型开始的——对计算机更重要信息。

让我们再看另一个类，gamemove 类，它将是一个抽象类。类与玩家相关联，所以你的 gamemove 将有一个成员变量 Player，你将使其成为 protected 变量，以便从它继承的所有类都可以访问此变量。它还将有一个虚函数 ask_move，必须要求玩家进行移动。它将接受一个整数参数：轮到谁。因为这是虚函数，UML 惯例是用斜体写它。

每个移动都有一点不同。connect4_move 需要存储一列——棋子将被放入其中。aversi_move 需要存储行和列。

每个派生类也需要提供 ask_move 函数的具体实现。此外，你需要访问函数，以便其他类可以找到移动的位置以及哪个玩家进行了移动。你将使用 r 表示列，p 表示玩家来提供此信息。

同样，你需要定义 gameboard 类及其派生类 connect4_board 和 reversi_board。gameboard 将是一个抽象类，它需要有几个公共的虚函数。它应该能够打印游戏板，所以你将声明 print_board 函数。它应该能够检查移动，返回一个整数表示谁获胜或平局。它应该能够在收到适当类型的移动时进行移动。所有这些函数都将根据特定游戏而变化，因此抽象 gameboard 不能实现任何这些。

在 gameboard 类中声明的虚函数。你还需要存储有关棋盘的信息。你希望在 gameboard 中存储行数和列数，因为你将使用向量向量来存储棋盘每个点上的信息。

最后，你还将有几个构造函数：一个用于默认大小的 Connect 4 棋盘，一个用于你指定行数和列数的棋盘。

你还有 2 个派生类，connect4_move 和 reversi_move。它们继承自 gamemove 类。继承是通过使用带有未填充箭头的箭头来表示的。

```
connect4_move
  - column : int
  + ask_move(nextplayer) : int
  + c () : int
  + p () : int
```

在 connect4_board 类中，你需要每个的

```
connect4_board
  - rows : int
  - columns : int
  - board : vector<vector<int>>
  + connect4_board()
  + connect4_board(int r, int c)
  + print_board() : int
  + winner() : int
  + take_turn(m : gamemove*)
```

```
gamemove
  # player : int
  + ask_move(nextplayer) : int
```

```
gameboard
  + print_board() : int
  + winner() : int
  + take_turn(m : gamemove*)
```

```
reversi_board
  - board : vector<vector<int>>
  + reversi_board()
  + print_board() : int
  + winner() : int
  + take_turn(m : gamemove*)
```

## Lecture 21 | Using Classes to Build a Game Engine in C++

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_249_0.png)

