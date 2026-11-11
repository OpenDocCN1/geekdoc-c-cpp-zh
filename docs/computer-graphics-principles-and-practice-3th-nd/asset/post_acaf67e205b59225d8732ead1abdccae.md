
![](img/f464cd0043eb5336aa0543fe20a0561b_1117_0.png)

*Figure 37.2: During any time interval, a sphere moving with constant velocity traces the volume of a capsule. If the intersection of the capsule and the boxes is not empty during a time interval, a collision occurred during that interval.*

- The intersection of a ball¹ around a light source with a scene to determine which objects receive significant direct illumination from it
- The intersection of a ball with a set of stored incoming photon paths to estimate radiance in photon mapping

In the dynamics example of a scene with three boxes and a single moving sphere, it would be reasonable to compute the capsule at each time step and then iterate through all boxes testing for intersections with it. That strategy for collision detection would not scale to a scene with millions of geometric primitives. Informally, to scale well, we require an algorithm that can detect a collision in fewer than a linear number of operations in the number of primitives, *n*. We expect that using data structures such as trees can reduce the intersection-testing costs to O(log *n*) in the average case, for example. The best asymptotic time performance that an algorithm could exhibit in a nontrivial case is O(*m*) for *m* actual intersections, since the intersections themselves must be enumerated. This is achievable if we place spatial distribution constraints on the input; for example, accepting an upper bound on the spatial density of primitives [SHH99]. Note that even with such constraints, *m* = *n* in the worst case, so any spatial intersection query necessarily exhibits worst-case O(*n*) time complexity. Furthermore, obtaining optimal performance might require more storage space or algorithmic complexity than an implementation is able to support.

There is no “best” spatial data structure. Different data structures are appropriate for different data and queries. For example, finding capsule-box intersections in a scene with four primitives lends itself to a different data structure than ray-triangle intersections in a scene with millions of rays and triangles. This is the same principle.

1. A ball is the volume inside the sphere; technically, a geometric sphere S^k is the (k − 1) dimensional surface and not the k-dimensional volume within it. However, beware that intersections with balls are usually referred to as “sphere intersections” by most practitioners.

![](img/f464cd0043eb5336aa0543fe20a0561b_1119_0.png)

*Figure 37.3: (Left) The geometric intersection of a ball with a set of boxes in 2D. (Right) A conservative result that may be more efficient to compute.*

(Figure 37.3, left) or conservatively to return all primitives containing the intersection geometry (see Figure 37.3, right). The latter is important because the intersections between simple shapes may be hard to represent efficiently. For example, consider the intersection of a set of triangles with a ball about a point light. The intersection probably contains many triangles that are cut by the surface of the ball. The resultant shapes are not representable as triangles. However, the rendering system that will use this information likely operates on triangles, since that was the representation chosen for the underlying scene. Creating a representation for triangles-cut-by-curves will create complexity in the system that only results in shapes that the renderer can't directly process anyway. In this case, a conservative query that returns all triangles that intersect the ball is more useful than a precise query that returns the geometric intersection of the scene and the ball.

To make the structures useful, traditional set operations such as insert, remove, and is-member are generally provided along with geometric intersection. The algorithms for those tend to be straightforward applications of nonspatial data structure techniques. In contrast, the intersection queries depend on the geometry. They are the core of what makes *spatial* data structures unique, so we'll focus on those.

## 37.2.1 Intersection Methods

Some of the most common methods of spatial data structures are those that are used to find the intersection of a set of primitives with a ball (the solid interior bounded by a sphere), an axis-aligned box, and a ray. Listing 37.1 gives a sample C++ interface for these.

*Listing 37.1: Typical intersection methods on all spatial data structures.*

```cpp
template<class Value>
class SpatialDataStructure {
public:
    void getBallIntersection(const Ball& ball, std::vector<Value*>& result) const;
    void getAABBIntersection(const AABB& box, std::vector<Value*>& result) const;
    bool firstRayIntersection(const Ray& ray, Value*& value, float& distance) const;
};
```

Appending to, rather than overwriting, the array allows the caller more flexibility. If the caller requires overwrite behavior, then it can simply clear the array itself before invoking the query. Some tasks in which overwriting is undesirable are accumulating the results of several queries, and applying the same query to primitive sets stored in different data structures.

We assume `getBallIntersection` returns only primitives that overlap the ball. The primitives stored in the data structure may contain additional information that is unnecessary for the intersection computation, such as reflectivity data for rendering or a network connection for a distributed application like a multi-player game. They may also present different geometry to different subsystems. Thus, while a data structure may make conservative approximations for efficiency, it must ultimately query the primitive to determine exact intersections. Querying the primitives may be relatively expensive compared to the conservative approximations. An alternative interface to the ball intersection routine would return a conservative result of primitives that may overlap the ball, using only the conservative tests. This is useful, for example, if the caller intends to perform additional intersection tests on the result anyway.

Method `getAABBIntersection`,

```cpp
void getAABBIntersection(const AABB& box, std::vector<Value*>& result) const;
```

is similar to `getBallIntersection`. It finds all primitives in the data structure that overlap the interior of the axis-aligned box named box. Overlap tests against an axis-aligned box are often significantly faster than those performed against an arbitrarily oriented box, and the box itself can be represented very compactly.

The use of axis-aligned boxes is important for more than primitive intersections. For data structures such as the kd-tree and grid that contain spatial partitions aligned with the axes, the axis-aligned box intersection against internal nodes in a data structure may be particularly efficient and implemented with only one or two comparisons per axis.

Method `firstRayIntersection`,

```cpp
bool firstRayIntersection(const Ray& ray, Value*& value, float& distance) const;
```

tests for intersections between the primitive set and a ray (Figure 37.5). There are three possible results.

1. There is no intersection. The method returns false and the referenced parameters are unmodified.
2. The intersection closest to the ray origin is at distance r and r ≥ distance. The method returns false and the referenced parameters are unmodified.

![](img/f464cd0043eb5336aa0543fe20a0561b_1121_0.png)

*Figure 37.5: (Left) The geometric intersection I of a 2D query ray Q with box B. (Right) The point F that we call the first intersection between the ray and box, that is, the point on the geometric intersection that is closest to the ray origin.*

For ray-triangle intersection, `firstRayIntersection` is often extended to return the barycentric coordinates of the intersection location on the triangle hit. As described in Section 9.2, these three weights are sufficient to reconstruct both the location on the triangle where the ray first intersects it and any shading parameters interpolated from the vertices of the triangle. Returning the barycentric coordinates is not necessary because, given the distance along the ray to the intersection, the caller could reconstruct them. However, they are naturally computed during the intersection computation, so it is efficient and convenient to pass them back to the caller rather than imposing the cost of recomputing them outside the query operation.

Some data structures can resolve the query of whether *any* intersection exists for `r < distance` faster than they can find the *closest* one. This is useful for shadow and ambient occlusion ray casting. In that case a method variant that takes no value parameter and does not update distance is a useful extension.

## 37.2.2 Extracting Keys and Bounds

💠 We want to be able to make data structures that can be instantiated for different kinds of primitives. For example, a tree of triangles and a tree of boxes should share an implementation. This notion of the tree template as separate from a specific type of tree is called **polymorphism**. It is something that you are probably very familiar with from classic data structures. For example, `std::vector<int>` and `std::vector<std::string>` share an implementation but are specialized for different value types.

For spatial data structures, we therefore require some polymorphic interface both for each data structure and for extracting a key from each value. The choice of interface depends on the implementation language and the needs of the surrounding program.

### 37.2.2.1 Inheritance

In an object-oriented language such as Java, one typically uses inheritance to extract keys, as shown in Listings 37.3 and 37.4 (the latter listing has the example).

*Listing 37.3: A Java inheritance interface for expressing axis-aligned bounding box, sphere, and point keys on a primitive and responding to corresponding conservative intersection queries.*

```java
public interface Primitive {
    /** Returns a box that surrounds the primitive for use in
        building spatial data structures. */
    public void getBoxBounds(AABB bounds);

    public void getSphereBounds(Sphere bounds);

    public void getPosition(Point3 pos);

    /** Returns true if the primitive overlaps a box for use
        in responding to spatial queries. */
    public boolean intersectsBox(AABB box);

    public boolean intersectsBall(Ball ball);
```
