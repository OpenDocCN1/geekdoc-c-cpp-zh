Let’s proceed by adding a simple pyramid, so our scene includes both a single cube and a pyramid. The code is shown in Program 4.3. A few of the key details are highlighted, such as where we specify one or the other buffer and where we specify the number of vertices contained in the model. Note that the pyramid is composed of six triangles—four on the sides and two on the bottom, totaling 6×3=18 vertices.

The resulting scene, containing both the cube and the pyramid, is shown in Figure 4.10.

# Program 4.3 Cube and Pyramid

```
```java
private void setupVertices()
{
    GL4 gl = (GL4) GLContext.getCurrentGL();

    float[] cubePositions =
    { -1.0f,  1.0f, -1.0f, -1.0f, -1.0f,  1.0f, -1.0f,
       1.0f, -1.0f, -1.0f,  1.0f, -1.0f, -1.0f,
       ... same as before, for the rest of the cube vertices
    };

    // pyramid with 18 vertices, comprising 6 triangles (four sides, and two on the bottom)
    float[] pyramidPositions =
    {
       -1.0f, -1.0f,  1.0f,  1.0f, -1.0f,  1.0f,  0.0f, 0.0f,       // front face
        1.0f, -1.0f,  1.0f,  1.0f, -1.0f, -1.0f,  0.0f, 1.0f,       // right face
        1.0f, -1.0f, -1.0f, -1.0f, -1.0f, -1.0f,  0.0f, 1.0f,       // back face
       -1.0f, -1.0f, -1.0f, -1.0f, -1.0f,  1.0f,  0.0f, 0.0f,       // left face
       -1.0f, -1.0f,  1.0f,  1.0f, -1.0f,  1.0f, -1.0f, -1.0f, 1.0f, // base – left front
        1.0f, -1.0f,  1.0f, -1.0f, -1.0f, -1.0f,  1.0f, -1.0f, 1.0f, // base – right back
    };
    gl.glGenVertexArrays(vao.length, vao, 0);
    gl.glBindVertexArray(vao[0]);
    gl.glGenBuffers(vbo.length, vbo, 0);

    gl.glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
    FloatBuffer cubeBuf = Buffers.newDirectFloatBuffer(cubePositions);
    gl.glBufferData(GL_ARRAY_BUFFER, cubeBuf.limit()*4, cubeBuf, GL_STATIC_DRAW);

    gl.glBindBuffer(GL_ARRAY_BUFFER, vbo[1]);
    FloatBuffer pyrBuf = Buffers.newDirectFloatBuffer(pyramidPositions);
    gl.glBufferData(GL_ARRAY_BUFFER, pyrBuf.limit()*4, pyrBuf, GL_STATIC_DRAW);
}

public void display(GLAutoDrawable drawable)
{  . . . clear the color and depth buffers as before (not shown here)
```
```