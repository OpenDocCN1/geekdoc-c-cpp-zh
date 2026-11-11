
storing redundant information for all the edges with two adjacent faces. A common trick obfuscates the code a bit by eliminating this storage overhead. The trick is to store only one half-edge for each mesh edge, and to index from a face using two’s complement when the half-edge is oriented opposite the direction that it should appear in that face. The two’s complement of a non-negative index *e* (written *-e* in C-like languages) is guaranteed to be a negative number, so indices of oppositely directed edges are easy to identify. The two’s complement operator is efficient on most architectures, so it incurs little overhead. Each edge then uses the same trick to encode the indices of the adjacent faces, indicating whether that half-edge or its oppositely directed mate actually appears in the face.

*Listing 14.4: Sample mesh representation with full adjacency information.*

```cpp
struct Mesh {
    enum { NO_FACE = MAX_INT };

    struct Vertex {
        Point3          location;
        std::vector<int> edges;
        std::vector<int> faces;
    };

    struct Edge {
        int             vertices[2];
        /* May be NO_FACE if this edge is on a boundary. */
        int             faces[2];
    };

    struct Face {
        int             vertices[3];
        int             edges[3];
    };

    std::vector<int>    index;
    std::vector<Vertex> vertex;
    std::vector<Edge>   edge;
    std::vector<Face>   face;
};
```

### 14.5.1.4 Per-Vertex Properties

It is common to label the vertices of a mesh with additional information. Common rendering properties include **shading normals, texture coordinates, and tangent-space bases**.

A polygonal approximation of a curved surface appears faceted. The perception of faceting can be greatly reduced by shading the *points* indicated by the surface geometry, but altering the orientation of their tangent plane during illumination computations, as you saw in Chapter 6. It is common to model the orientation by specifying the desired surface normal at each vertex and interpolating between those normals within the surface of each polygon.

**Texture coordinates** are the additional *points* or vectors specified at each vertex to create a mapping from the surface of the model to a texture space that defines material properties, such as reflectance spectrum (“color”). Mapping from the surface to a 2D square using 2D points is perhaps the most common, but mappings to 1D spaces, 3D volumetric spaces, and the 2D surface of a 3D sphere are also common; Chapter 20 discusses this in detail. The last is sometimes called cube mapping, sphere mapping, or environment mapping depending on the specific parameterization and application.

A tangent space is just a plane that is tangent to a surface at a point. A mesh’s tangent space is undefined at edges and vertices. However, when the mesh has vertex normals there is an implied tangent space (the plane perpendicular to the vertex normal) at each vertex. The interpolated normals across faces (and edges) similarly imply tangent spaces at every point on the mesh. Many rendering algorithms depend on the orientation of a surface within its tangent plane. For example, a hair-rendering algorithm that models the hair as a solid “helmet” needs to know the orientation of the hair (i.e., which way it was combed) at every point on the surface. A **tangent-space basis** is one way to specify the orientation; it is simply a pair of linearly independent (and usually orthogonal and unit-length) vectors in the tangent plane. These can be interpolated across the surface of the mesh in the same way that shading normals are; of course, they may cease to be orthogonal and change length as they are interpolated, so it may be necessary to renormalize or even change their direction after interpolation to achieve the goals of a particular algorithm. Finding such a pair of vectors at every point of a closed surface is not always possible, as described in Chapter 25.

### 14.5.1.5 Cached and Precomputed Information on the Mesh

The preceding section described properties that extend the mesh representation with additional per-vertex information. It is also common to precompute properties of the mesh and store them at vertices to speed later computation, such as curvature information (and the adjacency information that we have already seen). One can even evaluate arbitrary, expensive functions and then approximate their value at points within the mesh (or even within the volume contained by the mesh) by barycentric interpolation.

Gouraud shading is an example. We compute and store direct illumination at vertices during the rendering of a frame, and interpolate these stored values across the interior of each face. This was once common practice for all rasterization renderers. Today it is primarily used only on renderers for which the triangles are small compared to pixels so that there is no loss of shading resolution from the interpolation. The **micropolygon** renderers popular in the film industry use this method, but they ensure that vertices are sufficiently dense in screen space by subdividing large polygons during rendering until each is smaller than a pixel [CC87]. Per-pixel direct illumination is now considered sufficiently inexpensive because processor performance has grown faster than screen resolutions. However, it has not grown faster than scene complexity, so some algorithms still compute **global** illumination terms such as ambient occlusion (an estimated reduction in brightness due to nearby geometry) or diffuse interreflection at vertices [Bun05].

The vertices of a mesh form a natural data structure for recording values that describe a piecewise linear approximation of an arbitrary function as described in Chapter 9. The drawback of this approach is that other constraints on the modeling process may lead to a tessellation that is not ideal for representing the arbitrary function. For example, many meshes are created by artists with the goal of using the fewest triangles possible to reasonably approximate the silhouette of an object. Large, flat areas of the mesh will therefore contain few triangles. If we were to compute global illumination only at the vertices, we would find that the illumination computation became extremely blurry in these areas simply because the model had too few vertices.

- There are two common solutions to this problem, other than simply increasing the tessellation everywhere. The first is to subdivide triangles of the mesh during computation of the function that is to be stored at vertices [Hec90], until the approximation error across each triangle is small enough. The second is to define an invertible and approximately conformal mapping from the surface of the mesh into texture space, and encode the function values in a texture map. The latter is more efficient for functions with high variance where it is hard to predict the locations where changes occur a priori. Today this approach is more popular than the per-vertex computation. For example, many games rely on **light maps**, which store precomputed global illumination for static scenes in textures. Combined with real-time direct illumination, these provide a reasonable approximation of true global illumination if few objects move within the scene. Traditional light maps encoded only the magnitude, but not direction, of incident light at a surface. This has since been extended to encode directionality in various bases [PRT, AtiHL2]. **Texture-space diffusion**, as seen in d’Eon et al.’s subsurface scattering work [dLE07], is an example of dynamic data encoded in texture space.

## 14.5.2 Implicit Surfaces

Some geometric primitives are conveniently described by simple equations and correspond closely to shapes we encounter in the world around us. In 2D, these include lines, line segments, arcs of ellipses (including full circles), rectangles, trigonometric expressions such as sine waves, and low-order polynomial curves. In 3D, these include spheres, cylinders, boxes, planes, trigonometric expressions, quadrics, and other low-order polynomial surfaces.

Simple primitives can be represented via implicit equations or explicit parametric equations, as described in Chapter 7. We’ll recall some of those ideas briefly here.

An implicit equation is a test function \(f : \mathbb{R}^3 \to \mathbb{R}\) that can be applied to a point. The function classifies points in space: For any point \(P\), either \(f(P) > 0\), \(f(P) < 0\), or \(f(P) = 0\). Those with \(f(P) = 0\) are said to constitute the **implicit surface** defined by \(f\); by convention, those with \(f(P) < 0\) are said to be inside the surface, and the remainder are outside. Such a surface is an instance of a **level set** (for level 0) and an **isocontour** (for value 0) of the function.

As an example, consider a surface defined by the plane through point \(Q\) with normal \(\mathbf{n}\). A suitable test function is

\[f : \mathbb{R}^3 \to \mathbb{R} : P \mapsto (P-Q) \cdot \mathbf{n}.\tag{14.3}\]

For every point \(P\) in the plane, \(f(P) = 0\). For points on the side containing \(Q + \mathbf{n}\), \(f(P) > 0\); for points on the other side, \(f(P) < 0\).

An **explicit equation** or **parametric equation** defines a generator function for points in the plane in terms of scalar parameters. We can use such a function to synthesize points on the surface. The explicit form for a plane is

\[g : \mathbb{R} \times \mathbb{R} \to \mathbb{R}^3 : (u, v) \mapsto u\mathbf{h} + v\mathbf{k} + Q,\tag{14.4}\]

where \(\mathbf{h}\) and \(\mathbf{k}\) are two vectors in the plane that are linearly independent. For any particular pair of numbers \(u\) and \(v\), the point \(g(u, v)\) lies on the plane. Chapter 7
