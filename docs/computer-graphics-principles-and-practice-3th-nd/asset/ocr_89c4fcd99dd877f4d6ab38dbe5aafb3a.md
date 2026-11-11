**Inline Exercise 25.5:** (a) Describe how to determine whether a mesh is connected (i.e., whether the graph consisting of all vertices and edges of the mesh is a connected graph).

(b) Apply the orientation algorithm to the five-vertex mesh of Inline Exercise 25.4 to show it's not orientable.

(c) Once we orient one face of an orientable connected mesh, all others have their orientations determined by the algorithm just described, so there are only two possible orientations of any connected orientable mesh. Suppose that some mesh *M* is not connected, and instead has *n* > 1 components. How many different orientations can it have?

The algorithm above can be slightly modified to compute the oriented mesh boundary: In the course of processing each face, if one of its edges is not part of a second face, we record that (oriented) edge as part of the oriented boundary.

Although we've described orientable meshes and an algorithm for determining an orientation (i.e., a consistent orientation for each face), in practice we usually encounter *oriented* meshes, or ones for which a particular orientation has already been chosen. When these meshes represent closed surfaces in 3-space, like a sphere or torus, the orientation of a face (i, j, k) is usually chosen so that if v_i is the vector from vertex i to vertex j, and v_j is the vector from vertex j to vertex k, then v_i × v_j points “outward,” that is, toward the unbounded portion of space.

![](bbox=[0.72, 0.458, 0.917, 0.568])

**Figure 25.7:** The point P is on the same side of the plane J as C, and therefore may be in the triangle ABC. If it passes corresponding tests for planes containing the edges BC and CA, we know it's in the triangle.

Current work in collision detection primarily uses oriented meshes, and often stores triangles as lists of edges (or along with lists of their edges). The reason has to do with speeding up certain tests that occur often, namely, point-in-triangle tests. If you have a point P in the plane of a triangle ABC in space, and you want to test whether it's actually within the triangle, you can do three “Is this point on the right side of this plane?” tests to answer the question. Here's how: Let's suppose that the plane of ABC is S. Consider any plane J that contains the edge AB and is not parallel to S (see Figure 25.7). The plane J can be characterized by a point Q on the plane and a normal vector **n**; the equation for J is then

(X − Q) · **n** = 0.    (25.1)

To determine whether P is on “the right side” of J, we can substitute C for X in Equation 25.1; the result will be nonzero. If it's negative, we'll replace **n** by −**n**, so we can assume that it's positive:

(C − Q) · **n** > 0.    (25.2)

Now that we've arranged for **n** to point in the proper direction, the test for P being on the right side of J becomes

(P − Q) · **n** > 0.    (25.3)

If we compute Q and **n** once, we can associate them to the edge AB and reuse them for every point-in-triangle test.