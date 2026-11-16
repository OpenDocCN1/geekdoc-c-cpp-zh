![](bbox=[0.185, 0.115, 0.585, 0.29])

Figure 9.12 A shape, a cylinder with two flat ends, and the Gauss map representation for that shape. Normal vectors on the cylinder are illustrated by arrows. The cylinder is rotated slightly toward the viewer so the viewer can see one end. This makes the arrows vary in apparent length. The Gauss sphere itself is illustrated on a black background, and the areas that have been incremented are indicated as white. Two large red arrows have been drawn beside the sphere to indicate the normal directions at the two peaks.

the surface of a sphere, into whatever size patches you wish. This tessellation will determine the resolution of the map. Associate a counter (accumulator) with each cell of the tessellation. Now consider a range image. In the range image, calculate the surface normal at each pixel, and increment the accumulator of the Gauss map that has the same surface normal. This provides essentially a histogram of normal vectors, which in turn can be used to recognize the orientation of the object in the range image.

Determining the orientation of a surface from the Gauss map is accomplished by first identifying significant peaks in the map. The location of the peak on the map corresponds to the orientation of the surface, and the fact that the peak is large indicates that there are many surface patches with that orientation on the surface.

Figure 9.12 illustrates a 3D shape, a cylinder, and its Gauss sphere representation.

# 9.8 Finding the Correspondences – Parametric Consistency in Stereopsis

We will now briefly address the problem of stereopsis and provide an improvement based on accumulator arrays.

Although we won’t see the details until Chapter 12, you know already that when a person observes the same object separately with each eye, the object seems to move (horizontally) between the two views. This *disparity* is the distance in pixels between two corresponding pixels that can be calculated as

$$d = \frac{BF}{z}$$ (9.16)

where $z$ is the distance to the point corresponding to those two pixels, $B$ is the baseline (the distance between the two cameras/eyes), and $F$ is the focal distance of either of the