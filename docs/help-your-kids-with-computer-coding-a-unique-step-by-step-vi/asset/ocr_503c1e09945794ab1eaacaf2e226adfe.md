# Waiter robot program 3

In this version of the program, the robot successfully delivers the food to the diner avoiding any obstacles. But after putting the plate down, the robot remains standing at the table while food piles up in the kitchen.

+   1. Pick up a plate with food holding it level at all times

+   2. Move from kitchen to diner's table by:

+   Move to door between kitchen and dining area

+   checking for obstacles and steering around them

+   Move from door to the table

+   checking for obstacles and steering around them

![](bbox=[0.648, 0.135, 0.946, 0.348])

> Success at last?
The robot can deliver the food safely. But we forgot to give it instructions to go back to the kitchen and get the next plate.

+   3. Put plate down on the table in front of the diner

# Real-world example

The waiter robot might be imaginary, but algorithms like this are in action all around us. For example, a computercontrolled elevator faces the same sort of problems. Should it go up or down? Which floor should it go to next?

![](bbox=[0.715, 0.486, 0.936, 0.666])

+   1. Wait until doors are closed

+   2. Wait for button to be pressed

+   If button pressed is higher than current floor:

+   Move lift upwards

+   If button pressed is lower than current floor:

+   Move lift downwards

> Elevator program
For the elevator to work correctly and safely, every step has to be precise, clear, and cover every possibility. The programmers have to make sure they create a suitable algorithm.

+   3. Wait until current floor equals button pressed

+   4. Open doors