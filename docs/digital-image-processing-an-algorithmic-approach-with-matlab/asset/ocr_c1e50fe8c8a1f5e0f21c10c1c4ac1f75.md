![](bbox=[0.04, 0.1, 0.49, 0.32])

![](bbox=[0.51, 0.08, 0.89, 0.32])

![](bbox=[0.26, 0.35, 0.69, 0.62])

FIGURE 10.7 Application of the thinning operator. (a) Resulting image after three iterations, (b) resulting image segment after one iteration, (c) actual values for (b).

boundaries meets itself, the fire will extinguish itself; the points at which this happens form the so-called quench line. This line is the skeleton. According to this definition, it is clear that the thinning produces a sort of skeleton.

The terms medial axis transform (MAT) and skeletonization are often used interchangeably but with the slight distinction that the skeleton is simply a binary image showing the simple skeleton, whereas MAT is a gray-level image where each point on the skeleton has an intensity that represents its distance to a boundary in the original object. The skeleton/