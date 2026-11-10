GL_TRIANGLE_STRIP

![](bbox=[0.16, 0.13, 0.39, 0.21])

Each vertex that passes through the pipeline efficiently forms a triangle with the previous two vertices:

| vertices: | 0 | 1 | 2 | 3 | 4 | etc. |
|---|---|---|---|---|---|---|
| triangles: | | 0-1-2 | 2-3-4 | | | |

GL_TRIANGLE_FAN

![](bbox=[0.21, 0.26, 0.37, 0.35])

Each pair of vertices that passes through the pipeline forms a triangle with the very first vertex:

| vertices: | 0 | 1 | 2 | 3 | 4 | etc. |
|---|---|---|---|---|---|---|
| triangles: | | 0-1-2 | 0-2-3 | 0-3-4 | | |

GL_TRIANGLES_ADJACENCY

Intended only for use with geometry shaders. Allows the shader to access the vertices in the current triangle, plus additional adjacent vertices.

GL_TRIANGLE_STRIP_ADJACENCY

Intended only for use with geometry shaders. Similar to GL_TRIANGLES_ADJACENCY, except that triangle vertices overlap as for GL_TRIANGLE_STRIP.

# Line primitives:

GL_LINES

![](bbox=[0.16, 0.6, 0.39, 0.66])

Vertices that pass through the pipeline form distinct lines:

| vertices: | 0 | 1 | 2 | 3 | 4 | 5 | etc. |
|---|---|---|---|---|---|---|---|
| lines: | | 0-1 | 2-3 | 4-5 | | | |

GL_LINE_STRIP

![](bbox=[0.16, 0.7, 0.39, 0.76])

Each vertex that passes through the pipeline efficiently forms a line with the previous vertex:

| vertices: | 0 | 1 | 2 | 3 | etc. |
|---|---|---|---|---|---|
| lines: | | 0-1 | 1-2 | 2-3 | |

GL_LINE_LOOP

Same as GL_LINE_STRIP, except a line is also formed between the very first and very last vertices.