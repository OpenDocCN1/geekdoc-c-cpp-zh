![](bbox=[0.137, 0.108, 0.607, 0.291])

Figure 13.4: The distances to the near and far planes are measured along the look direction.

![](bbox=[0.159, 0.338, 0.572, 0.474])

Figure 13.5: Objects outside the view frustum will not be rendered.

It is not only the utility of being able to set the near- and far-plane distances that motivates their use, as you’ll see presently; they also allow a rasterizing renderer to avoid certain floating-point-comparison problems that generate errors in images.

Clipping planes have often been used in games to help reduce rendering time by removing distant objects, but sometimes as you move forward in a game, a distant object will “pop” into view, which can be distracting. The general solution to this problem was to render objects in the distance as being obscured by fog so that they appeared gradually as you approached them. In more modern games, we have better rendering systems, and many objects are represented with multiple different levels of detail (see Section 25.4) so that when they are distant, they can be rendered with fewer polygons, making the use of fog less common than it once was.

# 13.4 Building Transformations from a View Specification

We’ll now convert from a view specification to some specific geometry. From a specification, we’ll build (a) an orthonormal coordinate system based at the camera position, and (b) several points on the view cone, as shown in Figure 13.6. We’ll use these in building the transformations we need. Having a coordinate frame based at the camera is very convenient, since we’ll later be transforming the camera to the origin and aligning its coordinate frame with the standard *xyz*-coordinate system at the origin.