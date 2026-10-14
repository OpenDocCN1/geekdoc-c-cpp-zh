# Exercises

+   1. You would like to detect edges in an image. You can use a curvature based method C or a gradient based method G.
+   
+      (a) Would using C require using a single or multiple convolution operations? Justify your answer.
+   
+      (b) Would using G require using a single or multiple convolution operations? Justify your answer.
+   
+      (c) Edge detector filters usually combine a low pass filter with a curvature or gradient filter. Why?
+   
+      (d) How does the width of this low pass filter affect the resolution of the edges you would detect?

+   2. In gradient-based edge detection algorithms, a gradient is approximated by a difference. Three such difference operations are shown below. This difference can be viewed as a convolution of $f(x,y)$ with some impulse response of a filter $h(x,y)$. Determine $h(x,y)$ for each of the following difference operators.
+   
+      (a) $$f(x,y)-f(x-1,y)$$
+   
+      (b) $$f(x+1,y)-f(x,y)$$
+   
+      (c) $$f(x+1,y+1)-f(x-1,y+1)+2[f(x+1,y)-f(x-1,y)]+f(x+1,y-1)-f(x-1,y-1)$$

+   3. Consider a binary image created by an edge detection method that marks all the edge pixels. I would like to use a Hough transform to see if this image has any circles. The equation of a circle with center $(a,b)$ and radius $c$ is given by $(x-a)^2+(y-b)^2=c^2$.
+   
+      (a) What is the dimension of the Hough space?
+   
+      (b) Write the equation of the corresponding Hough space entity for each pixel $(x,y)$?
+   
+      (c) Infer from this equation the shape in the Hough space that corresponds to each pixel $(x,y)$?