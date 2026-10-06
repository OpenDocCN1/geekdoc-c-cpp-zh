# Type Basics and Argument Passing 201

| | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---||
| Row A | * | * | X | X | * | * | * |
| Row B | * | X | * | * | * | * | * |
| Row C | * | * | * | * | X | X | X |
| Row D | * | * | * | * | * | * | * |
| Row E | * | X | X | * | * | X | X |
| Row F | * | * | * | * | * | * |
| Row T | * | X | X | X | X | * | X |

Seats that are already reserved are marked with an X. Seats that are available are marked with a *.

+   3. Both you and your friend decide to go bowling. Bowling is a game where a ball is rolled down in an attempt to knock down pins. Write a script that calculates the total score of your games. One of bowling consists of 10 frames, with a minimum score of zero and a maximum of 300. Each frame consists of two chances to knock down ten pins. If all pins are knocked down on your first ball you get a 'strike'. A strike is denoted by an X. If it takes you two rolls to knock down all ten pins, it is called a 'spare'. A spare is denoted by a \on the score sheet. If there is at least one pin standing after two rolls, it is called an 'open frame'. Here are the scoring rules:

+   * Open frames are scored at face value.
* A strike is 10, plus the value of your next roll. If you knock down 4 pins on your next roll and zero pins on your next roll, the score for that frame will be 10+4+0=14. However, if you get another strike on your next roll and another strike on your next roll, the score for frame will be 10+10+10=30. The minimum score for a frame in which you get a strike is 10 and the maximum score is 30.
* A spare is 10, plus the value of your next roll. The minimum score for a frame in which you get a spare is 10 and the maximum score is 20 (a spare and a strike on your next roll).

Each frame consists of up to 2 rolls, except for the tenth frame which could consist of 3 rolls if the player gets a strike on their first roll of the frame. Read in the bowling marks for each frame and display the score sheet result (X, /, or a number), frame score, and a running total for each player.

4. The Galton box, also known as the bean machine, is a device created by Francis Galton. It consists of a vertical board with evenly spaced pegs in a triangular pattern. Each time a ball hits a peg, it will fall to either the left or right of the peg. Peg piles of balls are accumulated in the slots at the bottom of the board. Write a script that simulates the bean machine that has 8 slots in which you drop 20 balls. You should simulate the falling of each ball by printing the ball's path. For example, LLRLLR indicates each direction the ball fell before slot 4 on a bean machine with 8 slots. Print the final buildup of the balls in the slots in a machine.

+   5. Write a function that takes a Double* and returns the median value (not the