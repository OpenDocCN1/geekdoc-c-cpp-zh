# Geometric Transformations

Geometric transformation, in general, means transforming a geometric entity (e.g. point, line, object) to another. This can happen in any dimension. For example, a 2D image can be transformed to another by translating it or scaling it or applying a unique transformation to each of its pixels. Or, a 3D object like a cube can be transformed into a parallelepiped or sphere. All of these will be considered as geometric transformations. Often a 2D image transformation is also called an image warp.

# 6.1 Homogeneous Coordinates

Before we start with geometric transformations, we will first introduce a very important concept of homogeneous coordinates. Let us consider the very simple case of the 1D world (see the red line in Figure 6.1left). Let us consider a point P' on this line. The coordinate of this point will be one dimensional. Let it be (p). Now consider a higher dimensional 2D world in which this line is embedded at y = 1. Draw a ray from the origin of this world through the point P'. Consider

![](bbox=[0.18, 0.66, 0.82, 0.87])

Figure 6.1. Homogeneous coordinates in 1D (left) and in 2D (right).