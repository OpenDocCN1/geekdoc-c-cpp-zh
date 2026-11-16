![](bbox=[0.196, 0.119, 0.883, 0.379])

Figure 7.17 LEFT: An edge image. RIGHT: The DT of the LEFT image, computed using the mask of Figure 7.14.

where p_i denotes the coordinate of any point in region i, d calculates the distance between point x and point p_i. The set of points equidistant from two of those regions is referred to as the Voronoi diagram, and is illustrated by the dark lines in the figure.

Breu et al. showed in [7.2] how the DT of d-dimensional binary image can be computed by constructing and regularly sampling the Voronoi diagram.

![](bbox=[0.196, 0.576, 0.623, 0.883])

Figure 7.18 The distance transform shown in Figure 7.17 (RIGHT), using a random pseudocolor assignment.