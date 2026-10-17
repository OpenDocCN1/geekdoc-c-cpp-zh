be the optimal contour. In fact, this problem of inherently preferring short contours over long contours has already been identified in the graph cut- based approaches where the minimum cut usually prefers to take a “short cut” in the image (Sinop and Grady, 2007).

To fix this “short-cut” problem, we have to transfer these contours to a space where their lengths no longer depend upon the area they enclose in the Cartesian space. And, the cost of tracing these contours in this space will now be independent of their scales in the Cartesian space. The polar space has this property, and we use it to solve the scale problem. The contours are transformed from the Cartesian coordinate system to the polar

![](bbox=[0.0, 0.1185, 0.999, 0.5265])