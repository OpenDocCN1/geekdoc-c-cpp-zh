# WHAT'S NEXT?

There are several directions you could go to take your programming skills to the next level.

+   » You could learn more about algorithms and data structures in general.
» You could explore a particular application area, including learning one of the many libraries that give you tools to approach applications.
» You could use your foundation of C++ to learn almost any other language you might want, such as C#, Java, or JavaScript.

# READINGS

a Stroustrup, *Programming Principles and Practice Using C++*, chap. 20.

b Lippman, Lajoie, and Moo, *C++ Primer*, sections 3.4 and 9.1-9.3.

# // QUIZ

1 Lecture 21 presented a program that would allow the game Reversi (Othello) to be played. Now imagine that you wanted to build an AI for Othello, similar to the one you built for Connect 4. The process of looking ahead by several moves would be no different for the Reversi game. However, you would need a different board evaluation function as well as different functions to list the available moves.

For the board evaluation function for a Reversi game:

a What would be a straightforward board evaluation for Reversi? Remember, you want a computation that would give a low score if player 1 is winning and a high score if player 2 is winning.

b Write the board evaluation function that you would use. The name should be get_board_score, and it would return an integer. It should be a member of the reversi_board class:

```
class reversi_board {
  private:
    vector<vector<int> > board;
    // Other code including board evaluation function here
};
```

Recall that the board is 8 by 8 in size and that the elements are 0 if there is no piece on the square or 1 or 2 if player 1 or 2 has his or her piece on the square.

Note: As an exercise, you might want to try on your own to adapt the AI for playing Connect 4 to instead play Reversi. You will need to update the earlier Reversi game functions similar to the way the Connect 4 functions were updated and introduce new routines for finding all valid moves and the board evaluation.

Click here to see the answer.