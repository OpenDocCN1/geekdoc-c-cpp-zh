```
bool traverse_maze() :
// Precondition: The user of the program is facing an unblocked spot in the
// maze, and this spot has not previously been visited by the user.
// Postcondition: The function has asked a series of queries and provided
// various directions to the user. The questions and directions have led the
// user through the maze and back to the exact same position where the
// user started. The return value of the function is a true/false value
// indicating whether the user found a magic tapestry in the maze.
```

This recursive function will return a boolean value (rather than being a void function). A function that returns a value can be recursive in situations like this where the answer to a smaller problem will help to solve the complete problem. In this particular case, we'll see that searching part of the maze can help us determine whether the tapestry is present in the entire maze.

# FIGURE 9.6 Script for the Maze Traversal Function

# A Sample Dialogue

Step forward & write your name on the ground.
Have you found the tapestry? [Yes or No]
No
Please turn left 90 degrees.
Are you facing a wall? [Yes or No]
No
Is your name written ahead of you? [Yes or No]
No
Step forward & write your name on the ground.
Have you found the tapestry? [Yes or No]
No
Please turn left 90 degrees.
Are you facing a wall? [Yes or No]
Yes
Please turn right 90 degrees.
Are you facing a wall? [Yes or No]
No
Is your name written ahead of you? [Yes or No]
No
Step forward & write your name on the ground.
Have you found the tapestry? [Yes or No]
Yes
Pick up the tapestry, and take a step backward.
Please turn right 90 degrees.
Please turn right 90 degrees.
Please step forward, then turn 180 degrees.
Please turn right, then turn right.
Please turn right 90 degrees.
Please turn right 90 degrees.
Please step forward, then turn 180 degrees.

> This dialogue supposes that the user starts at the entrance to the maze drawn below. The starting point of the user is represented by the arrow in a circle, with the arrow pointing in the direction that the user is facing. The large X is the magic tapestry.

![](bbox=[0.58, 0.58, 0.84, 0.83])