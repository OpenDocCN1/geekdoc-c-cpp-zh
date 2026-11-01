

## 表 6.1 井字棋函数

| 函数 | 描述 |
|---|---|
| void instructions() | 显示游戏说明。 |
| char askYesNo(string question) | 询问一个是或否的问题。接收一个问题。返回 'y' 或 'n'。 |
| int askNumber(string question, int high, int low = 0) | 询问一个在指定范围内的数字。接收一个问题、一个最低数字和一个最高数字。返回从 low 到 high 范围内的一个数字。 |
| char humanPiece() | 确定人类玩家的棋子。返回 'X' 或 'O'。 |
| char opponent(char piece) | 根据给定的棋子计算出对手的棋子。接收 'X' 或 'O'。返回 'X' 或 'O'。 |
| void displayBoard(const vector<char>& board) | 在屏幕上显示棋盘。接收一个棋盘。 |
| char winner(const vector<char>& board) | 确定游戏赢家。接收一个棋盘。返回 'X'、'O'、'T'（表示平局）或 'N'（表示尚无赢家）。 |
| bool isLegal(const vector<char>& board, int move) | 判断一步棋是否合法。接收一个棋盘和一步棋。返回 true 或 false。 |
| int humanMove(const vector<char>& board, char human) | 获取人类玩家的走法。接收一个棋盘和人类玩家的棋子。返回人类玩家的走法。 |
| int computerMove(vector<char> board, char computer) | 计算计算机的走法。接收一个棋盘和计算机的棋子。返回计算机的走法。 |
| void announceWinner(char winner, char computer, char human) | 祝贺赢家或宣布平局。接收获胜方、计算机的棋子和人类玩家的棋子。 |

```cpp
// global constants
const char X = 'X';
const char O = 'O';
const char EMPTY = ' ';
const char TIE = 'T';
const char NO_ONE = 'N';

// function prototypes
void instructions();
char askYesNo(string question);
int askNumber(string question, int high, int low = 0);
char humanPiece();
char opponent(char piece);
void displayBoard(const vector<char>& board);
char winner(const vector<char>& board);
bool isLegal(const vector<char>& board, int move);
int humanMove(const vector<char>& board, char human);
int computerMove(vector<char> board, char computer);
void announceWinner(char winner, char computer, char human);
```

在全局常量部分，X 是字符 'X' 的简写，它是游戏中两种棋子之一。O 代表字符 'O'，是游戏中的另一种棋子。EMPTY 也是一个字符，代表棋盘上的空方格。它是一个空格，因为当它显示出来时，看起来就像一个空方格。TIE 是一个代表平局的字符。而 NO_ONE 是一个用于表示游戏双方中任何一方的字符，我用它来表示还没有人获胜。

## main() 函数

如你所见，main() 函数几乎完全就是我之前创建的伪代码。

```cpp
// main function
int main()
{
    int move;
    const int NUM_SQUARES = 9;
    vector<char> board(NUM_SQUARES, EMPTY);

    instructions();
    char human = humanPiece();
    char computer = opponent(human);
    char turn = X;
    displayBoard(board);

    while (winner(board) == NO_ONE)
    {
        if (turn == human)
        {
            move = humanMove(board, human);
            board[move] = human;
        }
        else
        {
            move = computerMove(board, computer);
            board[move] = computer;
        }
        displayBoard(board);
        turn = opponent(turn);
    }

    announceWinner(winner(board), computer, human);

    return 0;
}
```

## instructions() 函数

这个函数用于显示游戏说明，并让计算机对手带点挑衅的口气。

```cpp
void instructions()
{
    cout << "Welcome to the ultimate man-machine showdown: Tic-Tac-Toe.\n";
    cout << "--where human brain is pit against silicon processor\n\n";

    cout << "Make your move known by entering a number, 0 - 8. The number\n";
    cout << "corresponds to the desired board position, as illustrated:\n\n";

    cout << "*       0 | 1 | 2\n";
    cout << "*      -----|\n";
    cout << "*       3 | 4 | 5\n";
    cout << "*      -----|\n";
    cout << "*       6 | 7 | 8\n\n";

    cout << "*Prepare yourself, human. The battle is about to begin.\n\n";
}
```

## askYesNo() 函数

这个函数询问一个是或否的问题。它会反复提问，直到玩家输入 y 或 n。它接收一个问题，并返回 'y' 或 'n'。

```cpp
char askYesNo(string question)
{
    char response;
    do
    {
        cout << question << " (y/n): ";
        cin >> response;
    } while (response != 'y' && response != 'n');

    return response;
}
```

## askNumber() 函数

这个函数询问一个指定范围内的数字，并会一直询问，直到玩家输入一个有效的数字。它接收一个问题、一个最高数字和一个最低数字。它返回指定范围内的一个数字。

```cpp
int askNumber(string question, int high, int low)
{
    int number;
    do
    {
        cout << question << " (" << low << " - " << high << "): ";
        cin >> number;
    } while (number > high || number < low);

    return number;
}
```

如果你看一下这个函数的原型，就会发现最低数字的默认值为 0。当我在程序后面调用这个函数时，充分利用了这一特点。

## humanPiece() 函数

这个函数询问玩家是否想要先走，并根据选择返回人类玩家的棋子。正如井字棋的伟大传统所规定的那样，X 先走。

```cpp
char humanPiece()
{
    char go_first = askYesNo("Do you require the first move?");
    if (go_first == 'y')
    {
        cout << "\nThen take the first move. You will need it.\n";
        return X;
    }
    else
    {
        cout << "\nYour bravery will be your undoing... I will go first.\n";
        return O;
    }
}
```

## opponent() 函数

这个函数接收一个棋子（'X' 或 'O'），并返回对手的棋子（'X' 或 'O'）。

```cpp
char opponent(char piece)
{
    if (piece == X)
    {
        return O;
    }
    else
    {
        return X;
    }
}
```

## displayBoard() 函数

这个函数用于显示传入的棋盘。由于棋盘中的每个元素要么是空格、'X' 或 'O'，因此该函数可以逐个显示它们。我还使用了键盘上的其他几个字符来绘制一个像样的井字棋棋盘。

```cpp
void displayBoard(const vector<char>& board)
{
    cout << "\n\t" << board[0] << " | " << board[1] << " | " << board[2];
    cout << "\n\t" << "_______";
    cout << "\n\t" << board[3] << " | " << board[4] << " | " << board[5];
    cout << "\n\t" << "_______";
    cout << "\n\t" << board[6] << " | " << board[7] << " | " << board[8];
    cout << "\n\n";
}
```

注意，表示棋盘的 vector 是通过常量引用传递的。这意味着 vector 被高效地传递，不需要复制。同时，这也意味着 vector 被保护起来，不会被修改。由于我在此函数中只是显示棋盘而不修改它，因此这样做非常合适。

## winner() 函数

这个函数接收一个棋盘并返回赢家。赢家有四种可能的值。如果某一方玩家获胜，函数将返回 X 或 O。如果所有格子都被填满而无人获胜，则返回 TIE。最后，如果无人获胜且至少有一个空格，函数返回 NO_ONE。

```cpp
char winner(const vector<char>& board)
{
    // all possible winning rows
    const int WINNING_ROWS[8][3] = { {0, 1, 2},
                                     {3, 4, 5},
                                     {6, 7, 8},
                                     {0, 3, 6},
                                     {1, 4, 7},
                                     {2, 5, 8},
                                     {0, 4, 8},
                                     {2, 4, 6} };
```

首先要注意的是，表示棋盘的 vector 是通过常量引用传递的。这意味着 vector 被高效地传递，不需要复制。同时，这也意味着 vector 被保护起来，不会被修改。

在这个函数的初始部分，我定义了一个名为 WINNING_ROWS 的常量二维整数数组，它表示所有八种三连成线并赢得游戏的方式。每个获胜行都由一组三个数字表示——三个棋盘位置组成一个获胜行。例如，{0, 1, 2} 这一组代表最上面一行——棋盘位置 0、1 和 2。下一组 {3, 4, 5} 代表中间一行——棋盘位置 3、4 和 5。以此类推……

接下来我要检查双方玩家是否有人获胜。

