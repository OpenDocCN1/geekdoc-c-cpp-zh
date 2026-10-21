![](bbox=[0.19, 0.09, 0.88, 0.61])

Figure 14-8

A curve is somewhat different. An arbitrary number of points may define a curve. The mechanism you’ll use is illustrated in Figure 14-10.

As with the other shapes, the first point is defined by the cursor position when the left mouse button is pressed. Successive positions recorded when the mouse is moved are connected by straight line segments to form the curve, so the mouse track defines the curve to be drawn.

Now you know how the user is going to define an element, clearly the next step in understanding how to implement this is to get a grip on how the mouse is programmed.