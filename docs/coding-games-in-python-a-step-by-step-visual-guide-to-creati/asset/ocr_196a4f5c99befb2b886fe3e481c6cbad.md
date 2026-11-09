# ## How it works

First you’ll add the balloon and all the obstacles to the code. The program will check if the player has pressed the mouse button to move the balloon up, or hasn’t to let it fall. Once an obstacle has disappeared off the left edge of the screen, the program will place a new one up to 800 pixels off the right edge of the screen at a random position to make the obstacles appear at random intervals. If the balloon hits any of the obstacles, the game will end and the top scores will be displayed.

![](bbox=[0.656, 0.053, 0.972, 0.375])

![](bbox=[0.03, 0.282, 0.977, 0.986])

![](bbox=[0.092, 0.83, 0.259, 0.986])

# ### Balloon Flight flowchart

This flowchart maps the progress of the game, which constantly checks for obstacles appearing, disappearing, mouse clicks, and collisions between the balloon and the obstacles.