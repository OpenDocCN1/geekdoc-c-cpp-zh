

## gameboard

## connect4_board

```
+ print_board())
+ check_winner() : int
+ take_turn(m : gamemove+)
```

```
- rows : int
- columns : int
- board : vector<vector<int>>
+ connect4_board()
+ connect4_board(r: int, c: int)
+ print_board()
+ check_winner() : int
+ take_turn(m : gamemove+)
+ take_turn(m : connect4_move+)
- check_vertical_winner(player : int)
- check_horizontal_winner(player : int)
- check_increasing_diagonal_winner(player : int)
- check_decreasing_diagonal_winner(player : int)
- check_full_board()
```

在 reversi_board 类中，只需要默认构造函数就足够了，因为棋盘大小将是 8×8。同样，你需要用一个向量组成的向量来存储棋盘信息。并且你需要对父类中声明的虚函数提供具体的实现。

到目前为止，你基本上已经设计好了类集合。你可能需要——事实上最终会管理比这些更多的函数。有些函数会很大以至于在一个函数中完成所有工作，你希望使用自顶向下的设计原则将这些较大的任务分解成更小的任务。

对于 connect4_board，你需要在各个方向检查获胜者，因此你会包含用于检查垂直、水平以及两个对角线方向获胜者的函数。你还必须检查棋盘是否完全填满以及某一列是否已满。

所有这些都与你在之前讲座中做的过程式、自顶向下设计相似，但现在这些是 connect4_board 类的成员函数。

## reversi_board

```
- board : vector<vector<int>>
+ reversi_board()
+ print_board()
+ check_winner() : int
+ take_turn(m : gamemove+)
+ take_turn(m : reversi_move+)
- mark_up(r: int, c: int)
- mark_down(r: int, c: int)
- mark_right(r: int, c: int)
- mark_left(r: int, c: int)
- mark_diagl(r: int, c: int)
- mark_diagr(r: int, c: int)
- mark_diagdr(r: int, c: int)
- mark_diagdl(r: int, c: int)
```

同样，对于 reversi_board，你会想要一些额外的函数来帮助你更改棋盘。当你放置一个棋子时，你可能需要在任意 8 个方向翻转棋子：上、下、左、右，以及全部 4 个对角线。你将创建 8 个额外的函数来帮助在放置棋子后按 8 个方向标记棋盘。

## gameboard

```
+ print_board()
+ check_winner() : int
+ take_turn(m : gamemove+)
```

现实中，当你设计一组类时，你可能在开始时并不知道你需要的所有函数。这是可以的。你可能需要在构建过程中更改你的类设计，但希望你能把设计的主要部分放在合适的位置。

## CODING YOUR DESIGN

设计完成后，你现在想要开始编码所有内容。

一个好的开始是实现你的 game 类，因为它是这些类中最基础的。

首先将你在 UML 中得出的类设计与代码中的那些步骤进行比较。成员变量将声明为一个 gameboard 指针 board；一个 gamove 指针 turn；一个整数 playerturn；以及一个整数 numturms。

```
private:
gameboard* board;
gamove* turn;
int playerturn;
int numturms;
```

设计中的下一件事是该类的成员函数，其中包括你的构造函数，它将以 gameboard 和一个 gamove 作为输入。这 2 个类是抽象的并且没有具体的值，所以它们必须通过引用传递。你使用 gameboard b 来获取对 gameboard 的引用以及 gamove m 来获取对 gamove 的引用。在构造函数内部，你只是获取对 gameboard 的引用——在你的成员变量中。你对 gameboard 做同样的操作，将其分配给 turn 成员变量。

```
game(gameboard& b, gamove& m) {
board = &b;
turn = &m;
}
```

> 完整的代码有数百行，因此这里只突出了程序的一些关键部分。

> 完整程序可在 www.TheGreatCourses.com/CPlusPlus 下载。

设计中的下一个函数是 check_winner 函数，它是受保护的。你在 gameboard 类中实现 check_winner，因为 gameboard 本身决定谁是赢家。因此，你的代码只是调用你存储的 gameboard 中的 check_winner 函数。

```
int check_winner() {
return board->check_winner();
}
```

你接下来要查看的例程是 take_turn 例程，它应该在游戏中进行一次回合。这意味着你希望将 gameboard 打印到屏幕上，因此你调用板的 print_board 成员函数。你想要获取下一个玩家想要的移动。playerturn，应该说明轮到谁，所以你将它作为参数传递给你的 turn 成员变量的 ask_move 函数。这将调用 turn 指向的任何 gamove 中的 ask_move。最后，你需要根据该移动更新棋盘，因此你调用棋盘上的 take_turn，将你刚刚得到的移动传递给 gameboard。

```
void take_turn() {
board->print_board();
turn->ask_move(playturn);
board->take_turn();
}
```

你的 declare_winner 函数有几行代码，它实际上只是检查各种可能的游戏结束情况。你根据棋盘状态确定赢家，因此你只需在棋盘本身上调用 check_winner 来找出赢家是谁并打印最终棋盘和关于赢家的消息。

take_turn 你刚刚定义。回合结束后，你切换玩家轮到谁并增加回合数。当循环结束时——即当 check_winner 函数说游戏结束时——然后你调用你的 declare_winner 例程来打印结果。

正如 UML 所示，你的基类只有一个受保护的成员变量，即整数 player，以及一个纯虚函数 ask_move。

ask_move 函数接收一个整数参数并且不返回任何内容；在这里，因为它是纯虚函数，你在末尾加上 =0。

```
void declare_winner() {
int result = check_winner();
board->print_board();
cout << "The game ended after "
<< nummers << " turns." << endl;
if (result == 1) {
cout << "Player 1 wins!"\n}
else if (result == 2) {
cout << "Player 2 wins!"\n}
else if (result == 3) {
cout << "The game has ended
a tie." << endl;
}
else if (result == 0) {
cout << "The game ended before
it was completed." << endl;
}
```

```
void start_game() {
nummers = 0;
player = 1;
while (check_winner() == 0) {
take_turn();
if (playern == 1) {
player = 2;
} else {
player = 1;
}
nummers++;
declare_winner();
}
```

```
class gamemove {
protected:
int player;
public:
virtual void ask_move(int) = 0;
}
```

注意 connect_4 类是从 gamemove 派生的。有一个私有成员变量：一个整数，表示你打算放置棋子的列。

在 game 类之后，你接下来定义了抽象基类 gamemove 及其派生类 connect_4 和 reversi_move。

你的函数是 start_game。这个公共函数可能是 game 类中的主函数。它是实际使游戏运行的函数。在此函数中，你将成员变量初始化为 0。你进入一个循环，只要 gameboard 类中的 check_winner 函数报告游戏尚未结束就继续。在循环内你进行一次回合，调用

| connect_move |
| column : int |
| ask_move(nextplayer : int) |
| c ( ) : int |
| p ( ) : int |

| gamemove |
| player : int |
| ask_move(nextplayer : int) |

connect4_move 提供了 ask_move 函数的定义，它是 gamemove 的虚成员。此函数将玩家编号作为参数并使用它来设置从 gamemove 类继承的受保护成员变量 player。

实现 reversi_move 类是一个类似的过程。这里有一些小的差异，突出了 2 个游戏之间的独特差异：Reversi 移动需要行和列，因此存储了 2 个变量并从用户处询问 2 块信息。

但很明显 connect4_move 和 reversi_move 类密切相关，它们都实现了从 gamemove 所需的必要函数。

它从用户读取列号，将其存储在 column 变量中并调整为从 0 而不是 1 开始的编号。

你剩余的类实现是 gamepad 类。

最后，你有访问函数 c 和 p，它们返回移动的列和做出移动的玩家。

首先，你的 UML 图给出了你的类的设计。你的 gamepad 类需要有 3 个成员函数。你在 game 类实现中调用所有这些。实际的类实现了这些函数，以及为该游戏提供构造函数和成员变量所需的。

```
class connect4_move : public
gamemove
private:
int column;
```

```
class reversi_move : public
gamemove;
private:
int row;
int column;
```

```
void ask_move(int nextplayer) {
player = nextplayer;
cout << "Player" << nextplayer
 << "", which ROW do you do
want to place your piece in?";
 >> row;
cout << "Which COLUMN do you
want to place your piece in?";
cin column;
row--; // Adjust to make
the numbers start from 0
```

```
void ask_move(int nextplayer) {
player = nextplayer;
cout << "Player" << nextplayer
 << "", which column do you do
want to place your piece in?";
cin column;
column--; // Adjust to make
first column be 0
```

```
int c() {
return column;
}
int p() {
return player;
}
```

```
int r() {
return row;
}
int c() {
return column;
}
int p() {
return player;
}
```

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_253_0.png)

| rows | int |
| columns | int |
| board | vector<int> |

| connect4_move() |
| connect4_move(r: int, c: int) |
| print_board() |
| check_winner() : int |
| take_turn(m: gamemove) |

| print_board() |
| check_winner() : int |
| take_turn(m: gamemove) |

| reversi_board() |
| board | vector<int> |
| reversi_board() |
| check_winner() : int |
| take_turn(m: gamemove) |

Lecture 21 | Using Classes to Build a Game Engine in C++

248

