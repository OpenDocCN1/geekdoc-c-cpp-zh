+   18. Ask player(s) if they want to play again: Remember a good game loop should always allow the player(s) the option of playing again.
+   19. End or repeat game: Ending the gaming loop in our case means ending the game and returning to the menu portion. This allows the users to either quit the program or continue on to another game.

**Example 3.44. Eight directions of movement.**

![](bbox=[0.293, 0.274, 0.634, 0.424])

# Setting up the Compiler

At this point, we need to get the compiler up and running; repeat the steps used to link the class base and all of its counterparts. If you'd prefer to use chapter3\project2, you can just load it up, but if you're building from scratch you'll have to remember to add each file to the project, and in some cases, you'll have to remember to load the Windows Multimedia Library. Again, we'll need to build several user-defined functions with a final main function that controls this game (refer to the previous sections as needed).

# Animating Characters: Animating Spaceships

The key to animating the spaceship is keeping track of the direction the spaceship is facing and then drawing the corresponding image for that direction. Since each player can turn the spaceship, we need to update the direction of the spaceship (see Example 3.45). Now that we can keep track of the direction, we need a function that will display the appropriate image for that direction (see Example 3.46). In Example 3.47, you can see how this function is called for Player 1. The code is similar for Player 2. Note that this function makes use of arrays which are covered in Chapter 4.