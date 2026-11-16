```
glGenBuffers(1, &mVertexBuffer);

glBindBuffer(GL_ARRAY_BUFFER, mVertexBuffer);
```

The GL_ARRAY_BUFFER parameter to glBindBuffer means that you intend to use the buffer as a vertex buffer.

Once you have a vertex buffer, you need to copy the verts data passed into the VertexArray constructor into this vertex buffer. To copy the data, use glBufferData, which takes several parameters:

Click here to view code image

```
glBufferData(
    GL_ARRAY_BUFFER,    // The active buffer
    numVerts * 3 * sizeof(float), // Number of bytes t
    verts,    // Source to copy fr
    GL_STATIC_DRAW    // How will we use t
);
```

Note that you don't pass in the object ID to glBufferData; instead, you specify a currently bound buffer type to write to. In this case, GL_ARRAY_BUFFER means use the vertex buffer just created.

For the second parameter, you pass in the number of bytes, which is the amount of data for each vertex