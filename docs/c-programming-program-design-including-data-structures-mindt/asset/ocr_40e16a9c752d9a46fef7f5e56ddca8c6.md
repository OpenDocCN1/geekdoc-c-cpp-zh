# Input

This program has two types of input:

+   - The users’ responses when asked to play the game.
+   - The players’ choices.

# Output

The players’ choices and the winner of each play. After the game is over, the total number of plays and the number of times that each player won should be output as well.

# PROBLEM ANALYSIS AND ALGORITHM DESIGN

Two players play this game. Players enter their choices via the keyboard. Each player enters R or r for Rock, P or p for Paper, or S or s for Scissors. While the first player enters a choice, the second player looks elsewhere. Once both entries are in, if the entries are valid, the program outputs the players’ choices and declares the winner of the play. The game continues until one of the players decides to quit the game. After the game ends, the program outputs the total number of plays and the number of times that each player won. This discussion translates into the following algorithm:

+   1. Provide a brief explanation of the game and how it is played.
+   2. Ask the users if they want to play the game.
+   3. Get plays for both players.
+   4. If the plays are valid, output the plays and the winner.
+   5. Update the total game count and winner count.
+   6. Repeat Steps 2 through 5 while the users agree to play the game.
+   7. Output the number of plays and times that each player won.

We will use the following enumeration type to describe the objects.

```
enum objectType {ROCK, PAPER, SCISSORS};
```

# Variables (function main)

It is clear that you need the following variables in the function main:

```
int gameCount;  //variable to store the number of
                  //games played
int winCount1;  //variable to store the number of games
                //won by player 1
int winCount2;  //variable to store the number of games
                //won by player 2
int gamewinner;
char response;   //variable to get the user's response to
                 //play the game
char selection1;
char selection2;
objectType play1;  //player1's selection
objectType play2;  //player2's selection
```