```
g) char *s;
    printf("%s\n", s);
```

# 7.20 (Maze Traversal)

The following grid is a two-dimensional array representation of a maze. The # symbols represent the maze's walls, and the periods (.) represent squares in the possible paths through the maze.

![](bbox=[0.2, 0.27, 0.85, 0.62])

The Wikipedia page https://en.wikipedia.org/wiki/Maze_solving_algorithm lists several algorithms for finding a maze's exit. A simple algorithm for walking through a maze guarantees finding the exit (assuming there's an exit). Place your right hand on the wall to your right, and begin walking forward. Never remove your hand from the wall. If the maze turns to the right, you follow the wall to the right. As long as you do not remove your hand from the wall, eventually you'll arrive at the maze's exit. If there's not an exit, you'll eventually arrive back at the starting location. There may be a shorter path than the one you've taken, but you're guaranteed to get out of the maze.

Write recursive function mazeTraverse to walk through the maze. The function should receive as arguments a 12-by-12 character array representing the maze and the maze's starting location. As mazeTraverse attempts to locate the exit from the maze, it should place the character X in each square in the path. The function should display the maze after each move so the user can watch as the maze is solved.

# 7.21 (Generating Mazes Randomly)

Write a function mazeGenerator that takes as an argument a two-dimensional 12-by-12 character array and randomly produces a maze. The function should also provide the starting and ending locations of the maze. Try your function mazeTraverse from Exercise 7.20 using several randomly generated mazes.

# 7.22 (Mazes of Any Size)

Generalize functions mazeTraverse and mazeGenerator of Exercises 7.20–7.21 to process mazes of any width and height.

# 7.23 What does this program do, assuming that the user enters two strings of the same length?

```
// ex07_26.c
// What does this program do?
#include <stdio.h>
```