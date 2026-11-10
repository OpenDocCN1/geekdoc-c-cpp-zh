|  |  |  |
|---|---|---|
| lines_adjacency | GL_LINES_ADJACENCY, GL_LINE_STRIP_ADJACENCY | 4 |
| triangles | GL_TRIANGLES, GL_TRIANGLE_STRIP, GL_TRIANGLE_FAN | 3 |
| triangles_adjacency | GL_TRIANGLES_ADJACENCY, GL_TRIANGLE_STRIP_ADJACENCY | 6 |

The various OpenGL primitive types (including “strip” and “fan” types) were described in Chapter 4. “Adjacency” types were introduced in OpenGL for use with geometry shaders, and they allow access to vertices adjacent to the primitive. We don’t use them in this book, but they are listed for completeness.

The output primitive type must be *points*, *line_strip*, or *triangle_strip*. Note that the output layout qualifier also specifies the maximum number of vertices the shader outputs in each invocation.

This particular alteration to the torus could have been done more easily in the vertex shader. However, suppose that instead of moving each vertex outward along its own surface normal, we wished instead to move each *triangle* outward along its surface normal, in effect “exploding” the torus triangles outward. The vertex shader cannot do that, because computing a normal for the triangle requires averaging the vertex normals of all three triangle vertices, and the vertex shader only has access to the vertex attributes of one vertex in the triangle at a time. We can, however, do this in the geometry shader, because the geometry shader *does* have access to all three vertices in each triangle. We average their normals to compute a surface normal for the triangle, then add that averaged normal to each of the vertices in the triangle primitive. Figures 13.2, 13.3, and 13.4 show the averaging of the surface normals, the modified geometry shader `main()` code, and the resulting output respectively.

![](bbox=[0.257, 0.577, 0.743, 0.78])

**Figure 13.2**
Applying averaged triangle surface normal to triangle vertices.