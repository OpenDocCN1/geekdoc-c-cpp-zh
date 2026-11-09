+   5. Command `G17 (G68 X0 Y0 R<θ>)` (X0 Y0, which is the center of rotation, can be left blank because the current tool position automatically becomes the center of rotation, if it is not specified).
+   6. Execute machining program.
+   7. Command `G69` (cancel coordinate rotation).
+   8. End of program.

The X- and Y-coordinates of point O, and the angle θ, can be determined using touch probes. For this, the probe would need to touch the orthogonal edges of the workpiece at three points, as shown in Fig. 11.4. Let the coordinates of each of the points be $(x_A, y_A)$, $(x_C, y_C)$, and $(x_D, y_D)$, respectively, corresponding to points A, C, and D. The equation given below can be used for necessary calculations. (Try to derive these, using coordinate geometry.)

The equations of lines CD and AB (which is orthogonal to CD) would be:

$$y_{CD}=\frac{y_D-y_C}{x_D-x_C}(x-x_C)+y_C$$

$$y_{AB}=-\frac{x_D-x_C}{y_D-y_C}(x-x_A)+y_A$$

The coordinates $(x_B, y_B)$ of the point of intersection of these lines (point B) can be found out by solving these equations simultaneously, which gives:

$$x_B=\frac{m^2x_C-my_C+x_A+my_A}{m^2+1}$$

$$y_B=\frac{-mx_C+y_C+mx_A+m^2y_A}{m^2+1}$$

where

$$m=\frac{y_D-y_C}{x_D-x_C}$$

Angle θ would be given by

$$\theta=\tan^{-1}m$$

Finally, the coordinates of the program zero point O would be

$$x_O=x_B+\sqrt{2}\,r\cos(\theta+45)$$

$$y_O=y_B+\sqrt{2}\,r\sin(\theta+45)$$

where r is the radius of the ball of the probe.