strange to start our numbers at 0 instead of 1, but doing so will make our programming easier because we store information about the board in this two-dimensional array (which is a private member variable):

```
who data[ROWS][COLUMNS];
```

Remember that the who data type came from the game class. It is an enum type that has three possible values (HUMAN, NEUTRAL, COMPUTER). The ROWS and COLUMNS constants are defined as static member constants of the connect4 class (ROWS is 6 and COLUMNS is 7), so that each spot in the data array corresponds to one spot on the game board. For example, if the game board has a black checker at row 1 and column 6, then data[1][6] will be set to COMPUTER (since the computer is the second player, using black checkers). Any location without a checker will be recorded as NEUTRAL in the data array.

the purpose of the three member variables

In addition to the data array, we have two other private member variables:

```
int many_used[COLUMNS];
int most_recent_column;
```

The value of many_used[i] is the number of checkers in column number i (which is useful when you're calculating where the next checker in that column should go). After the game is started, the value of most_recent_column will be the column where the last checker was placed. This is useful for reducing the calculations about whether the game has ended.

The only remaining work is to understand and implement the eight virtual functions and the constructor. We'll do this over the next few pages, sometimes providing an implementation and other times providing only a discussion.

# The Connect Four Constructor and Restart Function

The connect4 default constructor activates the game constructor (using the member initialization list described in Figure 14.7 on page 697) and then activates the restart member function. The restart function initializes the connect4 member variables; for example, the data array is set to all NEUTRAL values. As indicated in the documentation for the game class (Figure 14.12 on page 713), the restart function of any derived class must also activate game::restart(), which will reinitialize the game's member variables.

# Three Connect Four Functions That Deal with the Game's Status

Each class that is derived from the game must implement three virtual member functions that allow the game class to access the current state of the game:

The display_status function. This void function has no parameters. It merely displays the current status of the game. Our implementation of display_status prints a grid representing the game, like this: