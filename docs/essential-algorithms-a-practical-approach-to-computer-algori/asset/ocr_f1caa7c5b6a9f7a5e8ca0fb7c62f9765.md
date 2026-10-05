With some work that is far outside the scope of this book, you can show that SAT and 3SAT are equivalent, so they are equally difficult to solve.
Note that the same kind of decision tree will solve either version of the problem.

# Summary

Decision trees are a powerful tool for approaching complex problems, but they are not the best approach for every problem. For example, you could model the eight queens problem described in Chapter 9 with a decision tree that was eight levels tall and had 64 branches per node, giving a total of $648 = 2.8 	imes 10^{14}$ leaf nodes. By taking advantage of the tree's structure, you can eliminate most of the tree's branches without exploring them and explore only 113 board positions. Thinking about the problem as a general decision tree may be a mistake, because it might make you miss the simplifications that let you solve the problem efficiently.

Still, decision trees are a powerful technique that you should at consider if you don't know of a better approach to a problem.

This chapter and the previous two trees and algorithms build, maintain, and search trees. The next two chapters discuss networks. Like trees, networks are linked data structures. Unlike trees, networks are not hierarchical, so they can contain loops. That makes them a bit more complicated than trees, but it also lets them model and solve some interesting problems that trees can't.

# Exercises

Asterisks indicate particularly difficult problems.

+   1. Write a program that exhaustively searches the tic-tac-toe game tree and counts the number of X wins, O wins, and the game ends in a tie. What are those counts, and what is the total number of games possible? Do the numbers give an advantage to one player or the other?
2. Modify the programs you wrote for Exercise 1 so that the user can place one or more pieces on a tic-tac-toe board and then count the number of X wins, O wins, and ties from that point. How many total games are possible starting from each of the nine initial moves by X? (Do you need to calculate all nine?)
3. Write a program that lets the player play-tac-toe against the computer. Let the player be X or O. Provide three skill levels: Random (the computer moves randomly), Beginner (the computer uses minimax with only three levels of recursion), and Expert (the computer uses a full minimax search).