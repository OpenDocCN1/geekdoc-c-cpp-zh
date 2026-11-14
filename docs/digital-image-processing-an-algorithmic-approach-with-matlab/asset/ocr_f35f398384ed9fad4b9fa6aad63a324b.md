The angle of orientation of the edge (relative to the pixel grid) giving rise to the spatial gradient is given by

$$\theta = \tan^{-1} \left( \frac{G_y}{G_x} \right).$$ (9.4)

In this case, orientation 0 is taken to mean that the direction of maximum contrast from black to white runs from left to right on the image, and

![](bbox=[0.05, 0.29, 0.45, 0.53])

![](bbox=[0.51, 0.29, 0.9, 0.53])

![](bbox=[0.05, 0.56, 0.45, 0.8])

![](bbox=[0.51, 0.56, 0.9, 0.8])

FIGURE 9.2 Application of the Sobel operator. (a) Original RGB image, (b) grayscale image, (c) $G_x$, (d) $G_y$ (e) image using Equation 9.2, (f) image using Equation 9.3, (g) MATLAB's Sobel operator with threshold 0.1, (h) MATLAB's Sobel operator with threshold 0.05.