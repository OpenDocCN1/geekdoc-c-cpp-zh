# 13.3 Examples of Recursive Algorithms

513

+   - Only one disk may be moved at a time
- A disk cannot be placed on top of a smaller disc
- All discs must be stored on a peg except while moving

According to the legend, when the monks have moved all of the discs from the first peg to the last peg, the world will come to an end.

To play the game, you must move all of the discs from the first peg to the third peg, following the same rules as the monks. Let's look at some example solutions to this game, for different numbers of discs. If you have only one disc, the solution to the game is simple: move the disc from peg 1 to peg 3. If you have two discs, the solution requires three moves:

+   - Move disc 1 to peg 2
- Move disc 2 to peg 3
- Move disc 1 to peg 3

Notice that this approach uses peg 2 as a temporary location. The complexity of the moves continues to increase as the number of discs increases. To move three discs requires the seven moves shown in Figure 13-6.

# Figure 13-6 Steps for moving three discs

![](bbox=[0.147, 0.458, 0.466, 0.542])

Original setup

![](bbox=[0.523, 0.458, 0.843, 0.542])

First move: Move disc 1 to peg 3

![](bbox=[0.147, 0.584, 0.466, 0.668])

Second move: Move disc 2 to peg 2.

![](bbox=[0.523, 0.584, 0.843, 0.668])

Third move: Move disc 1 to peg 2.

![](bbox=[0.147, 0.712, 0.466, 0.796])

Fourth move: Move disc 3 to peg 3.

![](bbox=[0.523, 0.712, 0.843, 0.796])

Firth move: Move disc 1 to peg 1.

![](bbox=[0.147, 0.84, 0.466, 0.924])

Sixth move: Move disc 2 to peg 3.

![](bbox=[0.523, 0.84, 0.843, 0.924])

Seventh move: Move disc 1 to peg 3.