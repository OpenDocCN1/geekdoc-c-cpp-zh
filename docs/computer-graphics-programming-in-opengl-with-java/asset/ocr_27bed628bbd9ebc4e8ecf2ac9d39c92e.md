```
```cpp
    // set up buffer containing vertices
    gl.glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
    gl.glVertexAttribPointer(0, 3, GL_FLOAT, false, 0, 0);
    gl.glEnableVertexAttribArray(0);

    // set up buffer containing texture coordinates
    gl.glBindBuffer(GL_ARRAY_BUFFER, vbo[1]);
    gl.glVertexAttribPointer(1, 2, GL_FLOAT, false, 0, 0);
    gl.glEnableVertexAttribArray(1);

    // activate the skybox texture
    gl.glActiveTexture(GL_TEXTURE0);
    gl.glBindTexture(GL_TEXTURE_2D, skyboxTexture);
    gl.glEnable(GL_CULL_FACE);
    gl.glFrontFace(GL_CCW);        // cube has CW winding order, but we are viewing its interior
    gl.glDisable(GL_DEPTH_TEST);
    gl.glDrawArrays(GL_TRIANGLES, 0, 36);  // draw the skybox without depth testing
    gl.glEnable(GL_DEPTH_TEST);

    // now draw desired scene objects as before
    ...
    gl.glDrawElements(...);        // as before for scene objects

}

private void setupVertices()
{  // cube_vertices defined same as before
   // cube texture coordinates for the skybox as they appear in Figure 9.3
   float[] cubeTextureCoord =
   {  1.00f, 0.66f, 1.00f, 0.33f, 0.75f, 0.33f,    // back face lower right
      0.75f, 0.33f, 0.75f, 0.66f, 1.00f, 0.66f,    // back face upper left
      0.75f, 0.33f, 0.50f, 0.33f, 0.75f, 0.66f,    // right face lower right
      0.50f, 0.33f, 0.50f, 0.66f, 0.75f, 0.66f,    // right face upper left
      0.50f, 0.33f, 0.25f, 0.33f, 0.50f, 0.66f,    // front face lower right
      0.25f, 0.33f, 0.25f, 0.66f, 0.50f, 0.66f,    // front face upper left
      0.25f, 0.33f, 0.00f, 0.33f, 0.25f, 0.66f,    // left face lower right
      0.00f, 0.33f, 0.00f, 0.66f, 0.25f, 0.66f,    // left face upper left
      0.25f, 0.33f, 0.50f, 0.33f, 0.50f, 0.00f,    // bottom face upper right
      0.50f, 0.00f, 0.25f, 0.00f, 0.25f, 0.33f,    // bottom face lower left
      0.25f, 1.00f, 0.50f, 1.00f, 0.50f, 0.66f,    // top face upper right
      0.50f, 0.66f, 0.25f, 0.66f, 0.25f, 1.00f     // top face lower left
   };

   // set up buffers for cube and scene objects as usual
}
// modules for loading shaders, textures, etc. as before
}
```
```