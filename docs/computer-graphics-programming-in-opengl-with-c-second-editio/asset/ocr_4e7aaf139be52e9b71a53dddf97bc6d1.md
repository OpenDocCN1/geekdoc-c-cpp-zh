```
in display()
...
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, vbo[3]);
glDrawElements(GL_TRIANGLES, myTorus.getNumIndices(), GL_UNSIGNED_INT, 0);
```

Note in the code that uses the Torus class that the loop in setupVertices() now stores the data associated with each vertex once, rather than once for each index entry (as was the case in the sphere example). This difference is also reflected in the declared array sizes for the data being entered into the VBOs. Also note that in the torus example, rather than using the index values when retrieving vertex data, they are simply loaded into VBO #3. Since that VBO is designated as a GL_ELEMENT_ARRAY_BUFFER, OpenGL knows that that VBO contains vertex indices.

Figure 6.12 shows the result of instantiating a torus and texturing it with the brick texture.

![](bbox=[0.16, 0.44, 0.84, 0.66])

# 6.3 LOADING EXTERNALLY PRODUCED MODELS

Complex 3D models, such as characters found in videogames or computer-generated movies, are typically produced using modeling tools. Such “DCC” (digital content creation) tools make it possible for people (such as artists) to build arbitrary shapes in 3D space and automatically produce the vertices, texture coordinates, vertex normals, and so on. There are too many such tools to list, but some examples are Maya, Blender, Lightwave, Cinema4D, and many others. Blender is free and open source. Figure 6.13 shows an example Blender screen during the editing of a 3D model.