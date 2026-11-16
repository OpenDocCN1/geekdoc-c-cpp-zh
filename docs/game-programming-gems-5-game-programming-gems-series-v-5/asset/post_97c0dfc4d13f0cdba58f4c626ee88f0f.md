
## Improved Frustum Culling

**Frank Puig Placeres**

fpuig2003@yahoo.com

A typical game scene generally consists of many objects, which if not managed appropriately may hinder rendering performance. Libraries such as OpenGL and DirectX do some geometry management by clipping polygons that are partially off-screen and early rejecting those that are completely out of view from further processing. To perform the clip, however, each vertex in a polygon must go through the library pipeline, be transformed to screen coordinates, and be checked with the active viewport. When the polygon count is low, this process does the job, but when rendering many objects consisting of many hundreds (or thousands) of polygons, the high cost of transmitting and processing all the vertices quickly overloads the system. A higher-level per-object culling algorithm must be implemented to effectively manage rendering a typical scene. This gem describes a clever improvement to an already well-known scene-management technique: view frustum culling.

### Frustum Culling

Frustum Culling works by defining a volume that wraps the space that is currently visible from a given point of view. As shown in Figure 1.6.1, that view volume is built by constructing a pyramid with the apex at the eye’s position and the four triangular faces aligned with the screen borders. Two parallel planes, the near- and far- clipping planes, slice this pyramid; nothing closer than the screen or farther than some predefined distance will be included in the view volume. The resulting volume is known in mathematics as a frustum, and the objects that are completely outside of this volume have no chance to be seen by the camera and may be rejected on a per-object level. Once the frustum is built, objects can be tested against it for visibility. Each object in the scene may be completely enclosed by a bounding primitive, such as a sphere, cube, cylinder, or cone, which is used to test against the frustum rather than using the object itself. This avoids the overhead of duplicating the work already in the rendering pipeline and allows a higher-level of efficiency than per-polygon culling. If

![](img/672fe9a2d008ba627b1991e15d70f43e_107_0.png)

FIGURE 1.6.1 The geometrical object that bounds the visible section of the world is called a frustum.

the simple bounding primitive falls completely outside the frustum, the entire object (or objects) it contains may be rejected. The key is to use shapes that can be quickly tested against the frustum, so the most commonly used primitives are spheres and axis-aligned bounding boxes.

### The Traditional Six Planes Approach

The most common representation of the frustum itself is six simple planes, which are extracted from the matrix composed of a concatenation of the model view and projection matrices, as shown in Figure 1.6.2. Each plane divides the space into two halves; the intersection of all the planes shapes a volume that defines what the camera sees.

Working with the six planes approach has some disadvantages, the first of which is processing expense. Determining whether a point falls inside the frustum means evaluating an equation for each plane. Only if the result is positive for every plane evaluation may the point in question be determined to fall within the frustum. A second drawback to this approach is that it is not so easy to extract the frustum's position and orientation, making operations such as an update quite difficult. This drawback is the reason why almost all implementations recreate the frustum every time the camera updates, which imposes a bit of overhead in the form of unnecessary floating-point operations (includes divides and square roots) as the six planes shaping the frustum are reconstructed [Morley00].

![](img/672fe9a2d008ba627b1991e15d70f43e_108_0.png)

FIGURE 1.6.2 The six planes that define a frustum.

### The Radar Approach

This algorithm was first designed for a two-dimensional radar system. The only intended purpose was to show the objects covered by a radar wave by leaving out those objects that were not covered. The approach proved to be very fast if some bounding primitives were inside the view, and the method was quickly extended to work in three dimensions. Now, the algorithm has been used for frustum culling with incredible results.

To describe how the radar approach works in a friendly way, let's first go back and introduce the two-dimensional algorithm and then extend it to the three-dimensional world.

When working on a system with two dimensions, a frustum becomes a triangle, and as a frustum is a symmetric object, the triangle is known to be isosceles as is shown in Figure 1.6.3. The segment that starts in the apex and is perpendicular to the base is called in mathematics the triangle height. The handy part of the height is that as the frustum is symmetric, it splits the isosceles triangle into two equal halves. Coincidentally, the height happens to be directionally parallel to the camera's forward vector.

Using the radar approach, a frustum is defined to be as intuitive as the camera, so frustum construction is almost free. The two-dimensional radar only needs to know the field-of-view angle (FOV), the forward vector, and the right vector. Conveniently enough, these are the same three parameters that the camera uses, so they can be extracted directly from the camera. The radar implementation does not, however, use the FOV

![](img/672fe9a2d008ba627b1991e15d70f43e_109_0.png)

FIGURE 1.6.3 A two dimensional frustum is represented as an isosceles triangle where the height matches the forward vector.

directly but the tangent of that angle; so that is the only thing that must be computed when building the frustum. Even that, though, can be cached and only computed when the camera changes the FOV (which, in most games, only occurs when a zoom is performed, changing the perspective. While that angle remains unchanged, the frustum is built by copying the forward and right vectors directly from the camera. This is far cheaper than performing all the calculations required to build a frustum using the six planes approach. And now, let's go to the really interesting part: knowing if something is inside the frustum.

### Is a Point Inside a Frustum?

First, let's see what we need for knowing if a given point is inside the frustum; check Figure 1.6.4. To know if the point P is in the frustum, the radar approach projects OP to the forward and right vectors. The point P is known to be in the frustum if the forward projection F is between the far and near values and the right projection R is between rLimit and -rLimit; otherwise, it is meant to be completely out.

As described earlier, the first thing that must be done is to compute the projections F and R. To project one vector into another, a dot product is performed and the resulting scalar is multiplied by either of the two vectors to obtain the projection in the desired axis. Figure 1.6.5 illustrates. There are two vectors V1 and V2, and the dot product of them returns a scalar s.

```
s = V1 dot V2 = V1 • V2 = V2.x * V1.x + V2.y * V1.y
```

![](img/672fe9a2d008ba627b1991e15d70f43e_110_0.png)

FIGURE 1.6.4 Classifying a point against a frustum.

![](img/672fe9a2d008ba627b1991e15d70f43e_110_1.png)

FIGURE 1.6.5 Projection of one vector into another.

The projection of V1 in V2 is V2 * s with the condition that V2 be of length 1.
Using the previous equation and considering that the forward and right vectors
are unitary, it is possible to compute the values F and R by performing:

f = Forward • OP And r = Right • OP

If the condition (near <= f <= far) is not true, the point is out of the frustum. Check the
first part of the code:

```
bool cFrustum::IsPointIn( const cVector2f& Point )
{
    cVector2f OP = Point - EyePosition;
    float f = OP * ForwardVector; // OP dot ForwardVector
    if ( f < NearZ || far < f) return false;
    float r = OP * RightVector; // OP dot RightVector
    float rLimit = rFactor * f;
    if ( r < -rLimit || rLimit < r) return false;
    // Up to here the point is known to be in the frustum
    return true;
}
```

Computing rLimit is trickier and involves the FOV tangent. The FOV tangent,
called the rFactor, was discussed previously and is computed as follows (see Figure 1.6.6).
