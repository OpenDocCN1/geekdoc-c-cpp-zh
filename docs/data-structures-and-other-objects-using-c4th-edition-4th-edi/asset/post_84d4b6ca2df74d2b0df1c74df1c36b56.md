
strange to start our numbers at 0 instead of 1, but doing so will make our programming easier because we store information about the board in this two-dimensional array (which is a private member variable):

```
who data[ROWS][COLUMNS];
```

Remember that the who data type came from the game class. It is an enum type that has three possible values (HUMAN, NEUTRAL, COMPUTER). The ROWS and COLUMNS constants are defined as static member constants of the connect4 class (ROWS is 6 and COLUMNS is 7), so that each spot in the data array corresponds to one spot on the game board. For example, if the game board has a black checker at row 1 and column 6, then data[1][6] will be set to COMPUTER (since the computer is the second player, using black checkers). Any location without a checker will be recorded as NEUTRAL in the data array.

### the purpose of the three member variables

In addition to the data array, we have two other private member variables:

```
int many_used[COLUMNS];
int most_recent_column;
```

The value of many_used[i] is the number of checkers in column number i (which is useful when you're calculating where the next checker in that column should go). After the game is started, the value of most_recent_column will be the column where the last checker was placed. This is useful for reducing the calculations about whether the game has ended.

The only remaining work is to understand and implement the eight virtual functions and the constructor. We'll do this over the next few pages, sometimes providing an implementation and other times providing only a discussion.

## The Connect Four Constructor and Restart Function

The connect4 default constructor activates the game constructor (using the member initialization list described in Figure 14.7 on page 697) and then activates the restart member function. The restart function initializes the connect4 member variables; for example, the data array is set to all NEUTRAL values. As indicated in the documentation for the game class (Figure 14.12 on page 713), the restart function of any derived class must also activate game::restart(), which will reinitialize the game's member variables.

## Three Connect Four Functions That Deal with the Game's Status

Each class that is derived from the game must implement three virtual member functions that allow the game class to access the current state of the game:

### The display_status function.

This void function has no parameters. It merely displays the current status of the game. Our implementation of display_status prints a grid representing the game, like this:

```
Current game status
(HUMAN = # and COMPUTER = @):
Most recent move in column 5
. . . . . . . .
. . . . . . . .
. . . . . . . .
. . . . . . . .
. . . @ . . . .
. . @ # # # # .
0 1 2 3 4 5 6
Computer's turn to move...
```

In this grid, we used the character '@' to represent a computer checker and the character '#' to represent the human's checker.

### The is_game_over function.

This bool function also has no parameters. Its return value is true if the current game is over. The game is over if the most recently placed checker is part of a four-in-a-row, or if all the columns are full.

### The evaluate function.

This function is the heart of the game. It examines the current status and provides a numerical estimate of how favorable the current status seems, providing a positive answer if the status is good for the computer and a negative answer if the status is good for the human. Larger magnitudes indicate a more certain answer, and an evaluation of zero indicates that the game is more-or-less even for both players.

The evaluation should be done in fixed way that doesn't try to look ahead at possible future moves (because looking ahead is already built into the game class's play function). There's no one right way to evaluate the game status, but we can tell you the idea we used, which was suggested by our colleague John Gillett: We examine each possible sequence of four consecutive locations, giving each such sequence a value as follows:

| If the four locations have... | then the value is... |
| --- | --- |
| ...four computer checkers | +500 |
| ...1 to 3 computer checkers and none of the human's | +1 to +3 |
| ...no checkers or a mixture of both players | zero |
| ...1 to 3 human checkers and none of the computer's | -1 to -3 |
| ...four of the human's checkers | -500 |

The result of our evaluation function is the sum of all these values from examining each of the possible sequences of four locations in the current game. The large numbers (+500 and -500) were selected so that the total evaluation would always favor the player who obtained four-in-a-row, even if the other locations completely favor the other player.

## Three Connect Four Functions That Deal with Moves

Our game class needs some way to represent a move in the game. Since the programmer of the game class doesn't know much about the exact game being played, we decided to use strings to represent moves. The exact format of these "move strings" can be decided by the programmer who implements a derived class. In the case of Connect Four, our move strings will just be simple strings that contain one digit specifying the slot in which the player wants to place the next checker. For example, the string “3” represents the move of putting a checker into slot number 3.

Each derived class must provide three virtual member functions that deal with its move strings:

### The is_legal_move function.

This bool function has a string as its parameter. It returns true if the string is currently a legal move for the next player. Among other things, the game class uses this function to determine whether a move typed by the user is currently legal. For Connect Four, a move is legal provided that it is a number from 0 to COLUMNS-1, and that the selected column is not already full.

### The make_move function.

This void function has a string move as its parameter. The string has already been checked to ensure that it is a legal move. The function is responsible for making this move (by updating the member variables that represent the status of the game). The function must also activate game::make_move, so that the base class can update any of its member variables that deal with the status of the game.

### The compute_moves function.

The prototype for this function is:

```
void compute_moves(std::queue<std::string>& moves) const;
```

The function examines the current status of the game and determines what moves are currently legal. All these legal moves are then placed into the queue. The function does not actually make any of these moves (it just puts these moves into the queue), so compute_moves can be a const member function.

If the game is not yet over, there should always be at least one legal move put into the queue (although in some games, such as Othello, this one legal move could be a “pass” move).

## The clone Function

Each class derived from our game class must provide one more function:

```
virtual game* clone( ) const;
```

The purpose of this function is to make a complete copy of the current game, and return a pointer to this copy. Such copies are needed by the game class when it is exploring possible future moves. (These potential moves are made to copies of the game, so that the actual game is not altered during the mere exploration of future possibilities).

The implementation of the connect4 clone function can use the automatic copy constructor, so there is not much work to making a copy:

```
game* connect4::clone( ) const
{
    return new connect4(*this);
}
```

## another reason why we used virtual member functions virtual constructors are forbidden

This call of the new operator uses the connect4 automatic copy constructor to create a copy of *this. The notation *this is always the object that activated the current method, in other words, the object that activated the clone method. So, the overall effect is to create a copy of the connect4 object that activated the clone method, and return a pointer to this new object.

Notice that the actual return type of the clone function is a pointer to a game object. This is fine because a pointer to a game object (the base class) can be used to point to a connect4 object (the derived type). Moreover, if we activate member functions of this object, we will always use the correct connect4 member functions (because we used virtual member functions).

Finally, notice that the clone method is simple, but it cannot be implemented by the game itself because the game base class cannot use the copy constructor of the derived class. We might get around this problem if constructors could be virtual, but C++ does not allow virtual constructors.

## Writing Your Own Derived Games from the game Class

You can now write the connect4 class yourself (for comparison to ours), or you could write other games that are derived from the game class. Some useful resources are online:

| /chapter14/game.h | our game class header file |
| /chapter14/game.cxx | our game class implementation file |
| /chapter14/connect4.h | our connect4 header file |
| /chapter14/connect4.cxx | our connect4 implementation file |
| /projects/ | ideas for other games to implement |

It's interesting that you can write such clever games without knowing the details of the game class's play function. In fact, we encourage you to write your derived classes without much concern for the workings of the base. On the other hand, it might be interesting to know a bit more about the game class's algorithm. You can download and read the entire game class, or read our short discussion, next.

## The game Class's Play Algorithm with Minimax

The play algorithm alternates between getting a human move and a computer move. The interesting part is the computer move, which starts by using compute_moves to calculate all the possible moves. For example, if the computer has three possible moves, then we can draw the situation as shown in the margin. Our first version of the game class had a private member function, eval_with_look_ahead, which was used to evaluate each of the possible new positions, with this specification:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_751_0.png)
