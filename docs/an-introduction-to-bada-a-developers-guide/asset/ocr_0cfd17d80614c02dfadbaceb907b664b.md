In this recipe the touch screen user input is handled by the application and is used to draw lines on a graphics canvas. Lines are drawn on the graphics canvas following the motion of the user's touch input. The double-tap touch input is used to clear the canvas.

![](bbox=[0.28, 0.28, 0.75, 0.78])

Figure R2.9 Drawing lines with multi-touch input.

This recipe details only the changes made to the ‘Get Touch Events’ recipe to enable the handling of multiple touch events.

In the ‘Get Touch Events’ recipe a member variable pointer of type Point was added to store the previous touch position for using in the TOUCH_MOVED event calculations. Because this recipe will be handling multiple touch points, a member variable pointer of type IList will be used to store the event information for each point instead: