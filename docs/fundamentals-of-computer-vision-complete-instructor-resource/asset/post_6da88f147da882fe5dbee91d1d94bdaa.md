
- (Section 12.6) With only one camera, we can sometimes still look at how things in the image change (things like shading, texture, focus, etc.) and get 3D information. These “shape from” methods are covered in Section 12.6.
- (Section 12.7) Finally, we examine the mathematics of the three-dimensional surfaces themselves.

We should emphasize that in this book, we only introduce the student to these methods. There are ways to combine information from multiple cameras, multiple views with the same camera, and a variety of other related approaches to these problems. The student confronting a problem in the field may have need of these extensions to the basic methods of this chapter, and is referred to more detailed references such as [12.15].

Before proceeding to the next section, we clarify some definitions first:

**A range image is** a data structure in the form that you are used to, f(x, y), but the difference is this: f does not represent brightness. Instead it represents some measure of distance from a camera to a surface. In Chapter 4, we distinguished between a range image and a depth image, and the difference was in the nature of the coordinate system. To be totally correct, we said, a range image is a collection of distances from a single point, the laser, to various points on the surface of interest, and hence takes the form r(θ, φ), where θ and φ are the pointing angles of the laser. That image can be converted to an image of the form z(x, y), which we called a depth image.

From here on, we won’t distinguish between depth images and range images. Instead we will refer to both as range images. This allows us some simplicity in discussion and agreement with most literature. So from here on, when you read “range,” know that it could be either measurement.

**A dense range image is** one in which, for every coordinate pair (x, y), there is a value of f given. In a dense range image the concept of neighbor makes sense (unless, of course, f is discontinuous).

**A sparse range image is** one in which f is only measured at a relatively few (x, y) points.

Finally, **a point cloud is** simply a set of triples {(x1, y1, z1), ...}. In a point cloud, neighborhood information is not implied, but it may be possible to compute which points are neighbors.

Frequently in literature the term “range image” means “dense range image.” So if it matters (and it usually does not), be careful in interpreting this particular term.

To repeat: a range image is the distance to a surface. We are measuring distances in 3-space, but that measurement stops when we encounter the surface. We do not look inside the object. If one had a sensor that could look inside the object, (e.g., computed tomography, positron emission tomography, magnetic resonance imaging), one could represent the object in the form d(x, y, z), where d denotes density or some other property of the material. Such images are common in medical imaging. However, we will not cover 3D images in this book.

## 12.2 Camera Geometry – Range from Two Known Cameras (Stereopsis)

In this section, we approach two issues: First we consider the camera, and relate points in the image (a 2-space) to the 3-space objects that are being imaged. Second, we find a transform that relates one image to another. Of course, we want to teach you about images and how they relate to the world, but we also want to teach you how to use several very important mathematical operations essential to Computer Vision. You will come to understand projective transformations and associated linear algebra, as well as how to minimize a quadratic function of a vector. That will involve a bit of matrix manipulation and differentiation.

First, let's consider projection.

### 12.2.1 Projections

We live in a 3-space: specifically a space with three spatial dimensions – we don't consider time as a dimension (here). From this 3-space, we have the ability to "project" information from the 3-space to any of an infinite set of two-dimensional spaces we call "pictures."

### Orthographic Projections

The first type of projection we could consider is called orthographic, and the simplest orthographic projection would be from some point in 3-space onto the z = 0 plane. Given a point [x, y, z]T in space, the orthographic projection onto the z = 0 plane is just [x, y]T. That's pretty simple, right? Of course, when you realize that all the points with the same x and y coordinates project to the same point on the camera plane, and, relative to the world, your camera is pretty small, you realize that the orthographic projection process could end up throwing away a lot of data.

Orthographic projection is commonly used in chest x-ray, where the image obtained from the film or sensing device is almost exactly the same size as the object being imaged. We won't do much with orthographic projections because they require extremely large focal planes. However, there is one case where we can think about such projections, and that is the case that the objects of interest are very small and a very long way from the camera (assuming a regular, projective camera model). In this case, the rays are nearly parallel, and the projection, at least the projection of the single, small object, is very nearly orthographic. In such a case, we might consider using orthographic projection because the math ends up being a bit easier.

However, let's go ahead and think about more realistic cameras. To understand cameras, recognize that there are two coordinate systems of interest, the world coordinate system that represents the camera in the world, and the camera coordinate system that represents the location of pixels on the focal plane of the camera. We usually use lower case bold symbols to represent points on the focal plane, and upper case bold symbols to represent points in space.

### Projections

The usual 3-space is referred to here as Euclidean space. We will do these mathematical operations in a higher-dimensional space, called "projective space." Projective 4-space is

![](img/5f95dd954ac63cc68119f6f48ca99e18_321_0.png)

Figure 12.1 The origin of the world coordinates is at the focal point, O. The origin of the focal plane is at the principal point. Note that the x axis of the focal plane is parallel to the X axis of the world, as is the y and Y. In this model of the projective camera, a point in space with coordinates (X, Y, Z) is projected onto a point on the image plane with coordinates (x, y). The camera origin, in turn, is related to the world origin by the projection matrix, which describes the camera, the position of the camera, and the direction of the camera.

a four-dimensional space of which conventional 3-space is a subspace. A point in 3-space relates to its corresponding point in projective 4-space by (for some scalar w)

```
\begin{bmatrix} X \\ Y \\ Z \\ \end{bmatrix} \Leftrightarrow \begin{bmatrix} Xw \\ Yw \\ Zw \\ w \\ \end{bmatrix} .
```

The mapping from 3- to 4-space is one-many, but two cases are especially interesting: If w = 1 we have the particularly simple case where the first three elements of the projective space representation are equal to the Euclidean representation. The other especially interesting case is the (infinite) set of points where w = 0. These are called “points at infinity.” One of the powers of the projective representation is the fact that infinitely-distant points may be conveniently represented. The use of a 3-vector augmented by a 1 is often referred to by the term “homogeneous coordinates,” as we saw in Chapter 10.

### 12.2.2 The Projective Camera

Most cameras can be modelled with a fairly simple model, the “projective camera,” which is illustrated in Figure 12.1. Some particular point in the world, X = [X Y Z 1]ᵀ, is projected onto the focal plane¹ by rays that pass through the imaging plane, and meet at the camera center, O, also referred to as the focal point. The ray from the focal point perpendicular to

¹ We will often refer to the focal plane as the imaging plane.
