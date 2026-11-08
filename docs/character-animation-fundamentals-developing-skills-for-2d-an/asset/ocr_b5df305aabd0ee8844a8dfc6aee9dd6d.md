At each of the frames where the crossover breakdown positions occur, move your man into a crossover position and set a key. For example, in ‘basic_walk_2D.avi’ these will be at frames 7 and 19.

Add extra key positions or manipulate the animation/function curves in order to stop the feet from sinking and sliding in the wrong places.

If you want to add whiz lines, make a sphere, distort it so it looks roughly like the shape of your drawn whiz line and place it behind one of the legs. Change the shape of the distortion for each frame, matching your drawn animation, and render it as a semi-transparent. Do the same for the other leg.

When it comes to rendering your animation, don’t render the last frame. For example, in ‘basic_walk_2D.avi’, only render 24 frames. This will prevent a jump at the point where the animation loops.

![](bbox=[0.404, 0.126, 0.565, 0.315])

![](bbox=[0.644, 0.099, 0.961, 0.314])

![](bbox=[0.404, 0.352, 0.565, 0.544])

![](bbox=[0.644, 0.334, 0.961, 0.548])

# Changing the Pace and Mood in a Walk
Exercise in 2D

The illustration (right) shows the background for the exercise we are going to do.

The idea is to have a character that walks into the scene from screen right, slows down to look at the sign (by taking shorter strides) and then, as a result of reading the sign, walks out screen left displaying a different emotion. Our character will be walking along the floor this time, rather than sliding its legs back, as in the walk cycle exercise.

![](bbox=[0.565, 0.636, 0.961, 0.859])