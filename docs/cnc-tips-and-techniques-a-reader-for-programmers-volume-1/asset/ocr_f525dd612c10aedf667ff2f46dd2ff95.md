be confused with Polar Coordinate Interpolation.

In cylindrical interpolation, the C-axis can also be used together with the Z-axis to program a continuous contour tool-path. This method provides synchronized motion of the linear Z-axis with C-axis part rotation. The most common application for this type of machining is cylindrical grooving.

This brief overview touched upon only some of the manual programming methods that can be used with C and Y axes. For more complex parts (especially contours), using a suitable CAM software is much more efficient.

![](bbox=[0.064, 0.387, 0.135, 0.428])

# ## Trial Cut for Measuring

*March 2008, updated February 2013*

Precision CNC machining is always a cooperative effort between CNC programmers and CNC machine operators. Programmers can employ certain program features that will enable the machine operators to perform functions that would otherwise be difficult or even impossible. One such method is programming a trial cut for measuring.

There are many factors in machining that influence the final size of a part, such as heat, tool deflection, tool wear, and even lubrication to some extent. For those parts that require very tight tolerances, the negative effect of these factors may result in an out of tolerance size and even a possible scrap. Another problem that is quite common is machining certain hard-to-measure shapes, such as a cone on CNC lathes. By using a simple programming method known as the trial cut, CNC programmers can greatly influence the final size of a part.

# ### Measuring Cones

Take the already mentioned cone as an example. Without a suitable custom gauge, a cone is a difficult shape to measure at the machine, as there is no flat spot for the micrometer to use.