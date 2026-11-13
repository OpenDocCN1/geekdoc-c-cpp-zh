that contain one digit specifying the slot in which the player wants to place the next checker. For example, the string “3” represents the move of putting a checker into slot number 3.

Each derived class must provide three virtual member functions that deal with its move strings:

**The is_legal_move function.** This bool function has a string as its parameter. It returns true if the string is currently a legal move for the next player. Among other things, the game class uses this function to determine whether a move typed by the user is currently legal. For Connect Four, a move is legal provided that it is a number from 0 to COLUMNS-1, and that the selected column is not already full.

**The make_move function.** This void function has a string move as its parameter. The string has already been checked to ensure that it is a legal move. The function is responsible for making this move (by updating the member variables that represent the status of the game). The function must also activate game::make_move, so that the base class can update any of its member variables that deal with the status of the game.

**The compute_moves function.** The prototype for this function is:

```
void compute_moves(std::queue<std::string>& moves) const;
```

The function examines the current status of the game and determines what moves are currently legal. All these legal moves are then placed into the queue. The function does not actually make any of these moves (it just puts these moves into the queue), so compute_moves can be a const member function.

If the game is not yet over, there should always be at least one legal move put into the queue (although in some games, such as Othello, this one legal move could be a “pass” move).

# The clone Function

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