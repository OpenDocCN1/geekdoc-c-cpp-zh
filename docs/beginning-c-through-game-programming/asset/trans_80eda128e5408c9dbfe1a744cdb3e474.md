

```
const int TOTAL_ROWS = 8;

// if any winning row has three values that are the same (and not EMPTY),
// then we have a winner
for(int row = 0; row < TOTAL_ROWS; ++row)
{
    if ( (board[WINNING_ROWS[row][0]] != EMPTY) &&
        (board[WINNING_ROWS[row][0]] == board[WINNING_ROWS[row][1]]) &&
        (board[WINNING_ROWS[row][1]] == board[WINNING_ROWS[row][2]]) )
    {
        return board[WINNING_ROWS[row][0]];
    }
}
```

我遍历每位玩家可能获胜的所有方式，以判断是否有任何一方已经连成三子。if 语句检查所涉及的三个方格是否都包含相同的值，并且不为 EMPTY。如果是，则说明该行中有三个 X 或三个 O，有一方获胜。然后函数返回该获胜行第一个位置上的棋子。

如果双方都未获胜，我再检查是否为平局。

```
// since nobody has won, check for a tie (no empty squares left)
if (count(board.begin(), board.end(), EMPTY) == 0)
    return TIE;
```

如果棋盘上没有空方格，那么游戏就是平局。我使用 STL 的 count() 算法来统计 board 中 EMPTY 元素的数量，该算法会统计某个给定值在容器元素中出现的次数。如果数量等于 0，函数返回 TIE。

最后，如果双方都未获胜，且比赛不是平局，那就说明还没有赢家。因此，函数返回 NO_ONE。

```
// since nobody has won and it isn't a tie, the game ain't over
return NO_ONE;
}
```

## isLegal() 函数

该函数接收一个棋盘和一步棋。如果这一步在棋盘上是合法的，则返回 true；否则返回 false。合法走法由空方格的编号表示。

```
inline bool isLegal(int move, const vector<char>& board)
{
    return (board[move] == EMPTY);
}
```

再次注意，表示棋盘的 vector 通过常量引用传递。这意味着 vector 被高效地传递，不会被复制。这也意味着 vector 受到保护，不会被修改。

你可以看到，我将 isLegal() 声明为内联函数。现代编译器已经非常擅长自行优化；不过，由于这个函数只有一行，它是内联的合适候选。

## humanMove() 函数

这个函数接收棋盘和人类的棋子。它返回玩家想要移动的方格编号。函数会一直询问玩家想要落子的方格编号，直到得到合法的走法为止。然后函数返回该走法。

```
int humanMove(const vector<char>& board, char human)
{
    int move = askNumber("Where will you move?", (board.size() - 1));
    while (!isLegal(move, board))
    {
        cout << "\nThat square is already occupied, foolish human.\n";
        move = askNumber("Where will you move?", (board.size() - 1));
    }
    cout << "Fine...\n";
    
    return move;
}
```

再次注意，表示棋盘的 vector 通过常量引用传递。这意味着 vector 被高效地传递，不会被复制。这也意味着 vector 受到保护，不会被修改。

## computerMove() 函数

这个函数接收棋盘和计算机的棋子。它返回计算机的走法。首先要注意的是，我没有通过引用传递棋盘。

```
int computerMove(vector<char> board, char computer)
```

相反，我选择按值传递，尽管这不如按引用传递高效。我按值传递，是因为我需要在一个棋盘副本上操作和修改，在空方格中放置棋子，以确定计算机的最佳走法。通过使用副本，我保证表示棋盘的原始 vector 是安全的。

现在进入函数的核心部分。那么，我如何编写一点 AI，让计算机能够进行像样的对抗呢？好吧，我提出了一个简单的三步策略来选择走法。

- 1. 如果计算机这一步能赢，就走这一步。
- 2. 否则，如果人类下一步能赢，就堵住他。
- 3. 否则，选择剩余的最佳空方格。最佳方格是中心。次佳方格是四个角，然后是其余方格。

函数的下一部分实现了第 1 步。

```
{
unsigned int move = 0;
bool found = false;

//if computer can win on next move, that’s the move to make
while (!found && move < board.size())
{
    if (isLegal(move, board))
    {
        board[move] = computer;
        found = winner(board) == computer;
        board[move] = EMPTY;
    }

    if (!found)
    {
        ++move;
    }
}
```

我开始遍历所有可能的走法，即 0 到 8。对于每一步，我测试该走法是否合法。如果合法，我在相应的方格中放置计算机的棋子，并检查这一步是否能让计算机获胜。然后，我把该方格重新置空，以撤销这一步。如果这一步没有让计算机获胜，我就继续检查下一个空方格。然而，如果这一步确实让计算机获胜了，那么循环就会结束——我已经找到了希望计算机执行的走法（即方格编号 move）来赢下游戏。

接下来，我检查是否需要进入我的 AI 策略的第 2 步。如果还没有找到走法（found 为 false），那么我会检查人类是否能在下一步获胜。

```
//otherwise, if human can win on next move, that's the move to make
if (!found)
{
    move = 0;
    char human = opponent(computer);

    while (!found && move < board.size())
    {
        if (isLegal(move, board))
        {
            board[move] = human;
            found = winner(board) == human;
            board[move] = EMPTY;
        }

        if (!found)
        {
            ++move;
        }
    }
}
```

我开始遍历所有可能的走法，即 0 到 8。对于每一步，我测试该走法是否合法。如果合法，我在相应的方格中放置人类的棋子，并检查这一步是否能让人类获胜。然后，我把该方格重新置空，以撤销这一步。如果这一步没有让人类获胜，我就继续检查下一个空方格。然而，如果这一步确实让人类获胜了，那么循环就会结束——我已经找到了希望计算机执行的走法（即方格编号 move），以阻止人类在下一步获胜。

接下来，我检查是否需要进入我的 AI 策略的第 3 步。如果还没有找到走法（found 为 false），那么我会按照合意程度从高到低查看最佳走法列表，并选择第一个合法走法。

```
//otherwise, moving to the best open square is the move to make
if (!found)
{
    move = 0;
    unsigned int i = 0;

    const int BEST_MOVES[] = {4, 0, 2, 6, 8, 1, 3, 5, 7};
    //pick best open square
    while (!found && i < board.size())
    {
        move = BEST_MOVES[i];
        if (isLegal(move, board))
        {
            found = true;
        }

        ++i;
    }
}
```

在函数的这个位置，我已经找到了希望计算机执行的走法——无论是能让计算机获胜的走法、能阻挡人类获胜的走法，还是仅仅是当前最佳空方格的走法。所以，我让计算机宣布走法，并返回相应的方格编号。

```
cout << "I shall take square number " << move << endl;
return move;
}
```

## 现实世界

井字棋游戏只考虑下一步可能的走法。而下像国际象棋这类严肃策略游戏的程序，会深入得多地审视每一步棋的后果，并考虑多个层次的走法与应对。事实上，优秀的计算机国际象棋程序在走出一步棋之前，确实能分析数百万个棋盘局面。

## announceWinner() 函数

这个函数接收游戏胜者、计算机的棋子和人类的棋子。函数宣告胜者，或者宣布平局。

```cpp
void announceWinner(char winner, char computer, char human)
{
    if (winner == computer)
    {
        cout << winner << "'s won!\n";
        cout << "As I predicted, human, I am triumphant once more -- proof\n";
        cout << "that computers are superior to humans in all regards.\n";
    }
    else if (winner == human)
    {
        cout << winner << "'s won!\n";
        cout << "No, no! It cannot be! Somehow you tricked me, human.\n";
        cout << "But never again! I, the computer, so swear it!\n";
    }
    else
    {
        cout << "It's a tie.\n";
        cout << "You were most lucky, human, and somehow managed to tie me.\n";
        cout << "Celebrate... for this is the best you will ever achieve.\n";
    }
}
```

## 本章小结

在本章中，你应该已经了解了以下概念：

- 引用是一种别名；它是变量的另一个名字。
- 你使用 &（即引用运算符）创建引用。
- 引用在定义时就必须被初始化。
- 引用不能被更改以指向另一个变量。
- 你对引用所做的一切，实际上都是对引用所引用的变量所做的。
- 当你使用引用为某个变量赋值时，你创建的是被引用值的一个新副本。

