![](bbox=[0.12, 0.1, 0.81, 0.6])

Figure 14-7

You could allow circles to be drawn in a similar fashion. The first press of the left mouse button would define the center and, as the cursor was moved with the button down, the program would track it. The circle would be continuously redrawn, with the current cursor position defining a point on the circumference of the circle. As with drawing a line, the circle would be fixed when the left mouse button was released. You can see this process illustrated in Figure 14-8.

You can draw a rectangle as easily as you draw a line, as illustrated in Figure 14-9.

The first point is defined by the position of the cursor when the left mouse button is pressed. This is one corner of the rectangle. The position of the cursor when the mouse is moved with the left button held down defines the diagonal opposite corner of the rectangle. The rectangle actually stored is the last one defined when the left mouse button is released.