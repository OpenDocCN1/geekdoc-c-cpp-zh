for the half-sized house. Now, inside the procedure house, we will use that number that Main sent
over. Instead of forward 1, we can say forward:size. This means "go forward by what's size.
We're reading those two dots in front of size as "what's in." We will worry about the details of
house in a minute.

Now, using the flowchart, code your Main procedure. Use question, answer, and if statements.
Brush on that by looking at the Help vocabulary if you need to. Remember to create the loop
by calling Main at the end, like this:

```
ifelse (answer = "y)[Main][animate]
```

In the middle of Main we need a line that moves the turtle to draw to a new house. Let's
consider that line. First pick the pen up. Then we need to drop the turtle down from the windowsill
to the street level, and then move it to the right. To add to the street level, you could make use of theuilt-in procedure size. If you command size -120, the turtle will drop out from wherever it
to, to the level of Y=-120. Try it: set size -120 in the Command Center, and see where your turtle
goes. If this isn't your street level, put the turtle at your street level and show pos in
t x and y coordinates. The second one;
that's your y coordinate. Next set with number. After dropping the turtle to street level,
move it to the 100 or 125 turtle steps. Add a comment to remind you what is going on, like
this: moving the turtle to a new spot.

To get our program going, we need to code these procedures: setup, house with one input,
Iwindow, Iwindow, filled, fillblue, and animate. I already gave you Start.

To setup, put your turtle where you want it to start, using the mouse. This will be along the
left side of the Graphics Page, fairly low. Now use show pos in the Command Center to find its
coordinates. In the setup procedure, to set t1 to its position there.

How do we code house? This is actually from Computer Science Pure and Simple Book 1, where
we draw a house and then added a variable that re-sized it. First, don't worry now about the variable
inside the procedure. Make a procedure to size that draws a house but doesn't actually
use size. It can be a simple house, or a more complex one. A simple house is a square 50 turtle
steps on one side, a triangle on top of it, and a door. Remember that if the turtle is drawing a triangle
with equal sides, it 120 degrees at each corner.

Next we will make two window procedures, Iwindow and Window. One draws one window, one
draws two. Each from the start where the drawing of house ended. Make a little sketch
with dimensions on it, to tell your turtle where to go to start.

Next, we will make two procedures, filled and fillblue. In each one, the turtle picks up one (pu)
and takes a step out into the square that represents the side of the house. It colors the in
the bucket using setc; for example, setc 15 sets it to red, and set 105 sets it to blue. It puts its pen in
down (pd). Then it fills the side of the house using color fill.

Animate is a fancy procedure we will develop later. For the time being, just make a dummy:

```
to animate
end
```

This will show us if our program as a whole works.

Make a Start button.