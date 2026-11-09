# 3. Write some instructions

Now add this code beneath the command to import Turtle. It creates variables that set the size and shape of the star. It also tells the turtle how to move around the window to draw the star.

```
import turtle as t

size = 300
points = 5
angle = 144

for i in range(points):
    t.forward(size)
    t.right(angle)
```

This is the angle formed by each star point, shown in degrees.

These are the instructions for the size and shape of the star.

This for loop makes the turtle repeat the same movement for each point of the star.

# 4. Draw a test star

From the IDLE menu, select “Run” and then “Run Module” to test the project. The Turtle Graphics window will appear (it might be behind another window) and you’ll see the turtle arrow begin to draw your star.

![](bbox=[0.366, 0.367, 0.749, 0.599])

The turtle arrow moves in the window, drawing the star as it goes.

The star is drawn one line at a time.

![](bbox=[0.817, 0.443, 0.932, 0.531])

Don’t forget to save your work

# 5. Add an angle calculator

It would be good to be able to draw stars with different numbers of points. Make this change to the code. It will calculate the angle of the turns that the turtle needs to make to draw a star with however many points you choose.

```
import turtle as t

size = 300
points = 5
angle = 180 - (180 / points)

for i in range(points):
    t.forward(size)
    t.right(angle)
```

The angle depends on the number of points the star has.